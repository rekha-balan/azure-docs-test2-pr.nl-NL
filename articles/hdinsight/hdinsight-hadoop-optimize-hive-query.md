---
title: Optimize your Hive queries for faster execution in HDInsight | Microsoft Docs
description: Learn how to optimize your Hive queries for Hadoop in HDInsight.
services: hdinsight
documentationcenter: ''
author: rashimg
manager: mwinkle
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/28/2015
ms.author: rashimg
ms.openlocfilehash: 4e975fc1e43b9a37ff3642b6e517f8ff751ac717
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564518"
---
# <a name="optimize-hive-queries-for-hadoop-in-hdinsight"></a><span data-ttu-id="1d419-103">Optimize Hive queries for Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d419-103">Optimize Hive queries for Hadoop in HDInsight</span></span>
<span data-ttu-id="1d419-104">By default, Hadoop clusters are not optimized for performance.</span><span class="sxs-lookup"><span data-stu-id="1d419-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="1d419-105">This article covers a few of the most common Hive performance optimization methods that you can apply to our queries.</span><span class="sxs-lookup"><span data-stu-id="1d419-105">This article covers a few of the most common Hive performance optimization methods that you can apply to our queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="1d419-106">Scale out worker nodes</span><span class="sxs-lookup"><span data-stu-id="1d419-106">Scale out worker nodes</span></span>
<span data-ttu-id="1d419-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span><span class="sxs-lookup"><span data-stu-id="1d419-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span></span> <span data-ttu-id="1d419-108">There are two ways you can increase scale out in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1d419-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="1d419-109">At the provision time, you can specify the number of worker nodes using the Azure Portal, Azure PowerShell or Cross-platform command line interface.</span><span class="sxs-lookup"><span data-stu-id="1d419-109">At the provision time, you can specify the number of worker nodes using the Azure Portal, Azure PowerShell or Cross-platform command line interface.</span></span>  <span data-ttu-id="1d419-110">For more information, see [Provision HDInsight clusters](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1d419-110">For more information, see [Provision HDInsight clusters](hdinsight-provision-clusters.md).</span></span> <span data-ttu-id="1d419-111">The following screen show the worker node configuration on the Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="1d419-111">The following screen show the worker node configuration on the Azure Portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="1d419-113">At the run time, you can also scale out a cluster without recreating one.</span><span class="sxs-lookup"><span data-stu-id="1d419-113">At the run time, you can also scale out a cluster without recreating one.</span></span> <span data-ttu-id="1d419-114">This is shown below.</span><span class="sxs-lookup"><span data-stu-id="1d419-114">This is shown below.</span></span>
  <span data-ttu-id="1d419-115">![scaleout_1][image-hdi-optimize-hive-scaleout_2]</span><span class="sxs-lookup"><span data-stu-id="1d419-115">![scaleout_1][image-hdi-optimize-hive-scaleout_2]</span></span>

<span data-ttu-id="1d419-116">For more details on the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1d419-116">For more details on the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="1d419-117">Enable Tez</span><span class="sxs-lookup"><span data-stu-id="1d419-117">Enable Tez</span></span>
<span data-ttu-id="1d419-118">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span><span class="sxs-lookup"><span data-stu-id="1d419-118">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="1d419-120">Tez is faster because:</span><span class="sxs-lookup"><span data-stu-id="1d419-120">Tez is faster because:</span></span>

* <span data-ttu-id="1d419-121">Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine, the DAG that is expressed requires each set of mappers to be followed by one set of reducers.</span><span class="sxs-lookup"><span data-stu-id="1d419-121">Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine, the DAG that is expressed requires each set of mappers to be followed by one set of reducers.</span></span> <span data-ttu-id="1d419-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span><span class="sxs-lookup"><span data-stu-id="1d419-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span></span> <span data-ttu-id="1d419-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span><span class="sxs-lookup"><span data-stu-id="1d419-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="1d419-124">**Avoids unnecessary writes** Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span><span class="sxs-lookup"><span data-stu-id="1d419-124">**Avoids unnecessary writes** Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span></span> <span data-ttu-id="1d419-125">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span><span class="sxs-lookup"><span data-stu-id="1d419-125">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span></span>
* <span data-ttu-id="1d419-126">**Minimizes start-up delays** Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span><span class="sxs-lookup"><span data-stu-id="1d419-126">**Minimizes start-up delays** Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span></span>
* <span data-ttu-id="1d419-127">**Reuses containers** Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span><span class="sxs-lookup"><span data-stu-id="1d419-127">**Reuses containers** Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span></span>
* <span data-ttu-id="1d419-128">**Continuous optimization techniques** Traditionally optimization was done during compilation phase.</span><span class="sxs-lookup"><span data-stu-id="1d419-128">**Continuous optimization techniques** Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="1d419-129">However more information about the inputs is available that allow for better optimization during runtime.</span><span class="sxs-lookup"><span data-stu-id="1d419-129">However more information about the inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="1d419-130">Tez uses continous optimization techniques that allows it to optimize the plan further into the runtime phase.</span><span class="sxs-lookup"><span data-stu-id="1d419-130">Tez uses continous optimization techniques that allows it to optimize the plan further into the runtime phase.</span></span>

<span data-ttu-id="1d419-131">For more details on these concepts, click [here](http://hortonworks.com/hadoop/tez/)</span><span class="sxs-lookup"><span data-stu-id="1d419-131">For more details on these concepts, click [here](http://hortonworks.com/hadoop/tez/)</span></span>

<span data-ttu-id="1d419-132">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span><span class="sxs-lookup"><span data-stu-id="1d419-132">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="1d419-133">For Windows-based HDInsight clusters, Tez must be enabled at the provision time.</span><span class="sxs-lookup"><span data-stu-id="1d419-133">For Windows-based HDInsight clusters, Tez must be enabled at the provision time.</span></span> <span data-ttu-id="1d419-134">The following is a sample Azure PowerShell script for provisioning a Hadoop cluster with Tez enabled:</span><span class="sxs-lookup"><span data-stu-id="1d419-134">The following is a sample Azure PowerShell script for provisioning a Hadoop cluster with Tez enabled:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $clusterName = "[HDInsightClusterName]"
    $location = "[AzureDataCenter]" #i.e. West US
    $dataNodes = 32 # number of worker nodes in the cluster

    $defaultStorageAccountName = "[DefaultStorageAccountName]"
    $defaultStorageContainerName = "[DefaultBlobContainerName]"
    $defaultStorageAccountKey = $defaultStorageAccountKey = Get-AzureStorageKey $defaultStorageAccountName.ToLower() | %{ $_.Primary }

    $hdiUserName = "[HTTPUserName]"
    $hdiPassword = "[HTTPUserPassword]"

    $hdiSecurePassword = ConvertTo-SecureString $hdiPassword -AsPlainText -Force
    $hdiCredential = New-Object System.Management.Automation.PSCredential($hdiUserName, $hdiSecurePassword)

    $hiveConfig = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightHiveConfiguration'
    $hiveConfig.Configuration = @{ "hive.execution.engine"="tez" }

    New-AzureHDInsightClusterConfig -ClusterSizeInNodes $dataNodes -HeadNodeVMSize Standard_D14 -DataNodeVMSize Standard_D14 |
    Set-AzureHDInsightDefaultStorage -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" -StorageAccountKey $defaultStorageAccountKey -StorageContainerName $defaultStorageContainerName |
    Add-AzureHDInsightConfigValues -Hive $hiveConfig |
    New-AzureHDInsightCluster -Name $clusterName -Location $location -Credential $hdiCredential


> [!NOTE]
> <span data-ttu-id="1d419-135">Linux-based HDInsight clusters have Tez enabled by default.</span><span class="sxs-lookup"><span data-stu-id="1d419-135">Linux-based HDInsight clusters have Tez enabled by default.</span></span>
> 
> 

## <a name="hive-partitioning"></a><span data-ttu-id="1d419-136">Hive partitioning</span><span class="sxs-lookup"><span data-stu-id="1d419-136">Hive partitioning</span></span>
<span data-ttu-id="1d419-137">I/O operation is the major performance bottleneck for running Hive queries.</span><span class="sxs-lookup"><span data-stu-id="1d419-137">I/O operation is the major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="1d419-138">The performance can be improved if the amount of data that needs to be read can be reduced.</span><span class="sxs-lookup"><span data-stu-id="1d419-138">The performance can be improved if the amount of data that needs to be read can be reduced.</span></span> <span data-ttu-id="1d419-139">By default, Hive queries scan entire Hive tables.</span><span class="sxs-lookup"><span data-stu-id="1d419-139">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="1d419-140">This is great for queries like table scans, however for queries that only need to scan a small amount of data (e.g. queries with filtering), this creates unnecessary overhead.</span><span class="sxs-lookup"><span data-stu-id="1d419-140">This is great for queries like table scans, however for queries that only need to scan a small amount of data (e.g. queries with filtering), this creates unnecessary overhead.</span></span> <span data-ttu-id="1d419-141">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span><span class="sxs-lookup"><span data-stu-id="1d419-141">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="1d419-142">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span><span class="sxs-lookup"><span data-stu-id="1d419-142">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span></span> <span data-ttu-id="1d419-143">The following diagram illustrates partitioning a Hive table by the column *Year*.</span><span class="sxs-lookup"><span data-stu-id="1d419-143">The following diagram illustrates partitioning a Hive table by the column *Year*.</span></span> <span data-ttu-id="1d419-144">A new directory is created for each year.</span><span class="sxs-lookup"><span data-stu-id="1d419-144">A new directory is created for each year.</span></span>

![partitioning][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="1d419-146">Some partitioning considerations:</span><span class="sxs-lookup"><span data-stu-id="1d419-146">Some partitioning considerations:</span></span>

* <span data-ttu-id="1d419-147">**Do not under-partition** - Partitioning on columns with only a few values can cause very few partitions.</span><span class="sxs-lookup"><span data-stu-id="1d419-147">**Do not under-partition** - Partitioning on columns with only a few values can cause very few partitions.</span></span> <span data-ttu-id="1d419-148">For example, partitioning on gender will only create two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span><span class="sxs-lookup"><span data-stu-id="1d419-148">For example, partitioning on gender will only create two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span></span>
* <span data-ttu-id="1d419-149">**Do not over-partition** - On the other extreme, creating a partition on a column with a unique value (e.g. userid) will cause multiple partitions causing a lot of stress on the cluster namenode as it will have to handle the large amount of directories.</span><span class="sxs-lookup"><span data-stu-id="1d419-149">**Do not over-partition** - On the other extreme, creating a partition on a column with a unique value (e.g. userid) will cause multiple partitions causing a lot of stress on the cluster namenode as it will have to handle the large amount of directories.</span></span>
* <span data-ttu-id="1d419-150">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span><span class="sxs-lookup"><span data-stu-id="1d419-150">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="1d419-151">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span><span class="sxs-lookup"><span data-stu-id="1d419-151">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span></span>

<span data-ttu-id="1d419-152">To create a partition table, use the *Partitioned By* clause:</span><span class="sxs-lookup"><span data-stu-id="1d419-152">To create a partition table, use the *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="1d419-153">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span><span class="sxs-lookup"><span data-stu-id="1d419-153">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="1d419-154">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span><span class="sxs-lookup"><span data-stu-id="1d419-154">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span></span> <span data-ttu-id="1d419-155">This is shown in the code snippet below.</span><span class="sxs-lookup"><span data-stu-id="1d419-155">This is shown in the code snippet below.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasbs://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="1d419-156">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span><span class="sxs-lookup"><span data-stu-id="1d419-156">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span></span> <span data-ttu-id="1d419-157">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table as shown below:</span><span class="sxs-lookup"><span data-stu-id="1d419-157">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table as shown below:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="1d419-158">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="1d419-158">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-the-orcfile-format"></a><span data-ttu-id="1d419-159">Use the ORCFile format</span><span class="sxs-lookup"><span data-stu-id="1d419-159">Use the ORCFile format</span></span>
<span data-ttu-id="1d419-160">Hive supports different file formats.</span><span class="sxs-lookup"><span data-stu-id="1d419-160">Hive supports different file formats.</span></span> <span data-ttu-id="1d419-161">For example:</span><span class="sxs-lookup"><span data-stu-id="1d419-161">For example:</span></span>

* <span data-ttu-id="1d419-162">**Text**: this is the default file format and works with most scenarios</span><span class="sxs-lookup"><span data-stu-id="1d419-162">**Text**: this is the default file format and works with most scenarios</span></span>
* <span data-ttu-id="1d419-163">**Avro**: works well for interoperability scenarios</span><span class="sxs-lookup"><span data-stu-id="1d419-163">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="1d419-164">**ORC/Parquet**: best suited for performance</span><span class="sxs-lookup"><span data-stu-id="1d419-164">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="1d419-165">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span><span class="sxs-lookup"><span data-stu-id="1d419-165">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span></span> <span data-ttu-id="1d419-166">Compared to other formats, ORC has the following advantages:</span><span class="sxs-lookup"><span data-stu-id="1d419-166">Compared to other formats, ORC has the following advantages:</span></span>

* <span data-ttu-id="1d419-167">support for complex types including DateTime and complex and semi-structured types</span><span class="sxs-lookup"><span data-stu-id="1d419-167">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="1d419-168">up to 70% compression</span><span class="sxs-lookup"><span data-stu-id="1d419-168">up to 70% compression</span></span>
* <span data-ttu-id="1d419-169">indexes every 10,000 rows which allow skipping rows</span><span class="sxs-lookup"><span data-stu-id="1d419-169">indexes every 10,000 rows which allow skipping rows</span></span>
* <span data-ttu-id="1d419-170">a significant drop in run-time execution</span><span class="sxs-lookup"><span data-stu-id="1d419-170">a significant drop in run-time execution</span></span>

<span data-ttu-id="1d419-171">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span><span class="sxs-lookup"><span data-stu-id="1d419-171">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="1d419-172">Next, you insert data to the ORC table from the staging table.</span><span class="sxs-lookup"><span data-stu-id="1d419-172">Next, you insert data to the ORC table from the staging table.</span></span> <span data-ttu-id="1d419-173">For example:</span><span class="sxs-lookup"><span data-stu-id="1d419-173">For example:</span></span>

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

<span data-ttu-id="1d419-174">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="1d419-174">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="1d419-175">Vectorization</span><span class="sxs-lookup"><span data-stu-id="1d419-175">Vectorization</span></span>
<span data-ttu-id="1d419-176">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span><span class="sxs-lookup"><span data-stu-id="1d419-176">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="1d419-177">This means that simple operations are done faster because less internal code needs to run.</span><span class="sxs-lookup"><span data-stu-id="1d419-177">This means that simple operations are done faster because less internal code needs to run.</span></span>

<span data-ttu-id="1d419-178">To enable vectorization prefix your Hive query with the following setting:</span><span class="sxs-lookup"><span data-stu-id="1d419-178">To enable vectorization prefix your Hive query with the following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="1d419-179">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="1d419-179">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="1d419-180">Other optimization methods</span><span class="sxs-lookup"><span data-stu-id="1d419-180">Other optimization methods</span></span>
<span data-ttu-id="1d419-181">There are more optimization methods that you can consider, for example:</span><span class="sxs-lookup"><span data-stu-id="1d419-181">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="1d419-182">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span><span class="sxs-lookup"><span data-stu-id="1d419-182">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span></span>
* <span data-ttu-id="1d419-183">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span><span class="sxs-lookup"><span data-stu-id="1d419-183">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span></span> <span data-ttu-id="1d419-184">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="1d419-184">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="1d419-185">**increase Reducers**</span><span class="sxs-lookup"><span data-stu-id="1d419-185">**increase Reducers**</span></span>

## <a id="nextsteps"></a> <span data-ttu-id="1d419-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d419-186">Next steps</span></span>
<span data-ttu-id="1d419-187">In this article, you have learned several common Hive query optimization methods.</span><span class="sxs-lookup"><span data-stu-id="1d419-187">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="1d419-188">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="1d419-188">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="1d419-189">Use Apache Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d419-189">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1d419-190">Analyze flight delay data by using Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d419-190">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="1d419-191">Analyze Twitter data using Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d419-191">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="1d419-192">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d419-192">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="1d419-193">Use Hive with HDInsight to analyze logs from websites</span><span class="sxs-lookup"><span data-stu-id="1d419-193">Use Hive with HDInsight to analyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png




