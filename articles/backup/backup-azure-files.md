---
title: Back up Azure File Shares
description: This article details how to back up and restore your Azure file shares, and explains management tasks.
services: backup
author: markgalioto
ms.author: markgal
ms.date: 3/23/2018
ms.topic: tutorial
ms.service: backup
manager: carmonm
ms.openlocfilehash: d21a235602c425cef77b26d8c60f1e3562411095
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865281"
---
# <a name="back-up-azure-file-shares"></a><span data-ttu-id="443fc-103">Back up Azure file shares</span><span class="sxs-lookup"><span data-stu-id="443fc-103">Back up Azure file shares</span></span>
<span data-ttu-id="443fc-104">This article explains how to use the Azure portal to back up and restore [Azure file shares](../storage/files/storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="443fc-104">This article explains how to use the Azure portal to back up and restore [Azure file shares](../storage/files/storage-files-introduction.md).</span></span>

<span data-ttu-id="443fc-105">In this guide, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="443fc-105">In this guide, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="443fc-106">Configure a Recovery Services vault to back up Azure Files</span><span class="sxs-lookup"><span data-stu-id="443fc-106">Configure a Recovery Services vault to back up Azure Files</span></span>
> * <span data-ttu-id="443fc-107">Run an on-demand backup job to create a restore point</span><span class="sxs-lookup"><span data-stu-id="443fc-107">Run an on-demand backup job to create a restore point</span></span>
> * <span data-ttu-id="443fc-108">Restore a file or files from a restore point</span><span class="sxs-lookup"><span data-stu-id="443fc-108">Restore a file or files from a restore point</span></span>
> * <span data-ttu-id="443fc-109">Manage Backup jobs</span><span class="sxs-lookup"><span data-stu-id="443fc-109">Manage Backup jobs</span></span>
> * <span data-ttu-id="443fc-110">Stop protection on Azure Files</span><span class="sxs-lookup"><span data-stu-id="443fc-110">Stop protection on Azure Files</span></span>
> * <span data-ttu-id="443fc-111">Delete your backup data</span><span class="sxs-lookup"><span data-stu-id="443fc-111">Delete your backup data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="443fc-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="443fc-112">Prerequisites</span></span>
<span data-ttu-id="443fc-113">Before you can back up an Azure file share, ensure that it's present in one of the [supported Storage Account types](backup-azure-files.md#limitations-for-azure-file-share-backup-during-preview).</span><span class="sxs-lookup"><span data-stu-id="443fc-113">Before you can back up an Azure file share, ensure that it's present in one of the [supported Storage Account types](backup-azure-files.md#limitations-for-azure-file-share-backup-during-preview).</span></span> <span data-ttu-id="443fc-114">Once you have verified this, you can protect your file shares.</span><span class="sxs-lookup"><span data-stu-id="443fc-114">Once you have verified this, you can protect your file shares.</span></span>

## <a name="limitations-for-azure-file-share-backup-during-preview"></a><span data-ttu-id="443fc-115">Limitations for Azure file share backup during Preview</span><span class="sxs-lookup"><span data-stu-id="443fc-115">Limitations for Azure file share backup during Preview</span></span>
<span data-ttu-id="443fc-116">Backup for Azure File shares is in Preview.</span><span class="sxs-lookup"><span data-stu-id="443fc-116">Backup for Azure File shares is in Preview.</span></span> <span data-ttu-id="443fc-117">The following backup scenarios aren't supported for Azure file shares:</span><span class="sxs-lookup"><span data-stu-id="443fc-117">The following backup scenarios aren't supported for Azure file shares:</span></span>
- <span data-ttu-id="443fc-118">You can't protect Azure file shares in Storage Accounts with [read-access geo-redundant storage](../storage/common/storage-redundancy-grs.md) (RA-GRS) replication\*.</span><span class="sxs-lookup"><span data-stu-id="443fc-118">You can't protect Azure file shares in Storage Accounts with [read-access geo-redundant storage](../storage/common/storage-redundancy-grs.md) (RA-GRS) replication\*.</span></span>
- <span data-ttu-id="443fc-119">You can't protect Azure file shares in storage accounts that have Virtual Networks or Firewall enabled.</span><span class="sxs-lookup"><span data-stu-id="443fc-119">You can't protect Azure file shares in storage accounts that have Virtual Networks or Firewall enabled.</span></span>
- <span data-ttu-id="443fc-120">There is no PowerShell or CLI available for protecting Azure Files using Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="443fc-120">There is no PowerShell or CLI available for protecting Azure Files using Azure Backup.</span></span>
- <span data-ttu-id="443fc-121">The maximum number of scheduled backups per day is one.</span><span class="sxs-lookup"><span data-stu-id="443fc-121">The maximum number of scheduled backups per day is one.</span></span>
- <span data-ttu-id="443fc-122">The maximum number of on-demand backups per day is four.</span><span class="sxs-lookup"><span data-stu-id="443fc-122">The maximum number of on-demand backups per day is four.</span></span>
- <span data-ttu-id="443fc-123">Use [resource locks](https://docs.microsoft.com/cli/azure/resource/lock?view=azure-cli-latest) on the storage account to prevent accidental deletion of backups in your Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="443fc-123">Use [resource locks](https://docs.microsoft.com/cli/azure/resource/lock?view=azure-cli-latest) on the storage account to prevent accidental deletion of backups in your Recovery Services vault.</span></span>
- <span data-ttu-id="443fc-124">Do not delete snapshots created by Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="443fc-124">Do not delete snapshots created by Azure Backup.</span></span> <span data-ttu-id="443fc-125">Deleting snapshots can result in loss of recovery points and/or restore failures.</span><span class="sxs-lookup"><span data-stu-id="443fc-125">Deleting snapshots can result in loss of recovery points and/or restore failures.</span></span>

<span data-ttu-id="443fc-126">\*Azure File Shares in Storage Accounts with [read-access geo-redundant storage](../storage/common/storage-redundancy-grs.md) (RA-GRS) replication function as GRS and billed at GRS prices.</span><span class="sxs-lookup"><span data-stu-id="443fc-126">\*Azure File Shares in Storage Accounts with [read-access geo-redundant storage](../storage/common/storage-redundancy-grs.md) (RA-GRS) replication function as GRS and billed at GRS prices.</span></span>

<span data-ttu-id="443fc-127">Backup for Azure File Shares in Storage Accounts with [zone redundant storage](../storage/common/storage-redundancy-zrs.md) (ZRS) replication is currently available only in Central US (CUS), East US 2 (EUS2), North Europe (NE), SouthEast Asia (SEA) and West Europe (WE).</span><span class="sxs-lookup"><span data-stu-id="443fc-127">Backup for Azure File Shares in Storage Accounts with [zone redundant storage](../storage/common/storage-redundancy-zrs.md) (ZRS) replication is currently available only in Central US (CUS), East US 2 (EUS2), North Europe (NE), SouthEast Asia (SEA) and West Europe (WE).</span></span>

## <a name="configuring-backup-for-an-azure-file-share"></a><span data-ttu-id="443fc-128">Configuring backup for an Azure file share</span><span class="sxs-lookup"><span data-stu-id="443fc-128">Configuring backup for an Azure file share</span></span>
<span data-ttu-id="443fc-129">All backup data is stored in Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="443fc-129">All backup data is stored in Recovery Services vaults.</span></span> <span data-ttu-id="443fc-130">This tutorial assumes you already have established an Azure file share.</span><span class="sxs-lookup"><span data-stu-id="443fc-130">This tutorial assumes you already have established an Azure file share.</span></span> <span data-ttu-id="443fc-131">To back up your Azure file share:</span><span class="sxs-lookup"><span data-stu-id="443fc-131">To back up your Azure file share:</span></span>

1. <span data-ttu-id="443fc-132">Create a Recovery Services vault in the same region as your file share.</span><span class="sxs-lookup"><span data-stu-id="443fc-132">Create a Recovery Services vault in the same region as your file share.</span></span> <span data-ttu-id="443fc-133">If you already have a vault, open your vault's Overview page and click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="443fc-133">If you already have a vault, open your vault's Overview page and click **Backup**.</span></span>

    ![Choose Azure Fileshare as Backup goal](./media/backup-file-shares/overview-backup-page.png)

2. <span data-ttu-id="443fc-135">In the Backup Goal menu, from **What do you want to backup?**, choose Azure File Share.</span><span class="sxs-lookup"><span data-stu-id="443fc-135">In the Backup Goal menu, from **What do you want to backup?**, choose Azure File Share.</span></span>

    ![Choose Azure Fileshare as Backup goal](./media/backup-file-shares/choose-azure-fileshare-from-backup-goal.png)

3. <span data-ttu-id="443fc-137">Click **Backup** to configure the Azure file share to your Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="443fc-137">Click **Backup** to configure the Azure file share to your Recovery Services vault.</span></span> 

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/set-backup-goal.png)

    <span data-ttu-id="443fc-139">Once the vault is associated with the Azure file share, the Backup menu opens and prompts you select a Storage account.</span><span class="sxs-lookup"><span data-stu-id="443fc-139">Once the vault is associated with the Azure file share, the Backup menu opens and prompts you select a Storage account.</span></span> <span data-ttu-id="443fc-140">The menu displays all supported Storage Accounts in the region where your vault exists, that aren't already associated with a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="443fc-140">The menu displays all supported Storage Accounts in the region where your vault exists, that aren't already associated with a Recovery Services vault.</span></span>

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/list-of-storage-accounts.png)

4. <span data-ttu-id="443fc-142">In the list of Storage accounts, select an account, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="443fc-142">In the list of Storage accounts, select an account, and click **OK**.</span></span> <span data-ttu-id="443fc-143">Azure searches the storage account for files shares that can be backed up.</span><span class="sxs-lookup"><span data-stu-id="443fc-143">Azure searches the storage account for files shares that can be backed up.</span></span> <span data-ttu-id="443fc-144">If you recently added your file shares and do not see them in the list, allow a little time for the file shares to appear.</span><span class="sxs-lookup"><span data-stu-id="443fc-144">If you recently added your file shares and do not see them in the list, allow a little time for the file shares to appear.</span></span>

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/discover-file-shares.png)

5. <span data-ttu-id="443fc-146">From the **File Shares** list, select one or more of the file shares you want to backup, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="443fc-146">From the **File Shares** list, select one or more of the file shares you want to backup, and click **OK**.</span></span>

6. <span data-ttu-id="443fc-147">After choosing your File Shares, the Backup menu switches to the **Backup policy**.</span><span class="sxs-lookup"><span data-stu-id="443fc-147">After choosing your File Shares, the Backup menu switches to the **Backup policy**.</span></span> <span data-ttu-id="443fc-148">From this menu either select an existing backup policy, or create a new one, and then click **Enable Backup**.</span><span class="sxs-lookup"><span data-stu-id="443fc-148">From this menu either select an existing backup policy, or create a new one, and then click **Enable Backup**.</span></span> 

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/apply-backup-policy.png)

    <span data-ttu-id="443fc-150">After establishing a backup policy, a snapshot of the File Shares will be taken at the scheduled time, and the recovery point is retained for the chosen period.</span><span class="sxs-lookup"><span data-stu-id="443fc-150">After establishing a backup policy, a snapshot of the File Shares will be taken at the scheduled time, and the recovery point is retained for the chosen period.</span></span>

## <a name="create-an-on-demand-backup"></a><span data-ttu-id="443fc-151">Create an on-demand backup</span><span class="sxs-lookup"><span data-stu-id="443fc-151">Create an on-demand backup</span></span>
<span data-ttu-id="443fc-152">Occasionally you may want to generate a backup snapshot, or recovery point, outside of the times scheduled in the backup policy.</span><span class="sxs-lookup"><span data-stu-id="443fc-152">Occasionally you may want to generate a backup snapshot, or recovery point, outside of the times scheduled in the backup policy.</span></span> <span data-ttu-id="443fc-153">A common time to generate an on-demand backup is right after you've configured the backup policy.</span><span class="sxs-lookup"><span data-stu-id="443fc-153">A common time to generate an on-demand backup is right after you've configured the backup policy.</span></span> <span data-ttu-id="443fc-154">Based on the schedule in the backup policy, it may be hours or days until a snapshot is taken.</span><span class="sxs-lookup"><span data-stu-id="443fc-154">Based on the schedule in the backup policy, it may be hours or days until a snapshot is taken.</span></span> <span data-ttu-id="443fc-155">To protect your data until the backup policy engages, initiate an on-demand backup.</span><span class="sxs-lookup"><span data-stu-id="443fc-155">To protect your data until the backup policy engages, initiate an on-demand backup.</span></span> <span data-ttu-id="443fc-156">Creating an Oo-demand backup is often required before you make planned changes to your file shares.</span><span class="sxs-lookup"><span data-stu-id="443fc-156">Creating an Oo-demand backup is often required before you make planned changes to your file shares.</span></span> 

### <a name="to-create-an-on-demand-backup"></a><span data-ttu-id="443fc-157">To create an on-demand backup</span><span class="sxs-lookup"><span data-stu-id="443fc-157">To create an on-demand backup</span></span>

1. <span data-ttu-id="443fc-158">Open the Recovery Services vault that contains the file share recovery points, and click **Backup Items**.</span><span class="sxs-lookup"><span data-stu-id="443fc-158">Open the Recovery Services vault that contains the file share recovery points, and click **Backup Items**.</span></span> <span data-ttu-id="443fc-159">The list of Backup Item types appears.</span><span class="sxs-lookup"><span data-stu-id="443fc-159">The list of Backup Item types appears.</span></span>

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/list-of-backup-items.png)

2. <span data-ttu-id="443fc-161">From the list, select **Azure Storage (Azure Files)**.</span><span class="sxs-lookup"><span data-stu-id="443fc-161">From the list, select **Azure Storage (Azure Files)**.</span></span> <span data-ttu-id="443fc-162">The list of Azure file shares appears.</span><span class="sxs-lookup"><span data-stu-id="443fc-162">The list of Azure file shares appears.</span></span>

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/list-of-azure-files-backup-items.png)

3. <span data-ttu-id="443fc-164">From the list of Azure file shares, select the desired file share.</span><span class="sxs-lookup"><span data-stu-id="443fc-164">From the list of Azure file shares, select the desired file share.</span></span> <span data-ttu-id="443fc-165">The Backup Item menu for the selected file share opens.</span><span class="sxs-lookup"><span data-stu-id="443fc-165">The Backup Item menu for the selected file share opens.</span></span>

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/backup-item-menu.png)

4. <span data-ttu-id="443fc-167">From the Backup Item menu, click **Backup Now**.</span><span class="sxs-lookup"><span data-stu-id="443fc-167">From the Backup Item menu, click **Backup Now**.</span></span> <span data-ttu-id="443fc-168">Because this is an on-demand backup job, there is no retention policy associated with the recovery point.</span><span class="sxs-lookup"><span data-stu-id="443fc-168">Because this is an on-demand backup job, there is no retention policy associated with the recovery point.</span></span> <span data-ttu-id="443fc-169">The **Backup Now** dialog opens.</span><span class="sxs-lookup"><span data-stu-id="443fc-169">The **Backup Now** dialog opens.</span></span> <span data-ttu-id="443fc-170">Specify the last day you want to retain the recovery point.</span><span class="sxs-lookup"><span data-stu-id="443fc-170">Specify the last day you want to retain the recovery point.</span></span> 
  
   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/backup-now-menu.png)

## <a name="restore-from-backup-of-azure-file-share"></a><span data-ttu-id="443fc-172">Restore from backup of Azure file share</span><span class="sxs-lookup"><span data-stu-id="443fc-172">Restore from backup of Azure file share</span></span>
<span data-ttu-id="443fc-173">If you need to restore an entire file share or individual files or folders from a Restore Point, head to the Backup Item as detailed in the previous section.</span><span class="sxs-lookup"><span data-stu-id="443fc-173">If you need to restore an entire file share or individual files or folders from a Restore Point, head to the Backup Item as detailed in the previous section.</span></span> <span data-ttu-id="443fc-174">Choose **Restore Share** to restore an entire file share from a desired Point-in-time.</span><span class="sxs-lookup"><span data-stu-id="443fc-174">Choose **Restore Share** to restore an entire file share from a desired Point-in-time.</span></span> <span data-ttu-id="443fc-175">From the list of Restore Points that show up, select one to be able to Overwrite your current file share or Restore this to an alternate file share in the same region.</span><span class="sxs-lookup"><span data-stu-id="443fc-175">From the list of Restore Points that show up, select one to be able to Overwrite your current file share or Restore this to an alternate file share in the same region.</span></span>

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/select-restore-location.png)

## <a name="restore-individual-files-or-folders-from-backup-of-azure-file-shares"></a><span data-ttu-id="443fc-177">Restore individual files or folders from backup of Azure file shares</span><span class="sxs-lookup"><span data-stu-id="443fc-177">Restore individual files or folders from backup of Azure file shares</span></span>
<span data-ttu-id="443fc-178">Azure Backup provides the ability to browse a Restore Point within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="443fc-178">Azure Backup provides the ability to browse a Restore Point within the Azure portal.</span></span> <span data-ttu-id="443fc-179">To restore a file or folder of your choice, click on File Recovery from the Backup Item page and choose from the list of Restore Points.</span><span class="sxs-lookup"><span data-stu-id="443fc-179">To restore a file or folder of your choice, click on File Recovery from the Backup Item page and choose from the list of Restore Points.</span></span> <span data-ttu-id="443fc-180">Select the Recovery Destination and then click **Select File** to browse the restore point.</span><span class="sxs-lookup"><span data-stu-id="443fc-180">Select the Recovery Destination and then click **Select File** to browse the restore point.</span></span> <span data-ttu-id="443fc-181">Select the file or folder of your choice and **Restore**.</span><span class="sxs-lookup"><span data-stu-id="443fc-181">Select the file or folder of your choice and **Restore**.</span></span>

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/restore-individual-files-folders.png)

## <a name="manage-azure-file-share-backups"></a><span data-ttu-id="443fc-183">Manage Azure file share backups</span><span class="sxs-lookup"><span data-stu-id="443fc-183">Manage Azure file share backups</span></span>

<span data-ttu-id="443fc-184">You can execute several management tasks for File share backups on the **Backup Jobs** page, including:</span><span class="sxs-lookup"><span data-stu-id="443fc-184">You can execute several management tasks for File share backups on the **Backup Jobs** page, including:</span></span>
- [<span data-ttu-id="443fc-185">Monitor jobs</span><span class="sxs-lookup"><span data-stu-id="443fc-185">Monitor jobs</span></span>](backup-azure-files.md#monitor-jobs)
- [<span data-ttu-id="443fc-186">Create a new policy</span><span class="sxs-lookup"><span data-stu-id="443fc-186">Create a new policy</span></span>](backup-azure-files.md#create-a-new-policy)
- [<span data-ttu-id="443fc-187">Stop protection on a file share</span><span class="sxs-lookup"><span data-stu-id="443fc-187">Stop protection on a file share</span></span>](backup-azure-files.md#stop-protecting-an-azure-file-share)
- [<span data-ttu-id="443fc-188">Resume protection on a file share</span><span class="sxs-lookup"><span data-stu-id="443fc-188">Resume protection on a file share</span></span>](backup-azure-files.md#resume-protection-for-azure-file-share)
- [<span data-ttu-id="443fc-189">Delete backup data</span><span class="sxs-lookup"><span data-stu-id="443fc-189">Delete backup data</span></span>](backup-azure-files.md#delete-backup-data)

### <a name="monitor-jobs"></a><span data-ttu-id="443fc-190">Monitor jobs</span><span class="sxs-lookup"><span data-stu-id="443fc-190">Monitor jobs</span></span>

<span data-ttu-id="443fc-191">You can monitor the progress of all jobs on the **Backup Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="443fc-191">You can monitor the progress of all jobs on the **Backup Jobs** page.</span></span>

<span data-ttu-id="443fc-192">To open the **Backup Jobs** page:</span><span class="sxs-lookup"><span data-stu-id="443fc-192">To open the **Backup Jobs** page:</span></span>

- <span data-ttu-id="443fc-193">Open the Recovery Services vault you want to monitor, and in the Recovery Services vault menu, click **Jobs** and then click **Backup Jobs**.</span><span class="sxs-lookup"><span data-stu-id="443fc-193">Open the Recovery Services vault you want to monitor, and in the Recovery Services vault menu, click **Jobs** and then click **Backup Jobs**.</span></span>
   <span data-ttu-id="443fc-194">![Select the job you want to monitor](./media/backup-file-shares/open-backup-jobs.png)</span><span class="sxs-lookup"><span data-stu-id="443fc-194">![Select the job you want to monitor](./media/backup-file-shares/open-backup-jobs.png)</span></span>

    <span data-ttu-id="443fc-195">The list of Backup jobs and the status of those jobs appears.</span><span class="sxs-lookup"><span data-stu-id="443fc-195">The list of Backup jobs and the status of those jobs appears.</span></span>
   <span data-ttu-id="443fc-196">![Select the job you want to monitor](./media/backup-file-shares/backup-jobs-progress-list.png)</span><span class="sxs-lookup"><span data-stu-id="443fc-196">![Select the job you want to monitor](./media/backup-file-shares/backup-jobs-progress-list.png)</span></span>

### <a name="create-a-new-policy"></a><span data-ttu-id="443fc-197">Create a new policy</span><span class="sxs-lookup"><span data-stu-id="443fc-197">Create a new policy</span></span>

<span data-ttu-id="443fc-198">You can create a new policy to back up Azure file shares from the **Backup Policies** of the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="443fc-198">You can create a new policy to back up Azure file shares from the **Backup Policies** of the Recovery Services vault.</span></span> <span data-ttu-id="443fc-199">All policies created when you configure Backup for file shares show up with the Policy Type as Azure file Share.</span><span class="sxs-lookup"><span data-stu-id="443fc-199">All policies created when you configure Backup for file shares show up with the Policy Type as Azure file Share.</span></span>

<span data-ttu-id="443fc-200">To view the existing Backup policies:</span><span class="sxs-lookup"><span data-stu-id="443fc-200">To view the existing Backup policies:</span></span>

- <span data-ttu-id="443fc-201">Open the Recovery Services vault you want, and in the Recovery Services vault menu, click **Backup policies**.</span><span class="sxs-lookup"><span data-stu-id="443fc-201">Open the Recovery Services vault you want, and in the Recovery Services vault menu, click **Backup policies**.</span></span> <span data-ttu-id="443fc-202">All Backup policies are listed.</span><span class="sxs-lookup"><span data-stu-id="443fc-202">All Backup policies are listed.</span></span>

   ![Select the job you want to monitor](./media/backup-file-shares/list-of-backup-policies.png)

<span data-ttu-id="443fc-204">To create a new Backup policy:</span><span class="sxs-lookup"><span data-stu-id="443fc-204">To create a new Backup policy:</span></span>

1. <span data-ttu-id="443fc-205">In the Recovery Services vault menu, click **Backup policies**.</span><span class="sxs-lookup"><span data-stu-id="443fc-205">In the Recovery Services vault menu, click **Backup policies**.</span></span>
2. <span data-ttu-id="443fc-206">In the list of Backup policies, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="443fc-206">In the list of Backup policies, click **Add**.</span></span>

   ![Select the job you want to monitor](./media/backup-file-shares/new-backup-policy.png)

3. <span data-ttu-id="443fc-208">In the **Add** menu, select **Azure File Share**.</span><span class="sxs-lookup"><span data-stu-id="443fc-208">In the **Add** menu, select **Azure File Share**.</span></span> <span data-ttu-id="443fc-209">The Backup policy menu for Azure file share opens.</span><span class="sxs-lookup"><span data-stu-id="443fc-209">The Backup policy menu for Azure file share opens.</span></span> <span data-ttu-id="443fc-210">Provide the name for the policy, backup frequency, and retention range for the recovery points.</span><span class="sxs-lookup"><span data-stu-id="443fc-210">Provide the name for the policy, backup frequency, and retention range for the recovery points.</span></span> <span data-ttu-id="443fc-211">Click OK when you have defined the policy.</span><span class="sxs-lookup"><span data-stu-id="443fc-211">Click OK when you have defined the policy.</span></span>

   ![Select the job you want to monitor](./media/backup-file-shares/create-new-policy.png)

### <a name="stop-protecting-an-azure-file-share"></a><span data-ttu-id="443fc-213">Stop protecting an Azure file share</span><span class="sxs-lookup"><span data-stu-id="443fc-213">Stop protecting an Azure file share</span></span>

<span data-ttu-id="443fc-214">If you choose to stop protecting an Azure file share, you are asked if you want to retain the recovery points.</span><span class="sxs-lookup"><span data-stu-id="443fc-214">If you choose to stop protecting an Azure file share, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="443fc-215">There are two ways to stop protecting Azure file shares:</span><span class="sxs-lookup"><span data-stu-id="443fc-215">There are two ways to stop protecting Azure file shares:</span></span>

- <span data-ttu-id="443fc-216">Stop all future backup jobs and delete all recovery points, or</span><span class="sxs-lookup"><span data-stu-id="443fc-216">Stop all future backup jobs and delete all recovery points, or</span></span>
- <span data-ttu-id="443fc-217">Stop all future backup jobs but leave the recovery points</span><span class="sxs-lookup"><span data-stu-id="443fc-217">Stop all future backup jobs but leave the recovery points</span></span>

<span data-ttu-id="443fc-218">There may be a cost associated with leaving the recovery points in storage as the underlying snapshots created by Azure Backup will be retained.</span><span class="sxs-lookup"><span data-stu-id="443fc-218">There may be a cost associated with leaving the recovery points in storage as the underlying snapshots created by Azure Backup will be retained.</span></span> <span data-ttu-id="443fc-219">However, the benefit of leaving the recovery points is you can restore the File share later, if desired.</span><span class="sxs-lookup"><span data-stu-id="443fc-219">However, the benefit of leaving the recovery points is you can restore the File share later, if desired.</span></span> <span data-ttu-id="443fc-220">For information about the cost of leaving the recovery points, see the pricing details.</span><span class="sxs-lookup"><span data-stu-id="443fc-220">For information about the cost of leaving the recovery points, see the pricing details.</span></span> <span data-ttu-id="443fc-221">If you choose to delete all recovery points, you can't restore the File share.</span><span class="sxs-lookup"><span data-stu-id="443fc-221">If you choose to delete all recovery points, you can't restore the File share.</span></span>

<span data-ttu-id="443fc-222">To stop protection for an Azure file share:</span><span class="sxs-lookup"><span data-stu-id="443fc-222">To stop protection for an Azure file share:</span></span>

1. <span data-ttu-id="443fc-223">Open the Recovery Services vault that contains the file share recovery points, and click **Backup Items**.</span><span class="sxs-lookup"><span data-stu-id="443fc-223">Open the Recovery Services vault that contains the file share recovery points, and click **Backup Items**.</span></span> <span data-ttu-id="443fc-224">The list of Backup Item types appears.</span><span class="sxs-lookup"><span data-stu-id="443fc-224">The list of Backup Item types appears.</span></span>

   ![click Backup to associate the Azure file share with vault](./media/backup-file-shares/list-of-backup-items.png) 

2. <span data-ttu-id="443fc-226">In the **Backup Management Type** list, select **Azure Storage (Azure Files)**.</span><span class="sxs-lookup"><span data-stu-id="443fc-226">In the **Backup Management Type** list, select **Azure Storage (Azure Files)**.</span></span> <span data-ttu-id="443fc-227">The list of Backup Items for (Azure Storage (Azure Files)) appears.</span><span class="sxs-lookup"><span data-stu-id="443fc-227">The list of Backup Items for (Azure Storage (Azure Files)) appears.</span></span>

   ![click item to open additional menu](./media/backup-file-shares/azure-file-share-backup-items.png) 

3. <span data-ttu-id="443fc-229">In the list of Backup Items (Azure Storage (Azure Files)), select the backup item you want to stop.</span><span class="sxs-lookup"><span data-stu-id="443fc-229">In the list of Backup Items (Azure Storage (Azure Files)), select the backup item you want to stop.</span></span>

4. <span data-ttu-id="443fc-230">In the Azure file share items, click the **More** menu, and select **Stop Backup**.</span><span class="sxs-lookup"><span data-stu-id="443fc-230">In the Azure file share items, click the **More** menu, and select **Stop Backup**.</span></span> 

   ![click item to open additional menu](./media/backup-file-shares/stop-backup.png)

5. <span data-ttu-id="443fc-232">From the Stop Backup menu, choose to **Retain** or **Delete Backup Data** and click **Stop Backup**.</span><span class="sxs-lookup"><span data-stu-id="443fc-232">From the Stop Backup menu, choose to **Retain** or **Delete Backup Data** and click **Stop Backup**.</span></span>

   ![click item to open additional menu](./media/backup-file-shares/retain-data.png)

### <a name="resume-protection-for-azure-file-share"></a><span data-ttu-id="443fc-234">Resume protection for Azure file share</span><span class="sxs-lookup"><span data-stu-id="443fc-234">Resume protection for Azure file share</span></span>

<span data-ttu-id="443fc-235">If the Retain Backup Data option was chosen when protection for the file share was stopped, then it's possible to resume protection.</span><span class="sxs-lookup"><span data-stu-id="443fc-235">If the Retain Backup Data option was chosen when protection for the file share was stopped, then it's possible to resume protection.</span></span> <span data-ttu-id="443fc-236">If the **Delete Backup Data** option was chosen, then protection for the file share can't resume.</span><span class="sxs-lookup"><span data-stu-id="443fc-236">If the **Delete Backup Data** option was chosen, then protection for the file share can't resume.</span></span>

<span data-ttu-id="443fc-237">To resume protection for the file share, go to the Backup Item and click Resume Backup.</span><span class="sxs-lookup"><span data-stu-id="443fc-237">To resume protection for the file share, go to the Backup Item and click Resume Backup.</span></span> <span data-ttu-id="443fc-238">The Backup Policy opens and you can choose a policy of your choice to resume backup.</span><span class="sxs-lookup"><span data-stu-id="443fc-238">The Backup Policy opens and you can choose a policy of your choice to resume backup.</span></span>

   ![Select the job you want to monitor](./media/backup-file-shares/resume-backup-job.png)

### <a name="delete-backup-data"></a><span data-ttu-id="443fc-240">Delete Backup data</span><span class="sxs-lookup"><span data-stu-id="443fc-240">Delete Backup data</span></span> 

<span data-ttu-id="443fc-241">You can delete the backup of a file share during the Stop backup job, or any time after you have stopped protection.</span><span class="sxs-lookup"><span data-stu-id="443fc-241">You can delete the backup of a file share during the Stop backup job, or any time after you have stopped protection.</span></span> <span data-ttu-id="443fc-242">It may even be beneficial to wait days or weeks before deleting the recovery points.</span><span class="sxs-lookup"><span data-stu-id="443fc-242">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="443fc-243">Unlike restoring recovery points, when deleting backup data, you can't choose specific recovery points to delete.</span><span class="sxs-lookup"><span data-stu-id="443fc-243">Unlike restoring recovery points, when deleting backup data, you can't choose specific recovery points to delete.</span></span> <span data-ttu-id="443fc-244">If you choose to delete your backup data, you delete all recovery points associated with the item.</span><span class="sxs-lookup"><span data-stu-id="443fc-244">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="443fc-245">The following procedure assumes the Backup job for the virtual machine has been stopped.</span><span class="sxs-lookup"><span data-stu-id="443fc-245">The following procedure assumes the Backup job for the virtual machine has been stopped.</span></span> <span data-ttu-id="443fc-246">Once the Backup job is stopped, the Resume backup and Delete Backup Data options are available in the Backup item dashboard.</span><span class="sxs-lookup"><span data-stu-id="443fc-246">Once the Backup job is stopped, the Resume backup and Delete Backup Data options are available in the Backup item dashboard.</span></span> <span data-ttu-id="443fc-247">Click Delete Backup Data and type the name of the File share to confirm deletion.</span><span class="sxs-lookup"><span data-stu-id="443fc-247">Click Delete Backup Data and type the name of the File share to confirm deletion.</span></span> <span data-ttu-id="443fc-248">Optionally, provide a Reason to delete or Comment.</span><span class="sxs-lookup"><span data-stu-id="443fc-248">Optionally, provide a Reason to delete or Comment.</span></span>

## <a name="see-also"></a><span data-ttu-id="443fc-249">See Also</span><span class="sxs-lookup"><span data-stu-id="443fc-249">See Also</span></span>
<span data-ttu-id="443fc-250">For additional information on Azure file shares, see</span><span class="sxs-lookup"><span data-stu-id="443fc-250">For additional information on Azure file shares, see</span></span>
- [<span data-ttu-id="443fc-251">FAQ for Azure file share backup</span><span class="sxs-lookup"><span data-stu-id="443fc-251">FAQ for Azure file share backup</span></span>](backup-azure-files-faq.md)
- [<span data-ttu-id="443fc-252">Troubleshoot Azure file share backup</span><span class="sxs-lookup"><span data-stu-id="443fc-252">Troubleshoot Azure file share backup</span></span>](troubleshoot-azure-files.md)
