---
title: Upload a custom Linux image with Azure CLI 1.0 | Microsoft Docs
description: Create and upload a virtual hard disk (VHD) to Azure with a custom Linux image using the Resource Manager deployment model and the Azure CLI 1.0.
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
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: cd63f91e1ce43dec8acf2b7ec037e9c45355115e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663067"
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-the-azure-cli-10"></a><span data-ttu-id="955b3-103">Upload and create a Linux VM from custom disk image by using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="955b3-103">Upload and create a Linux VM from custom disk image by using the Azure CLI 1.0</span></span>
<span data-ttu-id="955b3-104">This article shows you how to upload a virtual hard disk (VHD) to Azure using the Resource Manager deployment model and create Linux VMs from this custom image.</span><span class="sxs-lookup"><span data-stu-id="955b3-104">This article shows you how to upload a virtual hard disk (VHD) to Azure using the Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="955b3-105">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="955b3-105">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="955b3-106">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="955b3-106">CLI versions to complete the task</span></span>
<span data-ttu-id="955b3-107">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="955b3-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="955b3-108">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="955b3-108">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="955b3-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="955b3-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="955b3-110">Quick commands</span><span class="sxs-lookup"><span data-stu-id="955b3-110">Quick commands</span></span>
<span data-ttu-id="955b3-111">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span><span class="sxs-lookup"><span data-stu-id="955b3-111">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="955b3-112">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span><span class="sxs-lookup"><span data-stu-id="955b3-112">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="955b3-113">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="955b3-113">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="955b3-114">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="955b3-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="955b3-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span><span class="sxs-lookup"><span data-stu-id="955b3-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="955b3-116">First, create a resource group.</span><span class="sxs-lookup"><span data-stu-id="955b3-116">First, create a resource group.</span></span> <span data-ttu-id="955b3-117">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span><span class="sxs-lookup"><span data-stu-id="955b3-117">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="955b3-118">Create a storage account to hold your virtual disks.</span><span class="sxs-lookup"><span data-stu-id="955b3-118">Create a storage account to hold your virtual disks.</span></span> <span data-ttu-id="955b3-119">The following example creates a storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="955b3-119">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="955b3-120">List the access keys for your storage account.</span><span class="sxs-lookup"><span data-stu-id="955b3-120">List the access keys for your storage account.</span></span> <span data-ttu-id="955b3-121">Make a note of `key1`:</span><span class="sxs-lookup"><span data-stu-id="955b3-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="955b3-122">Create a container within your storage account using the storage key you obtained.</span><span class="sxs-lookup"><span data-stu-id="955b3-122">Create a container within your storage account using the storage key you obtained.</span></span> <span data-ttu-id="955b3-123">The following example creates a container named `myimages` using the storage key value from `key1`:</span><span class="sxs-lookup"><span data-stu-id="955b3-123">The following example creates a container named `myimages` using the storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="955b3-124">Finally, upload your VHD to the container you created.</span><span class="sxs-lookup"><span data-stu-id="955b3-124">Finally, upload your VHD to the container you created.</span></span> <span data-ttu-id="955b3-125">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="955b3-125">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="955b3-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="955b3-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="955b3-127">You can also use the CLI by specifying the URI to your disk (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="955b3-127">You can also use the CLI by specifying the URI to your disk (`--image-urn`).</span></span> <span data-ttu-id="955b3-128">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span><span class="sxs-lookup"><span data-stu-id="955b3-128">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="955b3-129">The destination storage account has to be the same as where you uploaded your virtual disk to.</span><span class="sxs-lookup"><span data-stu-id="955b3-129">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="955b3-130">You also need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span><span class="sxs-lookup"><span data-stu-id="955b3-130">You also need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="955b3-131">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="955b3-131">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="955b3-132">Requirements</span><span class="sxs-lookup"><span data-stu-id="955b3-132">Requirements</span></span>
<span data-ttu-id="955b3-133">To complete the following steps, you need:</span><span class="sxs-lookup"><span data-stu-id="955b3-133">To complete the following steps, you need:</span></span>

* <span data-ttu-id="955b3-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span><span class="sxs-lookup"><span data-stu-id="955b3-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="955b3-135">Multiple tools exist to create a VM and VHD:</span><span class="sxs-lookup"><span data-stu-id="955b3-135">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="955b3-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span><span class="sxs-lookup"><span data-stu-id="955b3-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="955b3-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="955b3-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="955b3-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="955b3-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="955b3-139">The newer VHDX format is not supported in Azure.</span><span class="sxs-lookup"><span data-stu-id="955b3-139">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="955b3-140">When you create a VM, specify VHD as the format.</span><span class="sxs-lookup"><span data-stu-id="955b3-140">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="955b3-141">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="955b3-141">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="955b3-142">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span><span class="sxs-lookup"><span data-stu-id="955b3-142">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="955b3-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span><span class="sxs-lookup"><span data-stu-id="955b3-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="955b3-144">VMs created from your custom image must reside in the same storage account as the image itself</span><span class="sxs-lookup"><span data-stu-id="955b3-144">VMs created from your custom image must reside in the same storage account as the image itself</span></span>
  * <span data-ttu-id="955b3-145">Create a storage account and container to hold both your custom image and created VMs</span><span class="sxs-lookup"><span data-stu-id="955b3-145">Create a storage account and container to hold both your custom image and created VMs</span></span>
  * <span data-ttu-id="955b3-146">After you have created all your VMs, you can safely delete your image</span><span class="sxs-lookup"><span data-stu-id="955b3-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="955b3-147">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="955b3-147">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="955b3-148">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="955b3-148">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="955b3-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span><span class="sxs-lookup"><span data-stu-id="955b3-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="955b3-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="955b3-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-image-to-be-uploaded"></a><span data-ttu-id="955b3-151">Prepare the image to be uploaded</span><span class="sxs-lookup"><span data-stu-id="955b3-151">Prepare the image to be uploaded</span></span>
<span data-ttu-id="955b3-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="955b3-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="955b3-153">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span><span class="sxs-lookup"><span data-stu-id="955b3-153">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="955b3-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="955b3-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="955b3-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="955b3-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="955b3-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="955b3-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="955b3-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="955b3-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="955b3-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="955b3-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="955b3-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="955b3-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="955b3-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="955b3-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="955b3-161">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span><span class="sxs-lookup"><span data-stu-id="955b3-161">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="955b3-162">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="955b3-162">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="955b3-163">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="955b3-163">Create a resource group</span></span>
<span data-ttu-id="955b3-164">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span><span class="sxs-lookup"><span data-stu-id="955b3-164">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="955b3-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="955b3-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="955b3-166">Before uploading your custom disk image and creating VMs, you first need to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="955b3-166">Before uploading your custom disk image and creating VMs, you first need to create a resource group.</span></span> 

<span data-ttu-id="955b3-167">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span><span class="sxs-lookup"><span data-stu-id="955b3-167">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="955b3-168">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="955b3-168">Create a storage account</span></span>
<span data-ttu-id="955b3-169">VMs are stored as page blobs within a storage account.</span><span class="sxs-lookup"><span data-stu-id="955b3-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="955b3-170">Read more about [Azure blob storage here](../../storage/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="955b3-170">Read more about [Azure blob storage here](../../storage/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="955b3-171">You create a storage account for your custom disk image and VMs.</span><span class="sxs-lookup"><span data-stu-id="955b3-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="955b3-172">Any VMs that you create from your custom disk image need to be in the same storage account as that image.</span><span class="sxs-lookup"><span data-stu-id="955b3-172">Any VMs that you create from your custom disk image need to be in the same storage account as that image.</span></span>

<span data-ttu-id="955b3-173">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span><span class="sxs-lookup"><span data-stu-id="955b3-173">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="955b3-174">List storage account keys</span><span class="sxs-lookup"><span data-stu-id="955b3-174">List storage account keys</span></span>
<span data-ttu-id="955b3-175">Azure generates two 512-bit access keys for each storage account.</span><span class="sxs-lookup"><span data-stu-id="955b3-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="955b3-176">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span><span class="sxs-lookup"><span data-stu-id="955b3-176">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="955b3-177">Read more about [managing access to storage here](../../storage/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="955b3-177">Read more about [managing access to storage here](../../storage/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="955b3-178">You can view access keys with the `azure storage account keys list` command.</span><span class="sxs-lookup"><span data-stu-id="955b3-178">You can view access keys with the `azure storage account keys list` command.</span></span>

<span data-ttu-id="955b3-179">View the access keys for the storage account you created:</span><span class="sxs-lookup"><span data-stu-id="955b3-179">View the access keys for the storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="955b3-180">The output is similar to:</span><span class="sxs-lookup"><span data-stu-id="955b3-180">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="955b3-181">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span><span class="sxs-lookup"><span data-stu-id="955b3-181">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="955b3-182">Create a storage container</span><span class="sxs-lookup"><span data-stu-id="955b3-182">Create a storage container</span></span>
<span data-ttu-id="955b3-183">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your virtual disks and images.</span><span class="sxs-lookup"><span data-stu-id="955b3-183">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your virtual disks and images.</span></span> <span data-ttu-id="955b3-184">A storage account can contain any number of containers.</span><span class="sxs-lookup"><span data-stu-id="955b3-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="955b3-185">The following example creates a container named `myimages`, specifying the access key obtained in the previous step (`key1`):</span><span class="sxs-lookup"><span data-stu-id="955b3-185">The following example creates a container named `myimages`, specifying the access key obtained in the previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="955b3-186">Upload VHD</span><span class="sxs-lookup"><span data-stu-id="955b3-186">Upload VHD</span></span>
<span data-ttu-id="955b3-187">Now you can actually upload your custom disk image.</span><span class="sxs-lookup"><span data-stu-id="955b3-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="955b3-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span><span class="sxs-lookup"><span data-stu-id="955b3-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="955b3-189">Specify your access key, the container you created in the previous step, and then the path to the custom disk image on your local computer:</span><span class="sxs-lookup"><span data-stu-id="955b3-189">Specify your access key, the container you created in the previous step, and then the path to the custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="955b3-190">Create VM from custom image</span><span class="sxs-lookup"><span data-stu-id="955b3-190">Create VM from custom image</span></span>
<span data-ttu-id="955b3-191">When you create VMs from your custom disk image, specify the URI to the disk image.</span><span class="sxs-lookup"><span data-stu-id="955b3-191">When you create VMs from your custom disk image, specify the URI to the disk image.</span></span> <span data-ttu-id="955b3-192">Ensure that the destination storage account matches where your custom disk image is stored.</span><span class="sxs-lookup"><span data-stu-id="955b3-192">Ensure that the destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="955b3-193">You can create your VM using the Azure CLI or Resource Manager JSON template.</span><span class="sxs-lookup"><span data-stu-id="955b3-193">You can create your VM using the Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-the-azure-cli"></a><span data-ttu-id="955b3-194">Create a VM using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="955b3-194">Create a VM using the Azure CLI</span></span>
<span data-ttu-id="955b3-195">You specify the `--image-urn` parameter with the `azure vm create` command to point to your custom disk image.</span><span class="sxs-lookup"><span data-stu-id="955b3-195">You specify the `--image-urn` parameter with the `azure vm create` command to point to your custom disk image.</span></span> <span data-ttu-id="955b3-196">Ensure that `--storage-account-name` matches the storage account where your custom disk image is stored.</span><span class="sxs-lookup"><span data-stu-id="955b3-196">Ensure that `--storage-account-name` matches the storage account where your custom disk image is stored.</span></span> <span data-ttu-id="955b3-197">You do not have to use the same container as the custom disk image to store your VMs.</span><span class="sxs-lookup"><span data-stu-id="955b3-197">You do not have to use the same container as the custom disk image to store your VMs.</span></span> <span data-ttu-id="955b3-198">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk images.</span><span class="sxs-lookup"><span data-stu-id="955b3-198">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="955b3-199">The following example creates a VM named `myVM` from your custom disk image:</span><span class="sxs-lookup"><span data-stu-id="955b3-199">The following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="955b3-200">You still need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span><span class="sxs-lookup"><span data-stu-id="955b3-200">You still need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="955b3-201">Read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="955b3-201">Read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="955b3-202">Create a VM using a JSON template</span><span class="sxs-lookup"><span data-stu-id="955b3-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="955b3-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span><span class="sxs-lookup"><span data-stu-id="955b3-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="955b3-204">The templates are broken down in to different resource providers such as compute or network.</span><span class="sxs-lookup"><span data-stu-id="955b3-204">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="955b3-205">You can use existing templates or write your own.</span><span class="sxs-lookup"><span data-stu-id="955b3-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="955b3-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="955b3-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="955b3-207">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span><span class="sxs-lookup"><span data-stu-id="955b3-207">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="955b3-208">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk image and your new VM's virtual disk.</span><span class="sxs-lookup"><span data-stu-id="955b3-208">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="955b3-209">The following shows an example of the JSON for using a custom disk image:</span><span class="sxs-lookup"><span data-stu-id="955b3-209">The following shows an example of the JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="955b3-210">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="955b3-210">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="955b3-211">Once you have a template configured, you create your VMs using the `azure group deployment create` command.</span><span class="sxs-lookup"><span data-stu-id="955b3-211">Once you have a template configured, you create your VMs using the `azure group deployment create` command.</span></span> <span data-ttu-id="955b3-212">Specify the URI of your JSON template with the `--template-uri` parameter:</span><span class="sxs-lookup"><span data-stu-id="955b3-212">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="955b3-213">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span><span class="sxs-lookup"><span data-stu-id="955b3-213">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="955b3-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="955b3-214">Next steps</span></span>
<span data-ttu-id="955b3-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="955b3-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="955b3-216">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span><span class="sxs-lookup"><span data-stu-id="955b3-216">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="955b3-217">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="955b3-217">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

