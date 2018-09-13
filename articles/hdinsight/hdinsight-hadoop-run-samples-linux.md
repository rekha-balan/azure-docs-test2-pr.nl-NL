---
title: Run Hadoop MapReduce samples on HDInsight | Microsoft Docs
description: Get started using MapReduce samples with HDInsight. Use SSH to connect to the cluster, then use the Hadoop command to run sample jobs.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: larryfr
ms.openlocfilehash: 0d3983bfec41146b875897bb1cb8d96fa9207f3c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556713"
---
# <a name="run-the-hadoop-samples-in-hdinsight"></a><span data-ttu-id="4405d-104">Run the Hadoop samples in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4405d-104">Run the Hadoop samples in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="4405d-105">Learn about MapReduce examples that are included with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4405d-105">Learn about MapReduce examples that are included with HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4405d-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4405d-106">Prerequisites</span></span>

* <span data-ttu-id="4405d-107">**A Linux-based HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="4405d-107">**A Linux-based HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4405d-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="4405d-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4405d-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="4405d-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="4405d-110">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4405d-110">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-samples"></a><span data-ttu-id="4405d-111">The samples</span><span class="sxs-lookup"><span data-stu-id="4405d-111">The samples</span></span>

<span data-ttu-id="4405d-112">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="4405d-112">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="4405d-113">**Contents**: The following samples are contained in this archive:</span><span class="sxs-lookup"><span data-stu-id="4405d-113">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="4405d-114">**aggregatewordcount**: An Aggregate based map/reduce program that counts the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="4405d-114">**aggregatewordcount**: An Aggregate based map/reduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="4405d-115">**aggregatewordhist**: An Aggregate based map/reduce program that computes the histogram of the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="4405d-115">**aggregatewordhist**: An Aggregate based map/reduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="4405d-116">**bbp**: A map/reduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span><span class="sxs-lookup"><span data-stu-id="4405d-116">**bbp**: A map/reduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="4405d-117">**dbcount**: An example job that counts the pageview logs stored in a database.</span><span class="sxs-lookup"><span data-stu-id="4405d-117">**dbcount**: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="4405d-118">**distbbp**: A map/reduce program that uses a BBP-type formula to compute exact bits of Pi.</span><span class="sxs-lookup"><span data-stu-id="4405d-118">**distbbp**: A map/reduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="4405d-119">**grep**: A map/reduce program that counts the matches of a regex in the input.</span><span class="sxs-lookup"><span data-stu-id="4405d-119">**grep**: A map/reduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="4405d-120">**join**: A job that performs a join over sorted, equally partitioned datasets.</span><span class="sxs-lookup"><span data-stu-id="4405d-120">**join**: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="4405d-121">**multifilewc**: A job that counts words from several files.</span><span class="sxs-lookup"><span data-stu-id="4405d-121">**multifilewc**: A job that counts words from several files.</span></span>
* <span data-ttu-id="4405d-122">**pentomino**: A map/reduce tile laying program to find solutions to pentomino problems.</span><span class="sxs-lookup"><span data-stu-id="4405d-122">**pentomino**: A map/reduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="4405d-123">**pi**: A map/reduce program that estimates Pi using a quasi-Monte Carlo method.</span><span class="sxs-lookup"><span data-stu-id="4405d-123">**pi**: A map/reduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="4405d-124">**randomtextwriter**: A map/reduce program that writes 10GB of random textual data per node.</span><span class="sxs-lookup"><span data-stu-id="4405d-124">**randomtextwriter**: A map/reduce program that writes 10GB of random textual data per node.</span></span>
* <span data-ttu-id="4405d-125">**randomwriter**: A map/reduce program that writes 10GB of random data per node.</span><span class="sxs-lookup"><span data-stu-id="4405d-125">**randomwriter**: A map/reduce program that writes 10GB of random data per node.</span></span>
* <span data-ttu-id="4405d-126">**secondarysort**: An example defining a secondary sort to the reduce phase.</span><span class="sxs-lookup"><span data-stu-id="4405d-126">**secondarysort**: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="4405d-127">**sort**: A map/reduce program that sorts the data written by the random writer.</span><span class="sxs-lookup"><span data-stu-id="4405d-127">**sort**: A map/reduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="4405d-128">**sudoku**: A sudoku solver.</span><span class="sxs-lookup"><span data-stu-id="4405d-128">**sudoku**: A sudoku solver.</span></span>
* <span data-ttu-id="4405d-129">**teragen**: Generate data for the terasort.</span><span class="sxs-lookup"><span data-stu-id="4405d-129">**teragen**: Generate data for the terasort.</span></span>
* <span data-ttu-id="4405d-130">**terasort**: Run the terasort.</span><span class="sxs-lookup"><span data-stu-id="4405d-130">**terasort**: Run the terasort.</span></span>
* <span data-ttu-id="4405d-131">**teravalidate**: Checking results of terasort.</span><span class="sxs-lookup"><span data-stu-id="4405d-131">**teravalidate**: Checking results of terasort.</span></span>
* <span data-ttu-id="4405d-132">**wordcount**: A map/reduce program that counts the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="4405d-132">**wordcount**: A map/reduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="4405d-133">**wordmean**: A map/reduce program that counts the average length of the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="4405d-133">**wordmean**: A map/reduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="4405d-134">**wordmedian**: A map/reduce program that counts the median length of the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="4405d-134">**wordmedian**: A map/reduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="4405d-135">**wordstandarddeviation**: A map/reduce program that counts the standard deviation of the length of the words in the input files.</span><span class="sxs-lookup"><span data-stu-id="4405d-135">**wordstandarddeviation**: A map/reduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="4405d-136">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="4405d-136">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="4405d-137">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span><span class="sxs-lookup"><span data-stu-id="4405d-137">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="how-to-run-the-samples"></a><span data-ttu-id="4405d-138">How to run the samples</span><span class="sxs-lookup"><span data-stu-id="4405d-138">How to run the samples</span></span>

1. <span data-ttu-id="4405d-139">Connect to HDInsight using SSH.</span><span class="sxs-lookup"><span data-stu-id="4405d-139">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="4405d-140">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4405d-140">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4405d-141">From the `username@#######:~$` prompt, use the following command to list the samples:</span><span class="sxs-lookup"><span data-stu-id="4405d-141">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="4405d-142">This command generates the list of sample from the previous section of this document.</span><span class="sxs-lookup"><span data-stu-id="4405d-142">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="4405d-143">Use the following command to get help on a specific sample.</span><span class="sxs-lookup"><span data-stu-id="4405d-143">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="4405d-144">In this case, the **wordcount** sample:</span><span class="sxs-lookup"><span data-stu-id="4405d-144">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="4405d-145">You receive the following message:</span><span class="sxs-lookup"><span data-stu-id="4405d-145">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="4405d-146">This message indicates that you can provide several input paths for the source documents.</span><span class="sxs-lookup"><span data-stu-id="4405d-146">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="4405d-147">The final path is where the output (count of words in the source documents,) is stored.</span><span class="sxs-lookup"><span data-stu-id="4405d-147">The final path is where the output (count of words in the source documents,) is stored.</span></span>

4. <span data-ttu-id="4405d-148">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span><span class="sxs-lookup"><span data-stu-id="4405d-148">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="4405d-149">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="4405d-149">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="4405d-150">Output for this example is stored in `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="4405d-150">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="4405d-151">Both paths are located on default storage for the cluster, not the local file system.</span><span class="sxs-lookup"><span data-stu-id="4405d-151">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4405d-152">As noted in the help for the wordcount sample, you could also specify multiple input files.</span><span class="sxs-lookup"><span data-stu-id="4405d-152">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="4405d-153">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span><span class="sxs-lookup"><span data-stu-id="4405d-153">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="4405d-154">Once the job completes, use the following command to view the output:</span><span class="sxs-lookup"><span data-stu-id="4405d-154">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="4405d-155">This command concatenates all the output files produced by the job.</span><span class="sxs-lookup"><span data-stu-id="4405d-155">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="4405d-156">It displays the output to the console.</span><span class="sxs-lookup"><span data-stu-id="4405d-156">It displays the output to the console.</span></span> <span data-ttu-id="4405d-157">The output is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="4405d-157">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="4405d-158">Each line represents a word and how many times it occurred in the input data.</span><span class="sxs-lookup"><span data-stu-id="4405d-158">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="sudoku"></a><span data-ttu-id="4405d-159">Sudoku</span><span class="sxs-lookup"><span data-stu-id="4405d-159">Sudoku</span></span>

<span data-ttu-id="4405d-160">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span><span class="sxs-lookup"><span data-stu-id="4405d-160">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="4405d-161">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span><span class="sxs-lookup"><span data-stu-id="4405d-161">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="4405d-162">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span><span class="sxs-lookup"><span data-stu-id="4405d-162">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="4405d-163">So our input should be a file that is in the following format:</span><span class="sxs-lookup"><span data-stu-id="4405d-163">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="4405d-164">Nine rows of nine columns</span><span class="sxs-lookup"><span data-stu-id="4405d-164">Nine rows of nine columns</span></span>
* <span data-ttu-id="4405d-165">Each column can contain either a number or `?` (which indicates a blank cell)</span><span class="sxs-lookup"><span data-stu-id="4405d-165">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="4405d-166">Cells are separated by a space</span><span class="sxs-lookup"><span data-stu-id="4405d-166">Cells are separated by a space</span></span>

<span data-ttu-id="4405d-167">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span><span class="sxs-lookup"><span data-stu-id="4405d-167">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="4405d-168">There's an example on the HDInsight cluster that is properly constructed.</span><span class="sxs-lookup"><span data-stu-id="4405d-168">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="4405d-169">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span><span class="sxs-lookup"><span data-stu-id="4405d-169">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="4405d-170">To run this example problem through the Sudoku example, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4405d-170">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="4405d-171">The results appear similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="4405d-171">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi-"></a><span data-ttu-id="4405d-172">Pi (π)</span><span class="sxs-lookup"><span data-stu-id="4405d-172">Pi (π)</span></span>

<span data-ttu-id="4405d-173">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span><span class="sxs-lookup"><span data-stu-id="4405d-173">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="4405d-174">Points are placed at random in a unit square.</span><span class="sxs-lookup"><span data-stu-id="4405d-174">Points are placed at random in a unit square.</span></span> <span data-ttu-id="4405d-175">The square also contains a circle.</span><span class="sxs-lookup"><span data-stu-id="4405d-175">The square also contains a circle.</span></span> <span data-ttu-id="4405d-176">The probability that the points will fall within the circle are equal to the area of the circle, pi/4.</span><span class="sxs-lookup"><span data-stu-id="4405d-176">The probability that the points will fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="4405d-177">The value of pi can be estimated from the value of 4R, where R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span><span class="sxs-lookup"><span data-stu-id="4405d-177">The value of pi can be estimated from the value of 4R, where R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="4405d-178">The larger the sample of points used, the better the estimate is.</span><span class="sxs-lookup"><span data-stu-id="4405d-178">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="4405d-179">Use the following command to run this sample.</span><span class="sxs-lookup"><span data-stu-id="4405d-179">Use the following command to run this sample.</span></span> <span data-ttu-id="4405d-180">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span><span class="sxs-lookup"><span data-stu-id="4405d-180">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="4405d-181">The value returned by this should be similar to **3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="4405d-181">The value returned by this should be similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="4405d-182">For references, the first 10 decimal places of pi are 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="4405d-182">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10gb-greysort"></a><span data-ttu-id="4405d-183">10GB Greysort</span><span class="sxs-lookup"><span data-stu-id="4405d-183">10GB Greysort</span></span>

<span data-ttu-id="4405d-184">GraySort is a benchmark sort whose metric is the sort rate (TB/minute) that is achieved while sorting very large amounts of data, usually a 100 TB minimum.</span><span class="sxs-lookup"><span data-stu-id="4405d-184">GraySort is a benchmark sort whose metric is the sort rate (TB/minute) that is achieved while sorting very large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="4405d-185">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span><span class="sxs-lookup"><span data-stu-id="4405d-185">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="4405d-186">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy that won the annual general-purpose ("daytona") terabyte sort benchmark in 2009 with a rate of 0.578 TB/min (100 TB in 173 minutes).</span><span class="sxs-lookup"><span data-stu-id="4405d-186">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy that won the annual general-purpose ("daytona") terabyte sort benchmark in 2009 with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="4405d-187">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span><span class="sxs-lookup"><span data-stu-id="4405d-187">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="4405d-188">This sample uses three sets of MapReduce programs:</span><span class="sxs-lookup"><span data-stu-id="4405d-188">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="4405d-189">**TeraGen**: A MapReduce program that generates rows of data to sort</span><span class="sxs-lookup"><span data-stu-id="4405d-189">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="4405d-190">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span><span class="sxs-lookup"><span data-stu-id="4405d-190">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="4405d-191">TeraSort is a standard MapReduce sort, except for a custom partitioner that uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span><span class="sxs-lookup"><span data-stu-id="4405d-191">TeraSort is a standard MapReduce sort, except for a custom partitioner that uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="4405d-192">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span><span class="sxs-lookup"><span data-stu-id="4405d-192">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="4405d-193">This guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span><span class="sxs-lookup"><span data-stu-id="4405d-193">This guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="4405d-194">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span><span class="sxs-lookup"><span data-stu-id="4405d-194">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="4405d-195">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span><span class="sxs-lookup"><span data-stu-id="4405d-195">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="4405d-196">The map function generates records of the first and last keys of each file.</span><span class="sxs-lookup"><span data-stu-id="4405d-196">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="4405d-197">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span><span class="sxs-lookup"><span data-stu-id="4405d-197">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="4405d-198">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span><span class="sxs-lookup"><span data-stu-id="4405d-198">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="4405d-199">Use the following steps to generate data, sort, and then validate the output:</span><span class="sxs-lookup"><span data-stu-id="4405d-199">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="4405d-200">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="4405d-200">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="4405d-201">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span><span class="sxs-lookup"><span data-stu-id="4405d-201">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="4405d-202">The final two parameters instruct the job to create 10 GB worth of data and to store it at `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="4405d-202">The final two parameters instruct the job to create 10 GB worth of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="4405d-203">Use the following command to sort the data:</span><span class="sxs-lookup"><span data-stu-id="4405d-203">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="4405d-204">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span><span class="sxs-lookup"><span data-stu-id="4405d-204">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="4405d-205">The final two parameters are just the input and output locations for data.</span><span class="sxs-lookup"><span data-stu-id="4405d-205">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="4405d-206">Use the following to validate the data generated by the sort:</span><span class="sxs-lookup"><span data-stu-id="4405d-206">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="4405d-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="4405d-207">Next steps</span></span>

<span data-ttu-id="4405d-208">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="4405d-208">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="4405d-209">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="4405d-209">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="4405d-210">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="4405d-210">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="4405d-211">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="4405d-211">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="4405d-212">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="4405d-212">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-errors]: hdinsight-debug-jobs.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
