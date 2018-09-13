---
title: Attach a disk to a Linux VM in Azure | Microsoft Docs
description: Learn how to attach a data disk to a Linux VM using the Classic deployment model and initialize the disk so it's ready for use
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 0366d11aff8c86510f0f184fdcba9375581ffdaf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549300"
---
# <a name="how-to-attach-a-data-disk-to-a-linux-virtual-machine"></a><span data-ttu-id="da84c-103">How to Attach a Data Disk to a Linux Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="da84c-103">How to Attach a Data Disk to a Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="da84c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="da84c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="da84c-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="da84c-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="da84c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="da84c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="da84c-107">See how to [attach a data disk using the Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da84c-107">See how to [attach a data disk using the Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="da84c-108">You can attach both empty disks and disks that contain data to your Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="da84c-108">You can attach both empty disks and disks that contain data to your Azure VMs.</span></span> <span data-ttu-id="da84c-109">Both types of disks are .vhd files that reside in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="da84c-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="da84c-110">As with adding any disk to a Linux machine, after you attach the disk you need to initialize and format it so it's ready for use.</span><span class="sxs-lookup"><span data-stu-id="da84c-110">As with adding any disk to a Linux machine, after you attach the disk you need to initialize and format it so it's ready for use.</span></span> <span data-ttu-id="da84c-111">This article details attaching both empty disks and disks already containing data to your VMs, as well as how to then initialize and format a new disk.</span><span class="sxs-lookup"><span data-stu-id="da84c-111">This article details attaching both empty disks and disks already containing data to your VMs, as well as how to then initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="da84c-112">It's a best practice to use one or more separate disks to store a virtual machine's data.</span><span class="sxs-lookup"><span data-stu-id="da84c-112">It's a best practice to use one or more separate disks to store a virtual machine's data.</span></span> <span data-ttu-id="da84c-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span><span class="sxs-lookup"><span data-stu-id="da84c-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="da84c-114">**Do not use the temporary disk to store persistent data.**</span><span class="sxs-lookup"><span data-stu-id="da84c-114">**Do not use the temporary disk to store persistent data.**</span></span> <span data-ttu-id="da84c-115">As the name implies, it provides temporary storage only.</span><span class="sxs-lookup"><span data-stu-id="da84c-115">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="da84c-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="da84c-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="da84c-117">The temporary disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span><span class="sxs-lookup"><span data-stu-id="da84c-117">The temporary disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="da84c-118">On the other hand, a data disk might be named by the Linux kernel something like `/dev/sdc`, and you need to partition, format, and mount this resource.</span><span class="sxs-lookup"><span data-stu-id="da84c-118">On the other hand, a data disk might be named by the Linux kernel something like `/dev/sdc`, and you need to partition, format, and mount this resource.</span></span> <span data-ttu-id="da84c-119">See the [Azure Linux Agent User Guide][Agent] for details.</span><span class="sxs-lookup"><span data-stu-id="da84c-119">See the [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="da84c-120">Initialize a new data disk in Linux</span><span class="sxs-lookup"><span data-stu-id="da84c-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="da84c-121">SSH to your VM.</span><span class="sxs-lookup"><span data-stu-id="da84c-121">SSH to your VM.</span></span> <span data-ttu-id="da84c-122">For more information, see [How to log on to a virtual machine running Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="da84c-122">For more information, see [How to log on to a virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="da84c-123">Next you need to find the device identifier for the data disk to initialize.</span><span class="sxs-lookup"><span data-stu-id="da84c-123">Next you need to find the device identifier for the data disk to initialize.</span></span> <span data-ttu-id="da84c-124">There are two ways to do that:</span><span class="sxs-lookup"><span data-stu-id="da84c-124">There are two ways to do that:</span></span>
   
    <span data-ttu-id="da84c-125">a) Grep for SCSI devices in the logs, such as in the following command:</span><span class="sxs-lookup"><span data-stu-id="da84c-125">a) Grep for SCSI devices in the logs, such as in the following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="da84c-126">For recent Ubuntu distributions, you may need to use `sudo grep SCSI /var/log/syslog` because logging to `/var/log/messages` might be disabled by default.</span><span class="sxs-lookup"><span data-stu-id="da84c-126">For recent Ubuntu distributions, you may need to use `sudo grep SCSI /var/log/syslog` because logging to `/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="da84c-127">You can find the identifier of the last data disk that was added in the messages that are displayed.</span><span class="sxs-lookup"><span data-stu-id="da84c-127">You can find the identifier of the last data disk that was added in the messages that are displayed.</span></span>
   
    ![Get the disk messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="da84c-129">OR</span><span class="sxs-lookup"><span data-stu-id="da84c-129">OR</span></span>
   
    <span data-ttu-id="da84c-130">b) Use the `lsscsi` command to find out the device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span><span class="sxs-lookup"><span data-stu-id="da84c-130">b) Use the `lsscsi` command to find out the device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="da84c-131">You can find the disk you are looking for by its *lun* or **logical unit number**.</span><span class="sxs-lookup"><span data-stu-id="da84c-131">You can find the disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="da84c-132">For example, the *lun* for the disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span><span class="sxs-lookup"><span data-stu-id="da84c-132">For example, the *lun* for the disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="da84c-133">The output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="da84c-133">The output is similar to the following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="da84c-134">Compare this data with the output of `lsscsi` for the same sample virtual machine:</span><span class="sxs-lookup"><span data-stu-id="da84c-134">Compare this data with the output of `lsscsi` for the same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="da84c-135">The last number in the tuple in each row is the *lun*.</span><span class="sxs-lookup"><span data-stu-id="da84c-135">The last number in the tuple in each row is the *lun*.</span></span> <span data-ttu-id="da84c-136">See `man lsscsi` for more information.</span><span class="sxs-lookup"><span data-stu-id="da84c-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="da84c-137">At the prompt, type the following command to create your device:</span><span class="sxs-lookup"><span data-stu-id="da84c-137">At the prompt, type the following command to create your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="da84c-138">When prompted, type **n** to create a partition.</span><span class="sxs-lookup"><span data-stu-id="da84c-138">When prompted, type **n** to create a partition.</span></span>

    ![Create device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="da84c-140">When prompted, type **p** to make the partition the primary partition.</span><span class="sxs-lookup"><span data-stu-id="da84c-140">When prompted, type **p** to make the partition the primary partition.</span></span> <span data-ttu-id="da84c-141">Type **1** to make it the first partition, and then type enter to accept the default value for the cylinder.</span><span class="sxs-lookup"><span data-stu-id="da84c-141">Type **1** to make it the first partition, and then type enter to accept the default value for the cylinder.</span></span> <span data-ttu-id="da84c-142">On some systems, it can show the default values of the first and the last sectors, instead of the cylinder.</span><span class="sxs-lookup"><span data-stu-id="da84c-142">On some systems, it can show the default values of the first and the last sectors, instead of the cylinder.</span></span> <span data-ttu-id="da84c-143">You can choose to accept these defaults.</span><span class="sxs-lookup"><span data-stu-id="da84c-143">You can choose to accept these defaults.</span></span>

    ![Create partition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="da84c-145">Type **p** to see the details about the disk that is being partitioned.</span><span class="sxs-lookup"><span data-stu-id="da84c-145">Type **p** to see the details about the disk that is being partitioned.</span></span>

    ![List disk information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="da84c-147">Type **w** to write the settings for the disk.</span><span class="sxs-lookup"><span data-stu-id="da84c-147">Type **w** to write the settings for the disk.</span></span>

    ![Write the disk changes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="da84c-149">Now you can create the file system on the new partition.</span><span class="sxs-lookup"><span data-stu-id="da84c-149">Now you can create the file system on the new partition.</span></span> <span data-ttu-id="da84c-150">Append the partition number to the device ID (in the following example `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="da84c-150">Append the partition number to the device ID (in the following example `/dev/sdc1`).</span></span> <span data-ttu-id="da84c-151">The following example creates an ext4 partition on /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="da84c-151">The following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Create file system](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="da84c-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span><span class="sxs-lookup"><span data-stu-id="da84c-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="da84c-154">For these systems, it is recommended to format the new file system as ext3 rather than ext4.</span><span class="sxs-lookup"><span data-stu-id="da84c-154">For these systems, it is recommended to format the new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="da84c-155">Make a directory to mount the new file system, as follows:</span><span class="sxs-lookup"><span data-stu-id="da84c-155">Make a directory to mount the new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="da84c-156">Finally you can mount the drive, as follows:</span><span class="sxs-lookup"><span data-stu-id="da84c-156">Finally you can mount the drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="da84c-157">The data disk is now ready to use as **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="da84c-157">The data disk is now ready to use as **/datadrive**.</span></span>
   
    ![Create the directory and mount the disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="da84c-159">Add the new drive to /etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="da84c-159">Add the new drive to /etc/fstab:</span></span>
   
    <span data-ttu-id="da84c-160">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span><span class="sxs-lookup"><span data-stu-id="da84c-160">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="da84c-161">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="da84c-161">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="da84c-162">Using the UUID avoids the incorrect disk being mounted to a given location if the OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span><span class="sxs-lookup"><span data-stu-id="da84c-162">Using the UUID avoids the incorrect disk being mounted to a given location if the OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="da84c-163">To find the UUID of the new drive, you can use the **blkid** utility:</span><span class="sxs-lookup"><span data-stu-id="da84c-163">To find the UUID of the new drive, you can use the **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="da84c-164">The output looks similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="da84c-164">The output looks similar to the following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="da84c-165">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span><span class="sxs-lookup"><span data-stu-id="da84c-165">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="da84c-166">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span><span class="sxs-lookup"><span data-stu-id="da84c-166">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="da84c-167">It is also recommended that a backup of the /etc/fstab file is created before editing.</span><span class="sxs-lookup"><span data-stu-id="da84c-167">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="da84c-168">Next, open the **/etc/fstab** file in a text editor:</span><span class="sxs-lookup"><span data-stu-id="da84c-168">Next, open the **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="da84c-169">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="da84c-169">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="da84c-170">Add the following line to the end of the **/etc/fstab** file:</span><span class="sxs-lookup"><span data-stu-id="da84c-170">Add the following line to the end of the **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="da84c-171">Or, on systems based on SuSE Linux you may need to use a slightly different format:</span><span class="sxs-lookup"><span data-stu-id="da84c-171">Or, on systems based on SuSE Linux you may need to use a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="da84c-172">The `nofail` option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span><span class="sxs-lookup"><span data-stu-id="da84c-172">The `nofail` option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="da84c-173">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="da84c-173">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="da84c-174">You can now test that the file system is mounted properly by unmounting and then remounting the file system, i.e. using the example mount point `/datadrive` created in the earlier steps:</span><span class="sxs-lookup"><span data-stu-id="da84c-174">You can now test that the file system is mounted properly by unmounting and then remounting the file system, i.e. using the example mount point `/datadrive` created in the earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="da84c-175">If the `mount` command produces an error, check the /etc/fstab file for correct syntax.</span><span class="sxs-lookup"><span data-stu-id="da84c-175">If the `mount` command produces an error, check the /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="da84c-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span><span class="sxs-lookup"><span data-stu-id="da84c-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="da84c-177">Make the drive writable by using this command:</span><span class="sxs-lookup"><span data-stu-id="da84c-177">Make the drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="da84c-178">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span><span class="sxs-lookup"><span data-stu-id="da84c-178">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="da84c-179">If this is a common occurrence, most distributions provide either the `nofail` and/or `nobootwait` fstab options that allow a system to boot even if the disk fails to mount at boot time.</span><span class="sxs-lookup"><span data-stu-id="da84c-179">If this is a common occurrence, most distributions provide either the `nofail` and/or `nobootwait` fstab options that allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="da84c-180">Consult your distribution's documentation for more information on these parameters.</span><span class="sxs-lookup"><span data-stu-id="da84c-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="da84c-181">TRIM/UNMAP support for Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="da84c-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="da84c-182">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span><span class="sxs-lookup"><span data-stu-id="da84c-182">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="da84c-183">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span><span class="sxs-lookup"><span data-stu-id="da84c-183">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="da84c-184">Discarding pages can save cost if you create large files and then delete them.</span><span class="sxs-lookup"><span data-stu-id="da84c-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="da84c-185">There are two ways to enable TRIM support in your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="da84c-185">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="da84c-186">As usual, consult your distribution for the recommended approach:</span><span class="sxs-lookup"><span data-stu-id="da84c-186">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="da84c-187">Use the `discard` mount option in `/etc/fstab`, for example:</span><span class="sxs-lookup"><span data-stu-id="da84c-187">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="da84c-188">In some cases the `discard` option may have performance implications.</span><span class="sxs-lookup"><span data-stu-id="da84c-188">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="da84c-189">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span><span class="sxs-lookup"><span data-stu-id="da84c-189">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="da84c-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="da84c-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="da84c-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="da84c-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="da84c-192">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="da84c-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="da84c-193">Next Steps</span><span class="sxs-lookup"><span data-stu-id="da84c-193">Next Steps</span></span>
<span data-ttu-id="da84c-194">You can read more about using your Linux VM in the following articles:</span><span class="sxs-lookup"><span data-stu-id="da84c-194">You can read more about using your Linux VM in the following articles:</span></span>

* <span data-ttu-id="da84c-195">[How to log on to a virtual machine running Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="da84c-195">[How to log on to a virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="da84c-196">How to detach a disk from a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="da84c-196">How to detach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="da84c-197">Using the Azure CLI with the Classic deployment model</span><span class="sxs-lookup"><span data-stu-id="da84c-197">Using the Azure CLI with the Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="da84c-198">Configure RAID on a Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="da84c-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="da84c-199">Configure LVM on a Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="da84c-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md







