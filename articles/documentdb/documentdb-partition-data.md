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
# <a name="partitioning-partition-keys-and-scaling-in-documentdb"></a><span data-ttu-id="f7166-103">Partitioning, partition keys, and scaling in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f7166-103">Partitioning, partition keys, and scaling in DocumentDB</span></span>

<span data-ttu-id="f7166-104">[Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) is designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span><span class="sxs-lookup"><span data-stu-id="f7166-104">[Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) is designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> <span data-ttu-id="f7166-105">This article provides an overview of how partitioning works in DocumentDB, and describes how you can configure DocumentDB collections to effectively scale your applications.</span><span class="sxs-lookup"><span data-stu-id="f7166-105">This article provides an overview of how partitioning works in DocumentDB, and describes how you can configure DocumentDB collections to effectively scale your applications.</span></span>

<span data-ttu-id="f7166-106">After reading this article, you will be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="f7166-106">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="f7166-107">How does partitioning work in Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="f7166-107">How does partitioning work in Azure DocumentDB?</span></span>
* <span data-ttu-id="f7166-108">How do I configure partitioning in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f7166-108">How do I configure partitioning in DocumentDB</span></span>
* <span data-ttu-id="f7166-109">What are partition keys, and how do I pick the right partition key for my application?</span><span class="sxs-lookup"><span data-stu-id="f7166-109">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="f7166-110">To get started with code, download the project from [DocumentDB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="f7166-110">To get started with code, download the project from [DocumentDB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="f7166-111">Partitioning and partition keys are also covered in this Azure Friday video with Scott Hanselman and DocumentDB Principal Engineering Manager, Shireesh Thota.</span><span class="sxs-lookup"><span data-stu-id="f7166-111">Partitioning and partition keys are also covered in this Azure Friday video with Scott Hanselman and DocumentDB Principal Engineering Manager, Shireesh Thota.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-documentdb"></a><span data-ttu-id="f7166-112">Partitioning in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f7166-112">Partitioning in DocumentDB</span></span>
<span data-ttu-id="f7166-113">In DocumentDB, you can store and query schema-less JSON documents with order-of-millisecond response times at any scale.</span><span class="sxs-lookup"><span data-stu-id="f7166-113">In DocumentDB, you can store and query schema-less JSON documents with order-of-millisecond response times at any scale.</span></span> <span data-ttu-id="f7166-114">DocumentDB provides containers for storing data called **collections**.</span><span class="sxs-lookup"><span data-stu-id="f7166-114">DocumentDB provides containers for storing data called **collections**.</span></span> <span data-ttu-id="f7166-115">Collections are logical resources and can span one or more physical partitions or servers.</span><span class="sxs-lookup"><span data-stu-id="f7166-115">Collections are logical resources and can span one or more physical partitions or servers.</span></span> <span data-ttu-id="f7166-116">The number of partitions is determined by DocumentDB based on the storage size and the provisioned throughput of the collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-116">The number of partitions is determined by DocumentDB based on the storage size and the provisioned throughput of the collection.</span></span> <span data-ttu-id="f7166-117">Every partition in DocumentDB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span><span class="sxs-lookup"><span data-stu-id="f7166-117">Every partition in DocumentDB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span></span> <span data-ttu-id="f7166-118">Partition management is fully managed by Azure DocumentDB, and you do not have to write complex code or manage your partitions.</span><span class="sxs-lookup"><span data-stu-id="f7166-118">Partition management is fully managed by Azure DocumentDB, and you do not have to write complex code or manage your partitions.</span></span> <span data-ttu-id="f7166-119">DocumentDB collections are **practically unlimited** in terms of storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="f7166-119">DocumentDB collections are **practically unlimited** in terms of storage and throughput.</span></span> 

<span data-ttu-id="f7166-120">Partitioning is completely transparent to your application.</span><span class="sxs-lookup"><span data-stu-id="f7166-120">Partitioning is completely transparent to your application.</span></span> <span data-ttu-id="f7166-121">DocumentDB supports fast reads and writes, SQL and LINQ queries, JavaScript based transactional logic, consistency levels, and fine-grained access control via REST API calls to a single collection resource.</span><span class="sxs-lookup"><span data-stu-id="f7166-121">DocumentDB supports fast reads and writes, SQL and LINQ queries, JavaScript based transactional logic, consistency levels, and fine-grained access control via REST API calls to a single collection resource.</span></span> <span data-ttu-id="f7166-122">The service handles distributing data across partitions and routing query requests to the right partition.</span><span class="sxs-lookup"><span data-stu-id="f7166-122">The service handles distributing data across partitions and routing query requests to the right partition.</span></span> 

<span data-ttu-id="f7166-123">How does this work?</span><span class="sxs-lookup"><span data-stu-id="f7166-123">How does this work?</span></span> <span data-ttu-id="f7166-124">When you create a collection in DocumentDB, you can specify **partition key property** configuration value.</span><span class="sxs-lookup"><span data-stu-id="f7166-124">When you create a collection in DocumentDB, you can specify **partition key property** configuration value.</span></span> <span data-ttu-id="f7166-125">This is the JSON property (or path) within your documents that can be used by DocumentDB to distribute your data among multiple servers or partitions.</span><span class="sxs-lookup"><span data-stu-id="f7166-125">This is the JSON property (or path) within your documents that can be used by DocumentDB to distribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="f7166-126">DocumentDB will hash the partition key value and use the hashed result to determine the partition in which the JSON document will be stored.</span><span class="sxs-lookup"><span data-stu-id="f7166-126">DocumentDB will hash the partition key value and use the hashed result to determine the partition in which the JSON document will be stored.</span></span> <span data-ttu-id="f7166-127">All documents with the same partition key will be stored in the same partition.</span><span class="sxs-lookup"><span data-stu-id="f7166-127">All documents with the same partition key will be stored in the same partition.</span></span> 

<span data-ttu-id="f7166-128">For example, consider an application that stores data about employees and their departments in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f7166-128">For example, consider an application that stores data about employees and their departments in DocumentDB.</span></span> <span data-ttu-id="f7166-129">Let's choose `"department"` as the partition key property, in order to scale out data by department.</span><span class="sxs-lookup"><span data-stu-id="f7166-129">Let's choose `"department"` as the partition key property, in order to scale out data by department.</span></span> <span data-ttu-id="f7166-130">Every document in DocumentDB must contain a mandatory `"id"` property that must be unique for every document with the same partition key value, e.g. `"Marketing`".</span><span class="sxs-lookup"><span data-stu-id="f7166-130">Every document in DocumentDB must contain a mandatory `"id"` property that must be unique for every document with the same partition key value, e.g. `"Marketing`".</span></span> <span data-ttu-id="f7166-131">Every document stored in a collection must have a unique combination of partition key and id, e.g. `{ "Department": "Marketing", "id": "0001" }`, `{ "Department": "Marketing", "id": "0002" }`, and `{ "Department": "Sales", "id": "0001" }`.</span><span class="sxs-lookup"><span data-stu-id="f7166-131">Every document stored in a collection must have a unique combination of partition key and id, e.g. `{ "Department": "Marketing", "id": "0001" }`, `{ "Department": "Marketing", "id": "0002" }`, and `{ "Department": "Sales", "id": "0001" }`.</span></span> <span data-ttu-id="f7166-132">In other words, the compound property of (partition key, id) is the primary key for your collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-132">In other words, the compound property of (partition key, id) is the primary key for your collection.</span></span>

<span data-ttu-id="f7166-133">DocumentDB creates a small number of physical partitions behind each collection based on storage size and provisioned throughput.</span><span class="sxs-lookup"><span data-stu-id="f7166-133">DocumentDB creates a small number of physical partitions behind each collection based on storage size and provisioned throughput.</span></span> <span data-ttu-id="f7166-134">The property that you define as partition key is a logical partition.</span><span class="sxs-lookup"><span data-stu-id="f7166-134">The property that you define as partition key is a logical partition.</span></span> <span data-ttu-id="f7166-135">Multiple partition key values typically share a single physical partition, but a single value will never span a partition.</span><span class="sxs-lookup"><span data-stu-id="f7166-135">Multiple partition key values typically share a single physical partition, but a single value will never span a partition.</span></span> <span data-ttu-id="f7166-136">If you have a partition key with a lot of values, it’s good because DocumentDB will be able to perform better load balancing as your data grows or you increase the provisioned throughput.</span><span class="sxs-lookup"><span data-stu-id="f7166-136">If you have a partition key with a lot of values, it’s good because DocumentDB will be able to perform better load balancing as your data grows or you increase the provisioned throughput.</span></span>

<span data-ttu-id="f7166-137">For example, let’s say you create a collection with 25,000 requests per second throughput and DocumentDB can support 10,000 requests per second per single physical partition.</span><span class="sxs-lookup"><span data-stu-id="f7166-137">For example, let’s say you create a collection with 25,000 requests per second throughput and DocumentDB can support 10,000 requests per second per single physical partition.</span></span> <span data-ttu-id="f7166-138">DocumentDB would create 3 physical partitions P1, P2, and P3 for your collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-138">DocumentDB would create 3 physical partitions P1, P2, and P3 for your collection.</span></span> <span data-ttu-id="f7166-139">During the insertion or read of a document, the DocumentDB service hashes the corresponding `Department` value to map data to the three partitions P1, P2, and P3.</span><span class="sxs-lookup"><span data-stu-id="f7166-139">During the insertion or read of a document, the DocumentDB service hashes the corresponding `Department` value to map data to the three partitions P1, P2, and P3.</span></span> <span data-ttu-id="f7166-140">So for example, if “Marketing” and “Sales” hash to 1, they are both stored in P1.</span><span class="sxs-lookup"><span data-stu-id="f7166-140">So for example, if “Marketing” and “Sales” hash to 1, they are both stored in P1.</span></span> <span data-ttu-id="f7166-141">And if P1 becomes full, DocumentDB splits P1 into two new partitions P4 and P5.</span><span class="sxs-lookup"><span data-stu-id="f7166-141">And if P1 becomes full, DocumentDB splits P1 into two new partitions P4 and P5.</span></span> <span data-ttu-id="f7166-142">Then the service might move “Marketing” to P4 and “Sales” to P5 after the split, then drop P1.</span><span class="sxs-lookup"><span data-stu-id="f7166-142">Then the service might move “Marketing” to P4 and “Sales” to P5 after the split, then drop P1.</span></span> <span data-ttu-id="f7166-143">These moves of partition keys between partitions are transparent to your application, and have no impact to the availability of your collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-143">These moves of partition keys between partitions are transparent to your application, and have no impact to the availability of your collection.</span></span>

## <a name="sharding-in-api-for-mongodb"></a><span data-ttu-id="f7166-144">Sharding in API for MongoDB</span><span class="sxs-lookup"><span data-stu-id="f7166-144">Sharding in API for MongoDB</span></span>
<span data-ttu-id="f7166-145">Sharded collections in API for MongoDB are using the same infrastructure as DocumentDB's partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="f7166-145">Sharded collections in API for MongoDB are using the same infrastructure as DocumentDB's partitioned collections.</span></span> <span data-ttu-id="f7166-146">Like partitioned collections, sharded collections can have any number of shards and each shard has a fixed amount of SSD-backed storage associated with it.</span><span class="sxs-lookup"><span data-stu-id="f7166-146">Like partitioned collections, sharded collections can have any number of shards and each shard has a fixed amount of SSD-backed storage associated with it.</span></span> <span data-ttu-id="f7166-147">Sharded collections are practically unlimited in terms of storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="f7166-147">Sharded collections are practically unlimited in terms of storage and throughput.</span></span> <span data-ttu-id="f7166-148">API for MongoDB's shard key is equivalent to DocumentDB's partition key and when deciding a shard key, make sure to read the [Partition keys](#partition-keys) and [Designing for partitioning](#designing-for-partitioning) sections.</span><span class="sxs-lookup"><span data-stu-id="f7166-148">API for MongoDB's shard key is equivalent to DocumentDB's partition key and when deciding a shard key, make sure to read the [Partition keys](#partition-keys) and [Designing for partitioning](#designing-for-partitioning) sections.</span></span>

<a name="partition-keys"></a>
## <a name="partition-keys"></a><span data-ttu-id="f7166-149">Partition keys</span><span class="sxs-lookup"><span data-stu-id="f7166-149">Partition keys</span></span>
<span data-ttu-id="f7166-150">The choice of the partition key is an important decision that you’ll have to make at design time.</span><span class="sxs-lookup"><span data-stu-id="f7166-150">The choice of the partition key is an important decision that you’ll have to make at design time.</span></span> <span data-ttu-id="f7166-151">You must pick a JSON property name that has a wide range of values and is likely to have evenly distributed access patterns.</span><span class="sxs-lookup"><span data-stu-id="f7166-151">You must pick a JSON property name that has a wide range of values and is likely to have evenly distributed access patterns.</span></span> 

> [!NOTE]
> <span data-ttu-id="f7166-152">It is a best practice to have a partition key with a large number of distinct values (100s-1000s at a minimum).</span><span class="sxs-lookup"><span data-stu-id="f7166-152">It is a best practice to have a partition key with a large number of distinct values (100s-1000s at a minimum).</span></span> <span data-ttu-id="f7166-153">Many customers use DocumentDB as effectively a key value store, where the unique “id” is the partition key of millions-billions of partition keys.</span><span class="sxs-lookup"><span data-stu-id="f7166-153">Many customers use DocumentDB as effectively a key value store, where the unique “id” is the partition key of millions-billions of partition keys.</span></span>
>

<span data-ttu-id="f7166-154">The following table shows examples of partition key definitions and the JSON values corresponding to each.</span><span class="sxs-lookup"><span data-stu-id="f7166-154">The following table shows examples of partition key definitions and the JSON values corresponding to each.</span></span> <span data-ttu-id="f7166-155">The partition key is specified as a JSON path, e.g. `/department` represents the property department.</span><span class="sxs-lookup"><span data-stu-id="f7166-155">The partition key is specified as a JSON path, e.g. `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-156"><strong>Partition Key Path</strong></span><span class="sxs-lookup"><span data-stu-id="f7166-156"><strong>Partition Key Path</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-157"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="f7166-157"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-158">/department</span><span class="sxs-lookup"><span data-stu-id="f7166-158">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-159">Corresponds to the JSON value of doc.department where doc is the document.</span><span class="sxs-lookup"><span data-stu-id="f7166-159">Corresponds to the JSON value of doc.department where doc is the document.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-160">/properties/name</span><span class="sxs-lookup"><span data-stu-id="f7166-160">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-161">Corresponds to the JSON value of doc.properties.name where doc is the document (nested property).</span><span class="sxs-lookup"><span data-stu-id="f7166-161">Corresponds to the JSON value of doc.properties.name where doc is the document (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-162">/id</span><span class="sxs-lookup"><span data-stu-id="f7166-162">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-163">Corresponds to the JSON value of doc.id (id and partition key are the same property).</span><span class="sxs-lookup"><span data-stu-id="f7166-163">Corresponds to the JSON value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-164">/"department name"</span><span class="sxs-lookup"><span data-stu-id="f7166-164">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-165">Corresponds to the JSON value of doc["department name"] where doc is the document.</span><span class="sxs-lookup"><span data-stu-id="f7166-165">Corresponds to the JSON value of doc["department name"] where doc is the document.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="f7166-166">The syntax for partition key path is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span><span class="sxs-lookup"><span data-stu-id="f7166-166">The syntax for partition key path is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="f7166-167">For example, you would specify /department/?</span><span class="sxs-lookup"><span data-stu-id="f7166-167">For example, you would specify /department/?</span></span> <span data-ttu-id="f7166-168">to index the values under department, but specify /department as the partition key definition.</span><span class="sxs-lookup"><span data-stu-id="f7166-168">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="f7166-169">The partition key path is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span><span class="sxs-lookup"><span data-stu-id="f7166-169">The partition key path is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="f7166-170">Let's look at how the choice of partition key impacts the performance of your application.</span><span class="sxs-lookup"><span data-stu-id="f7166-170">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="partitioning-and-provisioned-throughput"></a><span data-ttu-id="f7166-171">Partitioning and provisioned throughput</span><span class="sxs-lookup"><span data-stu-id="f7166-171">Partitioning and provisioned throughput</span></span>
<span data-ttu-id="f7166-172">DocumentDB is designed for predictable performance.</span><span class="sxs-lookup"><span data-stu-id="f7166-172">DocumentDB is designed for predictable performance.</span></span> <span data-ttu-id="f7166-173">When you create a collection, you reserve throughput in terms of **[request units](documentdb-request-units.md) (RU) per second**.</span><span class="sxs-lookup"><span data-stu-id="f7166-173">When you create a collection, you reserve throughput in terms of **[request units](documentdb-request-units.md) (RU) per second**.</span></span> <span data-ttu-id="f7166-174">Each request is assigned a request unit charge that is proportionate to the amount of system resources like CPU and IO consumed by the operation.</span><span class="sxs-lookup"><span data-stu-id="f7166-174">Each request is assigned a request unit charge that is proportionate to the amount of system resources like CPU and IO consumed by the operation.</span></span> <span data-ttu-id="f7166-175">A read of a 1 kB document with Session consistency consumes 1 request unit.</span><span class="sxs-lookup"><span data-stu-id="f7166-175">A read of a 1 kB document with Session consistency consumes 1 request unit.</span></span> <span data-ttu-id="f7166-176">A read is 1 RU regardless of the number of items stored or the number of concurrent requests running at the same time.</span><span class="sxs-lookup"><span data-stu-id="f7166-176">A read is 1 RU regardless of the number of items stored or the number of concurrent requests running at the same time.</span></span> <span data-ttu-id="f7166-177">Larger documents require higher request units depending on the size.</span><span class="sxs-lookup"><span data-stu-id="f7166-177">Larger documents require higher request units depending on the size.</span></span> <span data-ttu-id="f7166-178">If you know the size of your entities and the number of reads you need to support for your application, you can provision the exact amount of throughput required for your application's read needs.</span><span class="sxs-lookup"><span data-stu-id="f7166-178">If you know the size of your entities and the number of reads you need to support for your application, you can provision the exact amount of throughput required for your application's read needs.</span></span> 

<span data-ttu-id="f7166-179">When DocumentDB stores documents, it distributes them evenly among partitions based on the partition key value.</span><span class="sxs-lookup"><span data-stu-id="f7166-179">When DocumentDB stores documents, it distributes them evenly among partitions based on the partition key value.</span></span> <span data-ttu-id="f7166-180">The throughput is also distributed evenly among the available partitions i.e. the throughput per partition = (total throughput per collection)/ (number of partitions).</span><span class="sxs-lookup"><span data-stu-id="f7166-180">The throughput is also distributed evenly among the available partitions i.e. the throughput per partition = (total throughput per collection)/ (number of partitions).</span></span> 

> [!NOTE]
> <span data-ttu-id="f7166-181">In order to achieve the full throughput of the collection, you must choose a partition key that allows you to evenly distribute requests among a number of distinct partition key values.</span><span class="sxs-lookup"><span data-stu-id="f7166-181">In order to achieve the full throughput of the collection, you must choose a partition key that allows you to evenly distribute requests among a number of distinct partition key values.</span></span>
> 
> 

## <a name="single-partition-and-partitioned-collections"></a><span data-ttu-id="f7166-182">Single partition and partitioned collections</span><span class="sxs-lookup"><span data-stu-id="f7166-182">Single partition and partitioned collections</span></span>
<span data-ttu-id="f7166-183">DocumentDB supports the creation of both single-partition and partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="f7166-183">DocumentDB supports the creation of both single-partition and partitioned collections.</span></span> 

* <span data-ttu-id="f7166-184">**Partitioned collections** can span multiple partitions and support unlimited storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="f7166-184">**Partitioned collections** can span multiple partitions and support unlimited storage and throughput.</span></span> <span data-ttu-id="f7166-185">You must specify a partition key for the collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-185">You must specify a partition key for the collection.</span></span> 
* <span data-ttu-id="f7166-186">**Single-partition collections** have lower price options, but they are limited in terms of maximum low storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="f7166-186">**Single-partition collections** have lower price options, but they are limited in terms of maximum low storage and throughput.</span></span> <span data-ttu-id="f7166-187">You do not have to specify a partition key for these collections.</span><span class="sxs-lookup"><span data-stu-id="f7166-187">You do not have to specify a partition key for these collections.</span></span> <span data-ttu-id="f7166-188">We recommend using partitioned collections over single-partitioned collections for all scenarios, except in situations where you expect only a small amount of data storage and requests.</span><span class="sxs-lookup"><span data-stu-id="f7166-188">We recommend using partitioned collections over single-partitioned collections for all scenarios, except in situations where you expect only a small amount of data storage and requests.</span></span>

![Partitioned collections in DocumentDB][2] 

<span data-ttu-id="f7166-190">Partitioned collections can support unlimited storage and throughput.</span><span class="sxs-lookup"><span data-stu-id="f7166-190">Partitioned collections can support unlimited storage and throughput.</span></span>

<span data-ttu-id="f7166-191">The following table lists differences in working with a single-partition and partitioned collections:</span><span class="sxs-lookup"><span data-stu-id="f7166-191">The following table lists differences in working with a single-partition and partitioned collections:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-192"><strong>Single Partition Collection</strong></span><span class="sxs-lookup"><span data-stu-id="f7166-192"><strong>Single Partition Collection</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-193"><strong>Partitioned Collection</strong></span><span class="sxs-lookup"><span data-stu-id="f7166-193"><strong>Partitioned Collection</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-194">Partition Key</span><span class="sxs-lookup"><span data-stu-id="f7166-194">Partition Key</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-195">None</span><span class="sxs-lookup"><span data-stu-id="f7166-195">None</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-196">Required</span><span class="sxs-lookup"><span data-stu-id="f7166-196">Required</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-197">Primary Key for Document</span><span class="sxs-lookup"><span data-stu-id="f7166-197">Primary Key for Document</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-198">"id"</span><span class="sxs-lookup"><span data-stu-id="f7166-198">"id"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-199">compound key &lt;partition key&gt; and "id"</span><span class="sxs-lookup"><span data-stu-id="f7166-199">compound key &lt;partition key&gt; and "id"</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-200">Minimum Storage</span><span class="sxs-lookup"><span data-stu-id="f7166-200">Minimum Storage</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-201">0 GB</span><span class="sxs-lookup"><span data-stu-id="f7166-201">0 GB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-202">0 GB</span><span class="sxs-lookup"><span data-stu-id="f7166-202">0 GB</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-203">Maximum Storage</span><span class="sxs-lookup"><span data-stu-id="f7166-203">Maximum Storage</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-204">10 GB</span><span class="sxs-lookup"><span data-stu-id="f7166-204">10 GB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-205">Unlimited</span><span class="sxs-lookup"><span data-stu-id="f7166-205">Unlimited</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-206">Minimum Throughput</span><span class="sxs-lookup"><span data-stu-id="f7166-206">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-207">400 request units per second</span><span class="sxs-lookup"><span data-stu-id="f7166-207">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-208">2,500 request units per second</span><span class="sxs-lookup"><span data-stu-id="f7166-208">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-209">Maximum Throughput</span><span class="sxs-lookup"><span data-stu-id="f7166-209">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-210">10,000 request units per second</span><span class="sxs-lookup"><span data-stu-id="f7166-210">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-211">Unlimited</span><span class="sxs-lookup"><span data-stu-id="f7166-211">Unlimited</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f7166-212">API versions</span><span class="sxs-lookup"><span data-stu-id="f7166-212">API versions</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-213">All</span><span class="sxs-lookup"><span data-stu-id="f7166-213">All</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f7166-214">API 2015-12-16 and newer</span><span class="sxs-lookup"><span data-stu-id="f7166-214">API 2015-12-16 and newer</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="working-with-the-documentdb-sdks"></a><span data-ttu-id="f7166-215">Working with the DocumentDB SDKs</span><span class="sxs-lookup"><span data-stu-id="f7166-215">Working with the DocumentDB SDKs</span></span>
<span data-ttu-id="f7166-216">Azure DocumentDB added support for automatic partitioning with [REST API version 2015-12-16](https://msdn.microsoft.com/library/azure/dn781481.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7166-216">Azure DocumentDB added support for automatic partitioning with [REST API version 2015-12-16](https://msdn.microsoft.com/library/azure/dn781481.aspx).</span></span> <span data-ttu-id="f7166-217">In order to create partitioned collections, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python).</span><span class="sxs-lookup"><span data-stu-id="f7166-217">In order to create partitioned collections, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python).</span></span> 

### <a name="creating-partitioned-collections"></a><span data-ttu-id="f7166-218">Creating partitioned collections</span><span class="sxs-lookup"><span data-stu-id="f7166-218">Creating partitioned collections</span></span>
<span data-ttu-id="f7166-219">The following sample shows a .NET snippet to create a collection to store device telemetry data of 20,000 request units per second of throughput.</span><span class="sxs-lookup"><span data-stu-id="f7166-219">The following sample shows a .NET snippet to create a collection to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="f7166-220">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span><span class="sxs-lookup"><span data-stu-id="f7166-220">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="f7166-221">Here we set the `/deviceId` as the partition key.</span><span class="sxs-lookup"><span data-stu-id="f7166-221">Here we set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="f7166-222">The choice of partition key is saved along with the rest of the collection metadata like name and indexing policy.</span><span class="sxs-lookup"><span data-stu-id="f7166-222">The choice of partition key is saved along with the rest of the collection metadata like name and indexing policy.</span></span>

<span data-ttu-id="f7166-223">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span><span class="sxs-lookup"><span data-stu-id="f7166-223">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

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
> <span data-ttu-id="f7166-224">In order to create partitioned collections using the SDK, you must specify a throughput value equal or greater than 10,100 RU/s.</span><span class="sxs-lookup"><span data-stu-id="f7166-224">In order to create partitioned collections using the SDK, you must specify a throughput value equal or greater than 10,100 RU/s.</span></span> <span data-ttu-id="f7166-225">To set a throughput value between 2,500 and 10,000 for partitioned collections you must temporarily use the Azure portal, as these new lower values are not yet available in the SDK.</span><span class="sxs-lookup"><span data-stu-id="f7166-225">To set a throughput value between 2,500 and 10,000 for partitioned collections you must temporarily use the Azure portal, as these new lower values are not yet available in the SDK.</span></span>
> 
> 

<span data-ttu-id="f7166-226">This method makes a REST API call to DocumentDB, and the service will provision a number of partitions based on the requested throughput.</span><span class="sxs-lookup"><span data-stu-id="f7166-226">This method makes a REST API call to DocumentDB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="f7166-227">You can change the throughput of a collection as your performance needs evolve.</span><span class="sxs-lookup"><span data-stu-id="f7166-227">You can change the throughput of a collection as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-documents"></a><span data-ttu-id="f7166-228">Reading and writing documents</span><span class="sxs-lookup"><span data-stu-id="f7166-228">Reading and writing documents</span></span>
<span data-ttu-id="f7166-229">Now, let's insert data into DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f7166-229">Now, let's insert data into DocumentDB.</span></span> <span data-ttu-id="f7166-230">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-230">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a collection.</span></span>

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

<span data-ttu-id="f7166-231">Let's read the document by it's partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span><span class="sxs-lookup"><span data-stu-id="f7166-231">Let's read the document by it's partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

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

### <a name="querying-partitioned-collections"></a><span data-ttu-id="f7166-232">Querying partitioned collections</span><span class="sxs-lookup"><span data-stu-id="f7166-232">Querying partitioned collections</span></span>
<span data-ttu-id="f7166-233">When you query data in partitioned collections, DocumentDB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span><span class="sxs-lookup"><span data-stu-id="f7166-233">When you query data in partitioned collections, DocumentDB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="f7166-234">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="f7166-234">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="f7166-235">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span><span class="sxs-lookup"><span data-stu-id="f7166-235">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="f7166-236">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span><span class="sxs-lookup"><span data-stu-id="f7166-236">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="f7166-237">DocumentDB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned collections using SQL starting with SDKs 1.12.0 and above.</span><span class="sxs-lookup"><span data-stu-id="f7166-237">DocumentDB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned collections using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="f7166-238">Queries must include a single aggregate operator, and must include a single value in the projection.</span><span class="sxs-lookup"><span data-stu-id="f7166-238">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="f7166-239">Parallel query execution</span><span class="sxs-lookup"><span data-stu-id="f7166-239">Parallel query execution</span></span>
<span data-ttu-id="f7166-240">The DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span><span class="sxs-lookup"><span data-stu-id="f7166-240">The DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="f7166-241">For example, the following query is configured to run in parallel across partitions.</span><span class="sxs-lookup"><span data-stu-id="f7166-241">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="f7166-242">You can manage parallel query execution by tuning the following parameters:</span><span class="sxs-lookup"><span data-stu-id="f7166-242">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="f7166-243">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the collection's partitions.</span><span class="sxs-lookup"><span data-stu-id="f7166-243">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the collection's partitions.</span></span> <span data-ttu-id="f7166-244">If you set this to -1, the degree of parallelism is managed by the SDK.</span><span class="sxs-lookup"><span data-stu-id="f7166-244">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="f7166-245">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the collection's partitions.</span><span class="sxs-lookup"><span data-stu-id="f7166-245">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the collection's partitions.</span></span>
* <span data-ttu-id="f7166-246">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span><span class="sxs-lookup"><span data-stu-id="f7166-246">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="f7166-247">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span><span class="sxs-lookup"><span data-stu-id="f7166-247">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="f7166-248">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span><span class="sxs-lookup"><span data-stu-id="f7166-248">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="f7166-249">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the DocumentDB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span><span class="sxs-lookup"><span data-stu-id="f7166-249">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the DocumentDB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="f7166-250">Executing stored procedures</span><span class="sxs-lookup"><span data-stu-id="f7166-250">Executing stored procedures</span></span>
<span data-ttu-id="f7166-251">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single document.</span><span class="sxs-lookup"><span data-stu-id="f7166-251">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single document.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
    
<span data-ttu-id="f7166-252">In the next section, we look at how you can move to partitioned collections from single-partition collections.</span><span class="sxs-lookup"><span data-stu-id="f7166-252">In the next section, we look at how you can move to partitioned collections from single-partition collections.</span></span>

## <a name="creating-an-api-for-mongodb-sharded-collection"></a><span data-ttu-id="f7166-253">Creating an API for MongoDB sharded collection</span><span class="sxs-lookup"><span data-stu-id="f7166-253">Creating an API for MongoDB sharded collection</span></span>
<span data-ttu-id="f7166-254">The simplest way to create an API for MongoDB sharded collection is through your favorite tool, driver, or SDK.</span><span class="sxs-lookup"><span data-stu-id="f7166-254">The simplest way to create an API for MongoDB sharded collection is through your favorite tool, driver, or SDK.</span></span> <span data-ttu-id="f7166-255">In this example, we will use the Mongo Shell for the collection creation.</span><span class="sxs-lookup"><span data-stu-id="f7166-255">In this example, we will use the Mongo Shell for the collection creation.</span></span>

<span data-ttu-id="f7166-256">In the Mongo Shell:</span><span class="sxs-lookup"><span data-stu-id="f7166-256">In the Mongo Shell:</span></span>

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
<span data-ttu-id="f7166-257">Results:</span><span class="sxs-lookup"><span data-stu-id="f7166-257">Results:</span></span>

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

<a name="migrating-from-single-partition"></a>

## <a name="migrating-from-single-partition-to-partitioned-collections-in-documentdb"></a><span data-ttu-id="f7166-258">Migrating from single-partition to partitioned collections in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f7166-258">Migrating from single-partition to partitioned collections in DocumentDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7166-259">If you are importing to API for MongoDB, follow these [instructions](documentdb-mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="f7166-259">If you are importing to API for MongoDB, follow these [instructions](documentdb-mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="f7166-260">When an application using a single-partition collection needs higher throughput (>10,000 RU/s) or larger data storage (>10GB), you can use the [DocumentDB Data Migration Tool](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) to migrate the data from the single-partition collection to a partitioned collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-260">When an application using a single-partition collection needs higher throughput (>10,000 RU/s) or larger data storage (>10GB), you can use the [DocumentDB Data Migration Tool](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) to migrate the data from the single-partition collection to a partitioned collection.</span></span> 

<span data-ttu-id="f7166-261">To migrate from a single-partition collection to a partitioned collection</span><span class="sxs-lookup"><span data-stu-id="f7166-261">To migrate from a single-partition collection to a partitioned collection</span></span>

1. <span data-ttu-id="f7166-262">Export data from the single-partition collection to JSON.</span><span class="sxs-lookup"><span data-stu-id="f7166-262">Export data from the single-partition collection to JSON.</span></span> <span data-ttu-id="f7166-263">See [Export to JSON file](documentdb-import-data.md#export-to-json-file) for additional details.</span><span class="sxs-lookup"><span data-stu-id="f7166-263">See [Export to JSON file](documentdb-import-data.md#export-to-json-file) for additional details.</span></span>
2. <span data-ttu-id="f7166-264">Import the data into a partitioned collection created with a partition key definition and over 2,500 request units per second throughput, as shown in the example below.</span><span class="sxs-lookup"><span data-stu-id="f7166-264">Import the data into a partitioned collection created with a partition key definition and over 2,500 request units per second throughput, as shown in the example below.</span></span> <span data-ttu-id="f7166-265">See [Import to DocumentDB](documentdb-import-data.md#DocumentDBSeqTarget) for additional details.</span><span class="sxs-lookup"><span data-stu-id="f7166-265">See [Import to DocumentDB](documentdb-import-data.md#DocumentDBSeqTarget) for additional details.</span></span>

![Migrating Data to a Partitioned collection in DocumentDB][3]  

> [!TIP]
> <span data-ttu-id="f7166-267">For faster import times, consider increasing the Number of Parallel Requests to 100 or higher to take advantage of the higher throughput available for partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="f7166-267">For faster import times, consider increasing the Number of Parallel Requests to 100 or higher to take advantage of the higher throughput available for partitioned collections.</span></span> 
> 
> 

<span data-ttu-id="f7166-268">Now that we've completed the basics, let's look at a few important design considerations when working with partition keys in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f7166-268">Now that we've completed the basics, let's look at a few important design considerations when working with partition keys in DocumentDB.</span></span>

<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a><span data-ttu-id="f7166-269">Designing for partitioning</span><span class="sxs-lookup"><span data-stu-id="f7166-269">Designing for partitioning</span></span>
<span data-ttu-id="f7166-270">The choice of the partition key is an important decision that you’ll have to make at design time.</span><span class="sxs-lookup"><span data-stu-id="f7166-270">The choice of the partition key is an important decision that you’ll have to make at design time.</span></span> <span data-ttu-id="f7166-271">This section describes some of the tradeoffs involved in selecting a partition key for your collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-271">This section describes some of the tradeoffs involved in selecting a partition key for your collection.</span></span>

### <a name="partition-key-as-the-transaction-boundary"></a><span data-ttu-id="f7166-272">Partition key as the transaction boundary</span><span class="sxs-lookup"><span data-stu-id="f7166-272">Partition key as the transaction boundary</span></span>
<span data-ttu-id="f7166-273">Your choice of partition key should balance the need to enable the use of transactions against the requirement to distribute your entities across multiple partition keys to ensure a scalable solution.</span><span class="sxs-lookup"><span data-stu-id="f7166-273">Your choice of partition key should balance the need to enable the use of transactions against the requirement to distribute your entities across multiple partition keys to ensure a scalable solution.</span></span> <span data-ttu-id="f7166-274">At one extreme, you could set the same partition key for all your documents, but this may limit the scalability of your solution.</span><span class="sxs-lookup"><span data-stu-id="f7166-274">At one extreme, you could set the same partition key for all your documents, but this may limit the scalability of your solution.</span></span> <span data-ttu-id="f7166-275">At the other extreme, you could assign a unique partition key for each document, which would be highly scalable but would prevent you from using cross document transactions via stored procedures and triggers.</span><span class="sxs-lookup"><span data-stu-id="f7166-275">At the other extreme, you could assign a unique partition key for each document, which would be highly scalable but would prevent you from using cross document transactions via stored procedures and triggers.</span></span> <span data-ttu-id="f7166-276">An ideal partition key is one that enables you to use efficient queries and that has sufficient cardinality to ensure your solution is scalable.</span><span class="sxs-lookup"><span data-stu-id="f7166-276">An ideal partition key is one that enables you to use efficient queries and that has sufficient cardinality to ensure your solution is scalable.</span></span> 

### <a name="avoiding-storage-and-performance-bottlenecks"></a><span data-ttu-id="f7166-277">Avoiding storage and performance bottlenecks</span><span class="sxs-lookup"><span data-stu-id="f7166-277">Avoiding storage and performance bottlenecks</span></span>
<span data-ttu-id="f7166-278">It is also important to pick a property which allows writes to be distributed across a number of distinct values.</span><span class="sxs-lookup"><span data-stu-id="f7166-278">It is also important to pick a property which allows writes to be distributed across a number of distinct values.</span></span> <span data-ttu-id="f7166-279">Requests to the same partition key cannot exceed the throughput of a single partition, and will be throttled.</span><span class="sxs-lookup"><span data-stu-id="f7166-279">Requests to the same partition key cannot exceed the throughput of a single partition, and will be throttled.</span></span> <span data-ttu-id="f7166-280">So it is important to pick a partition key that does not result in **"hot spots"** within your application.</span><span class="sxs-lookup"><span data-stu-id="f7166-280">So it is important to pick a partition key that does not result in **"hot spots"** within your application.</span></span> <span data-ttu-id="f7166-281">Since all the data for a single partition key must be stored within a partition, it is also recommended to avoid partition keys that have high volumes of data for the same value.</span><span class="sxs-lookup"><span data-stu-id="f7166-281">Since all the data for a single partition key must be stored within a partition, it is also recommended to avoid partition keys that have high volumes of data for the same value.</span></span> 

### <a name="examples-of-good-partition-keys"></a><span data-ttu-id="f7166-282">Examples of good partition keys</span><span class="sxs-lookup"><span data-stu-id="f7166-282">Examples of good partition keys</span></span>
<span data-ttu-id="f7166-283">Here are a few examples for how to pick the partition key for your application:</span><span class="sxs-lookup"><span data-stu-id="f7166-283">Here are a few examples for how to pick the partition key for your application:</span></span>

* <span data-ttu-id="f7166-284">If you’re implementing a user profile backend, then the user ID is a good choice for partition key.</span><span class="sxs-lookup"><span data-stu-id="f7166-284">If you’re implementing a user profile backend, then the user ID is a good choice for partition key.</span></span>
* <span data-ttu-id="f7166-285">If you’re storing IoT data e.g. device state, a device ID is a good choice for partition key.</span><span class="sxs-lookup"><span data-stu-id="f7166-285">If you’re storing IoT data e.g. device state, a device ID is a good choice for partition key.</span></span>
* <span data-ttu-id="f7166-286">If you’re using DocumentDB for logging time-series data, then the hostname or process ID is a good choice for partition key.</span><span class="sxs-lookup"><span data-stu-id="f7166-286">If you’re using DocumentDB for logging time-series data, then the hostname or process ID is a good choice for partition key.</span></span>
* <span data-ttu-id="f7166-287">If you have a multi-tenant architecture, the tenant ID is a good choice for partition key.</span><span class="sxs-lookup"><span data-stu-id="f7166-287">If you have a multi-tenant architecture, the tenant ID is a good choice for partition key.</span></span>

<span data-ttu-id="f7166-288">Note that in some use cases (like the IoT and user profiles described above), the partition key might be the same as your id (document key).</span><span class="sxs-lookup"><span data-stu-id="f7166-288">Note that in some use cases (like the IoT and user profiles described above), the partition key might be the same as your id (document key).</span></span> <span data-ttu-id="f7166-289">In others like the time series data, you might have a partition key that’s different than the id.</span><span class="sxs-lookup"><span data-stu-id="f7166-289">In others like the time series data, you might have a partition key that’s different than the id.</span></span>

### <a name="partitioning-and-loggingtime-series-data"></a><span data-ttu-id="f7166-290">Partitioning and logging/time-series data</span><span class="sxs-lookup"><span data-stu-id="f7166-290">Partitioning and logging/time-series data</span></span>
<span data-ttu-id="f7166-291">One of the most common use cases of DocumentDB is for logging and telemetry.</span><span class="sxs-lookup"><span data-stu-id="f7166-291">One of the most common use cases of DocumentDB is for logging and telemetry.</span></span> <span data-ttu-id="f7166-292">It is important to pick a good partition key since you might need to read/write vast volumes of data.</span><span class="sxs-lookup"><span data-stu-id="f7166-292">It is important to pick a good partition key since you might need to read/write vast volumes of data.</span></span> <span data-ttu-id="f7166-293">The choice will depend on your read and write rates and kinds of queries you expect to run.</span><span class="sxs-lookup"><span data-stu-id="f7166-293">The choice will depend on your read and write rates and kinds of queries you expect to run.</span></span> <span data-ttu-id="f7166-294">Here are some tips on how to choose a good partition key.</span><span class="sxs-lookup"><span data-stu-id="f7166-294">Here are some tips on how to choose a good partition key.</span></span>

* <span data-ttu-id="f7166-295">If your use case involves a small rate of writes acculumating over a long period of time, and need to query by ranges of timestamps and other filters, then using a rollup of the timestamp e.g. date as a partition key is a good approach.</span><span class="sxs-lookup"><span data-stu-id="f7166-295">If your use case involves a small rate of writes acculumating over a long period of time, and need to query by ranges of timestamps and other filters, then using a rollup of the timestamp e.g. date as a partition key is a good approach.</span></span> <span data-ttu-id="f7166-296">This allows you to query over all the data for a date from a single partition.</span><span class="sxs-lookup"><span data-stu-id="f7166-296">This allows you to query over all the data for a date from a single partition.</span></span> 
* <span data-ttu-id="f7166-297">If your workload is write heavy, which is generally more common, you should use a partition key that’s not based on timestamp so that DocumentDB can distribute writes evenly across a number of partitions.</span><span class="sxs-lookup"><span data-stu-id="f7166-297">If your workload is write heavy, which is generally more common, you should use a partition key that’s not based on timestamp so that DocumentDB can distribute writes evenly across a number of partitions.</span></span> <span data-ttu-id="f7166-298">Here a hostname, process ID, activity ID, or another property with high cardinality is a good choice.</span><span class="sxs-lookup"><span data-stu-id="f7166-298">Here a hostname, process ID, activity ID, or another property with high cardinality is a good choice.</span></span> 
* <span data-ttu-id="f7166-299">A third approach is a hybrid one where you have multiple collections, one for each day/month and the partition key is a granular property like hostname.</span><span class="sxs-lookup"><span data-stu-id="f7166-299">A third approach is a hybrid one where you have multiple collections, one for each day/month and the partition key is a granular property like hostname.</span></span> <span data-ttu-id="f7166-300">This has the benefit that you can set different throughput based on the time window, e.g. the collection for the current month is provisioned with higher throughput since it serves reads and writes, whereas previous months with lower throughput since they only serve reads.</span><span class="sxs-lookup"><span data-stu-id="f7166-300">This has the benefit that you can set different throughput based on the time window, e.g. the collection for the current month is provisioned with higher throughput since it serves reads and writes, whereas previous months with lower throughput since they only serve reads.</span></span>

### <a name="partitioning-and-multi-tenancy"></a><span data-ttu-id="f7166-301">Partitioning and multi-tenancy</span><span class="sxs-lookup"><span data-stu-id="f7166-301">Partitioning and multi-tenancy</span></span>
<span data-ttu-id="f7166-302">If you are implementing a multi-tenant application using DocumentDB, there are two major patterns for implementing tenancy with DocumentDB – one partition key per tenant, and one collection per tenant.</span><span class="sxs-lookup"><span data-stu-id="f7166-302">If you are implementing a multi-tenant application using DocumentDB, there are two major patterns for implementing tenancy with DocumentDB – one partition key per tenant, and one collection per tenant.</span></span> <span data-ttu-id="f7166-303">Here are the pros and cons for each:</span><span class="sxs-lookup"><span data-stu-id="f7166-303">Here are the pros and cons for each:</span></span>

* <span data-ttu-id="f7166-304">One Partition Key per tenant: In this model, tenants are collocated within a single collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-304">One Partition Key per tenant: In this model, tenants are collocated within a single collection.</span></span> <span data-ttu-id="f7166-305">But queries and inserts for documents within a single tenant can be performed against a single partition.</span><span class="sxs-lookup"><span data-stu-id="f7166-305">But queries and inserts for documents within a single tenant can be performed against a single partition.</span></span> <span data-ttu-id="f7166-306">You can also implement transactional logic across all documents within a tenant.</span><span class="sxs-lookup"><span data-stu-id="f7166-306">You can also implement transactional logic across all documents within a tenant.</span></span> <span data-ttu-id="f7166-307">Since multiple tenants share a collection, you can save storage and throughput costs by pooling resources for tenants within a single collection rather than provisioning extra headroom for each tenant.</span><span class="sxs-lookup"><span data-stu-id="f7166-307">Since multiple tenants share a collection, you can save storage and throughput costs by pooling resources for tenants within a single collection rather than provisioning extra headroom for each tenant.</span></span> <span data-ttu-id="f7166-308">The drawback is that you do not have performance isolation per tenant.</span><span class="sxs-lookup"><span data-stu-id="f7166-308">The drawback is that you do not have performance isolation per tenant.</span></span> <span data-ttu-id="f7166-309">Performance/throughput increases apply to the entire collection vs targeted increases for tenants.</span><span class="sxs-lookup"><span data-stu-id="f7166-309">Performance/throughput increases apply to the entire collection vs targeted increases for tenants.</span></span>
* <span data-ttu-id="f7166-310">One Collection per tenant: Each tenant has its own collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-310">One Collection per tenant: Each tenant has its own collection.</span></span> <span data-ttu-id="f7166-311">In this model, you can reserve performance per tenant.</span><span class="sxs-lookup"><span data-stu-id="f7166-311">In this model, you can reserve performance per tenant.</span></span> <span data-ttu-id="f7166-312">With DocumentDB's new consumption-based pricing model, this model is more cost-effective for multi-tenant applications with a small number of tenants.</span><span class="sxs-lookup"><span data-stu-id="f7166-312">With DocumentDB's new consumption-based pricing model, this model is more cost-effective for multi-tenant applications with a small number of tenants.</span></span>

<span data-ttu-id="f7166-313">You can also use a combination/tiered approach that collocates small tenants and migrates larger tenants to their own collection.</span><span class="sxs-lookup"><span data-stu-id="f7166-313">You can also use a combination/tiered approach that collocates small tenants and migrates larger tenants to their own collection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7166-314">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7166-314">Next steps</span></span>
<span data-ttu-id="f7166-315">In this article, we've described how partitioning works in Azure DocumentDB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span><span class="sxs-lookup"><span data-stu-id="f7166-315">In this article, we've described how partitioning works in Azure DocumentDB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span> 

* <span data-ttu-id="f7166-316">Perform scale and performance testing with DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f7166-316">Perform scale and performance testing with DocumentDB.</span></span> <span data-ttu-id="f7166-317">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md) for a sample.</span><span class="sxs-lookup"><span data-stu-id="f7166-317">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="f7166-318">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx)</span><span class="sxs-lookup"><span data-stu-id="f7166-318">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx)</span></span>
* <span data-ttu-id="f7166-319">Learn about [provisioned throughput in DocumentDB](documentdb-performance-levels.md)</span><span class="sxs-lookup"><span data-stu-id="f7166-319">Learn about [provisioned throughput in DocumentDB](documentdb-performance-levels.md)</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-partition-data/partitioning.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-partition-data/single-and-partitioned.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-partition-data/documentdb-migration-partitioned-collection.png  





