---
title: Indexing in Azure Cosmos DB MongoDB API | Microsoft Docs
description: Presents an overview of the indexing capabilities in Azure Cosmos DB MongoDB API.
services: cosmos-db
author: orestis-ms
manager: kfile
editor: ''
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: nodejs
ms.topic: conceptual
ms.date: 03/01/2018
ms.author: orkostak
ms.openlocfilehash: a3dadfc4257d43f9df1b93f5d486e5577b7889d6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864855"
---
# <a name="indexing-in-the-azure-cosmos-db-mongodb-api"></a><span data-ttu-id="390c6-103">Indexing in the Azure Cosmos DB: MongoDB API</span><span class="sxs-lookup"><span data-stu-id="390c6-103">Indexing in the Azure Cosmos DB: MongoDB API</span></span>

<span data-ttu-id="390c6-104">Azure Cosmos DB MongoDB API leverages automatic index management capabilities of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="390c6-104">Azure Cosmos DB MongoDB API leverages automatic index management capabilities of Azure Cosmos DB.</span></span> <span data-ttu-id="390c6-105">As a result, users have access to the default indexing policies of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="390c6-105">As a result, users have access to the default indexing policies of Azure Cosmos DB.</span></span> <span data-ttu-id="390c6-106">So, if no indexes have been defined by the user, or no indexes have been dropped, then all fields will be automatically indexed by default when inserted into the collection.</span><span class="sxs-lookup"><span data-stu-id="390c6-106">So, if no indexes have been defined by the user, or no indexes have been dropped, then all fields will be automatically indexed by default when inserted into the collection.</span></span> <span data-ttu-id="390c6-107">For most scenarios, we recommend using the default indexing policy set on the account.</span><span class="sxs-lookup"><span data-stu-id="390c6-107">For most scenarios, we recommend using the default indexing policy set on the account.</span></span>

## <a name="dropping-the-default-indexes"></a><span data-ttu-id="390c6-108">Dropping the default indexes</span><span class="sxs-lookup"><span data-stu-id="390c6-108">Dropping the default indexes</span></span>

<span data-ttu-id="390c6-109">The following command can be used to drop the default indexes for a collection ```coll```:</span><span class="sxs-lookup"><span data-stu-id="390c6-109">The following command can be used to drop the default indexes for a collection ```coll```:</span></span>

```JavaScript
> db.coll.dropIndexes()
{ "_t" : "DropIndexesResponse", "ok" : 1, "nIndexesWas" : 3 }
```

## <a name="creating-compound-indexes"></a><span data-ttu-id="390c6-110">Creating compound indexes</span><span class="sxs-lookup"><span data-stu-id="390c6-110">Creating compound indexes</span></span>

<span data-ttu-id="390c6-111">Compound indexes hold references to multiple fields of a document.</span><span class="sxs-lookup"><span data-stu-id="390c6-111">Compound indexes hold references to multiple fields of a document.</span></span> <span data-ttu-id="390c6-112">Logically, they are equivalent to creating multiple individual indexes per field.</span><span class="sxs-lookup"><span data-stu-id="390c6-112">Logically, they are equivalent to creating multiple individual indexes per field.</span></span> <span data-ttu-id="390c6-113">To take advantage of the optimizations provided by Cosmos DB indexing techniques, we recommend creating multiple individual indexes instead of a single (non-unique) compound index.</span><span class="sxs-lookup"><span data-stu-id="390c6-113">To take advantage of the optimizations provided by Cosmos DB indexing techniques, we recommend creating multiple individual indexes instead of a single (non-unique) compound index.</span></span>

## <a name="creating-unique-indexes"></a><span data-ttu-id="390c6-114">Creating unique indexes</span><span class="sxs-lookup"><span data-stu-id="390c6-114">Creating unique indexes</span></span>

<span data-ttu-id="390c6-115">[Unique indexes](unique-keys.md) are useful for enforcing that no two or more documents contain the same value for the indexed field(s).</span><span class="sxs-lookup"><span data-stu-id="390c6-115">[Unique indexes](unique-keys.md) are useful for enforcing that no two or more documents contain the same value for the indexed field(s).</span></span> 
>[!important] 
> <span data-ttu-id="390c6-116">Currently, unique indexes can be created only when the collection is empty (contains no documents).</span><span class="sxs-lookup"><span data-stu-id="390c6-116">Currently, unique indexes can be created only when the collection is empty (contains no documents).</span></span> 

<span data-ttu-id="390c6-117">The following command creates a unique index on the field "student_id":</span><span class="sxs-lookup"><span data-stu-id="390c6-117">The following command creates a unique index on the field "student_id":</span></span>

```JavaScript
globaldb:PRIMARY> db.coll.createIndex( { "student_id" : 1 }, {unique:true} ) 
{
        "_t" : "CreateIndexesResponse",
        "ok" : 1,
        "createdCollectionAutomatically" : false,
        "numIndexesBefore" : 1,
        "numIndexesAfter" : 4
}
```

<span data-ttu-id="390c6-118">For sharded collections, as per MongoDB behavior, creating a unique index requires providing the shard (partition) key.</span><span class="sxs-lookup"><span data-stu-id="390c6-118">For sharded collections, as per MongoDB behavior, creating a unique index requires providing the shard (partition) key.</span></span> <span data-ttu-id="390c6-119">In other words, all unique indexes on a sharded collection are compound indexes where one of the fields is the partition key.</span><span class="sxs-lookup"><span data-stu-id="390c6-119">In other words, all unique indexes on a sharded collection are compound indexes where one of the fields is the partition key.</span></span>

<span data-ttu-id="390c6-120">The following commands create a sharded collection ```coll``` (shard key is ```university```) with a unique index on fields student_id and university:</span><span class="sxs-lookup"><span data-stu-id="390c6-120">The following commands create a sharded collection ```coll``` (shard key is ```university```) with a unique index on fields student_id and university:</span></span>

```JavaScript
globaldb:PRIMARY> db.runCommand({shardCollection: db.coll._fullName, key: { university: "hashed"}});
{
        "_t" : "ShardCollectionResponse",
        "ok" : 1,
        "collectionsharded" : "test.coll"
}
globaldb:PRIMARY> db.coll.createIndex( { "student_id" : 1, "university" : 1 }, {unique:true})
{
        "_t" : "CreateIndexesResponse",
        "ok" : 1,
        "createdCollectionAutomatically" : false,
        "numIndexesBefore" : 3,
        "numIndexesAfter" : 4
}
```

<span data-ttu-id="390c6-121">In the above example, if ```"university":1``` clause was omitted, an error with the following message would be returned:</span><span class="sxs-lookup"><span data-stu-id="390c6-121">In the above example, if ```"university":1``` clause was omitted, an error with the following message would be returned:</span></span>

```"cannot create unique index over {student_id : 1.0} with shard key pattern { university : 1.0 }"```

## <a name="ttl-indexes"></a><span data-ttu-id="390c6-122">TTL indexes</span><span class="sxs-lookup"><span data-stu-id="390c6-122">TTL indexes</span></span>

<span data-ttu-id="390c6-123">To enable document expiration in a particular collection, a ["TTL index" (time-to-live index)](../cosmos-db/time-to-live.md) needs to be created.</span><span class="sxs-lookup"><span data-stu-id="390c6-123">To enable document expiration in a particular collection, a ["TTL index" (time-to-live index)](../cosmos-db/time-to-live.md) needs to be created.</span></span> <span data-ttu-id="390c6-124">A TTL index is an index on the _ts field with an "expireAfterSeconds" value.</span><span class="sxs-lookup"><span data-stu-id="390c6-124">A TTL index is an index on the _ts field with an "expireAfterSeconds" value.</span></span>
 
<span data-ttu-id="390c6-125">Example:</span><span class="sxs-lookup"><span data-stu-id="390c6-125">Example:</span></span>
```JavaScript
globaldb:PRIMARY> db.coll.createIndex({"_ts":1}, {expireAfterSeconds: 10})
```

<span data-ttu-id="390c6-126">The preceding command will cause the deletion of any documents in ```db.coll``` collection that have not been modified in the last 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="390c6-126">The preceding command will cause the deletion of any documents in ```db.coll``` collection that have not been modified in the last 10 seconds.</span></span> 
 
> [!NOTE]
> <span data-ttu-id="390c6-127">**_ts** is a Cosmos DB-specific field and is not accessible from MongoDB clients.</span><span class="sxs-lookup"><span data-stu-id="390c6-127">**_ts** is a Cosmos DB-specific field and is not accessible from MongoDB clients.</span></span> <span data-ttu-id="390c6-128">It is a reserved (system) property that contains the timestamp of the document's last modification.</span><span class="sxs-lookup"><span data-stu-id="390c6-128">It is a reserved (system) property that contains the timestamp of the document's last modification.</span></span>
>

## <a name="migrating-collections-with-indexes"></a><span data-ttu-id="390c6-129">Migrating collections with indexes</span><span class="sxs-lookup"><span data-stu-id="390c6-129">Migrating collections with indexes</span></span>

<span data-ttu-id="390c6-130">Currently, creating unique indexes is possible only when the collection contains no documents.</span><span class="sxs-lookup"><span data-stu-id="390c6-130">Currently, creating unique indexes is possible only when the collection contains no documents.</span></span> <span data-ttu-id="390c6-131">Popular MongoDB migration tools attempt to create the unique indexes after importing the data.</span><span class="sxs-lookup"><span data-stu-id="390c6-131">Popular MongoDB migration tools attempt to create the unique indexes after importing the data.</span></span> <span data-ttu-id="390c6-132">To circumvent this issue, it is suggested that users manually create the corresponding collections and unique indexes, instead of allowing the migration tool (for ```mongorestore``` this behavior is achieved by using the --noIndexRestore flag in the command line).</span><span class="sxs-lookup"><span data-stu-id="390c6-132">To circumvent this issue, it is suggested that users manually create the corresponding collections and unique indexes, instead of allowing the migration tool (for ```mongorestore``` this behavior is achieved by using the --noIndexRestore flag in the command line).</span></span>

## <a name="next-steps"></a><span data-ttu-id="390c6-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="390c6-133">Next steps</span></span>
* [<span data-ttu-id="390c6-134">How does Azure Cosmos DB index data?</span><span class="sxs-lookup"><span data-stu-id="390c6-134">How does Azure Cosmos DB index data?</span></span>](../cosmos-db/indexing-policies.md)
* [<span data-ttu-id="390c6-135">Expire data in Azure Cosmos DB collections automatically with time to live</span><span class="sxs-lookup"><span data-stu-id="390c6-135">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>](../cosmos-db/time-to-live.md)
