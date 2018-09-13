---
title: Use Hadoop Oozie workflows in Linux-based HDInsight | Microsoft Docs
description: Use Hadoop Oozie in Linux-based HDInsight. Learn how to define an Oozie workflow, and submit an Oozie job.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: larryfr
ms.openlocfilehash: c8cb7662955ad36835e34c98208b5c1aec38417c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550625"
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="ba6cb-104">Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="ba6cb-104">Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="ba6cb-105">Learn how to use Apache Oozie to define a workflow that uses Hive and Sqoop, and then run the workflow on a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-105">Learn how to use Apache Oozie to define a workflow that uses Hive and Sqoop, and then run the workflow on a Linux-based HDInsight cluster.</span></span>

<span data-ttu-id="ba6cb-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="ba6cb-107">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-107">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="ba6cb-108">It can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts</span><span class="sxs-lookup"><span data-stu-id="ba6cb-108">It can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="ba6cb-109">Another option for defining workflows with HDInsight is Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-109">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="ba6cb-110">To learn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="ba6cb-110">To learn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba6cb-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ba6cb-111">Prerequisites</span></span>

<span data-ttu-id="ba6cb-112">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-112">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="ba6cb-113">**Azure CLI**: See [Install and Configure the Azure CLI](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="ba6cb-113">**Azure CLI**: See [Install and Configure the Azure CLI](../cli-install-nodejs.md)</span></span>

* <span data-ttu-id="ba6cb-114">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="ba6cb-114">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ba6cb-115">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-115">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="ba6cb-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ba6cb-117">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="ba6cb-117">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="ba6cb-118">**An Azure SQL database**: This is created using the steps in this document</span><span class="sxs-lookup"><span data-stu-id="ba6cb-118">**An Azure SQL database**: This is created using the steps in this document</span></span>

## <a name="example-workflow"></a><span data-ttu-id="ba6cb-119">Example workflow</span><span class="sxs-lookup"><span data-stu-id="ba6cb-119">Example workflow</span></span>

<span data-ttu-id="ba6cb-120">The workflow used in this document contains two actions.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-120">The workflow used in this document contains two actions.</span></span> <span data-ttu-id="ba6cb-121">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-121">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Workflow diagram][img-workflow-diagram]

1. <span data-ttu-id="ba6cb-123">A Hive action runs a HiveQL script to extract records from the **hivesampletable** included with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-123">A Hive action runs a HiveQL script to extract records from the **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="ba6cb-124">Each row of data describes a visit from a specific mobile device.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-124">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="ba6cb-125">The record format appears similar to the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-125">The record format appears similar to the following:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="ba6cb-126">The Hive script used in this document counts the total visits for each platform (such as Android or iPhone,) and stores the counts to a new Hive table.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-126">The Hive script used in this document counts the total visits for each platform (such as Android or iPhone,) and stores the counts to a new Hive table.</span></span>

    <span data-ttu-id="ba6cb-127">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="ba6cb-127">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="ba6cb-128">A Sqoop action exports the contents of the new Hive table to a table in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-128">A Sqoop action exports the contents of the new Hive table to a table in an Azure SQL database.</span></span> <span data-ttu-id="ba6cb-129">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="ba6cb-129">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="ba6cb-130">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="ba6cb-130">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-the-working-directory"></a><span data-ttu-id="ba6cb-131">Create the working directory</span><span class="sxs-lookup"><span data-stu-id="ba6cb-131">Create the working directory</span></span>

<span data-ttu-id="ba6cb-132">Oozie expects resources required for a job to be stored in the same directory.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-132">Oozie expects resources required for a job to be stored in the same directory.</span></span> <span data-ttu-id="ba6cb-133">This example uses **wasbs:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-133">This example uses **wasbs:///tutorials/useoozie**.</span></span> <span data-ttu-id="ba6cb-134">Use the following command to create this directory, and the data directory that holds the new Hive table created by this workflow:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-134">Use the following command to create this directory, and the data directory that holds the new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="ba6cb-135">The `-p` parameter caused all directories in the path to be created if they do not already exist.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-135">The `-p` parameter caused all directories in the path to be created if they do not already exist.</span></span> <span data-ttu-id="ba6cb-136">The **data** directory is used to hold data used by the **useooziewf.hql** script.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-136">The **data** directory is used to hold data used by the **useooziewf.hql** script.</span></span>

<span data-ttu-id="ba6cb-137">Also run the following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-137">Also run the following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="ba6cb-138">Replace **USERNAME** with your login name:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-138">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

<span data-ttu-id="ba6cb-139">If you receive an error that the user is already a member of users, you can just ignore it.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-139">If you receive an error that the user is already a member of users, you can just ignore it.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="ba6cb-140">Add a database driver</span><span class="sxs-lookup"><span data-stu-id="ba6cb-140">Add a database driver</span></span>

<span data-ttu-id="ba6cb-141">Since this workflow uses Sqoop to export data to SQL Database, you must provide a copy of the JDBC driver used to talk to SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-141">Since this workflow uses Sqoop to export data to SQL Database, you must provide a copy of the JDBC driver used to talk to SQL Database.</span></span> <span data-ttu-id="ba6cb-142">Use the following command to copy it to the working directory:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-142">Use the following command to copy it to the working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="ba6cb-143">If your workflow used other resources, such as a jar containing a MapReduce application, you would need to add these as well.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-143">If your workflow used other resources, such as a jar containing a MapReduce application, you would need to add these as well.</span></span>

## <a name="define-the-hive-query"></a><span data-ttu-id="ba6cb-144">Define the Hive query</span><span class="sxs-lookup"><span data-stu-id="ba6cb-144">Define the Hive query</span></span>

<span data-ttu-id="ba6cb-145">Use the following steps to create a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-145">Use the following steps to create a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="ba6cb-146">Connect to the cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-146">Connect to the cluster using SSH.</span></span> <span data-ttu-id="ba6cb-147">The following command is an example of using the `ssh` command.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-147">The following command is an example of using the `ssh` command.</span></span> <span data-ttu-id="ba6cb-148">Replace __USERNAME__ with the SSH user for the cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-148">Replace __USERNAME__ with the SSH user for the cluster.</span></span> <span data-ttu-id="ba6cb-149">Replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-149">Replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="ba6cb-150">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ba6cb-150">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ba6cb-151">From the SSH connection, use the following command to create a new file:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-151">From the SSH connection, use the following command to create a new file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="ba6cb-152">Once the nano editor opens, use the following as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-152">Once the nano editor opens, use the following as the contents of the file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="ba6cb-153">There are two variables used in the script:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-153">There are two variables used in the script:</span></span>

    * <span data-ttu-id="ba6cb-154">**${hiveTableName}**: contains the name of the table to be created</span><span class="sxs-lookup"><span data-stu-id="ba6cb-154">**${hiveTableName}**: contains the name of the table to be created</span></span>

    * <span data-ttu-id="ba6cb-155">**${hiveDataFolder}**: contains the location to store the data files for the table</span><span class="sxs-lookup"><span data-stu-id="ba6cb-155">**${hiveDataFolder}**: contains the location to store the data files for the table</span></span>

    <span data-ttu-id="ba6cb-156">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time</span><span class="sxs-lookup"><span data-stu-id="ba6cb-156">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time</span></span>

4. <span data-ttu-id="ba6cb-157">Press Ctrl-X to exit the editor.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-157">Press Ctrl-X to exit the editor.</span></span> <span data-ttu-id="ba6cb-158">When prompted, select **Y** to save the file, then use **Enter** to use the **useooziewf.hql** file name.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-158">When prompted, select **Y** to save the file, then use **Enter** to use the **useooziewf.hql** file name.</span></span>
5. <span data-ttu-id="ba6cb-159">Use the following commands to copy **useooziewf.hql** to **wasbs:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-159">Use the following commands to copy **useooziewf.hql** to **wasbs:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="ba6cb-160">These commands store the **useooziewf.hql** file on the Azure Storage account associated with this cluster, which preserves the file even if the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-160">These commands store the **useooziewf.hql** file on the Azure Storage account associated with this cluster, which preserves the file even if the cluster is deleted.</span></span> <span data-ttu-id="ba6cb-161">This allows you to save money by deleting clusters when they aren't in use, while maintaining your jobs and workflows.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-161">This allows you to save money by deleting clusters when they aren't in use, while maintaining your jobs and workflows.</span></span>

## <a name="define-the-workflow"></a><span data-ttu-id="ba6cb-162">Define the workflow</span><span class="sxs-lookup"><span data-stu-id="ba6cb-162">Define the workflow</span></span>

<span data-ttu-id="ba6cb-163">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span><span class="sxs-lookup"><span data-stu-id="ba6cb-163">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="ba6cb-164">Use the following steps to define the workflow:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-164">Use the following steps to define the workflow:</span></span>

1. <span data-ttu-id="ba6cb-165">Use the following statement to create and edit a new file:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-165">Use the following statement to create and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="ba6cb-166">Once the nano editor opens, enter the following as the file contents:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-166">Once the nano editor opens, enter the following as the file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="ba6cb-167">There are two actions defined in the workflow:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-167">There are two actions defined in the workflow:</span></span>

   * <span data-ttu-id="ba6cb-168">**RunHiveScript**: This is the start action, and runs the **useooziewf.hql** Hive script</span><span class="sxs-lookup"><span data-stu-id="ba6cb-168">**RunHiveScript**: This is the start action, and runs the **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="ba6cb-169">**RunSqoopExport**: This exports the data created from the Hive script to SQL Database using Sqoop.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-169">**RunSqoopExport**: This exports the data created from the Hive script to SQL Database using Sqoop.</span></span> <span data-ttu-id="ba6cb-170">This only runs if the **RunHiveScript** action is successful.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-170">This only runs if the **RunHiveScript** action is successful.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ba6cb-171">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span><span class="sxs-lookup"><span data-stu-id="ba6cb-171">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

     <span data-ttu-id="ba6cb-172">Note that the workflow has several entries, such as `${jobTracker}`, that is replaced by values you use in the job definition later in this document.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-172">Note that the workflow has several entries, such as `${jobTracker}`, that is replaced by values you use in the job definition later in this document.</span></span>

     <span data-ttu-id="ba6cb-173">Also note the `<archive>sqljdbc4.jar</arcive>` entry in the Sqoop section.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-173">Also note the `<archive>sqljdbc4.jar</arcive>` entry in the Sqoop section.</span></span> <span data-ttu-id="ba6cb-174">This instructs Oozie to make this archive available for Sqoop when this action runs.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-174">This instructs Oozie to make this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="ba6cb-175">Use Ctrl-X, then **Y** and **Enter** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-175">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

4. <span data-ttu-id="ba6cb-176">Use the following command to copy the **workflow.xml** file to **/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-176">Use the following command to copy the **workflow.xml** file to **/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-the-database"></a><span data-ttu-id="ba6cb-177">Create the database</span><span class="sxs-lookup"><span data-stu-id="ba6cb-177">Create the database</span></span>

<span data-ttu-id="ba6cb-178">Follow the steps in the [Create a SQL Database](../sql-database/sql-database-get-started.md) document to create a new database.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-178">Follow the steps in the [Create a SQL Database](../sql-database/sql-database-get-started.md) document to create a new database.</span></span> <span data-ttu-id="ba6cb-179">When creating the database, use **oozietest** as the database name.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-179">When creating the database, use **oozietest** as the database name.</span></span> <span data-ttu-id="ba6cb-180">Also make a note of the name used for the database server, as this is needed in the next section.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-180">Also make a note of the name used for the database server, as this is needed in the next section.</span></span>

### <a name="create-the-table"></a><span data-ttu-id="ba6cb-181">Create the table</span><span class="sxs-lookup"><span data-stu-id="ba6cb-181">Create the table</span></span>

> [!NOTE]
> <span data-ttu-id="ba6cb-182">There are many ways to connect to SQL Database to create a table.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-182">There are many ways to connect to SQL Database to create a table.</span></span> <span data-ttu-id="ba6cb-183">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-183">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="ba6cb-184">Use the following command to install FreeTDS on the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-184">Use the following command to install FreeTDS on the HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="ba6cb-185">Once FreeTDS has been installed, use the following command to connect to the SQL Database server you created previously:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-185">Once FreeTDS has been installed, use the following command to connect to the SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="ba6cb-186">You receive output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-186">You receive output similar to the following:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to oozietest
        1>

3. <span data-ttu-id="ba6cb-187">At the `1>` prompt, enter the following lines:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-187">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="ba6cb-188">When the `GO` statement is entered, the previous statements are evaluated.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-188">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="ba6cb-189">This creates a new table named **mobiledata** that is written to by Sqoop.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-189">This creates a new table named **mobiledata** that is written to by Sqoop.</span></span>

    <span data-ttu-id="ba6cb-190">Use the following to verify that the table has been created:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-190">Use the following to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="ba6cb-191">You should see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-191">You should see output similar to the following:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="ba6cb-192">Enter `exit` at the `1>` prompt to exit the tsql utility.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-192">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="create-the-job-definition"></a><span data-ttu-id="ba6cb-193">Create the job definition</span><span class="sxs-lookup"><span data-stu-id="ba6cb-193">Create the job definition</span></span>

<span data-ttu-id="ba6cb-194">The job definition describes where to find the workflow.xml, as well as other files used by the workflow (such as useooziewf.hql.) It also defines the values for properties used within the workflow and associated files.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-194">The job definition describes where to find the workflow.xml, as well as other files used by the workflow (such as useooziewf.hql.) It also defines the values for properties used within the workflow and associated files.</span></span>

1. <span data-ttu-id="ba6cb-195">Use the following command to get the full WASB address to default storage.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-195">Use the following command to get the full WASB address to default storage.</span></span> <span data-ttu-id="ba6cb-196">This is used in the configuration file in a moment:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-196">This is used in the configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="ba6cb-197">This should return information similar to the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-197">This should return information similar to the following:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasbs://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="ba6cb-198">If the HDInsight cluster uses Azure Storage as the default storage, the `<value>` element contents begin with `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-198">If the HDInsight cluster uses Azure Storage as the default storage, the `<value>` element contents begin with `wasbs://`.</span></span> <span data-ttu-id="ba6cb-199">If Azure Data Lake Store is used instead, it begins with `adl://`.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-199">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="ba6cb-200">Save the contents of the `<value>` element, as it is used in the next steps.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-200">Save the contents of the `<value>` element, as it is used in the next steps.</span></span>

2. <span data-ttu-id="ba6cb-201">Use the following command to get FQDN of the cluster headnode.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-201">Use the following command to get FQDN of the cluster headnode.</span></span> <span data-ttu-id="ba6cb-202">This is used for the JobTracker address for the cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-202">This is used for the JobTracker address for the cluster.</span></span> <span data-ttu-id="ba6cb-203">This is used in the configuration file in a moment:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-203">This is used in the configuration file in a moment:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="ba6cb-204">This returns information similar to the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-204">This returns information similar to the following:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="ba6cb-205">The port used for the JobTracker is 8050, so the full address to use for the JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-205">The port used for the JobTracker is 8050, so the full address to use for the JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="ba6cb-206">Use the following to create the Oozie job definition configuration:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-206">Use the following to create the Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="ba6cb-207">Once the nano editor opens, use the following as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-207">Once the nano editor opens, use the following as the contents of the file:</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasbs://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasbs://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasbs://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasbs://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * <span data-ttu-id="ba6cb-208">Replace all instances of **wasbs://mycontainer@mystorageaccount.blob.core.windows.net** with the value you received earlier for default storage.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-208">Replace all instances of **wasbs://mycontainer@mystorageaccount.blob.core.windows.net** with the value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="ba6cb-209">If the path is a `wasb` path, you must use the full path.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-209">If the path is a `wasb` path, you must use the full path.</span></span> <span data-ttu-id="ba6cb-210">Do not shorten it to just `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-210">Do not shorten it to just `wasb:///`.</span></span>

   * <span data-ttu-id="ba6cb-211">Replace **JOBTRACKERADDRESS** with the JobTracker/ResourceManager address you received earlier.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-211">Replace **JOBTRACKERADDRESS** with the JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="ba6cb-212">Replace **YourName** with your login name for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-212">Replace **YourName** with your login name for the HDInsight cluster.</span></span>
   * <span data-ttu-id="ba6cb-213">Replace **serverName**, **adminLogin**, and **adminPassword** with the information for your Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-213">Replace **serverName**, **adminLogin**, and **adminPassword** with the information for your Azure SQL Database.</span></span>

     <span data-ttu-id="ba6cb-214">Most of the information in this file is used to populate the values used in the workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="ba6cb-214">Most of the information in this file is used to populate the values used in the workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="ba6cb-215">The **oozie.wf.application.path** entry defines where to find the workflow.xml file, which contains the workflow ran by this job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-215">The **oozie.wf.application.path** entry defines where to find the workflow.xml file, which contains the workflow ran by this job.</span></span>

5. <span data-ttu-id="ba6cb-216">Use Ctrl-X, then **Y** and **Enter** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-216">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

## <a name="submit-and-manage-the-job"></a><span data-ttu-id="ba6cb-217">Submit and manage the job</span><span class="sxs-lookup"><span data-stu-id="ba6cb-217">Submit and manage the job</span></span>

<span data-ttu-id="ba6cb-218">The following steps use the Oozie command to submit and manage Oozie workflows on the cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-218">The following steps use the Oozie command to submit and manage Oozie workflows on the cluster.</span></span> <span data-ttu-id="ba6cb-219">The Oozie command is a friendly interface over the [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="ba6cb-219">The Oozie command is a friendly interface over the [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba6cb-220">When using the Oozie command, you must use the FQDN for the HDInsight headnode.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-220">When using the Oozie command, you must use the FQDN for the HDInsight headnode.</span></span> <span data-ttu-id="ba6cb-221">This FQDN is only accessible from the cluster, or if the cluster is on an Azure Virtual Network, from other machines on the same network.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-221">This FQDN is only accessible from the cluster, or if the cluster is on an Azure Virtual Network, from other machines on the same network.</span></span>


1. <span data-ttu-id="ba6cb-222">Use the following to obtain the URL to the Oozie service:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-222">Use the following to obtain the URL to the Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="ba6cb-223">This returns information similar to the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-223">This returns information similar to the following:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="ba6cb-224">The `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is the URL to use with the Oozie command.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-224">The `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is the URL to use with the Oozie command.</span></span>

2. <span data-ttu-id="ba6cb-225">Use the following to create an environment variable for the URL, so you don't have to type it for every command:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-225">Use the following to create an environment variable for the URL, so you don't have to type it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="ba6cb-226">Replace the URL with the one you received earlier.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-226">Replace the URL with the one you received earlier.</span></span>
3. <span data-ttu-id="ba6cb-227">Use the following to submit the job:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-227">Use the following to submit the job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="ba6cb-228">This loads the job information from **job.xml** and submits it to Oozie, but does not run it.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-228">This loads the job information from **job.xml** and submits it to Oozie, but does not run it.</span></span>

    <span data-ttu-id="ba6cb-229">Once the command completes, it should return the ID of the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-229">Once the command completes, it should return the ID of the job.</span></span> <span data-ttu-id="ba6cb-230">For example, `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-230">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="ba6cb-231">This is used to manage the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-231">This is used to manage the job.</span></span>

4. <span data-ttu-id="ba6cb-232">View the status of the job using the following command.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-232">View the status of the job using the following command.</span></span> <span data-ttu-id="ba6cb-233">Enter the job ID returned by the previous command:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-233">Enter the job ID returned by the previous command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    <span data-ttu-id="ba6cb-234">This returns information similar to the following.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-234">This returns information similar to the following.</span></span>

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasbs:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    <span data-ttu-id="ba6cb-235">This job has a status of `PREP`, which indicates that it was submitted, but has not been started yet.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-235">This job has a status of `PREP`, which indicates that it was submitted, but has not been started yet.</span></span>

5. <span data-ttu-id="ba6cb-236">Use the following to start the job:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-236">Use the following to start the job:</span></span>

    ```
    oozie job -start JOBID
    ```

    <span data-ttu-id="ba6cb-237">If you check the status after this command, it is in a running state, and information is returned for the actions within the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-237">If you check the status after this command, it is in a running state, and information is returned for the actions within the job.</span></span>

6. <span data-ttu-id="ba6cb-238">Once the task completes successfully, you can verify that the data was generated and exported to the SQL Database table by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-238">Once the task completes successfully, you can verify that the data was generated and exported to the SQL Database table by using the following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="ba6cb-239">At the `1>` prompt, enter the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-239">At the `1>` prompt, enter the following:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="ba6cb-240">The information returned is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-240">The information returned is similar to the following:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="ba6cb-241">For more information on the Oozie command, see [Oozie Command Line Tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="ba6cb-241">For more information on the Oozie command, see [Oozie Command Line Tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="ba6cb-242">Oozie REST API</span><span class="sxs-lookup"><span data-stu-id="ba6cb-242">Oozie REST API</span></span>

<span data-ttu-id="ba6cb-243">The Oozie REST API allow you to build your own tools that work with Oozie.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-243">The Oozie REST API allow you to build your own tools that work with Oozie.</span></span> <span data-ttu-id="ba6cb-244">The following are HDInsight specific information about using the Oozie REST API:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-244">The following are HDInsight specific information about using the Oozie REST API:</span></span>

* <span data-ttu-id="ba6cb-245">**URI**: The REST API can be accessed from outside the cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="ba6cb-245">**URI**: The REST API can be accessed from outside the cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="ba6cb-246">**Authentication**: You must authenticate to the API using the cluster HTTP account (admin,) and password.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-246">**Authentication**: You must authenticate to the API using the cluster HTTP account (admin,) and password.</span></span> <span data-ttu-id="ba6cb-247">For example:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-247">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="ba6cb-248">For more information on using the Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="ba6cb-248">For more information on using the Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="ba6cb-249">Oozie Web UI</span><span class="sxs-lookup"><span data-stu-id="ba6cb-249">Oozie Web UI</span></span>

<span data-ttu-id="ba6cb-250">The Oozie Web UI provides a web-based view into the status of Oozie jobs on the cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-250">The Oozie Web UI provides a web-based view into the status of Oozie jobs on the cluster.</span></span> <span data-ttu-id="ba6cb-251">It allows you to view job status, the job definition, configuration, a graph of the actions in the job, and logs for the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-251">It allows you to view job status, the job definition, configuration, a graph of the actions in the job, and logs for the job.</span></span> <span data-ttu-id="ba6cb-252">You can also view details for actions within a job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-252">You can also view details for actions within a job.</span></span>

<span data-ttu-id="ba6cb-253">To access the Oozie Web UI, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-253">To access the Oozie Web UI, use the following steps:</span></span>

1. <span data-ttu-id="ba6cb-254">Create an SSH tunnel to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-254">Create an SSH tunnel to the HDInsight cluster.</span></span> <span data-ttu-id="ba6cb-255">For information on how to do this, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UI's](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="ba6cb-255">For information on how to do this, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UI's](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

2. <span data-ttu-id="ba6cb-256">Once a tunnel has been created, open the Ambari web UI in your web browser.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-256">Once a tunnel has been created, open the Ambari web UI in your web browser.</span></span> <span data-ttu-id="ba6cb-257">The URI for the Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-257">The URI for the Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="ba6cb-258">Replace **CLUSTERNAME** with the name of your Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-258">Replace **CLUSTERNAME** with the name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="ba6cb-259">From the left side of the page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-259">From the left side of the page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![image of the menus](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="ba6cb-261">The Oozie Web UI defaults to displaying running Workflow Jobs.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-261">The Oozie Web UI defaults to displaying running Workflow Jobs.</span></span> <span data-ttu-id="ba6cb-262">To see all workflow jobs, select **All Jobs**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-262">To see all workflow jobs, select **All Jobs**.</span></span>

    ![All jobs displayed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="ba6cb-264">Select a job to view more information about the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-264">Select a job to view more information about the job.</span></span>

    ![Job info](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="ba6cb-266">From the Job Info tab, you can see basic job information, as well as the individual actions within the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-266">From the Job Info tab, you can see basic job information, as well as the individual actions within the job.</span></span> <span data-ttu-id="ba6cb-267">Using the tabs at the top you can view the Job Definition, Job Configuration, access the Job Log or view a Directed Acyclic Graph (DAG) of the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-267">Using the tabs at the top you can view the Job Definition, Job Configuration, access the Job Log or view a Directed Acyclic Graph (DAG) of the job.</span></span>

   * <span data-ttu-id="ba6cb-268">**Job Log**: Select the **GetLogs** button to get all logs for the job, or use the **Enter Search Filter** field to filter logs</span><span class="sxs-lookup"><span data-stu-id="ba6cb-268">**Job Log**: Select the **GetLogs** button to get all logs for the job, or use the **Enter Search Filter** field to filter logs</span></span>

       ![Job log](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="ba6cb-270">**JobDAG**: The DAG is a graphical overview of the data paths taken through the workflow</span><span class="sxs-lookup"><span data-stu-id="ba6cb-270">**JobDAG**: The DAG is a graphical overview of the data paths taken through the workflow</span></span>

       ![Job DAG](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="ba6cb-272">Selecting one of the actions from the **Job Info** tab brings up information for the action.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-272">Selecting one of the actions from the **Job Info** tab brings up information for the action.</span></span> <span data-ttu-id="ba6cb-273">For example, select the **RunHiveScript** action.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-273">For example, select the **RunHiveScript** action.</span></span>

    ![Action info](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="ba6cb-275">You can see details for the action, including a link to the **Console URL**, which can be used to view JobTracker information for the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-275">You can see details for the action, including a link to the **Console URL**, which can be used to view JobTracker information for the job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="ba6cb-276">Scheduling jobs</span><span class="sxs-lookup"><span data-stu-id="ba6cb-276">Scheduling jobs</span></span>

<span data-ttu-id="ba6cb-277">The coordinator allows you to specify a start, end, and occurrance frequency for jobs so that they can be scheduled for certain times.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-277">The coordinator allows you to specify a start, end, and occurrance frequency for jobs so that they can be scheduled for certain times.</span></span>

<span data-ttu-id="ba6cb-278">To define a schedule for the workflow, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-278">To define a schedule for the workflow, use the following steps:</span></span>

1. <span data-ttu-id="ba6cb-279">Use the following to create a new file named **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-279">Use the following to create a new file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="ba6cb-280">Use the following as the contents of the file:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-280">Use the following as the contents of the file:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="ba6cb-281">Note the `${...}` variables; these are replaced by values in the job definition at run-time.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-281">Note the `${...}` variables; these are replaced by values in the job definition at run-time.</span></span> <span data-ttu-id="ba6cb-282">The variables are:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-282">The variables are:</span></span>

   * <span data-ttu-id="ba6cb-283">**${coordFrequency}**: Time between running instances of the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-283">**${coordFrequency}**: Time between running instances of the job.</span></span>

   * <span data-ttu-id="ba6cb-284">**${coordStart}**: The job start time.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-284">**${coordStart}**: The job start time.</span></span>

   * <span data-ttu-id="ba6cb-285">**${coordEnd}**: The job end time.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-285">**${coordEnd}**: The job end time.</span></span>

   * <span data-ttu-id="ba6cb-286">**${coordTimezone}**: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span><span class="sxs-lookup"><span data-stu-id="ba6cb-286">**${coordTimezone}**: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="ba6cb-287">This time zone is referred as the "Oozie processing timezone".</span><span class="sxs-lookup"><span data-stu-id="ba6cb-287">This time zone is referred as the "Oozie processing timezone".</span></span>

   * <span data-ttu-id="ba6cb-288">**${wfPath}**: The path to the workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-288">**${wfPath}**: The path to the workflow.xml.</span></span>

2. <span data-ttu-id="ba6cb-289">Use Ctrl-X, then **Y** and **Enter** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-289">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

3. <span data-ttu-id="ba6cb-290">Use the following command to copy the file to the working directory for this job:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-290">Use the following command to copy the file to the working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="ba6cb-291">Use the following to modify the **job.xml** file:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-291">Use the following to modify the **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="ba6cb-292">Make the following changes:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-292">Make the following changes:</span></span>

   * <span data-ttu-id="ba6cb-293">Change `<name>oozie.wf.application.path</name>` to `<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-293">Change `<name>oozie.wf.application.path</name>` to `<name>oozie.coord.application.path</name>`.</span></span> <span data-ttu-id="ba6cb-294">This instructs Oozie to run the coordinator file instead of the workflow file.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-294">This instructs Oozie to run the coordinator file instead of the workflow file.</span></span>

   * <span data-ttu-id="ba6cb-295">Add the following, which sets a variable used in the coordinator.xml to point to the location of the workflow.xml:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-295">Add the following, which sets a variable used in the coordinator.xml to point to the location of the workflow.xml:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasbs://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="ba6cb-296">Replace the `wasbs://mycontainer@mystorageaccount.blob.core.windows` text with the value used in other entries in the job.xml file.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-296">Replace the `wasbs://mycontainer@mystorageaccount.blob.core.windows` text with the value used in other entries in the job.xml file.</span></span>

   * <span data-ttu-id="ba6cb-297">Add the following, which define the start, end, and frequency to use for the coordinator.xml file:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-297">Add the following, which define the start, end, and frequency to use for the coordinator.xml file:</span></span>

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-02-07T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-02-09T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       <span data-ttu-id="ba6cb-298">These set the start time to 12:00PM on February 7th, 2017, the end time to February 9th, 2017, and the interval for running this job daily.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-298">These set the start time to 12:00PM on February 7th, 2017, the end time to February 9th, 2017, and the interval for running this job daily.</span></span> <span data-ttu-id="ba6cb-299">The frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-299">The frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="ba6cb-300">Finally, the timezone is set to UTC.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-300">Finally, the timezone is set to UTC.</span></span>

5. <span data-ttu-id="ba6cb-301">Use Ctrl-X, then **Y** and **Enter** to save the file.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-301">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

6. <span data-ttu-id="ba6cb-302">To run the job, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-302">To run the job, use the following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="ba6cb-303">This submits and starts the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-303">This submits and starts the job.</span></span>

7. <span data-ttu-id="ba6cb-304">If you visit the Oozie Web UI and select the **Coordinator Jobs** tab, you see information similar to the following:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-304">If you visit the Oozie Web UI and select the **Coordinator Jobs** tab, you see information similar to the following:</span></span>

    ![coordinator jobs tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="ba6cb-306">Note the **Next Materialization** entry; this is when the job runs next.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-306">Note the **Next Materialization** entry; this is when the job runs next.</span></span>

8. <span data-ttu-id="ba6cb-307">Similar to the earlier workflow job, selecting the job entry in the web UI displays information on the job:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-307">Similar to the earlier workflow job, selecting the job entry in the web UI displays information on the job:</span></span>

    ![Coordinator job info](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    <span data-ttu-id="ba6cb-309">Note that this only shows successful runs of the job, not individual actions within the scheduled workflow.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-309">Note that this only shows successful runs of the job, not individual actions within the scheduled workflow.</span></span> <span data-ttu-id="ba6cb-310">To see that, select one of the **Action** entries.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-310">To see that, select one of the **Action** entries.</span></span> <span data-ttu-id="ba6cb-311">This displays information similar to that retrieved for the earlier workflow job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-311">This displays information similar to that retrieved for the earlier workflow job.</span></span>

    ![Action info](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="ba6cb-313">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="ba6cb-313">Troubleshooting</span></span>

<span data-ttu-id="ba6cb-314">When troubleshooting problems with Oozie jobs, the Oozie UI is very helpful as it allows you to easily view both Oozie logs, as well as links to JobTracker logs for MapReduce tasks such as Hive queries.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-314">When troubleshooting problems with Oozie jobs, the Oozie UI is very helpful as it allows you to easily view both Oozie logs, as well as links to JobTracker logs for MapReduce tasks such as Hive queries.</span></span> <span data-ttu-id="ba6cb-315">In general, the pattern for troubleshooting should be:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-315">In general, the pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="ba6cb-316">View the job in Oozie Web UI.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-316">View the job in Oozie Web UI.</span></span>

2. <span data-ttu-id="ba6cb-317">If there is an error or failure for a specific action, select the action to see if the **Error Message** field provides more information on the failure.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-317">If there is an error or failure for a specific action, select the action to see if the **Error Message** field provides more information on the failure.</span></span>

3. <span data-ttu-id="ba6cb-318">If available, use the URL from the action to view more details (such as JobTracker logs,) for the action.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-318">If available, use the URL from the action to view more details (such as JobTracker logs,) for the action.</span></span>

<span data-ttu-id="ba6cb-319">The following are specific errors you may encounter, and how to resolve them.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-319">The following are specific errors you may encounter, and how to resolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="ba6cb-320">JA009: Cannot initialize cluster</span><span class="sxs-lookup"><span data-stu-id="ba6cb-320">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="ba6cb-321">**Symptoms**: The job status changes to **SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-321">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="ba6cb-322">Details for the job shows the RunHiveScript status as **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-322">Details for the job shows the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="ba6cb-323">Selecting the action displays the following error message:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-323">Selecting the action displays the following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="ba6cb-324">**Cause**: The WASB addresses used in the **job.xml** file do not contain the storage container or storage account name.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-324">**Cause**: The WASB addresses used in the **job.xml** file do not contain the storage container or storage account name.</span></span> <span data-ttu-id="ba6cb-325">The WASB address format must be `wasbs://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-325">The WASB address format must be `wasbs://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="ba6cb-326">**Resolution**: Change the WASB addresses used by the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-326">**Resolution**: Change the WASB addresses used by the job.</span></span>

### <a name="ja002-oozie-is-not-allowed-to-impersonate-ltuser"></a><span data-ttu-id="ba6cb-327">JA002: Oozie is not allowed to impersonate &lt;USER></span><span class="sxs-lookup"><span data-stu-id="ba6cb-327">JA002: Oozie is not allowed to impersonate &lt;USER></span></span>

<span data-ttu-id="ba6cb-328">**Symptoms**: The job status changes to **SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-328">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="ba6cb-329">Details for the job shows the RunHiveScript status as **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-329">Details for the job shows the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="ba6cb-330">Selecting the action shows the following error message:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-330">Selecting the action shows the following error message:</span></span>

    JA002: User: oozie is not allowed to impersonate <USER>

<span data-ttu-id="ba6cb-331">**Cause**: Current permission settings do not allow Oozie to impersonate the specified user account.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-331">**Cause**: Current permission settings do not allow Oozie to impersonate the specified user account.</span></span>

<span data-ttu-id="ba6cb-332">**Resolution**: Oozie is allowed to impersonate users in the **users** group.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-332">**Resolution**: Oozie is allowed to impersonate users in the **users** group.</span></span> <span data-ttu-id="ba6cb-333">Use the `groups USERNAME` to see the groups that the user account is a member of.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-333">Use the `groups USERNAME` to see the groups that the user account is a member of.</span></span> <span data-ttu-id="ba6cb-334">If the user is not a member of the **users** group, use the following command to add the user to the group:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-334">If the user is not a member of the **users** group, use the following command to add the user to the group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="ba6cb-335">It may take several minutes before HDInsight recognizes that the user has been added to the group.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-335">It may take several minutes before HDInsight recognizes that the user has been added to the group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="ba6cb-336">Launcher ERROR (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="ba6cb-336">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="ba6cb-337">**Symptoms**: The job status changes to **KILLED**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-337">**Symptoms**: The job status changes to **KILLED**.</span></span> <span data-ttu-id="ba6cb-338">Details for the job shows the RunSqoopExport status as **ERROR**.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-338">Details for the job shows the RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="ba6cb-339">Selecting the action shows the following error message:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-339">Selecting the action shows the following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="ba6cb-340">**Cause**: Sqoop is unable to load the database driver required to access the database.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-340">**Cause**: Sqoop is unable to load the database driver required to access the database.</span></span>

<span data-ttu-id="ba6cb-341">**Resolution**: When using Sqoop from an Oozie job, you must include the database driver with the other resources (such as the workflow.xml,) used by the job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-341">**Resolution**: When using Sqoop from an Oozie job, you must include the database driver with the other resources (such as the workflow.xml,) used by the job.</span></span>

<span data-ttu-id="ba6cb-342">You must also reference the archive containing the database driver from the `<sqoop>...</sqoop>` section of the workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-342">You must also reference the archive containing the database driver from the `<sqoop>...</sqoop>` section of the workflow.xml.</span></span>

<span data-ttu-id="ba6cb-343">For example, for the job in this document, you would use the following steps:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-343">For example, for the job in this document, you would use the following steps:</span></span>

1. <span data-ttu-id="ba6cb-344">Copy the sqljdbc4.1.jar file to the /tutorials/useoozie directory:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-344">Copy the sqljdbc4.1.jar file to the /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="ba6cb-345">Modify the workflow.xml to add the following on a new line above `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-345">Modify the workflow.xml to add the following on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="ba6cb-346">Next steps</span><span class="sxs-lookup"><span data-stu-id="ba6cb-346">Next steps</span></span>

<span data-ttu-id="ba6cb-347">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job.</span><span class="sxs-lookup"><span data-stu-id="ba6cb-347">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job.</span></span> <span data-ttu-id="ba6cb-348">To learn more about working with HDInsight, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="ba6cb-348">To learn more about working with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="ba6cb-349">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="ba6cb-349">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="ba6cb-350">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ba6cb-350">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ba6cb-351">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="ba6cb-351">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="ba6cb-352">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="ba6cb-352">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="ba6cb-353">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ba6cb-353">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="ba6cb-354">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="ba6cb-354">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]: storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx












