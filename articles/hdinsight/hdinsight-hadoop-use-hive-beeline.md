---
title: Use Beeline to work with Hive on HDInsight (Hadoop) | Microsoft Docs
description: Learn how to use SSH to connect to a Hadoop cluster in HDInsight, and then interactively submit Hive queries by using Beeline. Beeline is a utility for working with HiveServer2 over JDBC.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/05/2017
ms.author: larryfr
ms.openlocfilehash: 7a1757a7ef2881b9e09389745a8e5aeaea2abf9d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540973"
---
# <a name="use-hive-with-hadoop-in-hdinsight-with-beeline"></a><span data-ttu-id="0f2e5-104">Use Hive with Hadoop in HDInsight with Beeline</span><span class="sxs-lookup"><span data-stu-id="0f2e5-104">Use Hive with Hadoop in HDInsight with Beeline</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="0f2e5-105">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-105">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span></span>

<span data-ttu-id="0f2e5-106">Beeline is a command-line tool that is included on the head nodes of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-106">Beeline is a command-line tool that is included on the head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="0f2e5-107">It uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-107">It uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="0f2e5-108">The following table provides connection strings for use with Beeline:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-108">The following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="0f2e5-109">Where you run Beeline from</span><span class="sxs-lookup"><span data-stu-id="0f2e5-109">Where you run Beeline from</span></span> | <span data-ttu-id="0f2e5-110">Connection string</span><span class="sxs-lookup"><span data-stu-id="0f2e5-110">Connection string</span></span> | <span data-ttu-id="0f2e5-111">Other parameters</span><span class="sxs-lookup"><span data-stu-id="0f2e5-111">Other parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f2e5-112">An SSH connection to a headnode</span><span class="sxs-lookup"><span data-stu-id="0f2e5-112">An SSH connection to a headnode</span></span> | `jdbc:hive2://localhost:10001/;transportMode=http` | `-n admin` |
| <span data-ttu-id="0f2e5-113">An edge node</span><span class="sxs-lookup"><span data-stu-id="0f2e5-113">An edge node</span></span> | `jdbc:hive2://headnodehost:10001/;transportMode=http` | `-n admin` |
| <span data-ttu-id="0f2e5-114">Outside the cluster</span><span class="sxs-lookup"><span data-stu-id="0f2e5-114">Outside the cluster</span></span> | `jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2` | `-n admin -p password` |

> [!NOTE]
> <span data-ttu-id="0f2e5-115">Replace 'admin' with the cluster login account for your cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-115">Replace 'admin' with the cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="0f2e5-116">Replace 'password' with the password for the cluster login account.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-116">Replace 'password' with the password for the cluster login account.</span></span>
>
> <span data-ttu-id="0f2e5-117">Replace `clustername` with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-117">Replace `clustername` with the name of your HDInsight cluster.</span></span>

## <a id="prereq"></a><span data-ttu-id="0f2e5-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0f2e5-118">Prerequisites</span></span>

* <span data-ttu-id="0f2e5-119">A Linux-based Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0f2e5-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0f2e5-121">For more information, see [HDInsight version 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="0f2e5-121">For more information, see [HDInsight version 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="0f2e5-122">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-122">An SSH client.</span></span> <span data-ttu-id="0f2e5-123">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0f2e5-123">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a id="ssh"></a><span data-ttu-id="0f2e5-124">Connect with SSH</span><span class="sxs-lookup"><span data-stu-id="0f2e5-124">Connect with SSH</span></span>

<span data-ttu-id="0f2e5-125">Connect to your cluster using SSH using the following command:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-125">Connect to your cluster using SSH using the following command:</span></span>

```bash
ssh sshuser@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="0f2e5-126">Replace `sshuser` with the SSH account for your cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-126">Replace `sshuser` with the SSH account for your cluster.</span></span> <span data-ttu-id="0f2e5-127">Replace `myhdinsight` with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-127">Replace `myhdinsight` with the name of your HDInsight cluster.</span></span>

<span data-ttu-id="0f2e5-128">**If you provided a password for SSH authentication** when you created the HDInsight cluster, you must provide the password when prompted.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-128">**If you provided a password for SSH authentication** when you created the HDInsight cluster, you must provide the password when prompted.</span></span>

<span data-ttu-id="0f2e5-129">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-129">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system:</span></span>

    ssh -i ~/.ssh/mykey.key ssh@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="0f2e5-130">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0f2e5-130">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a id="beeline"></a><span data-ttu-id="0f2e5-131">Use the Beeline command</span><span class="sxs-lookup"><span data-stu-id="0f2e5-131">Use the Beeline command</span></span>

1. <span data-ttu-id="0f2e5-132">From the SSH session, use the following command to start Beeline:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-132">From the SSH session, use the following command to start Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="0f2e5-133">This command starts the Beeline client, and connect to the HiveServer2 on the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-133">This command starts the Beeline client, and connect to the HiveServer2 on the cluster head node.</span></span> <span data-ttu-id="0f2e5-134">The `-n` parameter is used to provide the cluster login account.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-134">The `-n` parameter is used to provide the cluster login account.</span></span> <span data-ttu-id="0f2e5-135">The default login is `admin`.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-135">The default login is `admin`.</span></span> <span data-ttu-id="0f2e5-136">If you used a different name during cluster creation, use it instead of `admin`.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-136">If you used a different name during cluster creation, use it instead of `admin`.</span></span>

    <span data-ttu-id="0f2e5-137">Once the command completes, you arrive at a `jdbc:hive2://localhost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-137">Once the command completes, you arrive at a `jdbc:hive2://localhost:10001/>` prompt.</span></span>

2. <span data-ttu-id="0f2e5-138">Beeline commands begin with a `!` character, for example `!help` displays help.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-138">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="0f2e5-139">However the `!` can be omitted for some commands.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-139">However the `!` can be omitted for some commands.</span></span> <span data-ttu-id="0f2e5-140">For example, `help` also works.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-140">For example, `help` also works.</span></span>

    <span data-ttu-id="0f2e5-141">There is a `!sql`, which is used to execute HiveQL statements.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-141">There is a `!sql`, which is used to execute HiveQL statements.</span></span> <span data-ttu-id="0f2e5-142">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-142">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span></span> <span data-ttu-id="0f2e5-143">The following two statements are equivalent:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-143">The following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="0f2e5-144">On a new cluster, only one table is listed: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-144">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="0f2e5-145">Use the following command to display the schema for the hivesampletable:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-145">Use the following command to display the schema for the hivesampletable:</span></span>

    ```bash
    describe hivesampletable;
    ```

    <span data-ttu-id="0f2e5-146">This command returns the following information:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-146">This command returns the following information:</span></span>

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

    <span data-ttu-id="0f2e5-147">This information describes the columns in the table.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-147">This information describes the columns in the table.</span></span> <span data-ttu-id="0f2e5-148">While we could perform some queries against this data, let's instead create a brand new table to demonstrate how to load data into Hive and apply a schema.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-148">While we could perform some queries against this data, let's instead create a brand new table to demonstrate how to load data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="0f2e5-149">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-149">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasbs:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="0f2e5-150">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-150">These statements perform the following actions:</span></span>

    * <span data-ttu-id="0f2e5-151">**DROP TABLE** - If the table exists, it is deleted.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-151">**DROP TABLE** - If the table exists, it is deleted.</span></span>

    * <span data-ttu-id="0f2e5-152">**CREATE EXTERNAL TABLE** - Creates an **external** table in Hive.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-152">**CREATE EXTERNAL TABLE** - Creates an **external** table in Hive.</span></span> <span data-ttu-id="0f2e5-153">External tables only store the table definition in Hive.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-153">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="0f2e5-154">The data is left in the original location.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-154">The data is left in the original location.</span></span>

    * <span data-ttu-id="0f2e5-155">**ROW FORMAT** - How the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-155">**ROW FORMAT** - How the data is formatted.</span></span> <span data-ttu-id="0f2e5-156">In this case, the fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-156">In this case, the fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="0f2e5-157">**STORED AS TEXTFILE LOCATION** - Where the data is stored and in what file format.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-157">**STORED AS TEXTFILE LOCATION** - Where the data is stored and in what file format.</span></span>

    * <span data-ttu-id="0f2e5-158">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-158">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="0f2e5-159">This query returns a value of **3** as there are three rows that contain this value.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-159">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="0f2e5-160">**INPUT__FILE__NAME LIKE '%.log'** - The example data file is stored with other files.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-160">**INPUT__FILE__NAME LIKE '%.log'** - The example data file is stored with other files.</span></span> <span data-ttu-id="0f2e5-161">This statement limits the query to data stored in files that end in .log.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-161">This statement limits the query to data stored in files that end in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0f2e5-162">External tables should be used when you expect the underlying data to be updated by an external source.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-162">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="0f2e5-163">For example, an automated data upload process or a MapReduce operation.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="0f2e5-164">Dropping an external table does **not** delete the data, only the table definition.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-164">Dropping an external table does **not** delete the data, only the table definition.</span></span>

    <span data-ttu-id="0f2e5-165">The output of this command is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-165">The output of this command is similar to the following text:</span></span>

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

5. <span data-ttu-id="0f2e5-166">To exit Beeline, use `!exit`.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-166">To exit Beeline, use `!exit`.</span></span>

## <a id="file"></a><span data-ttu-id="0f2e5-167">Run a HiveQL file</span><span class="sxs-lookup"><span data-stu-id="0f2e5-167">Run a HiveQL file</span></span>

<span data-ttu-id="0f2e5-168">Use the following steps to create a file, then run it using Beeline.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-168">Use the following steps to create a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="0f2e5-169">Use the following command to create a file named **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-169">Use the following command to create a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="0f2e5-170">Use the following text as the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-170">Use the following text as the contents of the file.</span></span> <span data-ttu-id="0f2e5-171">This query creates a new 'internal' table named **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="0f2e5-172">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-172">These statements perform the following actions:</span></span>

    * <span data-ttu-id="0f2e5-173">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-173">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span></span> <span data-ttu-id="0f2e5-174">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-174">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="0f2e5-175">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-175">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="0f2e5-176">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-176">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="0f2e5-177">ORC format is a highly optimized and efficient format for storing Hive data.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="0f2e5-178">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-178">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0f2e5-179">Unlike external tables, dropping an internal table deletes the underlying data as well.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-179">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

3. <span data-ttu-id="0f2e5-180">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-180">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="0f2e5-181">Use the following to run the file using Beeline.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-181">Use the following to run the file using Beeline.</span></span> <span data-ttu-id="0f2e5-182">Replace **HOSTNAME** with the name obtained earlier for the head node, and **PASSWORD** with the password for the admin account:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-182">Replace **HOSTNAME** with the name obtained earlier for the head node, and **PASSWORD** with the password for the admin account:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="0f2e5-183">The `-i` parameter starts Beeline, runs the statements in the query.hql file.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-183">The `-i` parameter starts Beeline, runs the statements in the query.hql file.</span></span> <span data-ttu-id="0f2e5-184">Once the query completes, you arrive at the `jdbc:hive2://localhost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-184">Once the query completes, you arrive at the `jdbc:hive2://localhost:10001/>` prompt.</span></span> <span data-ttu-id="0f2e5-185">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-185">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span></span>

5. <span data-ttu-id="0f2e5-186">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-186">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="0f2e5-187">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-187">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a name="edge-nodes"></a><span data-ttu-id="0f2e5-188">Edge nodes</span><span class="sxs-lookup"><span data-stu-id="0f2e5-188">Edge nodes</span></span>

<span data-ttu-id="0f2e5-189">If your cluster has an edge node, we recommend always using the edge node instead of the head node when connecting with SSH.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-189">If your cluster has an edge node, we recommend always using the edge node instead of the head node when connecting with SSH.</span></span> <span data-ttu-id="0f2e5-190">To start Beeline from an SSH connection to an edge node, use the following command:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-190">To start Beeline from an SSH connection to an edge node, use the following command:</span></span>

```bash
beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -n admin
```

## <a name="remote-clients"></a><span data-ttu-id="0f2e5-191">Remote clients</span><span class="sxs-lookup"><span data-stu-id="0f2e5-191">Remote clients</span></span>

<span data-ttu-id="0f2e5-192">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-192">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use the following parameters:</span></span>

* <span data-ttu-id="0f2e5-193">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="0f2e5-193">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="0f2e5-194">__Cluster login name__: `-n admin`</span><span class="sxs-lookup"><span data-stu-id="0f2e5-194">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="0f2e5-195">__Cluster login password__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="0f2e5-195">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="0f2e5-196">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-196">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span></span>

<span data-ttu-id="0f2e5-197">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span><span class="sxs-lookup"><span data-stu-id="0f2e5-197">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span></span>

## <a id="summary"></a><span data-ttu-id="0f2e5-198"><a id="nextsteps"></a>Next steps</span><span class="sxs-lookup"><span data-stu-id="0f2e5-198"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="0f2e5-199">For more general information on Hive in HDInsight, see the following document:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-199">For more general information on Hive in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="0f2e5-200">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f2e5-200">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="0f2e5-201">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-201">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="0f2e5-202">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f2e5-202">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0f2e5-203">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f2e5-203">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="0f2e5-204">If you are using Tez with Hive, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="0f2e5-204">If you are using Tez with Hive, see the following documents:</span></span>

* [<span data-ttu-id="0f2e5-205">Use the Tez UI on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f2e5-205">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="0f2e5-206">Use the Ambari Tez view on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f2e5-206">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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


[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
