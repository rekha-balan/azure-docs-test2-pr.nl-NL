---
title: Upload a specialized VHD to Azure to use for creating a new VM | Microsoft Docs
description: Upload a specialized VHD to Azure to use for creating a new VM.
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
ms.date: 02/05/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 232a7274a657302e71c6d3f181cad8a00ae685b8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553796"
---
# <a name="how-to-upload-a-specialized-vhd-to-create-a-vm-in-azure"></a><span data-ttu-id="e30b8-103">How to upload a specialized VHD to create a VM in Azure</span><span class="sxs-lookup"><span data-stu-id="e30b8-103">How to upload a specialized VHD to create a VM in Azure</span></span>

<span data-ttu-id="e30b8-104">A specialized VHD maintains the user accounts, applications and other state data from your original VM.</span><span class="sxs-lookup"><span data-stu-id="e30b8-104">A specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="e30b8-105">You can upload a specialized VHD to Azure and use it to create a VM that uses Managed Disks or an unmanaged storage account.</span><span class="sxs-lookup"><span data-stu-id="e30b8-105">You can upload a specialized VHD to Azure and use it to create a VM that uses Managed Disks or an unmanaged storage account.</span></span> <span data-ttu-id="e30b8-106">We recommend that you use [Managed Disks](../../storage/storage-managed-disks-overview.md) to take advantage of the simplified management and additional features that Managed Disks offer.</span><span class="sxs-lookup"><span data-stu-id="e30b8-106">We recommend that you use [Managed Disks](../../storage/storage-managed-disks-overview.md) to take advantage of the simplified management and additional features that Managed Disks offer.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="e30b8-107">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e30b8-107">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
>
>


* <span data-ttu-id="e30b8-108">For information about pricing of the various VM sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="e30b8-108">For information about pricing of the various VM sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span>
* <span data-ttu-id="e30b8-109">For information on storage pricing, see [Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="e30b8-109">For information on storage pricing, see [Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span> 
* <span data-ttu-id="e30b8-110">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="e30b8-110">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
* <span data-ttu-id="e30b8-111">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="e30b8-111">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e30b8-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="e30b8-112">Before you begin</span></span>
<span data-ttu-id="e30b8-113">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="e30b8-113">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="e30b8-114">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="e30b8-114">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="e30b8-115">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="e30b8-115">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>


## <a name="prepare-the-vm"></a><span data-ttu-id="e30b8-116">Prepare the VM</span><span class="sxs-lookup"><span data-stu-id="e30b8-116">Prepare the VM</span></span>
 
<span data-ttu-id="e30b8-117">If you intend to use the specialized VHD as-is to create a new VM, ensure the following steps are completed.</span><span class="sxs-lookup"><span data-stu-id="e30b8-117">If you intend to use the specialized VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  * <span data-ttu-id="e30b8-118">If you are going to use Managed Disks, review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="e30b8-118">If you are going to use Managed Disks, review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>
  * <span data-ttu-id="e30b8-119">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e30b8-119">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e30b8-120">**Do not** generalize the VM using Sysprep.</span><span class="sxs-lookup"><span data-stu-id="e30b8-120">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="e30b8-121">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span><span class="sxs-lookup"><span data-stu-id="e30b8-121">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="e30b8-122">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span><span class="sxs-lookup"><span data-stu-id="e30b8-122">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="e30b8-123">This ensures that the server obtains an IP address within the VNet when it starts up.</span><span class="sxs-lookup"><span data-stu-id="e30b8-123">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 
  * <span data-ttu-id="e30b8-124">Shut down to VM before proceeding.</span><span class="sxs-lookup"><span data-stu-id="e30b8-124">Shut down to VM before proceeding.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="e30b8-125">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="e30b8-125">Log in to Azure</span></span>
<span data-ttu-id="e30b8-126">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="e30b8-126">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

1. <span data-ttu-id="e30b8-127">Open Azure PowerShell and sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="e30b8-127">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="e30b8-128">A pop-up window opens for you to enter your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="e30b8-128">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="e30b8-129">Get the subscription IDs for your available subscriptions.</span><span class="sxs-lookup"><span data-stu-id="e30b8-129">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="e30b8-130">Set the correct subscription using the subscription ID.</span><span class="sxs-lookup"><span data-stu-id="e30b8-130">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="e30b8-131">Replace `<subscriptionID>` with the ID of the correct subscription.</span><span class="sxs-lookup"><span data-stu-id="e30b8-131">Replace `<subscriptionID>` with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="e30b8-132">Get the storage account</span><span class="sxs-lookup"><span data-stu-id="e30b8-132">Get the storage account</span></span>
<span data-ttu-id="e30b8-133">You need a storage account in Azure to store the uploaded VM image.</span><span class="sxs-lookup"><span data-stu-id="e30b8-133">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="e30b8-134">You can either use an existing storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="e30b8-134">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="e30b8-135">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span><span class="sxs-lookup"><span data-stu-id="e30b8-135">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="e30b8-136">To show the available storage accounts, type:</span><span class="sxs-lookup"><span data-stu-id="e30b8-136">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="e30b8-137">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span><span class="sxs-lookup"><span data-stu-id="e30b8-137">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="e30b8-138">If you need to create a storage account, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="e30b8-138">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="e30b8-139">You need the name of the resource group where the storage account should be created.</span><span class="sxs-lookup"><span data-stu-id="e30b8-139">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="e30b8-140">To find out all the resource groups that are in your subscription, type:</span><span class="sxs-lookup"><span data-stu-id="e30b8-140">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="e30b8-141">To create a resource group named **myResourceGroup** in the **West US** region, type:</span><span class="sxs-lookup"><span data-stu-id="e30b8-141">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="e30b8-142">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e30b8-142">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="e30b8-143">Valid values for -SkuName are:</span><span class="sxs-lookup"><span data-stu-id="e30b8-143">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="e30b8-144">**Standard_LRS** - Locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="e30b8-144">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="e30b8-145">**Standard_ZRS** - Zone redundant storage.</span><span class="sxs-lookup"><span data-stu-id="e30b8-145">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="e30b8-146">**Standard_GRS** - Geo redundant storage.</span><span class="sxs-lookup"><span data-stu-id="e30b8-146">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="e30b8-147">**Standard_RAGRS** - Read access geo redundant storage.</span><span class="sxs-lookup"><span data-stu-id="e30b8-147">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="e30b8-148">**Premium_LRS** - Premium locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="e30b8-148">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="e30b8-149">Upload the VHD to your storage account</span><span class="sxs-lookup"><span data-stu-id="e30b8-149">Upload the VHD to your storage account</span></span>

<span data-ttu-id="e30b8-150">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="e30b8-150">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="e30b8-151">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span><span class="sxs-lookup"><span data-stu-id="e30b8-151">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="e30b8-152">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="e30b8-152">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="e30b8-153">If successful, you get a response that looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="e30b8-153">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="e30b8-154">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span><span class="sxs-lookup"><span data-stu-id="e30b8-154">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="e30b8-155">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span><span class="sxs-lookup"><span data-stu-id="e30b8-155">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="e30b8-156">Other options for uploading a VHD</span><span class="sxs-lookup"><span data-stu-id="e30b8-156">Other options for uploading a VHD</span></span>

<span data-ttu-id="e30b8-157">You can also upload a VHD to your storage account using one of the following:</span><span class="sxs-lookup"><span data-stu-id="e30b8-157">You can also upload a VHD to your storage account using one of the following:</span></span>

-   [<span data-ttu-id="e30b8-158">Azure Storage Copy Blob API</span><span class="sxs-lookup"><span data-stu-id="e30b8-158">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)

-   [<span data-ttu-id="e30b8-159">Azure Storage Explorer Uploading Blobs</span><span class="sxs-lookup"><span data-stu-id="e30b8-159">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)

-   [<span data-ttu-id="e30b8-160">Storage Import/Export Service REST API Reference</span><span class="sxs-lookup"><span data-stu-id="e30b8-160">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

    <span data-ttu-id="e30b8-161">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span><span class="sxs-lookup"><span data-stu-id="e30b8-161">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="e30b8-162">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span><span class="sxs-lookup"><span data-stu-id="e30b8-162">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 

    <span data-ttu-id="e30b8-163">Import/Export can be used to copy to a standard storage account.</span><span class="sxs-lookup"><span data-stu-id="e30b8-163">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="e30b8-164">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e30b8-164">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>

    
## <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="e30b8-165">Create the subNet and vNet</span><span class="sxs-lookup"><span data-stu-id="e30b8-165">Create the subNet and vNet</span></span>

<span data-ttu-id="e30b8-166">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e30b8-166">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="e30b8-167">Create the subNet.</span><span class="sxs-lookup"><span data-stu-id="e30b8-167">Create the subNet.</span></span> <span data-ttu-id="e30b8-168">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="e30b8-168">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
    ```powershell
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="e30b8-169">Create the vNet.</span><span class="sxs-lookup"><span data-stu-id="e30b8-169">Create the vNet.</span></span> <span data-ttu-id="e30b8-170">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="e30b8-170">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="e30b8-171">Create a public IP address and NIC</span><span class="sxs-lookup"><span data-stu-id="e30b8-171">Create a public IP address and NIC</span></span>
<span data-ttu-id="e30b8-172">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span><span class="sxs-lookup"><span data-stu-id="e30b8-172">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="e30b8-173">Create the public IP.</span><span class="sxs-lookup"><span data-stu-id="e30b8-173">Create the public IP.</span></span> <span data-ttu-id="e30b8-174">In this example, the public IP address name is set to **myIP**.</span><span class="sxs-lookup"><span data-stu-id="e30b8-174">In this example, the public IP address name is set to **myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="e30b8-175">Create the NIC.</span><span class="sxs-lookup"><span data-stu-id="e30b8-175">Create the NIC.</span></span> <span data-ttu-id="e30b8-176">In this example, the NIC name is set to **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="e30b8-176">In this example, the NIC name is set to **myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="e30b8-177">Create the network security group and an RDP rule</span><span class="sxs-lookup"><span data-stu-id="e30b8-177">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="e30b8-178">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span><span class="sxs-lookup"><span data-stu-id="e30b8-178">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="e30b8-179">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span><span class="sxs-lookup"><span data-stu-id="e30b8-179">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span></span>

<span data-ttu-id="e30b8-180">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="e30b8-180">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="e30b8-181">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e30b8-181">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="set-the-vm-name-and-size"></a><span data-ttu-id="e30b8-182">Set the VM name and size</span><span class="sxs-lookup"><span data-stu-id="e30b8-182">Set the VM name and size</span></span>

<span data-ttu-id="e30b8-183">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="e30b8-183">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

## <a name="add-the-nic"></a><span data-ttu-id="e30b8-184">Add the NIC</span><span class="sxs-lookup"><span data-stu-id="e30b8-184">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
## <a name="configure-the-os-disk"></a><span data-ttu-id="e30b8-185">Configure the OS disk</span><span class="sxs-lookup"><span data-stu-id="e30b8-185">Configure the OS disk</span></span>

<span data-ttu-id="e30b8-186">The specialised OS could be a VHD that you [uploaded to Azure](upload-image.md) or a [copy the VHD from an existing Azure VM](vhd-copy.md).</span><span class="sxs-lookup"><span data-stu-id="e30b8-186">The specialised OS could be a VHD that you [uploaded to Azure](upload-image.md) or a [copy the VHD from an existing Azure VM](vhd-copy.md).</span></span> 

<span data-ttu-id="e30b8-187">You can choose one of two options:</span><span class="sxs-lookup"><span data-stu-id="e30b8-187">You can choose one of two options:</span></span>
- <span data-ttu-id="e30b8-188">**Option 1**: Create a specialized managed disk from a specialied VHD in an existing storage account to use as the OS disk.</span><span class="sxs-lookup"><span data-stu-id="e30b8-188">**Option 1**: Create a specialized managed disk from a specialied VHD in an existing storage account to use as the OS disk.</span></span>

<span data-ttu-id="e30b8-189">or</span><span class="sxs-lookup"><span data-stu-id="e30b8-189">or</span></span> 

- <span data-ttu-id="e30b8-190">**Option 2**: Use a specialized VHD stored in your own storage account (an unmanaged disk).</span><span class="sxs-lookup"><span data-stu-id="e30b8-190">**Option 2**: Use a specialized VHD stored in your own storage account (an unmanaged disk).</span></span> 

### <a name="option-1-create-a-managed-disk-from-an-unmanaged-specialized-disk"></a><span data-ttu-id="e30b8-191">Option 1: Create a managed disk from an unmanaged specialized disk</span><span class="sxs-lookup"><span data-stu-id="e30b8-191">Option 1: Create a managed disk from an unmanaged specialized disk</span></span>

1. <span data-ttu-id="e30b8-192">Create a managed disk from the existing specialized VHD in your storage account.</span><span class="sxs-lookup"><span data-stu-id="e30b8-192">Create a managed disk from the existing specialized VHD in your storage account.</span></span> <span data-ttu-id="e30b8-193">This example uses **myOSDisk1** for the disk name, puts the disk in **StandardLRS** storage and uses **https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vh.vhd** as the URI for the source VHD.</span><span class="sxs-lookup"><span data-stu-id="e30b8-193">This example uses **myOSDisk1** for the disk name, puts the disk in **StandardLRS** storage and uses **https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vh.vhd** as the URI for the source VHD.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName "myOSDisk1" -Disk (New-AzureRmDiskConfig `
    -AccountType StandardLRS  -Location $location -CreationDataCreateOption Import `
    -SourceUri $urlOfUploadedImageVhd -ResourceGroupName $rgName
    ```

2. <span data-ttu-id="e30b8-194">Add the OS disk to the configuration.</span><span class="sxs-lookup"><span data-stu-id="e30b8-194">Add the OS disk to the configuration.</span></span> <span data-ttu-id="e30b8-195">This example sets the size of the disk to **128 GB** and attaches the managed disk as a **Windows** OS disk.</span><span class="sxs-lookup"><span data-stu-id="e30b8-195">This example sets the size of the disk to **128 GB** and attaches the managed disk as a **Windows** OS disk.</span></span>
    
    ```powershell
    $vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -ManagedDiskStorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

<span data-ttu-id="e30b8-196">Optional: Attach additional managed disks as data disks.</span><span class="sxs-lookup"><span data-stu-id="e30b8-196">Optional: Attach additional managed disks as data disks.</span></span> <span data-ttu-id="e30b8-197">This option assumes that you created your managed data disks using [Create managed data disks](create-managed-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e30b8-197">This option assumes that you created your managed data disks using [Create managed data disks](create-managed-disk-ps.md).</span></span> 

```powershell
$vm = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
```


### <a name="option-2-attach-a-vhd-that-is-in-an-existing-storage-account"></a><span data-ttu-id="e30b8-198">Option 2: Attach a VHD that is in an existing storage account</span><span class="sxs-lookup"><span data-stu-id="e30b8-198">Option 2: Attach a VHD that is in an existing storage account</span></span>

1. <span data-ttu-id="e30b8-199">Set the URI for the VHD that you want to use.</span><span class="sxs-lookup"><span data-stu-id="e30b8-199">Set the URI for the VHD that you want to use.</span></span> <span data-ttu-id="e30b8-200">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="e30b8-200">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = $urlOfUploadedImageVhd
    ```
2. <span data-ttu-id="e30b8-201">Add the OS disk by using the URL of the copied OS VHD.</span><span class="sxs-lookup"><span data-stu-id="e30b8-201">Add the OS disk by using the URL of the copied OS VHD.</span></span> <span data-ttu-id="e30b8-202">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span><span class="sxs-lookup"><span data-stu-id="e30b8-202">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span></span> <span data-ttu-id="e30b8-203">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span><span class="sxs-lookup"><span data-stu-id="e30b8-203">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="e30b8-204">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span><span class="sxs-lookup"><span data-stu-id="e30b8-204">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="e30b8-205">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="e30b8-205">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="e30b8-206">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span><span class="sxs-lookup"><span data-stu-id="e30b8-206">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span></span>


## <a name="create-the-vm"></a><span data-ttu-id="e30b8-207">Create the VM</span><span class="sxs-lookup"><span data-stu-id="e30b8-207">Create the VM</span></span>

<span data-ttu-id="e30b8-208">Create the VM using the configurations that we just created.</span><span class="sxs-lookup"><span data-stu-id="e30b8-208">Create the VM using the configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="e30b8-209">If this command was successful, you'll see output like this:</span><span class="sxs-lookup"><span data-stu-id="e30b8-209">If this command was successful, you'll see output like this:</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="e30b8-210">Verify that the VM was created</span><span class="sxs-lookup"><span data-stu-id="e30b8-210">Verify that the VM was created</span></span>
<span data-ttu-id="e30b8-211">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="e30b8-211">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="e30b8-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="e30b8-212">Next steps</span></span>
<span data-ttu-id="e30b8-213">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span><span class="sxs-lookup"><span data-stu-id="e30b8-213">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="e30b8-214">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e30b8-214">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="e30b8-215">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e30b8-215">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
