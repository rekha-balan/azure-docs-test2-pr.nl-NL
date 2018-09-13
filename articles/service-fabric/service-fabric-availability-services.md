---
title: Availability of Service Fabric services | Microsoft Docs
description: Describes fault detection, failover, and recovery for services
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: masnider
ms.openlocfilehash: 1db7b4bcfa4b7c474a4b0eb4ef469a6cb1fe54a0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556297"
---
# <a name="availability-of-service-fabric-services"></a><span data-ttu-id="3f531-103">Availability of Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="3f531-103">Availability of Service Fabric services</span></span>
<span data-ttu-id="3f531-104">This article gives an overview of how Service Fabric maintains availability of a service.</span><span class="sxs-lookup"><span data-stu-id="3f531-104">This article gives an overview of how Service Fabric maintains availability of a service.</span></span>

## <a name="availability-of-service-fabric-stateless-services"></a><span data-ttu-id="3f531-105">Availability of Service Fabric stateless services</span><span class="sxs-lookup"><span data-stu-id="3f531-105">Availability of Service Fabric stateless services</span></span>
<span data-ttu-id="3f531-106">Azure Service Fabric services can be either stateful or stateless.</span><span class="sxs-lookup"><span data-stu-id="3f531-106">Azure Service Fabric services can be either stateful or stateless.</span></span> <span data-ttu-id="3f531-107">A stateless service is an application service that does not have any [local persistent state](service-fabric-concepts-state.md).</span><span class="sxs-lookup"><span data-stu-id="3f531-107">A stateless service is an application service that does not have any [local persistent state](service-fabric-concepts-state.md).</span></span>

<span data-ttu-id="3f531-108">Creating a stateless service requires defining an instance count.</span><span class="sxs-lookup"><span data-stu-id="3f531-108">Creating a stateless service requires defining an instance count.</span></span> <span data-ttu-id="3f531-109">The instance count defines the number of instances of the stateless service's application logic that should be running in the cluster.</span><span class="sxs-lookup"><span data-stu-id="3f531-109">The instance count defines the number of instances of the stateless service's application logic that should be running in the cluster.</span></span> <span data-ttu-id="3f531-110">Increasing the number of instances is the recommended way of scaling out a stateless service.</span><span class="sxs-lookup"><span data-stu-id="3f531-110">Increasing the number of instances is the recommended way of scaling out a stateless service.</span></span>

<span data-ttu-id="3f531-111">When a fault is detected on any instance of a stateless service, a new instance is created on some eligible node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="3f531-111">When a fault is detected on any instance of a stateless service, a new instance is created on some eligible node in the cluster.</span></span>

## <a name="availability-of-service-fabric-stateful-services"></a><span data-ttu-id="3f531-112">Availability of Service Fabric stateful services</span><span class="sxs-lookup"><span data-stu-id="3f531-112">Availability of Service Fabric stateful services</span></span>
<span data-ttu-id="3f531-113">A stateful service has some state associated with it.</span><span class="sxs-lookup"><span data-stu-id="3f531-113">A stateful service has some state associated with it.</span></span> <span data-ttu-id="3f531-114">In Service Fabric, a stateful service is modeled as a set of replicas.</span><span class="sxs-lookup"><span data-stu-id="3f531-114">In Service Fabric, a stateful service is modeled as a set of replicas.</span></span> <span data-ttu-id="3f531-115">Each replica is an instance of the code of the service that has a copy of the state.</span><span class="sxs-lookup"><span data-stu-id="3f531-115">Each replica is an instance of the code of the service that has a copy of the state.</span></span> <span data-ttu-id="3f531-116">Read and write operations are performed at one replica (called the Primary).</span><span class="sxs-lookup"><span data-stu-id="3f531-116">Read and write operations are performed at one replica (called the Primary).</span></span> <span data-ttu-id="3f531-117">Changes to state from write operations are *replicated* to multiple other replicas (called Active Secondaries).</span><span class="sxs-lookup"><span data-stu-id="3f531-117">Changes to state from write operations are *replicated* to multiple other replicas (called Active Secondaries).</span></span> <span data-ttu-id="3f531-118">The combination of Primary and Active Secondaries make up the replica set of the service.</span><span class="sxs-lookup"><span data-stu-id="3f531-118">The combination of Primary and Active Secondaries make up the replica set of the service.</span></span>

<span data-ttu-id="3f531-119">There can be only one Primary replica servicing read and write requests, but there can be multiple Active Secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="3f531-119">There can be only one Primary replica servicing read and write requests, but there can be multiple Active Secondary replicas.</span></span> <span data-ttu-id="3f531-120">The number of Active Secondary replicas is configurable, and a higher number of replicas can tolerate a greater number of concurrent software and hardware failures.</span><span class="sxs-lookup"><span data-stu-id="3f531-120">The number of Active Secondary replicas is configurable, and a higher number of replicas can tolerate a greater number of concurrent software and hardware failures.</span></span>

<span data-ttu-id="3f531-121">If the Primary replica goes down, Service Fabric makes one of the Active Secondary replicas the new Primary replica.</span><span class="sxs-lookup"><span data-stu-id="3f531-121">If the Primary replica goes down, Service Fabric makes one of the Active Secondary replicas the new Primary replica.</span></span> <span data-ttu-id="3f531-122">This Active Secondary replica already has the updated version of the state (via *replication*), and it can continue processing further read and write operations.</span><span class="sxs-lookup"><span data-stu-id="3f531-122">This Active Secondary replica already has the updated version of the state (via *replication*), and it can continue processing further read and write operations.</span></span>

<span data-ttu-id="3f531-123">This concept, of a replica being either a Primary or Active Secondary, is known as the Replica Role.</span><span class="sxs-lookup"><span data-stu-id="3f531-123">This concept, of a replica being either a Primary or Active Secondary, is known as the Replica Role.</span></span>

### <a name="replica-roles"></a><span data-ttu-id="3f531-124">Replica roles</span><span class="sxs-lookup"><span data-stu-id="3f531-124">Replica roles</span></span>
<span data-ttu-id="3f531-125">The role of a replica is used to manage the life cycle of the state being managed by that replica.</span><span class="sxs-lookup"><span data-stu-id="3f531-125">The role of a replica is used to manage the life cycle of the state being managed by that replica.</span></span> <span data-ttu-id="3f531-126">A replica whose role is Primary services read requests.</span><span class="sxs-lookup"><span data-stu-id="3f531-126">A replica whose role is Primary services read requests.</span></span> <span data-ttu-id="3f531-127">The Primary also handles all write requests by updating its state and replicating the changes.</span><span class="sxs-lookup"><span data-stu-id="3f531-127">The Primary also handles all write requests by updating its state and replicating the changes.</span></span> <span data-ttu-id="3f531-128">These changes are applied to the Active Secondaries in the replica set.</span><span class="sxs-lookup"><span data-stu-id="3f531-128">These changes are applied to the Active Secondaries in the replica set.</span></span> <span data-ttu-id="3f531-129">The job of an Active Secondary is to receive state changes that the Primary replica has replicated and update its view of the state.</span><span class="sxs-lookup"><span data-stu-id="3f531-129">The job of an Active Secondary is to receive state changes that the Primary replica has replicated and update its view of the state.</span></span>

> [!NOTE]
> <span data-ttu-id="3f531-130">Higher-level programming models such as the [reliable actors framework](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) abstract away the concept of replica role from the developer.</span><span class="sxs-lookup"><span data-stu-id="3f531-130">Higher-level programming models such as the [reliable actors framework](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) abstract away the concept of replica role from the developer.</span></span> <span data-ttu-id="3f531-131">In actors, the notion of role is unnecessary, while in Services it is visible if necessary but largely simplified.</span><span class="sxs-lookup"><span data-stu-id="3f531-131">In actors, the notion of role is unnecessary, while in Services it is visible if necessary but largely simplified.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3f531-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f531-132">Next steps</span></span>
<span data-ttu-id="3f531-133">For more information on Service Fabric concepts, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="3f531-133">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="3f531-134">Scalability of Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="3f531-134">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="3f531-135">Partitioning Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="3f531-135">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="3f531-136">Defining and managing state</span><span class="sxs-lookup"><span data-stu-id="3f531-136">Defining and managing state</span></span>](service-fabric-concepts-state.md)
* [<span data-ttu-id="3f531-137">Reliable Services</span><span class="sxs-lookup"><span data-stu-id="3f531-137">Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
