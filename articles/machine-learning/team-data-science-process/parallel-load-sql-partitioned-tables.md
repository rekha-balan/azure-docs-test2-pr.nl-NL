---
title: Build and optimize tables for fast parallel import of data into a SQL Server on an Azure VM| Microsoft Docs
description: Parallel Bulk Data Import Using SQL Partition Tables
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: deguhath
ms.openlocfilehash: f87bc1d8140bea9ebb09e45d42b27e201b474026
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867706"
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="5ad57-103">Parallel Bulk Data Import Using SQL Partition Tables</span><span class="sxs-lookup"><span data-stu-id="5ad57-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="5ad57-104">This document describes how to build partitioned tables for fast parallel bulk importing of data to a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="5ad57-104">This document describes how to build partitioned tables for fast parallel bulk importing of data to a SQL Server database.</span></span> <span data-ttu-id="5ad57-105">For big data loading/transfer to a SQL database, importing data to the SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span><span class="sxs-lookup"><span data-stu-id="5ad57-105">For big data loading/transfer to a SQL database, importing data to the SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="5ad57-106">Create a new database and a set of filegroups</span><span class="sxs-lookup"><span data-stu-id="5ad57-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="5ad57-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span><span class="sxs-lookup"><span data-stu-id="5ad57-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="5ad57-108">Add database filegroups to the database, which holds the partitioned physical files.</span><span class="sxs-lookup"><span data-stu-id="5ad57-108">Add database filegroups to the database, which holds the partitioned physical files.</span></span> 
* <span data-ttu-id="5ad57-109">This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if the database exists already.</span><span class="sxs-lookup"><span data-stu-id="5ad57-109">This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if the database exists already.</span></span>
* <span data-ttu-id="5ad57-110">Add one or more files (as needed) to each database filegroup.</span><span class="sxs-lookup"><span data-stu-id="5ad57-110">Add one or more files (as needed) to each database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5ad57-111">Specify the target filegroup, which holds data for this partition and the physical database file name(s) where the filegroup data is stored.</span><span class="sxs-lookup"><span data-stu-id="5ad57-111">Specify the target filegroup, which holds data for this partition and the physical database file name(s) where the filegroup data is stored.</span></span>
  > 
  > 

<span data-ttu-id="5ad57-112">The following example creates a new database with three filegroups other than the primary and log groups, containing one physical file in each.</span><span class="sxs-lookup"><span data-stu-id="5ad57-112">The following example creates a new database with three filegroups other than the primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="5ad57-113">The database files are created in the default SQL Server Data folder, as configured in the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="5ad57-113">The database files are created in the default SQL Server Data folder, as configured in the SQL Server instance.</span></span> <span data-ttu-id="5ad57-114">For more information about the default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ad57-114">For more information about the default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a><span data-ttu-id="5ad57-115">Create a partitioned table</span><span class="sxs-lookup"><span data-stu-id="5ad57-115">Create a partitioned table</span></span>
<span data-ttu-id="5ad57-116">To create partitioned table(s) according to the data schema, mapped to the database filegroups created in the previous step, you must first create a partition function and scheme.</span><span class="sxs-lookup"><span data-stu-id="5ad57-116">To create partitioned table(s) according to the data schema, mapped to the database filegroups created in the previous step, you must first create a partition function and scheme.</span></span> <span data-ttu-id="5ad57-117">When data is bulk imported to the partitioned table(s), records are distributed among the filegroups according to a partition scheme, as described below.</span><span class="sxs-lookup"><span data-stu-id="5ad57-117">When data is bulk imported to the partitioned table(s), records are distributed among the filegroups according to a partition scheme, as described below.</span></span>

### <a name="1-create-a-partition-function"></a><span data-ttu-id="5ad57-118">1. Create a partition function</span><span class="sxs-lookup"><span data-stu-id="5ad57-118">1. Create a partition function</span></span>
<span data-ttu-id="5ad57-119">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) This function defines the range of values/boundaries to be included in each individual partition table, for example, to limit partitions by month(some\_datetime\_field) in the year 2013:</span><span class="sxs-lookup"><span data-stu-id="5ad57-119">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) This function defines the range of values/boundaries to be included in each individual partition table, for example, to limit partitions by month(some\_datetime\_field) in the year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )

### <a name="2-create-a-partition-scheme"></a><span data-ttu-id="5ad57-120">2. Create a partition scheme</span><span class="sxs-lookup"><span data-stu-id="5ad57-120">2. Create a partition scheme</span></span>
<span data-ttu-id="5ad57-121">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ad57-121">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx).</span></span> <span data-ttu-id="5ad57-122">This scheme maps each partition range in the partition function to a physical filegroup, for example:</span><span class="sxs-lookup"><span data-stu-id="5ad57-122">This scheme maps each partition range in the partition function to a physical filegroup, for example:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> TO (
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="5ad57-123">To verify the ranges in effect in each partition according to the function/scheme, run the following query:</span><span class="sxs-lookup"><span data-stu-id="5ad57-123">To verify the ranges in effect in each partition according to the function/scheme, run the following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>

### <a name="3-create-a-partition-table"></a><span data-ttu-id="5ad57-124">3. Create a partition table</span><span class="sxs-lookup"><span data-stu-id="5ad57-124">3. Create a partition table</span></span>
<span data-ttu-id="5ad57-125">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according to your data schema, and specify the partition scheme and constraint field used to partition the table, for example:</span><span class="sxs-lookup"><span data-stu-id="5ad57-125">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according to your data schema, and specify the partition scheme and constraint field used to partition the table, for example:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="5ad57-126">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ad57-126">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-the-data-for-each-individual-partition-table"></a><span data-ttu-id="5ad57-127">Bulk import the data for each individual partition table</span><span class="sxs-lookup"><span data-stu-id="5ad57-127">Bulk import the data for each individual partition table</span></span>

* <span data-ttu-id="5ad57-128">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="5ad57-128">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="5ad57-129">The example provided uses the BCP method.</span><span class="sxs-lookup"><span data-stu-id="5ad57-129">The example provided uses the BCP method.</span></span>
* <span data-ttu-id="5ad57-130">[Alter the database](https://msdn.microsoft.com/library/bb522682.aspx) to change transaction logging scheme to BULK_LOGGED to minimize overhead of logging, for example:</span><span class="sxs-lookup"><span data-stu-id="5ad57-130">[Alter the database](https://msdn.microsoft.com/library/bb522682.aspx) to change transaction logging scheme to BULK_LOGGED to minimize overhead of logging, for example:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="5ad57-131">To expedite data loading, launch the bulk import operations in parallel.</span><span class="sxs-lookup"><span data-stu-id="5ad57-131">To expedite data loading, launch the bulk import operations in parallel.</span></span> <span data-ttu-id="5ad57-132">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ad57-132">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="5ad57-133">The following PowerShell script is an example of parallel data loading using BCP.</span><span class="sxs-lookup"><span data-stu-id="5ad57-133">The following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # The example assumes the partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes the input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set the server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match the number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name to be loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-to-optimize-joins-and-query-performance"></a><span data-ttu-id="5ad57-134">Create indexes to optimize joins and query performance</span><span class="sxs-lookup"><span data-stu-id="5ad57-134">Create indexes to optimize joins and query performance</span></span>
* <span data-ttu-id="5ad57-135">If you extract data for modeling from multiple tables, create indexes on the join keys to improve the join performance.</span><span class="sxs-lookup"><span data-stu-id="5ad57-135">If you extract data for modeling from multiple tables, create indexes on the join keys to improve the join performance.</span></span>
* <span data-ttu-id="5ad57-136">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting the same filegroup for each partition, for example:</span><span class="sxs-lookup"><span data-stu-id="5ad57-136">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting the same filegroup for each partition, for example:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="5ad57-137">or,</span><span class="sxs-lookup"><span data-stu-id="5ad57-137">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="5ad57-138">You may choose to create the indexes before bulk importing the data.</span><span class="sxs-lookup"><span data-stu-id="5ad57-138">You may choose to create the indexes before bulk importing the data.</span></span> <span data-ttu-id="5ad57-139">Index creation before bulk importing slows down the data loading.</span><span class="sxs-lookup"><span data-stu-id="5ad57-139">Index creation before bulk importing slows down the data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="5ad57-140">Advanced Analytics Process and Technology in Action Example</span><span class="sxs-lookup"><span data-stu-id="5ad57-140">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="5ad57-141">For an end-to-end walkthrough example using the Team Data Science Process with a public dataset, see [Team Data Science Process in Action: using SQL Server](sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5ad57-141">For an end-to-end walkthrough example using the Team Data Science Process with a public dataset, see [Team Data Science Process in Action: using SQL Server](sql-walkthrough.md).</span></span>

