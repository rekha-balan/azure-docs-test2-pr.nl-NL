---
title: Use a Windows troubleshooting VM in the Azure portal | Microsoft Docs
description: Learn how to troubleshoot Windows virtual machine issues in Azure by connecting the OS disk to a recovery VM using the Azure portal
services: virtual-machines-windows
documentationCenter: ''
authors: genlin
manager: jeconnoc
editor: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/013/2018
ms.author: genli
ms.openlocfilehash: 96bb554bbd25e14732d85da6d68bd6a6b983b70e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819070"
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="85d7e-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="85d7e-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="85d7e-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span><span class="sxs-lookup"><span data-stu-id="85d7e-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="85d7e-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span><span class="sxs-lookup"><span data-stu-id="85d7e-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="85d7e-106">This article details how to use the Azure portal to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-106">This article details how to use the Azure portal to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="85d7e-107">Recovery process overview</span><span class="sxs-lookup"><span data-stu-id="85d7e-107">Recovery process overview</span></span>
<span data-ttu-id="85d7e-108">The troubleshooting process is as follows:</span><span class="sxs-lookup"><span data-stu-id="85d7e-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="85d7e-109">Delete the VM encountering issues, keeping the virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="85d7e-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="85d7e-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="85d7e-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="85d7e-111">Connect to the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="85d7e-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="85d7e-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="85d7e-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="85d7e-114">Create a VM using the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="85d7e-114">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="85d7e-115">For the VM that uses managed disk, we can now use Azure PowerShell to change the OS disk for a VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-115">For the VM that uses managed disk, we can now use Azure PowerShell to change the OS disk for a VM.</span></span> <span data-ttu-id="85d7e-116">We no longer need to delete and recreate the VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-116">We no longer need to delete and recreate the VM.</span></span> <span data-ttu-id="85d7e-117">For more information, see [Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell](troubleshoot-recovery-disks.md).</span><span class="sxs-lookup"><span data-stu-id="85d7e-117">For more information, see [Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell](troubleshoot-recovery-disks.md).</span></span>

## <a name="determine-boot-issues"></a><span data-ttu-id="85d7e-118">Determine boot issues</span><span class="sxs-lookup"><span data-stu-id="85d7e-118">Determine boot issues</span></span>
<span data-ttu-id="85d7e-119">To determine why your VM is not able to boot correctly, examine the boot diagnostics VM screenshot.</span><span class="sxs-lookup"><span data-stu-id="85d7e-119">To determine why your VM is not able to boot correctly, examine the boot diagnostics VM screenshot.</span></span> <span data-ttu-id="85d7e-120">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span><span class="sxs-lookup"><span data-stu-id="85d7e-120">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="85d7e-121">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span><span class="sxs-lookup"><span data-stu-id="85d7e-121">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="85d7e-122">Click **Boot diagnostics** to view the screenshot.</span><span class="sxs-lookup"><span data-stu-id="85d7e-122">Click **Boot diagnostics** to view the screenshot.</span></span> <span data-ttu-id="85d7e-123">Note any specific error messages or error codes to help determine why the VM is encountering an issue.</span><span class="sxs-lookup"><span data-stu-id="85d7e-123">Note any specific error messages or error codes to help determine why the VM is encountering an issue.</span></span> <span data-ttu-id="85d7e-124">The following example shows a VM waiting on stopping services:</span><span class="sxs-lookup"><span data-stu-id="85d7e-124">The following example shows a VM waiting on stopping services:</span></span>

![Viewing VM boot diagnostics console logs](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

<span data-ttu-id="85d7e-126">You can also click **Screenshot** to download a capture of the VM screenshot.</span><span class="sxs-lookup"><span data-stu-id="85d7e-126">You can also click **Screenshot** to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="85d7e-127">View existing virtual hard disk details</span><span class="sxs-lookup"><span data-stu-id="85d7e-127">View existing virtual hard disk details</span></span>
<span data-ttu-id="85d7e-128">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span><span class="sxs-lookup"><span data-stu-id="85d7e-128">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="85d7e-129">Select your resource group from the portal, then select your storage account.</span><span class="sxs-lookup"><span data-stu-id="85d7e-129">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="85d7e-130">Click **Blobs**, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="85d7e-130">Click **Blobs**, as in the following example:</span></span>

![Select storage blobs](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="85d7e-132">Typically you have a container named **vhds** that stores your virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="85d7e-132">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="85d7e-133">Select the container to view a list of virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="85d7e-133">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="85d7e-134">Note the name of your VHD (the prefix is usually the name of your VM):</span><span class="sxs-lookup"><span data-stu-id="85d7e-134">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![Identify VHD in storage container](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="85d7e-136">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span><span class="sxs-lookup"><span data-stu-id="85d7e-136">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![Copy existing virtual hard disk URL](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="85d7e-138">Delete existing VM</span><span class="sxs-lookup"><span data-stu-id="85d7e-138">Delete existing VM</span></span>
<span data-ttu-id="85d7e-139">Virtual hard disks and VMs are two distinct resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="85d7e-139">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="85d7e-140">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span><span class="sxs-lookup"><span data-stu-id="85d7e-140">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="85d7e-141">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span><span class="sxs-lookup"><span data-stu-id="85d7e-141">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="85d7e-142">Each virtual hard disk has a lease assigned when attached to a VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-142">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="85d7e-143">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span><span class="sxs-lookup"><span data-stu-id="85d7e-143">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="85d7e-144">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span><span class="sxs-lookup"><span data-stu-id="85d7e-144">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="85d7e-145">The first step to recover your VM is to delete the VM resource itself.</span><span class="sxs-lookup"><span data-stu-id="85d7e-145">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="85d7e-146">Deleting the VM leaves the virtual hard disks in your storage account.</span><span class="sxs-lookup"><span data-stu-id="85d7e-146">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="85d7e-147">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span><span class="sxs-lookup"><span data-stu-id="85d7e-147">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="85d7e-148">Select your VM in the portal, then click **Delete**:</span><span class="sxs-lookup"><span data-stu-id="85d7e-148">Select your VM in the portal, then click **Delete**:</span></span>

![VM boot diagnostics screenshot showing boot error](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="85d7e-150">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-150">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="85d7e-151">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-151">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="85d7e-152">Attach existing virtual hard disk to another VM</span><span class="sxs-lookup"><span data-stu-id="85d7e-152">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="85d7e-153">For the next few steps, you use another VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="85d7e-153">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="85d7e-154">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span><span class="sxs-lookup"><span data-stu-id="85d7e-154">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="85d7e-155">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span><span class="sxs-lookup"><span data-stu-id="85d7e-155">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="85d7e-156">Choose or create another VM to use for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="85d7e-156">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="85d7e-157">Select your resource group from the portal, then select your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-157">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="85d7e-158">Select **Disks** and then click **Attach existing**:</span><span class="sxs-lookup"><span data-stu-id="85d7e-158">Select **Disks** and then click **Attach existing**:</span></span>

    ![Attach existing disk in the portal](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="85d7e-160">To select your existing virtual hard disk, click **VHD File**:</span><span class="sxs-lookup"><span data-stu-id="85d7e-160">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![Browse for existing VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="85d7e-162">Select your storage account and container, then click your existing VHD.</span><span class="sxs-lookup"><span data-stu-id="85d7e-162">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="85d7e-163">Click the **Select** button to confirm your choice:</span><span class="sxs-lookup"><span data-stu-id="85d7e-163">Click the **Select** button to confirm your choice:</span></span>

    ![Select your existing VHD](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="85d7e-165">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span><span class="sxs-lookup"><span data-stu-id="85d7e-165">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![Confirm attaching existing virtual hard disk](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="85d7e-167">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span><span class="sxs-lookup"><span data-stu-id="85d7e-167">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Existing virtual hard disk attached as a data disk](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="85d7e-169">Mount the attached data disk</span><span class="sxs-lookup"><span data-stu-id="85d7e-169">Mount the attached data disk</span></span>

1. <span data-ttu-id="85d7e-170">Open a Remote Desktop connection to your VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-170">Open a Remote Desktop connection to your VM.</span></span> <span data-ttu-id="85d7e-171">Select your VM in the portal and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="85d7e-171">Select your VM in the portal and click **Connect**.</span></span> <span data-ttu-id="85d7e-172">Download and open the RDP connection file.</span><span class="sxs-lookup"><span data-stu-id="85d7e-172">Download and open the RDP connection file.</span></span> <span data-ttu-id="85d7e-173">Enter your credentials to sign in to your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="85d7e-173">Enter your credentials to sign in to your VM as follows:</span></span>

    ![Sign in to your VM using Remote Desktop](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. <span data-ttu-id="85d7e-175">Open **Server Manager**, then select **File and Storage Services**.</span><span class="sxs-lookup"><span data-stu-id="85d7e-175">Open **Server Manager**, then select **File and Storage Services**.</span></span> 

    ![Select File and Storage Services within Server Manager](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. <span data-ttu-id="85d7e-177">The data disk is automatically detected and attached.</span><span class="sxs-lookup"><span data-stu-id="85d7e-177">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="85d7e-178">To see a list of the connected disks, select **Disks**.</span><span class="sxs-lookup"><span data-stu-id="85d7e-178">To see a list of the connected disks, select **Disks**.</span></span> <span data-ttu-id="85d7e-179">You can select your data disk to view volume information, including the drive letter.</span><span class="sxs-lookup"><span data-stu-id="85d7e-179">You can select your data disk to view volume information, including the drive letter.</span></span> <span data-ttu-id="85d7e-180">The following example shows the data disk attached and using **F:**:</span><span class="sxs-lookup"><span data-stu-id="85d7e-180">The following example shows the data disk attached and using **F:**:</span></span>

    ![Disk attached and volume information in Server Manager](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="85d7e-182">Fix issues on original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="85d7e-182">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="85d7e-183">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span><span class="sxs-lookup"><span data-stu-id="85d7e-183">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="85d7e-184">Once you have addressed the issues, continue with the following steps.</span><span class="sxs-lookup"><span data-stu-id="85d7e-184">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="85d7e-185">Unmount and detach original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="85d7e-185">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="85d7e-186">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-186">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="85d7e-187">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span><span class="sxs-lookup"><span data-stu-id="85d7e-187">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="85d7e-188">From the RDP session to your VM, open **Server Manager**, then select **File and Storage Services**:</span><span class="sxs-lookup"><span data-stu-id="85d7e-188">From the RDP session to your VM, open **Server Manager**, then select **File and Storage Services**:</span></span>

    ![Select File and Storage Services in Server Manager](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. <span data-ttu-id="85d7e-190">Select **Disks** and then select your data disk.</span><span class="sxs-lookup"><span data-stu-id="85d7e-190">Select **Disks** and then select your data disk.</span></span> <span data-ttu-id="85d7e-191">Right-click on your data disk and select **Take Offline**:</span><span class="sxs-lookup"><span data-stu-id="85d7e-191">Right-click on your data disk and select **Take Offline**:</span></span>

    ![Set the data disk as offline in Server Manager](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. <span data-ttu-id="85d7e-193">Now detach the virtual hard disk from the VM.</span><span class="sxs-lookup"><span data-stu-id="85d7e-193">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="85d7e-194">Select your VM in the Azure portal and click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="85d7e-194">Select your VM in the Azure portal and click **Disks**.</span></span> <span data-ttu-id="85d7e-195">Select your existing virtual hard disk and then click **Detach**:</span><span class="sxs-lookup"><span data-stu-id="85d7e-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Detach existing virtual hard disk](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="85d7e-197">Wait until the VM has successfully detached the data disk before continuing.</span><span class="sxs-lookup"><span data-stu-id="85d7e-197">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="85d7e-198">Create VM from original hard disk</span><span class="sxs-lookup"><span data-stu-id="85d7e-198">Create VM from original hard disk</span></span>
<span data-ttu-id="85d7e-199">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="85d7e-199">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="85d7e-200">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span><span class="sxs-lookup"><span data-stu-id="85d7e-200">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="85d7e-201">Click the **Deploy to Azure** button as follows:</span><span class="sxs-lookup"><span data-stu-id="85d7e-201">Click the **Deploy to Azure** button as follows:</span></span>

![Deploy VM from template from Github](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="85d7e-203">The template is loaded into the Azure portal for deployment.</span><span class="sxs-lookup"><span data-stu-id="85d7e-203">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="85d7e-204">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="85d7e-204">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="85d7e-205">To begin the deployment, click **Purchase**:</span><span class="sxs-lookup"><span data-stu-id="85d7e-205">To begin the deployment, click **Purchase**:</span></span>

![Deploy VM from template](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="85d7e-207">Re-enable boot diagnostics</span><span class="sxs-lookup"><span data-stu-id="85d7e-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="85d7e-208">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span><span class="sxs-lookup"><span data-stu-id="85d7e-208">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="85d7e-209">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span><span class="sxs-lookup"><span data-stu-id="85d7e-209">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="85d7e-210">Under **Monitoring**, click **Diagnostics settings**.</span><span class="sxs-lookup"><span data-stu-id="85d7e-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="85d7e-211">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span><span class="sxs-lookup"><span data-stu-id="85d7e-211">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="85d7e-212">If you make any changes, click **Save**:</span><span class="sxs-lookup"><span data-stu-id="85d7e-212">If you make any changes, click **Save**:</span></span>

![Update boot diagnostics settings](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="85d7e-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="85d7e-214">Next steps</span></span>
<span data-ttu-id="85d7e-215">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="85d7e-215">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="85d7e-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="85d7e-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="85d7e-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="85d7e-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
