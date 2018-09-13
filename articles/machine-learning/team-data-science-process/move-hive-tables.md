---
title: Create Hive tables and load data from Azure Blob Storage | Microsoft Docs
description: Create Hive tables and load data in blob to hive tables
services: machine-learning,storage
documentationcenter: ''
author: deguhath
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: deguhath
ms.openlocfilehash: ccfa3f8681b220d01f8347abd58140e2621f4282
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867686"
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a><span data-ttu-id="a2b4f-103">Create Hive tables and load data from Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="a2b4f-103">Create Hive tables and load data from Azure Blob Storage</span></span>
<span data-ttu-id="a2b4f-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-104">This topic presents generic Hive queries that create Hive tables and load data from Azure blob storage.</span></span> <span data-ttu-id="a2b4f-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-105">Some guidance is also provided on partitioning Hive tables and on using the Optimized Row Columnar (ORC) formatting to improve query performance.</span></span>

<span data-ttu-id="a2b4f-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span><span class="sxs-lookup"><span data-stu-id="a2b4f-106">This **menu** links to topics that describe how to ingest data into target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="a2b4f-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a2b4f-107">Prerequisites</span></span>
<span data-ttu-id="a2b4f-108">This article assumes that you have:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-108">This article assumes that you have:</span></span>

* <span data-ttu-id="a2b4f-109">Created an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-109">Created an Azure storage account.</span></span> <span data-ttu-id="a2b4f-110">If you need instructions, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a2b4f-110">If you need instructions, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="a2b4f-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-111">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="a2b4f-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a2b4f-112">If you need instructions, see [Customize Azure HDInsight Hadoop clusters for advanced analytics](customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="a2b4f-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-113">Enabled remote access to the cluster, logged in, and opened the Hadoop Command-Line console.</span></span> <span data-ttu-id="a2b4f-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a2b4f-114">If you need instructions, see [Access the Head Node of Hadoop Cluster](customize-hadoop-cluster.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="a2b4f-115">Upload data to Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="a2b4f-115">Upload data to Azure blob storage</span></span>
<span data-ttu-id="a2b4f-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](../data-science-virtual-machine/setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-116">If you created an Azure virtual machine by following the instructions provided in [Set up an Azure virtual machine for advanced analytics](../data-science-virtual-machine/setup-virtual-machine.md), this script file should have been downloaded to the *C:\\Users\\\<user name\>\\Documents\\Data Science Scripts* directory on the virtual machine.</span></span> <span data-ttu-id="a2b4f-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-117">These Hive queries only require that you plug in your own data schema and Azure blob storage configuration in the appropriate fields to be ready for submission.</span></span>

<span data-ttu-id="a2b4f-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-118">We assume that the data for Hive tables is in an **uncompressed** tabular format, and that the data has been uploaded to the default (or to an additional) container of the storage account used by the Hadoop cluster.</span></span>

<span data-ttu-id="a2b4f-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-119">If you want to practice on the **NYC Taxi Trip Data**, you need to:</span></span>

* <span data-ttu-id="a2b4f-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span><span class="sxs-lookup"><span data-stu-id="a2b4f-120">**download** the 24 [NYC Taxi Trip Data](http://www.andresmh.com/nyctaxitrips) files (12 Trip files and 12 Fare files),</span></span>
* <span data-ttu-id="a2b4f-121">**unzip** all files into .csv files, and then</span><span class="sxs-lookup"><span data-stu-id="a2b4f-121">**unzip** all files into .csv files, and then</span></span>
* <span data-ttu-id="a2b4f-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](customize-hadoop-cluster.md) topic.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-122">**upload** them to the default (or appropriate container) of the Azure storage account that was created by the procedure outlined in the [Customize Azure HDInsight Hadoop clusters for Advanced Analytics Process and Technology](customize-hadoop-cluster.md) topic.</span></span> <span data-ttu-id="a2b4f-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](hive-walkthrough.md#upload).</span><span class="sxs-lookup"><span data-stu-id="a2b4f-123">The process to upload the .csv files to the default container on the storage account can be found on this [page](hive-walkthrough.md#upload).</span></span>

## <a name="submit"></a><span data-ttu-id="a2b4f-124">How to submit Hive queries</span><span class="sxs-lookup"><span data-stu-id="a2b4f-124">How to submit Hive queries</span></span>
<span data-ttu-id="a2b4f-125">Hive queries can be submitted by using:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-125">Hive queries can be submitted by using:</span></span>

1. [<span data-ttu-id="a2b4f-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="a2b4f-126">Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>](#headnode)
2. [<span data-ttu-id="a2b4f-127">Submit Hive queries with the Hive Editor</span><span class="sxs-lookup"><span data-stu-id="a2b4f-127">Submit Hive queries with the Hive Editor</span></span>](#hive-editor)
3. [<span data-ttu-id="a2b4f-128">Submit Hive queries with Azure PowerShell Commands</span><span class="sxs-lookup"><span data-stu-id="a2b4f-128">Submit Hive queries with Azure PowerShell Commands</span></span>](#ps)

<span data-ttu-id="a2b4f-129">Hive queries are SQL-like.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-129">Hive queries are SQL-like.</span></span> <span data-ttu-id="a2b4f-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-130">If you are familiar with SQL, you may find the [Hive for SQL Users Cheat Sheet](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) useful.</span></span>

<span data-ttu-id="a2b4f-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-131">When submitting a Hive query, you can also control the destination of the output from Hive queries, whether it be on the screen or to a local file on the head node or to an Azure blob.</span></span>

### <a name="headnode"></a> <span data-ttu-id="a2b4f-132">1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="a2b4f-132">1. Submit Hive queries through Hadoop Command Line in headnode of Hadoop cluster</span></span>
<span data-ttu-id="a2b4f-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-133">If the Hive query is complex, submitting it directly in the head node of the Hadoop cluster typically leads to faster turn around than submitting it with a Hive Editor or Azure PowerShell scripts.</span></span>

<span data-ttu-id="a2b4f-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-134">Log in to the head node of the Hadoop cluster, open the Hadoop Command Line on the desktop of the head node, and enter command `cd %hive_home%\bin`.</span></span>

<span data-ttu-id="a2b4f-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-135">You have three ways to submit Hive queries in the Hadoop Command Line:</span></span>

* <span data-ttu-id="a2b4f-136">directly</span><span class="sxs-lookup"><span data-stu-id="a2b4f-136">directly</span></span>
* <span data-ttu-id="a2b4f-137">using .hql files</span><span class="sxs-lookup"><span data-stu-id="a2b4f-137">using .hql files</span></span>
* <span data-ttu-id="a2b4f-138">with the Hive command console</span><span class="sxs-lookup"><span data-stu-id="a2b4f-138">with the Hive command console</span></span>

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a><span data-ttu-id="a2b4f-139">Submit Hive queries directly in Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-139">Submit Hive queries directly in Hadoop Command Line.</span></span>
<span data-ttu-id="a2b4f-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-140">You can run command like `hive -e "<your hive query>;` to submit simple Hive queries directly in Hadoop Command Line.</span></span> <span data-ttu-id="a2b4f-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-141">Here is an example, where the red box outlines the command that submits the Hive query, and the green box outlines the output from the Hive query.</span></span>

![Create workspace](./media/move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a><span data-ttu-id="a2b4f-143">Submit Hive queries in .hql files</span><span class="sxs-lookup"><span data-stu-id="a2b4f-143">Submit Hive queries in .hql files</span></span>
<span data-ttu-id="a2b4f-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-144">When the Hive query is more complicated and has multiple lines, editing queries in command line or Hive command console is not practical.</span></span> <span data-ttu-id="a2b4f-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-145">An alternative is to use a text editor in the head node of the Hadoop cluster to save the Hive queries in a .hql file in a local directory of the head node.</span></span> <span data-ttu-id="a2b4f-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-146">Then the Hive query in the .hql file can be submitted by using the `-f` argument as follows:</span></span>

    hive -f "<path to the .hql file>"

![Create workspace](./media/move-hive-tables/run-hive-queries-3.png)

<span data-ttu-id="a2b4f-148">**Suppress progress status screen print of Hive queries**</span><span class="sxs-lookup"><span data-stu-id="a2b4f-148">**Suppress progress status screen print of Hive queries**</span></span>

<span data-ttu-id="a2b4f-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-149">By default, after Hive query is submitted in Hadoop Command Line, the progress of the Map/Reduce job is printed out on screen.</span></span> <span data-ttu-id="a2b4f-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-150">To suppress the screen print of the Map/Reduce job progress, you can use an argument `-S` ("S" in upper case) in the command line as follows:</span></span>

    hive -S -f "<path to the .hql file>"
    hive -S -e "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a><span data-ttu-id="a2b4f-151">Submit Hive queries in Hive command console.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-151">Submit Hive queries in Hive command console.</span></span>
<span data-ttu-id="a2b4f-152">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-152">You can also first enter the Hive command console by running command `hive` in Hadoop Command Line, and then submit Hive queries in Hive command console.</span></span> <span data-ttu-id="a2b4f-153">Here is an example.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-153">Here is an example.</span></span> <span data-ttu-id="a2b4f-154">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-154">In this example, the two red boxes highlight the commands used to enter the Hive command console, and the Hive query submitted in Hive command console, respectively.</span></span> <span data-ttu-id="a2b4f-155">The green box highlights the output from the Hive query.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-155">The green box highlights the output from the Hive query.</span></span>

![Create workspace](./media/move-hive-tables/run-hive-queries-2.png)

<span data-ttu-id="a2b4f-157">The previous examples directly output the Hive query results on screen.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-157">The previous examples directly output the Hive query results on screen.</span></span> <span data-ttu-id="a2b4f-158">You can also write the output to a local file on the head node, or to an Azure blob.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-158">You can also write the output to a local file on the head node, or to an Azure blob.</span></span> <span data-ttu-id="a2b4f-159">Then, you can use other tools to further analyze the output of Hive queries.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-159">Then, you can use other tools to further analyze the output of Hive queries.</span></span>

<span data-ttu-id="a2b4f-160">**Output Hive query results to a local file.**</span><span class="sxs-lookup"><span data-stu-id="a2b4f-160">**Output Hive query results to a local file.**</span></span>
<span data-ttu-id="a2b4f-161">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-161">To output Hive query results to a local directory on the head node, you have to submit the Hive query in the Hadoop Command Line as follows:</span></span>

    hive -e "<hive query>" > <local path in the head node>

<span data-ttu-id="a2b4f-162">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-162">In the following example, the output of Hive query is written into a file `hivequeryoutput.txt` in directory `C:\apps\temp`.</span></span>

![Create workspace](./media/move-hive-tables/output-hive-results-1.png)

<span data-ttu-id="a2b4f-164">**Output Hive query results to an Azure blob**</span><span class="sxs-lookup"><span data-stu-id="a2b4f-164">**Output Hive query results to an Azure blob**</span></span>

<span data-ttu-id="a2b4f-165">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-165">You can also output the Hive query results to an Azure blob, within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="a2b4f-166">The Hive query for this is as follows:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-166">The Hive query for this is as follows:</span></span>

    insert overwrite directory wasb:///<directory within the default container> <select clause from ...>

<span data-ttu-id="a2b4f-167">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-167">In the following example, the output of Hive query is written to a blob directory `queryoutputdir` within the default container of the Hadoop cluster.</span></span> <span data-ttu-id="a2b4f-168">Here, you only need to provide the directory name, without the blob name.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-168">Here, you only need to provide the directory name, without the blob name.</span></span> <span data-ttu-id="a2b4f-169">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-169">An error is thrown if you provide both directory and blob names, such as `wasb:///queryoutputdir/queryoutput.txt`.</span></span>

![Create workspace](./media/move-hive-tables/output-hive-results-2.png)

<span data-ttu-id="a2b4f-171">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-171">If you open the default container of the Hadoop cluster using Azure Storage Explorer, you can see the output of the Hive query as shown in the following figure.</span></span> <span data-ttu-id="a2b4f-172">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-172">You can apply the filter (highlighted by red box) to only retrieve the blob with specified letters in names.</span></span>

![Create workspace](./media/move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> <span data-ttu-id="a2b4f-174">2. Submit Hive queries with the Hive Editor</span><span class="sxs-lookup"><span data-stu-id="a2b4f-174">2. Submit Hive queries with the Hive Editor</span></span>
<span data-ttu-id="a2b4f-175">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://<Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-175">You can also use the Query Console (Hive Editor) by entering a URL of the form *https://<Hadoop cluster name>.azurehdinsight.net/Home/HiveEditor* into a web browser.</span></span> <span data-ttu-id="a2b4f-176">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-176">You must be logged in the see this console and so you need your Hadoop cluster credentials here.</span></span>

### <a name="ps"></a> <span data-ttu-id="a2b4f-177">3. Submit Hive queries with Azure PowerShell Commands</span><span class="sxs-lookup"><span data-stu-id="a2b4f-177">3. Submit Hive queries with Azure PowerShell Commands</span></span>
<span data-ttu-id="a2b4f-178">You can also use PowerShell to submit Hive queries.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-178">You can also use PowerShell to submit Hive queries.</span></span> <span data-ttu-id="a2b4f-179">For instructions, see [Submit Hive jobs using PowerShell](../../hdinsight/hadoop/apache-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a2b4f-179">For instructions, see [Submit Hive jobs using PowerShell](../../hdinsight/hadoop/apache-hadoop-use-hive-powershell.md).</span></span>

## <a name="create-tables"></a><span data-ttu-id="a2b4f-180">Create Hive database and tables</span><span class="sxs-lookup"><span data-stu-id="a2b4f-180">Create Hive database and tables</span></span>
<span data-ttu-id="a2b4f-181">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-181">The Hive queries are shared in the [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) and can be downloaded from there.</span></span>

<span data-ttu-id="a2b4f-182">Here is the Hive query that creates a Hive table.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-182">Here is the Hive query that creates a Hive table.</span></span>

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

<span data-ttu-id="a2b4f-183">Here are the descriptions of the fields that you need to plug in and other configurations:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-183">Here are the descriptions of the fields that you need to plug in and other configurations:</span></span>

* <span data-ttu-id="a2b4f-184">**<database name>**: the name of the database that you want to create.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-184">**<database name>**: the name of the database that you want to create.</span></span> <span data-ttu-id="a2b4f-185">If you just want to use the default database, the query *create database...* can be omitted.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-185">If you just want to use the default database, the query *create database...* can be omitted.</span></span>
* <span data-ttu-id="a2b4f-186">**<table name>**: the name of the table that you want to create within the specified database.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-186">**<table name>**: the name of the table that you want to create within the specified database.</span></span> <span data-ttu-id="a2b4f-187">If you want to use the default database, the table can be directly referred by *<table name>* without <database name>.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-187">If you want to use the default database, the table can be directly referred by *<table name>* without <database name>.</span></span>
* <span data-ttu-id="a2b4f-188">**<field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-188">**<field separator>**: the separator that delimits fields in the data file to be uploaded to the Hive table.</span></span>
* <span data-ttu-id="a2b4f-189">**<line separator>**: the separator that delimits lines in the data file.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-189">**<line separator>**: the separator that delimits lines in the data file.</span></span>
* <span data-ttu-id="a2b4f-190">**<storage location>**: the Azure storage location to save the data of Hive tables.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-190">**<storage location>**: the Azure storage location to save the data of Hive tables.</span></span> <span data-ttu-id="a2b4f-191">If you do not specify *LOCATION <storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-191">If you do not specify *LOCATION <storage location>*, the database and the tables are stored in *hive/warehouse/* directory in the default container of the Hive cluster by default.</span></span> <span data-ttu-id="a2b4f-192">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-192">If you want to specify the storage location, the storage location has to be within the default container for the database and tables.</span></span> <span data-ttu-id="a2b4f-193">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///<directory 1>/'* or *'wasb:///<directory 1>/<directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-193">This location has to be referred as location relative to the default container of the cluster in the format of *'wasb:///<directory 1>/'* or *'wasb:///<directory 1>/<directory 2>/'*, etc. After the query is executed, the relative directories are created within the default container.</span></span>
* <span data-ttu-id="a2b4f-194">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-194">**TBLPROPERTIES("skip.header.line.count"="1")**: If the data file has a header line, you have to add this property **at the end** of the *create table* query.</span></span> <span data-ttu-id="a2b4f-195">Otherwise, the header line is loaded as a record to the table.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-195">Otherwise, the header line is loaded as a record to the table.</span></span> <span data-ttu-id="a2b4f-196">If the data file does not have a header line, this configuration can be omitted in the query.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-196">If the data file does not have a header line, this configuration can be omitted in the query.</span></span>

## <a name="load-data"></a><span data-ttu-id="a2b4f-197">Load data to Hive tables</span><span class="sxs-lookup"><span data-stu-id="a2b4f-197">Load data to Hive tables</span></span>
<span data-ttu-id="a2b4f-198">Here is the Hive query that loads data into a Hive table.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-198">Here is the Hive query that loads data into a Hive table.</span></span>

    LOAD DATA INPATH '<path to blob data>' INTO TABLE <database name>.<table name>;

* <span data-ttu-id="a2b4f-199">**<path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *<path to blob data>* should be in the format *'wasb:///<directory in this container>/<blob file name>'*.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-199">**<path to blob data>**: If the blob file to be uploaded to the Hive table is in the default container of the HDInsight Hadoop cluster, the *<path to blob data>* should be in the format *'wasb:///<directory in this container>/<blob file name>'*.</span></span> <span data-ttu-id="a2b4f-200">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-200">The blob file can also be in an additional container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="a2b4f-201">In this case, *<path to blob data>* should be in the format *'wasb://<container name><storage account name>.blob.core.windows.net/<blob file name>'*.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-201">In this case, *<path to blob data>* should be in the format *'wasb://<container name><storage account name>.blob.core.windows.net/<blob file name>'*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a2b4f-202">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-202">The blob data to be uploaded to Hive table has to be in the default or additional container of the storage account for the Hadoop cluster.</span></span> <span data-ttu-id="a2b4f-203">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-203">Otherwise, the *LOAD DATA* query fails complaining that it cannot access the data.</span></span>
  >
  >

## <a name="partition-orc"></a><span data-ttu-id="a2b4f-204">Advanced topics: partitioned table and store Hive data in ORC format</span><span class="sxs-lookup"><span data-stu-id="a2b4f-204">Advanced topics: partitioned table and store Hive data in ORC format</span></span>
<span data-ttu-id="a2b4f-205">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-205">If the data is large, partitioning the table is beneficial for queries that only need to scan a few partitions of the table.</span></span> <span data-ttu-id="a2b4f-206">For instance, it is reasonable to partition the log data of a web site by dates.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-206">For instance, it is reasonable to partition the log data of a web site by dates.</span></span>

<span data-ttu-id="a2b4f-207">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-207">In addition to partitioning Hive tables, it is also beneficial to store the Hive data in the Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="a2b4f-208">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-208">For more information on ORC formatting, see <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">Using ORC files improves performance when Hive is reading, writing, and processing data</a>.</span></span>

### <a name="partitioned-table"></a><span data-ttu-id="a2b4f-209">Partitioned table</span><span class="sxs-lookup"><span data-stu-id="a2b4f-209">Partitioned table</span></span>
<span data-ttu-id="a2b4f-210">Here is the Hive query that creates a partitioned table and loads data into it.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-210">Here is the Hive query that creates a partitioned table and loads data into it.</span></span>

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

<span data-ttu-id="a2b4f-211">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-211">When querying partitioned tables, it is recommended to add the partition condition in the **beginning** of the `where` clause as this improves the efficacy of searching significantly.</span></span>

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a><span data-ttu-id="a2b4f-212">Store Hive data in ORC format</span><span class="sxs-lookup"><span data-stu-id="a2b4f-212">Store Hive data in ORC format</span></span>
<span data-ttu-id="a2b4f-213">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-213">You cannot directly load data from blob storage into Hive tables that is stored in the ORC format.</span></span> <span data-ttu-id="a2b4f-214">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-214">Here are the steps that the you need to take to load data from Azure blobs to Hive tables stored in ORC format.</span></span>

<span data-ttu-id="a2b4f-215">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-215">Create an external table **STORED AS TEXTFILE** and load data from blob storage to the table.</span></span>

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path to the source file>' INTO TABLE <database name>.<table name>;

<span data-ttu-id="a2b4f-216">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-216">Create an internal table with the same schema as the external table in step 1, with the same field delimiter, and store the Hive data in the ORC format.</span></span>

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

<span data-ttu-id="a2b4f-217">Select data from the external table in step 1 and insert into the ORC table</span><span class="sxs-lookup"><span data-stu-id="a2b4f-217">Select data from the external table in step 1 and insert into the ORC table</span></span>

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> <span data-ttu-id="a2b4f-218">If the TEXTFILE table *<database name>.<external textfile table name>*</span><span class="sxs-lookup"><span data-stu-id="a2b4f-218">If the TEXTFILE table *<database name>.<external textfile table name>*</span></span> <span data-ttu-id="a2b4f-219">has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-219">has partitions, in STEP 3, the `SELECT * FROM <database name>.<external textfile table name>` command selects the partition variable as a field in the returned data set.</span></span> <span data-ttu-id="a2b4f-220">Inserting it into the *<database name>.<ORC table name>*</span><span class="sxs-lookup"><span data-stu-id="a2b4f-220">Inserting it into the *<database name>.<ORC table name>*</span></span> <span data-ttu-id="a2b4f-221">fails since *<database name>.<ORC table name>*</span><span class="sxs-lookup"><span data-stu-id="a2b4f-221">fails since *<database name>.<ORC table name>*</span></span> <span data-ttu-id="a2b4f-222">does not have the partition variable as a field in the table schema.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-222">does not have the partition variable as a field in the table schema.</span></span> <span data-ttu-id="a2b4f-223">In this case, you need to specifically select the fields to be inserted to *<database name>.<ORC table name>*</span><span class="sxs-lookup"><span data-stu-id="a2b4f-223">In this case, you need to specifically select the fields to be inserted to *<database name>.<ORC table name>*</span></span> <span data-ttu-id="a2b4f-224">as follows:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-224">as follows:</span></span>
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

<span data-ttu-id="a2b4f-225">It is safe to drop the *<external textfile table name>* when using the following query after all data has been inserted into *<database name>.<ORC table name>*:</span><span class="sxs-lookup"><span data-stu-id="a2b4f-225">It is safe to drop the *<external textfile table name>* when using the following query after all data has been inserted into *<database name>.<ORC table name>*:</span></span>

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

<span data-ttu-id="a2b4f-226">After following this procedure, you should have a table with data in the ORC format ready to use.</span><span class="sxs-lookup"><span data-stu-id="a2b4f-226">After following this procedure, you should have a table with data in the ORC format ready to use.</span></span>  
