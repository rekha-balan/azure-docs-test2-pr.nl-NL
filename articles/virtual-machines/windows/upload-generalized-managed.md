---
title: Create a managed Azure VM from a generalized on-premises VHDs | Microsoft Docs
description: Create a managed VM in Azure using VHDs uploaded from on-premises and use managed disks, in the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: cynthn
ms.openlocfilehash: 3bf86fc5dd49bb5de7fff42129d3606b45eff42e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550988"
---
# <a name="create-a-new-vm-from-a-generalized-vhd-uploaded-to-azure-using-managed-disks"></a><span data-ttu-id="68ea5-103">Create a new VM from a generalized VHD uploaded to Azure using Managed Disks</span><span class="sxs-lookup"><span data-stu-id="68ea5-103">Create a new VM from a generalized VHD uploaded to Azure using Managed Disks</span></span>

<span data-ttu-id="68ea5-104">You can create a new VM in Azure by uploading a VHD exported from an on-premises virtualization tool or from another cloud.</span><span class="sxs-lookup"><span data-stu-id="68ea5-104">You can create a new VM in Azure by uploading a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="68ea5-105">Using [Managed Disks](../../storage/storage-managed-disks-overview.md) for the new VM simplifies the VM managment and provides better availability when the VM is placed in an availability set.</span><span class="sxs-lookup"><span data-stu-id="68ea5-105">Using [Managed Disks](../../storage/storage-managed-disks-overview.md) for the new VM simplifies the VM managment and provides better availability when the VM is placed in an availability set.</span></span> <span data-ttu-id="68ea5-106">If you are uploading a VHD that will be used to create multiple Azure VMs, you must first generalize VHD using [Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68ea5-106">If you are uploading a VHD that will be used to create multiple Azure VMs, you must first generalize VHD using [Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="68ea5-107">Sysprep removes any machine-specific information and personal account information from the VHD.</span><span class="sxs-lookup"><span data-stu-id="68ea5-107">Sysprep removes any machine-specific information and personal account information from the VHD.</span></span> 

<span data-ttu-id="68ea5-108">Azure managed disks removes the need of managing [storage accounts](../../storage/storage-introduction.md) for Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="68ea5-108">Azure managed disks removes the need of managing [storage accounts](../../storage/storage-introduction.md) for Azure VMs.</span></span> <span data-ttu-id="68ea5-109">You only have specify the type [Premium](../../storage/storage-premium-storage-performance.md) or [Standard](../../storage/storage-standard-storage.md) and size of disk you need, and Azure will create and manage the disk for you.</span><span class="sxs-lookup"><span data-stu-id="68ea5-109">You only have specify the type [Premium](../../storage/storage-premium-storage-performance.md) or [Standard](../../storage/storage-standard-storage.md) and size of disk you need, and Azure will create and manage the disk for you.</span></span> 


> [!IMPORTANT]
> <span data-ttu-id="68ea5-110">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration to [Managed Disks](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68ea5-110">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration to [Managed Disks](../../storage/storage-managed-disks-overview.md).</span></span>
>
> <span data-ttu-id="68ea5-111">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="68ea5-111">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
>
>

## <a name="before-you-begin"></a><span data-ttu-id="68ea5-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="68ea5-112">Before you begin</span></span>
<span data-ttu-id="68ea5-113">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="68ea5-113">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="68ea5-114">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="68ea5-114">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="68ea5-115">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="68ea5-115">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="68ea5-116">Generalize the Windows VM using Sysprep</span><span class="sxs-lookup"><span data-stu-id="68ea5-116">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="68ea5-117">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span><span class="sxs-lookup"><span data-stu-id="68ea5-117">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="68ea5-118">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="68ea5-118">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="68ea5-119">Make sure the server roles running on the machine are supported by Sysprep.</span><span class="sxs-lookup"><span data-stu-id="68ea5-119">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="68ea5-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="68ea5-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68ea5-121">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span><span class="sxs-lookup"><span data-stu-id="68ea5-121">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="68ea5-122">Sign in to the Windows virtual machine.</span><span class="sxs-lookup"><span data-stu-id="68ea5-122">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="68ea5-123">Open the Command Prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="68ea5-123">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="68ea5-124">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="68ea5-124">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="68ea5-125">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="68ea5-125">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="68ea5-126">In **Shutdown Options**, select **Shutdown**.</span><span class="sxs-lookup"><span data-stu-id="68ea5-126">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="68ea5-127">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="68ea5-127">Click **OK**.</span></span>
   
    ![Start Sysprep](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="68ea5-129">When Sysprep completes, it shuts down the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="68ea5-129">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="68ea5-130">Do not restart the VM.</span><span class="sxs-lookup"><span data-stu-id="68ea5-130">Do not restart the VM.</span></span>



## <a name="log-in-to-azure"></a><span data-ttu-id="68ea5-131">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="68ea5-131">Log in to Azure</span></span>
<span data-ttu-id="68ea5-132">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="68ea5-132">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

1. <span data-ttu-id="68ea5-133">Open Azure PowerShell and sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="68ea5-133">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="68ea5-134">A pop-up window opens for you to enter your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="68ea5-134">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="68ea5-135">Get the subscription IDs for your available subscriptions.</span><span class="sxs-lookup"><span data-stu-id="68ea5-135">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="68ea5-136">Set the correct subscription using the subscription ID.</span><span class="sxs-lookup"><span data-stu-id="68ea5-136">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="68ea5-137">Replace `<subscriptionID>` with the ID of the correct subscription.</span><span class="sxs-lookup"><span data-stu-id="68ea5-137">Replace `<subscriptionID>` with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="68ea5-138">Get the storage account</span><span class="sxs-lookup"><span data-stu-id="68ea5-138">Get the storage account</span></span>
<span data-ttu-id="68ea5-139">You need a storage account in Azure to store the uploaded VM image.</span><span class="sxs-lookup"><span data-stu-id="68ea5-139">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="68ea5-140">You can either use an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="68ea5-140">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="68ea5-141">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span><span class="sxs-lookup"><span data-stu-id="68ea5-141">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="68ea5-142">To show the available storage accounts, type:</span><span class="sxs-lookup"><span data-stu-id="68ea5-142">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="68ea5-143">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span><span class="sxs-lookup"><span data-stu-id="68ea5-143">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="68ea5-144">If you need to create a storage account, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="68ea5-144">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="68ea5-145">You need the name of the resource group where the storage account should be created.</span><span class="sxs-lookup"><span data-stu-id="68ea5-145">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="68ea5-146">To find out all the resource groups that are in your subscription, type:</span><span class="sxs-lookup"><span data-stu-id="68ea5-146">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="68ea5-147">To create a resource group named **myResourceGroup** in the **West US** region, type:</span><span class="sxs-lookup"><span data-stu-id="68ea5-147">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="68ea5-148">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="68ea5-148">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="68ea5-149">Valid values for -SkuName are:</span><span class="sxs-lookup"><span data-stu-id="68ea5-149">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="68ea5-150">**Standard_LRS** - Locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="68ea5-150">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="68ea5-151">**Standard_ZRS** - Zone redundant storage.</span><span class="sxs-lookup"><span data-stu-id="68ea5-151">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="68ea5-152">**Standard_GRS** - Geo redundant storage.</span><span class="sxs-lookup"><span data-stu-id="68ea5-152">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="68ea5-153">**Standard_RAGRS** - Read access geo redundant storage.</span><span class="sxs-lookup"><span data-stu-id="68ea5-153">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="68ea5-154">**Premium_LRS** - Premium locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="68ea5-154">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="68ea5-155">Upload the VHD to your storage account</span><span class="sxs-lookup"><span data-stu-id="68ea5-155">Upload the VHD to your storage account</span></span>

<span data-ttu-id="68ea5-156">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="68ea5-156">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="68ea5-157">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span><span class="sxs-lookup"><span data-stu-id="68ea5-157">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="68ea5-158">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="68ea5-158">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="68ea5-159">If successful, you get a response that looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="68ea5-159">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="68ea5-160">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span><span class="sxs-lookup"><span data-stu-id="68ea5-160">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="68ea5-161">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span><span class="sxs-lookup"><span data-stu-id="68ea5-161">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="68ea5-162">Other options for uploading a VHD</span><span class="sxs-lookup"><span data-stu-id="68ea5-162">Other options for uploading a VHD</span></span>

<span data-ttu-id="68ea5-163">You can also upload a VHD to your storage account using one of the following:</span><span class="sxs-lookup"><span data-stu-id="68ea5-163">You can also upload a VHD to your storage account using one of the following:</span></span>

-   [<span data-ttu-id="68ea5-164">Azure Storage Copy Blob API</span><span class="sxs-lookup"><span data-stu-id="68ea5-164">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)

-   [<span data-ttu-id="68ea5-165">Azure Storage Explorer Uploading Blobs</span><span class="sxs-lookup"><span data-stu-id="68ea5-165">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)

-   [<span data-ttu-id="68ea5-166">Storage Import/Export Service REST API Reference</span><span class="sxs-lookup"><span data-stu-id="68ea5-166">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

    <span data-ttu-id="68ea5-167">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span><span class="sxs-lookup"><span data-stu-id="68ea5-167">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="68ea5-168">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span><span class="sxs-lookup"><span data-stu-id="68ea5-168">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 

    <span data-ttu-id="68ea5-169">Import/Export can be used to copy to a standard storage account.</span><span class="sxs-lookup"><span data-stu-id="68ea5-169">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="68ea5-170">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span><span class="sxs-lookup"><span data-stu-id="68ea5-170">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>

## <a name="create-a-managed-image-from-the-uploaded-vhd"></a><span data-ttu-id="68ea5-171">Create a managed image from the uploaded VHD</span><span class="sxs-lookup"><span data-stu-id="68ea5-171">Create a managed image from the uploaded VHD</span></span> 

<span data-ttu-id="68ea5-172">Create a managed image using your generalized OS VHD.</span><span class="sxs-lookup"><span data-stu-id="68ea5-172">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="68ea5-173">First, set the common parameters:</span><span class="sxs-lookup"><span data-stu-id="68ea5-173">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```

4.  <span data-ttu-id="68ea5-174">Create the image using your generalized OS VHD.</span><span class="sxs-lookup"><span data-stu-id="68ea5-174">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="setup-some-variables-for-the-image"></a><span data-ttu-id="68ea5-175">Setup some variables for the image</span><span class="sxs-lookup"><span data-stu-id="68ea5-175">Setup some variables for the image</span></span>

<span data-ttu-id="68ea5-176">First we need to gather basic information about the image and create a variable for the image.</span><span class="sxs-lookup"><span data-stu-id="68ea5-176">First we need to gather basic information about the image and create a variable for the image.</span></span> <span data-ttu-id="68ea5-177">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span><span class="sxs-lookup"><span data-stu-id="68ea5-177">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="68ea5-178">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="68ea5-178">Create a virtual network</span></span>
<span data-ttu-id="68ea5-179">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68ea5-179">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="68ea5-180">Create the subnet.</span><span class="sxs-lookup"><span data-stu-id="68ea5-180">Create the subnet.</span></span> <span data-ttu-id="68ea5-181">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="68ea5-181">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="68ea5-182">Create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="68ea5-182">Create the virtual network.</span></span> <span data-ttu-id="68ea5-183">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="68ea5-183">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="68ea5-184">Create a public IP address and network interface</span><span class="sxs-lookup"><span data-stu-id="68ea5-184">Create a public IP address and network interface</span></span>

<span data-ttu-id="68ea5-185">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span><span class="sxs-lookup"><span data-stu-id="68ea5-185">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="68ea5-186">Create a public IP address.</span><span class="sxs-lookup"><span data-stu-id="68ea5-186">Create a public IP address.</span></span> <span data-ttu-id="68ea5-187">This example creates a public IP address named **myPip**.</span><span class="sxs-lookup"><span data-stu-id="68ea5-187">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="68ea5-188">Create the NIC.</span><span class="sxs-lookup"><span data-stu-id="68ea5-188">Create the NIC.</span></span> <span data-ttu-id="68ea5-189">This example creates a NIC named **myNic**.</span><span class="sxs-lookup"><span data-stu-id="68ea5-189">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="68ea5-190">Create the network security group and an RDP rule</span><span class="sxs-lookup"><span data-stu-id="68ea5-190">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="68ea5-191">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span><span class="sxs-lookup"><span data-stu-id="68ea5-191">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="68ea5-192">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span><span class="sxs-lookup"><span data-stu-id="68ea5-192">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="68ea5-193">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68ea5-193">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="68ea5-194">Create a variable for the virtual network</span><span class="sxs-lookup"><span data-stu-id="68ea5-194">Create a variable for the virtual network</span></span>

<span data-ttu-id="68ea5-195">Create a variable for the completed virtual network.</span><span class="sxs-lookup"><span data-stu-id="68ea5-195">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="68ea5-196">Get the credentials for the VM</span><span class="sxs-lookup"><span data-stu-id="68ea5-196">Get the credentials for the VM</span></span>

<span data-ttu-id="68ea5-197">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span><span class="sxs-lookup"><span data-stu-id="68ea5-197">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-the-vm-name-computer-name-and-the-size-of-the-vm"></a><span data-ttu-id="68ea5-198">Set variables for the VM name, computer name and the size of the VM</span><span class="sxs-lookup"><span data-stu-id="68ea5-198">Set variables for the VM name, computer name and the size of the VM</span></span>

1. <span data-ttu-id="68ea5-199">Create variables for the VM name and computer name.</span><span class="sxs-lookup"><span data-stu-id="68ea5-199">Create variables for the VM name and computer name.</span></span> <span data-ttu-id="68ea5-200">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span><span class="sxs-lookup"><span data-stu-id="68ea5-200">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="68ea5-201">Set the size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="68ea5-201">Set the size of the virtual machine.</span></span> <span data-ttu-id="68ea5-202">This example creates **Standard_DS1_v2** sized VM.</span><span class="sxs-lookup"><span data-stu-id="68ea5-202">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="68ea5-203">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span><span class="sxs-lookup"><span data-stu-id="68ea5-203">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="68ea5-204">Add the VM name and size to the VM configuration.</span><span class="sxs-lookup"><span data-stu-id="68ea5-204">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="68ea5-205">Set the VM image as source image for the new VM</span><span class="sxs-lookup"><span data-stu-id="68ea5-205">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="68ea5-206">Set the source image using the ID of the managed VM image.</span><span class="sxs-lookup"><span data-stu-id="68ea5-206">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="68ea5-207">Set the OS configuration and add the NIC.</span><span class="sxs-lookup"><span data-stu-id="68ea5-207">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="68ea5-208">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span><span class="sxs-lookup"><span data-stu-id="68ea5-208">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="68ea5-209">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="68ea5-209">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -ManagedDiskStorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="68ea5-210">Create the VM</span><span class="sxs-lookup"><span data-stu-id="68ea5-210">Create the VM</span></span>

<span data-ttu-id="68ea5-211">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span><span class="sxs-lookup"><span data-stu-id="68ea5-211">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="68ea5-212">Verify that the VM was created</span><span class="sxs-lookup"><span data-stu-id="68ea5-212">Verify that the VM was created</span></span>
<span data-ttu-id="68ea5-213">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="68ea5-213">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="68ea5-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="68ea5-214">Next steps</span></span>

<span data-ttu-id="68ea5-215">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span><span class="sxs-lookup"><span data-stu-id="68ea5-215">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="68ea5-216">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="68ea5-216">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="68ea5-217">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68ea5-217">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


