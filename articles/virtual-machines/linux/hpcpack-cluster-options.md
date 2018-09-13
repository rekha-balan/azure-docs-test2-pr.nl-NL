---
title: Linux HPC Pack cluster options in Azure | Microsoft Docs
description: Learn about options with Microsoft HPC Pack to create and manage a Linux high performance computing (HPC) cluster in the Azure cloud
services: virtual-machines-linux,cloud-services
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 05/14/2018
ms.author: danlep
ms.openlocfilehash: 9bb2219a9b28a1e783739818b561960d53854cfa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804237"
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-cluster-for-linux-hpc-workloads-in-azure"></a><span data-ttu-id="3f3d1-103">Options with HPC Pack to create and manage a cluster for Linux HPC workloads in Azure</span><span class="sxs-lookup"><span data-stu-id="3f3d1-103">Options with HPC Pack to create and manage a cluster for Linux HPC workloads in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="3f3d1-104">This article focuses on Azure options to use HPC Pack to run Linux workloads.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-104">This article focuses on Azure options to use HPC Pack to run Linux workloads.</span></span> <span data-ttu-id="3f3d1-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3f3d1-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="hpc-pack-cluster-in-azure-vms-and-vm-scale-sets"></a><span data-ttu-id="3f3d1-106">HPC Pack cluster in Azure VMs and VM scale sets</span><span class="sxs-lookup"><span data-stu-id="3f3d1-106">HPC Pack cluster in Azure VMs and VM scale sets</span></span>
### <a name="azure-resource-manager-templates"></a><span data-ttu-id="3f3d1-107">Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="3f3d1-107">Azure Resource Manager templates</span></span>
* <span data-ttu-id="3f3d1-108">(GitHub) [HPC Pack 2016 Update 1 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="3f3d1-108">(GitHub) [HPC Pack 2016 Update 1 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="3f3d1-109">(GitHub) [HPC Pack 2012 R2 cluster templates](https://github.com/MsHpcPack/HPCPack2012R2)</span><span class="sxs-lookup"><span data-stu-id="3f3d1-109">(GitHub) [HPC Pack 2012 R2 cluster templates](https://github.com/MsHpcPack/HPCPack2012R2)</span></span>
* <span data-ttu-id="3f3d1-110">(Quickstart) [Create an HPC Pack 2012 R2 cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="3f3d1-110">(Quickstart) [Create an HPC Pack 2012 R2 cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="3f3d1-111">Azure VM images</span><span class="sxs-lookup"><span data-stu-id="3f3d1-111">Azure VM images</span></span>
<span data-ttu-id="3f3d1-112">Browse [HPC Pack images in the Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?page=1&search=%22HPC%20%20Pack%22) if you want to build your own HPC Pack cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-112">Browse [HPC Pack images in the Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?page=1&search=%22HPC%20%20Pack%22) if you want to build your own HPC Pack cluster in Azure.</span></span>

## <a name="hpc-pack-2012-r2-cluster-in-classic-deployment-model"></a><span data-ttu-id="3f3d1-113">HPC Pack 2012 R2 cluster in classic deployment model</span><span class="sxs-lookup"><span data-stu-id="3f3d1-113">HPC Pack 2012 R2 cluster in classic deployment model</span></span>
* [<span data-ttu-id="3f3d1-114">Create a Linux HPC cluster with the HPC Pack IaaS deployment script</span><span class="sxs-lookup"><span data-stu-id="3f3d1-114">Create a Linux HPC cluster with the HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="3f3d1-115">Set up a Linux RDMA cluster to run MPI applications</span><span class="sxs-lookup"><span data-stu-id="3f3d1-115">Set up a Linux RDMA cluster to run MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="3f3d1-116">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="3f3d1-116">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="3f3d1-117">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span><span class="sxs-lookup"><span data-stu-id="3f3d1-117">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="3f3d1-118">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="3f3d1-118">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="3f3d1-119">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="3f3d1-119">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="job-submisssion"></a><span data-ttu-id="3f3d1-120">Job submisssion</span><span class="sxs-lookup"><span data-stu-id="3f3d1-120">Job submisssion</span></span>
* [<span data-ttu-id="3f3d1-121">Submit jobs to an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="3f3d1-121">Submit jobs to an HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)




