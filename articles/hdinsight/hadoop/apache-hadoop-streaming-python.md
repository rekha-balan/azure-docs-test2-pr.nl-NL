---
title: Develop Python streaming MapReduce jobs with HDInsight - Azure
description: Learn how to use Python in streaming MapReduce jobs. Hadoop provides a streaming API for MapReduce for writing in languages other than Java.
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 04/10/2018
ms.author: jasonh
ms.openlocfilehash: 8e2d13e0d9e51855bc8945db61c78a2fec736c33
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966349"
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="c8e7b-104">Develop Python streaming MapReduce programs for HDInsight</span><span class="sxs-lookup"><span data-stu-id="c8e7b-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="c8e7b-105">Learn how to use Python in streaming MapReduce operations.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="c8e7b-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="c8e7b-107">The steps in this document implement the Map and Reduce components in Python.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8e7b-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c8e7b-108">Prerequisites</span></span>

* <span data-ttu-id="c8e7b-109">A Linux-based Hadoop on HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="c8e7b-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c8e7b-110">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="c8e7b-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c8e7b-112">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c8e7b-112">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c8e7b-113">A text editor</span><span class="sxs-lookup"><span data-stu-id="c8e7b-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c8e7b-114">The text editor must use LF as the line ending.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="c8e7b-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="c8e7b-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="c8e7b-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="c8e7b-117">Word count</span><span class="sxs-lookup"><span data-stu-id="c8e7b-117">Word count</span></span>

<span data-ttu-id="c8e7b-118">This example is a basic word count implemented in a python a mapper and reducer.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="c8e7b-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="c8e7b-120">The following flowchart illustrates what happens during the map and reduce phases.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![illustration of the mapreduce process](./media/apache-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="c8e7b-122">Streaming MapReduce</span><span class="sxs-lookup"><span data-stu-id="c8e7b-122">Streaming MapReduce</span></span>

<span data-ttu-id="c8e7b-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="c8e7b-124">The specific requirements for the map and reduce logic are:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="c8e7b-125">**Input**: The map and reduce components must read input data from STDIN.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="c8e7b-126">**Output**: The map and reduce components must write output data to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="c8e7b-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="c8e7b-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="c8e7b-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="c8e7b-130">Create the mapper and reducer</span><span class="sxs-lookup"><span data-stu-id="c8e7b-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="c8e7b-131">Create a file named `mapper.py` and use the following code as the content:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="c8e7b-132">Create a file named **reducer.py** and use the following code as the content:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="c8e7b-133">Run using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8e7b-133">Run using PowerShell</span></span>

<span data-ttu-id="c8e7b-134">To ensure that your files have the right line endings, use the following PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

[!code-powershell[main](../../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="c8e7b-135">Use the following PowerShell script to upload the files, run the job, and view the output:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-135">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

[!code-powershell[main](../../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="c8e7b-136">Run from an SSH session</span><span class="sxs-lookup"><span data-stu-id="c8e7b-136">Run from an SSH session</span></span>

1. <span data-ttu-id="c8e7b-137">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-137">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="c8e7b-138">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-138">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="c8e7b-139">This command copies the files from the local system to the head node.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-139">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c8e7b-140">If you used a password to secure your SSH account, you are prompted for the password.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-140">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="c8e7b-141">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-141">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="c8e7b-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="c8e7b-143">Connect to the cluster by using SSH:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-143">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="c8e7b-144">For more information on, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c8e7b-144">For more information on, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="c8e7b-145">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-145">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="c8e7b-146">Use the following command to start the MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-146">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="c8e7b-147">This command has the following parts:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-147">This command has the following parts:</span></span>

   * <span data-ttu-id="c8e7b-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="c8e7b-149">It interfaces Hadoop with the external MapReduce code you provide.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-149">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="c8e7b-150">**-files**: Adds the specified files to the MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-150">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="c8e7b-151">**-mapper**: Tells Hadoop which file to use as the mapper.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-151">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="c8e7b-152">**-reducer**: Tells Hadoop which file to use as the reducer.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-152">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="c8e7b-153">**-input**: The input file that we should count words from.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-153">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="c8e7b-154">**-output**: The directory that the output is written to.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-154">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="c8e7b-155">As the MapReduce job works, the process is displayed as percentages.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-155">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="c8e7b-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="c8e7b-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="c8e7b-157">To view the output, use the following command:</span><span class="sxs-lookup"><span data-stu-id="c8e7b-157">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="c8e7b-158">This command displays a list of words and how many times the word occurred.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-158">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8e7b-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8e7b-159">Next steps</span></span>

<span data-ttu-id="c8e7b-160">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c8e7b-160">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="c8e7b-161">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="c8e7b-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c8e7b-162">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="c8e7b-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c8e7b-163">Use MapReduce jobs with HDInsight</span><span class="sxs-lookup"><span data-stu-id="c8e7b-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
