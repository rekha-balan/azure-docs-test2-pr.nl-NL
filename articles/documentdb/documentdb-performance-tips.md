---
title: Performance tips - Azure DocumentDB NoSQL | Microsoft Docs
description: Learn client configuration options to improve Azure DocumentDB database performance
keywords: how to improve database performance
services: documentdb
author: mimig1
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: f1897bebceaf8e4e50a703adf7b4b707bd6fce05
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564092"
---
# <a name="performance-tips-for-documentdb"></a>Performance tips for DocumentDB
Azure DocumentDB is a fast and flexible distributed database that scales seamlessly with guaranteed latency and throughput. You do not have to make major architecture changes or write complex code to scale your database with DocumentDB. Scaling up and down is as easy as making a single API call or [SDK method call](documentdb-set-throughput.md#set-throughput-sdk). However, because DocumentDB is accessed via network calls there are client-side optimizations you can make to achieve peak performance.

So if you're asking "How can I improve my database performance?" consider the following options:

## <a name="networking"></a>Networking
<a id="direct-connection"></a>

1. **Connection policy: Use direct connection mode**

    How a client connects to Azure DocumentDB has important implications on performance, especially in terms of observed client-side latency. There are two key configuration settings available for configuring client Connection Policy – the connection *mode* and the [connection *protocol*](#connection-protocol).  The two available modes are:

   1. Gateway Mode (default)
   2. Direct Mode

      Gateway Mode is supported on all SDK platforms and is the configured default.  If your application runs within a corporate network with strict firewall restrictions, Gateway Mode is the best choice since it uses the standard HTTPS port and a single endpoint. The performance tradeoff, however, is that Gateway Mode involves an additional network hop every time data is read or written to DocumentDB. Because of this, Direct Mode offers better performance due to fewer network hops.
<a id="use-tcp"></a>
2. **Connection policy: Use the TCP protocol**

    When using Direct Mode, there are two protocol options available:

   * TCP
   * HTTPS

     DocumentDB offers a simple and open RESTful programming model over HTTPS. Additionally, it offers an efficient TCP protocol, which is also RESTful in its communication model and is available through the .NET client SDK. Both Direct TCP and HTTPS use SSL for initial authentication and encrypting traffic. For best performance, use the TCP protocol when possible.

     When using TCP in Gateway Mode, TCP Port 443 is the DocumentDB port, and 10250 is the MongoDB API port. When using TCP in Direct Mode, in addition to the Gateway ports, you need to ensure the port range between 10000 and 20000 is open because DocumentDB uses dynamic TCP ports. If these ports are not open and you attempt to use TCP, you receive a 503 Service Unavailable error.

     The Connectivity Mode is configured during the construction of the DocumentClient instance with the ConnectionPolicy parameter. If Direct Mode is used, the Protocol can also be set within the ConnectionPolicy parameter.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from the Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    Because TCP is only supported in Direct Mode, if Gateway Mode is used, then the HTTPS protocol is always used to communicate with the Gateway and the Protocol value in the ConnectionPolicy is ignored.

    ![Illustration of the DocumentDB connection policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-performance-tips/azure-documentdb-connection-policy.png)

3. **Call OpenAsync to avoid startup latency on first request**

    By default, the first request has a higher latency because it has to fetch the address routing table. To avoid this startup latency on the first request, you should call OpenAsync() once during initialization as follows.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Collocate clients in same Azure region for performance**

    When possible, place any applications calling DocumentDB in the same region as the DocumentDB database. For an approximate comparison, calls to DocumentDB within the same region complete within 1-2 ms, but the latency between the West and East coast of the US is >50 ms. This latency can likely vary from request to request depending on the route taken by the request as it passes from the client to the Azure datacenter boundary. The lowest possible latency is achieved by ensuring the calling application is located within the same Azure region as the provisioned DocumentDB endpoint. For a list of available regions, see [Azure Regions](https://azure.microsoft.com/regions/#services).

    ![Illustration of the DocumentDB connection policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-performance-tips/azure-documentdb-same-region.png)
   <a id="increase-threads"></a>
5. **Increase number of threads/tasks**

    Since calls to DocumentDB are made over the network, you may need to vary the degree of parallelism of your requests so that the client application spends very little time waiting between requests. For example, if you're using .NET's [Task Parallel Library](https://msdn.microsoft.com//library/dd460717.aspx), create in the order of 100s of Tasks reading or writing to DocumentDB.

## <a name="sdk-usage"></a>SDK Usage
1. **Install the most recent SDK**

    The DocumentDB SDKs are constantly being improved to provide the best performance. See the [DocumentDB SDK](documentdb-sdk-dotnet.md) pages to determine the most recent SDK and review improvements.
2. **Use a singleton DocumentDB client for the lifetime of your application**

    Note that each DocumentClient instance is thread-safe and performs efficient connection management and address caching when operating in Direct Mode. To allow efficient connection management and better performance by DocumentClient, it is recommended to use a single instance of DocumentClient per AppDomain for the lifetime of the application.

   <a id="max-connection"></a>
3. **Increase System.Net MaxConnections per host when using Gateway mode**

    DocumentDB requests are made over HTTPS/REST when using Gateway mode, and are subjected to the default connection limit per hostname or IP address. You may need to set the MaxConnections to a higher value (100-1000) so that the client library can utilize multiple simultaneous connections to DocumentDB. In the .NET SDK 1.8.0 and above, the default value for [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) is 50 and to change the value, you can set the [Documents.Client.ConnectionPolicy.MaxConnectionLimit](https://msdn.microsoft.com/en-us/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) to a higher value.   
4. **Tuning parallel queries for partitioned collections**

     DocumentDB .NET SDK version 1.9.0 and above support parallel queries, which enable you to query a partitioned collection in parallel (see [Working with the SDKs](documentdb-partition-data.md#working-with-the-documentdb-sdks) and the related [code samples](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) for more info). Parallel queries are designed to improve query latency and throughput over their serial counterpart. Parallel queries provide two parameters that users can tune to custom-fit their requirements, (a) MaxDegreeOfParallelism: to control the maximum number of partitions then can be queried in parallel, and (b) MaxBufferedItemCount: to control the number of pre-fetched results.

    (a) ***Tuning MaxDegreeOfParallelism\:*** Parallel query works by querying multiple partitions in parallel. However, data from an individual partitioned collect is fetched serially with respect to the query. So, setting the MaxDegreeOfParallelism to the number of partitions has the maximum chance of achieving the most performant query, provided all other system conditions remain the same. If you don't know the number of partitions, you can set the MaxDegreeOfParallelism to a high number, and the system chooses the minimum (number of partitions, user provided input) as the MaxDegreeOfParallelism.

    It is important to note that parallel queries produce the best benefits if the data is evenly distributed across all partitions with respect to the query. If the partitioned collection is partitioned such a way that all or a majority of the data returned by a query is concentrated in a few partitions (one partition in worst case), then the performance of the query would be bottlenecked by those partitions.

    (b) ***Tuning MaxBufferedItemCount\:*** Parallel query is designed to pre-fetch results while the current batch of results is being processed by the client. The pre-fetching helps in overall latency improvement of a query. MaxBufferedItemCount is the parameter to limit the number of pre-fetched results. Setting MaxBufferedItemCount to the expected number of results returned (or a higher number) allows the query to receive maximum benefit from pre-fetching.

    Note that pre-fetching works the same way irrespective of the MaxDegreeOfParallelism, and there is a single buffer for the data from all partitions.  
5. **Turn on server-side GC**

    Reducing the frequency of garbage collection may help in some cases. In .NET, set [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) to true.
6. **Implement backoff at RetryAfter intervals**

    During performance testing, you should increase load until a small rate of requests get throttled. If throttled, the client application should backoff on throttle for the server-specified retry interval. Respecting the backoff ensures that you spend minimal amount of time waiting between retries. Retry policy support is included in Version 1.8.0 and above of the DocumentDB [.NET](documentdb-sdk-dotnet.md) and [Java](documentdb-sdk-java.md), version 1.9.0 and above of the [Node.js](documentdb-sdk-node.md) and [Python](documentdb-sdk-python.md), and all supported versions of the [.NET Core](documentdb-sdk-dotnet-core.md) SDKs. For more information, see [Exceeding reserved throughput limits](documentdb-request-units.md#RequestRateTooLarge) and [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **Scale out your client-workload**

    If you are testing at high throughput levels (>50,000 RU/s), the client application may become the bottleneck due to the machine capping out on CPU or Network utilization. If you reach this point, you can continue to push the DocumentDB account further by scaling out your client applications across multiple servers.
8. **Cache document URIs for lower read latency**

    Cache document URIs whenever possible for the best read performance.
   <a id="tune-page-size"></a>
9. **Tune the page size for queries/read feeds for better performance**

    When performing a bulk read of documents using read feed functionality (for example, ReadDocumentFeedAsync) or when issuing a DocumentDB SQL query, the results are returned in a segmented fashion if the result set is too large. By default, results are returned in chunks of 100 items or 1 MB, whichever limit is hit first.

    To reduce the number of network round trips required to retrieve all applicable results, you can increase the page size using x-ms-max-item-count request header to up to 1000. In cases where you need to display only a few results, for example, if your user interface or application API returns only 10 results a time, you can also decrease the page size to 10 to reduce the throughput consumed for reads and queries.

    You may also set the page size using the available DocumentDB SDKs.  For example:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **Increase number of threads/tasks**

    See [Increase number of threads/tasks](#increase-threads) in the Networking section.

11. **Use 64-bit host processing**

    The DocumentDB SDK works in a 32-bit host process when you are using DocumentDB .NET SDK version 1.11.4 and above. However, if you are using cross partition queries, 64-bit host processing is recommended for improved performance. The following types of applications have 32-bit host process as the default, so in order to change that to 64-bit, follow these steps based on the type of your application:

    - For Executable applications, this can be done by unchecking the **Prefer 32-bit** option in the **Project Properties** window, on the **Build** tab.

    - For VSTest based test projects, this can be done by selecting **Test**->**Test Settings**->**Default Processor Architecture as X64**, from the **Visual Studio Test** menu option.

    - For locally deployed ASP.NET Web applications, this can be done by checking the **Use the 64-bit version of IIS Express for web sites and projects**, under **Tools**->**Options**->**Projects and Solutions**->**Web Projects**.

    - For ASP.NET Web applications deployed on Azure, this can be done by choosing the **Platform as 64-bit** in the **Application Settings** on the Azure portal.

## <a name="indexing-policy"></a>Indexing Policy
1. **Use lazy indexing for faster peak time ingestion rates**

    DocumentDB allows you to specify – at the collection level – an indexing policy, which enables you to choose if you want the documents in a collection to be automatically indexed or not.  In addition, you may also choose between synchronous (Consistent) and asynchronous (Lazy) index updates. By default, the index is updated synchronously on each insert, replace, or delete of a document to the collection. Synchronously mode enables the queries to honor the same [consistency level](documentdb-consistency-levels.md) as that of the document reads without any delay for the index to “catch up".

    Lazy indexing may be considered for scenarios in which data is written in bursts, and you want to amortize the work required to index content over a longer period of time. Lazy indexing also allows you to use your provisioned throughput effectively and serve write requests at peak times with minimal latency. It is important to note, however, that when lazy indexing is enabled, query results are eventually consistent regardless of the consistency level configured for the DocumentDB account.

    Hence, Consistent indexing mode (IndexingPolicy.IndexingMode is set to Consistent) incurs the highest request unit charge per write, while Lazy indexing mode (IndexingPolicy.IndexingMode is set to Lazy) and no indexing (IndexingPolicy.Automatic is set to False) have zero indexing cost at the time of write.
2. **Exclude unused paths from indexing for faster writes**

    DocumentDB’s indexing policy also allows you to specify which document paths to include or exclude from indexing by leveraging Indexing Paths (IndexingPolicy.IncludedPaths and IndexingPolicy.ExcludedPaths). The use of indexing paths can offer improved write performance and lower index storage for scenarios in which the query patterns are known beforehand, as indexing costs are directly correlated to the number of unique paths indexed.  For example, the following code shows how to exclude an entire section of the documents (a.k.a. a subtree) from indexing using the "*" wildcard.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    For more information, see [DocumentDB indexing policies](documentdb-indexing-policies.md).

## <a name="throughput"></a>Throughput
<a id="measure-rus"></a>

1. **Measure and tune for lower request units/second usage**

    DocumentDB offers a rich set of database operations including relational and hierarchical queries with UDFs, stored procedures, and triggers – all operating on the documents within a database collection. The cost associated with each of these operations varies based on the CPU, IO, and memory required to complete the operation. Instead of thinking about and managing hardware resources, you can think of a request unit (RU) as a single measure for the resources required to perform various database operations and service an application request.

    [Request units](documentdb-request-units.md) are provisioned for each database account based on the number of capacity units that you purchase. Request unit consumption is evaluated as a rate per second. Applications that exceed the provisioned request unit rate for their account is limited until the rate drops below the reserved level for the account. If your application requires a higher level of throughput, you can purchase additional capacity units.

    The complexity of a query impacts how many Request Units are consumed for an operation. The number of predicates, nature of the predicates, number of UDFs, and the size of the source data set all influence the cost of query operations.

    To measure the overhead of any operation (create, update, or delete), inspect the x-ms-request-charge header (or the equivalent RequestCharge property in ResourceResponse<T> or FeedResponse<T> in the .NET SDK) to measure the number of request units consumed by these operations.

    ```C#
    // Measure the performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure the performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    The request charge returned in this header is a fraction of your provisioned throughput (i.e., 2000 RUs / second). For example, if the preceding query returns 1000 1KB-documents, the cost of the operation is 1000. As such, within one second, the server honors only two such requests before throttling subsequent requests. For more information, see [Request units](documentdb-request-units.md) and the [request unit calculator](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Handle rate limiting/request rate too large**

    When a client attempts to exceed the reserved throughput for an account, there is no performance degradation at the server and no use of throughput capacity beyond the reserved level. The server will preemptively end the request with RequestRateTooLarge (HTTP status code 429) and return the x-ms-retry-after-ms header indicating the amount of time, in milliseconds, that the user must wait before reattempting the request.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    The SDKs all implicitly catch this response, respect the server-specified retry-after header, and retry the request. Unless your account is being accessed concurrently by multiple clients, the next retry will succeed.

    If you have more than one client cumulatively operating consistently above the request rate, the default retry count currently set to 9 internally by the client may not suffice; in this case, the client throws a DocumentClientException with status code 429 to the application. The default retry count can be changed by setting the RetryOptions on the ConnectionPolicy instance. By default, the DocumentClientException with status code 429 is returned after a cumulative wait time of 30 seconds if the request continues to operate above the request rate. This occurs even when the current retry count is less than the max retry count, be it the default of 9 or a user-defined value.

    While the automated retry behavior helps to improve resiliency and usability for the most applications, it might come at odds when doing performance benchmarks, especially when measuring latency.  The client-observed latency will spike if the experiment hits the server throttle and causes the client SDK to silently retry. To avoid latency spikes during performance experiments, measure the charge returned by each operation and ensure that requests are operating below the reserved request rate. For more information, see [Request units](documentdb-request-units.md).
3. **Design for smaller documents for higher throughput**

    The request charge (i.e. request processing cost) of a given operation is directly correlated to the size of the document. Operations on large documents cost more than operations for small documents.

## <a name="next-steps"></a>Next steps
For a sample application used to evaluate DocumentDB for high-performance scenarios on a few client machines, see [Performance and scale testing with Azure DocumentDB](documentdb-performance-testing.md).

Also, to learn more about designing your application for scale and high performance, see [Partitioning and scaling in Azure DocumentDB](documentdb-partition-data.md).


