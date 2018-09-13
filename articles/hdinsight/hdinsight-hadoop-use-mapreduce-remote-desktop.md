---
title: MapReduce and Remote Desktop with Hadoop in HDInsight | Microsoft Docs
description: Learn how to use Remote Desktop to connect to Hadoop on HDInsight and run MapReduce jobs.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 76e8fc27c87a427d7cb2527c2c53a5b463798610
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540896"
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="35e2e-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="35e2e-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="35e2e-104">In this article, you will learn how to connect to a Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using the Hadoop command.</span><span class="sxs-lookup"><span data-stu-id="35e2e-104">In this article, you will learn how to connect to a Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using the Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="35e2e-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="35e2e-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="35e2e-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="35e2e-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="35e2e-107">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="35e2e-107">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>
>
> <span data-ttu-id="35e2e-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting to the HDInsight cluster and running MapReduce jobs.</span><span class="sxs-lookup"><span data-stu-id="35e2e-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting to the HDInsight cluster and running MapReduce jobs.</span></span>

## <a id="prereq"></a><span data-ttu-id="35e2e-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="35e2e-109">Prerequisites</span></span>
<span data-ttu-id="35e2e-110">To complete the steps in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="35e2e-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="35e2e-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span><span class="sxs-lookup"><span data-stu-id="35e2e-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="35e2e-112">A client computer running Windows 10, Windows 8, or Windows 7</span><span class="sxs-lookup"><span data-stu-id="35e2e-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <a id="connect"></a><span data-ttu-id="35e2e-113">Connect with Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="35e2e-113">Connect with Remote Desktop</span></span>
<span data-ttu-id="35e2e-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="35e2e-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <a id="hadoop"></a><span data-ttu-id="35e2e-115">Use the Hadoop command</span><span class="sxs-lookup"><span data-stu-id="35e2e-115">Use the Hadoop command</span></span>
<span data-ttu-id="35e2e-116">When you are connected to the desktop for the HDInsight cluster, use the following steps to run a MapReduce job by using the Hadoop command:</span><span class="sxs-lookup"><span data-stu-id="35e2e-116">When you are connected to the desktop for the HDInsight cluster, use the following steps to run a MapReduce job by using the Hadoop command:</span></span>

1. <span data-ttu-id="35e2e-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span><span class="sxs-lookup"><span data-stu-id="35e2e-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span> <span data-ttu-id="35e2e-118">This opens a new command prompt in the **c:\apps\dist\hadoop-&lt;version number>** directory.</span><span class="sxs-lookup"><span data-stu-id="35e2e-118">This opens a new command prompt in the **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="35e2e-119">The version number changes as Hadoop is updated.</span><span class="sxs-lookup"><span data-stu-id="35e2e-119">The version number changes as Hadoop is updated.</span></span> <span data-ttu-id="35e2e-120">The **HADOOP_HOME** environment variable can be used to find the path.</span><span class="sxs-lookup"><span data-stu-id="35e2e-120">The **HADOOP_HOME** environment variable can be used to find the path.</span></span> <span data-ttu-id="35e2e-121">For example, `cd %HADOOP_HOME%` changes directories to the Hadoop directory, without requiring you to know the version number.</span><span class="sxs-lookup"><span data-stu-id="35e2e-121">For example, `cd %HADOOP_HOME%` changes directories to the Hadoop directory, without requiring you to know the version number.</span></span>
   >
   >
2. <span data-ttu-id="35e2e-122">To use the **Hadoop** command to run an example MapReduce job, use the following command:</span><span class="sxs-lookup"><span data-stu-id="35e2e-122">To use the **Hadoop** command to run an example MapReduce job, use the following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasbs:///example/data/gutenberg/davinci.txt wasbs:///example/data/WordCountOutput

    <span data-ttu-id="35e2e-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file in the current directory.</span><span class="sxs-lookup"><span data-stu-id="35e2e-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file in the current directory.</span></span> <span data-ttu-id="35e2e-124">As input, it uses the **wasbs://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasbs:///example/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="35e2e-124">As input, it uses the **wasbs://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasbs:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="35e2e-125">for more information about this MapReduce job and the example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="35e2e-125">for more information about this MapReduce job and the example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="35e2e-126">The job emits details as it is processed, and it returns information similar to the following when the job is complete:</span><span class="sxs-lookup"><span data-stu-id="35e2e-126">The job emits details as it is processed, and it returns information similar to the following when the job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="35e2e-127">When the job is complete, use the following command to list the output files stored at **wasbs://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="35e2e-127">When the job is complete, use the following command to list the output files stored at **wasbs://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasbs:///example/data/WordCountOutput

    <span data-ttu-id="35e2e-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="35e2e-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="35e2e-129">The **part-r-00000** file contains the output for this job.</span><span class="sxs-lookup"><span data-stu-id="35e2e-129">The **part-r-00000** file contains the output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="35e2e-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span><span class="sxs-lookup"><span data-stu-id="35e2e-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="35e2e-131">If so, use the ##### suffix to indicate the order of the files.</span><span class="sxs-lookup"><span data-stu-id="35e2e-131">If so, use the ##### suffix to indicate the order of the files.</span></span>
   >
   >
5. <span data-ttu-id="35e2e-132">To view the output, use the following command:</span><span class="sxs-lookup"><span data-stu-id="35e2e-132">To view the output, use the following command:</span></span>

        hadoop fs -cat wasbs:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="35e2e-133">This displays a list of the words that are contained in the **wasbs://example/data/gutenberg/davinci.txt** file, along with the number of times each word occured.</span><span class="sxs-lookup"><span data-stu-id="35e2e-133">This displays a list of the words that are contained in the **wasbs://example/data/gutenberg/davinci.txt** file, along with the number of times each word occured.</span></span> <span data-ttu-id="35e2e-134">The following is an example of the data that will be contained in the file:</span><span class="sxs-lookup"><span data-stu-id="35e2e-134">The following is an example of the data that will be contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a><span data-ttu-id="35e2e-135">Summary</span><span class="sxs-lookup"><span data-stu-id="35e2e-135">Summary</span></span>
<span data-ttu-id="35e2e-136">As you can see, the Hadoop command provides an easy way to run MapReduce jobs on an HDInsight cluster and then view the job output.</span><span class="sxs-lookup"><span data-stu-id="35e2e-136">As you can see, the Hadoop command provides an easy way to run MapReduce jobs on an HDInsight cluster and then view the job output.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="35e2e-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="35e2e-137">Next steps</span></span>
<span data-ttu-id="35e2e-138">For general information about MapReduce jobs in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="35e2e-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="35e2e-139">Use MapReduce on HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="35e2e-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="35e2e-140">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="35e2e-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="35e2e-141">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="35e2e-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="35e2e-142">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="35e2e-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
