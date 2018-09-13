---
title: How to resize a Linux VM with the Azure CLI 1.0 | Microsoft Docs
description: How to scale up or scale down a Linux virtual machine, by changing the VM size.
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: ''
tags: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1fb2921127852ce974563d0b5a911bea4af8cf61
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564416"
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="f173b-103">Resize a Linux VM with Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f173b-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="f173b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f173b-104">Overview</span></span>

<span data-ttu-id="f173b-105">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="f173b-105">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="f173b-106">In some cases, you must deallocate the VM first.</span><span class="sxs-lookup"><span data-stu-id="f173b-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="f173b-107">This can happen if the new size is not available on the hardware cluster that is hosting the VM.</span><span class="sxs-lookup"><span data-stu-id="f173b-107">This can happen if the new size is not available on the hardware cluster that is hosting the VM.</span></span>

<span data-ttu-id="f173b-108">This article shows how to resize a Linux VM using the [Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="f173b-108">This article shows how to resize a Linux VM using the [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f173b-109">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="f173b-109">CLI versions to complete the task</span></span>
<span data-ttu-id="f173b-110">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="f173b-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="f173b-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="f173b-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f173b-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="f173b-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="f173b-113">Resize a Linux VM</span><span class="sxs-lookup"><span data-stu-id="f173b-113">Resize a Linux VM</span></span>
<span data-ttu-id="f173b-114">To resize a VM, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="f173b-114">To resize a VM, perform the following steps.</span></span>

1. <span data-ttu-id="f173b-115">Run the following CLI command.</span><span class="sxs-lookup"><span data-stu-id="f173b-115">Run the following CLI command.</span></span> <span data-ttu-id="f173b-116">This command lists the VM sizes that are available on the hardware cluster where the VM is hosted.</span><span class="sxs-lookup"><span data-stu-id="f173b-116">This command lists the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="f173b-117">If the desired size is listed, run the following command to resize the VM.</span><span class="sxs-lookup"><span data-stu-id="f173b-117">If the desired size is listed, run the following command to resize the VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="f173b-118">The VM will restart during this process.</span><span class="sxs-lookup"><span data-stu-id="f173b-118">The VM will restart during this process.</span></span> <span data-ttu-id="f173b-119">After the restart, your existing OS and data disks will be remapped.</span><span class="sxs-lookup"><span data-stu-id="f173b-119">After the restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="f173b-120">Anything on the temporary disk will be lost.</span><span class="sxs-lookup"><span data-stu-id="f173b-120">Anything on the temporary disk will be lost.</span></span>
   
    <span data-ttu-id="f173b-121">Use the `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], to log any errors related to startup.</span><span class="sxs-lookup"><span data-stu-id="f173b-121">Use the `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], to log any errors related to startup.</span></span>
3. <span data-ttu-id="f173b-122">Otherwise, if the desired size is not listed, run the following commands to deallocate the VM, resize it, and then restart the VM.</span><span class="sxs-lookup"><span data-stu-id="f173b-122">Otherwise, if the desired size is not listed, run the following commands to deallocate the VM, resize it, and then restart the VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="f173b-123">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span><span class="sxs-lookup"><span data-stu-id="f173b-123">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="f173b-124">The OS and data disks are not affected.</span><span class="sxs-lookup"><span data-stu-id="f173b-124">The OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="f173b-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="f173b-125">Next steps</span></span>
<span data-ttu-id="f173b-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span><span class="sxs-lookup"><span data-stu-id="f173b-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
