---
title: Create and upload a Linux VHD to Azure | Microsoft Docs
description: Create and upload an Azure virtual hard disk (VHD) that contains the Linux operating system using the Classic deployment model
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 8bb0357a1ac2effd1144afd2af1741205592d253
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554146"
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-the-linux-operating-system"></a><span data-ttu-id="d4914-103">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span><span class="sxs-lookup"><span data-stu-id="d4914-103">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d4914-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d4914-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d4914-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="d4914-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d4914-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="d4914-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="d4914-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4914-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d4914-108">This article shows you how to create and upload a virtual hard disk (VHD) so you can use it as your own image to create virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="d4914-108">This article shows you how to create and upload a virtual hard disk (VHD) so you can use it as your own image to create virtual machines in Azure.</span></span> <span data-ttu-id="d4914-109">Learn how to prepare the operating system so you can use it to create multiple virtual machines based on that image.</span><span class="sxs-lookup"><span data-stu-id="d4914-109">Learn how to prepare the operating system so you can use it to create multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="d4914-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d4914-110">Prerequisites</span></span>
<span data-ttu-id="d4914-111">This article assumes that you have the following items:</span><span class="sxs-lookup"><span data-stu-id="d4914-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="d4914-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span><span class="sxs-lookup"><span data-stu-id="d4914-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="d4914-113">Multiple tools exist to create a VM and VHD:</span><span class="sxs-lookup"><span data-stu-id="d4914-113">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="d4914-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span><span class="sxs-lookup"><span data-stu-id="d4914-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="d4914-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="d4914-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="d4914-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4914-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="d4914-117">The newer VHDX format is not supported in Azure.</span><span class="sxs-lookup"><span data-stu-id="d4914-117">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="d4914-118">When you create a VM, specify VHD as the format.</span><span class="sxs-lookup"><span data-stu-id="d4914-118">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="d4914-119">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d4914-119">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="d4914-120">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span><span class="sxs-lookup"><span data-stu-id="d4914-120">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="d4914-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span><span class="sxs-lookup"><span data-stu-id="d4914-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>

* <span data-ttu-id="d4914-122">**Azure Command-line Interface** - Install the latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to upload the VHD.</span><span class="sxs-lookup"><span data-stu-id="d4914-122">**Azure Command-line Interface** - Install the latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to upload the VHD.</span></span>

<span data-ttu-id="d4914-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="d4914-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-the-image-to-be-uploaded"></a><span data-ttu-id="d4914-124">Step 1: Prepare the image to be uploaded</span><span class="sxs-lookup"><span data-stu-id="d4914-124">Step 1: Prepare the image to be uploaded</span></span>
<span data-ttu-id="d4914-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="d4914-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="d4914-126">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure.</span><span class="sxs-lookup"><span data-stu-id="d4914-126">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="d4914-127">After you complete the steps in the following guides, come back here once you have a VHD file that is ready to upload to Azure:</span><span class="sxs-lookup"><span data-stu-id="d4914-127">After you complete the steps in the following guides, come back here once you have a VHD file that is ready to upload to Azure:</span></span>

* <span data-ttu-id="d4914-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d4914-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d4914-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d4914-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d4914-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d4914-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d4914-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d4914-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d4914-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d4914-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d4914-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d4914-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="d4914-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="d4914-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="d4914-135">The Azure platform SLA applies to virtual machines running the Linux OS only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4914-135">The Azure platform SLA applies to virtual machines running the Linux OS only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d4914-136">All Linux distributions in the Azure image gallery are endorsed distributions with the required configuration.</span><span class="sxs-lookup"><span data-stu-id="d4914-136">All Linux distributions in the Azure image gallery are endorsed distributions with the required configuration.</span></span>
> 
> 

<span data-ttu-id="d4914-137">Also see the **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span><span class="sxs-lookup"><span data-stu-id="d4914-137">Also see the **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="d4914-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="d4914-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-the-connection-to-azure"></a><span data-ttu-id="d4914-139">Step 2: Prepare the connection to Azure</span><span class="sxs-lookup"><span data-stu-id="d4914-139">Step 2: Prepare the connection to Azure</span></span>
<span data-ttu-id="d4914-140">Make sure you are using the Azure CLI in the classic deployment model (`azure config mode asm`), then log in to your account:</span><span class="sxs-lookup"><span data-stu-id="d4914-140">Make sure you are using the Azure CLI in the classic deployment model (`azure config mode asm`), then log in to your account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="d4914-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="d4914-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-the-image-to-azure"></a><span data-ttu-id="d4914-142">Step 3: Upload the image to Azure</span><span class="sxs-lookup"><span data-stu-id="d4914-142">Step 3: Upload the image to Azure</span></span>
<span data-ttu-id="d4914-143">You need a storage account to upload your VHD file to.</span><span class="sxs-lookup"><span data-stu-id="d4914-143">You need a storage account to upload your VHD file to.</span></span> <span data-ttu-id="d4914-144">You can either pick an existing storage account or [create a new one](../../../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d4914-144">You can either pick an existing storage account or [create a new one](../../../storage/storage-create-storage-account.md).</span></span>

<span data-ttu-id="d4914-145">Use the Azure CLI to upload the image by using the following command:</span><span class="sxs-lookup"><span data-stu-id="d4914-145">Use the Azure CLI to upload the image by using the following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="d4914-146">In the previous example:</span><span class="sxs-lookup"><span data-stu-id="d4914-146">In the previous example:</span></span>

* <span data-ttu-id="d4914-147">**BlobStorageURL** is the URL for the storage account you plan to use</span><span class="sxs-lookup"><span data-stu-id="d4914-147">**BlobStorageURL** is the URL for the storage account you plan to use</span></span>
* <span data-ttu-id="d4914-148">**YourImagesFolder** is the container within blob storage where you want to store your images</span><span class="sxs-lookup"><span data-stu-id="d4914-148">**YourImagesFolder** is the container within blob storage where you want to store your images</span></span>
* <span data-ttu-id="d4914-149">**VHDName** is the label that appears in portal to identify the virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="d4914-149">**VHDName** is the label that appears in portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="d4914-150">**PathToVHDFile** is the full path and name of the .vhd file on your machine.</span><span class="sxs-lookup"><span data-stu-id="d4914-150">**PathToVHDFile** is the full path and name of the .vhd file on your machine.</span></span>

<span data-ttu-id="d4914-151">The following command shows a complete example:</span><span class="sxs-lookup"><span data-stu-id="d4914-151">The following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-the-image"></a><span data-ttu-id="d4914-152">Step 4: Create a VM from the image</span><span class="sxs-lookup"><span data-stu-id="d4914-152">Step 4: Create a VM from the image</span></span>
<span data-ttu-id="d4914-153">You create a VM using `azure vm create` in the same way as a regular VM.</span><span class="sxs-lookup"><span data-stu-id="d4914-153">You create a VM using `azure vm create` in the same way as a regular VM.</span></span> <span data-ttu-id="d4914-154">Specify the name you gave your image in the previous step.</span><span class="sxs-lookup"><span data-stu-id="d4914-154">Specify the name you gave your image in the previous step.</span></span> <span data-ttu-id="d4914-155">In the following example, we use the **myImage** image name given in the previous step:</span><span class="sxs-lookup"><span data-stu-id="d4914-155">In the following example, we use the **myImage** image name given in the previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="d4914-156">To create your own VMs, provide your own username + password, location, DNS name, and image name.</span><span class="sxs-lookup"><span data-stu-id="d4914-156">To create your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4914-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4914-157">Next steps</span></span>
<span data-ttu-id="d4914-158">For more information, see [Azure CLI reference for the Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="d4914-158">For more information, see [Azure CLI reference for the Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare the image to be uploaded]:#prepimage
[Step 2: Prepare the connection to Azure]:#connect
[Step 3: Upload the image to Azure]:#upload
