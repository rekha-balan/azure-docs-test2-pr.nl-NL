---
title: Copy a Linux VM by using Azure CLI 2.0 | Microsoft Docs
description: Learn how to create a copy of your Azure Linux VM by using Azure CLI 2.0 and Managed Disks.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: e519411837ac9e1b31c2c57a07bac96c65dec649
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554284"
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="42a55-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span><span class="sxs-lookup"><span data-stu-id="42a55-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="42a55-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Azure CLI 2.0 and the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="42a55-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Azure CLI 2.0 and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="42a55-105">You can also perform these steps with the [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42a55-105">You can also perform these steps with the [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="42a55-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42a55-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42a55-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42a55-107">Prerequisites</span></span>


-   <span data-ttu-id="42a55-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="42a55-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="42a55-109">Sign in to an Azure account with [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="42a55-109">Sign in to an Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="42a55-110">Have an Azure VM to use as the source for your copy.</span><span class="sxs-lookup"><span data-stu-id="42a55-110">Have an Azure VM to use as the source for your copy.</span></span>

## <a name="step-1-stop-the-source-vm"></a><span data-ttu-id="42a55-111">Step 1: Stop the source VM</span><span class="sxs-lookup"><span data-stu-id="42a55-111">Step 1: Stop the source VM</span></span>


<span data-ttu-id="42a55-112">Deallocate the source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="42a55-112">Deallocate the source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="42a55-113">The following example deallocates the VM named **myVM** in the resource group **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="42a55-113">The following example deallocates the VM named **myVM** in the resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-the-source-vm"></a><span data-ttu-id="42a55-114">Step 2: Copy the source VM</span><span class="sxs-lookup"><span data-stu-id="42a55-114">Step 2: Copy the source VM</span></span>


<span data-ttu-id="42a55-115">To copy a VM, you create a copy of the underlying virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="42a55-115">To copy a VM, you create a copy of the underlying virtual hard disk.</span></span> <span data-ttu-id="42a55-116">This process creates a specialized VHD as a Managed Disk that contains the same configuration and settings as the source VM.</span><span class="sxs-lookup"><span data-stu-id="42a55-116">This process creates a specialized VHD as a Managed Disk that contains the same configuration and settings as the source VM.</span></span>

<span data-ttu-id="42a55-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42a55-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="42a55-118">List each VM and the name of its OS disk with [az vm list](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="42a55-118">List each VM and the name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="42a55-119">The following example lists all VMs in the resource group named **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="42a55-119">The following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="42a55-120">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="42a55-120">The output is similar to the following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="42a55-121">Copy the disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="42a55-121">Copy the disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="42a55-122">The following example creates a disk named **myCopiedDisk** from the managed disk named **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="42a55-122">The following example creates a disk named **myCopiedDisk** from the managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="42a55-123">Verify the managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="42a55-123">Verify the managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="42a55-124">The following example lists the managed disks in the resource group named **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="42a55-124">The following example lists the managed disks in the resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="42a55-125">Skip to ["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="42a55-125">Skip to ["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="42a55-126">Step 3: Set up a virtual network</span><span class="sxs-lookup"><span data-stu-id="42a55-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="42a55-127">The following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span><span class="sxs-lookup"><span data-stu-id="42a55-127">The following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="42a55-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want to use a VM in an existing virtual network.</span><span class="sxs-lookup"><span data-stu-id="42a55-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want to use a VM in an existing virtual network.</span></span>

<span data-ttu-id="42a55-129">If you want to create a virtual network infrastructure for your copied VMs, follow the next few steps.</span><span class="sxs-lookup"><span data-stu-id="42a55-129">If you want to create a virtual network infrastructure for your copied VMs, follow the next few steps.</span></span> <span data-ttu-id="42a55-130">If you don't want to create a virtual network, skip to [Step 4: Create a VM](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="42a55-130">If you don't want to create a virtual network, skip to [Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="42a55-131">Create the virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="42a55-131">Create the virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="42a55-132">The following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="42a55-132">The following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="42a55-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="42a55-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="42a55-134">The following example creates a public IP named **myPublicIP** with the DNS name of **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="42a55-134">The following example creates a public IP named **myPublicIP** with the DNS name of **mypublicdns**.</span></span> <span data-ttu-id="42a55-135">(The DNS name must be unique, so provide a unique name.)</span><span class="sxs-lookup"><span data-stu-id="42a55-135">(The DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="42a55-136">Create the NIC using [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="42a55-136">Create the NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="42a55-137">The following example creates a NIC named **myNic** that's attached to the **mySubnet** subnet:</span><span class="sxs-lookup"><span data-stu-id="42a55-137">The following example creates a NIC named **myNic** that's attached to the **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="42a55-138">Step 4: Create a VM</span><span class="sxs-lookup"><span data-stu-id="42a55-138">Step 4: Create a VM</span></span>

<span data-ttu-id="42a55-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="42a55-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="42a55-140">Specify the copied managed disk to use as the OS disk (--attach-os-disk), as follows:</span><span class="sxs-lookup"><span data-stu-id="42a55-140">Specify the copied managed disk to use as the OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="42a55-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="42a55-141">Next steps</span></span>

<span data-ttu-id="42a55-142">To learn how to use Azure CLI to manage your new VM, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="42a55-142">To learn how to use Azure CLI to manage your new VM, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
