---
title: Attach a data disk to a Linux VM | Microsoft Docs
description: Use the portal to attach new or existing data disk to a Linux VM.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2018
ms.author: cynthn
ms.openlocfilehash: f3636f6f88da53f2fcad8e0e2bb692533681c592
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775014"
---
# <a name="use-the-portal-to-attach-a-data-disk-to-a-linux-vm"></a><span data-ttu-id="70508-103">Use the portal to attach a data disk to a Linux VM</span><span class="sxs-lookup"><span data-stu-id="70508-103">Use the portal to attach a data disk to a Linux VM</span></span> 
<span data-ttu-id="70508-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="70508-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span></span> <span data-ttu-id="70508-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70508-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="70508-106">Before you attach disks to your VM, review these tips:</span><span class="sxs-lookup"><span data-stu-id="70508-106">Before you attach disks to your VM, review these tips:</span></span>

* <span data-ttu-id="70508-107">The size of the virtual machine controls how many data disks you can attach.</span><span class="sxs-lookup"><span data-stu-id="70508-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="70508-108">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70508-108">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="70508-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70508-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="70508-110">You can use both Premium and Standard disks with these virtual machines.</span><span class="sxs-lookup"><span data-stu-id="70508-110">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="70508-111">Premium storage is available in certain regions.</span><span class="sxs-lookup"><span data-stu-id="70508-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="70508-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../windows/premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70508-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../windows/premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="70508-113">Disks attached to virtual machines are actually .vhd files stored in Azure.</span><span class="sxs-lookup"><span data-stu-id="70508-113">Disks attached to virtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="70508-114">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70508-114">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="70508-115">After attaching the disk, you need to [connect to the Linux VM to mount the new disk](#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="70508-115">After attaching the disk, you need to [connect to the Linux VM to mount the new disk](#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="70508-116">Find the virtual machine</span><span class="sxs-lookup"><span data-stu-id="70508-116">Find the virtual machine</span></span>
1. <span data-ttu-id="70508-117">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="70508-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="70508-118">On the left menu, click **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="70508-118">On the left menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="70508-119">Select the virtual machine from the list.</span><span class="sxs-lookup"><span data-stu-id="70508-119">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="70508-120">To the Virtual machines page, in **Essentials**, click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="70508-120">To the Virtual machines page, in **Essentials**, click **Disks**.</span></span>
   
    ![Open disk settings](./media/attach-disk-portal/find-disk-settings.png)


## <a name="attach-a-new-disk"></a><span data-ttu-id="70508-122">Attach a new disk</span><span class="sxs-lookup"><span data-stu-id="70508-122">Attach a new disk</span></span>

1. <span data-ttu-id="70508-123">On the **Disks** pane, click **+ Add data disk**.</span><span class="sxs-lookup"><span data-stu-id="70508-123">On the **Disks** pane, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="70508-124">Click the drop-down menu for **Name** and select **Create disk**:</span><span class="sxs-lookup"><span data-stu-id="70508-124">Click the drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Create Azure managed disk](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="70508-126">Enter a name for your managed disk.</span><span class="sxs-lookup"><span data-stu-id="70508-126">Enter a name for your managed disk.</span></span> <span data-ttu-id="70508-127">Review the default settings, update as necessary, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="70508-127">Review the default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Review disk settings](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="70508-129">Click **Save** to create the managed disk and update the VM configuration:</span><span class="sxs-lookup"><span data-stu-id="70508-129">Click **Save** to create the managed disk and update the VM configuration:</span></span>

   ![Save new Azure Managed Disk](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="70508-131">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="70508-131">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="70508-132">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span><span class="sxs-lookup"><span data-stu-id="70508-132">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span></span>

   ![Azure Managed Disk in resource group](./media/attach-disk-portal/view-md-resource-group.png)

## <a name="attach-an-existing-disk"></a><span data-ttu-id="70508-134">Attach an existing disk</span><span class="sxs-lookup"><span data-stu-id="70508-134">Attach an existing disk</span></span>
1. <span data-ttu-id="70508-135">On the **Disks** pane, click **+ Add data disk**.</span><span class="sxs-lookup"><span data-stu-id="70508-135">On the **Disks** pane, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="70508-136">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="70508-136">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span></span> <span data-ttu-id="70508-137">Select the managed disk to attach:</span><span class="sxs-lookup"><span data-stu-id="70508-137">Select the managed disk to attach:</span></span>

   ![Attach existing Azure Managed Disk](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="70508-139">Click **Save** to attach the existing managed disk and update the VM configuration:</span><span class="sxs-lookup"><span data-stu-id="70508-139">Click **Save** to attach the existing managed disk and update the VM configuration:</span></span>
   
   ![Save Azure Managed Disk updates](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="70508-141">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span><span class="sxs-lookup"><span data-stu-id="70508-141">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="connect-to-the-linux-vm-to-mount-the-new-disk"></a><span data-ttu-id="70508-142">Connect to the Linux VM to mount the new disk</span><span class="sxs-lookup"><span data-stu-id="70508-142">Connect to the Linux VM to mount the new disk</span></span>
<span data-ttu-id="70508-143">To partition, format, and mount your new disk so your Linux VM can use it, SSH into your VM.</span><span class="sxs-lookup"><span data-stu-id="70508-143">To partition, format, and mount your new disk so your Linux VM can use it, SSH into your VM.</span></span> <span data-ttu-id="70508-144">For more information, see [How to use SSH with Linux on Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="70508-144">For more information, see [How to use SSH with Linux on Azure](mac-create-ssh-keys.md).</span></span> <span data-ttu-id="70508-145">The following example connects to a VM with the public DNS entry of *mypublicdns.westus.cloudapp.azure.com* with the username *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="70508-145">The following example connects to a VM with the public DNS entry of *mypublicdns.westus.cloudapp.azure.com* with the username *azureuser*:</span></span> 

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="70508-146">Once connected to your VM, you're ready to attach a disk.</span><span class="sxs-lookup"><span data-stu-id="70508-146">Once connected to your VM, you're ready to attach a disk.</span></span> <span data-ttu-id="70508-147">First, find the disk using `dmesg` (the method you use to discover your new disk may vary).</span><span class="sxs-lookup"><span data-stu-id="70508-147">First, find the disk using `dmesg` (the method you use to discover your new disk may vary).</span></span> <span data-ttu-id="70508-148">The following example uses dmesg to filter on *SCSI* disks:</span><span class="sxs-lookup"><span data-stu-id="70508-148">The following example uses dmesg to filter on *SCSI* disks:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="70508-149">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="70508-149">The output is similar to the following example:</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="70508-150">Here, *sdc* is the disk that we want.</span><span class="sxs-lookup"><span data-stu-id="70508-150">Here, *sdc* is the disk that we want.</span></span> <span data-ttu-id="70508-151">Partition the disk with `fdisk`, make it a primary disk on partition 1, and accept the other defaults.</span><span class="sxs-lookup"><span data-stu-id="70508-151">Partition the disk with `fdisk`, make it a primary disk on partition 1, and accept the other defaults.</span></span> <span data-ttu-id="70508-152">The following example starts the `fdisk` process on */dev/sdc*:</span><span class="sxs-lookup"><span data-stu-id="70508-152">The following example starts the `fdisk` process on */dev/sdc*:</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="70508-153">Use the `n` command to add a new partition.</span><span class="sxs-lookup"><span data-stu-id="70508-153">Use the `n` command to add a new partition.</span></span> <span data-ttu-id="70508-154">In this example, we also choose `p` for a primary partition and accept the rest of the default values.</span><span class="sxs-lookup"><span data-stu-id="70508-154">In this example, we also choose `p` for a primary partition and accept the rest of the default values.</span></span> <span data-ttu-id="70508-155">The output will be similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="70508-155">The output will be similar to the following example:</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

<span data-ttu-id="70508-156">Print the partition table by typing `p` and then use `w` to write the table to disk and exit.</span><span class="sxs-lookup"><span data-stu-id="70508-156">Print the partition table by typing `p` and then use `w` to write the table to disk and exit.</span></span> <span data-ttu-id="70508-157">The output should look similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="70508-157">The output should look similar to the following example:</span></span>

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

<span data-ttu-id="70508-158">Now, write a file system to the partition with the `mkfs` command.</span><span class="sxs-lookup"><span data-stu-id="70508-158">Now, write a file system to the partition with the `mkfs` command.</span></span> <span data-ttu-id="70508-159">Specify your filesystem type and the device name.</span><span class="sxs-lookup"><span data-stu-id="70508-159">Specify your filesystem type and the device name.</span></span> <span data-ttu-id="70508-160">The following example creates an *ext4* filesystem on the */dev/sdc1* partition that was created in the preceding steps:</span><span class="sxs-lookup"><span data-stu-id="70508-160">The following example creates an *ext4* filesystem on the */dev/sdc1* partition that was created in the preceding steps:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="70508-161">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="70508-161">The output is similar to the following example:</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

<span data-ttu-id="70508-162">Now, create a directory to mount the file system using `mkdir`.</span><span class="sxs-lookup"><span data-stu-id="70508-162">Now, create a directory to mount the file system using `mkdir`.</span></span> <span data-ttu-id="70508-163">The following example creates a directory at */datadrive*:</span><span class="sxs-lookup"><span data-stu-id="70508-163">The following example creates a directory at */datadrive*:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="70508-164">Use `mount` to then mount the filesystem.</span><span class="sxs-lookup"><span data-stu-id="70508-164">Use `mount` to then mount the filesystem.</span></span> <span data-ttu-id="70508-165">The following example mounts the */dev/sdc1* partition to the */datadrive* mount point:</span><span class="sxs-lookup"><span data-stu-id="70508-165">The following example mounts the */dev/sdc1* partition to the */datadrive* mount point:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="70508-166">To ensure that the drive is remounted automatically after a reboot, it must be added to the */etc/fstab* file.</span><span class="sxs-lookup"><span data-stu-id="70508-166">To ensure that the drive is remounted automatically after a reboot, it must be added to the */etc/fstab* file.</span></span> <span data-ttu-id="70508-167">It is also highly recommended that the UUID (Universally Unique IDentifier) is used in */etc/fstab* to refer to the drive rather than just the device name (such as, */dev/sdc1*).</span><span class="sxs-lookup"><span data-stu-id="70508-167">It is also highly recommended that the UUID (Universally Unique IDentifier) is used in */etc/fstab* to refer to the drive rather than just the device name (such as, */dev/sdc1*).</span></span> <span data-ttu-id="70508-168">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span><span class="sxs-lookup"><span data-stu-id="70508-168">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="70508-169">Remaining data disks would then be assigned those same device IDs.</span><span class="sxs-lookup"><span data-stu-id="70508-169">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="70508-170">To find the UUID of the new drive, use the `blkid` utility:</span><span class="sxs-lookup"><span data-stu-id="70508-170">To find the UUID of the new drive, use the `blkid` utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="70508-171">The output looks similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="70508-171">The output looks similar to the following example:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="70508-172">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span><span class="sxs-lookup"><span data-stu-id="70508-172">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="70508-173">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span><span class="sxs-lookup"><span data-stu-id="70508-173">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="70508-174">It is also recommended that a backup of the /etc/fstab file is created before editing.</span><span class="sxs-lookup"><span data-stu-id="70508-174">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

<span data-ttu-id="70508-175">Next, open the */etc/fstab* file in a text editor as follows:</span><span class="sxs-lookup"><span data-stu-id="70508-175">Next, open the */etc/fstab* file in a text editor as follows:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="70508-176">In this example, use the UUID value for the */dev/sdc1* device that was created in the previous steps, and the mountpoint of */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="70508-176">In this example, use the UUID value for the */dev/sdc1* device that was created in the previous steps, and the mountpoint of */datadrive*.</span></span> <span data-ttu-id="70508-177">Add the following line to the end of the */etc/fstab* file:</span><span class="sxs-lookup"><span data-stu-id="70508-177">Add the following line to the end of the */etc/fstab* file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="70508-178">Later removing a data disk without editing fstab could cause the VM to fail to boot.</span><span class="sxs-lookup"><span data-stu-id="70508-178">Later removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="70508-179">Most distributions provide either the *nofail* and/or *nobootwait* fstab options.</span><span class="sxs-lookup"><span data-stu-id="70508-179">Most distributions provide either the *nofail* and/or *nobootwait* fstab options.</span></span> <span data-ttu-id="70508-180">These options allow a system to boot even if the disk fails to mount at boot time.</span><span class="sxs-lookup"><span data-stu-id="70508-180">These options allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="70508-181">Consult your distribution's documentation for more information on these parameters.</span><span class="sxs-lookup"><span data-stu-id="70508-181">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="70508-182">The *nofail* option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span><span class="sxs-lookup"><span data-stu-id="70508-182">The *nofail* option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="70508-183">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="70508-183">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="70508-184">TRIM/UNMAP support for Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="70508-184">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="70508-185">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span><span class="sxs-lookup"><span data-stu-id="70508-185">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="70508-186">This feature is primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded, and can save money if you create large files and then delete them.</span><span class="sxs-lookup"><span data-stu-id="70508-186">This feature is primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded, and can save money if you create large files and then delete them.</span></span>

<span data-ttu-id="70508-187">There are two ways to enable TRIM support in your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="70508-187">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="70508-188">As usual, consult your distribution for the recommended approach:</span><span class="sxs-lookup"><span data-stu-id="70508-188">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="70508-189">Use the `discard` mount option in */etc/fstab*, for example:</span><span class="sxs-lookup"><span data-stu-id="70508-189">Use the `discard` mount option in */etc/fstab*, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="70508-190">In some cases, the `discard` option may have performance implications.</span><span class="sxs-lookup"><span data-stu-id="70508-190">In some cases, the `discard` option may have performance implications.</span></span> <span data-ttu-id="70508-191">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span><span class="sxs-lookup"><span data-stu-id="70508-191">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="70508-192">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="70508-192">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="70508-193">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="70508-193">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="70508-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="70508-194">Next steps</span></span>
<span data-ttu-id="70508-195">You can also [attach a data disk](add-disk.md) using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="70508-195">You can also [attach a data disk](add-disk.md) using the Azure CLI.</span></span>
