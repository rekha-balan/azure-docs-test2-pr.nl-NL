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
# <a name="working-with-the-change-feed-support-in-azure-documentdb"></a>Working with the Change Feed support in Azure DocumentDB
[Azure DocumentDB](documentdb-introduction.md) is a fast and flexible NoSQL database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes. This makes it well-suited for IoT, gaming, retail, and operational logging applications. A common design pattern in these applications is to track changes made to DocumentDB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes. DocumentDB's **Change Feed support** allows you to build efficient and scalable solutions for each of these patterns.

With Change Feed support, DocumentDB provides a sorted list of documents within a DocumentDB collection in the order in which they were modified. This feed can be used to listen for modifications to data within the collection and perform actions such as:

* Trigger a call to an API when a document is inserted or modified
* Perform real-time (stream) processing on updates
* Synchronize data with a cache, search engine, or data warehouse

Changes in DocumentDB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing. Let's look at the APIs for Change Feed and how you can use them to build scalable real-time applications.

![Using DocumentDB Change Feed to power real-time analytics and event-driven computing scenarios](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-feed/changefeed.png)

## <a name="use-cases-and-scenarios"></a>Use cases and scenarios
Change Feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed. For example, you can perform the following tasks efficiently:

* Update a cache, search index, or a data warehouse with data stored in Azure DocumentDB.
* Implement application-level data tiering and archival, that is, store "hot data" in DocumentDB, and age out "cold data" to [Azure Blob Storage](../storage/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).
* Implement batch analytics on data using [Apache Hadoop](documentdb-run-hadoop-with-hdinsight.md).
* Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with DocumentDB. DocumentDB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO. 
* Perform zero down-time migrations to another Azure DocumentDB account with a different partitioning scheme.

**Lambda Pipelines with Azure DocumentDB for ingestion and query:**

![Azure DocumentDB based lambda pipeline for ingestion and query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-feed/lambda.png)

You can use DocumentDB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

Within web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/). If you're using DocumentDB to build a game, you can, for example, use Change Feed to implement real-time leaderboards based on scores from completed games.

## <a name="how-change-feed-works-in-azure-documentdb"></a>How Change Feed works in Azure DocumentDB
DocumentDB provides the ability to incrementally read updates made to a DocumentDB collection. This change feed has the following properties:

* Changes are persistent in DocumentDB and can be processed asynchronously.
* Changes to documents within a collection are available immediately in the change feed.
* Each change to a document appears only once in the change feed. Only the most recent change for a given document is included in the change log. Intermediate changes may not be available.
* The change feed is sorted by order of modification within each partition key value. There is no guaranteed order across partition-key values.
* Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.
* Changes are available in chunks of partition key ranges. This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.
* Applications can request for multiple Change Feeds simultaneously on the same collection.

DocumentDB's Change Feed is enabled by default for all accounts, and does not incur any additional costs on your account. You can use your [provisioned throughput](documentdb-request-units.md) in your write region or any [read region](documentdb-distribute-data-globally.md) to read from the change feed, just like any other operation from DocumentDB. The change feed includes inserts and update operations made to documents within the collection. You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes. Alternatively, you can set a finite expiration period for your documents via the [TTL capability](documentdb-time-to-live.md), for example, 24 hours and use the value of that property to capture deletes. With this solution, you have to process changes within a shorter time interval than the TTL expiration period. The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing. 

![Distributed processing of DocumentDB change feed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-feed/changefeedvisual.png)

In the following section, we describe how to access the change feed using the DocumentDB REST API and SDKs. For .NET applications, we recommend using the [Change feed processor library]() for processing events from the change feed.

## <a id="rest-apis"></a>Working with the REST API and SDK
DocumentDB provides elastic containers of storage and throughput called **collections**. Data within collections is logically grouped using [partition keys](documentdb-partition-data.md) for scalability and performance. DocumentDB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans). The change feed can be obtained by populating two new request headers to DocumentDB's `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed API
Let's take a brief look at how ReadDocumentFeed works. DocumentDB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API. For example, the following request returns a page of documents inside the `serverlogs` collection. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response. When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially. 

**Serial Read Document Feed**

You can also retrieve the feed of documents using one of the supported [DocumentDB SDKs](documentdb-sdk-dotnet.md). For example, the following snippet shows how to perform ReadDocumentFeed in .NET.

    FeedResponse<dynamic> feedResponse = null;
    do
    {
        feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
    }
    while (feedResponse.ResponseContinuation != null);

### <a name="distributed-execution-of-readdocumentfeed"></a>Distributed execution of ReadDocumentFeed
For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical. In order to support these big data scenarios, DocumentDB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers. 

**Distributed Read Document Feed**

To provide scalable processing of incremental changes, DocumentDB supports a scale-out model for the change feed API based on ranges of partition keys.

* You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call. 
* For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Retrieving partition key ranges for a collection
You can retrieve the Partition Key Ranges by requesting the `pkranges` resource within a collection. For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

This request returns the following response containing metadata about the partition key ranges:

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


**Partition Key Range Properties**: Each partition key range includes the metadata properties in the following table:

<table>
    <tr>
        <th>Header name</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>The ID for the partition key range. This is a stable and unique ID within each collection.</p>
            <p>Must be used in the following call to read changes by partition key range.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>The maximum partition key hash value for the partition key range. For internal use.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>The minimum partition key hash value for the partition key range. For internal use.</td>
    </tr>       
</table>

You can do this using one of the supported [DocumentDB SDKs](documentdb-sdk-dotnet.md). For example, the following snippet shows how to retrieve partition key ranges in .NET.

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

DocumentDB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Performing an incremental ReadDocumentFeed
ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in DocumentDB collections:

* Read all changes to documents from the beginning, that is, from collection creation.
* Read all changes to future updates to documents from current time.
* Read all changes to documents from a logical version of the collection (ETag). You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.

The changes include inserts and updates to documents. To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](documentdb-time-to-live.md) to signal a pending deletion in the change feed.

The following table lists the request and response headers for ReadDocumentFeed operations.

**Request Headers for incremental ReadDocumentFeed**:

<table>
    <tr>
        <th>Header name</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>A-IM</td>
        <td>Must be set to "Incremental feed", or omitted otherwise</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>No header: returns all changes from the beginning (collection creation)</p>
            <p>"*": returns all new changes to data within the collection</p>
            <p>&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</p>
        </td>
    </tr>
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>The partition key range ID for reading data.</td>
    </tr>
</table>

**Response Headers for incremental ReadDocumentFeed**:

<table>
    <tr>
        <th>Header name</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>etag</td>
        <td>
            <p>The logical sequence number (LSN) of last document returned in the response.</p>
            <p>incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</p>
        </td>
    </tr>
</table>

Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:

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

Changes are ordered by time within each partition key value within the partition key range. There is no guaranteed order across partition-key values. If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response. If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.

> [!NOTE]
> With Change Feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers. 

The .NET SDK provides the [CreateDocumentChangeFeedQuery](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) and [ChangeFeedOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.changefeedoptions.aspx) helper classes to access changes made to a collection. The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.

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

And the following snippet shows how to process changes in real-time with DocumentDB by using the Change Feed support and the preceding function. The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.

    // Returns all documents in the collection.
    Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

    await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
    await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

    // Returns only the two documents created above.
    checkpoints = await GetChanges(client, collection, checkpoints);


You can also filter the change feed using client side logic to selectively process events. For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.

    FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

    foreach (DeviceReading changedDocument in 
        readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
    {
        // trigger an action, like call an API
    }

## <a id="change-feed-processor"></a>Change feed processor library
The [DocumentDB change feed processor library](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/ChangeFeedProcessor) can be used to distribute event processing from the change feed across multiple consumers. You should use this implementation when building change feed readers on the .NET platform. The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.

To use the [`ChangeFeedProcessorHost`](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/ChangeFeedProcessor/DocumentDB.ChangeFeedProcessor/ChangeFeedEventHost.cs) class, you can implement [`IChangeFeedObserver`](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/ChangeFeedProcessor/DocumentDB.ChangeFeedProcessor/IChangeFeedObserver.cs). This interface contains three methods:

* OpenAsync
* CloseAsync
* ProcessEventsAsync

To start event processing, instantiate ChangeFeedProcessorHost, providing the appropriate parameters for your DocumentDB collection. Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` implementation with the runtime. At this point, the host will attempt to acquire a lease on every partition key range in the DocumentDB collection using a "greedy" algorithm. These leases will last for a given timeframe and must then be renewed. As new nodes, worker instances in this case, come online, they place lease reservations and over time the load shifts between nodes as each attempts to acquire more leases.

![Using the DocumentDB change feed processor host](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-feed/changefeedprocessor.png)

Over time, an equilibrium is established. This dynamic capability enables CPU-based autoscaling to be applied to consumers for both scale-up and scale-down. If changes are available in DocumentDB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.

The `ChangeFeedProcessorHost` class also implements an checkpointing mechanism using a separate DocumentDB leases collection. This mechanism stores the offset on a per-partition basis, so that each consumer can determine what the last checkpoint from the previous consumer was. As partitions transition between nodes via leases, this is the synchronization mechanism that facilitates load shifting.


Here's a code snippet for a simple change feed processor host that prints changes to the console:

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

The following code snippet shows how to register a new host to listen to changes from a DocumentDB collection. Here, we configure a separate collection to manage the leases to partitions across multiple consumers:

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

In this article, we provided a walkthrough of DocumentDB's Change Feed support, and how to track changes made to DocumentDB data using the DocumentDB REST API and/or SDKs. 

## <a name="next-steps"></a>Next steps
* Try the [DocumentDB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Learn more about [DocumentDB's resource model and hierarchy](documentdb-resources.md)
* Get started coding with the [DocumentDB SDKs](documentdb-sdk-dotnet.md) or the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx)




