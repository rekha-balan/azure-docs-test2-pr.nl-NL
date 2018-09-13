---
title: Use Hadoop Pig in HDInsight | Microsoft Docs
description: Learn how to use Pig with Hadoop on HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/03/2017
ms.author: larryfr
ms.openlocfilehash: e4d1ebe756c242db5e528c9bc861ce7b5d2d09da
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551279"
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="a4b9e-103">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4b9e-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="a4b9e-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight...</span><span class="sxs-lookup"><span data-stu-id="a4b9e-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="a4b9e-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="a4b9e-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="a4b9e-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a4b9e-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="a4b9e-108">**Use this** if you want...</span><span class="sxs-lookup"><span data-stu-id="a4b9e-108">**Use this** if you want...</span></span> | <span data-ttu-id="a4b9e-109">...an **interactive** shell</span><span class="sxs-lookup"><span data-stu-id="a4b9e-109">...an **interactive** shell</span></span> | <span data-ttu-id="a4b9e-110">...**batch** processing</span><span class="sxs-lookup"><span data-stu-id="a4b9e-110">...**batch** processing</span></span> | <span data-ttu-id="a4b9e-111">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="a4b9e-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="a4b9e-112">...from this **client operating system**</span><span class="sxs-lookup"><span data-stu-id="a4b9e-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="a4b9e-113">SSH</span><span class="sxs-lookup"><span data-stu-id="a4b9e-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="a4b9e-114">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-114">✔</span></span> |<span data-ttu-id="a4b9e-115">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-115">✔</span></span> |<span data-ttu-id="a4b9e-116">Linux</span><span class="sxs-lookup"><span data-stu-id="a4b9e-116">Linux</span></span> |<span data-ttu-id="a4b9e-117">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a4b9e-118">REST API</span><span class="sxs-lookup"><span data-stu-id="a4b9e-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="a4b9e-119">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-119">✔</span></span> |<span data-ttu-id="a4b9e-120">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-120">Linux or Windows</span></span> |<span data-ttu-id="a4b9e-121">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a4b9e-122">.NET SDK for Hadoop</span><span class="sxs-lookup"><span data-stu-id="a4b9e-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="a4b9e-123">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-123">✔</span></span> |<span data-ttu-id="a4b9e-124">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-124">Linux or Windows</span></span> |<span data-ttu-id="a4b9e-125">Windows (for now)</span><span class="sxs-lookup"><span data-stu-id="a4b9e-125">Windows (for now)</span></span> |
| [<span data-ttu-id="a4b9e-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4b9e-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="a4b9e-127">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-127">✔</span></span> |<span data-ttu-id="a4b9e-128">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-128">Linux or Windows</span></span> |<span data-ttu-id="a4b9e-129">Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-129">Windows</span></span> |
| <span data-ttu-id="a4b9e-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span><span class="sxs-lookup"><span data-stu-id="a4b9e-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="a4b9e-131">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-131">✔</span></span> |<span data-ttu-id="a4b9e-132">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-132">✔</span></span> |<span data-ttu-id="a4b9e-133">Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-133">Windows</span></span> |<span data-ttu-id="a4b9e-134">Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a4b9e-135">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-135">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a4b9e-136">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="a4b9e-136">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a id="why"></a><span data-ttu-id="a4b9e-137">Why use Pig</span><span class="sxs-lookup"><span data-stu-id="a4b9e-137">Why use Pig</span></span>

<span data-ttu-id="a4b9e-138">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-138">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="a4b9e-139">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-139">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span></span>

<span data-ttu-id="a4b9e-140">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-140">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span></span>

<span data-ttu-id="a4b9e-141">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-141">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span></span> <span data-ttu-id="a4b9e-142">Pig Latin programs follow this general pattern:</span><span class="sxs-lookup"><span data-stu-id="a4b9e-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="a4b9e-143">**Load**: Read data to be manipulated from the file system</span><span class="sxs-lookup"><span data-stu-id="a4b9e-143">**Load**: Read data to be manipulated from the file system</span></span>

* <span data-ttu-id="a4b9e-144">**Transform**: Manipulate the data</span><span class="sxs-lookup"><span data-stu-id="a4b9e-144">**Transform**: Manipulate the data</span></span>

* <span data-ttu-id="a4b9e-145">**Dump or store**: Output data to the screen or store it for processing</span><span class="sxs-lookup"><span data-stu-id="a4b9e-145">**Dump or store**: Output data to the screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="a4b9e-146">User-defined functions</span><span class="sxs-lookup"><span data-stu-id="a4b9e-146">User-defined functions</span></span>

<span data-ttu-id="a4b9e-147">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-147">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span></span>

<span data-ttu-id="a4b9e-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="a4b9e-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="a4b9e-149">For an example of using UDFs with Pig, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="a4b9e-149">For an example of using UDFs with Pig, see the following documents:</span></span>

* <span data-ttu-id="a4b9e-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span><span class="sxs-lookup"><span data-stu-id="a4b9e-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="a4b9e-151">Use Python with Pig and Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4b9e-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="a4b9e-152">Use C# with Hive and Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4b9e-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a><span data-ttu-id="a4b9e-153">Example data</span><span class="sxs-lookup"><span data-stu-id="a4b9e-153">Example data</span></span>

<span data-ttu-id="a4b9e-154">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-154">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="a4b9e-155">These directories are in the default storage for your cluster.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-155">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="a4b9e-156">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-156">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="a4b9e-157">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span><span class="sxs-lookup"><span data-stu-id="a4b9e-157">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="a4b9e-158">In the previous example, the log level is ERROR.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-158">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="a4b9e-159">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-159">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span></span> <span data-ttu-id="a4b9e-160">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-160">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="a4b9e-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a4b9e-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <a id="job"></a><span data-ttu-id="a4b9e-162">Example job</span><span class="sxs-lookup"><span data-stu-id="a4b9e-162">Example job</span></span>

<span data-ttu-id="a4b9e-163">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-163">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="a4b9e-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span></span> <span data-ttu-id="a4b9e-165">The results are written to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-165">The results are written to STDOUT.</span></span>

    LOGS = LOAD 'wasbs:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="a4b9e-166">The following image shows a summary of what each transformation does to the data.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-166">The following image shows a summary of what each transformation does to the data.</span></span>

![Graphical representation of the transformations][image-hdi-pig-data-transformation]

## <a id="run"></a><span data-ttu-id="a4b9e-168">Run the Pig Latin job</span><span class="sxs-lookup"><span data-stu-id="a4b9e-168">Run the Pig Latin job</span></span>

<span data-ttu-id="a4b9e-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="a4b9e-170">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-170">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="a4b9e-171">**Use this** if you want...</span><span class="sxs-lookup"><span data-stu-id="a4b9e-171">**Use this** if you want...</span></span> | <span data-ttu-id="a4b9e-172">...an **interactive** shell</span><span class="sxs-lookup"><span data-stu-id="a4b9e-172">...an **interactive** shell</span></span> | <span data-ttu-id="a4b9e-173">...**batch** processing</span><span class="sxs-lookup"><span data-stu-id="a4b9e-173">...**batch** processing</span></span> | <span data-ttu-id="a4b9e-174">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="a4b9e-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="a4b9e-175">...from this **client**</span><span class="sxs-lookup"><span data-stu-id="a4b9e-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="a4b9e-176">SSH</span><span class="sxs-lookup"><span data-stu-id="a4b9e-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="a4b9e-177">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-177">✔</span></span> |<span data-ttu-id="a4b9e-178">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-178">✔</span></span> |<span data-ttu-id="a4b9e-179">Linux</span><span class="sxs-lookup"><span data-stu-id="a4b9e-179">Linux</span></span> |<span data-ttu-id="a4b9e-180">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a4b9e-181">Curl</span><span class="sxs-lookup"><span data-stu-id="a4b9e-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="a4b9e-182">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-182">✔</span></span> |<span data-ttu-id="a4b9e-183">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-183">Linux or Windows</span></span> |<span data-ttu-id="a4b9e-184">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a4b9e-185">.NET SDK for Hadoop</span><span class="sxs-lookup"><span data-stu-id="a4b9e-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="a4b9e-186">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-186">✔</span></span> |<span data-ttu-id="a4b9e-187">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-187">Linux or Windows</span></span> |<span data-ttu-id="a4b9e-188">Windows (for now)</span><span class="sxs-lookup"><span data-stu-id="a4b9e-188">Windows (for now)</span></span> |
| [<span data-ttu-id="a4b9e-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4b9e-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="a4b9e-190">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-190">✔</span></span> |<span data-ttu-id="a4b9e-191">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-191">Linux or Windows</span></span> |<span data-ttu-id="a4b9e-192">Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-192">Windows</span></span> |
| <span data-ttu-id="a4b9e-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span><span class="sxs-lookup"><span data-stu-id="a4b9e-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="a4b9e-194">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-194">✔</span></span> |<span data-ttu-id="a4b9e-195">✔</span><span class="sxs-lookup"><span data-stu-id="a4b9e-195">✔</span></span> |<span data-ttu-id="a4b9e-196">Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-196">Windows</span></span> |<span data-ttu-id="a4b9e-197">Windows</span><span class="sxs-lookup"><span data-stu-id="a4b9e-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a4b9e-198">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-198">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a4b9e-199">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="a4b9e-199">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="a4b9e-200">Pig and SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="a4b9e-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="a4b9e-201">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-201">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span></span> <span data-ttu-id="a4b9e-202">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-202">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="a4b9e-203">[Azure HDInsight Pig Task][pigtask]</span><span class="sxs-lookup"><span data-stu-id="a4b9e-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="a4b9e-204">[Azure Subscription Connection Manager][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="a4b9e-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="a4b9e-205">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span><span class="sxs-lookup"><span data-stu-id="a4b9e-205">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <a id="nextsteps"></a><span data-ttu-id="a4b9e-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4b9e-206">Next steps</span></span>
<span data-ttu-id="a4b9e-207">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4b9e-207">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="a4b9e-208">[Upload data to HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="a4b9e-208">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="a4b9e-209">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="a4b9e-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="a4b9e-210">Use Sqoop with HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4b9e-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="a4b9e-211">Use Oozie with HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4b9e-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="a4b9e-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="a4b9e-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-pig/HDI.DataTransformation.gif

