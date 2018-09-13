---
title: About compute-intensive VMs with Windows | Microsoft Docs
description: Get background information and considerations for using the Azure H-series and A8, A9, A10, and A11 compute-intensive sizes for Windows VMs and cloud services
services: virtual-machines-windows, cloud-services
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f344747cae0e26089ce1c6585ebada3876255f9a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548870"
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-windows"></a><span data-ttu-id="84fe9-103">About H-series and compute-intensive A-series VMs for Windows</span><span class="sxs-lookup"><span data-stu-id="84fe9-103">About H-series and compute-intensive A-series VMs for Windows</span></span>
<span data-ttu-id="84fe9-104">Here is background information and some considerations for using the newer Azure H-series and the earlier A8, A9, A10, and A11 instances, also known as *compute-intensive* instances.</span><span class="sxs-lookup"><span data-stu-id="84fe9-104">Here is background information and some considerations for using the newer Azure H-series and the earlier A8, A9, A10, and A11 instances, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="84fe9-105">This article focuses on using these instances for Windows VMs.</span><span class="sxs-lookup"><span data-stu-id="84fe9-105">This article focuses on using these instances for Windows VMs.</span></span> <span data-ttu-id="84fe9-106">You can also use them for [Linux VMs](../linux/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84fe9-106">You can also use them for [Linux VMs](../linux/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="84fe9-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84fe9-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a><span data-ttu-id="84fe9-108">Access to the RDMA network</span><span class="sxs-lookup"><span data-stu-id="84fe9-108">Access to the RDMA network</span></span>
<span data-ttu-id="84fe9-109">To access the Azure RDMA network for Windows MPI traffic, RDMA-capable instances must meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="84fe9-109">To access the Azure RDMA network for Windows MPI traffic, RDMA-capable instances must meet the following requirements:</span></span> 

* <span data-ttu-id="84fe9-110">**Operating system**</span><span class="sxs-lookup"><span data-stu-id="84fe9-110">**Operating system**</span></span>
  
  * <span data-ttu-id="84fe9-111">**Virtual machines** - Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="84fe9-111">**Virtual machines** - Windows Server 2012 R2, Windows Server 2012</span></span>
  * <span data-ttu-id="84fe9-112">**Cloud services** - Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 Guest OS family</span><span class="sxs-lookup"><span data-stu-id="84fe9-112">**Cloud services** - Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 Guest OS family</span></span>

    > [!NOTE]
    > <span data-ttu-id="84fe9-113">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span><span class="sxs-lookup"><span data-stu-id="84fe9-113">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
    >
    
* <span data-ttu-id="84fe9-114">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="84fe9-114">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="84fe9-115">Supported MPI implementations use the Microsoft Network Direct interface to communicate between instances.</span><span class="sxs-lookup"><span data-stu-id="84fe9-115">Supported MPI implementations use the Microsoft Network Direct interface to communicate between instances.</span></span> 
* <span data-ttu-id="84fe9-116">**HpcVmDrivers VM extension** - On RDMA-capable VMs, the HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span><span class="sxs-lookup"><span data-stu-id="84fe9-116">**HpcVmDrivers VM extension** - On RDMA-capable VMs, the HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="84fe9-117">(In certain deployments of A8 and A9 instances, the HpcVmDrivers extension is added automatically.) If you need to add the VM extension to a VM, you can use [Azure PowerShell](/powershell/azureps-cmdlets-docs) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="84fe9-117">(In certain deployments of A8 and A9 instances, the HpcVmDrivers extension is added automatically.) If you need to add the VM extension to a VM, you can use [Azure PowerShell](/powershell/azureps-cmdlets-docs) cmdlets.</span></span> 

  
  <span data-ttu-id="84fe9-118">For example, to install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM deployed in the Resource Manager deployment model:</span><span class="sxs-lookup"><span data-stu-id="84fe9-118">For example, to install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM deployed in the Resource Manager deployment model:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="84fe9-119">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84fe9-119">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="84fe9-120">You can also work with extensions for VMs deployed in the [classic deployment model](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="84fe9-120">You can also work with extensions for VMs deployed in the [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="considerations-for-hpc-pack-and-windows"></a><span data-ttu-id="84fe9-121">Considerations for HPC Pack and Windows</span><span class="sxs-lookup"><span data-stu-id="84fe9-121">Considerations for HPC Pack and Windows</span></span>
<span data-ttu-id="84fe9-122">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is not required for you to use the compute-intensive instances with Windows Server.</span><span class="sxs-lookup"><span data-stu-id="84fe9-122">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is not required for you to use the compute-intensive instances with Windows Server.</span></span> <span data-ttu-id="84fe9-123">However, it is one option for you to create a compute cluster in Azure to run Windows-based MPI applications and other HPC workloads.</span><span class="sxs-lookup"><span data-stu-id="84fe9-123">However, it is one option for you to create a compute cluster in Azure to run Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="84fe9-124">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that can use the Azure RDMA network when deployed on RDMA-capable VMs.</span><span class="sxs-lookup"><span data-stu-id="84fe9-124">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that can use the Azure RDMA network when deployed on RDMA-capable VMs.</span></span>

<span data-ttu-id="84fe9-125">For more information and checklists to use the compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84fe9-125">For more information and checklists to use the compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="84fe9-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="84fe9-126">Next steps</span></span>
* <span data-ttu-id="84fe9-127">For details about availability and pricing of the compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows) and [Cloud Services pricing](https://azure.microsoft.com/pricing/details/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="84fe9-127">For details about availability and pricing of the compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows) and [Cloud Services pricing](https://azure.microsoft.com/pricing/details/cloud-services/).</span></span>
* <span data-ttu-id="84fe9-128">For storage capacities and disk details, see [Sizes for virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84fe9-128">For storage capacities and disk details, see [Sizes for virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="84fe9-129">To get started deploying and using compute-intensive instances with HPC Pack on Windows, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84fe9-129">To get started deploying and using compute-intensive instances with HPC Pack on Windows, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
* <span data-ttu-id="84fe9-130">For information about using compute-intensive instances to run MPI applications with Azure Batch, see [Use multi-instance tasks to run Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="84fe9-130">For information about using compute-intensive instances to run MPI applications with Azure Batch, see [Use multi-instance tasks to run Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

