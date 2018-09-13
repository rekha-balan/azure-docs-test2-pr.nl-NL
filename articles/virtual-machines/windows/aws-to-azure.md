---
title: Migrate AWS VMs to Azure | Microsoft Docs
description: Migrate an Amazon Web Services (AWS) EC2 instance to Azure Virtual Machines. This scenario uses Managed Disks to simplify your cloud storage.
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
ms.openlocfilehash: 44060766da6d3004a18611e41c5c81e8c4e2b417
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540781"
---
# <a name="migrate-from-amazon-web-services-aws-to-azure-managed-disks"></a><span data-ttu-id="98499-104">Migrate from Amazon Web Services (AWS) to Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="98499-104">Migrate from Amazon Web Services (AWS) to Azure Managed Disks</span></span>

<span data-ttu-id="98499-105">You can migrate an Amazon Web Services (AWS) EC2 instance to Azure by uploading the VHD.</span><span class="sxs-lookup"><span data-stu-id="98499-105">You can migrate an Amazon Web Services (AWS) EC2 instance to Azure by uploading the VHD.</span></span> <span data-ttu-id="98499-106">If you want to create multiple VMs in Azure from the same image, you must first generalize the VM and then export the generalized VHD to a local directory.</span><span class="sxs-lookup"><span data-stu-id="98499-106">If you want to create multiple VMs in Azure from the same image, you must first generalize the VM and then export the generalized VHD to a local directory.</span></span> <span data-ttu-id="98499-107">Once the VHD is uploaded, you can create a new Azure VM that uses [Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for storage.</span><span class="sxs-lookup"><span data-stu-id="98499-107">Once the VHD is uploaded, you can create a new Azure VM that uses [Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for storage.</span></span> <span data-ttu-id="98499-108">Azure Managed Disks removes the need to manage storage accounts for Azure IaaS VMs.</span><span class="sxs-lookup"><span data-stu-id="98499-108">Azure Managed Disks removes the need to manage storage accounts for Azure IaaS VMs.</span></span> <span data-ttu-id="98499-109">You have to only specify the type (Premium or Standard) and size of disk you need, and Azure will create and manage the disk for you.</span><span class="sxs-lookup"><span data-stu-id="98499-109">You have to only specify the type (Premium or Standard) and size of disk you need, and Azure will create and manage the disk for you.</span></span> 

<span data-ttu-id="98499-110">Before starting this process,  make sure that you review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="98499-110">Before starting this process,  make sure that you review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

<span data-ttu-id="98499-111">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98499-111">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="98499-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="98499-112">Before you begin</span></span>
<span data-ttu-id="98499-113">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="98499-113">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="98499-114">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="98499-114">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -MinimumVersion 2.6.0
```
<span data-ttu-id="98499-115">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="98499-115">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="98499-116">Generalize the Windows VM using Sysprep</span><span class="sxs-lookup"><span data-stu-id="98499-116">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="98499-117">Generalizing a VM using Sysprep removes any machine-specific information and personal account information from the VHD and prepares the machine to be used as an image.</span><span class="sxs-lookup"><span data-stu-id="98499-117">Generalizing a VM using Sysprep removes any machine-specific information and personal account information from the VHD and prepares the machine to be used as an image.</span></span> <span data-ttu-id="98499-118">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="98499-118">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="98499-119">Make sure the server roles running on the machine are supported by Sysprep.</span><span class="sxs-lookup"><span data-stu-id="98499-119">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="98499-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="98499-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98499-121">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span><span class="sxs-lookup"><span data-stu-id="98499-121">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="98499-122">Sign in to the Windows virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98499-122">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="98499-123">Open the Command Prompt window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="98499-123">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="98499-124">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="98499-124">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="98499-125">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="98499-125">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="98499-126">In **Shutdown Options**, select **Shutdown**.</span><span class="sxs-lookup"><span data-stu-id="98499-126">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="98499-127">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="98499-127">Click **OK**.</span></span>
   
    ![Start Sysprep](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/aws-to-azure/sysprepgeneral.png)
6. <span data-ttu-id="98499-129">When Sysprep completes, it shuts down the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98499-129">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="98499-130">Do not restart the VM.</span><span class="sxs-lookup"><span data-stu-id="98499-130">Do not restart the VM.</span></span>



## <a name="export-the-vhd-from-an-ec2-instance"></a><span data-ttu-id="98499-131">Export the VHD from an EC2 instance</span><span class="sxs-lookup"><span data-stu-id="98499-131">Export the VHD from an EC2 instance</span></span>

1.  <span data-ttu-id="98499-132">If you are using Amazon Web Services (AWS), export the EC2 instance to a VHD in an Amazon S3 bucket.</span><span class="sxs-lookup"><span data-stu-id="98499-132">If you are using Amazon Web Services (AWS), export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="98499-133">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span><span class="sxs-lookup"><span data-stu-id="98499-133">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="98499-134">Be sure to use VHD for the DISK_IMAGE_FORMAT variable when running the create-instance-export-task command.</span><span class="sxs-lookup"><span data-stu-id="98499-134">Be sure to use VHD for the DISK_IMAGE_FORMAT variable when running the create-instance-export-task command.</span></span> <span data-ttu-id="98499-135">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span><span class="sxs-lookup"><span data-stu-id="98499-135">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT '
    --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2.  <span data-ttu-id="98499-136">Download the VHD file from the S3 bucket.</span><span class="sxs-lookup"><span data-stu-id="98499-136">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="98499-137">Select the VHD file, then select **Actions** > **Download**.</span><span class="sxs-lookup"><span data-stu-id="98499-137">Select the VHD file, then select **Actions** > **Download**.</span></span>



## <a name="log-in-to-azure"></a><span data-ttu-id="98499-138">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="98499-138">Log in to Azure</span></span>
<span data-ttu-id="98499-139">If you don't already have PowerShell version installed, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="98499-139">If you don't already have PowerShell version installed, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

1. <span data-ttu-id="98499-140">Open Azure PowerShell and sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="98499-140">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="98499-141">A pop-up window opens for you to enter your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="98499-141">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="98499-142">Get the subscription IDs for your available subscriptions.</span><span class="sxs-lookup"><span data-stu-id="98499-142">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="98499-143">Set the correct subscription using the subscription ID.</span><span class="sxs-lookup"><span data-stu-id="98499-143">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="98499-144">Replace `<subscriptionID>` with the ID of the correct subscription.</span><span class="sxs-lookup"><span data-stu-id="98499-144">Replace `<subscriptionID>` with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="98499-145">Get the storage account</span><span class="sxs-lookup"><span data-stu-id="98499-145">Get the storage account</span></span>
<span data-ttu-id="98499-146">You need a storage account in Azure to store the uploaded VM image.</span><span class="sxs-lookup"><span data-stu-id="98499-146">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="98499-147">You can either use an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="98499-147">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="98499-148">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span><span class="sxs-lookup"><span data-stu-id="98499-148">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="98499-149">To show the available storage accounts, type:</span><span class="sxs-lookup"><span data-stu-id="98499-149">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="98499-150">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span><span class="sxs-lookup"><span data-stu-id="98499-150">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="98499-151">If you need to create a storage account, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="98499-151">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="98499-152">You need the name of the resource group where the storage account should be created.</span><span class="sxs-lookup"><span data-stu-id="98499-152">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="98499-153">To find out all the resource groups that are in your subscription, type:</span><span class="sxs-lookup"><span data-stu-id="98499-153">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="98499-154">To create a resource group named **myResourceGroup** in the **West US** region, type:</span><span class="sxs-lookup"><span data-stu-id="98499-154">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="98499-155">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="98499-155">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="98499-156">Valid values for -SkuName are:</span><span class="sxs-lookup"><span data-stu-id="98499-156">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="98499-157">**Standard_LRS** - Locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="98499-157">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="98499-158">**Standard_ZRS** - Zone redundant storage.</span><span class="sxs-lookup"><span data-stu-id="98499-158">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="98499-159">**Standard_GRS** - Geo redundant storage.</span><span class="sxs-lookup"><span data-stu-id="98499-159">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="98499-160">**Standard_RAGRS** - Read access geo redundant storage.</span><span class="sxs-lookup"><span data-stu-id="98499-160">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="98499-161">**Premium_LRS** - Premium locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="98499-161">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="98499-162">Upload the VHD to your storage account</span><span class="sxs-lookup"><span data-stu-id="98499-162">Upload the VHD to your storage account</span></span>

<span data-ttu-id="98499-163">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="98499-163">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="98499-164">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span><span class="sxs-lookup"><span data-stu-id="98499-164">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="98499-165">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="98499-165">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="98499-166">If successful, you get a response that looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="98499-166">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="98499-167">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span><span class="sxs-lookup"><span data-stu-id="98499-167">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="98499-168">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span><span class="sxs-lookup"><span data-stu-id="98499-168">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="98499-169">Other options for uploading a VHD</span><span class="sxs-lookup"><span data-stu-id="98499-169">Other options for uploading a VHD</span></span>

<span data-ttu-id="98499-170">You can also upload a VHD to your storage account using one of the following:</span><span class="sxs-lookup"><span data-stu-id="98499-170">You can also upload a VHD to your storage account using one of the following:</span></span>

-   [<span data-ttu-id="98499-171">Azure Storage Copy Blob API</span><span class="sxs-lookup"><span data-stu-id="98499-171">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)

-   [<span data-ttu-id="98499-172">Azure Storage Explorer Uploading Blobs</span><span class="sxs-lookup"><span data-stu-id="98499-172">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)

-   [<span data-ttu-id="98499-173">Storage Import/Export Service REST API Reference</span><span class="sxs-lookup"><span data-stu-id="98499-173">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

    <span data-ttu-id="98499-174">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span><span class="sxs-lookup"><span data-stu-id="98499-174">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="98499-175">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span><span class="sxs-lookup"><span data-stu-id="98499-175">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 

    <span data-ttu-id="98499-176">Import/Export can be used to copy to a standard storage account.</span><span class="sxs-lookup"><span data-stu-id="98499-176">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="98499-177">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span><span class="sxs-lookup"><span data-stu-id="98499-177">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>

## <a name="create-a-managed-image-from-the-uploaded-vhd"></a><span data-ttu-id="98499-178">Create a managed image from the uploaded VHD</span><span class="sxs-lookup"><span data-stu-id="98499-178">Create a managed image from the uploaded VHD</span></span> 

<span data-ttu-id="98499-179">Create a managed image using your generalized OS VHD.</span><span class="sxs-lookup"><span data-stu-id="98499-179">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="98499-180">First, set the common parameters:</span><span class="sxs-lookup"><span data-stu-id="98499-180">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```

4.  <span data-ttu-id="98499-181">Create the image using your generalized OS VHD.</span><span class="sxs-lookup"><span data-stu-id="98499-181">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="setup-some-variables-for-the-image"></a><span data-ttu-id="98499-182">Setup some variables for the image</span><span class="sxs-lookup"><span data-stu-id="98499-182">Setup some variables for the image</span></span>

<span data-ttu-id="98499-183">First we need to gather basic information about the image and create a variable for the image.</span><span class="sxs-lookup"><span data-stu-id="98499-183">First we need to gather basic information about the image and create a variable for the image.</span></span> <span data-ttu-id="98499-184">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span><span class="sxs-lookup"><span data-stu-id="98499-184">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="98499-185">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="98499-185">Create a virtual network</span></span>
<span data-ttu-id="98499-186">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98499-186">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="98499-187">Create the subnet.</span><span class="sxs-lookup"><span data-stu-id="98499-187">Create the subnet.</span></span> <span data-ttu-id="98499-188">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="98499-188">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="98499-189">Create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="98499-189">Create the virtual network.</span></span> <span data-ttu-id="98499-190">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="98499-190">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="98499-191">Create a public IP address and network interface</span><span class="sxs-lookup"><span data-stu-id="98499-191">Create a public IP address and network interface</span></span>

<span data-ttu-id="98499-192">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span><span class="sxs-lookup"><span data-stu-id="98499-192">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="98499-193">Create a public IP address.</span><span class="sxs-lookup"><span data-stu-id="98499-193">Create a public IP address.</span></span> <span data-ttu-id="98499-194">This example creates a public IP address named **myPip**.</span><span class="sxs-lookup"><span data-stu-id="98499-194">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="98499-195">Create the NIC.</span><span class="sxs-lookup"><span data-stu-id="98499-195">Create the NIC.</span></span> <span data-ttu-id="98499-196">This example creates a NIC named **myNic**.</span><span class="sxs-lookup"><span data-stu-id="98499-196">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="98499-197">Create the network security group and an RDP rule</span><span class="sxs-lookup"><span data-stu-id="98499-197">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="98499-198">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span><span class="sxs-lookup"><span data-stu-id="98499-198">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="98499-199">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span><span class="sxs-lookup"><span data-stu-id="98499-199">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="98499-200">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98499-200">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="98499-201">Create a variable for the virtual network</span><span class="sxs-lookup"><span data-stu-id="98499-201">Create a variable for the virtual network</span></span>

<span data-ttu-id="98499-202">Create a variable for the completed virtual network.</span><span class="sxs-lookup"><span data-stu-id="98499-202">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="98499-203">Get the credentials for the VM</span><span class="sxs-lookup"><span data-stu-id="98499-203">Get the credentials for the VM</span></span>

<span data-ttu-id="98499-204">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span><span class="sxs-lookup"><span data-stu-id="98499-204">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-the-vm-name-computer-name-and-the-size-of-the-vm"></a><span data-ttu-id="98499-205">Set variables for the VM name, computer name and the size of the VM</span><span class="sxs-lookup"><span data-stu-id="98499-205">Set variables for the VM name, computer name and the size of the VM</span></span>

1. <span data-ttu-id="98499-206">Create variables for the VM name and computer name.</span><span class="sxs-lookup"><span data-stu-id="98499-206">Create variables for the VM name and computer name.</span></span> <span data-ttu-id="98499-207">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span><span class="sxs-lookup"><span data-stu-id="98499-207">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="98499-208">Set the size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98499-208">Set the size of the virtual machine.</span></span> <span data-ttu-id="98499-209">This example creates **Standard_DS1_v2** sized VM.</span><span class="sxs-lookup"><span data-stu-id="98499-209">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="98499-210">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span><span class="sxs-lookup"><span data-stu-id="98499-210">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="98499-211">Add the VM name and size to the VM configuration.</span><span class="sxs-lookup"><span data-stu-id="98499-211">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="98499-212">Set the VM image as source image for the new VM</span><span class="sxs-lookup"><span data-stu-id="98499-212">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="98499-213">Set the source image using the ID of the managed VM image.</span><span class="sxs-lookup"><span data-stu-id="98499-213">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="98499-214">Set the OS configuration and add the NIC.</span><span class="sxs-lookup"><span data-stu-id="98499-214">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="98499-215">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span><span class="sxs-lookup"><span data-stu-id="98499-215">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="98499-216">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="98499-216">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -ManagedDiskStorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="98499-217">Create the VM</span><span class="sxs-lookup"><span data-stu-id="98499-217">Create the VM</span></span>

<span data-ttu-id="98499-218">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span><span class="sxs-lookup"><span data-stu-id="98499-218">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="98499-219">Verify that the VM was created</span><span class="sxs-lookup"><span data-stu-id="98499-219">Verify that the VM was created</span></span>
<span data-ttu-id="98499-220">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="98499-220">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="98499-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="98499-221">Next steps</span></span>

<span data-ttu-id="98499-222">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span><span class="sxs-lookup"><span data-stu-id="98499-222">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="98499-223">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98499-223">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="98499-224">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98499-224">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
 

