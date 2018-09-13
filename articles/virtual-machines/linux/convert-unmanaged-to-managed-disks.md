---
title: Convert a Linux virtual machine in Azure from unmanaged disks to managed disks - Azure Managed Disks  | Microsoft Docs
description: How to convert a Linux VM from unmanaged disks to managed disks by using Azure CLI 2.0 in the Resource Manager deployment model
services: virtual-machines-linux
documentationcenter: ''
author: roygara
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 12/15/2017
ms.author: rogarana
ms.openlocfilehash: 8a7abc7d3a209f036862233c8f38fcac7cfc26f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44788910"
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="ad3f4-103">Convert a Linux virtual machine from unmanaged disks to managed disks</span><span class="sxs-lookup"><span data-stu-id="ad3f4-103">Convert a Linux virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="ad3f4-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use [Azure Managed Disks](../linux/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use [Azure Managed Disks](../linux/managed-disks-overview.md).</span></span> <span data-ttu-id="ad3f4-105">This process converts both the OS disk and any attached data disks.</span><span class="sxs-lookup"><span data-stu-id="ad3f4-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="ad3f4-106">This article shows you how to convert VMs by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ad3f4-106">This article shows you how to convert VMs by using the Azure CLI.</span></span> <span data-ttu-id="ad3f4-107">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-107">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="ad3f4-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="ad3f4-108">Before you begin</span></span>
* <span data-ttu-id="ad3f4-109">Review [the FAQ about migration to Managed Disks](faq-for-disks.md#migrate-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-109">Review [the FAQ about migration to Managed Disks](faq-for-disks.md#migrate-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="ad3f4-110">Convert single-instance VMs</span><span class="sxs-lookup"><span data-stu-id="ad3f4-110">Convert single-instance VMs</span></span>
<span data-ttu-id="ad3f4-111">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span><span class="sxs-lookup"><span data-stu-id="ad3f4-111">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="ad3f4-112">(If your VMs are in an availability set, see the next section.) You can use this process to convert the VMs from premium (SSD) unmanaged disks to premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span><span class="sxs-lookup"><span data-stu-id="ad3f4-112">(If your VMs are in an availability set, see the next section.) You can use this process to convert the VMs from premium (SSD) unmanaged disks to premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span></span>

1. <span data-ttu-id="ad3f4-113">Deallocate the VM by using [az vm deallocate](/cli/azure/vm#az_vm_deallocate).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-113">Deallocate the VM by using [az vm deallocate](/cli/azure/vm#az_vm_deallocate).</span></span> <span data-ttu-id="ad3f4-114">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad3f4-114">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="ad3f4-115">Convert the VM to managed disks by using [az vm convert](/cli/azure/vm#az_vm_convert).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-115">Convert the VM to managed disks by using [az vm convert](/cli/azure/vm#az_vm_convert).</span></span> <span data-ttu-id="ad3f4-116">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span><span class="sxs-lookup"><span data-stu-id="ad3f4-116">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="ad3f4-117">Start the VM after the conversion to managed disks by using [az vm start](/cli/azure/vm#az_vm_start).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-117">Start the VM after the conversion to managed disks by using [az vm start](/cli/azure/vm#az_vm_start).</span></span> <span data-ttu-id="ad3f4-118">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="ad3f4-118">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="ad3f4-119">Convert VMs in an availability set</span><span class="sxs-lookup"><span data-stu-id="ad3f4-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="ad3f4-120">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span><span class="sxs-lookup"><span data-stu-id="ad3f4-120">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

<span data-ttu-id="ad3f4-121">All VMs in the availability set must be deallocated before you convert the availability set.</span><span class="sxs-lookup"><span data-stu-id="ad3f4-121">All VMs in the availability set must be deallocated before you convert the availability set.</span></span> <span data-ttu-id="ad3f4-122">Plan to convert all VMs to managed disks after the availability set itself has been converted to a managed availability set.</span><span class="sxs-lookup"><span data-stu-id="ad3f4-122">Plan to convert all VMs to managed disks after the availability set itself has been converted to a managed availability set.</span></span> <span data-ttu-id="ad3f4-123">Then, start all the VMs and continue operating as normal.</span><span class="sxs-lookup"><span data-stu-id="ad3f4-123">Then, start all the VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="ad3f4-124">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#az_vm_availability_set_list).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-124">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#az_vm_availability_set_list).</span></span> <span data-ttu-id="ad3f4-125">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad3f4-125">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="ad3f4-126">Deallocate all the VMs by using [az vm deallocate](/cli/azure/vm#az_vm_deallocate).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-126">Deallocate all the VMs by using [az vm deallocate](/cli/azure/vm#az_vm_deallocate).</span></span> <span data-ttu-id="ad3f4-127">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad3f4-127">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="ad3f4-128">Convert the availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#az_vm_availability_set_convert).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-128">Convert the availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#az_vm_availability_set_convert).</span></span> <span data-ttu-id="ad3f4-129">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad3f4-129">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="ad3f4-130">Convert all the VMs to managed disks by using [az vm convert](/cli/azure/vm#az_vm_convert).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-130">Convert all the VMs to managed disks by using [az vm convert](/cli/azure/vm#az_vm_convert).</span></span> <span data-ttu-id="ad3f4-131">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span><span class="sxs-lookup"><span data-stu-id="ad3f4-131">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="ad3f4-132">Start all the VMs after the conversion to managed disks by using [az vm start](/cli/azure/vm#az_vm_start).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-132">Start all the VMs after the conversion to managed disks by using [az vm start](/cli/azure/vm#az_vm_start).</span></span> <span data-ttu-id="ad3f4-133">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ad3f4-133">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="ad3f4-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad3f4-134">Next steps</span></span>
<span data-ttu-id="ad3f4-135">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad3f4-135">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
