---
title: Use Modern Backup Storage with Azure Backup Server v2
description: Learn about the new features in Azure Backup Server v2. This article describes how to upgrade your Backup Server installation.
services: backup
author: markgalioto
manager: carmonm
ms.service: backup
ms.topic: conceptual
ms.date: 05/15/2017
ms.author: markgal
ms.openlocfilehash: 7c583ea048ed1837c662869c62039165aaa3c024
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866926"
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="431e9-104">Add storage to Azure Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="431e9-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="431e9-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="431e9-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="431e9-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span><span class="sxs-lookup"><span data-stu-id="431e9-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="431e9-107">It also offers workload-aware storage.</span><span class="sxs-lookup"><span data-stu-id="431e9-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="431e9-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="431e9-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="431e9-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="431e9-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="431e9-110">Instead, it protects workloads as it does with Backup Server v1.</span><span class="sxs-lookup"><span data-stu-id="431e9-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="431e9-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="431e9-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="431e9-112">Volumes in Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="431e9-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="431e9-113">Backup Server v2 accepts storage volumes.</span><span class="sxs-lookup"><span data-stu-id="431e9-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="431e9-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span><span class="sxs-lookup"><span data-stu-id="431e9-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="431e9-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span><span class="sxs-lookup"><span data-stu-id="431e9-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="431e9-116">Set up Backup Server v2 on a VM.</span><span class="sxs-lookup"><span data-stu-id="431e9-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="431e9-117">Create a volume on a virtual disk in a storage pool:</span><span class="sxs-lookup"><span data-stu-id="431e9-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="431e9-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span><span class="sxs-lookup"><span data-stu-id="431e9-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="431e9-119">Add any additional disks, and extend the virtual disk.</span><span class="sxs-lookup"><span data-stu-id="431e9-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="431e9-120">Create volumes on the virtual disk.</span><span class="sxs-lookup"><span data-stu-id="431e9-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="431e9-121">Add the volumes to Backup Server.</span><span class="sxs-lookup"><span data-stu-id="431e9-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="431e9-122">Configure workload-aware storage.</span><span class="sxs-lookup"><span data-stu-id="431e9-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="431e9-123">Create a volume for Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="431e9-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="431e9-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span><span class="sxs-lookup"><span data-stu-id="431e9-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="431e9-125">A volume can be a single disk.</span><span class="sxs-lookup"><span data-stu-id="431e9-125">A volume can be a single disk.</span></span> <span data-ttu-id="431e9-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span><span class="sxs-lookup"><span data-stu-id="431e9-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="431e9-127">This can help if you want to expand the volume for backup storage.</span><span class="sxs-lookup"><span data-stu-id="431e9-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="431e9-128">This section offers best practices for creating a volume with this setup.</span><span class="sxs-lookup"><span data-stu-id="431e9-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="431e9-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span><span class="sxs-lookup"><span data-stu-id="431e9-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="431e9-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span><span class="sxs-lookup"><span data-stu-id="431e9-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Create a new storage pool](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="431e9-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span><span class="sxs-lookup"><span data-stu-id="431e9-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Add a virtual disk](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="431e9-134">Select the storage pool, and then select **Add Physical Disk**.</span><span class="sxs-lookup"><span data-stu-id="431e9-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![Add a physical disk](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="431e9-136">Select the physical disk, and then select **Extend Virtual Disk**.</span><span class="sxs-lookup"><span data-stu-id="431e9-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Extend the virtual disk](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="431e9-138">Select the virtual disk, and then select **New Volume**.</span><span class="sxs-lookup"><span data-stu-id="431e9-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![Create a new volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="431e9-140">In the **Select the server and disk** dialog, select the server and the new disk.</span><span class="sxs-lookup"><span data-stu-id="431e9-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="431e9-141">Then, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="431e9-141">Then, select **Next**.</span></span>

    ![Select the server and disk](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="431e9-143">Add volumes to Backup Server disk storage</span><span class="sxs-lookup"><span data-stu-id="431e9-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="431e9-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="431e9-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="431e9-145">A list of all the volumes available to be added for Backup Server Storage appears.</span><span class="sxs-lookup"><span data-stu-id="431e9-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="431e9-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span><span class="sxs-lookup"><span data-stu-id="431e9-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="431e9-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="431e9-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![Add Available Volumes](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="431e9-149">Set up workload-aware storage</span><span class="sxs-lookup"><span data-stu-id="431e9-149">Set up workload-aware storage</span></span>

<span data-ttu-id="431e9-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span><span class="sxs-lookup"><span data-stu-id="431e9-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="431e9-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span><span class="sxs-lookup"><span data-stu-id="431e9-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="431e9-152">An example is SQL Server with transaction logs.</span><span class="sxs-lookup"><span data-stu-id="431e9-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="431e9-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span><span class="sxs-lookup"><span data-stu-id="431e9-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="431e9-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="431e9-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="431e9-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span><span class="sxs-lookup"><span data-stu-id="431e9-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="431e9-156">Syntax:</span><span class="sxs-lookup"><span data-stu-id="431e9-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="431e9-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="431e9-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![The Update-DPMDiskStorage command in the PowerShell window](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="431e9-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span><span class="sxs-lookup"><span data-stu-id="431e9-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![Disks and volumes in the Administrator Console](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="431e9-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="431e9-161">Next steps</span></span>
<span data-ttu-id="431e9-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span><span class="sxs-lookup"><span data-stu-id="431e9-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="431e9-163">Prepare Backup Server workloads</span><span class="sxs-lookup"><span data-stu-id="431e9-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="431e9-164">Use Backup Server to back up a VMware server</span><span class="sxs-lookup"><span data-stu-id="431e9-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="431e9-165">Use Backup Server to back up SQL Server</span><span class="sxs-lookup"><span data-stu-id="431e9-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

