---
title: Learn what is Hive and how to use HiveQL | Microsoft Docs
description: Learn about Apache Hive and how to use it with Hadoop in HDInsight. Choose how to run your Hive job, and use HiveQL to analyze a sample Apache log4j file.
keywords: hiveql,what is hive
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: db324cc8269a1f23613e5193f5a1dec1d26a62b1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550461"
---
# <a name="use-hive-and-hiveql-with-hadoop-in-hdinsight"></a><span data-ttu-id="9e5eb-105">Use Hive and HiveQL with Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e5eb-105">Use Hive and HiveQL with Hadoop in HDInsight</span></span>

<span data-ttu-id="9e5eb-106">Learn how to use Hive with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-106">Learn how to use Hive with HDInsight.</span></span> <span data-ttu-id="9e5eb-107">Use the following table to discover the various ways that Hive can be used with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-107">Use the following table to discover the various ways that Hive can be used with HDInsight:</span></span>

| <span data-ttu-id="9e5eb-108">**Use this** if you want...</span><span class="sxs-lookup"><span data-stu-id="9e5eb-108">**Use this** if you want...</span></span> | <span data-ttu-id="9e5eb-109">...an **interactive** shell</span><span class="sxs-lookup"><span data-stu-id="9e5eb-109">...an **interactive** shell</span></span> | <span data-ttu-id="9e5eb-110">...**batch** processing</span><span class="sxs-lookup"><span data-stu-id="9e5eb-110">...**batch** processing</span></span> | <span data-ttu-id="9e5eb-111">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="9e5eb-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="9e5eb-112">...from this **client operating system**</span><span class="sxs-lookup"><span data-stu-id="9e5eb-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="9e5eb-113">Hive View</span><span class="sxs-lookup"><span data-stu-id="9e5eb-113">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="9e5eb-114">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-114">✔</span></span> |<span data-ttu-id="9e5eb-115">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-115">✔</span></span> |<span data-ttu-id="9e5eb-116">Linux</span><span class="sxs-lookup"><span data-stu-id="9e5eb-116">Linux</span></span> |<span data-ttu-id="9e5eb-117">Any (browser based)</span><span class="sxs-lookup"><span data-stu-id="9e5eb-117">Any (browser based)</span></span> |
| [<span data-ttu-id="9e5eb-118">Beeline command</span><span class="sxs-lookup"><span data-stu-id="9e5eb-118">Beeline command</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="9e5eb-119">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-119">✔</span></span> |<span data-ttu-id="9e5eb-120">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-120">✔</span></span> |<span data-ttu-id="9e5eb-121">Linux</span><span class="sxs-lookup"><span data-stu-id="9e5eb-121">Linux</span></span> |<span data-ttu-id="9e5eb-122">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-122">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="9e5eb-123">REST API</span><span class="sxs-lookup"><span data-stu-id="9e5eb-123">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="9e5eb-124">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-124">✔</span></span> |<span data-ttu-id="9e5eb-125">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-125">Linux or Windows</span></span> |<span data-ttu-id="9e5eb-126">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-126">Linux, Unix, Mac OS X, or Windows</span></span> |
| <span data-ttu-id="9e5eb-127">[Query console](hdinsight-hadoop-use-hive-query-console.md) (HDInsight 3.2 and 3.3)</span><span class="sxs-lookup"><span data-stu-id="9e5eb-127">[Query console](hdinsight-hadoop-use-hive-query-console.md) (HDInsight 3.2 and 3.3)</span></span> |&nbsp; |<span data-ttu-id="9e5eb-128">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-128">✔</span></span> |<span data-ttu-id="9e5eb-129">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-129">Windows</span></span> |<span data-ttu-id="9e5eb-130">Any (browser based)</span><span class="sxs-lookup"><span data-stu-id="9e5eb-130">Any (browser based)</span></span> |
| [<span data-ttu-id="9e5eb-131">HDInsight tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e5eb-131">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="9e5eb-132">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-132">✔</span></span> |<span data-ttu-id="9e5eb-133">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-133">Linux or Windows</span></span> |<span data-ttu-id="9e5eb-134">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-134">Windows</span></span> |
| [<span data-ttu-id="9e5eb-135">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e5eb-135">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="9e5eb-136">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-136">✔</span></span> |<span data-ttu-id="9e5eb-137">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-137">Linux or Windows</span></span> |<span data-ttu-id="9e5eb-138">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-138">Windows</span></span> |
| <span data-ttu-id="9e5eb-139">[Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) (HDInsight 3.2 and 3.3)</span><span class="sxs-lookup"><span data-stu-id="9e5eb-139">[Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="9e5eb-140">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-140">✔</span></span> |<span data-ttu-id="9e5eb-141">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-141">✔</span></span> |<span data-ttu-id="9e5eb-142">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-142">Windows</span></span> |<span data-ttu-id="9e5eb-143">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-143">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="9e5eb-144">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-144">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9e5eb-145">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="9e5eb-145">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a id="why"></a><span data-ttu-id="9e5eb-146">What is Hive</span><span class="sxs-lookup"><span data-stu-id="9e5eb-146">What is Hive</span></span>

<span data-ttu-id="9e5eb-147">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop, which enables data summarization, querying, and analysis of data.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-147">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop, which enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="9e5eb-148">Hive allows you to project structure on largely unstructured data.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-148">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="9e5eb-149">After you define the structure, you can use Hive to query that data without knowledge of Java or MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-149">After you define the structure, you can use Hive to query that data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="9e5eb-150">Hive queries are written in HiveQL, which is a query language similar to SQL.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-150">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span> <span data-ttu-id="9e5eb-151">Hive can be used to interactively explore your data or to create reusable batch processing jobs.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-151">Hive can be used to interactively explore your data or to create reusable batch processing jobs.</span></span>

<span data-ttu-id="9e5eb-152">Hive understands how to work with structured and semi-structured data, such as text files where the fields are delimited by specific characters.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-152">Hive understands how to work with structured and semi-structured data, such as text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="9e5eb-153">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-153">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="9e5eb-154">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-154">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="9e5eb-155">User-defined functions (UDF)</span><span class="sxs-lookup"><span data-stu-id="9e5eb-155">User-defined functions (UDF)</span></span>

<span data-ttu-id="9e5eb-156">Hive can also be extended through **user-defined functions (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-156">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="9e5eb-157">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-157">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="9e5eb-158">For an example of using UDFs with Hive, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-158">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="9e5eb-159">Use a Java user-defined Function with Hive</span><span class="sxs-lookup"><span data-stu-id="9e5eb-159">Use a Java user-defined Function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="9e5eb-160">Using Python with Hive and Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e5eb-160">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)

* [<span data-ttu-id="9e5eb-161">Use C# with Hive and Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e5eb-161">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="9e5eb-162">How to add a custom Hive UDF to HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e5eb-162">How to add a custom Hive UDF to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="9e5eb-163">Custom Hive UDF example to convert date/time formats to Hive timestamp</span><span class="sxs-lookup"><span data-stu-id="9e5eb-163">Custom Hive UDF example to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="9e5eb-164">Hive internal tables vs external tables</span><span class="sxs-lookup"><span data-stu-id="9e5eb-164">Hive internal tables vs external tables</span></span>

<span data-ttu-id="9e5eb-165">There are a few things you need to know about the Hive internal table and external table:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-165">There are a few things you need to know about the Hive internal table and external table:</span></span>

* <span data-ttu-id="9e5eb-166">The **CREATE TABLE** command creates an internal table.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-166">The **CREATE TABLE** command creates an internal table.</span></span> <span data-ttu-id="9e5eb-167">The data file must be located in the default container.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-167">The data file must be located in the default container.</span></span>

* <span data-ttu-id="9e5eb-168">The **CREATE TABLE** command moves the data file to the `/hive/warehouse/<TableName>` directory on default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-168">The **CREATE TABLE** command moves the data file to the `/hive/warehouse/<TableName>` directory on default storage for the cluster.</span></span>

* <span data-ttu-id="9e5eb-169">The **CREATE EXTERNAL TABLE** command creates an external table.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-169">The **CREATE EXTERNAL TABLE** command creates an external table.</span></span> <span data-ttu-id="9e5eb-170">The data file can be located outside the default container.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-170">The data file can be located outside the default container.</span></span>

* <span data-ttu-id="9e5eb-171">The **CREATE EXTERNAL TABLE** command does not move the data file.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-171">The **CREATE EXTERNAL TABLE** command does not move the data file.</span></span>

<span data-ttu-id="9e5eb-172">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="9e5eb-172">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

## <a id="data"></a><span data-ttu-id="9e5eb-173">Example data</span><span class="sxs-lookup"><span data-stu-id="9e5eb-173">Example data</span></span>

<span data-ttu-id="9e5eb-174">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-174">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="9e5eb-175">These directories exist in the default storage for your cluster.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-175">These directories exist in the default storage for your cluster.</span></span> <span data-ttu-id="9e5eb-176">This document uses the `/example/data/sample.log` file.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-176">This document uses the `/example/data/sample.log` file.</span></span> <span data-ttu-id="9e5eb-177">This file is a *log4j* file.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-177">This file is a *log4j* file.</span></span> <span data-ttu-id="9e5eb-178">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-178">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="9e5eb-179">In the previous example, the log level is ERROR.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-179">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="9e5eb-180">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to the blob container.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-180">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to the blob container.</span></span> <span data-ttu-id="9e5eb-181">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-181">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="9e5eb-182">For more information about how Azure Blob storage is used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9e5eb-182">For more information about how Azure Blob storage is used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <a id="job"></a><span data-ttu-id="9e5eb-183">Sample Hive query</span><span class="sxs-lookup"><span data-stu-id="9e5eb-183">Sample Hive query</span></span>

<span data-ttu-id="9e5eb-184">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-184">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="9e5eb-185">In the previous example, the HiveQL statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-185">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="9e5eb-186">**set hive.execution.engine=tez;**: Sets the execution engine to use Tez.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-186">**set hive.execution.engine=tez;**: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="9e5eb-187">Using Tez instead of MapReduce can provide an increase in query performance.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-187">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="9e5eb-188">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-188">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9e5eb-189">This statement is only required when using a Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-189">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="9e5eb-190">Tez is the default execution engine for Linux-based HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-190">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="9e5eb-191">**DROP TABLE**: If the table already exists, delete it.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-191">**DROP TABLE**: If the table already exists, delete it.</span></span>

* <span data-ttu-id="9e5eb-192">**CREATE EXTERNAL TABLE**: Creates a new **external** table in Hive.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-192">**CREATE EXTERNAL TABLE**: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="9e5eb-193">External tables only store the table definition in Hive.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-193">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="9e5eb-194">The data is left in the original location and in the original format.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-194">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="9e5eb-195">**ROW FORMAT**: Tells Hive how the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-195">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="9e5eb-196">In this case, the fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-196">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="9e5eb-197">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-197">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="9e5eb-198">The data can be in one file or spread across multiple files within the directory.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-198">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="9e5eb-199">**SELECT**: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-199">**SELECT**: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="9e5eb-200">This statement returns a value of **3** because there are three rows that contain this value.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-200">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="9e5eb-201">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-201">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="9e5eb-202">This statement restricts the search to the `sample.log` file that contains the data.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-202">This statement restricts the search to the `sample.log` file that contains the data.</span></span>

> [!NOTE]
> <span data-ttu-id="9e5eb-203">External tables should be used when you expect the underlying data to be updated by an external source.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-203">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="9e5eb-204">For example, an automated data upload process, or MapReduce operation.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-204">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="9e5eb-205">Dropping an external table does **not** delete the data, it only deletes the table definition.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-205">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="9e5eb-206">To create an **internal** table instead of external, use the following HiveQL:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-206">To create an **internal** table instead of external, use the following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="9e5eb-207">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-207">These statements perform the following actions:</span></span>

* <span data-ttu-id="9e5eb-208">**CREATE TABLE IF NOT EXISTS**: If the table does not exist, create it.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-208">**CREATE TABLE IF NOT EXISTS**: If the table does not exist, create it.</span></span> <span data-ttu-id="9e5eb-209">Because the **EXTERNAL** keyword is not used, this statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-209">Because the **EXTERNAL** keyword is not used, this statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="9e5eb-210">**STORED AS ORC**: Stores the data in Optimized Row Columnar (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-210">**STORED AS ORC**: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="9e5eb-211">This is a highly optimized and efficient format for storing Hive data.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-211">This is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="9e5eb-212">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-212">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="9e5eb-213">Unlike external tables, dropping an internal table also deletes the underlying data.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-213">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a id="usetez"></a><span data-ttu-id="9e5eb-214">Use Apache Tez for improved performance</span><span class="sxs-lookup"><span data-stu-id="9e5eb-214">Use Apache Tez for improved performance</span></span>

<span data-ttu-id="9e5eb-215">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-215">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="9e5eb-216">In the latest release of HDInsight, Hive supports running on Tez.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-216">In the latest release of HDInsight, Hive supports running on Tez.</span></span> <span data-ttu-id="9e5eb-217">Tez is enabled by default for Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-217">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="9e5eb-218">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-218">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="9e5eb-219">To take advantage of Tez, the following value must be set for a Hive query:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-219">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="9e5eb-220">Tez is the default engine for Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-220">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="9e5eb-221">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-221">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="9e5eb-222">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span><span class="sxs-lookup"><span data-stu-id="9e5eb-222">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="9e5eb-223">Use the Ambari Tez view on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e5eb-223">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="9e5eb-224">Use the Tez UI on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e5eb-224">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

## <a id="run"></a><span data-ttu-id="9e5eb-225">How to run the HiveQL job</span><span class="sxs-lookup"><span data-stu-id="9e5eb-225">How to run the HiveQL job</span></span>

<span data-ttu-id="9e5eb-226">HDInsight can run HiveQL jobs using various methods.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-226">HDInsight can run HiveQL jobs using various methods.</span></span> <span data-ttu-id="9e5eb-227">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-227">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="9e5eb-228">**Use this** if you want...</span><span class="sxs-lookup"><span data-stu-id="9e5eb-228">**Use this** if you want...</span></span> | <span data-ttu-id="9e5eb-229">...an **interactive** shell</span><span class="sxs-lookup"><span data-stu-id="9e5eb-229">...an **interactive** shell</span></span> | <span data-ttu-id="9e5eb-230">...**batch** processing</span><span class="sxs-lookup"><span data-stu-id="9e5eb-230">...**batch** processing</span></span> | <span data-ttu-id="9e5eb-231">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="9e5eb-231">...with this **cluster operating system**</span></span> | <span data-ttu-id="9e5eb-232">...from this **client operating system**</span><span class="sxs-lookup"><span data-stu-id="9e5eb-232">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="9e5eb-233">Hive View</span><span class="sxs-lookup"><span data-stu-id="9e5eb-233">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="9e5eb-234">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-234">✔</span></span> |<span data-ttu-id="9e5eb-235">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-235">✔</span></span> |<span data-ttu-id="9e5eb-236">Linux</span><span class="sxs-lookup"><span data-stu-id="9e5eb-236">Linux</span></span> |<span data-ttu-id="9e5eb-237">Any (browser based)</span><span class="sxs-lookup"><span data-stu-id="9e5eb-237">Any (browser based)</span></span> |
| [<span data-ttu-id="9e5eb-238">Beeline command</span><span class="sxs-lookup"><span data-stu-id="9e5eb-238">Beeline command</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="9e5eb-239">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-239">✔</span></span> |<span data-ttu-id="9e5eb-240">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-240">✔</span></span> |<span data-ttu-id="9e5eb-241">Linux</span><span class="sxs-lookup"><span data-stu-id="9e5eb-241">Linux</span></span> |<span data-ttu-id="9e5eb-242">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-242">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="9e5eb-243">REST API</span><span class="sxs-lookup"><span data-stu-id="9e5eb-243">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="9e5eb-244">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-244">✔</span></span> |<span data-ttu-id="9e5eb-245">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-245">Linux or Windows</span></span> |<span data-ttu-id="9e5eb-246">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-246">Linux, Unix, Mac OS X, or Windows</span></span> |
| <span data-ttu-id="9e5eb-247">[Query console](hdinsight-hadoop-use-hive-query-console.md) (HDInsight 3.2 and 3.3)</span><span class="sxs-lookup"><span data-stu-id="9e5eb-247">[Query console](hdinsight-hadoop-use-hive-query-console.md) (HDInsight 3.2 and 3.3)</span></span> |&nbsp; |<span data-ttu-id="9e5eb-248">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-248">✔</span></span> |<span data-ttu-id="9e5eb-249">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-249">Windows</span></span> |<span data-ttu-id="9e5eb-250">Any (browser based)</span><span class="sxs-lookup"><span data-stu-id="9e5eb-250">Any (browser based)</span></span> |
| [<span data-ttu-id="9e5eb-251">HDInsight tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e5eb-251">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="9e5eb-252">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-252">✔</span></span> |<span data-ttu-id="9e5eb-253">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-253">Linux or Windows</span></span> |<span data-ttu-id="9e5eb-254">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-254">Windows</span></span> |
| [<span data-ttu-id="9e5eb-255">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e5eb-255">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="9e5eb-256">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-256">✔</span></span> |<span data-ttu-id="9e5eb-257">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-257">Linux or Windows</span></span> |<span data-ttu-id="9e5eb-258">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-258">Windows</span></span> |
| <span data-ttu-id="9e5eb-259">[Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) (HDInsight 3.2 and 3.3)</span><span class="sxs-lookup"><span data-stu-id="9e5eb-259">[Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="9e5eb-260">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-260">✔</span></span> |<span data-ttu-id="9e5eb-261">✔</span><span class="sxs-lookup"><span data-stu-id="9e5eb-261">✔</span></span> |<span data-ttu-id="9e5eb-262">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-262">Windows</span></span> |<span data-ttu-id="9e5eb-263">Windows</span><span class="sxs-lookup"><span data-stu-id="9e5eb-263">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="9e5eb-264">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-264">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9e5eb-265">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="9e5eb-265">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="9e5eb-266">Hive jobs and SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="9e5eb-266">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="9e5eb-267">You can also use SQL Server Integration Services (SSIS) to run a Hive job.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-267">You can also use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="9e5eb-268">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-268">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="9e5eb-269">[Azure HDInsight Hive Task][hivetask]</span><span class="sxs-lookup"><span data-stu-id="9e5eb-269">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="9e5eb-270">[Azure Subscription Connection Manager][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="9e5eb-270">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="9e5eb-271">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span><span class="sxs-lookup"><span data-stu-id="9e5eb-271">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <a id="nextsteps"></a><span data-ttu-id="9e5eb-272">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e5eb-272">Next steps</span></span>

<span data-ttu-id="9e5eb-273">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e5eb-273">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="9e5eb-274">[Upload data to HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="9e5eb-274">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="9e5eb-275">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="9e5eb-275">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="9e5eb-276">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="9e5eb-276">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
