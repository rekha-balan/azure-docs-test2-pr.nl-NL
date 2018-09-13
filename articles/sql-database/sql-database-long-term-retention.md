---
title: Storing Azure SQL Database Backups for up to 10 years | Microsoft Docs
description: Learn how Azure SQL Database supports storing backups for up to 10 years.
keywords: ''
services: sql-database
documentationcenter: ''
author: anosov1960
manager: jhubbard
editor: ''
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 6620fbce6f819a69661b9c3cb04c6c825df01c42
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551863"
---
# <a name="storing-azure-sql-database-backups-for-up-to-10-years"></a><span data-ttu-id="a628b-103">Storing Azure SQL Database Backups for up to 10 years</span><span class="sxs-lookup"><span data-stu-id="a628b-103">Storing Azure SQL Database Backups for up to 10 years</span></span>
<span data-ttu-id="a628b-104">Many applications have regulatory, compliance, or other business purposes that require you to retain the automatic full database backups beyond the 7-35 days provided by SQL Database's [automatic backups](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="a628b-104">Many applications have regulatory, compliance, or other business purposes that require you to retain the automatic full database backups beyond the 7-35 days provided by SQL Database's [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="a628b-105">The **Long-Term Backup Retention** feature enables you to store your Azure SQL Database backups in an Azure Recovery Services vault for up to 10 years.</span><span class="sxs-lookup"><span data-stu-id="a628b-105">The **Long-Term Backup Retention** feature enables you to store your Azure SQL Database backups in an Azure Recovery Services vault for up to 10 years.</span></span> <span data-ttu-id="a628b-106">You can store up to 1000 databases per vault.</span><span class="sxs-lookup"><span data-stu-id="a628b-106">You can store up to 1000 databases per vault.</span></span> <span data-ttu-id="a628b-107">You can select any backup in the vault to restore it as a new database.</span><span class="sxs-lookup"><span data-stu-id="a628b-107">You can select any backup in the vault to restore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a628b-108">Long-Term Backup Retention is currently in preview and available in the following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span><span class="sxs-lookup"><span data-stu-id="a628b-108">Long-Term Backup Retention is currently in preview and available in the following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="a628b-109">You can enable up to 200 databases per vault during a 24-hour period.</span><span class="sxs-lookup"><span data-stu-id="a628b-109">You can enable up to 200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="a628b-110">Therefore, we recommend that you use a separate vault for each server to minimize the impact of this limit.</span><span class="sxs-lookup"><span data-stu-id="a628b-110">Therefore, we recommend that you use a separate vault for each server to minimize the impact of this limit.</span></span> 
> 



 
## <a name="how-does-sql-database-long-term-backup-retention-work"></a><span data-ttu-id="a628b-111">How does SQL Database long-term backup retention work?</span><span class="sxs-lookup"><span data-stu-id="a628b-111">How does SQL Database long-term backup retention work?</span></span>

<span data-ttu-id="a628b-112">Long-term backup retention of backups allows you to associate an Azure SQL Database server with an Azure Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="a628b-112">Long-term backup retention of backups allows you to associate an Azure SQL Database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="a628b-113">The vault must be created in the same Azure subscription that created the SQL server and in the same geographic region and resource group.</span><span class="sxs-lookup"><span data-stu-id="a628b-113">The vault must be created in the same Azure subscription that created the SQL server and in the same geographic region and resource group.</span></span> 
* <span data-ttu-id="a628b-114">You then configure a retention policy for any database.</span><span class="sxs-lookup"><span data-stu-id="a628b-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="a628b-115">The policy causes the weekly full database backups be copied to the Recovery Services vault and retained for the specified retention period (up to 10 years).</span><span class="sxs-lookup"><span data-stu-id="a628b-115">The policy causes the weekly full database backups be copied to the Recovery Services vault and retained for the specified retention period (up to 10 years).</span></span> 
* <span data-ttu-id="a628b-116">You can then restore from any of these backups to a new database in any server in the subscription.</span><span class="sxs-lookup"><span data-stu-id="a628b-116">You can then restore from any of these backups to a new database in any server in the subscription.</span></span> <span data-ttu-id="a628b-117">The copy is performed by Azure storage from existing backups and has no performance impact on the existing database.</span><span class="sxs-lookup"><span data-stu-id="a628b-117">The copy is performed by Azure storage from existing backups and has no performance impact on the existing database.</span></span>

> [!TIP]
> <span data-ttu-id="a628b-118">For a how-to guide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md)</span><span class="sxs-lookup"><span data-stu-id="a628b-118">For a how-to guide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md)</span></span>

## <a name="how-do-i-enable-long-term-backup-retention"></a><span data-ttu-id="a628b-119">How do I enable long-term backup retention?</span><span class="sxs-lookup"><span data-stu-id="a628b-119">How do I enable long-term backup retention?</span></span>

<span data-ttu-id="a628b-120">To configure long-term backup retention for a database:</span><span class="sxs-lookup"><span data-stu-id="a628b-120">To configure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="a628b-121">Create an Azure Recovery Services vault in the same region, subscription, and resource group as your SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="a628b-121">Create an Azure Recovery Services vault in the same region, subscription, and resource group as your SQL Database server.</span></span> 
2. <span data-ttu-id="a628b-122">Register the server to the vault</span><span class="sxs-lookup"><span data-stu-id="a628b-122">Register the server to the vault</span></span>
3. <span data-ttu-id="a628b-123">Create an Azure Recovery Services Protection Policy</span><span class="sxs-lookup"><span data-stu-id="a628b-123">Create an Azure Recovery Services Protection Policy</span></span>
4. <span data-ttu-id="a628b-124">Apply the protection policy to the databases that require long-term backup retention</span><span class="sxs-lookup"><span data-stu-id="a628b-124">Apply the protection policy to the databases that require long-term backup retention</span></span>

### <a name="azure-portal"></a><span data-ttu-id="a628b-125">Azure portal</span><span class="sxs-lookup"><span data-stu-id="a628b-125">Azure portal</span></span>

<span data-ttu-id="a628b-126">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using the Azure portal, click **Long-term backup retention**, select a database, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="a628b-126">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using the Azure portal, click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![select database for long-term backup retention](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

<span data-ttu-id="a628b-128">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using PowerShell, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a628b-128">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using PowerShell, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="how-do-i-restore-a-database-stored-with-the-long-term-backup-retention-feature"></a><span data-ttu-id="a628b-129">How do I restore a database stored with the long-term backup retention feature?</span><span class="sxs-lookup"><span data-stu-id="a628b-129">How do I restore a database stored with the long-term backup retention feature?</span></span>

<span data-ttu-id="a628b-130">To recover from a long-term backup retention backup:</span><span class="sxs-lookup"><span data-stu-id="a628b-130">To recover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="a628b-131">List the vault where the backup is stored</span><span class="sxs-lookup"><span data-stu-id="a628b-131">List the vault where the backup is stored</span></span>
2. <span data-ttu-id="a628b-132">List the container that is mapped to your logical server</span><span class="sxs-lookup"><span data-stu-id="a628b-132">List the container that is mapped to your logical server</span></span>
3. <span data-ttu-id="a628b-133">List the data source within the vault that is mapped to your database</span><span class="sxs-lookup"><span data-stu-id="a628b-133">List the data source within the vault that is mapped to your database</span></span>
4. <span data-ttu-id="a628b-134">List the recovery points available to restore</span><span class="sxs-lookup"><span data-stu-id="a628b-134">List the recovery points available to restore</span></span>
5. <span data-ttu-id="a628b-135">Restore from the recovery point to the target server within your subscription</span><span class="sxs-lookup"><span data-stu-id="a628b-135">Restore from the recovery point to the target server within your subscription</span></span>

<span data-ttu-id="a628b-136">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using the Azure portal, see [Manage long-term backup retention usihg the Azure portal](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a628b-136">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using the Azure portal, see [Manage long-term backup retention usihg the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> <span data-ttu-id="a628b-137">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using PowerShell, see [Manage long-term backup retention usihg PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a628b-137">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using PowerShell, see [Manage long-term backup retention usihg PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="how-much-does-long-term-backup-retention-cost"></a><span data-ttu-id="a628b-138">How much does long-term backup retention cost?</span><span class="sxs-lookup"><span data-stu-id="a628b-138">How much does long-term backup retention cost?</span></span>

<span data-ttu-id="a628b-139">Long-term backup retention of an Azure SQL database is charged according to the [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="a628b-139">Long-term backup retention of an Azure SQL database is charged according to the [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="a628b-140">After the Azure SQL Database server is registered to the vault, you are charged for the total storage that is used by the weekly backups stored in the vault.</span><span class="sxs-lookup"><span data-stu-id="a628b-140">After the Azure SQL Database server is registered to the vault, you are charged for the total storage that is used by the weekly backups stored in the vault.</span></span>

## <a name="view-available-backups-stored-in-long-term-backup-retention"></a><span data-ttu-id="a628b-141">View available backups stored in long-term backup retention</span><span class="sxs-lookup"><span data-stu-id="a628b-141">View available backups stored in long-term backup retention</span></span>

<span data-ttu-id="a628b-142">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using the Azure portal, see [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a628b-142">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using the Azure portal, see [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> <span data-ttu-id="a628b-143">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using PowerShell, see [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a628b-143">To configure, manage, and restore from long-term backup retention of automated backups in an Azure Recovery Services vault using PowerShell, see [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disabling-long-term-retention"></a><span data-ttu-id="a628b-144">Disabling Long-term Retention</span><span class="sxs-lookup"><span data-stu-id="a628b-144">Disabling Long-term Retention</span></span>

<span data-ttu-id="a628b-145">The Recovery Service automatically handles cleanup of backups based on the provided retention policy.</span><span class="sxs-lookup"><span data-stu-id="a628b-145">The Recovery Service automatically handles cleanup of backups based on the provided retention policy.</span></span> 

* <span data-ttu-id="a628b-146">To stop sending the backups for a specific database to the vault, remove the retention policy for that database.</span><span class="sxs-lookup"><span data-stu-id="a628b-146">To stop sending the backups for a specific database to the vault, remove the retention policy for that database.</span></span>
  
    ```
    Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
    ```

> [!NOTE]
> <span data-ttu-id="a628b-147">The backups already in the vault are not be impacted.</span><span class="sxs-lookup"><span data-stu-id="a628b-147">The backups already in the vault are not be impacted.</span></span> <span data-ttu-id="a628b-148">They are automatically deleted by the Recovery Service when their retention period expires.</span><span class="sxs-lookup"><span data-stu-id="a628b-148">They are automatically deleted by the Recovery Service when their retention period expires.</span></span>

## <a name="removing-long-term-backup-retention-backups-from-the-azure-recovery-services-vault"></a><span data-ttu-id="a628b-149">Removing long-term backup retention backups from the Azure Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="a628b-149">Removing long-term backup retention backups from the Azure Recovery Services vault</span></span>

<span data-ttu-id="a628b-150">To remove long-term backup retention backups from the vault, see [Delete long-term backup retention backups](sql-database-long-term-backup-retention-configure.md)</span><span class="sxs-lookup"><span data-stu-id="a628b-150">To remove long-term backup retention backups from the vault, see [Delete long-term backup retention backups](sql-database-long-term-backup-retention-configure.md)</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="a628b-151">Long-term backup retention FAQ:</span><span class="sxs-lookup"><span data-stu-id="a628b-151">Long-term backup retention FAQ:</span></span>

1. <span data-ttu-id="a628b-152">Q: Can I manually delete specific backups in the vault?</span><span class="sxs-lookup"><span data-stu-id="a628b-152">Q: Can I manually delete specific backups in the vault?</span></span>

    <span data-ttu-id="a628b-153">A: Not currently.</span><span class="sxs-lookup"><span data-stu-id="a628b-153">A: Not currently.</span></span> <span data-ttu-id="a628b-154">The vault automatically cleans up backups when the retention period has expired.</span><span class="sxs-lookup"><span data-stu-id="a628b-154">The vault automatically cleans up backups when the retention period has expired.</span></span>
2. <span data-ttu-id="a628b-155">Q: Can I register my server to store Backups to more than one vault?</span><span class="sxs-lookup"><span data-stu-id="a628b-155">Q: Can I register my server to store Backups to more than one vault?</span></span>

    <span data-ttu-id="a628b-156">A: No, today you can only store backups to one vault at a time.</span><span class="sxs-lookup"><span data-stu-id="a628b-156">A: No, today you can only store backups to one vault at a time.</span></span>
3. <span data-ttu-id="a628b-157">Q: Can I have a vault and server in different subscriptions?</span><span class="sxs-lookup"><span data-stu-id="a628b-157">Q: Can I have a vault and server in different subscriptions?</span></span>

    <span data-ttu-id="a628b-158">A: No, currently the vault and server must be in both the same subscription and resource group.</span><span class="sxs-lookup"><span data-stu-id="a628b-158">A: No, currently the vault and server must be in both the same subscription and resource group.</span></span>
4. <span data-ttu-id="a628b-159">Q: Can I use a vault I created in a different region than my server’s region?</span><span class="sxs-lookup"><span data-stu-id="a628b-159">Q: Can I use a vault I created in a different region than my server’s region?</span></span>

    <span data-ttu-id="a628b-160">A: No, the vault and server must be in the same region to minimize the copy time and avoid the traffic charges.</span><span class="sxs-lookup"><span data-stu-id="a628b-160">A: No, the vault and server must be in the same region to minimize the copy time and avoid the traffic charges.</span></span>
5. <span data-ttu-id="a628b-161">Q: How many databases can I store in one vault?</span><span class="sxs-lookup"><span data-stu-id="a628b-161">Q: How many databases can I store in one vault?</span></span>

    <span data-ttu-id="a628b-162">A: Currently, we only support up to 1000 databases per vault.</span><span class="sxs-lookup"><span data-stu-id="a628b-162">A: Currently, we only support up to 1000 databases per vault.</span></span> 
6. <span data-ttu-id="a628b-163">Q.</span><span class="sxs-lookup"><span data-stu-id="a628b-163">Q.</span></span> <span data-ttu-id="a628b-164">How many vaults can I create per subscription?</span><span class="sxs-lookup"><span data-stu-id="a628b-164">How many vaults can I create per subscription?</span></span>

    <span data-ttu-id="a628b-165">A.</span><span class="sxs-lookup"><span data-stu-id="a628b-165">A.</span></span> <span data-ttu-id="a628b-166">You can create up to 25 vaults per subscription.</span><span class="sxs-lookup"><span data-stu-id="a628b-166">You can create up to 25 vaults per subscription.</span></span>
7. <span data-ttu-id="a628b-167">Q.</span><span class="sxs-lookup"><span data-stu-id="a628b-167">Q.</span></span> <span data-ttu-id="a628b-168">How many databases can I configure per day per vault?</span><span class="sxs-lookup"><span data-stu-id="a628b-168">How many databases can I configure per day per vault?</span></span>

    <span data-ttu-id="a628b-169">A.</span><span class="sxs-lookup"><span data-stu-id="a628b-169">A.</span></span> <span data-ttu-id="a628b-170">You can only set up 200 databases per day per vault.</span><span class="sxs-lookup"><span data-stu-id="a628b-170">You can only set up 200 databases per day per vault.</span></span>
8. <span data-ttu-id="a628b-171">Q: Does long-term backup retention work with elastic pools?</span><span class="sxs-lookup"><span data-stu-id="a628b-171">Q: Does long-term backup retention work with elastic pools?</span></span>

    <span data-ttu-id="a628b-172">A: Yes.</span><span class="sxs-lookup"><span data-stu-id="a628b-172">A: Yes.</span></span> <span data-ttu-id="a628b-173">Any database in the pool can be configured with the retention policy.</span><span class="sxs-lookup"><span data-stu-id="a628b-173">Any database in the pool can be configured with the retention policy.</span></span>
9. <span data-ttu-id="a628b-174">Q: Can I choose the time at which the backup is created?</span><span class="sxs-lookup"><span data-stu-id="a628b-174">Q: Can I choose the time at which the backup is created?</span></span>

    <span data-ttu-id="a628b-175">A: No, SQL Database controls the backups schedule to minimize the performance impact on your databases.</span><span class="sxs-lookup"><span data-stu-id="a628b-175">A: No, SQL Database controls the backups schedule to minimize the performance impact on your databases.</span></span>
10. <span data-ttu-id="a628b-176">Q: I have TDE enabled for my database.</span><span class="sxs-lookup"><span data-stu-id="a628b-176">Q: I have TDE enabled for my database.</span></span> <span data-ttu-id="a628b-177">Can I use TDE with the vault?</span><span class="sxs-lookup"><span data-stu-id="a628b-177">Can I use TDE with the vault?</span></span> 

    <span data-ttu-id="a628b-178">A.</span><span class="sxs-lookup"><span data-stu-id="a628b-178">A.</span></span> <span data-ttu-id="a628b-179">Yes, TDE is supported.</span><span class="sxs-lookup"><span data-stu-id="a628b-179">Yes, TDE is supported.</span></span> <span data-ttu-id="a628b-180">You can restore the database from the vault even if the original database no longer exists.</span><span class="sxs-lookup"><span data-stu-id="a628b-180">You can restore the database from the vault even if the original database no longer exists.</span></span>
11. <span data-ttu-id="a628b-181">Q.</span><span class="sxs-lookup"><span data-stu-id="a628b-181">Q.</span></span> <span data-ttu-id="a628b-182">What happens with the backups in the vault if my subscription is suspended?</span><span class="sxs-lookup"><span data-stu-id="a628b-182">What happens with the backups in the vault if my subscription is suspended?</span></span> 

    <span data-ttu-id="a628b-183">A.</span><span class="sxs-lookup"><span data-stu-id="a628b-183">A.</span></span> <span data-ttu-id="a628b-184">If your subscription is suspended, we retain the existing databases and backups.</span><span class="sxs-lookup"><span data-stu-id="a628b-184">If your subscription is suspended, we retain the existing databases and backups.</span></span> <span data-ttu-id="a628b-185">New backups are not being copied to the vault.</span><span class="sxs-lookup"><span data-stu-id="a628b-185">New backups are not being copied to the vault.</span></span> <span data-ttu-id="a628b-186">After you reactivate the subscription, the service resumes copying backups to the vault.</span><span class="sxs-lookup"><span data-stu-id="a628b-186">After you reactivate the subscription, the service resumes copying backups to the vault.</span></span> <span data-ttu-id="a628b-187">Your vault becomes accessible to the restore operations using the backups that had been copied there before the subscription was suspended.</span><span class="sxs-lookup"><span data-stu-id="a628b-187">Your vault becomes accessible to the restore operations using the backups that had been copied there before the subscription was suspended.</span></span> 
12. <span data-ttu-id="a628b-188">Q: Can I get access to the SQL Database backup files so I can download / restore to SQL Server?</span><span class="sxs-lookup"><span data-stu-id="a628b-188">Q: Can I get access to the SQL Database backup files so I can download / restore to SQL Server?</span></span>

    <span data-ttu-id="a628b-189">A: No, not currently.</span><span class="sxs-lookup"><span data-stu-id="a628b-189">A: No, not currently.</span></span>
13. <span data-ttu-id="a628b-190">Q: Is it possible to have multiple Schedules (Daily, Weekly, Monthly, Yearly) within a SQL Retention Policy.</span><span class="sxs-lookup"><span data-stu-id="a628b-190">Q: Is it possible to have multiple Schedules (Daily, Weekly, Monthly, Yearly) within a SQL Retention Policy.</span></span>

    <span data-ttu-id="a628b-191">A: No, this is currently only available for virtual machine backups.</span><span class="sxs-lookup"><span data-stu-id="a628b-191">A: No, this is currently only available for virtual machine backups.</span></span>
14. <span data-ttu-id="a628b-192">Q.</span><span class="sxs-lookup"><span data-stu-id="a628b-192">Q.</span></span> <span data-ttu-id="a628b-193">What if we set up long-term backup retention on a database that is an active geo-replication secondary?</span><span class="sxs-lookup"><span data-stu-id="a628b-193">What if we set up long-term backup retention on a database that is an active geo-replication secondary?</span></span>

    <span data-ttu-id="a628b-194">A: Currently we don't take backups on replicas, and therefore, there is no option for long-term backup retention on secondaries.</span><span class="sxs-lookup"><span data-stu-id="a628b-194">A: Currently we don't take backups on replicas, and therefore, there is no option for long-term backup retention on secondaries.</span></span> <span data-ttu-id="a628b-195">However, it is important for a customer to set up long-term backup retention on an active geo-replication secondary for these reasons:</span><span class="sxs-lookup"><span data-stu-id="a628b-195">However, it is important for a customer to set up long-term backup retention on an active geo-replication secondary for these reasons:</span></span>
    - <span data-ttu-id="a628b-196">When a failover happens and the database becomes a primary, we take a full backup and this full backup is uploaded to vault.</span><span class="sxs-lookup"><span data-stu-id="a628b-196">When a failover happens and the database becomes a primary, we take a full backup and this full backup is uploaded to vault.</span></span>
    - <span data-ttu-id="a628b-197">There is no extra cost to the customer for setting up long-term backup retention on a secondary.</span><span class="sxs-lookup"><span data-stu-id="a628b-197">There is no extra cost to the customer for setting up long-term backup retention on a secondary.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a628b-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="a628b-198">Next steps</span></span>
<span data-ttu-id="a628b-199">Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion.</span><span class="sxs-lookup"><span data-stu-id="a628b-199">Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion.</span></span> <span data-ttu-id="a628b-200">To learn about the other Azure SQL Database business continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="a628b-200">To learn about the other Azure SQL Database business continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>


