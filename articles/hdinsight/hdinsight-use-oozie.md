---
title: Use Hadoop Oozie in HDInsight | Microsoft Docs
description: Use Hadoop Oozie in HDInsight, a big data service. Learn how to define an Oozie workflow, and submit an Oozie job.
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 82ba8cf60eaeeddb40d40ee230cc29cd78bf52d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551733"
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="eaba2-104">Use Oozie with Hadoop to define and run a workflow in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eaba2-104">Use Oozie with Hadoop to define and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="eaba2-105">Learn how to use Apache Oozie to define a workflow and run the workflow on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eaba2-105">Learn how to use Apache Oozie to define a workflow and run the workflow on HDInsight.</span></span> <span data-ttu-id="eaba2-106">To learn about the Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span><span class="sxs-lookup"><span data-stu-id="eaba2-106">To learn about the Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="eaba2-107">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="eaba2-107">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="eaba2-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="eaba2-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="eaba2-109">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="eaba2-109">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="eaba2-110">It can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts.</span><span class="sxs-lookup"><span data-stu-id="eaba2-110">It can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="eaba2-111">The workflow you will implement by following the instructions in this tutorial contains two actions:</span><span class="sxs-lookup"><span data-stu-id="eaba2-111">The workflow you will implement by following the instructions in this tutorial contains two actions:</span></span>

![Workflow diagram][img-workflow-diagram]

1. <span data-ttu-id="eaba2-113">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j file.</span><span class="sxs-lookup"><span data-stu-id="eaba2-113">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="eaba2-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows the type and the severity, for example:</span><span class="sxs-lookup"><span data-stu-id="eaba2-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows the type and the severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="eaba2-115">The Hive script output is similar to:</span><span class="sxs-lookup"><span data-stu-id="eaba2-115">The Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="eaba2-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="eaba2-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="eaba2-117">A Sqoop action exports the HiveQL output to a table in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="eaba2-117">A Sqoop action exports the HiveQL output to a table in an Azure SQL database.</span></span> <span data-ttu-id="eaba2-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="eaba2-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="eaba2-119">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="eaba2-119">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="eaba2-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eaba2-120">Prerequisites</span></span>
<span data-ttu-id="eaba2-121">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="eaba2-121">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="eaba2-122">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="eaba2-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="eaba2-123">Define Oozie workflow and the related HiveQL script</span><span class="sxs-lookup"><span data-stu-id="eaba2-123">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="eaba2-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span><span class="sxs-lookup"><span data-stu-id="eaba2-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="eaba2-125">The default workflow file name is *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="eaba2-125">The default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="eaba2-126">The following is the workflow file you will use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="eaba2-126">The following is the workflow file you will use in this tutorial.</span></span>

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
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
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
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>

<span data-ttu-id="eaba2-127">There are two actions defined in the workflow.</span><span class="sxs-lookup"><span data-stu-id="eaba2-127">There are two actions defined in the workflow.</span></span> <span data-ttu-id="eaba2-128">The start-to action is *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="eaba2-128">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="eaba2-129">If the action runs successfully, the next action is *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="eaba2-129">If the action runs successfully, the next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="eaba2-130">The RunHiveScript has several variables.</span><span class="sxs-lookup"><span data-stu-id="eaba2-130">The RunHiveScript has several variables.</span></span> <span data-ttu-id="eaba2-131">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eaba2-131">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="eaba2-132">Workflow variables</span><span class="sxs-lookup"><span data-stu-id="eaba2-132">Workflow variables</span></span></th><th><span data-ttu-id="eaba2-133">Description</span><span class="sxs-lookup"><span data-stu-id="eaba2-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="eaba2-134">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="eaba2-134">${jobTracker}</span></span></td><td><span data-ttu-id="eaba2-135">Specifies the URL of the Hadoop job tracker.</span><span class="sxs-lookup"><span data-stu-id="eaba2-135">Specifies the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="eaba2-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span><span class="sxs-lookup"><span data-stu-id="eaba2-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="eaba2-137">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="eaba2-137">${nameNode}</span></span></td><td><span data-ttu-id="eaba2-138">Specifies the URL of the Hadoop name node.</span><span class="sxs-lookup"><span data-stu-id="eaba2-138">Specifies the URL of the Hadoop name node.</span></span> <span data-ttu-id="eaba2-139">Use the default file system address, for example, <i>wasbs://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="eaba2-139">Use the default file system address, for example, <i>wasbs://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="eaba2-140">${queueName}</span><span class="sxs-lookup"><span data-stu-id="eaba2-140">${queueName}</span></span></td><td><span data-ttu-id="eaba2-141">Specifies the queue name that the job will be submitted to.</span><span class="sxs-lookup"><span data-stu-id="eaba2-141">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="eaba2-142">Use the <strong>default</strong>.</span><span class="sxs-lookup"><span data-stu-id="eaba2-142">Use the <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="eaba2-143">Hive action variable</span><span class="sxs-lookup"><span data-stu-id="eaba2-143">Hive action variable</span></span></th><th><span data-ttu-id="eaba2-144">Description</span><span class="sxs-lookup"><span data-stu-id="eaba2-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="eaba2-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="eaba2-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="eaba2-146">Specifies the source directory for the Hive Create Table command.</span><span class="sxs-lookup"><span data-stu-id="eaba2-146">Specifies the source directory for the Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="eaba2-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="eaba2-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="eaba2-148">Specifies the output folder for the INSERT OVERWRITE statement.</span><span class="sxs-lookup"><span data-stu-id="eaba2-148">Specifies the output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="eaba2-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="eaba2-149">${hiveTableName}</span></span></td><td><span data-ttu-id="eaba2-150">Specifies the name of the Hive table that references the log4j data files.</span><span class="sxs-lookup"><span data-stu-id="eaba2-150">Specifies the name of the Hive table that references the log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="eaba2-151">Sqoop action variable</span><span class="sxs-lookup"><span data-stu-id="eaba2-151">Sqoop action variable</span></span></th><th><span data-ttu-id="eaba2-152">Description</span><span class="sxs-lookup"><span data-stu-id="eaba2-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="eaba2-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="eaba2-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="eaba2-154">Specifies the Azure SQL database connection string.</span><span class="sxs-lookup"><span data-stu-id="eaba2-154">Specifies the Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="eaba2-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="eaba2-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="eaba2-156">Specifies the Azure SQL database table where the data will be exported to.</span><span class="sxs-lookup"><span data-stu-id="eaba2-156">Specifies the Azure SQL database table where the data will be exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="eaba2-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="eaba2-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="eaba2-158">Specifies the output folder for the Hive INSERT OVERWRITE statement.</span><span class="sxs-lookup"><span data-stu-id="eaba2-158">Specifies the output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="eaba2-159">This is the same folder for the Sqoop export (export-dir).</span><span class="sxs-lookup"><span data-stu-id="eaba2-159">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="eaba2-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span><span class="sxs-lookup"><span data-stu-id="eaba2-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="eaba2-161">The Hive action in the workflow calls a HiveQL script file.</span><span class="sxs-lookup"><span data-stu-id="eaba2-161">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="eaba2-162">This script file contains three HiveQL statements:</span><span class="sxs-lookup"><span data-stu-id="eaba2-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="eaba2-163">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span><span class="sxs-lookup"><span data-stu-id="eaba2-163">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="eaba2-164">**The CREATE TABLE statement** creates a log4j Hive external table that points to the location of the log4j log file.</span><span class="sxs-lookup"><span data-stu-id="eaba2-164">**The CREATE TABLE statement** creates a log4j Hive external table that points to the location of the log4j log file.</span></span> <span data-ttu-id="eaba2-165">The field delimiter is ",".</span><span class="sxs-lookup"><span data-stu-id="eaba2-165">The field delimiter is ",".</span></span> <span data-ttu-id="eaba2-166">The default line delimiter is "\n".</span><span class="sxs-lookup"><span data-stu-id="eaba2-166">The default line delimiter is "\n".</span></span> <span data-ttu-id="eaba2-167">A Hive external table is used to avoid the data file being removed from the original location if you want to run the Oozie workflow multiple times.</span><span class="sxs-lookup"><span data-stu-id="eaba2-167">A Hive external table is used to avoid the data file being removed from the original location if you want to run the Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="eaba2-168">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and saves the output to a blob in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="eaba2-168">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and saves the output to a blob in Azure Storage.</span></span>

<span data-ttu-id="eaba2-169">There are three variables used in the script:</span><span class="sxs-lookup"><span data-stu-id="eaba2-169">There are three variables used in the script:</span></span>

* <span data-ttu-id="eaba2-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="eaba2-170">${hiveTableName}</span></span>
* <span data-ttu-id="eaba2-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="eaba2-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="eaba2-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="eaba2-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="eaba2-173">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time.</span><span class="sxs-lookup"><span data-stu-id="eaba2-173">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time.</span></span>

<span data-ttu-id="eaba2-174">Both the workflow file and the HiveQL file are stored in a blob container.</span><span class="sxs-lookup"><span data-stu-id="eaba2-174">Both the workflow file and the HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="eaba2-175">The PowerShell script you will use later in this tutorial will copy both files to the default Storage account.</span><span class="sxs-lookup"><span data-stu-id="eaba2-175">The PowerShell script you will use later in this tutorial will copy both files to the default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="eaba2-176">Submit Oozie jobs using PowerShell</span><span class="sxs-lookup"><span data-stu-id="eaba2-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="eaba2-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span><span class="sxs-lookup"><span data-stu-id="eaba2-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="eaba2-178">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span><span class="sxs-lookup"><span data-stu-id="eaba2-178">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="eaba2-179">The Oozie web services API is a HTTP REST JSON API.</span><span class="sxs-lookup"><span data-stu-id="eaba2-179">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="eaba2-180">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span><span class="sxs-lookup"><span data-stu-id="eaba2-180">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="eaba2-181">The PowerShell script in this section performs the following steps:</span><span class="sxs-lookup"><span data-stu-id="eaba2-181">The PowerShell script in this section performs the following steps:</span></span>

1. <span data-ttu-id="eaba2-182">Connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="eaba2-182">Connect to Azure.</span></span>
2. <span data-ttu-id="eaba2-183">Create an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="eaba2-183">Create an Azure resource group.</span></span> <span data-ttu-id="eaba2-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="eaba2-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="eaba2-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span><span class="sxs-lookup"><span data-stu-id="eaba2-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="eaba2-186">These are used by the Sqoop action in the workflow.</span><span class="sxs-lookup"><span data-stu-id="eaba2-186">These are used by the Sqoop action in the workflow.</span></span>
   
    <span data-ttu-id="eaba2-187">The table name is *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="eaba2-187">The table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="eaba2-188">Create an HDInsight cluster used to run Oozie jobs.</span><span class="sxs-lookup"><span data-stu-id="eaba2-188">Create an HDInsight cluster used to run Oozie jobs.</span></span>
   
    <span data-ttu-id="eaba2-189">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eaba2-189">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="eaba2-190">Copy the oozie workflow file and the HiveQL script file to the default file system.</span><span class="sxs-lookup"><span data-stu-id="eaba2-190">Copy the oozie workflow file and the HiveQL script file to the default file system.</span></span>
   
    <span data-ttu-id="eaba2-191">Both files are stored in a public Blob container.</span><span class="sxs-lookup"><span data-stu-id="eaba2-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="eaba2-192">Copy the HiveQL script (useoozie.hql) to Azure Storage (wasbs:///tutorials/useoozie/useoozie.hql).</span><span class="sxs-lookup"><span data-stu-id="eaba2-192">Copy the HiveQL script (useoozie.hql) to Azure Storage (wasbs:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="eaba2-193">Copy workflow.xml to wasbs:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="eaba2-193">Copy workflow.xml to wasbs:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="eaba2-194">Copy the data file (/example/data/sample.log) to wasbs:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="eaba2-194">Copy the data file (/example/data/sample.log) to wasbs:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="eaba2-195">Submit an Oozie job.</span><span class="sxs-lookup"><span data-stu-id="eaba2-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="eaba2-196">To examine the OOzie job results, use Visual Studio or other tools to connect to the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="eaba2-196">To examine the OOzie job results, use Visual Studio or other tools to connect to the Azure SQL Database.</span></span>

<span data-ttu-id="eaba2-197">Here is the script.</span><span class="sxs-lookup"><span data-stu-id="eaba2-197">Here is the script.</span></span>  <span data-ttu-id="eaba2-198">You can run the script from Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="eaba2-198">You can run the script from Windows PowerShell ISE.</span></span> <span data-ttu-id="eaba2-199">You only need to configure the first 7 variables.</span><span class="sxs-lookup"><span data-stu-id="eaba2-199">You only need to configure the first 7 variables.</span></span>

    #region - provide the following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # The default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating the log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate the copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy the sample.log file

    Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate the copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasbs://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

    <property>
        <name>nameNode</name>
        <value>$storageUrI</value>
    </property>

    <property>
        <name>jobTracker</name>
        <value>jobtrackerhost:9010</value>
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
        <value>$hiveScript</value>
    </property>

    <property>
        <name>hiveTableName</name>
        <value>$hiveTableName</value>
    </property>

    <property>
        <name>hiveDataFolder</name>
        <value>$hiveDataFolder</value>
    </property>

    <property>
        <name>hiveOutputFolder</name>
        <value>$hiveOutputFolder</value>
    </property>

    <property>
        <name>sqlDatabaseConnectionString</name>
        <value>&quot;$sqlDatabaseConnectionString&quot;</value>
    </property>

    <property>
        <name>sqlDatabaseTableName</name>
        <value>$SQLDatabaseTableName</value>
    </property>

    <property>
        <name>user.name</name>
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting the Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="eaba2-200">**To re-run the tutorial**</span><span class="sxs-lookup"><span data-stu-id="eaba2-200">**To re-run the tutorial**</span></span>

<span data-ttu-id="eaba2-201">To re-run the workflow, you must delete the following:</span><span class="sxs-lookup"><span data-stu-id="eaba2-201">To re-run the workflow, you must delete the following:</span></span>

* <span data-ttu-id="eaba2-202">The Hive script output file</span><span class="sxs-lookup"><span data-stu-id="eaba2-202">The Hive script output file</span></span>
* <span data-ttu-id="eaba2-203">The data in the log4jLogsCount table</span><span class="sxs-lookup"><span data-stu-id="eaba2-203">The data in the log4jLogsCount table</span></span>

<span data-ttu-id="eaba2-204">Here is a sample PowerShell script that you can use:</span><span class="sxs-lookup"><span data-stu-id="eaba2-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete the Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="eaba2-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="eaba2-205">Next steps</span></span>
<span data-ttu-id="eaba2-206">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eaba2-206">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job by using PowerShell.</span></span> <span data-ttu-id="eaba2-207">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="eaba2-207">To learn more, see the following articles:</span></span>

* <span data-ttu-id="eaba2-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="eaba2-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="eaba2-209">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="eaba2-209">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="eaba2-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="eaba2-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="eaba2-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="eaba2-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="eaba2-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="eaba2-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="eaba2-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="eaba2-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="eaba2-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="eaba2-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="eaba2-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="eaba2-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="eaba2-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="eaba2-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]: ../storage-create-storage-account.md

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



