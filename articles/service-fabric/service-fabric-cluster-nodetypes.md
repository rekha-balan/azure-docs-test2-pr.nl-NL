---
title: Service Fabric node types and VM Scale Sets | Microsoft Docs
description: Describes how Service Fabric node types relate to VM Scale Sets and how to remote connect to a VM Scale Set instance or a cluster node.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: ''
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: chackdan
ms.openlocfilehash: e944c423457fd3af7aee26dfbed61f2ed81caf45
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662442"
---
# <a name="the-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="087cb-103">The relationship between Service Fabric node types and Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="087cb-103">The relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="087cb-104">Virtual Machine Scale Sets are an Azure Compute resource you can use to deploy and manage a collection of virtual machines as a set.</span><span class="sxs-lookup"><span data-stu-id="087cb-104">Virtual Machine Scale Sets are an Azure Compute resource you can use to deploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="087cb-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span><span class="sxs-lookup"><span data-stu-id="087cb-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="087cb-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span><span class="sxs-lookup"><span data-stu-id="087cb-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="087cb-107">The following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span><span class="sxs-lookup"><span data-stu-id="087cb-107">The following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="087cb-108">Each node type has five nodes each.</span><span class="sxs-lookup"><span data-stu-id="087cb-108">Each node type has five nodes each.</span></span>

![Screen shot of a cluster that has two Node Types][NodeTypes]

## <a name="mapping-vm-scale-set-instances-to-nodes"></a><span data-ttu-id="087cb-110">Mapping VM Scale Set instances to nodes</span><span class="sxs-lookup"><span data-stu-id="087cb-110">Mapping VM Scale Set instances to nodes</span></span>
<span data-ttu-id="087cb-111">As you can see above, the VM Scale Set instances start from instance 0 and then goes up.</span><span class="sxs-lookup"><span data-stu-id="087cb-111">As you can see above, the VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="087cb-112">The numbering is reflected in the names.</span><span class="sxs-lookup"><span data-stu-id="087cb-112">The numbering is reflected in the names.</span></span> <span data-ttu-id="087cb-113">For example, BackEnd_0 is instance 0 of the BackEnd VM Scale Set.</span><span class="sxs-lookup"><span data-stu-id="087cb-113">For example, BackEnd_0 is instance 0 of the BackEnd VM Scale Set.</span></span> <span data-ttu-id="087cb-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="087cb-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="087cb-115">When you scale up a VM Scale Set a new instance is created.</span><span class="sxs-lookup"><span data-stu-id="087cb-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="087cb-116">The new VM Scale Set instance name will typically be the VM Scale Set name + the next instance number.</span><span class="sxs-lookup"><span data-stu-id="087cb-116">The new VM Scale Set instance name will typically be the VM Scale Set name + the next instance number.</span></span> <span data-ttu-id="087cb-117">In our example, it is BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="087cb-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-to-each-node-typevm-scale-set"></a><span data-ttu-id="087cb-118">Mapping VM scale set load balancers to each node type/VM Scale Set</span><span class="sxs-lookup"><span data-stu-id="087cb-118">Mapping VM scale set load balancers to each node type/VM Scale Set</span></span>
<span data-ttu-id="087cb-119">If you have deployed your cluster from the portal or have used the sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see the load balancers for each VM Scale Set or node type.</span><span class="sxs-lookup"><span data-stu-id="087cb-119">If you have deployed your cluster from the portal or have used the sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see the load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="087cb-120">The name would something like: **LB-&lt;NodeType name&gt;**.</span><span class="sxs-lookup"><span data-stu-id="087cb-120">The name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="087cb-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span><span class="sxs-lookup"><span data-stu-id="087cb-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Resources][Resources]

## <a name="remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="087cb-123">Remote connect to a VM Scale Set instance or a cluster node</span><span class="sxs-lookup"><span data-stu-id="087cb-123">Remote connect to a VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="087cb-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span><span class="sxs-lookup"><span data-stu-id="087cb-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="087cb-125">That means the node types can be scaled up or down independently and can be made of different VM SKUs.</span><span class="sxs-lookup"><span data-stu-id="087cb-125">That means the node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="087cb-126">Unlike single instance VMs, the VM Scale Set instances do not get a virtual IP address of their own.</span><span class="sxs-lookup"><span data-stu-id="087cb-126">Unlike single instance VMs, the VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="087cb-127">So it can be a bit challenging when you are looking for an IP address and port that you can use to remote connect to a specific instance.</span><span class="sxs-lookup"><span data-stu-id="087cb-127">So it can be a bit challenging when you are looking for an IP address and port that you can use to remote connect to a specific instance.</span></span>

<span data-ttu-id="087cb-128">Here are the steps you can follow to discover them.</span><span class="sxs-lookup"><span data-stu-id="087cb-128">Here are the steps you can follow to discover them.</span></span>

### <a name="step-1-find-out-the-virtual-ip-address-for-the-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="087cb-129">Step 1: Find out the virtual IP address for the node type and then Inbound NAT rules for RDP</span><span class="sxs-lookup"><span data-stu-id="087cb-129">Step 1: Find out the virtual IP address for the node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="087cb-130">In order to get that, you need to get the inbound NAT rules values that were defined as a part of the resource definition for **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="087cb-130">In order to get that, you need to get the inbound NAT rules values that were defined as a part of the resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="087cb-131">In the portal, navigate to the Load balancer blade and then **Settings**.</span><span class="sxs-lookup"><span data-stu-id="087cb-131">In the portal, navigate to the Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="087cb-133">In **Settings**, click on **Inbound NAT rules**.</span><span class="sxs-lookup"><span data-stu-id="087cb-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="087cb-134">This now gives you the IP address and port that you can use to remote connect to the first VM Scale Set instance.</span><span class="sxs-lookup"><span data-stu-id="087cb-134">This now gives you the IP address and port that you can use to remote connect to the first VM Scale Set instance.</span></span> <span data-ttu-id="087cb-135">In the screenshot below, it is **104.42.106.156** and **3389**</span><span class="sxs-lookup"><span data-stu-id="087cb-135">In the screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-the-port-that-you-can-use-to-remote-connect-to-the-specific-vm-scale-set-instancenode"></a><span data-ttu-id="087cb-137">Step 2: Find out the port that you can use to remote connect to the specific VM Scale Set instance/node</span><span class="sxs-lookup"><span data-stu-id="087cb-137">Step 2: Find out the port that you can use to remote connect to the specific VM Scale Set instance/node</span></span>
<span data-ttu-id="087cb-138">Earlier in this document, I talked about how the VM Scale Set instances map to the nodes.</span><span class="sxs-lookup"><span data-stu-id="087cb-138">Earlier in this document, I talked about how the VM Scale Set instances map to the nodes.</span></span> <span data-ttu-id="087cb-139">We will use that to figure out the exact port.</span><span class="sxs-lookup"><span data-stu-id="087cb-139">We will use that to figure out the exact port.</span></span>

<span data-ttu-id="087cb-140">The ports are allocated in ascending order of the VM Scale Set instance.</span><span class="sxs-lookup"><span data-stu-id="087cb-140">The ports are allocated in ascending order of the VM Scale Set instance.</span></span> <span data-ttu-id="087cb-141">so in my example for the FrontEnd node type, the ports for each of the five instances are the following.</span><span class="sxs-lookup"><span data-stu-id="087cb-141">so in my example for the FrontEnd node type, the ports for each of the five instances are the following.</span></span> <span data-ttu-id="087cb-142">you now need to do the same mapping for your VM Scale Set instance.</span><span class="sxs-lookup"><span data-stu-id="087cb-142">you now need to do the same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="087cb-143">**VM Scale Set Instance**</span><span class="sxs-lookup"><span data-stu-id="087cb-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="087cb-144">**Port**</span><span class="sxs-lookup"><span data-stu-id="087cb-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="087cb-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="087cb-145">FrontEnd_0</span></span> |<span data-ttu-id="087cb-146">3389</span><span class="sxs-lookup"><span data-stu-id="087cb-146">3389</span></span> |
| <span data-ttu-id="087cb-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="087cb-147">FrontEnd_1</span></span> |<span data-ttu-id="087cb-148">3390</span><span class="sxs-lookup"><span data-stu-id="087cb-148">3390</span></span> |
| <span data-ttu-id="087cb-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="087cb-149">FrontEnd_2</span></span> |<span data-ttu-id="087cb-150">3391</span><span class="sxs-lookup"><span data-stu-id="087cb-150">3391</span></span> |
| <span data-ttu-id="087cb-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="087cb-151">FrontEnd_3</span></span> |<span data-ttu-id="087cb-152">3392</span><span class="sxs-lookup"><span data-stu-id="087cb-152">3392</span></span> |
| <span data-ttu-id="087cb-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="087cb-153">FrontEnd_4</span></span> |<span data-ttu-id="087cb-154">3393</span><span class="sxs-lookup"><span data-stu-id="087cb-154">3393</span></span> |
| <span data-ttu-id="087cb-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="087cb-155">FrontEnd_5</span></span> |<span data-ttu-id="087cb-156">3394</span><span class="sxs-lookup"><span data-stu-id="087cb-156">3394</span></span> |

### <a name="step-3-remote-connect-to-the-specific-vm-scale-set-instance"></a><span data-ttu-id="087cb-157">Step 3: Remote connect to the specific VM Scale Set instance</span><span class="sxs-lookup"><span data-stu-id="087cb-157">Step 3: Remote connect to the specific VM Scale Set instance</span></span>
<span data-ttu-id="087cb-158">In the screenshot below I use Remote Desktop Connection to connect to the FrontEnd_1:</span><span class="sxs-lookup"><span data-stu-id="087cb-158">In the screenshot below I use Remote Desktop Connection to connect to the FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-to-change-the-rdp-port-range-values"></a><span data-ttu-id="087cb-160">How to change the RDP port range values</span><span class="sxs-lookup"><span data-stu-id="087cb-160">How to change the RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="087cb-161">Before cluster deployment</span><span class="sxs-lookup"><span data-stu-id="087cb-161">Before cluster deployment</span></span>
<span data-ttu-id="087cb-162">When you are setting up the cluster using an Resource Manager template, you can specify the range in the **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="087cb-162">When you are setting up the cluster using an Resource Manager template, you can specify the range in the **inboundNatPools**.</span></span>

<span data-ttu-id="087cb-163">Go to the resource definition for **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="087cb-163">Go to the resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="087cb-164">Under that you find the description for **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="087cb-164">Under that you find the description for **inboundNatPools**.</span></span>  <span data-ttu-id="087cb-165">Replace the *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span><span class="sxs-lookup"><span data-stu-id="087cb-165">Replace the *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![InboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="087cb-167">After cluster deployment</span><span class="sxs-lookup"><span data-stu-id="087cb-167">After cluster deployment</span></span>
<span data-ttu-id="087cb-168">This is a bit more involved and may result in the VMs getting recycled.</span><span class="sxs-lookup"><span data-stu-id="087cb-168">This is a bit more involved and may result in the VMs getting recycled.</span></span> <span data-ttu-id="087cb-169">You will now have to set new values using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="087cb-169">You will now have to set new values using Azure PowerShell.</span></span> <span data-ttu-id="087cb-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="087cb-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="087cb-171">If you have not done this before, I strongly suggest that you follow the steps outlined in [How to install and configure Azure PowerShell.](/powershell/azureps-cmdlets-docs)</span><span class="sxs-lookup"><span data-stu-id="087cb-171">If you have not done this before, I strongly suggest that you follow the steps outlined in [How to install and configure Azure PowerShell.](/powershell/azureps-cmdlets-docs)</span></span>

<span data-ttu-id="087cb-172">Sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="087cb-172">Sign in to your Azure account.</span></span> <span data-ttu-id="087cb-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span><span class="sxs-lookup"><span data-stu-id="087cb-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="087cb-174">Run the following to get details on your load balancer and you see the values for the description for **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="087cb-174">Run the following to get details on your load balancer and you see the values for the description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="087cb-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* to the values you want.</span><span class="sxs-lookup"><span data-stu-id="087cb-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* to the values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use the API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="087cb-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="087cb-176">Next steps</span></span>
* [<span data-ttu-id="087cb-177">Overview of the "Deploy anywhere" feature and a comparison with Azure-managed clusters</span><span class="sxs-lookup"><span data-stu-id="087cb-177">Overview of the "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="087cb-178">Cluster security</span><span class="sxs-lookup"><span data-stu-id="087cb-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="087cb-179"> Service Fabric SDK and getting started</span><span class="sxs-lookup"><span data-stu-id="087cb-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cluster-nodetypes/RDP.png






