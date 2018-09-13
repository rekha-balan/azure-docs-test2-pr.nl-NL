---
title: Import a BACPAC file to create an Azure SQL database | Microsoft Docs
description: Create a newAzure SQL database by importing a BACPAC file.
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: move data
ms.devlang: NA
ms.date: 04/07/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 44502a1e12a0b5772e536e6e9dc5c9349a271d2f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555407"
---
# <a name="import-a-bacpac-file-to-a-new-azure-sql-database"></a><span data-ttu-id="37737-103">Import a BACPAC file to a new Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="37737-103">Import a BACPAC file to a new Azure SQL Database</span></span>

<span data-ttu-id="37737-104">This article discusses importing a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file to a new Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="37737-104">This article discusses importing a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file to a new Azure SQL database.</span></span> <span data-ttu-id="37737-105">This article discusses using the following methods:</span><span class="sxs-lookup"><span data-stu-id="37737-105">This article discusses using the following methods:</span></span>
- <span data-ttu-id="37737-106">The [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="37737-106">The [Azure portal](https://portal.azure.com)</span></span>
- <span data-ttu-id="37737-107">the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility</span><span class="sxs-lookup"><span data-stu-id="37737-107">the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility</span></span>
- <span data-ttu-id="37737-108">the [New-AzureRmSqlDatabaseImport](https://docs.microsoft.com/powershell/module/azurerm.sql/new-azurermsqldatabaseimport?view=azurermps-3.7.0) cmdlet</span><span class="sxs-lookup"><span data-stu-id="37737-108">the [New-AzureRmSqlDatabaseImport](https://docs.microsoft.com/powershell/module/azurerm.sql/new-azurermsqldatabaseimport?view=azurermps-3.7.0) cmdlet</span></span>

## <a name="overview"></a><span data-ttu-id="37737-109">Overview</span><span class="sxs-lookup"><span data-stu-id="37737-109">Overview</span></span>

<span data-ttu-id="37737-110">When you need to import a database from an archive or when migrating from another platform, you can import the database schema and data from a BACPAC file.</span><span class="sxs-lookup"><span data-stu-id="37737-110">When you need to import a database from an archive or when migrating from another platform, you can import the database schema and data from a BACPAC file.</span></span> <span data-ttu-id="37737-111">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="37737-111">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="37737-112">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span><span class="sxs-lookup"><span data-stu-id="37737-112">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="37737-113">To maximize the import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale to down as appropriate after the import is successful.</span><span class="sxs-lookup"><span data-stu-id="37737-113">To maximize the import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale to down as appropriate after the import is successful.</span></span> <span data-ttu-id="37737-114">Also, the database compatibility level after the import is based on the compatibility level of the source database.</span><span class="sxs-lookup"><span data-stu-id="37737-114">Also, the database compatibility level after the import is based on the compatibility level of the source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="37737-115">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span><span class="sxs-lookup"><span data-stu-id="37737-115">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="37737-116">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="37737-116">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="37737-117">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span><span class="sxs-lookup"><span data-stu-id="37737-117">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="37737-118">To import a BACPAC to a new database, you must first create an Azure SQL Database logical server.</span><span class="sxs-lookup"><span data-stu-id="37737-118">To import a BACPAC to a new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="37737-119">For a tutorial showing you how to migrate a SQL Server database to Azure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="37737-119">For a tutorial showing you how to migrate a SQL Server database to Azure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="azure-portal"></a><span data-ttu-id="37737-120">Azure portal</span><span class="sxs-lookup"><span data-stu-id="37737-120">Azure portal</span></span>

<span data-ttu-id="37737-121">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="37737-121">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="37737-122">Import using the Azure portal only supports importing a BACPAC file from Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="37737-122">Import using the Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="37737-123">To import a database using the Azure portal, open the page for your database and click **Import** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="37737-123">To import a database using the Azure portal, open the page for your database and click **Import** on the toolbar.</span></span> <span data-ttu-id="37737-124">Specify the \*.bacpac filename, provide the Azure storage account and container for the bacpac, and provide the credentials to connect to the source database.</span><span class="sxs-lookup"><span data-stu-id="37737-124">Specify the \*.bacpac filename, provide the Azure storage account and container for the bacpac, and provide the credentials to connect to the source database.</span></span>  

   ![Database import](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-import/import.png)

<span data-ttu-id="37737-126">To monitor the progress of the import operation, open the page for the logical server containing the database being imported.</span><span class="sxs-lookup"><span data-stu-id="37737-126">To monitor the progress of the import operation, open the page for the logical server containing the database being imported.</span></span> <span data-ttu-id="37737-127">Scroll down to **Operations** and then click **Import/Export** history.</span><span class="sxs-lookup"><span data-stu-id="37737-127">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-the-progress-of-the-import-operation"></a><span data-ttu-id="37737-128">Monitor the progress of the import operation</span><span class="sxs-lookup"><span data-stu-id="37737-128">Monitor the progress of the import operation</span></span>
1. <span data-ttu-id="37737-129">Click **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="37737-129">Click **SQL servers**.</span></span>
2. <span data-ttu-id="37737-130">Click the server you are restoring to.</span><span class="sxs-lookup"><span data-stu-id="37737-130">Click the server you are restoring to.</span></span>
3. <span data-ttu-id="37737-131">In the SQL server blade, in the Operations area, click **Import/Export history**:</span><span class="sxs-lookup"><span data-stu-id="37737-131">In the SQL server blade, in the Operations area, click **Import/Export history**:</span></span>
   
   <span data-ttu-id="37737-132">![import](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-import/import.png)
   ![import status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="37737-132">![import](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-import/import.png)
![import status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-import/import-status.png)</span></span>

4. <span data-ttu-id="37737-133">To verify the database is live on the server, click **SQL databases** and verify the new database is **Online**.</span><span class="sxs-lookup"><span data-stu-id="37737-133">To verify the database is live on the server, click **SQL databases** and verify the new database is **Online**.</span></span>

## <a name="sqlpackage"></a><span data-ttu-id="37737-134">SQLPackage</span><span class="sxs-lookup"><span data-stu-id="37737-134">SQLPackage</span></span>

<span data-ttu-id="37737-135">To import a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="37737-135">To import a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="37737-136">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span><span class="sxs-lookup"><span data-stu-id="37737-136">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="37737-137">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span><span class="sxs-lookup"><span data-stu-id="37737-137">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="37737-138">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="37737-138">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="37737-139">See the following SQLPackage command for a sample script for how to import the **AdventureWorks2008R2** database from local storage to an Azure SQL Database logical server, called **mynewserver20170403** in this example.</span><span class="sxs-lookup"><span data-stu-id="37737-139">See the following SQLPackage command for a sample script for how to import the **AdventureWorks2008R2** database from local storage to an Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="37737-140">This script shows the creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span><span class="sxs-lookup"><span data-stu-id="37737-140">This script shows the creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="37737-141">Change these values as appropriate to your environment.</span><span class="sxs-lookup"><span data-stu-id="37737-141">Change these values as appropriate to your environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage import](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="37737-143">An Azure SQL Database logical server listens on port 1433.</span><span class="sxs-lookup"><span data-stu-id="37737-143">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="37737-144">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span><span class="sxs-lookup"><span data-stu-id="37737-144">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

## <a name="powershell"></a><span data-ttu-id="37737-145">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37737-145">PowerShell</span></span>

<span data-ttu-id="37737-146">Use the [New-AzureRmSqlDatabaseImport](https://docs.microsoft.com/powershell/module/azurerm.sql/new-azurermsqldatabaseimport?view=azurermps-3.7.0) cmdlet to submit an import database request to the Azure SQL Database service.</span><span class="sxs-lookup"><span data-stu-id="37737-146">Use the [New-AzureRmSqlDatabaseImport](https://docs.microsoft.com/powershell/module/azurerm.sql/new-azurermsqldatabaseimport?view=azurermps-3.7.0) cmdlet to submit an import database request to the Azure SQL Database service.</span></span> <span data-ttu-id="37737-147">Depending on the size of your database, the import operation may take some time to complete.</span><span class="sxs-lookup"><span data-stu-id="37737-147">Depending on the size of your database, the import operation may take some time to complete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="37737-148">To check the status of the import request, use the [Get-AzureRmSqlDatabaseImportExportStatus](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/get-azurermsqldatabaseimportexportstatus) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="37737-148">To check the status of the import request, use the [Get-AzureRmSqlDatabaseImportExportStatus](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.7.0/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="37737-149">Running this immediately after the request usually returns **Status: InProgress**.</span><span class="sxs-lookup"><span data-stu-id="37737-149">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="37737-150">When you see **Status: Succeeded** the import is complete.</span><span class="sxs-lookup"><span data-stu-id="37737-150">When you see **Status: Succeeded** the import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

## <a name="next-steps"></a><span data-ttu-id="37737-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="37737-151">Next steps</span></span>
* <span data-ttu-id="37737-152">To learn how to connect to and query an imported SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="37737-152">To learn how to connect to and query an imported SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="37737-153">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="37737-153">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="37737-154">For a discussion of the entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="37737-154">For a discussion of the entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>







