---
title: Back up SQL Server workloads on Azure Stack
description: Use Azure Backup Server to protect SQL Server workload on Azure Stack.
services: backup
author: pvrk
manager: Shivamg
ms.service: backup
ms.topic: conceptual
ms.date: 6/8/2018
ms.author: pullabhk
ms.openlocfilehash: ca7da7ab048b6f7bfdba81aac9bc7702b20ff967
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866026"
---
# <a name="back-up-sql-server-on-stack"></a><span data-ttu-id="611e5-103">Back up SQL Server on Stack</span><span class="sxs-lookup"><span data-stu-id="611e5-103">Back up SQL Server on Stack</span></span>
<span data-ttu-id="611e5-104">Use this article to configure Microsoft Azure Backup Server (MABS) to protect SQL Server databases on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="611e5-104">Use this article to configure Microsoft Azure Backup Server (MABS) to protect SQL Server databases on Azure Stack.</span></span>

<span data-ttu-id="611e5-105">The management of SQL Server database backup to Azure and recovery from Azure involves three steps:</span><span class="sxs-lookup"><span data-stu-id="611e5-105">The management of SQL Server database backup to Azure and recovery from Azure involves three steps:</span></span>

1. <span data-ttu-id="611e5-106">Create a backup policy to protect SQL Server databases</span><span class="sxs-lookup"><span data-stu-id="611e5-106">Create a backup policy to protect SQL Server databases</span></span>
2. <span data-ttu-id="611e5-107">Create on-demand backup copies</span><span class="sxs-lookup"><span data-stu-id="611e5-107">Create on-demand backup copies</span></span>
3. <span data-ttu-id="611e5-108">Recover the database from Disks, and from Azure</span><span class="sxs-lookup"><span data-stu-id="611e5-108">Recover the database from Disks, and from Azure</span></span>

## <a name="before-you-start"></a><span data-ttu-id="611e5-109">Before you start</span><span class="sxs-lookup"><span data-stu-id="611e5-109">Before you start</span></span>

<span data-ttu-id="611e5-110">[Install and prepare Azure Backup Server](backup-mabs-install-azure-stack.md).</span><span class="sxs-lookup"><span data-stu-id="611e5-110">[Install and prepare Azure Backup Server](backup-mabs-install-azure-stack.md).</span></span>

## <a name="create-a-backup-policy-to-protect-sql-server-databases-to-azure"></a><span data-ttu-id="611e5-111">Create a backup policy to protect SQL Server databases to Azure</span><span class="sxs-lookup"><span data-stu-id="611e5-111">Create a backup policy to protect SQL Server databases to Azure</span></span>
1. <span data-ttu-id="611e5-112">On the Azure Backup Server UI, click the **Protection** workspace.</span><span class="sxs-lookup"><span data-stu-id="611e5-112">On the Azure Backup Server UI, click the **Protection** workspace.</span></span>

2. <span data-ttu-id="611e5-113">On the tool ribbon, click **New** to create a new protection group.</span><span class="sxs-lookup"><span data-stu-id="611e5-113">On the tool ribbon, click **New** to create a new protection group.</span></span>

    ![Create Protection Group](./media/backup-azure-backup-sql/protection-group.png)

    <span data-ttu-id="611e5-115">Azure Backup Server starts the Protection Group wizard, which leads you through creating a **Protection Group**.</span><span class="sxs-lookup"><span data-stu-id="611e5-115">Azure Backup Server starts the Protection Group wizard, which leads you through creating a **Protection Group**.</span></span> <span data-ttu-id="611e5-116">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-116">Click **Next**.</span></span>

3. <span data-ttu-id="611e5-117">In the **Select Protection Group Type** screen, select **Servers**.</span><span class="sxs-lookup"><span data-stu-id="611e5-117">In the **Select Protection Group Type** screen, select **Servers**.</span></span>

    ![Select Protection Group Type - 'Servers'](./media/backup-azure-backup-sql/pg-servers.png)

4. <span data-ttu-id="611e5-119">In the **Select Group Members** screen, the Available members list displays the various data sources.</span><span class="sxs-lookup"><span data-stu-id="611e5-119">In the **Select Group Members** screen, the Available members list displays the various data sources.</span></span> <span data-ttu-id="611e5-120">Click **+** to expand a folder and reveal the subfolders.</span><span class="sxs-lookup"><span data-stu-id="611e5-120">Click **+** to expand a folder and reveal the subfolders.</span></span> <span data-ttu-id="611e5-121">Click the checkbox to select an item.</span><span class="sxs-lookup"><span data-stu-id="611e5-121">Click the checkbox to select an item.</span></span>

    ![Select SQL DB](./media/backup-azure-backup-sql/pg-databases.png)

    <span data-ttu-id="611e5-123">All selected items appear in the Selected members list.</span><span class="sxs-lookup"><span data-stu-id="611e5-123">All selected items appear in the Selected members list.</span></span> <span data-ttu-id="611e5-124">After selecting the servers or databases you want to protect, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-124">After selecting the servers or databases you want to protect, click **Next**.</span></span>

5. <span data-ttu-id="611e5-125">In the **Select Data Protection Method** screen, provide a name for the protection group and select the **I want online Protection** checkbox.</span><span class="sxs-lookup"><span data-stu-id="611e5-125">In the **Select Data Protection Method** screen, provide a name for the protection group and select the **I want online Protection** checkbox.</span></span>

    ![Data Protection Method - short-term disk & Online Azure](./media/backup-azure-backup-sql/pg-name.png)

6. <span data-ttu-id="611e5-127">In the **Specify Short-Term Goals** screen, include the necessary inputs to create backup points to disk, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-127">In the **Specify Short-Term Goals** screen, include the necessary inputs to create backup points to disk, and click **Next**.</span></span>

    <span data-ttu-id="611e5-128">In the example, **Retention range** is **5 days**, **Synchronization frequency** is once every **15 minutes**, which is the backup frequency.</span><span class="sxs-lookup"><span data-stu-id="611e5-128">In the example, **Retention range** is **5 days**, **Synchronization frequency** is once every **15 minutes**, which is the backup frequency.</span></span> <span data-ttu-id="611e5-129">**Express Full Backup** is set to **8:00 P.M**.</span><span class="sxs-lookup"><span data-stu-id="611e5-129">**Express Full Backup** is set to **8:00 P.M**.</span></span>

    ![Short-term goals](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > <span data-ttu-id="611e5-131">In the example shown, at 8:00 PM every day a backup point is created by transferring the modified data from the previous day’s 8:00 PM backup point.</span><span class="sxs-lookup"><span data-stu-id="611e5-131">In the example shown, at 8:00 PM every day a backup point is created by transferring the modified data from the previous day’s 8:00 PM backup point.</span></span> <span data-ttu-id="611e5-132">This process is called **Express Full Backup**.</span><span class="sxs-lookup"><span data-stu-id="611e5-132">This process is called **Express Full Backup**.</span></span> <span data-ttu-id="611e5-133">Transaction logs are synchronized every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="611e5-133">Transaction logs are synchronized every 15 minutes.</span></span> <span data-ttu-id="611e5-134">If you need to recover the database at 9:00 PM, the point is created from the logs from the last express full backup point (8PM in this case).</span><span class="sxs-lookup"><span data-stu-id="611e5-134">If you need to recover the database at 9:00 PM, the point is created from the logs from the last express full backup point (8PM in this case).</span></span>
   >
   >

7. <span data-ttu-id="611e5-135">On the **Review disk allocation** screen, verify the overall storage space available, and the potential disk space.</span><span class="sxs-lookup"><span data-stu-id="611e5-135">On the **Review disk allocation** screen, verify the overall storage space available, and the potential disk space.</span></span> <span data-ttu-id="611e5-136">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-136">Click **Next**.</span></span>

8. <span data-ttu-id="611e5-137">In the **Choose Replica Creation Method**, choose how to create your first recovery point.</span><span class="sxs-lookup"><span data-stu-id="611e5-137">In the **Choose Replica Creation Method**, choose how to create your first recovery point.</span></span> <span data-ttu-id="611e5-138">You can transfer the initial backup manually (off network) to avoid bandwidth congestion or over the network.</span><span class="sxs-lookup"><span data-stu-id="611e5-138">You can transfer the initial backup manually (off network) to avoid bandwidth congestion or over the network.</span></span> <span data-ttu-id="611e5-139">If you choose to wait to transfer the first backup, you can specify the time for the initial transfer.</span><span class="sxs-lookup"><span data-stu-id="611e5-139">If you choose to wait to transfer the first backup, you can specify the time for the initial transfer.</span></span> <span data-ttu-id="611e5-140">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-140">Click **Next**.</span></span>

    ![Initial replication method](./media/backup-azure-backup-sql/pg-manual.png)

    <span data-ttu-id="611e5-142">The initial backup copy requires transferring the entire data source (SQL Server database) from production server (SQL Server machine) to Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="611e5-142">The initial backup copy requires transferring the entire data source (SQL Server database) from production server (SQL Server machine) to Azure Backup Server.</span></span> <span data-ttu-id="611e5-143">This data might be large, and transferring the data over the network could exceed bandwidth.</span><span class="sxs-lookup"><span data-stu-id="611e5-143">This data might be large, and transferring the data over the network could exceed bandwidth.</span></span> <span data-ttu-id="611e5-144">For this reason, you can choose to transfer the initial backup: **Manually** (using removable media) to avoid bandwidth congestion, or **Automatically over the network** (at a specified time).</span><span class="sxs-lookup"><span data-stu-id="611e5-144">For this reason, you can choose to transfer the initial backup: **Manually** (using removable media) to avoid bandwidth congestion, or **Automatically over the network** (at a specified time).</span></span>

    <span data-ttu-id="611e5-145">Once the initial backup is complete, the rest of the backups are incremental backups on the initial backup copy.</span><span class="sxs-lookup"><span data-stu-id="611e5-145">Once the initial backup is complete, the rest of the backups are incremental backups on the initial backup copy.</span></span> <span data-ttu-id="611e5-146">Incremental backups tend to be small and are easily transferred across the network.</span><span class="sxs-lookup"><span data-stu-id="611e5-146">Incremental backups tend to be small and are easily transferred across the network.</span></span>

9. <span data-ttu-id="611e5-147">Choose when you want the consistency check to run and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-147">Choose when you want the consistency check to run and click **Next**.</span></span>

    ![Consistency check](./media/backup-azure-backup-sql/pg-consistent.png)

    <span data-ttu-id="611e5-149">Azure Backup Server performs a consistency check on the integrity of the backup point.</span><span class="sxs-lookup"><span data-stu-id="611e5-149">Azure Backup Server performs a consistency check on the integrity of the backup point.</span></span> <span data-ttu-id="611e5-150">Azure Backup Server calculates the checksum of the backup file on the production server (SQL Server machine in this scenario) and the backed-up data for that file.</span><span class="sxs-lookup"><span data-stu-id="611e5-150">Azure Backup Server calculates the checksum of the backup file on the production server (SQL Server machine in this scenario) and the backed-up data for that file.</span></span> <span data-ttu-id="611e5-151">If there is a conflict, it's assumed the backed-up file on Azure Backup Server is corrupt.</span><span class="sxs-lookup"><span data-stu-id="611e5-151">If there is a conflict, it's assumed the backed-up file on Azure Backup Server is corrupt.</span></span> <span data-ttu-id="611e5-152">Azure Backup Server rectifies the backed-up data by sending the blocks corresponding to the checksum mismatch.</span><span class="sxs-lookup"><span data-stu-id="611e5-152">Azure Backup Server rectifies the backed-up data by sending the blocks corresponding to the checksum mismatch.</span></span> <span data-ttu-id="611e5-153">Because consistency checks are performance-intensive, you can schedule the consistency check or run it automatically.</span><span class="sxs-lookup"><span data-stu-id="611e5-153">Because consistency checks are performance-intensive, you can schedule the consistency check or run it automatically.</span></span>

10. <span data-ttu-id="611e5-154">To specify online protection of the datasources, select the databases to be protected to Azure and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-154">To specify online protection of the datasources, select the databases to be protected to Azure and click **Next**.</span></span>

    ![Select datasources](./media/backup-azure-backup-sql/pg-sqldatabases.png)

11. <span data-ttu-id="611e5-156">Choose backup schedules and retention policies that suit the organization policies.</span><span class="sxs-lookup"><span data-stu-id="611e5-156">Choose backup schedules and retention policies that suit the organization policies.</span></span>

    ![Schedule and Retention](./media/backup-azure-backup-sql/pg-schedule.png)

    <span data-ttu-id="611e5-158">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen)</span><span class="sxs-lookup"><span data-stu-id="611e5-158">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen)</span></span>

    > [!NOTE]
    > <span data-ttu-id="611e5-159">It’s a good practice to have a few short-term recovery points on disk, for quick recovery.</span><span class="sxs-lookup"><span data-stu-id="611e5-159">It’s a good practice to have a few short-term recovery points on disk, for quick recovery.</span></span> <span data-ttu-id="611e5-160">These recovery points are used for operational recovery.</span><span class="sxs-lookup"><span data-stu-id="611e5-160">These recovery points are used for operational recovery.</span></span> <span data-ttu-id="611e5-161">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span><span class="sxs-lookup"><span data-stu-id="611e5-161">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span></span>
    >
    >

    <span data-ttu-id="611e5-162">**Best Practice**: If you schedule backups to Azure to start after the local disk backups complete, the latest disk backups are always copied to Azure.</span><span class="sxs-lookup"><span data-stu-id="611e5-162">**Best Practice**: If you schedule backups to Azure to start after the local disk backups complete, the latest disk backups are always copied to Azure.</span></span>

12. <span data-ttu-id="611e5-163">Choose the retention policy schedule.</span><span class="sxs-lookup"><span data-stu-id="611e5-163">Choose the retention policy schedule.</span></span> <span data-ttu-id="611e5-164">The details on how the retention policy works are provided at [Use Azure Backup to replace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="611e5-164">The details on how the retention policy works are provided at [Use Azure Backup to replace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span></span>

    ![Retention Policy](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    <span data-ttu-id="611e5-166">In this example:</span><span class="sxs-lookup"><span data-stu-id="611e5-166">In this example:</span></span>

    * <span data-ttu-id="611e5-167">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen) and are retained for 180 days.</span><span class="sxs-lookup"><span data-stu-id="611e5-167">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen) and are retained for 180 days.</span></span>
    * <span data-ttu-id="611e5-168">The backup on Saturday at 12:00 P.M.</span><span class="sxs-lookup"><span data-stu-id="611e5-168">The backup on Saturday at 12:00 P.M.</span></span> <span data-ttu-id="611e5-169">is retained for 104 weeks</span><span class="sxs-lookup"><span data-stu-id="611e5-169">is retained for 104 weeks</span></span>
    * <span data-ttu-id="611e5-170">The backup on Last Saturday at 12:00 P.M.</span><span class="sxs-lookup"><span data-stu-id="611e5-170">The backup on Last Saturday at 12:00 P.M.</span></span> <span data-ttu-id="611e5-171">is retained for 60 months</span><span class="sxs-lookup"><span data-stu-id="611e5-171">is retained for 60 months</span></span>
    * <span data-ttu-id="611e5-172">The backup on Last Saturday of March at 12:00 P.M.</span><span class="sxs-lookup"><span data-stu-id="611e5-172">The backup on Last Saturday of March at 12:00 P.M.</span></span> <span data-ttu-id="611e5-173">is retained for 10 years</span><span class="sxs-lookup"><span data-stu-id="611e5-173">is retained for 10 years</span></span>
13. <span data-ttu-id="611e5-174">Click **Next** and select the appropriate option for transferring the initial backup copy to Azure.</span><span class="sxs-lookup"><span data-stu-id="611e5-174">Click **Next** and select the appropriate option for transferring the initial backup copy to Azure.</span></span> <span data-ttu-id="611e5-175">You can choose **Automatically over the network**</span><span class="sxs-lookup"><span data-stu-id="611e5-175">You can choose **Automatically over the network**</span></span>

14. <span data-ttu-id="611e5-176">Once you review the policy details in the **Summary** screen, click **Create group** to complete the workflow.</span><span class="sxs-lookup"><span data-stu-id="611e5-176">Once you review the policy details in the **Summary** screen, click **Create group** to complete the workflow.</span></span> <span data-ttu-id="611e5-177">You can click **Close** and monitor the job progress in Monitoring workspace.</span><span class="sxs-lookup"><span data-stu-id="611e5-177">You can click **Close** and monitor the job progress in Monitoring workspace.</span></span>

    ![Creation of Protection Group In-Progress](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a><span data-ttu-id="611e5-179">On-demand backup of a SQL Server database</span><span class="sxs-lookup"><span data-stu-id="611e5-179">On-demand backup of a SQL Server database</span></span>
<span data-ttu-id="611e5-180">While the previous steps created a backup policy, a “recovery point” is created only when the first backup occurs.</span><span class="sxs-lookup"><span data-stu-id="611e5-180">While the previous steps created a backup policy, a “recovery point” is created only when the first backup occurs.</span></span> <span data-ttu-id="611e5-181">Rather than waiting for the scheduler to kick in, the steps below trigger the creation of a recovery point manually.</span><span class="sxs-lookup"><span data-stu-id="611e5-181">Rather than waiting for the scheduler to kick in, the steps below trigger the creation of a recovery point manually.</span></span>

1. <span data-ttu-id="611e5-182">Wait until the protection group status shows **OK** for the database before creating the recovery point.</span><span class="sxs-lookup"><span data-stu-id="611e5-182">Wait until the protection group status shows **OK** for the database before creating the recovery point.</span></span>

    ![Protection Group Members](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. <span data-ttu-id="611e5-184">Right-click on the database and select **Create Recovery Point**.</span><span class="sxs-lookup"><span data-stu-id="611e5-184">Right-click on the database and select **Create Recovery Point**.</span></span>

    ![Create Online Recovery Point](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. <span data-ttu-id="611e5-186">Choose **Online Protection** in the drop-down menu and click **OK** to start creation of a recovery point in Azure.</span><span class="sxs-lookup"><span data-stu-id="611e5-186">Choose **Online Protection** in the drop-down menu and click **OK** to start creation of a recovery point in Azure.</span></span>

    ![Create recovery point](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. <span data-ttu-id="611e5-188">View the job progress in the **Monitoring** workspace.</span><span class="sxs-lookup"><span data-stu-id="611e5-188">View the job progress in the **Monitoring** workspace.</span></span>

    ![Monitoring console](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a><span data-ttu-id="611e5-190">Recover a SQL Server database from Azure</span><span class="sxs-lookup"><span data-stu-id="611e5-190">Recover a SQL Server database from Azure</span></span>
<span data-ttu-id="611e5-191">The following steps are required to recover a protected entity (SQL Server database) from Azure.</span><span class="sxs-lookup"><span data-stu-id="611e5-191">The following steps are required to recover a protected entity (SQL Server database) from Azure.</span></span>

1. <span data-ttu-id="611e5-192">Open the Azure Backup Server Management Console.</span><span class="sxs-lookup"><span data-stu-id="611e5-192">Open the Azure Backup Server Management Console.</span></span> <span data-ttu-id="611e5-193">Navigate to **Recovery** workspace where you can see the protected servers.</span><span class="sxs-lookup"><span data-stu-id="611e5-193">Navigate to **Recovery** workspace where you can see the protected servers.</span></span> <span data-ttu-id="611e5-194">Browse the required database (in this case ReportServer$MSDPM2012).</span><span class="sxs-lookup"><span data-stu-id="611e5-194">Browse the required database (in this case ReportServer$MSDPM2012).</span></span> <span data-ttu-id="611e5-195">Select a **Recovery from** time that is specified as an **Online** point.</span><span class="sxs-lookup"><span data-stu-id="611e5-195">Select a **Recovery from** time that is specified as an **Online** point.</span></span>

    ![Select Recovery point](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. <span data-ttu-id="611e5-197">Right-click the database name and click **Recover**.</span><span class="sxs-lookup"><span data-stu-id="611e5-197">Right-click the database name and click **Recover**.</span></span>

    ![Recover from Azure](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. <span data-ttu-id="611e5-199">MABS shows the details of the recovery point.</span><span class="sxs-lookup"><span data-stu-id="611e5-199">MABS shows the details of the recovery point.</span></span> <span data-ttu-id="611e5-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-200">Click **Next**.</span></span> <span data-ttu-id="611e5-201">To overwrite the database, select the recovery type **Recover to original instance of SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="611e5-201">To overwrite the database, select the recovery type **Recover to original instance of SQL Server**.</span></span> <span data-ttu-id="611e5-202">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-202">Click **Next**.</span></span>

    ![Recover to Original Location](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    <span data-ttu-id="611e5-204">In this example, MABS recovers the database to another SQL Server instance, or to a standalone network folder.</span><span class="sxs-lookup"><span data-stu-id="611e5-204">In this example, MABS recovers the database to another SQL Server instance, or to a standalone network folder.</span></span>

4. <span data-ttu-id="611e5-205">In the **Specify Recovery options** screen, you can select the recovery options like Network bandwidth usage throttling to throttle the bandwidth used by recovery.</span><span class="sxs-lookup"><span data-stu-id="611e5-205">In the **Specify Recovery options** screen, you can select the recovery options like Network bandwidth usage throttling to throttle the bandwidth used by recovery.</span></span> <span data-ttu-id="611e5-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="611e5-206">Click **Next**.</span></span>

5. <span data-ttu-id="611e5-207">In the **Summary** screen, you see all the recovery configurations provided so far.</span><span class="sxs-lookup"><span data-stu-id="611e5-207">In the **Summary** screen, you see all the recovery configurations provided so far.</span></span> <span data-ttu-id="611e5-208">Click **Recover**.</span><span class="sxs-lookup"><span data-stu-id="611e5-208">Click **Recover**.</span></span>

    <span data-ttu-id="611e5-209">The Recovery status shows the database being recovered.</span><span class="sxs-lookup"><span data-stu-id="611e5-209">The Recovery status shows the database being recovered.</span></span> <span data-ttu-id="611e5-210">You can click **Close** to close the wizard and view the progress in the **Monitoring** workspace.</span><span class="sxs-lookup"><span data-stu-id="611e5-210">You can click **Close** to close the wizard and view the progress in the **Monitoring** workspace.</span></span>

    ![Initiate recovery process](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    <span data-ttu-id="611e5-212">Once the recovery is completed, the restored database is application consistent.</span><span class="sxs-lookup"><span data-stu-id="611e5-212">Once the recovery is completed, the restored database is application consistent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="611e5-213">Next Steps</span><span class="sxs-lookup"><span data-stu-id="611e5-213">Next Steps</span></span>

<span data-ttu-id="611e5-214">See the [Backup files and application](backup-mabs-files-applications-azure-stack.md) article.</span><span class="sxs-lookup"><span data-stu-id="611e5-214">See the [Backup files and application](backup-mabs-files-applications-azure-stack.md) article.</span></span>
<span data-ttu-id="611e5-215">See the [Backup SharePoint on Azure Stack](backup-mabs-sharepoint-azure-stack.md) article.</span><span class="sxs-lookup"><span data-stu-id="611e5-215">See the [Backup SharePoint on Azure Stack](backup-mabs-sharepoint-azure-stack.md) article.</span></span>
