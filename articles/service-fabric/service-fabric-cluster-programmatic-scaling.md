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
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2018
ms.author: mikerou
ms.openlocfilehash: dcf4721012fb8ec39bcd1de02c294747357b3539
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784568"
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="f51bd-103">Scale a Service Fabric cluster programmatically</span><span class="sxs-lookup"><span data-stu-id="f51bd-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="f51bd-104">Service Fabric clusters running in Azure are built on top of virtual machine scale sets.</span><span class="sxs-lookup"><span data-stu-id="f51bd-104">Service Fabric clusters running in Azure are built on top of virtual machine scale sets.</span></span>  <span data-ttu-id="f51bd-105">[Cluster scaling](./service-fabric-cluster-scale-up-down.md) describes how Service Fabric clusters can be scaled either manually or with auto-scale rules.</span><span class="sxs-lookup"><span data-stu-id="f51bd-105">[Cluster scaling](./service-fabric-cluster-scale-up-down.md) describes how Service Fabric clusters can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="f51bd-106">This article describes how to manage credentials and scale a cluster in or out using the fluent Azure compute SDK, which is a more advanced scenario.</span><span class="sxs-lookup"><span data-stu-id="f51bd-106">This article describes how to manage credentials and scale a cluster in or out using the fluent Azure compute SDK, which is a more advanced scenario.</span></span> <span data-ttu-id="f51bd-107">For an overview, read [programmatic methods of coordinating Azure scaling operations](service-fabric-cluster-scaling.md#programmatic-scaling).</span><span class="sxs-lookup"><span data-stu-id="f51bd-107">For an overview, read [programmatic methods of coordinating Azure scaling operations](service-fabric-cluster-scaling.md#programmatic-scaling).</span></span> 

## <a name="manage-credentials"></a><span data-ttu-id="f51bd-108">Manage credentials</span><span class="sxs-lookup"><span data-stu-id="f51bd-108">Manage credentials</span></span>
<span data-ttu-id="f51bd-109">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span><span class="sxs-lookup"><span data-stu-id="f51bd-109">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="f51bd-110">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span><span class="sxs-lookup"><span data-stu-id="f51bd-110">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="f51bd-111">To log in, you can use a [service principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f51bd-111">To log in, you can use a [service principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="f51bd-112">A service principal can be created with the following steps:</span><span class="sxs-lookup"><span data-stu-id="f51bd-112">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="f51bd-113">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f51bd-113">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="f51bd-114">Create the service principal with `az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="f51bd-114">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="f51bd-115">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span><span class="sxs-lookup"><span data-stu-id="f51bd-115">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="f51bd-116">You will also need your subscription ID, which can be viewed with `az account list`</span><span class="sxs-lookup"><span data-stu-id="f51bd-116">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="f51bd-117">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span><span class="sxs-lookup"><span data-stu-id="f51bd-117">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```csharp
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
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

<span data-ttu-id="f51bd-118">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="f51bd-118">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="f51bd-119">Scaling out</span><span class="sxs-lookup"><span data-stu-id="f51bd-119">Scaling out</span></span>
<span data-ttu-id="f51bd-120">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span><span class="sxs-lookup"><span data-stu-id="f51bd-120">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```csharp
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="f51bd-121">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f51bd-121">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="f51bd-122">[`Get-AzureRmVmss`](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span><span class="sxs-lookup"><span data-stu-id="f51bd-122">[`Get-AzureRmVmss`](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span></span> <span data-ttu-id="f51bd-123">The current capacity is available through the `.sku.capacity` property.</span><span class="sxs-lookup"><span data-stu-id="f51bd-123">The current capacity is available through the `.sku.capacity` property.</span></span> <span data-ttu-id="f51bd-124">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvmss) command.</span><span class="sxs-lookup"><span data-stu-id="f51bd-124">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="f51bd-125">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="f51bd-125">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="f51bd-126">Scaling in</span><span class="sxs-lookup"><span data-stu-id="f51bd-126">Scaling in</span></span>

<span data-ttu-id="f51bd-127">Scaling in is similar to scaling out. The actual virtual machine scale set changes are practically the same.</span><span class="sxs-lookup"><span data-stu-id="f51bd-127">Scaling in is similar to scaling out. The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="f51bd-128">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span><span class="sxs-lookup"><span data-stu-id="f51bd-128">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="f51bd-129">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span><span class="sxs-lookup"><span data-stu-id="f51bd-129">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="f51bd-130">Preparing the node for shutdown involves finding the node to be removed (the most recently added virtual machine scale set instance) and deactivating it.</span><span class="sxs-lookup"><span data-stu-id="f51bd-130">Preparing the node for shutdown involves finding the node to be removed (the most recently added virtual machine scale set instance) and deactivating it.</span></span> <span data-ttu-id="f51bd-131">Virtual machine scale set instances are numbered in the order they are added, so newer nodes can be found by comparing the number suffix in the nodes' names (which match the underlying virtual machine scale set instance names).</span><span class="sxs-lookup"><span data-stu-id="f51bd-131">Virtual machine scale set instances are numbered in the order they are added, so newer nodes can be found by comparing the number suffix in the nodes' names (which match the underlying virtual machine scale set instance names).</span></span> 

```csharp
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n =>
        {
            var instanceIdIndex = n.NodeName.LastIndexOf("_");
            var instanceIdString = n.NodeName.Substring(instanceIdIndex + 1);
            return int.Parse(instanceIdString);
        })
        .FirstOrDefault();
```

<span data-ttu-id="f51bd-132">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span><span class="sxs-lookup"><span data-stu-id="f51bd-132">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```csharp
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

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
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="f51bd-133">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span><span class="sxs-lookup"><span data-stu-id="f51bd-133">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="f51bd-134">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span><span class="sxs-lookup"><span data-stu-id="f51bd-134">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```csharp
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="next-steps"></a><span data-ttu-id="f51bd-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="f51bd-135">Next steps</span></span>

<span data-ttu-id="f51bd-136">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span><span class="sxs-lookup"><span data-stu-id="f51bd-136">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="f51bd-137">Scaling manually or with auto-scale rules</span><span class="sxs-lookup"><span data-stu-id="f51bd-137">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="f51bd-138">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span><span class="sxs-lookup"><span data-stu-id="f51bd-138">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="f51bd-139">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span><span class="sxs-lookup"><span data-stu-id="f51bd-139">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
