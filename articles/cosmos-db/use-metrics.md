---
title: Monitoring and debugging with metrics in Azure Cosmos DB | Microsoft Docs
description: Use metrics in Azure Cosmos DB to debug common issues and monitor the database.
keywords: metrics
services: cosmos-db
author: kanshiG
manager: kfile
editor: ''
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 09/25/2017
ms.author: govindk
ms.openlocfilehash: 792e0b3f8fdfe4ab1b79fec5f45d0587033eca0d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871518"
---
# <a name="monitoring-and-debugging-with-metrics-in-azure-cosmos-db"></a><span data-ttu-id="91c66-104">Monitoring and debugging with metrics in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="91c66-104">Monitoring and debugging with metrics in Azure Cosmos DB</span></span>

<span data-ttu-id="91c66-105">Azure Cosmos DB provides metrics for throughput, storage, consistency, availability, and latency.</span><span class="sxs-lookup"><span data-stu-id="91c66-105">Azure Cosmos DB provides metrics for throughput, storage, consistency, availability, and latency.</span></span> <span data-ttu-id="91c66-106">The [Azure portal](https://portal.azure.com) provides an aggregated view of these metrics; for more granular metrics, both the client SDK and the [diagnostic logs](./logging.md) are available.</span><span class="sxs-lookup"><span data-stu-id="91c66-106">The [Azure portal](https://portal.azure.com) provides an aggregated view of these metrics; for more granular metrics, both the client SDK and the [diagnostic logs](./logging.md) are available.</span></span>

<span data-ttu-id="91c66-107">This article walks through common use cases and how Azure Cosmos DB metrics can be used to analyze and debug these issues.</span><span class="sxs-lookup"><span data-stu-id="91c66-107">This article walks through common use cases and how Azure Cosmos DB metrics can be used to analyze and debug these issues.</span></span> <span data-ttu-id="91c66-108">Metrics are collected every five minutes and are retained for seven days.</span><span class="sxs-lookup"><span data-stu-id="91c66-108">Metrics are collected every five minutes and are retained for seven days.</span></span>

## <a name="understanding-how-many-requests-are-succeeding-or-causing-errors"></a><span data-ttu-id="91c66-109">Understanding how many requests are succeeding or causing errors</span><span class="sxs-lookup"><span data-stu-id="91c66-109">Understanding how many requests are succeeding or causing errors</span></span>

<span data-ttu-id="91c66-110">To get started, head to the [Azure portal](https://portal.azure.com) and navigate to the **Metrics** blade.</span><span class="sxs-lookup"><span data-stu-id="91c66-110">To get started, head to the [Azure portal](https://portal.azure.com) and navigate to the **Metrics** blade.</span></span> <span data-ttu-id="91c66-111">In the blade, find the **Number of requests exceeded capacity per 1 minute** chart.</span><span class="sxs-lookup"><span data-stu-id="91c66-111">In the blade, find the **Number of requests exceeded capacity per 1 minute** chart.</span></span> <span data-ttu-id="91c66-112">This chart shows a minute by minute total requests segmented by the status code.</span><span class="sxs-lookup"><span data-stu-id="91c66-112">This chart shows a minute by minute total requests segmented by the status code.</span></span> <span data-ttu-id="91c66-113">For more information about HTTP status codes, see [HTTP Status Codes for Azure Cosmos DB](https://docs.microsoft.com/rest/api/cosmos-db/http-status-codes-for-cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="91c66-113">For more information about HTTP status codes, see [HTTP Status Codes for Azure Cosmos DB](https://docs.microsoft.com/rest/api/cosmos-db/http-status-codes-for-cosmosdb).</span></span>

<span data-ttu-id="91c66-114">The most common error status code is 429 (rate limiting/throttling), which means that requests to Azure Cosmos DB are exceeding the provisioned throughput.</span><span class="sxs-lookup"><span data-stu-id="91c66-114">The most common error status code is 429 (rate limiting/throttling), which means that requests to Azure Cosmos DB are exceeding the provisioned throughput.</span></span> <span data-ttu-id="91c66-115">The most common solution to this is to [scale up the RUs](./set-throughput.md) for the given collection.</span><span class="sxs-lookup"><span data-stu-id="91c66-115">The most common solution to this is to [scale up the RUs](./set-throughput.md) for the given collection.</span></span>

![Number of requests per minute](media/use-metrics/metrics-12.png)

## <a name="determining-the-throughput-distribution-across-partitions"></a><span data-ttu-id="91c66-117">Determining the throughput distribution across partitions</span><span class="sxs-lookup"><span data-stu-id="91c66-117">Determining the throughput distribution across partitions</span></span>

<span data-ttu-id="91c66-118">Having a good cardinality of your partition keys is essential for any scalable application.</span><span class="sxs-lookup"><span data-stu-id="91c66-118">Having a good cardinality of your partition keys is essential for any scalable application.</span></span> <span data-ttu-id="91c66-119">To determine the throughput distribution of any partitioned container broken down by partitions, navigate to the **Metrics blade** in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91c66-119">To determine the throughput distribution of any partitioned container broken down by partitions, navigate to the **Metrics blade** in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="91c66-120">In the **Throughput** tab, the storage breakdown is shown in the **Max consumed RU/second by each physical partition** chart.</span><span class="sxs-lookup"><span data-stu-id="91c66-120">In the **Throughput** tab, the storage breakdown is shown in the **Max consumed RU/second by each physical partition** chart.</span></span> <span data-ttu-id="91c66-121">The following graphic illustrates an example of a poor distribution of data as evidenced by the skewed partition on the far left.</span><span class="sxs-lookup"><span data-stu-id="91c66-121">The following graphic illustrates an example of a poor distribution of data as evidenced by the skewed partition on the far left.</span></span> 

![Single partition seeing heavy usage at 3:05 PM](media/use-metrics/metrics-17.png)

<span data-ttu-id="91c66-123">An uneven throughput distribution may cause *hot* partitions, which can result in throttled requests and may require repartitioning.</span><span class="sxs-lookup"><span data-stu-id="91c66-123">An uneven throughput distribution may cause *hot* partitions, which can result in throttled requests and may require repartitioning.</span></span> <span data-ttu-id="91c66-124">For more information about partitioning in Azure Cosmos DB, see [Partition and scale in Azure Cosmos DB](./partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="91c66-124">For more information about partitioning in Azure Cosmos DB, see [Partition and scale in Azure Cosmos DB](./partition-data.md).</span></span>

## <a name="determining-the-storage-distribution-across-partitions"></a><span data-ttu-id="91c66-125">Determining the storage distribution across partitions</span><span class="sxs-lookup"><span data-stu-id="91c66-125">Determining the storage distribution across partitions</span></span>

<span data-ttu-id="91c66-126">Having a good cardinality of your partition is essential for any scalable application.</span><span class="sxs-lookup"><span data-stu-id="91c66-126">Having a good cardinality of your partition is essential for any scalable application.</span></span> <span data-ttu-id="91c66-127">To determine the throughput distribution of any partitioned container broken down by partitions, head to the Metrics blade in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91c66-127">To determine the throughput distribution of any partitioned container broken down by partitions, head to the Metrics blade in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="91c66-128">In the Throughput tab, the storage breakdown is shown in the Max consumed RU/second by each physical partition chart.</span><span class="sxs-lookup"><span data-stu-id="91c66-128">In the Throughput tab, the storage breakdown is shown in the Max consumed RU/second by each physical partition chart.</span></span> <span data-ttu-id="91c66-129">The following graphic illustrates a poor distribution of data as evidenced by the skewed partition on the far left.</span><span class="sxs-lookup"><span data-stu-id="91c66-129">The following graphic illustrates a poor distribution of data as evidenced by the skewed partition on the far left.</span></span> 

![Example of poor data distribution](media/use-metrics/metrics-07.png)

<span data-ttu-id="91c66-131">You can root cause which partition key is skewing the distribution by clicking on the partition in the chart.</span><span class="sxs-lookup"><span data-stu-id="91c66-131">You can root cause which partition key is skewing the distribution by clicking on the partition in the chart.</span></span> 

![Partition key is skewing the distribution](media/use-metrics/metrics-05.png)

<span data-ttu-id="91c66-133">After identifying which partition key is causing the skew in distribution, you may have to repartition your container with a more distributed partition key.</span><span class="sxs-lookup"><span data-stu-id="91c66-133">After identifying which partition key is causing the skew in distribution, you may have to repartition your container with a more distributed partition key.</span></span> <span data-ttu-id="91c66-134">For more information about partitioning in Azure Cosmos DB, see [Partition and scale in Azure Cosmos DB](./partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="91c66-134">For more information about partitioning in Azure Cosmos DB, see [Partition and scale in Azure Cosmos DB](./partition-data.md).</span></span>

## <a name="comparing-data-size-against-index-size"></a><span data-ttu-id="91c66-135">Comparing data size against index size</span><span class="sxs-lookup"><span data-stu-id="91c66-135">Comparing data size against index size</span></span>

<span data-ttu-id="91c66-136">In Azure Cosmos DB, the total consumed storage is the combination of both the Data size and Index size.</span><span class="sxs-lookup"><span data-stu-id="91c66-136">In Azure Cosmos DB, the total consumed storage is the combination of both the Data size and Index size.</span></span> <span data-ttu-id="91c66-137">Typically, the index size is a fraction of the data size.</span><span class="sxs-lookup"><span data-stu-id="91c66-137">Typically, the index size is a fraction of the data size.</span></span> <span data-ttu-id="91c66-138">In the Metrics blade in the [Azure portal](https://portal.azure.com), the Storage tab showcases the breakdown of storage consumption based on data and index.</span><span class="sxs-lookup"><span data-stu-id="91c66-138">In the Metrics blade in the [Azure portal](https://portal.azure.com), the Storage tab showcases the breakdown of storage consumption based on data and index.</span></span> <span data-ttu-id="91c66-139">Image (maybe) Alternatively, from the SDK, you can find the current storage usage through a collection read.</span><span class="sxs-lookup"><span data-stu-id="91c66-139">Image (maybe) Alternatively, from the SDK, you can find the current storage usage through a collection read.</span></span>
```csharp
// Measure the document size usage (which includes the index size)  
ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll")); 
 Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);
``` 
<span data-ttu-id="91c66-140">If you would like to conserve index space, you can adjust the [indexing policy](./indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="91c66-140">If you would like to conserve index space, you can adjust the [indexing policy](./indexing-policies.md).</span></span>

## <a name="debugging-why-queries-are-running-slow"></a><span data-ttu-id="91c66-141">Debugging why queries are running slow</span><span class="sxs-lookup"><span data-stu-id="91c66-141">Debugging why queries are running slow</span></span>

<span data-ttu-id="91c66-142">In the SQL API SDKs, Azure Cosmos DB provides query execution statistics.</span><span class="sxs-lookup"><span data-stu-id="91c66-142">In the SQL API SDKs, Azure Cosmos DB provides query execution statistics.</span></span> 

```csharp
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
 UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
 "SELECT * FROM c WHERE c.city = 'Seattle'", 
 new FeedOptions 
 { 
 PopulateQueryMetrics = true, 
 MaxItemCount = -1, 
 MaxDegreeOfParallelism = -1, 
 EnableCrossPartitionQuery = true 
 }).AsDocumentQuery();
FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id 
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;
```

<span data-ttu-id="91c66-143">*QueryMetrics* provides details on how long each component of the query took to execution.</span><span class="sxs-lookup"><span data-stu-id="91c66-143">*QueryMetrics* provides details on how long each component of the query took to execution.</span></span> <span data-ttu-id="91c66-144">The most common root cause for long running queries are scans (the query was unable to leverage the indexes), which can be resolved with a better filter condition.</span><span class="sxs-lookup"><span data-stu-id="91c66-144">The most common root cause for long running queries are scans (the query was unable to leverage the indexes), which can be resolved with a better filter condition.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91c66-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="91c66-145">Next steps</span></span>

<span data-ttu-id="91c66-146">Now that you've learned how to monitor and debug issues using the metrics provided in the Azure portal, you may want to learn more about improving database performance by reading the following articles:</span><span class="sxs-lookup"><span data-stu-id="91c66-146">Now that you've learned how to monitor and debug issues using the metrics provided in the Azure portal, you may want to learn more about improving database performance by reading the following articles:</span></span>

* [<span data-ttu-id="91c66-147">Performance and scale testing with Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="91c66-147">Performance and scale testing with Azure Cosmos DB</span></span>](performance-testing.md)
* [<span data-ttu-id="91c66-148">Performance tips for Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="91c66-148">Performance tips for Azure Cosmos DB</span></span>](performance-tips.md)
