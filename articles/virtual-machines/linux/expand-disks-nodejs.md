---
title: Expand OS disk on Linux VM with the Azure CLI 1.0 | Microsoft Docs
description: Learn how to expand the operating system (OS) virtual disk on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/10/2017
ms.author: iainfou
ms.openlocfilehash: 200a3e5a07d55a2f153b462f0b758542142f3f2e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555702"
---
# <a name="expand-os-disk-on-a-linux-vm-using-the-azure-cli-with-the-azure-cli-10"></a><span data-ttu-id="e2d41-103">Expand OS disk on a Linux VM using the Azure CLI with the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e2d41-103">Expand OS disk on a Linux VM using the Azure CLI with the Azure CLI 1.0</span></span>
<span data-ttu-id="e2d41-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="e2d41-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="e2d41-105">You can [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to provide for additional storage space, but you may also wish to expand the OS disk.</span><span class="sxs-lookup"><span data-stu-id="e2d41-105">You can [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to provide for additional storage space, but you may also wish to expand the OS disk.</span></span> <span data-ttu-id="e2d41-106">This article details how to expand the OS disk for a Linux VM using unmanaged disks with the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e2d41-106">This article details how to expand the OS disk for a Linux VM using unmanaged disks with the Azure CLI 1.0</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e2d41-107">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="e2d41-107">CLI versions to complete the task</span></span>
<span data-ttu-id="e2d41-108">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="e2d41-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="e2d41-109">[Azure CLI 1.0](#prerequisites) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="e2d41-109">[Azure CLI 1.0](#prerequisites) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e2d41-110">[Azure CLI 2.0](expand-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="e2d41-110">[Azure CLI 2.0](expand-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2d41-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e2d41-111">Prerequisites</span></span>
<span data-ttu-id="e2d41-112">You need the [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in to an [Azure account](https://azure.microsoft.com/pricing/free-trial/) using the Resource Manager mode as follows:</span><span class="sxs-lookup"><span data-stu-id="e2d41-112">You need the [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in to an [Azure account](https://azure.microsoft.com/pricing/free-trial/) using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e2d41-113">In the following samples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="e2d41-113">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e2d41-114">Example parameter names include `myResourceGroup` and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e2d41-114">Example parameter names include `myResourceGroup` and `myVM`.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="e2d41-115">Expand OS disk</span><span class="sxs-lookup"><span data-stu-id="e2d41-115">Expand OS disk</span></span>

1. <span data-ttu-id="e2d41-116">Operations on virtual hard disks cannot be performed with the VM running.</span><span class="sxs-lookup"><span data-stu-id="e2d41-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="e2d41-117">The following example stops and deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e2d41-117">The following example stops and deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="e2d41-118">`azure vm stop` does not release the compute resources.</span><span class="sxs-lookup"><span data-stu-id="e2d41-118">`azure vm stop` does not release the compute resources.</span></span> <span data-ttu-id="e2d41-119">To release compute resources, use `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="e2d41-119">To release compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="e2d41-120">The VM must be deallocated to expand the virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="e2d41-120">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="e2d41-121">Update the size of the OS unmanaged disk using the `azure vm set` command.</span><span class="sxs-lookup"><span data-stu-id="e2d41-121">Update the size of the OS unmanaged disk using the `azure vm set` command.</span></span> <span data-ttu-id="e2d41-122">The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to be `50` GB:</span><span class="sxs-lookup"><span data-stu-id="e2d41-122">The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to be `50` GB:</span></span>

    ```azurecli
    azure vm set --resource-group myResourceGroup --name myVM --new-os-disk-size 50
    ```

3. <span data-ttu-id="e2d41-123">Start your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="e2d41-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="e2d41-124">SSH to your VM with the appropriate credentials.</span><span class="sxs-lookup"><span data-stu-id="e2d41-124">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="e2d41-125">To verify the OS disk has been resized, use `df -h`.</span><span class="sxs-lookup"><span data-stu-id="e2d41-125">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="e2d41-126">The following example output shows the primary partition (`/dev/sda1`) is now 50 GB:</span><span class="sxs-lookup"><span data-stu-id="e2d41-126">The following example output shows the primary partition (`/dev/sda1`) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="e2d41-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2d41-127">Next steps</span></span>
<span data-ttu-id="e2d41-128">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2d41-128">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e2d41-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2d41-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
