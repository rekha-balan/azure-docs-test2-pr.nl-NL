---
title: Run Hadoop MapReduce examples on HDInsight - Azure
description: Get started using MapReduce samples in jar files included in HDInsight. Use SSH to connect to the cluster, and then use the Hadoop command to run sample jobs.
keywords: hadoop example jar,hadoop examples jar,hadoop mapreduce examples,mapreduce examples
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: b0a4088a4473a731f9dec2d5f1e495b2eb9e937c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966533"
---
# <a name="run-the-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="8ed20-105">Run the MapReduce examples included in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ed20-105">Run the MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="8ed20-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ed20-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ed20-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8ed20-107">Prerequisites</span></span>

* <span data-ttu-id="8ed20-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](apache-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="8ed20-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](apache-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8ed20-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="8ed20-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8ed20-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8ed20-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="8ed20-111">**An SSH client**: For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8ed20-111">**An SSH client**: For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-mapreduce-examples"></a><span data-ttu-id="8ed20-112">The MapReduce examples</span><span class="sxs-lookup"><span data-stu-id="8ed20-112">The MapReduce examples</span></span>

<span data-ttu-id="8ed20-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="8ed20-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="8ed20-114">**Contents**: The following samples are contained in this archive:</span><span class="sxs-lookup"><span data-stu-id="8ed20-114">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="8ed20-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="8ed20-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="8ed20-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="8ed20-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="8ed20-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span><span class="sxs-lookup"><span data-stu-id="8ed20-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="8ed20-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span><span class="sxs-lookup"><span data-stu-id="8ed20-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="8ed20-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span><span class="sxs-lookup"><span data-stu-id="8ed20-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="8ed20-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span><span class="sxs-lookup"><span data-stu-id="8ed20-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="8ed20-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span><span class="sxs-lookup"><span data-stu-id="8ed20-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="8ed20-122">`multifilewc`: A job that counts words from several files.</span><span class="sxs-lookup"><span data-stu-id="8ed20-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="8ed20-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span><span class="sxs-lookup"><span data-stu-id="8ed20-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="8ed20-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span><span class="sxs-lookup"><span data-stu-id="8ed20-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="8ed20-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span><span class="sxs-lookup"><span data-stu-id="8ed20-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="8ed20-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span><span class="sxs-lookup"><span data-stu-id="8ed20-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="8ed20-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span><span class="sxs-lookup"><span data-stu-id="8ed20-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="8ed20-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span><span class="sxs-lookup"><span data-stu-id="8ed20-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="8ed20-129">`sudoku`: A sudoku solver.</span><span class="sxs-lookup"><span data-stu-id="8ed20-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="8ed20-130">`teragen`: Generate data for the terasort.</span><span class="sxs-lookup"><span data-stu-id="8ed20-130">`teragen`: Generate data for the terasort.</span></span>
* <span data-ttu-id="8ed20-131">`terasort`: Run the terasort.</span><span class="sxs-lookup"><span data-stu-id="8ed20-131">`terasort`: Run the terasort.</span></span>
* <span data-ttu-id="8ed20-132">`teravalidate`: Checking results of terasort.</span><span class="sxs-lookup"><span data-stu-id="8ed20-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="8ed20-133">`wordcount`: A mapreduce program that counts the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="8ed20-133">`wordcount`: A mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="8ed20-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="8ed20-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="8ed20-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="8ed20-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="8ed20-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="8ed20-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="8ed20-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/current/hadoop-client/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="8ed20-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/current/hadoop-client/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

## <a name="run-the-wordcount-example"></a><span data-ttu-id="8ed20-138">Run the wordcount example</span><span class="sxs-lookup"><span data-stu-id="8ed20-138">Run the wordcount example</span></span>

1. <span data-ttu-id="8ed20-139">Connect to HDInsight using SSH.</span><span class="sxs-lookup"><span data-stu-id="8ed20-139">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="8ed20-140">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8ed20-140">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="8ed20-141">From the `username@#######:~$` prompt, use the following command to list the samples:</span><span class="sxs-lookup"><span data-stu-id="8ed20-141">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="8ed20-142">This command generates the list of sample from the previous section of this document.</span><span class="sxs-lookup"><span data-stu-id="8ed20-142">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="8ed20-143">Use the following command to get help on a specific sample.</span><span class="sxs-lookup"><span data-stu-id="8ed20-143">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="8ed20-144">In this case, the **wordcount** sample:</span><span class="sxs-lookup"><span data-stu-id="8ed20-144">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="8ed20-145">You receive the following message:</span><span class="sxs-lookup"><span data-stu-id="8ed20-145">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="8ed20-146">This message indicates that you can provide several input paths for the source documents.</span><span class="sxs-lookup"><span data-stu-id="8ed20-146">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="8ed20-147">The final path is where the output (count of words in the source documents) is stored.</span><span class="sxs-lookup"><span data-stu-id="8ed20-147">The final path is where the output (count of words in the source documents) is stored.</span></span>

4. <span data-ttu-id="8ed20-148">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span><span class="sxs-lookup"><span data-stu-id="8ed20-148">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="8ed20-149">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="8ed20-149">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="8ed20-150">Output for this example is stored in `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="8ed20-150">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="8ed20-151">Both paths are located on default storage for the cluster, not the local file system.</span><span class="sxs-lookup"><span data-stu-id="8ed20-151">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8ed20-152">As noted in the help for the wordcount sample, you could also specify multiple input files.</span><span class="sxs-lookup"><span data-stu-id="8ed20-152">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="8ed20-153">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="8ed20-153">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="8ed20-154">Once the job completes, use the following command to view the output:</span><span class="sxs-lookup"><span data-stu-id="8ed20-154">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="8ed20-155">This command concatenates all the output files produced by the job.</span><span class="sxs-lookup"><span data-stu-id="8ed20-155">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="8ed20-156">It displays the output to the console.</span><span class="sxs-lookup"><span data-stu-id="8ed20-156">It displays the output to the console.</span></span> <span data-ttu-id="8ed20-157">The output is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="8ed20-157">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="8ed20-158">Each line represents a word and how many times it occurred in the input data.</span><span class="sxs-lookup"><span data-stu-id="8ed20-158">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="the-sudoku-example"></a><span data-ttu-id="8ed20-159">The Sudoku example</span><span class="sxs-lookup"><span data-stu-id="8ed20-159">The Sudoku example</span></span>

<span data-ttu-id="8ed20-160">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span><span class="sxs-lookup"><span data-stu-id="8ed20-160">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="8ed20-161">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span><span class="sxs-lookup"><span data-stu-id="8ed20-161">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="8ed20-162">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span><span class="sxs-lookup"><span data-stu-id="8ed20-162">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="8ed20-163">So our input should be a file that is in the following format:</span><span class="sxs-lookup"><span data-stu-id="8ed20-163">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="8ed20-164">Nine rows of nine columns</span><span class="sxs-lookup"><span data-stu-id="8ed20-164">Nine rows of nine columns</span></span>
* <span data-ttu-id="8ed20-165">Each column can contain either a number or `?` (which indicates a blank cell)</span><span class="sxs-lookup"><span data-stu-id="8ed20-165">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="8ed20-166">Cells are separated by a space</span><span class="sxs-lookup"><span data-stu-id="8ed20-166">Cells are separated by a space</span></span>

<span data-ttu-id="8ed20-167">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span><span class="sxs-lookup"><span data-stu-id="8ed20-167">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="8ed20-168">There's an example on the HDInsight cluster that is properly constructed.</span><span class="sxs-lookup"><span data-stu-id="8ed20-168">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="8ed20-169">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span><span class="sxs-lookup"><span data-stu-id="8ed20-169">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="8ed20-170">To run this example problem through the Sudoku example, use the following command:</span><span class="sxs-lookup"><span data-stu-id="8ed20-170">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="8ed20-171">The results appear similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="8ed20-171">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="8ed20-172">Pi (π) example</span><span class="sxs-lookup"><span data-stu-id="8ed20-172">Pi (π) example</span></span>

<span data-ttu-id="8ed20-173">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span><span class="sxs-lookup"><span data-stu-id="8ed20-173">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="8ed20-174">Points are placed at random in a unit square.</span><span class="sxs-lookup"><span data-stu-id="8ed20-174">Points are placed at random in a unit square.</span></span> <span data-ttu-id="8ed20-175">The square also contains a circle.</span><span class="sxs-lookup"><span data-stu-id="8ed20-175">The square also contains a circle.</span></span> <span data-ttu-id="8ed20-176">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span><span class="sxs-lookup"><span data-stu-id="8ed20-176">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="8ed20-177">The value of pi can be estimated from the value of 4R.</span><span class="sxs-lookup"><span data-stu-id="8ed20-177">The value of pi can be estimated from the value of 4R.</span></span> <span data-ttu-id="8ed20-178">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span><span class="sxs-lookup"><span data-stu-id="8ed20-178">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="8ed20-179">The larger the sample of points used, the better the estimate is.</span><span class="sxs-lookup"><span data-stu-id="8ed20-179">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="8ed20-180">Use the following command to run this sample.</span><span class="sxs-lookup"><span data-stu-id="8ed20-180">Use the following command to run this sample.</span></span> <span data-ttu-id="8ed20-181">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span><span class="sxs-lookup"><span data-stu-id="8ed20-181">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="8ed20-182">The value returned by this command is similar to **3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="8ed20-182">The value returned by this command is similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="8ed20-183">For references, the first 10 decimal places of pi are 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="8ed20-183">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="8ed20-184">10 GB Greysort example</span><span class="sxs-lookup"><span data-stu-id="8ed20-184">10 GB Greysort example</span></span>

<span data-ttu-id="8ed20-185">GraySort is a benchmark sort.</span><span class="sxs-lookup"><span data-stu-id="8ed20-185">GraySort is a benchmark sort.</span></span> <span data-ttu-id="8ed20-186">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span><span class="sxs-lookup"><span data-stu-id="8ed20-186">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="8ed20-187">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span><span class="sxs-lookup"><span data-stu-id="8ed20-187">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="8ed20-188">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span><span class="sxs-lookup"><span data-stu-id="8ed20-188">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="8ed20-189">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span><span class="sxs-lookup"><span data-stu-id="8ed20-189">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="8ed20-190">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span><span class="sxs-lookup"><span data-stu-id="8ed20-190">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="8ed20-191">This sample uses three sets of MapReduce programs:</span><span class="sxs-lookup"><span data-stu-id="8ed20-191">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="8ed20-192">**TeraGen**: A MapReduce program that generates rows of data to sort</span><span class="sxs-lookup"><span data-stu-id="8ed20-192">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="8ed20-193">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span><span class="sxs-lookup"><span data-stu-id="8ed20-193">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="8ed20-194">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span><span class="sxs-lookup"><span data-stu-id="8ed20-194">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="8ed20-195">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span><span class="sxs-lookup"><span data-stu-id="8ed20-195">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="8ed20-196">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span><span class="sxs-lookup"><span data-stu-id="8ed20-196">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="8ed20-197">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span><span class="sxs-lookup"><span data-stu-id="8ed20-197">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="8ed20-198">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span><span class="sxs-lookup"><span data-stu-id="8ed20-198">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="8ed20-199">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span><span class="sxs-lookup"><span data-stu-id="8ed20-199">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="8ed20-200">The map function generates records of the first and last keys of each file.</span><span class="sxs-lookup"><span data-stu-id="8ed20-200">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="8ed20-201">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span><span class="sxs-lookup"><span data-stu-id="8ed20-201">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="8ed20-202">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span><span class="sxs-lookup"><span data-stu-id="8ed20-202">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="8ed20-203">Use the following steps to generate data, sort, and then validate the output:</span><span class="sxs-lookup"><span data-stu-id="8ed20-203">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="8ed20-204">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="8ed20-204">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="8ed20-205">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span><span class="sxs-lookup"><span data-stu-id="8ed20-205">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="8ed20-206">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="8ed20-206">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="8ed20-207">Use the following command to sort the data:</span><span class="sxs-lookup"><span data-stu-id="8ed20-207">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="8ed20-208">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span><span class="sxs-lookup"><span data-stu-id="8ed20-208">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="8ed20-209">The final two parameters are just the input and output locations for data.</span><span class="sxs-lookup"><span data-stu-id="8ed20-209">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="8ed20-210">Use the following to validate the data generated by the sort:</span><span class="sxs-lookup"><span data-stu-id="8ed20-210">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="8ed20-211">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ed20-211">Next steps</span></span>

<span data-ttu-id="8ed20-212">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="8ed20-212">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="8ed20-213">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="8ed20-213">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* [<span data-ttu-id="8ed20-214">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ed20-214">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="8ed20-215">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ed20-215">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="8ed20-216">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ed20-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[hdinsight-introduction]:apache-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

