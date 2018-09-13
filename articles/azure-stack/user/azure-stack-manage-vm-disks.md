---
title: Manage VM disks in Azure Stack | Microsoft Docs
description: Provision disks for virtual machines in Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 4e5833cf-4790-4146-82d6-737975fb06ba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/05/2018
ms.author: mabrigg
ms.reviewer: jiahan
ms.openlocfilehash: bdf31c72fbcd8941161e6b9df0a490df7f6a16e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871430"
---
# <a name="provision-virtual-machine-disk-storage-in-azure-stack"></a><span data-ttu-id="7b94b-103">Provision virtual machine disk storage in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7b94b-103">Provision virtual machine disk storage in Azure Stack</span></span>

<span data-ttu-id="7b94b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="7b94b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="7b94b-105">This article describes how to provision virtual machine disk storage by using the Azure Stack portal or by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b94b-105">This article describes how to provision virtual machine disk storage by using the Azure Stack portal or by using PowerShell.</span></span>

## <a name="overview"></a><span data-ttu-id="7b94b-106">Overview</span><span class="sxs-lookup"><span data-stu-id="7b94b-106">Overview</span></span>

<span data-ttu-id="7b94b-107">Beginning with version 1808, Azure Stack supports the use of managed disks and unmanaged disks on virtual machines, as both an operating system (OS) and a data disk.</span><span class="sxs-lookup"><span data-stu-id="7b94b-107">Beginning with version 1808, Azure Stack supports the use of managed disks and unmanaged disks on virtual machines, as both an operating system (OS) and a data disk.</span></span> <span data-ttu-id="7b94b-108">Prior to version 1808, only unmanaged disks are supported.</span><span class="sxs-lookup"><span data-stu-id="7b94b-108">Prior to version 1808, only unmanaged disks are supported.</span></span> 

<span data-ttu-id="7b94b-109">**[Managed disks](https://docs.microsoft.com/azure/virtual-machines/windows/about-disks-and-vhds#managed-disks)** simplify disk management for Azure IaaS VMs by managing the storage accounts associated with the VM disks.</span><span class="sxs-lookup"><span data-stu-id="7b94b-109">**[Managed disks](https://docs.microsoft.com/azure/virtual-machines/windows/about-disks-and-vhds#managed-disks)** simplify disk management for Azure IaaS VMs by managing the storage accounts associated with the VM disks.</span></span> <span data-ttu-id="7b94b-110">You only have to specify the size of disk you need, and Azure Stack creates and manages the disk for you.</span><span class="sxs-lookup"><span data-stu-id="7b94b-110">You only have to specify the size of disk you need, and Azure Stack creates and manages the disk for you.</span></span>

<span data-ttu-id="7b94b-111">**[Unmanaged disks](https://docs.microsoft.com/azure/virtual-machines/windows/about-disks-and-vhds#unmanaged-disks)**, require that you create a [storage account](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account) to store the disks.</span><span class="sxs-lookup"><span data-stu-id="7b94b-111">**[Unmanaged disks](https://docs.microsoft.com/azure/virtual-machines/windows/about-disks-and-vhds#unmanaged-disks)**, require that you create a [storage account](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account) to store the disks.</span></span> <span data-ttu-id="7b94b-112">The disks you create are referred to as VM disks and are stored in containers in the storage account.</span><span class="sxs-lookup"><span data-stu-id="7b94b-112">The disks you create are referred to as VM disks and are stored in containers in the storage account.</span></span>

 

### <a name="best-practice-guidelines"></a><span data-ttu-id="7b94b-113">Best practice guidelines</span><span class="sxs-lookup"><span data-stu-id="7b94b-113">Best practice guidelines</span></span>

<span data-ttu-id="7b94b-114">To improve performance and reduce the overall costs, we recommend you place each VM disk in a separate container.</span><span class="sxs-lookup"><span data-stu-id="7b94b-114">To improve performance and reduce the overall costs, we recommend you place each VM disk in a separate container.</span></span> <span data-ttu-id="7b94b-115">A container should hold either an OS disk or a data disk, but not both at the same time.</span><span class="sxs-lookup"><span data-stu-id="7b94b-115">A container should hold either an OS disk or a data disk, but not both at the same time.</span></span> <span data-ttu-id="7b94b-116">(However, there's nothing to prevent you from putting both kinds of disk in the same container.)</span><span class="sxs-lookup"><span data-stu-id="7b94b-116">(However, there's nothing to prevent you from putting both kinds of disk in the same container.)</span></span>

<span data-ttu-id="7b94b-117">If you add one or more data disks to a VM, use additional containers as a location to store these disks.</span><span class="sxs-lookup"><span data-stu-id="7b94b-117">If you add one or more data disks to a VM, use additional containers as a location to store these disks.</span></span> <span data-ttu-id="7b94b-118">The OS disk for additional VMs should also be in their own containers.</span><span class="sxs-lookup"><span data-stu-id="7b94b-118">The OS disk for additional VMs should also be in their own containers.</span></span>

<span data-ttu-id="7b94b-119">When you create multiple VMs, you can reuse the same storage account for each new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7b94b-119">When you create multiple VMs, you can reuse the same storage account for each new virtual machine.</span></span> <span data-ttu-id="7b94b-120">Only the containers you create should be unique.</span><span class="sxs-lookup"><span data-stu-id="7b94b-120">Only the containers you create should be unique.</span></span>

### <a name="adding-new-disks"></a><span data-ttu-id="7b94b-121">Adding new disks</span><span class="sxs-lookup"><span data-stu-id="7b94b-121">Adding new disks</span></span>

<span data-ttu-id="7b94b-122">The following table summarizes how to add disks by using the portal and by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b94b-122">The following table summarizes how to add disks by using the portal and by using PowerShell.</span></span>

| <span data-ttu-id="7b94b-123">Method</span><span class="sxs-lookup"><span data-stu-id="7b94b-123">Method</span></span> | <span data-ttu-id="7b94b-124">Options</span><span class="sxs-lookup"><span data-stu-id="7b94b-124">Options</span></span>
|-|-|
|[<span data-ttu-id="7b94b-125">User portal</span><span class="sxs-lookup"><span data-stu-id="7b94b-125">User portal</span></span>](#use-the-portal-to-add-additional-disks-to-a-vm)|<span data-ttu-id="7b94b-126">- Add new data disks to an existing VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-126">- Add new data disks to an existing VM.</span></span> <span data-ttu-id="7b94b-127">New disks are created by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7b94b-127">New disks are created by Azure Stack.</span></span> </br> </br><span data-ttu-id="7b94b-128">- Add an existing disk (.vhd) file to a  previously provisioned VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-128">- Add an existing disk (.vhd) file to a  previously provisioned VM.</span></span> <span data-ttu-id="7b94b-129">To do this, you must prepare the .vhd  and then upload the file to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7b94b-129">To do this, you must prepare the .vhd  and then upload the file to Azure Stack.</span></span> |
|[<span data-ttu-id="7b94b-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b94b-130">PowerShell</span></span>](#use-powershell-to-add-multiple-unmanaged-disks-to-a-vm) | <span data-ttu-id="7b94b-131">- Create a new VM with an OS disk, and at the same time add one or more data disks to that VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-131">- Create a new VM with an OS disk, and at the same time add one or more data disks to that VM.</span></span> |

## <a name="use-the-portal-to-add-disks-to-a-vm"></a><span data-ttu-id="7b94b-132">Use the portal to add disks to a VM</span><span class="sxs-lookup"><span data-stu-id="7b94b-132">Use the portal to add disks to a VM</span></span>

<span data-ttu-id="7b94b-133">By default, when you use the portal to create a VM for most marketplace items, only the OS disk is created.</span><span class="sxs-lookup"><span data-stu-id="7b94b-133">By default, when you use the portal to create a VM for most marketplace items, only the OS disk is created.</span></span>

<span data-ttu-id="7b94b-134">After you create a VM, you can use the portal to:</span><span class="sxs-lookup"><span data-stu-id="7b94b-134">After you create a VM, you can use the portal to:</span></span>
* <span data-ttu-id="7b94b-135">Create a new data disk and attach it to the VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-135">Create a new data disk and attach it to the VM.</span></span>
* <span data-ttu-id="7b94b-136">Upload an existing data disk and attach it to the VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-136">Upload an existing data disk and attach it to the VM.</span></span>

<span data-ttu-id="7b94b-137">Each unmanaged disk you add should be put in a separate container.</span><span class="sxs-lookup"><span data-stu-id="7b94b-137">Each unmanaged disk you add should be put in a separate container.</span></span>

>[!NOTE]
><span data-ttu-id="7b94b-138">Disks created and managed by Azure are called [managed disks](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview).</span><span class="sxs-lookup"><span data-stu-id="7b94b-138">Disks created and managed by Azure are called [managed disks](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview).</span></span>

### <a name="use-the-portal-to-create-and-attach-a-new-data-disk"></a><span data-ttu-id="7b94b-139">Use the portal to create and attach a new data disk</span><span class="sxs-lookup"><span data-stu-id="7b94b-139">Use the portal to create and attach a new data disk</span></span>

1.  <span data-ttu-id="7b94b-140">In the portal, choose **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="7b94b-140">In the portal, choose **Virtual machines**.</span></span>    
    <span data-ttu-id="7b94b-141">![Example: VM dashboard](media/azure-stack-manage-vm-disks/vm-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-141">![Example: VM dashboard](media/azure-stack-manage-vm-disks/vm-dashboard.png)</span></span>

2.  <span data-ttu-id="7b94b-142">Select a virtual machine that has previously been provisioned.</span><span class="sxs-lookup"><span data-stu-id="7b94b-142">Select a virtual machine that has previously been provisioned.</span></span>   
    ![Example: Select a VM in the dashboard](media/azure-stack-manage-vm-disks/select-a-vm.png)

3.  <span data-ttu-id="7b94b-144">For the virtual machine, select **Disks** > **Attach new**.</span><span class="sxs-lookup"><span data-stu-id="7b94b-144">For the virtual machine, select **Disks** > **Attach new**.</span></span>       
    <span data-ttu-id="7b94b-145">![Example: Attach a new disk to the vm](media/azure-stack-manage-vm-disks/Attach-disks.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-145">![Example: Attach a new disk to the vm](media/azure-stack-manage-vm-disks/Attach-disks.png)</span></span>    

4.  <span data-ttu-id="7b94b-146">In the **Attach new disk** pane, select **Location**.</span><span class="sxs-lookup"><span data-stu-id="7b94b-146">In the **Attach new disk** pane, select **Location**.</span></span> <span data-ttu-id="7b94b-147">By default, the Location is set to the same container that holds the OS disk.</span><span class="sxs-lookup"><span data-stu-id="7b94b-147">By default, the Location is set to the same container that holds the OS disk.</span></span>      
    <span data-ttu-id="7b94b-148">![Example: Set the disk location](media/azure-stack-manage-vm-disks/disk-location.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-148">![Example: Set the disk location](media/azure-stack-manage-vm-disks/disk-location.png)</span></span>

5.  <span data-ttu-id="7b94b-149">Select the **Storage account** to use.</span><span class="sxs-lookup"><span data-stu-id="7b94b-149">Select the **Storage account** to use.</span></span> <span data-ttu-id="7b94b-150">Next, select the **Container** where you want to put the data disk.</span><span class="sxs-lookup"><span data-stu-id="7b94b-150">Next, select the **Container** where you want to put the data disk.</span></span> <span data-ttu-id="7b94b-151">From the **Containers** page, you can create a new container if you want.</span><span class="sxs-lookup"><span data-stu-id="7b94b-151">From the **Containers** page, you can create a new container if you want.</span></span> <span data-ttu-id="7b94b-152">You can then change the location for the new disk to its own container.</span><span class="sxs-lookup"><span data-stu-id="7b94b-152">You can then change the location for the new disk to its own container.</span></span> <span data-ttu-id="7b94b-153">When you use a separate container for each disk, you distribute the placement of the data disk that can improve performance.</span><span class="sxs-lookup"><span data-stu-id="7b94b-153">When you use a separate container for each disk, you distribute the placement of the data disk that can improve performance.</span></span> <span data-ttu-id="7b94b-154">Choose **Select** to save the selection.</span><span class="sxs-lookup"><span data-stu-id="7b94b-154">Choose **Select** to save the selection.</span></span>     
    <span data-ttu-id="7b94b-155">![Example: Select a container](media/azure-stack-manage-vm-disks/select-container.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-155">![Example: Select a container](media/azure-stack-manage-vm-disks/select-container.png)</span></span>

6.  <span data-ttu-id="7b94b-156">In the **Attach new disk** page, update the **Name**, **Type**, **Size**, and **Host caching** settings of the disk.</span><span class="sxs-lookup"><span data-stu-id="7b94b-156">In the **Attach new disk** page, update the **Name**, **Type**, **Size**, and **Host caching** settings of the disk.</span></span> <span data-ttu-id="7b94b-157">Then select **OK** to save the new disk configuration for the VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-157">Then select **OK** to save the new disk configuration for the VM.</span></span>  
    <span data-ttu-id="7b94b-158">![Example: Complete disk attachment](media/azure-stack-manage-vm-disks/complete-disk-attach.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-158">![Example: Complete disk attachment](media/azure-stack-manage-vm-disks/complete-disk-attach.png)</span></span>  

7.  <span data-ttu-id="7b94b-159">After Azure Stack creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **DATA DISKS**.</span><span class="sxs-lookup"><span data-stu-id="7b94b-159">After Azure Stack creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **DATA DISKS**.</span></span>   
    <span data-ttu-id="7b94b-160">![Example: View disk](media/azure-stack-manage-vm-disks/view-data-disk.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-160">![Example: View disk](media/azure-stack-manage-vm-disks/view-data-disk.png)</span></span>


### <a name="attach-an-existing-data-disk-to-a-vm"></a><span data-ttu-id="7b94b-161">Attach an existing data disk to a VM</span><span class="sxs-lookup"><span data-stu-id="7b94b-161">Attach an existing data disk to a VM</span></span>

1.  <span data-ttu-id="7b94b-162">[Prepare a .vhd file](https://docs.microsoft.com/azure/virtual-machines/windows/classic/createupload-vhd) for use as data disk for a VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-162">[Prepare a .vhd file](https://docs.microsoft.com/azure/virtual-machines/windows/classic/createupload-vhd) for use as data disk for a VM.</span></span> <span data-ttu-id="7b94b-163">Upload that .vhd file to a storage account that you use with the VM that you want to attach the .vhd file to.</span><span class="sxs-lookup"><span data-stu-id="7b94b-163">Upload that .vhd file to a storage account that you use with the VM that you want to attach the .vhd file to.</span></span>

  <span data-ttu-id="7b94b-164">Plan to use a different container to hold the .vhd file than the container that holds the OS disk.</span><span class="sxs-lookup"><span data-stu-id="7b94b-164">Plan to use a different container to hold the .vhd file than the container that holds the OS disk.</span></span>   
  ![Example: Upload a VHD file](media/azure-stack-manage-vm-disks/upload-vhd.png)

2.  <span data-ttu-id="7b94b-166">After the .vhd file is uploaded, you are ready to attach the VHD to a VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-166">After the .vhd file is uploaded, you are ready to attach the VHD to a VM.</span></span> <span data-ttu-id="7b94b-167">In the menu on the left, select  **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="7b94b-167">In the menu on the left, select  **Virtual machines**.</span></span>  
 <span data-ttu-id="7b94b-168">![Example: Select a VM in the dashboard](media/azure-stack-manage-vm-disks/vm-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-168">![Example: Select a VM in the dashboard](media/azure-stack-manage-vm-disks/vm-dashboard.png)</span></span>

3.  <span data-ttu-id="7b94b-169">Choose the virtual machine from the list.</span><span class="sxs-lookup"><span data-stu-id="7b94b-169">Choose the virtual machine from the list.</span></span>    
  ![Example: Select a VM in the dashboard](media/azure-stack-manage-vm-disks/select-a-vm.png)

4.  <span data-ttu-id="7b94b-171">On the page for the virtual machine, select **Disks** > **Attach existing**.</span><span class="sxs-lookup"><span data-stu-id="7b94b-171">On the page for the virtual machine, select **Disks** > **Attach existing**.</span></span>   
  <span data-ttu-id="7b94b-172">![Example: Attach an existing disk](media/azure-stack-manage-vm-disks/attach-disks2.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-172">![Example: Attach an existing disk](media/azure-stack-manage-vm-disks/attach-disks2.png)</span></span>

5.  <span data-ttu-id="7b94b-173">In the **Attach existing disk** page, select **VHD File**.</span><span class="sxs-lookup"><span data-stu-id="7b94b-173">In the **Attach existing disk** page, select **VHD File**.</span></span> <span data-ttu-id="7b94b-174">The **Storage accounts** page opens.</span><span class="sxs-lookup"><span data-stu-id="7b94b-174">The **Storage accounts** page opens.</span></span>    
  <span data-ttu-id="7b94b-175">![Example: Select a VHD file](media/azure-stack-manage-vm-disks/select-vhd.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-175">![Example: Select a VHD file](media/azure-stack-manage-vm-disks/select-vhd.png)</span></span>

6.  <span data-ttu-id="7b94b-176">Under **Storage accounts**, select the account to use, and then choose a container that holds the .vhd file you previously uploaded.</span><span class="sxs-lookup"><span data-stu-id="7b94b-176">Under **Storage accounts**, select the account to use, and then choose a container that holds the .vhd file you previously uploaded.</span></span> <span data-ttu-id="7b94b-177">Select the .vhd file, and then choose **Select** to save the selection.</span><span class="sxs-lookup"><span data-stu-id="7b94b-177">Select the .vhd file, and then choose **Select** to save the selection.</span></span>    
  <span data-ttu-id="7b94b-178">![Example: Select a container](media/azure-stack-manage-vm-disks/select-container2.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-178">![Example: Select a container](media/azure-stack-manage-vm-disks/select-container2.png)</span></span>

7.  <span data-ttu-id="7b94b-179">Under **Attach existing disk**, the file you selected is listed under **VHD File**.</span><span class="sxs-lookup"><span data-stu-id="7b94b-179">Under **Attach existing disk**, the file you selected is listed under **VHD File**.</span></span> <span data-ttu-id="7b94b-180">Update the **Host caching** setting of the disk, and then select **OK** to save the new disk configuration for the VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-180">Update the **Host caching** setting of the disk, and then select **OK** to save the new disk configuration for the VM.</span></span>    
  <span data-ttu-id="7b94b-181">![Example: Attach the VHD file](media/azure-stack-manage-vm-disks/attach-vhd.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-181">![Example: Attach the VHD file](media/azure-stack-manage-vm-disks/attach-vhd.png)</span></span>

8.  <span data-ttu-id="7b94b-182">After Azure Stack creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="7b94b-182">After Azure Stack creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>   
  <span data-ttu-id="7b94b-183">![Example: Complete the disk attach](media/azure-stack-manage-vm-disks/complete-disk-attach.png)</span><span class="sxs-lookup"><span data-stu-id="7b94b-183">![Example: Complete the disk attach](media/azure-stack-manage-vm-disks/complete-disk-attach.png)</span></span>


## <a name="use-powershell-to-add-multiple-unmanaged-disks-to-a-vm"></a><span data-ttu-id="7b94b-184">Use PowerShell to add multiple unmanaged disks to a VM</span><span class="sxs-lookup"><span data-stu-id="7b94b-184">Use PowerShell to add multiple unmanaged disks to a VM</span></span>
<span data-ttu-id="7b94b-185">You can use PowerShell to provision a VM and add a new data disk or attach a pre-existing **.vhd** file as a data disk.</span><span class="sxs-lookup"><span data-stu-id="7b94b-185">You can use PowerShell to provision a VM and add a new data disk or attach a pre-existing **.vhd** file as a data disk.</span></span>

<span data-ttu-id="7b94b-186">The **Add-AzureRmVMDataDisk** cmdlet adds a data disk to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7b94b-186">The **Add-AzureRmVMDataDisk** cmdlet adds a data disk to a virtual machine.</span></span> <span data-ttu-id="7b94b-187">You can add a data disk when you create a virtual machine, or you can add a data disk to an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7b94b-187">You can add a data disk when you create a virtual machine, or you can add a data disk to an existing virtual machine.</span></span> <span data-ttu-id="7b94b-188">Specify the **VhdUri** parameter to distribute the disks to different containers.</span><span class="sxs-lookup"><span data-stu-id="7b94b-188">Specify the **VhdUri** parameter to distribute the disks to different containers.</span></span>

### <a name="add-data-disks-to-a-new-virtual-machine"></a><span data-ttu-id="7b94b-189">Add data disks to a new virtual machine</span><span class="sxs-lookup"><span data-stu-id="7b94b-189">Add data disks to a new virtual machine</span></span>
<span data-ttu-id="7b94b-190">The following examples use PowerShell commands to create a VM with three data disks, each placed in a different container.</span><span class="sxs-lookup"><span data-stu-id="7b94b-190">The following examples use PowerShell commands to create a VM with three data disks, each placed in a different container.</span></span>

<span data-ttu-id="7b94b-191">The first command creates a virtual machine object, and then stores it in the *$VirtualMachine* variable.</span><span class="sxs-lookup"><span data-stu-id="7b94b-191">The first command creates a virtual machine object, and then stores it in the *$VirtualMachine* variable.</span></span> <span data-ttu-id="7b94b-192">The command assigns a name and size to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7b94b-192">The command assigns a name and size to the virtual machine.</span></span>
  ```
  $VirtualMachine = New-AzureRmVMConfig -VMName "VirtualMachine" `
                                      -VMSize "Standard_A2"
  ```

<span data-ttu-id="7b94b-193">The next three commands assign paths of three data disks to the *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, and *$DataDiskVhdUri03* variables.</span><span class="sxs-lookup"><span data-stu-id="7b94b-193">The next three commands assign paths of three data disks to the *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, and *$DataDiskVhdUri03* variables.</span></span> <span data-ttu-id="7b94b-194">Define a different path name in the URL to distribute the disks to different containers.</span><span class="sxs-lookup"><span data-stu-id="7b94b-194">Define a different path name in the URL to distribute the disks to different containers.</span></span>     
  ```
  $DataDiskVhdUri01 = "https://contoso.blob.local.azurestack.external/test1/data1.vhd"
  ```

  ```
  $DataDiskVhdUri02 = "https://contoso.blob.local.azurestack.external/test2/data2.vhd"
  ```

  ```
  $DataDiskVhdUri03 = "https://contoso.blob.local.azurestack.external/test3/data3.vhd"
  ```

<span data-ttu-id="7b94b-195">The final three commands add data disks to the virtual machine stored in *$VirtualMachine*.</span><span class="sxs-lookup"><span data-stu-id="7b94b-195">The final three commands add data disks to the virtual machine stored in *$VirtualMachine*.</span></span> <span data-ttu-id="7b94b-196">Each command specifies the name, location, and additional properties of the disk.</span><span class="sxs-lookup"><span data-stu-id="7b94b-196">Each command specifies the name, location, and additional properties of the disk.</span></span> <span data-ttu-id="7b94b-197">The URI of each disk is stored in *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, and *$DataDiskVhdUri03*.</span><span class="sxs-lookup"><span data-stu-id="7b94b-197">The URI of each disk is stored in *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, and *$DataDiskVhdUri03*.</span></span>
  ```
  $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name 'DataDisk1' `
                  -Caching 'ReadOnly' -DiskSizeInGB 10 -Lun 0 `
                  -VhdUri $DataDiskVhdUri01 -CreateOption Empty
  ```

  ```
  $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name 'DataDisk2' `
                 -Caching 'ReadOnly' -DiskSizeInGB 11 -Lun 1 `
                 -VhdUri $DataDiskVhdUri02 -CreateOption Empty
  ```

  ```
  $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name 'DataDisk3' `
                  -Caching 'ReadOnly' -DiskSizeInGB 12 -Lun 2 `
                  -VhdUri $DataDiskVhdUri03 -CreateOption Empty
  ```

<span data-ttu-id="7b94b-198">Use the following PowerShell commands to add the OS disk and network configuration to the VM, and then start the new VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-198">Use the following PowerShell commands to add the OS disk and network configuration to the VM, and then start the new VM.</span></span>
  ```
  #set variables
  $rgName = "myResourceGroup"
  $location = "local"
  #Set OS Disk
  $osDiskUri = "https://contoso.blob.local.azurestack.external/vhds/osDisk.vhd"
  $osDiskName = "osDisk"

  $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $osDiskName -VhdUri $osDiskUri `
      -CreateOption FromImage -Windows

  # Create a subnet configuration
  $subnetName = "mySubNet"
  $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24

  # Create a vnet configuration
  $vnetName = "myVnetName"
  $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
      -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet

  # Create a public IP
  $ipName = "myIP"
  $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
      -AllocationMethod Dynamic

  # Create a network security group cnfiguration
  $nsgName = "myNsg"
  $rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
      -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
      -SourceAddressPrefix Internet -SourcePortRange * `
      -DestinationAddressPrefix * -DestinationPortRange 3389
  $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
      -Name $nsgName -SecurityRules $rdpRule

  # Create a NIC configuration
  $nicName = "myNicName"
  $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
  -Location $location -SubnetId $vnet.Subnets[0].Id -NetworkSecurityGroupId $nsg.Id -PublicIpAddressId $pip.Id

  #Create the new VM
  $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName VirtualMachine | `
      Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
      -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
  New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $VirtualMachine
  ```



### <a name="add-data-disks-to-an-existing-virtual-machine"></a><span data-ttu-id="7b94b-199">Add data disks to an existing virtual machine</span><span class="sxs-lookup"><span data-stu-id="7b94b-199">Add data disks to an existing virtual machine</span></span>
<span data-ttu-id="7b94b-200">The following examples use PowerShell commands to add three data disks to an existing VM.</span><span class="sxs-lookup"><span data-stu-id="7b94b-200">The following examples use PowerShell commands to add three data disks to an existing VM.</span></span>
<span data-ttu-id="7b94b-201">The first command gets the virtual machine named VirtualMachine by using the **Get-AzureRmVM** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7b94b-201">The first command gets the virtual machine named VirtualMachine by using the **Get-AzureRmVM** cmdlet.</span></span> <span data-ttu-id="7b94b-202">The command stores the virtual machine in the *$VirtualMachine* variable.</span><span class="sxs-lookup"><span data-stu-id="7b94b-202">The command stores the virtual machine in the *$VirtualMachine* variable.</span></span>
  ```
  $VirtualMachine = Get-AzureRmVM -ResourceGroupName "myResourceGroup" `
                                  -Name "VirtualMachine"
  ```
<span data-ttu-id="7b94b-203">The next three commands assign paths of three data disks to the $DataDiskVhdUri01, $DataDiskVhdUri02, and $DataDiskVhdUri03 variables.</span><span class="sxs-lookup"><span data-stu-id="7b94b-203">The next three commands assign paths of three data disks to the $DataDiskVhdUri01, $DataDiskVhdUri02, and $DataDiskVhdUri03 variables.</span></span>  <span data-ttu-id="7b94b-204">The different path names in the vhduri indicate different containers for the disk placement.</span><span class="sxs-lookup"><span data-stu-id="7b94b-204">The different path names in the vhduri indicate different containers for the disk placement.</span></span>
  ```
  $DataDiskVhdUri01 = "https://contoso.blob.local.azurestack.external/test1/data1.vhd"
  ```
  ```
  $DataDiskVhdUri02 = "https://contoso.blob.local.azurestack.external/test2/data2.vhd"
  ```
  ```
  $DataDiskVhdUri03 = "https://contoso.blob.local.azurestack.external/test3/data3.vhd"
  ```


  <span data-ttu-id="7b94b-205">The next three commands add the data disks to the virtual machine stored in the *$VirtualMachine* variable.</span><span class="sxs-lookup"><span data-stu-id="7b94b-205">The next three commands add the data disks to the virtual machine stored in the *$VirtualMachine* variable.</span></span> <span data-ttu-id="7b94b-206">Each command specifies the name, location, and additional properties of the disk.</span><span class="sxs-lookup"><span data-stu-id="7b94b-206">Each command specifies the name, location, and additional properties of the disk.</span></span> <span data-ttu-id="7b94b-207">The URI of each disk is stored in *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, and *$DataDiskVhdUri03*.</span><span class="sxs-lookup"><span data-stu-id="7b94b-207">The URI of each disk is stored in *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, and *$DataDiskVhdUri03*.</span></span>
  ```
  Add-AzureRmVMDataDisk -VM $VirtualMachine -Name "disk1" `
                        -VhdUri $DataDiskVhdUri01 -LUN 0 `
                        -Caching ReadOnly -DiskSizeinGB 10 -CreateOption Empty
  ```
  ```
  Add-AzureRmVMDataDisk -VM $VirtualMachine -Name "disk2" `
                        -VhdUri $DataDiskVhdUri02 -LUN 1 `
                        -Caching ReadOnly -DiskSizeinGB 11 -CreateOption Empty
  ```
  ```
  Add-AzureRmVMDataDisk -VM $VirtualMachine -Name "disk3" `
                        -VhdUri $DataDiskVhdUri03 -LUN 2 `
                        -Caching ReadOnly -DiskSizeinGB 12 -CreateOption Empty
  ```


  <span data-ttu-id="7b94b-208">The final command updates the state of the virtual machine stored in *$VirtualMachine* in -*ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="7b94b-208">The final command updates the state of the virtual machine stored in *$VirtualMachine* in -*ResourceGroupName*.</span></span>
  ```
  Update-AzureRmVM -ResourceGroupName "myResourceGroup" -VM $VirtualMachine
  ```
<!-- Pending scripts  

## Distribute the data disks of an existing VM
If you have a VM with more than one disk in the same container, the service operator of the Azure Stack deployment might ask you to redistribute the disks into individual containers.

To do so, use the scripts from the following location in GitHub. These scripts can be used to move the data disks to different containers.
-->

## <a name="next-steps"></a><span data-ttu-id="7b94b-209">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7b94b-209">Next Steps</span></span>
<span data-ttu-id="7b94b-210">To learn more about Azure Stack virtual machines, see [Considerations for Virtual Machines in Azure Stack](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-vm-considerations).</span><span class="sxs-lookup"><span data-stu-id="7b94b-210">To learn more about Azure Stack virtual machines, see [Considerations for Virtual Machines in Azure Stack](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-vm-considerations).</span></span>
