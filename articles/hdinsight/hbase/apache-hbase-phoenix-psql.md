---
title: Bulk loading into Apache Phoenix using psql - Azure HDInsight
description: Use the psql tool to load bulk load data into Phoenix tables.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 11/10/2017
ms.author: ashishth
ms.openlocfilehash: 4f4caec33414a9bf644e1b1860686247697b3fb4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868021"
---
# <a name="bulk-load-data-into-phoenix-using-psql"></a><span data-ttu-id="35b5c-103">Bulk load data into Phoenix using psql</span><span class="sxs-lookup"><span data-stu-id="35b5c-103">Bulk load data into Phoenix using psql</span></span>

<span data-ttu-id="35b5c-104">[Apache Phoenix](http://phoenix.apache.org/) is an open source, massively parallel relational database built on [HBase](../hbase/apache-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35b5c-104">[Apache Phoenix](http://phoenix.apache.org/) is an open source, massively parallel relational database built on [HBase](../hbase/apache-hbase-overview.md).</span></span> <span data-ttu-id="35b5c-105">Phoenix provides SQL-like queries over HBase.</span><span class="sxs-lookup"><span data-stu-id="35b5c-105">Phoenix provides SQL-like queries over HBase.</span></span> <span data-ttu-id="35b5c-106">Phoenix uses JDBC drivers to enable users to create, delete, and alter SQL tables, indexes, views and sequences, and upsert rows individually and in bulk.</span><span class="sxs-lookup"><span data-stu-id="35b5c-106">Phoenix uses JDBC drivers to enable users to create, delete, and alter SQL tables, indexes, views and sequences, and upsert rows individually and in bulk.</span></span> <span data-ttu-id="35b5c-107">Phoenix uses noSQL native compilation rather than using MapReduce to compile queries, to create low-latency applications on top of HBase.</span><span class="sxs-lookup"><span data-stu-id="35b5c-107">Phoenix uses noSQL native compilation rather than using MapReduce to compile queries, to create low-latency applications on top of HBase.</span></span> <span data-ttu-id="35b5c-108">Phoenix adds co-processors to support running client-supplied code in the address space of the server, executing the code co-located with the data.</span><span class="sxs-lookup"><span data-stu-id="35b5c-108">Phoenix adds co-processors to support running client-supplied code in the address space of the server, executing the code co-located with the data.</span></span> <span data-ttu-id="35b5c-109">This minimizes client/server data transfer.</span><span class="sxs-lookup"><span data-stu-id="35b5c-109">This minimizes client/server data transfer.</span></span>  <span data-ttu-id="35b5c-110">To work with data using Phoenix in HDInsight, first create tables and then load data into them.</span><span class="sxs-lookup"><span data-stu-id="35b5c-110">To work with data using Phoenix in HDInsight, first create tables and then load data into them.</span></span>

## <a name="bulk-loading-with-phoenix"></a><span data-ttu-id="35b5c-111">Bulk loading with Phoenix</span><span class="sxs-lookup"><span data-stu-id="35b5c-111">Bulk loading with Phoenix</span></span>

<span data-ttu-id="35b5c-112">There are multiple ways to get data into HBase including using client APIs, a MapReduce job with TableOutputFormat, or inputting the data manually using the HBase shell.</span><span class="sxs-lookup"><span data-stu-id="35b5c-112">There are multiple ways to get data into HBase including using client APIs, a MapReduce job with TableOutputFormat, or inputting the data manually using the HBase shell.</span></span> <span data-ttu-id="35b5c-113">Phoenix provides two methods for loading CSV data into Phoenix tables: a client loading tool named `psql`, and a MapReduce-based bulk load tool.</span><span class="sxs-lookup"><span data-stu-id="35b5c-113">Phoenix provides two methods for loading CSV data into Phoenix tables: a client loading tool named `psql`, and a MapReduce-based bulk load tool.</span></span>

<span data-ttu-id="35b5c-114">The `psql` tool is single-threaded and is best suited for loading megabytes or gigabytes of data.</span><span class="sxs-lookup"><span data-stu-id="35b5c-114">The `psql` tool is single-threaded and is best suited for loading megabytes or gigabytes of data.</span></span> <span data-ttu-id="35b5c-115">All CSV files to be loaded must have the '.csv' file extension.</span><span class="sxs-lookup"><span data-stu-id="35b5c-115">All CSV files to be loaded must have the '.csv' file extension.</span></span>  <span data-ttu-id="35b5c-116">You can also specify SQL script files in the `psql` command line with the '.sql' file extension.</span><span class="sxs-lookup"><span data-stu-id="35b5c-116">You can also specify SQL script files in the `psql` command line with the '.sql' file extension.</span></span>

<span data-ttu-id="35b5c-117">Bulk loading with MapReduce is used for much larger data volumes, typically in production scenarios, as MapReduce uses multiple threads.</span><span class="sxs-lookup"><span data-stu-id="35b5c-117">Bulk loading with MapReduce is used for much larger data volumes, typically in production scenarios, as MapReduce uses multiple threads.</span></span>

<span data-ttu-id="35b5c-118">Before you start loading data, verify that Phoenix is enabled and that query timeout settings are as expected.</span><span class="sxs-lookup"><span data-stu-id="35b5c-118">Before you start loading data, verify that Phoenix is enabled and that query timeout settings are as expected.</span></span>  <span data-ttu-id="35b5c-119">Access your HDInsight cluster Ambari dashboard, select HBase, and then the Configuration tab.  Scroll down to verify that Apache Phoenix is set to `enabled` as shown:</span><span class="sxs-lookup"><span data-stu-id="35b5c-119">Access your HDInsight cluster Ambari dashboard, select HBase, and then the Configuration tab.  Scroll down to verify that Apache Phoenix is set to `enabled` as shown:</span></span>

![Apache Phoenix HDInsight Cluster Settings](./media/apache-hbase-phoenix-psql/ambari-phoenix.png)

### <a name="use-psql-to-bulk-load-tables"></a><span data-ttu-id="35b5c-121">Use `psql` to bulk load tables</span><span class="sxs-lookup"><span data-stu-id="35b5c-121">Use `psql` to bulk load tables</span></span>

1. <span data-ttu-id="35b5c-122">Create a new table, then save your query with filename `createCustomersTable.sql`.</span><span class="sxs-lookup"><span data-stu-id="35b5c-122">Create a new table, then save your query with filename `createCustomersTable.sql`.</span></span>

    ```sql
    CREATE TABLE Customers (
        ID varchar NOT NULL PRIMARY KEY,
        Name varchar,
        Income decimal,
        Age INTEGER,
        Country varchar);
    ```

2. <span data-ttu-id="35b5c-123">Copy your CSV file (example contents shown) as `customers.csv` into a `/tmp/` directory for loading into your newly created table.</span><span class="sxs-lookup"><span data-stu-id="35b5c-123">Copy your CSV file (example contents shown) as `customers.csv` into a `/tmp/` directory for loading into your newly created table.</span></span>  <span data-ttu-id="35b5c-124">Use the `hdfs` command to copy the CSV file to your desired source location.</span><span class="sxs-lookup"><span data-stu-id="35b5c-124">Use the `hdfs` command to copy the CSV file to your desired source location.</span></span>

    ```
    1,Samantha,260000.0,18,US
    2,Sam,10000.5,56,US
    3,Anton,550150.0,Norway
    ... 4997 more rows 
    ```

    ```bash
    hdfs dfs -copyToLocal /example/data/customers.csv /tmp/
    ```

3. <span data-ttu-id="35b5c-125">Create a SQL SELECT query to verify the input data loaded properly, then save your query with filename `listCustomers.sql`.</span><span class="sxs-lookup"><span data-stu-id="35b5c-125">Create a SQL SELECT query to verify the input data loaded properly, then save your query with filename `listCustomers.sql`.</span></span> <span data-ttu-id="35b5c-126">You can use any SQL query.</span><span class="sxs-lookup"><span data-stu-id="35b5c-126">You can use any SQL query.</span></span>
     ```sql
    SELECT Name, Income from Customers group by Country;
    ```

4. <span data-ttu-id="35b5c-127">Bulk load the data by opening a *new* Hadoop command window.</span><span class="sxs-lookup"><span data-stu-id="35b5c-127">Bulk load the data by opening a *new* Hadoop command window.</span></span> <span data-ttu-id="35b5c-128">First change to the execution directory location with the `cd` command, and then use the `psql` tool (Python `psql.py` command).</span><span class="sxs-lookup"><span data-stu-id="35b5c-128">First change to the execution directory location with the `cd` command, and then use the `psql` tool (Python `psql.py` command).</span></span> 

    <span data-ttu-id="35b5c-129">The following example expects that you copied the `customers.csv` file from a storage account to your local temp directory using `hdfs` as in step 2 above.</span><span class="sxs-lookup"><span data-stu-id="35b5c-129">The following example expects that you copied the `customers.csv` file from a storage account to your local temp directory using `hdfs` as in step 2 above.</span></span>

    ```bash
    cd /usr/hdp/current/phoenix-client/bin

    python psql.py ZookeeperQuorum createCustomersTable.sql /tmp/customers.csv listCustomers.sql
    ```

    > [!NOTE] 
    > <span data-ttu-id="35b5c-130">To determine the `ZookeeperQuorum` name, locate the zookeeper quorum string in the file `/etc/hbase/conf/hbase-site.xml` with property name `hbase.zookeeper.quorum`.</span><span class="sxs-lookup"><span data-stu-id="35b5c-130">To determine the `ZookeeperQuorum` name, locate the zookeeper quorum string in the file `/etc/hbase/conf/hbase-site.xml` with property name `hbase.zookeeper.quorum`.</span></span>

5. <span data-ttu-id="35b5c-131">After the `psql` operation has completed, you should see a message in your command window:</span><span class="sxs-lookup"><span data-stu-id="35b5c-131">After the `psql` operation has completed, you should see a message in your command window:</span></span>

    ```
    CSV Upsert complete. 5000 rows upserted
    Time: 4.548 sec(s)
    ```

## <a name="use-mapreduce-to-bulk-load-tables"></a><span data-ttu-id="35b5c-132">Use MapReduce to bulk load tables</span><span class="sxs-lookup"><span data-stu-id="35b5c-132">Use MapReduce to bulk load tables</span></span>

<span data-ttu-id="35b5c-133">For higher-throughput loading distributed over the cluster, use the MapReduce load tool.</span><span class="sxs-lookup"><span data-stu-id="35b5c-133">For higher-throughput loading distributed over the cluster, use the MapReduce load tool.</span></span> <span data-ttu-id="35b5c-134">This loader first converts all data into HFiles, and then provides the created HFiles to HBase.</span><span class="sxs-lookup"><span data-stu-id="35b5c-134">This loader first converts all data into HFiles, and then provides the created HFiles to HBase.</span></span>

1. <span data-ttu-id="35b5c-135">Launch the CSV MapReduce loader by using the `hadoop` command with the Phoenix client jar:</span><span class="sxs-lookup"><span data-stu-id="35b5c-135">Launch the CSV MapReduce loader by using the `hadoop` command with the Phoenix client jar:</span></span>

    ```bash
    hadoop jar phoenix-<version>-client.jar org.apache.phoenix.mapreduce.CsvBulkLoadTool --table CUSTOMERS --input /data/customers.csv
    ```

2. <span data-ttu-id="35b5c-136">Create a new table with a SQL statement, as with `CreateCustomersTable.sql` in the previous step 1.</span><span class="sxs-lookup"><span data-stu-id="35b5c-136">Create a new table with a SQL statement, as with `CreateCustomersTable.sql` in the previous step 1.</span></span>

3. <span data-ttu-id="35b5c-137">To verify the schema of your table, run `!describe inputTable`.</span><span class="sxs-lookup"><span data-stu-id="35b5c-137">To verify the schema of your table, run `!describe inputTable`.</span></span>

4. <span data-ttu-id="35b5c-138">Determine the location path to your input data, such as the example `customers.csv` file.</span><span class="sxs-lookup"><span data-stu-id="35b5c-138">Determine the location path to your input data, such as the example `customers.csv` file.</span></span> <span data-ttu-id="35b5c-139">The input files may be in your WASB/ADLS storage account.</span><span class="sxs-lookup"><span data-stu-id="35b5c-139">The input files may be in your WASB/ADLS storage account.</span></span> <span data-ttu-id="35b5c-140">In this example scenario, the input files are in the `<storage account parent>/inputFolderBulkLoad` directory.</span><span class="sxs-lookup"><span data-stu-id="35b5c-140">In this example scenario, the input files are in the `<storage account parent>/inputFolderBulkLoad` directory.</span></span>

5. <span data-ttu-id="35b5c-141">Change to the execution directory for the MapReduce bulk load command:</span><span class="sxs-lookup"><span data-stu-id="35b5c-141">Change to the execution directory for the MapReduce bulk load command:</span></span>

    ```bash
    cd /usr/hdp/current/phoenix-client/bin
    ```

6. <span data-ttu-id="35b5c-142">Locate your `ZookeeperQuorum` value in `/etc/hbase/conf/hbase-site.xml`, with property name `hbase.zookeeper.quorum`.</span><span class="sxs-lookup"><span data-stu-id="35b5c-142">Locate your `ZookeeperQuorum` value in `/etc/hbase/conf/hbase-site.xml`, with property name `hbase.zookeeper.quorum`.</span></span>

7. <span data-ttu-id="35b5c-143">Set up the classpath and run the `CsvBulkLoadTool` tool command:</span><span class="sxs-lookup"><span data-stu-id="35b5c-143">Set up the classpath and run the `CsvBulkLoadTool` tool command:</span></span>

    ```bash
    /usr/hdp/current/phoenix-client$ HADOOP_CLASSPATH=/usr/hdp/current/hbase-client/lib/hbase-protocol.jar:/etc/hbase/conf hadoop jar /usr/hdp/2.4.2.0-258/phoenix/phoenix-4.4.0.2.4.2.0-258-client.jar

    org.apache.phoenix.mapreduce.CsvBulkLoadTool --table Customers --input /inputFolderBulkLoad/customers.csv –zookeeper ZookeeperQuorum:2181:/hbase-unsecure
    ```

8. <span data-ttu-id="35b5c-144">To use MapReduce with ADLS, locate the ADLS root directory, which is the `hbase.rootdir` value in `hbase-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="35b5c-144">To use MapReduce with ADLS, locate the ADLS root directory, which is the `hbase.rootdir` value in `hbase-site.xml`.</span></span> <span data-ttu-id="35b5c-145">In the following command, the ADLS root directory is `adl://hdinsightconf1.azuredatalakestore.net:443/hbase1`.</span><span class="sxs-lookup"><span data-stu-id="35b5c-145">In the following command, the ADLS root directory is `adl://hdinsightconf1.azuredatalakestore.net:443/hbase1`.</span></span> <span data-ttu-id="35b5c-146">In this command, specify the ADLS input and output folders as parameters:</span><span class="sxs-lookup"><span data-stu-id="35b5c-146">In this command, specify the ADLS input and output folders as parameters:</span></span>

    ```bash
    cd /usr/hdp/current/phoenix-client

    $HADOOP_CLASSPATH=$(hbase mapredcp):/etc/hbase/conf hadoop jar /usr/hdp/2.4.2.0-258/phoenix/phoenix-4.4.0.2.4.2.0-258-client.jar

    org.apache.phoenix.mapreduce.CsvBulkLoadTool --table Customers --input adl://hdinsightconf1.azuredatalakestore.net:443/hbase1/data/hbase/temp/input/customers.csv –zookeeper ZookeeperQuorum:2181:/hbase-unsecure --output  adl://hdinsightconf1.azuredatalakestore.net:443/hbase1/data/hbase/output1
    ```

## <a name="recommendations"></a><span data-ttu-id="35b5c-147">Recommendations</span><span class="sxs-lookup"><span data-stu-id="35b5c-147">Recommendations</span></span>

* <span data-ttu-id="35b5c-148">Use the same storage medium for both input and output folders, either  WASB or  ADLS.</span><span class="sxs-lookup"><span data-stu-id="35b5c-148">Use the same storage medium for both input and output folders, either  WASB or  ADLS.</span></span> <span data-ttu-id="35b5c-149">To transfer data from WASB to ADLS, you can use the `distcp` command:</span><span class="sxs-lookup"><span data-stu-id="35b5c-149">To transfer data from WASB to ADLS, you can use the `distcp` command:</span></span>

    ```bash
    hadoop distcp wasb://@.blob.core.windows.net/example/data/gutenberg adl://.azuredatalakestore.net:443/myfolder
    ```

* <span data-ttu-id="35b5c-150">Use larger-size worker nodes.</span><span class="sxs-lookup"><span data-stu-id="35b5c-150">Use larger-size worker nodes.</span></span> <span data-ttu-id="35b5c-151">The map processes of the MapReduce bulk copy produce large amounts of temporary output that fill up the available non-DFS space.</span><span class="sxs-lookup"><span data-stu-id="35b5c-151">The map processes of the MapReduce bulk copy produce large amounts of temporary output that fill up the available non-DFS space.</span></span> <span data-ttu-id="35b5c-152">For a large amount of bulk loading, use more and larger-size worker nodes.</span><span class="sxs-lookup"><span data-stu-id="35b5c-152">For a large amount of bulk loading, use more and larger-size worker nodes.</span></span> <span data-ttu-id="35b5c-153">The number of worker nodes you allocate to your cluster directly affects the processing speed.</span><span class="sxs-lookup"><span data-stu-id="35b5c-153">The number of worker nodes you allocate to your cluster directly affects the processing speed.</span></span>

* <span data-ttu-id="35b5c-154">Split input files into ~10-GB chunks.</span><span class="sxs-lookup"><span data-stu-id="35b5c-154">Split input files into ~10-GB chunks.</span></span> <span data-ttu-id="35b5c-155">Bulk loading is a storage-intensive operation, so splitting your input files into multiple chunks results in better performance.</span><span class="sxs-lookup"><span data-stu-id="35b5c-155">Bulk loading is a storage-intensive operation, so splitting your input files into multiple chunks results in better performance.</span></span>

* <span data-ttu-id="35b5c-156">Avoid region server hotspots.</span><span class="sxs-lookup"><span data-stu-id="35b5c-156">Avoid region server hotspots.</span></span> <span data-ttu-id="35b5c-157">If your row key is monotonically increasing, HBase sequential writes may induce region server hotspotting.</span><span class="sxs-lookup"><span data-stu-id="35b5c-157">If your row key is monotonically increasing, HBase sequential writes may induce region server hotspotting.</span></span> <span data-ttu-id="35b5c-158">*Salting* the row key reduces sequential writes.</span><span class="sxs-lookup"><span data-stu-id="35b5c-158">*Salting* the row key reduces sequential writes.</span></span> <span data-ttu-id="35b5c-159">Phoenix provides a way to transparently salt the row key with a salting byte for a particular table, as referenced below.</span><span class="sxs-lookup"><span data-stu-id="35b5c-159">Phoenix provides a way to transparently salt the row key with a salting byte for a particular table, as referenced below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35b5c-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="35b5c-160">Next steps</span></span>

* [<span data-ttu-id="35b5c-161">Bulk Data Loading with Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="35b5c-161">Bulk Data Loading with Apache Phoenix</span></span>](http://phoenix.apache.org/bulk_dataload.html)
* [<span data-ttu-id="35b5c-162">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="35b5c-162">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>](../hbase/apache-hbase-phoenix-squirrel-linux.md)
* [<span data-ttu-id="35b5c-163">Salted Tables</span><span class="sxs-lookup"><span data-stu-id="35b5c-163">Salted Tables</span></span>](https://phoenix.apache.org/salted.html)
* [<span data-ttu-id="35b5c-164">Phoenix Grammar</span><span class="sxs-lookup"><span data-stu-id="35b5c-164">Phoenix Grammar</span></span>](http://phoenix.apache.org/language/index.html)
