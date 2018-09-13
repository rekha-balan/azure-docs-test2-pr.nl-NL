---
title: MapReduce and SSH connection with Hadoop in HDInsight | Microsoft Docs
description: Learn how to use SSH to run MapReduce jobs using Hadoop on HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/08/2017
ms.author: larryfr
ms.openlocfilehash: fbf33ea6a6362857bf4bc92055cabd9b099a6d0c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550615"
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="8afd6-103">Use MapReduce with Hadoop on HDInsight with SSH</span><span class="sxs-lookup"><span data-stu-id="8afd6-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="8afd6-104">In this article, you learn how to use Secure Shell (SSH) to connect to a Hadoop on HDInsight cluster and then submit MapReduce jobs by using Hadoop commands.</span><span class="sxs-lookup"><span data-stu-id="8afd6-104">In this article, you learn how to use Secure Shell (SSH) to connect to a Hadoop on HDInsight cluster and then submit MapReduce jobs by using Hadoop commands.</span></span>

> [!NOTE]
> <span data-ttu-id="8afd6-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="8afd6-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <a id="prereq"></a><span data-ttu-id="8afd6-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8afd6-106">Prerequisites</span></span>

<span data-ttu-id="8afd6-107">To complete the steps in this article, you need the following:</span><span class="sxs-lookup"><span data-stu-id="8afd6-107">To complete the steps in this article, you need the following:</span></span>

* <span data-ttu-id="8afd6-108">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span><span class="sxs-lookup"><span data-stu-id="8afd6-108">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8afd6-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="8afd6-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8afd6-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="8afd6-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="8afd6-111">An SSH client.</span><span class="sxs-lookup"><span data-stu-id="8afd6-111">An SSH client.</span></span> <span data-ttu-id="8afd6-112">Linux, Unix, and Mac operating systems should come with an SSH client.</span><span class="sxs-lookup"><span data-stu-id="8afd6-112">Linux, Unix, and Mac operating systems should come with an SSH client.</span></span> <span data-ttu-id="8afd6-113">Windows users must download a client, such as [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="8afd6-113">Windows users must download a client, such as [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

## <a id="ssh"></a><span data-ttu-id="8afd6-114">Connect with SSH</span><span class="sxs-lookup"><span data-stu-id="8afd6-114">Connect with SSH</span></span>

<span data-ttu-id="8afd6-115">Connect to the fully qualified domain name (FQDN) of your HDInsight cluster by using the SSH command.</span><span class="sxs-lookup"><span data-stu-id="8afd6-115">Connect to the fully qualified domain name (FQDN) of your HDInsight cluster by using the SSH command.</span></span> <span data-ttu-id="8afd6-116">The FQDN is the name you gave the cluster, followed by **.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="8afd6-116">The FQDN is the name you gave the cluster, followed by **.azurehdinsight.net**.</span></span> <span data-ttu-id="8afd6-117">For example, the following would connect to a cluster named **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="8afd6-117">For example, the following would connect to a cluster named **myhdinsight**:</span></span>

    ssh admin@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="8afd6-118">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system, for example:</span><span class="sxs-lookup"><span data-stu-id="8afd6-118">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system, for example:</span></span>

    ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="8afd6-119">**If you provided a password for SSH authentication** when you created the HDInsight cluster, you need to provide the password when prompted.</span><span class="sxs-lookup"><span data-stu-id="8afd6-119">**If you provided a password for SSH authentication** when you created the HDInsight cluster, you need to provide the password when prompted.</span></span>

<span data-ttu-id="8afd6-120">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8afd6-120">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a id="hadoop"></a><span data-ttu-id="8afd6-121">Use Hadoop commands</span><span class="sxs-lookup"><span data-stu-id="8afd6-121">Use Hadoop commands</span></span>

1. <span data-ttu-id="8afd6-122">After you are connected to the HDInsight cluster, use the following **Hadoop** command to start a MapReduce job:</span><span class="sxs-lookup"><span data-stu-id="8afd6-122">After you are connected to the HDInsight cluster, use the following **Hadoop** command to start a MapReduce job:</span></span>

    ```
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="8afd6-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file.</span><span class="sxs-lookup"><span data-stu-id="8afd6-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file.</span></span> <span data-ttu-id="8afd6-124">As input, it uses the **/example/data/gutenberg/davinci.txt** document, and output is stored at **/example/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="8afd6-124">As input, it uses the **/example/data/gutenberg/davinci.txt** document, and output is stored at **/example/data/WordCountOutput**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8afd6-125">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="8afd6-125">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="8afd6-126">The job emits details as it processes, and it returns information similar to the following when the job completes:</span><span class="sxs-lookup"><span data-stu-id="8afd6-126">The job emits details as it processes, and it returns information similar to the following when the job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="8afd6-127">When the job completes, use the following command to list the output files that are stored at **wasbs://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="8afd6-127">When the job completes, use the following command to list the output files that are stored at **wasbs://example/data/WordCountOutput**:</span></span>

    ```
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="8afd6-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="8afd6-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="8afd6-129">The **part-r-00000** file contains the output for this job.</span><span class="sxs-lookup"><span data-stu-id="8afd6-129">The **part-r-00000** file contains the output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8afd6-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span><span class="sxs-lookup"><span data-stu-id="8afd6-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="8afd6-131">If so, use the ##### suffix to indicate the order of the files.</span><span class="sxs-lookup"><span data-stu-id="8afd6-131">If so, use the ##### suffix to indicate the order of the files.</span></span>

4. <span data-ttu-id="8afd6-132">To view the output, use the following command:</span><span class="sxs-lookup"><span data-stu-id="8afd6-132">To view the output, use the following command:</span></span>

    ```
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="8afd6-133">This displays a list of the words that are contained in the **wasbs://example/data/gutenberg/davinci.txt** file and the number of times each word occured.</span><span class="sxs-lookup"><span data-stu-id="8afd6-133">This displays a list of the words that are contained in the **wasbs://example/data/gutenberg/davinci.txt** file and the number of times each word occured.</span></span> <span data-ttu-id="8afd6-134">The following is an example of the data that is contained in the file:</span><span class="sxs-lookup"><span data-stu-id="8afd6-134">The following is an example of the data that is contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a><span data-ttu-id="8afd6-135">Summary</span><span class="sxs-lookup"><span data-stu-id="8afd6-135">Summary</span></span>

<span data-ttu-id="8afd6-136">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span><span class="sxs-lookup"><span data-stu-id="8afd6-136">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="8afd6-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="8afd6-137">Next steps</span></span>

<span data-ttu-id="8afd6-138">For general information about MapReduce jobs in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8afd6-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="8afd6-139">Use MapReduce on HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="8afd6-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="8afd6-140">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8afd6-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="8afd6-141">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8afd6-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="8afd6-142">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8afd6-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
