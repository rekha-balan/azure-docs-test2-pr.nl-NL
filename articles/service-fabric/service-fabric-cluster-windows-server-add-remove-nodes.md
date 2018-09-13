---
title: Add or remove nodes to a standalone Service Fabric cluster | Microsoft Docs
description: Learn how to add or remove nodes to an Azure Service Fabric cluster on a physical or virtual machine running Windows Server, which could be on-premises or in any cloud.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: chackdan
ms.openlocfilehash: 68474b24519a46db71fe59b5d0574cc4700efccb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563593"
---
# <a name="add-or-remove-nodes-to-a-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="34fe1-103">Add or remove nodes to a standalone Service Fabric cluster running on Windows Server</span><span class="sxs-lookup"><span data-stu-id="34fe1-103">Add or remove nodes to a standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="34fe1-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change so that you might need to add or remove multiple nodes to your cluster.</span><span class="sxs-lookup"><span data-stu-id="34fe1-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change so that you might need to add or remove multiple nodes to your cluster.</span></span> <span data-ttu-id="34fe1-105">This article provides detailed steps to achieve this goal.</span><span class="sxs-lookup"><span data-stu-id="34fe1-105">This article provides detailed steps to achieve this goal.</span></span>

## <a name="add-nodes-to-your-cluster"></a><span data-ttu-id="34fe1-106">Add nodes to your cluster</span><span class="sxs-lookup"><span data-stu-id="34fe1-106">Add nodes to your cluster</span></span>
1. <span data-ttu-id="34fe1-107">Prepare the VM/machine you want to add to your cluster by following the steps mentioned in the [Prepare the machines to meet the prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section.</span><span class="sxs-lookup"><span data-stu-id="34fe1-107">Prepare the VM/machine you want to add to your cluster by following the steps mentioned in the [Prepare the machines to meet the prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section.</span></span>
2. <span data-ttu-id="34fe1-108">Plan which fault domain and upgrade domain you are going to add this VM/machine to.</span><span class="sxs-lookup"><span data-stu-id="34fe1-108">Plan which fault domain and upgrade domain you are going to add this VM/machine to.</span></span>
3. <span data-ttu-id="34fe1-109">Remote desktop (RDP) into the VM/machine that you want to add to the cluster.</span><span class="sxs-lookup"><span data-stu-id="34fe1-109">Remote desktop (RDP) into the VM/machine that you want to add to the cluster.</span></span>
4. <span data-ttu-id="34fe1-110">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) to this VM/machine and unzip the package.</span><span class="sxs-lookup"><span data-stu-id="34fe1-110">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) to this VM/machine and unzip the package.</span></span>
5. <span data-ttu-id="34fe1-111">Run Powershell as an administrator, and navigate to the location of the unzipped package.</span><span class="sxs-lookup"><span data-stu-id="34fe1-111">Run Powershell as an administrator, and navigate to the location of the unzipped package.</span></span>
6. <span data-ttu-id="34fe1-112">Run *AddNode.ps1* Powershell with the parameters describing the new node to add.</span><span class="sxs-lookup"><span data-stu-id="34fe1-112">Run *AddNode.ps1* Powershell with the parameters describing the new node to add.</span></span> <span data-ttu-id="34fe1-113">The example below adds a new node called VM5, with type NodeType0, IP address 182.17.34.52 into UD1 and fd:/dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="34fe1-113">The example below adds a new node called VM5, with type NodeType0, IP address 182.17.34.52 into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="34fe1-114">The *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in the existing cluster.</span><span class="sxs-lookup"><span data-stu-id="34fe1-114">The *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in the existing cluster.</span></span> <span data-ttu-id="34fe1-115">For this endpoint, you can choose the IP address of *any* node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="34fe1-115">For this endpoint, you can choose the IP address of *any* node in the cluster.</span></span>

```
.\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA

```
<span data-ttu-id="34fe1-116">You can check if the new node is added by running the cmdlet [Get-ServiceFabricNode](https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode).</span><span class="sxs-lookup"><span data-stu-id="34fe1-116">You can check if the new node is added by running the cmdlet [Get-ServiceFabricNode](https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode).</span></span>


## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="34fe1-117">Remove nodes from your cluster</span><span class="sxs-lookup"><span data-stu-id="34fe1-117">Remove nodes from your cluster</span></span>
<span data-ttu-id="34fe1-118">Depending on the Reliability level chosen for the cluster, you cannot remove the first n (3/5/7/9) nodes of the primary node type.</span><span class="sxs-lookup"><span data-stu-id="34fe1-118">Depending on the Reliability level chosen for the cluster, you cannot remove the first n (3/5/7/9) nodes of the primary node type.</span></span> <span data-ttu-id="34fe1-119">Also note that running RemoveNode command on a dev cluster is not supported.</span><span class="sxs-lookup"><span data-stu-id="34fe1-119">Also note that running RemoveNode command on a dev cluster is not supported.</span></span>

1. <span data-ttu-id="34fe1-120">Remote desktop (RDP) into the VM/machine that you want to remove from the cluster.</span><span class="sxs-lookup"><span data-stu-id="34fe1-120">Remote desktop (RDP) into the VM/machine that you want to remove from the cluster.</span></span>
2. <span data-ttu-id="34fe1-121">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) and unzip the package to this VM/machine.</span><span class="sxs-lookup"><span data-stu-id="34fe1-121">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) and unzip the package to this VM/machine.</span></span>
3. <span data-ttu-id="34fe1-122">Run Powershell as an administrator, and navigate to the location of the unzipped package.</span><span class="sxs-lookup"><span data-stu-id="34fe1-122">Run Powershell as an administrator, and navigate to the location of the unzipped package.</span></span>
4. <span data-ttu-id="34fe1-123">Run *RemoveNode.ps1* in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34fe1-123">Run *RemoveNode.ps1* in PowerShell.</span></span> <span data-ttu-id="34fe1-124">The example below removes the current node from the cluster.</span><span class="sxs-lookup"><span data-stu-id="34fe1-124">The example below removes the current node from the cluster.</span></span> <span data-ttu-id="34fe1-125">The *ExistingClientConnectionEndpoint* is a client connection endpoint for any node that will remain in the cluster.</span><span class="sxs-lookup"><span data-stu-id="34fe1-125">The *ExistingClientConnectionEndpoint* is a client connection endpoint for any node that will remain in the cluster.</span></span> <span data-ttu-id="34fe1-126">Choose the IP address and the endpoint port of *any* **other node** in the cluster.</span><span class="sxs-lookup"><span data-stu-id="34fe1-126">Choose the IP address and the endpoint port of *any* **other node** in the cluster.</span></span> <span data-ttu-id="34fe1-127">This **other node** will in turn update the cluster configuration for the removed node.</span><span class="sxs-lookup"><span data-stu-id="34fe1-127">This **other node** will in turn update the cluster configuration for the removed node.</span></span> 

```

.\RemoveNode.ps1 -ExistingClientConnectionEndpoint 182.17.34.50:19000

```

> [!NOTE]
> <span data-ttu-id="34fe1-128">Some nodes may not be removed due to system services dependencies.</span><span class="sxs-lookup"><span data-stu-id="34fe1-128">Some nodes may not be removed due to system services dependencies.</span></span> <span data-ttu-id="34fe1-129">These nodes are primary nodes and can be identified by querying the cluster manifest using `Get-ServiceFabricClusterManifest` and finding node entries marked with `IsSeedNode=”true”`.</span><span class="sxs-lookup"><span data-stu-id="34fe1-129">These nodes are primary nodes and can be identified by querying the cluster manifest using `Get-ServiceFabricClusterManifest` and finding node entries marked with `IsSeedNode=”true”`.</span></span> 
> 
> 

<span data-ttu-id="34fe1-130">Even after removing a node, if it shows up as being down in queries and SFX, please note that this is a known defect.</span><span class="sxs-lookup"><span data-stu-id="34fe1-130">Even after removing a node, if it shows up as being down in queries and SFX, please note that this is a known defect.</span></span> <span data-ttu-id="34fe1-131">It will be fixed in an upcoming release.</span><span class="sxs-lookup"><span data-stu-id="34fe1-131">It will be fixed in an upcoming release.</span></span> 


## <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="34fe1-132">Remove node types from your cluster</span><span class="sxs-lookup"><span data-stu-id="34fe1-132">Remove node types from your cluster</span></span>
<span data-ttu-id="34fe1-133">Removing a node type requires extra caution.</span><span class="sxs-lookup"><span data-stu-id="34fe1-133">Removing a node type requires extra caution.</span></span> <span data-ttu-id="34fe1-134">Before removing a node type, please double check if there is any node referencing the node type.</span><span class="sxs-lookup"><span data-stu-id="34fe1-134">Before removing a node type, please double check if there is any node referencing the node type.</span></span>


## <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="34fe1-135">Replace primary nodes of your cluster</span><span class="sxs-lookup"><span data-stu-id="34fe1-135">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="34fe1-136">The replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span><span class="sxs-lookup"><span data-stu-id="34fe1-136">The replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="34fe1-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="34fe1-137">Next steps</span></span>
* [<span data-ttu-id="34fe1-138">Configuration settings for standalone Windows cluster</span><span class="sxs-lookup"><span data-stu-id="34fe1-138">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="34fe1-139">Secure a standalone cluster on Windows using X509 certificates</span><span class="sxs-lookup"><span data-stu-id="34fe1-139">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="34fe1-140">Create a standalone Service Fabric cluster with Azure VMs running Windows</span><span class="sxs-lookup"><span data-stu-id="34fe1-140">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

