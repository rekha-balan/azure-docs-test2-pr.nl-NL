---
title: 'Azure Backup: Recover files and folders from an Azure VM backup | Microsoft Docs'
description: Recover files from an Azure virtual machine recovery point
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: item level recovery; file recovery from Azure VM backup; restore files from Azure VM
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 2/6/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: c4859683d550054763c93589658f9f12e80d3b4c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555520"
---
# <a name="recover-files-from-azure-virtual-machine-backup-preview"></a><span data-ttu-id="110de-104">Recover files from Azure virtual machine backup (Preview)</span><span class="sxs-lookup"><span data-stu-id="110de-104">Recover files from Azure virtual machine backup (Preview)</span></span>

<span data-ttu-id="110de-105">Azure backup provides the capability to restore [Azure VMs and disks](./backup-azure-arm-restore-vms.md) from Azure VM backups.</span><span class="sxs-lookup"><span data-stu-id="110de-105">Azure backup provides the capability to restore [Azure VMs and disks](./backup-azure-arm-restore-vms.md) from Azure VM backups.</span></span> <span data-ttu-id="110de-106">Now this article explains how you can recover items such as files and folders from an Azure VM backup.</span><span class="sxs-lookup"><span data-stu-id="110de-106">Now this article explains how you can recover items such as files and folders from an Azure VM backup.</span></span>

> [!Note]
> <span data-ttu-id="110de-107">This feature is available for Azure VMs deployed using the Resource Manager model and protected to a Recovery services vault.</span><span class="sxs-lookup"><span data-stu-id="110de-107">This feature is available for Azure VMs deployed using the Resource Manager model and protected to a Recovery services vault.</span></span>
> <span data-ttu-id="110de-108">File recovery from an encrypted VM backup is not supported.</span><span class="sxs-lookup"><span data-stu-id="110de-108">File recovery from an encrypted VM backup is not supported.</span></span>
>

## <a name="mount-the-volume-and-copy-files"></a><span data-ttu-id="110de-109">Mount the volume and copy files</span><span class="sxs-lookup"><span data-stu-id="110de-109">Mount the volume and copy files</span></span>

1. <span data-ttu-id="110de-110">Sign into the [Azure portal](http://portal.Azure.com).</span><span class="sxs-lookup"><span data-stu-id="110de-110">Sign into the [Azure portal](http://portal.Azure.com).</span></span> <span data-ttu-id="110de-111">Find the relevant Recovery services vault and the required backup item.</span><span class="sxs-lookup"><span data-stu-id="110de-111">Find the relevant Recovery services vault and the required backup item.</span></span>

2. <span data-ttu-id="110de-112">On the Backup Item blade, click **File Recovery (Preview)**</span><span class="sxs-lookup"><span data-stu-id="110de-112">On the Backup Item blade, click **File Recovery (Preview)**</span></span>

    ![Open Recovery Services vault backup item](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-files-from-vm/open-vault-item.png)

    <span data-ttu-id="110de-114">The **File Recovery** blade opens.</span><span class="sxs-lookup"><span data-stu-id="110de-114">The **File Recovery** blade opens.</span></span>

    ![File recovery blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. <span data-ttu-id="110de-116">From the **Select recovery point** drop-down menu, select the recovery point that contains the files you want.</span><span class="sxs-lookup"><span data-stu-id="110de-116">From the **Select recovery point** drop-down menu, select the recovery point that contains the files you want.</span></span> <span data-ttu-id="110de-117">By default, the latest recovery point is already selected.</span><span class="sxs-lookup"><span data-stu-id="110de-117">By default, the latest recovery point is already selected.</span></span>

4. <span data-ttu-id="110de-118">Click **Download Executable** (for Windows Azure VM) or **Download Script** (for Linux Azure VM) to download the software that you'll use to copy files from the recovery point.</span><span class="sxs-lookup"><span data-stu-id="110de-118">Click **Download Executable** (for Windows Azure VM) or **Download Script** (for Linux Azure VM) to download the software that you'll use to copy files from the recovery point.</span></span>

  <span data-ttu-id="110de-119">The executable/script creates a connection between the local computer and the specified recovery point.</span><span class="sxs-lookup"><span data-stu-id="110de-119">The executable/script creates a connection between the local computer and the specified recovery point.</span></span>

5. <span data-ttu-id="110de-120">On the computer where you want to recover the files, run the executable/script.</span><span class="sxs-lookup"><span data-stu-id="110de-120">On the computer where you want to recover the files, run the executable/script.</span></span> <span data-ttu-id="110de-121">You must run it with Administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="110de-121">You must run it with Administrator credentials.</span></span> <span data-ttu-id="110de-122">If you run the script on a computer with restricted access, ensure there is access to:</span><span class="sxs-lookup"><span data-stu-id="110de-122">If you run the script on a computer with restricted access, ensure there is access to:</span></span>

    - <span data-ttu-id="110de-123">go.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="110de-123">go.microsoft.com</span></span>
    - <span data-ttu-id="110de-124">Azure endpoints used for Azure VM backups</span><span class="sxs-lookup"><span data-stu-id="110de-124">Azure endpoints used for Azure VM backups</span></span>
    - <span data-ttu-id="110de-125">outbound port 3260</span><span class="sxs-lookup"><span data-stu-id="110de-125">outbound port 3260</span></span>

   <span data-ttu-id="110de-126">For Linux, the script requires 'open-iscsi' and 'lshw' components to connect to the recovery point.</span><span class="sxs-lookup"><span data-stu-id="110de-126">For Linux, the script requires 'open-iscsi' and 'lshw' components to connect to the recovery point.</span></span> <span data-ttu-id="110de-127">If those do not exist on the machine where it is run, it asks for permission to install the relevant components and installs them upon consent.</span><span class="sxs-lookup"><span data-stu-id="110de-127">If those do not exist on the machine where it is run, it asks for permission to install the relevant components and installs them upon consent.</span></span>
      
    ![File recovery blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   <span data-ttu-id="110de-129">You can run the script on any machine that has the same (or compatible) operating system as the backed-up VM.</span><span class="sxs-lookup"><span data-stu-id="110de-129">You can run the script on any machine that has the same (or compatible) operating system as the backed-up VM.</span></span> <span data-ttu-id="110de-130">See the [Compatible OS table](backup-azure-restore-files-from-vm.md#compatible-os) for compatible operating systems.</span><span class="sxs-lookup"><span data-stu-id="110de-130">See the [Compatible OS table](backup-azure-restore-files-from-vm.md#compatible-os) for compatible operating systems.</span></span> <span data-ttu-id="110de-131">If the protected Azure virtual machine uses Windows Storage Spaces (for Windows Azure VMs) or LVM/RAID Arrays(for Linux VMs), then you can't run the executable/script on the same virtual machine.</span><span class="sxs-lookup"><span data-stu-id="110de-131">If the protected Azure virtual machine uses Windows Storage Spaces (for Windows Azure VMs) or LVM/RAID Arrays(for Linux VMs), then you can't run the executable/script on the same virtual machine.</span></span> <span data-ttu-id="110de-132">Instead, run it on any other machine with a compatible operating system.</span><span class="sxs-lookup"><span data-stu-id="110de-132">Instead, run it on any other machine with a compatible operating system.</span></span>

### <a name="compatible-os"></a><span data-ttu-id="110de-133">Compatible OS</span><span class="sxs-lookup"><span data-stu-id="110de-133">Compatible OS</span></span>

#### <a name="for-windows"></a><span data-ttu-id="110de-134">For Windows</span><span class="sxs-lookup"><span data-stu-id="110de-134">For Windows</span></span>

<span data-ttu-id="110de-135">The following table shows the compatibility between server and computer operating systems.</span><span class="sxs-lookup"><span data-stu-id="110de-135">The following table shows the compatibility between server and computer operating systems.</span></span> <span data-ttu-id="110de-136">When recovering files, you can't restore files between incompatible operating systems.</span><span class="sxs-lookup"><span data-stu-id="110de-136">When recovering files, you can't restore files between incompatible operating systems.</span></span>

|<span data-ttu-id="110de-137">Server OS</span><span class="sxs-lookup"><span data-stu-id="110de-137">Server OS</span></span> | <span data-ttu-id="110de-138">Compatible client OS</span><span class="sxs-lookup"><span data-stu-id="110de-138">Compatible client OS</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="110de-139">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="110de-139">Windows Server 2012 R2</span></span> | <span data-ttu-id="110de-140">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="110de-140">Windows 8.1</span></span> |
| <span data-ttu-id="110de-141">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="110de-141">Windows Server 2012</span></span>    | <span data-ttu-id="110de-142">Windows 8</span><span class="sxs-lookup"><span data-stu-id="110de-142">Windows 8</span></span>  |
| <span data-ttu-id="110de-143">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="110de-143">Windows Server 2008 R2</span></span> | <span data-ttu-id="110de-144">Windows 7</span><span class="sxs-lookup"><span data-stu-id="110de-144">Windows 7</span></span>   |

#### <a name="for-linux"></a><span data-ttu-id="110de-145">For Linux</span><span class="sxs-lookup"><span data-stu-id="110de-145">For Linux</span></span>

<span data-ttu-id="110de-146">In Linux, the fundamental requirement is that the OS of the machine where the script is run should support the filesystem of the files present in the backed-up Linux VM.</span><span class="sxs-lookup"><span data-stu-id="110de-146">In Linux, the fundamental requirement is that the OS of the machine where the script is run should support the filesystem of the files present in the backed-up Linux VM.</span></span> <span data-ttu-id="110de-147">While selecting a machine to run the script, please ensure it has the compatible OS and the versions as mentioned in the table below.</span><span class="sxs-lookup"><span data-stu-id="110de-147">While selecting a machine to run the script, please ensure it has the compatible OS and the versions as mentioned in the table below.</span></span>

|<span data-ttu-id="110de-148">Linux OS</span><span class="sxs-lookup"><span data-stu-id="110de-148">Linux OS</span></span> | <span data-ttu-id="110de-149">Versions</span><span class="sxs-lookup"><span data-stu-id="110de-149">Versions</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="110de-150">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="110de-150">Ubuntu</span></span> | <span data-ttu-id="110de-151">12.04 and above</span><span class="sxs-lookup"><span data-stu-id="110de-151">12.04 and above</span></span> |
| <span data-ttu-id="110de-152">CentOS</span><span class="sxs-lookup"><span data-stu-id="110de-152">CentOS</span></span> | <span data-ttu-id="110de-153">6.5 and above</span><span class="sxs-lookup"><span data-stu-id="110de-153">6.5 and above</span></span>  |
| <span data-ttu-id="110de-154">RHEL</span><span class="sxs-lookup"><span data-stu-id="110de-154">RHEL</span></span> | <span data-ttu-id="110de-155">6.7 and above</span><span class="sxs-lookup"><span data-stu-id="110de-155">6.7 and above</span></span> |
| <span data-ttu-id="110de-156">Debian</span><span class="sxs-lookup"><span data-stu-id="110de-156">Debian</span></span> | <span data-ttu-id="110de-157">7 and above</span><span class="sxs-lookup"><span data-stu-id="110de-157">7 and above</span></span> |
| <span data-ttu-id="110de-158">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="110de-158">Oracle Linux</span></span> | <span data-ttu-id="110de-159">6.4 and above</span><span class="sxs-lookup"><span data-stu-id="110de-159">6.4 and above</span></span> |

<span data-ttu-id="110de-160">The script also requires python and bash components to execute and connect securely to the recovery point.</span><span class="sxs-lookup"><span data-stu-id="110de-160">The script also requires python and bash components to execute and connect securely to the recovery point.</span></span>

|<span data-ttu-id="110de-161">Component</span><span class="sxs-lookup"><span data-stu-id="110de-161">Component</span></span> | <span data-ttu-id="110de-162">Version</span><span class="sxs-lookup"><span data-stu-id="110de-162">Version</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="110de-163">bash</span><span class="sxs-lookup"><span data-stu-id="110de-163">bash</span></span> | <span data-ttu-id="110de-164">4 and above</span><span class="sxs-lookup"><span data-stu-id="110de-164">4 and above</span></span> |
| <span data-ttu-id="110de-165">python</span><span class="sxs-lookup"><span data-stu-id="110de-165">python</span></span> | <span data-ttu-id="110de-166">2.6.6 and above</span><span class="sxs-lookup"><span data-stu-id="110de-166">2.6.6 and above</span></span>  |


### <a name="identifying-volumes"></a><span data-ttu-id="110de-167">Identifying Volumes</span><span class="sxs-lookup"><span data-stu-id="110de-167">Identifying Volumes</span></span>

#### <a name="for-windows"></a><span data-ttu-id="110de-168">For Windows</span><span class="sxs-lookup"><span data-stu-id="110de-168">For Windows</span></span>

<span data-ttu-id="110de-169">When you run the exectuable, the operating system mounts the new volumes and assigns drive letters.</span><span class="sxs-lookup"><span data-stu-id="110de-169">When you run the exectuable, the operating system mounts the new volumes and assigns drive letters.</span></span> <span data-ttu-id="110de-170">You can use Windows Explorer or File Explorer to browse those drives.</span><span class="sxs-lookup"><span data-stu-id="110de-170">You can use Windows Explorer or File Explorer to browse those drives.</span></span> <span data-ttu-id="110de-171">The drive letters assigned to the volumes may not be the same letters as the original virtual machine, however, the volume name is preserved.</span><span class="sxs-lookup"><span data-stu-id="110de-171">The drive letters assigned to the volumes may not be the same letters as the original virtual machine, however, the volume name is preserved.</span></span> <span data-ttu-id="110de-172">For example, if the volume on the original virtual machine was “Data Disk (E:\)”, that volume can be attached as “Data Disk ('Any drive letter available':\) on the local computer.</span><span class="sxs-lookup"><span data-stu-id="110de-172">For example, if the volume on the original virtual machine was “Data Disk (E:\)”, that volume can be attached as “Data Disk ('Any drive letter available':\) on the local computer.</span></span> <span data-ttu-id="110de-173">Browse through all volumes mentioned in the script output until you find your files/folder.</span><span class="sxs-lookup"><span data-stu-id="110de-173">Browse through all volumes mentioned in the script output until you find your files/folder.</span></span>  
       
   ![File recovery blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a><span data-ttu-id="110de-175">For Linux</span><span class="sxs-lookup"><span data-stu-id="110de-175">For Linux</span></span>

<span data-ttu-id="110de-176">In Linux, the volumes of the recovery point are mounted to the folder where the script is run.</span><span class="sxs-lookup"><span data-stu-id="110de-176">In Linux, the volumes of the recovery point are mounted to the folder where the script is run.</span></span> <span data-ttu-id="110de-177">The attached disks, volumes and the corresponding mount paths are shown accordingly.</span><span class="sxs-lookup"><span data-stu-id="110de-177">The attached disks, volumes and the corresponding mount paths are shown accordingly.</span></span> <span data-ttu-id="110de-178">These mount paths are visible to users having root level access.</span><span class="sxs-lookup"><span data-stu-id="110de-178">These mount paths are visible to users having root level access.</span></span> <span data-ttu-id="110de-179">Browse through the volumes mentioned in the script output.</span><span class="sxs-lookup"><span data-stu-id="110de-179">Browse through the volumes mentioned in the script output.</span></span>

  ![Linux File recovery blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-the-connection"></a><span data-ttu-id="110de-181">Closing the connection</span><span class="sxs-lookup"><span data-stu-id="110de-181">Closing the connection</span></span>

<span data-ttu-id="110de-182">After identifying the files and copying them to a local storage location, remove (or unmount) the additional drives.</span><span class="sxs-lookup"><span data-stu-id="110de-182">After identifying the files and copying them to a local storage location, remove (or unmount) the additional drives.</span></span> <span data-ttu-id="110de-183">To unmount the drives, on the **File Recovery** blade in the Azure portal, click **Unmount Disks**.</span><span class="sxs-lookup"><span data-stu-id="110de-183">To unmount the drives, on the **File Recovery** blade in the Azure portal, click **Unmount Disks**.</span></span>

![Unmount disks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-files-from-vm/unmount-disks3.png)

<span data-ttu-id="110de-185">Once the disks have been unmounted, you receive a message letting you know it was successful.</span><span class="sxs-lookup"><span data-stu-id="110de-185">Once the disks have been unmounted, you receive a message letting you know it was successful.</span></span> <span data-ttu-id="110de-186">It may take a few minutes for the connection to refresh so that you can remove the disks.</span><span class="sxs-lookup"><span data-stu-id="110de-186">It may take a few minutes for the connection to refresh so that you can remove the disks.</span></span>

<span data-ttu-id="110de-187">In Linux, after the connection to the recovery point is severed, the OS doesn't remove the corresponding mount paths automatically.</span><span class="sxs-lookup"><span data-stu-id="110de-187">In Linux, after the connection to the recovery point is severed, the OS doesn't remove the corresponding mount paths automatically.</span></span> <span data-ttu-id="110de-188">These exist as "orphan" volumes and they are visible but throw an error when you access/write the files.</span><span class="sxs-lookup"><span data-stu-id="110de-188">These exist as "orphan" volumes and they are visible but throw an error when you access/write the files.</span></span> <span data-ttu-id="110de-189">They can be manually removed.</span><span class="sxs-lookup"><span data-stu-id="110de-189">They can be manually removed.</span></span> <span data-ttu-id="110de-190">The script, when run, identifies any such volumes existing from any previous recovery points and cleans them up upon consent.</span><span class="sxs-lookup"><span data-stu-id="110de-190">The script, when run, identifies any such volumes existing from any previous recovery points and cleans them up upon consent.</span></span>

## <a name="special-configurations"></a><span data-ttu-id="110de-191">Special configurations</span><span class="sxs-lookup"><span data-stu-id="110de-191">Special configurations</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="110de-192">Windows Storage Spaces</span><span class="sxs-lookup"><span data-stu-id="110de-192">Windows Storage Spaces</span></span>

<span data-ttu-id="110de-193">Windows Storage Spaces is a technology in Windows storage that enables you to virtualize storage.</span><span class="sxs-lookup"><span data-stu-id="110de-193">Windows Storage Spaces is a technology in Windows storage that enables you to virtualize storage.</span></span> <span data-ttu-id="110de-194">With Windows Storage Spaces you can group industry-standard disks into storage pools, and then create virtual disks, called storage spaces, from the available space in those storage pools.</span><span class="sxs-lookup"><span data-stu-id="110de-194">With Windows Storage Spaces you can group industry-standard disks into storage pools, and then create virtual disks, called storage spaces, from the available space in those storage pools.</span></span>

<span data-ttu-id="110de-195">If the Azure VM that was backed up uses Windows Storage Spaces, then you can't run the executable script on the same VM.</span><span class="sxs-lookup"><span data-stu-id="110de-195">If the Azure VM that was backed up uses Windows Storage Spaces, then you can't run the executable script on the same VM.</span></span> <span data-ttu-id="110de-196">Instead, run the executable script on any other machine with a compatible operating system.</span><span class="sxs-lookup"><span data-stu-id="110de-196">Instead, run the executable script on any other machine with a compatible operating system.</span></span>

### <a name="lvmraid-arrays"></a><span data-ttu-id="110de-197">LVM/RAID Arrays</span><span class="sxs-lookup"><span data-stu-id="110de-197">LVM/RAID Arrays</span></span>

<span data-ttu-id="110de-198">In Linux, Logical volume manager (LVM) and/or software RAID Arrays are used to manage logical volumes over multiple disks.</span><span class="sxs-lookup"><span data-stu-id="110de-198">In Linux, Logical volume manager (LVM) and/or software RAID Arrays are used to manage logical volumes over multiple disks.</span></span> <span data-ttu-id="110de-199">If the backed up Linux VM uses LVM and/or RAID Arrays, you can't run the script on the same VM.</span><span class="sxs-lookup"><span data-stu-id="110de-199">If the backed up Linux VM uses LVM and/or RAID Arrays, you can't run the script on the same VM.</span></span> <span data-ttu-id="110de-200">Instead run the script on any other machine with compatible OS and which supports filesystem of the backed up VM.</span><span class="sxs-lookup"><span data-stu-id="110de-200">Instead run the script on any other machine with compatible OS and which supports filesystem of the backed up VM.</span></span>

<span data-ttu-id="110de-201">The script output displays the LVM and/or RAID Arrays disks and the volumes with the partition type as shown below</span><span class="sxs-lookup"><span data-stu-id="110de-201">The script output displays the LVM and/or RAID Arrays disks and the volumes with the partition type as shown below</span></span>

   ![Linux LVM Output blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
<span data-ttu-id="110de-203">The following commands need to be run by the user to bring these partitions online.</span><span class="sxs-lookup"><span data-stu-id="110de-203">The following commands need to be run by the user to bring these partitions online.</span></span> 

<span data-ttu-id="110de-204">**For LVM Partitions**</span><span class="sxs-lookup"><span data-stu-id="110de-204">**For LVM Partitions**</span></span>

```
$ pvs <volume name as shown above in the script output> 
```
<span data-ttu-id="110de-205">This lists the volume group names under a physical volume.</span><span class="sxs-lookup"><span data-stu-id="110de-205">This lists the volume group names under a physical volume.</span></span>

```
$ lvdisplay <volume-group-name from the pvs command’s results> 
```
<span data-ttu-id="110de-206">This lists all logical volumes, names and their paths in a volume group.</span><span class="sxs-lookup"><span data-stu-id="110de-206">This lists all logical volumes, names and their paths in a volume group.</span></span>

```
$ mount <LV path> </mountpath>
```
<span data-ttu-id="110de-207">To mount the logical volumes to the path of your choice.</span><span class="sxs-lookup"><span data-stu-id="110de-207">To mount the logical volumes to the path of your choice.</span></span>


<span data-ttu-id="110de-208">**For RAID Arrays**</span><span class="sxs-lookup"><span data-stu-id="110de-208">**For RAID Arrays**</span></span>

```
$ mdadm –detail –scan
```
<span data-ttu-id="110de-209">This displays details about all raid disks.</span><span class="sxs-lookup"><span data-stu-id="110de-209">This displays details about all raid disks.</span></span> <span data-ttu-id="110de-210">The relevant RAID disk will be displayed as `/dev/mdm/<RAID array name in the backed up VM>`</span><span class="sxs-lookup"><span data-stu-id="110de-210">The relevant RAID disk will be displayed as `/dev/mdm/<RAID array name in the backed up VM>`</span></span>

<span data-ttu-id="110de-211">Use the mount command if the RAID disk has physical volumes.</span><span class="sxs-lookup"><span data-stu-id="110de-211">Use the mount command if the RAID disk has physical volumes.</span></span>
```
$ mount [RAID Disk Path] [/mounthpath]
```

<span data-ttu-id="110de-212">If this RAID disk has another LVM configured in it then follow the same procedure as outlined above for LVM partitions with the volume name being the RAID Disk name</span><span class="sxs-lookup"><span data-stu-id="110de-212">If this RAID disk has another LVM configured in it then follow the same procedure as outlined above for LVM partitions with the volume name being the RAID Disk name</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="110de-213">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="110de-213">Troubleshooting</span></span>

<span data-ttu-id="110de-214">If you have problems while recovering files from the virtual machines, check the following table for additional information.</span><span class="sxs-lookup"><span data-stu-id="110de-214">If you have problems while recovering files from the virtual machines, check the following table for additional information.</span></span>

| <span data-ttu-id="110de-215">Error Message / Scenario</span><span class="sxs-lookup"><span data-stu-id="110de-215">Error Message / Scenario</span></span> | <span data-ttu-id="110de-216">Probable Cause</span><span class="sxs-lookup"><span data-stu-id="110de-216">Probable Cause</span></span> | <span data-ttu-id="110de-217">Recommended action</span><span class="sxs-lookup"><span data-stu-id="110de-217">Recommended action</span></span> |
| ------------------------ | -------------- | ------------------ |
| <span data-ttu-id="110de-218">Exe output: *Exception connecting to the target*</span><span class="sxs-lookup"><span data-stu-id="110de-218">Exe output: *Exception connecting to the target*</span></span> |<span data-ttu-id="110de-219">Script is not able to access the recovery point</span><span class="sxs-lookup"><span data-stu-id="110de-219">Script is not able to access the recovery point</span></span> | <span data-ttu-id="110de-220">Check whether the machine fulfills the access requirements mentioned above</span><span class="sxs-lookup"><span data-stu-id="110de-220">Check whether the machine fulfills the access requirements mentioned above</span></span>|  
|   <span data-ttu-id="110de-221">Exe output: *The target has already been logged in via an ISCSI session.*</span><span class="sxs-lookup"><span data-stu-id="110de-221">Exe output: *The target has already been logged in via an ISCSI session.*</span></span> | <span data-ttu-id="110de-222">The script was already executed on the same machine and the drives have been attached</span><span class="sxs-lookup"><span data-stu-id="110de-222">The script was already executed on the same machine and the drives have been attached</span></span> | <span data-ttu-id="110de-223">The volumes of the recovery point have already been attached.</span><span class="sxs-lookup"><span data-stu-id="110de-223">The volumes of the recovery point have already been attached.</span></span> <span data-ttu-id="110de-224">They may NOT be mounted with the same drive letters of the original VM.</span><span class="sxs-lookup"><span data-stu-id="110de-224">They may NOT be mounted with the same drive letters of the original VM.</span></span> <span data-ttu-id="110de-225">Browse through all the available volumes in the file explorer for your file</span><span class="sxs-lookup"><span data-stu-id="110de-225">Browse through all the available volumes in the file explorer for your file</span></span> |
| <span data-ttu-id="110de-226">Exe output: *This script is invalid because the disks have been dismounted via portal/exceeded the 12-hr limit. Please download a new script from the portal.*</span><span class="sxs-lookup"><span data-stu-id="110de-226">Exe output: *This script is invalid because the disks have been dismounted via portal/exceeded the 12-hr limit. Please download a new script from the portal.*</span></span> |  <span data-ttu-id="110de-227">The disks have been dismounted from the portal or the 12-hr limit exceeded</span><span class="sxs-lookup"><span data-stu-id="110de-227">The disks have been dismounted from the portal or the 12-hr limit exceeded</span></span> |    <span data-ttu-id="110de-228">This particular exe is now invalid and can’t be run.</span><span class="sxs-lookup"><span data-stu-id="110de-228">This particular exe is now invalid and can’t be run.</span></span> <span data-ttu-id="110de-229">If you want to access the files of that recovery point-in-time, visit the portal for a new exe</span><span class="sxs-lookup"><span data-stu-id="110de-229">If you want to access the files of that recovery point-in-time, visit the portal for a new exe</span></span>|
| <span data-ttu-id="110de-230">On the machine where the exe is run: The new volumes are not dismounted after the dismount button is clicked</span><span class="sxs-lookup"><span data-stu-id="110de-230">On the machine where the exe is run: The new volumes are not dismounted after the dismount button is clicked</span></span> |    <span data-ttu-id="110de-231">The ISCSI initiator on the machine is not responding/refreshing its connection to the target and maintaining the cache</span><span class="sxs-lookup"><span data-stu-id="110de-231">The ISCSI initiator on the machine is not responding/refreshing its connection to the target and maintaining the cache</span></span> |    <span data-ttu-id="110de-232">Wait for some mins after the dismount button is pressed.</span><span class="sxs-lookup"><span data-stu-id="110de-232">Wait for some mins after the dismount button is pressed.</span></span> <span data-ttu-id="110de-233">If the new volumes are still not dismounted, please browse through all the volumes.</span><span class="sxs-lookup"><span data-stu-id="110de-233">If the new volumes are still not dismounted, please browse through all the volumes.</span></span> <span data-ttu-id="110de-234">This forces the initiator to refresh the connection and the volume is dismounted with an error message that the disk is not available</span><span class="sxs-lookup"><span data-stu-id="110de-234">This forces the initiator to refresh the connection and the volume is dismounted with an error message that the disk is not available</span></span>|
| <span data-ttu-id="110de-235">Exe output: Script is run successfully but “New volumes attached” is not displayed on the script output</span><span class="sxs-lookup"><span data-stu-id="110de-235">Exe output: Script is run successfully but “New volumes attached” is not displayed on the script output</span></span> | <span data-ttu-id="110de-236">This is a transient error</span><span class="sxs-lookup"><span data-stu-id="110de-236">This is a transient error</span></span>   | <span data-ttu-id="110de-237">The volumes would have been already attached.</span><span class="sxs-lookup"><span data-stu-id="110de-237">The volumes would have been already attached.</span></span> <span data-ttu-id="110de-238">Open Explorer to browse.</span><span class="sxs-lookup"><span data-stu-id="110de-238">Open Explorer to browse.</span></span> <span data-ttu-id="110de-239">If you are using the same machine for running scripts every time, consider restarting the machine and the list should be displayed in the subsequent exe runs.</span><span class="sxs-lookup"><span data-stu-id="110de-239">If you are using the same machine for running scripts every time, consider restarting the machine and the list should be displayed in the subsequent exe runs.</span></span> |
| <span data-ttu-id="110de-240">Linux specific: Not able to view the desired volumes</span><span class="sxs-lookup"><span data-stu-id="110de-240">Linux specific: Not able to view the desired volumes</span></span> | <span data-ttu-id="110de-241">The OS of the machine where the script is run may not recognize the underlying filesystem of the backed up VM</span><span class="sxs-lookup"><span data-stu-id="110de-241">The OS of the machine where the script is run may not recognize the underlying filesystem of the backed up VM</span></span> | <span data-ttu-id="110de-242">Check whether the recovery point is crash consistent or file-consistent.</span><span class="sxs-lookup"><span data-stu-id="110de-242">Check whether the recovery point is crash consistent or file-consistent.</span></span> <span data-ttu-id="110de-243">If file consistent, run the script on another machine whose OS recognizes the backed up VM's filesystem</span><span class="sxs-lookup"><span data-stu-id="110de-243">If file consistent, run the script on another machine whose OS recognizes the backed up VM's filesystem</span></span> |







