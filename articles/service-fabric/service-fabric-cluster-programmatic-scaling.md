---
title: Azure Service Fabric Programmatic Scaling | Microsoft Docs
description: Scale an Azure Service Fabric cluster in or out programmatically, according to custom triggers
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: ''
ms.assetid: ''
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: mikerou
ms.openlocfilehash: 8d7052fabeb348b4bba744b43d9af78f058175a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555983"
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="98a16-103">Scale a Service Fabric cluster programmatically</span><span class="sxs-lookup"><span data-stu-id="98a16-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="98a16-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="98a16-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="98a16-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span><span class="sxs-lookup"><span data-stu-id="98a16-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="98a16-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span><span class="sxs-lookup"><span data-stu-id="98a16-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="98a16-107">Reasons for programmatic scaling</span><span class="sxs-lookup"><span data-stu-id="98a16-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="98a16-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span><span class="sxs-lookup"><span data-stu-id="98a16-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="98a16-109">In other scenarios, though, they may not be the right fit.</span><span class="sxs-lookup"><span data-stu-id="98a16-109">In other scenarios, though, they may not be the right fit.</span></span> <span data-ttu-id="98a16-110">Potential drawbacks to these approaches include:</span><span class="sxs-lookup"><span data-stu-id="98a16-110">Potential drawbacks to these approaches include:</span></span>

- <span data-ttu-id="98a16-111">Manually scaling requires you to log in and explicitly request scaling operations.</span><span class="sxs-lookup"><span data-stu-id="98a16-111">Manually scaling requires you to log in and explicitly request scaling operations.</span></span> <span data-ttu-id="98a16-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span><span class="sxs-lookup"><span data-stu-id="98a16-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="98a16-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span><span class="sxs-lookup"><span data-stu-id="98a16-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="98a16-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span><span class="sxs-lookup"><span data-stu-id="98a16-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="98a16-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span><span class="sxs-lookup"><span data-stu-id="98a16-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="98a16-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="98a16-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span></span>
  - <span data-ttu-id="98a16-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span><span class="sxs-lookup"><span data-stu-id="98a16-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="98a16-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span><span class="sxs-lookup"><span data-stu-id="98a16-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="98a16-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span><span class="sxs-lookup"><span data-stu-id="98a16-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="98a16-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span><span class="sxs-lookup"><span data-stu-id="98a16-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="98a16-121">Scaling APIs</span><span class="sxs-lookup"><span data-stu-id="98a16-121">Scaling APIs</span></span>
<span data-ttu-id="98a16-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span><span class="sxs-lookup"><span data-stu-id="98a16-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="98a16-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span><span class="sxs-lookup"><span data-stu-id="98a16-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span></span> 

<span data-ttu-id="98a16-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span><span class="sxs-lookup"><span data-stu-id="98a16-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span></span> <span data-ttu-id="98a16-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span><span class="sxs-lookup"><span data-stu-id="98a16-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="98a16-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the fluent [Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/1.0.0-beta50).</span><span class="sxs-lookup"><span data-stu-id="98a16-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the fluent [Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/1.0.0-beta50).</span></span> <span data-ttu-id="98a16-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span><span class="sxs-lookup"><span data-stu-id="98a16-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="98a16-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="98a16-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="98a16-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span><span class="sxs-lookup"><span data-stu-id="98a16-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span></span> <span data-ttu-id="98a16-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="98a16-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="98a16-131">Credential management</span><span class="sxs-lookup"><span data-stu-id="98a16-131">Credential management</span></span>
<span data-ttu-id="98a16-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span><span class="sxs-lookup"><span data-stu-id="98a16-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="98a16-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span><span class="sxs-lookup"><span data-stu-id="98a16-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="98a16-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="98a16-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="98a16-135">A service principal can be created with the following steps:</span><span class="sxs-lookup"><span data-stu-id="98a16-135">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="98a16-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="98a16-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="98a16-137">Create the service principal with `az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="98a16-137">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="98a16-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span><span class="sxs-lookup"><span data-stu-id="98a16-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="98a16-139">You will also need your subscription ID, which can be viewed with `az account list`</span><span class="sxs-lookup"><span data-stu-id="98a16-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="98a16-140">The fluent compute library can log in using these credentials as follows:</span><span class="sxs-lookup"><span data-stu-id="98a16-140">The fluent compute library can log in using these credentials as follows:</span></span>

```C#
var credentials = AzureCredentials.FromServicePrincipal(AzureClientId, AzureClientKey, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed to login to Azure");
}
```

<span data-ttu-id="98a16-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="98a16-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="98a16-142">Scaling out</span><span class="sxs-lookup"><span data-stu-id="98a16-142">Scaling out</span></span>
<span data-ttu-id="98a16-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span><span class="sxs-lookup"><span data-stu-id="98a16-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient?.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = Math.Min(MaximumNodeCount, NodeCount.Value + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="98a16-144">**There is currently [a bug](https://github.com/Azure/azure-sdk-for-net/issues/2716) that keeps this code from working**, but a fix has been merged, so the issue should be resolved in published versions of Microsoft.Azure.Management.Compute.Fluent soon.</span><span class="sxs-lookup"><span data-stu-id="98a16-144">**There is currently [a bug](https://github.com/Azure/azure-sdk-for-net/issues/2716) that keeps this code from working**, but a fix has been merged, so the issue should be resolved in published versions of Microsoft.Azure.Management.Compute.Fluent soon.</span></span> <span data-ttu-id="98a16-145">The bug is that when changing virtual machine scale set properties (like capacity) with the fluent compute API, protected settings from the scale set's Resource Manager template are lost.</span><span class="sxs-lookup"><span data-stu-id="98a16-145">The bug is that when changing virtual machine scale set properties (like capacity) with the fluent compute API, protected settings from the scale set's Resource Manager template are lost.</span></span> <span data-ttu-id="98a16-146">These missing settings cause (among other things) Service Fabric services to not set up properly on new virtual machine instances.</span><span class="sxs-lookup"><span data-stu-id="98a16-146">These missing settings cause (among other things) Service Fabric services to not set up properly on new virtual machine instances.</span></span>

<span data-ttu-id="98a16-147">As a temporary workaround, PowerShell cmdlets can be invoked from the scaling service to enact the same change (though this route means that PowerShell tools must be present):</span><span class="sxs-lookup"><span data-stu-id="98a16-147">As a temporary workaround, PowerShell cmdlets can be invoked from the scaling service to enact the same change (though this route means that PowerShell tools must be present):</span></span>

```C#
using (var psInstance = PowerShell.Create())
{
    psInstance.AddScript($@"
        $clientId = ""{AzureClientId}""
        $clientKey = ConvertTo-SecureString -String ""{AzureClientKey}"" -AsPlainText -Force
        $Credential = New-Object -TypeName ""System.Management.Automation.PSCredential"" -ArgumentList $clientId, $clientKey
        Login-AzureRmAccount -Credential $Credential -ServicePrincipal -TenantId {AzureTenantId}
        
        $vmss = Get-AzureRmVmss -ResourceGroupName {ResourceGroup} -VMScaleSetName {NodeTypeToScale}
        $vmss.sku.capacity = {newCapacity}
        Update-AzureRmVmss -ResourceGroupName {ResourceGroup} -Name {NodeTypeToScale} -VirtualMachineScaleSet $vmss
    ");

    psInstance.Invoke();

    if (psInstance.HadErrors)
    {
        foreach (var error in psInstance.Streams.Error)
        {
            ServiceEventSource.Current.ServiceMessage(Context, $"ERROR adding node: {error.ToString()}");
        }
    }                
}
```

<span data-ttu-id="98a16-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="98a16-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="98a16-149">Scaling in</span><span class="sxs-lookup"><span data-stu-id="98a16-149">Scaling in</span></span>

<span data-ttu-id="98a16-150">Scaling in is similar to scaling out. The actual virtual machine scale set changes are practically the same.</span><span class="sxs-lookup"><span data-stu-id="98a16-150">Scaling in is similar to scaling out. The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="98a16-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span><span class="sxs-lookup"><span data-stu-id="98a16-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="98a16-152">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span><span class="sxs-lookup"><span data-stu-id="98a16-152">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="98a16-153">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span><span class="sxs-lookup"><span data-stu-id="98a16-153">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span></span> <span data-ttu-id="98a16-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="98a16-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="98a16-155">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span><span class="sxs-lookup"><span data-stu-id="98a16-155">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="98a16-156">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span><span class="sxs-lookup"><span data-stu-id="98a16-156">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient?.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove the node from the Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up to a timeout) for the node to gracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = Math.Max(MinimumNodeCount, NodeCount.Value - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="98a16-157">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span><span class="sxs-lookup"><span data-stu-id="98a16-157">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

<span data-ttu-id="98a16-158">As before, you need to work around `IVirtualMachineScaleSet.Update()` not working until [Azure/azure-sdk-for-net#2716](https://github.com/Azure/azure-sdk-for-net/issues/2716) is addressed.</span><span class="sxs-lookup"><span data-stu-id="98a16-158">As before, you need to work around `IVirtualMachineScaleSet.Update()` not working until [Azure/azure-sdk-for-net#2716](https://github.com/Azure/azure-sdk-for-net/issues/2716) is addressed.</span></span>

## <a name="potential-drawbacks"></a><span data-ttu-id="98a16-159">Potential drawbacks</span><span class="sxs-lookup"><span data-stu-id="98a16-159">Potential drawbacks</span></span>

<span data-ttu-id="98a16-160">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span><span class="sxs-lookup"><span data-stu-id="98a16-160">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="98a16-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span><span class="sxs-lookup"><span data-stu-id="98a16-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="98a16-162">Using this approach means that you need to own scaling code, which is non-trivial.</span><span class="sxs-lookup"><span data-stu-id="98a16-162">Using this approach means that you need to own scaling code, which is non-trivial.</span></span>

<span data-ttu-id="98a16-163">How you should approach Service Fabric scaling depends on your scenario.</span><span class="sxs-lookup"><span data-stu-id="98a16-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="98a16-164">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span><span class="sxs-lookup"><span data-stu-id="98a16-164">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="98a16-165">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span><span class="sxs-lookup"><span data-stu-id="98a16-165">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98a16-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="98a16-166">Next steps</span></span>

<span data-ttu-id="98a16-167">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span><span class="sxs-lookup"><span data-stu-id="98a16-167">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="98a16-168">Scaling manually or with auto-scale rules</span><span class="sxs-lookup"><span data-stu-id="98a16-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="98a16-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span><span class="sxs-lookup"><span data-stu-id="98a16-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="98a16-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span><span class="sxs-lookup"><span data-stu-id="98a16-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>