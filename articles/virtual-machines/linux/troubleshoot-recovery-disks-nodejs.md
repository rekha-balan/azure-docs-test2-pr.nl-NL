---
title: Use a Linux troubleshooting VM with the Azure CLI 1.0 | Microsoft Docs
description: Learn how to troubleshoot Linux VM issues by connecting the OS disk to a recovery VM using the Azure CLI 1.0
services: virtual-machines-linux
documentationCenter: ''
authors: iainfoulds
manager: timlt
editor: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 42f8cbc48f679a465d4c90688ab15c80eef3e2e6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553024"
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-cli-10"></a><span data-ttu-id="e212b-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e212b-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="e212b-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span><span class="sxs-lookup"><span data-stu-id="e212b-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="e212b-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span><span class="sxs-lookup"><span data-stu-id="e212b-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="e212b-106">This article details how to use the Azure CLI 1.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-106">This article details how to use the Azure CLI 1.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e212b-107">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="e212b-107">CLI versions to complete the task</span></span>
<span data-ttu-id="e212b-108">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="e212b-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="e212b-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="e212b-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e212b-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="e212b-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="e212b-111">Recovery process overview</span><span class="sxs-lookup"><span data-stu-id="e212b-111">Recovery process overview</span></span>
<span data-ttu-id="e212b-112">The troubleshooting process is as follows:</span><span class="sxs-lookup"><span data-stu-id="e212b-112">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="e212b-113">Delete the VM encountering issues, keeping the virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="e212b-113">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="e212b-114">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="e212b-114">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="e212b-115">Connect to the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-115">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="e212b-116">Edit files or run any tools to fix issues on the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="e212b-116">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="e212b-117">Unmount and detach the virtual hard disk from the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-117">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="e212b-118">Create a VM using the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="e212b-118">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="e212b-119">Make sure that you have [the latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="e212b-119">Make sure that you have [the latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e212b-120">In the following examples, replace parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="e212b-120">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="e212b-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e212b-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="e212b-122">Determine boot issues</span><span class="sxs-lookup"><span data-stu-id="e212b-122">Determine boot issues</span></span>
<span data-ttu-id="e212b-123">Examine the serial output to determine why your VM is not able to boot correctly.</span><span class="sxs-lookup"><span data-stu-id="e212b-123">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="e212b-124">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span><span class="sxs-lookup"><span data-stu-id="e212b-124">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="e212b-125">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e212b-125">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e212b-126">Review the serial output to determine why the VM is failing to boot.</span><span class="sxs-lookup"><span data-stu-id="e212b-126">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="e212b-127">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-127">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="e212b-128">View existing virtual hard disk details</span><span class="sxs-lookup"><span data-stu-id="e212b-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="e212b-129">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span><span class="sxs-lookup"><span data-stu-id="e212b-129">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="e212b-130">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e212b-130">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e212b-131">Look for `Vhd URI` in the output from the preceding command.</span><span class="sxs-lookup"><span data-stu-id="e212b-131">Look for `Vhd URI` in the output from the preceding command.</span></span> <span data-ttu-id="e212b-132">The following truncated example output shows the `Vhd URI` on the last line:</span><span class="sxs-lookup"><span data-stu-id="e212b-132">The following truncated example output shows the `Vhd URI` on the last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myVM"
+ Looking up the NIC "myNic"
+ Looking up the public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="e212b-133">Delete existing VM</span><span class="sxs-lookup"><span data-stu-id="e212b-133">Delete existing VM</span></span>
<span data-ttu-id="e212b-134">Virtual hard disks and VMs are two distinct resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="e212b-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="e212b-135">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span><span class="sxs-lookup"><span data-stu-id="e212b-135">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="e212b-136">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span><span class="sxs-lookup"><span data-stu-id="e212b-136">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="e212b-137">Each virtual hard disk has a lease assigned when attached to a VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-137">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="e212b-138">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span><span class="sxs-lookup"><span data-stu-id="e212b-138">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="e212b-139">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span><span class="sxs-lookup"><span data-stu-id="e212b-139">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="e212b-140">The first step to recover your VM is to delete the VM resource itself.</span><span class="sxs-lookup"><span data-stu-id="e212b-140">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="e212b-141">Deleting the VM leaves the virtual hard disks in your storage account.</span><span class="sxs-lookup"><span data-stu-id="e212b-141">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="e212b-142">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span><span class="sxs-lookup"><span data-stu-id="e212b-142">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="e212b-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e212b-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="e212b-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="e212b-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="e212b-146">Attach existing virtual hard disk to another VM</span><span class="sxs-lookup"><span data-stu-id="e212b-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="e212b-147">For the next few steps, you use another VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="e212b-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="e212b-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span><span class="sxs-lookup"><span data-stu-id="e212b-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="e212b-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span><span class="sxs-lookup"><span data-stu-id="e212b-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="e212b-150">Choose or create another VM to use for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="e212b-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="e212b-151">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `azure vm show` command.</span><span class="sxs-lookup"><span data-stu-id="e212b-151">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `azure vm show` command.</span></span> <span data-ttu-id="e212b-152">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e212b-152">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="e212b-153">Mount the attached data disk</span><span class="sxs-lookup"><span data-stu-id="e212b-153">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="e212b-154">The following examples detail the steps required on an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-154">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="e212b-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span><span class="sxs-lookup"><span data-stu-id="e212b-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="e212b-156">Refer to the documentation for your specific distro for the appropriate changes in commands.</span><span class="sxs-lookup"><span data-stu-id="e212b-156">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="e212b-157">SSH to your troubleshooting VM using the appropriate credentials.</span><span class="sxs-lookup"><span data-stu-id="e212b-157">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="e212b-158">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="e212b-158">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="e212b-159">Use `dmseg` to view attached disks:</span><span class="sxs-lookup"><span data-stu-id="e212b-159">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="e212b-160">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="e212b-160">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="e212b-161">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="e212b-161">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="e212b-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span><span class="sxs-lookup"><span data-stu-id="e212b-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="e212b-163">Create a directory to mount your existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="e212b-163">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="e212b-164">The following example creates a directory named `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="e212b-164">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="e212b-165">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span><span class="sxs-lookup"><span data-stu-id="e212b-165">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="e212b-166">The following example mounts the first primary partition at `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e212b-166">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="e212b-167">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="e212b-167">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="e212b-168">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span><span class="sxs-lookup"><span data-stu-id="e212b-168">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="e212b-169">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span><span class="sxs-lookup"><span data-stu-id="e212b-169">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="e212b-170">Fix issues on original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="e212b-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="e212b-171">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span><span class="sxs-lookup"><span data-stu-id="e212b-171">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="e212b-172">Once you have addressed the issues, continue with the following steps.</span><span class="sxs-lookup"><span data-stu-id="e212b-172">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="e212b-173">Unmount and detach original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="e212b-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="e212b-174">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-174">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="e212b-175">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span><span class="sxs-lookup"><span data-stu-id="e212b-175">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="e212b-176">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="e212b-176">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="e212b-177">Change out of the parent directory for your mount point first:</span><span class="sxs-lookup"><span data-stu-id="e212b-177">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="e212b-178">Now unmount the existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="e212b-178">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="e212b-179">The following example unmounts the device at `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e212b-179">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="e212b-180">Now detach the virtual hard disk from the VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-180">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="e212b-181">Exit the SSH session to your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-181">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="e212b-182">In the Azure CLI, first list the attached data disks to your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-182">In the Azure CLI, first list the attached data disks to your troubleshooting VM.</span></span> <span data-ttu-id="e212b-183">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e212b-183">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="e212b-184">Note the `Lun` value for your existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="e212b-184">Note the `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="e212b-185">The following example command output shows the existing virtual disk attached at LUN 0:</span><span class="sxs-lookup"><span data-stu-id="e212b-185">The following example command output shows the existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up the VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="e212b-186">Detach the data disk from your VM using the applicable `Lun` value:</span><span class="sxs-lookup"><span data-stu-id="e212b-186">Detach the data disk from your VM using the applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="e212b-187">Create VM from original hard disk</span><span class="sxs-lookup"><span data-stu-id="e212b-187">Create VM from original hard disk</span></span>
<span data-ttu-id="e212b-188">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="e212b-188">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="e212b-189">The actual JSON template is at the following link:</span><span class="sxs-lookup"><span data-stu-id="e212b-189">The actual JSON template is at the following link:</span></span>

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

<span data-ttu-id="e212b-190">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span><span class="sxs-lookup"><span data-stu-id="e212b-190">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="e212b-191">The following example deploys the template to the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e212b-191">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="e212b-192">Answer the prompts for the template such as VM name (`myDeployedVM` the following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="e212b-192">Answer the prompts for the template such as VM name (`myDeployedVM` the following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="e212b-193">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="e212b-193">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span> <span data-ttu-id="e212b-194">An example of the command output and prompts is as follows:</span><span class="sxs-lookup"><span data-stu-id="e212b-194">An example of the command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment to complete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="e212b-195">Re-enable boot diagnostics</span><span class="sxs-lookup"><span data-stu-id="e212b-195">Re-enable boot diagnostics</span></span>

<span data-ttu-id="e212b-196">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span><span class="sxs-lookup"><span data-stu-id="e212b-196">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="e212b-197">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e212b-197">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="e212b-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="e212b-198">Next steps</span></span>
<span data-ttu-id="e212b-199">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e212b-199">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e212b-200">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e212b-200">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>