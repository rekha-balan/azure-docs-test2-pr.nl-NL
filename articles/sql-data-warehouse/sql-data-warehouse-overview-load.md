---
title: Load data into Azure SQL Data Warehouse | Microsoft Docs
description: Learn the common scenarios for data loading into SQL Data Warehouse. These include using PolyBase, Azure blob storage, flat files, and disk shipping. You can also use third-party tools.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 5dd34ddb7b410eccf170a77def3defddf0b245d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563355"
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="ec5c3-105">Load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ec5c3-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="ec5c3-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="ec5c3-107">The hardest part of loading data is usually preparing the data for the load.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="ec5c3-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="ec5c3-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="ec5c3-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="ec5c3-111">Load from Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="ec5c3-111">Load from Azure blob storage</span></span>
<span data-ttu-id="ec5c3-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="ec5c3-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="ec5c3-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="ec5c3-115">1. Use PolyBase and T-SQL</span><span class="sxs-lookup"><span data-stu-id="ec5c3-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="ec5c3-116">Summary of loading process:</span><span class="sxs-lookup"><span data-stu-id="ec5c3-116">Summary of loading process:</span></span>

1. <span data-ttu-id="ec5c3-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="ec5c3-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span><span class="sxs-lookup"><span data-stu-id="ec5c3-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="ec5c3-119">Run a T-SQL command to load the data in parallel into a new database table.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="ec5c3-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="ec5c3-121">2. Use Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ec5c3-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="ec5c3-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="ec5c3-123">This is fast to configure since you don't need to define the T-SQL objects.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="ec5c3-124">If you need to query the external data without importing it, use T-SQL.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="ec5c3-125">Summary of loading process:</span><span class="sxs-lookup"><span data-stu-id="ec5c3-125">Summary of loading process:</span></span>

1. <span data-ttu-id="ec5c3-126">Move your data to Azure blob storage and store it in text files.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="ec5c3-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span><span class="sxs-lookup"><span data-stu-id="ec5c3-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="ec5c3-128">Create an Azure Data Factory pipeline to ingest the data.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="ec5c3-129">Use the PolyBase option.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="ec5c3-130">Schedule and run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="ec5c3-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="ec5c3-132">Load from SQL Server</span><span class="sxs-lookup"><span data-stu-id="ec5c3-132">Load from SQL Server</span></span>
<span data-ttu-id="ec5c3-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="ec5c3-134">Read on to see a summary of the different loading processes and links to tutorials.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="ec5c3-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="ec5c3-136">Use Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="ec5c3-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="ec5c3-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="ec5c3-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="ec5c3-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="ec5c3-140">Summary of loading process:</span><span class="sxs-lookup"><span data-stu-id="ec5c3-140">Summary of loading process:</span></span>

1. <span data-ttu-id="ec5c3-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="ec5c3-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="ec5c3-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="ec5c3-144">Schedule and run the package.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-144">Schedule and run the package.</span></span>

<span data-ttu-id="ec5c3-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="ec5c3-146">Use AZCopy (recommended for < 10 TB data)</span><span class="sxs-lookup"><span data-stu-id="ec5c3-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="ec5c3-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ec5c3-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="ec5c3-148">Summary of loading process:</span><span class="sxs-lookup"><span data-stu-id="ec5c3-148">Summary of loading process:</span></span>

1. <span data-ttu-id="ec5c3-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="ec5c3-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="ec5c3-151">Use PolyBase to load into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="ec5c3-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="ec5c3-153">Use bcp</span><span class="sxs-lookup"><span data-stu-id="ec5c3-153">Use bcp</span></span>
<span data-ttu-id="ec5c3-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="ec5c3-155">Summary of loading process:</span><span class="sxs-lookup"><span data-stu-id="ec5c3-155">Summary of loading process:</span></span>

1. <span data-ttu-id="ec5c3-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="ec5c3-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="ec5c3-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="ec5c3-159">Use Import/Export (recommended for > 10 TB data)</span><span class="sxs-lookup"><span data-stu-id="ec5c3-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="ec5c3-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="ec5c3-161">Summary of loading process</span><span class="sxs-lookup"><span data-stu-id="ec5c3-161">Summary of loading process</span></span>

1. <span data-ttu-id="ec5c3-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="ec5c3-163">Ship the disks to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="ec5c3-164">Microsoft loads the data into SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ec5c3-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="ec5c3-165">Load from HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec5c3-165">Load from HDInsight</span></span>
<span data-ttu-id="ec5c3-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="ec5c3-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="ec5c3-168">1. Use PolyBase and T-SQL</span><span class="sxs-lookup"><span data-stu-id="ec5c3-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="ec5c3-169">Summary of loading process:</span><span class="sxs-lookup"><span data-stu-id="ec5c3-169">Summary of loading process:</span></span>

1. <span data-ttu-id="ec5c3-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="ec5c3-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="ec5c3-172">Run a T-SQL command to load the data in parallel into a new database table.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="ec5c3-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="ec5c3-174">Recommendations</span><span class="sxs-lookup"><span data-stu-id="ec5c3-174">Recommendations</span></span>
<span data-ttu-id="ec5c3-175">Many of our partners have loading solutions.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="ec5c3-176">To find out more, see a list of our [solution partners][solution partners].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="ec5c3-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="ec5c3-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="ec5c3-179">Create statistics on newly loaded data.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="ec5c3-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="ec5c3-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span><span class="sxs-lookup"><span data-stu-id="ec5c3-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="ec5c3-182">For details, see [Statistics][Statistics].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec5c3-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="ec5c3-183">Next steps</span></span>
<span data-ttu-id="ec5c3-184">For more development tips, see the [development overview][development overview].</span><span class="sxs-lookup"><span data-stu-id="ec5c3-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
