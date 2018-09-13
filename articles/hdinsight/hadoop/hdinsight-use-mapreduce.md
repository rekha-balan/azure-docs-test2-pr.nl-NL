---
title: MapReduce with Hadoop on HDInsight
description: Learn how to run MapReduce jobs on Hadoop in HDInsight clusters.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.openlocfilehash: 3b9cc70a1adc55850923f2313f17be435257117d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867459"
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="b0730-103">Use MapReduce in Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0730-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="b0730-104">Learn how to run MapReduce jobs on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="b0730-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="b0730-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b0730-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="b0730-106">**Use this**...</span><span class="sxs-lookup"><span data-stu-id="b0730-106">**Use this**...</span></span> | <span data-ttu-id="b0730-107">**...to do this**</span><span class="sxs-lookup"><span data-stu-id="b0730-107">**...to do this**</span></span> | <span data-ttu-id="b0730-108">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="b0730-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="b0730-109">...from this **client operating system**</span><span class="sxs-lookup"><span data-stu-id="b0730-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="b0730-110">SSH</span><span class="sxs-lookup"><span data-stu-id="b0730-110">SSH</span></span>](apache-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="b0730-111">Use the Hadoop command through **SSH**</span><span class="sxs-lookup"><span data-stu-id="b0730-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="b0730-112">Linux</span><span class="sxs-lookup"><span data-stu-id="b0730-112">Linux</span></span> |<span data-ttu-id="b0730-113">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="b0730-114">REST</span><span class="sxs-lookup"><span data-stu-id="b0730-114">REST</span></span>](apache-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="b0730-115">Submit the job remotely by using **REST** (examples use cURL)</span><span class="sxs-lookup"><span data-stu-id="b0730-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="b0730-116">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-116">Linux or Windows</span></span> |<span data-ttu-id="b0730-117">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="b0730-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0730-118">Windows PowerShell</span></span>](apache-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="b0730-119">Submit the job remotely by using **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b0730-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="b0730-120">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-120">Linux or Windows</span></span> |<span data-ttu-id="b0730-121">Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-121">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="b0730-122">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="b0730-122">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b0730-123">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b0730-123">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>

## <a id="whatis"></a><span data-ttu-id="b0730-124">What is MapReduce</span><span class="sxs-lookup"><span data-stu-id="b0730-124">What is MapReduce</span></span>

<span data-ttu-id="b0730-125">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span><span class="sxs-lookup"><span data-stu-id="b0730-125">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="b0730-126">Input data is split into independent chunks.</span><span class="sxs-lookup"><span data-stu-id="b0730-126">Input data is split into independent chunks.</span></span> <span data-ttu-id="b0730-127">Each chunk is processed in parallel across the nodes in your cluster.</span><span class="sxs-lookup"><span data-stu-id="b0730-127">Each chunk is processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="b0730-128">A MapReduce job consists of two functions:</span><span class="sxs-lookup"><span data-stu-id="b0730-128">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="b0730-129">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span><span class="sxs-lookup"><span data-stu-id="b0730-129">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="b0730-130">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span><span class="sxs-lookup"><span data-stu-id="b0730-130">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="b0730-131">A basic word count MapReduce job example is illustrated in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="b0730-131">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="b0730-133">The output of this job is a count of how many times each word occurred in the text.</span><span class="sxs-lookup"><span data-stu-id="b0730-133">The output of this job is a count of how many times each word occurred in the text.</span></span>

* <span data-ttu-id="b0730-134">The mapper takes each line from the input text as an input and breaks it into words.</span><span class="sxs-lookup"><span data-stu-id="b0730-134">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="b0730-135">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span><span class="sxs-lookup"><span data-stu-id="b0730-135">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="b0730-136">The output is sorted before sending it to reducer.</span><span class="sxs-lookup"><span data-stu-id="b0730-136">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="b0730-137">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span><span class="sxs-lookup"><span data-stu-id="b0730-137">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="b0730-138">MapReduce can be implemented in various languages.</span><span class="sxs-lookup"><span data-stu-id="b0730-138">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="b0730-139">Java is the most common implementation, and is used for demonstration purposes in this document.</span><span class="sxs-lookup"><span data-stu-id="b0730-139">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="b0730-140">Development languages</span><span class="sxs-lookup"><span data-stu-id="b0730-140">Development languages</span></span>

<span data-ttu-id="b0730-141">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="b0730-141">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="b0730-142">The example used in this document is a Java MapReduce application.</span><span class="sxs-lookup"><span data-stu-id="b0730-142">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="b0730-143">Non-Java languages, such as C#, Python, or standalone executables, must use **Hadoop streaming**.</span><span class="sxs-lookup"><span data-stu-id="b0730-143">Non-Java languages, such as C#, Python, or standalone executables, must use **Hadoop streaming**.</span></span>

<span data-ttu-id="b0730-144">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span><span class="sxs-lookup"><span data-stu-id="b0730-144">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="b0730-145">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="b0730-145">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="b0730-146">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span><span class="sxs-lookup"><span data-stu-id="b0730-146">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="b0730-147">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="b0730-147">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="b0730-148">For examples of using Hadoop streaming with HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="b0730-148">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="b0730-149">Develop C# MapReduce jobs</span><span class="sxs-lookup"><span data-stu-id="b0730-149">Develop C# MapReduce jobs</span></span>](apache-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="b0730-150">Develop Python MapReduce jobs</span><span class="sxs-lookup"><span data-stu-id="b0730-150">Develop Python MapReduce jobs</span></span>](apache-hadoop-streaming-python.md)

## <a id="data"></a><span data-ttu-id="b0730-151">Example data</span><span class="sxs-lookup"><span data-stu-id="b0730-151">Example data</span></span>

<span data-ttu-id="b0730-152">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span><span class="sxs-lookup"><span data-stu-id="b0730-152">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="b0730-153">These directories are in the default storage for your cluster.</span><span class="sxs-lookup"><span data-stu-id="b0730-153">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="b0730-154">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span><span class="sxs-lookup"><span data-stu-id="b0730-154">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="b0730-155">This file contains the notebooks of Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="b0730-155">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <a id="job"></a><span data-ttu-id="b0730-156">Example MapReduce</span><span class="sxs-lookup"><span data-stu-id="b0730-156">Example MapReduce</span></span>

<span data-ttu-id="b0730-157">An example MapReduce word count application is included with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b0730-157">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="b0730-158">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span><span class="sxs-lookup"><span data-stu-id="b0730-158">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="b0730-159">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span><span class="sxs-lookup"><span data-stu-id="b0730-159">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="b0730-160">For instructions to write your own MapReduce applications, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="b0730-160">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="b0730-161">Develop Java MapReduce applications for HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0730-161">Develop Java MapReduce applications for HDInsight</span></span>](apache-hadoop-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="b0730-162">Develop Python MapReduce applications for HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0730-162">Develop Python MapReduce applications for HDInsight</span></span>](apache-hadoop-streaming-python.md)

## <a id="run"></a><span data-ttu-id="b0730-163">Run the MapReduce</span><span class="sxs-lookup"><span data-stu-id="b0730-163">Run the MapReduce</span></span>

<span data-ttu-id="b0730-164">HDInsight can run HiveQL jobs by using various methods.</span><span class="sxs-lookup"><span data-stu-id="b0730-164">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="b0730-165">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span><span class="sxs-lookup"><span data-stu-id="b0730-165">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="b0730-166">**Use this**...</span><span class="sxs-lookup"><span data-stu-id="b0730-166">**Use this**...</span></span> | <span data-ttu-id="b0730-167">**...to do this**</span><span class="sxs-lookup"><span data-stu-id="b0730-167">**...to do this**</span></span> | <span data-ttu-id="b0730-168">...with this **cluster operating system**</span><span class="sxs-lookup"><span data-stu-id="b0730-168">...with this **cluster operating system**</span></span> | <span data-ttu-id="b0730-169">...from this **client operating system**</span><span class="sxs-lookup"><span data-stu-id="b0730-169">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="b0730-170">SSH</span><span class="sxs-lookup"><span data-stu-id="b0730-170">SSH</span></span>](apache-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="b0730-171">Use the Hadoop command through **SSH**</span><span class="sxs-lookup"><span data-stu-id="b0730-171">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="b0730-172">Linux</span><span class="sxs-lookup"><span data-stu-id="b0730-172">Linux</span></span> |<span data-ttu-id="b0730-173">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-173">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="b0730-174">Curl</span><span class="sxs-lookup"><span data-stu-id="b0730-174">Curl</span></span>](apache-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="b0730-175">Submit the job remotely by using **REST**</span><span class="sxs-lookup"><span data-stu-id="b0730-175">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="b0730-176">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-176">Linux or Windows</span></span> |<span data-ttu-id="b0730-177">Linux, Unix, Mac OS X, or Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-177">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="b0730-178">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0730-178">Windows PowerShell</span></span>](apache-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="b0730-179">Submit the job remotely by using **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b0730-179">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="b0730-180">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-180">Linux or Windows</span></span> |<span data-ttu-id="b0730-181">Windows</span><span class="sxs-lookup"><span data-stu-id="b0730-181">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="b0730-182">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="b0730-182">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b0730-183">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b0730-183">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a id="nextsteps"></a><span data-ttu-id="b0730-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0730-184">Next steps</span></span>

<span data-ttu-id="b0730-185">To learn more about working with data in HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="b0730-185">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="b0730-186">Develop Java MapReduce programs for HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0730-186">Develop Java MapReduce programs for HDInsight</span></span>](apache-hadoop-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="b0730-187">Develop Python streaming MapReduce programs for HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0730-187">Develop Python streaming MapReduce programs for HDInsight</span></span>](apache-hadoop-streaming-python.md)

* <span data-ttu-id="b0730-188">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="b0730-188">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="b0730-189">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="b0730-189">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]:apache-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: apache-hadoop-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]:../hdinsight-use-hive.md
[hdinsight-use-pig]:hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
