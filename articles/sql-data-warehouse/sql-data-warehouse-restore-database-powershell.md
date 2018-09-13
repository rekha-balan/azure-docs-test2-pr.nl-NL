---
title: Restore an Azure SQL Data Warehouse  (PowerShell) | Microsoft Docs
description: PowerShell tasks for restoring an Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: ''
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 27b290ef70061b98d99478559e9d1356fb867505
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550385"
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="66db7-103">Restore an Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="66db7-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [Overview][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

<span data-ttu-id="66db7-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66db7-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="66db7-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="66db7-109">Before you begin</span></span>
<span data-ttu-id="66db7-110">**Verify your DTU capacity.**</span><span class="sxs-lookup"><span data-stu-id="66db7-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="66db7-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span><span class="sxs-lookup"><span data-stu-id="66db7-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="66db7-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span><span class="sxs-lookup"><span data-stu-id="66db7-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="66db7-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="66db7-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="66db7-114">Install PowerShell</span><span class="sxs-lookup"><span data-stu-id="66db7-114">Install PowerShell</span></span>
<span data-ttu-id="66db7-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span><span class="sxs-lookup"><span data-stu-id="66db7-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="66db7-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="66db7-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="66db7-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="66db7-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="66db7-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="66db7-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="66db7-119">Restore an active or paused database</span><span class="sxs-lookup"><span data-stu-id="66db7-119">Restore an active or paused database</span></span>
<span data-ttu-id="66db7-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66db7-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="66db7-121">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66db7-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="66db7-122">Connect to your Azure account and list all the subscriptions associated with your account.</span><span class="sxs-lookup"><span data-stu-id="66db7-122">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="66db7-123">Select the subscription that contains the database to be restored.</span><span class="sxs-lookup"><span data-stu-id="66db7-123">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="66db7-124">List the restore points for the database.</span><span class="sxs-lookup"><span data-stu-id="66db7-124">List the restore points for the database.</span></span>
5. <span data-ttu-id="66db7-125">Pick the desired restore point using the RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="66db7-125">Pick the desired restore point using the RestorePointCreationDate.</span></span>
6. <span data-ttu-id="66db7-126">Restore the database to the desired restore point.</span><span class="sxs-lookup"><span data-stu-id="66db7-126">Restore the database to the desired restore point.</span></span>
7. <span data-ttu-id="66db7-127">Verify that the restored database is online.</span><span class="sxs-lookup"><span data-stu-id="66db7-127">Verify that the restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="66db7-129">Restore a deleted database</span><span class="sxs-lookup"><span data-stu-id="66db7-129">Restore a deleted database</span></span>
<span data-ttu-id="66db7-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66db7-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="66db7-131">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66db7-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="66db7-132">Connect to your Azure account and list all the subscriptions associated with your account.</span><span class="sxs-lookup"><span data-stu-id="66db7-132">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="66db7-133">Select the subscription that contains the deleted database to be restored.</span><span class="sxs-lookup"><span data-stu-id="66db7-133">Select the subscription that contains the deleted database to be restored.</span></span>
4. <span data-ttu-id="66db7-134">Get the specific deleted database.</span><span class="sxs-lookup"><span data-stu-id="66db7-134">Get the specific deleted database.</span></span>
5. <span data-ttu-id="66db7-135">Restore the deleted database.</span><span class="sxs-lookup"><span data-stu-id="66db7-135">Restore the deleted database.</span></span>
6. <span data-ttu-id="66db7-136">Verify that the restored database is online.</span><span class="sxs-lookup"><span data-stu-id="66db7-136">Verify that the restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupNam -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="66db7-138">Restore from an Azure geographical region</span><span class="sxs-lookup"><span data-stu-id="66db7-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="66db7-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66db7-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="66db7-140">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66db7-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="66db7-141">Connect to your Azure account and list all the subscriptions associated with your account.</span><span class="sxs-lookup"><span data-stu-id="66db7-141">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="66db7-142">Select the subscription that contains the database to be restored.</span><span class="sxs-lookup"><span data-stu-id="66db7-142">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="66db7-143">Get the database you want to recover.</span><span class="sxs-lookup"><span data-stu-id="66db7-143">Get the database you want to recover.</span></span>
5. <span data-ttu-id="66db7-144">Create the recovery request for the database.</span><span class="sxs-lookup"><span data-stu-id="66db7-144">Create the recovery request for the database.</span></span>
6. <span data-ttu-id="66db7-145">Verify the status of the geo-restored database.</span><span class="sxs-lookup"><span data-stu-id="66db7-145">Verify the status of the geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].
> 
> 

<span data-ttu-id="66db7-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span><span class="sxs-lookup"><span data-stu-id="66db7-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66db7-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="66db7-148">Next steps</span></span>
<span data-ttu-id="66db7-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="66db7-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
