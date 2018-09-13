---
title: Expand virtual hard disks on Linux VM in Azure | Microsoft Docs
description: Learn how to expand virtual hard disks on a Linux VM with the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/22/2017
ms.author: iainfou
ms.openlocfilehash: 98f110c4af2be7aa2164b46670fa5c21f8339b16
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549065"
---
# <a name="how-to-expand-virtual-hard-disks-on-a-linux-vm-with-the-azure-cli-20"></a><span data-ttu-id="49c5f-103">How to expand virtual hard disks on a Linux VM with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="49c5f-103">How to expand virtual hard disks on a Linux VM with the Azure CLI 2.0</span></span>
<span data-ttu-id="49c5f-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="49c5f-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="49c5f-105">You can [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to provide for additional storage space, but you may also wish to expand the OS disk or existing data disk.</span><span class="sxs-lookup"><span data-stu-id="49c5f-105">You can [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to provide for additional storage space, but you may also wish to expand the OS disk or existing data disk.</span></span> <span data-ttu-id="49c5f-106">This article details how to expand managed disks for a Linux VM with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="49c5f-106">This article details how to expand managed disks for a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="49c5f-107">You can also expand the unmanaged OS disk with the [Azure CLI 1.0](expand-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49c5f-107">You can also expand the unmanaged OS disk with the [Azure CLI 1.0](expand-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="expand-managed-disk"></a><span data-ttu-id="49c5f-108">Expand managed disk</span><span class="sxs-lookup"><span data-stu-id="49c5f-108">Expand managed disk</span></span>
<span data-ttu-id="49c5f-109">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="49c5f-109">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="49c5f-110">In the following samples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="49c5f-110">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="49c5f-111">Example parameter names include `myResourceGroup` and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="49c5f-111">Example parameter names include `myResourceGroup` and `myVM`.</span></span>

1. <span data-ttu-id="49c5f-112">Operations on virtual hard disks cannot be performed with the VM running.</span><span class="sxs-lookup"><span data-stu-id="49c5f-112">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="49c5f-113">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="49c5f-113">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="49c5f-114">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="49c5f-114">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="49c5f-115">`az vm stop` does not release the compute resources.</span><span class="sxs-lookup"><span data-stu-id="49c5f-115">`az vm stop` does not release the compute resources.</span></span> <span data-ttu-id="49c5f-116">To release compute resources, use `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="49c5f-116">To release compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="49c5f-117">The VM must be deallocated to expand the virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="49c5f-117">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="49c5f-118">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="49c5f-118">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="49c5f-119">The following example displays a list of managed disks in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="49c5f-119">The following example displays a list of managed disks in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az disk list -g myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="49c5f-120">Expand the required disk with [az disk update](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="49c5f-120">Expand the required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="49c5f-121">The following example expands the managed disk named `myDataDisk` to be `200`Gb in size:</span><span class="sxs-lookup"><span data-stu-id="49c5f-121">The following example expands the managed disk named `myDataDisk` to be `200`Gb in size:</span></span>

    ```azurecli
    az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="49c5f-122">When you expand a managed disk, the updated size is mapped to the nearest managed disk size.</span><span class="sxs-lookup"><span data-stu-id="49c5f-122">When you expand a managed disk, the updated size is mapped to the nearest managed disk size.</span></span> <span data-ttu-id="49c5f-123">For a table of the available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="49c5f-123">For a table of the available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#pricing-and-billing).</span></span>

3. <span data-ttu-id="49c5f-124">Start your VM with [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="49c5f-124">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="49c5f-125">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="49c5f-125">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="49c5f-126">SSH to your VM with the appropriate credentials.</span><span class="sxs-lookup"><span data-stu-id="49c5f-126">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="49c5f-127">To verify the OS disk has been resized, use `df -h`.</span><span class="sxs-lookup"><span data-stu-id="49c5f-127">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="49c5f-128">The following example output shows the primary partition (`/dev/sda1`) is now 200 GB:</span><span class="sxs-lookup"><span data-stu-id="49c5f-128">The following example output shows the primary partition (`/dev/sda1`) is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        194G   52M   193G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="49c5f-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="49c5f-129">Next steps</span></span>
<span data-ttu-id="49c5f-130">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49c5f-130">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="49c5f-131">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49c5f-131">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
