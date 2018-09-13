---
title: Working with the Change Feed support in Azure DocumentDB | Microsoft Docs
description: Use Azure DocumentDB's Change Feed support to track changes in DocumentDB documents and perform event-based processing like triggers and keeping caches and analytics systems up-to-date.
keywords: change feed
services: documentdb
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: ''
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 03/23/2017
ms.author: arramac
ms.openlocfilehash: 8e2a6b3ab98c383d576d5ba14224b4a136054f70
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540687"
---
# <a name="working-with-the-change-feed-support-in-azure-documentdb"></a><span data-ttu-id="68b81-104">Working with the Change Feed support in Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="68b81-104">Working with the Change Feed support in Azure DocumentDB</span></span>
<span data-ttu-id="68b81-105">[Azure DocumentDB](documentdb-introduction.md) is a fast and flexible NoSQL database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span><span class="sxs-lookup"><span data-stu-id="68b81-105">[Azure DocumentDB](documentdb-introduction.md) is a fast and flexible NoSQL database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="68b81-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span><span class="sxs-lookup"><span data-stu-id="68b81-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="68b81-107">A common design pattern in these applications is to track changes made to DocumentDB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span><span class="sxs-lookup"><span data-stu-id="68b81-107">A common design pattern in these applications is to track changes made to DocumentDB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="68b81-108">DocumentDB's **Change Feed support** allows you to build efficient and scalable solutions for each of these patterns.</span><span class="sxs-lookup"><span data-stu-id="68b81-108">DocumentDB's **Change Feed support** allows you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="68b81-109">With Change Feed support, DocumentDB provides a sorted list of documents within a DocumentDB collection in the order in which they were modified.</span><span class="sxs-lookup"><span data-stu-id="68b81-109">With Change Feed support, DocumentDB provides a sorted list of documents within a DocumentDB collection in the order in which they were modified.</span></span> <span data-ttu-id="68b81-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span><span class="sxs-lookup"><span data-stu-id="68b81-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="68b81-111">Trigger a call to an API when a document is inserted or modified</span><span class="sxs-lookup"><span data-stu-id="68b81-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="68b81-112">Perform real-time (stream) processing on updates</span><span class="sxs-lookup"><span data-stu-id="68b81-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="68b81-113">Synchronize data with a cache, search engine, or data warehouse</span><span class="sxs-lookup"><span data-stu-id="68b81-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="68b81-114">Changes in DocumentDB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span><span class="sxs-lookup"><span data-stu-id="68b81-114">Changes in DocumentDB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="68b81-115">Let's look at the APIs for Change Feed and how you can use them to build scalable real-time applications.</span><span class="sxs-lookup"><span data-stu-id="68b81-115">Let's look at the APIs for Change Feed and how you can use them to build scalable real-time applications.</span></span>

![Using DocumentDB Change Feed to power real-time analytics and event-driven computing scenarios](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-feed/changefeed.png)

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="68b81-117">Use cases and scenarios</span><span class="sxs-lookup"><span data-stu-id="68b81-117">Use cases and scenarios</span></span>
<span data-ttu-id="68b81-118">Change Feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span><span class="sxs-lookup"><span data-stu-id="68b81-118">Change Feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="68b81-119">For example, you can perform the following tasks efficiently:</span><span class="sxs-lookup"><span data-stu-id="68b81-119">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="68b81-120">Update a cache, search index, or a data warehouse with data stored in Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="68b81-120">Update a cache, search index, or a data warehouse with data stored in Azure DocumentDB.</span></span>
* <span data-ttu-id="68b81-121">Implement application-level data tiering and archival, that is, store "hot data" in DocumentDB, and age out "cold data" to [Azure Blob Storage](../storage/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68b81-121">Implement application-level data tiering and archival, that is, store "hot data" in DocumentDB, and age out "cold data" to [Azure Blob Storage](../storage/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="68b81-122">Implement batch analytics on data using [Apache Hadoop](documentdb-run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="68b81-122">Implement batch analytics on data using [Apache Hadoop](documentdb-run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="68b81-123">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="68b81-123">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with DocumentDB.</span></span> <span data-ttu-id="68b81-124">DocumentDB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span><span class="sxs-lookup"><span data-stu-id="68b81-124">DocumentDB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="68b81-125">Perform zero down-time migrations to another Azure DocumentDB account with a different partitioning scheme.</span><span class="sxs-lookup"><span data-stu-id="68b81-125">Perform zero down-time migrations to another Azure DocumentDB account with a different partitioning scheme.</span></span>

<span data-ttu-id="68b81-126">**Lambda Pipelines with Azure DocumentDB for ingestion and query:**</span><span class="sxs-lookup"><span data-stu-id="68b81-126">**Lambda Pipelines with Azure DocumentDB for ingestion and query:**</span></span>

![Azure DocumentDB based lambda pipeline for ingestion and query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-feed/lambda.png)

<span data-ttu-id="68b81-128">You can use DocumentDB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68b81-128">You can use DocumentDB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="68b81-129">Within web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="68b81-129">Within web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="68b81-130">If you're using DocumentDB to build a game, you can, for example, use Change Feed to implement real-time leaderboards based on scores from completed games.</span><span class="sxs-lookup"><span data-stu-id="68b81-130">If you're using DocumentDB to build a game, you can, for example, use Change Feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-documentdb"></a><span data-ttu-id="68b81-131">How Change Feed works in Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="68b81-131">How Change Feed works in Azure DocumentDB</span></span>
<span data-ttu-id="68b81-132">DocumentDB provides the ability to incrementally read updates made to a DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-132">DocumentDB provides the ability to incrementally read updates made to a DocumentDB collection.</span></span> <span data-ttu-id="68b81-133">This change feed has the following properties:</span><span class="sxs-lookup"><span data-stu-id="68b81-133">This change feed has the following properties:</span></span>

* <span data-ttu-id="68b81-134">Changes are persistent in DocumentDB and can be processed asynchronously.</span><span class="sxs-lookup"><span data-stu-id="68b81-134">Changes are persistent in DocumentDB and can be processed asynchronously.</span></span>
* <span data-ttu-id="68b81-135">Changes to documents within a collection are available immediately in the change feed.</span><span class="sxs-lookup"><span data-stu-id="68b81-135">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="68b81-136">Each change to a document appears only once in the change feed.</span><span class="sxs-lookup"><span data-stu-id="68b81-136">Each change to a document appears only once in the change feed.</span></span> <span data-ttu-id="68b81-137">Only the most recent change for a given document is included in the change log.</span><span class="sxs-lookup"><span data-stu-id="68b81-137">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="68b81-138">Intermediate changes may not be available.</span><span class="sxs-lookup"><span data-stu-id="68b81-138">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="68b81-139">The change feed is sorted by order of modification within each partition key value.</span><span class="sxs-lookup"><span data-stu-id="68b81-139">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="68b81-140">There is no guaranteed order across partition-key values.</span><span class="sxs-lookup"><span data-stu-id="68b81-140">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="68b81-141">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span><span class="sxs-lookup"><span data-stu-id="68b81-141">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="68b81-142">Changes are available in chunks of partition key ranges.</span><span class="sxs-lookup"><span data-stu-id="68b81-142">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="68b81-143">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span><span class="sxs-lookup"><span data-stu-id="68b81-143">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="68b81-144">Applications can request for multiple Change Feeds simultaneously on the same collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-144">Applications can request for multiple Change Feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="68b81-145">DocumentDB's Change Feed is enabled by default for all accounts, and does not incur any additional costs on your account.</span><span class="sxs-lookup"><span data-stu-id="68b81-145">DocumentDB's Change Feed is enabled by default for all accounts, and does not incur any additional costs on your account.</span></span> <span data-ttu-id="68b81-146">You can use your [provisioned throughput](documentdb-request-units.md) in your write region or any [read region](documentdb-distribute-data-globally.md) to read from the change feed, just like any other operation from DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="68b81-146">You can use your [provisioned throughput](documentdb-request-units.md) in your write region or any [read region](documentdb-distribute-data-globally.md) to read from the change feed, just like any other operation from DocumentDB.</span></span> <span data-ttu-id="68b81-147">The change feed includes inserts and update operations made to documents within the collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-147">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="68b81-148">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span><span class="sxs-lookup"><span data-stu-id="68b81-148">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="68b81-149">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](documentdb-time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span><span class="sxs-lookup"><span data-stu-id="68b81-149">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](documentdb-time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="68b81-150">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span><span class="sxs-lookup"><span data-stu-id="68b81-150">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="68b81-151">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span><span class="sxs-lookup"><span data-stu-id="68b81-151">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Distributed processing of DocumentDB change feed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-feed/changefeedvisual.png)

<span data-ttu-id="68b81-153">In the following section, we describe how to access the change feed using the DocumentDB REST API and SDKs.</span><span class="sxs-lookup"><span data-stu-id="68b81-153">In the following section, we describe how to access the change feed using the DocumentDB REST API and SDKs.</span></span> <span data-ttu-id="68b81-154">For .NET applications, we recommend using the [Change feed processor library]() for processing events from the change feed.</span><span class="sxs-lookup"><span data-stu-id="68b81-154">For .NET applications, we recommend using the [Change feed processor library]() for processing events from the change feed.</span></span>

## <a id="rest-apis"></a><span data-ttu-id="68b81-155">Working with the REST API and SDK</span><span class="sxs-lookup"><span data-stu-id="68b81-155">Working with the REST API and SDK</span></span>
<span data-ttu-id="68b81-156">DocumentDB provides elastic containers of storage and throughput called **collections**.</span><span class="sxs-lookup"><span data-stu-id="68b81-156">DocumentDB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="68b81-157">Data within collections is logically grouped using [partition keys](documentdb-partition-data.md) for scalability and performance.</span><span class="sxs-lookup"><span data-stu-id="68b81-157">Data within collections is logically grouped using [partition keys](documentdb-partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="68b81-158">DocumentDB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span><span class="sxs-lookup"><span data-stu-id="68b81-158">DocumentDB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="68b81-159">The change feed can be obtained by populating two new request headers to DocumentDB's `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span><span class="sxs-lookup"><span data-stu-id="68b81-159">The change feed can be obtained by populating two new request headers to DocumentDB's `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="68b81-160">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="68b81-160">ReadDocumentFeed API</span></span>
<span data-ttu-id="68b81-161">Let's take a brief look at how ReadDocumentFeed works.</span><span class="sxs-lookup"><span data-stu-id="68b81-161">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="68b81-162">DocumentDB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="68b81-162">DocumentDB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="68b81-163">For example, the following request returns a page of documents inside the `serverlogs` collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-163">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="68b81-164">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span><span class="sxs-lookup"><span data-stu-id="68b81-164">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="68b81-165">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span><span class="sxs-lookup"><span data-stu-id="68b81-165">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="68b81-166">**Serial Read Document Feed**</span><span class="sxs-lookup"><span data-stu-id="68b81-166">**Serial Read Document Feed**</span></span>

<span data-ttu-id="68b81-167">You can also retrieve the feed of documents using one of the supported [DocumentDB SDKs](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="68b81-167">You can also retrieve the feed of documents using one of the supported [DocumentDB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="68b81-168">For example, the following snippet shows how to perform ReadDocumentFeed in .NET.</span><span class="sxs-lookup"><span data-stu-id="68b81-168">For example, the following snippet shows how to perform ReadDocumentFeed in .NET.</span></span>

    FeedResponse<dynamic> feedResponse = null;
    do
    {
        feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
    }
    while (feedResponse.ResponseContinuation != null);

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="68b81-169">Distributed execution of ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="68b81-169">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="68b81-170">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span><span class="sxs-lookup"><span data-stu-id="68b81-170">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="68b81-171">In order to support these big data scenarios, DocumentDB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span><span class="sxs-lookup"><span data-stu-id="68b81-171">In order to support these big data scenarios, DocumentDB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="68b81-172">**Distributed Read Document Feed**</span><span class="sxs-lookup"><span data-stu-id="68b81-172">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="68b81-173">To provide scalable processing of incremental changes, DocumentDB supports a scale-out model for the change feed API based on ranges of partition keys.</span><span class="sxs-lookup"><span data-stu-id="68b81-173">To provide scalable processing of incremental changes, DocumentDB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="68b81-174">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span><span class="sxs-lookup"><span data-stu-id="68b81-174">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="68b81-175">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span><span class="sxs-lookup"><span data-stu-id="68b81-175">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="68b81-176">Retrieving partition key ranges for a collection</span><span class="sxs-lookup"><span data-stu-id="68b81-176">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="68b81-177">You can retrieve the Partition Key Ranges by requesting the `pkranges` resource within a collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-177">You can retrieve the Partition Key Ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="68b81-178">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span><span class="sxs-lookup"><span data-stu-id="68b81-178">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="68b81-179">This request returns the following response containing metadata about the partition key ranges:</span><span class="sxs-lookup"><span data-stu-id="68b81-179">This request returns the following response containing metadata about the partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="68b81-180">**Partition Key Range Properties**: Each partition key range includes the metadata properties in the following table:</span><span class="sxs-lookup"><span data-stu-id="68b81-180">**Partition Key Range Properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="68b81-181">Header name</span><span class="sxs-lookup"><span data-stu-id="68b81-181">Header name</span></span></th>
        <th><span data-ttu-id="68b81-182">Description</span><span class="sxs-lookup"><span data-stu-id="68b81-182">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="68b81-183">id</span><span class="sxs-lookup"><span data-stu-id="68b81-183">id</span></span></td>
        <td>
            <p><span data-ttu-id="68b81-184">The ID for the partition key range.</span><span class="sxs-lookup"><span data-stu-id="68b81-184">The ID for the partition key range.</span></span> <span data-ttu-id="68b81-185">This is a stable and unique ID within each collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-185">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="68b81-186">Must be used in the following call to read changes by partition key range.</span><span class="sxs-lookup"><span data-stu-id="68b81-186">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="68b81-187">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="68b81-187">maxExclusive</span></span></td>
        <td><span data-ttu-id="68b81-188">The maximum partition key hash value for the partition key range.</span><span class="sxs-lookup"><span data-stu-id="68b81-188">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="68b81-189">For internal use.</span><span class="sxs-lookup"><span data-stu-id="68b81-189">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="68b81-190">minInclusive</span><span class="sxs-lookup"><span data-stu-id="68b81-190">minInclusive</span></span></td>
        <td><span data-ttu-id="68b81-191">The minimum partition key hash value for the partition key range.</span><span class="sxs-lookup"><span data-stu-id="68b81-191">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="68b81-192">For internal use.</span><span class="sxs-lookup"><span data-stu-id="68b81-192">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="68b81-193">You can do this using one of the supported [DocumentDB SDKs](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="68b81-193">You can do this using one of the supported [DocumentDB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="68b81-194">For example, the following snippet shows how to retrieve partition key ranges in .NET.</span><span class="sxs-lookup"><span data-stu-id="68b81-194">For example, the following snippet shows how to retrieve partition key ranges in .NET.</span></span>

    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

<span data-ttu-id="68b81-195">DocumentDB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span><span class="sxs-lookup"><span data-stu-id="68b81-195">DocumentDB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="68b81-196">Performing an incremental ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="68b81-196">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="68b81-197">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in DocumentDB collections:</span><span class="sxs-lookup"><span data-stu-id="68b81-197">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in DocumentDB collections:</span></span>

* <span data-ttu-id="68b81-198">Read all changes to documents from the beginning, that is, from collection creation.</span><span class="sxs-lookup"><span data-stu-id="68b81-198">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="68b81-199">Read all changes to future updates to documents from current time.</span><span class="sxs-lookup"><span data-stu-id="68b81-199">Read all changes to future updates to documents from current time.</span></span>
* <span data-ttu-id="68b81-200">Read all changes to documents from a logical version of the collection (ETag).</span><span class="sxs-lookup"><span data-stu-id="68b81-200">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="68b81-201">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span><span class="sxs-lookup"><span data-stu-id="68b81-201">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="68b81-202">The changes include inserts and updates to documents.</span><span class="sxs-lookup"><span data-stu-id="68b81-202">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="68b81-203">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](documentdb-time-to-live.md) to signal a pending deletion in the change feed.</span><span class="sxs-lookup"><span data-stu-id="68b81-203">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](documentdb-time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="68b81-204">The following table lists the request and response headers for ReadDocumentFeed operations.</span><span class="sxs-lookup"><span data-stu-id="68b81-204">The following table lists the request and response headers for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="68b81-205">**Request Headers for incremental ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="68b81-205">**Request Headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="68b81-206">Header name</span><span class="sxs-lookup"><span data-stu-id="68b81-206">Header name</span></span></th>
        <th><span data-ttu-id="68b81-207">Description</span><span class="sxs-lookup"><span data-stu-id="68b81-207">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="68b81-208">A-IM</span><span class="sxs-lookup"><span data-stu-id="68b81-208">A-IM</span></span></td>
        <td><span data-ttu-id="68b81-209">Must be set to "Incremental feed", or omitted otherwise</span><span class="sxs-lookup"><span data-stu-id="68b81-209">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="68b81-210">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="68b81-210">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="68b81-211">No header: returns all changes from the beginning (collection creation)</span><span class="sxs-lookup"><span data-stu-id="68b81-211">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="68b81-212">"\*": returns all new changes to data within the collection</span><span class="sxs-lookup"><span data-stu-id="68b81-212">"\*": returns all new changes to data within the collection</span></span></p>
            <p><span data-ttu-id="68b81-213">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span><span class="sxs-lookup"><span data-stu-id="68b81-213">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="68b81-214">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="68b81-214">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="68b81-215">The partition key range ID for reading data.</span><span class="sxs-lookup"><span data-stu-id="68b81-215">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="68b81-216">**Response Headers for incremental ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="68b81-216">**Response Headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="68b81-217">Header name</span><span class="sxs-lookup"><span data-stu-id="68b81-217">Header name</span></span></th>
        <th><span data-ttu-id="68b81-218">Description</span><span class="sxs-lookup"><span data-stu-id="68b81-218">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="68b81-219">etag</span><span class="sxs-lookup"><span data-stu-id="68b81-219">etag</span></span></td>
        <td>
            <p><span data-ttu-id="68b81-220">The logical sequence number (LSN) of last document returned in the response.</span><span class="sxs-lookup"><span data-stu-id="68b81-220">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="68b81-221">incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="68b81-221">incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="68b81-222">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span><span class="sxs-lookup"><span data-stu-id="68b81-222">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="68b81-223">Changes are ordered by time within each partition key value within the partition key range.</span><span class="sxs-lookup"><span data-stu-id="68b81-223">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="68b81-224">There is no guaranteed order across partition-key values.</span><span class="sxs-lookup"><span data-stu-id="68b81-224">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="68b81-225">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span><span class="sxs-lookup"><span data-stu-id="68b81-225">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="68b81-226">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span><span class="sxs-lookup"><span data-stu-id="68b81-226">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="68b81-227">With Change Feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span><span class="sxs-lookup"><span data-stu-id="68b81-227">With Change Feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="68b81-228">The .NET SDK provides the [CreateDocumentChangeFeedQuery](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) and [ChangeFeedOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.changefeedoptions.aspx) helper classes to access changes made to a collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-228">The .NET SDK provides the [CreateDocumentChangeFeedQuery](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) and [ChangeFeedOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.changefeedoptions.aspx) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="68b81-229">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span><span class="sxs-lookup"><span data-stu-id="68b81-229">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

    private async Task<Dictionary<string, string>> GetChanges(
        DocumentClient client,
        string collection,
        Dictionary<string, string> checkpoints)
    {
        string pkRangesResponseContinuation = null;
        List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

        do
        {
            FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
                collectionUri, 
                new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

            partitionKeyRanges.AddRange(pkRangesResponse);
            pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
        }
        while (pkRangesResponseContinuation != null);

        foreach (PartitionKeyRange pkRange in partitionKeyRanges)
        {
            string continuation = null;
            checkpoints.TryGetValue(pkRange.Id, out continuation);

            IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
                collection,
                new ChangeFeedOptions
                {
                    PartitionKeyRangeId = pkRange.Id,
                    StartFromBeginning = true,
                    RequestContinuation = continuation,
                    MaxItemCount = 1
                });

            while (query.HasMoreResults)
            {
                FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

                foreach (DeviceReading changedDocument in readChangesResponse)
                {
                    Console.WriteLine(changedDocument.Id);
                }

                checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
            }
        }

        return checkpoints;
    }

<span data-ttu-id="68b81-230">And the following snippet shows how to process changes in real-time with DocumentDB by using the Change Feed support and the preceding function.</span><span class="sxs-lookup"><span data-stu-id="68b81-230">And the following snippet shows how to process changes in real-time with DocumentDB by using the Change Feed support and the preceding function.</span></span> <span data-ttu-id="68b81-231">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span><span class="sxs-lookup"><span data-stu-id="68b81-231">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

    // Returns all documents in the collection.
    Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

    await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
    await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

    // Returns only the two documents created above.
    checkpoints = await GetChanges(client, collection, checkpoints);


<span data-ttu-id="68b81-232">You can also filter the change feed using client side logic to selectively process events.</span><span class="sxs-lookup"><span data-stu-id="68b81-232">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="68b81-233">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span><span class="sxs-lookup"><span data-stu-id="68b81-233">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

    FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

    foreach (DeviceReading changedDocument in 
        readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
    {
        // trigger an action, like call an API
    }

## <a id="change-feed-processor"></a><span data-ttu-id="68b81-234">Change feed processor library</span><span class="sxs-lookup"><span data-stu-id="68b81-234">Change feed processor library</span></span>
<span data-ttu-id="68b81-235">The [DocumentDB change feed processor library](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/ChangeFeedProcessor) can be used to distribute event processing from the change feed across multiple consumers.</span><span class="sxs-lookup"><span data-stu-id="68b81-235">The [DocumentDB change feed processor library](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/ChangeFeedProcessor) can be used to distribute event processing from the change feed across multiple consumers.</span></span> <span data-ttu-id="68b81-236">You should use this implementation when building change feed readers on the .NET platform.</span><span class="sxs-lookup"><span data-stu-id="68b81-236">You should use this implementation when building change feed readers on the .NET platform.</span></span> <span data-ttu-id="68b81-237">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span><span class="sxs-lookup"><span data-stu-id="68b81-237">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span>

<span data-ttu-id="68b81-238">To use the [`ChangeFeedProcessorHost`](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/ChangeFeedProcessor/DocumentDB.ChangeFeedProcessor/ChangeFeedEventHost.cs) class, you can implement [`IChangeFeedObserver`](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/ChangeFeedProcessor/DocumentDB.ChangeFeedProcessor/IChangeFeedObserver.cs).</span><span class="sxs-lookup"><span data-stu-id="68b81-238">To use the [`ChangeFeedProcessorHost`](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/ChangeFeedProcessor/DocumentDB.ChangeFeedProcessor/ChangeFeedEventHost.cs) class, you can implement [`IChangeFeedObserver`](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/ChangeFeedProcessor/DocumentDB.ChangeFeedProcessor/IChangeFeedObserver.cs).</span></span> <span data-ttu-id="68b81-239">This interface contains three methods:</span><span class="sxs-lookup"><span data-stu-id="68b81-239">This interface contains three methods:</span></span>

* <span data-ttu-id="68b81-240">OpenAsync</span><span class="sxs-lookup"><span data-stu-id="68b81-240">OpenAsync</span></span>
* <span data-ttu-id="68b81-241">CloseAsync</span><span class="sxs-lookup"><span data-stu-id="68b81-241">CloseAsync</span></span>
* <span data-ttu-id="68b81-242">ProcessEventsAsync</span><span class="sxs-lookup"><span data-stu-id="68b81-242">ProcessEventsAsync</span></span>

<span data-ttu-id="68b81-243">To start event processing, instantiate ChangeFeedProcessorHost, providing the appropriate parameters for your DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-243">To start event processing, instantiate ChangeFeedProcessorHost, providing the appropriate parameters for your DocumentDB collection.</span></span> <span data-ttu-id="68b81-244">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` implementation with the runtime.</span><span class="sxs-lookup"><span data-stu-id="68b81-244">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` implementation with the runtime.</span></span> <span data-ttu-id="68b81-245">At this point, the host will attempt to acquire a lease on every partition key range in the DocumentDB collection using a "greedy" algorithm.</span><span class="sxs-lookup"><span data-stu-id="68b81-245">At this point, the host will attempt to acquire a lease on every partition key range in the DocumentDB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="68b81-246">These leases will last for a given timeframe and must then be renewed.</span><span class="sxs-lookup"><span data-stu-id="68b81-246">These leases will last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="68b81-247">As new nodes, worker instances in this case, come online, they place lease reservations and over time the load shifts between nodes as each attempts to acquire more leases.</span><span class="sxs-lookup"><span data-stu-id="68b81-247">As new nodes, worker instances in this case, come online, they place lease reservations and over time the load shifts between nodes as each attempts to acquire more leases.</span></span>

![Using the DocumentDB change feed processor host](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-feed/changefeedprocessor.png)

<span data-ttu-id="68b81-249">Over time, an equilibrium is established.</span><span class="sxs-lookup"><span data-stu-id="68b81-249">Over time, an equilibrium is established.</span></span> <span data-ttu-id="68b81-250">This dynamic capability enables CPU-based autoscaling to be applied to consumers for both scale-up and scale-down.</span><span class="sxs-lookup"><span data-stu-id="68b81-250">This dynamic capability enables CPU-based autoscaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="68b81-251">If changes are available in DocumentDB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span><span class="sxs-lookup"><span data-stu-id="68b81-251">If changes are available in DocumentDB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

<span data-ttu-id="68b81-252">The `ChangeFeedProcessorHost` class also implements an checkpointing mechanism using a separate DocumentDB leases collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-252">The `ChangeFeedProcessorHost` class also implements an checkpointing mechanism using a separate DocumentDB leases collection.</span></span> <span data-ttu-id="68b81-253">This mechanism stores the offset on a per-partition basis, so that each consumer can determine what the last checkpoint from the previous consumer was.</span><span class="sxs-lookup"><span data-stu-id="68b81-253">This mechanism stores the offset on a per-partition basis, so that each consumer can determine what the last checkpoint from the previous consumer was.</span></span> <span data-ttu-id="68b81-254">As partitions transition between nodes via leases, this is the synchronization mechanism that facilitates load shifting.</span><span class="sxs-lookup"><span data-stu-id="68b81-254">As partitions transition between nodes via leases, this is the synchronization mechanism that facilitates load shifting.</span></span>


<span data-ttu-id="68b81-255">Here's a code snippet for a simple change feed processor host that prints changes to the console:</span><span class="sxs-lookup"><span data-stu-id="68b81-255">Here's a code snippet for a simple change feed processor host that prints changes to the console:</span></span>

```cs
    class DocumentFeedObserver : IChangeFeedObserver
    {
        private static int s_totalDocs = 0;
        public Task OpenAsync(ChangeFeedObserverContext context)
        {
            Console.WriteLine("Worker opened, {0}", context.PartitionKeyRangeId);
            return Task.CompletedTask;  // Requires targeting .NET 4.6+.
        }
        public Task CloseAsync(ChangeFeedObserverContext context, ChangeFeedObserverCloseReason reason)
        {
            Console.WriteLine("Worker closed, {0}", context.PartitionKeyRangeId);
            return Task.CompletedTask;
        }
        public Task ProcessEventsAsync(IReadOnlyList<Document> docs, ChangeFeedObserverContext context)
        {
            Console.WriteLine("Change feed: total {0} doc(s)", Interlocked.Add(ref s_totalDocs, docs.Count));
            return Task.CompletedTask;
        }
    }
```

<span data-ttu-id="68b81-256">The following code snippet shows how to register a new host to listen to changes from a DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="68b81-256">The following code snippet shows how to register a new host to listen to changes from a DocumentDB collection.</span></span> <span data-ttu-id="68b81-257">Here, we configure a separate collection to manage the leases to partitions across multiple consumers:</span><span class="sxs-lookup"><span data-stu-id="68b81-257">Here, we configure a separate collection to manage the leases to partitions across multiple consumers:</span></span>

```cs
    string hostName = Guid.NewGuid().ToString();
    DocumentCollectionInfo documentCollectionLocation = new DocumentCollectionInfo
    {
        Uri = new Uri("https://YOUR_SERVICE.documents.azure.com:443/"),
        MasterKey = "YOUR_SECRET_KEY==",
        DatabaseName = "db1",
        CollectionName = "documents"
    };

    DocumentCollectionInfo leaseCollectionLocation = new DocumentCollectionInfo
    {
        Uri = new Uri("https://YOUR_SERVICE.documents.azure.com:443/"),
        MasterKey = "YOUR_SECRET_KEY==",
        DatabaseName = "db1",
        CollectionName = "leases"
    };

    ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation);
    await host.RegisterObserverAsync<DocumentFeedObserver>();
```

<span data-ttu-id="68b81-258">In this article, we provided a walkthrough of DocumentDB's Change Feed support, and how to track changes made to DocumentDB data using the DocumentDB REST API and/or SDKs.</span><span class="sxs-lookup"><span data-stu-id="68b81-258">In this article, we provided a walkthrough of DocumentDB's Change Feed support, and how to track changes made to DocumentDB data using the DocumentDB REST API and/or SDKs.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="68b81-259">Next steps</span><span class="sxs-lookup"><span data-stu-id="68b81-259">Next steps</span></span>
* <span data-ttu-id="68b81-260">Try the [DocumentDB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="68b81-260">Try the [DocumentDB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="68b81-261">Learn more about [DocumentDB's resource model and hierarchy](documentdb-resources.md)</span><span class="sxs-lookup"><span data-stu-id="68b81-261">Learn more about [DocumentDB's resource model and hierarchy](documentdb-resources.md)</span></span>
* <span data-ttu-id="68b81-262">Get started coding with the [DocumentDB SDKs](documentdb-sdk-dotnet.md) or the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx)</span><span class="sxs-lookup"><span data-stu-id="68b81-262">Get started coding with the [DocumentDB SDKs](documentdb-sdk-dotnet.md) or the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx)</span></span>




