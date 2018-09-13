---
title: Using Apache Hive as an ETL Tool - Azure HDInsight
description: Use Apache Hive to extract, transform, and load (ETL) data in Azure HDInsight.
services: hdinsight
ms.service: hdinsight
author: ashishthaps
ms.author: ashishth
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 11/14/2017
ms.openlocfilehash: cd62083bc7bd0254084f0fc209540de929c25d06
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866340"
---
# <a name="use-apache-hive-as-an-extract-transform-and-load-etl-tool"></a><span data-ttu-id="4fd0a-103">Use Apache Hive as an Extract, Transform, and Load (ETL) tool</span><span class="sxs-lookup"><span data-stu-id="4fd0a-103">Use Apache Hive as an Extract, Transform, and Load (ETL) tool</span></span>

<span data-ttu-id="4fd0a-104">You typically need to clean and transform incoming data before loading it into a destination suitable for analytics.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-104">You typically need to clean and transform incoming data before loading it into a destination suitable for analytics.</span></span> <span data-ttu-id="4fd0a-105">Extract, Transform, and Load (ETL) operations are used to prepare data and load it into a data destination.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-105">Extract, Transform, and Load (ETL) operations are used to prepare data and load it into a data destination.</span></span>  <span data-ttu-id="4fd0a-106">Hive on HDInsight can read in unstructured data, process the data as needed, and then load the data into a relational data warehouse for decision support systems.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-106">Hive on HDInsight can read in unstructured data, process the data as needed, and then load the data into a relational data warehouse for decision support systems.</span></span> <span data-ttu-id="4fd0a-107">In this approach, data is extracted from the source and stored in scalable storage, such as Azure Storage blobs or Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-107">In this approach, data is extracted from the source and stored in scalable storage, such as Azure Storage blobs or Azure Data Lake Store.</span></span> <span data-ttu-id="4fd0a-108">The data is then transformed using a sequence of Hive queries and is finally staged within Hive in preparation for bulk loading into the destination data store.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-108">The data is then transformed using a sequence of Hive queries and is finally staged within Hive in preparation for bulk loading into the destination data store.</span></span>

## <a name="use-case-and-model-overview"></a><span data-ttu-id="4fd0a-109">Use case and model overview</span><span class="sxs-lookup"><span data-stu-id="4fd0a-109">Use case and model overview</span></span>

<span data-ttu-id="4fd0a-110">The following figure shows an overview of the use case and model for ETL automation.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-110">The following figure shows an overview of the use case and model for ETL automation.</span></span> <span data-ttu-id="4fd0a-111">Input data is transformed to generate the appropriate output.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-111">Input data is transformed to generate the appropriate output.</span></span>  <span data-ttu-id="4fd0a-112">During that transformation, the data can change shape, data type, and even language.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-112">During that transformation, the data can change shape, data type, and even language.</span></span>  <span data-ttu-id="4fd0a-113">ETL processes can convert Imperial to metric, change time zones, and improve precision to properly align with existing data in the destination.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-113">ETL processes can convert Imperial to metric, change time zones, and improve precision to properly align with existing data in the destination.</span></span>  <span data-ttu-id="4fd0a-114">ETL processes can also combine new data with existing data to keep reporting up-to-date, or to provide further insight into existing data.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-114">ETL processes can also combine new data with existing data to keep reporting up-to-date, or to provide further insight into existing data.</span></span>  <span data-ttu-id="4fd0a-115">Applications such as reporting tools and services can then consume this data in the desired format.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-115">Applications such as reporting tools and services can then consume this data in the desired format.</span></span>

![Apache Hive as ETL](./media/apache-hadoop-using-apache-hive-as-an-etl-tool/hdinsight-etl-architecture.png)

<span data-ttu-id="4fd0a-117">Hadoop is typically used in ETL processes that import either a massive number of text files (like CSVs) or a smaller but frequently changing number of text files, or both.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-117">Hadoop is typically used in ETL processes that import either a massive number of text files (like CSVs) or a smaller but frequently changing number of text files, or both.</span></span>  <span data-ttu-id="4fd0a-118">Hive is a great tool to use to prepare the data before loading it into the data destination.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-118">Hive is a great tool to use to prepare the data before loading it into the data destination.</span></span>  <span data-ttu-id="4fd0a-119">Hive allows you to create a schema over the CSV and use a SQL-like language to generate MapReduce programs that interact with the data.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-119">Hive allows you to create a schema over the CSV and use a SQL-like language to generate MapReduce programs that interact with the data.</span></span> 

<span data-ttu-id="4fd0a-120">The typical steps to using Hive to perform ETL are as follows:</span><span class="sxs-lookup"><span data-stu-id="4fd0a-120">The typical steps to using Hive to perform ETL are as follows:</span></span>

1. <span data-ttu-id="4fd0a-121">Load data into Azure Data Lake Store or Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-121">Load data into Azure Data Lake Store or Azure Blob Storage.</span></span>
2. <span data-ttu-id="4fd0a-122">Create a Metadata Store database (using Azure SQL Database) for use by Hive in storing your schemas.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-122">Create a Metadata Store database (using Azure SQL Database) for use by Hive in storing your schemas.</span></span>
3. <span data-ttu-id="4fd0a-123">Create an HDInsight cluster and connect the data store.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-123">Create an HDInsight cluster and connect the data store.</span></span>
4. <span data-ttu-id="4fd0a-124">Define the schema to apply at read-time over data in the data store:</span><span class="sxs-lookup"><span data-stu-id="4fd0a-124">Define the schema to apply at read-time over data in the data store:</span></span>

    ```
    DROP TABLE IF EXISTS hvac;

    --create the hvac table on comma-separated sensor data stored in Azure Storage blobs
    
    CREATE EXTERNAL TABLE hvac(`date` STRING, time STRING, targettemp BIGINT,
        actualtemp BIGINT, 
        system BIGINT, 
        systemage BIGINT, 
        buildingid BIGINT)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
    STORED AS TEXTFILE LOCATION 'wasb://{container}@{storageaccount}.blob.core.windows.net/HdiSamples/SensorSampleData/hvac/';
    ```

5. <span data-ttu-id="4fd0a-125">Transform the data and load it into the destination.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-125">Transform the data and load it into the destination.</span></span>  <span data-ttu-id="4fd0a-126">There are several ways to use Hive during the transformation and loading:</span><span class="sxs-lookup"><span data-stu-id="4fd0a-126">There are several ways to use Hive during the transformation and loading:</span></span>

    * <span data-ttu-id="4fd0a-127">Query and prepare data using Hive and save it as a CSV in Azure Data Lake Store or Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-127">Query and prepare data using Hive and save it as a CSV in Azure Data Lake Store or Azure blob storage.</span></span>  <span data-ttu-id="4fd0a-128">Then use a tool like SQL Server Integration Services (SSIS) to acquire those CSVs and load the data into a destination relational database such as SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-128">Then use a tool like SQL Server Integration Services (SSIS) to acquire those CSVs and load the data into a destination relational database such as SQL Server.</span></span>
    * <span data-ttu-id="4fd0a-129">Query the data directly from Excel or C# using the Hive ODBC driver.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-129">Query the data directly from Excel or C# using the Hive ODBC driver.</span></span>
    * <span data-ttu-id="4fd0a-130">Use [Apache Sqoop](apache-hadoop-use-sqoop-mac-linux.md) to read the prepared flat CSV files and load them into the destination relational database.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-130">Use [Apache Sqoop](apache-hadoop-use-sqoop-mac-linux.md) to read the prepared flat CSV files and load them into the destination relational database.</span></span>

## <a name="data-sources"></a><span data-ttu-id="4fd0a-131">Data sources</span><span class="sxs-lookup"><span data-stu-id="4fd0a-131">Data sources</span></span>

<span data-ttu-id="4fd0a-132">Data sources are typically external data that can be matched to existing data in your data store, for example:</span><span class="sxs-lookup"><span data-stu-id="4fd0a-132">Data sources are typically external data that can be matched to existing data in your data store, for example:</span></span>

* <span data-ttu-id="4fd0a-133">Social media data, log files, sensors, and applications that generate data files.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-133">Social media data, log files, sensors, and applications that generate data files.</span></span>
* <span data-ttu-id="4fd0a-134">Datasets obtained from data providers, such as weather statistics or vendor sales numbers.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-134">Datasets obtained from data providers, such as weather statistics or vendor sales numbers.</span></span>
* <span data-ttu-id="4fd0a-135">Streaming data captured, filtered, and processed through a suitable tool or framework.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-135">Streaming data captured, filtered, and processed through a suitable tool or framework.</span></span>

<!-- TODO: (see Collecting and loading data into HDInsight). -->

## <a name="output-targets"></a><span data-ttu-id="4fd0a-136">Output targets</span><span class="sxs-lookup"><span data-stu-id="4fd0a-136">Output targets</span></span>

<span data-ttu-id="4fd0a-137">You can use Hive to output data to a variety of targets including:</span><span class="sxs-lookup"><span data-stu-id="4fd0a-137">You can use Hive to output data to a variety of targets including:</span></span>

* <span data-ttu-id="4fd0a-138">A relational database, such as SQL Server or Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-138">A relational database, such as SQL Server or Azure SQL Database.</span></span>
* <span data-ttu-id="4fd0a-139">A data warehouse, such as Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-139">A data warehouse, such as Azure SQL Data Warehouse.</span></span>
* <span data-ttu-id="4fd0a-140">Excel.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-140">Excel.</span></span>
* <span data-ttu-id="4fd0a-141">Azure table and blob storage.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-141">Azure table and blob storage.</span></span>
* <span data-ttu-id="4fd0a-142">Applications or services that require data to be processed into specific formats, or as files that contain specific types of information structure.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-142">Applications or services that require data to be processed into specific formats, or as files that contain specific types of information structure.</span></span>
* <span data-ttu-id="4fd0a-143">A JSON Document Store like <a href="https://azure.microsoft.com/services/cosmos-db/">CosmosDB</a>.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-143">A JSON Document Store like <a href="https://azure.microsoft.com/services/cosmos-db/">CosmosDB</a>.</span></span>

## <a name="considerations"></a><span data-ttu-id="4fd0a-144">Considerations</span><span class="sxs-lookup"><span data-stu-id="4fd0a-144">Considerations</span></span>

<span data-ttu-id="4fd0a-145">The ETL model is typically used when you want to:</span><span class="sxs-lookup"><span data-stu-id="4fd0a-145">The ETL model is typically used when you want to:</span></span>

* <span data-ttu-id="4fd0a-146">Load stream data or large volumes of semi-structured or unstructured data from external sources into an existing database or information system.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-146">Load stream data or large volumes of semi-structured or unstructured data from external sources into an existing database or information system.</span></span>
* <span data-ttu-id="4fd0a-147">Clean, transform, and validate the data before loading it, perhaps by using more than one transformation pass through the cluster.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-147">Clean, transform, and validate the data before loading it, perhaps by using more than one transformation pass through the cluster.</span></span>
* <span data-ttu-id="4fd0a-148">Generate reports and visualizations that are regularly updated.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-148">Generate reports and visualizations that are regularly updated.</span></span>  <span data-ttu-id="4fd0a-149">For example, if the report takes too long to generate during the day,  you can schedule the report to run at night.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-149">For example, if the report takes too long to generate during the day,  you can schedule the report to run at night.</span></span>  <span data-ttu-id="4fd0a-150">You can use Azure Scheduler and PowerShell to automatically run a Hive query.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-150">You can use Azure Scheduler and PowerShell to automatically run a Hive query.</span></span>

<span data-ttu-id="4fd0a-151">If the target for the data is not a database, you can generate a file in the appropriate format within the query, for example a CSV.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-151">If the target for the data is not a database, you can generate a file in the appropriate format within the query, for example a CSV.</span></span> <span data-ttu-id="4fd0a-152">This file can then be imported into Excel or Power BI.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-152">This file can then be imported into Excel or Power BI.</span></span>

<span data-ttu-id="4fd0a-153">If you need to execute several operations on the data as part of the ETL process, consider how you manage them.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-153">If you need to execute several operations on the data as part of the ETL process, consider how you manage them.</span></span> <span data-ttu-id="4fd0a-154">If the operations are controlled by an external program, rather than as a workflow within the solution, you need to decide whether some operations can be executed in parallel, and to detect when each job  completes.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-154">If the operations are controlled by an external program, rather than as a workflow within the solution, you need to decide whether some operations can be executed in parallel, and to detect when each job  completes.</span></span> <span data-ttu-id="4fd0a-155">Using a workflow mechanism such as Oozie within Hadoop may be easier than trying to orchestrate a sequence of operations using external scripts or custom programs.</span><span class="sxs-lookup"><span data-stu-id="4fd0a-155">Using a workflow mechanism such as Oozie within Hadoop may be easier than trying to orchestrate a sequence of operations using external scripts or custom programs.</span></span> <span data-ttu-id="4fd0a-156">For more information about Oozie, see [Workflow and job orchestration](https://msdn.microsoft.com/library/dn749829.aspx).</span><span class="sxs-lookup"><span data-stu-id="4fd0a-156">For more information about Oozie, see [Workflow and job orchestration](https://msdn.microsoft.com/library/dn749829.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fd0a-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="4fd0a-157">Next steps</span></span>

* [<span data-ttu-id="4fd0a-158">ETL at scale</span><span class="sxs-lookup"><span data-stu-id="4fd0a-158">ETL at scale</span></span>](apache-hadoop-etl-at-scale.md)
* [<span data-ttu-id="4fd0a-159">Operationalize a data pipeline</span><span class="sxs-lookup"><span data-stu-id="4fd0a-159">Operationalize a data pipeline</span></span>](../hdinsight-operationalize-data-pipeline.md)

<!-- * [ETL Deep Dive](../hdinsight-etl-deep-dive.md) -->
