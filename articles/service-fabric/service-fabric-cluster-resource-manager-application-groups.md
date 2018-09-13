---
title: Service Fabric Cluster Resource Manager - Application Groups | Microsoft Docs
description: Overview of the Application Group functionality in the Service Fabric Cluster Resource Manager
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: ''
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 8297ef2e9a42a0b4aec26f977d090847471e0913
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783320"
---
# <a name="introduction-to-application-groups"></a><span data-ttu-id="6a40f-103">Introduction to Application Groups</span><span class="sxs-lookup"><span data-stu-id="6a40f-103">Introduction to Application Groups</span></span>
<span data-ttu-id="6a40f-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading the load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout the cluster.</span><span class="sxs-lookup"><span data-stu-id="6a40f-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading the load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout the cluster.</span></span> <span data-ttu-id="6a40f-105">Service Fabric manages the capacity of the nodes in the cluster and the cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="6a40f-105">Service Fabric manages the capacity of the nodes in the cluster and the cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="6a40f-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span><span class="sxs-lookup"><span data-stu-id="6a40f-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="6a40f-107">For example you may want to:</span><span class="sxs-lookup"><span data-stu-id="6a40f-107">For example you may want to:</span></span>

- <span data-ttu-id="6a40f-108">Reserve some capacity on the nodes in the cluster for the services within some named application instance</span><span class="sxs-lookup"><span data-stu-id="6a40f-108">Reserve some capacity on the nodes in the cluster for the services within some named application instance</span></span>
- <span data-ttu-id="6a40f-109">Limit the total number of nodes that the services within a named application instance run on (instead of spreading them out over the entire cluster)</span><span class="sxs-lookup"><span data-stu-id="6a40f-109">Limit the total number of nodes that the services within a named application instance run on (instead of spreading them out over the entire cluster)</span></span>
- <span data-ttu-id="6a40f-110">Define capacities on the named application instance itself to limit the number of services or total resource consumption of the services inside it</span><span class="sxs-lookup"><span data-stu-id="6a40f-110">Define capacities on the named application instance itself to limit the number of services or total resource consumption of the services inside it</span></span>

<span data-ttu-id="6a40f-111">To meet these requirements, the Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span><span class="sxs-lookup"><span data-stu-id="6a40f-111">To meet these requirements, the Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-the-maximum-number-of-nodes"></a><span data-ttu-id="6a40f-112">Limiting the maximum number of nodes</span><span class="sxs-lookup"><span data-stu-id="6a40f-112">Limiting the maximum number of nodes</span></span>
<span data-ttu-id="6a40f-113">The simplest use case for Application capacity is when an application instance needs to be limited to a certain maximum number of nodes.</span><span class="sxs-lookup"><span data-stu-id="6a40f-113">The simplest use case for Application capacity is when an application instance needs to be limited to a certain maximum number of nodes.</span></span> <span data-ttu-id="6a40f-114">This consolidates all services within that application instance onto a set number of machines.</span><span class="sxs-lookup"><span data-stu-id="6a40f-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="6a40f-115">Consolidation is useful when you're trying to predict or cap physical resource use by the services within that named application instance.</span><span class="sxs-lookup"><span data-stu-id="6a40f-115">Consolidation is useful when you're trying to predict or cap physical resource use by the services within that named application instance.</span></span> 

<span data-ttu-id="6a40f-116">The following image shows an application instance with and without a maximum number of nodes defined:</span><span class="sxs-lookup"><span data-stu-id="6a40f-116">The following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="6a40f-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="6a40f-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="6a40f-118">In the left example, the application doesn’t have a maximum number of nodes defined, and it has three services.</span><span class="sxs-lookup"><span data-stu-id="6a40f-118">In the left example, the application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="6a40f-119">The Cluster Resource Manager has spread out all replicas across six available nodes to achieve the best balance in the cluster (the default behavior).</span><span class="sxs-lookup"><span data-stu-id="6a40f-119">The Cluster Resource Manager has spread out all replicas across six available nodes to achieve the best balance in the cluster (the default behavior).</span></span> <span data-ttu-id="6a40f-120">In the right example, we see the same application limited to three nodes.</span><span class="sxs-lookup"><span data-stu-id="6a40f-120">In the right example, we see the same application limited to three nodes.</span></span>

<span data-ttu-id="6a40f-121">The parameter that controls this behavior is called MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="6a40f-121">The parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="6a40f-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span><span class="sxs-lookup"><span data-stu-id="6a40f-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="6a40f-123">Powershell</span><span class="sxs-lookup"><span data-stu-id="6a40f-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –ApplicationName fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="6a40f-124">C#</span><span class="sxs-lookup"><span data-stu-id="6a40f-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="6a40f-125">Within the set of nodes, the Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span><span class="sxs-lookup"><span data-stu-id="6a40f-125">Within the set of nodes, the Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="6a40f-126">Application Metrics, Load, and Capacity</span><span class="sxs-lookup"><span data-stu-id="6a40f-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="6a40f-127">Application Groups also allow you to define metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span><span class="sxs-lookup"><span data-stu-id="6a40f-127">Application Groups also allow you to define metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="6a40f-128">Application metrics allow you to track, reserve, and limit the resource consumption of the services inside that application instance.</span><span class="sxs-lookup"><span data-stu-id="6a40f-128">Application metrics allow you to track, reserve, and limit the resource consumption of the services inside that application instance.</span></span>

<span data-ttu-id="6a40f-129">For each application metric, there are two values that can be set:</span><span class="sxs-lookup"><span data-stu-id="6a40f-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="6a40f-130">**Total Application Capacity** – This setting represents the total capacity of the application for a particular metric.</span><span class="sxs-lookup"><span data-stu-id="6a40f-130">**Total Application Capacity** – This setting represents the total capacity of the application for a particular metric.</span></span> <span data-ttu-id="6a40f-131">The Cluster Resource Manager disallows the creation of any new services within this application instance that would cause total load to exceed this value.</span><span class="sxs-lookup"><span data-stu-id="6a40f-131">The Cluster Resource Manager disallows the creation of any new services within this application instance that would cause total load to exceed this value.</span></span> <span data-ttu-id="6a40f-132">For example, let's say the application instance had a capacity of 10 and already had load of five.</span><span class="sxs-lookup"><span data-stu-id="6a40f-132">For example, let's say the application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="6a40f-133">The creation of a service with a total default load of 10 would be disallowed.</span><span class="sxs-lookup"><span data-stu-id="6a40f-133">The creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="6a40f-134">**Maximum Node Capacity** – This setting specifies the maximum total load for the application on a single node.</span><span class="sxs-lookup"><span data-stu-id="6a40f-134">**Maximum Node Capacity** – This setting specifies the maximum total load for the application on a single node.</span></span> <span data-ttu-id="6a40f-135">If load goes over this capacity, the Cluster Resource Manager moves replicas to other nodes so that the load decreases.</span><span class="sxs-lookup"><span data-stu-id="6a40f-135">If load goes over this capacity, the Cluster Resource Manager moves replicas to other nodes so that the load decreases.</span></span>


<span data-ttu-id="6a40f-136">Powershell:</span><span class="sxs-lookup"><span data-stu-id="6a40f-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="6a40f-137">C#:</span><span class="sxs-lookup"><span data-stu-id="6a40f-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="6a40f-138">Reserving Capacity</span><span class="sxs-lookup"><span data-stu-id="6a40f-138">Reserving Capacity</span></span>
<span data-ttu-id="6a40f-139">Another common use for application groups is to ensure that resources within the cluster are reserved for a given application instance.</span><span class="sxs-lookup"><span data-stu-id="6a40f-139">Another common use for application groups is to ensure that resources within the cluster are reserved for a given application instance.</span></span> <span data-ttu-id="6a40f-140">The space is always reserved when the application instance is created.</span><span class="sxs-lookup"><span data-stu-id="6a40f-140">The space is always reserved when the application instance is created.</span></span>

<span data-ttu-id="6a40f-141">Reserving space in the cluster for the application happens immediately even when:</span><span class="sxs-lookup"><span data-stu-id="6a40f-141">Reserving space in the cluster for the application happens immediately even when:</span></span>
- <span data-ttu-id="6a40f-142">the application instance is created but doesn't have any services within it yet</span><span class="sxs-lookup"><span data-stu-id="6a40f-142">the application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="6a40f-143">the number of services within the application instance changes every time</span><span class="sxs-lookup"><span data-stu-id="6a40f-143">the number of services within the application instance changes every time</span></span> 
- <span data-ttu-id="6a40f-144">the services exist but aren't consuming the resources</span><span class="sxs-lookup"><span data-stu-id="6a40f-144">the services exist but aren't consuming the resources</span></span> 

<span data-ttu-id="6a40f-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="6a40f-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="6a40f-146">**MinimumNodes** - Defines the minimum number of nodes that the application instance should run on.</span><span class="sxs-lookup"><span data-stu-id="6a40f-146">**MinimumNodes** - Defines the minimum number of nodes that the application instance should run on.</span></span>  
- <span data-ttu-id="6a40f-147">**NodeReservationCapacity** - This setting is per metric for the application.</span><span class="sxs-lookup"><span data-stu-id="6a40f-147">**NodeReservationCapacity** - This setting is per metric for the application.</span></span> <span data-ttu-id="6a40f-148">The value is the amount of that metric reserved for the application on any node where that the services in that application run.</span><span class="sxs-lookup"><span data-stu-id="6a40f-148">The value is the amount of that metric reserved for the application on any node where that the services in that application run.</span></span>

<span data-ttu-id="6a40f-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for the application within the cluster.</span><span class="sxs-lookup"><span data-stu-id="6a40f-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for the application within the cluster.</span></span> <span data-ttu-id="6a40f-150">If there's less remaining capacity in the cluster than the total reservation required, creation of the application fails.</span><span class="sxs-lookup"><span data-stu-id="6a40f-150">If there's less remaining capacity in the cluster than the total reservation required, creation of the application fails.</span></span> 

<span data-ttu-id="6a40f-151">Let's look at an example of capacity reservation:</span><span class="sxs-lookup"><span data-stu-id="6a40f-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="6a40f-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="6a40f-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="6a40f-153">In the left example, applications do not have any Application Capacity defined.</span><span class="sxs-lookup"><span data-stu-id="6a40f-153">In the left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="6a40f-154">The Cluster Resource Manager balances everything according to normal rules.</span><span class="sxs-lookup"><span data-stu-id="6a40f-154">The Cluster Resource Manager balances everything according to normal rules.</span></span>

<span data-ttu-id="6a40f-155">In the example on the right, let's say that Application1 was created with the following settings:</span><span class="sxs-lookup"><span data-stu-id="6a40f-155">In the example on the right, let's say that Application1 was created with the following settings:</span></span>

- <span data-ttu-id="6a40f-156">MinimumNodes set to two</span><span class="sxs-lookup"><span data-stu-id="6a40f-156">MinimumNodes set to two</span></span>
- <span data-ttu-id="6a40f-157">An application Metric defined with</span><span class="sxs-lookup"><span data-stu-id="6a40f-157">An application Metric defined with</span></span>
  - <span data-ttu-id="6a40f-158">NodeReservationCapacity of 20</span><span class="sxs-lookup"><span data-stu-id="6a40f-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="6a40f-159">Powershell</span><span class="sxs-lookup"><span data-stu-id="6a40f-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="6a40f-160">C#</span><span class="sxs-lookup"><span data-stu-id="6a40f-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="6a40f-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 to consume that capacity even if there are no load is being consumed by the services inside Application1 at the time.</span><span class="sxs-lookup"><span data-stu-id="6a40f-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 to consume that capacity even if there are no load is being consumed by the services inside Application1 at the time.</span></span> <span data-ttu-id="6a40f-162">This reserved application capacity is considered consumed  and counts against the remaining capacity on that node and within the cluster.</span><span class="sxs-lookup"><span data-stu-id="6a40f-162">This reserved application capacity is considered consumed  and counts against the remaining capacity on that node and within the cluster.</span></span>  <span data-ttu-id="6a40f-163">The reservation is deducted from the remaining cluster capacity immediately, however the reserved consumption is deducted from the capacity of a specific node only when at least one service object is placed on it.</span><span class="sxs-lookup"><span data-stu-id="6a40f-163">The reservation is deducted from the remaining cluster capacity immediately, however the reserved consumption is deducted from the capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="6a40f-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span><span class="sxs-lookup"><span data-stu-id="6a40f-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-the-application-load-information"></a><span data-ttu-id="6a40f-165">Obtaining the application load information</span><span class="sxs-lookup"><span data-stu-id="6a40f-165">Obtaining the application load information</span></span>
<span data-ttu-id="6a40f-166">For each application that has an Application Capacity defined for one or more metrics you can obtain the information about the aggregate load reported by replicas of its services.</span><span class="sxs-lookup"><span data-stu-id="6a40f-166">For each application that has an Application Capacity defined for one or more metrics you can obtain the information about the aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="6a40f-167">Powershell:</span><span class="sxs-lookup"><span data-stu-id="6a40f-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoadInformation –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="6a40f-168">C#</span><span class="sxs-lookup"><span data-stu-id="6a40f-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="6a40f-169">The ApplicationLoad query returns the basic information about Application Capacity that was specified for the application.</span><span class="sxs-lookup"><span data-stu-id="6a40f-169">The ApplicationLoad query returns the basic information about Application Capacity that was specified for the application.</span></span> <span data-ttu-id="6a40f-170">This information includes the Minimum Nodes and Maximum Nodes info, and the number that the application is currently occupying.</span><span class="sxs-lookup"><span data-stu-id="6a40f-170">This information includes the Minimum Nodes and Maximum Nodes info, and the number that the application is currently occupying.</span></span> <span data-ttu-id="6a40f-171">It also includes information about each application load metric, including:</span><span class="sxs-lookup"><span data-stu-id="6a40f-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="6a40f-172">Metric Name: Name of the metric.</span><span class="sxs-lookup"><span data-stu-id="6a40f-172">Metric Name: Name of the metric.</span></span>
* <span data-ttu-id="6a40f-173">Reservation Capacity: Cluster Capacity that is reserved in the cluster for this Application.</span><span class="sxs-lookup"><span data-stu-id="6a40f-173">Reservation Capacity: Cluster Capacity that is reserved in the cluster for this Application.</span></span>
* <span data-ttu-id="6a40f-174">Application Load: Total Load of this Application’s child replicas.</span><span class="sxs-lookup"><span data-stu-id="6a40f-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="6a40f-175">Application Capacity: Maximum permitted value of Application Load.</span><span class="sxs-lookup"><span data-stu-id="6a40f-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="6a40f-176">Removing Application Capacity</span><span class="sxs-lookup"><span data-stu-id="6a40f-176">Removing Application Capacity</span></span>
<span data-ttu-id="6a40f-177">Once the Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6a40f-177">Once the Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="6a40f-178">For example:</span><span class="sxs-lookup"><span data-stu-id="6a40f-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="6a40f-179">This command removes all Application capacity management parameters from the application instance.</span><span class="sxs-lookup"><span data-stu-id="6a40f-179">This command removes all Application capacity management parameters from the application instance.</span></span> <span data-ttu-id="6a40f-180">This includes MinimumNodes, MaximumNodes, and the Application's metrics, if any.</span><span class="sxs-lookup"><span data-stu-id="6a40f-180">This includes MinimumNodes, MaximumNodes, and the Application's metrics, if any.</span></span> <span data-ttu-id="6a40f-181">The effect of the command is immediate.</span><span class="sxs-lookup"><span data-stu-id="6a40f-181">The effect of the command is immediate.</span></span> <span data-ttu-id="6a40f-182">After this command completes, the Cluster Resource Manager uses the default behavior for managing applications.</span><span class="sxs-lookup"><span data-stu-id="6a40f-182">After this command completes, the Cluster Resource Manager uses the default behavior for managing applications.</span></span> <span data-ttu-id="6a40f-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="6a40f-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="6a40f-184">Restrictions on Application Capacity</span><span class="sxs-lookup"><span data-stu-id="6a40f-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="6a40f-185">There are several restrictions on Application Capacity parameters that must be respected.</span><span class="sxs-lookup"><span data-stu-id="6a40f-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="6a40f-186">If there are validation errors no changes take place.</span><span class="sxs-lookup"><span data-stu-id="6a40f-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="6a40f-187">All integer parameters must be non-negative numbers.</span><span class="sxs-lookup"><span data-stu-id="6a40f-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="6a40f-188">MinimumNodes must never be greater than MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="6a40f-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="6a40f-189">If capacities for a load metric are defined, then they must follow these rules:</span><span class="sxs-lookup"><span data-stu-id="6a40f-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="6a40f-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span><span class="sxs-lookup"><span data-stu-id="6a40f-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="6a40f-191">For example, you cannot limit the capacity for the metric “CPU” on the node to two units and try to reserve three units on each node.</span><span class="sxs-lookup"><span data-stu-id="6a40f-191">For example, you cannot limit the capacity for the metric “CPU” on the node to two units and try to reserve three units on each node.</span></span>
  - <span data-ttu-id="6a40f-192">If MaximumNodes is specified, then the product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span><span class="sxs-lookup"><span data-stu-id="6a40f-192">If MaximumNodes is specified, then the product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="6a40f-193">For example, let's say the Maximum Node Capacity for load metric “CPU” is set to eight.</span><span class="sxs-lookup"><span data-stu-id="6a40f-193">For example, let's say the Maximum Node Capacity for load metric “CPU” is set to eight.</span></span> <span data-ttu-id="6a40f-194">Let's also say you set the Maximum Nodes to 10.</span><span class="sxs-lookup"><span data-stu-id="6a40f-194">Let's also say you set the Maximum Nodes to 10.</span></span> <span data-ttu-id="6a40f-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span><span class="sxs-lookup"><span data-stu-id="6a40f-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="6a40f-196">The restrictions are enforced both during application creation and updates.</span><span class="sxs-lookup"><span data-stu-id="6a40f-196">The restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-to-use-application-capacity"></a><span data-ttu-id="6a40f-197">How not to use Application Capacity</span><span class="sxs-lookup"><span data-stu-id="6a40f-197">How not to use Application Capacity</span></span>
- <span data-ttu-id="6a40f-198">Do not try to use the Application Group features to constrain the application to a _specific_ subset of nodes.</span><span class="sxs-lookup"><span data-stu-id="6a40f-198">Do not try to use the Application Group features to constrain the application to a _specific_ subset of nodes.</span></span> <span data-ttu-id="6a40f-199">In other words, you can specify that the application runs on at most five nodes, but not which specific five nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="6a40f-199">In other words, you can specify that the application runs on at most five nodes, but not which specific five nodes in the cluster.</span></span> <span data-ttu-id="6a40f-200">Constraining an application to specific nodes can be achieved using placement constraints for services.</span><span class="sxs-lookup"><span data-stu-id="6a40f-200">Constraining an application to specific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="6a40f-201">Do not try to use the Application Capacity to ensure that two services from the same application are placed on the same nodes.</span><span class="sxs-lookup"><span data-stu-id="6a40f-201">Do not try to use the Application Capacity to ensure that two services from the same application are placed on the same nodes.</span></span> <span data-ttu-id="6a40f-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="6a40f-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a40f-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a40f-203">Next steps</span></span>
- <span data-ttu-id="6a40f-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="6a40f-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="6a40f-205">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="6a40f-205">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="6a40f-206">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6a40f-206">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="6a40f-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="6a40f-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="6a40f-208">The Cluster Resource Manager has many options for describing the cluster.</span><span class="sxs-lookup"><span data-stu-id="6a40f-208">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="6a40f-209">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="6a40f-209">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
