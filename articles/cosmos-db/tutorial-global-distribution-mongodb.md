---
title: Azure Cosmos DB global distribution tutorial for MongoDB API | Microsoft Docs
description: Learn how to set up Azure Cosmos DB global distribution using the MongoDB API.
services: cosmos-db
keywords: global distribution, MongoDB
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: na
ms.topic: tutorial
ms.date: 05/10/2017
ms.author: sngun
ms.custom: mvc
ms.openlocfilehash: 91b52b2d1446227f9896351c81e763333ec36e26
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869004"
---
# <a name="set-up-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="86bfb-104">Set up Azure Cosmos DB global distribution using the MongoDB API</span><span class="sxs-lookup"><span data-stu-id="86bfb-104">Set up Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="86bfb-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="86bfb-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="86bfb-106">This article covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="86bfb-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="86bfb-107">Configure global distribution using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="86bfb-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="86bfb-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="86bfb-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="86bfb-109">Verifying your regional setup using the MongoDB API</span><span class="sxs-lookup"><span data-stu-id="86bfb-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="86bfb-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span><span class="sxs-lookup"><span data-stu-id="86bfb-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="86bfb-111">From your Mongo Shell:</span><span class="sxs-lookup"><span data-stu-id="86bfb-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="86bfb-112">Example results:</span><span class="sxs-lookup"><span data-stu-id="86bfb-112">Example results:</span></span>

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="86bfb-113">Connecting to a preferred region using the MongoDB API</span><span class="sxs-lookup"><span data-stu-id="86bfb-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="86bfb-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span><span class="sxs-lookup"><span data-stu-id="86bfb-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="86bfb-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span><span class="sxs-lookup"><span data-stu-id="86bfb-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="86bfb-116">A read preference of *nearest* is configured to read from the closest region.</span><span class="sxs-lookup"><span data-stu-id="86bfb-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="86bfb-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span><span class="sxs-lookup"><span data-stu-id="86bfb-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="86bfb-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span><span class="sxs-lookup"><span data-stu-id="86bfb-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="86bfb-119">Lastly, if you would like to manually specify your read regions.</span><span class="sxs-lookup"><span data-stu-id="86bfb-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="86bfb-120">You can set the region Tag within your read preference.</span><span class="sxs-lookup"><span data-stu-id="86bfb-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="86bfb-121">That's it, that completes this tutorial.</span><span class="sxs-lookup"><span data-stu-id="86bfb-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="86bfb-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="86bfb-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="86bfb-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="86bfb-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86bfb-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="86bfb-124">Next steps</span></span>

<span data-ttu-id="86bfb-125">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="86bfb-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86bfb-126">Configure global distribution using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="86bfb-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="86bfb-127">Configure global distribution using the SQL APIs</span><span class="sxs-lookup"><span data-stu-id="86bfb-127">Configure global distribution using the SQL APIs</span></span>

<span data-ttu-id="86bfb-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span><span class="sxs-lookup"><span data-stu-id="86bfb-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="86bfb-129">Develop locally with the emulator</span><span class="sxs-lookup"><span data-stu-id="86bfb-129">Develop locally with the emulator</span></span>](local-emulator.md)
