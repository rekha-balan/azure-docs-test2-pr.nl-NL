---
title: What is Apache Hive and HiveQL - Azure HDInsight
description: Apache Hive is a data warehouse system for Hadoop. You can query data stored in Hive using HiveQL, which similar to Transact-SQL. In this document, learn how to use Hive and HiveQL with Azure HDInsight.
keywords: hiveql,what is hive,hadoop hiveql,how to use hive,learn hive,what is hive
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 04/23/2018
ms.openlocfilehash: 446bb23e15d908c8afe189a33e4d8a70faad284a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864988"
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="ee322-106">What is Apache Hive and HiveQL on Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="ee322-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="ee322-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ee322-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="ee322-108">Hive enables data summarization, querying, and analysis of data.</span><span class="sxs-lookup"><span data-stu-id="ee322-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="ee322-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span><span class="sxs-lookup"><span data-stu-id="ee322-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span>

<span data-ttu-id="ee322-110">Hive allows you to project structure on largely unstructured data.</span><span class="sxs-lookup"><span data-stu-id="ee322-110">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="ee322-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span><span class="sxs-lookup"><span data-stu-id="ee322-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="ee322-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span><span class="sxs-lookup"><span data-stu-id="ee322-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="ee322-113">The following cluster types are most often used for Hive queries:</span><span class="sxs-lookup"><span data-stu-id="ee322-113">The following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="ee322-114">__Interactive Query__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span><span class="sxs-lookup"><span data-stu-id="ee322-114">__Interactive Query__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span></span> <span data-ttu-id="ee322-115">For more information, see the [Start with Interactive Query in HDInsight](../interactive-query/apache-interactive-query-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="ee322-115">For more information, see the [Start with Interactive Query in HDInsight](../interactive-query/apache-interactive-query-get-started.md) document.</span></span>

* <span data-ttu-id="ee322-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span><span class="sxs-lookup"><span data-stu-id="ee322-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="ee322-117">For more information, see the [Start with Hadoop in HDInsight](../hadoop/apache-hadoop-linux-tutorial-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="ee322-117">For more information, see the [Start with Hadoop in HDInsight](../hadoop/apache-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="ee322-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span><span class="sxs-lookup"><span data-stu-id="ee322-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="ee322-119">For more information, see the [Start with Spark on HDInsight](../spark/apache-spark-jupyter-spark-sql.md) document.</span><span class="sxs-lookup"><span data-stu-id="ee322-119">For more information, see the [Start with Spark on HDInsight](../spark/apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="ee322-120">__HBase__: HiveQL can be used to query data stored in HBase.</span><span class="sxs-lookup"><span data-stu-id="ee322-120">__HBase__: HiveQL can be used to query data stored in HBase.</span></span> <span data-ttu-id="ee322-121">For more information, see the [Start with HBase on HDInsight](../hbase/apache-hbase-tutorial-get-started-linux.md) document.</span><span class="sxs-lookup"><span data-stu-id="ee322-121">For more information, see the [Start with HBase on HDInsight](../hbase/apache-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-to-use-hive"></a><span data-ttu-id="ee322-122">How to use Hive</span><span class="sxs-lookup"><span data-stu-id="ee322-122">How to use Hive</span></span>

<span data-ttu-id="ee322-123">Use the following table to discover the different ways to use Hive with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ee322-123">Use the following table to discover the different ways to use Hive with HDInsight:</span></span>

| <span data-ttu-id="ee322-124">**Use this method** if you want...</span><span class="sxs-lookup"><span data-stu-id="ee322-124">**Use this method** if you want...</span></span> | <span data-ttu-id="ee322-125">...**interactive** queries</span><span class="sxs-lookup"><span data-stu-id="ee322-125">...**interactive** queries</span></span> | <span data-ttu-id="ee322-126">...**batch** processing</span><span class="sxs-lookup"><span data-stu-id="ee322-126">...**batch** processing</span></span> | <span data-ttu-id="ee322-127">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="ee322-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="ee322-128">...from this **client operating system**</span><span class="sxs-lookup"><span data-stu-id="ee322-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="ee322-129">HDInsight tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ee322-129">HDInsight tools for Visual Studio Code</span></span>](../hdinsight-for-vscode.md) |<span data-ttu-id="ee322-130">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-130">✔</span></span> |<span data-ttu-id="ee322-131">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-131">✔</span></span> |<span data-ttu-id="ee322-132">Linux</span><span class="sxs-lookup"><span data-stu-id="ee322-132">Linux</span></span> | <span data-ttu-id="ee322-133">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="ee322-133">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ee322-134">HDInsight tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee322-134">HDInsight tools for Visual Studio</span></span>](../hadoop/apache-hadoop-use-hive-visual-studio.md) |<span data-ttu-id="ee322-135">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-135">✔</span></span> |<span data-ttu-id="ee322-136">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-136">✔</span></span> |<span data-ttu-id="ee322-137">Linux or Windows\*</span><span class="sxs-lookup"><span data-stu-id="ee322-137">Linux or Windows\*</span></span> |<span data-ttu-id="ee322-138">Windows</span><span class="sxs-lookup"><span data-stu-id="ee322-138">Windows</span></span> |
| [<span data-ttu-id="ee322-139">Hive View</span><span class="sxs-lookup"><span data-stu-id="ee322-139">Hive View</span></span>](../hadoop/apache-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="ee322-140">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-140">✔</span></span> |<span data-ttu-id="ee322-141">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-141">✔</span></span> |<span data-ttu-id="ee322-142">Linux</span><span class="sxs-lookup"><span data-stu-id="ee322-142">Linux</span></span> |<span data-ttu-id="ee322-143">Any (browser based)</span><span class="sxs-lookup"><span data-stu-id="ee322-143">Any (browser based)</span></span> |
| [<span data-ttu-id="ee322-144">Beeline client</span><span class="sxs-lookup"><span data-stu-id="ee322-144">Beeline client</span></span>](../hadoop/apache-hadoop-use-hive-beeline.md) |<span data-ttu-id="ee322-145">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-145">✔</span></span> |<span data-ttu-id="ee322-146">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-146">✔</span></span> |<span data-ttu-id="ee322-147">Linux</span><span class="sxs-lookup"><span data-stu-id="ee322-147">Linux</span></span> |<span data-ttu-id="ee322-148">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="ee322-148">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ee322-149">REST API</span><span class="sxs-lookup"><span data-stu-id="ee322-149">REST API</span></span>](../hadoop/apache-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="ee322-150">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-150">✔</span></span> |<span data-ttu-id="ee322-151">Linux or Windows\*</span><span class="sxs-lookup"><span data-stu-id="ee322-151">Linux or Windows\*</span></span> |<span data-ttu-id="ee322-152">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="ee322-152">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ee322-153">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee322-153">Windows PowerShell</span></span>](../hadoop/apache-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="ee322-154">✔</span><span class="sxs-lookup"><span data-stu-id="ee322-154">✔</span></span> |<span data-ttu-id="ee322-155">Linux or Windows\*</span><span class="sxs-lookup"><span data-stu-id="ee322-155">Linux or Windows\*</span></span> |<span data-ttu-id="ee322-156">Windows</span><span class="sxs-lookup"><span data-stu-id="ee322-156">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ee322-157">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="ee322-157">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ee322-158">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ee322-158">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="ee322-159">HiveQL language reference</span><span class="sxs-lookup"><span data-stu-id="ee322-159">HiveQL language reference</span></span>

<span data-ttu-id="ee322-160">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="ee322-160">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="ee322-161">Hive and data structure</span><span class="sxs-lookup"><span data-stu-id="ee322-161">Hive and data structure</span></span>

<span data-ttu-id="ee322-162">Hive understands how to work with structured and semi-structured data.</span><span class="sxs-lookup"><span data-stu-id="ee322-162">Hive understands how to work with structured and semi-structured data.</span></span> <span data-ttu-id="ee322-163">For example, text files where the fields are delimited by specific characters.</span><span class="sxs-lookup"><span data-stu-id="ee322-163">For example, text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="ee322-164">The following HiveQL statement creates a table over space-delimited data:</span><span class="sxs-lookup"><span data-stu-id="ee322-164">The following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (
    t1 string,
    t2 string,
    t3 string,
    t4 string,
    t5 string,
    t6 string,
    t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="ee322-165">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span><span class="sxs-lookup"><span data-stu-id="ee322-165">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="ee322-166">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="ee322-166">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="ee322-167">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="ee322-167">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

### <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="ee322-168">Hive internal tables vs external tables</span><span class="sxs-lookup"><span data-stu-id="ee322-168">Hive internal tables vs external tables</span></span>

<span data-ttu-id="ee322-169">There are two types of tables that you can create with Hive:</span><span class="sxs-lookup"><span data-stu-id="ee322-169">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="ee322-170">__Internal__: Data is stored in the Hive data warehouse.</span><span class="sxs-lookup"><span data-stu-id="ee322-170">__Internal__: Data is stored in the Hive data warehouse.</span></span> <span data-ttu-id="ee322-171">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span><span class="sxs-lookup"><span data-stu-id="ee322-171">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span></span>

    <span data-ttu-id="ee322-172">Use internal tables when one of the following conditions apply:</span><span class="sxs-lookup"><span data-stu-id="ee322-172">Use internal tables when one of the following conditions apply:</span></span>

    * <span data-ttu-id="ee322-173">Data is temporary.</span><span class="sxs-lookup"><span data-stu-id="ee322-173">Data is temporary.</span></span>
    * <span data-ttu-id="ee322-174">You want Hive to manage the lifecycle of the table and data.</span><span class="sxs-lookup"><span data-stu-id="ee322-174">You want Hive to manage the lifecycle of the table and data.</span></span>

* <span data-ttu-id="ee322-175">__External__: Data is stored outside the data warehouse.</span><span class="sxs-lookup"><span data-stu-id="ee322-175">__External__: Data is stored outside the data warehouse.</span></span> <span data-ttu-id="ee322-176">The data can be stored on any storage accessible by the cluster.</span><span class="sxs-lookup"><span data-stu-id="ee322-176">The data can be stored on any storage accessible by the cluster.</span></span>

    <span data-ttu-id="ee322-177">Use external tables when one of the following conditions apply:</span><span class="sxs-lookup"><span data-stu-id="ee322-177">Use external tables when one of the following conditions apply:</span></span>

    * <span data-ttu-id="ee322-178">The data is also used outside of Hive.</span><span class="sxs-lookup"><span data-stu-id="ee322-178">The data is also used outside of Hive.</span></span> <span data-ttu-id="ee322-179">For example, the data files are updated by another process (that does not lock the files.)</span><span class="sxs-lookup"><span data-stu-id="ee322-179">For example, the data files are updated by another process (that does not lock the files.)</span></span>
    * <span data-ttu-id="ee322-180">Data needs to remain in the underlying location, even after dropping the table.</span><span class="sxs-lookup"><span data-stu-id="ee322-180">Data needs to remain in the underlying location, even after dropping the table.</span></span>
    * <span data-ttu-id="ee322-181">You need a custom location, such as a non-default storage account.</span><span class="sxs-lookup"><span data-stu-id="ee322-181">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="ee322-182">A program other than hive manages the data format, location, etc.</span><span class="sxs-lookup"><span data-stu-id="ee322-182">A program other than hive manages the data format, location, etc.</span></span>

<span data-ttu-id="ee322-183">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span><span class="sxs-lookup"><span data-stu-id="ee322-183">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="ee322-184">User-defined functions (UDF)</span><span class="sxs-lookup"><span data-stu-id="ee322-184">User-defined functions (UDF)</span></span>

<span data-ttu-id="ee322-185">Hive can also be extended through **user-defined functions (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="ee322-185">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="ee322-186">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="ee322-186">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="ee322-187">For an example of using UDFs with Hive, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="ee322-187">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="ee322-188">Use a Java user-defined function with Hive</span><span class="sxs-lookup"><span data-stu-id="ee322-188">Use a Java user-defined function with Hive</span></span>](../hadoop/apache-hadoop-hive-java-udf.md)

* [<span data-ttu-id="ee322-189">Use a Python user-defined function with Hive</span><span class="sxs-lookup"><span data-stu-id="ee322-189">Use a Python user-defined function with Hive</span></span>](../hadoop/python-udf-hdinsight.md)

* [<span data-ttu-id="ee322-190">Use a C# user-defined function with Hive</span><span class="sxs-lookup"><span data-stu-id="ee322-190">Use a C# user-defined function with Hive</span></span>](../hadoop/apache-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="ee322-191">How to add a custom Hive user-defined function to HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee322-191">How to add a custom Hive user-defined function to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="ee322-192">An example Hive user-defined function to convert date/time formats to Hive timestamp</span><span class="sxs-lookup"><span data-stu-id="ee322-192">An example Hive user-defined function to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a><span data-ttu-id="ee322-193">Example data</span><span class="sxs-lookup"><span data-stu-id="ee322-193">Example data</span></span>

<span data-ttu-id="ee322-194">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="ee322-194">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="ee322-195">HDInsight also provides example data sets that can be used with Hive.</span><span class="sxs-lookup"><span data-stu-id="ee322-195">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="ee322-196">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span><span class="sxs-lookup"><span data-stu-id="ee322-196">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="ee322-197">These directories exist in the default storage for your cluster.</span><span class="sxs-lookup"><span data-stu-id="ee322-197">These directories exist in the default storage for your cluster.</span></span>

## <a id="job"></a><span data-ttu-id="ee322-198">Example Hive query</span><span class="sxs-lookup"><span data-stu-id="ee322-198">Example Hive query</span></span>

<span data-ttu-id="ee322-199">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span><span class="sxs-lookup"><span data-stu-id="ee322-199">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

```hiveql
set hive.execution.engine=tez;
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
STORED AS TEXTFILE LOCATION '/example/data/';
SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs 
    WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' 
    GROUP BY t4;
```

<span data-ttu-id="ee322-200">In the previous example, the HiveQL statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="ee322-200">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="ee322-201">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span><span class="sxs-lookup"><span data-stu-id="ee322-201">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="ee322-202">Using Tez can provide an increase in query performance.</span><span class="sxs-lookup"><span data-stu-id="ee322-202">Using Tez can provide an increase in query performance.</span></span> <span data-ttu-id="ee322-203">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span><span class="sxs-lookup"><span data-stu-id="ee322-203">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ee322-204">This statement is only required when using a Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ee322-204">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="ee322-205">Tez is the default execution engine for Linux-based HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee322-205">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="ee322-206">`DROP TABLE`: If the table already exists, delete it.</span><span class="sxs-lookup"><span data-stu-id="ee322-206">`DROP TABLE`: If the table already exists, delete it.</span></span>

* <span data-ttu-id="ee322-207">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span><span class="sxs-lookup"><span data-stu-id="ee322-207">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="ee322-208">External tables only store the table definition in Hive.</span><span class="sxs-lookup"><span data-stu-id="ee322-208">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="ee322-209">The data is left in the original location and in the original format.</span><span class="sxs-lookup"><span data-stu-id="ee322-209">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="ee322-210">`ROW FORMAT`: Tells Hive how the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="ee322-210">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="ee322-211">In this case, the fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="ee322-211">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="ee322-212">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span><span class="sxs-lookup"><span data-stu-id="ee322-212">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="ee322-213">The data can be in one file or spread across multiple files within the directory.</span><span class="sxs-lookup"><span data-stu-id="ee322-213">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="ee322-214">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="ee322-214">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="ee322-215">This statement returns a value of **3** because there are three rows that contain this value.</span><span class="sxs-lookup"><span data-stu-id="ee322-215">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="ee322-216">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span><span class="sxs-lookup"><span data-stu-id="ee322-216">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="ee322-217">In this case, the directory contains files that do not match the schema.</span><span class="sxs-lookup"><span data-stu-id="ee322-217">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="ee322-218">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span><span class="sxs-lookup"><span data-stu-id="ee322-218">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="ee322-219">External tables should be used when you expect the underlying data to be updated by an external source.</span><span class="sxs-lookup"><span data-stu-id="ee322-219">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="ee322-220">For example, an automated data upload process, or MapReduce operation.</span><span class="sxs-lookup"><span data-stu-id="ee322-220">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="ee322-221">Dropping an external table does **not** delete the data, it only deletes the table definition.</span><span class="sxs-lookup"><span data-stu-id="ee322-221">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="ee322-222">To create an **internal** table instead of external, use the following HiveQL:</span><span class="sxs-lookup"><span data-stu-id="ee322-222">To create an **internal** table instead of external, use the following HiveQL:</span></span>

```hiveql
set hive.execution.engine=tez;
CREATE TABLE IF NOT EXISTS errorLogs (
    t1 string,
    t2 string,
    t3 string,
    t4 string,
    t5 string,
    t6 string,
    t7 string)
STORED AS ORC;
INSERT OVERWRITE TABLE errorLogs
SELECT t1, t2, t3, t4, t5, t6, t7 
    FROM log4jLogs WHERE t4 = '[ERROR]';
```

<span data-ttu-id="ee322-223">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="ee322-223">These statements perform the following actions:</span></span>

* <span data-ttu-id="ee322-224">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span><span class="sxs-lookup"><span data-stu-id="ee322-224">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span></span> <span data-ttu-id="ee322-225">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span><span class="sxs-lookup"><span data-stu-id="ee322-225">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="ee322-226">The table is stored in the Hive data warehouse and is managed completely by Hive.</span><span class="sxs-lookup"><span data-stu-id="ee322-226">The table is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="ee322-227">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="ee322-227">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="ee322-228">ORC is a highly optimized and efficient format for storing Hive data.</span><span class="sxs-lookup"><span data-stu-id="ee322-228">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="ee322-229">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span><span class="sxs-lookup"><span data-stu-id="ee322-229">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="ee322-230">Unlike external tables, dropping an internal table also deletes the underlying data.</span><span class="sxs-lookup"><span data-stu-id="ee322-230">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="ee322-231">Improve Hive query performance</span><span class="sxs-lookup"><span data-stu-id="ee322-231">Improve Hive query performance</span></span>

### <a id="usetez"></a><span data-ttu-id="ee322-232">Apache Tez</span><span class="sxs-lookup"><span data-stu-id="ee322-232">Apache Tez</span></span>

<span data-ttu-id="ee322-233">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span><span class="sxs-lookup"><span data-stu-id="ee322-233">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="ee322-234">Tez is enabled by default for Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="ee322-234">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="ee322-235">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span><span class="sxs-lookup"><span data-stu-id="ee322-235">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="ee322-236">To take advantage of Tez, the following value must be set for a Hive query:</span><span class="sxs-lookup"><span data-stu-id="ee322-236">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="ee322-237">Tez is the default engine for Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="ee322-237">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="ee322-238">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span><span class="sxs-lookup"><span data-stu-id="ee322-238">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="ee322-239">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span><span class="sxs-lookup"><span data-stu-id="ee322-239">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="ee322-240">Use the Ambari Tez view on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee322-240">Use the Ambari Tez view on Linux-based HDInsight</span></span>](../hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="ee322-241">Use the Tez UI on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee322-241">Use the Tez UI on Windows-based HDInsight</span></span>](../hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="ee322-242">Low Latency Analytical Processing (LLAP)</span><span class="sxs-lookup"><span data-stu-id="ee322-242">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="ee322-243">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span><span class="sxs-lookup"><span data-stu-id="ee322-243">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="ee322-244">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="ee322-244">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="ee322-245">HDInsight provides LLAP in the Interactive Query cluster type.</span><span class="sxs-lookup"><span data-stu-id="ee322-245">HDInsight provides LLAP in the Interactive Query cluster type.</span></span> <span data-ttu-id="ee322-246">For more information, see the [Start with Interactive Query](../interactive-query/apache-interactive-query-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="ee322-246">For more information, see the [Start with Interactive Query](../interactive-query/apache-interactive-query-get-started.md) document.</span></span>

## <a name="scheduling-hive-queries"></a><span data-ttu-id="ee322-247">Scheduling Hive queries</span><span class="sxs-lookup"><span data-stu-id="ee322-247">Scheduling Hive queries</span></span>

<span data-ttu-id="ee322-248">There are several services that can be used to run Hive queries as part of a scheduled or on-demand workflow.</span><span class="sxs-lookup"><span data-stu-id="ee322-248">There are several services that can be used to run Hive queries as part of a scheduled or on-demand workflow.</span></span>

### <a name="azure-data-factory"></a><span data-ttu-id="ee322-249">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ee322-249">Azure Data Factory</span></span>

<span data-ttu-id="ee322-250">Azure Data Factory allows you to use HDInsight as part of a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="ee322-250">Azure Data Factory allows you to use HDInsight as part of a Data Factory pipeline.</span></span> <span data-ttu-id="ee322-251">For more information on using Hive from a pipeline, see the [Transform data using Hive activity in Azure Data Factory](../../data-factory/transform-data-using-hadoop-hive.md) document.</span><span class="sxs-lookup"><span data-stu-id="ee322-251">For more information on using Hive from a pipeline, see the [Transform data using Hive activity in Azure Data Factory](../../data-factory/transform-data-using-hadoop-hive.md) document.</span></span>

### <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="ee322-252">Hive jobs and SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="ee322-252">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="ee322-253">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span><span class="sxs-lookup"><span data-stu-id="ee322-253">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="ee322-254">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee322-254">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="ee322-255">[Azure HDInsight Hive Task][hivetask]</span><span class="sxs-lookup"><span data-stu-id="ee322-255">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="ee322-256">[Azure Subscription Connection Manager][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="ee322-256">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="ee322-257">For more information, see the [Azure Feature Pack][ssispack] documentation.</span><span class="sxs-lookup"><span data-stu-id="ee322-257">For more information, see the [Azure Feature Pack][ssispack] documentation.</span></span>

### <a name="apache-oozie"></a><span data-ttu-id="ee322-258">Apache Oozie</span><span class="sxs-lookup"><span data-stu-id="ee322-258">Apache Oozie</span></span>

<span data-ttu-id="ee322-259">Apache Oozie is a workflow and coordination system that manages Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="ee322-259">Apache Oozie is a workflow and coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="ee322-260">For more information on using Oozie with Hive, see the [Use Oozie to define and run a workflow](../hdinsight-use-oozie-linux-mac.md) document.</span><span class="sxs-lookup"><span data-stu-id="ee322-260">For more information on using Oozie with Hive, see the [Use Oozie to define and run a workflow](../hdinsight-use-oozie-linux-mac.md) document.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="ee322-261">Next steps</span><span class="sxs-lookup"><span data-stu-id="ee322-261">Next steps</span></span>

<span data-ttu-id="ee322-262">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee322-262">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="ee322-263">[Upload data to HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ee322-263">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ee322-264">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ee322-264">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="ee322-265">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="ee322-265">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: ../hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
