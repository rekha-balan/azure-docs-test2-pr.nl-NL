---
title: Convert a Linux VM in Azure from unmanaged to managed disks | Microsoft Docs
description: How to convert a VM from unmanaged disks to Azure managed disks using the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 1174a3f4295b272b0a0fb5c6b790bb59b53ff63a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564667"
---
# <a name="how-to-convert-a-linux-vm-from-unmanaged-disks-to-azure-managed-disks"></a><span data-ttu-id="dbebd-103">How to convert a Linux VM from unmanaged disks to Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="dbebd-103">How to convert a Linux VM from unmanaged disks to Azure Managed Disks</span></span>

<span data-ttu-id="dbebd-104">If you have existing Linux VMs in Azure that use unmanaged disks in storage accounts and you want those VMs to be able to take advantage of managed disks, you can convert the VMs.</span><span class="sxs-lookup"><span data-stu-id="dbebd-104">If you have existing Linux VMs in Azure that use unmanaged disks in storage accounts and you want those VMs to be able to take advantage of managed disks, you can convert the VMs.</span></span> <span data-ttu-id="dbebd-105">This process converts both the OS disk and any attached data disks.</span><span class="sxs-lookup"><span data-stu-id="dbebd-105">This process converts both the OS disk and any attached data disks.</span></span> <span data-ttu-id="dbebd-106">The conversion process requires a restart of the VM, so schedule the migration of your VMs during a pre-existing maintenance window.</span><span class="sxs-lookup"><span data-stu-id="dbebd-106">The conversion process requires a restart of the VM, so schedule the migration of your VMs during a pre-existing maintenance window.</span></span> <span data-ttu-id="dbebd-107">The migration process is not reversible.</span><span class="sxs-lookup"><span data-stu-id="dbebd-107">The migration process is not reversible.</span></span> <span data-ttu-id="dbebd-108">Be sure to test the migration process by migrating a test virtual machine before performing the migration in production.</span><span class="sxs-lookup"><span data-stu-id="dbebd-108">Be sure to test the migration process by migrating a test virtual machine before performing the migration in production.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbebd-109">During the conversion, you deallocate the VM.</span><span class="sxs-lookup"><span data-stu-id="dbebd-109">During the conversion, you deallocate the VM.</span></span> <span data-ttu-id="dbebd-110">The VM receives a new IP address when it is started after the conversion.</span><span class="sxs-lookup"><span data-stu-id="dbebd-110">The VM receives a new IP address when it is started after the conversion.</span></span> <span data-ttu-id="dbebd-111">If you have a dependency on a fixed IP, use a reserved IP.</span><span class="sxs-lookup"><span data-stu-id="dbebd-111">If you have a dependency on a fixed IP, use a reserved IP.</span></span>

<span data-ttu-id="dbebd-112">You cannot convert an unmanaged disk into a managed disk if the unmanaged disk is in a storage account that is, or at any time has been, encrypted using [Azure Storage Service Encryption (SSE)](../../storage/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dbebd-112">You cannot convert an unmanaged disk into a managed disk if the unmanaged disk is in a storage account that is, or at any time has been, encrypted using [Azure Storage Service Encryption (SSE)](../../storage/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="dbebd-113">The following steps detail how to convert unmanaged disks that are, or have been, in an encrypted storage account:</span><span class="sxs-lookup"><span data-stu-id="dbebd-113">The following steps detail how to convert unmanaged disks that are, or have been, in an encrypted storage account:</span></span>

- <span data-ttu-id="dbebd-114">Copy the virtual hard disk (VHD) with [az storage blob copy start](/cli/azure/storage/blob/copy#start) to a storage account that has never been enabled for Azure Storage Service Encryption.</span><span class="sxs-lookup"><span data-stu-id="dbebd-114">Copy the virtual hard disk (VHD) with [az storage blob copy start](/cli/azure/storage/blob/copy#start) to a storage account that has never been enabled for Azure Storage Service Encryption.</span></span>
- <span data-ttu-id="dbebd-115">Create a VM that uses managed disks and specify that VHD file during creation with [az vm create](/cli/azure/vm#create), or</span><span class="sxs-lookup"><span data-stu-id="dbebd-115">Create a VM that uses managed disks and specify that VHD file during creation with [az vm create](/cli/azure/vm#create), or</span></span>
- <span data-ttu-id="dbebd-116">Attach the copied VHD with [az vm disk attach](/cli/azure/vm/disk#attach) to a running VM with managed disks.</span><span class="sxs-lookup"><span data-stu-id="dbebd-116">Attach the copied VHD with [az vm disk attach](/cli/azure/vm/disk#attach) to a running VM with managed disks.</span></span>

## <a name="convert-vm-to-azure-managed-disks"></a><span data-ttu-id="dbebd-117">Convert VM to Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="dbebd-117">Convert VM to Azure Managed Disks</span></span>
<span data-ttu-id="dbebd-118">This section covers how to convert your existing Azure VMs from unmanaged disks to managed disks.</span><span class="sxs-lookup"><span data-stu-id="dbebd-118">This section covers how to convert your existing Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="dbebd-119">You can use this process to convert from Premium (SDD) unmanaged disks to Premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span><span class="sxs-lookup"><span data-stu-id="dbebd-119">You can use this process to convert from Premium (SDD) unmanaged disks to Premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbebd-120">After performing the following procedure, there is a single block blob that remains in the default vhds container.</span><span class="sxs-lookup"><span data-stu-id="dbebd-120">After performing the following procedure, there is a single block blob that remains in the default vhds container.</span></span> <span data-ttu-id="dbebd-121">The name of the file is “VMName.xxxxxxx.status”.</span><span class="sxs-lookup"><span data-stu-id="dbebd-121">The name of the file is “VMName.xxxxxxx.status”.</span></span> <span data-ttu-id="dbebd-122">Do not delete this remaining status object.</span><span class="sxs-lookup"><span data-stu-id="dbebd-122">Do not delete this remaining status object.</span></span> <span data-ttu-id="dbebd-123">Future work should address this issue.</span><span class="sxs-lookup"><span data-stu-id="dbebd-123">Future work should address this issue.</span></span>

1. <span data-ttu-id="dbebd-124">Deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="dbebd-124">Deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="dbebd-125">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dbebd-125">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="dbebd-126">Convert the VM to managed disks with [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="dbebd-126">Convert the VM to managed disks with [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="dbebd-127">The following process converts the VM named `myVM` including the OS disk and any data disks:</span><span class="sxs-lookup"><span data-stu-id="dbebd-127">The following process converts the VM named `myVM` including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="dbebd-128">Start the VM after the conversion to managed disks with [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="dbebd-128">Start the VM after the conversion to managed disks with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="dbebd-129">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="dbebd-129">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vm-in-an-availability-set-to-managed-disks"></a><span data-ttu-id="dbebd-130">Convert VM in an availability set to managed disks</span><span class="sxs-lookup"><span data-stu-id="dbebd-130">Convert VM in an availability set to managed disks</span></span>

<span data-ttu-id="dbebd-131">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span><span class="sxs-lookup"><span data-stu-id="dbebd-131">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

<span data-ttu-id="dbebd-132">All VMs in the availability set must be deallocated before you convert the availability set.</span><span class="sxs-lookup"><span data-stu-id="dbebd-132">All VMs in the availability set must be deallocated before you convert the availability set.</span></span> <span data-ttu-id="dbebd-133">Plan to convert all VMs to managed disks once the availability itself has been converted to a managed availability set.</span><span class="sxs-lookup"><span data-stu-id="dbebd-133">Plan to convert all VMs to managed disks once the availability itself has been converted to a managed availability set.</span></span> <span data-ttu-id="dbebd-134">You can then start all the VMs and continue operating as normal.</span><span class="sxs-lookup"><span data-stu-id="dbebd-134">You can then start all the VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="dbebd-135">List all VMs in an availability set with [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="dbebd-135">List all VMs in an availability set with [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="dbebd-136">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dbebd-136">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show --resource-group myResourceGroup \
        --name myAvailabilitySet --query [virtualMachines[*].id] --output table
    ```

2. <span data-ttu-id="dbebd-137">Deallocate all the VMs with [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="dbebd-137">Deallocate all the VMs with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="dbebd-138">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dbebd-138">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="dbebd-139">Convert the availability set with [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="dbebd-139">Convert the availability set with [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="dbebd-140">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="dbebd-140">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="dbebd-141">Convert all the VMs to managed disks with [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="dbebd-141">Convert all the VMs to managed disks with [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="dbebd-142">The following process converts the VM named `myVM` including the OS disk and any data disks:</span><span class="sxs-lookup"><span data-stu-id="dbebd-142">The following process converts the VM named `myVM` including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="dbebd-143">Start all the VMs after the conversion to managed disks with [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="dbebd-143">Start all the VMs after the conversion to managed disks with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="dbebd-144">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="dbebd-144">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="dbebd-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbebd-145">Next steps</span></span>
<span data-ttu-id="dbebd-146">For more information about storage options, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="dbebd-146">For more information about storage options, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md)</span></span>
