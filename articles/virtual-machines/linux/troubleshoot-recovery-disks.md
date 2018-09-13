---
title: Use a Linux troubleshooting VM with the Azure CLI 2.0 | Microsoft Docs
description: Learn how to troubleshoot Linux VM issues by connecting the OS disk to a recovery VM using the Azure CLI 2.0
services: virtual-machines-linux
documentationCenter: ''
authors: iainfoulds
manager: timlt
editor: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 1e22eee296cc93e60c63715f26c585d4c1cefad9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564405"
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-with-the-azure-cli-20"></a><span data-ttu-id="2f042-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2f042-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM with the Azure CLI 2.0</span></span>
<span data-ttu-id="2f042-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span><span class="sxs-lookup"><span data-stu-id="2f042-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="2f042-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span><span class="sxs-lookup"><span data-stu-id="2f042-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="2f042-106">This article details how to use the Azure CLI 2.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-106">This article details how to use the Azure CLI 2.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span> <span data-ttu-id="2f042-107">You can also perform these steps with the [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f042-107">You can also perform these steps with the [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="2f042-108">Recovery process overview</span><span class="sxs-lookup"><span data-stu-id="2f042-108">Recovery process overview</span></span>
<span data-ttu-id="2f042-109">The troubleshooting process is as follows:</span><span class="sxs-lookup"><span data-stu-id="2f042-109">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="2f042-110">Delete the VM encountering issues, keeping the virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="2f042-110">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="2f042-111">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="2f042-111">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="2f042-112">Connect to the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-112">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="2f042-113">Edit files or run any tools to fix issues on the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="2f042-113">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="2f042-114">Unmount and detach the virtual hard disk from the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-114">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="2f042-115">Create a VM using the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="2f042-115">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="2f042-116">To perform these troubleshooting steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2f042-116">To perform these troubleshooting steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="2f042-117">In the following examples, replace parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="2f042-117">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="2f042-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="2f042-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="2f042-119">Determine boot issues</span><span class="sxs-lookup"><span data-stu-id="2f042-119">Determine boot issues</span></span>
<span data-ttu-id="2f042-120">Examine the serial output to determine why your VM is not able to boot correctly.</span><span class="sxs-lookup"><span data-stu-id="2f042-120">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="2f042-121">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span><span class="sxs-lookup"><span data-stu-id="2f042-121">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="2f042-122">Get the boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="2f042-122">Get the boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="2f042-123">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f042-123">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="2f042-124">Review the serial output to determine why the VM is failing to boot.</span><span class="sxs-lookup"><span data-stu-id="2f042-124">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="2f042-125">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-125">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="2f042-126">View existing virtual hard disk details</span><span class="sxs-lookup"><span data-stu-id="2f042-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="2f042-127">Before you can attach your virtual hard disk (VHD) to another VM, you need to identify the URI of the OS disk.</span><span class="sxs-lookup"><span data-stu-id="2f042-127">Before you can attach your virtual hard disk (VHD) to another VM, you need to identify the URI of the OS disk.</span></span> 

<span data-ttu-id="2f042-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="2f042-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="2f042-129">Use the `--query` flag to extract the URI to the OS disk.</span><span class="sxs-lookup"><span data-stu-id="2f042-129">Use the `--query` flag to extract the URI to the OS disk.</span></span> <span data-ttu-id="2f042-130">The following example gets disk information for the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f042-130">The following example gets disk information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="2f042-131">The URI is similar to **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="2f042-131">The URI is similar to **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="2f042-132">Delete existing VM</span><span class="sxs-lookup"><span data-stu-id="2f042-132">Delete existing VM</span></span>
<span data-ttu-id="2f042-133">Virtual hard disks and VMs are two distinct resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f042-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="2f042-134">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span><span class="sxs-lookup"><span data-stu-id="2f042-134">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="2f042-135">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span><span class="sxs-lookup"><span data-stu-id="2f042-135">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="2f042-136">Each virtual hard disk has a lease assigned when attached to a VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-136">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="2f042-137">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span><span class="sxs-lookup"><span data-stu-id="2f042-137">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="2f042-138">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span><span class="sxs-lookup"><span data-stu-id="2f042-138">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="2f042-139">The first step to recover your VM is to delete the VM resource itself.</span><span class="sxs-lookup"><span data-stu-id="2f042-139">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="2f042-140">Deleting the VM leaves the virtual hard disks in your storage account.</span><span class="sxs-lookup"><span data-stu-id="2f042-140">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="2f042-141">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span><span class="sxs-lookup"><span data-stu-id="2f042-141">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="2f042-142">Delete the VM with [az vm delete](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="2f042-142">Delete the VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="2f042-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f042-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="2f042-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="2f042-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="2f042-146">Attach existing virtual hard disk to another VM</span><span class="sxs-lookup"><span data-stu-id="2f042-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="2f042-147">For the next few steps, you use another VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="2f042-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="2f042-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span><span class="sxs-lookup"><span data-stu-id="2f042-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="2f042-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span><span class="sxs-lookup"><span data-stu-id="2f042-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="2f042-150">Choose or create another VM to use for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="2f042-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="2f042-151">Attach the existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="2f042-151">Attach the existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="2f042-152">When you attach the existing virtual hard disk, specify the URI to the disk obtained in the preceding `az vm show` command.</span><span class="sxs-lookup"><span data-stu-id="2f042-152">When you attach the existing virtual hard disk, specify the URI to the disk obtained in the preceding `az vm show` command.</span></span> <span data-ttu-id="2f042-153">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f042-153">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="2f042-154">Mount the attached data disk</span><span class="sxs-lookup"><span data-stu-id="2f042-154">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="2f042-155">The following examples detail the steps required on an Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-155">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="2f042-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span><span class="sxs-lookup"><span data-stu-id="2f042-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="2f042-157">Refer to the documentation for your specific distro for the appropriate changes in commands.</span><span class="sxs-lookup"><span data-stu-id="2f042-157">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="2f042-158">SSH to your troubleshooting VM using the appropriate credentials.</span><span class="sxs-lookup"><span data-stu-id="2f042-158">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="2f042-159">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="2f042-159">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="2f042-160">Use `dmseg` to view attached disks:</span><span class="sxs-lookup"><span data-stu-id="2f042-160">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="2f042-161">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="2f042-161">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="2f042-162">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="2f042-162">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="2f042-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span><span class="sxs-lookup"><span data-stu-id="2f042-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="2f042-164">Create a directory to mount your existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="2f042-164">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="2f042-165">The following example creates a directory named `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="2f042-165">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="2f042-166">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span><span class="sxs-lookup"><span data-stu-id="2f042-166">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="2f042-167">The following example mounts the first primary partition at `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="2f042-167">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="2f042-168">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="2f042-168">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="2f042-169">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span><span class="sxs-lookup"><span data-stu-id="2f042-169">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="2f042-170">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span><span class="sxs-lookup"><span data-stu-id="2f042-170">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="2f042-171">Fix issues on original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="2f042-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="2f042-172">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span><span class="sxs-lookup"><span data-stu-id="2f042-172">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="2f042-173">Once you have addressed the issues, continue with the following steps.</span><span class="sxs-lookup"><span data-stu-id="2f042-173">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="2f042-174">Unmount and detach original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="2f042-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="2f042-175">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-175">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="2f042-176">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span><span class="sxs-lookup"><span data-stu-id="2f042-176">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="2f042-177">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="2f042-177">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="2f042-178">Change out of the parent directory for your mount point first:</span><span class="sxs-lookup"><span data-stu-id="2f042-178">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="2f042-179">Now unmount the existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="2f042-179">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="2f042-180">The following example unmounts the device at `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="2f042-180">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="2f042-181">Now detach the virtual hard disk from the VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-181">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="2f042-182">Exit the SSH session to your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="2f042-182">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="2f042-183">List the attached data disks to your troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="2f042-183">List the attached data disks to your troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="2f042-184">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f042-184">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="2f042-185">Note the name for your existing virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="2f042-185">Note the name for your existing virtual hard disk.</span></span> <span data-ttu-id="2f042-186">For example, the name of a disk with the URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="2f042-186">For example, the name of a disk with the URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="2f042-187">Detach the data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="2f042-187">Detach the data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="2f042-188">The following example detaches the disk named `myVHD` from the VM named `myVMRecovery` in the `myResourceGroup` resource group:</span><span class="sxs-lookup"><span data-stu-id="2f042-188">The following example detaches the disk named `myVHD` from the VM named `myVMRecovery` in the `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="2f042-189">Create VM from original hard disk</span><span class="sxs-lookup"><span data-stu-id="2f042-189">Create VM from original hard disk</span></span>
<span data-ttu-id="2f042-190">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="2f042-190">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="2f042-191">The actual JSON template is at the following link:</span><span class="sxs-lookup"><span data-stu-id="2f042-191">The actual JSON template is at the following link:</span></span>

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

<span data-ttu-id="2f042-192">The template deploys a VM using the VHD URI from the earlier command.</span><span class="sxs-lookup"><span data-stu-id="2f042-192">The template deploys a VM using the VHD URI from the earlier command.</span></span> <span data-ttu-id="2f042-193">Deploy the template with [az group deployment create](/cli/azure/vm/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="2f042-193">Deploy the template with [az group deployment create](/cli/azure/vm/deployment#create).</span></span> <span data-ttu-id="2f042-194">Provide the URI to your original VHD and then specify the OS type, VM size, and VM name as follows:</span><span class="sxs-lookup"><span data-stu-id="2f042-194">Provide the URI to your original VHD and then specify the OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="2f042-195">Re-enable boot diagnostics</span><span class="sxs-lookup"><span data-stu-id="2f042-195">Re-enable boot diagnostics</span></span>
<span data-ttu-id="2f042-196">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span><span class="sxs-lookup"><span data-stu-id="2f042-196">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="2f042-197">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="2f042-197">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="2f042-198">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f042-198">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="2f042-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f042-199">Next steps</span></span>
<span data-ttu-id="2f042-200">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f042-200">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2f042-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f042-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>