---
title: Use Beeline with Apache Hive - Azure HDInsight
description: Learn how to use the Beeline client to run Hive queries with Hadoop on HDInsight. Beeline is a utility for working with HiveServer2 over JDBC.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
keywords: beeline hive,hive beeline
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 04/20/2018
ms.author: jasonh
ms.openlocfilehash: 872b0e8ae3469cf3807268e07ca87cec9b00a70b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867068"
---
# <a name="use-the-beeline-client-with-apache-hive"></a><span data-ttu-id="3df5f-105">Use the Beeline client with Apache Hive</span><span class="sxs-lookup"><span data-stu-id="3df5f-105">Use the Beeline client with Apache Hive</span></span>

<span data-ttu-id="3df5f-106">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3df5f-106">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span></span>

<span data-ttu-id="3df5f-107">Beeline is a Hive client that is included on the head nodes of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3df5f-107">Beeline is a Hive client that is included on the head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="3df5f-108">Beeline uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3df5f-108">Beeline uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="3df5f-109">You can also use Beeline to access Hive on HDInsight remotely over the internet.</span><span class="sxs-lookup"><span data-stu-id="3df5f-109">You can also use Beeline to access Hive on HDInsight remotely over the internet.</span></span> <span data-ttu-id="3df5f-110">The following examples provide the most common connection strings used to connect to HDInsight from Beeline:</span><span class="sxs-lookup"><span data-stu-id="3df5f-110">The following examples provide the most common connection strings used to connect to HDInsight from Beeline:</span></span>

* <span data-ttu-id="3df5f-111">__Using Beeline from an SSH connection to a headnode or edge node__: `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'`</span><span class="sxs-lookup"><span data-stu-id="3df5f-111">__Using Beeline from an SSH connection to a headnode or edge node__: `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'`</span></span>
* <span data-ttu-id="3df5f-112">__Using Beeline on a client, connecting to HDInsight over an Azure Virtual Network__: `-u 'jdbc:hive2://<headnode-FQDN>:10001/;transportMode=http'`</span><span class="sxs-lookup"><span data-stu-id="3df5f-112">__Using Beeline on a client, connecting to HDInsight over an Azure Virtual Network__: `-u 'jdbc:hive2://<headnode-FQDN>:10001/;transportMode=http'`</span></span>
* <span data-ttu-id="3df5f-113">__Using Beeline on a client, connecting to HDInsight over the public internet__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password`</span><span class="sxs-lookup"><span data-stu-id="3df5f-113">__Using Beeline on a client, connecting to HDInsight over the public internet__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password`</span></span>

> [!NOTE]
> <span data-ttu-id="3df5f-114">Replace `admin` with the cluster login account for your cluster.</span><span class="sxs-lookup"><span data-stu-id="3df5f-114">Replace `admin` with the cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="3df5f-115">Replace `password` with the password for the cluster login account.</span><span class="sxs-lookup"><span data-stu-id="3df5f-115">Replace `password` with the password for the cluster login account.</span></span>
>
> <span data-ttu-id="3df5f-116">Replace `clustername` with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3df5f-116">Replace `clustername` with the name of your HDInsight cluster.</span></span>
>
> <span data-ttu-id="3df5f-117">When connecting to the cluster through a virtual network, replace `<headnode-FQDN>` with the fully qualified domain name of a cluster headnode.</span><span class="sxs-lookup"><span data-stu-id="3df5f-117">When connecting to the cluster through a virtual network, replace `<headnode-FQDN>` with the fully qualified domain name of a cluster headnode.</span></span>

## <a id="prereq"></a><span data-ttu-id="3df5f-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3df5f-118">Prerequisites</span></span>

* <span data-ttu-id="3df5f-119">A Linux-based Hadoop on HDInsight cluster version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="3df5f-119">A Linux-based Hadoop on HDInsight cluster version 3.4 or greater.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3df5f-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="3df5f-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3df5f-121">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3df5f-121">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="3df5f-122">An SSH client or a local Beeline client.</span><span class="sxs-lookup"><span data-stu-id="3df5f-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="3df5f-123">Most of the steps in this document assume that you are using Beeline from an SSH session to the cluster.</span><span class="sxs-lookup"><span data-stu-id="3df5f-123">Most of the steps in this document assume that you are using Beeline from an SSH session to the cluster.</span></span> <span data-ttu-id="3df5f-124">For information on running Beeline from outside the cluster, see the [use Beeline remotely](#remote) section.</span><span class="sxs-lookup"><span data-stu-id="3df5f-124">For information on running Beeline from outside the cluster, see the [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="3df5f-125">For more information on using SSH, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3df5f-125">For more information on using SSH, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a id="beeline"></a><span data-ttu-id="3df5f-126">Run a Hive query</span><span class="sxs-lookup"><span data-stu-id="3df5f-126">Run a Hive query</span></span>

1. <span data-ttu-id="3df5f-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="3df5f-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster:</span></span>

    * <span data-ttu-id="3df5f-128">When connecting over the public internet, you must provide the cluster login account name (default `admin`) and password.</span><span class="sxs-lookup"><span data-stu-id="3df5f-128">When connecting over the public internet, you must provide the cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="3df5f-129">For example, using Beeline from a client system to connect to the `<clustername>.azurehdinsight.net` address.</span><span class="sxs-lookup"><span data-stu-id="3df5f-129">For example, using Beeline from a client system to connect to the `<clustername>.azurehdinsight.net` address.</span></span> <span data-ttu-id="3df5f-130">This connection is made over port `443`, and is encrypted using SSL:</span><span class="sxs-lookup"><span data-stu-id="3df5f-130">This connection is made over port `443`, and is encrypted using SSL:</span></span>

        ```bash
        beeline -u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password
        ```

    * <span data-ttu-id="3df5f-131">When connecting from an SSH session to a cluster headnode, you can connect to the `headnodehost` address on port `10001`:</span><span class="sxs-lookup"><span data-stu-id="3df5f-131">When connecting from an SSH session to a cluster headnode, you can connect to the `headnodehost` address on port `10001`:</span></span>

        ```bash
        beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
        ```

    * <span data-ttu-id="3df5f-132">When connecting over an Azure Virtual Network, you must provide the fully qualified domain name (FQDN) of a cluster head node.</span><span class="sxs-lookup"><span data-stu-id="3df5f-132">When connecting over an Azure Virtual Network, you must provide the fully qualified domain name (FQDN) of a cluster head node.</span></span> <span data-ttu-id="3df5f-133">Since this connection is made directly to the cluster nodes, the connection uses port `10001`:</span><span class="sxs-lookup"><span data-stu-id="3df5f-133">Since this connection is made directly to the cluster nodes, the connection uses port `10001`:</span></span>

        ```bash
        beeline -u 'jdbc:hive2://<headnode-FQDN>:10001/;transportMode=http'
        ```

2. <span data-ttu-id="3df5f-134">Beeline commands begin with a `!` character, for example `!help` displays help.</span><span class="sxs-lookup"><span data-stu-id="3df5f-134">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="3df5f-135">However the `!` can be omitted for some commands.</span><span class="sxs-lookup"><span data-stu-id="3df5f-135">However the `!` can be omitted for some commands.</span></span> <span data-ttu-id="3df5f-136">For example, `help` also works.</span><span class="sxs-lookup"><span data-stu-id="3df5f-136">For example, `help` also works.</span></span>

    <span data-ttu-id="3df5f-137">There is a `!sql`, which is used to execute HiveQL statements.</span><span class="sxs-lookup"><span data-stu-id="3df5f-137">There is a `!sql`, which is used to execute HiveQL statements.</span></span> <span data-ttu-id="3df5f-138">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span><span class="sxs-lookup"><span data-stu-id="3df5f-138">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span></span> <span data-ttu-id="3df5f-139">The following two statements are equivalent:</span><span class="sxs-lookup"><span data-stu-id="3df5f-139">The following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="3df5f-140">On a new cluster, only one table is listed: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="3df5f-140">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="3df5f-141">Use the following command to display the schema for the hivesampletable:</span><span class="sxs-lookup"><span data-stu-id="3df5f-141">Use the following command to display the schema for the hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="3df5f-142">This command returns the following information:</span><span class="sxs-lookup"><span data-stu-id="3df5f-142">This command returns the following information:</span></span>

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    <span data-ttu-id="3df5f-143">This information describes the columns in the table.</span><span class="sxs-lookup"><span data-stu-id="3df5f-143">This information describes the columns in the table.</span></span>

4. <span data-ttu-id="3df5f-144">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="3df5f-144">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (
        t1 string,
        t2 string,
        t3 string,
        t4 string,
        t5 string,
        t6 string,
        t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs 
        WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' 
        GROUP BY t4;
    ```

    <span data-ttu-id="3df5f-145">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="3df5f-145">These statements perform the following actions:</span></span>

    * <span data-ttu-id="3df5f-146">`DROP TABLE` - If the table exists, it is deleted.</span><span class="sxs-lookup"><span data-stu-id="3df5f-146">`DROP TABLE` - If the table exists, it is deleted.</span></span>

    * <span data-ttu-id="3df5f-147">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span><span class="sxs-lookup"><span data-stu-id="3df5f-147">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="3df5f-148">External tables only store the table definition in Hive.</span><span class="sxs-lookup"><span data-stu-id="3df5f-148">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="3df5f-149">The data is left in the original location.</span><span class="sxs-lookup"><span data-stu-id="3df5f-149">The data is left in the original location.</span></span>

    * <span data-ttu-id="3df5f-150">`ROW FORMAT` - How the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="3df5f-150">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="3df5f-151">In this case, the fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="3df5f-151">In this case, the fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="3df5f-152">`STORED AS TEXTFILE LOCATION` - Where the data is stored and in what file format.</span><span class="sxs-lookup"><span data-stu-id="3df5f-152">`STORED AS TEXTFILE LOCATION` - Where the data is stored and in what file format.</span></span>

    * <span data-ttu-id="3df5f-153">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="3df5f-153">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="3df5f-154">This query returns a value of **3** as there are three rows that contain this value.</span><span class="sxs-lookup"><span data-stu-id="3df5f-154">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="3df5f-155">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span><span class="sxs-lookup"><span data-stu-id="3df5f-155">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="3df5f-156">In this case, the directory contains files that do not match the schema.</span><span class="sxs-lookup"><span data-stu-id="3df5f-156">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="3df5f-157">To prevent garbage data in the results, this statement tells Hive that it should only return data from files ending in .log.</span><span class="sxs-lookup"><span data-stu-id="3df5f-157">To prevent garbage data in the results, this statement tells Hive that it should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3df5f-158">External tables should be used when you expect the underlying data to be updated by an external source.</span><span class="sxs-lookup"><span data-stu-id="3df5f-158">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="3df5f-159">For example, an automated data upload process or a MapReduce operation.</span><span class="sxs-lookup"><span data-stu-id="3df5f-159">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="3df5f-160">Dropping an external table does **not** delete the data, only the table definition.</span><span class="sxs-lookup"><span data-stu-id="3df5f-160">Dropping an external table does **not** delete the data, only the table definition.</span></span>

    <span data-ttu-id="3df5f-161">The output of this command is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="3df5f-161">The output of this command is similar to the following text:</span></span>

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. <span data-ttu-id="3df5f-162">To exit Beeline, use `!exit`.</span><span class="sxs-lookup"><span data-stu-id="3df5f-162">To exit Beeline, use `!exit`.</span></span>

### <a id="file"></a><span data-ttu-id="3df5f-163">Use Beeline to run a HiveQL file</span><span class="sxs-lookup"><span data-stu-id="3df5f-163">Use Beeline to run a HiveQL file</span></span>

<span data-ttu-id="3df5f-164">Use the following steps to create a file, then run it using Beeline.</span><span class="sxs-lookup"><span data-stu-id="3df5f-164">Use the following steps to create a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="3df5f-165">Use the following command to create a file named **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="3df5f-165">Use the following command to create a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="3df5f-166">Use the following text as the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="3df5f-166">Use the following text as the contents of the file.</span></span> <span data-ttu-id="3df5f-167">This query creates a new 'internal' table named **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="3df5f-167">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="3df5f-168">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="3df5f-168">These statements perform the following actions:</span></span>

    * <span data-ttu-id="3df5f-169">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span><span class="sxs-lookup"><span data-stu-id="3df5f-169">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span></span> <span data-ttu-id="3df5f-170">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span><span class="sxs-lookup"><span data-stu-id="3df5f-170">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="3df5f-171">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span><span class="sxs-lookup"><span data-stu-id="3df5f-171">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="3df5f-172">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="3df5f-172">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="3df5f-173">ORC format is a highly optimized and efficient format for storing Hive data.</span><span class="sxs-lookup"><span data-stu-id="3df5f-173">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="3df5f-174">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span><span class="sxs-lookup"><span data-stu-id="3df5f-174">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3df5f-175">Unlike external tables, dropping an internal table deletes the underlying data as well.</span><span class="sxs-lookup"><span data-stu-id="3df5f-175">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

3. <span data-ttu-id="3df5f-176">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3df5f-176">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="3df5f-177">Use the following to run the file using Beeline:</span><span class="sxs-lookup"><span data-stu-id="3df5f-177">Use the following to run the file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="3df5f-178">The `-i` parameter starts Beeline and runs the statements in the `query.hql` file.</span><span class="sxs-lookup"><span data-stu-id="3df5f-178">The `-i` parameter starts Beeline and runs the statements in the `query.hql` file.</span></span> <span data-ttu-id="3df5f-179">Once the query completes, you arrive at the `jdbc:hive2://headnodehost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="3df5f-179">Once the query completes, you arrive at the `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="3df5f-180">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span><span class="sxs-lookup"><span data-stu-id="3df5f-180">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span></span>

5. <span data-ttu-id="3df5f-181">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="3df5f-181">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="3df5f-182">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span><span class="sxs-lookup"><span data-stu-id="3df5f-182">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a><span data-ttu-id="3df5f-183">Use Beeline remotely</span><span class="sxs-lookup"><span data-stu-id="3df5f-183">Use Beeline remotely</span></span>

<span data-ttu-id="3df5f-184">If you have Beeline installed locally, and connect over the public internet, use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="3df5f-184">If you have Beeline installed locally, and connect over the public internet, use the following parameters:</span></span>

* <span data-ttu-id="3df5f-185">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="3df5f-185">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="3df5f-186">__Cluster login name__: `-n admin`</span><span class="sxs-lookup"><span data-stu-id="3df5f-186">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="3df5f-187">__Cluster login password__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="3df5f-187">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="3df5f-188">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3df5f-188">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span></span>

<span data-ttu-id="3df5f-189">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span><span class="sxs-lookup"><span data-stu-id="3df5f-189">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span></span>

<span data-ttu-id="3df5f-190">If you have Beeline installed locally, and connect over an Azure Virtual Network, use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="3df5f-190">If you have Beeline installed locally, and connect over an Azure Virtual Network, use the following parameters:</span></span>

* <span data-ttu-id="3df5f-191">__Connection string__: `-u 'jdbc:hive2://<headnode-FQDN>:10001/;transportMode=http'`</span><span class="sxs-lookup"><span data-stu-id="3df5f-191">__Connection string__: `-u 'jdbc:hive2://<headnode-FQDN>:10001/;transportMode=http'`</span></span>

<span data-ttu-id="3df5f-192">To find the fully qualified domain name of a headnode, use the information in the [Manage HDInsight using the Ambari REST API](../hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.</span><span class="sxs-lookup"><span data-stu-id="3df5f-192">To find the fully qualified domain name of a headnode, use the information in the [Manage HDInsight using the Ambari REST API](../hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.</span></span>

## <a id="sparksql"></a><span data-ttu-id="3df5f-193">Use Beeline with Spark</span><span class="sxs-lookup"><span data-stu-id="3df5f-193">Use Beeline with Spark</span></span>

<span data-ttu-id="3df5f-194">Spark provides its own implementation of HiveServer2, which is sometimes referred to as the Spark Thrift server.</span><span class="sxs-lookup"><span data-stu-id="3df5f-194">Spark provides its own implementation of HiveServer2, which is sometimes referred to as the Spark Thrift server.</span></span> <span data-ttu-id="3df5f-195">This service uses Spark SQL to resolve queries instead of Hive, and may provide better performance depending on your query.</span><span class="sxs-lookup"><span data-stu-id="3df5f-195">This service uses Spark SQL to resolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="3df5f-196">The __connection string__ used when connecting over the internet is slightly different.</span><span class="sxs-lookup"><span data-stu-id="3df5f-196">The __connection string__ used when connecting over the internet is slightly different.</span></span> <span data-ttu-id="3df5f-197">Instead of containing `httpPath=/hive2` it is `httpPath/sparkhive2`.</span><span class="sxs-lookup"><span data-stu-id="3df5f-197">Instead of containing `httpPath=/hive2` it is `httpPath/sparkhive2`.</span></span> <span data-ttu-id="3df5f-198">The following is an example of connecting over the internet:</span><span class="sxs-lookup"><span data-stu-id="3df5f-198">The following is an example of connecting over the internet:</span></span>

```bash 
beeline -u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/sparkhive2' -n admin -p password
```

<span data-ttu-id="3df5f-199">When connecting directly from the cluster head node, or from a resource inside the same Azure Virtual Network as the HDInsight cluster, port `10002` should be used for Spark Thrift server instead of `10001`.</span><span class="sxs-lookup"><span data-stu-id="3df5f-199">When connecting directly from the cluster head node, or from a resource inside the same Azure Virtual Network as the HDInsight cluster, port `10002` should be used for Spark Thrift server instead of `10001`.</span></span> <span data-ttu-id="3df5f-200">The following is an example of connecting to directly to the head node:</span><span class="sxs-lookup"><span data-stu-id="3df5f-200">The following is an example of connecting to directly to the head node:</span></span>

```bash
beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'
```

## <a id="summary"></a><span data-ttu-id="3df5f-201"><a id="nextsteps"></a>Next steps</span><span class="sxs-lookup"><span data-stu-id="3df5f-201"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3df5f-202">For more general information on Hive in HDInsight, see the following document:</span><span class="sxs-lookup"><span data-stu-id="3df5f-202">For more general information on Hive in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="3df5f-203">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="3df5f-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="3df5f-204">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="3df5f-204">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="3df5f-205">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="3df5f-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="3df5f-206">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="3df5f-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="3df5f-207">If you are using Tez with Hive, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="3df5f-207">If you are using Tez with Hive, see the following documents:</span></span>

* [<span data-ttu-id="3df5f-208">Use the Tez UI on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="3df5f-208">Use the Tez UI on Windows-based HDInsight</span></span>](../hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="3df5f-209">Use the Ambari Tez view on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="3df5f-209">Use the Ambari Tez view on Linux-based HDInsight</span></span>](../hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
