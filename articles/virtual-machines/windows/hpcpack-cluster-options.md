---
title: Windows HPC Pack cluster options in the cloud | Microsoft Docs
description: Learn about options with Microsoft HPC Pack to create and manage a Windows high performance computing (HPC) cluster in the Azure cloud
services: virtual-machines-windows,cloud-services,batch
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: fbe11f664b57b2a9aa4bf0d50f4d6169a8c6ebd2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551837"
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="85f9b-103">Options with HPC Pack to create and manage a Windows HPC cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="85f9b-103">Options with HPC Pack to create and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="85f9b-104">This article focuses on options to create HPC Pack clusters to run Windows workloads.</span><span class="sxs-lookup"><span data-stu-id="85f9b-104">This article focuses on options to create HPC Pack clusters to run Windows workloads.</span></span> <span data-ttu-id="85f9b-105">There are also options for creating HPC Pack clusters to run [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="85f9b-105">There are also options for creating HPC Pack clusters to run [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="85f9b-106">Run an HPC Pack cluster in Azure VMs</span><span class="sxs-lookup"><span data-stu-id="85f9b-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="85f9b-107">Azure templates</span><span class="sxs-lookup"><span data-stu-id="85f9b-107">Azure templates</span></span>
* <span data-ttu-id="85f9b-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="85f9b-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="85f9b-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="85f9b-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="85f9b-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="85f9b-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="85f9b-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="85f9b-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="85f9b-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="85f9b-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="85f9b-113">Azure VM images</span><span class="sxs-lookup"><span data-stu-id="85f9b-113">Azure VM images</span></span>
* [<span data-ttu-id="85f9b-114">HPC Pack 2016 head node on Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="85f9b-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="85f9b-115">HPC Pack 2016 compute node on Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="85f9b-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="85f9b-116">HPC Pack 2016 head node on Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="85f9b-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="85f9b-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="85f9b-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="85f9b-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="85f9b-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="85f9b-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="85f9b-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="85f9b-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="85f9b-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="85f9b-121">PowerShell deployment script</span><span class="sxs-lookup"><span data-stu-id="85f9b-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="85f9b-122">Create an HPC cluster with the HPC Pack IaaS deployment script</span><span class="sxs-lookup"><span data-stu-id="85f9b-122">Create an HPC cluster with the HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="85f9b-123">Tutorials</span><span class="sxs-lookup"><span data-stu-id="85f9b-123">Tutorials</span></span>
* [<span data-ttu-id="85f9b-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="85f9b-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="85f9b-125">Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads</span><span class="sxs-lookup"><span data-stu-id="85f9b-125">Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a><span data-ttu-id="85f9b-126">Manual deployment with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="85f9b-126">Manual deployment with the Azure portal</span></span>
* [<span data-ttu-id="85f9b-127">Set up the head node of an HPC Pack cluster in an Azure VM</span><span class="sxs-lookup"><span data-stu-id="85f9b-127">Set up the head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="85f9b-128">Cluster management</span><span class="sxs-lookup"><span data-stu-id="85f9b-128">Cluster management</span></span>
* [<span data-ttu-id="85f9b-129">Manage compute nodes in an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="85f9b-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="85f9b-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span><span class="sxs-lookup"><span data-stu-id="85f9b-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="85f9b-131">Submit jobs to an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="85f9b-131">Submit jobs to an HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="85f9b-132">Job management in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="85f9b-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="85f9b-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85f9b-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-to-an-hpc-pack-cluster"></a><span data-ttu-id="85f9b-134">Add worker role nodes to an HPC Pack cluster</span><span class="sxs-lookup"><span data-stu-id="85f9b-134">Add worker role nodes to an HPC Pack cluster</span></span>
* [<span data-ttu-id="85f9b-135">Burst to Azure worker instances with HPC Pack</span><span class="sxs-lookup"><span data-stu-id="85f9b-135">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="85f9b-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="85f9b-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="85f9b-137">Add Azure "burst" nodes to an HPC Pack head node in Azure</span><span class="sxs-lookup"><span data-stu-id="85f9b-137">Add Azure "burst" nodes to an HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="85f9b-138">Integrate with Azure Batch</span><span class="sxs-lookup"><span data-stu-id="85f9b-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="85f9b-139">Burst to Azure Batch with HPC Pack</span><span class="sxs-lookup"><span data-stu-id="85f9b-139">Burst to Azure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="85f9b-140">Create RDMA clusters for MPI workloads</span><span class="sxs-lookup"><span data-stu-id="85f9b-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="85f9b-141">Set up a Windows RDMA cluster with HPC Pack to run MPI applications</span><span class="sxs-lookup"><span data-stu-id="85f9b-141">Set up a Windows RDMA cluster with HPC Pack to run MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

