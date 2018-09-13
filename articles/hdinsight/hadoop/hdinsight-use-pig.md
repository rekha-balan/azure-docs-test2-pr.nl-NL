---
title: Use Hadoop Pig in HDInsight
description: Learn how to use Pig with Hadoop on HDInsight.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/23/2018
ms.openlocfilehash: e97763adbe7998ed93e3ba8b87d89ffe8d8de6aa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868973"
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="d0af2-103">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0af2-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="d0af2-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0af2-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight.</span></span>

<span data-ttu-id="d0af2-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="d0af2-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="d0af2-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0af2-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="d0af2-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d0af2-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="d0af2-108">**Use this** if you want...</span><span class="sxs-lookup"><span data-stu-id="d0af2-108">**Use this** if you want...</span></span> | <span data-ttu-id="d0af2-109">...an **interactive** shell</span><span class="sxs-lookup"><span data-stu-id="d0af2-109">...an **interactive** shell</span></span> | <span data-ttu-id="d0af2-110">...**batch** processing</span><span class="sxs-lookup"><span data-stu-id="d0af2-110">...**batch** processing</span></span> | <span data-ttu-id="d0af2-111">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="d0af2-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="d0af2-112">...from this **client operating system**</span><span class="sxs-lookup"><span data-stu-id="d0af2-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="d0af2-113">SSH</span><span class="sxs-lookup"><span data-stu-id="d0af2-113">SSH</span></span>](apache-hadoop-use-pig-ssh.md) |<span data-ttu-id="d0af2-114">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-114">✔</span></span> |<span data-ttu-id="d0af2-115">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-115">✔</span></span> |<span data-ttu-id="d0af2-116">Linux</span><span class="sxs-lookup"><span data-stu-id="d0af2-116">Linux</span></span> |<span data-ttu-id="d0af2-117">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="d0af2-118">REST API</span><span class="sxs-lookup"><span data-stu-id="d0af2-118">REST API</span></span>](apache-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="d0af2-119">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-119">✔</span></span> |<span data-ttu-id="d0af2-120">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-120">Linux or Windows</span></span> |<span data-ttu-id="d0af2-121">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="d0af2-122">.NET SDK for Hadoop</span><span class="sxs-lookup"><span data-stu-id="d0af2-122">.NET SDK for Hadoop</span></span>](apache-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="d0af2-123">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-123">✔</span></span> |<span data-ttu-id="d0af2-124">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-124">Linux or Windows</span></span> |<span data-ttu-id="d0af2-125">Windows (for now)</span><span class="sxs-lookup"><span data-stu-id="d0af2-125">Windows (for now)</span></span> |
| [<span data-ttu-id="d0af2-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0af2-126">Windows PowerShell</span></span>](apache-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="d0af2-127">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-127">✔</span></span> |<span data-ttu-id="d0af2-128">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-128">Linux or Windows</span></span> |<span data-ttu-id="d0af2-129">Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-129">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d0af2-130">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="d0af2-130">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d0af2-131">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d0af2-131">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a id="why"></a><span data-ttu-id="d0af2-132">Why use Pig</span><span class="sxs-lookup"><span data-stu-id="d0af2-132">Why use Pig</span></span>

<span data-ttu-id="d0af2-133">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span><span class="sxs-lookup"><span data-stu-id="d0af2-133">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="d0af2-134">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span><span class="sxs-lookup"><span data-stu-id="d0af2-134">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span></span>

<span data-ttu-id="d0af2-135">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span><span class="sxs-lookup"><span data-stu-id="d0af2-135">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span></span>

<span data-ttu-id="d0af2-136">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span><span class="sxs-lookup"><span data-stu-id="d0af2-136">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span></span> <span data-ttu-id="d0af2-137">Pig Latin programs follow this general pattern:</span><span class="sxs-lookup"><span data-stu-id="d0af2-137">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="d0af2-138">**Load**: Read data to be manipulated from the file system</span><span class="sxs-lookup"><span data-stu-id="d0af2-138">**Load**: Read data to be manipulated from the file system</span></span>

* <span data-ttu-id="d0af2-139">**Transform**: Manipulate the data</span><span class="sxs-lookup"><span data-stu-id="d0af2-139">**Transform**: Manipulate the data</span></span>

* <span data-ttu-id="d0af2-140">**Dump or store**: Output data to the screen or store it for processing</span><span class="sxs-lookup"><span data-stu-id="d0af2-140">**Dump or store**: Output data to the screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="d0af2-141">User-defined functions</span><span class="sxs-lookup"><span data-stu-id="d0af2-141">User-defined functions</span></span>

<span data-ttu-id="d0af2-142">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="d0af2-142">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span></span>

<span data-ttu-id="d0af2-143">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://archive.cloudera.com/cdh/3/pig/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://archive.cloudera.com/cdh/3/pig/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="d0af2-143">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://archive.cloudera.com/cdh/3/pig/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://archive.cloudera.com/cdh/3/pig/piglatin_ref2.html).</span></span>

<span data-ttu-id="d0af2-144">For an example of using UDFs with Pig, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="d0af2-144">For an example of using UDFs with Pig, see the following documents:</span></span>

* <span data-ttu-id="d0af2-145">[Use DataFu with Pig in HDInsight](apache-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span><span class="sxs-lookup"><span data-stu-id="d0af2-145">[Use DataFu with Pig in HDInsight](apache-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="d0af2-146">Use Python with Pig and Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0af2-146">Use Python with Pig and Hive in HDInsight</span></span>](python-udf-hdinsight.md)
* [<span data-ttu-id="d0af2-147">Use C# with Hive and Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0af2-147">Use C# with Hive and Pig in HDInsight</span></span>](apache-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a><span data-ttu-id="d0af2-148">Example data</span><span class="sxs-lookup"><span data-stu-id="d0af2-148">Example data</span></span>

<span data-ttu-id="d0af2-149">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span><span class="sxs-lookup"><span data-stu-id="d0af2-149">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="d0af2-150">These directories are in the default storage for your cluster.</span><span class="sxs-lookup"><span data-stu-id="d0af2-150">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="d0af2-151">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="d0af2-151">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="d0af2-152">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span><span class="sxs-lookup"><span data-stu-id="d0af2-152">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="d0af2-153">In the previous example, the log level is ERROR.</span><span class="sxs-lookup"><span data-stu-id="d0af2-153">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="d0af2-154">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span><span class="sxs-lookup"><span data-stu-id="d0af2-154">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span></span> <span data-ttu-id="d0af2-155">See [Upload Data to HDInsight](../hdinsight-upload-data.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="d0af2-155">See [Upload Data to HDInsight](../hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="d0af2-156">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](../hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d0af2-156">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](../hdinsight-hadoop-use-blob-storage.md).</span></span>

## <a id="job"></a><span data-ttu-id="d0af2-157">Example job</span><span class="sxs-lookup"><span data-stu-id="d0af2-157">Example job</span></span>

<span data-ttu-id="d0af2-158">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d0af2-158">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="d0af2-159">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span><span class="sxs-lookup"><span data-stu-id="d0af2-159">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span></span> <span data-ttu-id="d0af2-160">The results are written to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="d0af2-160">The results are written to STDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="d0af2-161">The following image shows a summary of what each transformation does to the data.</span><span class="sxs-lookup"><span data-stu-id="d0af2-161">The following image shows a summary of what each transformation does to the data.</span></span>

![Graphical representation of the transformations][image-hdi-pig-data-transformation]

## <a id="run"></a><span data-ttu-id="d0af2-163">Run the Pig Latin job</span><span class="sxs-lookup"><span data-stu-id="d0af2-163">Run the Pig Latin job</span></span>

<span data-ttu-id="d0af2-164">HDInsight can run Pig Latin jobs by using a variety of methods.</span><span class="sxs-lookup"><span data-stu-id="d0af2-164">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="d0af2-165">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span><span class="sxs-lookup"><span data-stu-id="d0af2-165">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="d0af2-166">**Use this** if you want...</span><span class="sxs-lookup"><span data-stu-id="d0af2-166">**Use this** if you want...</span></span> | <span data-ttu-id="d0af2-167">...an **interactive** shell</span><span class="sxs-lookup"><span data-stu-id="d0af2-167">...an **interactive** shell</span></span> | <span data-ttu-id="d0af2-168">...**batch** processing</span><span class="sxs-lookup"><span data-stu-id="d0af2-168">...**batch** processing</span></span> | <span data-ttu-id="d0af2-169">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="d0af2-169">...with this **cluster operating system**</span></span> | <span data-ttu-id="d0af2-170">...from this **client**</span><span class="sxs-lookup"><span data-stu-id="d0af2-170">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="d0af2-171">SSH</span><span class="sxs-lookup"><span data-stu-id="d0af2-171">SSH</span></span>](apache-hadoop-use-pig-ssh.md) |<span data-ttu-id="d0af2-172">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-172">✔</span></span> |<span data-ttu-id="d0af2-173">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-173">✔</span></span> |<span data-ttu-id="d0af2-174">Linux</span><span class="sxs-lookup"><span data-stu-id="d0af2-174">Linux</span></span> |<span data-ttu-id="d0af2-175">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-175">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="d0af2-176">Curl</span><span class="sxs-lookup"><span data-stu-id="d0af2-176">Curl</span></span>](apache-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="d0af2-177">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-177">✔</span></span> |<span data-ttu-id="d0af2-178">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-178">Linux or Windows</span></span> |<span data-ttu-id="d0af2-179">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-179">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="d0af2-180">.NET SDK for Hadoop</span><span class="sxs-lookup"><span data-stu-id="d0af2-180">.NET SDK for Hadoop</span></span>](apache-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="d0af2-181">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-181">✔</span></span> |<span data-ttu-id="d0af2-182">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-182">Linux or Windows</span></span> |<span data-ttu-id="d0af2-183">Windows (for now)</span><span class="sxs-lookup"><span data-stu-id="d0af2-183">Windows (for now)</span></span> |
| [<span data-ttu-id="d0af2-184">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0af2-184">Windows PowerShell</span></span>](apache-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="d0af2-185">✔</span><span class="sxs-lookup"><span data-stu-id="d0af2-185">✔</span></span> |<span data-ttu-id="d0af2-186">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-186">Linux or Windows</span></span> |<span data-ttu-id="d0af2-187">Windows</span><span class="sxs-lookup"><span data-stu-id="d0af2-187">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d0af2-188">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="d0af2-188">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d0af2-189">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d0af2-189">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="d0af2-190">Pig and SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="d0af2-190">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="d0af2-191">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span><span class="sxs-lookup"><span data-stu-id="d0af2-191">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span></span> <span data-ttu-id="d0af2-192">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0af2-192">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="d0af2-193">[Azure HDInsight Pig Task][pigtask]</span><span class="sxs-lookup"><span data-stu-id="d0af2-193">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="d0af2-194">[Azure Subscription Connection Manager][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="d0af2-194">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="d0af2-195">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span><span class="sxs-lookup"><span data-stu-id="d0af2-195">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <a id="nextsteps"></a><span data-ttu-id="d0af2-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0af2-196">Next steps</span></span>
<span data-ttu-id="d0af2-197">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d0af2-197">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="d0af2-198">Upload data to HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0af2-198">Upload data to HDInsight</span></span>](../hdinsight-upload-data.md)
* <span data-ttu-id="d0af2-199">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d0af2-199">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="d0af2-200">Use Sqoop with HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0af2-200">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="d0af2-201">Use Oozie with HDInsight</span><span class="sxs-lookup"><span data-stu-id="d0af2-201">Use Oozie with HDInsight</span></span>](../hdinsight-use-oozie.md)
* <span data-ttu-id="d0af2-202">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="d0af2-202">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]:../hdinsight-use-hive.md
[hdinsight-use-mapreduce]:../hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
