---
title: Partitioning and scaling in Azure Cosmos DB | Microsoft Docs
description: Learn about how partitioning works in Azure Cosmos DB, how to configure partitioning and partition keys, and how to pick the right partition key for your application.
services: cosmos-db
author: rafats
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: na
ms.topic: conceptual
ms.date: 05/24/2017
ms.author: rafats
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e3c15ce201cee88d400b9d5fb9272b584293a2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865482"
---
# <a name="partitioning-in-azure-cosmos-db-using-the-sql-api"></a><span data-ttu-id="e4941-103">Partitioning in Azure Cosmos DB using the SQL API</span><span class="sxs-lookup"><span data-stu-id="e4941-103">Partitioning in Azure Cosmos DB using the SQL API</span></span>

<span data-ttu-id="e4941-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span><span class="sxs-lookup"><span data-stu-id="e4941-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="e4941-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the SQL API.</span><span class="sxs-lookup"><span data-stu-id="e4941-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the SQL API.</span></span> <span data-ttu-id="e4941-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span><span class="sxs-lookup"><span data-stu-id="e4941-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="e4941-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="e4941-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="e4941-108">After reading this article, you will be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="e4941-108">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="e4941-109">How does partitioning work in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e4941-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="e4941-110">How do I configure partitioning in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e4941-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="e4941-111">What are partition keys, and how do I pick the right partition key for my application?</span><span class="sxs-lookup"><span data-stu-id="e4941-111">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="e4941-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="e4941-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="e4941-113">Partition keys</span><span class="sxs-lookup"><span data-stu-id="e4941-113">Partition keys</span></span>

<span data-ttu-id="e4941-114">In the SQL API, you specify the partition key definition in the form of a JSON path.</span><span class="sxs-lookup"><span data-stu-id="e4941-114">In the SQL API, you specify the partition key definition in the form of a JSON path.</span></span> <span data-ttu-id="e4941-115">The following table shows examples of partition key definitions and the values corresponding to each.</span><span class="sxs-lookup"><span data-stu-id="e4941-115">The following table shows examples of partition key definitions and the values corresponding to each.</span></span> <span data-ttu-id="e4941-116">The partition key is specified as a path, for example, `/department` represents the property department.</span><span class="sxs-lookup"><span data-stu-id="e4941-116">The partition key is specified as a path, for example, `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="e4941-117"><strong>Partition Key</strong></span><span class="sxs-lookup"><span data-stu-id="e4941-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e4941-118"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="e4941-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e4941-119">/department</span><span class="sxs-lookup"><span data-stu-id="e4941-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e4941-120">Corresponds to the value of doc.department where doc is the item.</span><span class="sxs-lookup"><span data-stu-id="e4941-120">Corresponds to the value of doc.department where doc is the item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e4941-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="e4941-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e4941-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span><span class="sxs-lookup"><span data-stu-id="e4941-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e4941-123">/id</span><span class="sxs-lookup"><span data-stu-id="e4941-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e4941-124">Corresponds to the value of doc.id (id and partition key are the same property).</span><span class="sxs-lookup"><span data-stu-id="e4941-124">Corresponds to the value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e4941-125">/"department name"</span><span class="sxs-lookup"><span data-stu-id="e4941-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e4941-126">Corresponds to the value of doc["department name"] where doc is the item.</span><span class="sxs-lookup"><span data-stu-id="e4941-126">Corresponds to the value of doc["department name"] where doc is the item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="e4941-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span><span class="sxs-lookup"><span data-stu-id="e4941-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="e4941-128">For example, you would specify /department/?</span><span class="sxs-lookup"><span data-stu-id="e4941-128">For example, you would specify /department/?</span></span> <span data-ttu-id="e4941-129">to index the values under department, but specify /department as the partition key definition.</span><span class="sxs-lookup"><span data-stu-id="e4941-129">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="e4941-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span><span class="sxs-lookup"><span data-stu-id="e4941-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="e4941-131">Let's look at how the choice of partition key impacts the performance of your application.</span><span class="sxs-lookup"><span data-stu-id="e4941-131">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="working-with-the-azure-cosmos-db-sdks"></a><span data-ttu-id="e4941-132">Working with the Azure Cosmos DB SDKs</span><span class="sxs-lookup"><span data-stu-id="e4941-132">Working with the Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="e4941-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="e4941-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/cosmos-db/).</span></span> <span data-ttu-id="e4941-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="e4941-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="e4941-135">Creating containers</span><span class="sxs-lookup"><span data-stu-id="e4941-135">Creating containers</span></span>
<span data-ttu-id="e4941-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span><span class="sxs-lookup"><span data-stu-id="e4941-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="e4941-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span><span class="sxs-lookup"><span data-stu-id="e4941-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="e4941-138">Here you set the `/deviceId` as the partition key.</span><span class="sxs-lookup"><span data-stu-id="e4941-138">Here you set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="e4941-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span><span class="sxs-lookup"><span data-stu-id="e4941-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span></span>

<span data-ttu-id="e4941-140">For this sample, you picked `deviceId` since you know that (a) there are a large number of devices, writes can be distributed across partitions evenly and allowing you to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span><span class="sxs-lookup"><span data-stu-id="e4941-140">For this sample, you picked `deviceId` since you know that (a) there are a large number of devices, writes can be distributed across partitions evenly and allowing you to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
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

<span data-ttu-id="e4941-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span><span class="sxs-lookup"><span data-stu-id="e4941-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="e4941-142">You can change the throughput of a container or a set of containers as your performance needs evolve.</span><span class="sxs-lookup"><span data-stu-id="e4941-142">You can change the throughput of a container or a set of containers as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="e4941-143">Reading and writing items</span><span class="sxs-lookup"><span data-stu-id="e4941-143">Reading and writing items</span></span>
<span data-ttu-id="e4941-144">Now, let's insert data into Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4941-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="e4941-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span><span class="sxs-lookup"><span data-stu-id="e4941-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span></span> <span data-ttu-id="e4941-146">The following is an example code block that leverages the SQL API:</span><span class="sxs-lookup"><span data-stu-id="e4941-146">The following is an example code block that leverages the SQL API:</span></span>

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

<span data-ttu-id="e4941-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. The reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span><span class="sxs-lookup"><span data-stu-id="e4941-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. The reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="e4941-148">Querying partitioned containers</span><span class="sxs-lookup"><span data-stu-id="e4941-148">Querying partitioned containers</span></span>
<span data-ttu-id="e4941-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span><span class="sxs-lookup"><span data-stu-id="e4941-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="e4941-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="e4941-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="e4941-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span><span class="sxs-lookup"><span data-stu-id="e4941-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="e4941-152">You have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span><span class="sxs-lookup"><span data-stu-id="e4941-152">You have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="e4941-153">Cosmos DB supports [aggregate functions](sql-api-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, , and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span><span class="sxs-lookup"><span data-stu-id="e4941-153">Cosmos DB supports [aggregate functions](sql-api-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, , and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="e4941-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span><span class="sxs-lookup"><span data-stu-id="e4941-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="e4941-155">Parallel query execution</span><span class="sxs-lookup"><span data-stu-id="e4941-155">Parallel query execution</span></span>
<span data-ttu-id="e4941-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span><span class="sxs-lookup"><span data-stu-id="e4941-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="e4941-157">For example, the following query is configured to run in parallel across partitions.</span><span class="sxs-lookup"><span data-stu-id="e4941-157">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="e4941-158">You can manage parallel query execution by tuning the following parameters:</span><span class="sxs-lookup"><span data-stu-id="e4941-158">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="e4941-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism that is, the maximum number of simultaneous network connections to the container's partitions.</span><span class="sxs-lookup"><span data-stu-id="e4941-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism that is, the maximum number of simultaneous network connections to the container's partitions.</span></span> <span data-ttu-id="e4941-160">If you set this property to -1, the degree of parallelism is managed by the SDK.</span><span class="sxs-lookup"><span data-stu-id="e4941-160">If you set this property to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="e4941-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span><span class="sxs-lookup"><span data-stu-id="e4941-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span></span>
* <span data-ttu-id="e4941-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span><span class="sxs-lookup"><span data-stu-id="e4941-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="e4941-163">If you omit this parameter or set this property to -1, the number of items buffered during parallel query execution is managed by the SDK.</span><span class="sxs-lookup"><span data-stu-id="e4941-163">If you omit this parameter or set this property to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="e4941-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span><span class="sxs-lookup"><span data-stu-id="e4941-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="e4941-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span><span class="sxs-lookup"><span data-stu-id="e4941-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="e4941-166">Executing stored procedures</span><span class="sxs-lookup"><span data-stu-id="e4941-166">Executing stored procedures</span></span>
<span data-ttu-id="e4941-167">You can also execute atomic transactions against documents with the same device ID, for example, if you're maintaining aggregates or the latest state of a device in a single item.</span><span class="sxs-lookup"><span data-stu-id="e4941-167">You can also execute atomic transactions against documents with the same device ID, for example, if you're maintaining aggregates or the latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="e4941-168">In the next section, you look at how you can move to partitioned containers from single-partition containers.</span><span class="sxs-lookup"><span data-stu-id="e4941-168">In the next section, you look at how you can move to partitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4941-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="e4941-169">Next steps</span></span>
<span data-ttu-id="e4941-170">This article provided an overview of how to work with partitioning of Azure Cosmos DB containers with the SQL API.</span><span class="sxs-lookup"><span data-stu-id="e4941-170">This article provided an overview of how to work with partitioning of Azure Cosmos DB containers with the SQL API.</span></span> <span data-ttu-id="e4941-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span><span class="sxs-lookup"><span data-stu-id="e4941-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="e4941-172">Perform scale and performance testing with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4941-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="e4941-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span><span class="sxs-lookup"><span data-stu-id="e4941-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="e4941-174">Get started coding with the [SDKs](sql-api-sdk-dotnet.md) or the [REST API](/rest/api/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="e4941-174">Get started coding with the [SDKs](sql-api-sdk-dotnet.md) or the [REST API](/rest/api/cosmos-db/)</span></span>
* <span data-ttu-id="e4941-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="e4941-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

