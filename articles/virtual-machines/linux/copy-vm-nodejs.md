---
title: Create a copy of your Linux VM with the Azure CLI 1.0 | Microsoft Docs
description: Learn how to create a copy of your Azure Linux virtual machine with the Azure CLI 1.0 in the Resource Manager deployment model
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 4448c57cdd8a0d0bc94e013f7da74e1a332bfd42
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549762"
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-the-azure-cli-10"></a><span data-ttu-id="a995c-103">Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a995c-103">Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0</span></span>
<span data-ttu-id="a995c-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="a995c-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model.</span></span> <span data-ttu-id="a995c-105">First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a995c-105">First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.</span></span>

<span data-ttu-id="a995c-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a995c-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="a995c-107">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="a995c-107">CLI versions to complete the task</span></span>
<span data-ttu-id="a995c-108">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="a995c-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="a995c-109">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="a995c-109">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a995c-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="a995c-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a995c-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a995c-111">Before you begin</span></span>
<span data-ttu-id="a995c-112">Ensure that you meet the following prerequisites before you start the steps:</span><span class="sxs-lookup"><span data-stu-id="a995c-112">Ensure that you meet the following prerequisites before you start the steps:</span></span>

* <span data-ttu-id="a995c-113">You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="a995c-113">You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="a995c-114">You also need some information about your existing Azure Linux VM:</span><span class="sxs-lookup"><span data-stu-id="a995c-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="a995c-115">Source VM information</span><span class="sxs-lookup"><span data-stu-id="a995c-115">Source VM information</span></span> | <span data-ttu-id="a995c-116">Where to get it</span><span class="sxs-lookup"><span data-stu-id="a995c-116">Where to get it</span></span> |
| --- | --- |
| <span data-ttu-id="a995c-117">VM name</span><span class="sxs-lookup"><span data-stu-id="a995c-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="a995c-118">Resource Group name</span><span class="sxs-lookup"><span data-stu-id="a995c-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="a995c-119">Location</span><span class="sxs-lookup"><span data-stu-id="a995c-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="a995c-120">Storage Account name</span><span class="sxs-lookup"><span data-stu-id="a995c-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="a995c-121">Container name</span><span class="sxs-lookup"><span data-stu-id="a995c-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="a995c-122">Source VM VHD file name</span><span class="sxs-lookup"><span data-stu-id="a995c-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="a995c-123">You will need to make some choices about your new VM:    </span><span class="sxs-lookup"><span data-stu-id="a995c-123">You will need to make some choices about your new VM:    </span></span><br> <span data-ttu-id="a995c-124">-Container name    </span><span class="sxs-lookup"><span data-stu-id="a995c-124">-Container name    </span></span><br> <span data-ttu-id="a995c-125">-VM name    </span><span class="sxs-lookup"><span data-stu-id="a995c-125">-VM name    </span></span><br> <span data-ttu-id="a995c-126">-VM size    </span><span class="sxs-lookup"><span data-stu-id="a995c-126">-VM size    </span></span><br> <span data-ttu-id="a995c-127">-vNet name    </span><span class="sxs-lookup"><span data-stu-id="a995c-127">-vNet name    </span></span><br> <span data-ttu-id="a995c-128">-SubNet name    </span><span class="sxs-lookup"><span data-stu-id="a995c-128">-SubNet name    </span></span><br> <span data-ttu-id="a995c-129">-IP Name    </span><span class="sxs-lookup"><span data-stu-id="a995c-129">-IP Name    </span></span><br> <span data-ttu-id="a995c-130">-NIC name</span><span class="sxs-lookup"><span data-stu-id="a995c-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="a995c-131">Login and set your subscription</span><span class="sxs-lookup"><span data-stu-id="a995c-131">Login and set your subscription</span></span>
1. <span data-ttu-id="a995c-132">Login to the CLI.</span><span class="sxs-lookup"><span data-stu-id="a995c-132">Login to the CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="a995c-133">Make sure you are in Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="a995c-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="a995c-134">Set the correct subscription.</span><span class="sxs-lookup"><span data-stu-id="a995c-134">Set the correct subscription.</span></span> <span data-ttu-id="a995c-135">You can use 'azure account list' to see all of your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="a995c-135">You can use 'azure account list' to see all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-the-vm"></a><span data-ttu-id="a995c-136">Stop the VM</span><span class="sxs-lookup"><span data-stu-id="a995c-136">Stop the VM</span></span>
<span data-ttu-id="a995c-137">Stop and deallocate the source VM.</span><span class="sxs-lookup"><span data-stu-id="a995c-137">Stop and deallocate the source VM.</span></span> <span data-ttu-id="a995c-138">You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.</span><span class="sxs-lookup"><span data-stu-id="a995c-138">You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-the-vhd"></a><span data-ttu-id="a995c-139">Copy the VHD</span><span class="sxs-lookup"><span data-stu-id="a995c-139">Copy the VHD</span></span>
<span data-ttu-id="a995c-140">You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="a995c-140">You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`.</span></span> <span data-ttu-id="a995c-141">In this example, we are going to copy the VHD to the same storage account, but a different container.</span><span class="sxs-lookup"><span data-stu-id="a995c-141">In this example, we are going to copy the VHD to the same storage account, but a different container.</span></span>

<span data-ttu-id="a995c-142">To copy the VHD to another container in the same storage account, type:</span><span class="sxs-lookup"><span data-stu-id="a995c-142">To copy the VHD to another container in the same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-the-virtual-network-for-your-new-vm"></a><span data-ttu-id="a995c-143">Set up the virtual network for your new VM</span><span class="sxs-lookup"><span data-stu-id="a995c-143">Set up the virtual network for your new VM</span></span>
<span data-ttu-id="a995c-144">Set up a virtual network and NIC for your new VM.</span><span class="sxs-lookup"><span data-stu-id="a995c-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-the-new-vm"></a><span data-ttu-id="a995c-145">Create the new VM</span><span class="sxs-lookup"><span data-stu-id="a995c-145">Create the new VM</span></span>
<span data-ttu-id="a995c-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:</span><span class="sxs-lookup"><span data-stu-id="a995c-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="a995c-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="a995c-147">Next steps</span></span>
<span data-ttu-id="a995c-148">To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="a995c-148">To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

