---
title: MapReduce with Hadoop on HDInsight | Microsoft Docs
description: Learn how to run MapReduce jobs on Hadoop in HDInsight clusters.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/03/2017
ms.author: larryfr
ms.openlocfilehash: 7ee8a5bf922b56cb76c0230d751048b138c7b59d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550761"
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="900d1-103">Use MapReduce in Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="900d1-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="900d1-104">Learn how to run MapReduce jobs on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="900d1-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="900d1-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="900d1-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="900d1-106">**Use this**...</span><span class="sxs-lookup"><span data-stu-id="900d1-106">**Use this**...</span></span> | <span data-ttu-id="900d1-107">**...to do this**</span><span class="sxs-lookup"><span data-stu-id="900d1-107">**...to do this**</span></span> | <span data-ttu-id="900d1-108">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="900d1-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="900d1-109">...from this **client operating system**</span><span class="sxs-lookup"><span data-stu-id="900d1-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="900d1-110">SSH</span><span class="sxs-lookup"><span data-stu-id="900d1-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="900d1-111">Use the Hadoop command through **SSH**</span><span class="sxs-lookup"><span data-stu-id="900d1-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="900d1-112">Linux</span><span class="sxs-lookup"><span data-stu-id="900d1-112">Linux</span></span> |<span data-ttu-id="900d1-113">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="900d1-114">REST</span><span class="sxs-lookup"><span data-stu-id="900d1-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="900d1-115">Submit the job remotely by using **REST** (examples use cURL)</span><span class="sxs-lookup"><span data-stu-id="900d1-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="900d1-116">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-116">Linux or Windows</span></span> |<span data-ttu-id="900d1-117">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="900d1-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="900d1-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="900d1-119">Submit the job remotely by using **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="900d1-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="900d1-120">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-120">Linux or Windows</span></span> |<span data-ttu-id="900d1-121">Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-121">Windows</span></span> |
| <span data-ttu-id="900d1-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span><span class="sxs-lookup"><span data-stu-id="900d1-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="900d1-123">Use the Hadoop command through **Remote Desktop**</span><span class="sxs-lookup"><span data-stu-id="900d1-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="900d1-124">Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-124">Windows</span></span> |<span data-ttu-id="900d1-125">Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="900d1-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="900d1-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="900d1-127">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="900d1-127">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a id="whatis"></a><span data-ttu-id="900d1-128">What is MapReduce</span><span class="sxs-lookup"><span data-stu-id="900d1-128">What is MapReduce</span></span>

<span data-ttu-id="900d1-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span><span class="sxs-lookup"><span data-stu-id="900d1-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="900d1-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span><span class="sxs-lookup"><span data-stu-id="900d1-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="900d1-131">A MapReduce job consists of two functions:</span><span class="sxs-lookup"><span data-stu-id="900d1-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="900d1-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span><span class="sxs-lookup"><span data-stu-id="900d1-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="900d1-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span><span class="sxs-lookup"><span data-stu-id="900d1-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="900d1-134">A basic word count MapReduce job example is illustrated in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="900d1-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="900d1-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span><span class="sxs-lookup"><span data-stu-id="900d1-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="900d1-137">The mapper takes each line from the input text as an input and breaks it into words.</span><span class="sxs-lookup"><span data-stu-id="900d1-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="900d1-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span><span class="sxs-lookup"><span data-stu-id="900d1-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="900d1-139">The output is sorted before sending it to reducer.</span><span class="sxs-lookup"><span data-stu-id="900d1-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="900d1-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span><span class="sxs-lookup"><span data-stu-id="900d1-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="900d1-141">MapReduce can be implemented in various languages.</span><span class="sxs-lookup"><span data-stu-id="900d1-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="900d1-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span><span class="sxs-lookup"><span data-stu-id="900d1-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="900d1-143">Development languages</span><span class="sxs-lookup"><span data-stu-id="900d1-143">Development languages</span></span>

<span data-ttu-id="900d1-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="900d1-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="900d1-145">The example used in this document is a Java MapReduce application.</span><span class="sxs-lookup"><span data-stu-id="900d1-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="900d1-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span><span class="sxs-lookup"><span data-stu-id="900d1-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="900d1-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span><span class="sxs-lookup"><span data-stu-id="900d1-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="900d1-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="900d1-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="900d1-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span><span class="sxs-lookup"><span data-stu-id="900d1-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="900d1-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="900d1-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="900d1-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="900d1-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="900d1-152">Develop C# MapReduce jobs</span><span class="sxs-lookup"><span data-stu-id="900d1-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="900d1-153">Develop Python MapReduce jobs</span><span class="sxs-lookup"><span data-stu-id="900d1-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a><span data-ttu-id="900d1-154">Example data</span><span class="sxs-lookup"><span data-stu-id="900d1-154">Example data</span></span>

<span data-ttu-id="900d1-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span><span class="sxs-lookup"><span data-stu-id="900d1-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="900d1-156">These directories are in the default storage for your cluster.</span><span class="sxs-lookup"><span data-stu-id="900d1-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="900d1-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span><span class="sxs-lookup"><span data-stu-id="900d1-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="900d1-158">This file contains the notebooks of Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="900d1-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <a id="job"></a><span data-ttu-id="900d1-159">Example MapReduce</span><span class="sxs-lookup"><span data-stu-id="900d1-159">Example MapReduce</span></span>

<span data-ttu-id="900d1-160">An example MapReduce word count application is included with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="900d1-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="900d1-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span><span class="sxs-lookup"><span data-stu-id="900d1-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="900d1-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span><span class="sxs-lookup"><span data-stu-id="900d1-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

<span data-ttu-id="900d1-163">For instructions to write your own MapReduce applications, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="900d1-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="900d1-164">Develop Java MapReduce applications for HDInsight</span><span class="sxs-lookup"><span data-stu-id="900d1-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="900d1-165">Develop Python MapReduce applications for HDInsight</span><span class="sxs-lookup"><span data-stu-id="900d1-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a><span data-ttu-id="900d1-166">Run the MapReduce</span><span class="sxs-lookup"><span data-stu-id="900d1-166">Run the MapReduce</span></span>

<span data-ttu-id="900d1-167">HDInsight can run HiveQL jobs by using various methods.</span><span class="sxs-lookup"><span data-stu-id="900d1-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="900d1-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span><span class="sxs-lookup"><span data-stu-id="900d1-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="900d1-169">**Use this**...</span><span class="sxs-lookup"><span data-stu-id="900d1-169">**Use this**...</span></span> | <span data-ttu-id="900d1-170">**...to do this**</span><span class="sxs-lookup"><span data-stu-id="900d1-170">**...to do this**</span></span> | <span data-ttu-id="900d1-171">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="900d1-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="900d1-172">...from this **client operating system**</span><span class="sxs-lookup"><span data-stu-id="900d1-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="900d1-173">SSH</span><span class="sxs-lookup"><span data-stu-id="900d1-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="900d1-174">Use the Hadoop command through **SSH**</span><span class="sxs-lookup"><span data-stu-id="900d1-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="900d1-175">Linux</span><span class="sxs-lookup"><span data-stu-id="900d1-175">Linux</span></span> |<span data-ttu-id="900d1-176">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="900d1-177">Curl</span><span class="sxs-lookup"><span data-stu-id="900d1-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="900d1-178">Submit the job remotely by using **REST**</span><span class="sxs-lookup"><span data-stu-id="900d1-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="900d1-179">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-179">Linux or Windows</span></span> |<span data-ttu-id="900d1-180">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="900d1-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="900d1-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="900d1-182">Submit the job remotely by using **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="900d1-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="900d1-183">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-183">Linux or Windows</span></span> |<span data-ttu-id="900d1-184">Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-184">Windows</span></span> |
| <span data-ttu-id="900d1-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span><span class="sxs-lookup"><span data-stu-id="900d1-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="900d1-186">Use the Hadoop command through **Remote Desktop**</span><span class="sxs-lookup"><span data-stu-id="900d1-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="900d1-187">Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-187">Windows</span></span> |<span data-ttu-id="900d1-188">Windows</span><span class="sxs-lookup"><span data-stu-id="900d1-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="900d1-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="900d1-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="900d1-190">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="900d1-190">For more information, see [HDInsight 3.2 and 3.3 deprecation](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a id="nextsteps"></a><span data-ttu-id="900d1-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="900d1-191">Next steps</span></span>

<span data-ttu-id="900d1-192">To learn more about working with data in HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="900d1-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="900d1-193">Develop Java MapReduce programs for HDInsight</span><span class="sxs-lookup"><span data-stu-id="900d1-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="900d1-194">Develop Python streaming MapReduce programs for HDInsight</span><span class="sxs-lookup"><span data-stu-id="900d1-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="900d1-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="900d1-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="900d1-196">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="900d1-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="900d1-197">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="900d1-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif

