---
title: Availability of Service Fabric services | Microsoft Docs
description: Describes fault detection, failover, and recovery of services
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 8bd68336201672e0a000c1f0653af6b5f4d5610f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814397"
---
# <a name="availability-of-service-fabric-services"></a><span data-ttu-id="13d5a-103">Availability of Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="13d5a-103">Availability of Service Fabric services</span></span>
<span data-ttu-id="13d5a-104">This article gives an overview of how Azure Service Fabric maintains the availability of a service.</span><span class="sxs-lookup"><span data-stu-id="13d5a-104">This article gives an overview of how Azure Service Fabric maintains the availability of a service.</span></span>

## <a name="availability-of-service-fabric-stateless-services"></a><span data-ttu-id="13d5a-105">Availability of Service Fabric stateless services</span><span class="sxs-lookup"><span data-stu-id="13d5a-105">Availability of Service Fabric stateless services</span></span>
<span data-ttu-id="13d5a-106">Service Fabric services can be either stateful or stateless.</span><span class="sxs-lookup"><span data-stu-id="13d5a-106">Service Fabric services can be either stateful or stateless.</span></span> <span data-ttu-id="13d5a-107">A stateless service is an application service that does not have a [local state](service-fabric-concepts-state.md) that needs to be highly available or reliable.</span><span class="sxs-lookup"><span data-stu-id="13d5a-107">A stateless service is an application service that does not have a [local state](service-fabric-concepts-state.md) that needs to be highly available or reliable.</span></span>

<span data-ttu-id="13d5a-108">Creating a stateless service requires defining an `InstanceCount`.</span><span class="sxs-lookup"><span data-stu-id="13d5a-108">Creating a stateless service requires defining an `InstanceCount`.</span></span> <span data-ttu-id="13d5a-109">The instance count defines the number of instances of the stateless service's application logic that should be running in the cluster.</span><span class="sxs-lookup"><span data-stu-id="13d5a-109">The instance count defines the number of instances of the stateless service's application logic that should be running in the cluster.</span></span> <span data-ttu-id="13d5a-110">Increasing the number of instances is the recommended way of scaling out a stateless service.</span><span class="sxs-lookup"><span data-stu-id="13d5a-110">Increasing the number of instances is the recommended way of scaling out a stateless service.</span></span>

<span data-ttu-id="13d5a-111">When an instance of a stateless named-service fails, a new instance is created on an eligible node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="13d5a-111">When an instance of a stateless named-service fails, a new instance is created on an eligible node in the cluster.</span></span> <span data-ttu-id="13d5a-112">For example, a stateless service instance might fail on Node1 and be re-created on Node5.</span><span class="sxs-lookup"><span data-stu-id="13d5a-112">For example, a stateless service instance might fail on Node1 and be re-created on Node5.</span></span>

## <a name="availability-of-service-fabric-stateful-services"></a><span data-ttu-id="13d5a-113">Availability of Service Fabric stateful services</span><span class="sxs-lookup"><span data-stu-id="13d5a-113">Availability of Service Fabric stateful services</span></span>
<span data-ttu-id="13d5a-114">A stateful service has a state associated with it.</span><span class="sxs-lookup"><span data-stu-id="13d5a-114">A stateful service has a state associated with it.</span></span> <span data-ttu-id="13d5a-115">In Service Fabric, a stateful service is modeled as a set of replicas.</span><span class="sxs-lookup"><span data-stu-id="13d5a-115">In Service Fabric, a stateful service is modeled as a set of replicas.</span></span> <span data-ttu-id="13d5a-116">Each replica is a running instance of the code of the service.</span><span class="sxs-lookup"><span data-stu-id="13d5a-116">Each replica is a running instance of the code of the service.</span></span> <span data-ttu-id="13d5a-117">The replica also has a copy of the state for that service.</span><span class="sxs-lookup"><span data-stu-id="13d5a-117">The replica also has a copy of the state for that service.</span></span> <span data-ttu-id="13d5a-118">Read and write operations are performed at one replica, called the *Primary*.</span><span class="sxs-lookup"><span data-stu-id="13d5a-118">Read and write operations are performed at one replica, called the *Primary*.</span></span> <span data-ttu-id="13d5a-119">Changes to state from write operations are *replicated* to the other replicas in the replica set, called *Active Secondaries*, and applied.</span><span class="sxs-lookup"><span data-stu-id="13d5a-119">Changes to state from write operations are *replicated* to the other replicas in the replica set, called *Active Secondaries*, and applied.</span></span> 

<span data-ttu-id="13d5a-120">There can be only one Primary replica, but there can be multiple Active Secondary replicas.</span><span class="sxs-lookup"><span data-stu-id="13d5a-120">There can be only one Primary replica, but there can be multiple Active Secondary replicas.</span></span> <span data-ttu-id="13d5a-121">The number of active Secondary replicas is configurable, and a higher number of replicas can tolerate a greater number of concurrent software and hardware failures.</span><span class="sxs-lookup"><span data-stu-id="13d5a-121">The number of active Secondary replicas is configurable, and a higher number of replicas can tolerate a greater number of concurrent software and hardware failures.</span></span>

<span data-ttu-id="13d5a-122">If the Primary replica goes down, Service Fabric makes one of the Active Secondary replicas the new Primary replica.</span><span class="sxs-lookup"><span data-stu-id="13d5a-122">If the Primary replica goes down, Service Fabric makes one of the Active Secondary replicas the new Primary replica.</span></span> <span data-ttu-id="13d5a-123">This Active Secondary replica already has the updated version of the state, via *replication*, and it can continue processing further read/write operations.</span><span class="sxs-lookup"><span data-stu-id="13d5a-123">This Active Secondary replica already has the updated version of the state, via *replication*, and it can continue processing further read/write operations.</span></span> <span data-ttu-id="13d5a-124">This process is known as *reconfiguration* and is described further in the [Reconfiguration](service-fabric-concepts-reconfiguration.md) article.</span><span class="sxs-lookup"><span data-stu-id="13d5a-124">This process is known as *reconfiguration* and is described further in the [Reconfiguration](service-fabric-concepts-reconfiguration.md) article.</span></span>

<span data-ttu-id="13d5a-125">The concept of a replica being either a Primary or Active Secondary, is known as the *replica role*.</span><span class="sxs-lookup"><span data-stu-id="13d5a-125">The concept of a replica being either a Primary or Active Secondary, is known as the *replica role*.</span></span> <span data-ttu-id="13d5a-126">These replicas are described further in the [Replicas and instances](service-fabric-concepts-replica-lifecycle.md) article.</span><span class="sxs-lookup"><span data-stu-id="13d5a-126">These replicas are described further in the [Replicas and instances](service-fabric-concepts-replica-lifecycle.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="13d5a-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="13d5a-127">Next steps</span></span>
<span data-ttu-id="13d5a-128">For more information on Service Fabric concepts, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="13d5a-128">For more information on Service Fabric concepts, see the following articles:</span></span>

- [<span data-ttu-id="13d5a-129">Scaling Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="13d5a-129">Scaling Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
- [<span data-ttu-id="13d5a-130">Partitioning Service Fabric services</span><span class="sxs-lookup"><span data-stu-id="13d5a-130">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
- [<span data-ttu-id="13d5a-131">Defining and managing state</span><span class="sxs-lookup"><span data-stu-id="13d5a-131">Defining and managing state</span></span>](service-fabric-concepts-state.md)
- [<span data-ttu-id="13d5a-132">Reliable Services</span><span class="sxs-lookup"><span data-stu-id="13d5a-132">Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)

