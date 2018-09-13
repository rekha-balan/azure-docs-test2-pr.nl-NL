---
title: About compute-intensive VMs with Linux | Microsoft Docs
description: Get background information and considerations for using the H-series and A8, A9, A10, and A11 compute-intensive sizes for Linux VMs
services: virtual-machines-linux
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8512f65c3d0b9acbea034d23ba571d644545b2d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548859"
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="fe2c4-103">About H-series and compute-intensive A-series VMs for Linux</span><span class="sxs-lookup"><span data-stu-id="fe2c4-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="fe2c4-104">Here is background information and some considerations for using the newer Azure H-series and the earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-104">Here is background information and some considerations for using the newer Azure H-series and the earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="fe2c4-105">This article focuses on using these sizes for Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="fe2c4-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe2c4-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="fe2c4-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe2c4-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a><span data-ttu-id="fe2c4-108">Access to the RDMA network</span><span class="sxs-lookup"><span data-stu-id="fe2c4-108">Access to the RDMA network</span></span>
<span data-ttu-id="fe2c4-109">You can create clusters of RDMA-capable Linux VMs that run one of the following supported Linux HPC distributions and a supported MPI implementation to take advantage of the Azure RDMA network.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-109">You can create clusters of RDMA-capable Linux VMs that run one of the following supported Linux HPC distributions and a supported MPI implementation to take advantage of the Azure RDMA network.</span></span> <span data-ttu-id="fe2c4-110">See [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-110">See [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="fe2c4-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or OpenLogic CentOS-based HPC images in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or OpenLogic CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="fe2c4-112">The following Marketplace images support RDMA connectivity:</span><span class="sxs-lookup"><span data-stu-id="fe2c4-112">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="fe2c4-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="fe2c4-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="fe2c4-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="fe2c4-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="fe2c4-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="fe2c4-116">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-116">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="fe2c4-117">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-117">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="fe2c4-118">**MPI** - Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="fe2c4-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="fe2c4-119">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span><span class="sxs-lookup"><span data-stu-id="fe2c4-119">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="fe2c4-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="fe2c4-121">Install by running the following command:</span><span class="sxs-lookup"><span data-stu-id="fe2c4-121">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="fe2c4-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="fe2c4-123">Additional system configuration is needed to run MPI jobs on clustered VMs.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-123">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="fe2c4-124">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-124">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="fe2c4-125">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe2c4-125">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="fe2c4-126">Considerations for HPC Pack and Linux</span><span class="sxs-lookup"><span data-stu-id="fe2c4-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="fe2c4-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you to use the compute-intensive instances with Linux.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="fe2c4-128">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-128">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="fe2c4-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="fe2c4-130">To get started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe2c4-130">To get started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="fe2c4-131">Network topology considerations</span><span class="sxs-lookup"><span data-stu-id="fe2c4-131">Network topology considerations</span></span>
* <span data-ttu-id="fe2c4-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="fe2c4-133">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-133">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="fe2c4-134">Eth0 is reserved for regular Azure network traffic.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="fe2c4-135">In Azure, IP over InfiniBand (IB) is not supported.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="fe2c4-136">Only RDMA over IB is supported.</span><span class="sxs-lookup"><span data-stu-id="fe2c4-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="fe2c4-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="fe2c4-137">Next steps</span></span>
* <span data-ttu-id="fe2c4-138">For details about availability and pricing of the compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="fe2c4-138">For details about availability and pricing of the compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="fe2c4-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe2c4-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="fe2c4-140">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe2c4-140">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

