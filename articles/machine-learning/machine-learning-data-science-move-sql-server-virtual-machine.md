---
title: Move data to SQL Server on an Azure virtual machine| Microsoft Docs
description: Move data from flat files or from an on-premises SQL Server to SQL Server on Azure VM.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 064657b1b126bb2e9609f37aa5760be0423468bb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556420"
---
# <a name="move-data-to-sql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="d6665-103">Move data to SQL Server on an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="d6665-103">Move data to SQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="d6665-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premise SQL Server to SQL Server on an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d6665-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premise SQL Server to SQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="d6665-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span><span class="sxs-lookup"><span data-stu-id="d6665-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span></span>

<span data-ttu-id="d6665-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d6665-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="d6665-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span><span class="sxs-lookup"><span data-stu-id="d6665-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="d6665-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d6665-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="d6665-109"><b>SOURCE</b></span><span class="sxs-lookup"><span data-stu-id="d6665-109"><b>SOURCE</b></span></span> | <span data-ttu-id="d6665-110"><b>DESTINATION: SQL Server on Azure VM</b></span><span class="sxs-lookup"><span data-stu-id="d6665-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="d6665-111"><b>Flat File</b></span><span class="sxs-lookup"><span data-stu-id="d6665-111"><b>Flat File</b></span></span> |<span data-ttu-id="d6665-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span><span class="sxs-lookup"><span data-stu-id="d6665-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="d6665-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span><span class="sxs-lookup"><span data-stu-id="d6665-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="d6665-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="d6665-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="d6665-115"><b>On-Premises SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="d6665-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="d6665-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span><span class="sxs-lookup"><span data-stu-id="d6665-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="d6665-117">2. <a href="#export-flat-file">Export to a flat File </a></span><span class="sxs-lookup"><span data-stu-id="d6665-117">2. <a href="#export-flat-file">Export to a flat File </a></span></span><br> <span data-ttu-id="d6665-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span><span class="sxs-lookup"><span data-stu-id="d6665-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="d6665-119">4. <a href="#sql-backup">Database back up and restore </a></span><span class="sxs-lookup"><span data-stu-id="d6665-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="d6665-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span><span class="sxs-lookup"><span data-stu-id="d6665-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="d6665-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span><span class="sxs-lookup"><span data-stu-id="d6665-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span></span> <span data-ttu-id="d6665-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d6665-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <a name="prereqs"></a><span data-ttu-id="d6665-123">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d6665-123">Prerequisites</span></span>
<span data-ttu-id="d6665-124">This tutorial assumes you have:</span><span class="sxs-lookup"><span data-stu-id="d6665-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="d6665-125">An **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="d6665-125">An **Azure subscription**.</span></span> <span data-ttu-id="d6665-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6665-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d6665-127">An **Azure storage account**.</span><span class="sxs-lookup"><span data-stu-id="d6665-127">An **Azure storage account**.</span></span> <span data-ttu-id="d6665-128">You will use an Azure storage account for storing the data in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6665-128">You will use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="d6665-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) article.</span><span class="sxs-lookup"><span data-stu-id="d6665-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="d6665-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span><span class="sxs-lookup"><span data-stu-id="d6665-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="d6665-131">See [Manage your storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="d6665-131">See [Manage your storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="d6665-132">Provisioned **SQL Server on an Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="d6665-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="d6665-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="d6665-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="d6665-134">Installed and configured **Azure PowerShell** locally.</span><span class="sxs-lookup"><span data-stu-id="d6665-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="d6665-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="d6665-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

## <a name="filesource_to_sqlonazurevm"></a> <span data-ttu-id="d6665-136">Moving data from a flat file source to SQL Server on an Azure VM</span><span class="sxs-lookup"><span data-stu-id="d6665-136">Moving data from a flat file source to SQL Server on an Azure VM</span></span>
<span data-ttu-id="d6665-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span><span class="sxs-lookup"><span data-stu-id="d6665-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span></span>

1. [<span data-ttu-id="d6665-138">Command-line bulk copy utility (BCP)</span><span class="sxs-lookup"><span data-stu-id="d6665-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="d6665-139">Bulk Insert SQL Query </span><span class="sxs-lookup"><span data-stu-id="d6665-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="d6665-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span><span class="sxs-lookup"><span data-stu-id="d6665-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a><span data-ttu-id="d6665-141">Command-line bulk copy utility (BCP)</span><span class="sxs-lookup"><span data-stu-id="d6665-141">Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="d6665-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span><span class="sxs-lookup"><span data-stu-id="d6665-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span></span> <span data-ttu-id="d6665-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span><span class="sxs-lookup"><span data-stu-id="d6665-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="d6665-144">**Where should my data be for BCP?**</span><span class="sxs-lookup"><span data-stu-id="d6665-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="d6665-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span><span class="sxs-lookup"><span data-stu-id="d6665-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="d6665-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="d6665-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="d6665-147">Ensure that the database and the tables are created on the target SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="d6665-147">Ensure that the database and the tables are created on the target SQL Server database.</span></span> <span data-ttu-id="d6665-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span><span class="sxs-lookup"><span data-stu-id="d6665-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="d6665-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span><span class="sxs-lookup"><span data-stu-id="d6665-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="d6665-150">Insert the data into the database using the bcp command as follows.</span><span class="sxs-lookup"><span data-stu-id="d6665-150">Insert the data into the database using the bcp command as follows.</span></span> <span data-ttu-id="d6665-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span><span class="sxs-lookup"><span data-stu-id="d6665-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="d6665-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span><span class="sxs-lookup"><span data-stu-id="d6665-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span></span>
>
>

### <a name="insert-tables-bulkquery-parallel"></a><span data-ttu-id="d6665-153">Parallelizing Inserts for Faster Data Movement</span><span class="sxs-lookup"><span data-stu-id="d6665-153">Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="d6665-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span><span class="sxs-lookup"><span data-stu-id="d6665-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="d6665-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span><span class="sxs-lookup"><span data-stu-id="d6665-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="d6665-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="d6665-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="d6665-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span><span class="sxs-lookup"><span data-stu-id="d6665-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for the script to execute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all to complete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting the information back from the jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset the execution policy


### <a name="insert-tables-bulkquery"></a><span data-ttu-id="d6665-158">Bulk Insert SQL Query</span><span class="sxs-lookup"><span data-stu-id="d6665-158">Bulk Insert SQL Query</span></span>
<span data-ttu-id="d6665-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span><span class="sxs-lookup"><span data-stu-id="d6665-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="d6665-160">Here are some sample commands for Bulk Insert are as below:</span><span class="sxs-lookup"><span data-stu-id="d6665-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="d6665-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span><span class="sxs-lookup"><span data-stu-id="d6665-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span></span> <span data-ttu-id="d6665-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span><span class="sxs-lookup"><span data-stu-id="d6665-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="d6665-163">Import data using bulk import statements:</span><span class="sxs-lookup"><span data-stu-id="d6665-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be the row separator in your data
        )

### <a name="sql-builtin-utilities"></a><span data-ttu-id="d6665-164">Built-in Utilities in SQL Server</span><span class="sxs-lookup"><span data-stu-id="d6665-164">Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="d6665-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span><span class="sxs-lookup"><span data-stu-id="d6665-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="d6665-166">SSIS is available in two studio environments.</span><span class="sxs-lookup"><span data-stu-id="d6665-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="d6665-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="d6665-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="d6665-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="d6665-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="d6665-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="d6665-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <a name="sqlonprem_to_sqlonazurevm"></a><span data-ttu-id="d6665-170">Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span><span class="sxs-lookup"><span data-stu-id="d6665-170">Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span></span>
<span data-ttu-id="d6665-171">You can also use the following migration strategies:</span><span class="sxs-lookup"><span data-stu-id="d6665-171">You can also use the following migration strategies:</span></span>

1. [<span data-ttu-id="d6665-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span><span class="sxs-lookup"><span data-stu-id="d6665-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="d6665-173">Export to Flat File</span><span class="sxs-lookup"><span data-stu-id="d6665-173">Export to Flat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="d6665-174">SQL Database Migration Wizard</span><span class="sxs-lookup"><span data-stu-id="d6665-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="d6665-175">Database back up and restore</span><span class="sxs-lookup"><span data-stu-id="d6665-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="d6665-176">We describe each of these below:</span><span class="sxs-lookup"><span data-stu-id="d6665-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a><span data-ttu-id="d6665-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span><span class="sxs-lookup"><span data-stu-id="d6665-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>
<span data-ttu-id="d6665-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="d6665-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span></span> <span data-ttu-id="d6665-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d6665-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <a name="export-flat-file"></a><span data-ttu-id="d6665-180">Export to Flat File</span><span class="sxs-lookup"><span data-stu-id="d6665-180">Export to Flat File</span></span>
<span data-ttu-id="d6665-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="d6665-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="d6665-182">This document will cover the Bulk Copy Program (BCP) as an example.</span><span class="sxs-lookup"><span data-stu-id="d6665-182">This document will cover the Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="d6665-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span><span class="sxs-lookup"><span data-stu-id="d6665-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span></span>

1. <span data-ttu-id="d6665-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span><span class="sxs-lookup"><span data-stu-id="d6665-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="d6665-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span><span class="sxs-lookup"><span data-stu-id="d6665-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span></span>
3. <span data-ttu-id="d6665-186">Create a format file for describing the table schema of the data being exported/imported.</span><span class="sxs-lookup"><span data-stu-id="d6665-186">Create a format file for describing the table schema of the data being exported/imported.</span></span> <span data-ttu-id="d6665-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6665-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="d6665-188">Format file generation when running BCP from the SQL Server machine</span><span class="sxs-lookup"><span data-stu-id="d6665-188">Format file generation when running BCP from the SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="d6665-189">Format file generation when running BCP remotely against a SQL Server</span><span class="sxs-lookup"><span data-stu-id="d6665-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="d6665-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d6665-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span></span>

### <a name="sql-migration"></a><span data-ttu-id="d6665-191">SQL Database Migration Wizard</span><span class="sxs-lookup"><span data-stu-id="d6665-191">SQL Database Migration Wizard</span></span>
<span data-ttu-id="d6665-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span><span class="sxs-lookup"><span data-stu-id="d6665-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span></span> <span data-ttu-id="d6665-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span><span class="sxs-lookup"><span data-stu-id="d6665-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="d6665-194">It uses bulk copy (BCP) under the covers.</span><span class="sxs-lookup"><span data-stu-id="d6665-194">It uses bulk copy (BCP) under the covers.</span></span> <span data-ttu-id="d6665-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span><span class="sxs-lookup"><span data-stu-id="d6665-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span></span>  

![SQL Server Migration Wizard][2]

### <a name="sql-backup"></a><span data-ttu-id="d6665-197">Database back up and restore</span><span class="sxs-lookup"><span data-stu-id="d6665-197">Database back up and restore</span></span>
<span data-ttu-id="d6665-198">SQL Server supports:</span><span class="sxs-lookup"><span data-stu-id="d6665-198">SQL Server supports:</span></span>

1. <span data-ttu-id="d6665-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span><span class="sxs-lookup"><span data-stu-id="d6665-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="d6665-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span><span class="sxs-lookup"><span data-stu-id="d6665-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span></span> <span data-ttu-id="d6665-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6665-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="d6665-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span><span class="sxs-lookup"><span data-stu-id="d6665-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![SQL Server Import Tool][1]

## <a name="resources"></a><span data-ttu-id="d6665-204">Resources</span><span class="sxs-lookup"><span data-stu-id="d6665-204">Resources</span></span>
[<span data-ttu-id="d6665-205">Migrate a Database to SQL Server on an Azure VM</span><span class="sxs-lookup"><span data-stu-id="d6665-205">Migrate a Database to SQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="d6665-206">SQL Server on Azure Virtual Machines overview</span><span class="sxs-lookup"><span data-stu-id="d6665-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png


