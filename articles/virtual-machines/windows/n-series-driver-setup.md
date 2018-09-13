---
title: Azure N-series driver setup for Windows | Microsoft Docs
description: How to set up NVIDIA GPU drivers for N-series VMs running Windows Server or Windows in Azure
services: virtual-machines-windows
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/19/2018
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 204a3c27bd9416a952b3d8f5336d397d9d004e00
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784529"
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows"></a><span data-ttu-id="d1141-103">Set up GPU drivers for N-series VMs running Windows</span><span class="sxs-lookup"><span data-stu-id="d1141-103">Set up GPU drivers for N-series VMs running Windows</span></span> 
<span data-ttu-id="d1141-104">To take advantage of the GPU capabilities of Azure N-series VMs running Windows, NVIDIA GPU drivers must be installed.</span><span class="sxs-lookup"><span data-stu-id="d1141-104">To take advantage of the GPU capabilities of Azure N-series VMs running Windows, NVIDIA GPU drivers must be installed.</span></span> <span data-ttu-id="d1141-105">The [NVIDIA GPU Driver Extension](../extensions/hpccompute-gpu-windows.md) installs appropriate NVIDIA CUDA or GRID drivers on an N-series VM.</span><span class="sxs-lookup"><span data-stu-id="d1141-105">The [NVIDIA GPU Driver Extension](../extensions/hpccompute-gpu-windows.md) installs appropriate NVIDIA CUDA or GRID drivers on an N-series VM.</span></span> <span data-ttu-id="d1141-106">Install or manage the extension using the Azure portal or tools such as Azure PowerShell or Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="d1141-106">Install or manage the extension using the Azure portal or tools such as Azure PowerShell or Azure Resource Manager templates.</span></span> <span data-ttu-id="d1141-107">See the [NVIDIA GPU Driver Extension documentation](../extensions/hpccompute-gpu-windows.md) for supported operating systems and deployment steps.</span><span class="sxs-lookup"><span data-stu-id="d1141-107">See the [NVIDIA GPU Driver Extension documentation](../extensions/hpccompute-gpu-windows.md) for supported operating systems and deployment steps.</span></span>

<span data-ttu-id="d1141-108">If you choose to install GPU drivers manually, this article provides supported operating systems, drivers, and installation and verification steps.</span><span class="sxs-lookup"><span data-stu-id="d1141-108">If you choose to install GPU drivers manually, this article provides supported operating systems, drivers, and installation and verification steps.</span></span> <span data-ttu-id="d1141-109">Manual driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1141-109">Manual driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d1141-110">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1141-110">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]

## <a name="driver-installation"></a><span data-ttu-id="d1141-111">Driver installation</span><span class="sxs-lookup"><span data-stu-id="d1141-111">Driver installation</span></span>

1. <span data-ttu-id="d1141-112">Connect by Remote Desktop to each N-series VM.</span><span class="sxs-lookup"><span data-stu-id="d1141-112">Connect by Remote Desktop to each N-series VM.</span></span>

2. <span data-ttu-id="d1141-113">Download, extract, and install the supported driver for your Windows operating system.</span><span class="sxs-lookup"><span data-stu-id="d1141-113">Download, extract, and install the supported driver for your Windows operating system.</span></span>

<span data-ttu-id="d1141-114">On Azure NV VMs, a restart is required after driver installation.</span><span class="sxs-lookup"><span data-stu-id="d1141-114">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="d1141-115">On NC VMs, a restart is not required.</span><span class="sxs-lookup"><span data-stu-id="d1141-115">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="d1141-116">Verify driver installation</span><span class="sxs-lookup"><span data-stu-id="d1141-116">Verify driver installation</span></span>

<span data-ttu-id="d1141-117">You can verify driver installation in Device Manager.</span><span class="sxs-lookup"><span data-stu-id="d1141-117">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="d1141-118">The following example shows successful configuration of the Tesla K80 card on an Azure NC VM.</span><span class="sxs-lookup"><span data-stu-id="d1141-118">The following example shows successful configuration of the Tesla K80 card on an Azure NC VM.</span></span>

![GPU driver properties](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="d1141-120">To query the GPU device state, run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span><span class="sxs-lookup"><span data-stu-id="d1141-120">To query the GPU device state, run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span>

1. <span data-ttu-id="d1141-121">Open a command prompt and change to the **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span><span class="sxs-lookup"><span data-stu-id="d1141-121">Open a command prompt and change to the **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="d1141-122">Run `nvidia-smi`.</span><span class="sxs-lookup"><span data-stu-id="d1141-122">Run `nvidia-smi`.</span></span> <span data-ttu-id="d1141-123">If the driver is installed you will see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="d1141-123">If the driver is installed you will see output similar to the following.</span></span> <span data-ttu-id="d1141-124">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on the VM.</span><span class="sxs-lookup"><span data-stu-id="d1141-124">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on the VM.</span></span> <span data-ttu-id="d1141-125">Your driver version and GPU details may be different from the ones shown.</span><span class="sxs-lookup"><span data-stu-id="d1141-125">Your driver version and GPU details may be different from the ones shown.</span></span>

![NVIDIA device status](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-connectivity"></a><span data-ttu-id="d1141-127">RDMA network connectivity</span><span class="sxs-lookup"><span data-stu-id="d1141-127">RDMA network connectivity</span></span>

<span data-ttu-id="d1141-128">RDMA network connectivity can be enabled on RDMA-capable N-series VMs such as NC24r deployed in the same availability set or in a single placement group in a VM scale set.</span><span class="sxs-lookup"><span data-stu-id="d1141-128">RDMA network connectivity can be enabled on RDMA-capable N-series VMs such as NC24r deployed in the same availability set or in a single placement group in a VM scale set.</span></span> <span data-ttu-id="d1141-129">The HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span><span class="sxs-lookup"><span data-stu-id="d1141-129">The HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="d1141-130">To add the VM extension to an RDMA-enabled N-series VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d1141-130">To add the VM extension to an RDMA-enabled N-series VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

<span data-ttu-id="d1141-131">To install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in the West US region:</span><span class="sxs-lookup"><span data-stu-id="d1141-131">To install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in the West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="d1141-132">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1141-132">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="d1141-133">The RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="d1141-133">The RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="d1141-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1141-134">Next steps</span></span>

* <span data-ttu-id="d1141-135">Developers building GPU-accelerated applications for the NVIDIA Tesla GPUs can also download and install the latest [CUDA Toolkit](https://developer.nvidia.com/cuda-downloads).</span><span class="sxs-lookup"><span data-stu-id="d1141-135">Developers building GPU-accelerated applications for the NVIDIA Tesla GPUs can also download and install the latest [CUDA Toolkit](https://developer.nvidia.com/cuda-downloads).</span></span> <span data-ttu-id="d1141-136">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="d1141-136">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


