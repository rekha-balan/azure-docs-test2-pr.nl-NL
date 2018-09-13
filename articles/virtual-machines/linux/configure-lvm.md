---
title: Configure LVM on a virtual machine running Linux | Microsoft Docs
description: Learn how to configure LVM on Linux in Azure.
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 33821e01034b2bfb23d31f5198b5df19cd521f02
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552914"
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="bd39d-103">Configure LVM on a Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="bd39d-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="bd39d-104">This document will discuss how to configure Logical Volume Manager (LVM) in your Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bd39d-104">This document will discuss how to configure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="bd39d-105">While it is feasible to configure LVM on any disk attached to the virtual machine, by default most cloud images will not have LVM configured on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="bd39d-105">While it is feasible to configure LVM on any disk attached to the virtual machine, by default most cloud images will not have LVM configured on the OS disk.</span></span> <span data-ttu-id="bd39d-106">This is to prevent problems with duplicate volume groups if the OS disk is ever attached to another VM of the same distribution and type, i.e. during a recovery scenario.</span><span class="sxs-lookup"><span data-stu-id="bd39d-106">This is to prevent problems with duplicate volume groups if the OS disk is ever attached to another VM of the same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="bd39d-107">Therefore it is recommended only to use LVM on the data disks.</span><span class="sxs-lookup"><span data-stu-id="bd39d-107">Therefore it is recommended only to use LVM on the data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="bd39d-108">Linear vs. striped logical volumes</span><span class="sxs-lookup"><span data-stu-id="bd39d-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="bd39d-109">LVM can be used to combine a number of physical disks into a single storage volume.</span><span class="sxs-lookup"><span data-stu-id="bd39d-109">LVM can be used to combine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="bd39d-110">By default LVM will usually create linear logical volumes, which means that the physical storage is concatenated together.</span><span class="sxs-lookup"><span data-stu-id="bd39d-110">By default LVM will usually create linear logical volumes, which means that the physical storage is concatenated together.</span></span> <span data-ttu-id="bd39d-111">In this case read/write operations will typically only be sent to a single disk.</span><span class="sxs-lookup"><span data-stu-id="bd39d-111">In this case read/write operations will typically only be sent to a single disk.</span></span> <span data-ttu-id="bd39d-112">In contrast, we can also create striped logical volumes where reads and writes are distributed to multiple disks contained in the volume group (i.e. similar to RAID0).</span><span class="sxs-lookup"><span data-stu-id="bd39d-112">In contrast, we can also create striped logical volumes where reads and writes are distributed to multiple disks contained in the volume group (i.e. similar to RAID0).</span></span> <span data-ttu-id="bd39d-113">For performance reasons it is likely you will want to stripe your logical volumes so that reads and writes utilize all your attached data disks.</span><span class="sxs-lookup"><span data-stu-id="bd39d-113">For performance reasons it is likely you will want to stripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="bd39d-114">This document will describe how to combine several data disks into a single volume group, and then create a striped logical volume.</span><span class="sxs-lookup"><span data-stu-id="bd39d-114">This document will describe how to combine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="bd39d-115">The steps below are somewhat generalized to work with most distributions.</span><span class="sxs-lookup"><span data-stu-id="bd39d-115">The steps below are somewhat generalized to work with most distributions.</span></span> <span data-ttu-id="bd39d-116">In most cases the utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span><span class="sxs-lookup"><span data-stu-id="bd39d-116">In most cases the utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="bd39d-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span><span class="sxs-lookup"><span data-stu-id="bd39d-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="bd39d-118">Attaching data disks</span><span class="sxs-lookup"><span data-stu-id="bd39d-118">Attaching data disks</span></span>
<span data-ttu-id="bd39d-119">One will usually want to start with two or more empty data disks when using LVM.</span><span class="sxs-lookup"><span data-stu-id="bd39d-119">One will usually want to start with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="bd39d-120">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span><span class="sxs-lookup"><span data-stu-id="bd39d-120">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="bd39d-121">This article will not go into detail on how to provision and attach data disks to a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bd39d-121">This article will not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span> <span data-ttu-id="bd39d-122">Please see the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span><span class="sxs-lookup"><span data-stu-id="bd39d-122">Please see the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-lvm-utilities"></a><span data-ttu-id="bd39d-123">Install the LVM utilities</span><span class="sxs-lookup"><span data-stu-id="bd39d-123">Install the LVM utilities</span></span>
* <span data-ttu-id="bd39d-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="bd39d-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="bd39d-125">**RHEL, CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="bd39d-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="bd39d-126">**SLES 12 and openSUSE**</span><span class="sxs-lookup"><span data-stu-id="bd39d-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="bd39d-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="bd39d-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="bd39d-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` to "enable":</span><span class="sxs-lookup"><span data-stu-id="bd39d-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` to "enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="bd39d-129">Configure LVM</span><span class="sxs-lookup"><span data-stu-id="bd39d-129">Configure LVM</span></span>
<span data-ttu-id="bd39d-130">In this guide we will assume you have attached three data disks, which we'll refer to as `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="bd39d-130">In this guide we will assume you have attached three data disks, which we'll refer to as `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="bd39d-131">Note that these may not always be the same path names in your VM.</span><span class="sxs-lookup"><span data-stu-id="bd39d-131">Note that these may not always be the same path names in your VM.</span></span> <span data-ttu-id="bd39d-132">You can run '`sudo fdisk -l`' or similar command to list your available disks.</span><span class="sxs-lookup"><span data-stu-id="bd39d-132">You can run '`sudo fdisk -l`' or similar command to list your available disks.</span></span>

1. <span data-ttu-id="bd39d-133">Prepare the physical volumes:</span><span class="sxs-lookup"><span data-stu-id="bd39d-133">Prepare the physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="bd39d-134">Create a volume group.</span><span class="sxs-lookup"><span data-stu-id="bd39d-134">Create a volume group.</span></span> <span data-ttu-id="bd39d-135">In this example we are calling the volume group `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="bd39d-135">In this example we are calling the volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="bd39d-136">Create the logical volume(s).</span><span class="sxs-lookup"><span data-stu-id="bd39d-136">Create the logical volume(s).</span></span> <span data-ttu-id="bd39d-137">The command below we will create a single logical volume called `data-lv01` to span the entire volume group, but note that it is also feasible to create multiple logical volumes in the volume group.</span><span class="sxs-lookup"><span data-stu-id="bd39d-137">The command below we will create a single logical volume called `data-lv01` to span the entire volume group, but note that it is also feasible to create multiple logical volumes in the volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="bd39d-138">Format the logical volume</span><span class="sxs-lookup"><span data-stu-id="bd39d-138">Format the logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="bd39d-139">With SLES11 use `-t ext3` instead of ext4.</span><span class="sxs-lookup"><span data-stu-id="bd39d-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="bd39d-140">SLES11 only supports read-only access to ext4 filesystems.</span><span class="sxs-lookup"><span data-stu-id="bd39d-140">SLES11 only supports read-only access to ext4 filesystems.</span></span>

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="bd39d-141">Add the new file system to /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="bd39d-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bd39d-142">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span><span class="sxs-lookup"><span data-stu-id="bd39d-142">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="bd39d-143">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span><span class="sxs-lookup"><span data-stu-id="bd39d-143">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="bd39d-144">It is also recommended that a backup of the `/etc/fstab` file is created before editing.</span><span class="sxs-lookup"><span data-stu-id="bd39d-144">It is also recommended that a backup of the `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="bd39d-145">Create the desired mount point for your new file system, for example:</span><span class="sxs-lookup"><span data-stu-id="bd39d-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="bd39d-146">Locate the logical volume path</span><span class="sxs-lookup"><span data-stu-id="bd39d-146">Locate the logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="bd39d-147">Open `/etc/fstab` in a text editor and add an entry for the new file system, for example:</span><span class="sxs-lookup"><span data-stu-id="bd39d-147">Open `/etc/fstab` in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="bd39d-148">Then, save and close `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="bd39d-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="bd39d-149">Test that the `/etc/fstab` entry is correct:</span><span class="sxs-lookup"><span data-stu-id="bd39d-149">Test that the `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="bd39d-150">If this command results in an error message please check the syntax in the `/etc/fstab` file.</span><span class="sxs-lookup"><span data-stu-id="bd39d-150">If this command results in an error message please check the syntax in the `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="bd39d-151">Next run the `mount` command to ensure the file system is mounted:</span><span class="sxs-lookup"><span data-stu-id="bd39d-151">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="bd39d-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="bd39d-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="bd39d-153">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the `/etc/fstab` file.</span><span class="sxs-lookup"><span data-stu-id="bd39d-153">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="bd39d-154">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span><span class="sxs-lookup"><span data-stu-id="bd39d-154">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="bd39d-155">Please refer to your distribution's documentation for more information on these parameters.</span><span class="sxs-lookup"><span data-stu-id="bd39d-155">Please refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="bd39d-156">Example (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="bd39d-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="bd39d-157">TRIM/UNMAP support</span><span class="sxs-lookup"><span data-stu-id="bd39d-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="bd39d-158">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span><span class="sxs-lookup"><span data-stu-id="bd39d-158">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="bd39d-159">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span><span class="sxs-lookup"><span data-stu-id="bd39d-159">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="bd39d-160">Discarding pages can save cost if you create large files and then delete them.</span><span class="sxs-lookup"><span data-stu-id="bd39d-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="bd39d-161">There are two ways to enable TRIM support in your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="bd39d-161">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="bd39d-162">As usual, consult your distribution for the recommended approach:</span><span class="sxs-lookup"><span data-stu-id="bd39d-162">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="bd39d-163">Use the `discard` mount option in `/etc/fstab`, for example:</span><span class="sxs-lookup"><span data-stu-id="bd39d-163">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="bd39d-164">In some cases the `discard` option may have performance implications.</span><span class="sxs-lookup"><span data-stu-id="bd39d-164">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="bd39d-165">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span><span class="sxs-lookup"><span data-stu-id="bd39d-165">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="bd39d-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="bd39d-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="bd39d-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="bd39d-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
