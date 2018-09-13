---
title: Azure Backup for SQL Server workloads using DPM | Microsoft Docs
description: An introduction to backing up SQL Server databases using the Azure Backup service
services: backup
documentationcenter: ''
author: adigan
manager: Nkolli
editor: ''
ms.assetid: 59df5bec-d959-457d-8731-7b20f7f1013e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: d5e4222815204a085ad1d0a70e8ad961e196b909
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44541005"
---
# <a name="back-up-sql-server-to-azure-as-a-dpm-workload"></a><span data-ttu-id="e345c-103">Back up SQL Server to Azure as a DPM workload</span><span class="sxs-lookup"><span data-stu-id="e345c-103">Back up SQL Server to Azure as a DPM workload</span></span>
<span data-ttu-id="e345c-104">This article leads you through the configuration steps for backup of SQL Server databases using Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="e345c-104">This article leads you through the configuration steps for backup of SQL Server databases using Azure Backup.</span></span>

<span data-ttu-id="e345c-105">To back up SQL Server databases to Azure, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="e345c-105">To back up SQL Server databases to Azure, you need an Azure account.</span></span> <span data-ttu-id="e345c-106">If you don’t have an account, you can create a free trial account in just couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="e345c-106">If you don’t have an account, you can create a free trial account in just couple of minutes.</span></span> <span data-ttu-id="e345c-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e345c-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="e345c-108">The management of SQL Server database backup to Azure and recovery from Azure involves three steps:</span><span class="sxs-lookup"><span data-stu-id="e345c-108">The management of SQL Server database backup to Azure and recovery from Azure involves three steps:</span></span>

1. <span data-ttu-id="e345c-109">Create a backup policy to protect SQL Server databases to Azure.</span><span class="sxs-lookup"><span data-stu-id="e345c-109">Create a backup policy to protect SQL Server databases to Azure.</span></span>
2. <span data-ttu-id="e345c-110">Create on-demand backup copies to Azure.</span><span class="sxs-lookup"><span data-stu-id="e345c-110">Create on-demand backup copies to Azure.</span></span>
3. <span data-ttu-id="e345c-111">Recover the database from Azure.</span><span class="sxs-lookup"><span data-stu-id="e345c-111">Recover the database from Azure.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e345c-112">Before you start</span><span class="sxs-lookup"><span data-stu-id="e345c-112">Before you start</span></span>
<span data-ttu-id="e345c-113">Before you begin, ensure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span><span class="sxs-lookup"><span data-stu-id="e345c-113">Before you begin, ensure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="e345c-114">The prerequisites cover tasks such as: creating a backup vault, downloading vault credentials, installing the Azure Backup Agent, and registering the server with the vault.</span><span class="sxs-lookup"><span data-stu-id="e345c-114">The prerequisites cover tasks such as: creating a backup vault, downloading vault credentials, installing the Azure Backup Agent, and registering the server with the vault.</span></span>

## <a name="create-a-backup-policy-to-protect-sql-server-databases-to-azure"></a><span data-ttu-id="e345c-115">Create a backup policy to protect SQL Server databases to Azure</span><span class="sxs-lookup"><span data-stu-id="e345c-115">Create a backup policy to protect SQL Server databases to Azure</span></span>
1. <span data-ttu-id="e345c-116">On the DPM server, click the **Protection** workspace.</span><span class="sxs-lookup"><span data-stu-id="e345c-116">On the DPM server, click the **Protection** workspace.</span></span>
2. <span data-ttu-id="e345c-117">On the tool ribbon, click **New** to create a new protection group.</span><span class="sxs-lookup"><span data-stu-id="e345c-117">On the tool ribbon, click **New** to create a new protection group.</span></span>

    ![Create Protection Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/protection-group.png)
3. <span data-ttu-id="e345c-119">DPM shows the start screen with the guidance on creating a **Protection Group**.</span><span class="sxs-lookup"><span data-stu-id="e345c-119">DPM shows the start screen with the guidance on creating a **Protection Group**.</span></span> <span data-ttu-id="e345c-120">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e345c-120">Click **Next**.</span></span>
4. <span data-ttu-id="e345c-121">Select **Servers**.</span><span class="sxs-lookup"><span data-stu-id="e345c-121">Select **Servers**.</span></span>

    ![Select Protection Group Type - 'Servers'](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-servers.png)
5. <span data-ttu-id="e345c-123">Expand the SQL Server machine where the databases to be backed up are present.</span><span class="sxs-lookup"><span data-stu-id="e345c-123">Expand the SQL Server machine where the databases to be backed up are present.</span></span> <span data-ttu-id="e345c-124">DPM shows various data sources that can be backed up from that server.</span><span class="sxs-lookup"><span data-stu-id="e345c-124">DPM shows various data sources that can be backed up from that server.</span></span> <span data-ttu-id="e345c-125">Expand the **All SQL Shares** and select the databases (in this case we selected ReportServer$MSDPM2012 and ReportServer$MSDPM2012TempDB) to be backed up.</span><span class="sxs-lookup"><span data-stu-id="e345c-125">Expand the **All SQL Shares** and select the databases (in this case we selected ReportServer$MSDPM2012 and ReportServer$MSDPM2012TempDB) to be backed up.</span></span> <span data-ttu-id="e345c-126">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e345c-126">Click **Next**.</span></span>

    ![Select SQL DB](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-databases.png)
6. <span data-ttu-id="e345c-128">Provide a name for the protection group and select the **I want online Protection** checkbox.</span><span class="sxs-lookup"><span data-stu-id="e345c-128">Provide a name for the protection group and select the **I want online Protection** checkbox.</span></span>

    ![Data Protection Method - short term disk & Online Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-name.png)
7. <span data-ttu-id="e345c-130">In the **Specify Short-Term Goals** screen, include the necessary inputs to create backup points to disk.</span><span class="sxs-lookup"><span data-stu-id="e345c-130">In the **Specify Short-Term Goals** screen, include the necessary inputs to create backup points to disk.</span></span>

    <span data-ttu-id="e345c-131">Here we see that **Retention range** is set to *5 days*, **Synchronization frequency** is set to once every *15 minutes* which is the frequency at which backup is taken.</span><span class="sxs-lookup"><span data-stu-id="e345c-131">Here we see that **Retention range** is set to *5 days*, **Synchronization frequency** is set to once every *15 minutes* which is the frequency at which backup is taken.</span></span> <span data-ttu-id="e345c-132">**Express Full Backup** is set to *8:00 P.M*.</span><span class="sxs-lookup"><span data-stu-id="e345c-132">**Express Full Backup** is set to *8:00 P.M*.</span></span>

    ![Short term goals](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > <span data-ttu-id="e345c-134">At 8:00 PM (according to the screen input) a backup point is created every day by transferring the data that has been modified from the previous day’s 8:00 PM backup point.</span><span class="sxs-lookup"><span data-stu-id="e345c-134">At 8:00 PM (according to the screen input) a backup point is created every day by transferring the data that has been modified from the previous day’s 8:00 PM backup point.</span></span> <span data-ttu-id="e345c-135">This process is called **Express Full Backup**.</span><span class="sxs-lookup"><span data-stu-id="e345c-135">This process is called **Express Full Backup**.</span></span> <span data-ttu-id="e345c-136">While the transaction logs are synchronized every 15 minutes, if there is a need to recover the database at 9:00 PM – then the point is created by replaying the logs from the last express full backup point (8pm in this case).</span><span class="sxs-lookup"><span data-stu-id="e345c-136">While the transaction logs are synchronized every 15 minutes, if there is a need to recover the database at 9:00 PM – then the point is created by replaying the logs from the last express full backup point (8pm in this case).</span></span>
   >
   >

8. <span data-ttu-id="e345c-137">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="e345c-137">Click **Next**</span></span>

    <span data-ttu-id="e345c-138">DPM shows the overall storage space available and the potential disk space utilization.</span><span class="sxs-lookup"><span data-stu-id="e345c-138">DPM shows the overall storage space available and the potential disk space utilization.</span></span>

    ![Disk allocation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-storage.png)

    <span data-ttu-id="e345c-140">By default, DPM creates one volume per data source (SQL Server database) which is used for the initial backup copy.</span><span class="sxs-lookup"><span data-stu-id="e345c-140">By default, DPM creates one volume per data source (SQL Server database) which is used for the initial backup copy.</span></span> <span data-ttu-id="e345c-141">Using this approach, the Logical Disk Manager (LDM) limits DPM protection to 300 data sources (SQL Server databases).</span><span class="sxs-lookup"><span data-stu-id="e345c-141">Using this approach, the Logical Disk Manager (LDM) limits DPM protection to 300 data sources (SQL Server databases).</span></span> <span data-ttu-id="e345c-142">To work around this limitation, select the **Co-locate data in DPM Storage Pool**, option.</span><span class="sxs-lookup"><span data-stu-id="e345c-142">To work around this limitation, select the **Co-locate data in DPM Storage Pool**, option.</span></span> <span data-ttu-id="e345c-143">If you use this option, DPM uses a single volume for multiple data sources, which allows DPM to protect up to 2000 SQL databases.</span><span class="sxs-lookup"><span data-stu-id="e345c-143">If you use this option, DPM uses a single volume for multiple data sources, which allows DPM to protect up to 2000 SQL databases.</span></span>

    <span data-ttu-id="e345c-144">If **Automatically grow the volumes** option is selected, DPM can account for the increased backup volume as the production data grows.</span><span class="sxs-lookup"><span data-stu-id="e345c-144">If **Automatically grow the volumes** option is selected, DPM can account for the increased backup volume as the production data grows.</span></span> <span data-ttu-id="e345c-145">If **Automatically grow the volumes** option is not selected, DPM limits the backup storage used to the data sources in the protection group.</span><span class="sxs-lookup"><span data-stu-id="e345c-145">If **Automatically grow the volumes** option is not selected, DPM limits the backup storage used to the data sources in the protection group.</span></span>
9. <span data-ttu-id="e345c-146">Administrators are given the choice of transferring this initial backup manually (off network) to avoid bandwidth congestion or over the network.</span><span class="sxs-lookup"><span data-stu-id="e345c-146">Administrators are given the choice of transferring this initial backup manually (off network) to avoid bandwidth congestion or over the network.</span></span> <span data-ttu-id="e345c-147">They can also configure the time at which the initial transfer can happen.</span><span class="sxs-lookup"><span data-stu-id="e345c-147">They can also configure the time at which the initial transfer can happen.</span></span> <span data-ttu-id="e345c-148">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e345c-148">Click **Next**.</span></span>

    ![Initial replication method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-manual.png)

    <span data-ttu-id="e345c-150">The initial backup copy requires transfer of the entire data source (SQL Server database) from production server (SQL Server machine) to the DPM server.</span><span class="sxs-lookup"><span data-stu-id="e345c-150">The initial backup copy requires transfer of the entire data source (SQL Server database) from production server (SQL Server machine) to the DPM server.</span></span> <span data-ttu-id="e345c-151">This data might be large, and transferring the data over the network could exceed bandwidth.</span><span class="sxs-lookup"><span data-stu-id="e345c-151">This data might be large, and transferring the data over the network could exceed bandwidth.</span></span> <span data-ttu-id="e345c-152">For this reason, administrators can choose to transfer the initial backup: **Manually** (using removable media) to avoid bandwidth congestion, or **Automatically over the network** (at a specified time).</span><span class="sxs-lookup"><span data-stu-id="e345c-152">For this reason, administrators can choose to transfer the initial backup: **Manually** (using removable media) to avoid bandwidth congestion, or **Automatically over the network** (at a specified time).</span></span>

    <span data-ttu-id="e345c-153">Once the initial backup is complete, the rest of the backups are incremental backups on the initial backup copy.</span><span class="sxs-lookup"><span data-stu-id="e345c-153">Once the initial backup is complete, the rest of the backups are incremental backups on the initial backup copy.</span></span> <span data-ttu-id="e345c-154">Incremental backups tend to be small and are easily transferred across the network.</span><span class="sxs-lookup"><span data-stu-id="e345c-154">Incremental backups tend to be small and are easily transferred across the network.</span></span>
10. <span data-ttu-id="e345c-155">Choose when you want the consistency check to run and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e345c-155">Choose when you want the consistency check to run and click **Next**.</span></span>

    ![Consistency check](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-consistent.png)

    <span data-ttu-id="e345c-157">DPM can perform a consistency check to check the integrity of the backup point.</span><span class="sxs-lookup"><span data-stu-id="e345c-157">DPM can perform a consistency check to check the integrity of the backup point.</span></span> <span data-ttu-id="e345c-158">It calculates the checksum of the backup file on the production server (SQL Server machine in this scenario) and the backed-up data for that file at DPM.</span><span class="sxs-lookup"><span data-stu-id="e345c-158">It calculates the checksum of the backup file on the production server (SQL Server machine in this scenario) and the backed-up data for that file at DPM.</span></span> <span data-ttu-id="e345c-159">In the case of a conflict, it is assumed that the backed-up file at DPM is corrupt.</span><span class="sxs-lookup"><span data-stu-id="e345c-159">In the case of a conflict, it is assumed that the backed-up file at DPM is corrupt.</span></span> <span data-ttu-id="e345c-160">DPM rectifies the backed-up data by sending the blocks corresponding to the checksum mismatch.</span><span class="sxs-lookup"><span data-stu-id="e345c-160">DPM rectifies the backed-up data by sending the blocks corresponding to the checksum mismatch.</span></span> <span data-ttu-id="e345c-161">As the consistency check is a performance-intensive operation, administrators have the option of scheduling the consistency check or running it automatically.</span><span class="sxs-lookup"><span data-stu-id="e345c-161">As the consistency check is a performance-intensive operation, administrators have the option of scheduling the consistency check or running it automatically.</span></span>
11. <span data-ttu-id="e345c-162">To specify online protection of the datasources, select the databases to be protected to Azure and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e345c-162">To specify online protection of the datasources, select the databases to be protected to Azure and click **Next**.</span></span>

    ![Select datasources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-sqldatabases.png)
12. <span data-ttu-id="e345c-164">Administrators can choose backup schedules and retention policies that suit their organization policies.</span><span class="sxs-lookup"><span data-stu-id="e345c-164">Administrators can choose backup schedules and retention policies that suit their organization policies.</span></span>

    ![Schedule and Retention](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-schedule.png)

    <span data-ttu-id="e345c-166">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen)</span><span class="sxs-lookup"><span data-stu-id="e345c-166">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen)</span></span>

    > [!NOTE]
    > <span data-ttu-id="e345c-167">It’s a good practice to have a few short-term recovery points on disk, for quick recovery.</span><span class="sxs-lookup"><span data-stu-id="e345c-167">It’s a good practice to have a few short-term recovery points on disk, for quick recovery.</span></span> <span data-ttu-id="e345c-168">These recovery points are used for “operational recovery".</span><span class="sxs-lookup"><span data-stu-id="e345c-168">These recovery points are used for “operational recovery".</span></span> <span data-ttu-id="e345c-169">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span><span class="sxs-lookup"><span data-stu-id="e345c-169">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span></span>
    >
    >

    <span data-ttu-id="e345c-170">**Best Practice**: Make sure that Azure Backups are scheduled after the completion of local disk backups using DPM.</span><span class="sxs-lookup"><span data-stu-id="e345c-170">**Best Practice**: Make sure that Azure Backups are scheduled after the completion of local disk backups using DPM.</span></span> <span data-ttu-id="e345c-171">This enables the latest disk backup to be copied to Azure.</span><span class="sxs-lookup"><span data-stu-id="e345c-171">This enables the latest disk backup to be copied to Azure.</span></span>

13. <span data-ttu-id="e345c-172">Choose the retention policy schedule.</span><span class="sxs-lookup"><span data-stu-id="e345c-172">Choose the retention policy schedule.</span></span> <span data-ttu-id="e345c-173">The details on how the retention policy works are provided at [Use Azure Backup to replace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="e345c-173">The details on how the retention policy works are provided at [Use Azure Backup to replace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span></span>

    ![Retention Policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-retentionschedule.png)

    <span data-ttu-id="e345c-175">In this example:</span><span class="sxs-lookup"><span data-stu-id="e345c-175">In this example:</span></span>

    * <span data-ttu-id="e345c-176">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen) and are retained for 180 days.</span><span class="sxs-lookup"><span data-stu-id="e345c-176">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen) and are retained for 180 days.</span></span>
    * <span data-ttu-id="e345c-177">The backup on Saturday at 12:00 P.M.</span><span class="sxs-lookup"><span data-stu-id="e345c-177">The backup on Saturday at 12:00 P.M.</span></span> <span data-ttu-id="e345c-178">is retained for 104 weeks</span><span class="sxs-lookup"><span data-stu-id="e345c-178">is retained for 104 weeks</span></span>
    * <span data-ttu-id="e345c-179">The backup on Last Saturday at 12:00 P.M.</span><span class="sxs-lookup"><span data-stu-id="e345c-179">The backup on Last Saturday at 12:00 P.M.</span></span> <span data-ttu-id="e345c-180">is retained for 60 months</span><span class="sxs-lookup"><span data-stu-id="e345c-180">is retained for 60 months</span></span>
    * <span data-ttu-id="e345c-181">The backup on Last Saturday of March at 12:00 P.M.</span><span class="sxs-lookup"><span data-stu-id="e345c-181">The backup on Last Saturday of March at 12:00 P.M.</span></span> <span data-ttu-id="e345c-182">is retained for 10 years</span><span class="sxs-lookup"><span data-stu-id="e345c-182">is retained for 10 years</span></span>
14. <span data-ttu-id="e345c-183">Click **Next** and select the appropriate option for transferring the initial backup copy to Azure.</span><span class="sxs-lookup"><span data-stu-id="e345c-183">Click **Next** and select the appropriate option for transferring the initial backup copy to Azure.</span></span> <span data-ttu-id="e345c-184">You can choose **Automatically over the network** or **Offline Backup**.</span><span class="sxs-lookup"><span data-stu-id="e345c-184">You can choose **Automatically over the network** or **Offline Backup**.</span></span>

    * <span data-ttu-id="e345c-185">**Automatically over the network** transfers the backup data to Azure as per the schedule chosen for backup.</span><span class="sxs-lookup"><span data-stu-id="e345c-185">**Automatically over the network** transfers the backup data to Azure as per the schedule chosen for backup.</span></span>
    * <span data-ttu-id="e345c-186">How **Offline Backup** works is explained at [Offline Backup workflow in Azure Backup](backup-azure-backup-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="e345c-186">How **Offline Backup** works is explained at [Offline Backup workflow in Azure Backup](backup-azure-backup-import-export.md).</span></span>

    <span data-ttu-id="e345c-187">Choose the relevant transfer mechanism to send the initial backup copy to Azure and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e345c-187">Choose the relevant transfer mechanism to send the initial backup copy to Azure and click **Next**.</span></span>
15. <span data-ttu-id="e345c-188">Once you review the policy details in the **Summary** screen, click on the **Create group** button to complete the workflow.</span><span class="sxs-lookup"><span data-stu-id="e345c-188">Once you review the policy details in the **Summary** screen, click on the **Create group** button to complete the workflow.</span></span> <span data-ttu-id="e345c-189">You can click the **Close** button and monitor the job progress in Monitoring workspace.</span><span class="sxs-lookup"><span data-stu-id="e345c-189">You can click the **Close** button and monitor the job progress in Monitoring workspace.</span></span>

    ![Creation of Protection Group In-Progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a><span data-ttu-id="e345c-191">On-demand backup of a SQL Server database</span><span class="sxs-lookup"><span data-stu-id="e345c-191">On-demand backup of a SQL Server database</span></span>
<span data-ttu-id="e345c-192">While the previous steps created a backup policy, a “recovery point” is created only when the first backup occurs.</span><span class="sxs-lookup"><span data-stu-id="e345c-192">While the previous steps created a backup policy, a “recovery point” is created only when the first backup occurs.</span></span> <span data-ttu-id="e345c-193">Rather than waiting for the scheduler to kick in, the steps below trigger the creation of a recovery point manually.</span><span class="sxs-lookup"><span data-stu-id="e345c-193">Rather than waiting for the scheduler to kick in, the steps below trigger the creation of a recovery point manually.</span></span>

1. <span data-ttu-id="e345c-194">Wait until the protection group status shows **OK** for the database before creating the recovery point.</span><span class="sxs-lookup"><span data-stu-id="e345c-194">Wait until the protection group status shows **OK** for the database before creating the recovery point.</span></span>

    ![Protection Group Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. <span data-ttu-id="e345c-196">Right-click on the database and select **Create Recovery Point**.</span><span class="sxs-lookup"><span data-stu-id="e345c-196">Right-click on the database and select **Create Recovery Point**.</span></span>

    ![Create Online Recovery Point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. <span data-ttu-id="e345c-198">Choose **Online Protection** in the drop-down menu and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e345c-198">Choose **Online Protection** in the drop-down menu and click **OK**.</span></span> <span data-ttu-id="e345c-199">This starts the creation of a recovery point in Azure.</span><span class="sxs-lookup"><span data-stu-id="e345c-199">This starts the creation of a recovery point in Azure.</span></span>

    ![Create recovery point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/sqlbackup-azure.png)
4. <span data-ttu-id="e345c-201">You can view the job progress in the **Monitoring** workspace where you'll find an in progress job like the one depicted in the next figure.</span><span class="sxs-lookup"><span data-stu-id="e345c-201">You can view the job progress in the **Monitoring** workspace where you'll find an in progress job like the one depicted in the next figure.</span></span>

    ![Monitoring console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a><span data-ttu-id="e345c-203">Recover a SQL Server database from Azure</span><span class="sxs-lookup"><span data-stu-id="e345c-203">Recover a SQL Server database from Azure</span></span>
<span data-ttu-id="e345c-204">The following steps are required to recover a protected entity (SQL Server database) from Azure.</span><span class="sxs-lookup"><span data-stu-id="e345c-204">The following steps are required to recover a protected entity (SQL Server database) from Azure.</span></span>

1. <span data-ttu-id="e345c-205">Open the DPM server Management Console.</span><span class="sxs-lookup"><span data-stu-id="e345c-205">Open the DPM server Management Console.</span></span> <span data-ttu-id="e345c-206">Navigate to **Recovery** workspace where you can see the servers backed up by DPM.</span><span class="sxs-lookup"><span data-stu-id="e345c-206">Navigate to **Recovery** workspace where you can see the servers backed up by DPM.</span></span> <span data-ttu-id="e345c-207">Browse the required database (in this case ReportServer$MSDPM2012).</span><span class="sxs-lookup"><span data-stu-id="e345c-207">Browse the required database (in this case ReportServer$MSDPM2012).</span></span> <span data-ttu-id="e345c-208">Select a **Recovery from** time which ends with **Online**.</span><span class="sxs-lookup"><span data-stu-id="e345c-208">Select a **Recovery from** time which ends with **Online**.</span></span>

    ![Select Recovery point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. <span data-ttu-id="e345c-210">Right-click the database name and click **Recover**.</span><span class="sxs-lookup"><span data-stu-id="e345c-210">Right-click the database name and click **Recover**.</span></span>

    ![Recover from Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/sqlbackup-recover.png)
3. <span data-ttu-id="e345c-212">DPM shows the details of the recovery point.</span><span class="sxs-lookup"><span data-stu-id="e345c-212">DPM shows the details of the recovery point.</span></span> <span data-ttu-id="e345c-213">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e345c-213">Click **Next**.</span></span> <span data-ttu-id="e345c-214">To overwrite the database, select the recovery type **Recover to original instance of SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e345c-214">To overwrite the database, select the recovery type **Recover to original instance of SQL Server**.</span></span> <span data-ttu-id="e345c-215">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e345c-215">Click **Next**.</span></span>

    ![Recover to Original Location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    <span data-ttu-id="e345c-217">In this example, DPM allows recovery of the database to another SQL Server instance or to a standalone network folder.</span><span class="sxs-lookup"><span data-stu-id="e345c-217">In this example, DPM allows recovery of the database to another SQL Server instance or to a standalone network folder.</span></span>
4. <span data-ttu-id="e345c-218">In the **Specify Recovery options** screen, you can select the recovery options like Network bandwidth usage throttling to throttle the bandwidth used by recovery.</span><span class="sxs-lookup"><span data-stu-id="e345c-218">In the **Specify Recovery options** screen, you can select the recovery options like Network bandwidth usage throttling to throttle the bandwidth used by recovery.</span></span> <span data-ttu-id="e345c-219">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e345c-219">Click **Next**.</span></span>
5. <span data-ttu-id="e345c-220">In the **Summary** screen, you see all the recovery configurations provided so far.</span><span class="sxs-lookup"><span data-stu-id="e345c-220">In the **Summary** screen, you see all the recovery configurations provided so far.</span></span> <span data-ttu-id="e345c-221">Click **Recover**.</span><span class="sxs-lookup"><span data-stu-id="e345c-221">Click **Recover**.</span></span>

    <span data-ttu-id="e345c-222">The Recovery status shows the database being recovered.</span><span class="sxs-lookup"><span data-stu-id="e345c-222">The Recovery status shows the database being recovered.</span></span> <span data-ttu-id="e345c-223">You can click **Close** to close the wizard and view the progress in the **Monitoring** workspace.</span><span class="sxs-lookup"><span data-stu-id="e345c-223">You can click **Close** to close the wizard and view the progress in the **Monitoring** workspace.</span></span>

    ![Initiate recovery process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    <span data-ttu-id="e345c-225">Once the recovery is completed, the restored database is application consistent.</span><span class="sxs-lookup"><span data-stu-id="e345c-225">Once the recovery is completed, the restored database is application consistent.</span></span>

### <a name="next-steps"></a><span data-ttu-id="e345c-226">Next Steps:</span><span class="sxs-lookup"><span data-stu-id="e345c-226">Next Steps:</span></span>
<span data-ttu-id="e345c-227">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e345c-227">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>




















