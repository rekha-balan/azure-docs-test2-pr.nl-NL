---
title: Configure software RAID on a virtual machine running Linux | Microsoft Docs
description: Learn how to use mdadm to configure RAID on Linux in Azure.
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: 862cfe967907b604ff915fa8e4aa0fae53d374df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564307"
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="234a7-103">Configure Software RAID on Linux</span><span class="sxs-lookup"><span data-stu-id="234a7-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="234a7-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span><span class="sxs-lookup"><span data-stu-id="234a7-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="234a7-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span><span class="sxs-lookup"><span data-stu-id="234a7-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="234a7-106">Attaching data disks</span><span class="sxs-lookup"><span data-stu-id="234a7-106">Attaching data disks</span></span>
<span data-ttu-id="234a7-107">Two or more empty data disks are needed to configure a RAID device.</span><span class="sxs-lookup"><span data-stu-id="234a7-107">Two or more empty data disks are needed to configure a RAID device.</span></span>  <span data-ttu-id="234a7-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span><span class="sxs-lookup"><span data-stu-id="234a7-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span></span>  <span data-ttu-id="234a7-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span><span class="sxs-lookup"><span data-stu-id="234a7-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="234a7-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="234a7-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span>  <span data-ttu-id="234a7-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span><span class="sxs-lookup"><span data-stu-id="234a7-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-mdadm-utility"></a><span data-ttu-id="234a7-112">Install the mdadm utility</span><span class="sxs-lookup"><span data-stu-id="234a7-112">Install the mdadm utility</span></span>
* <span data-ttu-id="234a7-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="234a7-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="234a7-114">**CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="234a7-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="234a7-115">**SLES and openSUSE**</span><span class="sxs-lookup"><span data-stu-id="234a7-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-the-disk-partitions"></a><span data-ttu-id="234a7-116">Create the disk partitions</span><span class="sxs-lookup"><span data-stu-id="234a7-116">Create the disk partitions</span></span>
<span data-ttu-id="234a7-117">In this example, we create a single disk partition on /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="234a7-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="234a7-118">The new disk partition will be called /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="234a7-118">The new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="234a7-119">Start `fdisk` to begin creating partitions</span><span class="sxs-lookup"><span data-stu-id="234a7-119">Start `fdisk` to begin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off the mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="234a7-120">Press 'n' at the prompt to create a **n**ew partition:</span><span class="sxs-lookup"><span data-stu-id="234a7-120">Press 'n' at the prompt to create a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="234a7-121">Next, press 'p' to create a **p**rimary partition:</span><span class="sxs-lookup"><span data-stu-id="234a7-121">Next, press 'p' to create a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="234a7-122">Press '1' to select partition number 1:</span><span class="sxs-lookup"><span data-stu-id="234a7-122">Press '1' to select partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="234a7-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span><span class="sxs-lookup"><span data-stu-id="234a7-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="234a7-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span><span class="sxs-lookup"><span data-stu-id="234a7-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span></span> <span data-ttu-id="234a7-125">Or, press `<enter>` create a single partition that spans the entire drive:</span><span class="sxs-lookup"><span data-stu-id="234a7-125">Or, press `<enter>` create a single partition that spans the entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="234a7-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span><span class="sxs-lookup"><span data-stu-id="234a7-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L to list codes): fd
    ```

8. <span data-ttu-id="234a7-127">Finally, write the partition table to the drive and exit fdisk:</span><span class="sxs-lookup"><span data-stu-id="234a7-127">Finally, write the partition table to the drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    The partition table has been altered!
    ```

## <a name="create-the-raid-array"></a><span data-ttu-id="234a7-128">Create the RAID array</span><span class="sxs-lookup"><span data-stu-id="234a7-128">Create the RAID array</span></span>
1. <span data-ttu-id="234a7-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="234a7-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="234a7-130">After running this command a new RAID device called **/dev/md127** is created.</span><span class="sxs-lookup"><span data-stu-id="234a7-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="234a7-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span><span class="sxs-lookup"><span data-stu-id="234a7-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="234a7-132">Create the file system on the new RAID device</span><span class="sxs-lookup"><span data-stu-id="234a7-132">Create the file system on the new RAID device</span></span>
   
    <span data-ttu-id="234a7-133">a.</span><span class="sxs-lookup"><span data-stu-id="234a7-133">a.</span></span> <span data-ttu-id="234a7-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="234a7-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="234a7-135">b.</span><span class="sxs-lookup"><span data-stu-id="234a7-135">b.</span></span> <span data-ttu-id="234a7-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="234a7-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="234a7-137">c.</span><span class="sxs-lookup"><span data-stu-id="234a7-137">c.</span></span> <span data-ttu-id="234a7-138">**SLES 11** - enable boot.md and create mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="234a7-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="234a7-139">A reboot may be required after making these changes on SUSE systems.</span><span class="sxs-lookup"><span data-stu-id="234a7-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="234a7-140">This step is *not* required on SLES 12.</span><span class="sxs-lookup"><span data-stu-id="234a7-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="234a7-141">Add the new file system to /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="234a7-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="234a7-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span><span class="sxs-lookup"><span data-stu-id="234a7-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="234a7-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span><span class="sxs-lookup"><span data-stu-id="234a7-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="234a7-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span><span class="sxs-lookup"><span data-stu-id="234a7-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="234a7-145">Create the desired mount point for your new file system, for example:</span><span class="sxs-lookup"><span data-stu-id="234a7-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="234a7-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span><span class="sxs-lookup"><span data-stu-id="234a7-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span></span>  <span data-ttu-id="234a7-147">Use the `blkid` utility to determine the UUID for the new file system:</span><span class="sxs-lookup"><span data-stu-id="234a7-147">Use the `blkid` utility to determine the UUID for the new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="234a7-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span><span class="sxs-lookup"><span data-stu-id="234a7-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="234a7-149">Or on **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="234a7-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="234a7-150">Then, save and close /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="234a7-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="234a7-151">Test that the /etc/fstab entry is correct:</span><span class="sxs-lookup"><span data-stu-id="234a7-151">Test that the /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="234a7-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span><span class="sxs-lookup"><span data-stu-id="234a7-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span></span>
   
    <span data-ttu-id="234a7-153">Next run the `mount` command to ensure the file system is mounted:</span><span class="sxs-lookup"><span data-stu-id="234a7-153">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="234a7-154">(Optional) Failsafe Boot Parameters</span><span class="sxs-lookup"><span data-stu-id="234a7-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="234a7-155">**fstab configuration**</span><span class="sxs-lookup"><span data-stu-id="234a7-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="234a7-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span><span class="sxs-lookup"><span data-stu-id="234a7-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span></span> <span data-ttu-id="234a7-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span><span class="sxs-lookup"><span data-stu-id="234a7-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="234a7-158">Refer to your distribution's documentation for more information on these parameters.</span><span class="sxs-lookup"><span data-stu-id="234a7-158">Refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="234a7-159">Example (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="234a7-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="234a7-160">**Linux boot parameters**</span><span class="sxs-lookup"><span data-stu-id="234a7-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="234a7-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="234a7-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span></span> <span data-ttu-id="234a7-162">By default this could also result in a non-bootable system.</span><span class="sxs-lookup"><span data-stu-id="234a7-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="234a7-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span><span class="sxs-lookup"><span data-stu-id="234a7-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span></span> <span data-ttu-id="234a7-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span><span class="sxs-lookup"><span data-stu-id="234a7-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="234a7-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span><span class="sxs-lookup"><span data-stu-id="234a7-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="234a7-166">TRIM/UNMAP support</span><span class="sxs-lookup"><span data-stu-id="234a7-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="234a7-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span><span class="sxs-lookup"><span data-stu-id="234a7-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="234a7-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span><span class="sxs-lookup"><span data-stu-id="234a7-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="234a7-169">Discarding pages can save cost if you create large files and then delete them.</span><span class="sxs-lookup"><span data-stu-id="234a7-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="234a7-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span><span class="sxs-lookup"><span data-stu-id="234a7-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span></span> <span data-ttu-id="234a7-171">This is because the unmap granularity on the Host is also 512KB.</span><span class="sxs-lookup"><span data-stu-id="234a7-171">This is because the unmap granularity on the Host is also 512KB.</span></span> <span data-ttu-id="234a7-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span><span class="sxs-lookup"><span data-stu-id="234a7-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span></span>

<span data-ttu-id="234a7-173">There are two ways to enable TRIM support in your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="234a7-173">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="234a7-174">As usual, consult your distribution for the recommended approach:</span><span class="sxs-lookup"><span data-stu-id="234a7-174">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="234a7-175">Use the `discard` mount option in `/etc/fstab`, for example:</span><span class="sxs-lookup"><span data-stu-id="234a7-175">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="234a7-176">In some cases the `discard` option may have performance implications.</span><span class="sxs-lookup"><span data-stu-id="234a7-176">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="234a7-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span><span class="sxs-lookup"><span data-stu-id="234a7-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="234a7-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="234a7-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="234a7-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="234a7-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
