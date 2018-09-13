---
title: Creating an on-premises virtual machine image for the Azure Marketplace | Microsoft Docs
description: Understand and execute the steps to create an on-premises VM image and deploy to the Azure Marketplace for others to purchase.
services: marketplace-publishing
documentationcenter: ''
author: HannibalSII
manager: hascipio
editor: ''
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: db8028c5bc57760c00890725bb29a04b9a5a711b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669311"
---
# <a name="develop-an-on-premises-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="f06d8-103">Develop an on-premises virtual machine image for the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f06d8-103">Develop an on-premises virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="f06d8-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol.</span><span class="sxs-lookup"><span data-stu-id="f06d8-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="f06d8-105">However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f06d8-105">However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="f06d8-106">For on-premises development, you must download the operating system VHD of the created VM.</span><span class="sxs-lookup"><span data-stu-id="f06d8-106">For on-premises development, you must download the operating system VHD of the created VM.</span></span> <span data-ttu-id="f06d8-107">These steps would take place as part of step 3.3, above.</span><span class="sxs-lookup"><span data-stu-id="f06d8-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="f06d8-108">Download a VHD image</span><span class="sxs-lookup"><span data-stu-id="f06d8-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="f06d8-109">Locate a blob URL</span><span class="sxs-lookup"><span data-stu-id="f06d8-109">Locate a blob URL</span></span>
<span data-ttu-id="f06d8-110">In order to download the VHD, first locate the blob URL for the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="f06d8-110">In order to download the VHD, first locate the blob URL for the operating system disk.</span></span>

<span data-ttu-id="f06d8-111">Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="f06d8-111">Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="f06d8-112">Go to **Browse** > **VMs**, and then select the deployed VM.</span><span class="sxs-lookup"><span data-stu-id="f06d8-112">Go to **Browse** > **VMs**, and then select the deployed VM.</span></span>
2. <span data-ttu-id="f06d8-113">Under **Configure**, select the **Disks** tile, which opens the Disks blade.</span><span class="sxs-lookup"><span data-stu-id="f06d8-113">Under **Configure**, select the **Disks** tile, which opens the Disks blade.</span></span>
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="f06d8-115">Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.</span><span class="sxs-lookup"><span data-stu-id="f06d8-115">Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.</span></span>
4. <span data-ttu-id="f06d8-116">Copy this blob URL.</span><span class="sxs-lookup"><span data-stu-id="f06d8-116">Copy this blob URL.</span></span>
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="f06d8-118">Now, delete the deployed VM without deleting the backing disks.</span><span class="sxs-lookup"><span data-stu-id="f06d8-118">Now, delete the deployed VM without deleting the backing disks.</span></span> <span data-ttu-id="f06d8-119">You can also stop the VM instead of deleting it.</span><span class="sxs-lookup"><span data-stu-id="f06d8-119">You can also stop the VM instead of deleting it.</span></span> <span data-ttu-id="f06d8-120">Do not download the operating system VHD when the VM is running.</span><span class="sxs-lookup"><span data-stu-id="f06d8-120">Do not download the operating system VHD when the VM is running.</span></span>
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="f06d8-122">Download a VHD</span><span class="sxs-lookup"><span data-stu-id="f06d8-122">Download a VHD</span></span>
<span data-ttu-id="f06d8-123">After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f06d8-123">After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="f06d8-124">At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f06d8-124">At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="f06d8-125">**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="f06d8-125">**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="f06d8-126">Sign in to the Azure portal if you have not done so already.</span><span class="sxs-lookup"><span data-stu-id="f06d8-126">Sign in to the Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="f06d8-127">Click the **Storage** tab.</span><span class="sxs-lookup"><span data-stu-id="f06d8-127">Click the **Storage** tab.</span></span>
3. <span data-ttu-id="f06d8-128">Select the storage account within which the VHD is stored.</span><span class="sxs-lookup"><span data-stu-id="f06d8-128">Select the storage account within which the VHD is stored.</span></span>
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="f06d8-130">This displays storage account properties.</span><span class="sxs-lookup"><span data-stu-id="f06d8-130">This displays storage account properties.</span></span> <span data-ttu-id="f06d8-131">Select the **Containers** tab.</span><span class="sxs-lookup"><span data-stu-id="f06d8-131">Select the **Containers** tab.</span></span>
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="f06d8-133">Select the container in which the VHD is stored.</span><span class="sxs-lookup"><span data-stu-id="f06d8-133">Select the container in which the VHD is stored.</span></span> <span data-ttu-id="f06d8-134">By default, when created from the portal, the VHD is stored in a vhds container.</span><span class="sxs-lookup"><span data-stu-id="f06d8-134">By default, when created from the portal, the VHD is stored in a vhds container.</span></span>
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="f06d8-136">Select the correct operating system VHD by comparing the URL to the one you saved.</span><span class="sxs-lookup"><span data-stu-id="f06d8-136">Select the correct operating system VHD by comparing the URL to the one you saved.</span></span>
7. <span data-ttu-id="f06d8-137">Click **Download**.</span><span class="sxs-lookup"><span data-stu-id="f06d8-137">Click **Download**.</span></span>
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="f06d8-139">Download a VHD by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06d8-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="f06d8-140">In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.</span><span class="sxs-lookup"><span data-stu-id="f06d8-140">In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="f06d8-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="f06d8-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="f06d8-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.</span><span class="sxs-lookup"><span data-stu-id="f06d8-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.</span></span>
> 
> 

## <a name="upload-vhds-to-an-azure-storage-account"></a><span data-ttu-id="f06d8-143">Upload VHDs to an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="f06d8-143">Upload VHDs to an Azure storage account</span></span>
<span data-ttu-id="f06d8-144">If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure.</span><span class="sxs-lookup"><span data-stu-id="f06d8-144">If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure.</span></span> <span data-ttu-id="f06d8-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span><span class="sxs-lookup"><span data-stu-id="f06d8-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="f06d8-146">Create a storage account and container</span><span class="sxs-lookup"><span data-stu-id="f06d8-146">Create a storage account and container</span></span>
<span data-ttu-id="f06d8-147">We recommend that VHDs be uploaded into a storage account in a region in the United States.</span><span class="sxs-lookup"><span data-stu-id="f06d8-147">We recommend that VHDs be uploaded into a storage account in a region in the United States.</span></span> <span data-ttu-id="f06d8-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span><span class="sxs-lookup"><span data-stu-id="f06d8-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="f06d8-149">To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.</span><span class="sxs-lookup"><span data-stu-id="f06d8-149">To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.</span></span>  

<span data-ttu-id="f06d8-150">**Create a storage account from the Microsoft Azure portal**</span><span class="sxs-lookup"><span data-stu-id="f06d8-150">**Create a storage account from the Microsoft Azure portal**</span></span>

1. <span data-ttu-id="f06d8-151">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="f06d8-151">Click **New**.</span></span>
2. <span data-ttu-id="f06d8-152">Select **Storage**.</span><span class="sxs-lookup"><span data-stu-id="f06d8-152">Select **Storage**.</span></span>
3. <span data-ttu-id="f06d8-153">Fill in the storage account name, and then select a location.</span><span class="sxs-lookup"><span data-stu-id="f06d8-153">Fill in the storage account name, and then select a location.</span></span>
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="f06d8-155">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f06d8-155">Click **Create**.</span></span>
5. <span data-ttu-id="f06d8-156">The blade for the created storage account should be open.</span><span class="sxs-lookup"><span data-stu-id="f06d8-156">The blade for the created storage account should be open.</span></span> <span data-ttu-id="f06d8-157">If not, select **Browse** > **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="f06d8-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="f06d8-158">On the Storage account blade, select the storage account created.</span><span class="sxs-lookup"><span data-stu-id="f06d8-158">On the Storage account blade, select the storage account created.</span></span>
6. <span data-ttu-id="f06d8-159">Select **Containers**.</span><span class="sxs-lookup"><span data-stu-id="f06d8-159">Select **Containers**.</span></span>
   
   ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="f06d8-161">On the Containers blade, select **Add**, and then enter a container name and the container permissions.</span><span class="sxs-lookup"><span data-stu-id="f06d8-161">On the Containers blade, select **Add**, and then enter a container name and the container permissions.</span></span> <span data-ttu-id="f06d8-162">Select **Private** for container permissions.</span><span class="sxs-lookup"><span data-stu-id="f06d8-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="f06d8-163">We recommend that you create one container per SKU that you are planning to publish.</span><span class="sxs-lookup"><span data-stu-id="f06d8-163">We recommend that you create one container per SKU that you are planning to publish.</span></span>
> 
> 

  ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="f06d8-165">Create a storage account by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06d8-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="f06d8-166">Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f06d8-166">Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="f06d8-167">Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f06d8-167">Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="f06d8-168">Those commands assume that the current storage account context has already been set in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f06d8-168">Those commands assume that the current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="f06d8-169">Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span><span class="sxs-lookup"><span data-stu-id="f06d8-169">Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="f06d8-170">Create a storage account by using the command-line tool for Mac and Linux</span><span class="sxs-lookup"><span data-stu-id="f06d8-170">Create a storage account by using the command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="f06d8-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span><span class="sxs-lookup"><span data-stu-id="f06d8-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="f06d8-172">Create a container as follows.</span><span class="sxs-lookup"><span data-stu-id="f06d8-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="f06d8-173">Upload a VHD</span><span class="sxs-lookup"><span data-stu-id="f06d8-173">Upload a VHD</span></span>
<span data-ttu-id="f06d8-174">After the storage account and container are created, you can upload your prepared VHDs.</span><span class="sxs-lookup"><span data-stu-id="f06d8-174">After the storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="f06d8-175">You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.</span><span class="sxs-lookup"><span data-stu-id="f06d8-175">You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="f06d8-176">Upload a VHD via PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06d8-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="f06d8-177">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f06d8-177">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="f06d8-178">Upload a VHD by using the command-line tool for Mac and Linux</span><span class="sxs-lookup"><span data-stu-id="f06d8-178">Upload a VHD by using the command-line tool for Mac and Linux</span></span>
<span data-ttu-id="f06d8-179">With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="f06d8-179">With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="f06d8-180">See also</span><span class="sxs-lookup"><span data-stu-id="f06d8-180">See also</span></span>
* [<span data-ttu-id="f06d8-181">Creating a virtual machine image for the Marketplace</span><span class="sxs-lookup"><span data-stu-id="f06d8-181">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="f06d8-182">Setting up Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06d8-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)











