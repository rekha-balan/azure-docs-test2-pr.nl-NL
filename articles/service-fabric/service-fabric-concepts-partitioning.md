---
title: Partitioning Service Fabric services | Microsoft Docs
description: Describes how to partition Service Fabric stateful services. Partitions enables data storage on the local machines so data and compute can be scaled together.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: ''
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/17/2017
ms.author: msfussell
ms.openlocfilehash: 4b910992d1540e4e7102f213a3e916fb63a5e559
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562735"
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="a9ba3-104">Partition Service Fabric reliable services</span><span class="sxs-lookup"><span data-stu-id="a9ba3-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="a9ba3-105">This article provides an introduction to the basic concepts of partitioning Azure Service Fabric reliable services.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-105">This article provides an introduction to the basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="a9ba3-106">The source code used in the article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-106">The source code used in the article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="a9ba3-107">Partitioning</span><span class="sxs-lookup"><span data-stu-id="a9ba3-107">Partitioning</span></span>
<span data-ttu-id="a9ba3-108">Partitioning is not unique to Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-108">Partitioning is not unique to Service Fabric.</span></span> <span data-ttu-id="a9ba3-109">In fact, it is a core pattern of building scalable services.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="a9ba3-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units to improve scalability and performance.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units to improve scalability and performance.</span></span> <span data-ttu-id="a9ba3-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="a9ba3-112">Partition Service Fabric stateless services</span><span class="sxs-lookup"><span data-stu-id="a9ba3-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="a9ba3-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="a9ba3-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Stateless service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="a9ba3-116">There are really two types of stateless service solutions.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="a9ba3-117">The first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores the session information and data).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-117">The first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores the session information and data).</span></span> <span data-ttu-id="a9ba3-118">The second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-118">The second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="a9ba3-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="a9ba3-120">The only time you want to consider multiple partitions for stateless service instances is when you need to meet special routing requests.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-120">The only time you want to consider multiple partitions for stateless service instances is when you need to meet special routing requests.</span></span>

<span data-ttu-id="a9ba3-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="a9ba3-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want to control which service instance should write to the database shard--or perform other preparation work within the stateless service that requires the same partitioning information as is used in the backend.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want to control which service instance should write to the database shard--or perform other preparation work within the stateless service that requires the same partitioning information as is used in the backend.</span></span> <span data-ttu-id="a9ba3-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="a9ba3-124">The remainder of this walkthrough focuses on stateful services.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-124">The remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="a9ba3-125">Partition Service Fabric stateful services</span><span class="sxs-lookup"><span data-stu-id="a9ba3-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="a9ba3-126">Service Fabric makes it easy to develop scalable stateful services by offering a first-class way to partition state (data).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-126">Service Fabric makes it easy to develop scalable stateful services by offering a first-class way to partition state (data).</span></span> <span data-ttu-id="a9ba3-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across the nodes in a cluster.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across the nodes in a cluster.</span></span>

<span data-ttu-id="a9ba3-128">Partitioning in the context of Service Fabric stateful services refers to the process of determining that a particular service partition is responsible for a portion of the complete state of the service.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-128">Partitioning in the context of Service Fabric stateful services refers to the process of determining that a particular service partition is responsible for a portion of the complete state of the service.</span></span> <span data-ttu-id="a9ba3-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="a9ba3-130">A great thing about Service Fabric is that it places the partitions on different nodes.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-130">A great thing about Service Fabric is that it places the partitions on different nodes.</span></span> <span data-ttu-id="a9ba3-131">This allows them to grow to a node's resource limit.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-131">This allows them to grow to a node's resource limit.</span></span> <span data-ttu-id="a9ba3-132">As the data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-132">As the data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="a9ba3-133">This ensures the continued efficient use of hardware resources.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-133">This ensures the continued efficient use of hardware resources.</span></span>

<span data-ttu-id="a9ba3-134">To give you an example, say you start with a 5-node cluster and a service that is configured to have 10 partitions and a target of three replicas.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-134">To give you an example, say you start with a 5-node cluster and a service that is configured to have 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="a9ba3-135">In this case, Service Fabric would balance and distribute the replicas across the cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-135">In this case, Service Fabric would balance and distribute the replicas across the cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="a9ba3-136">If you now need to scale out the cluster to 10 nodes, Service Fabric would rebalance the primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-136">If you now need to scale out the cluster to 10 nodes, Service Fabric would rebalance the primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="a9ba3-137">Likewise, if you scaled back to 5 nodes, Service Fabric would rebalance all the replicas across the 5 nodes.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-137">Likewise, if you scaled back to 5 nodes, Service Fabric would rebalance all the replicas across the 5 nodes.</span></span>  

<span data-ttu-id="a9ba3-138">Figure 2 shows the distribution of 10 partitions before and after scaling the cluster.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-138">Figure 2 shows the distribution of 10 partitions before and after scaling the cluster.</span></span>

![Stateful service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="a9ba3-140">As a result, the scale-out is achieved since requests from clients are distributed across computers, overall performance of the application is improved, and contention on access to chunks of data is reduced.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-140">As a result, the scale-out is achieved since requests from clients are distributed across computers, overall performance of the application is improved, and contention on access to chunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="a9ba3-141">Plan for partitioning</span><span class="sxs-lookup"><span data-stu-id="a9ba3-141">Plan for partitioning</span></span>
<span data-ttu-id="a9ba3-142">Before implementing a service, you should always consider the partitioning strategy that is required to scale out. There are different ways, but all of them focus on what the application needs to achieve.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-142">Before implementing a service, you should always consider the partitioning strategy that is required to scale out. There are different ways, but all of them focus on what the application needs to achieve.</span></span> <span data-ttu-id="a9ba3-143">For the context of this article, let's consider some of the more important aspects.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-143">For the context of this article, let's consider some of the more important aspects.</span></span>

<span data-ttu-id="a9ba3-144">A good approach is to think about the structure of the state that needs to be partitioned, as the first step.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-144">A good approach is to think about the structure of the state that needs to be partitioned, as the first step.</span></span>

<span data-ttu-id="a9ba3-145">Let's take a simple example.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-145">Let's take a simple example.</span></span> <span data-ttu-id="a9ba3-146">If you were to build a service for a countywide poll, you could create a partition for each city in the county.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-146">If you were to build a service for a countywide poll, you could create a partition for each city in the county.</span></span> <span data-ttu-id="a9ba3-147">Then, you could store the votes for every person in the city in the partition that corresponds to that city.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-147">Then, you could store the votes for every person in the city in the partition that corresponds to that city.</span></span> <span data-ttu-id="a9ba3-148">Figure 3 illustrates a set of people and the city in which they reside.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-148">Figure 3 illustrates a set of people and the city in which they reside.</span></span>

![Simple partition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="a9ba3-150">As the population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-150">As the population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="a9ba3-151">So what is the impact of having partitions with uneven amounts of state?</span><span class="sxs-lookup"><span data-stu-id="a9ba3-151">So what is the impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="a9ba3-152">If you think about the example again, you can easily see that the partition that holds the votes for Seattle will get more traffic than the Kirkland one.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-152">If you think about the example again, you can easily see that the partition that holds the votes for Seattle will get more traffic than the Kirkland one.</span></span> <span data-ttu-id="a9ba3-153">By default, Service Fabric makes sure that there is about the same number of primary and secondary replicas on each node.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-153">By default, Service Fabric makes sure that there is about the same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="a9ba3-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="a9ba3-155">You would preferably want to avoid hot and cold spots like this in a cluster.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-155">You would preferably want to avoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="a9ba3-156">In order to avoid this, you should do two things, from a partitioning point of view:</span><span class="sxs-lookup"><span data-stu-id="a9ba3-156">In order to avoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="a9ba3-157">Try to partition the state so that it is evenly distributed across all partitions.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-157">Try to partition the state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="a9ba3-158">Report load from each of the replicas for the service.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-158">Report load from each of the replicas for the service.</span></span> <span data-ttu-id="a9ba3-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="a9ba3-160">Service Fabric provides the capability to report load consumed by services, such as amount of memory or number of records.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-160">Service Fabric provides the capability to report load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="a9ba3-161">Based on the metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances the cluster by moving replicas to more suitable nodes, so that overall no node is overloaded.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-161">Based on the metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances the cluster by moving replicas to more suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="a9ba3-162">Sometimes, you cannot know how much data will be in a given partition.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="a9ba3-163">So a general recommendation is to do both--first, by adopting a partitioning strategy that spreads the data evenly across the partitions and second, by reporting load.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-163">So a general recommendation is to do both--first, by adopting a partitioning strategy that spreads the data evenly across the partitions and second, by reporting load.</span></span>  <span data-ttu-id="a9ba3-164">The first method prevents situations described in the voting example, while the second helps smooth out temporary differences in access or load over time.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-164">The first method prevents situations described in the voting example, while the second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="a9ba3-165">Another aspect of partition planning is to choose the correct number of partitions to begin with.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-165">Another aspect of partition planning is to choose the correct number of partitions to begin with.</span></span>
<span data-ttu-id="a9ba3-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="a9ba3-167">In fact, assuming the maximum number of partitions is a valid approach.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-167">In fact, assuming the maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="a9ba3-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="a9ba3-169">As you cannot change the partition count after the fact, you would need to apply some advanced partition approaches, such as creating a new service instance of the same service type.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-169">As you cannot change the partition count after the fact, you would need to apply some advanced partition approaches, such as creating a new service instance of the same service type.</span></span> <span data-ttu-id="a9ba3-170">You would also need to implement some client-side logic that routes the requests to the correct service instance, based on client-side knowledge that your client code must maintain.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-170">You would also need to implement some client-side logic that routes the requests to the correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="a9ba3-171">Another consideration for partitioning planning is the available computer resources.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-171">Another consideration for partitioning planning is the available computer resources.</span></span> <span data-ttu-id="a9ba3-172">As the state needs to be accessed and stored, you are bound to follow:</span><span class="sxs-lookup"><span data-stu-id="a9ba3-172">As the state needs to be accessed and stored, you are bound to follow:</span></span>

* <span data-ttu-id="a9ba3-173">Network bandwidth limits</span><span class="sxs-lookup"><span data-stu-id="a9ba3-173">Network bandwidth limits</span></span>
* <span data-ttu-id="a9ba3-174">System memory limits</span><span class="sxs-lookup"><span data-stu-id="a9ba3-174">System memory limits</span></span>
* <span data-ttu-id="a9ba3-175">Disk storage limits</span><span class="sxs-lookup"><span data-stu-id="a9ba3-175">Disk storage limits</span></span>

<span data-ttu-id="a9ba3-176">So what happens if you run into resource constraints in a running cluster?</span><span class="sxs-lookup"><span data-stu-id="a9ba3-176">So what happens if you run into resource constraints in a running cluster?</span></span> <span data-ttu-id="a9ba3-177">The answer is that you can simply scale out the cluster to accommodate the new requirements.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-177">The answer is that you can simply scale out the cluster to accommodate the new requirements.</span></span>

<span data-ttu-id="a9ba3-178">[The capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how to determine how many nodes your cluster needs.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-178">[The capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how to determine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="a9ba3-179">Get started with partitioning</span><span class="sxs-lookup"><span data-stu-id="a9ba3-179">Get started with partitioning</span></span>
<span data-ttu-id="a9ba3-180">This section describes how to get started with partitioning your service.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-180">This section describes how to get started with partitioning your service.</span></span>

<span data-ttu-id="a9ba3-181">Service Fabric offers a choice of three partition schemes:</span><span class="sxs-lookup"><span data-stu-id="a9ba3-181">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="a9ba3-182">Ranged partitioning (otherwise known as UniformInt64Partition).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-182">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="a9ba3-183">Named partitioning.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-183">Named partitioning.</span></span> <span data-ttu-id="a9ba3-184">Applications using this model usually have data that can be bucketed, within a bounded set.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-184">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="a9ba3-185">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-185">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="a9ba3-186">Singleton partitioning.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-186">Singleton partitioning.</span></span> <span data-ttu-id="a9ba3-187">Singleton partitions are typically used when the service does not require any additional routing.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-187">Singleton partitions are typically used when the service does not require any additional routing.</span></span> <span data-ttu-id="a9ba3-188">For example, stateless services use this partitioning scheme by default.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-188">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="a9ba3-189">Named and Singleton partitioning schemes are special forms of ranged partitions.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-189">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="a9ba3-190">By default, the Visual Studio templates for Service Fabric use ranged partitioning, as it is the most common and useful one.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-190">By default, the Visual Studio templates for Service Fabric use ranged partitioning, as it is the most common and useful one.</span></span> <span data-ttu-id="a9ba3-191">The remainder of this article focuses on the ranged partitioning scheme.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-191">The remainder of this article focuses on the ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="a9ba3-192">Ranged partitioning scheme</span><span class="sxs-lookup"><span data-stu-id="a9ba3-192">Ranged partitioning scheme</span></span>
<span data-ttu-id="a9ba3-193">This is used to specify an integer range (identified by a low key and high key) and a number of partitions (n).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-193">This is used to specify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="a9ba3-194">It creates n partitions, each responsible for a non-overlapping subrange of the overall partition key range.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-194">It creates n partitions, each responsible for a non-overlapping subrange of the overall partition key range.</span></span> <span data-ttu-id="a9ba3-195">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-195">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Range partitioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="a9ba3-197">A common approach is to create a hash based on a unique key within the data set.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-197">A common approach is to create a hash based on a unique key within the data set.</span></span> <span data-ttu-id="a9ba3-198">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-198">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="a9ba3-199">By using this unique key, you would then generate a hash code, modulus the key range, to use as your key.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-199">By using this unique key, you would then generate a hash code, modulus the key range, to use as your key.</span></span> <span data-ttu-id="a9ba3-200">You can specify the upper and lower bounds of the allowed key range.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-200">You can specify the upper and lower bounds of the allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="a9ba3-201">Select a hash algorithm</span><span class="sxs-lookup"><span data-stu-id="a9ba3-201">Select a hash algorithm</span></span>
<span data-ttu-id="a9ba3-202">An important part of hashing is selecting your hash algorithm.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-202">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="a9ba3-203">A consideration is whether the goal is to group similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-203">A consideration is whether the goal is to group similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="a9ba3-204">The characteristics of a good distribution hashing algorithm are that it is easy to compute, it has few collisions, and it distributes the keys evenly.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-204">The characteristics of a good distribution hashing algorithm are that it is easy to compute, it has few collisions, and it distributes the keys evenly.</span></span> <span data-ttu-id="a9ba3-205">A good example of an efficient hash algorithm is the [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-205">A good example of an efficient hash algorithm is the [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="a9ba3-206">A good resource for general hash code algorithm choices is the [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-206">A good resource for general hash code algorithm choices is the [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="a9ba3-207">Build a stateful service with multiple partitions</span><span class="sxs-lookup"><span data-stu-id="a9ba3-207">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="a9ba3-208">Let's create your first reliable stateful service with multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-208">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="a9ba3-209">In this example, you will build a very simple application where you want to store all last names that start with the same letter in the same partition.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-209">In this example, you will build a very simple application where you want to store all last names that start with the same letter in the same partition.</span></span>

<span data-ttu-id="a9ba3-210">Before you write any code, you need to think about the partitions and partition keys.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-210">Before you write any code, you need to think about the partitions and partition keys.</span></span> <span data-ttu-id="a9ba3-211">You need 26 partitions (one for each letter in the alphabet), but what about the low and high keys?</span><span class="sxs-lookup"><span data-stu-id="a9ba3-211">You need 26 partitions (one for each letter in the alphabet), but what about the low and high keys?</span></span>
<span data-ttu-id="a9ba3-212">As we literally want to have one partition per letter, we can use 0 as the low key and 25 as the high key, as each letter is its own key.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-212">As we literally want to have one partition per letter, we can use 0 as the low key and 25 as the high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="a9ba3-213">This is a simplified scenario, as in reality the distribution would be uneven.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-213">This is a simplified scenario, as in reality the distribution would be uneven.</span></span> <span data-ttu-id="a9ba3-214">Last names starting with the letters "S" or "M" are more common than the ones starting with "X" or "Y".</span><span class="sxs-lookup"><span data-stu-id="a9ba3-214">Last names starting with the letters "S" or "M" are more common than the ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="a9ba3-215">Open **Visual Studio** > **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-215">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="a9ba3-216">In the **New Project** dialog box, choose the Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-216">In the **New Project** dialog box, choose the Service Fabric application.</span></span>
3. <span data-ttu-id="a9ba3-217">Call the project "AlphabetPartitions".</span><span class="sxs-lookup"><span data-stu-id="a9ba3-217">Call the project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="a9ba3-218">In the **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-218">In the **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in the image below.</span></span>
   
    ![Stateful service screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-concepts-partitioning/createstateful.png)
5. <span data-ttu-id="a9ba3-220">Set the number of partitions.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-220">Set the number of partitions.</span></span> <span data-ttu-id="a9ba3-221">Open the Applicationmanifest.xml file located in the ApplicationPackageRoot folder of the AlphabetPartitions project and update the parameter Processing_PartitionCount to 26 as shown below.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-221">Open the Applicationmanifest.xml file located in the ApplicationPackageRoot folder of the AlphabetPartitions project and update the parameter Processing_PartitionCount to 26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="a9ba3-222">You also need to update the LowKey and HighKey properties of the StatefulService element in the ApplicationManifest.xml as shown below.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-222">You also need to update the LowKey and HighKey properties of the StatefulService element in the ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="a9ba3-223">For the service to be accessible, open up an endpoint on a port by adding the endpoint element of ServiceManifest.xml (located in the PackageRoot folder) for the Alphabet.Processing service as shown below:</span><span class="sxs-lookup"><span data-stu-id="a9ba3-223">For the service to be accessible, open up an endpoint on a port by adding the endpoint element of ServiceManifest.xml (located in the PackageRoot folder) for the Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="a9ba3-224">Now the service is configured to listen to an internal endpoint with 26 partitions.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-224">Now the service is configured to listen to an internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="a9ba3-225">Next, you need to override the `CreateServiceReplicaListeners()` method of the Processing class.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-225">Next, you need to override the `CreateServiceReplicaListeners()` method of the Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a9ba3-226">For this sample, we assume that you are using a simple HttpCommunicationListener.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-226">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="a9ba3-227">For more information on reliable service communication, see [The Reliable Service communication model](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-227">For more information on reliable service communication, see [The Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="a9ba3-228">A recommended pattern for the URL that a replica listens on is the following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-228">A recommended pattern for the URL that a replica listens on is the following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="a9ba3-229">So you want to configure your communication listener to listen on the correct endpoints and with this pattern.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-229">So you want to configure your communication listener to listen on the correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="a9ba3-230">Multiple replicas of this service may be hosted on the same computer, so this address needs to be unique to the replica.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-230">Multiple replicas of this service may be hosted on the same computer, so this address needs to be unique to the replica.</span></span> <span data-ttu-id="a9ba3-231">This is why   partition ID + replica ID are in the URL.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-231">This is why   partition ID + replica ID are in the URL.</span></span> <span data-ttu-id="a9ba3-232">HttpListener can listen on multiple addresses on the same port as long as the URL prefix    is unique.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-232">HttpListener can listen on multiple addresses on the same port as long as the URL prefix    is unique.</span></span>
   
    <span data-ttu-id="a9ba3-233">The extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-233">The extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="a9ba3-234">When that's the case, you want to make sure that a new unique address is used when transitioning from primary to secondary to force clients to re-resolve the address.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-234">When that's the case, you want to make sure that a new unique address is used when transitioning from primary to secondary to force clients to re-resolve the address.</span></span> <span data-ttu-id="a9ba3-235">'+' is used as the address here so that the replica listens on all available hosts (IP, FQDM, localhost, etc.) The code below shows an example.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-235">'+' is used as the address here so that the replica listens on all available hosts (IP, FQDM, localhost, etc.) The code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="a9ba3-236">It's also worth noting that the published URL is slightly different from the listening URL prefix.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-236">It's also worth noting that the published URL is slightly different from the listening URL prefix.</span></span>
    <span data-ttu-id="a9ba3-237">The listening URL is given to HttpListener.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-237">The listening URL is given to HttpListener.</span></span> <span data-ttu-id="a9ba3-238">The published URL is the URL that is published to the Service Fabric Naming Service, which is used for service discovery.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-238">The published URL is the URL that is published to the Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="a9ba3-239">Clients will ask for this address through that discovery service.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-239">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="a9ba3-240">The address that clients get needs to have the actual IP or FQDN of the node in order to connect.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-240">The address that clients get needs to have the actual IP or FQDN of the node in order to connect.</span></span> <span data-ttu-id="a9ba3-241">So you need to replace '+' with the node's IP or FQDN as shown above.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-241">So you need to replace '+' with the node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="a9ba3-242">The last step is to add the processing logic to the service as shown below.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-242">The last step is to add the processing logic to the service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="a9ba3-243">`ProcessInternalRequest` reads the values of the query string parameter used to call the partition and calls `AddUserAsync` to add the lastname to the reliable dictionary `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-243">`ProcessInternalRequest` reads the values of the query string parameter used to call the partition and calls `AddUserAsync` to add the lastname to the reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="a9ba3-244">Let's add a stateless service to the project to see how you can call a particular partition.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-244">Let's add a stateless service to the project to see how you can call a particular partition.</span></span>
    
    <span data-ttu-id="a9ba3-245">This service serves as a simple web interface that accepts the lastname as a query string parameter, determines the partition key, and sends it to the Alphabet.Processing service for processing.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-245">This service serves as a simple web interface that accepts the lastname as a query string parameter, determines the partition key, and sends it to the Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="a9ba3-246">In the **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-246">In the **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Stateless service screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="a9ba3-248">.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-248">.</span></span>
12. <span data-ttu-id="a9ba3-249">Update the endpoint information in the ServiceManifest.xml of the Alphabet.WebApi service to open up a port as shown below.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-249">Update the endpoint information in the ServiceManifest.xml of the Alphabet.WebApi service to open up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="a9ba3-250">You need to return a collection of ServiceInstanceListeners in the class Web.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-250">You need to return a collection of ServiceInstanceListeners in the class Web.</span></span> <span data-ttu-id="a9ba3-251">Again, you can choose to implement a simple HttpCommunicationListener.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-251">Again, you can choose to implement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is the node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="a9ba3-252">Now you need to implement the processing logic.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-252">Now you need to implement the processing logic.</span></span> <span data-ttu-id="a9ba3-253">The HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-253">The HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="a9ba3-254">So let's go ahead and add the code below.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-254">So let's go ahead and add the code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from the first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added to Partition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="a9ba3-255">Let's walk through it step by step.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-255">Let's walk through it step by step.</span></span> <span data-ttu-id="a9ba3-256">The code reads the first letter of the query string parameter `lastname` into a char.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-256">The code reads the first letter of the query string parameter `lastname` into a char.</span></span> <span data-ttu-id="a9ba3-257">Then, it determines the partition key for this letter by subtracting the hexadecimal value of `A` from the hexadecimal value of the last names' first letter.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-257">Then, it determines the partition key for this letter by subtracting the hexadecimal value of `A` from the hexadecimal value of the last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="a9ba3-258">Remember, for this example, we are using 26 partitions with one partition key per partition.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-258">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="a9ba3-259">Next, we obtain the service partition `partition` for this key by using the `ResolveAsync` method on the `servicePartitionResolver` object.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-259">Next, we obtain the service partition `partition` for this key by using the `ResolveAsync` method on the `servicePartitionResolver` object.</span></span> <span data-ttu-id="a9ba3-260">`servicePartitionResolver` is defined as</span><span class="sxs-lookup"><span data-stu-id="a9ba3-260">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="a9ba3-261">The `ResolveAsync` method takes the service URI, the partition key, and a cancellation token as parameters.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-261">The `ResolveAsync` method takes the service URI, the partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="a9ba3-262">The service URI for the processing service is `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-262">The service URI for the processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="a9ba3-263">Next, we get the endpoint of the partition.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-263">Next, we get the endpoint of the partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="a9ba3-264">Finally, we build the endpoint URL plus the querystring and call the processing service.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-264">Finally, we build the endpoint URL plus the querystring and call the processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="a9ba3-265">Once the processing is done, we write the output back.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-265">Once the processing is done, we write the output back.</span></span>
15. <span data-ttu-id="a9ba3-266">The last step is to test the service.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-266">The last step is to test the service.</span></span> <span data-ttu-id="a9ba3-267">Visual Studio uses application parameters for local and cloud deployment.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-267">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="a9ba3-268">To test the service with 26 partitions locally, you need to update the `Local.xml` file in the ApplicationParameters folder of the AlphabetPartitions project as shown below:</span><span class="sxs-lookup"><span data-stu-id="a9ba3-268">To test the service with 26 partitions locally, you need to update the `Local.xml` file in the ApplicationParameters folder of the AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="a9ba3-269">Once you finish deployment, you can check the service and all of its partitions in the Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-269">Once you finish deployment, you can check the service and all of its partitions in the Service Fabric Explorer.</span></span>
    
    ![Service Fabric Explorer screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="a9ba3-271">In a browser, you can test the partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-271">In a browser, you can test the partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="a9ba3-272">You will see that each last name that starts with the same letter is being stored in the same partition.</span><span class="sxs-lookup"><span data-stu-id="a9ba3-272">You will see that each last name that starts with the same letter is being stored in the same partition.</span></span>
    
    ![Browser screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="a9ba3-274">The entire source code of the sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="a9ba3-274">The entire source code of the sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9ba3-275">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9ba3-275">Next steps</span></span>
<span data-ttu-id="a9ba3-276">For information on Service Fabric concepts, see the following:</span><span class="sxs-lookup"><span data-stu-id="a9ba3-276">For information on Service Fabric concepts, see the following:</span></span>

* [<span data-ttu-id="a9ba3-277">Availability of Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="a9ba3-277">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="a9ba3-278">Scalability of Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="a9ba3-278">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="a9ba3-279">Capacity planning for Service Fabric applications</span><span class="sxs-lookup"><span data-stu-id="a9ba3-279">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)








