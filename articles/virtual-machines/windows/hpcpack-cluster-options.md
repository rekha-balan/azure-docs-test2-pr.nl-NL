---
title: Windows HPC Pack cluster options in Azure | Microsoft Docs
description: Learn about options with Microsoft HPC Pack to create and manage a Windows high performance computing (HPC) cluster in the Azure cloud
services: virtual-machines-windows,cloud-services,batch
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/14/2018
ms.author: danlep
ms.openlocfilehash: 3aba51612ffa06619204051d0a132d53f0b35f6d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830362"
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-cluster-for-windows-hpc-workloads-in-azure"></a><span data-ttu-id="9f59f-103">Options with HPC Pack to create and manage a cluster for Windows HPC workloads in Azure</span><span class="sxs-lookup"><span data-stu-id="9f59f-103">Options with HPC Pack to create and manage a cluster for Windows HPC workloads in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="9f59f-104">This article focuses on Azure options to create HPC Pack clusters to run Windows workloads.</span><span class="sxs-lookup"><span data-stu-id="9f59f-104">This article focuses on Azure options to create HPC Pack clusters to run Windows workloads.</span></span> <span data-ttu-id="9f59f-105">There are also options for creating HPC Pack clusters to run [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f59f-105">There are also options for creating HPC Pack clusters to run [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="hpc-pack-cluster-in-azure-vms-and-vm-scale-sets"></a><span data-ttu-id="9f59f-106">HPC Pack cluster in Azure VMs and VM scale sets</span><span class="sxs-lookup"><span data-stu-id="9f59f-106">HPC Pack cluster in Azure VMs and VM scale sets</span></span>
### <a name="azure-resource-manager-templates"></a><span data-ttu-id="9f59f-107">Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="9f59f-107">Azure Resource Manager templates</span></span>
* <span data-ttu-id="9f59f-108">(GitHub) [HPC Pack 2016 Update 1 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="9f59f-108">(GitHub) [HPC Pack 2016 Update 1 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="9f59f-109">(GitHub) [HPC Pack 2012 R2 cluster templates](https://github.com/MsHpcPack/HPCPack2012R2)</span><span class="sxs-lookup"><span data-stu-id="9f59f-109">(GitHub) [HPC Pack 2012 R2 cluster templates](https://github.com/MsHpcPack/HPCPack2012R2)</span></span>
* <span data-ttu-id="9f59f-110">(Quickstart) [Create an HPC Pack 2012 R2 cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="9f59f-110">(Quickstart) [Create an HPC Pack 2012 R2 cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="9f59f-111">(Quickstart) [Create an HPC Pack 2012 R2 cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="9f59f-111">(Quickstart) [Create an HPC Pack 2012 R2 cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="9f59f-112">Azure VM images</span><span class="sxs-lookup"><span data-stu-id="9f59f-112">Azure VM images</span></span>
<span data-ttu-id="9f59f-113">Browse [HPC Pack images in the Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?page=1&search=%22HPC%20%20Pack%22) if you want to build your own HPC Pack cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="9f59f-113">Browse [HPC Pack images in the Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?page=1&search=%22HPC%20%20Pack%22) if you want to build your own HPC Pack cluster in Azure.</span></span>


### <a name="tutorials"></a><span data-ttu-id="9f59f-114">Tutorials</span><span class="sxs-lookup"><span data-stu-id="9f59f-114">Tutorials</span></span>
* [<span data-ttu-id="9f59f-115">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="9f59f-115">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="9f59f-116">Manage an HPC Pack 2016 cluster in Azure with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f59f-116">Manage an HPC Pack 2016 cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)


## <a name="hpc-pack-2012-r2-cluster-deployment-in-the-classic-deployment-model"></a><span data-ttu-id="9f59f-117">HPC Pack 2012 R2 cluster deployment in the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="9f59f-117">HPC Pack 2012 R2 cluster deployment in the classic deployment model</span></span>
* [<span data-ttu-id="9f59f-118">Create an HPC cluster with the HPC Pack IaaS deployment script</span><span class="sxs-lookup"><span data-stu-id="9f59f-118">Create an HPC cluster with the HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="9f59f-119">Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads</span><span class="sxs-lookup"><span data-stu-id="9f59f-119">Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="9f59f-120">Manage compute nodes in an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="9f59f-120">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="9f59f-121">Grow and shrink Azure compute resources in an HPC Pack cluster</span><span class="sxs-lookup"><span data-stu-id="9f59f-121">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="9f59f-122">Set up a Windows RDMA cluster with HPC Pack to run MPI applications</span><span class="sxs-lookup"><span data-stu-id="9f59f-122">Set up a Windows RDMA cluster with HPC Pack to run MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)


## <a name="burst-to-azure-from-hpc-pack-2012-r2"></a><span data-ttu-id="9f59f-123">Burst to Azure from HPC Pack 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9f59f-123">Burst to Azure from HPC Pack 2012 R2</span></span>
* [<span data-ttu-id="9f59f-124">Burst to Azure Worker Instances with Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="9f59f-124">Burst to Azure Worker Instances with Microsoft HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="9f59f-125">Burst to Azure Batch with HPC Pack</span><span class="sxs-lookup"><span data-stu-id="9f59f-125">Burst to Azure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="9f59f-126">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="9f59f-126">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)

## <a name="job-submission"></a><span data-ttu-id="9f59f-127">Job submission</span><span class="sxs-lookup"><span data-stu-id="9f59f-127">Job submission</span></span>

* [<span data-ttu-id="9f59f-128">Submit jobs to an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="9f59f-128">Submit jobs to an HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)






