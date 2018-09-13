---
title: Create a copy of a specialized VM in Azure | Microsoft Docs
description: Learn how to create a copy of a specialized Windows VM running in Azure, in the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ce7e6cd3-6a4a-4fab-bf66-52f699b1398a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: a7a1e823264bcb7c57ce40c56424733dc2309fef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549909"
---
# <a name="create-a-copy-of-a-specialized-windows-vm-running-in-azure"></a><span data-ttu-id="be4be-103">Create a copy of a specialized Windows VM running in Azure</span><span class="sxs-lookup"><span data-stu-id="be4be-103">Create a copy of a specialized Windows VM running in Azure</span></span>
<span data-ttu-id="be4be-104">This article shows you how to use the AZCopy tool to create a copy of the VHD from a specialized Windows VM that is running in Azure.</span><span class="sxs-lookup"><span data-stu-id="be4be-104">This article shows you how to use the AZCopy tool to create a copy of the VHD from a specialized Windows VM that is running in Azure.</span></span> <span data-ttu-id="be4be-105">You can then use the copy of the VHD to create a new VM.</span><span class="sxs-lookup"><span data-stu-id="be4be-105">You can then use the copy of the VHD to create a new VM.</span></span> 

* <span data-ttu-id="be4be-106">If want to copy a generalized VM, see [How to create a VM image from an existing generalized Azure VM](capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be4be-106">If want to copy a generalized VM, see [How to create a VM image from an existing generalized Azure VM](capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="be4be-107">If you want to upload a VHD from an on-premises VM, like one created using Hyper-V, the see [Upload a Windows VHD from an on-premises VM to Azure](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be4be-107">If you want to upload a VHD from an on-premises VM, like one created using Hyper-V, the see [Upload a Windows VHD from an on-premises VM to Azure](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="be4be-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="be4be-108">Before you begin</span></span>
<span data-ttu-id="be4be-109">Make sure that you:</span><span class="sxs-lookup"><span data-stu-id="be4be-109">Make sure that you:</span></span>

* <span data-ttu-id="be4be-110">Have information about the **source and destination storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="be4be-110">Have information about the **source and destination storage accounts**.</span></span> <span data-ttu-id="be4be-111">For the source VM, you need to have the storage account and container names.</span><span class="sxs-lookup"><span data-stu-id="be4be-111">For the source VM, you need to have the storage account and container names.</span></span> <span data-ttu-id="be4be-112">Usually, the container name will be **vhds**.</span><span class="sxs-lookup"><span data-stu-id="be4be-112">Usually, the container name will be **vhds**.</span></span> <span data-ttu-id="be4be-113">You also need to have a destination storage account.</span><span class="sxs-lookup"><span data-stu-id="be4be-113">You also need to have a destination storage account.</span></span> <span data-ttu-id="be4be-114">If you don't already have one, you can create one using either the portal (**More Services** > Storage accounts > Add) or using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="be4be-114">If you don't already have one, you can create one using either the portal (**More Services** > Storage accounts > Add) or using the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet.</span></span> 
* <span data-ttu-id="be4be-115">Have Azure [PowerShell 1.0](/powershell/azureps-cmdlets-docs) (or later) installed.</span><span class="sxs-lookup"><span data-stu-id="be4be-115">Have Azure [PowerShell 1.0](/powershell/azureps-cmdlets-docs) (or later) installed.</span></span>
* <span data-ttu-id="be4be-116">Have downloaded and installed the [AzCopy tool](../../storage/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="be4be-116">Have downloaded and installed the [AzCopy tool](../../storage/storage-use-azcopy.md).</span></span> 

## <a name="deallocate-the-vm"></a><span data-ttu-id="be4be-117">Deallocate the VM</span><span class="sxs-lookup"><span data-stu-id="be4be-117">Deallocate the VM</span></span>
<span data-ttu-id="be4be-118">Deallocate the VM, which frees up the VHD to be copied.</span><span class="sxs-lookup"><span data-stu-id="be4be-118">Deallocate the VM, which frees up the VHD to be copied.</span></span> 

* <span data-ttu-id="be4be-119">**Portal**: Click **Virtual machines** > **myVM** > Stop</span><span class="sxs-lookup"><span data-stu-id="be4be-119">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="be4be-120">**Powershell**: `Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM` deallocates the VM named **myVM** in resource group **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="be4be-120">**Powershell**: `Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM` deallocates the VM named **myVM** in resource group **myResourceGroup**.</span></span>

<span data-ttu-id="be4be-121">The **Status** for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="be4be-121">The **Status** for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>

## <a name="get-the-storage-account-urls"></a><span data-ttu-id="be4be-122">Get the storage account URLs</span><span class="sxs-lookup"><span data-stu-id="be4be-122">Get the storage account URLs</span></span>
<span data-ttu-id="be4be-123">You need the URLs of the source and destination storage accounts.</span><span class="sxs-lookup"><span data-stu-id="be4be-123">You need the URLs of the source and destination storage accounts.</span></span> <span data-ttu-id="be4be-124">The URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="be4be-124">The URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="be4be-125">If you already know the storage account and container name, you can just replace the information between the brackets to create your URL.</span><span class="sxs-lookup"><span data-stu-id="be4be-125">If you already know the storage account and container name, you can just replace the information between the brackets to create your URL.</span></span> 

<span data-ttu-id="be4be-126">You can use the Azure portal or Azure Powershell to get the URL:</span><span class="sxs-lookup"><span data-stu-id="be4be-126">You can use the Azure portal or Azure Powershell to get the URL:</span></span>

* <span data-ttu-id="be4be-127">**Portal**: Click **More services** > **Storage accounts** > <storage account> **Blobs** and your source VHD file is probably in the **vhds** container.</span><span class="sxs-lookup"><span data-stu-id="be4be-127">**Portal**: Click **More services** > **Storage accounts** > <storage account> **Blobs** and your source VHD file is probably in the **vhds** container.</span></span> <span data-ttu-id="be4be-128">Click **Properties** for the container, and copy the text labeled **URL**.</span><span class="sxs-lookup"><span data-stu-id="be4be-128">Click **Properties** for the container, and copy the text labeled **URL**.</span></span> <span data-ttu-id="be4be-129">You'll need the URLs of both the source and destination containers.</span><span class="sxs-lookup"><span data-stu-id="be4be-129">You'll need the URLs of both the source and destination containers.</span></span> 
* <span data-ttu-id="be4be-130">**Powershell**: `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` gets the information for VM named **myVM** in the resource group **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="be4be-130">**Powershell**: `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` gets the information for VM named **myVM** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="be4be-131">In the results, look in the **Storage profile** section for the **Vhd Uri**.</span><span class="sxs-lookup"><span data-stu-id="be4be-131">In the results, look in the **Storage profile** section for the **Vhd Uri**.</span></span> <span data-ttu-id="be4be-132">The first part of the Uri is the URL to the container and the last part is the OS VHD name for the VM.</span><span class="sxs-lookup"><span data-stu-id="be4be-132">The first part of the Uri is the URL to the container and the last part is the OS VHD name for the VM.</span></span>

## <a name="get-the-storage-access-keys"></a><span data-ttu-id="be4be-133">Get the storage access keys</span><span class="sxs-lookup"><span data-stu-id="be4be-133">Get the storage access keys</span></span>
<span data-ttu-id="be4be-134">Find the access keys for the source and destination storage accounts.</span><span class="sxs-lookup"><span data-stu-id="be4be-134">Find the access keys for the source and destination storage accounts.</span></span> <span data-ttu-id="be4be-135">For more information about access keys, see [About Azure storage accounts](../../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="be4be-135">For more information about access keys, see [About Azure storage accounts](../../storage/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="be4be-136">**Portal**: Click **More services** > **Storage accounts** > <storage account> **All Settings** > **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="be4be-136">**Portal**: Click **More services** > **Storage accounts** > <storage account> **All Settings** > **Access keys**.</span></span> <span data-ttu-id="be4be-137">Copy the key labeled as **key1**.</span><span class="sxs-lookup"><span data-stu-id="be4be-137">Copy the key labeled as **key1**.</span></span>
* <span data-ttu-id="be4be-138">**Powershell**: `Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup` gets the storage key for the storage account **mystorageaccount** in the resource group **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="be4be-138">**Powershell**: `Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup` gets the storage key for the storage account **mystorageaccount** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="be4be-139">Copy the key labeled as **key1**.</span><span class="sxs-lookup"><span data-stu-id="be4be-139">Copy the key labeled as **key1**.</span></span>

## <a name="copy-the-vhd"></a><span data-ttu-id="be4be-140">Copy the VHD</span><span class="sxs-lookup"><span data-stu-id="be4be-140">Copy the VHD</span></span>
<span data-ttu-id="be4be-141">You can copy files between storage accounts using AzCopy.</span><span class="sxs-lookup"><span data-stu-id="be4be-141">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="be4be-142">For the destination container, if the specified container doesn't exist, it will be created for you.</span><span class="sxs-lookup"><span data-stu-id="be4be-142">For the destination container, if the specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="be4be-143">To use AzCopy, open a command prompt on your local machine and navigate to the folder where AzCopy is installed.</span><span class="sxs-lookup"><span data-stu-id="be4be-143">To use AzCopy, open a command prompt on your local machine and navigate to the folder where AzCopy is installed.</span></span> <span data-ttu-id="be4be-144">It will be similar to *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="be4be-144">It will be similar to *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="be4be-145">To copy all of the files within a container, you use the **/S** switch.</span><span class="sxs-lookup"><span data-stu-id="be4be-145">To copy all of the files within a container, you use the **/S** switch.</span></span> <span data-ttu-id="be4be-146">This can be used to copy the OS VHD and all of the data disks if they are in the same container.</span><span class="sxs-lookup"><span data-stu-id="be4be-146">This can be used to copy the OS VHD and all of the data disks if they are in the same container.</span></span> <span data-ttu-id="be4be-147">This example shows how to copy all of the files in the container **mysourcecontainer** in storage account **mysourcestorageaccount** to the container **mydestinationcontainer** in the **mydestinationstorageaccount** storage account.</span><span class="sxs-lookup"><span data-stu-id="be4be-147">This example shows how to copy all of the files in the container **mysourcecontainer** in storage account **mysourcestorageaccount** to the container **mydestinationcontainer** in the **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="be4be-148">Replace the names of the storage accounts and containers with your own.</span><span class="sxs-lookup"><span data-stu-id="be4be-148">Replace the names of the storage accounts and containers with your own.</span></span> <span data-ttu-id="be4be-149">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span><span class="sxs-lookup"><span data-stu-id="be4be-149">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="be4be-150">If you only want to copy a specific VHD in a container with multiple files, you can also specify the file name using the /Pattern switch.</span><span class="sxs-lookup"><span data-stu-id="be4be-150">If you only want to copy a specific VHD in a container with multiple files, you can also specify the file name using the /Pattern switch.</span></span> <span data-ttu-id="be4be-151">In this example, only the file named **myFileName.vhd** will be copied.</span><span class="sxs-lookup"><span data-stu-id="be4be-151">In this example, only the file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="be4be-152">When it is finished, you will get a message that looks something like:</span><span class="sxs-lookup"><span data-stu-id="be4be-152">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

## <a name="troubleshooting"></a><span data-ttu-id="be4be-153">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="be4be-153">Troubleshooting</span></span>
* <span data-ttu-id="be4be-154">When you use AZCopy, if you see the error "Server failed to authenticate the request", make sure the value of the Authorization header is formed correctly including the signature.</span><span class="sxs-lookup"><span data-stu-id="be4be-154">When you use AZCopy, if you see the error "Server failed to authenticate the request", make sure the value of the Authorization header is formed correctly including the signature.</span></span> <span data-ttu-id="be4be-155">If you are using Key 2 or the secondary storage key, try using the primary or 1st storage key.</span><span class="sxs-lookup"><span data-stu-id="be4be-155">If you are using Key 2 or the secondary storage key, try using the primary or 1st storage key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be4be-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="be4be-156">Next steps</span></span>
* <span data-ttu-id="be4be-157">You can create a new VM by [attaching the copy of the VHD to a VM as an OS disk](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="be4be-157">You can create a new VM by [attaching the copy of the VHD to a VM as an OS disk](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

