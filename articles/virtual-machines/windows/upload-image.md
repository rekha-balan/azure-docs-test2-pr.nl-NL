---
title: Upload a Windows VHD for Resource Manager | Microsoft Docs
description: Learn to upload a Windows virtual machine VHD from on-premises to Azure, using the Resource Manager deployment model. You can upload a VHD from either a generalized or a specialized VM.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 192c8e5a-3411-48fe-9fc3-526e0296cf4c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: cynthn
ms.openlocfilehash: 7393f395a1bf443ae77587f30004ff0aa5239e2e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549722"
---
# <a name="upload-a-windows-vhd-from-an-on-premises-vm-to-azure"></a><span data-ttu-id="8f46c-104">Upload a Windows VHD from an on-premises VM to Azure</span><span class="sxs-lookup"><span data-stu-id="8f46c-104">Upload a Windows VHD from an on-premises VM to Azure</span></span>
<span data-ttu-id="8f46c-105">This article shows you how to create and upload a Windows virtual hard disk (VHD) to be used in creating an Azure Vm.</span><span class="sxs-lookup"><span data-stu-id="8f46c-105">This article shows you how to create and upload a Windows virtual hard disk (VHD) to be used in creating an Azure Vm.</span></span> <span data-ttu-id="8f46c-106">You can upload a VHD from either a generalized VM or a specialized VM.</span><span class="sxs-lookup"><span data-stu-id="8f46c-106">You can upload a VHD from either a generalized VM or a specialized VM.</span></span> 

<span data-ttu-id="8f46c-107">For a complete walk-through of how to prepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded to Azure using Managed Disks](upload-generalized-managed.md) or [Upload a specialized VHD to create a VM in Azure](upload-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="8f46c-107">For a complete walk-through of how to prepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded to Azure using Managed Disks](upload-generalized-managed.md) or [Upload a specialized VHD to create a VM in Azure](upload-specialized.md).</span></span>

<span data-ttu-id="8f46c-108">For more details about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f46c-108">For more details about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="8f46c-109">Prepare the VM</span><span class="sxs-lookup"><span data-stu-id="8f46c-109">Prepare the VM</span></span>
<span data-ttu-id="8f46c-110">You can upload both generalized and specialized VHDs to Azure.</span><span class="sxs-lookup"><span data-stu-id="8f46c-110">You can upload both generalized and specialized VHDs to Azure.</span></span> <span data-ttu-id="8f46c-111">Each type requires that you prepare the VM before starting.</span><span class="sxs-lookup"><span data-stu-id="8f46c-111">Each type requires that you prepare the VM before starting.</span></span>

* <span data-ttu-id="8f46c-112">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span><span class="sxs-lookup"><span data-stu-id="8f46c-112">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="8f46c-113">If you intend to use the VHD as an image to create new VMs from, you should:</span><span class="sxs-lookup"><span data-stu-id="8f46c-113">If you intend to use the VHD as an image to create new VMs from, you should:</span></span>
  
  * <span data-ttu-id="8f46c-114">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f46c-114">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
  * <span data-ttu-id="8f46c-115">[Generalize the virtual machine using Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f46c-115">[Generalize the virtual machine using Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
* <span data-ttu-id="8f46c-116">**Specialized VHD** - a specialized VHD maintains the user accounts, applications and other state data from your original VM.</span><span class="sxs-lookup"><span data-stu-id="8f46c-116">**Specialized VHD** - a specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="8f46c-117">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span><span class="sxs-lookup"><span data-stu-id="8f46c-117">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="8f46c-118">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f46c-118">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8f46c-119">**Do not** generalize the VM using Sysprep.</span><span class="sxs-lookup"><span data-stu-id="8f46c-119">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="8f46c-120">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span><span class="sxs-lookup"><span data-stu-id="8f46c-120">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="8f46c-121">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span><span class="sxs-lookup"><span data-stu-id="8f46c-121">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="8f46c-122">This ensures that the server obtains an IP address within the VNet when it starts up.</span><span class="sxs-lookup"><span data-stu-id="8f46c-122">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="8f46c-123">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="8f46c-123">Log in to Azure</span></span>
<span data-ttu-id="8f46c-124">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8f46c-124">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

1. <span data-ttu-id="8f46c-125">Open Azure PowerShell and sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="8f46c-125">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="8f46c-126">A pop-up window opens for you to enter your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="8f46c-126">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="8f46c-127">Get the subscription IDs for your available subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8f46c-127">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="8f46c-128">Set the correct subscription using the subscription ID.</span><span class="sxs-lookup"><span data-stu-id="8f46c-128">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="8f46c-129">Replace `<subscriptionID>` with the ID of the correct subscription.</span><span class="sxs-lookup"><span data-stu-id="8f46c-129">Replace `<subscriptionID>` with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="8f46c-130">Get the storage account</span><span class="sxs-lookup"><span data-stu-id="8f46c-130">Get the storage account</span></span>
<span data-ttu-id="8f46c-131">You need a storage account in Azure to store the uploaded VM image.</span><span class="sxs-lookup"><span data-stu-id="8f46c-131">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="8f46c-132">You can either use an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="8f46c-132">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="8f46c-133">To show the available storage accounts, type:</span><span class="sxs-lookup"><span data-stu-id="8f46c-133">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="8f46c-134">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span><span class="sxs-lookup"><span data-stu-id="8f46c-134">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="8f46c-135">If you need to create a storage account, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8f46c-135">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="8f46c-136">You need the name of the resource group where the storage account should be created.</span><span class="sxs-lookup"><span data-stu-id="8f46c-136">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="8f46c-137">To find out all the resource groups that are in your subscription, type:</span><span class="sxs-lookup"><span data-stu-id="8f46c-137">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="8f46c-138">To create a resource group named **myResourceGroup** in the **West US** region, type:</span><span class="sxs-lookup"><span data-stu-id="8f46c-138">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="8f46c-139">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8f46c-139">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="8f46c-140">Valid values for -SkuName are:</span><span class="sxs-lookup"><span data-stu-id="8f46c-140">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="8f46c-141">**Standard_LRS** - Locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="8f46c-141">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="8f46c-142">**Standard_ZRS** - Zone redundant storage.</span><span class="sxs-lookup"><span data-stu-id="8f46c-142">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="8f46c-143">**Standard_GRS** - Geo redundant storage.</span><span class="sxs-lookup"><span data-stu-id="8f46c-143">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="8f46c-144">**Standard_RAGRS** - Read access geo redundant storage.</span><span class="sxs-lookup"><span data-stu-id="8f46c-144">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="8f46c-145">**Premium_LRS** - Premium locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="8f46c-145">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="8f46c-146">Upload the VHD to your storage account</span><span class="sxs-lookup"><span data-stu-id="8f46c-146">Upload the VHD to your storage account</span></span>
<span data-ttu-id="8f46c-147">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the image to a container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="8f46c-147">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="8f46c-148">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span><span class="sxs-lookup"><span data-stu-id="8f46c-148">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="8f46c-149">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="8f46c-149">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="8f46c-150">If successful, you get a response that looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="8f46c-150">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="8f46c-151">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span><span class="sxs-lookup"><span data-stu-id="8f46c-151">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f46c-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f46c-152">Next steps</span></span>
* [<span data-ttu-id="8f46c-153">Create a VM in Azure from a generalized VHD</span><span class="sxs-lookup"><span data-stu-id="8f46c-153">Create a VM in Azure from a generalized VHD</span></span>](create-vm-generalized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="8f46c-154">[Create a VM in Azure from a specialized VHD](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) by attaching it as an OS disk when you create a new VM.</span><span class="sxs-lookup"><span data-stu-id="8f46c-154">[Create a VM in Azure from a specialized VHD](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) by attaching it as an OS disk when you create a new VM.</span></span>

