---
title: Working with dates in Azure Cosmos DB | Microsoft Docs
description: Learn about how to work with dates in Azure Cosmos DB.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 05/25/2017
ms.author: sngun
ms.openlocfilehash: d7188270ff5b1edd3b5e396be0cd5fd22e6123c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865924"
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="287e2-103">Working with Dates in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="287e2-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="287e2-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span><span class="sxs-lookup"><span data-stu-id="287e2-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="287e2-105">All Azure Cosmos DB resources including databases, containers, documents, and stored procedures are modeled and stored as JSON documents.</span><span class="sxs-lookup"><span data-stu-id="287e2-105">All Azure Cosmos DB resources including databases, containers, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="287e2-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span><span class="sxs-lookup"><span data-stu-id="287e2-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="287e2-107">However, JSON is flexible and allow developers and frameworks to represent more complex types using these primitives and composing them as objects or arrays.</span><span class="sxs-lookup"><span data-stu-id="287e2-107">However, JSON is flexible and allow developers and frameworks to represent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="287e2-108">In addition to the basic types, many applications need the [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type to represent dates and timestamps.</span><span class="sxs-lookup"><span data-stu-id="287e2-108">In addition to the basic types, many applications need the [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type to represent dates and timestamps.</span></span> <span data-ttu-id="287e2-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="287e2-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using the .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="287e2-110">Storing DateTimes</span><span class="sxs-lookup"><span data-stu-id="287e2-110">Storing DateTimes</span></span>
<span data-ttu-id="287e2-111">By default, the [Azure Cosmos DB SDK](sql-api-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span><span class="sxs-lookup"><span data-stu-id="287e2-111">By default, the [Azure Cosmos DB SDK](sql-api-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="287e2-112">Most applications can use the default string representation for DateTime for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="287e2-112">Most applications can use the default string representation for DateTime for the following reasons:</span></span>

* <span data-ttu-id="287e2-113">Strings can be compared, and the relative ordering of the DateTime values is preserved when they are transformed to strings.</span><span class="sxs-lookup"><span data-stu-id="287e2-113">Strings can be compared, and the relative ordering of the DateTime values is preserved when they are transformed to strings.</span></span> 
* <span data-ttu-id="287e2-114">This approach doesn't require any custom code or attributes for JSON conversion.</span><span class="sxs-lookup"><span data-stu-id="287e2-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="287e2-115">The dates as stored in JSON are human readable.</span><span class="sxs-lookup"><span data-stu-id="287e2-115">The dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="287e2-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span><span class="sxs-lookup"><span data-stu-id="287e2-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="287e2-117">For example, the following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using the .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="287e2-117">For example, the following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using the .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="287e2-118">This document is stored in Azure Cosmos DB as follows:</span><span class="sxs-lookup"><span data-stu-id="287e2-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="287e2-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing the number of elapsed seconds since January 1, 1970.</span><span class="sxs-lookup"><span data-stu-id="287e2-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing the number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="287e2-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span><span class="sxs-lookup"><span data-stu-id="287e2-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="287e2-121">You can use the [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class to serialize DateTimes as numbers.</span><span class="sxs-lookup"><span data-stu-id="287e2-121">You can use the [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class to serialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="287e2-122">Indexing DateTimes for range queries</span><span class="sxs-lookup"><span data-stu-id="287e2-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="287e2-123">Range queries are common with DateTime values.</span><span class="sxs-lookup"><span data-stu-id="287e2-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="287e2-124">For example, if you need to find all orders created since yesterday, or find all orders shipped in the last five minutes, you need to perform range queries.</span><span class="sxs-lookup"><span data-stu-id="287e2-124">For example, if you need to find all orders created since yesterday, or find all orders shipped in the last five minutes, you need to perform range queries.</span></span> <span data-ttu-id="287e2-125">To execute these queries efficiently, you must configure your collection for Range indexing on strings.</span><span class="sxs-lookup"><span data-stu-id="287e2-125">To execute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="287e2-126">You can learn more about how to configure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="287e2-126">You can learn more about how to configure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="287e2-127">Querying DateTimes in LINQ</span><span class="sxs-lookup"><span data-stu-id="287e2-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="287e2-128">The SQL .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span><span class="sxs-lookup"><span data-stu-id="287e2-128">The SQL .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="287e2-129">For example, the following snippet shows a LINQ query that filters orders that were shipped in the last three days.</span><span class="sxs-lookup"><span data-stu-id="287e2-129">For example, the following snippet shows a LINQ query that filters orders that were shipped in the last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated to the following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="287e2-130">You can learn more about Azure Cosmos DB's SQL query language and the LINQ provider at [Querying Cosmos DB](sql-api-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="287e2-130">You can learn more about Azure Cosmos DB's SQL query language and the LINQ provider at [Querying Cosmos DB](sql-api-sql-query.md).</span></span>

<span data-ttu-id="287e2-131">In this article, we looked at how to store, index, and query DateTimes in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="287e2-131">In this article, we looked at how to store, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="287e2-132">Next Steps</span><span class="sxs-lookup"><span data-stu-id="287e2-132">Next Steps</span></span>
* <span data-ttu-id="287e2-133">Download and run the [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="287e2-133">Download and run the [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="287e2-134">Learn more about [SQL queries](sql-api-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="287e2-134">Learn more about [SQL queries](sql-api-sql-query.md)</span></span>
* <span data-ttu-id="287e2-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="287e2-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
