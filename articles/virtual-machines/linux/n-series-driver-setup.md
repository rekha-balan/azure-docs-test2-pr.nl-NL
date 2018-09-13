---
title: Azure N-series driver setup for Linux | Microsoft Docs
description: How to set up NVIDIA GPU drivers for N-series VMs running Linux in Azure
services: virtual-machines-linux
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8a70c88109b0b629e4104fe5ff039e9f8aa705b1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671301"
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-linux"></a><span data-ttu-id="b48b3-103">Set up GPU drivers for N-series VMs running Linux</span><span class="sxs-lookup"><span data-stu-id="b48b3-103">Set up GPU drivers for N-series VMs running Linux</span></span>

<span data-ttu-id="b48b3-104">To take advantage of the GPU capabilities of Azure N-series VMs running a supported Linux distribution, you must install NVIDIA graphics drivers on each VM after deployment.</span><span class="sxs-lookup"><span data-stu-id="b48b3-104">To take advantage of the GPU capabilities of Azure N-series VMs running a supported Linux distribution, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="b48b3-105">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b48b3-105">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="b48b3-106">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="b48b3-106">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span>
> 

<span data-ttu-id="b48b3-107">For N-series VM specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b48b3-107">For N-series VM specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b48b3-108">See also [General considerations for N-series VMs](#general-considerations-for-n-series-vms).</span><span class="sxs-lookup"><span data-stu-id="b48b3-108">See also [General considerations for N-series VMs](#general-considerations-for-n-series-vms).</span></span>



## <a name="install-nvidia-cuda-drivers"></a><span data-ttu-id="b48b3-109">Install NVIDIA CUDA drivers</span><span class="sxs-lookup"><span data-stu-id="b48b3-109">Install NVIDIA CUDA drivers</span></span>

<span data-ttu-id="b48b3-110">Here are steps to install NVIDIA drivers on Linux NC VMs from the NVIDIA CUDA Toolkit 8.0.</span><span class="sxs-lookup"><span data-stu-id="b48b3-110">Here are steps to install NVIDIA drivers on Linux NC VMs from the NVIDIA CUDA Toolkit 8.0.</span></span> <span data-ttu-id="b48b3-111">C and C++ developers can optionally install the full Toolkit to build GPU-accelerated applications.</span><span class="sxs-lookup"><span data-stu-id="b48b3-111">C and C++ developers can optionally install the full Toolkit to build GPU-accelerated applications.</span></span> <span data-ttu-id="b48b3-112">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="b48b3-112">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="b48b3-113">Driver download links provided here are current at time of publication.</span><span class="sxs-lookup"><span data-stu-id="b48b3-113">Driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="b48b3-114">For the latest drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span><span class="sxs-lookup"><span data-stu-id="b48b3-114">For the latest drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span></span>

<span data-ttu-id="b48b3-115">To install CUDA Toolkit, make an SSH connection to each VM.</span><span class="sxs-lookup"><span data-stu-id="b48b3-115">To install CUDA Toolkit, make an SSH connection to each VM.</span></span> <span data-ttu-id="b48b3-116">To verify that the system has a CUDA-capable GPU, run the following command:</span><span class="sxs-lookup"><span data-stu-id="b48b3-116">To verify that the system has a CUDA-capable GPU, run the following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="b48b3-117">You will see output similar to the following example (showing an NVIDIA Tesla K80 card):</span><span class="sxs-lookup"><span data-stu-id="b48b3-117">You will see output similar to the following example (showing an NVIDIA Tesla K80 card):</span></span>

![lspci command output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/n-series-driver-setup/lspci.png)

<span data-ttu-id="b48b3-119">Then run commands specific for your distribution.</span><span class="sxs-lookup"><span data-stu-id="b48b3-119">Then run commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="b48b3-120">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="b48b3-120">Ubuntu 16.04 LTS</span></span>

```bash
CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

sudo dpkg -i /tmp/${CUDA_REPO_PKG}

rm -f /tmp/${CUDA_REPO_PKG}

sudo apt-get update

sudo apt-get install cuda-drivers

```
<span data-ttu-id="b48b3-121">The installation can take several minutes.</span><span class="sxs-lookup"><span data-stu-id="b48b3-121">The installation can take several minutes.</span></span>

<span data-ttu-id="b48b3-122">To optionally install the complete CUDA toolkit, type:</span><span class="sxs-lookup"><span data-stu-id="b48b3-122">To optionally install the complete CUDA toolkit, type:</span></span>

```bash
sudo apt-get install cuda
```

<span data-ttu-id="b48b3-123">Reboot the VM and proceed to verify the installation.</span><span class="sxs-lookup"><span data-stu-id="b48b3-123">Reboot the VM and proceed to verify the installation.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="b48b3-124">Verify driver installation</span><span class="sxs-lookup"><span data-stu-id="b48b3-124">Verify driver installation</span></span>


<span data-ttu-id="b48b3-125">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span><span class="sxs-lookup"><span data-stu-id="b48b3-125">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

![NVIDIA device status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/n-series-driver-setup/smi.png)

## <a name="cuda-driver-updates"></a><span data-ttu-id="b48b3-127">CUDA driver updates</span><span class="sxs-lookup"><span data-stu-id="b48b3-127">CUDA driver updates</span></span>

<span data-ttu-id="b48b3-128">We recommend that you periodically update CUDA drivers after deployment.</span><span class="sxs-lookup"><span data-stu-id="b48b3-128">We recommend that you periodically update CUDA drivers after deployment.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="b48b3-129">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="b48b3-129">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers
```

<span data-ttu-id="b48b3-130">After the update completes, restart the VM.</span><span class="sxs-lookup"><span data-stu-id="b48b3-130">After the update completes, restart the VM.</span></span>


[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="b48b3-131">We don't recommend installing X server or other systems that use the nouveau driver on Ubuntu NC VMs.</span><span class="sxs-lookup"><span data-stu-id="b48b3-131">We don't recommend installing X server or other systems that use the nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="b48b3-132">Before installing NVIDIA GPU drivers, you need to disable the nouveau driver.</span><span class="sxs-lookup"><span data-stu-id="b48b3-132">Before installing NVIDIA GPU drivers, you need to disable the nouveau driver.</span></span>  

* <span data-ttu-id="b48b3-133">If you want to capture an image of a Linux VM on which you installed NVIDIA drivers, see [How to generalize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b48b3-133">If you want to capture an image of a Linux VM on which you installed NVIDIA drivers, see [How to generalize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b48b3-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="b48b3-134">Next steps</span></span>

* <span data-ttu-id="b48b3-135">For more information about the NVIDIA GPUs on the N-series VMs, see:</span><span class="sxs-lookup"><span data-stu-id="b48b3-135">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="b48b3-136">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span><span class="sxs-lookup"><span data-stu-id="b48b3-136">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="b48b3-137">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span><span class="sxs-lookup"><span data-stu-id="b48b3-137">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>



