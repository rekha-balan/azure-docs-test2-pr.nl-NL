---
title: Use a Linux troubleshooting VM in the Azure portal | Microsoft Docs
description: Learn how to troubleshoot Linux virtual machine issues by connecting the OS disk to a recovery VM using the Azure portal
services: virtual-machines-linux
documentationCenter: ''
authors: cynthn
manager: jeconnoc
editor: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: cynthn
ms.openlocfilehash: 793e84e64c3a6f9d998d6c2cdfee074b5e359f13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803821"
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="c2d5b-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c2d5b-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="c2d5b-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="c2d5b-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="c2d5b-106">This article details how to use the Azure portal to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-106">This article details how to use the Azure portal to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="c2d5b-107">Recovery process overview</span><span class="sxs-lookup"><span data-stu-id="c2d5b-107">Recovery process overview</span></span>
<span data-ttu-id="c2d5b-108">The troubleshooting process is as follows:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="c2d5b-109">Delete the VM encountering issues, keeping the virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="c2d5b-110">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-110">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="c2d5b-111">Connect to the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="c2d5b-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="c2d5b-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="c2d5b-114">Create a VM using the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-114">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="c2d5b-115">For the VM that uses managed disk, see [Troubleshoot a Managed Disk VM by attaching a new OS disk](#troubleshoot-a-managed-disk-vm-by-attaching-a-new-os-disk).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-115">For the VM that uses managed disk, see [Troubleshoot a Managed Disk VM by attaching a new OS disk](#troubleshoot-a-managed-disk-vm-by-attaching-a-new-os-disk).</span></span>

## <a name="determine-boot-issues"></a><span data-ttu-id="c2d5b-116">Determine boot issues</span><span class="sxs-lookup"><span data-stu-id="c2d5b-116">Determine boot issues</span></span>
<span data-ttu-id="c2d5b-117">Examine the boot diagnostics and VM screenshot to determine why your VM is not able to boot correctly.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-117">Examine the boot diagnostics and VM screenshot to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="c2d5b-118">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-118">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="c2d5b-119">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-119">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="c2d5b-120">Click **Boot diagnostics** to view the console messages streamed from your VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-120">Click **Boot diagnostics** to view the console messages streamed from your VM.</span></span> <span data-ttu-id="c2d5b-121">Review the console logs to see if you can determine why the VM is encountering an issue.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-121">Review the console logs to see if you can determine why the VM is encountering an issue.</span></span> <span data-ttu-id="c2d5b-122">The following example shows a VM stuck in maintenance mode that requires manual interaction:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-122">The following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Viewing VM boot diagnostics console logs](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="c2d5b-124">You can also click **Screenshot** across the top of the boot diagnostics log to download a capture of the VM screenshot.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-124">You can also click **Screenshot** across the top of the boot diagnostics log to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="c2d5b-125">View existing virtual hard disk details</span><span class="sxs-lookup"><span data-stu-id="c2d5b-125">View existing virtual hard disk details</span></span>
<span data-ttu-id="c2d5b-126">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-126">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="c2d5b-127">Select your resource group from the portal, then select your storage account.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-127">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="c2d5b-128">Click **Blobs**, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-128">Click **Blobs**, as in the following example:</span></span>

![Select storage blobs](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="c2d5b-130">Typically you have a container named **vhds** that stores your virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-130">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="c2d5b-131">Select the container to view a list of virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-131">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="c2d5b-132">Note the name of your VHD (the prefix is usually the name of your VM):</span><span class="sxs-lookup"><span data-stu-id="c2d5b-132">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![Identify VHD in storage container](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="c2d5b-134">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-134">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![Copy existing virtual hard disk URL](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="c2d5b-136">Delete existing VM</span><span class="sxs-lookup"><span data-stu-id="c2d5b-136">Delete existing VM</span></span>
<span data-ttu-id="c2d5b-137">Virtual hard disks and VMs are two distinct resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-137">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="c2d5b-138">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-138">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="c2d5b-139">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-139">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="c2d5b-140">Each virtual hard disk has a lease assigned when attached to a VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-140">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="c2d5b-141">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-141">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="c2d5b-142">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-142">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="c2d5b-143">The first step to recover your VM is to delete the VM resource itself.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-143">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="c2d5b-144">Deleting the VM leaves the virtual hard disks in your storage account.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-144">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="c2d5b-145">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-145">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="c2d5b-146">Select your VM in the portal, then click **Delete**:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-146">Select your VM in the portal, then click **Delete**:</span></span>

![VM boot diagnostics screenshot showing boot error](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="c2d5b-148">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-148">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="c2d5b-149">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-149">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="c2d5b-150">Attach existing virtual hard disk to another VM</span><span class="sxs-lookup"><span data-stu-id="c2d5b-150">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="c2d5b-151">For the next few steps, you use another VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-151">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="c2d5b-152">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-152">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="c2d5b-153">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-153">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="c2d5b-154">Choose or create another VM to use for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-154">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="c2d5b-155">Select your resource group from the portal, then select your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-155">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="c2d5b-156">Select **Disks** and then click **Attach existing**:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-156">Select **Disks** and then click **Attach existing**:</span></span>

    ![Attach existing disk in the portal](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="c2d5b-158">To select your existing virtual hard disk, click **VHD File**:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-158">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![Browse for existing VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="c2d5b-160">Select your storage account and container, then click your existing VHD.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-160">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="c2d5b-161">Click the **Select** button to confirm your choice:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-161">Click the **Select** button to confirm your choice:</span></span>

    ![Select your existing VHD](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="c2d5b-163">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-163">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![Confirm attaching existing virtual hard disk](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="c2d5b-165">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-165">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Existing virtual hard disk attached as a data disk](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="c2d5b-167">Mount the attached data disk</span><span class="sxs-lookup"><span data-stu-id="c2d5b-167">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="c2d5b-168">The following examples detail the steps required on an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-168">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="c2d5b-169">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-169">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="c2d5b-170">Refer to the documentation for your specific distro for the appropriate changes in commands.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-170">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="c2d5b-171">SSH to your troubleshooting VM using the appropriate credentials.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-171">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="c2d5b-172">If this disk is the first data disk attached to your troubleshooting VM, it is likely connected to `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-172">If this disk is the first data disk attached to your troubleshooting VM, it is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="c2d5b-173">Use `dmseg` to list attached disks:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-173">Use `dmseg` to list attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="c2d5b-174">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-174">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="c2d5b-175">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-175">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="c2d5b-176">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-176">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="c2d5b-177">Create a directory to mount your existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-177">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="c2d5b-178">The following example creates a directory named `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-178">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="c2d5b-179">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-179">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="c2d5b-180">The following example mounts the first primary partition at `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-180">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="c2d5b-181">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-181">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="c2d5b-182">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-182">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="c2d5b-183">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-183">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="c2d5b-184">Fix issues on original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="c2d5b-184">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="c2d5b-185">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-185">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="c2d5b-186">Once you have addressed the issues, continue with the following steps.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-186">Once you have addressed the issues, continue with the following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="c2d5b-187">Unmount and detach original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="c2d5b-187">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="c2d5b-188">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-188">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="c2d5b-189">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-189">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="c2d5b-190">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-190">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="c2d5b-191">Change out of the parent directory for your mount point first:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-191">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="c2d5b-192">Now unmount the existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-192">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="c2d5b-193">The following example unmounts the device at `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-193">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="c2d5b-194">Now detach the virtual hard disk from the VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-194">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="c2d5b-195">Select your VM in the portal and click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-195">Select your VM in the portal and click **Disks**.</span></span> <span data-ttu-id="c2d5b-196">Select your existing virtual hard disk and then click **Detach**:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-196">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Detach existing virtual hard disk](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="c2d5b-198">Wait until the VM has successfully detached the data disk before continuing.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-198">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="c2d5b-199">Create VM from original hard disk</span><span class="sxs-lookup"><span data-stu-id="c2d5b-199">Create VM from original hard disk</span></span>
<span data-ttu-id="c2d5b-200">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-200">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="c2d5b-201">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-201">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="c2d5b-202">Click the **Deploy to Azure** button as follows:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-202">Click the **Deploy to Azure** button as follows:</span></span>

![Deploy VM from template from GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="c2d5b-204">The template is loaded into the Azure portal for deployment.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-204">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="c2d5b-205">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-205">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="c2d5b-206">To begin the deployment, click **Purchase**:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-206">To begin the deployment, click **Purchase**:</span></span>

![Deploy VM from template](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="c2d5b-208">Re-enable boot diagnostics</span><span class="sxs-lookup"><span data-stu-id="c2d5b-208">Re-enable boot diagnostics</span></span>
<span data-ttu-id="c2d5b-209">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-209">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="c2d5b-210">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-210">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="c2d5b-211">Under **Monitoring**, click **Diagnostics settings**.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-211">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="c2d5b-212">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-212">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="c2d5b-213">If you make any changes, click **Save**:</span><span class="sxs-lookup"><span data-stu-id="c2d5b-213">If you make any changes, click **Save**:</span></span>

![Update boot diagnostics settings](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="troubleshoot-a-managed-disk-vm-by-attaching-a-new-os-disk"></a><span data-ttu-id="c2d5b-215">Troubleshoot a Managed Disk VM by attaching a new OS disk</span><span class="sxs-lookup"><span data-stu-id="c2d5b-215">Troubleshoot a Managed Disk VM by attaching a new OS disk</span></span>
1. <span data-ttu-id="c2d5b-216">Stop the effected Managed Disk Windows VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-216">Stop the effected Managed Disk Windows VM.</span></span>
2. <span data-ttu-id="c2d5b-217">[Create a managed disk snapshot](../windows/snapshot-copy-managed-disk.md) of the OS Disk of the Managed Disk VM.</span><span class="sxs-lookup"><span data-stu-id="c2d5b-217">[Create a managed disk snapshot](../windows/snapshot-copy-managed-disk.md) of the OS Disk of the Managed Disk VM.</span></span>
3. <span data-ttu-id="c2d5b-218">[Create a managed disk from the snapshot](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-218">[Create a managed disk from the snapshot](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md).</span></span>
4. <span data-ttu-id="c2d5b-219">[Attach the managed disk as a data disk of the VM](../windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-219">[Attach the managed disk as a data disk of the VM](../windows/attach-disk-ps.md).</span></span>
5. <span data-ttu-id="c2d5b-220">[Change the data disk from step 4 to OS disk](../windows/os-disk-swap.md).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-220">[Change the data disk from step 4 to OS disk](../windows/os-disk-swap.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2d5b-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2d5b-221">Next steps</span></span>
<span data-ttu-id="c2d5b-222">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-222">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c2d5b-223">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-223">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c2d5b-224">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2d5b-224">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
