---
title: Upload a custom Linux disk with Azure CLI 2.0 | Microsoft Docs
description: Create and upload a virtual hard disk (VHD) to Azure using the Resource Manager deployment model and the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/02/2017
ms.author: iainfou
ms.openlocfilehash: 498601e34869baed90ef783787a3fb8f217c8229
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551708"
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="8dc6d-103">Upload and create a Linux VM from custom disk with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8dc6d-103">Upload and create a Linux VM from custom disk with the Azure CLI 2.0</span></span>
<span data-ttu-id="8dc6d-104">This article shows you how to upload a virtual hard disk (VHD) to Azure with the Azure CLI 2.0 and create Linux VMs from this custom disk.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-104">This article shows you how to upload a virtual hard disk (VHD) to Azure with the Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="8dc6d-105">You can also perform these steps with the [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-105">You can also perform these steps with the [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8dc6d-106">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-106">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="8dc6d-107">Quick commands</span><span class="sxs-lookup"><span data-stu-id="8dc6d-107">Quick commands</span></span>
<span data-ttu-id="8dc6d-108">If you need to quickly accomplish the task, the following section details the base commands to upload a VHD to Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-108">If you need to quickly accomplish the task, the following section details the base commands to upload a VHD to Azure.</span></span> <span data-ttu-id="8dc6d-109">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-109">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="8dc6d-110">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-110">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="8dc6d-111">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-111">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8dc6d-112">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-112">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="8dc6d-113">First, create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-113">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8dc6d-114">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-114">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="8dc6d-115">Create a storage account to hold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-115">Create a storage account to hold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="8dc6d-116">Even if you wish to use [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md), you need to create a storage account that you upload your VHD to before converting to a managed disk.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-116">Even if you wish to use [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md), you need to create a storage account that you upload your VHD to before converting to a managed disk.</span></span> <span data-ttu-id="8dc6d-117">The following example creates a storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-117">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="8dc6d-118">List the access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-118">List the access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="8dc6d-119">Make a note of `key1`:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="8dc6d-120">Create a container within your storage account using the storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-120">Create a container within your storage account using the storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="8dc6d-121">The following example creates a container named `mydisks` using the storage key value from `key1`:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-121">The following example creates a container named `mydisks` using the storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="8dc6d-122">Finally, upload your VHD to the container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-122">Finally, upload your VHD to the container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="8dc6d-123">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-123">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

### <a name="azure-managed-disks"></a><span data-ttu-id="8dc6d-124">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="8dc6d-124">Azure Managed Disks</span></span>
<span data-ttu-id="8dc6d-125">You can create a VM using Azure Managed Disks or unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-125">You can create a VM using Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="8dc6d-126">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-126">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="8dc6d-127">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-127">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="8dc6d-128">To create a VM from your VHD, first convert the VHD to a managed disk with [az disk create](/cli/azure/disk/create):</span><span class="sxs-lookup"><span data-stu-id="8dc6d-128">To create a VM from your VHD, first convert the VHD to a managed disk with [az disk create](/cli/azure/disk/create):</span></span>

```azurecli
az disk create --resource-group myResourceGroup --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```

<span data-ttu-id="8dc6d-129">Obtain the details of the managed disk you created with [az disk list](/cli/azure/disk/list):</span><span class="sxs-lookup"><span data-stu-id="8dc6d-129">Obtain the details of the managed disk you created with [az disk list](/cli/azure/disk/list):</span></span>

```azurecli
az disk list --resource-group myResourceGroup \
  --query [].{Name:name,ID:id} --output table
```

<span data-ttu-id="8dc6d-130">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-130">The output is similar to the following example:</span></span>

```azurecli
Name               ID
-----------------  ----------------------------------------------------------------------------------------------------
myManagedDisk    /subscriptions/mySubscriptionId/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/myManagedDisk
```

<span data-ttu-id="8dc6d-131">Now, create your VM with [az vm create](/cli/azure/vm#create) and specify the name of your managed disk (`--attach-os-disk`).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-131">Now, create your VM with [az vm create](/cli/azure/vm#create) and specify the name of your managed disk (`--attach-os-disk`).</span></span> <span data-ttu-id="8dc6d-132">The following example creates a VM named `myVM` using the managed disk created from your uploaded VHD:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-132">The following example creates a VM named `myVM` using the managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --attach-os-disk myManagedDisk
```

### <a name="unmanaged-disks"></a><span data-ttu-id="8dc6d-133">Unmanaged disks</span><span class="sxs-lookup"><span data-stu-id="8dc6d-133">Unmanaged disks</span></span>
<span data-ttu-id="8dc6d-134">To create a VM with unmanaged disks, specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-134">To create a VM with unmanaged disks, specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="8dc6d-135">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-135">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="8dc6d-136">The destination storage account has to be the same as where you uploaded your virtual disk to.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-136">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="8dc6d-137">You also need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-137">You also need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="8dc6d-138">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-138">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="8dc6d-139">Requirements</span><span class="sxs-lookup"><span data-stu-id="8dc6d-139">Requirements</span></span>
<span data-ttu-id="8dc6d-140">To complete the following steps, you need:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-140">To complete the following steps, you need:</span></span>

* <span data-ttu-id="8dc6d-141">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-141">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="8dc6d-142">Multiple tools exist to create a VM and VHD:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-142">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="8dc6d-143">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-143">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="8dc6d-144">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-144">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="8dc6d-145">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-145">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="8dc6d-146">The newer VHDX format is not supported in Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-146">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="8dc6d-147">When you create a VM, specify VHD as the format.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-147">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="8dc6d-148">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-148">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="8dc6d-149">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-149">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="8dc6d-150">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-150">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="8dc6d-151">VMs created from your custom disk must reside in the same storage account as the disk itself</span><span class="sxs-lookup"><span data-stu-id="8dc6d-151">VMs created from your custom disk must reside in the same storage account as the disk itself</span></span>
  * <span data-ttu-id="8dc6d-152">Create a storage account and container to hold both your custom disk and created VMs</span><span class="sxs-lookup"><span data-stu-id="8dc6d-152">Create a storage account and container to hold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="8dc6d-153">After you have created all your VMs, you can safely delete your disk</span><span class="sxs-lookup"><span data-stu-id="8dc6d-153">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="8dc6d-154">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-154">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="8dc6d-155">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-155">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8dc6d-156">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-156">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="8dc6d-157"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="8dc6d-157"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-disk-to-be-uploaded"></a><span data-ttu-id="8dc6d-158">Prepare the disk to be uploaded</span><span class="sxs-lookup"><span data-stu-id="8dc6d-158">Prepare the disk to be uploaded</span></span>
<span data-ttu-id="8dc6d-159">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-159">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="8dc6d-160">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-160">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="8dc6d-161">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="8dc6d-161">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="8dc6d-162">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="8dc6d-162">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="8dc6d-163">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="8dc6d-163">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="8dc6d-164">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="8dc6d-164">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="8dc6d-165">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="8dc6d-165">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="8dc6d-166">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="8dc6d-166">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="8dc6d-167">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="8dc6d-167">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="8dc6d-168">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-168">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="8dc6d-169">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-169">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="8dc6d-170">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="8dc6d-170">Create a resource group</span></span>
<span data-ttu-id="8dc6d-171">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-171">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="8dc6d-172">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-172">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="8dc6d-173">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-173">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="8dc6d-174">The following example creates a resource group named `myResourceGroup` in the `westus` location: [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8dc6d-174">The following example creates a resource group named `myResourceGroup` in the `westus` location: [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md)</span></span>
```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="8dc6d-175">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="8dc6d-175">Create a storage account</span></span>
<span data-ttu-id="8dc6d-176">When you create a VM, you can do so with Azure Managed Disks or unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-176">When you create a VM, you can do so with Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="8dc6d-177">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-177">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="8dc6d-178">Unmanaged disks are stored as page blobs within a storage account.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-178">Unmanaged disks are stored as page blobs within a storage account.</span></span> <span data-ttu-id="8dc6d-179">For more information, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md) or [Azure blob storage here](../../storage/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-179">For more information, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md) or [Azure blob storage here](../../storage/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="8dc6d-180">Even if you wish to use managed disks, you need to create a storage account that you upload your VHD to before converting to a managed disk.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-180">Even if you wish to use managed disks, you need to create a storage account that you upload your VHD to before converting to a managed disk.</span></span>

<span data-ttu-id="8dc6d-181">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-181">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="8dc6d-182">Any VMs with unmanaged disks that you create from your custom disk need to be in the same storage account as that disk.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-182">Any VMs with unmanaged disks that you create from your custom disk need to be in the same storage account as that disk.</span></span> <span data-ttu-id="8dc6d-183">You can create VMs with managed disks in any resource group within your subscription.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-183">You can create VMs with managed disks in any resource group within your subscription.</span></span>

<span data-ttu-id="8dc6d-184">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-184">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="8dc6d-185">List storage account keys</span><span class="sxs-lookup"><span data-stu-id="8dc6d-185">List storage account keys</span></span>
<span data-ttu-id="8dc6d-186">Azure generates two 512-bit access keys for each storage account.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-186">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="8dc6d-187">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-187">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="8dc6d-188">Read more about [managing access to storage here](../../storage/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-188">Read more about [managing access to storage here](../../storage/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="8dc6d-189">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-189">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="8dc6d-190">View the access keys for the storage account you created:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-190">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="8dc6d-191">The output is similar to:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-191">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="8dc6d-192">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-192">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="8dc6d-193">Create a storage container</span><span class="sxs-lookup"><span data-stu-id="8dc6d-193">Create a storage container</span></span>
<span data-ttu-id="8dc6d-194">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-194">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="8dc6d-195">A storage account can contain any number of containers.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-195">A storage account can contain any number of containers.</span></span> <span data-ttu-id="8dc6d-196">Create a container with [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-196">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="8dc6d-197">The following example creates a container named `mydisks`, specifying the access key obtained in the previous step (`key1`):</span><span class="sxs-lookup"><span data-stu-id="8dc6d-197">The following example creates a container named `mydisks`, specifying the access key obtained in the previous step (`key1`):</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="8dc6d-198">Upload VHD</span><span class="sxs-lookup"><span data-stu-id="8dc6d-198">Upload VHD</span></span>
<span data-ttu-id="8dc6d-199">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-199">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="8dc6d-200">You upload and store your custom disk as a page blob.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-200">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="8dc6d-201">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-201">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-vm-from-custom-disk"></a><span data-ttu-id="8dc6d-202">Create VM from custom disk</span><span class="sxs-lookup"><span data-stu-id="8dc6d-202">Create VM from custom disk</span></span>
<span data-ttu-id="8dc6d-203">Again, you can create a VM using Azure Managed Disks or unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-203">Again, you can create a VM using Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="8dc6d-204">For both types, specify the URI to the managed or unmanaged disk when you create a VM.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-204">For both types, specify the URI to the managed or unmanaged disk when you create a VM.</span></span> <span data-ttu-id="8dc6d-205">For unmanaged disks, ensure that the destination storage account matches where your custom disk is stored.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-205">For unmanaged disks, ensure that the destination storage account matches where your custom disk is stored.</span></span> <span data-ttu-id="8dc6d-206">You can create your VM using the Azure 2.0 or Resource Manager JSON template.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-206">You can create your VM using the Azure 2.0 or Resource Manager JSON template.</span></span>

### <a name="azure-cli-20---azure-managed-disks"></a><span data-ttu-id="8dc6d-207">Azure CLI 2.0 - Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="8dc6d-207">Azure CLI 2.0 - Azure Managed Disks</span></span>
<span data-ttu-id="8dc6d-208">To create a VM from your VHD, first convert the VHD to a managed disk with [az disk create](/cli/azure/disk/create).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-208">To create a VM from your VHD, first convert the VHD to a managed disk with [az disk create](/cli/azure/disk/create).</span></span> <span data-ttu-id="8dc6d-209">The following example creates a managed disk named `myManagedDisk` from the VHD you uploaded to your named storage account and container:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-209">The following example creates a managed disk named `myManagedDisk` from the VHD you uploaded to your named storage account and container:</span></span>

```azurecli
az disk create --resource-group myResourceGroup --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```

<span data-ttu-id="8dc6d-210">Obtain the URI of the managed disk you created with [az disk list](/cli/azure/disk/list):</span><span class="sxs-lookup"><span data-stu-id="8dc6d-210">Obtain the URI of the managed disk you created with [az disk list](/cli/azure/disk/list):</span></span>

```azurecli
az disk list --resource-group myResourceGroup \
  --query '[].{Name:name,URI:creationData.sourceUri}' --output table
```

<span data-ttu-id="8dc6d-211">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-211">The output is similar to the following example:</span></span>

```azurecli
Name               URI
-----------------  ----------------------------------------------------------------------------------------------------
myUMDiskFromVHD    https://vhdstoragezw9.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/my_image-osDisk.vhd
```

<span data-ttu-id="8dc6d-212">Now, create your VM with [az vm create](/cli/azure/vm#create) and specify the URI of your managed disk (`--image`).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-212">Now, create your VM with [az vm create](/cli/azure/vm#create) and specify the URI of your managed disk (`--image`).</span></span> <span data-ttu-id="8dc6d-213">The following example creates a VM named `myVM` using the managed disk created from your uploaded VHD:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-213">The following example creates a VM named `myVM` using the managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --attach-os-disk https://vhdstoragezw9.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/my_image-osDisk.vhd
```

### <a name="azure-20---unmanaged-disks"></a><span data-ttu-id="8dc6d-214">Azure 2.0 - unmanaged disks</span><span class="sxs-lookup"><span data-stu-id="8dc6d-214">Azure 2.0 - unmanaged disks</span></span>
<span data-ttu-id="8dc6d-215">To create a VM with unmanaged disks, specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-215">To create a VM with unmanaged disks, specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="8dc6d-216">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-216">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

<span data-ttu-id="8dc6d-217">You specify the `--image` parameter with [az vm create](/cli/azure/vm#create) to point to your custom disk.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-217">You specify the `--image` parameter with [az vm create](/cli/azure/vm#create) to point to your custom disk.</span></span> <span data-ttu-id="8dc6d-218">Ensure that `--storage-account` matches the storage account where your custom disk is stored.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-218">Ensure that `--storage-account` matches the storage account where your custom disk is stored.</span></span> <span data-ttu-id="8dc6d-219">You do not have to use the same container as the custom disk to store your VMs.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-219">You do not have to use the same container as the custom disk to store your VMs.</span></span> <span data-ttu-id="8dc6d-220">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-220">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="8dc6d-221">The following example creates a VM named `myVM` from your custom disk:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-221">The following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="8dc6d-222">You still need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as username and SSH keys.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-222">You still need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as username and SSH keys.</span></span>


### <a name="resource-manager-template---unmanaged-disks"></a><span data-ttu-id="8dc6d-223">Resource Manager template - unmanaged disks</span><span class="sxs-lookup"><span data-stu-id="8dc6d-223">Resource Manager template - unmanaged disks</span></span>
<span data-ttu-id="8dc6d-224">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-224">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="8dc6d-225">The templates are broken down in to different resource providers such as compute or network.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-225">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="8dc6d-226">You can use existing templates or write your own.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-226">You can use existing templates or write your own.</span></span> <span data-ttu-id="8dc6d-227">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-227">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="8dc6d-228">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-228">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="8dc6d-229">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk and your new VM's virtual disk.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-229">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="8dc6d-230">The following shows an example of the JSON for using a custom disk:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-230">The following shows an example of the JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="8dc6d-231">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-231">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="8dc6d-232">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) to create your VMs.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-232">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) to create your VMs.</span></span> <span data-ttu-id="8dc6d-233">Specify the URI of your JSON template with the `--template-uri` parameter:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-233">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="8dc6d-234">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span><span class="sxs-lookup"><span data-stu-id="8dc6d-234">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="8dc6d-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="8dc6d-235">Next steps</span></span>
<span data-ttu-id="8dc6d-236">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-236">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="8dc6d-237">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span><span class="sxs-lookup"><span data-stu-id="8dc6d-237">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="8dc6d-238">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8dc6d-238">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

