---
title: Optimize MySQL performance on Linux | Microsoft Docs
description: Learn how to optimize MySQL running on an Azure virtual machine (VM) running Linux.
services: virtual-machines-linux
documentationcenter: ''
author: NingKuang
manager: jeconnoc
editor: ''
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 447532452a848c88fd927f42e4263cef4742dd89
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44798127"
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="40078-103">Optimize MySQL Performance on Azure Linux VMs</span><span class="sxs-lookup"><span data-stu-id="40078-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="40078-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span><span class="sxs-lookup"><span data-stu-id="40078-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="40078-105">This article focuses on optimizing performance through storage, system, and database configurations.</span><span class="sxs-lookup"><span data-stu-id="40078-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40078-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span><span class="sxs-lookup"><span data-stu-id="40078-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="40078-107">This article covers using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="40078-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="40078-108">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="40078-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="40078-109">For information about Linux VM optimizations with the Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40078-109">For information about Linux VM optimizations with the Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> [!INCLUDE [virtual-machines-common-classic-createportal](../../../../includes/virtual-machines-classic-portal.md)]

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="40078-110">Utilize RAID on an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="40078-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="40078-111">Storage is the key factor that affects database performance in cloud environments.</span><span class="sxs-lookup"><span data-stu-id="40078-111">Storage is the key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="40078-112">Compared to a single disk, RAID can provide faster access via concurrency.</span><span class="sxs-lookup"><span data-stu-id="40078-112">Compared to a single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="40078-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="40078-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="40078-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span><span class="sxs-lookup"><span data-stu-id="40078-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="40078-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when the number of RAID disks is doubled (from two to four, four to eight, etc.).</span><span class="sxs-lookup"><span data-stu-id="40078-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when the number of RAID disks is doubled (from two to four, four to eight, etc.).</span></span> <span data-ttu-id="40078-116">See [Appendix A](#AppendixA) for details.</span><span class="sxs-lookup"><span data-stu-id="40078-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="40078-117">In addition to disk I/O, MySQL performance improves when you increase the RAID level.</span><span class="sxs-lookup"><span data-stu-id="40078-117">In addition to disk I/O, MySQL performance improves when you increase the RAID level.</span></span>  <span data-ttu-id="40078-118">See [Appendix B](#AppendixB) for details.</span><span class="sxs-lookup"><span data-stu-id="40078-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="40078-119">You might also want to consider the chunk size.</span><span class="sxs-lookup"><span data-stu-id="40078-119">You might also want to consider the chunk size.</span></span> <span data-ttu-id="40078-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span><span class="sxs-lookup"><span data-stu-id="40078-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="40078-121">However, when the chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span><span class="sxs-lookup"><span data-stu-id="40078-121">However, when the chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="40078-122">The current default size is 512 KB, which is proven to be optimal for most general production environments.</span><span class="sxs-lookup"><span data-stu-id="40078-122">The current default size is 512 KB, which is proven to be optimal for most general production environments.</span></span> <span data-ttu-id="40078-123">See [Appendix C](#AppendixC) for details.</span><span class="sxs-lookup"><span data-stu-id="40078-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="40078-124">There are limits on how many disks you can add for different virtual machine types.</span><span class="sxs-lookup"><span data-stu-id="40078-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="40078-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="40078-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="40078-126">You will need four attached data disks to follow the RAID example in this article, although you can choose to set up RAID with fewer disks.</span><span class="sxs-lookup"><span data-stu-id="40078-126">You will need four attached data disks to follow the RAID example in this article, although you can choose to set up RAID with fewer disks.</span></span>  

<span data-ttu-id="40078-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span><span class="sxs-lookup"><span data-stu-id="40078-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="40078-128">For more information on getting started, see How to install MySQL on Azure.</span><span class="sxs-lookup"><span data-stu-id="40078-128">For more information on getting started, see How to install MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="40078-129">Set up RAID on Azure</span><span class="sxs-lookup"><span data-stu-id="40078-129">Set up RAID on Azure</span></span>
<span data-ttu-id="40078-130">The following steps show how to create RAID on Azure by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="40078-130">The following steps show how to create RAID on Azure by using the Azure portal.</span></span> <span data-ttu-id="40078-131">You can also set up RAID by using Windows PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="40078-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="40078-132">In this example, we will configure RAID 0 with four disks.</span><span class="sxs-lookup"><span data-stu-id="40078-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-to-your-virtual-machine"></a><span data-ttu-id="40078-133">Add a data disk to your virtual machine</span><span class="sxs-lookup"><span data-stu-id="40078-133">Add a data disk to your virtual machine</span></span>
<span data-ttu-id="40078-134">In the Azure portal, go to the dashboard and select the virtual machine to which you want to add a data disk.</span><span class="sxs-lookup"><span data-stu-id="40078-134">In the Azure portal, go to the dashboard and select the virtual machine to which you want to add a data disk.</span></span> <span data-ttu-id="40078-135">In this example, the virtual machine is mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="40078-135">In this example, the virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="40078-136">Click **Disks** and then click **Attach New**.</span><span class="sxs-lookup"><span data-stu-id="40078-136">Click **Disks** and then click **Attach New**.</span></span>

![Virtual machines add disk](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="40078-138">Create a new 500 GB disk.</span><span class="sxs-lookup"><span data-stu-id="40078-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="40078-139">Make sure that **Host Cache Preference** is set to **None**.</span><span class="sxs-lookup"><span data-stu-id="40078-139">Make sure that **Host Cache Preference** is set to **None**.</span></span>  <span data-ttu-id="40078-140">When you're finished, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="40078-140">When you're finished, click **OK**.</span></span>

![Attach empty disk](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="40078-142">This adds one empty disk into your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="40078-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="40078-143">Repeat this step three more times so that you have four data disks for RAID.</span><span class="sxs-lookup"><span data-stu-id="40078-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="40078-144">You can see the added drives in the virtual machine by looking at the kernel message log.</span><span class="sxs-lookup"><span data-stu-id="40078-144">You can see the added drives in the virtual machine by looking at the kernel message log.</span></span> <span data-ttu-id="40078-145">For example, to see this on Ubuntu, use the following command:</span><span class="sxs-lookup"><span data-stu-id="40078-145">For example, to see this on Ubuntu, use the following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-the-additional-disks"></a><span data-ttu-id="40078-146">Create RAID with the additional disks</span><span class="sxs-lookup"><span data-stu-id="40078-146">Create RAID with the additional disks</span></span>
<span data-ttu-id="40078-147">The following steps describe how to [configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40078-147">The following steps describe how to [configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="40078-148">If you are using the XFS file system, execute the following steps after you have created RAID.</span><span class="sxs-lookup"><span data-stu-id="40078-148">If you are using the XFS file system, execute the following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="40078-149">To install XFS on Debian, Ubuntu, or Linux Mint, use the following command:</span><span class="sxs-lookup"><span data-stu-id="40078-149">To install XFS on Debian, Ubuntu, or Linux Mint, use the following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="40078-150">To install XFS on Fedora, CentOS, or RHEL, use the following command:</span><span class="sxs-lookup"><span data-stu-id="40078-150">To install XFS on Fedora, CentOS, or RHEL, use the following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="40078-151">Set up a new storage path</span><span class="sxs-lookup"><span data-stu-id="40078-151">Set up a new storage path</span></span>
<span data-ttu-id="40078-152">Use the following command to set up a new storage path:</span><span class="sxs-lookup"><span data-stu-id="40078-152">Use the following command to set up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-the-original-data-to-the-new-storage-path"></a><span data-ttu-id="40078-153">Copy the original data to the new storage path</span><span class="sxs-lookup"><span data-stu-id="40078-153">Copy the original data to the new storage path</span></span>
<span data-ttu-id="40078-154">Use the following command to copy data to the new storage path:</span><span class="sxs-lookup"><span data-stu-id="40078-154">Use the following command to copy data to the new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-the-data-disk"></a><span data-ttu-id="40078-155">Modify permissions so MySQL can access (read and write) the data disk</span><span class="sxs-lookup"><span data-stu-id="40078-155">Modify permissions so MySQL can access (read and write) the data disk</span></span>
<span data-ttu-id="40078-156">Use the following command to modify permissions:</span><span class="sxs-lookup"><span data-stu-id="40078-156">Use the following command to modify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-the-disk-io-scheduling-algorithm"></a><span data-ttu-id="40078-157">Adjust the disk I/O scheduling algorithm</span><span class="sxs-lookup"><span data-stu-id="40078-157">Adjust the disk I/O scheduling algorithm</span></span>
<span data-ttu-id="40078-158">Linux implements four types of I/O scheduling algorithms:</span><span class="sxs-lookup"><span data-stu-id="40078-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="40078-159">NOOP algorithm (No Operation)</span><span class="sxs-lookup"><span data-stu-id="40078-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="40078-160">Deadline algorithm (Deadline)</span><span class="sxs-lookup"><span data-stu-id="40078-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="40078-161">Completely fair queuing algorithm (CFQ)</span><span class="sxs-lookup"><span data-stu-id="40078-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="40078-162">Budget period algorithm (Anticipatory)</span><span class="sxs-lookup"><span data-stu-id="40078-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="40078-163">You can select different I/O schedulers under different scenarios to optimize performance.</span><span class="sxs-lookup"><span data-stu-id="40078-163">You can select different I/O schedulers under different scenarios to optimize performance.</span></span> <span data-ttu-id="40078-164">In a completely random access environment, there is not a significant difference between the CFQ and Deadline algorithms for performance.</span><span class="sxs-lookup"><span data-stu-id="40078-164">In a completely random access environment, there is not a significant difference between the CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="40078-165">We recommend that you set the MySQL database environment to Deadline for stability.</span><span class="sxs-lookup"><span data-stu-id="40078-165">We recommend that you set the MySQL database environment to Deadline for stability.</span></span> <span data-ttu-id="40078-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span><span class="sxs-lookup"><span data-stu-id="40078-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="40078-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than the default scheduler.</span><span class="sxs-lookup"><span data-stu-id="40078-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than the default scheduler.</span></span>   

<span data-ttu-id="40078-168">Prior to the kernel 2.5, the default I/O scheduling algorithm is Deadline.</span><span class="sxs-lookup"><span data-stu-id="40078-168">Prior to the kernel 2.5, the default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="40078-169">Starting with the kernel 2.6.18, CFQ became the default I/O scheduling algorithm.</span><span class="sxs-lookup"><span data-stu-id="40078-169">Starting with the kernel 2.6.18, CFQ became the default I/O scheduling algorithm.</span></span>  <span data-ttu-id="40078-170">You can specify this setting at kernel boot time or dynamically modify this setting when the system is running.</span><span class="sxs-lookup"><span data-stu-id="40078-170">You can specify this setting at kernel boot time or dynamically modify this setting when the system is running.</span></span>  

<span data-ttu-id="40078-171">The following example demonstrates how to check and set the default scheduler to the NOOP algorithm in the Debian distribution family.</span><span class="sxs-lookup"><span data-stu-id="40078-171">The following example demonstrates how to check and set the default scheduler to the NOOP algorithm in the Debian distribution family.</span></span>  

### <a name="view-the-current-io-scheduler"></a><span data-ttu-id="40078-172">View the current I/O scheduler</span><span class="sxs-lookup"><span data-stu-id="40078-172">View the current I/O scheduler</span></span>
<span data-ttu-id="40078-173">To view the scheduler run the following command:</span><span class="sxs-lookup"><span data-stu-id="40078-173">To view the scheduler run the following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="40078-174">You will see following output, which indicates the current scheduler:</span><span class="sxs-lookup"><span data-stu-id="40078-174">You will see following output, which indicates the current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-the-current-device-devsda-of-the-io-scheduling-algorithm"></a><span data-ttu-id="40078-175">Change the current device (/dev/sda) of the I/O scheduling algorithm</span><span class="sxs-lookup"><span data-stu-id="40078-175">Change the current device (/dev/sda) of the I/O scheduling algorithm</span></span>
<span data-ttu-id="40078-176">Run the following commands to change the current device:</span><span class="sxs-lookup"><span data-stu-id="40078-176">Run the following commands to change the current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="40078-177">Setting this for /dev/sda alone is not useful.</span><span class="sxs-lookup"><span data-stu-id="40078-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="40078-178">It must be set on all data disks where the database resides.</span><span class="sxs-lookup"><span data-stu-id="40078-178">It must be set on all data disks where the database resides.</span></span>  
>
>

<span data-ttu-id="40078-179">You should see the following output, indicating that grub.cfg has been rebuilt successfully and that the default scheduler has been updated to NOOP:</span><span class="sxs-lookup"><span data-stu-id="40078-179">You should see the following output, indicating that grub.cfg has been rebuilt successfully and that the default scheduler has been updated to NOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="40078-180">For the Red Hat distribution family, you need only the following command:</span><span class="sxs-lookup"><span data-stu-id="40078-180">For the Red Hat distribution family, you need only the following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="40078-181">Configure system file operations settings</span><span class="sxs-lookup"><span data-stu-id="40078-181">Configure system file operations settings</span></span>
<span data-ttu-id="40078-182">One best practice is to disable the *atime* logging feature on the file system.</span><span class="sxs-lookup"><span data-stu-id="40078-182">One best practice is to disable the *atime* logging feature on the file system.</span></span> <span data-ttu-id="40078-183">Atime is the last file access time.</span><span class="sxs-lookup"><span data-stu-id="40078-183">Atime is the last file access time.</span></span> <span data-ttu-id="40078-184">Whenever a file is accessed, the file system records the timestamp in the log.</span><span class="sxs-lookup"><span data-stu-id="40078-184">Whenever a file is accessed, the file system records the timestamp in the log.</span></span> <span data-ttu-id="40078-185">However, this information is rarely used.</span><span class="sxs-lookup"><span data-stu-id="40078-185">However, this information is rarely used.</span></span> <span data-ttu-id="40078-186">You can disable it if you don't need it, which will reduce overall disk access time.</span><span class="sxs-lookup"><span data-stu-id="40078-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="40078-187">To disable atime logging, you need to modify the file system configuration file /etc/ fstab and add the **noatime** option.</span><span class="sxs-lookup"><span data-stu-id="40078-187">To disable atime logging, you need to modify the file system configuration file /etc/ fstab and add the **noatime** option.</span></span>  

<span data-ttu-id="40078-188">For example, edit the vim /etc/fstab file, adding the noatime as shown in the following sample:</span><span class="sxs-lookup"><span data-stu-id="40078-188">For example, edit the vim /etc/fstab file, adding the noatime as shown in the following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by the Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add the “noatime” option below to disable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="40078-189">Then, remount the file system with the following command:</span><span class="sxs-lookup"><span data-stu-id="40078-189">Then, remount the file system with the following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="40078-190">Test the modified result.</span><span class="sxs-lookup"><span data-stu-id="40078-190">Test the modified result.</span></span> <span data-ttu-id="40078-191">When you modify the test file, the access time is not updated.</span><span class="sxs-lookup"><span data-stu-id="40078-191">When you modify the test file, the access time is not updated.</span></span> <span data-ttu-id="40078-192">The following examples show what the code looks like before and after modification.</span><span class="sxs-lookup"><span data-stu-id="40078-192">The following examples show what the code looks like before and after modification.</span></span>

<span data-ttu-id="40078-193">Before:</span><span class="sxs-lookup"><span data-stu-id="40078-193">Before:</span></span>        

![Code before access modification][5]

<span data-ttu-id="40078-195">After:</span><span class="sxs-lookup"><span data-stu-id="40078-195">After:</span></span>

![Code after access modification][6]

## <a name="increase-the-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="40078-197">Increase the maximum number of system handles for high concurrency</span><span class="sxs-lookup"><span data-stu-id="40078-197">Increase the maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="40078-198">MySQL is a high concurrency database.</span><span class="sxs-lookup"><span data-stu-id="40078-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="40078-199">The default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span><span class="sxs-lookup"><span data-stu-id="40078-199">The default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="40078-200">Use the following steps to increase the maximum concurrent handles of the system to support high concurrency of MySQL.</span><span class="sxs-lookup"><span data-stu-id="40078-200">Use the following steps to increase the maximum concurrent handles of the system to support high concurrency of MySQL.</span></span>

### <a name="modify-the-limitsconf-file"></a><span data-ttu-id="40078-201">Modify the limits.conf file</span><span class="sxs-lookup"><span data-stu-id="40078-201">Modify the limits.conf file</span></span>
<span data-ttu-id="40078-202">To increase the maximum allowed concurrent handles, add the following four lines in the /etc/security/limits.conf file.</span><span class="sxs-lookup"><span data-stu-id="40078-202">To increase the maximum allowed concurrent handles, add the following four lines in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="40078-203">Note that 65536 is the maximum number that the system can support.</span><span class="sxs-lookup"><span data-stu-id="40078-203">Note that 65536 is the maximum number that the system can support.</span></span>   

    * <span data-ttu-id="40078-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="40078-204">soft nofile 65536</span></span>
    * <span data-ttu-id="40078-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="40078-205">hard nofile 65536</span></span>
    * <span data-ttu-id="40078-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="40078-206">soft nproc 65536</span></span>
    * <span data-ttu-id="40078-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="40078-207">hard nproc 65536</span></span>

### <a name="update-the-system-for-the-new-limits"></a><span data-ttu-id="40078-208">Update the system for the new limits</span><span class="sxs-lookup"><span data-stu-id="40078-208">Update the system for the new limits</span></span>
<span data-ttu-id="40078-209">To update the system, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="40078-209">To update the system, run the following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-the-limits-are-updated-at-boot-time"></a><span data-ttu-id="40078-210">Ensure that the limits are updated at boot time</span><span class="sxs-lookup"><span data-stu-id="40078-210">Ensure that the limits are updated at boot time</span></span>
<span data-ttu-id="40078-211">Put the following startup commands in the /etc/rc.local file so it will take effect at boot time.</span><span class="sxs-lookup"><span data-stu-id="40078-211">Put the following startup commands in the /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="40078-212">MySQL database optimization</span><span class="sxs-lookup"><span data-stu-id="40078-212">MySQL database optimization</span></span>
<span data-ttu-id="40078-213">To configure MySQL on Azure, you can use the same performance-tuning strategy you use on an on-premises machine.</span><span class="sxs-lookup"><span data-stu-id="40078-213">To configure MySQL on Azure, you can use the same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="40078-214">The main I/O optimization rules are:</span><span class="sxs-lookup"><span data-stu-id="40078-214">The main I/O optimization rules are:</span></span>   

* <span data-ttu-id="40078-215">Increase the cache size.</span><span class="sxs-lookup"><span data-stu-id="40078-215">Increase the cache size.</span></span>
* <span data-ttu-id="40078-216">Reduce I/O response time.</span><span class="sxs-lookup"><span data-stu-id="40078-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="40078-217">To optimize MySQL server settings, you can update the my.cnf file, which is the default configuration file for both server and client computers.</span><span class="sxs-lookup"><span data-stu-id="40078-217">To optimize MySQL server settings, you can update the my.cnf file, which is the default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="40078-218">The following configuration items are the main factors that affect MySQL performance:</span><span class="sxs-lookup"><span data-stu-id="40078-218">The following configuration items are the main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="40078-219">**innodb_buffer_pool_size**: The buffer pool contains buffered data and the index.</span><span class="sxs-lookup"><span data-stu-id="40078-219">**innodb_buffer_pool_size**: The buffer pool contains buffered data and the index.</span></span> <span data-ttu-id="40078-220">This is usually set to 70 percent of physical memory.</span><span class="sxs-lookup"><span data-stu-id="40078-220">This is usually set to 70 percent of physical memory.</span></span>
* <span data-ttu-id="40078-221">**innodb_log_file_size**: This is the redo log size.</span><span class="sxs-lookup"><span data-stu-id="40078-221">**innodb_log_file_size**: This is the redo log size.</span></span> <span data-ttu-id="40078-222">You use redo logs to ensure that write operations are fast, reliable, and recoverable after a crash.</span><span class="sxs-lookup"><span data-stu-id="40078-222">You use redo logs to ensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="40078-223">This is set to 512 MB, which will give you plenty of space for logging write operations.</span><span class="sxs-lookup"><span data-stu-id="40078-223">This is set to 512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="40078-224">**max_connections**: Sometimes applications do not close connections properly.</span><span class="sxs-lookup"><span data-stu-id="40078-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="40078-225">A larger value will give the server more time to recycle idled connections.</span><span class="sxs-lookup"><span data-stu-id="40078-225">A larger value will give the server more time to recycle idled connections.</span></span> <span data-ttu-id="40078-226">The maximum number of connections is 10,000, but the recommended maximum is 5,000.</span><span class="sxs-lookup"><span data-stu-id="40078-226">The maximum number of connections is 10,000, but the recommended maximum is 5,000.</span></span>
* <span data-ttu-id="40078-227">**Innodb_file_per_table**: This setting enables or disables the ability of InnoDB to store tables in separate files.</span><span class="sxs-lookup"><span data-stu-id="40078-227">**Innodb_file_per_table**: This setting enables or disables the ability of InnoDB to store tables in separate files.</span></span> <span data-ttu-id="40078-228">Turn on the option to ensure that several advanced administration operations can be applied efficiently.</span><span class="sxs-lookup"><span data-stu-id="40078-228">Turn on the option to ensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="40078-229">From a performance point of view, it can speed up the table space transmission and optimize the debris management performance.</span><span class="sxs-lookup"><span data-stu-id="40078-229">From a performance point of view, it can speed up the table space transmission and optimize the debris management performance.</span></span> <span data-ttu-id="40078-230">The recommended setting for this option is ON.</span><span class="sxs-lookup"><span data-stu-id="40078-230">The recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="40078-231">From MySQL 5.6, the default setting is ON, so no action is required.</span><span class="sxs-lookup"><span data-stu-id="40078-231">From MySQL 5.6, the default setting is ON, so no action is required.</span></span> <span data-ttu-id="40078-232">For earlier versions, the default setting is OFF.</span><span class="sxs-lookup"><span data-stu-id="40078-232">For earlier versions, the default setting is OFF.</span></span> <span data-ttu-id="40078-233">The setting should be changed before data is loaded, because only newly created tables are affected.</span><span class="sxs-lookup"><span data-stu-id="40078-233">The setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="40078-234">**innodb_flush_log_at_trx_commit**: The default value is 1, with the scope set to 0~2.</span><span class="sxs-lookup"><span data-stu-id="40078-234">**innodb_flush_log_at_trx_commit**: The default value is 1, with the scope set to 0~2.</span></span> <span data-ttu-id="40078-235">The default value is the most suitable option for standalone MySQL DB.</span><span class="sxs-lookup"><span data-stu-id="40078-235">The default value is the most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="40078-236">The setting of 2 enables the most data integrity and is suitable for Master in MySQL Cluster.</span><span class="sxs-lookup"><span data-stu-id="40078-236">The setting of 2 enables the most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="40078-237">The setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span><span class="sxs-lookup"><span data-stu-id="40078-237">The setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="40078-238">**Innodb_log_buffer_size**: The log buffer allows transactions to run without having to flush the log to disk before the transactions commit.</span><span class="sxs-lookup"><span data-stu-id="40078-238">**Innodb_log_buffer_size**: The log buffer allows transactions to run without having to flush the log to disk before the transactions commit.</span></span> <span data-ttu-id="40078-239">However, if there is large binary object or text field, the cache will be consumed quickly and frequent disk I/O will be triggered.</span><span class="sxs-lookup"><span data-stu-id="40078-239">However, if there is large binary object or text field, the cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="40078-240">It is better increase the buffer size if Innodb_log_waits state variable is not 0.</span><span class="sxs-lookup"><span data-stu-id="40078-240">It is better increase the buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="40078-241">**query_cache_size**: The best option is to disable it from the outset.</span><span class="sxs-lookup"><span data-stu-id="40078-241">**query_cache_size**: The best option is to disable it from the outset.</span></span> <span data-ttu-id="40078-242">Set query_cache_size to 0 (this is the default setting in MySQL 5.6) and use other methods to speed up queries.</span><span class="sxs-lookup"><span data-stu-id="40078-242">Set query_cache_size to 0 (this is the default setting in MySQL 5.6) and use other methods to speed up queries.</span></span>  

<span data-ttu-id="40078-243">See [Appendix D](#AppendixD) for a comparison of performance before and after the optimization.</span><span class="sxs-lookup"><span data-stu-id="40078-243">See [Appendix D](#AppendixD) for a comparison of performance before and after the optimization.</span></span>

## <a name="turn-on-the-mysql-slow-query-log-for-analyzing-the-performance-bottleneck"></a><span data-ttu-id="40078-244">Turn on the MySQL slow query log for analyzing the performance bottleneck</span><span class="sxs-lookup"><span data-stu-id="40078-244">Turn on the MySQL slow query log for analyzing the performance bottleneck</span></span>
<span data-ttu-id="40078-245">The MySQL slow query log can help you identify the slow queries for MySQL.</span><span class="sxs-lookup"><span data-stu-id="40078-245">The MySQL slow query log can help you identify the slow queries for MySQL.</span></span> <span data-ttu-id="40078-246">After enabling the MySQL slow query log, you can use MySQL tools like **mysqldumpslow** to identify the performance bottleneck.</span><span class="sxs-lookup"><span data-stu-id="40078-246">After enabling the MySQL slow query log, you can use MySQL tools like **mysqldumpslow** to identify the performance bottleneck.</span></span>  

<span data-ttu-id="40078-247">By default, this is not enabled.</span><span class="sxs-lookup"><span data-stu-id="40078-247">By default, this is not enabled.</span></span> <span data-ttu-id="40078-248">Turning on the slow query log might consume some CPU resources.</span><span class="sxs-lookup"><span data-stu-id="40078-248">Turning on the slow query log might consume some CPU resources.</span></span> <span data-ttu-id="40078-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span><span class="sxs-lookup"><span data-stu-id="40078-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="40078-250">To turn on the slow query log:</span><span class="sxs-lookup"><span data-stu-id="40078-250">To turn on the slow query log:</span></span>

1. <span data-ttu-id="40078-251">Modify the my.cnf file by adding the following lines to the end:</span><span class="sxs-lookup"><span data-stu-id="40078-251">Modify the my.cnf file by adding the following lines to the end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="40078-252">Restart the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="40078-252">Restart the MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="40078-253">Check whether the setting is taking effect by using the **show** command.</span><span class="sxs-lookup"><span data-stu-id="40078-253">Check whether the setting is taking effect by using the **show** command.</span></span>

![Slow-query-log ON][7]   

![Slow-query-log results][8]

<span data-ttu-id="40078-256">In this example, you can see that the slow query feature has been turned on.</span><span class="sxs-lookup"><span data-stu-id="40078-256">In this example, you can see that the slow query feature has been turned on.</span></span> <span data-ttu-id="40078-257">You can then use the **mysqldumpslow** tool to determine performance bottlenecks and optimize performance, such as adding indexes.</span><span class="sxs-lookup"><span data-stu-id="40078-257">You can then use the **mysqldumpslow** tool to determine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="40078-258">Appendices</span><span class="sxs-lookup"><span data-stu-id="40078-258">Appendices</span></span>
<span data-ttu-id="40078-259">The following are sample performance test data produced in a targeted lab environment.</span><span class="sxs-lookup"><span data-stu-id="40078-259">The following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="40078-260">They provide general background on the performance data trend with different performance tuning approaches.</span><span class="sxs-lookup"><span data-stu-id="40078-260">They provide general background on the performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="40078-261">The results might vary under different environment or product versions.</span><span class="sxs-lookup"><span data-stu-id="40078-261">The results might vary under different environment or product versions.</span></span>

### <a name="AppendixA"></a><span data-ttu-id="40078-262">Appendix A</span><span class="sxs-lookup"><span data-stu-id="40078-262">Appendix A</span></span>  
<span data-ttu-id="40078-263">**Disk performance (IOPS) with different RAID levels**</span><span class="sxs-lookup"><span data-stu-id="40078-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![Disk IOPS with different RAID levels][9]

<span data-ttu-id="40078-265">**Test commands**</span><span class="sxs-lookup"><span data-stu-id="40078-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="40078-266">The workload of this test uses 64 threads, trying to reach the upper limit of RAID.</span><span class="sxs-lookup"><span data-stu-id="40078-266">The workload of this test uses 64 threads, trying to reach the upper limit of RAID.</span></span>
>
>

### <a name="AppendixB"></a><span data-ttu-id="40078-267">Appendix B</span><span class="sxs-lookup"><span data-stu-id="40078-267">Appendix B</span></span>  
<span data-ttu-id="40078-268">**MySQL performance (throughput) comparison with different RAID levels** </span><span class="sxs-lookup"><span data-stu-id="40078-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="40078-269">(XFS file system)</span><span class="sxs-lookup"><span data-stu-id="40078-269">(XFS file system)</span></span>

![MySQL performance comparison with different RAID levels][10]  
![MySQL performance comparison with different RAID levels][11]

<span data-ttu-id="40078-272">**Test commands**</span><span class="sxs-lookup"><span data-stu-id="40078-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="40078-273">**MySQL performance (OLTP) comparison with different RAID levels**</span><span class="sxs-lookup"><span data-stu-id="40078-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="40078-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span><span class="sxs-lookup"><span data-stu-id="40078-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="40078-275">**Test commands**</span><span class="sxs-lookup"><span data-stu-id="40078-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a><span data-ttu-id="40078-276">Appendix C</span><span class="sxs-lookup"><span data-stu-id="40078-276">Appendix C</span></span>   
<span data-ttu-id="40078-277">**Disk performance (IOPS) comparison for different chunk sizes**</span><span class="sxs-lookup"><span data-stu-id="40078-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="40078-278">(XFS file system)</span><span class="sxs-lookup"><span data-stu-id="40078-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="40078-279">**Test commands**</span><span class="sxs-lookup"><span data-stu-id="40078-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="40078-280">The file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span><span class="sxs-lookup"><span data-stu-id="40078-280">The file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <a name="AppendixD"></a><span data-ttu-id="40078-281">Appendix D</span><span class="sxs-lookup"><span data-stu-id="40078-281">Appendix D</span></span>  
<span data-ttu-id="40078-282">**MySQL performance (throughput) comparison before and after optimization**</span><span class="sxs-lookup"><span data-stu-id="40078-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="40078-283">(XFS File System)</span><span class="sxs-lookup"><span data-stu-id="40078-283">(XFS File System)</span></span>

![MySQL performance (throughput) comparison before and after optimization][14]

<span data-ttu-id="40078-285">**Test commands**</span><span class="sxs-lookup"><span data-stu-id="40078-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="40078-286">**The configuration setting for default and optimization is as follows:**</span><span class="sxs-lookup"><span data-stu-id="40078-286">**The configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="40078-287">Parameters</span><span class="sxs-lookup"><span data-stu-id="40078-287">Parameters</span></span> | <span data-ttu-id="40078-288">Default</span><span class="sxs-lookup"><span data-stu-id="40078-288">Default</span></span> | <span data-ttu-id="40078-289">Optimization</span><span class="sxs-lookup"><span data-stu-id="40078-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40078-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="40078-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="40078-291">None</span><span class="sxs-lookup"><span data-stu-id="40078-291">None</span></span> |<span data-ttu-id="40078-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="40078-292">7 GB</span></span> |
| <span data-ttu-id="40078-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="40078-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="40078-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="40078-294">5 MB</span></span> |<span data-ttu-id="40078-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="40078-295">512 MB</span></span> |
| <span data-ttu-id="40078-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="40078-296">**max_connections**</span></span> |<span data-ttu-id="40078-297">100</span><span class="sxs-lookup"><span data-stu-id="40078-297">100</span></span> |<span data-ttu-id="40078-298">5000</span><span class="sxs-lookup"><span data-stu-id="40078-298">5000</span></span> |
| <span data-ttu-id="40078-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="40078-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="40078-300">0</span><span class="sxs-lookup"><span data-stu-id="40078-300">0</span></span> |<span data-ttu-id="40078-301">1</span><span class="sxs-lookup"><span data-stu-id="40078-301">1</span></span> |
| <span data-ttu-id="40078-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="40078-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="40078-303">1</span><span class="sxs-lookup"><span data-stu-id="40078-303">1</span></span> |<span data-ttu-id="40078-304">2</span><span class="sxs-lookup"><span data-stu-id="40078-304">2</span></span> |
| <span data-ttu-id="40078-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="40078-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="40078-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="40078-306">8 MB</span></span> |<span data-ttu-id="40078-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="40078-307">128 MB</span></span> |
| <span data-ttu-id="40078-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="40078-308">**query_cache_size**</span></span> |<span data-ttu-id="40078-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="40078-309">16 MB</span></span> |<span data-ttu-id="40078-310">0</span><span class="sxs-lookup"><span data-stu-id="40078-310">0</span></span> |

<span data-ttu-id="40078-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer to the [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="40078-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer to the [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="40078-312">**Test environment**</span><span class="sxs-lookup"><span data-stu-id="40078-312">**Test environment**</span></span>  

| <span data-ttu-id="40078-313">Hardware</span><span class="sxs-lookup"><span data-stu-id="40078-313">Hardware</span></span> | <span data-ttu-id="40078-314">Details</span><span class="sxs-lookup"><span data-stu-id="40078-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="40078-315">CPU</span><span class="sxs-lookup"><span data-stu-id="40078-315">CPU</span></span> |<span data-ttu-id="40078-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span><span class="sxs-lookup"><span data-stu-id="40078-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="40078-317">Memory</span><span class="sxs-lookup"><span data-stu-id="40078-317">Memory</span></span> |<span data-ttu-id="40078-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="40078-318">14 GB</span></span> |
| <span data-ttu-id="40078-319">Disk</span><span class="sxs-lookup"><span data-stu-id="40078-319">Disk</span></span> |<span data-ttu-id="40078-320">10 GB/disk</span><span class="sxs-lookup"><span data-stu-id="40078-320">10 GB/disk</span></span> |
| <span data-ttu-id="40078-321">OS</span><span class="sxs-lookup"><span data-stu-id="40078-321">OS</span></span> |<span data-ttu-id="40078-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="40078-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

