---
title: Upload or copy a custom Linux VM with Azure CLI 2.0 | Microsoft Docs
description: Upload or copy a customized virtual machine using the Resource Manager deployment model and the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 8211466698cdcc6f80d21660b930b35b3be5cbdc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827171"
---
# <a name="create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="f7332-103">Create a Linux VM from custom disk with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f7332-103">Create a Linux VM from custom disk with the Azure CLI 2.0</span></span>

<!-- rename to create-vm-specialized -->

<span data-ttu-id="f7332-104">This article shows you how to upload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from the custom disk.</span><span class="sxs-lookup"><span data-stu-id="f7332-104">This article shows you how to upload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from the custom disk.</span></span> <span data-ttu-id="f7332-105">You can install and configure a Linux distro to your requirements and then use that VHD to quickly create a new Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f7332-105">You can install and configure a Linux distro to your requirements and then use that VHD to quickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="f7332-106">If you want to create multiple VMs from your customized disk, you should create an image from your VM or VHD.</span><span class="sxs-lookup"><span data-stu-id="f7332-106">If you want to create multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="f7332-107">For more information, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="f7332-107">For more information, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="f7332-108">You have two options:</span><span class="sxs-lookup"><span data-stu-id="f7332-108">You have two options:</span></span>
* [<span data-ttu-id="f7332-109">Upload a VHD</span><span class="sxs-lookup"><span data-stu-id="f7332-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="f7332-110">Copy an existing Azure VM</span><span class="sxs-lookup"><span data-stu-id="f7332-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="f7332-111">Quick commands</span><span class="sxs-lookup"><span data-stu-id="f7332-111">Quick commands</span></span>

<span data-ttu-id="f7332-112">When creating a new VM using [az vm create](/cli/azure/vm#az_vm_create) from a customized or specialized disk you **attach** the disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span><span class="sxs-lookup"><span data-stu-id="f7332-112">When creating a new VM using [az vm create](/cli/azure/vm#az_vm_create) from a customized or specialized disk you **attach** the disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="f7332-113">The following example creates a VM named *myVM* using the managed disk named *myManagedDisk* created from your customized VHD:</span><span class="sxs-lookup"><span data-stu-id="f7332-113">The following example creates a VM named *myVM* using the managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="f7332-114">Requirements</span><span class="sxs-lookup"><span data-stu-id="f7332-114">Requirements</span></span>
<span data-ttu-id="f7332-115">To complete the following steps, you need:</span><span class="sxs-lookup"><span data-stu-id="f7332-115">To complete the following steps, you need:</span></span>

* <span data-ttu-id="f7332-116">A Linux virtual machine that has been prepared for use in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7332-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="f7332-117">The [Prepare the VM](#prepare-the-vm) section of this article covers how to find distro specific information on installing the Azure Linux Agent (waagent) which is required for the VM to work properly in Azure and for you to be able to connect to it using SSH.</span><span class="sxs-lookup"><span data-stu-id="f7332-117">The [Prepare the VM](#prepare-the-vm) section of this article covers how to find distro specific information on installing the Azure Linux Agent (waagent) which is required for the VM to work properly in Azure and for you to be able to connect to it using SSH.</span></span>
* <span data-ttu-id="f7332-118">The VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span><span class="sxs-lookup"><span data-stu-id="f7332-118">The VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="f7332-119">Multiple tools exist to create a VM and VHD:</span><span class="sxs-lookup"><span data-stu-id="f7332-119">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="f7332-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span><span class="sxs-lookup"><span data-stu-id="f7332-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="f7332-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span><span class="sxs-lookup"><span data-stu-id="f7332-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="f7332-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7332-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f7332-123">The newer VHDX format is not supported in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7332-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="f7332-124">When you create a VM, specify VHD as the format.</span><span class="sxs-lookup"><span data-stu-id="f7332-124">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="f7332-125">If needed, you can convert VHDX disks to VHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f7332-125">If needed, you can convert VHDX disks to VHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="f7332-126">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span><span class="sxs-lookup"><span data-stu-id="f7332-126">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="f7332-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span><span class="sxs-lookup"><span data-stu-id="f7332-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 


* <span data-ttu-id="f7332-128">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="f7332-128">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span>

<span data-ttu-id="f7332-129">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="f7332-129">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f7332-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="f7332-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="f7332-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="f7332-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="f7332-132">Prepare the VM</span><span class="sxs-lookup"><span data-stu-id="f7332-132">Prepare the VM</span></span>

<span data-ttu-id="f7332-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="f7332-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="f7332-134">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span><span class="sxs-lookup"><span data-stu-id="f7332-134">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="f7332-135">CentOS-based Distributions</span><span class="sxs-lookup"><span data-stu-id="f7332-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f7332-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="f7332-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f7332-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="f7332-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f7332-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="f7332-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f7332-139">SLES & openSUSE</span><span class="sxs-lookup"><span data-stu-id="f7332-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f7332-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f7332-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f7332-141">Other - Non-Endorsed Distributions</span><span class="sxs-lookup"><span data-stu-id="f7332-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="f7332-142">Also see the [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span><span class="sxs-lookup"><span data-stu-id="f7332-142">Also see the [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f7332-143">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7332-143">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="f7332-144">Option 1: Upload a VHD</span><span class="sxs-lookup"><span data-stu-id="f7332-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="f7332-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span><span class="sxs-lookup"><span data-stu-id="f7332-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="f7332-146">To use the VHD to create a new Azure VM, you need to upload the VHD to a storage account and create a managed disk from the VHD.</span><span class="sxs-lookup"><span data-stu-id="f7332-146">To use the VHD to create a new Azure VM, you need to upload the VHD to a storage account and create a managed disk from the VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="f7332-147">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f7332-147">Create a resource group</span></span>

<span data-ttu-id="f7332-148">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#az_group_create).</span><span class="sxs-lookup"><span data-stu-id="f7332-148">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#az_group_create).</span></span>

<span data-ttu-id="f7332-149">The following example creates a resource group named *myResourceGroup* in the *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f7332-149">The following example creates a resource group named *myResourceGroup* in the *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="f7332-150">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="f7332-150">Create a storage account</span></span>

<span data-ttu-id="f7332-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#az_storage_account_create).</span><span class="sxs-lookup"><span data-stu-id="f7332-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#az_storage_account_create).</span></span> 

<span data-ttu-id="f7332-152">The following example creates a storage account named *mystorageaccount* in the resource group previously created:</span><span class="sxs-lookup"><span data-stu-id="f7332-152">The following example creates a storage account named *mystorageaccount* in the resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="f7332-153">List storage account keys</span><span class="sxs-lookup"><span data-stu-id="f7332-153">List storage account keys</span></span>
<span data-ttu-id="f7332-154">Azure generates two 512-bit access keys for each storage account.</span><span class="sxs-lookup"><span data-stu-id="f7332-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="f7332-155">These access keys are used when authenticating to the storage account, like carrying out write operations.</span><span class="sxs-lookup"><span data-stu-id="f7332-155">These access keys are used when authenticating to the storage account, like carrying out write operations.</span></span> <span data-ttu-id="f7332-156">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f7332-156">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="f7332-157">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#az_storage_account_keys_list).</span><span class="sxs-lookup"><span data-stu-id="f7332-157">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#az_storage_account_keys_list).</span></span>

<span data-ttu-id="f7332-158">View the access keys for the storage account you created:</span><span class="sxs-lookup"><span data-stu-id="f7332-158">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="f7332-159">The output is similar to:</span><span class="sxs-lookup"><span data-stu-id="f7332-159">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="f7332-160">Make a note of **key1** as you will use it to interact with your storage account in the next steps.</span><span class="sxs-lookup"><span data-stu-id="f7332-160">Make a note of **key1** as you will use it to interact with your storage account in the next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="f7332-161">Create a storage container</span><span class="sxs-lookup"><span data-stu-id="f7332-161">Create a storage container</span></span>
<span data-ttu-id="f7332-162">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span><span class="sxs-lookup"><span data-stu-id="f7332-162">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="f7332-163">A storage account can contain any number of containers.</span><span class="sxs-lookup"><span data-stu-id="f7332-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="f7332-164">Create a container with [az storage container create](/cli/azure/storage/container#az_storage_container_create).</span><span class="sxs-lookup"><span data-stu-id="f7332-164">Create a container with [az storage container create](/cli/azure/storage/container#az_storage_container_create).</span></span>

<span data-ttu-id="f7332-165">The following example creates a container named *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="f7332-165">The following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-the-vhd"></a><span data-ttu-id="f7332-166">Upload the VHD</span><span class="sxs-lookup"><span data-stu-id="f7332-166">Upload the VHD</span></span>
<span data-ttu-id="f7332-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#az_storage_blob_upload).</span><span class="sxs-lookup"><span data-stu-id="f7332-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#az_storage_blob_upload).</span></span> <span data-ttu-id="f7332-168">You upload and store your custom disk as a page blob.</span><span class="sxs-lookup"><span data-stu-id="f7332-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="f7332-169">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span><span class="sxs-lookup"><span data-stu-id="f7332-169">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="f7332-170">Uploading the VHD may take a while.</span><span class="sxs-lookup"><span data-stu-id="f7332-170">Uploading the VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="f7332-171">Create a managed disk</span><span class="sxs-lookup"><span data-stu-id="f7332-171">Create a managed disk</span></span>


<span data-ttu-id="f7332-172">Create a managed disk from the VHD using [az disk create](/cli/azure/disk#az_disk_create).</span><span class="sxs-lookup"><span data-stu-id="f7332-172">Create a managed disk from the VHD using [az disk create](/cli/azure/disk#az_disk_create).</span></span> <span data-ttu-id="f7332-173">The following example creates a managed disk named *myManagedDisk* from the VHD you uploaded to your named storage account and container:</span><span class="sxs-lookup"><span data-stu-id="f7332-173">The following example creates a managed disk named *myManagedDisk* from the VHD you uploaded to your named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="f7332-174">Option 2: Copy an existing VM</span><span class="sxs-lookup"><span data-stu-id="f7332-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="f7332-175">You can also create the customized VM in Azure and then copy the OS disk and attach it to a new VM to create another copy.</span><span class="sxs-lookup"><span data-stu-id="f7332-175">You can also create the customized VM in Azure and then copy the OS disk and attach it to a new VM to create another copy.</span></span> <span data-ttu-id="f7332-176">This is fine for testing, but if you want to use an existing Azure VM as the model for multiple new VMs, you really should create an **image** instead.</span><span class="sxs-lookup"><span data-stu-id="f7332-176">This is fine for testing, but if you want to use an existing Azure VM as the model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="f7332-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="f7332-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="f7332-178">Create a snapshot</span><span class="sxs-lookup"><span data-stu-id="f7332-178">Create a snapshot</span></span>

<span data-ttu-id="f7332-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="f7332-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-the-managed-disk"></a><span data-ttu-id="f7332-180">Create the managed disk</span><span class="sxs-lookup"><span data-stu-id="f7332-180">Create the managed disk</span></span>

<span data-ttu-id="f7332-181">Create a new managed disk from the snapshot.</span><span class="sxs-lookup"><span data-stu-id="f7332-181">Create a new managed disk from the snapshot.</span></span>

<span data-ttu-id="f7332-182">Get the ID of the snapshot.</span><span class="sxs-lookup"><span data-stu-id="f7332-182">Get the ID of the snapshot.</span></span> <span data-ttu-id="f7332-183">In this example, the snapshot is named *osDiskSnapshot* and it is in the *myResourceGroup* resource group.</span><span class="sxs-lookup"><span data-stu-id="f7332-183">In this example, the snapshot is named *osDiskSnapshot* and it is in the *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="f7332-184">Create the managed disk.</span><span class="sxs-lookup"><span data-stu-id="f7332-184">Create the managed disk.</span></span> <span data-ttu-id="f7332-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span><span class="sxs-lookup"><span data-stu-id="f7332-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-the-vm"></a><span data-ttu-id="f7332-186">Create the VM</span><span class="sxs-lookup"><span data-stu-id="f7332-186">Create the VM</span></span>

<span data-ttu-id="f7332-187">Now, create your VM with [az vm create](/cli/azure/vm#az_vm_create) and attach (--attach-os-disk) the managed disk as the OS disk.</span><span class="sxs-lookup"><span data-stu-id="f7332-187">Now, create your VM with [az vm create](/cli/azure/vm#az_vm_create) and attach (--attach-os-disk) the managed disk as the OS disk.</span></span> <span data-ttu-id="f7332-188">The following example creates a VM named *myNewVM* using the managed disk created from your uploaded VHD:</span><span class="sxs-lookup"><span data-stu-id="f7332-188">The following example creates a VM named *myNewVM* using the managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="f7332-189">You should be able to SSH into the VM using the credentials from the source VM.</span><span class="sxs-lookup"><span data-stu-id="f7332-189">You should be able to SSH into the VM using the credentials from the source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f7332-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7332-190">Next steps</span></span>
<span data-ttu-id="f7332-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7332-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f7332-192">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span><span class="sxs-lookup"><span data-stu-id="f7332-192">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="f7332-193">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7332-193">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

