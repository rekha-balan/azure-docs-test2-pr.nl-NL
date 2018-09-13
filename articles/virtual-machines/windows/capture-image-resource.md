---
title: Create a managed image in Azure | Microsoft Docs
description: Create a managed image of a generalized VM or VHD in Azure. Images can be used to create multiple VMs that use managed disks.
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: c5db143508b2ce46c9f47a0514cc9bd053b6613d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554161"
---
# <a name="capture-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="e93ea-104">Capture a managed image of a generalized VM in Azure</span><span class="sxs-lookup"><span data-stu-id="e93ea-104">Capture a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="e93ea-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disks in a storage account.</span><span class="sxs-lookup"><span data-stu-id="e93ea-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disks in a storage account.</span></span> <span data-ttu-id="e93ea-106">The image can then be used to create multiple VMs that use managed disks for storage.</span><span class="sxs-lookup"><span data-stu-id="e93ea-106">The image can then be used to create multiple VMs that use managed disks for storage.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="e93ea-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e93ea-107">Prerequisites</span></span>
<span data-ttu-id="e93ea-108">You need to have already [generalized the VM](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and Stop\deallocatted the VM.</span><span class="sxs-lookup"><span data-stu-id="e93ea-108">You need to have already [generalized the VM](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and Stop\deallocatted the VM.</span></span> <span data-ttu-id="e93ea-109">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span><span class="sxs-lookup"><span data-stu-id="e93ea-109">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span>



## <a name="create-a-managed-image-in-the-portal"></a><span data-ttu-id="e93ea-110">Create a managed image in the portal</span><span class="sxs-lookup"><span data-stu-id="e93ea-110">Create a managed image in the portal</span></span> 

1. <span data-ttu-id="e93ea-111">Open the [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e93ea-111">Open the [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e93ea-112">Click the plus sign to create a new resource.</span><span class="sxs-lookup"><span data-stu-id="e93ea-112">Click the plus sign to create a new resource.</span></span>
3. <span data-ttu-id="e93ea-113">In the filter search, type **Image**.</span><span class="sxs-lookup"><span data-stu-id="e93ea-113">In the filter search, type **Image**.</span></span>
4. <span data-ttu-id="e93ea-114">Select **Image** from the results.</span><span class="sxs-lookup"><span data-stu-id="e93ea-114">Select **Image** from the results.</span></span>
5. <span data-ttu-id="e93ea-115">In the **Image** blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e93ea-115">In the **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="e93ea-116">In **Name**, type a name for the image.</span><span class="sxs-lookup"><span data-stu-id="e93ea-116">In **Name**, type a name for the image.</span></span>
7. <span data-ttu-id="e93ea-117">If you have more than one subscription, select the correct one from the **Subscription** drop-down.</span><span class="sxs-lookup"><span data-stu-id="e93ea-117">If you have more than one subscription, select the correct one from the **Subscription** drop-down.</span></span>
7. <span data-ttu-id="e93ea-118">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group to use from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="e93ea-118">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group to use from the drop-down list.</span></span>
8. <span data-ttu-id="e93ea-119">In **Location**, choose the location of your resource group.</span><span class="sxs-lookup"><span data-stu-id="e93ea-119">In **Location**, choose the location of your resource group.</span></span>
9. <span data-ttu-id="e93ea-120">In **OS type** select the type of operating system, either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="e93ea-120">In **OS type** select the type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="e93ea-121">In **Storage blob**, click **Browse** to look for the VHD in your Azure storage.</span><span class="sxs-lookup"><span data-stu-id="e93ea-121">In **Storage blob**, click **Browse** to look for the VHD in your Azure storage.</span></span>
12. <span data-ttu-id="e93ea-122">In **Account type** choose Standard_LRS or Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="e93ea-122">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="e93ea-123">Standard uses hard-disk drives and Premium uses solid-state drives.</span><span class="sxs-lookup"><span data-stu-id="e93ea-123">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="e93ea-124">Both use locally-redundant storage.</span><span class="sxs-lookup"><span data-stu-id="e93ea-124">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="e93ea-125">In **Disk caching** select the appropriate disk caching option.</span><span class="sxs-lookup"><span data-stu-id="e93ea-125">In **Disk caching** select the appropriate disk caching option.</span></span> <span data-ttu-id="e93ea-126">The options are **None**, **Read-only** and **Read\write**.</span><span class="sxs-lookup"><span data-stu-id="e93ea-126">The options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="e93ea-127">Optional: You can also add an existing data disk to the image by clicking **+ Add data disk**.</span><span class="sxs-lookup"><span data-stu-id="e93ea-127">Optional: You can also add an existing data disk to the image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="e93ea-128">When you are done making your selections, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e93ea-128">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="e93ea-129">After the image is created, you will see it as an **Image** resource in the list of resources in the resource group you chose.</span><span class="sxs-lookup"><span data-stu-id="e93ea-129">After the image is created, you will see it as an **Image** resource in the list of resources in the resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="e93ea-130">Create a managed image of a VM using Powershell</span><span class="sxs-lookup"><span data-stu-id="e93ea-130">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="e93ea-131">Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS Disk and any data disks.</span><span class="sxs-lookup"><span data-stu-id="e93ea-131">Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS Disk and any data disks.</span></span>


<span data-ttu-id="e93ea-132">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="e93ea-132">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="e93ea-133">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="e93ea-133">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="e93ea-134">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="e93ea-134">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>


1. <span data-ttu-id="e93ea-135">Create some variables.</span><span class="sxs-lookup"><span data-stu-id="e93ea-135">Create some variables.</span></span> 
    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="e93ea-136">Make sure the VM has been deallocated.</span><span class="sxs-lookup"><span data-stu-id="e93ea-136">Make sure the VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="e93ea-137">Set the status of the virtual machine to **Generalized**.</span><span class="sxs-lookup"><span data-stu-id="e93ea-137">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="e93ea-138">Get the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e93ea-138">Get the virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="e93ea-139">Create the image configuration.</span><span class="sxs-lookup"><span data-stu-id="e93ea-139">Create the image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="e93ea-140">Create the image.</span><span class="sxs-lookup"><span data-stu-id="e93ea-140">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="e93ea-141">Create a managed image of a VHD in PowerShell</span><span class="sxs-lookup"><span data-stu-id="e93ea-141">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="e93ea-142">Create a managed image using your generalized OS VHD.</span><span class="sxs-lookup"><span data-stu-id="e93ea-142">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="e93ea-143">First, set the common parameters:</span><span class="sxs-lookup"><span data-stu-id="e93ea-143">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="e93ea-144">Step\deallocate the VM.</span><span class="sxs-lookup"><span data-stu-id="e93ea-144">Step\deallocate the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="e93ea-145">Mark the VM as generalized.</span><span class="sxs-lookup"><span data-stu-id="e93ea-145">Mark the VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="e93ea-146">Create the image using your generalized OS VHD.</span><span class="sxs-lookup"><span data-stu-id="e93ea-146">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="e93ea-147">Create a managed image from a snapshot using Powershell</span><span class="sxs-lookup"><span data-stu-id="e93ea-147">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="e93ea-148">You can also create a managed image from a snapshot of the VHD from a generalized VM.</span><span class="sxs-lookup"><span data-stu-id="e93ea-148">You can also create a managed image from a snapshot of the VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="e93ea-149">Create some variables.</span><span class="sxs-lookup"><span data-stu-id="e93ea-149">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="e93ea-150">Get the snapshot.</span><span class="sxs-lookup"><span data-stu-id="e93ea-150">Get the snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="e93ea-151">Create the image configuration.</span><span class="sxs-lookup"><span data-stu-id="e93ea-151">Create the image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="e93ea-152">Create the image.</span><span class="sxs-lookup"><span data-stu-id="e93ea-152">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="e93ea-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="e93ea-153">Next steps</span></span>
- <span data-ttu-id="e93ea-154">Now you can [create a VM from the generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e93ea-154">Now you can [create a VM from the generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>  

