---
title: Use Hadoop Pig with SSH on an HDInsight cluster | Microsoft Docs
description: Learn how connect to a Linux-based Hadoop cluster with SSH, and then use the Pig command to run Pig Latin statements interactively, or as a batch job.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: edda959693061850248ba97795c2390a592cbb21
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564635"
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="096b1-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span><span class="sxs-lookup"><span data-stu-id="096b1-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="096b1-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="096b1-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="096b1-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span><span class="sxs-lookup"><span data-stu-id="096b1-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="096b1-106">The steps in this document require a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="096b1-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="096b1-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="096b1-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="096b1-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="096b1-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a id="ssh"></a><span data-ttu-id="096b1-109">Connect with SSH</span><span class="sxs-lookup"><span data-stu-id="096b1-109">Connect with SSH</span></span>

<span data-ttu-id="096b1-110">Use SSH to connect to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="096b1-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="096b1-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="096b1-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="096b1-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span><span class="sxs-lookup"><span data-stu-id="096b1-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="096b1-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span><span class="sxs-lookup"><span data-stu-id="096b1-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span></span>

<span data-ttu-id="096b1-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="096b1-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a id="pig"></a><span data-ttu-id="096b1-115">Use the Pig command</span><span class="sxs-lookup"><span data-stu-id="096b1-115">Use the Pig command</span></span>

1. <span data-ttu-id="096b1-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span><span class="sxs-lookup"><span data-stu-id="096b1-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

        pig

    <span data-ttu-id="096b1-117">After a moment, you should see a `grunt>` prompt.</span><span class="sxs-lookup"><span data-stu-id="096b1-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="096b1-118">Enter the following statement:</span><span class="sxs-lookup"><span data-stu-id="096b1-118">Enter the following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="096b1-119">This command loads the contents of the sample.log file into LOGS.</span><span class="sxs-lookup"><span data-stu-id="096b1-119">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="096b1-120">You can view the contents of the file by using the following statement:</span><span class="sxs-lookup"><span data-stu-id="096b1-120">You can view the contents of the file by using the following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="096b1-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span><span class="sxs-lookup"><span data-stu-id="096b1-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="096b1-122">You can use **DUMP** to view the data after the transformation.</span><span class="sxs-lookup"><span data-stu-id="096b1-122">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="096b1-123">In this case, use `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="096b1-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="096b1-124">Continue applying transformations by using the statements in the following table:</span><span class="sxs-lookup"><span data-stu-id="096b1-124">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="096b1-125">Pig Latin statement</span><span class="sxs-lookup"><span data-stu-id="096b1-125">Pig Latin statement</span></span> | <span data-ttu-id="096b1-126">What the statement does</span><span class="sxs-lookup"><span data-stu-id="096b1-126">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="096b1-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="096b1-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="096b1-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="096b1-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="096b1-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span><span class="sxs-lookup"><span data-stu-id="096b1-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="096b1-130">The data set is stored into `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="096b1-130">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="096b1-131">Orders the log levels by count (descending) and stores into `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="096b1-131">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="096b1-132">Use `DUMP` to view the result of the transformation after each step.</span><span class="sxs-lookup"><span data-stu-id="096b1-132">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="096b1-133">You can also save the results of a transformation by using the `STORE` statement.</span><span class="sxs-lookup"><span data-stu-id="096b1-133">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="096b1-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span><span class="sxs-lookup"><span data-stu-id="096b1-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="096b1-135">The data is stored in the specified directory in files named `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="096b1-135">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="096b1-136">If the directory already exists, you receive an error.</span><span class="sxs-lookup"><span data-stu-id="096b1-136">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="096b1-137">To exit the grunt prompt, enter the following statement:</span><span class="sxs-lookup"><span data-stu-id="096b1-137">To exit the grunt prompt, enter the following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="096b1-138">Pig Latin batch files</span><span class="sxs-lookup"><span data-stu-id="096b1-138">Pig Latin batch files</span></span>

<span data-ttu-id="096b1-139">You can also use the Pig command to run Pig Latin contained in a file.</span><span class="sxs-lookup"><span data-stu-id="096b1-139">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="096b1-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="096b1-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="096b1-141">This file is created in the home directory for the SSH user account.</span><span class="sxs-lookup"><span data-stu-id="096b1-141">This file is created in the home directory for the SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="096b1-142">Type or paste the following lines, and then use Ctrl+D when finished.</span><span class="sxs-lookup"><span data-stu-id="096b1-142">Type or paste the following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="096b1-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span><span class="sxs-lookup"><span data-stu-id="096b1-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="096b1-144">Once the batch job finishes, you see the following output:</span><span class="sxs-lookup"><span data-stu-id="096b1-144">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a><span data-ttu-id="096b1-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="096b1-145">Next steps</span></span>

<span data-ttu-id="096b1-146">For general information on Pig in HDInsight, see the following document:</span><span class="sxs-lookup"><span data-stu-id="096b1-146">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="096b1-147">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="096b1-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="096b1-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="096b1-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="096b1-149">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="096b1-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="096b1-150">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="096b1-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
