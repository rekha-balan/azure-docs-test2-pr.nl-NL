---
title: Export an Azure SQL database to a BACPAC file | Microsoft Docs
description: Export an Azure SQL database to a BACPAC file  using the Azure Portal
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: move data
ms.devlang: NA
ms.date: 04/05/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 0f20a781717fb36e01a09d3ba9c7da690fa0bcc8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551877"
---
# <a name="export-an-azure-sql-database-to-a-bacpac-file"></a><span data-ttu-id="b06b1-103">Export an Azure SQL database to a BACPAC file</span><span class="sxs-lookup"><span data-stu-id="b06b1-103">Export an Azure SQL database to a BACPAC file</span></span>

<span data-ttu-id="b06b1-104">This article discusses exporting an Azure SQL database to a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span><span class="sxs-lookup"><span data-stu-id="b06b1-104">This article discusses exporting an Azure SQL database to a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="b06b1-105">This article discusses using the following methods:</span><span class="sxs-lookup"><span data-stu-id="b06b1-105">This article discusses using the following methods:</span></span>
- <span data-ttu-id="b06b1-106">The [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b06b1-106">The [Azure portal](https://portal.azure.com)</span></span>
- <span data-ttu-id="b06b1-107">the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility</span><span class="sxs-lookup"><span data-stu-id="b06b1-107">the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility</span></span>
- <span data-ttu-id="b06b1-108">the [New-AzureRmSqlDatabaseExport](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/new-azurermsqldatabaseexport) cmdlet</span><span class="sxs-lookup"><span data-stu-id="b06b1-108">the [New-AzureRmSqlDatabaseExport](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/new-azurermsqldatabaseexport) cmdlet</span></span>
- <span data-ttu-id="b06b1-109">the [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) wizard in [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span><span class="sxs-lookup"><span data-stu-id="b06b1-109">the [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) wizard in [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b06b1-110">Azure SQL Database Automated Export is now in preview and will be retired on March 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="b06b1-110">Azure SQL Database Automated Export is now in preview and will be retired on March 1, 2017.</span></span> <span data-ttu-id="b06b1-111">Starting December 1, 2016, you will no longer be able to configure automated export on any SQL database.</span><span class="sxs-lookup"><span data-stu-id="b06b1-111">Starting December 1, 2016, you will no longer be able to configure automated export on any SQL database.</span></span> <span data-ttu-id="b06b1-112">All your existing automated export jobs will continue to work until March 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="b06b1-112">All your existing automated export jobs will continue to work until March 1, 2017.</span></span> <span data-ttu-id="b06b1-113">After December 1, 2016, you can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) to archive SQL databases periodically using PowerShell periodically according to a schedule of your choice.</span><span class="sxs-lookup"><span data-stu-id="b06b1-113">After December 1, 2016, you can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) to archive SQL databases periodically using PowerShell periodically according to a schedule of your choice.</span></span> <span data-ttu-id="b06b1-114">For a sample script, you can download the [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.</span><span class="sxs-lookup"><span data-stu-id="b06b1-114">For a sample script, you can download the [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.</span></span>
>

> [!IMPORTANT] 
> <span data-ttu-id="b06b1-115">Azure SQL Database Automated Export is now in preview and will be retired on March 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="b06b1-115">Azure SQL Database Automated Export is now in preview and will be retired on March 1, 2017.</span></span> <span data-ttu-id="b06b1-116">Starting December 1, 2016, you will no longer be able to configure automated export on any SQL database.</span><span class="sxs-lookup"><span data-stu-id="b06b1-116">Starting December 1, 2016, you will no longer be able to configure automated export on any SQL database.</span></span> <span data-ttu-id="b06b1-117">All your existing automated export jobs will continue to work until March 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="b06b1-117">All your existing automated export jobs will continue to work until March 1, 2017.</span></span> <span data-ttu-id="b06b1-118">After December 1, 2016, you can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) to archive SQL databases periodically using PowerShell periodically according to a schedule of your choice.</span><span class="sxs-lookup"><span data-stu-id="b06b1-118">After December 1, 2016, you can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) to archive SQL databases periodically using PowerShell periodically according to a schedule of your choice.</span></span> <span data-ttu-id="b06b1-119">For a sample script, you can download the [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.</span><span class="sxs-lookup"><span data-stu-id="b06b1-119">For a sample script, you can download the [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.</span></span>
>

## <a name="overview"></a><span data-ttu-id="b06b1-120">Overview</span><span class="sxs-lookup"><span data-stu-id="b06b1-120">Overview</span></span>

<span data-ttu-id="b06b1-121">When you need to export a database for archiving or for moving to another platform, you can export the database schema and data to a BACPAC file.</span><span class="sxs-lookup"><span data-stu-id="b06b1-121">When you need to export a database for archiving or for moving to another platform, you can export the database schema and data to a BACPAC file.</span></span> <span data-ttu-id="b06b1-122">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="b06b1-122">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="b06b1-123">A BACPAC file can be stored in Azure blob storage or in local storage in an on-premises location and later imported back into Azure SQL Database or into a SQL Server on-premises installation.</span><span class="sxs-lookup"><span data-stu-id="b06b1-123">A BACPAC file can be stored in Azure blob storage or in local storage in an on-premises location and later imported back into Azure SQL Database or into a SQL Server on-premises installation.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b06b1-124">If you are exporting from SQL Server as a prelude to migration to Azure SQL Database, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="b06b1-124">If you are exporting from SQL Server as a prelude to migration to Azure SQL Database, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>
> 

## <a name="considerations"></a><span data-ttu-id="b06b1-125">Considerations</span><span class="sxs-lookup"><span data-stu-id="b06b1-125">Considerations</span></span>

* <span data-ttu-id="b06b1-126">For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export, or that you are exporting from a [transactionally consistent copy](sql-database-copy.md) of your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="b06b1-126">For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export, or that you are exporting from a [transactionally consistent copy](sql-database-copy.md) of your Azure SQL database.</span></span>
* <span data-ttu-id="b06b1-127">If you are exporting to blob storage, the maximum size of a BACPAC file is 200 GB.</span><span class="sxs-lookup"><span data-stu-id="b06b1-127">If you are exporting to blob storage, the maximum size of a BACPAC file is 200 GB.</span></span> <span data-ttu-id="b06b1-128">To archive a larger BACPAC file, export to local storage.</span><span class="sxs-lookup"><span data-stu-id="b06b1-128">To archive a larger BACPAC file, export to local storage.</span></span>
* <span data-ttu-id="b06b1-129">Exporting a BACPAC file to Azure premium storage using the methods discussed in this article is not supported.</span><span class="sxs-lookup"><span data-stu-id="b06b1-129">Exporting a BACPAC file to Azure premium storage using the methods discussed in this article is not supported.</span></span>
* <span data-ttu-id="b06b1-130">If the export operation from Azure SQL Database exceeds 20 hours, it may be canceled.</span><span class="sxs-lookup"><span data-stu-id="b06b1-130">If the export operation from Azure SQL Database exceeds 20 hours, it may be canceled.</span></span> <span data-ttu-id="b06b1-131">To increase performance during export, you can:</span><span class="sxs-lookup"><span data-stu-id="b06b1-131">To increase performance during export, you can:</span></span>
  * <span data-ttu-id="b06b1-132">Temporarily increase your service level.</span><span class="sxs-lookup"><span data-stu-id="b06b1-132">Temporarily increase your service level.</span></span>
  * <span data-ttu-id="b06b1-133">Cease all read and write activity during the export.</span><span class="sxs-lookup"><span data-stu-id="b06b1-133">Cease all read and write activity during the export.</span></span>
  * <span data-ttu-id="b06b1-134">Use a [clustered index](https://msdn.microsoft.com/library/ms190457.aspx) with non-null values on all large tables.</span><span class="sxs-lookup"><span data-stu-id="b06b1-134">Use a [clustered index](https://msdn.microsoft.com/library/ms190457.aspx) with non-null values on all large tables.</span></span> <span data-ttu-id="b06b1-135">Without clustered indexes, an export may fail if it takes longer than 6-12 hours.</span><span class="sxs-lookup"><span data-stu-id="b06b1-135">Without clustered indexes, an export may fail if it takes longer than 6-12 hours.</span></span> <span data-ttu-id="b06b1-136">This is because the export service needs to complete a table scan to try to export entire table.</span><span class="sxs-lookup"><span data-stu-id="b06b1-136">This is because the export service needs to complete a table scan to try to export entire table.</span></span> <span data-ttu-id="b06b1-137">A good way to determine if your tables are optimized for export is to run **DBCC SHOW_STATISTICS** and make sure that the *RANGE_HI_KEY* is not null and its value has good distribution.</span><span class="sxs-lookup"><span data-stu-id="b06b1-137">A good way to determine if your tables are optimized for export is to run **DBCC SHOW_STATISTICS** and make sure that the *RANGE_HI_KEY* is not null and its value has good distribution.</span></span> <span data-ttu-id="b06b1-138">For details, see [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).</span><span class="sxs-lookup"><span data-stu-id="b06b1-138">For details, see [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b06b1-139">BACPACs are not intended to be used for backup and restore operations.</span><span class="sxs-lookup"><span data-stu-id="b06b1-139">BACPACs are not intended to be used for backup and restore operations.</span></span> <span data-ttu-id="b06b1-140">Azure SQL Database automatically creates backups for every user database.</span><span class="sxs-lookup"><span data-stu-id="b06b1-140">Azure SQL Database automatically creates backups for every user database.</span></span> <span data-ttu-id="b06b1-141">For details, see [Business Continuity Overview](sql-database-business-continuity.md) and [SQL Database backups](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="b06b1-141">For details, see [Business Continuity Overview](sql-database-business-continuity.md) and [SQL Database backups](sql-database-automated-backups.md).</span></span>  
> 

## <a name="azure-portal"></a><span data-ttu-id="b06b1-142">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b06b1-142">Azure portal</span></span>

<span data-ttu-id="b06b1-143">To export a database using the Azure portal, open the page for your database and click **Export** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="b06b1-143">To export a database using the Azure portal, open the page for your database and click **Export** on the toolbar.</span></span> <span data-ttu-id="b06b1-144">Specify the \*.bacpac filename, provide the Azure storage account and container for the export, and provide the credentials to connect to the source database.</span><span class="sxs-lookup"><span data-stu-id="b06b1-144">Specify the \*.bacpac filename, provide the Azure storage account and container for the export, and provide the credentials to connect to the source database.</span></span>  

   ![Database export](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-export/database-export.png)

<span data-ttu-id="b06b1-146">To monitor the progress of the export operation, open the page for the logical server containing the database being exported.</span><span class="sxs-lookup"><span data-stu-id="b06b1-146">To monitor the progress of the export operation, open the page for the logical server containing the database being exported.</span></span> <span data-ttu-id="b06b1-147">Scroll down to **Operations** and then click **Import/Export** history.</span><span class="sxs-lookup"><span data-stu-id="b06b1-147">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

## <a name="sqlpackage-utility"></a><span data-ttu-id="b06b1-148">SQLPackage utility</span><span class="sxs-lookup"><span data-stu-id="b06b1-148">SQLPackage utility</span></span>

<span data-ttu-id="b06b1-149">To export a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Export parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="b06b1-149">To export a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Export parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties).</span></span> <span data-ttu-id="b06b1-150">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span><span class="sxs-lookup"><span data-stu-id="b06b1-150">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="b06b1-151">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span><span class="sxs-lookup"><span data-stu-id="b06b1-151">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="b06b1-152">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="b06b1-152">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

## <a name="sql-server-management-studio"></a><span data-ttu-id="b06b1-153">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b06b1-153">SQL Server Management Studio</span></span>

<span data-ttu-id="b06b1-154">The newest versions of SQL Server Management Studio also provide a wizard to export an Azure SQL Database to a bacpac file.</span><span class="sxs-lookup"><span data-stu-id="b06b1-154">The newest versions of SQL Server Management Studio also provide a wizard to export an Azure SQL Database to a bacpac file.</span></span> <span data-ttu-id="b06b1-155">See the [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).</span><span class="sxs-lookup"><span data-stu-id="b06b1-155">See the [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).</span></span>

## <a name="powershell"></a><span data-ttu-id="b06b1-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b06b1-156">PowerShell</span></span>

<span data-ttu-id="b06b1-157">Use the [New-AzureRmSqlDatabaseImport](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/new-azurermsqldatabaseexport) cmdlet to submit an export database request to the Azure SQL Database service.</span><span class="sxs-lookup"><span data-stu-id="b06b1-157">Use the [New-AzureRmSqlDatabaseImport](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/new-azurermsqldatabaseexport) cmdlet to submit an export database request to the Azure SQL Database service.</span></span> <span data-ttu-id="b06b1-158">Depending on the size of your database, the export operation may take some time to complete.</span><span class="sxs-lookup"><span data-stu-id="b06b1-158">Depending on the size of your database, the export operation may take some time to complete.</span></span>

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

<span data-ttu-id="b06b1-159">To check the status of the export request, use the [Get-AzureRmSqlDatabaseImportExportStatus](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/get-azurermsqldatabaseimportexportstatus) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b06b1-159">To check the status of the export request, use the [Get-AzureRmSqlDatabaseImportExportStatus](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="b06b1-160">Running this immediately after the request usually returns **Status: InProgress**.</span><span class="sxs-lookup"><span data-stu-id="b06b1-160">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="b06b1-161">When you see **Status: Succeeded** the export is complete.</span><span class="sxs-lookup"><span data-stu-id="b06b1-161">When you see **Status: Succeeded** the export is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

### <a name="export-sql-database-example"></a><span data-ttu-id="b06b1-162">Export SQL database example</span><span class="sxs-lookup"><span data-stu-id="b06b1-162">Export SQL database example</span></span>
<span data-ttu-id="b06b1-163">The following example exports an existing Azure SQL database to a BACPAC and then shows how to check the status of the export operation.</span><span class="sxs-lookup"><span data-stu-id="b06b1-163">The following example exports an existing Azure SQL database to a BACPAC and then shows how to check the status of the export operation.</span></span>

<span data-ttu-id="b06b1-164">To run the example, there are a few variables you need to replace with the specific values for your database and storage account.</span><span class="sxs-lookup"><span data-stu-id="b06b1-164">To run the example, there are a few variables you need to replace with the specific values for your database and storage account.</span></span> <span data-ttu-id="b06b1-165">In the [Azure portal](https://portal.azure.com), browse to your storage account to get the storage account name, blob container name, and key value.</span><span class="sxs-lookup"><span data-stu-id="b06b1-165">In the [Azure portal](https://portal.azure.com), browse to your storage account to get the storage account name, blob container name, and key value.</span></span> <span data-ttu-id="b06b1-166">You can find the key by clicking **Access keys** on your storage account blade.</span><span class="sxs-lookup"><span data-stu-id="b06b1-166">You can find the key by clicking **Access keys** on your storage account blade.</span></span>

<span data-ttu-id="b06b1-167">Replace the following `VARIABLE-VALUES` with values for your specific Azure resources.</span><span class="sxs-lookup"><span data-stu-id="b06b1-167">Replace the following `VARIABLE-VALUES` with values for your specific Azure resources.</span></span> <span data-ttu-id="b06b1-168">The database name is the existing database you want to export.</span><span class="sxs-lookup"><span data-stu-id="b06b1-168">The database name is the existing database you want to export.</span></span>

```powershell
$subscriptionId = "YOUR AZURE SUBSCRIPTION ID"

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Database to export
$DatabaseName = "DATABASE-NAME"
$ResourceGroupName = "RESOURCE-GROUP-NAME"
$ServerName = "SERVER-NAME
$serverAdmin = "ADMIN-NAME"
$serverPassword = "ADMIN-PASSWORD" 
$securePassword = ConvertTo-SecureString -String $serverPassword -AsPlainText -Force
$creds = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $serverAdmin, $securePassword

# Generate a unique filename for the BACPAC
$bacpacFilename = $DatabaseName + (Get-Date).ToString("yyyyMMddHHmm") + ".bacpac"

# Storage account info for the BACPAC
$BaseStorageUri = "https://STORAGE-NAME.blob.core.windows.net/BLOB-CONTAINER-NAME/"
$BacpacUri = $BaseStorageUri + $bacpacFilename
$StorageKeytype = "StorageAccessKey"
$StorageKey = "YOUR STORAGE KEY"

$exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
  -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
  -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password

$exportRequest

# Check status of the export
Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
```

## <a name="next-steps"></a><span data-ttu-id="b06b1-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="b06b1-169">Next steps</span></span>

* <span data-ttu-id="b06b1-170">To learn about long-term backup retention of an Azure SQL database backup as an alternative to exported a database for archive purposes, see [Long-term backup retention](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="b06b1-170">To learn about long-term backup retention of an Azure SQL database backup as an alternative to exported a database for archive purposes, see [Long-term backup retention](sql-database-long-term-retention.md).</span></span>
- <span data-ttu-id="b06b1-171">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="b06b1-171">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="b06b1-172">To learn about importing a BACPAC to a SQL Server database, see [Import a BACPCAC to a SQL Server database](https://msdn.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="b06b1-172">To learn about importing a BACPAC to a SQL Server database, see [Import a BACPCAC to a SQL Server database](https://msdn.microsoft.com/library/hh710052.aspx).</span></span>
* <span data-ttu-id="b06b1-173">To learn about exporting a BACPAC from a SQL Server database, see [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) and [Migrate your first database](sql-database-migrate-your-sql-server-database.md).</span><span class="sxs-lookup"><span data-stu-id="b06b1-173">To learn about exporting a BACPAC from a SQL Server database, see [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) and [Migrate your first database](sql-database-migrate-your-sql-server-database.md).</span></span>

