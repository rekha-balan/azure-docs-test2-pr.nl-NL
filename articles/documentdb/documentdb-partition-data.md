---
title: Partitioning and scaling in Azure DocumentDB | Microsoft Docs
description: Learn about how partitioning works in Azure DocumentDB, how to configure partitioning and partition keys, and how to pick the right partition key for your application.
services: documentdb
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: ''
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 10a2df4fee9a6b24ef7def500a3da37a26595700
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564096"
---
# <a name="partitioning-partition-keys-and-scaling-in-documentdb"></a>Partitioning, partition keys, and scaling in DocumentDB

[Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) is designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows. This article provides an overview of how partitioning works in DocumentDB, and describes how you can configure DocumentDB collections to effectively scale your applications.

After reading this article, you will be able to answer the following questions:   

* How does partitioning work in Azure DocumentDB?
* How do I configure partitioning in DocumentDB
* What are partition keys, and how do I pick the right partition key for my application?

To get started with code, download the project from [DocumentDB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

Partitioning and partition keys are also covered in this Azure Friday video with Scott Hanselman and DocumentDB Principal Engineering Manager, Shireesh Thota.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-documentdb"></a>Partitioning in DocumentDB
In DocumentDB, you can store and query schema-less JSON documents with order-of-millisecond response times at any scale. DocumentDB provides containers for storing data called **collections**. Collections are logical resources and can span one or more physical partitions or servers. The number of partitions is determined by DocumentDB based on the storage size and the provisioned throughput of the collection. Every partition in DocumentDB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability. Partition management is fully managed by Azure DocumentDB, and you do not have to write complex code or manage your partitions. DocumentDB collections are **practically unlimited** in terms of storage and throughput. 

Partitioning is completely transparent to your application. DocumentDB supports fast reads and writes, SQL and LINQ queries, JavaScript based transactional logic, consistency levels, and fine-grained access control via REST API calls to a single collection resource. The service handles distributing data across partitions and routing query requests to the right partition. 

How does this work? When you create a collection in DocumentDB, you can specify **partition key property** configuration value. This is the JSON property (or path) within your documents that can be used by DocumentDB to distribute your data among multiple servers or partitions. DocumentDB will hash the partition key value and use the hashed result to determine the partition in which the JSON document will be stored. All documents with the same partition key will be stored in the same partition. 

For example, consider an application that stores data about employees and their departments in DocumentDB. Let's choose `"department"` as the partition key property, in order to scale out data by department. Every document in DocumentDB must contain a mandatory `"id"` property that must be unique for every document with the same partition key value, e.g. `"Marketing`". Every document stored in a collection must have a unique combination of partition key and id, e.g. `{ "Department": "Marketing", "id": "0001" }`, `{ "Department": "Marketing", "id": "0002" }`, and `{ "Department": "Sales", "id": "0001" }`. In other words, the compound property of (partition key, id) is the primary key for your collection.

DocumentDB creates a small number of physical partitions behind each collection based on storage size and provisioned throughput. The property that you define as partition key is a logical partition. Multiple partition key values typically share a single physical partition, but a single value will never span a partition. If you have a partition key with a lot of values, it’s good because DocumentDB will be able to perform better load balancing as your data grows or you increase the provisioned throughput.

For example, let’s say you create a collection with 25,000 requests per second throughput and DocumentDB can support 10,000 requests per second per single physical partition. DocumentDB would create 3 physical partitions P1, P2, and P3 for your collection. During the insertion or read of a document, the DocumentDB service hashes the corresponding `Department` value to map data to the three partitions P1, P2, and P3. So for example, if “Marketing” and “Sales” hash to 1, they are both stored in P1. And if P1 becomes full, DocumentDB splits P1 into two new partitions P4 and P5. Then the service might move “Marketing” to P4 and “Sales” to P5 after the split, then drop P1. These moves of partition keys between partitions are transparent to your application, and have no impact to the availability of your collection.

## <a name="sharding-in-api-for-mongodb"></a>Sharding in API for MongoDB
Sharded collections in API for MongoDB are using the same infrastructure as DocumentDB's partitioned collections. Like partitioned collections, sharded collections can have any number of shards and each shard has a fixed amount of SSD-backed storage associated with it. Sharded collections are practically unlimited in terms of storage and throughput. API for MongoDB's shard key is equivalent to DocumentDB's partition key and when deciding a shard key, make sure to read the [Partition keys](#partition-keys) and [Designing for partitioning](#designing-for-partitioning) sections.

<a name="partition-keys"></a>
## <a name="partition-keys"></a>Partition keys
The choice of the partition key is an important decision that you’ll have to make at design time. You must pick a JSON property name that has a wide range of values and is likely to have evenly distributed access patterns. 

> [!NOTE]
> It is a best practice to have a partition key with a large number of distinct values (100s-1000s at a minimum). Many customers use DocumentDB as effectively a key value store, where the unique “id” is the partition key of millions-billions of partition keys.
>

The following table shows examples of partition key definitions and the JSON values corresponding to each. The partition key is specified as a JSON path, e.g. `/department` represents the property department. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Partition Key Path</strong></p></td>
            <td valign="top"><p><strong>Description</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/department</p></td>
            <td valign="top"><p>Corresponds to the JSON value of doc.department where doc is the document.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/properties/name</p></td>
            <td valign="top"><p>Corresponds to the JSON value of doc.properties.name where doc is the document (nested property).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/id</p></td>
            <td valign="top"><p>Corresponds to the JSON value of doc.id (id and partition key are the same property).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/"department name"</p></td>
            <td valign="top"><p>Corresponds to the JSON value of doc["department name"] where doc is the document.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> The syntax for partition key path is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end. For example, you would specify /department/? to index the values under department, but specify /department as the partition key definition. The partition key path is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.
> 
> 

Let's look at how the choice of partition key impacts the performance of your application.

## <a name="partitioning-and-provisioned-throughput"></a>Partitioning and provisioned throughput
DocumentDB is designed for predictable performance. When you create a collection, you reserve throughput in terms of **[request units](documentdb-request-units.md) (RU) per second**. Each request is assigned a request unit charge that is proportionate to the amount of system resources like CPU and IO consumed by the operation. A read of a 1 kB document with Session consistency consumes 1 request unit. A read is 1 RU regardless of the number of items stored or the number of concurrent requests running at the same time. Larger documents require higher request units depending on the size. If you know the size of your entities and the number of reads you need to support for your application, you can provision the exact amount of throughput required for your application's read needs. 

When DocumentDB stores documents, it distributes them evenly among partitions based on the partition key value. The throughput is also distributed evenly among the available partitions i.e. the throughput per partition = (total throughput per collection)/ (number of partitions). 

> [!NOTE]
> In order to achieve the full throughput of the collection, you must choose a partition key that allows you to evenly distribute requests among a number of distinct partition key values.
> 
> 

## <a name="single-partition-and-partitioned-collections"></a>Single partition and partitioned collections
DocumentDB supports the creation of both single-partition and partitioned collections. 

* **Partitioned collections** can span multiple partitions and support unlimited storage and throughput. You must specify a partition key for the collection. 
* **Single-partition collections** have lower price options, but they are limited in terms of maximum low storage and throughput. You do not have to specify a partition key for these collections. We recommend using partitioned collections over single-partitioned collections for all scenarios, except in situations where you expect only a small amount of data storage and requests.

![Partitioned collections in DocumentDB][2] 

Partitioned collections can support unlimited storage and throughput.

The following table lists differences in working with a single-partition and partitioned collections:

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Single Partition Collection</strong></p></td>
            <td valign="top"><p><strong>Partitioned Collection</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Partition Key</p></td>
            <td valign="top"><p>None</p></td>
            <td valign="top"><p>Required</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Primary Key for Document</p></td>
            <td valign="top"><p>"id"</p></td>
            <td valign="top"><p>compound key &lt;partition key&gt; and "id"</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Minimum Storage</p></td>
            <td valign="top"><p>0 GB</p></td>
            <td valign="top"><p>0 GB</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Maximum Storage</p></td>
            <td valign="top"><p>10 GB</p></td>
            <td valign="top"><p>Unlimited</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Minimum Throughput</p></td>
            <td valign="top"><p>400 request units per second</p></td>
            <td valign="top"><p>2,500 request units per second</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Maximum Throughput</p></td>
            <td valign="top"><p>10,000 request units per second</p></td>
            <td valign="top"><p>Unlimited</p></td>
        </tr>
        <tr>
            <td valign="top"><p>API versions</p></td>
            <td valign="top"><p>All</p></td>
            <td valign="top"><p>API 2015-12-16 and newer</p></td>
        </tr>
    </tbody>
</table>

## <a name="working-with-the-documentdb-sdks"></a>Working with the DocumentDB SDKs
Azure DocumentDB added support for automatic partitioning with [REST API version 2015-12-16](https://msdn.microsoft.com/library/azure/dn781481.aspx). In order to create partitioned collections, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python). 

### <a name="creating-partitioned-collections"></a>Creating partitioned collections
The following sample shows a .NET snippet to create a collection to store device telemetry data of 20,000 request units per second of throughput. The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API). Here we set the `/deviceId` as the partition key. The choice of partition key is saved along with the rest of the collection metadata like name and indexing policy.

For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Collection for device telemetry. Here the JSON property deviceId will be used as the partition key to 
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

> [!NOTE]
> In order to create partitioned collections using the SDK, you must specify a throughput value equal or greater than 10,100 RU/s. To set a throughput value between 2,500 and 10,000 for partitioned collections you must temporarily use the Azure portal, as these new lower values are not yet available in the SDK.
> 
> 

This method makes a REST API call to DocumentDB, and the service will provision a number of partitions based on the requested throughput. You can change the throughput of a collection as your performance needs evolve. 

### <a name="reading-and-writing-documents"></a>Reading and writing documents
Now, let's insert data into DocumentDB. Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a collection.

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```

Let's read the document by it's partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-collections"></a>Querying partitioned collections
When you query data in partitioned collections, DocumentDB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any). For example, this query is routed to just the partition containing the partition key "XMS-0001".

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index. Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

DocumentDB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned collections using SQL starting with SDKs 1.12.0 and above. Queries must include a single aggregate operator, and must include a single value in the projection.

### <a name="parallel-query-execution"></a>Parallel query execution
The DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions. For example, the following query is configured to run in parallel across partitions.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
You can manage parallel query execution by tuning the following parameters:

* By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the collection's partitions. If you set this to -1, the degree of parallelism is managed by the SDK. If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the collection's partitions.
* By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization. If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.

Given the same state of the collection, a parallel query will return results in the same order as in serial execution. When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the DocumentDB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.

### <a name="executing-stored-procedures"></a>Executing stored procedures
You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single document. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
    
In the next section, we look at how you can move to partitioned collections from single-partition collections.

## <a name="creating-an-api-for-mongodb-sharded-collection"></a>Creating an API for MongoDB sharded collection
The simplest way to create an API for MongoDB sharded collection is through your favorite tool, driver, or SDK. In this example, we will use the Mongo Shell for the collection creation.

In the Mongo Shell:

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
Results:

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

<a name="migrating-from-single-partition"></a>

## <a name="migrating-from-single-partition-to-partitioned-collections-in-documentdb"></a>Migrating from single-partition to partitioned collections in DocumentDB

> [!IMPORTANT]
> If you are importing to API for MongoDB, follow these [instructions](documentdb-mongodb-migrate.md).
> 
> 

When an application using a single-partition collection needs higher throughput (>10,000 RU/s) or larger data storage (>10GB), you can use the [DocumentDB Data Migration Tool](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) to migrate the data from the single-partition collection to a partitioned collection. 

To migrate from a single-partition collection to a partitioned collection

1. Export data from the single-partition collection to JSON. See [Export to JSON file](documentdb-import-data.md#export-to-json-file) for additional details.
2. Import the data into a partitioned collection created with a partition key definition and over 2,500 request units per second throughput, as shown in the example below. See [Import to DocumentDB](documentdb-import-data.md#DocumentDBSeqTarget) for additional details.

![Migrating Data to a Partitioned collection in DocumentDB][3]  

> [!TIP]
> For faster import times, consider increasing the Number of Parallel Requests to 100 or higher to take advantage of the higher throughput available for partitioned collections. 
> 
> 

Now that we've completed the basics, let's look at a few important design considerations when working with partition keys in DocumentDB.

<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Designing for partitioning
The choice of the partition key is an important decision that you’ll have to make at design time. This section describes some of the tradeoffs involved in selecting a partition key for your collection.

### <a name="partition-key-as-the-transaction-boundary"></a>Partition key as the transaction boundary
Your choice of partition key should balance the need to enable the use of transactions against the requirement to distribute your entities across multiple partition keys to ensure a scalable solution. At one extreme, you could set the same partition key for all your documents, but this may limit the scalability of your solution. At the other extreme, you could assign a unique partition key for each document, which would be highly scalable but would prevent you from using cross document transactions via stored procedures and triggers. An ideal partition key is one that enables you to use efficient queries and that has sufficient cardinality to ensure your solution is scalable. 

### <a name="avoiding-storage-and-performance-bottlenecks"></a>Avoiding storage and performance bottlenecks
It is also important to pick a property which allows writes to be distributed across a number of distinct values. Requests to the same partition key cannot exceed the throughput of a single partition, and will be throttled. So it is important to pick a partition key that does not result in **"hot spots"** within your application. Since all the data for a single partition key must be stored within a partition, it is also recommended to avoid partition keys that have high volumes of data for the same value. 

### <a name="examples-of-good-partition-keys"></a>Examples of good partition keys
Here are a few examples for how to pick the partition key for your application:

* If you’re implementing a user profile backend, then the user ID is a good choice for partition key.
* If you’re storing IoT data e.g. device state, a device ID is a good choice for partition key.
* If you’re using DocumentDB for logging time-series data, then the hostname or process ID is a good choice for partition key.
* If you have a multi-tenant architecture, the tenant ID is a good choice for partition key.

Note that in some use cases (like the IoT and user profiles described above), the partition key might be the same as your id (document key). In others like the time series data, you might have a partition key that’s different than the id.

### <a name="partitioning-and-loggingtime-series-data"></a>Partitioning and logging/time-series data
One of the most common use cases of DocumentDB is for logging and telemetry. It is important to pick a good partition key since you might need to read/write vast volumes of data. The choice will depend on your read and write rates and kinds of queries you expect to run. Here are some tips on how to choose a good partition key.

* If your use case involves a small rate of writes acculumating over a long period of time, and need to query by ranges of timestamps and other filters, then using a rollup of the timestamp e.g. date as a partition key is a good approach. This allows you to query over all the data for a date from a single partition. 
* If your workload is write heavy, which is generally more common, you should use a partition key that’s not based on timestamp so that DocumentDB can distribute writes evenly across a number of partitions. Here a hostname, process ID, activity ID, or another property with high cardinality is a good choice. 
* A third approach is a hybrid one where you have multiple collections, one for each day/month and the partition key is a granular property like hostname. This has the benefit that you can set different throughput based on the time window, e.g. the collection for the current month is provisioned with higher throughput since it serves reads and writes, whereas previous months with lower throughput since they only serve reads.

### <a name="partitioning-and-multi-tenancy"></a>Partitioning and multi-tenancy
If you are implementing a multi-tenant application using DocumentDB, there are two major patterns for implementing tenancy with DocumentDB – one partition key per tenant, and one collection per tenant. Here are the pros and cons for each:

* One Partition Key per tenant: In this model, tenants are collocated within a single collection. But queries and inserts for documents within a single tenant can be performed against a single partition. You can also implement transactional logic across all documents within a tenant. Since multiple tenants share a collection, you can save storage and throughput costs by pooling resources for tenants within a single collection rather than provisioning extra headroom for each tenant. The drawback is that you do not have performance isolation per tenant. Performance/throughput increases apply to the entire collection vs targeted increases for tenants.
* One Collection per tenant: Each tenant has its own collection. In this model, you can reserve performance per tenant. With DocumentDB's new consumption-based pricing model, this model is more cost-effective for multi-tenant applications with a small number of tenants.

You can also use a combination/tiered approach that collocates small tenants and migrates larger tenants to their own collection.

## <a name="next-steps"></a>Next steps
In this article, we've described how partitioning works in Azure DocumentDB, how you can create partitioned collections, and how you can pick a good partition key for your application. 

* Perform scale and performance testing with DocumentDB. See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md) for a sample.
* Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx)
* Learn about [provisioned throughput in DocumentDB](documentdb-performance-levels.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-partition-data/partitioning.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-partition-data/single-and-partitioned.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-partition-data/documentdb-migration-partitioned-collection.png  





