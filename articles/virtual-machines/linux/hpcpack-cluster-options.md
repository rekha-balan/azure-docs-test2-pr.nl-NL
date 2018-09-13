---
title: Linux HPC Pack cluster options in the cloud | Microsoft Docs
description: Learn about options with Microsoft HPC Pack to create and manage a Linux high performance computing (HPC) cluster in the Azure cloud
services: virtual-machines-linux,cloud-services
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: eb1effae3f512d53da3acb168071161b8b756aa4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661007"
---
# <a name="options-with-hpc-pack-to-create-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="80487-103">Options with HPC Pack to create and manage an HPC cluster in Azure for Linux workloads</span><span class="sxs-lookup"><span data-stu-id="80487-103">Options with HPC Pack to create and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="80487-104">This article focuses on options to use HPC Pack to run Linux workloads.</span><span class="sxs-lookup"><span data-stu-id="80487-104">This article focuses on options to use HPC Pack to run Linux workloads.</span></span> <span data-ttu-id="80487-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80487-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="80487-106">Run an HPC Pack cluster in Azure VMs</span><span class="sxs-lookup"><span data-stu-id="80487-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="80487-107">Azure templates</span><span class="sxs-lookup"><span data-stu-id="80487-107">Azure templates</span></span>
* <span data-ttu-id="80487-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="80487-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="80487-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="80487-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="80487-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="80487-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="80487-111">PowerShell deployment script</span><span class="sxs-lookup"><span data-stu-id="80487-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="80487-112">Create a Linux HPC cluster with the HPC Pack IaaS deployment script</span><span class="sxs-lookup"><span data-stu-id="80487-112">Create a Linux HPC cluster with the HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="80487-113">Tutorials</span><span class="sxs-lookup"><span data-stu-id="80487-113">Tutorials</span></span>
* [<span data-ttu-id="80487-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="80487-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="80487-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span><span class="sxs-lookup"><span data-stu-id="80487-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="80487-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="80487-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="80487-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="80487-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="80487-118">Cluster management</span><span class="sxs-lookup"><span data-stu-id="80487-118">Cluster management</span></span>
* [<span data-ttu-id="80487-119">Submit jobs to an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="80487-119">Submit jobs to an HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="80487-120">Job management in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="80487-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="80487-121">Create RDMA clusters for MPI workloads</span><span class="sxs-lookup"><span data-stu-id="80487-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="80487-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="80487-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="80487-123">Set up a Linux RDMA cluster to run MPI applications</span><span class="sxs-lookup"><span data-stu-id="80487-123">Set up a Linux RDMA cluster to run MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

