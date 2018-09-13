---
title: Install Azure Backup Server v2
description: Azure Backup Server v2 gives you enhanced backup capabilities for protecting VMs, files and folders, workloads, and more. Learn how to install or upgrade to Azure Backup Server v2.
services: backup
author: markgalioto
manager: carmonm
ms.service: backup
ms.topic: conceptual
ms.date: 05/15/2017
ms.author: adigan
ms.openlocfilehash: a458a46f3775a593f369d5acb967fc90d61efde8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867392"
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="336bc-104">Install Azure Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="336bc-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="336bc-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span><span class="sxs-lookup"><span data-stu-id="336bc-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="336bc-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span><span class="sxs-lookup"><span data-stu-id="336bc-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="336bc-107">For a comparison of v1 and v2 features, see the [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="336bc-107">For a comparison of v1 and v2 features, see the [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="336bc-108">The additional features in Backup Server v2 are an upgrade from Backup Server v1.</span><span class="sxs-lookup"><span data-stu-id="336bc-108">The additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="336bc-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span><span class="sxs-lookup"><span data-stu-id="336bc-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="336bc-110">If you want to upgrade from Backup Server v1 to Backup Server v2, install Backup Server v2 on the Backup Server protection server.</span><span class="sxs-lookup"><span data-stu-id="336bc-110">If you want to upgrade from Backup Server v1 to Backup Server v2, install Backup Server v2 on the Backup Server protection server.</span></span> <span data-ttu-id="336bc-111">Your existing Backup Server settings remain intact.</span><span class="sxs-lookup"><span data-stu-id="336bc-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="336bc-112">You can install Backup Server v2 on Windows Server 2016 or Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="336bc-112">You can install Backup Server v2 on Windows Server 2016 or Windows Server 2012 R2.</span></span> <span data-ttu-id="336bc-113">To take advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="336bc-113">To take advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="336bc-114">Before you upgrade to or install Backup Server v2, read about the [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="336bc-114">Before you upgrade to or install Backup Server v2, read about the [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="336bc-115">Azure Backup Server has the same code base as System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="336bc-115">Azure Backup Server has the same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="336bc-116">Backup Server v1 is equivalent to Data Protection Manager 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="336bc-116">Backup Server v1 is equivalent to Data Protection Manager 2012 R2.</span></span> <span data-ttu-id="336bc-117">Backup Server v2 is equivalent to Data Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="336bc-117">Backup Server v2 is equivalent to Data Protection Manager 2016.</span></span> <span data-ttu-id="336bc-118">This article occasionally references the Data Protection Manager documentation.</span><span class="sxs-lookup"><span data-stu-id="336bc-118">This article occasionally references the Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-to-v2"></a><span data-ttu-id="336bc-119">Upgrade Backup Server to v2</span><span class="sxs-lookup"><span data-stu-id="336bc-119">Upgrade Backup Server to v2</span></span>
<span data-ttu-id="336bc-120">To upgrade from Backup Server v1 to Backup Server v2, make sure your installation has the required updates:</span><span class="sxs-lookup"><span data-stu-id="336bc-120">To upgrade from Backup Server v1 to Backup Server v2, make sure your installation has the required updates:</span></span>

- <span data-ttu-id="336bc-121">[Update the protection agents](backup-mabs-upgrade-to-v2.md#update-the-data-protection-manager-protection-agent) on the protected servers.</span><span class="sxs-lookup"><span data-stu-id="336bc-121">[Update the protection agents](backup-mabs-upgrade-to-v2.md#update-the-data-protection-manager-protection-agent) on the protected servers.</span></span>
- <span data-ttu-id="336bc-122">Upgrade Windows Server 2012 R2 to Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="336bc-122">Upgrade Windows Server 2012 R2 to Windows Server 2016.</span></span>
- <span data-ttu-id="336bc-123">Upgrade Azure Backup Server Remote Administrator on all production servers.</span><span class="sxs-lookup"><span data-stu-id="336bc-123">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="336bc-124">Ensure that backups are set to continue without restarting your production server.</span><span class="sxs-lookup"><span data-stu-id="336bc-124">Ensure that backups are set to continue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="336bc-125">Upgrade steps for Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="336bc-125">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="336bc-126">In the Download Center, [download the upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="336bc-126">In the Download Center, [download the upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="336bc-127">After you extract the setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="336bc-127">After you extract the setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Setup installer - Run Setup](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="336bc-129">In the Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span><span class="sxs-lookup"><span data-stu-id="336bc-129">In the Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Setup installer - Select Install](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="336bc-131">On the **Welcome** page, review the warnings, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="336bc-131">On the **Welcome** page, review the warnings, and then select **Next**.</span></span>

  ![Setup installer - Welcome page](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="336bc-133">The setup wizard performs prerequisite checks to make sure your environment can upgrade.</span><span class="sxs-lookup"><span data-stu-id="336bc-133">The setup wizard performs prerequisite checks to make sure your environment can upgrade.</span></span> <span data-ttu-id="336bc-134">On the **Prerequisite Checks** page, select **Check**.</span><span class="sxs-lookup"><span data-stu-id="336bc-134">On the **Prerequisite Checks** page, select **Check**.</span></span>

  ![Setup installer - Prerequisite Checks page](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="336bc-136">Your environment must pass the prerequisite checks.</span><span class="sxs-lookup"><span data-stu-id="336bc-136">Your environment must pass the prerequisite checks.</span></span> <span data-ttu-id="336bc-137">If your environment doesn't pass the checks, note the issues and fix them.</span><span class="sxs-lookup"><span data-stu-id="336bc-137">If your environment doesn't pass the checks, note the issues and fix them.</span></span> <span data-ttu-id="336bc-138">Then, select **Check Again**.</span><span class="sxs-lookup"><span data-stu-id="336bc-138">Then, select **Check Again**.</span></span> <span data-ttu-id="336bc-139">After you pass the prerequisite checks, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="336bc-139">After you pass the prerequisite checks, select **Next**.</span></span>

  ![Setup installer - Check Again button](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="336bc-141">On the **SQL Settings** page, select the relevant option for your SQL installation, and then select **Check and Install**.</span><span class="sxs-lookup"><span data-stu-id="336bc-141">On the **SQL Settings** page, select the relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Setup installer - SQL Settings page](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="336bc-143">The checks might take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="336bc-143">The checks might take a few minutes.</span></span> <span data-ttu-id="336bc-144">When the checks are finished, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="336bc-144">When the checks are finished, select **Next**.</span></span>

  ![Setup installer - SQL Settings Check and Install button](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and-fix-settings.png)

8. <span data-ttu-id="336bc-146">On the **Installation Settings** page, make any changes to the location where Backup Server is installed, or to the Scratch Location.</span><span class="sxs-lookup"><span data-stu-id="336bc-146">On the **Installation Settings** page, make any changes to the location where Backup Server is installed, or to the Scratch Location.</span></span> <span data-ttu-id="336bc-147">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="336bc-147">Select **Next**.</span></span>

  ![Setup installer - Installation Settings page](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="336bc-149">To finish the setup wizard, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="336bc-149">To finish the setup wizard, select **Finish**.</span></span>

  ![Setup installer - Finish](./media/backup-mabs-upgrade-to-v2/run-setup.png)

## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="336bc-151">Add storage for Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="336bc-151">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="336bc-152">To improve backup storage efficiency, Backup Server v2 adds support for volumes.</span><span class="sxs-lookup"><span data-stu-id="336bc-152">To improve backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="336bc-153">Backup Server v1 and Backup Server v2 both support disks.</span><span class="sxs-lookup"><span data-stu-id="336bc-153">Backup Server v1 and Backup Server v2 both support disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="336bc-154">Add volumes and disks</span><span class="sxs-lookup"><span data-stu-id="336bc-154">Add volumes and disks</span></span>

<span data-ttu-id="336bc-155">If you run Backup Server v2 on Windows Server 2016, you can use volumes to store backup data.</span><span class="sxs-lookup"><span data-stu-id="336bc-155">If you run Backup Server v2 on Windows Server 2016, you can use volumes to store backup data.</span></span> <span data-ttu-id="336bc-156">Volumes offer storage savings and faster backups.</span><span class="sxs-lookup"><span data-stu-id="336bc-156">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="336bc-157">Because volumes are new to Backup Server, you must add them.</span><span class="sxs-lookup"><span data-stu-id="336bc-157">Because volumes are new to Backup Server, you must add them.</span></span> 

<span data-ttu-id="336bc-158">When you add a volume to Backup Server, you can give the volume a friendly name.</span><span class="sxs-lookup"><span data-stu-id="336bc-158">When you add a volume to Backup Server, you can give the volume a friendly name.</span></span> <span data-ttu-id="336bc-159">Select the **Friendly Name** column of the volume you want to name.</span><span class="sxs-lookup"><span data-stu-id="336bc-159">Select the **Friendly Name** column of the volume you want to name.</span></span> <span data-ttu-id="336bc-160">You can change the name later, if necessary.</span><span class="sxs-lookup"><span data-stu-id="336bc-160">You can change the name later, if necessary.</span></span> <span data-ttu-id="336bc-161">You also can use PowerShell to add or change friendly names for volumes.</span><span class="sxs-lookup"><span data-stu-id="336bc-161">You also can use PowerShell to add or change friendly names for volumes.</span></span>

<span data-ttu-id="336bc-162">To add a volume in the Administrator Console:</span><span class="sxs-lookup"><span data-stu-id="336bc-162">To add a volume in the Administrator Console:</span></span>

1. <span data-ttu-id="336bc-163">In the Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="336bc-163">In the Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

  ![Open the Add Disk Storage wizard](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

  <span data-ttu-id="336bc-165">The Add Disk Storage wizard opens.</span><span class="sxs-lookup"><span data-stu-id="336bc-165">The Add Disk Storage wizard opens.</span></span>

2. <span data-ttu-id="336bc-166">On the **Add Disk Storage** page, in the **Available volumes** box, select a volume, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="336bc-166">On the **Add Disk Storage** page, in the **Available volumes** box, select a volume, and then select **Add**.</span></span>

3. <span data-ttu-id="336bc-167">In the **Selected volumes** box, enter a friendly name for the volume, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="336bc-167">In the **Selected volumes** box, enter a friendly name for the volume, and then select **OK**.</span></span>

  ![Add Disk Storage wizard - Add volume](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="336bc-169">If you want to add a disk, the disk must belong to a protection group that has legacy storage.</span><span class="sxs-lookup"><span data-stu-id="336bc-169">If you want to add a disk, the disk must belong to a protection group that has legacy storage.</span></span> <span data-ttu-id="336bc-170">You can use these disks only for these protection groups.</span><span class="sxs-lookup"><span data-stu-id="336bc-170">You can use these disks only for these protection groups.</span></span> <span data-ttu-id="336bc-171">If Backup Server doesn't have sources that have legacy protection, the disk isn't listed.</span><span class="sxs-lookup"><span data-stu-id="336bc-171">If Backup Server doesn't have sources that have legacy protection, the disk isn't listed.</span></span>

  <span data-ttu-id="336bc-172">For more information about adding disks, see [Add disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="336bc-172">For more information about adding disks, see [Add disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="336bc-173">You can't give a disk a friendly name.</span><span class="sxs-lookup"><span data-stu-id="336bc-173">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-to-volumes"></a><span data-ttu-id="336bc-174">Assign workloads to volumes</span><span class="sxs-lookup"><span data-stu-id="336bc-174">Assign workloads to volumes</span></span>

<span data-ttu-id="336bc-175">In Backup Server, you specify which workloads are assigned to which volumes.</span><span class="sxs-lookup"><span data-stu-id="336bc-175">In Backup Server, you specify which workloads are assigned to which volumes.</span></span> <span data-ttu-id="336bc-176">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only workloads that require frequent, high-volume backups.</span><span class="sxs-lookup"><span data-stu-id="336bc-176">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="336bc-177">An example is SQL Server with transaction logs.</span><span class="sxs-lookup"><span data-stu-id="336bc-177">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="336bc-178">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="336bc-178">Update-DPMDiskStorage</span></span>

<span data-ttu-id="336bc-179">To update the properties of a volume in the storage pool in Backup Server, use the PowerShell cmdlet **Update-DPMDiskStorage**.</span><span class="sxs-lookup"><span data-stu-id="336bc-179">To update the properties of a volume in the storage pool in Backup Server, use the PowerShell cmdlet **Update-DPMDiskStorage**.</span></span>

<span data-ttu-id="336bc-180">Syntax:</span><span class="sxs-lookup"><span data-stu-id="336bc-180">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="336bc-181">All changes that you make by using PowerShell are reflected in the UI.</span><span class="sxs-lookup"><span data-stu-id="336bc-181">All changes that you make by using PowerShell are reflected in the UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="336bc-182">Protect data sources</span><span class="sxs-lookup"><span data-stu-id="336bc-182">Protect data sources</span></span>
<span data-ttu-id="336bc-183">To begin protecting data sources, create a protection group.</span><span class="sxs-lookup"><span data-stu-id="336bc-183">To begin protecting data sources, create a protection group.</span></span> <span data-ttu-id="336bc-184">The following steps highlight changes or additions to the New Protection Group wizard.</span><span class="sxs-lookup"><span data-stu-id="336bc-184">The following steps highlight changes or additions to the New Protection Group wizard.</span></span>

<span data-ttu-id="336bc-185">To create a protection group:</span><span class="sxs-lookup"><span data-stu-id="336bc-185">To create a protection group:</span></span>

1. <span data-ttu-id="336bc-186">In the Backup Server Administrator Console, select **Protection**.</span><span class="sxs-lookup"><span data-stu-id="336bc-186">In the Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="336bc-187">On the tool ribbon, select **New**.</span><span class="sxs-lookup"><span data-stu-id="336bc-187">On the tool ribbon, select **New**.</span></span>

  <span data-ttu-id="336bc-188">The Create New Protection Group wizard opens.</span><span class="sxs-lookup"><span data-stu-id="336bc-188">The Create New Protection Group wizard opens.</span></span>

  ![Create New Protection Group wizard](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="336bc-190">On the **Welcome** page, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="336bc-190">On the **Welcome** page, select **Next**.</span></span>

4. <span data-ttu-id="336bc-191">On the **Select Protection Group Type** page, select the type of protection group you want to create, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="336bc-191">On the **Select Protection Group Type** page, select the type of protection group you want to create, and then select **Next**.</span></span>

  ![Select Protection Group Type page](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="336bc-193">On the **Select Group Members** page, in the **Available members** box, the members with protection agents are listed.</span><span class="sxs-lookup"><span data-stu-id="336bc-193">On the **Select Group Members** page, in the **Available members** box, the members with protection agents are listed.</span></span> <span data-ttu-id="336bc-194">For this example, select volume D:\ and E:\, and then add them to **Selected members**.</span><span class="sxs-lookup"><span data-stu-id="336bc-194">For this example, select volume D:\ and E:\, and then add them to **Selected members**.</span></span> <span data-ttu-id="336bc-195">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="336bc-195">Select **Next**.</span></span>

  ![Select Group Members page](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="336bc-197">On the **Select Data Protection Method** page, enter a **Protection group name**, select the protection method, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="336bc-197">On the **Select Data Protection Method** page, enter a **Protection group name**, select the protection method, and then select **Next**.</span></span> <span data-ttu-id="336bc-198">If you want short-term protection, select the **Disk** backup method.</span><span class="sxs-lookup"><span data-stu-id="336bc-198">If you want short-term protection, select the **Disk** backup method.</span></span>

  ![Select Data Protection Method page](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="336bc-200">On the **Specify Short-Term Goals** page, select the details for **Retention range** and **Synchronization frequency**.</span><span class="sxs-lookup"><span data-stu-id="336bc-200">On the **Specify Short-Term Goals** page, select the details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="336bc-201">Then, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="336bc-201">Then, select **Next**.</span></span> <span data-ttu-id="336bc-202">Optionally, to change the schedule for when recovery points are taken, select **Modify**.</span><span class="sxs-lookup"><span data-stu-id="336bc-202">Optionally, to change the schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Specify Short-Term Goals page](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="336bc-204">On the **Review Disk Storage Allocation** page, review details about the data sources you selected, including data source size, values for the space to be provisioned, and the target storage volume.</span><span class="sxs-lookup"><span data-stu-id="336bc-204">On the **Review Disk Storage Allocation** page, review details about the data sources you selected, including data source size, values for the space to be provisioned, and the target storage volume.</span></span>

  ![Review Disk Storage Allocation page](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="336bc-206">Storage volumes are based on the workload volume allocation (set by using PowerShell) and the available storage.</span><span class="sxs-lookup"><span data-stu-id="336bc-206">Storage volumes are based on the workload volume allocation (set by using PowerShell) and the available storage.</span></span> <span data-ttu-id="336bc-207">You can change the storage volumes by selecting other volumes in the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="336bc-207">You can change the storage volumes by selecting other volumes in the drop-down menu.</span></span> <span data-ttu-id="336bc-208">If you change the value for **Target Storage**, the value for **Available disk storage** dynamically changes to reflect values under **Free Space** and **Underprovisioned Space**.</span><span class="sxs-lookup"><span data-stu-id="336bc-208">If you change the value for **Target Storage**, the value for **Available disk storage** dynamically changes to reflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="336bc-209">If the data sources grow as planned, the value for the **Underprovisioned Space** column in **Available disk storage** reflects the amount of additional storage that's needed.</span><span class="sxs-lookup"><span data-stu-id="336bc-209">If the data sources grow as planned, the value for the **Underprovisioned Space** column in **Available disk storage** reflects the amount of additional storage that's needed.</span></span> <span data-ttu-id="336bc-210">Use this value to help plan your storage needs for smooth backups.</span><span class="sxs-lookup"><span data-stu-id="336bc-210">Use this value to help plan your storage needs for smooth backups.</span></span> <span data-ttu-id="336bc-211">If the value is zero, there are no potential problems with storage in the foreseeable future.</span><span class="sxs-lookup"><span data-stu-id="336bc-211">If the value is zero, there are no potential problems with storage in the foreseeable future.</span></span> <span data-ttu-id="336bc-212">If the value is a number other than zero, you don't have sufficient storage allocated (based on your protection policy and the data size of your protected members).</span><span class="sxs-lookup"><span data-stu-id="336bc-212">If the value is a number other than zero, you don't have sufficient storage allocated (based on your protection policy and the data size of your protected members).</span></span>

  ![Underallocated disk storage](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

  <span data-ttu-id="336bc-214">To finish creating your protection group, complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="336bc-214">To finish creating your protection group, complete the wizard.</span></span>

## <a name="migrate-legacy-storage-to-modern-backup-storage"></a><span data-ttu-id="336bc-215">Migrate legacy storage to Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="336bc-215">Migrate legacy storage to Modern Backup Storage</span></span>
<span data-ttu-id="336bc-216">After you upgrade to or install Backup Server v2 and then upgrade the operating system to Windows Server 2016, update your protection groups to use Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="336bc-216">After you upgrade to or install Backup Server v2 and then upgrade the operating system to Windows Server 2016, update your protection groups to use Modern Backup Storage.</span></span> <span data-ttu-id="336bc-217">By default, protection groups are not changed.</span><span class="sxs-lookup"><span data-stu-id="336bc-217">By default, protection groups are not changed.</span></span> <span data-ttu-id="336bc-218">They continue to function as they were initially set up.</span><span class="sxs-lookup"><span data-stu-id="336bc-218">They continue to function as they were initially set up.</span></span> 

<span data-ttu-id="336bc-219">Updating protection groups to use Modern Backup Storage is optional.</span><span class="sxs-lookup"><span data-stu-id="336bc-219">Updating protection groups to use Modern Backup Storage is optional.</span></span> <span data-ttu-id="336bc-220">To update the protection group, stop protection of all data sources by using the retain data option.</span><span class="sxs-lookup"><span data-stu-id="336bc-220">To update the protection group, stop protection of all data sources by using the retain data option.</span></span> <span data-ttu-id="336bc-221">Then, add the data sources to a new protection group.</span><span class="sxs-lookup"><span data-stu-id="336bc-221">Then, add the data sources to a new protection group.</span></span>

1. <span data-ttu-id="336bc-222">In the System Center 2016 DPM Administrator Console, select the **Protection** feature.</span><span class="sxs-lookup"><span data-stu-id="336bc-222">In the System Center 2016 DPM Administrator Console, select the **Protection** feature.</span></span> <span data-ttu-id="336bc-223">In the **Protection Group Member** list, right-click the member, and then select **Stop protection of member**.</span><span class="sxs-lookup"><span data-stu-id="336bc-223">In the **Protection Group Member** list, right-click the member, and then select **Stop protection of member**.</span></span>

  ![Stop protection of member](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="336bc-225">In the **Remove from Group** dialog box, review the used disk space and the available free space for the storage pool.</span><span class="sxs-lookup"><span data-stu-id="336bc-225">In the **Remove from Group** dialog box, review the used disk space and the available free space for the storage pool.</span></span> <span data-ttu-id="336bc-226">The default is to leave the recovery points on the disk and allow them to expire per their associated retention policy.</span><span class="sxs-lookup"><span data-stu-id="336bc-226">The default is to leave the recovery points on the disk and allow them to expire per their associated retention policy.</span></span> <span data-ttu-id="336bc-227">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="336bc-227">Select **OK**.</span></span>

  <span data-ttu-id="336bc-228">If you want to immediately return the used disk space to the free storage pool, select the **Delete replica on disk** check box to delete the backup data (and recovery points) associated with that member.</span><span class="sxs-lookup"><span data-stu-id="336bc-228">If you want to immediately return the used disk space to the free storage pool, select the **Delete replica on disk** check box to delete the backup data (and recovery points) associated with that member.</span></span>

  ![Remove from Group dialog box](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="336bc-230">Create a protection group that uses Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="336bc-230">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="336bc-231">Include the unprotected data sources.</span><span class="sxs-lookup"><span data-stu-id="336bc-231">Include the unprotected data sources.</span></span>


## <a name="add-disks-to-increase-legacy-storage"></a><span data-ttu-id="336bc-232">Add disks to increase legacy storage</span><span class="sxs-lookup"><span data-stu-id="336bc-232">Add disks to increase legacy storage</span></span>

<span data-ttu-id="336bc-233">If you want to use legacy storage with Backup Server, you might need to add disks to increase legacy storage.</span><span class="sxs-lookup"><span data-stu-id="336bc-233">If you want to use legacy storage with Backup Server, you might need to add disks to increase legacy storage.</span></span> 

<span data-ttu-id="336bc-234">To add disk storage:</span><span class="sxs-lookup"><span data-stu-id="336bc-234">To add disk storage:</span></span>

1. <span data-ttu-id="336bc-235">In the System Center 2016 DPM Administrator Console, select **Management** > **Disk Storage** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="336bc-235">In the System Center 2016 DPM Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

  ![Add Disk Storage dialog](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

2. <span data-ttu-id="336bc-237">In the **Add Disk Storage** dialog box, select **Add disks**.</span><span class="sxs-lookup"><span data-stu-id="336bc-237">In the **Add Disk Storage** dialog box, select **Add disks**.</span></span>

3. <span data-ttu-id="336bc-238">In the list of available disks, select the disks you want to add.</span><span class="sxs-lookup"><span data-stu-id="336bc-238">In the list of available disks, select the disks you want to add.</span></span> <span data-ttu-id="336bc-239">Select **Add**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="336bc-239">Select **Add**, and then select **OK**.</span></span>

## <a name="update-the-data-protection-manager-protection-agent"></a><span data-ttu-id="336bc-240">Update the Data Protection Manager protection agent</span><span class="sxs-lookup"><span data-stu-id="336bc-240">Update the Data Protection Manager protection agent</span></span>

<span data-ttu-id="336bc-241">Backup Server uses the System Center Data Protection Manager protection agent for updates.</span><span class="sxs-lookup"><span data-stu-id="336bc-241">Backup Server uses the System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="336bc-242">If you're upgrading a protection agent that isn't connected to the network, you can't use the Data Protection Manager Administrator Console to complete a connected agent upgrade.</span><span class="sxs-lookup"><span data-stu-id="336bc-242">If you're upgrading a protection agent that isn't connected to the network, you can't use the Data Protection Manager Administrator Console to complete a connected agent upgrade.</span></span> <span data-ttu-id="336bc-243">You must upgrade the protection agent in a nonactive domain environment.</span><span class="sxs-lookup"><span data-stu-id="336bc-243">You must upgrade the protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="336bc-244">Until the client computer is connected to the network, the Data Protection Manager Administrator Console shows that the protection agent update is pending.</span><span class="sxs-lookup"><span data-stu-id="336bc-244">Until the client computer is connected to the network, the Data Protection Manager Administrator Console shows that the protection agent update is pending.</span></span>

<span data-ttu-id="336bc-245">The following sections describe how to update protection agents for client computers that are connected, and for client computers that aren't connected.</span><span class="sxs-lookup"><span data-stu-id="336bc-245">The following sections describe how to update protection agents for client computers that are connected, and for client computers that aren't connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="336bc-246">Update a protection agent for a connected client computer</span><span class="sxs-lookup"><span data-stu-id="336bc-246">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="336bc-247">In the Backup Server Administrator Console, select **Management** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="336bc-247">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="336bc-248">In the display pane, select the client computers for which you want to update the protection agent.</span><span class="sxs-lookup"><span data-stu-id="336bc-248">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="336bc-249">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span><span class="sxs-lookup"><span data-stu-id="336bc-249">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="336bc-250">In the **Actions** pane, the **Update** action is available only when a protected computer is selected and updates are available.</span><span class="sxs-lookup"><span data-stu-id="336bc-250">In the **Actions** pane, the **Update** action is available only when a protected computer is selected and updates are available.</span></span>

3. <span data-ttu-id="336bc-251">To install updated protection agents on the selected computers, in the **Actions** pane, select **Update**.</span><span class="sxs-lookup"><span data-stu-id="336bc-251">To install updated protection agents on the selected computers, in the **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="336bc-252">Update a protection agent on a client computer that is not connected</span><span class="sxs-lookup"><span data-stu-id="336bc-252">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="336bc-253">In the Backup Server Administrator Console, select **Management** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="336bc-253">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="336bc-254">In the display pane, select the client computers for which you want to update the protection agent.</span><span class="sxs-lookup"><span data-stu-id="336bc-254">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="336bc-255">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span><span class="sxs-lookup"><span data-stu-id="336bc-255">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="336bc-256">In the **Actions** pane, the **Update** action isn't available when a protected computer is selected unless updates are available.</span><span class="sxs-lookup"><span data-stu-id="336bc-256">In the **Actions** pane, the **Update** action isn't available when a protected computer is selected unless updates are available.</span></span>

3. <span data-ttu-id="336bc-257">To install updated protection agents on the selected computers, select **Update**.</span><span class="sxs-lookup"><span data-stu-id="336bc-257">To install updated protection agents on the selected computers, select **Update**.</span></span>

4. <span data-ttu-id="336bc-258">For a client computer that isn't connected to the network, until the computer is connected to the network, the **Agent Status** column shows a status of **Update Pending**.</span><span class="sxs-lookup"><span data-stu-id="336bc-258">For a client computer that isn't connected to the network, until the computer is connected to the network, the **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="336bc-259">When a client computer is connected to the network, the **Agent Updates** column for the client computer shows a status of **Updating**.</span><span class="sxs-lookup"><span data-stu-id="336bc-259">When a client computer is connected to the network, the **Agent Updates** column for the client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-the-old-version-and-sync-the-new-version-with-azure"></a><span data-ttu-id="336bc-260">Move legacy protection groups from the old version and sync the new version with Azure</span><span class="sxs-lookup"><span data-stu-id="336bc-260">Move legacy protection groups from the old version and sync the new version with Azure</span></span>

<span data-ttu-id="336bc-261">When Azure Backup Server and the OS are both updated, you're ready to protect new data sources by using Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="336bc-261">When Azure Backup Server and the OS are both updated, you're ready to protect new data sources by using Modern Backup Storage.</span></span> <span data-ttu-id="336bc-262">Data sources that are already protected continue to be protected as they were in Azure Backup Server (legacy).</span><span class="sxs-lookup"><span data-stu-id="336bc-262">Data sources that are already protected continue to be protected as they were in Azure Backup Server (legacy).</span></span> <span data-ttu-id="336bc-263">All new protection groups use Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="336bc-263">All new protection groups use Modern Backup Storage.</span></span>

<span data-ttu-id="336bc-264">To migrate data sources from the legacy mode of protection to Modern Backup Storage:</span><span class="sxs-lookup"><span data-stu-id="336bc-264">To migrate data sources from the legacy mode of protection to Modern Backup Storage:</span></span>

1.  <span data-ttu-id="336bc-265">Add the new volume(s) to the Data Protection Manager storage pool.</span><span class="sxs-lookup"><span data-stu-id="336bc-265">Add the new volume(s) to the Data Protection Manager storage pool.</span></span> <span data-ttu-id="336bc-266">You can also assign a friendly name and select data source tags.</span><span class="sxs-lookup"><span data-stu-id="336bc-266">You can also assign a friendly name and select data source tags.</span></span>

2. <span data-ttu-id="336bc-267">For each data source that is in legacy mode, stop protection of the data sources.</span><span class="sxs-lookup"><span data-stu-id="336bc-267">For each data source that is in legacy mode, stop protection of the data sources.</span></span> <span data-ttu-id="336bc-268">Then, select **Retain Protected Data**.</span><span class="sxs-lookup"><span data-stu-id="336bc-268">Then, select **Retain Protected Data**.</span></span>  <span data-ttu-id="336bc-269">This allows recovery of old recovery points after migration.</span><span class="sxs-lookup"><span data-stu-id="336bc-269">This allows recovery of old recovery points after migration.</span></span>

3. <span data-ttu-id="336bc-270">Create a new protection group.</span><span class="sxs-lookup"><span data-stu-id="336bc-270">Create a new protection group.</span></span> <span data-ttu-id="336bc-271">Then, select the data sources that you want to store by using the new format.</span><span class="sxs-lookup"><span data-stu-id="336bc-271">Then, select the data sources that you want to store by using the new format.</span></span>

  <span data-ttu-id="336bc-272">Data Protection Manager stores a replica copy from the legacy backup storage in the Modern Backup Storage volume locally.</span><span class="sxs-lookup"><span data-stu-id="336bc-272">Data Protection Manager stores a replica copy from the legacy backup storage in the Modern Backup Storage volume locally.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="336bc-273">Creating the copy appears as a post-recovery operation job.</span><span class="sxs-lookup"><span data-stu-id="336bc-273">Creating the copy appears as a post-recovery operation job.</span></span>

  <span data-ttu-id="336bc-274">All new sync and recovery points are then stored in Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="336bc-274">All new sync and recovery points are then stored in Modern Backup Storage.</span></span>

  <span data-ttu-id="336bc-275">Old recovery points are pruned out as they expire.</span><span class="sxs-lookup"><span data-stu-id="336bc-275">Old recovery points are pruned out as they expire.</span></span> <span data-ttu-id="336bc-276">As old recovery points are deleted, disk space is freed up.</span><span class="sxs-lookup"><span data-stu-id="336bc-276">As old recovery points are deleted, disk space is freed up.</span></span>

  <span data-ttu-id="336bc-277">When all legacy volumes are deleted from the old storage, you can remove the disk from Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="336bc-277">When all legacy volumes are deleted from the old storage, you can remove the disk from Azure Backup.</span></span> <span data-ttu-id="336bc-278">You can then remove the disk from the system.</span><span class="sxs-lookup"><span data-stu-id="336bc-278">You can then remove the disk from the system.</span></span>

4. <span data-ttu-id="336bc-279">Make a backup of the Data Protection Manager database.</span><span class="sxs-lookup"><span data-stu-id="336bc-279">Make a backup of the Data Protection Manager database.</span></span>

  > [!IMPORTANT]
  > - <span data-ttu-id="336bc-280">The new server name must be the same name as the original Azure Backup Server instance.</span><span class="sxs-lookup"><span data-stu-id="336bc-280">The new server name must be the same name as the original Azure Backup Server instance.</span></span> <span data-ttu-id="336bc-281">You can't change the name of the new Azure Backup Server instance if you want to use the previous storage pool and Data Protection Manager database to retain recovery points.</span><span class="sxs-lookup"><span data-stu-id="336bc-281">You can't change the name of the new Azure Backup Server instance if you want to use the previous storage pool and Data Protection Manager database to retain recovery points.</span></span>
  > - <span data-ttu-id="336bc-282">You must have a backup of the Data Protection Manager database.</span><span class="sxs-lookup"><span data-stu-id="336bc-282">You must have a backup of the Data Protection Manager database.</span></span> <span data-ttu-id="336bc-283">You'll need to restore the database.</span><span class="sxs-lookup"><span data-stu-id="336bc-283">You'll need to restore the database.</span></span>

5. <span data-ttu-id="336bc-284">Shut down the original Azure Backup Server instance, or take the server offline.</span><span class="sxs-lookup"><span data-stu-id="336bc-284">Shut down the original Azure Backup Server instance, or take the server offline.</span></span>

6. <span data-ttu-id="336bc-285">Reset the machine account in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="336bc-285">Reset the machine account in Active Directory.</span></span>

7. <span data-ttu-id="336bc-286">Install Windows Server 2016 on a new machine.</span><span class="sxs-lookup"><span data-stu-id="336bc-286">Install Windows Server 2016 on a new machine.</span></span> <span data-ttu-id="336bc-287">For the server name, use the same machine name as the original Azure Backup Server instance.</span><span class="sxs-lookup"><span data-stu-id="336bc-287">For the server name, use the same machine name as the original Azure Backup Server instance.</span></span>

8. <span data-ttu-id="336bc-288">Join the domain.</span><span class="sxs-lookup"><span data-stu-id="336bc-288">Join the domain.</span></span>

9. <span data-ttu-id="336bc-289">Install Azure Backup Server v2.</span><span class="sxs-lookup"><span data-stu-id="336bc-289">Install Azure Backup Server v2.</span></span> <span data-ttu-id="336bc-290">(Remove the Data Protection Manager storage pool disks from the old server, and import them to the new server.)</span><span class="sxs-lookup"><span data-stu-id="336bc-290">(Remove the Data Protection Manager storage pool disks from the old server, and import them to the new server.)</span></span>

10. <span data-ttu-id="336bc-291">Restore the Data Protection Manager database you created in step 4.</span><span class="sxs-lookup"><span data-stu-id="336bc-291">Restore the Data Protection Manager database you created in step 4.</span></span>

11. <span data-ttu-id="336bc-292">Attach the storage from the original backup server to the new server.</span><span class="sxs-lookup"><span data-stu-id="336bc-292">Attach the storage from the original backup server to the new server.</span></span>

12. <span data-ttu-id="336bc-293">In SQL Server, restore the Data Protection Manager database.</span><span class="sxs-lookup"><span data-stu-id="336bc-293">In SQL Server, restore the Data Protection Manager database.</span></span>

13. <span data-ttu-id="336bc-294">At the administrator command line on the new server, use `cd` to go to the Microsoft Azure Backup installation location and bin folder.</span><span class="sxs-lookup"><span data-stu-id="336bc-294">At the administrator command line on the new server, use `cd` to go to the Microsoft Azure Backup installation location and bin folder.</span></span>  

  <span data-ttu-id="336bc-295">Example:</span><span class="sxs-lookup"><span data-stu-id="336bc-295">Example:</span></span>  
  <span data-ttu-id="336bc-296">C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\ to Azure Backup</span><span class="sxs-lookup"><span data-stu-id="336bc-296">C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\ to Azure Backup</span></span>

14. <span data-ttu-id="336bc-297">Run `DPMSYNC -SYNC`.</span><span class="sxs-lookup"><span data-stu-id="336bc-297">Run `DPMSYNC -SYNC`.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="336bc-298">If you added *new* disks to the Data Protection Manager storage pool instead of moving the old ones, run `DPMSYNC -Reallocatereplica`.</span><span class="sxs-lookup"><span data-stu-id="336bc-298">If you added *new* disks to the Data Protection Manager storage pool instead of moving the old ones, run `DPMSYNC -Reallocatereplica`.</span></span>

## <a name="new-powershell-cmdlets-in-backup-server-v2"></a><span data-ttu-id="336bc-299">New PowerShell cmdlets in Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="336bc-299">New PowerShell cmdlets in Backup Server v2</span></span>

<span data-ttu-id="336bc-300">When you install Azure Backup Server v2, two new cmdlets are available:</span><span class="sxs-lookup"><span data-stu-id="336bc-300">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="336bc-301">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="336bc-301">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="336bc-302">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="336bc-302">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="336bc-303">Next steps</span><span class="sxs-lookup"><span data-stu-id="336bc-303">Next steps</span></span>

<span data-ttu-id="336bc-304">Learn how to prepare your server or begin protecting a workload:</span><span class="sxs-lookup"><span data-stu-id="336bc-304">Learn how to prepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="336bc-305">Prepare Backup Server workloads</span><span class="sxs-lookup"><span data-stu-id="336bc-305">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="336bc-306">Use Backup Server to back up a VMware server</span><span class="sxs-lookup"><span data-stu-id="336bc-306">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="336bc-307">Use Backup Server to back up SQL Server</span><span class="sxs-lookup"><span data-stu-id="336bc-307">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="336bc-308">Use Modern Backup Storage with Backup Server</span><span class="sxs-lookup"><span data-stu-id="336bc-308">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

