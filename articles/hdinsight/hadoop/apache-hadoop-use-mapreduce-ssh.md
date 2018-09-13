---
title: MapReduce and SSH connection with Hadoop in HDInsight - Azure
description: Learn how to use SSH to run MapReduce jobs using Hadoop on HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/10/2018
ms.author: jasonh
ms.openlocfilehash: 71472edf74fba433f24b83362b2880575b73ce85
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868779"
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="936d8-103">Use MapReduce with Hadoop on HDInsight with SSH</span><span class="sxs-lookup"><span data-stu-id="936d8-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="936d8-104">Learn how to submit MapReduce jobs from a Secure Shell (SSH) connection to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="936d8-104">Learn how to submit MapReduce jobs from a Secure Shell (SSH) connection to HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="936d8-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](../hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="936d8-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](../hdinsight-hadoop-linux-information.md).</span></span>

## <a id="prereq"></a><span data-ttu-id="936d8-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="936d8-106">Prerequisites</span></span>

* <span data-ttu-id="936d8-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span><span class="sxs-lookup"><span data-stu-id="936d8-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="936d8-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="936d8-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="936d8-109">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="936d8-109">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="936d8-110">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="936d8-110">An SSH client.</span></span> <span data-ttu-id="936d8-111">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="936d8-111">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <a id="ssh"></a><span data-ttu-id="936d8-112">Connect with SSH</span><span class="sxs-lookup"><span data-stu-id="936d8-112">Connect with SSH</span></span>

<span data-ttu-id="936d8-113">Connect to the cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="936d8-113">Connect to the cluster using SSH.</span></span> <span data-ttu-id="936d8-114">For example, the following command connects to a cluster named **myhdinsight** as the **sshuser** account:</span><span class="sxs-lookup"><span data-stu-id="936d8-114">For example, the following command connects to a cluster named **myhdinsight** as the **sshuser** account:</span></span>

```bash
ssh sshuser@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="936d8-115">**If you use a certificate key for SSH authentication**, you may need to specify the location of the private key on your client system, for example:</span><span class="sxs-lookup"><span data-stu-id="936d8-115">**If you use a certificate key for SSH authentication**, you may need to specify the location of the private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key sshuser@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="936d8-116">**If you use a password for SSH authentication**, you need to provide the password when prompted.</span><span class="sxs-lookup"><span data-stu-id="936d8-116">**If you use a password for SSH authentication**, you need to provide the password when prompted.</span></span>

<span data-ttu-id="936d8-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="936d8-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a id="hadoop"></a><span data-ttu-id="936d8-118">Use Hadoop commands</span><span class="sxs-lookup"><span data-stu-id="936d8-118">Use Hadoop commands</span></span>

1. <span data-ttu-id="936d8-119">After you are connected to the HDInsight cluster, use the following command to start a MapReduce job:</span><span class="sxs-lookup"><span data-stu-id="936d8-119">After you are connected to the HDInsight cluster, use the following command to start a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="936d8-120">This command starts the `wordcount` class, which is contained in the `hadoop-mapreduce-examples.jar` file.</span><span class="sxs-lookup"><span data-stu-id="936d8-120">This command starts the `wordcount` class, which is contained in the `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="936d8-121">It uses the `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="936d8-121">It uses the `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="936d8-122">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="936d8-122">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="936d8-123">The job emits details as it processes, and it returns information similar to the following text when the job completes:</span><span class="sxs-lookup"><span data-stu-id="936d8-123">The job emits details as it processes, and it returns information similar to the following text when the job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="936d8-124">When the job completes, use the following command to list the output files:</span><span class="sxs-lookup"><span data-stu-id="936d8-124">When the job completes, use the following command to list the output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="936d8-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="936d8-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="936d8-126">The `part-r-00000` file contains the output for this job.</span><span class="sxs-lookup"><span data-stu-id="936d8-126">The `part-r-00000` file contains the output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="936d8-127">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span><span class="sxs-lookup"><span data-stu-id="936d8-127">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="936d8-128">If so, use the ##### suffix to indicate the order of the files.</span><span class="sxs-lookup"><span data-stu-id="936d8-128">If so, use the ##### suffix to indicate the order of the files.</span></span>

4. <span data-ttu-id="936d8-129">To view the output, use the following command:</span><span class="sxs-lookup"><span data-stu-id="936d8-129">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="936d8-130">This command displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file and the number of times each word occurred.</span><span class="sxs-lookup"><span data-stu-id="936d8-130">This command displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file and the number of times each word occurred.</span></span> <span data-ttu-id="936d8-131">The following text is an example of the data that is contained in the file:</span><span class="sxs-lookup"><span data-stu-id="936d8-131">The following text is an example of the data that is contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a><span data-ttu-id="936d8-132">Summary</span><span class="sxs-lookup"><span data-stu-id="936d8-132">Summary</span></span>

<span data-ttu-id="936d8-133">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span><span class="sxs-lookup"><span data-stu-id="936d8-133">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="936d8-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="936d8-134">Next steps</span></span>

<span data-ttu-id="936d8-135">For general information about MapReduce jobs in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="936d8-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="936d8-136">Use MapReduce on HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="936d8-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="936d8-137">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="936d8-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="936d8-138">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="936d8-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="936d8-139">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="936d8-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
