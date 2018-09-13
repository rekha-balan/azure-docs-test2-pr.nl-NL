---
title: Use a Windows troubleshooting VM in the Azure portal | Microsoft Docs
description: Learn how to troubleshoot Windows virtual machine issues in Azure by connecting the OS disk to a recovery VM using the Azure portal
services: virtual-machines-windows
documentationCenter: ''
authors: iainfoulds
manager: timlt
editor: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 12/12/2016
ms.author: iainfou
ms.openlocfilehash: 85c1f4a43b89056b55ca4d2814ef94a165262c5d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549921"
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="c6a3f-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c6a3f-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="c6a3f-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="c6a3f-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="c6a3f-106">This article details how to use the Azure portal to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-106">This article details how to use the Azure portal to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="c6a3f-107">Recovery process overview</span><span class="sxs-lookup"><span data-stu-id="c6a3f-107">Recovery process overview</span></span>
<span data-ttu-id="c6a3f-108">The troubleshooting process is as follows:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="c6a3f-109">Delete the VM encountering issues, keeping the virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="c6a3f-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="c6a3f-111">Connect to the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="c6a3f-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="c6a3f-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="c6a3f-114">Create a VM using the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-114">Create a VM using the original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="c6a3f-115">Determine boot issues</span><span class="sxs-lookup"><span data-stu-id="c6a3f-115">Determine boot issues</span></span>
<span data-ttu-id="c6a3f-116">To determine why your VM is not able to boot correctly, examine the boot diagnostics VM screenshot.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-116">To determine why your VM is not able to boot correctly, examine the boot diagnostics VM screenshot.</span></span> <span data-ttu-id="c6a3f-117">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-117">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="c6a3f-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="c6a3f-119">Click **Boot diagnostics** to view the screenshot.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-119">Click **Boot diagnostics** to view the screenshot.</span></span> <span data-ttu-id="c6a3f-120">Note any specific error messages or error codes to help determine why the VM is encountering an issue.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-120">Note any specific error messages or error codes to help determine why the VM is encountering an issue.</span></span> <span data-ttu-id="c6a3f-121">The following example shows a VM waiting on stopping services:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-121">The following example shows a VM waiting on stopping services:</span></span>

![Viewing VM boot diagnostics console logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/screenshot-error.png)

<span data-ttu-id="c6a3f-123">You can also click **Screenshot** to download a capture of the VM screenshot.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-123">You can also click **Screenshot** to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="c6a3f-124">View existing virtual hard disk details</span><span class="sxs-lookup"><span data-stu-id="c6a3f-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="c6a3f-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span><span class="sxs-lookup"><span data-stu-id="c6a3f-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="c6a3f-126">Select your resource group from the portal, then select your storage account.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-126">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="c6a3f-127">Click **Blobs**, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-127">Click **Blobs**, as in the following example:</span></span>

![Select storage blobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="c6a3f-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="c6a3f-130">Select the container to view a list of virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-130">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="c6a3f-131">Note the name of your VHD (the prefix is usually the name of your VM):</span><span class="sxs-lookup"><span data-stu-id="c6a3f-131">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![Identify VHD in storage container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="c6a3f-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![Copy existing virtual hard disk URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="c6a3f-135">Delete existing VM</span><span class="sxs-lookup"><span data-stu-id="c6a3f-135">Delete existing VM</span></span>
<span data-ttu-id="c6a3f-136">Virtual hard disks and VMs are two distinct resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="c6a3f-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="c6a3f-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span><span class="sxs-lookup"><span data-stu-id="c6a3f-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="c6a3f-139">Each virtual hard disk has a lease assigned when attached to a VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-139">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="c6a3f-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="c6a3f-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="c6a3f-142">The first step to recover your VM is to delete the VM resource itself.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-142">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="c6a3f-143">Deleting the VM leaves the virtual hard disks in your storage account.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-143">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="c6a3f-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="c6a3f-145">Select your VM in the portal, then click **Delete**:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-145">Select your VM in the portal, then click **Delete**:</span></span>

![VM boot diagnostics screenshot showing boot error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="c6a3f-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="c6a3f-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="c6a3f-149">Attach existing virtual hard disk to another VM</span><span class="sxs-lookup"><span data-stu-id="c6a3f-149">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="c6a3f-150">For the next few steps, you use another VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-150">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="c6a3f-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="c6a3f-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="c6a3f-153">Choose or create another VM to use for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-153">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="c6a3f-154">Select your resource group from the portal, then select your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-154">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="c6a3f-155">Select **Disks** and then click **Attach existing**:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Attach existing disk in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="c6a3f-157">To select your existing virtual hard disk, click **VHD File**:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-157">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![Browse for existing VHD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="c6a3f-159">Select your storage account and container, then click your existing VHD.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="c6a3f-160">Click the **Select** button to confirm your choice:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-160">Click the **Select** button to confirm your choice:</span></span>

    ![Select your existing VHD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="c6a3f-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![Confirm attaching existing virtual hard disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="c6a3f-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Existing virtual hard disk attached as a data disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="c6a3f-166">Mount the attached data disk</span><span class="sxs-lookup"><span data-stu-id="c6a3f-166">Mount the attached data disk</span></span>

1. <span data-ttu-id="c6a3f-167">Open a Remote Desktop connection to your VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-167">Open a Remote Desktop connection to your VM.</span></span> <span data-ttu-id="c6a3f-168">Select your VM in the portal and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-168">Select your VM in the portal and click **Connect**.</span></span> <span data-ttu-id="c6a3f-169">Download and open the RDP connection file.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-169">Download and open the RDP connection file.</span></span> <span data-ttu-id="c6a3f-170">Enter your credentials to log in to your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-170">Enter your credentials to log in to your VM as follows:</span></span>

    ![Log in to your VM using Remote Desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. <span data-ttu-id="c6a3f-172">Open **Server Manager**, then select **File and Storage Services**.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-172">Open **Server Manager**, then select **File and Storage Services**.</span></span> 

    ![Select File and Storage Services within Server Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. <span data-ttu-id="c6a3f-174">The data disk is automatically detected and attached.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-174">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="c6a3f-175">To see a list of the connected disks, select **Disks**.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-175">To see a list of the connected disks, select **Disks**.</span></span> <span data-ttu-id="c6a3f-176">You can select your data disk to view volume information, including the drive letter.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-176">You can select your data disk to view volume information, including the drive letter.</span></span> <span data-ttu-id="c6a3f-177">The following example shows the data disk attached and using **F:**:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-177">The following example shows the data disk attached and using **F:**:</span></span>

    ![Disk attached and volume information in Server Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="c6a3f-179">Fix issues on original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="c6a3f-179">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="c6a3f-180">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-180">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="c6a3f-181">Once you have addressed the issues, continue with the following steps.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-181">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="c6a3f-182">Unmount and detach original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="c6a3f-182">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="c6a3f-183">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-183">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="c6a3f-184">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-184">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="c6a3f-185">From the RDP session to your VM, open **Server Manager**, then select **File and Storage Services**:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-185">From the RDP session to your VM, open **Server Manager**, then select **File and Storage Services**:</span></span>

    ![Select File and Storage Services in Server Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. <span data-ttu-id="c6a3f-187">Select **Disks** and then select your data disk.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-187">Select **Disks** and then select your data disk.</span></span> <span data-ttu-id="c6a3f-188">Right-click on your data disk and select **Take Offline**:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-188">Right-click on your data disk and select **Take Offline**:</span></span>

    ![Set the data disk as offline in Server Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. <span data-ttu-id="c6a3f-190">Now detach the virtual hard disk from the VM.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-190">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="c6a3f-191">Select your VM in the Azure portal and click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-191">Select your VM in the Azure portal and click **Disks**.</span></span> <span data-ttu-id="c6a3f-192">Select your existing virtual hard disk and then click **Detach**:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-192">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Detach existing virtual hard disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="c6a3f-194">Wait until the VM has successfully detached the data disk before continuing.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-194">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="c6a3f-195">Create VM from original hard disk</span><span class="sxs-lookup"><span data-stu-id="c6a3f-195">Create VM from original hard disk</span></span>
<span data-ttu-id="c6a3f-196">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="c6a3f-196">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="c6a3f-197">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-197">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="c6a3f-198">Click the **Deploy to Azure** button as follows:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-198">Click the **Deploy to Azure** button as follows:</span></span>

![Deploy VM from template from Github](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="c6a3f-200">The template is loaded into the Azure portal for deployment.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-200">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="c6a3f-201">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-201">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="c6a3f-202">To begin the deployment, click **Purchase**:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-202">To begin the deployment, click **Purchase**:</span></span>

![Deploy VM from template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="c6a3f-204">Re-enable boot diagnostics</span><span class="sxs-lookup"><span data-stu-id="c6a3f-204">Re-enable boot diagnostics</span></span>
<span data-ttu-id="c6a3f-205">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-205">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="c6a3f-206">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-206">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="c6a3f-207">Under **Monitoring**, click **Diagnostics settings**.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-207">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="c6a3f-208">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span><span class="sxs-lookup"><span data-stu-id="c6a3f-208">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="c6a3f-209">If you make any changes, click **Save**:</span><span class="sxs-lookup"><span data-stu-id="c6a3f-209">If you make any changes, click **Save**:</span></span>

![Update boot diagnostics settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="c6a3f-211">Next steps</span><span class="sxs-lookup"><span data-stu-id="c6a3f-211">Next steps</span></span>
<span data-ttu-id="c6a3f-212">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6a3f-212">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="c6a3f-213">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6a3f-213">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c6a3f-214">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6a3f-214">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


















