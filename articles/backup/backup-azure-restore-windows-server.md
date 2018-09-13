---
title: Restore data in Azure to a Windows Server or Windows computer | Microsoft Docs
description: Learn how to restore data stored in Azure to a Windows Server or Windows computer.
services: backup
documentationcenter: ''
author: saurabhsensharma
manager: shivamg
editor: ''
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/1/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 162e83ad95d7702f62f744fa475dddc59bf2aca4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553452"
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="074aa-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span><span class="sxs-lookup"><span data-stu-id="074aa-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](backup-azure-restore-windows-server.md)
> * [Classic portal](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="074aa-106">This article explains how to restore data from a backup vault.</span><span class="sxs-lookup"><span data-stu-id="074aa-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="074aa-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span><span class="sxs-lookup"><span data-stu-id="074aa-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="074aa-108">When you restore data, it is possible to:</span><span class="sxs-lookup"><span data-stu-id="074aa-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="074aa-109">Restore data to the same machine from which the backups were taken.</span><span class="sxs-lookup"><span data-stu-id="074aa-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="074aa-110">Restore data to an alternate machine.</span><span class="sxs-lookup"><span data-stu-id="074aa-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="074aa-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span><span class="sxs-lookup"><span data-stu-id="074aa-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="074aa-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span><span class="sxs-lookup"><span data-stu-id="074aa-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="074aa-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span><span class="sxs-lookup"><span data-stu-id="074aa-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data. Also the backup data must be protected in vaults in locales listed in the support article. Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore. Instant Restore is **not** currently available in all locales.
>

<span data-ttu-id="074aa-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="074aa-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="074aa-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span><span class="sxs-lookup"><span data-stu-id="074aa-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="recover-data-to-the-same-machine"></a><span data-ttu-id="074aa-120">Recover data to the same machine</span><span class="sxs-lookup"><span data-stu-id="074aa-120">Recover data to the same machine</span></span>
<span data-ttu-id="074aa-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span><span class="sxs-lookup"><span data-stu-id="074aa-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="074aa-122">Open the **Microsoft Azure Backup** snap in.</span><span class="sxs-lookup"><span data-stu-id="074aa-122">Open the **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="074aa-123">Click **Recover Data** to initiate the workflow.</span><span class="sxs-lookup"><span data-stu-id="074aa-123">Click **Recover Data** to initiate the workflow.</span></span>

    ![Recover Data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/recover.png)
3. <span data-ttu-id="074aa-125">Select the **This server (*yourmachinename*)** option to restore the backed up file on the same machine.</span><span class="sxs-lookup"><span data-stu-id="074aa-125">Select the **This server (*yourmachinename*)** option to restore the backed up file on the same machine.</span></span>

    ![Same machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/samemachine.png)
4. <span data-ttu-id="074aa-127">Choose to **Browse for files** or **Search for files**.</span><span class="sxs-lookup"><span data-stu-id="074aa-127">Choose to **Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="074aa-128">Leave the default option if you plan to restore one or more files whose path is known.</span><span class="sxs-lookup"><span data-stu-id="074aa-128">Leave the default option if you plan to restore one or more files whose path is known.</span></span> <span data-ttu-id="074aa-129">If you are not sure about the folder structure but would like to search for a file, pick the **Search for files** option.</span><span class="sxs-lookup"><span data-stu-id="074aa-129">If you are not sure about the folder structure but would like to search for a file, pick the **Search for files** option.</span></span> <span data-ttu-id="074aa-130">For the purpose of this section, we will proceed with the default option.</span><span class="sxs-lookup"><span data-stu-id="074aa-130">For the purpose of this section, we will proceed with the default option.</span></span>

    ![Browse files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/browseandsearch.png)
5. <span data-ttu-id="074aa-132">Select the volume from which you wish to restore the file.</span><span class="sxs-lookup"><span data-stu-id="074aa-132">Select the volume from which you wish to restore the file.</span></span>

    <span data-ttu-id="074aa-133">You can restore from any point in time.</span><span class="sxs-lookup"><span data-stu-id="074aa-133">You can restore from any point in time.</span></span> <span data-ttu-id="074aa-134">Dates which appear in **bold** in the calendar control indicate the availability of a restore point.</span><span class="sxs-lookup"><span data-stu-id="074aa-134">Dates which appear in **bold** in the calendar control indicate the availability of a restore point.</span></span> <span data-ttu-id="074aa-135">Once a date is selected, based on your backup schedule (and the success of a backup operation), you can select a point in time from the **Time** drop down.</span><span class="sxs-lookup"><span data-stu-id="074aa-135">Once a date is selected, based on your backup schedule (and the success of a backup operation), you can select a point in time from the **Time** drop down.</span></span>

    ![Volume and Date](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/volanddate.png)
6. <span data-ttu-id="074aa-137">Select the items to recover.</span><span class="sxs-lookup"><span data-stu-id="074aa-137">Select the items to recover.</span></span> <span data-ttu-id="074aa-138">You can multi-select folders/files you wish to restore.</span><span class="sxs-lookup"><span data-stu-id="074aa-138">You can multi-select folders/files you wish to restore.</span></span>

    ![Select files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/selectfiles.png)
7. <span data-ttu-id="074aa-140">Specify the recovery parameters.</span><span class="sxs-lookup"><span data-stu-id="074aa-140">Specify the recovery parameters.</span></span>

    ![Recovery options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/recoveroptions.png)

   * <span data-ttu-id="074aa-142">You have an option of restoring to the original location (in which the file/folder would be overwritten) or to another location in the same machine.</span><span class="sxs-lookup"><span data-stu-id="074aa-142">You have an option of restoring to the original location (in which the file/folder would be overwritten) or to another location in the same machine.</span></span>
   * <span data-ttu-id="074aa-143">If the file/folder you wish to restore exists in the target location, you can create copies (two versions of the same file), overwrite the files in the target location, or skip the recovery of the files which exist in the target.</span><span class="sxs-lookup"><span data-stu-id="074aa-143">If the file/folder you wish to restore exists in the target location, you can create copies (two versions of the same file), overwrite the files in the target location, or skip the recovery of the files which exist in the target.</span></span>
   * <span data-ttu-id="074aa-144">It is highly recommended that you leave the default option of restoring the ACLs on the files which are being recovered.</span><span class="sxs-lookup"><span data-stu-id="074aa-144">It is highly recommended that you leave the default option of restoring the ACLs on the files which are being recovered.</span></span>
8. <span data-ttu-id="074aa-145">Once these inputs are provided, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="074aa-145">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="074aa-146">The recovery workflow, which restores the files to this machine, will begin.</span><span class="sxs-lookup"><span data-stu-id="074aa-146">The recovery workflow, which restores the files to this machine, will begin.</span></span>

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="074aa-147">Use Instant Restore to recover data to the same machine</span><span class="sxs-lookup"><span data-stu-id="074aa-147">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="074aa-148">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span><span class="sxs-lookup"><span data-stu-id="074aa-148">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="074aa-149">Open the **Microsoft Azure Backup** snap in.</span><span class="sxs-lookup"><span data-stu-id="074aa-149">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="074aa-150">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="074aa-150">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="074aa-151">The desktop app should appear in the search results.</span><span class="sxs-lookup"><span data-stu-id="074aa-151">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="074aa-152">Click **Recover Data** to start the wizard.</span><span class="sxs-lookup"><span data-stu-id="074aa-152">Click **Recover Data** to start the wizard.</span></span>

    ![Recover Data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="074aa-154">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="074aa-154">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Choose This server option to restore the data to the same machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="074aa-156">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="074aa-156">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Browse files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="074aa-158">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span><span class="sxs-lookup"><span data-stu-id="074aa-158">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="074aa-159">On the calendar, select a recovery point.</span><span class="sxs-lookup"><span data-stu-id="074aa-159">On the calendar, select a recovery point.</span></span> <span data-ttu-id="074aa-160">You can restore from any recovery point in time.</span><span class="sxs-lookup"><span data-stu-id="074aa-160">You can restore from any recovery point in time.</span></span> <span data-ttu-id="074aa-161">Dates in **bold** indicate the availability of at least one recovery point.</span><span class="sxs-lookup"><span data-stu-id="074aa-161">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="074aa-162">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="074aa-162">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume and Date](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="074aa-164">Once you have chosen the recovery point to restore, click **Mount**.</span><span class="sxs-lookup"><span data-stu-id="074aa-164">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="074aa-165">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span><span class="sxs-lookup"><span data-stu-id="074aa-165">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="074aa-166">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span><span class="sxs-lookup"><span data-stu-id="074aa-166">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Recovery options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="074aa-168">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span><span class="sxs-lookup"><span data-stu-id="074aa-168">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="074aa-169">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span><span class="sxs-lookup"><span data-stu-id="074aa-169">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Copy and paste files and folders from mounted volume to local location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="074aa-171">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span><span class="sxs-lookup"><span data-stu-id="074aa-171">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="074aa-172">Then click **Yes** to confirm that you want to unmount the volume.</span><span class="sxs-lookup"><span data-stu-id="074aa-172">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Unmount the volume and confirm](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted. No backup operations will run while the volume is mounted. Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.
    >

## <a name="recover-to-an-alternate-machine"></a><span data-ttu-id="074aa-177">Recover to an alternate machine</span><span class="sxs-lookup"><span data-stu-id="074aa-177">Recover to an alternate machine</span></span>

<span data-ttu-id="074aa-178">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span><span class="sxs-lookup"><span data-stu-id="074aa-178">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="074aa-179">The following steps illustrate the workflow.</span><span class="sxs-lookup"><span data-stu-id="074aa-179">The following steps illustrate the workflow.</span></span>  

<span data-ttu-id="074aa-180">The terminology used in these steps includes:</span><span class="sxs-lookup"><span data-stu-id="074aa-180">The terminology used in these steps includes:</span></span>

- <span data-ttu-id="074aa-181">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span><span class="sxs-lookup"><span data-stu-id="074aa-181">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="074aa-182">*Target machine* – The machine to which the data is being recovered.</span><span class="sxs-lookup"><span data-stu-id="074aa-182">*Target machine* – The machine to which the data is being recovered.</span></span>
- <span data-ttu-id="074aa-183">*Sample vault* – The Backup vault to which the *Source machine* and *Target machine* are registered.</span><span class="sxs-lookup"><span data-stu-id="074aa-183">*Sample vault* – The Backup vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> Backups taken from a machine cannot be restored on a machine which is running an earlier version of the operating system. For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine. However, the vice-versa does not hold true.
>
>

1. <span data-ttu-id="074aa-187">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span><span class="sxs-lookup"><span data-stu-id="074aa-187">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>
2. <span data-ttu-id="074aa-188">Ensure that the *Target machine* and the *Source machine* are registered to the same backup vault.</span><span class="sxs-lookup"><span data-stu-id="074aa-188">Ensure that the *Target machine* and the *Source machine* are registered to the same backup vault.</span></span>
3. <span data-ttu-id="074aa-189">Click **Recover Data** to initiate the workflow.</span><span class="sxs-lookup"><span data-stu-id="074aa-189">Click **Recover Data** to initiate the workflow.</span></span>

    ![Recover Data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="074aa-191">Select **Another server**</span><span class="sxs-lookup"><span data-stu-id="074aa-191">Select **Another server**</span></span>

    ![Another Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="074aa-193">Provide the vault credential file that corresponds to the *Sample vault*.</span><span class="sxs-lookup"><span data-stu-id="074aa-193">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="074aa-194">If the vault credential file is invalid (or expired) download a new vault credential file from the *Sample vault* in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="074aa-194">If the vault credential file is invalid (or expired) download a new vault credential file from the *Sample vault* in the Azure classic portal.</span></span> <span data-ttu-id="074aa-195">Once the vault credential file is provided, the backup vault against the vault credential file is displayed.</span><span class="sxs-lookup"><span data-stu-id="074aa-195">Once the vault credential file is provided, the backup vault against the vault credential file is displayed.</span></span>
6. <span data-ttu-id="074aa-196">Select the *Source machine* from the list of displayed machines.</span><span class="sxs-lookup"><span data-stu-id="074aa-196">Select the *Source machine* from the list of displayed machines.</span></span>

    ![List of machines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="074aa-198">Select either the **Search for files** or **Browse for files** option.</span><span class="sxs-lookup"><span data-stu-id="074aa-198">Select either the **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="074aa-199">For the purpose of this section, we will use the **Search for files** option.</span><span class="sxs-lookup"><span data-stu-id="074aa-199">For the purpose of this section, we will use the **Search for files** option.</span></span>

    ![Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="074aa-201">Select the volume and date in the next screen.</span><span class="sxs-lookup"><span data-stu-id="074aa-201">Select the volume and date in the next screen.</span></span> <span data-ttu-id="074aa-202">Search for the folder/file name you want to restore.</span><span class="sxs-lookup"><span data-stu-id="074aa-202">Search for the folder/file name you want to restore.</span></span>

    ![Search items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="074aa-204">Select the location where the files need to be restored.</span><span class="sxs-lookup"><span data-stu-id="074aa-204">Select the location where the files need to be restored.</span></span>

    ![Restore location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="074aa-206">Provide the encryption passphrase that was provided during *Source machine’s* registration to *Sample vault*.</span><span class="sxs-lookup"><span data-stu-id="074aa-206">Provide the encryption passphrase that was provided during *Source machine’s* registration to *Sample vault*.</span></span>

    ![Encryption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="074aa-208">Once the input is provided, click **Recover**, which triggers the restore of the backed up files to the destination provided.</span><span class="sxs-lookup"><span data-stu-id="074aa-208">Once the input is provided, click **Recover**, which triggers the restore of the backed up files to the destination provided.</span></span>


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="074aa-209">Use Instant Restore to restore data to an alternate machine</span><span class="sxs-lookup"><span data-stu-id="074aa-209">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="074aa-210">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span><span class="sxs-lookup"><span data-stu-id="074aa-210">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="074aa-211">The following steps illustrate the workflow.</span><span class="sxs-lookup"><span data-stu-id="074aa-211">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="074aa-212">The terminology used in these steps includes:</span><span class="sxs-lookup"><span data-stu-id="074aa-212">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="074aa-213">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span><span class="sxs-lookup"><span data-stu-id="074aa-213">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="074aa-214">*Target machine* – The machine to which the data is being recovered.</span><span class="sxs-lookup"><span data-stu-id="074aa-214">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="074aa-215">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span><span class="sxs-lookup"><span data-stu-id="074aa-215">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> Backups can't be restored to a target machine running an earlier version of the operating system. For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer. A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.
>
>

1. <span data-ttu-id="074aa-219">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span><span class="sxs-lookup"><span data-stu-id="074aa-219">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="074aa-220">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="074aa-220">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="074aa-221">Click **Recover Data** to open the **Recover Data wizard**.</span><span class="sxs-lookup"><span data-stu-id="074aa-221">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Recover Data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="074aa-223">On the **Getting Started** pane, select **Another server**</span><span class="sxs-lookup"><span data-stu-id="074aa-223">On the **Getting Started** pane, select **Another server**</span></span>

    ![Another Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="074aa-225">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="074aa-225">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="074aa-226">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="074aa-226">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="074aa-227">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span><span class="sxs-lookup"><span data-stu-id="074aa-227">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="074aa-228">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span><span class="sxs-lookup"><span data-stu-id="074aa-228">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="074aa-229">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="074aa-229">Then click **Next**.</span></span>

    ![List of machines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="074aa-231">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="074aa-231">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="074aa-233">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span><span class="sxs-lookup"><span data-stu-id="074aa-233">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="074aa-234">On the calendar, select a recovery point.</span><span class="sxs-lookup"><span data-stu-id="074aa-234">On the calendar, select a recovery point.</span></span> <span data-ttu-id="074aa-235">You can restore from any recovery point in time.</span><span class="sxs-lookup"><span data-stu-id="074aa-235">You can restore from any recovery point in time.</span></span> <span data-ttu-id="074aa-236">Dates in **bold** indicate the availability of at least one recovery point.</span><span class="sxs-lookup"><span data-stu-id="074aa-236">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="074aa-237">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="074aa-237">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Search items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="074aa-239">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span><span class="sxs-lookup"><span data-stu-id="074aa-239">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="074aa-240">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span><span class="sxs-lookup"><span data-stu-id="074aa-240">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Encryption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="074aa-242">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span><span class="sxs-lookup"><span data-stu-id="074aa-242">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="074aa-243">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span><span class="sxs-lookup"><span data-stu-id="074aa-243">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Encryption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="074aa-245">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span><span class="sxs-lookup"><span data-stu-id="074aa-245">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="074aa-246">Then click **Yes** to confirm that you want to unmount the volume.</span><span class="sxs-lookup"><span data-stu-id="074aa-246">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Encryption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted. No backup operations will run while the volume is mounted. Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.
    >

## <a name="next-steps"></a><span data-ttu-id="074aa-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="074aa-251">Next steps</span></span>
* <span data-ttu-id="074aa-252">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="074aa-252">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>




























