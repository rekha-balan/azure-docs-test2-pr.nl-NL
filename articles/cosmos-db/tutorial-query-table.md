---
title: How to query table data in Azure Cosmos DB? | Microsoft Docs
description: Learn to query table data in Azure Cosmos DB
services: cosmos-db
author: kanshiG
manager: kfile
editor: ''
tags: ''
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: na
ms.topic: tutorial
ms.date: 11/15/2017
ms.author: govindk
ms.custom: mvc
ms.openlocfilehash: 8a629a7b1340547f43919a1e88abbda53e9e2ae0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870177"
---
# <a name="tutorial-query-azure-cosmos-db-by-using-the-table-api"></a><span data-ttu-id="609d3-104">Tutorial: Query Azure Cosmos DB by using the Table API</span><span class="sxs-lookup"><span data-stu-id="609d3-104">Tutorial: Query Azure Cosmos DB by using the Table API</span></span>

<span data-ttu-id="609d3-105">The Azure Cosmos DB [Table API](table-introduction.md) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span><span class="sxs-lookup"><span data-stu-id="609d3-105">The Azure Cosmos DB [Table API](table-introduction.md) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="609d3-106">This article covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="609d3-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="609d3-107">Querying data with the Table API</span><span class="sxs-lookup"><span data-stu-id="609d3-107">Querying data with the Table API</span></span>

<span data-ttu-id="609d3-108">The queries in this article use the following sample `People` table:</span><span class="sxs-lookup"><span data-stu-id="609d3-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="609d3-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="609d3-109">PartitionKey</span></span> | <span data-ttu-id="609d3-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="609d3-110">RowKey</span></span> | <span data-ttu-id="609d3-111">Email</span><span class="sxs-lookup"><span data-stu-id="609d3-111">Email</span></span> | <span data-ttu-id="609d3-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="609d3-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="609d3-113">Harp</span><span class="sxs-lookup"><span data-stu-id="609d3-113">Harp</span></span> | <span data-ttu-id="609d3-114">Walter</span><span class="sxs-lookup"><span data-stu-id="609d3-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="609d3-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="609d3-115">425-555-0101</span></span> |
| <span data-ttu-id="609d3-116">Smith</span><span class="sxs-lookup"><span data-stu-id="609d3-116">Smith</span></span> | <span data-ttu-id="609d3-117">Ben</span><span class="sxs-lookup"><span data-stu-id="609d3-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="609d3-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="609d3-118">425-555-0102</span></span> |
| <span data-ttu-id="609d3-119">Smith</span><span class="sxs-lookup"><span data-stu-id="609d3-119">Smith</span></span> | <span data-ttu-id="609d3-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="609d3-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="609d3-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="609d3-121">425-555-0104</span></span> | 

<span data-ttu-id="609d3-122">See [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span><span class="sxs-lookup"><span data-stu-id="609d3-122">See [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="609d3-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="609d3-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="609d3-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="609d3-124">Prerequisites</span></span>

<span data-ttu-id="609d3-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span><span class="sxs-lookup"><span data-stu-id="609d3-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="609d3-126">Don't have any of those?</span><span class="sxs-lookup"><span data-stu-id="609d3-126">Don't have any of those?</span></span> <span data-ttu-id="609d3-127">Complete the [five-minute quickstart](create-table-dotnet.md) or the [developer tutorial](tutorial-develop-table-dotnet.md) to create an account and populate your database.</span><span class="sxs-lookup"><span data-stu-id="609d3-127">Complete the [five-minute quickstart](create-table-dotnet.md) or the [developer tutorial](tutorial-develop-table-dotnet.md) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="609d3-128">Query on PartitionKey and RowKey</span><span class="sxs-lookup"><span data-stu-id="609d3-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="609d3-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span><span class="sxs-lookup"><span data-stu-id="609d3-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="609d3-130">**Query**</span><span class="sxs-lookup"><span data-stu-id="609d3-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="609d3-131">**Results**</span><span class="sxs-lookup"><span data-stu-id="609d3-131">**Results**</span></span>

| <span data-ttu-id="609d3-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="609d3-132">PartitionKey</span></span> | <span data-ttu-id="609d3-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="609d3-133">RowKey</span></span> | <span data-ttu-id="609d3-134">Email</span><span class="sxs-lookup"><span data-stu-id="609d3-134">Email</span></span> | <span data-ttu-id="609d3-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="609d3-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="609d3-136">Harp</span><span class="sxs-lookup"><span data-stu-id="609d3-136">Harp</span></span> | <span data-ttu-id="609d3-137">Walter</span><span class="sxs-lookup"><span data-stu-id="609d3-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="609d3-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="609d3-138">425-555-0104</span></span> |

<span data-ttu-id="609d3-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span><span class="sxs-lookup"><span data-stu-id="609d3-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="609d3-140">Note that the key property names and constant values are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="609d3-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="609d3-141">Both the PartitionKey and RowKey properties are of type String.</span><span class="sxs-lookup"><span data-stu-id="609d3-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="609d3-142">Query by using an OData filter</span><span class="sxs-lookup"><span data-stu-id="609d3-142">Query by using an OData filter</span></span>
<span data-ttu-id="609d3-143">When you're constructing a filter string, keep these rules in mind:</span><span class="sxs-lookup"><span data-stu-id="609d3-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="609d3-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span><span class="sxs-lookup"><span data-stu-id="609d3-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="609d3-145">Note that you can't compare a property to a dynamic value.</span><span class="sxs-lookup"><span data-stu-id="609d3-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="609d3-146">One side of the expression must be a constant.</span><span class="sxs-lookup"><span data-stu-id="609d3-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="609d3-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span><span class="sxs-lookup"><span data-stu-id="609d3-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="609d3-148">A space is URL-encoded as `%20`.</span><span class="sxs-lookup"><span data-stu-id="609d3-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="609d3-149">All parts of the filter string are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="609d3-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="609d3-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span><span class="sxs-lookup"><span data-stu-id="609d3-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="609d3-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="609d3-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="609d3-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="609d3-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="609d3-153">**Query**</span><span class="sxs-lookup"><span data-stu-id="609d3-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="609d3-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="609d3-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="609d3-155">**Results**</span><span class="sxs-lookup"><span data-stu-id="609d3-155">**Results**</span></span>

| <span data-ttu-id="609d3-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="609d3-156">PartitionKey</span></span> | <span data-ttu-id="609d3-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="609d3-157">RowKey</span></span> | <span data-ttu-id="609d3-158">Email</span><span class="sxs-lookup"><span data-stu-id="609d3-158">Email</span></span> | <span data-ttu-id="609d3-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="609d3-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="609d3-160">Ben</span><span class="sxs-lookup"><span data-stu-id="609d3-160">Ben</span></span> |<span data-ttu-id="609d3-161">Smith</span><span class="sxs-lookup"><span data-stu-id="609d3-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="609d3-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="609d3-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="609d3-163">Query by using LINQ</span><span class="sxs-lookup"><span data-stu-id="609d3-163">Query by using LINQ</span></span> 
<span data-ttu-id="609d3-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span><span class="sxs-lookup"><span data-stu-id="609d3-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="609d3-165">Here's an example of how to build queries by using the .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="609d3-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a><span data-ttu-id="609d3-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="609d3-166">Next steps</span></span>

<span data-ttu-id="609d3-167">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="609d3-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="609d3-168">Learned how to query by using the Table API</span><span class="sxs-lookup"><span data-stu-id="609d3-168">Learned how to query by using the Table API</span></span>

<span data-ttu-id="609d3-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span><span class="sxs-lookup"><span data-stu-id="609d3-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="609d3-170">Distribute your data globally</span><span class="sxs-lookup"><span data-stu-id="609d3-170">Distribute your data globally</span></span>](tutorial-global-distribution-table.md)
