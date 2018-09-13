---
title: Learn how to set time to live value for Azure Cosmos DB documents created through MongoDB API to automatically purge them from the system after a period of time.
description: Documentation for the MongoDB per-document TTL feature.
services: cosmos-db
author: orestis-ms
manager: kfile
editor: ''
ms.service: cosmos-db
ms.devlang: javascript
ms.topic: quickstart
ms.date: 08/10/2018
ms.author: orkostak
ms.openlocfilehash: 0bf8891e28897321dbfbad4486dd11c0b5ee4264
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866045"
---
# <a name="expire-data-in-azure-cosmos-db-mongodb-api"></a><span data-ttu-id="75f2a-103">Expire data in Azure Cosmos DB MongoDB API</span><span class="sxs-lookup"><span data-stu-id="75f2a-103">Expire data in Azure Cosmos DB MongoDB API</span></span>

<span data-ttu-id="75f2a-104">Time-to-live (TTL) functionality allows the database to automatically expire data.</span><span class="sxs-lookup"><span data-stu-id="75f2a-104">Time-to-live (TTL) functionality allows the database to automatically expire data.</span></span> <span data-ttu-id="75f2a-105">MongoDB API utilizes Azure Cosmos DB's TTL capabilities.</span><span class="sxs-lookup"><span data-stu-id="75f2a-105">MongoDB API utilizes Azure Cosmos DB's TTL capabilities.</span></span> <span data-ttu-id="75f2a-106">Two modes are supported: setting a default TTL value on the whole collection, and setting individual TTL values for each document.</span><span class="sxs-lookup"><span data-stu-id="75f2a-106">Two modes are supported: setting a default TTL value on the whole collection, and setting individual TTL values for each document.</span></span> <span data-ttu-id="75f2a-107">The logic governing TTL indexes and per-document TTL values in MongoDB  API is the [same as in Azure Cosmos DB](../cosmos-db/mongodb-indexing.md).</span><span class="sxs-lookup"><span data-stu-id="75f2a-107">The logic governing TTL indexes and per-document TTL values in MongoDB  API is the [same as in Azure Cosmos DB](../cosmos-db/mongodb-indexing.md).</span></span>

## <a name="ttl-indexes"></a><span data-ttu-id="75f2a-108">TTL indexes</span><span class="sxs-lookup"><span data-stu-id="75f2a-108">TTL indexes</span></span>
<span data-ttu-id="75f2a-109">To enable TTL universally on a collection, a ["TTL index" (time-to-live index)](../cosmos-db/mongodb-indexing.md) needs to be created.</span><span class="sxs-lookup"><span data-stu-id="75f2a-109">To enable TTL universally on a collection, a ["TTL index" (time-to-live index)](../cosmos-db/mongodb-indexing.md) needs to be created.</span></span> <span data-ttu-id="75f2a-110">The TTL index is an index on the _ts field with an "expireAfterSeconds" value.</span><span class="sxs-lookup"><span data-stu-id="75f2a-110">The TTL index is an index on the _ts field with an "expireAfterSeconds" value.</span></span>

<span data-ttu-id="75f2a-111">Example:</span><span class="sxs-lookup"><span data-stu-id="75f2a-111">Example:</span></span>
```JavaScript
globaldb:PRIMARY> db.coll.createIndex({"_ts":1}, {expireAfterSeconds: 10})
{
        "_t" : "CreateIndexesResponse",
        "ok" : 1,
        "createdCollectionAutomatically" : true,
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 4
}
```

<span data-ttu-id="75f2a-112">The command in the above example will create an index with TTL functionality.</span><span class="sxs-lookup"><span data-stu-id="75f2a-112">The command in the above example will create an index with TTL functionality.</span></span> <span data-ttu-id="75f2a-113">Once the index is created, the database will automatically delete any documents in that collection that have not been modified in the last 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="75f2a-113">Once the index is created, the database will automatically delete any documents in that collection that have not been modified in the last 10 seconds.</span></span> 

> [!NOTE]
> <span data-ttu-id="75f2a-114">**_ts** is a Cosmos DB-specific field and is not accessible from MongoDB clients.</span><span class="sxs-lookup"><span data-stu-id="75f2a-114">**_ts** is a Cosmos DB-specific field and is not accessible from MongoDB clients.</span></span> <span data-ttu-id="75f2a-115">It is a reserved (system) property that contains the timestamp of the document's last modification.</span><span class="sxs-lookup"><span data-stu-id="75f2a-115">It is a reserved (system) property that contains the timestamp of the document's last modification.</span></span>
>
    
<span data-ttu-id="75f2a-116">Additionally, a C# example:</span><span class="sxs-lookup"><span data-stu-id="75f2a-116">Additionally, a C# example:</span></span> 
```C# 
var options = new CreateIndexOptions {ExpireAfter = TimeSpan.FromSeconds(10)}; 
var field = new StringFieldDefinition<BsonDocument>("_ts"); 
var indexDefinition = new IndexKeysDefinitionBuilder<BsonDocument>().Ascending(field); 
await collection.Indexes.CreateOneAsync(indexDefinition, options); 
``` 

## <a name="set-time-to-live-value-for-a-document"></a><span data-ttu-id="75f2a-117">Set time to live value for a document</span><span class="sxs-lookup"><span data-stu-id="75f2a-117">Set time to live value for a document</span></span> 
<span data-ttu-id="75f2a-118">Per-document TTL values are also supported.</span><span class="sxs-lookup"><span data-stu-id="75f2a-118">Per-document TTL values are also supported.</span></span> <span data-ttu-id="75f2a-119">The document(s) must contain a root-level property "ttl" (lower-case), and a TTL index as described above must have been created for that collection.</span><span class="sxs-lookup"><span data-stu-id="75f2a-119">The document(s) must contain a root-level property "ttl" (lower-case), and a TTL index as described above must have been created for that collection.</span></span> <span data-ttu-id="75f2a-120">TTL values set on a document will override the collection's TTL value.</span><span class="sxs-lookup"><span data-stu-id="75f2a-120">TTL values set on a document will override the collection's TTL value.</span></span>

<span data-ttu-id="75f2a-121">The TTL value must be an int32.</span><span class="sxs-lookup"><span data-stu-id="75f2a-121">The TTL value must be an int32.</span></span> <span data-ttu-id="75f2a-122">Alternatively, an int64 that fits in an int32, or a double with no decimal part that fits in an int32.</span><span class="sxs-lookup"><span data-stu-id="75f2a-122">Alternatively, an int64 that fits in an int32, or a double with no decimal part that fits in an int32.</span></span> <span data-ttu-id="75f2a-123">Values for the TTL property that do not conform to these specifications are allowed but not treated as a meaningful document TTL value.</span><span class="sxs-lookup"><span data-stu-id="75f2a-123">Values for the TTL property that do not conform to these specifications are allowed but not treated as a meaningful document TTL value.</span></span>

<span data-ttu-id="75f2a-124">The TTL value for the document is optional; documents without a TTL value can be inserted into the collection.</span><span class="sxs-lookup"><span data-stu-id="75f2a-124">The TTL value for the document is optional; documents without a TTL value can be inserted into the collection.</span></span>  <span data-ttu-id="75f2a-125">In this case, the collection's TTL value will be honored.</span><span class="sxs-lookup"><span data-stu-id="75f2a-125">In this case, the collection's TTL value will be honored.</span></span> 

<span data-ttu-id="75f2a-126">The following documents have valid TTL values.</span><span class="sxs-lookup"><span data-stu-id="75f2a-126">The following documents have valid TTL values.</span></span> <span data-ttu-id="75f2a-127">Once the documents are insterted, the document TTL values override the collection's TTL values.</span><span class="sxs-lookup"><span data-stu-id="75f2a-127">Once the documents are insterted, the document TTL values override the collection's TTL values.</span></span> <span data-ttu-id="75f2a-128">So, the documents will be removed after 20 seconds.</span><span class="sxs-lookup"><span data-stu-id="75f2a-128">So, the documents will be removed after 20 seconds.</span></span>  

```JavaScript 
globaldb:PRIMARY> db.coll.insert({id:1, location: "Paris", ttl: 20.0}) 
globaldb:PRIMARY> db.coll.insert({id:1, location: "Paris", ttl: NumberInt(20)}) 
globaldb:PRIMARY> db.coll.insert({id:1, location: "Paris", ttl: NumberLong(20)}) 
```

<span data-ttu-id="75f2a-129">The following documents have invalid TTL values.</span><span class="sxs-lookup"><span data-stu-id="75f2a-129">The following documents have invalid TTL values.</span></span> <span data-ttu-id="75f2a-130">The documents will be inserted, but the document TTL value will not be honored.</span><span class="sxs-lookup"><span data-stu-id="75f2a-130">The documents will be inserted, but the document TTL value will not be honored.</span></span> <span data-ttu-id="75f2a-131">So, the documents will be removed after 10 seconds because of the collection's TTL value.</span><span class="sxs-lookup"><span data-stu-id="75f2a-131">So, the documents will be removed after 10 seconds because of the collection's TTL value.</span></span> 

```JavaScript 
globaldb:PRIMARY> db.coll.insert({id:1, location: "Paris", ttl: 20.5}) //TTL value contains non-zero decimal part. 
globaldb:PRIMARY> db.coll.insert({id:1, location: "Paris", ttl: NumberLong(2147483649)}) //TTL value is greater than Int32.MaxValue (2,147,483,648). 
``` 

## <a name="how-to-activate-the-per-document-ttl-feature"></a><span data-ttu-id="75f2a-132">How to activate the per-document TTL feature</span><span class="sxs-lookup"><span data-stu-id="75f2a-132">How to activate the per-document TTL feature</span></span>
<span data-ttu-id="75f2a-133">The per-document TTL feature can be activated via the MongoDB API account's "Preview Features" tab in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="75f2a-133">The per-document TTL feature can be activated via the MongoDB API account's "Preview Features" tab in Azure Portal.</span></span>

![Screen shot of the Per-document TTL feature activation in Portal](./media/mongodb-ttl/mongodb_portal_ttl.png) 

## <a name="next-steps"></a><span data-ttu-id="75f2a-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="75f2a-135">Next steps</span></span>
* [<span data-ttu-id="75f2a-136">Expire data in Azure Cosmos DB collections automatically with time to live</span><span class="sxs-lookup"><span data-stu-id="75f2a-136">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>](../cosmos-db/time-to-live.md)
* [<span data-ttu-id="75f2a-137">Indexing in the Azure Cosmos DB MongoDB API</span><span class="sxs-lookup"><span data-stu-id="75f2a-137">Indexing in the Azure Cosmos DB MongoDB API</span></span>](../cosmos-db/mongodb-indexing.md)
