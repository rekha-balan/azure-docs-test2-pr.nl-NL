---
title: Use time-based Hadoop Oozie coordinator in HDInsight
description: Use time-based Hadoop Oozie coordinator in HDInsight, a big data service. Learn how to define Oozie workflows and coordinators, and submit jobs.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.author: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 10/04/2017
ROBOTS: NOINDEX
ms.openlocfilehash: 783857b9ca1d3e3a5aef13c24f9a3633533a2050
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793629"
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-to-define-workflows-and-coordinate-jobs"></a><span data-ttu-id="1d322-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span><span class="sxs-lookup"><span data-stu-id="1d322-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span></span>
<span data-ttu-id="1d322-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span><span class="sxs-lookup"><span data-stu-id="1d322-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span></span> <span data-ttu-id="1d322-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span><span class="sxs-lookup"><span data-stu-id="1d322-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="1d322-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1d322-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="1d322-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/transform-data.md).</span><span class="sxs-lookup"><span data-stu-id="1d322-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/transform-data.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1d322-109">This article requires a Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1d322-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="1d322-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="1d322-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="1d322-111">What is Oozie</span><span class="sxs-lookup"><span data-stu-id="1d322-111">What is Oozie</span></span>
<span data-ttu-id="1d322-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="1d322-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="1d322-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="1d322-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="1d322-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span><span class="sxs-lookup"><span data-stu-id="1d322-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="1d322-115">The following image shows the workflow you will implement:</span><span class="sxs-lookup"><span data-stu-id="1d322-115">The following image shows the workflow you will implement:</span></span>

![Workflow diagram][img-workflow-diagram]

<span data-ttu-id="1d322-117">The workflow contains two actions:</span><span class="sxs-lookup"><span data-stu-id="1d322-117">The workflow contains two actions:</span></span>

1. <span data-ttu-id="1d322-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span><span class="sxs-lookup"><span data-stu-id="1d322-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="1d322-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span><span class="sxs-lookup"><span data-stu-id="1d322-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="1d322-120">The Hive script output is similar to:</span><span class="sxs-lookup"><span data-stu-id="1d322-120">The Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="1d322-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="1d322-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="1d322-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="1d322-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span></span> <span data-ttu-id="1d322-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="1d322-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="1d322-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="1d322-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="1d322-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1d322-125">Prerequisites</span></span>
<span data-ttu-id="1d322-126">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="1d322-126">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="1d322-127">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1d322-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1d322-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="1d322-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="1d322-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d322-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="1d322-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d322-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="1d322-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="1d322-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="1d322-132">**An HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="1d322-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="1d322-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="1d322-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="1d322-134">You will need the following data to go through the tutorial:</span><span class="sxs-lookup"><span data-stu-id="1d322-134">You will need the following data to go through the tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="1d322-135">Cluster property</span><span class="sxs-lookup"><span data-stu-id="1d322-135">Cluster property</span></span></th><th><span data-ttu-id="1d322-136">Windows PowerShell variable name</span><span class="sxs-lookup"><span data-stu-id="1d322-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="1d322-137">Value</span><span class="sxs-lookup"><span data-stu-id="1d322-137">Value</span></span></th><th><span data-ttu-id="1d322-138">Description</span><span class="sxs-lookup"><span data-stu-id="1d322-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="1d322-139">HDInsight cluster name</span><span class="sxs-lookup"><span data-stu-id="1d322-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="1d322-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="1d322-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="1d322-141">The HDInsight cluster on which you will run this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d322-141">The HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-142">HDInsight cluster username</span><span class="sxs-lookup"><span data-stu-id="1d322-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="1d322-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="1d322-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="1d322-144">The HDInsight cluster user name.</span><span class="sxs-lookup"><span data-stu-id="1d322-144">The HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="1d322-145">HDInsight cluster user password</span><span class="sxs-lookup"><span data-stu-id="1d322-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="1d322-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="1d322-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="1d322-147">The HDInsight cluster user password.</span><span class="sxs-lookup"><span data-stu-id="1d322-147">The HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-148">Azure storage account name</span><span class="sxs-lookup"><span data-stu-id="1d322-148">Azure storage account name</span></span></td><td><span data-ttu-id="1d322-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="1d322-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="1d322-150">An Azure Storage account available to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1d322-150">An Azure Storage account available to the HDInsight cluster.</span></span> <span data-ttu-id="1d322-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span><span class="sxs-lookup"><span data-stu-id="1d322-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-152">Azure Blob container name</span><span class="sxs-lookup"><span data-stu-id="1d322-152">Azure Blob container name</span></span></td><td><span data-ttu-id="1d322-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="1d322-153">$containerName</span></span></td><td></td><td><span data-ttu-id="1d322-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span><span class="sxs-lookup"><span data-stu-id="1d322-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span></span> <span data-ttu-id="1d322-155">By default, it has the same name as the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1d322-155">By default, it has the same name as the HDInsight cluster.</span></span></td></tr>
    </table>

* <span data-ttu-id="1d322-156">**An Azure SQL database**.</span><span class="sxs-lookup"><span data-stu-id="1d322-156">**An Azure SQL database**.</span></span> <span data-ttu-id="1d322-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span><span class="sxs-lookup"><span data-stu-id="1d322-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span></span> <span data-ttu-id="1d322-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="1d322-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="1d322-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d322-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="1d322-160">SQL database property</span><span class="sxs-lookup"><span data-stu-id="1d322-160">SQL database property</span></span></th><th><span data-ttu-id="1d322-161">Windows PowerShell variable name</span><span class="sxs-lookup"><span data-stu-id="1d322-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="1d322-162">Value</span><span class="sxs-lookup"><span data-stu-id="1d322-162">Value</span></span></th><th><span data-ttu-id="1d322-163">Description</span><span class="sxs-lookup"><span data-stu-id="1d322-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="1d322-164">SQL database server name</span><span class="sxs-lookup"><span data-stu-id="1d322-164">SQL database server name</span></span></td><td><span data-ttu-id="1d322-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="1d322-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="1d322-166">The SQL database server to which Sqoop will export data.</span><span class="sxs-lookup"><span data-stu-id="1d322-166">The SQL database server to which Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="1d322-167">SQL database login name</span><span class="sxs-lookup"><span data-stu-id="1d322-167">SQL database login name</span></span></td><td><span data-ttu-id="1d322-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="1d322-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="1d322-169">SQL Database login name.</span><span class="sxs-lookup"><span data-stu-id="1d322-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-170">SQL database login password</span><span class="sxs-lookup"><span data-stu-id="1d322-170">SQL database login password</span></span></td><td><span data-ttu-id="1d322-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="1d322-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="1d322-172">SQL Database login password.</span><span class="sxs-lookup"><span data-stu-id="1d322-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-173">SQL database name</span><span class="sxs-lookup"><span data-stu-id="1d322-173">SQL database name</span></span></td><td><span data-ttu-id="1d322-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="1d322-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="1d322-175">The Azure SQL database to which Sqoop will export data.</span><span class="sxs-lookup"><span data-stu-id="1d322-175">The Azure SQL database to which Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="1d322-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1d322-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="1d322-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1d322-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span></span> <span data-ttu-id="1d322-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="1d322-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="1d322-179">Fill-in the values in the tables.</span><span class="sxs-lookup"><span data-stu-id="1d322-179">Fill-in the values in the tables.</span></span> <span data-ttu-id="1d322-180">It will be helpful for going through this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d322-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="1d322-181">Define Oozie workflow and the related HiveQL script</span><span class="sxs-lookup"><span data-stu-id="1d322-181">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="1d322-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span><span class="sxs-lookup"><span data-stu-id="1d322-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="1d322-183">The default workflow file name is *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="1d322-183">The default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="1d322-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d322-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="1d322-185">The Hive action in the workflow calls a HiveQL script file.</span><span class="sxs-lookup"><span data-stu-id="1d322-185">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="1d322-186">This script file contains three HiveQL statements:</span><span class="sxs-lookup"><span data-stu-id="1d322-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="1d322-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span><span class="sxs-lookup"><span data-stu-id="1d322-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="1d322-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span><span class="sxs-lookup"><span data-stu-id="1d322-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span></span>
3. <span data-ttu-id="1d322-189">**The location of the log4j log file**.</span><span class="sxs-lookup"><span data-stu-id="1d322-189">**The location of the log4j log file**.</span></span> <span data-ttu-id="1d322-190">The field delimiter is ",".</span><span class="sxs-lookup"><span data-stu-id="1d322-190">The field delimiter is ",".</span></span> <span data-ttu-id="1d322-191">The default line delimiter is "\n".</span><span class="sxs-lookup"><span data-stu-id="1d322-191">The default line delimiter is "\n".</span></span> <span data-ttu-id="1d322-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span><span class="sxs-lookup"><span data-stu-id="1d322-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="1d322-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span><span class="sxs-lookup"><span data-stu-id="1d322-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="1d322-194">There is a known Hive path issue.</span><span class="sxs-lookup"><span data-stu-id="1d322-194">There is a known Hive path issue.</span></span> <span data-ttu-id="1d322-195">You will run into this problem when submitting an Oozie job.</span><span class="sxs-lookup"><span data-stu-id="1d322-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="1d322-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="1d322-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span></span>

<span data-ttu-id="1d322-197">**To define the HiveQL script file to be called by the workflow**</span><span class="sxs-lookup"><span data-stu-id="1d322-197">**To define the HiveQL script file to be called by the workflow**</span></span>

1. <span data-ttu-id="1d322-198">Create a text file with the following content:</span><span class="sxs-lookup"><span data-stu-id="1d322-198">Create a text file with the following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="1d322-199">There are three variables used in the script:</span><span class="sxs-lookup"><span data-stu-id="1d322-199">There are three variables used in the script:</span></span>

   * <span data-ttu-id="1d322-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="1d322-200">${hiveTableName}</span></span>
   * <span data-ttu-id="1d322-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="1d322-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="1d322-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="1d322-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="1d322-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span><span class="sxs-lookup"><span data-stu-id="1d322-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span></span>
2. <span data-ttu-id="1d322-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span><span class="sxs-lookup"><span data-stu-id="1d322-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="1d322-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d322-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span></span>

<span data-ttu-id="1d322-206">**To define a workflow**</span><span class="sxs-lookup"><span data-stu-id="1d322-206">**To define a workflow**</span></span>

1. <span data-ttu-id="1d322-207">Create a text file with the following content:</span><span class="sxs-lookup"><span data-stu-id="1d322-207">Create a text file with the following content:</span></span>

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
    ```

    <span data-ttu-id="1d322-208">There are two actions defined in the workflow.</span><span class="sxs-lookup"><span data-stu-id="1d322-208">There are two actions defined in the workflow.</span></span> <span data-ttu-id="1d322-209">The start-to action is *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="1d322-209">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="1d322-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="1d322-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="1d322-211">The RunHiveScript has several variables.</span><span class="sxs-lookup"><span data-stu-id="1d322-211">The RunHiveScript has several variables.</span></span> <span data-ttu-id="1d322-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d322-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="1d322-213">Workflow variables</span><span class="sxs-lookup"><span data-stu-id="1d322-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="1d322-214">Workflow variables</span><span class="sxs-lookup"><span data-stu-id="1d322-214">Workflow variables</span></span></th><th><span data-ttu-id="1d322-215">Description</span><span class="sxs-lookup"><span data-stu-id="1d322-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="1d322-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="1d322-216">${jobTracker}</span></span></td><td><span data-ttu-id="1d322-217">Specify the URL of the Hadoop job tracker.</span><span class="sxs-lookup"><span data-stu-id="1d322-217">Specify the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="1d322-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span><span class="sxs-lookup"><span data-stu-id="1d322-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="1d322-219">${nameNode}</span></span></td><td><span data-ttu-id="1d322-220">Specify the URL of the Hadoop name node.</span><span class="sxs-lookup"><span data-stu-id="1d322-220">Specify the URL of the Hadoop name node.</span></span> <span data-ttu-id="1d322-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="1d322-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="1d322-222">${queueName}</span></span></td><td><span data-ttu-id="1d322-223">Specifies the queue name that the job will be submitted to.</span><span class="sxs-lookup"><span data-stu-id="1d322-223">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="1d322-224">Use <strong>default</strong>.</span><span class="sxs-lookup"><span data-stu-id="1d322-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="1d322-225">Hive action variables</span><span class="sxs-lookup"><span data-stu-id="1d322-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="1d322-226">Hive action variable</span><span class="sxs-lookup"><span data-stu-id="1d322-226">Hive action variable</span></span></th><th><span data-ttu-id="1d322-227">Description</span><span class="sxs-lookup"><span data-stu-id="1d322-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="1d322-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="1d322-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="1d322-229">The source directory for the Hive Create Table command.</span><span class="sxs-lookup"><span data-stu-id="1d322-229">The source directory for the Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="1d322-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="1d322-231">The output folder for the INSERT OVERWRITE statement.</span><span class="sxs-lookup"><span data-stu-id="1d322-231">The output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="1d322-232">${hiveTableName}</span></span></td><td><span data-ttu-id="1d322-233">The name of the Hive table that references the log4j data files.</span><span class="sxs-lookup"><span data-stu-id="1d322-233">The name of the Hive table that references the log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="1d322-234">Sqoop action variables</span><span class="sxs-lookup"><span data-stu-id="1d322-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="1d322-235">Sqoop action variable</span><span class="sxs-lookup"><span data-stu-id="1d322-235">Sqoop action variable</span></span></th><th><span data-ttu-id="1d322-236">Description</span><span class="sxs-lookup"><span data-stu-id="1d322-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="1d322-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="1d322-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="1d322-238">SQL Database connection string.</span><span class="sxs-lookup"><span data-stu-id="1d322-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="1d322-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="1d322-240">The Azure SQL database table to where the data will be exported.</span><span class="sxs-lookup"><span data-stu-id="1d322-240">The Azure SQL database table to where the data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="1d322-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="1d322-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="1d322-242">The output folder for the Hive INSERT OVERWRITE statement.</span><span class="sxs-lookup"><span data-stu-id="1d322-242">The output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="1d322-243">This is the same folder for the Sqoop export (export-dir).</span><span class="sxs-lookup"><span data-stu-id="1d322-243">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="1d322-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span><span class="sxs-lookup"><span data-stu-id="1d322-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="1d322-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span><span class="sxs-lookup"><span data-stu-id="1d322-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="1d322-246">(Use Notepad if your text editor doesn't provide this option.)</span><span class="sxs-lookup"><span data-stu-id="1d322-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="1d322-247">**To define coordinator**</span><span class="sxs-lookup"><span data-stu-id="1d322-247">**To define coordinator**</span></span>

1. <span data-ttu-id="1d322-248">Create a text file with the following content:</span><span class="sxs-lookup"><span data-stu-id="1d322-248">Create a text file with the following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="1d322-249">There are five variables used in the definition file:</span><span class="sxs-lookup"><span data-stu-id="1d322-249">There are five variables used in the definition file:</span></span>

   | <span data-ttu-id="1d322-250">Variable</span><span class="sxs-lookup"><span data-stu-id="1d322-250">Variable</span></span> | <span data-ttu-id="1d322-251">Description</span><span class="sxs-lookup"><span data-stu-id="1d322-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="1d322-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="1d322-252">${coordFrequency}</span></span> |<span data-ttu-id="1d322-253">Job pause time.</span><span class="sxs-lookup"><span data-stu-id="1d322-253">Job pause time.</span></span> <span data-ttu-id="1d322-254">Frequency is always expressed in minutes.</span><span class="sxs-lookup"><span data-stu-id="1d322-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="1d322-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="1d322-255">${coordStart}</span></span> |<span data-ttu-id="1d322-256">Job start time.</span><span class="sxs-lookup"><span data-stu-id="1d322-256">Job start time.</span></span> |
   | <span data-ttu-id="1d322-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="1d322-257">${coordEnd}</span></span> |<span data-ttu-id="1d322-258">Job end time.</span><span class="sxs-lookup"><span data-stu-id="1d322-258">Job end time.</span></span> |
   | <span data-ttu-id="1d322-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="1d322-259">${coordTimezone}</span></span> |<span data-ttu-id="1d322-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span><span class="sxs-lookup"><span data-stu-id="1d322-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="1d322-261">This time zone is referred as the "Oozie processing timezone."</span><span class="sxs-lookup"><span data-stu-id="1d322-261">This time zone is referred as the "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="1d322-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="1d322-262">${wfPath}</span></span> |<span data-ttu-id="1d322-263">The path for the workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="1d322-263">The path for the workflow.xml.</span></span>  <span data-ttu-id="1d322-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span><span class="sxs-lookup"><span data-stu-id="1d322-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="1d322-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span><span class="sxs-lookup"><span data-stu-id="1d322-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span></span> <span data-ttu-id="1d322-266">(Use Notepad if your text editor doesn't provide this option.)</span><span class="sxs-lookup"><span data-stu-id="1d322-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-the-oozie-project-and-prepare-the-tutorial"></a><span data-ttu-id="1d322-267">Deploy the Oozie project and prepare the tutorial</span><span class="sxs-lookup"><span data-stu-id="1d322-267">Deploy the Oozie project and prepare the tutorial</span></span>
<span data-ttu-id="1d322-268">You will run an Azure PowerShell script to perform the following:</span><span class="sxs-lookup"><span data-stu-id="1d322-268">You will run an Azure PowerShell script to perform the following:</span></span>

* <span data-ttu-id="1d322-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="1d322-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="1d322-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="1d322-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="1d322-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="1d322-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="1d322-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="1d322-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="1d322-273">Create an Azure SQL database table for storing Sqoop export data.</span><span class="sxs-lookup"><span data-stu-id="1d322-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="1d322-274">The table name is *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="1d322-274">The table name is *log4jLogCount*.</span></span>

<span data-ttu-id="1d322-275">**Understand HDInsight storage**</span><span class="sxs-lookup"><span data-stu-id="1d322-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="1d322-276">HDInsight uses Azure Blob storage for data storage.</span><span class="sxs-lookup"><span data-stu-id="1d322-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="1d322-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="1d322-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="1d322-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="1d322-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="1d322-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span><span class="sxs-lookup"><span data-stu-id="1d322-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span></span> <span data-ttu-id="1d322-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="1d322-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span></span> <span data-ttu-id="1d322-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="1d322-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="1d322-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="1d322-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="1d322-283">By default, this container has the same name as the HDInsight cluster name.</span><span class="sxs-lookup"><span data-stu-id="1d322-283">By default, this container has the same name as the HDInsight cluster name.</span></span>
<span data-ttu-id="1d322-284">The syntax is:</span><span class="sxs-lookup"><span data-stu-id="1d322-284">The syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="1d322-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span><span class="sxs-lookup"><span data-stu-id="1d322-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="1d322-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span><span class="sxs-lookup"><span data-stu-id="1d322-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="1d322-287">The wasb:// path is a virtual path.</span><span class="sxs-lookup"><span data-stu-id="1d322-287">The wasb:// path is a virtual path.</span></span> <span data-ttu-id="1d322-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="1d322-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="1d322-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span><span class="sxs-lookup"><span data-stu-id="1d322-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="1d322-290">If you want to access the file directly from the storage account, the blob name for the file is:</span><span class="sxs-lookup"><span data-stu-id="1d322-290">If you want to access the file directly from the storage account, the blob name for the file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="1d322-291">**Understand Hive internal and external tables**</span><span class="sxs-lookup"><span data-stu-id="1d322-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="1d322-292">There are a few things you need to know about Hive internal and external tables:</span><span class="sxs-lookup"><span data-stu-id="1d322-292">There are a few things you need to know about Hive internal and external tables:</span></span>

* <span data-ttu-id="1d322-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span><span class="sxs-lookup"><span data-stu-id="1d322-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="1d322-294">The data file must be located in the default container.</span><span class="sxs-lookup"><span data-stu-id="1d322-294">The data file must be located in the default container.</span></span>
* <span data-ttu-id="1d322-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span><span class="sxs-lookup"><span data-stu-id="1d322-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span></span>
* <span data-ttu-id="1d322-296">The CREATE EXTERNAL TABLE command creates an external table.</span><span class="sxs-lookup"><span data-stu-id="1d322-296">The CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="1d322-297">The data file can be located outside the default container.</span><span class="sxs-lookup"><span data-stu-id="1d322-297">The data file can be located outside the default container.</span></span>
* <span data-ttu-id="1d322-298">The CREATE EXTERNAL TABLE command does not move the data file.</span><span class="sxs-lookup"><span data-stu-id="1d322-298">The CREATE EXTERNAL TABLE command does not move the data file.</span></span>
* <span data-ttu-id="1d322-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span><span class="sxs-lookup"><span data-stu-id="1d322-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span></span> <span data-ttu-id="1d322-300">This is the reason why the tutorial makes a copy of the sample.log file.</span><span class="sxs-lookup"><span data-stu-id="1d322-300">This is the reason why the tutorial makes a copy of the sample.log file.</span></span>

<span data-ttu-id="1d322-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="1d322-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="1d322-302">**To prepare the tutorial**</span><span class="sxs-lookup"><span data-stu-id="1d322-302">**To prepare the tutorial**</span></span>

1. <span data-ttu-id="1d322-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="1d322-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="1d322-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="1d322-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="1d322-305">In the bottom pane, run the following command to connect to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="1d322-305">In the bottom pane, run the following command to connect to your Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="1d322-306">You will be prompted to enter your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="1d322-306">You will be prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="1d322-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span><span class="sxs-lookup"><span data-stu-id="1d322-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1d322-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span><span class="sxs-lookup"><span data-stu-id="1d322-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span></span>

3. <span data-ttu-id="1d322-309">Copy the following script into the script pane, and then set the first six variables:</span><span class="sxs-lookup"><span data-stu-id="1d322-309">Copy the following script into the script pane, and then set the first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for the tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here
    ```

    <span data-ttu-id="1d322-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d322-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="1d322-311">Append the following to the script in the script pane:</span><span class="sxs-lookup"><span data-stu-id="1d322-311">Append the following to the script in the script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create the log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log to example/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="1d322-312">Click **Run Script** or press **F5** to run the script.</span><span class="sxs-lookup"><span data-stu-id="1d322-312">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="1d322-313">The output will be similar to:</span><span class="sxs-lookup"><span data-stu-id="1d322-313">The output will be similar to:</span></span>

    ![Tutorial preparation output][img-preparation-output]

## <a name="run-the-oozie-project"></a><span data-ttu-id="1d322-315">Run the Oozie project</span><span class="sxs-lookup"><span data-stu-id="1d322-315">Run the Oozie project</span></span>
<span data-ttu-id="1d322-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span><span class="sxs-lookup"><span data-stu-id="1d322-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="1d322-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span><span class="sxs-lookup"><span data-stu-id="1d322-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="1d322-318">The Oozie web services API is a HTTP REST JSON API.</span><span class="sxs-lookup"><span data-stu-id="1d322-318">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="1d322-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span><span class="sxs-lookup"><span data-stu-id="1d322-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="1d322-320">**To submit an Oozie job**</span><span class="sxs-lookup"><span data-stu-id="1d322-320">**To submit an Oozie job**</span></span>

1. <span data-ttu-id="1d322-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="1d322-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="1d322-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="1d322-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="1d322-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="1d322-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"  
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="1d322-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d322-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="1d322-325">$coordstart and $coordend are the workflow starting and ending time.</span><span class="sxs-lookup"><span data-stu-id="1d322-325">$coordstart and $coordend are the workflow starting and ending time.</span></span> <span data-ttu-id="1d322-326">To find out the UTC/GMT time, search "utc time" on bing.com.</span><span class="sxs-lookup"><span data-stu-id="1d322-326">To find out the UTC/GMT time, search "utc time" on bing.com.</span></span> <span data-ttu-id="1d322-327">The $coordFrequency is how often in minutes you want to run the workflow.</span><span class="sxs-lookup"><span data-stu-id="1d322-327">The $coordFrequency is how often in minutes you want to run the workflow.</span></span>
3. <span data-ttu-id="1d322-328">Append the following to the script.</span><span class="sxs-lookup"><span data-stu-id="1d322-328">Append the following to the script.</span></span> <span data-ttu-id="1d322-329">This part defines the Oozie payload:</span><span class="sxs-lookup"><span data-stu-id="1d322-329">This part defines the Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
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
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
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
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="1d322-330">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="1d322-330">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="1d322-331">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span><span class="sxs-lookup"><span data-stu-id="1d322-331">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="1d322-332">Append the following to the script.</span><span class="sxs-lookup"><span data-stu-id="1d322-332">Append the following to the script.</span></span> <span data-ttu-id="1d322-333">This part checks the Oozie web service status:</span><span class="sxs-lookup"><span data-stu-id="1d322-333">This part checks the Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check the server status and re-run the job."
        }
    }
    ```

5. <span data-ttu-id="1d322-334">Append the following to the script.</span><span class="sxs-lookup"><span data-stu-id="1d322-334">Append the following to the script.</span></span> <span data-ttu-id="1d322-335">This part creates an Oozie job:</span><span class="sxs-lookup"><span data-stu-id="1d322-335">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="1d322-336">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span><span class="sxs-lookup"><span data-stu-id="1d322-336">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span></span> <span data-ttu-id="1d322-337">In this case, the coordinator job is triggered by time.</span><span class="sxs-lookup"><span data-stu-id="1d322-337">In this case, the coordinator job is triggered by time.</span></span> <span data-ttu-id="1d322-338">The job will start automatically.</span><span class="sxs-lookup"><span data-stu-id="1d322-338">The job will start automatically.</span></span>

6. <span data-ttu-id="1d322-339">Append the following to the script.</span><span class="sxs-lookup"><span data-stu-id="1d322-339">Append the following to the script.</span></span> <span data-ttu-id="1d322-340">This part checks the Oozie job status:</span><span class="sxs-lookup"><span data-stu-id="1d322-340">This part checks the Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
        }
    }
    ```

7. <span data-ttu-id="1d322-341">(Optional) Append the following to the script.</span><span class="sxs-lookup"><span data-stu-id="1d322-341">(Optional) Append the following to the script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing the Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for the 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="1d322-342">Append the following to the script:</span><span class="sxs-lookup"><span data-stu-id="1d322-342">Append the following to the script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

<span data-ttu-id="1d322-343">Remove the # signs if you want to run the additional functions.</span><span class="sxs-lookup"><span data-stu-id="1d322-343">Remove the # signs if you want to run the additional functions.</span></span>

9. <span data-ttu-id="1d322-344">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span><span class="sxs-lookup"><span data-stu-id="1d322-344">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="1d322-345">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span><span class="sxs-lookup"><span data-stu-id="1d322-345">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span></span>
10. <span data-ttu-id="1d322-346">Click **Run Script** or press **F5** to run the script.</span><span class="sxs-lookup"><span data-stu-id="1d322-346">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="1d322-347">The output will be similar to:</span><span class="sxs-lookup"><span data-stu-id="1d322-347">The output will be similar to:</span></span>

     ![Tutorial run workflow output][img-runworkflow-output]
11. <span data-ttu-id="1d322-349">Connect to your SQL Database to see the exported data.</span><span class="sxs-lookup"><span data-stu-id="1d322-349">Connect to your SQL Database to see the exported data.</span></span>

<span data-ttu-id="1d322-350">**To check the job error log**</span><span class="sxs-lookup"><span data-stu-id="1d322-350">**To check the job error log**</span></span>

<span data-ttu-id="1d322-351">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span><span class="sxs-lookup"><span data-stu-id="1d322-351">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span></span> <span data-ttu-id="1d322-352">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="1d322-352">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="1d322-353">**To rerun the tutorial**</span><span class="sxs-lookup"><span data-stu-id="1d322-353">**To rerun the tutorial**</span></span>

<span data-ttu-id="1d322-354">To rerun the workflow, you must perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="1d322-354">To rerun the workflow, you must perform the following tasks:</span></span>

* <span data-ttu-id="1d322-355">Delete the Hive script output file.</span><span class="sxs-lookup"><span data-stu-id="1d322-355">Delete the Hive script output file.</span></span>
* <span data-ttu-id="1d322-356">Delete the data in the log4jLogsCount table.</span><span class="sxs-lookup"><span data-stu-id="1d322-356">Delete the data in the log4jLogsCount table.</span></span>

<span data-ttu-id="1d322-357">Here is a sample Windows PowerShell script that you can use:</span><span class="sxs-lookup"><span data-stu-id="1d322-357">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete the Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="1d322-358">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d322-358">Next steps</span></span>
<span data-ttu-id="1d322-359">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d322-359">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="1d322-360">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="1d322-360">To learn more, see the following articles:</span></span>

* <span data-ttu-id="1d322-361">[Get started with HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="1d322-361">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="1d322-362">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="1d322-362">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="1d322-363">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="1d322-363">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="1d322-364">[Upload data to HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="1d322-364">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="1d322-365">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="1d322-365">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="1d322-366">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1d322-366">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="1d322-367">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1d322-367">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="1d322-368">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="1d322-368">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]:hadoop/apache-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]:hadoop/hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]:hadoop/hdinsight-use-hive.md
[hdinsight-use-pig]:hadoop/hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]:hadoop/apache-hadoop-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: https://docs.microsoft.com/en-us/powershell/scripting/setup/starting-windows-powershell?view=powershell-6
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
