---
title: Azure N-series driver setup for Windows | Microsoft Docs
description: How to set up NVIDIA GPU drivers for N-series VMs running Windows in Azure
services: virtual-machines-windows
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37079a77fae27c0784b56c11b84784875d3f511e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670769"
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="dfeb1-103">Set up GPU drivers for N-series VMs running Windows Server</span><span class="sxs-lookup"><span data-stu-id="dfeb1-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="dfeb1-104">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-104">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="dfeb1-105">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfeb1-105">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="dfeb1-106">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfeb1-106">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="dfeb1-107">See also [General considerations for N-series VMs](#general-considerations-for-n-series-vms).</span><span class="sxs-lookup"><span data-stu-id="dfeb1-107">See also [General considerations for N-series VMs](#general-considerations-for-n-series-vms).</span></span>



## <a name="supported-gpu-drivers"></a><span data-ttu-id="dfeb1-108">Supported GPU drivers</span><span class="sxs-lookup"><span data-stu-id="dfeb1-108">Supported GPU drivers</span></span>

<span data-ttu-id="dfeb1-109">Connect by Remote Desktop to each N-series VM.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-109">Connect by Remote Desktop to each N-series VM.</span></span> <span data-ttu-id="dfeb1-110">Download, extract, and install the supported driver for your Windows operating system.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-110">Download, extract, and install the supported driver for your Windows operating system.</span></span> 

### <a name="nvidia-tesla-drivers-for-nc-vms-tesla-k80"></a><span data-ttu-id="dfeb1-111">NVIDIA Tesla drivers for NC VMs (Tesla K80)</span><span class="sxs-lookup"><span data-stu-id="dfeb1-111">NVIDIA Tesla drivers for NC VMs (Tesla K80)</span></span>



| <span data-ttu-id="dfeb1-112">OS</span><span class="sxs-lookup"><span data-stu-id="dfeb1-112">OS</span></span> | <span data-ttu-id="dfeb1-113">Driver version</span><span class="sxs-lookup"><span data-stu-id="dfeb1-113">Driver version</span></span> |
| -------- |------------- |
| <span data-ttu-id="dfeb1-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="dfeb1-114">Windows Server 2016</span></span> | <span data-ttu-id="dfeb1-115">[376.84](http://us.download.nvidia.com/Windows/Quadro_Certified/376.84/376.84-tesla-desktop-winserver2016-international-whql.exe) (.exe)</span><span class="sxs-lookup"><span data-stu-id="dfeb1-115">[376.84](http://us.download.nvidia.com/Windows/Quadro_Certified/376.84/376.84-tesla-desktop-winserver2016-international-whql.exe) (.exe)</span></span> |
| <span data-ttu-id="dfeb1-116">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="dfeb1-116">Windows Server 2012 R2</span></span> | <span data-ttu-id="dfeb1-117">[376.84](http://us.download.nvidia.com/Windows/Quadro_Certified/376.84/376.84-tesla-desktop-winserver2008-2012r2-64bit-international-whql.exe) (.exe)</span><span class="sxs-lookup"><span data-stu-id="dfeb1-117">[376.84](http://us.download.nvidia.com/Windows/Quadro_Certified/376.84/376.84-tesla-desktop-winserver2008-2012r2-64bit-international-whql.exe) (.exe)</span></span> |

> [!NOTE]
> <span data-ttu-id="dfeb1-118">Tesla driver download links provided here are current at time of publication.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-118">Tesla driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="dfeb1-119">For the latest drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-119">For the latest drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

### <a name="nvidia-grid-drivers-for-nv-vms-tesla-m60"></a><span data-ttu-id="dfeb1-120">NVIDIA GRID drivers for NV VMs (Tesla M60)</span><span class="sxs-lookup"><span data-stu-id="dfeb1-120">NVIDIA GRID drivers for NV VMs (Tesla M60)</span></span>

| <span data-ttu-id="dfeb1-121">OS</span><span class="sxs-lookup"><span data-stu-id="dfeb1-121">OS</span></span> | <span data-ttu-id="dfeb1-122">Driver version</span><span class="sxs-lookup"><span data-stu-id="dfeb1-122">Driver version</span></span> |
| -------- |------------- |
| <span data-ttu-id="dfeb1-123">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="dfeb1-123">Windows Server 2016</span></span> | <span data-ttu-id="dfeb1-124">[369.95](https://go.microsoft.com/fwlink/?linkid=836843) (.zip)</span><span class="sxs-lookup"><span data-stu-id="dfeb1-124">[369.95](https://go.microsoft.com/fwlink/?linkid=836843) (.zip)</span></span> |
| <span data-ttu-id="dfeb1-125">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="dfeb1-125">Windows Server 2012 R2</span></span> | <span data-ttu-id="dfeb1-126">[369.95](https://go.microsoft.com/fwlink/?linkid=836844) (.zip)</span><span class="sxs-lookup"><span data-stu-id="dfeb1-126">[369.95](https://go.microsoft.com/fwlink/?linkid=836844) (.zip)</span></span>  |



## <a name="verify-gpu-driver-installation"></a><span data-ttu-id="dfeb1-127">Verify GPU driver installation</span><span class="sxs-lookup"><span data-stu-id="dfeb1-127">Verify GPU driver installation</span></span>

<span data-ttu-id="dfeb1-128">On Azure NV VMs, a restart is required after driver installation.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-128">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="dfeb1-129">On NC VMs, a restart is not required.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-129">On NC VMs, a restart is not required.</span></span>

<span data-ttu-id="dfeb1-130">You can verify driver installation in Device Manager.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-130">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="dfeb1-131">The following example shows successful configuration of the Tesla K80 card on an Azure NC VM.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-131">The following example shows successful configuration of the Tesla K80 card on an Azure NC VM.</span></span>

![GPU driver properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/n-series-driver-setup/gpu_driver_properties.png)

<span data-ttu-id="dfeb1-133">To query the GPU device state, run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-133">To query the GPU device state, run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

![NVIDIA device status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="dfeb1-135">RDMA network for NC24r VMs</span><span class="sxs-lookup"><span data-stu-id="dfeb1-135">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="dfeb1-136">RDMA network connectivity can be enabled on NC24r VMs deployed in the same availability set.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-136">RDMA network connectivity can be enabled on NC24r VMs deployed in the same availability set.</span></span> <span data-ttu-id="dfeb1-137">The HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-137">The HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="dfeb1-138">To add the VM extension to an NC24r VM, use [Azure PowerShell](/powershell/azureps-cmdlets-docs) cmdlets for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-138">To add the VM extension to an NC24r VM, use [Azure PowerShell](/powershell/azureps-cmdlets-docs) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="dfeb1-139">Currently, only Windows Server 2012 R2 supports the RDMA network on NC24r VMs.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-139">Currently, only Windows Server 2012 R2 supports the RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="dfeb1-140">To install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in the West US region:</span><span class="sxs-lookup"><span data-stu-id="dfeb1-140">To install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in the West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="dfeb1-141">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfeb1-141">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="dfeb1-142">The RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="dfeb1-142">The RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

## <a name="next-steps"></a><span data-ttu-id="dfeb1-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="dfeb1-143">Next steps</span></span>

* <span data-ttu-id="dfeb1-144">For more information about the NVIDIA GPUs on the N-series VMs, see:</span><span class="sxs-lookup"><span data-stu-id="dfeb1-144">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="dfeb1-145">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span><span class="sxs-lookup"><span data-stu-id="dfeb1-145">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="dfeb1-146">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span><span class="sxs-lookup"><span data-stu-id="dfeb1-146">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="dfeb1-147">Developers building GPU-accelerated applications for the NVIDIA Tesla GPUs can also download and install the CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="dfeb1-147">Developers building GPU-accelerated applications for the NVIDIA Tesla GPUs can also download and install the CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="dfeb1-148">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="dfeb1-148">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>




