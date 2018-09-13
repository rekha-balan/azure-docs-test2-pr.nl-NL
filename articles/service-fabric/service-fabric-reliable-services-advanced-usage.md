---
title: Advanced usage of Reliable Services | Microsoft Docs
description: Learn about advanced usage of Service Fabric's Reliable Services for added flexibility in your services.
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: vturecek
ms.openlocfilehash: 2dc98ec311f74630db58c1fd07949b9673d77b6c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553959"
---
# <a name="advanced-usage-of-the-reliable-services-programming-model"></a><span data-ttu-id="f55dd-103">Advanced usage of the Reliable Services programming model</span><span class="sxs-lookup"><span data-stu-id="f55dd-103">Advanced usage of the Reliable Services programming model</span></span>
<span data-ttu-id="f55dd-104">Azure Service Fabric simplifies writing and managing reliable stateless and stateful services.</span><span class="sxs-lookup"><span data-stu-id="f55dd-104">Azure Service Fabric simplifies writing and managing reliable stateless and stateful services.</span></span> <span data-ttu-id="f55dd-105">This guide talks about advanced usages of Reliable Services to gain more control and flexibility over your services.</span><span class="sxs-lookup"><span data-stu-id="f55dd-105">This guide talks about advanced usages of Reliable Services to gain more control and flexibility over your services.</span></span> <span data-ttu-id="f55dd-106">Prior to reading this guide, familiarize yourself with [the Reliable Services programming model](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f55dd-106">Prior to reading this guide, familiarize yourself with [the Reliable Services programming model](service-fabric-reliable-services-introduction.md).</span></span>

<span data-ttu-id="f55dd-107">Both stateful and stateless services have two primary entry points for user code:</span><span class="sxs-lookup"><span data-stu-id="f55dd-107">Both stateful and stateless services have two primary entry points for user code:</span></span>

* <span data-ttu-id="f55dd-108">`RunAsync(C#) / runAsync(Java)` is a general-purpose entry point for your service code.</span><span class="sxs-lookup"><span data-stu-id="f55dd-108">`RunAsync(C#) / runAsync(Java)` is a general-purpose entry point for your service code.</span></span>
* <span data-ttu-id="f55dd-109">`CreateServiceReplicaListeners(C#)` and `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` is for opening communication listeners for client requests.</span><span class="sxs-lookup"><span data-stu-id="f55dd-109">`CreateServiceReplicaListeners(C#)` and `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` is for opening communication listeners for client requests.</span></span>

<span data-ttu-id="f55dd-110">For most services, these two entry points are sufficient.</span><span class="sxs-lookup"><span data-stu-id="f55dd-110">For most services, these two entry points are sufficient.</span></span> <span data-ttu-id="f55dd-111">In rare cases when more control over a service's lifecycle is required, additional lifecycle events are available.</span><span class="sxs-lookup"><span data-stu-id="f55dd-111">In rare cases when more control over a service's lifecycle is required, additional lifecycle events are available.</span></span>

## <a name="stateless-service-instance-lifecycle"></a><span data-ttu-id="f55dd-112">Stateless service instance lifecycle</span><span class="sxs-lookup"><span data-stu-id="f55dd-112">Stateless service instance lifecycle</span></span>
<span data-ttu-id="f55dd-113">A stateless service's lifecycle is very simple.</span><span class="sxs-lookup"><span data-stu-id="f55dd-113">A stateless service's lifecycle is very simple.</span></span> <span data-ttu-id="f55dd-114">A stateless service can only be opened, closed, or aborted.</span><span class="sxs-lookup"><span data-stu-id="f55dd-114">A stateless service can only be opened, closed, or aborted.</span></span> <span data-ttu-id="f55dd-115">`RunAsync` in a stateless service is executed when a service instance is opened, and canceled when a service instance is closed or aborted.</span><span class="sxs-lookup"><span data-stu-id="f55dd-115">`RunAsync` in a stateless service is executed when a service instance is opened, and canceled when a service instance is closed or aborted.</span></span>

<span data-ttu-id="f55dd-116">Although `RunAsync` should be sufficient in almost all cases, the open, close, and abort events in a stateless service are also available:</span><span class="sxs-lookup"><span data-stu-id="f55dd-116">Although `RunAsync` should be sufficient in almost all cases, the open, close, and abort events in a stateless service are also available:</span></span>

* <span data-ttu-id="f55dd-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java` OnOpenAsync is called when the stateless service instance is about to be used.</span><span class="sxs-lookup"><span data-stu-id="f55dd-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java` OnOpenAsync is called when the stateless service instance is about to be used.</span></span> <span data-ttu-id="f55dd-118">Extended service initialization tasks can be started at this time.</span><span class="sxs-lookup"><span data-stu-id="f55dd-118">Extended service initialization tasks can be started at this time.</span></span>
* <span data-ttu-id="f55dd-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java` OnCloseAsync is called when the stateless service instance is going to be gracefully shut down.</span><span class="sxs-lookup"><span data-stu-id="f55dd-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java` OnCloseAsync is called when the stateless service instance is going to be gracefully shut down.</span></span> <span data-ttu-id="f55dd-120">This can occur when the service's code is being upgraded, the service instance is being moved due to load balancing, or a transient fault is detected.</span><span class="sxs-lookup"><span data-stu-id="f55dd-120">This can occur when the service's code is being upgraded, the service instance is being moved due to load balancing, or a transient fault is detected.</span></span> <span data-ttu-id="f55dd-121">OnCloseAsync can be used to safely close any resources, stop any background processing, finish saving external state, or close down existing connections.</span><span class="sxs-lookup"><span data-stu-id="f55dd-121">OnCloseAsync can be used to safely close any resources, stop any background processing, finish saving external state, or close down existing connections.</span></span>
* <span data-ttu-id="f55dd-122">`void OnAbort() - C# / void onAbort() - Java` OnAbort is called when the stateless service instance is being forcefully shut down.</span><span class="sxs-lookup"><span data-stu-id="f55dd-122">`void OnAbort() - C# / void onAbort() - Java` OnAbort is called when the stateless service instance is being forcefully shut down.</span></span> <span data-ttu-id="f55dd-123">This is generally called when a permanent fault is detected on the node, or when Service Fabric cannot reliably manage the service instance's lifecycle due to internal failures.</span><span class="sxs-lookup"><span data-stu-id="f55dd-123">This is generally called when a permanent fault is detected on the node, or when Service Fabric cannot reliably manage the service instance's lifecycle due to internal failures.</span></span>

## <a name="stateful-service-replica-lifecycle"></a><span data-ttu-id="f55dd-124">Stateful service replica lifecycle</span><span class="sxs-lookup"><span data-stu-id="f55dd-124">Stateful service replica lifecycle</span></span>

> [!NOTE]
> <span data-ttu-id="f55dd-125">Stateful reliable services are not supported in Java yet.</span><span class="sxs-lookup"><span data-stu-id="f55dd-125">Stateful reliable services are not supported in Java yet.</span></span>
>
>

<span data-ttu-id="f55dd-126">A stateful service replica's lifecycle is much more complex than a stateless service instance.</span><span class="sxs-lookup"><span data-stu-id="f55dd-126">A stateful service replica's lifecycle is much more complex than a stateless service instance.</span></span> <span data-ttu-id="f55dd-127">In addition to open, close, and abort events, a stateful service replica undergoes role changes during its lifetime.</span><span class="sxs-lookup"><span data-stu-id="f55dd-127">In addition to open, close, and abort events, a stateful service replica undergoes role changes during its lifetime.</span></span> <span data-ttu-id="f55dd-128">When a stateful service replica changes role, the `OnChangeRoleAsync` event is triggered:</span><span class="sxs-lookup"><span data-stu-id="f55dd-128">When a stateful service replica changes role, the `OnChangeRoleAsync` event is triggered:</span></span>

* <span data-ttu-id="f55dd-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)` OnChangeRoleAsync is called when the stateful service replica is changing role, for example to primary or secondary.</span><span class="sxs-lookup"><span data-stu-id="f55dd-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)` OnChangeRoleAsync is called when the stateful service replica is changing role, for example to primary or secondary.</span></span> <span data-ttu-id="f55dd-130">Primary replicas are given write status (are allowed to create and write to Reliable Collections).</span><span class="sxs-lookup"><span data-stu-id="f55dd-130">Primary replicas are given write status (are allowed to create and write to Reliable Collections).</span></span> <span data-ttu-id="f55dd-131">Secondary replicas are given read status (can only read from existing Reliable Collections).</span><span class="sxs-lookup"><span data-stu-id="f55dd-131">Secondary replicas are given read status (can only read from existing Reliable Collections).</span></span> <span data-ttu-id="f55dd-132">Most work in a stateful service is performed at the primary replica.</span><span class="sxs-lookup"><span data-stu-id="f55dd-132">Most work in a stateful service is performed at the primary replica.</span></span> <span data-ttu-id="f55dd-133">Secondary replicas can perform read-only validation, report generation, data mining, or other read-only jobs.</span><span class="sxs-lookup"><span data-stu-id="f55dd-133">Secondary replicas can perform read-only validation, report generation, data mining, or other read-only jobs.</span></span>

<span data-ttu-id="f55dd-134">In a stateful service, only the primary replica has write access to state and thus is generally when the service is performing actual work.</span><span class="sxs-lookup"><span data-stu-id="f55dd-134">In a stateful service, only the primary replica has write access to state and thus is generally when the service is performing actual work.</span></span> <span data-ttu-id="f55dd-135">The `RunAsync` method in a stateful service is executed only when the stateful service replica is primary.</span><span class="sxs-lookup"><span data-stu-id="f55dd-135">The `RunAsync` method in a stateful service is executed only when the stateful service replica is primary.</span></span> <span data-ttu-id="f55dd-136">The `RunAsync` method is canceled when a primary replica's role changes away from primary, as well as during the close and abort events.</span><span class="sxs-lookup"><span data-stu-id="f55dd-136">The `RunAsync` method is canceled when a primary replica's role changes away from primary, as well as during the close and abort events.</span></span>

<span data-ttu-id="f55dd-137">Using the `OnChangeRoleAsync` event allows you to perform work depending on replica role as well as in response to role change.</span><span class="sxs-lookup"><span data-stu-id="f55dd-137">Using the `OnChangeRoleAsync` event allows you to perform work depending on replica role as well as in response to role change.</span></span>

<span data-ttu-id="f55dd-138">A stateful service also provides the same four lifecycle events as a stateless service, with the same semantics and use cases:</span><span class="sxs-lookup"><span data-stu-id="f55dd-138">A stateful service also provides the same four lifecycle events as a stateless service, with the same semantics and use cases:</span></span>

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a><span data-ttu-id="f55dd-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="f55dd-139">Next steps</span></span>
<span data-ttu-id="f55dd-140">For more advanced topics related to Service Fabric, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="f55dd-140">For more advanced topics related to Service Fabric, see the following articles:</span></span>

* [<span data-ttu-id="f55dd-141">Configuring stateful Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f55dd-141">Configuring stateful Reliable Services</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="f55dd-142">Service Fabric health introduction</span><span class="sxs-lookup"><span data-stu-id="f55dd-142">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="f55dd-143">Using system health reports for troubleshooting</span><span class="sxs-lookup"><span data-stu-id="f55dd-143">Using system health reports for troubleshooting</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="f55dd-144">Configuring Services with the Service Fabric Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f55dd-144">Configuring Services with the Service Fabric Cluster Resource Manager</span></span>](service-fabric-cluster-resource-manager-configure-services.md)
