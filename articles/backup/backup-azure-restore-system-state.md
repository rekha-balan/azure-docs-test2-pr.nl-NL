---
title: 'Azure Backup: Restore System State to a Windows Server'
description: Step by step explanation for restoring Windows Server System State from a backup in Azure.
services: backup
author: saurabhsensharma
manager: shivamg
ms.service: backup
ms.topic: conceptual
ms.date: 8/18/2017
ms.author: saurse
ms.openlocfilehash: f8011fb3e7e1c5267f259a43f06d605690ffd281
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867384"
---
# <a name="restore-system-state-to-windows-server"></a><span data-ttu-id="a3ada-103">Restore System State to Windows Server</span><span class="sxs-lookup"><span data-stu-id="a3ada-103">Restore System State to Windows Server</span></span>

<span data-ttu-id="a3ada-104">This article explains how to restore Windows Server System State backups from an Azure Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="a3ada-104">This article explains how to restore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="a3ada-105">To restore System State, you must have a System State backup (created using the instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state), and make sure you have installed the [latest version of the Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="a3ada-105">To restore System State, you must have a System State backup (created using the instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state), and make sure you have installed the [latest version of the Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="a3ada-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span><span class="sxs-lookup"><span data-stu-id="a3ada-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="a3ada-107">Restore System State as files from Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="a3ada-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="a3ada-108">When restoring System State as files from Azure Backup, you can either:</span><span class="sxs-lookup"><span data-stu-id="a3ada-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="a3ada-109">Restore System State to the same server where the backups were taken, or</span><span class="sxs-lookup"><span data-stu-id="a3ada-109">Restore System State to the same server where the backups were taken, or</span></span>
  * <span data-ttu-id="a3ada-110">Restore System State file to an alternate server.</span><span class="sxs-lookup"><span data-stu-id="a3ada-110">Restore System State file to an alternate server.</span></span>

2. <span data-ttu-id="a3ada-111">Apply the restored System State files to a Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3ada-111">Apply the restored System State files to a Windows Server.</span></span>


## <a name="recover-system-state-files-to-the-same-server"></a><span data-ttu-id="a3ada-112">Recover System State files to the same server</span><span class="sxs-lookup"><span data-stu-id="a3ada-112">Recover System State files to the same server</span></span>
<span data-ttu-id="a3ada-113">The following steps explain how to roll back your Windows Server configuration to a previous state.</span><span class="sxs-lookup"><span data-stu-id="a3ada-113">The following steps explain how to roll back your Windows Server configuration to a previous state.</span></span> <span data-ttu-id="a3ada-114">Rolling your server configuration back to a known, stable state, can be extremely valuable.</span><span class="sxs-lookup"><span data-stu-id="a3ada-114">Rolling your server configuration back to a known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="a3ada-115">The following steps restore the server's System State from a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="a3ada-115">The following steps restore the server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="a3ada-116">Open the **Microsoft Azure Backup** snap-in.</span><span class="sxs-lookup"><span data-stu-id="a3ada-116">Open the **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="a3ada-117">If you don't know where the snap-in was installed, search the computer or server for **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-117">If you don't know where the snap-in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="a3ada-118">The desktop app should appear in the search results.</span><span class="sxs-lookup"><span data-stu-id="a3ada-118">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="a3ada-119">Click **Recover Data** to start the wizard.</span><span class="sxs-lookup"><span data-stu-id="a3ada-119">Click **Recover Data** to start the wizard.</span></span>

    ![Recover Data](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="a3ada-121">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-121">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Choose This server option to restore the data to the same machine](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="a3ada-123">On the **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-123">On the **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Browse files](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="a3ada-125">On the calendar in **Select Volume and Date** pane, select a recovery point.</span><span class="sxs-lookup"><span data-stu-id="a3ada-125">On the calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="a3ada-126">You can restore from any recovery point in time.</span><span class="sxs-lookup"><span data-stu-id="a3ada-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="a3ada-127">Dates in **bold** indicate the availability of at least one recovery point.</span><span class="sxs-lookup"><span data-stu-id="a3ada-127">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="a3ada-128">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="a3ada-128">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume and Date](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="a3ada-130">Once you have chosen the recovery point to restore, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-130">Once you have chosen the recovery point to restore, click **Next**.</span></span>

    <span data-ttu-id="a3ada-131">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span><span class="sxs-lookup"><span data-stu-id="a3ada-131">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="a3ada-132">On the next pane, specify the destination for the recovered System State files and click **Browse** to open Windows Explorer and find the files and folders you want.</span><span class="sxs-lookup"><span data-stu-id="a3ada-132">On the next pane, specify the destination for the recovered System State files and click **Browse** to open Windows Explorer and find the files and folders you want.</span></span> <span data-ttu-id="a3ada-133">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span><span class="sxs-lookup"><span data-stu-id="a3ada-133">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

    ![Recovery options](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="a3ada-135">Verify the details of recovery on the **Confirmation** pane and click **Recover**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-135">Verify the details of recovery on the **Confirmation** pane and click **Recover**.</span></span>

   ![click Recover to acknowledge the recover action](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="a3ada-137">Copy the *WindowsImageBackup* directory in the Recovery destination to a non-critical volume of the server.</span><span class="sxs-lookup"><span data-stu-id="a3ada-137">Copy the *WindowsImageBackup* directory in the Recovery destination to a non-critical volume of the server.</span></span> <span data-ttu-id="a3ada-138">Usually, the Windows OS volume is the critical volume.</span><span class="sxs-lookup"><span data-stu-id="a3ada-138">Usually, the Windows OS volume is the critical volume.</span></span>

10. <span data-ttu-id="a3ada-139">Once the recovery is successful, follow the steps in the section, [Apply restored System State files to the Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), to complete the System State recovery process.</span><span class="sxs-lookup"><span data-stu-id="a3ada-139">Once the recovery is successful, follow the steps in the section, [Apply restored System State files to the Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), to complete the System State recovery process.</span></span>

## <a name="recover-system-state-files-to-an-alternate-server"></a><span data-ttu-id="a3ada-140">Recover System State files to an alternate server</span><span class="sxs-lookup"><span data-stu-id="a3ada-140">Recover System State files to an alternate server</span></span>

<span data-ttu-id="a3ada-141">If your Windows Server is corrupted or inaccessible, and you want to restore it to a stable state by recovering the Windows Server System State, you can restore the corrupted server's System State from another server.</span><span class="sxs-lookup"><span data-stu-id="a3ada-141">If your Windows Server is corrupted or inaccessible, and you want to restore it to a stable state by recovering the Windows Server System State, you can restore the corrupted server's System State from another server.</span></span> <span data-ttu-id="a3ada-142">Use the following steps to the restore System State on a separate server.</span><span class="sxs-lookup"><span data-stu-id="a3ada-142">Use the following steps to the restore System State on a separate server.</span></span>  

<span data-ttu-id="a3ada-143">The terminology used in these steps includes:</span><span class="sxs-lookup"><span data-stu-id="a3ada-143">The terminology used in these steps includes:</span></span>

- <span data-ttu-id="a3ada-144">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span><span class="sxs-lookup"><span data-stu-id="a3ada-144">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="a3ada-145">*Target machine* – The machine to which the data is being recovered.</span><span class="sxs-lookup"><span data-stu-id="a3ada-145">*Target machine* – The machine to which the data is being recovered.</span></span>
- <span data-ttu-id="a3ada-146">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span><span class="sxs-lookup"><span data-stu-id="a3ada-146">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="a3ada-147">Backups taken from one machine cannot be restored to a machine running an earlier version of the operating system.</span><span class="sxs-lookup"><span data-stu-id="a3ada-147">Backups taken from one machine cannot be restored to a machine running an earlier version of the operating system.</span></span> <span data-ttu-id="a3ada-148">For example, backups taken from a Windows Server 2016 machine can't be restored to Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="a3ada-148">For example, backups taken from a Windows Server 2016 machine can't be restored to Windows Server 2012 R2.</span></span> <span data-ttu-id="a3ada-149">However, the inverse is possible.</span><span class="sxs-lookup"><span data-stu-id="a3ada-149">However, the inverse is possible.</span></span> <span data-ttu-id="a3ada-150">You can use backups from Windows Server 2012 R2 to restore Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a3ada-150">You can use backups from Windows Server 2012 R2 to restore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="a3ada-151">Open the **Microsoft Azure Backup** snap-in on the *Target machine*.</span><span class="sxs-lookup"><span data-stu-id="a3ada-151">Open the **Microsoft Azure Backup** snap-in on the *Target machine*.</span></span>
2. <span data-ttu-id="a3ada-152">Ensure that the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="a3ada-152">Ensure that the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>
3. <span data-ttu-id="a3ada-153">Click **Recover Data** to initiate the workflow.</span><span class="sxs-lookup"><span data-stu-id="a3ada-153">Click **Recover Data** to initiate the workflow.</span></span>
4. <span data-ttu-id="a3ada-154">Select **Another server**</span><span class="sxs-lookup"><span data-stu-id="a3ada-154">Select **Another server**</span></span>

    ![Another Server](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="a3ada-156">Provide the vault credential file that corresponds to the *Sample vault*.</span><span class="sxs-lookup"><span data-stu-id="a3ada-156">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="a3ada-157">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a3ada-157">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="a3ada-158">Once the vault credential file is provided, the Recovery Services vault associated with the vault credential file appears.</span><span class="sxs-lookup"><span data-stu-id="a3ada-158">Once the vault credential file is provided, the Recovery Services vault associated with the vault credential file appears.</span></span>

6. <span data-ttu-id="a3ada-159">On the Select Backup Server pane, select the *Source machine* from the list of displayed machines.</span><span class="sxs-lookup"><span data-stu-id="a3ada-159">On the Select Backup Server pane, select the *Source machine* from the list of displayed machines.</span></span>
7. <span data-ttu-id="a3ada-160">On the Select Recovery Mode pane, choose **System State** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-160">On the Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="a3ada-162">On the Calendar in the **Select Volume and Date** pane, select a recovery point.</span><span class="sxs-lookup"><span data-stu-id="a3ada-162">On the Calendar in the **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="a3ada-163">You can restore from any recovery point in time.</span><span class="sxs-lookup"><span data-stu-id="a3ada-163">You can restore from any recovery point in time.</span></span> <span data-ttu-id="a3ada-164">Dates in **bold** indicate the availability of at least one recovery point.</span><span class="sxs-lookup"><span data-stu-id="a3ada-164">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="a3ada-165">Once  you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="a3ada-165">Once  you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span> 

    ![Search items](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="a3ada-167">Once you have chosen the recovery point to restore, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-167">Once you have chosen the recovery point to restore, click **Next**.</span></span>

10. <span data-ttu-id="a3ada-168">On the **Select System State Recovery Mode** pane, specify the destination where you want System State files to be recovered, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-168">On the **Select System State Recovery Mode** pane, specify the destination where you want System State files to be recovered, then click **Next**.</span></span>

    ![Encryption](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="a3ada-170">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span><span class="sxs-lookup"><span data-stu-id="a3ada-170">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

11. <span data-ttu-id="a3ada-171">Verify the details of recovery on the Confirmation pane, and click **Recover**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-171">Verify the details of recovery on the Confirmation pane, and click **Recover**.</span></span> 

    ![click the Recover button to confirm the recovery process](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="a3ada-173">Copy the *WindowsImageBackup* directory to a non-critical volume of the server (for example D:\).</span><span class="sxs-lookup"><span data-stu-id="a3ada-173">Copy the *WindowsImageBackup* directory to a non-critical volume of the server (for example D:\).</span></span> <span data-ttu-id="a3ada-174">Usually the Windows OS volume is the critical volume.</span><span class="sxs-lookup"><span data-stu-id="a3ada-174">Usually the Windows OS volume is the critical volume.</span></span>

13. <span data-ttu-id="a3ada-175">To complete the recovery process, use the following section to [apply the restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="a3ada-175">To complete the recovery process, use the following section to [apply the restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="a3ada-176">Apply restored System State on a Windows Server</span><span class="sxs-lookup"><span data-stu-id="a3ada-176">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="a3ada-177">Once you have recovered System State as files using Azure Recovery Services Agent, use the Windows Server Backup utility to apply the recovered System State to Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3ada-177">Once you have recovered System State as files using Azure Recovery Services Agent, use the Windows Server Backup utility to apply the recovered System State to Windows Server.</span></span> <span data-ttu-id="a3ada-178">The Windows Server Backup utility is already available on the server.</span><span class="sxs-lookup"><span data-stu-id="a3ada-178">The Windows Server Backup utility is already available on the server.</span></span> <span data-ttu-id="a3ada-179">The following steps explain how to apply the recovered System State.</span><span class="sxs-lookup"><span data-stu-id="a3ada-179">The following steps explain how to apply the recovered System State.</span></span>

1. <span data-ttu-id="a3ada-180">Use the following commands to reboot your server in *Directory Services Repair Mode*.</span><span class="sxs-lookup"><span data-stu-id="a3ada-180">Use the following commands to reboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="a3ada-181">In an elevated command prompt:</span><span class="sxs-lookup"><span data-stu-id="a3ada-181">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="a3ada-182">After the reboot, open the Windows Server Backup snap-in.</span><span class="sxs-lookup"><span data-stu-id="a3ada-182">After the reboot, open the Windows Server Backup snap-in.</span></span> <span data-ttu-id="a3ada-183">If you don't know where the snap-in was installed, search the computer or server for **Windows Server Backup**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-183">If you don't know where the snap-in was installed, search the computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="a3ada-184">The desktop app appears in the search results.</span><span class="sxs-lookup"><span data-stu-id="a3ada-184">The desktop app appears in the search results.</span></span>

3. <span data-ttu-id="a3ada-185">In the snap-in, select **Local Backup**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-185">In the snap-in, select **Local Backup**.</span></span>

    ![select Local Backup to restore from there](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="a3ada-187">On the Local Backup console, in the **Actions Pane**, click **Recover** to open the Recovery Wizard.</span><span class="sxs-lookup"><span data-stu-id="a3ada-187">On the Local Backup console, in the **Actions Pane**, click **Recover** to open the Recovery Wizard.</span></span>

5. <span data-ttu-id="a3ada-188">Select the option, **A backup stored in another location**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-188">Select the option, **A backup stored in another location**, and click **Next**.</span></span>

   ![choose to recover to a different server](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="a3ada-190">When specifying the location type, select **Remote shared folder** if your System State backup was recovered to another server.</span><span class="sxs-lookup"><span data-stu-id="a3ada-190">When specifying the location type, select **Remote shared folder** if your System State backup was recovered to another server.</span></span> <span data-ttu-id="a3ada-191">If your System State was recovered locally, then select **Local drives**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-191">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![select whether to recovery from local server or another](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="a3ada-193">Enter the path to the *WindowsImageBackup* directory, or choose the local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of the System State files recovery using Azure Recovery Services Agent and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-193">Enter the path to the *WindowsImageBackup* directory, or choose the local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of the System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![path to the shared file](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="a3ada-195">Select the System State version that you want to restore, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-195">Select the System State version that you want to restore, and click **Next**.</span></span>

9. <span data-ttu-id="a3ada-196">In the Select Recovery Type pane, select **System State** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-196">In the Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="a3ada-197">For the location of the System State Recovery, select **Original Location**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3ada-197">For the location of the System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="a3ada-198">Review the confirmation details, verify the reboot settings, and click **Recover** to applly the restored System State files.</span><span class="sxs-lookup"><span data-stu-id="a3ada-198">Review the confirmation details, verify the reboot settings, and click **Recover** to applly the restored System State files.</span></span>

    ![launch the restore System State files](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="a3ada-200">Special considerations for System State recovery on Active Directory server</span><span class="sxs-lookup"><span data-stu-id="a3ada-200">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="a3ada-201">System State backup includes Active Directory data.</span><span class="sxs-lookup"><span data-stu-id="a3ada-201">System State backup includes Active Directory data.</span></span> <span data-ttu-id="a3ada-202">Use the following steps to restore Active Directory Domain Service (AD DS) from its current state to a previous state.</span><span class="sxs-lookup"><span data-stu-id="a3ada-202">Use the following steps to restore Active Directory Domain Service (AD DS) from its current state to a previous state.</span></span>

1. <span data-ttu-id="a3ada-203">Restart the domain controller in Directory Services Restore Mode (DSRM).</span><span class="sxs-lookup"><span data-stu-id="a3ada-203">Restart the domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="a3ada-204">Follow the steps [here](https://technet.microsoft.com/library/cc794755(v=ws.10).aspx) to use Windows Server Backup cmdlets to recover AD DS.</span><span class="sxs-lookup"><span data-stu-id="a3ada-204">Follow the steps [here](https://technet.microsoft.com/library/cc794755(v=ws.10).aspx) to use Windows Server Backup cmdlets to recover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="a3ada-205">Troubleshoot failed System State restore</span><span class="sxs-lookup"><span data-stu-id="a3ada-205">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="a3ada-206">If the previous process of applying System State does not complete successfully, use the Windows Recovery Environment (Win RE) to recover your Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3ada-206">If the previous process of applying System State does not complete successfully, use the Windows Recovery Environment (Win RE) to recover your Windows Server.</span></span> <span data-ttu-id="a3ada-207">The following steps explain how to recover using Win RE.</span><span class="sxs-lookup"><span data-stu-id="a3ada-207">The following steps explain how to recover using Win RE.</span></span> <span data-ttu-id="a3ada-208">Use This option only if Windows Server does not boot normally after a System State restore.</span><span class="sxs-lookup"><span data-stu-id="a3ada-208">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="a3ada-209">The following process erases non-system data, use caution.</span><span class="sxs-lookup"><span data-stu-id="a3ada-209">The following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="a3ada-210">Boot your Windows Server into the Windows Recovery Environment (Win RE).</span><span class="sxs-lookup"><span data-stu-id="a3ada-210">Boot your Windows Server into the Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="a3ada-211">Select Troubleshoot from the three available options.</span><span class="sxs-lookup"><span data-stu-id="a3ada-211">Select Troubleshoot from the three available options.</span></span>

    ![opening menu](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="a3ada-213">From the **Advanced Options** screen, select **Command Prompt** and provide the server administrator username and password.</span><span class="sxs-lookup"><span data-stu-id="a3ada-213">From the **Advanced Options** screen, select **Command Prompt** and provide the server administrator username and password.</span></span>

   ![opening menu](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="a3ada-215">Provide the server administrator username and password.</span><span class="sxs-lookup"><span data-stu-id="a3ada-215">Provide the server administrator username and password.</span></span>

    ![opening menu](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="a3ada-217">When you open the command prompt in administrator mode, run following command to get the System State backup versions.</span><span class="sxs-lookup"><span data-stu-id="a3ada-217">When you open the command prompt in administrator mode, run following command to get the System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![get System State backup versions](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="a3ada-219">Run the following command to get all volumes available in the backup.</span><span class="sxs-lookup"><span data-stu-id="a3ada-219">Run the following command to get all volumes available in the backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![get System State backup versions](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="a3ada-221">The following command recovers all volumes that are part of the System State Backup.</span><span class="sxs-lookup"><span data-stu-id="a3ada-221">The following command recovers all volumes that are part of the System State Backup.</span></span> <span data-ttu-id="a3ada-222">Note that this step recovers only the critical volumes that are part of the System State.</span><span class="sxs-lookup"><span data-stu-id="a3ada-222">Note that this step recovers only the critical volumes that are part of the System State.</span></span> <span data-ttu-id="a3ada-223">All non-System data is erased.</span><span class="sxs-lookup"><span data-stu-id="a3ada-223">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![get System State backup versions](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="a3ada-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3ada-225">Next steps</span></span>
* <span data-ttu-id="a3ada-226">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="a3ada-226">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
