---
title: Request units & estimating throughput - Azure DocumentDB | Microsoft Docs
description: Learn about how to understand, specify, and estimate request unit requirements in DocumentDB.
services: documentdb
author: syamkmsft
manager: jhubbard
editor: mimig
documentationcenter: ''
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: syamk
ms.openlocfilehash: cbe7d76a1982cf02c03a1944b18a29766e39153c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563762"
---
# <a name="request-units-in-documentdb"></a><span data-ttu-id="9feef-103">Request Units in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="9feef-103">Request Units in DocumentDB</span></span>
<span data-ttu-id="9feef-104">Now available: DocumentDB [request unit calculator](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="9feef-104">Now available: DocumentDB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="9feef-105">Learn more in [Estimating your throughput needs](documentdb-request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="9feef-105">Learn more in [Estimating your throughput needs](documentdb-request-units.md#estimating-throughput-needs).</span></span>

![Throughput calculator][5]

## <a name="introduction"></a><span data-ttu-id="9feef-107">Introduction</span><span class="sxs-lookup"><span data-stu-id="9feef-107">Introduction</span></span>
<span data-ttu-id="9feef-108">[Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) is a fully managed, scalable NoSQL database service for JSON documents.</span><span class="sxs-lookup"><span data-stu-id="9feef-108">[Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) is a fully managed, scalable NoSQL database service for JSON documents.</span></span> <span data-ttu-id="9feef-109">With DocumentDB, you don’t have to rent virtual machines, deploy software, or monitor databases.</span><span class="sxs-lookup"><span data-stu-id="9feef-109">With DocumentDB, you don’t have to rent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="9feef-110">DocumentDB is operated and continuously monitored by Microsoft engineers to deliver world class availability, performance, and data protection.</span><span class="sxs-lookup"><span data-stu-id="9feef-110">DocumentDB is operated and continuously monitored by Microsoft engineers to deliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="9feef-111">Data in DocumentDB is stored within collections, which are elastic, highly available containers.</span><span class="sxs-lookup"><span data-stu-id="9feef-111">Data in DocumentDB is stored within collections, which are elastic, highly available containers.</span></span> <span data-ttu-id="9feef-112">Instead of thinking about and managing hardware resources like CPU, memory, and IOPs for a collection, you can reserve throughput in terms of requests per second.</span><span class="sxs-lookup"><span data-stu-id="9feef-112">Instead of thinking about and managing hardware resources like CPU, memory, and IOPs for a collection, you can reserve throughput in terms of requests per second.</span></span> <span data-ttu-id="9feef-113">DocumentDB will automatically manage the provisioning, transparent partitioning, and scaling of your collection in order to serve the provisioned number of requests.</span><span class="sxs-lookup"><span data-stu-id="9feef-113">DocumentDB will automatically manage the provisioning, transparent partitioning, and scaling of your collection in order to serve the provisioned number of requests.</span></span> 

<span data-ttu-id="9feef-114">DocumentDB supports a number of APIs for reads, writes, queries, and stored procedure executions.</span><span class="sxs-lookup"><span data-stu-id="9feef-114">DocumentDB supports a number of APIs for reads, writes, queries, and stored procedure executions.</span></span> <span data-ttu-id="9feef-115">Since not all requests are equal, they are assigned a normalized amount of **request units** based on the amount of computation required to serve the request.</span><span class="sxs-lookup"><span data-stu-id="9feef-115">Since not all requests are equal, they are assigned a normalized amount of **request units** based on the amount of computation required to serve the request.</span></span> <span data-ttu-id="9feef-116">The number of request units for an operation is deterministic, and you can track the number of request units consumed by any operation in DocumentDB via a response header.</span><span class="sxs-lookup"><span data-stu-id="9feef-116">The number of request units for an operation is deterministic, and you can track the number of request units consumed by any operation in DocumentDB via a response header.</span></span>

<span data-ttu-id="9feef-117">Each collection in DocumentDB can be reserved with throughput, also expressed in terms of request units.</span><span class="sxs-lookup"><span data-stu-id="9feef-117">Each collection in DocumentDB can be reserved with throughput, also expressed in terms of request units.</span></span> <span data-ttu-id="9feef-118">This is expressed in blocks of 100 request units per second, ranging from hundreds up to millions of request units per second.</span><span class="sxs-lookup"><span data-stu-id="9feef-118">This is expressed in blocks of 100 request units per second, ranging from hundreds up to millions of request units per second.</span></span> <span data-ttu-id="9feef-119">The provisioned throughput can be adjusted throughout the life of a collection to adapt to the changing processing needs and access patterns of your application.</span><span class="sxs-lookup"><span data-stu-id="9feef-119">The provisioned throughput can be adjusted throughout the life of a collection to adapt to the changing processing needs and access patterns of your application.</span></span> 

<span data-ttu-id="9feef-120">After reading this article, you'll be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="9feef-120">After reading this article, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="9feef-121">What are request units and request charges?</span><span class="sxs-lookup"><span data-stu-id="9feef-121">What are request units and request charges?</span></span>
* <span data-ttu-id="9feef-122">How do I specify request unit capacity for a collection?</span><span class="sxs-lookup"><span data-stu-id="9feef-122">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="9feef-123">How do I estimate my application's request unit needs?</span><span class="sxs-lookup"><span data-stu-id="9feef-123">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="9feef-124">What happens if I exceed request unit capacity for a collection?</span><span class="sxs-lookup"><span data-stu-id="9feef-124">What happens if I exceed request unit capacity for a collection?</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="9feef-125">Request units and request charges</span><span class="sxs-lookup"><span data-stu-id="9feef-125">Request units and request charges</span></span>
<span data-ttu-id="9feef-126">DocumentDB and API for MongoDB delivers fast, predictable performance by *reserving* resources to satisfy your application's throughput needs.</span><span class="sxs-lookup"><span data-stu-id="9feef-126">DocumentDB and API for MongoDB delivers fast, predictable performance by *reserving* resources to satisfy your application's throughput needs.</span></span>  <span data-ttu-id="9feef-127">Because application load and access patterns change over time, DocumentDB allows you to easily increase or decrease the amount of reserved throughput available to your application.</span><span class="sxs-lookup"><span data-stu-id="9feef-127">Because application load and access patterns change over time, DocumentDB allows you to easily increase or decrease the amount of reserved throughput available to your application.</span></span>

<span data-ttu-id="9feef-128">With DocumentDB, reserved throughput is specified in terms of request units processing per second.</span><span class="sxs-lookup"><span data-stu-id="9feef-128">With DocumentDB, reserved throughput is specified in terms of request units processing per second.</span></span>  <span data-ttu-id="9feef-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available to your application on per second basis.</span><span class="sxs-lookup"><span data-stu-id="9feef-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available to your application on per second basis.</span></span>  <span data-ttu-id="9feef-130">Each operation in DocumentDB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span><span class="sxs-lookup"><span data-stu-id="9feef-130">Each operation in DocumentDB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="9feef-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span><span class="sxs-lookup"><span data-stu-id="9feef-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="9feef-132">Understanding the factors which impact request unit charges, along with your application's throughput requirements, enables you to run your application as cost effectively as possible.</span><span class="sxs-lookup"><span data-stu-id="9feef-132">Understanding the factors which impact request unit charges, along with your application's throughput requirements, enables you to run your application as cost effectively as possible.</span></span> 

<span data-ttu-id="9feef-133">We recommend getting started by watching the following video, where Aravind Ramachandran explains request units and predictable performance with DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="9feef-133">We recommend getting started by watching the following video, where Aravind Ramachandran explains request units and predictable performance with DocumentDB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-documentdb"></a><span data-ttu-id="9feef-134">Specifying request unit capacity in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="9feef-134">Specifying request unit capacity in DocumentDB</span></span>
<span data-ttu-id="9feef-135">When creating a DocumentDB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span><span class="sxs-lookup"><span data-stu-id="9feef-135">When creating a DocumentDB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span></span> <span data-ttu-id="9feef-136">Based on the provisioned throughput, DocumentDB allocates physical partitions to host your collection and splits/rebalances data across partitions as it grows.</span><span class="sxs-lookup"><span data-stu-id="9feef-136">Based on the provisioned throughput, DocumentDB allocates physical partitions to host your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="9feef-137">DocumentDB requires a partition key to be specified when a collection is provisioned with 10,000 request units or higher.</span><span class="sxs-lookup"><span data-stu-id="9feef-137">DocumentDB requires a partition key to be specified when a collection is provisioned with 10,000 request units or higher.</span></span> <span data-ttu-id="9feef-138">A partition key is also required to scale your collection's throughput beyond 10,000 request units in the future.</span><span class="sxs-lookup"><span data-stu-id="9feef-138">A partition key is also required to scale your collection's throughput beyond 10,000 request units in the future.</span></span> <span data-ttu-id="9feef-139">Therefore, it is highly recommended to configure a [partition key](documentdb-partition-data.md) when creating a collection regardless of your initial throughput.</span><span class="sxs-lookup"><span data-stu-id="9feef-139">Therefore, it is highly recommended to configure a [partition key](documentdb-partition-data.md) when creating a collection regardless of your initial throughput.</span></span> <span data-ttu-id="9feef-140">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100s to millions of distinct values) so that your collection and requests can be scaled uniformly by DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="9feef-140">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100s to millions of distinct values) so that your collection and requests can be scaled uniformly by DocumentDB.</span></span> 

> [!NOTE]
> <span data-ttu-id="9feef-141">A partition key is a logical boundary, and not a physical one.</span><span class="sxs-lookup"><span data-stu-id="9feef-141">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="9feef-142">Therefore, you do not need to limit the number of distinct partition key values.</span><span class="sxs-lookup"><span data-stu-id="9feef-142">Therefore, you do not need to limit the number of distinct partition key values.</span></span> <span data-ttu-id="9feef-143">It is in fact better to have more distinct partition key values than less, as DocumentDB has more load balancing options.</span><span class="sxs-lookup"><span data-stu-id="9feef-143">It is in fact better to have more distinct partition key values than less, as DocumentDB has more load balancing options.</span></span>

<span data-ttu-id="9feef-144">Here is a code snippet for creating a collection with 3,000 request units per second using the .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="9feef-144">Here is a code snippet for creating a collection with 3,000 request units per second using the .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="9feef-145">DocumentDB operates on a reservation model on throughput.</span><span class="sxs-lookup"><span data-stu-id="9feef-145">DocumentDB operates on a reservation model on throughput.</span></span> <span data-ttu-id="9feef-146">That is, you are billed for the amount of throughput *reserved* for the collection, regardless of how much of that throughput is actively *used*.</span><span class="sxs-lookup"><span data-stu-id="9feef-146">That is, you are billed for the amount of throughput *reserved* for the collection, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="9feef-147">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through DocumentDB SDKs or using the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9feef-147">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through DocumentDB SDKs or using the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="9feef-148">Each collection is mapped to an `Offer` resource in DocumentDB, which has metadata about the collection's provisioned throughput.</span><span class="sxs-lookup"><span data-stu-id="9feef-148">Each collection is mapped to an `Offer` resource in DocumentDB, which has metadata about the collection's provisioned throughput.</span></span> <span data-ttu-id="9feef-149">You can change the allocated throughput by looking up the corresponding offer resource for a collection, then updating it with the new throughput value.</span><span class="sxs-lookup"><span data-stu-id="9feef-149">You can change the allocated throughput by looking up the corresponding offer resource for a collection, then updating it with the new throughput value.</span></span> <span data-ttu-id="9feef-150">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second using the .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="9feef-150">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second using the .NET SDK:</span></span>

```csharp
// Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="9feef-151">There is no impact to the availability of your collection when you change the throughput.</span><span class="sxs-lookup"><span data-stu-id="9feef-151">There is no impact to the availability of your collection when you change the throughput.</span></span> <span data-ttu-id="9feef-152">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span><span class="sxs-lookup"><span data-stu-id="9feef-152">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span></span>

## <a name="specifying-request-unit-capacity-in-api-for-mongodb"></a><span data-ttu-id="9feef-153">Specifying request unit capacity in API for MongoDB</span><span class="sxs-lookup"><span data-stu-id="9feef-153">Specifying request unit capacity in API for MongoDB</span></span>
<span data-ttu-id="9feef-154">API for MongoDB allows you to specify the number of request units per second (RU per second) you want reserved for the collection.</span><span class="sxs-lookup"><span data-stu-id="9feef-154">API for MongoDB allows you to specify the number of request units per second (RU per second) you want reserved for the collection.</span></span>

<span data-ttu-id="9feef-155">API for MongoDB operates on the same reservation model based on throughput as DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="9feef-155">API for MongoDB operates on the same reservation model based on throughput as DocumentDB.</span></span> <span data-ttu-id="9feef-156">That is, you are billed for the amount of throughput *reserved* for the collection, regardless of how much of that throughput is actively *used*.</span><span class="sxs-lookup"><span data-stu-id="9feef-156">That is, you are billed for the amount of throughput *reserved* for the collection, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="9feef-157">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9feef-157">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="9feef-158">There is no impact to the availability of your collection when you change the throughput.</span><span class="sxs-lookup"><span data-stu-id="9feef-158">There is no impact to the availability of your collection when you change the throughput.</span></span> <span data-ttu-id="9feef-159">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span><span class="sxs-lookup"><span data-stu-id="9feef-159">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="9feef-160">Request unit considerations</span><span class="sxs-lookup"><span data-stu-id="9feef-160">Request unit considerations</span></span>
<span data-ttu-id="9feef-161">When estimating the number of request units to reserve for your DocumentDB collection, it is important to take the following variables into consideration:</span><span class="sxs-lookup"><span data-stu-id="9feef-161">When estimating the number of request units to reserve for your DocumentDB collection, it is important to take the following variables into consideration:</span></span>

* <span data-ttu-id="9feef-162">**Document size**.</span><span class="sxs-lookup"><span data-stu-id="9feef-162">**Document size**.</span></span> <span data-ttu-id="9feef-163">As document sizes increase the units consumed to read or write the data will also increase.</span><span class="sxs-lookup"><span data-stu-id="9feef-163">As document sizes increase the units consumed to read or write the data will also increase.</span></span>
* <span data-ttu-id="9feef-164">**Document property count**.</span><span class="sxs-lookup"><span data-stu-id="9feef-164">**Document property count**.</span></span> <span data-ttu-id="9feef-165">Assuming default indexing of all properties, the units consumed to write a document will increase as the property count increases.</span><span class="sxs-lookup"><span data-stu-id="9feef-165">Assuming default indexing of all properties, the units consumed to write a document will increase as the property count increases.</span></span>
* <span data-ttu-id="9feef-166">**Data consistency**.</span><span class="sxs-lookup"><span data-stu-id="9feef-166">**Data consistency**.</span></span> <span data-ttu-id="9feef-167">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed to read documents.</span><span class="sxs-lookup"><span data-stu-id="9feef-167">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed to read documents.</span></span>
* <span data-ttu-id="9feef-168">**Indexed properties**.</span><span class="sxs-lookup"><span data-stu-id="9feef-168">**Indexed properties**.</span></span> <span data-ttu-id="9feef-169">An index policy on each collection determines which properties are indexed by default.</span><span class="sxs-lookup"><span data-stu-id="9feef-169">An index policy on each collection determines which properties are indexed by default.</span></span> <span data-ttu-id="9feef-170">You can reduce your request unit consumption by limiting the number of indexed properties or by enabling lazy indexing.</span><span class="sxs-lookup"><span data-stu-id="9feef-170">You can reduce your request unit consumption by limiting the number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="9feef-171">**Document indexing**.</span><span class="sxs-lookup"><span data-stu-id="9feef-171">**Document indexing**.</span></span> <span data-ttu-id="9feef-172">By default each document is automatically indexed, you will consume fewer request units if you choose not to index some of your documents.</span><span class="sxs-lookup"><span data-stu-id="9feef-172">By default each document is automatically indexed, you will consume fewer request units if you choose not to index some of your documents.</span></span>
* <span data-ttu-id="9feef-173">**Query patterns**.</span><span class="sxs-lookup"><span data-stu-id="9feef-173">**Query patterns**.</span></span> <span data-ttu-id="9feef-174">The complexity of a query impacts how many Request Units are consumed for an operation.</span><span class="sxs-lookup"><span data-stu-id="9feef-174">The complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="9feef-175">The number of predicates, nature of the predicates, projections, number of UDFs, and the size of the source data set all influence the cost of query operations.</span><span class="sxs-lookup"><span data-stu-id="9feef-175">The number of predicates, nature of the predicates, projections, number of UDFs, and the size of the source data set all influence the cost of query operations.</span></span>
* <span data-ttu-id="9feef-176">**Script usage**.</span><span class="sxs-lookup"><span data-stu-id="9feef-176">**Script usage**.</span></span>  <span data-ttu-id="9feef-177">As with queries, stored procedures and triggers consume request units based on the complexity of the operations being performed.</span><span class="sxs-lookup"><span data-stu-id="9feef-177">As with queries, stored procedures and triggers consume request units based on the complexity of the operations being performed.</span></span> <span data-ttu-id="9feef-178">As you develop your application, inspect the request charge header to better understand how each operation is consuming request unit capacity.</span><span class="sxs-lookup"><span data-stu-id="9feef-178">As you develop your application, inspect the request charge header to better understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="9feef-179">Estimating throughput needs</span><span class="sxs-lookup"><span data-stu-id="9feef-179">Estimating throughput needs</span></span>
<span data-ttu-id="9feef-180">A request unit is a normalized measure of request processing cost.</span><span class="sxs-lookup"><span data-stu-id="9feef-180">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="9feef-181">A single request unit represents the processing capacity required to read (via self link or id) a single 1KB JSON document consisting of 10 unique property values (excluding system properties).</span><span class="sxs-lookup"><span data-stu-id="9feef-181">A single request unit represents the processing capacity required to read (via self link or id) a single 1KB JSON document consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="9feef-182">A request to create (insert), replace or delete the same document will consume more processing from the service and thereby more request units.</span><span class="sxs-lookup"><span data-stu-id="9feef-182">A request to create (insert), replace or delete the same document will consume more processing from the service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="9feef-183">The baseline of 1 request unit for a 1KB document corresponds to a simple GET by self link or id of the document.</span><span class="sxs-lookup"><span data-stu-id="9feef-183">The baseline of 1 request unit for a 1KB document corresponds to a simple GET by self link or id of the document.</span></span>
> 
> 

<span data-ttu-id="9feef-184">For example, here's a table that shows how many request units to provision at three different document sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span><span class="sxs-lookup"><span data-stu-id="9feef-184">For example, here's a table that shows how many request units to provision at three different document sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="9feef-185">The data consistency was configured at Session, and the indexing policy was set to None.</span><span class="sxs-lookup"><span data-stu-id="9feef-185">The data consistency was configured at Session, and the indexing policy was set to None.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="9feef-186"><strong>Document size</strong></span><span class="sxs-lookup"><span data-stu-id="9feef-186"><strong>Document size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-187"><strong>Reads/second</strong></span><span class="sxs-lookup"><span data-stu-id="9feef-187"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-188"><strong>Writes/second</strong></span><span class="sxs-lookup"><span data-stu-id="9feef-188"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-189"><strong>Request units</strong></span><span class="sxs-lookup"><span data-stu-id="9feef-189"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9feef-190">1 KB</span><span class="sxs-lookup"><span data-stu-id="9feef-190">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-191">500</span><span class="sxs-lookup"><span data-stu-id="9feef-191">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-192">100</span><span class="sxs-lookup"><span data-stu-id="9feef-192">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-193">(500 \* 1) + (100 \* 5) = 1,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="9feef-193">(500 \* 1) + (100 \* 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9feef-194">1 KB</span><span class="sxs-lookup"><span data-stu-id="9feef-194">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-195">500</span><span class="sxs-lookup"><span data-stu-id="9feef-195">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-196">500</span><span class="sxs-lookup"><span data-stu-id="9feef-196">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-197">(500 \* 1) + (500 \* 5) = 3,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="9feef-197">(500 \* 1) + (500 \* 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9feef-198">4 KB</span><span class="sxs-lookup"><span data-stu-id="9feef-198">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-199">500</span><span class="sxs-lookup"><span data-stu-id="9feef-199">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-200">100</span><span class="sxs-lookup"><span data-stu-id="9feef-200">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-201">(500 \* 1.3) + (100 \* 7) = 1,350 RU/s</span><span class="sxs-lookup"><span data-stu-id="9feef-201">(500 \* 1.3) + (100 \* 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9feef-202">4 KB</span><span class="sxs-lookup"><span data-stu-id="9feef-202">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-203">500</span><span class="sxs-lookup"><span data-stu-id="9feef-203">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-204">500</span><span class="sxs-lookup"><span data-stu-id="9feef-204">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-205">(500 \* 1.3) + (500 \* 7) = 4,150 RU/s</span><span class="sxs-lookup"><span data-stu-id="9feef-205">(500 \* 1.3) + (500 \* 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9feef-206">64 KB</span><span class="sxs-lookup"><span data-stu-id="9feef-206">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-207">500</span><span class="sxs-lookup"><span data-stu-id="9feef-207">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-208">100</span><span class="sxs-lookup"><span data-stu-id="9feef-208">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-209">(500 \* 10) + (100 \* 48) = 9,800 RU/s</span><span class="sxs-lookup"><span data-stu-id="9feef-209">(500 \* 10) + (100 \* 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="9feef-210">64 KB</span><span class="sxs-lookup"><span data-stu-id="9feef-210">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-211">500</span><span class="sxs-lookup"><span data-stu-id="9feef-211">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-212">500</span><span class="sxs-lookup"><span data-stu-id="9feef-212">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="9feef-213">(500 \* 10) + (500 \* 48) = 29,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="9feef-213">(500 \* 10) + (500 \* 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-the-request-unit-calculator"></a><span data-ttu-id="9feef-214">Use the request unit calculator</span><span class="sxs-lookup"><span data-stu-id="9feef-214">Use the request unit calculator</span></span>
<span data-ttu-id="9feef-215">To help customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) to help estimate the request unit requirements for typical operations, including:</span><span class="sxs-lookup"><span data-stu-id="9feef-215">To help customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) to help estimate the request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="9feef-216">Document creates (writes)</span><span class="sxs-lookup"><span data-stu-id="9feef-216">Document creates (writes)</span></span>
* <span data-ttu-id="9feef-217">Document reads</span><span class="sxs-lookup"><span data-stu-id="9feef-217">Document reads</span></span>
* <span data-ttu-id="9feef-218">Document deletes</span><span class="sxs-lookup"><span data-stu-id="9feef-218">Document deletes</span></span>
* <span data-ttu-id="9feef-219">Document updates</span><span class="sxs-lookup"><span data-stu-id="9feef-219">Document updates</span></span>

<span data-ttu-id="9feef-220">The tool also includes support for estimating data storage needs based on the sample documents you provide.</span><span class="sxs-lookup"><span data-stu-id="9feef-220">The tool also includes support for estimating data storage needs based on the sample documents you provide.</span></span>

<span data-ttu-id="9feef-221">Using the tool is simple:</span><span class="sxs-lookup"><span data-stu-id="9feef-221">Using the tool is simple:</span></span>

1. <span data-ttu-id="9feef-222">Upload one or more representative JSON documents.</span><span class="sxs-lookup"><span data-stu-id="9feef-222">Upload one or more representative JSON documents.</span></span>
   
    ![Upload documents to the request unit calculator][2]
2. <span data-ttu-id="9feef-224">To estimate data storage requirements, enter the total number of documents you expect to store.</span><span class="sxs-lookup"><span data-stu-id="9feef-224">To estimate data storage requirements, enter the total number of documents you expect to store.</span></span>
3. <span data-ttu-id="9feef-225">Enter the number of document create, read, update, and delete operations you require (on a per-second basis).</span><span class="sxs-lookup"><span data-stu-id="9feef-225">Enter the number of document create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="9feef-226">To estimate the request unit charges of document update operations, upload a copy of the sample document from step 1 above that includes typical field updates.</span><span class="sxs-lookup"><span data-stu-id="9feef-226">To estimate the request unit charges of document update operations, upload a copy of the sample document from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="9feef-227">For example, if document updates typically modify two properties named lastLogin and userVisits, then simply copy the sample document, update the values for those two properties, and upload the copied document.</span><span class="sxs-lookup"><span data-stu-id="9feef-227">For example, if document updates typically modify two properties named lastLogin and userVisits, then simply copy the sample document, update the values for those two properties, and upload the copied document.</span></span>
   
    ![Enter throughput requirements in the request unit calculator][3]
4. <span data-ttu-id="9feef-229">Click calculate and examine the results.</span><span class="sxs-lookup"><span data-stu-id="9feef-229">Click calculate and examine the results.</span></span>
   
    ![Request unit calculator results][4]

> [!NOTE]
> <span data-ttu-id="9feef-231">If you have document types which will differ dramatically in terms of size and the number of indexed properties, then upload a sample of each *type* of typical document to the tool and then calculate the results.</span><span class="sxs-lookup"><span data-stu-id="9feef-231">If you have document types which will differ dramatically in terms of size and the number of indexed properties, then upload a sample of each *type* of typical document to the tool and then calculate the results.</span></span>
> 
> 

### <a name="use-the-documentdb-request-charge-response-header"></a><span data-ttu-id="9feef-232">Use the DocumentDB request charge response header</span><span class="sxs-lookup"><span data-stu-id="9feef-232">Use the DocumentDB request charge response header</span></span>
<span data-ttu-id="9feef-233">Every response from the DocumentDB service includes a custom header (`x-ms-request-charge`) that contains the request units consumed for the request.</span><span class="sxs-lookup"><span data-stu-id="9feef-233">Every response from the DocumentDB service includes a custom header (`x-ms-request-charge`) that contains the request units consumed for the request.</span></span> <span data-ttu-id="9feef-234">This header is also accessible through the  DocumentDB SDKs.</span><span class="sxs-lookup"><span data-stu-id="9feef-234">This header is also accessible through the  DocumentDB SDKs.</span></span> <span data-ttu-id="9feef-235">In the .NET SDK, RequestCharge is a property of the ResourceResponse object.</span><span class="sxs-lookup"><span data-stu-id="9feef-235">In the .NET SDK, RequestCharge is a property of the ResourceResponse object.</span></span>  <span data-ttu-id="9feef-236">For queries, the DocumentDB Query Explorer in the Azure portal provides request charge information for executed queries.</span><span class="sxs-lookup"><span data-stu-id="9feef-236">For queries, the DocumentDB Query Explorer in the Azure portal provides request charge information for executed queries.</span></span>

![Examining RU charges in the Query Explorer][1]

<span data-ttu-id="9feef-238">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative document used by your application and then estimating the number of operations you anticipate performing each second.</span><span class="sxs-lookup"><span data-stu-id="9feef-238">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative document used by your application and then estimating the number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="9feef-239">Be sure to measure and include typical queries and DocumentDB script usage as well.</span><span class="sxs-lookup"><span data-stu-id="9feef-239">Be sure to measure and include typical queries and DocumentDB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="9feef-240">If you have document types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical document.</span><span class="sxs-lookup"><span data-stu-id="9feef-240">If you have document types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical document.</span></span>
> 
> 

<span data-ttu-id="9feef-241">For example:</span><span class="sxs-lookup"><span data-stu-id="9feef-241">For example:</span></span>

1. <span data-ttu-id="9feef-242">Record the request unit charge of creating (inserting) a typical document.</span><span class="sxs-lookup"><span data-stu-id="9feef-242">Record the request unit charge of creating (inserting) a typical document.</span></span> 
2. <span data-ttu-id="9feef-243">Record the request unit charge of reading a typical document.</span><span class="sxs-lookup"><span data-stu-id="9feef-243">Record the request unit charge of reading a typical document.</span></span>
3. <span data-ttu-id="9feef-244">Record the request unit charge of updating a typical document.</span><span class="sxs-lookup"><span data-stu-id="9feef-244">Record the request unit charge of updating a typical document.</span></span>
4. <span data-ttu-id="9feef-245">Record the request unit charge of typical, common document queries.</span><span class="sxs-lookup"><span data-stu-id="9feef-245">Record the request unit charge of typical, common document queries.</span></span>
5. <span data-ttu-id="9feef-246">Record the request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by the application</span><span class="sxs-lookup"><span data-stu-id="9feef-246">Record the request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by the application</span></span>
6. <span data-ttu-id="9feef-247">Calculate the required request units given the estimated number of operations you anticipate to run each second.</span><span class="sxs-lookup"><span data-stu-id="9feef-247">Calculate the required request units given the estimated number of operations you anticipate to run each second.</span></span>

### <a id="GetLastRequestStatistics"></a><span data-ttu-id="9feef-248">Use API for MongoDB's GetLastRequestStatistics command</span><span class="sxs-lookup"><span data-stu-id="9feef-248">Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="9feef-249">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving the request charge for specified operations.</span><span class="sxs-lookup"><span data-stu-id="9feef-249">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving the request charge for specified operations.</span></span>

<span data-ttu-id="9feef-250">For example, in the Mongo Shell, execute the operation you want to verify the request charge for.</span><span class="sxs-lookup"><span data-stu-id="9feef-250">For example, in the Mongo Shell, execute the operation you want to verify the request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="9feef-251">Next, execute the command *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="9feef-251">Next, execute the command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="9feef-252">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative document used by your application and then estimating the number of operations you anticipate performing each second.</span><span class="sxs-lookup"><span data-stu-id="9feef-252">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative document used by your application and then estimating the number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="9feef-253">If you have document types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical document.</span><span class="sxs-lookup"><span data-stu-id="9feef-253">If you have document types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical document.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="9feef-254">Use API for MongoDB's portal metrics</span><span class="sxs-lookup"><span data-stu-id="9feef-254">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="9feef-255">The simplest way to get a good estimation of request unit charges for your API for MongoDB database is to use the [Azure portal](https://portal.azure.com) metrics.</span><span class="sxs-lookup"><span data-stu-id="9feef-255">The simplest way to get a good estimation of request unit charges for your API for MongoDB database is to use the [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="9feef-256">With the *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative to one another.</span><span class="sxs-lookup"><span data-stu-id="9feef-256">With the *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative to one another.</span></span>

![API for MongoDB portal metrics][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="9feef-258">A request unit estimation example</span><span class="sxs-lookup"><span data-stu-id="9feef-258">A request unit estimation example</span></span>
<span data-ttu-id="9feef-259">Consider the following ~1KB document:</span><span class="sxs-lookup"><span data-stu-id="9feef-259">Consider the following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="9feef-260">Documents are minified in DocumentDB, so the system calculated size of the document above is slightly less than 1KB.</span><span class="sxs-lookup"><span data-stu-id="9feef-260">Documents are minified in DocumentDB, so the system calculated size of the document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="9feef-261">The following table shows approximate request unit charges for typical operations on this document (the approximate request unit charge assumes that the account consistency level is set to “Session” and that all documents are automatically indexed):</span><span class="sxs-lookup"><span data-stu-id="9feef-261">The following table shows approximate request unit charges for typical operations on this document (the approximate request unit charge assumes that the account consistency level is set to “Session” and that all documents are automatically indexed):</span></span>

| <span data-ttu-id="9feef-262">Operation</span><span class="sxs-lookup"><span data-stu-id="9feef-262">Operation</span></span> | <span data-ttu-id="9feef-263">Request Unit Charge</span><span class="sxs-lookup"><span data-stu-id="9feef-263">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="9feef-264">Create document</span><span class="sxs-lookup"><span data-stu-id="9feef-264">Create document</span></span> |<span data-ttu-id="9feef-265">~15 RU</span><span class="sxs-lookup"><span data-stu-id="9feef-265">~15 RU</span></span> |
| <span data-ttu-id="9feef-266">Read document</span><span class="sxs-lookup"><span data-stu-id="9feef-266">Read document</span></span> |<span data-ttu-id="9feef-267">~1 RU</span><span class="sxs-lookup"><span data-stu-id="9feef-267">~1 RU</span></span> |
| <span data-ttu-id="9feef-268">Query document by id</span><span class="sxs-lookup"><span data-stu-id="9feef-268">Query document by id</span></span> |<span data-ttu-id="9feef-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="9feef-269">~2.5 RU</span></span> |

<span data-ttu-id="9feef-270">Additionally, this table shows approximate request unit charges for typical queries used in the application:</span><span class="sxs-lookup"><span data-stu-id="9feef-270">Additionally, this table shows approximate request unit charges for typical queries used in the application:</span></span>

| <span data-ttu-id="9feef-271">Query</span><span class="sxs-lookup"><span data-stu-id="9feef-271">Query</span></span> | <span data-ttu-id="9feef-272">Request Unit Charge</span><span class="sxs-lookup"><span data-stu-id="9feef-272">Request Unit Charge</span></span> | <span data-ttu-id="9feef-273"># of Returned Documents</span><span class="sxs-lookup"><span data-stu-id="9feef-273"># of Returned Documents</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9feef-274">Select food by id</span><span class="sxs-lookup"><span data-stu-id="9feef-274">Select food by id</span></span> |<span data-ttu-id="9feef-275">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="9feef-275">~2.5 RU</span></span> |<span data-ttu-id="9feef-276">1</span><span class="sxs-lookup"><span data-stu-id="9feef-276">1</span></span> |
| <span data-ttu-id="9feef-277">Select foods by manufacturer</span><span class="sxs-lookup"><span data-stu-id="9feef-277">Select foods by manufacturer</span></span> |<span data-ttu-id="9feef-278">~7 RU</span><span class="sxs-lookup"><span data-stu-id="9feef-278">~7 RU</span></span> |<span data-ttu-id="9feef-279">7</span><span class="sxs-lookup"><span data-stu-id="9feef-279">7</span></span> |
| <span data-ttu-id="9feef-280">Select by food group and order by weight</span><span class="sxs-lookup"><span data-stu-id="9feef-280">Select by food group and order by weight</span></span> |<span data-ttu-id="9feef-281">~70 RU</span><span class="sxs-lookup"><span data-stu-id="9feef-281">~70 RU</span></span> |<span data-ttu-id="9feef-282">100</span><span class="sxs-lookup"><span data-stu-id="9feef-282">100</span></span> |
| <span data-ttu-id="9feef-283">Select top 10 foods in a food group</span><span class="sxs-lookup"><span data-stu-id="9feef-283">Select top 10 foods in a food group</span></span> |<span data-ttu-id="9feef-284">~10 RU</span><span class="sxs-lookup"><span data-stu-id="9feef-284">~10 RU</span></span> |<span data-ttu-id="9feef-285">10</span><span class="sxs-lookup"><span data-stu-id="9feef-285">10</span></span> |

> [!NOTE]
> <span data-ttu-id="9feef-286">RU charges vary based on the number of documents returned.</span><span class="sxs-lookup"><span data-stu-id="9feef-286">RU charges vary based on the number of documents returned.</span></span>
> 
> 

<span data-ttu-id="9feef-287">With this information, we can estimate the RU requirements for this application given the number of operations and queries we expect per second:</span><span class="sxs-lookup"><span data-stu-id="9feef-287">With this information, we can estimate the RU requirements for this application given the number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="9feef-288">Operation/Query</span><span class="sxs-lookup"><span data-stu-id="9feef-288">Operation/Query</span></span> | <span data-ttu-id="9feef-289">Estimated number per second</span><span class="sxs-lookup"><span data-stu-id="9feef-289">Estimated number per second</span></span> | <span data-ttu-id="9feef-290">Required RUs</span><span class="sxs-lookup"><span data-stu-id="9feef-290">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9feef-291">Create document</span><span class="sxs-lookup"><span data-stu-id="9feef-291">Create document</span></span> |<span data-ttu-id="9feef-292">10</span><span class="sxs-lookup"><span data-stu-id="9feef-292">10</span></span> |<span data-ttu-id="9feef-293">150</span><span class="sxs-lookup"><span data-stu-id="9feef-293">150</span></span> |
| <span data-ttu-id="9feef-294">Read document</span><span class="sxs-lookup"><span data-stu-id="9feef-294">Read document</span></span> |<span data-ttu-id="9feef-295">100</span><span class="sxs-lookup"><span data-stu-id="9feef-295">100</span></span> |<span data-ttu-id="9feef-296">100</span><span class="sxs-lookup"><span data-stu-id="9feef-296">100</span></span> |
| <span data-ttu-id="9feef-297">Select foods by manufacturer</span><span class="sxs-lookup"><span data-stu-id="9feef-297">Select foods by manufacturer</span></span> |<span data-ttu-id="9feef-298">25</span><span class="sxs-lookup"><span data-stu-id="9feef-298">25</span></span> |<span data-ttu-id="9feef-299">175</span><span class="sxs-lookup"><span data-stu-id="9feef-299">175</span></span> |
| <span data-ttu-id="9feef-300">Select by food group</span><span class="sxs-lookup"><span data-stu-id="9feef-300">Select by food group</span></span> |<span data-ttu-id="9feef-301">10</span><span class="sxs-lookup"><span data-stu-id="9feef-301">10</span></span> |<span data-ttu-id="9feef-302">700</span><span class="sxs-lookup"><span data-stu-id="9feef-302">700</span></span> |
| <span data-ttu-id="9feef-303">Select top 10</span><span class="sxs-lookup"><span data-stu-id="9feef-303">Select top 10</span></span> |<span data-ttu-id="9feef-304">15</span><span class="sxs-lookup"><span data-stu-id="9feef-304">15</span></span> |<span data-ttu-id="9feef-305">150 Total</span><span class="sxs-lookup"><span data-stu-id="9feef-305">150 Total</span></span> |

<span data-ttu-id="9feef-306">In this case, we expect an average throughput requirement of 1,275 RU/s.</span><span class="sxs-lookup"><span data-stu-id="9feef-306">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="9feef-307">Rounding up to the nearest 100, we would provision 1,300 RU/s for this application's collection.</span><span class="sxs-lookup"><span data-stu-id="9feef-307">Rounding up to the nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <a id="RequestRateTooLarge"></a> <span data-ttu-id="9feef-308">Exceeding reserved throughput limits in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="9feef-308">Exceeding reserved throughput limits in DocumentDB</span></span>
<span data-ttu-id="9feef-309">Recall that request unit consumption is evaluated as a rate per second.</span><span class="sxs-lookup"><span data-stu-id="9feef-309">Recall that request unit consumption is evaluated as a rate per second.</span></span> <span data-ttu-id="9feef-310">For applications that exceed the provisioned request unit rate for a collection, requests to that collection will be throttled until the rate drops below the reserved level.</span><span class="sxs-lookup"><span data-stu-id="9feef-310">For applications that exceed the provisioned request unit rate for a collection, requests to that collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="9feef-311">When a throttle occurs, the server will preemptively end the request with RequestRateTooLargeException (HTTP status code 429) and return the x-ms-retry-after-ms header indicating the amount of time, in milliseconds, that the user must wait before reattempting the request.</span><span class="sxs-lookup"><span data-stu-id="9feef-311">When a throttle occurs, the server will preemptively end the request with RequestRateTooLargeException (HTTP status code 429) and return the x-ms-retry-after-ms header indicating the amount of time, in milliseconds, that the user must wait before reattempting the request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="9feef-312">If you are using the .NET Client SDK and LINQ queries, then most of the time you never have to deal with this exception, as the current version of the .NET Client SDK implicitly catches this response, respects the server-specified retry-after header, and retries the request.</span><span class="sxs-lookup"><span data-stu-id="9feef-312">If you are using the .NET Client SDK and LINQ queries, then most of the time you never have to deal with this exception, as the current version of the .NET Client SDK implicitly catches this response, respects the server-specified retry-after header, and retries the request.</span></span> <span data-ttu-id="9feef-313">Unless your account is being accessed concurrently by multiple clients, the next retry will succeed.</span><span class="sxs-lookup"><span data-stu-id="9feef-313">Unless your account is being accessed concurrently by multiple clients, the next retry will succeed.</span></span>

<span data-ttu-id="9feef-314">If you have more than one client cumulatively operating above the request rate, the default retry behavior may not suffice, and the client will throw a DocumentClientException with status code 429 to the application.</span><span class="sxs-lookup"><span data-stu-id="9feef-314">If you have more than one client cumulatively operating above the request rate, the default retry behavior may not suffice, and the client will throw a DocumentClientException with status code 429 to the application.</span></span> <span data-ttu-id="9feef-315">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing the reserved throughput for the collection.</span><span class="sxs-lookup"><span data-stu-id="9feef-315">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing the reserved throughput for the collection.</span></span>

## <a id="RequestRateTooLargeAPIforMongoDB"></a> <span data-ttu-id="9feef-316">Exceeding reserved throughput limits in API for MongoDB</span><span class="sxs-lookup"><span data-stu-id="9feef-316">Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="9feef-317">Applications that exceed the provisioned request units for a collection will be throttled until the rate drops below the reserved level.</span><span class="sxs-lookup"><span data-stu-id="9feef-317">Applications that exceed the provisioned request units for a collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="9feef-318">When a throttle occurs, the backend will preemptively end the request with a *16500* error code - *Too Many Requests*.</span><span class="sxs-lookup"><span data-stu-id="9feef-318">When a throttle occurs, the backend will preemptively end the request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="9feef-319">By default, API for MongoDB will automatically retry up to 10 times before returning a *Too Many Requests* error code.</span><span class="sxs-lookup"><span data-stu-id="9feef-319">By default, API for MongoDB will automatically retry up to 10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="9feef-320">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing the reserved throughput for the collection](documentdb-set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="9feef-320">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing the reserved throughput for the collection](documentdb-set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9feef-321">Next steps</span><span class="sxs-lookup"><span data-stu-id="9feef-321">Next steps</span></span>
<span data-ttu-id="9feef-322">To learn more about reserved throughput with Azure DocumentDB databases, explore these resources:</span><span class="sxs-lookup"><span data-stu-id="9feef-322">To learn more about reserved throughput with Azure DocumentDB databases, explore these resources:</span></span>

* [<span data-ttu-id="9feef-323">DocumentDB pricing</span><span class="sxs-lookup"><span data-stu-id="9feef-323">DocumentDB pricing</span></span>](https://azure.microsoft.com/pricing/details/documentdb/)
* [<span data-ttu-id="9feef-324">Modeling data in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="9feef-324">Modeling data in DocumentDB</span></span>](documentdb-modeling-data.md)
* [<span data-ttu-id="9feef-325">DocumentDB performance levels</span><span class="sxs-lookup"><span data-stu-id="9feef-325">DocumentDB performance levels</span></span>](documentdb-partition-data.md)

<span data-ttu-id="9feef-326">To learn more about DocumentDB, see the Azure DocumentDB [documentation](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="9feef-326">To learn more about DocumentDB, see the Azure DocumentDB [documentation](https://azure.microsoft.com/documentation/services/documentdb/).</span></span> 

<span data-ttu-id="9feef-327">To get started with scale and performance testing with DocumentDB, see [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="9feef-327">To get started with scale and performance testing with DocumentDB, see [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md).</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-request-units/queryexplorer.png 
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-request-units/RUEstimatorUpload.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-request-units/RUEstimatorDocuments.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-request-units/RUEstimatorResults.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-request-units/RUCalculator2.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-request-units/api-for-mongodb-metrics.png






