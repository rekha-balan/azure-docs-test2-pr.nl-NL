---
title: Configure long-term backup retention - Azure SQL database | Microsoft Docs
description: Learn how to store automated backups in the Azure Recovery Services vault and to restore from the Azure Recovery Services vault
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 5c26c789fc57c0d68ee85069491ec3870c3000d1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563925"
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="c28ec-103">Configure and restore from Azure SQL Database long-term backup retention</span><span class="sxs-lookup"><span data-stu-id="c28ec-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="c28ec-104">You can configure the Azure Recovery Services vault to store Azure SQL database backups and then recover a database using backups retained in the vault using the Azure portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c28ec-104">You can configure the Azure Recovery Services vault to store Azure SQL database backups and then recover a database using backups retained in the vault using the Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="c28ec-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c28ec-105">Azure portal</span></span>

<span data-ttu-id="c28ec-106">The following sections show you how to use the Azure portal to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-106">The following sections show you how to use the Azure portal to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="configure-the-vault-register-the-server-and-select-databases"></a><span data-ttu-id="c28ec-107">Configure the vault, register the server, and select databases</span><span class="sxs-lookup"><span data-stu-id="c28ec-107">Configure the vault, register the server, and select databases</span></span>

<span data-ttu-id="c28ec-108">You [configure an Azure Recovery Services vault to retain automated backups](sql-database-long-term-retention.md) for a period longer than the retention period for your service tier.</span><span class="sxs-lookup"><span data-stu-id="c28ec-108">You [configure an Azure Recovery Services vault to retain automated backups](sql-database-long-term-retention.md) for a period longer than the retention period for your service tier.</span></span> 

> [!TIP]
> <span data-ttu-id="c28ec-109">To delete backups in long-term backup retention, see [Configure and use long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c28ec-109">To delete backups in long-term backup retention, see [Configure and use long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>
>

1. <span data-ttu-id="c28ec-110">Open the **SQL Server** page for your server.</span><span class="sxs-lookup"><span data-stu-id="c28ec-110">Open the **SQL Server** page for your server.</span></span>

   ![sql server page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="c28ec-112">Click **Long-term backup retention**.</span><span class="sxs-lookup"><span data-stu-id="c28ec-112">Click **Long-term backup retention**.</span></span>

   ![long-term backup retention link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="c28ec-114">On the **Long-term backup retention** page for your server, review and accept the preview terms (unless you have already done so - or this feature is no longer in preview).</span><span class="sxs-lookup"><span data-stu-id="c28ec-114">On the **Long-term backup retention** page for your server, review and accept the preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![accept the preview terms](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="c28ec-116">To configure long-term backup retention, select that database in the grid and then click **Configure** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="c28ec-116">To configure long-term backup retention, select that database in the grid and then click **Configure** on the toolbar.</span></span>

   ![select database for long-term backup retention](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="c28ec-118">On the **Configure** page, click **Configure required settings** under **Recovery service vault**.</span><span class="sxs-lookup"><span data-stu-id="c28ec-118">On the **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![configure vault link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="c28ec-120">On the **Recovery services vault** page, select an existing vault, if any.</span><span class="sxs-lookup"><span data-stu-id="c28ec-120">On the **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="c28ec-121">Otherwise, if no recovery services vault found for your subscription, click to exit the flow and create a recovery services vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-121">Otherwise, if no recovery services vault found for your subscription, click to exit the flow and create a recovery services vault.</span></span>

   ![create vault link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="c28ec-123">On the **Recovery Services vaults** page, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c28ec-123">On the **Recovery Services vaults** page, click **Add**.</span></span>

   ![add vault link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="c28ec-125">On the **Recovery Services vault** page, provide a valid name for the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-125">On the **Recovery Services vault** page, provide a valid name for the Recovery Services vault.</span></span>

   ![new vault name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="c28ec-127">Select your subscription and resource group, and then select the location for the vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-127">Select your subscription and resource group, and then select the location for the vault.</span></span> <span data-ttu-id="c28ec-128">When done, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c28ec-128">When done, click **Create**.</span></span>

   ![create vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="c28ec-130">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span><span class="sxs-lookup"><span data-stu-id="c28ec-130">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>
   >

10. <span data-ttu-id="c28ec-131">After the new vault is created, execute the necessary steps to return to the **Recovery services vault** page.</span><span class="sxs-lookup"><span data-stu-id="c28ec-131">After the new vault is created, execute the necessary steps to return to the **Recovery services vault** page.</span></span>

11. <span data-ttu-id="c28ec-132">On the **Recovery services vault** page, click the vault and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="c28ec-132">On the **Recovery services vault** page, click the vault and then click **Select**.</span></span>

   ![select existing vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="c28ec-134">On the **Configure** page, provide a valid name for the new retention policy, modify the default retention policy as appropriate, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c28ec-134">On the **Configure** page, provide a valid name for the new retention policy, modify the default retention policy as appropriate, and then click **OK**.</span></span>

   ![define retention policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="c28ec-136">On the **Long-term backup retention** page for your database, click **Save** and then click **OK** to apply the long-term backup retention policy to all selected databases.</span><span class="sxs-lookup"><span data-stu-id="c28ec-136">On the **Long-term backup retention** page for your database, click **Save** and then click **OK** to apply the long-term backup retention policy to all selected databases.</span></span>

   ![define retention policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="c28ec-138">Click **Save** to enable long-term backup retention using this new policy to the Azure Recovery Services vault that you configured.</span><span class="sxs-lookup"><span data-stu-id="c28ec-138">Click **Save** to enable long-term backup retention using this new policy to the Azure Recovery Services vault that you configured.</span></span>

   ![define retention policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="c28ec-140">Once configured, backups show up in the vault within next seven days.</span><span class="sxs-lookup"><span data-stu-id="c28ec-140">Once configured, backups show up in the vault within next seven days.</span></span> <span data-ttu-id="c28ec-141">Do not continue this tutorial until backups show up in the vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-141">Do not continue this tutorial until backups show up in the vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="c28ec-142">View backups in long-term retention using Azure portal</span><span class="sxs-lookup"><span data-stu-id="c28ec-142">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="c28ec-143">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="c28ec-143">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="c28ec-144">In the Azure portal, open your Azure Recovery Services vault for your database backups (go to **All resources** and select it from the list of resources for your subscription) to view the amount of storage used by your database backups in the vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-144">In the Azure portal, open your Azure Recovery Services vault for your database backups (go to **All resources** and select it from the list of resources for your subscription) to view the amount of storage used by your database backups in the vault.</span></span>

   ![view recovery services vault with backups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="c28ec-146">Open the **SQL database** page for your database.</span><span class="sxs-lookup"><span data-stu-id="c28ec-146">Open the **SQL database** page for your database.</span></span>

   ![new sample db page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="c28ec-148">On the toolbar, click **Restore**.</span><span class="sxs-lookup"><span data-stu-id="c28ec-148">On the toolbar, click **Restore**.</span></span>

   ![restore toolbar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="c28ec-150">On the Restore page, click **Long-term**.</span><span class="sxs-lookup"><span data-stu-id="c28ec-150">On the Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="c28ec-151">Under Azure vault backups, click **Select a backup** to view the available database backups in long-term backup retention.</span><span class="sxs-lookup"><span data-stu-id="c28ec-151">Under Azure vault backups, click **Select a backup** to view the available database backups in long-term backup retention.</span></span>

   ![backups in vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-the-azure-portal"></a><span data-ttu-id="c28ec-153">Restore a database from a backup in long-term backup retention using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c28ec-153">Restore a database from a backup in long-term backup retention using the Azure portal</span></span>

<span data-ttu-id="c28ec-154">You restore the database to a new database from a backup in the Azure Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-154">You restore the database to a new database from a backup in the Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="c28ec-155">On the **Azure vault backups** page, click the backup to restore and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="c28ec-155">On the **Azure vault backups** page, click the backup to restore and then click **Select**.</span></span>

   ![select backup in vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="c28ec-157">In the **Database name** text box, provide the name for the restored database.</span><span class="sxs-lookup"><span data-stu-id="c28ec-157">In the **Database name** text box, provide the name for the restored database.</span></span>

   ![new database name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="c28ec-159">Click **OK** to restore your database from the backup in the vault to the new database.</span><span class="sxs-lookup"><span data-stu-id="c28ec-159">Click **OK** to restore your database from the backup in the vault to the new database.</span></span>

4. <span data-ttu-id="c28ec-160">On the toolbar, click the notification icon to view the status of the restore job.</span><span class="sxs-lookup"><span data-stu-id="c28ec-160">On the toolbar, click the notification icon to view the status of the restore job.</span></span>

   ![restore job progress from vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="c28ec-162">When the restore job is completed, open the **SQL databases** page to view the newly restored database.</span><span class="sxs-lookup"><span data-stu-id="c28ec-162">When the restore job is completed, open the **SQL databases** page to view the newly restored database.</span></span>

   ![restored database from vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="c28ec-164">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="c28ec-164">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="c28ec-165">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c28ec-165">PowerShell</span></span>

<span data-ttu-id="c28ec-166">The following sections show you how to use PowerShell to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-166">The following sections show you how to use PowerShell to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="c28ec-167">Create a recovery services vault</span><span class="sxs-lookup"><span data-stu-id="c28ec-167">Create a recovery services vault</span></span>

<span data-ttu-id="c28ec-168">Use the [New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault?view=azurermps-3.7.0) to create a recovery services vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-168">Use the [New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault?view=azurermps-3.7.0) to create a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c28ec-169">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span><span class="sxs-lookup"><span data-stu-id="c28ec-169">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-to-use-the-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="c28ec-170">Set your server to use the recovery vault for its long-term retention backups</span><span class="sxs-lookup"><span data-stu-id="c28ec-170">Set your server to use the recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="c28ec-171">Use the [Set-AzureRmSqlServerBackupLongTermRetentionVault](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.3.0/set-azurermsqlserverbackuplongtermretentionvault) cmdlet to associate a previously created recovery services vault with a specific Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="c28ec-171">Use the [Set-AzureRmSqlServerBackupLongTermRetentionVault](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.3.0/set-azurermsqlserverbackuplongtermretentionvault) cmdlet to associate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server to use the vault to for long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="c28ec-172">Create a retention policy</span><span class="sxs-lookup"><span data-stu-id="c28ec-172">Create a retention policy</span></span>

<span data-ttu-id="c28ec-173">A retention policy is where you set how long to keep a database backup.</span><span class="sxs-lookup"><span data-stu-id="c28ec-173">A retention policy is where you set how long to keep a database backup.</span></span> <span data-ttu-id="c28ec-174">Use the [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet to get the default retention policy to use as the template for creating policies.</span><span class="sxs-lookup"><span data-stu-id="c28ec-174">Use the [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet to get the default retention policy to use as the template for creating policies.</span></span> <span data-ttu-id="c28ec-175">In this template, the retention period is set for 2 years.</span><span class="sxs-lookup"><span data-stu-id="c28ec-175">In this template, the retention period is set for 2 years.</span></span> <span data-ttu-id="c28ec-176">Next, run the [New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/new-azurermrecoveryservicesbackupprotectionpolicy) to finally create the policy.</span><span class="sxs-lookup"><span data-stu-id="c28ec-176">Next, run the [New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/new-azurermrecoveryservicesbackupprotectionpolicy) to finally create the policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="c28ec-177">Some cmdlets require that you set the vault context before running ([Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices/v2.3.0/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span><span class="sxs-lookup"><span data-stu-id="c28ec-177">Some cmdlets require that you set the vault context before running ([Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices/v2.3.0/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="c28ec-178">You set the context because the policy is part of the vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-178">You set the context because the policy is part of the vault.</span></span> <span data-ttu-id="c28ec-179">You can create multiple retention policies for each vault and then apply the desired policy to specific databases.</span><span class="sxs-lookup"><span data-stu-id="c28ec-179">You can create multiple retention policies for each vault and then apply the desired policy to specific databases.</span></span> 


```PowerShell
# Retrieve the default retention policy for the AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set the retention value to two years (you can set to any time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set the vault context to the vault you are creating the policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create the new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-to-use-the-previously-defined-retention-policy"></a><span data-ttu-id="c28ec-180">Configure a database to use the previously defined retention policy</span><span class="sxs-lookup"><span data-stu-id="c28ec-180">Configure a database to use the previously defined retention policy</span></span>

<span data-ttu-id="c28ec-181">Use the [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.3.0/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet to apply the new policy to a specific database.</span><span class="sxs-lookup"><span data-stu-id="c28ec-181">Use the [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.3.0/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet to apply the new policy to a specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

> [!IMPORTANT]
> <span data-ttu-id="c28ec-182">Once configured, backups show up in the vault within next seven days.</span><span class="sxs-lookup"><span data-stu-id="c28ec-182">Once configured, backups show up in the vault within next seven days.</span></span> <span data-ttu-id="c28ec-183">Continue this tutorial after backups show up in the vault.</span><span class="sxs-lookup"><span data-stu-id="c28ec-183">Continue this tutorial after backups show up in the vault.</span></span>

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="c28ec-184">View backup info, and backups in long-term retention</span><span class="sxs-lookup"><span data-stu-id="c28ec-184">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="c28ec-185">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="c28ec-185">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="c28ec-186">Use the following cmdlets to view backup information:</span><span class="sxs-lookup"><span data-stu-id="c28ec-186">Use the following cmdlets to view backup information:</span></span>

- [<span data-ttu-id="c28ec-187">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="c28ec-187">Get-AzureRmRecoveryServicesBackupContainer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="c28ec-188">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="c28ec-188">Get-AzureRmRecoveryServicesBackupItem</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="c28ec-189">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="c28ec-189">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set the vault context to the vault we want to restore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# the following commands find the container associated with the server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get the long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for the previously indicated database
# Optionally, set the -StartDate and -EndDate parameters to return backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="c28ec-190">Restore a database from a backup in long-term backup retention</span><span class="sxs-lookup"><span data-stu-id="c28ec-190">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="c28ec-191">Restoring from long-term backup retention uses the [Restore-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.3.0/restore-azurermsqldatabase) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c28ec-191">Restoring from long-term backup retention uses the [Restore-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.3.0/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore the most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> <span data-ttu-id="c28ec-192">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="c28ec-192">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c28ec-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="c28ec-193">Next steps</span></span>

- <span data-ttu-id="c28ec-194">To learn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="c28ec-194">To learn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="c28ec-195">To learn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="c28ec-195">To learn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="c28ec-196">To learn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="c28ec-196">To learn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>





















