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
# <a name="export-an-azure-sql-database-to-a-bacpac-file"></a>Export an Azure SQL database to a BACPAC file

This article discusses exporting an Azure SQL database to a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file. This article discusses using the following methods:
- The [Azure portal](https://portal.azure.com)
- the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility
- the [New-AzureRmSqlDatabaseExport](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/new-azurermsqldatabaseexport) cmdlet
- the [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) wizard in [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).

> [!IMPORTANT] 
> Azure SQL Database Automated Export is now in preview and will be retired on March 1, 2017. Starting December 1, 2016, you will no longer be able to configure automated export on any SQL database. All your existing automated export jobs will continue to work until March 1, 2017. After December 1, 2016, you can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) to archive SQL databases periodically using PowerShell periodically according to a schedule of your choice. For a sample script, you can download the [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.
>

> [!IMPORTANT] 
> Azure SQL Database Automated Export is now in preview and will be retired on March 1, 2017. Starting December 1, 2016, you will no longer be able to configure automated export on any SQL database. All your existing automated export jobs will continue to work until March 1, 2017. After December 1, 2016, you can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) to archive SQL databases periodically using PowerShell periodically according to a schedule of your choice. For a sample script, you can download the [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.
>

## <a name="overview"></a>Overview

When you need to export a database for archiving or for moving to another platform, you can export the database schema and data to a BACPAC file. A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database. A BACPAC file can be stored in Azure blob storage or in local storage in an on-premises location and later imported back into Azure SQL Database or into a SQL Server on-premises installation. 

> [!IMPORTANT]
> If you are exporting from SQL Server as a prelude to migration to Azure SQL Database, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).
> 

## <a name="considerations"></a>Considerations

* For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export, or that you are exporting from a [transactionally consistent copy](sql-database-copy.md) of your Azure SQL database.
* If you are exporting to blob storage, the maximum size of a BACPAC file is 200 GB. To archive a larger BACPAC file, export to local storage.
* Exporting a BACPAC file to Azure premium storage using the methods discussed in this article is not supported.
* If the export operation from Azure SQL Database exceeds 20 hours, it may be canceled. To increase performance during export, you can:
  * Temporarily increase your service level.
  * Cease all read and write activity during the export.
  * Use a [clustered index](https://msdn.microsoft.com/library/ms190457.aspx) with non-null values on all large tables. Without clustered indexes, an export may fail if it takes longer than 6-12 hours. This is because the export service needs to complete a table scan to try to export entire table. A good way to determine if your tables are optimized for export is to run **DBCC SHOW_STATISTICS** and make sure that the *RANGE_HI_KEY* is not null and its value has good distribution. For details, see [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> BACPACs are not intended to be used for backup and restore operations. Azure SQL Database automatically creates backups for every user database. For details, see [Business Continuity Overview](sql-database-business-continuity.md) and [SQL Database backups](sql-database-automated-backups.md).  
> 

## <a name="azure-portal"></a>Azure portal

To export a database using the Azure portal, open the page for your database and click **Export** on the toolbar. Specify the *.bacpac filename, provide the Azure storage account and container for the export, and provide the credentials to connect to the source database.  

   ![Database export](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-export/database-export.png)

To monitor the progress of the export operation, open the page for the logical server containing the database being exported. Scroll down to **Operations** and then click **Import/Export** history.

## <a name="sqlpackage-utility"></a>SQLPackage utility

To export a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Export parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.

We recommend the use of the SQLPackage utility for scale and performance in most production environments. For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

The newest versions of SQL Server Management Studio also provide a wizard to export an Azure SQL Database to a bacpac file. See the [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="powershell"></a>PowerShell

Use the [New-AzureRmSqlDatabaseImport](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/new-azurermsqldatabaseexport) cmdlet to submit an export database request to the Azure SQL Database service. Depending on the size of your database, the export operation may take some time to complete.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

To check the status of the export request, use the [Get-AzureRmSqlDatabaseImportExportStatus](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/get-azurermsqldatabaseimportexportstatus) cmdlet. Running this immediately after the request usually returns **Status: InProgress**. When you see **Status: Succeeded** the export is complete.

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

### <a name="export-sql-database-example"></a>Export SQL database example
The following example exports an existing Azure SQL database to a BACPAC and then shows how to check the status of the export operation.

To run the example, there are a few variables you need to replace with the specific values for your database and storage account. In the [Azure portal](https://portal.azure.com), browse to your storage account to get the storage account name, blob container name, and key value. You can find the key by clicking **Access keys** on your storage account blade.

Replace the following `VARIABLE-VALUES` with values for your specific Azure resources. The database name is the existing database you want to export.

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

## <a name="next-steps"></a>Next steps

* To learn about long-term backup retention of an Azure SQL database backup as an alternative to exported a database for archive purposes, see [Long-term backup retention](sql-database-long-term-retention.md).
- For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* To learn about importing a BACPAC to a SQL Server database, see [Import a BACPCAC to a SQL Server database](https://msdn.microsoft.com/library/hh710052.aspx).
* To learn about exporting a BACPAC from a SQL Server database, see [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) and [Migrate your first database](sql-database-migrate-your-sql-server-database.md).

