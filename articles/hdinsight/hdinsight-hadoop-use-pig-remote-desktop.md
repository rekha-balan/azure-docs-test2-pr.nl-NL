---
title: Use Hadoop Pig with Remote Desktop in HDInsight | Microsoft Docs
description: Learn how to use the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based Hadoop cluster in HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 543483b08b32b7a280979502c5548702995f90af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662950"
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="e505a-103">Run Pig jobs from a Remote Desktop connection</span><span class="sxs-lookup"><span data-stu-id="e505a-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="e505a-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e505a-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="e505a-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span><span class="sxs-lookup"><span data-stu-id="e505a-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e505a-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span><span class="sxs-lookup"><span data-stu-id="e505a-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="e505a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="e505a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e505a-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="e505a-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>
>
> <span data-ttu-id="e505a-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span><span class="sxs-lookup"><span data-stu-id="e505a-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <a id="prereq"></a><span data-ttu-id="e505a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e505a-110">Prerequisites</span></span>
<span data-ttu-id="e505a-111">To complete the steps in this article, you will need the following.</span><span class="sxs-lookup"><span data-stu-id="e505a-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="e505a-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span><span class="sxs-lookup"><span data-stu-id="e505a-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="e505a-113">A client computer running Windows 10, Windows 8, or Windows 7</span><span class="sxs-lookup"><span data-stu-id="e505a-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <a id="connect"></a><span data-ttu-id="e505a-114">Connect with Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="e505a-114">Connect with Remote Desktop</span></span>
<span data-ttu-id="e505a-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="e505a-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <a id="pig"></a><span data-ttu-id="e505a-116">Use the Pig command</span><span class="sxs-lookup"><span data-stu-id="e505a-116">Use the Pig command</span></span>
1. <span data-ttu-id="e505a-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span><span class="sxs-lookup"><span data-stu-id="e505a-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="e505a-118">Use the following to start the Pig command:</span><span class="sxs-lookup"><span data-stu-id="e505a-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="e505a-119">You will be presented with a `grunt>` prompt.</span><span class="sxs-lookup"><span data-stu-id="e505a-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="e505a-120">Enter the following statement:</span><span class="sxs-lookup"><span data-stu-id="e505a-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasbs:///example/data/sample.log';

    <span data-ttu-id="e505a-121">This command loads the contents of the sample.log file into the LOGS file.</span><span class="sxs-lookup"><span data-stu-id="e505a-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="e505a-122">You can view the contents of the file by using the following command:</span><span class="sxs-lookup"><span data-stu-id="e505a-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="e505a-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span><span class="sxs-lookup"><span data-stu-id="e505a-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="e505a-124">You can use **DUMP** to view the data after the transformation.</span><span class="sxs-lookup"><span data-stu-id="e505a-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="e505a-125">In this case, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="e505a-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="e505a-126">Continue applying transformations by using the following statements.</span><span class="sxs-lookup"><span data-stu-id="e505a-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="e505a-127">Use `DUMP` to view the result of the transformation after each step.</span><span class="sxs-lookup"><span data-stu-id="e505a-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="e505a-128">Statement</span><span class="sxs-lookup"><span data-stu-id="e505a-128">Statement</span></span></th><th><span data-ttu-id="e505a-129">What it does</span><span class="sxs-lookup"><span data-stu-id="e505a-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="e505a-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="e505a-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="e505a-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="e505a-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e505a-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="e505a-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="e505a-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="e505a-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e505a-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="e505a-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="e505a-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span><span class="sxs-lookup"><span data-stu-id="e505a-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="e505a-136">This is stored into FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="e505a-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e505a-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="e505a-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="e505a-138">Orders the log levels by count (descending,) and stores into RESULT</span><span class="sxs-lookup"><span data-stu-id="e505a-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="e505a-139">
6. You can also save the results of a transformation by using the `STORE\` statement.</span><span class="sxs-lookup"><span data-stu-id="e505a-139">
6. You can also save the results of a transformation by using the `STORE\` statement.</span></span> <span data-ttu-id="e505a-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span><span class="sxs-lookup"><span data-stu-id="e505a-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasbs:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="e505a-141">The data is stored in the specified directory in files named **part-nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="e505a-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="e505a-142">If the directory already exists, you will receive an error message.</span><span class="sxs-lookup"><span data-stu-id="e505a-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="e505a-143">To exit the grunt prompt, enter the following statement.</span><span class="sxs-lookup"><span data-stu-id="e505a-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="e505a-144">Pig Latin batch files</span><span class="sxs-lookup"><span data-stu-id="e505a-144">Pig Latin batch files</span></span>
<span data-ttu-id="e505a-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span><span class="sxs-lookup"><span data-stu-id="e505a-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="e505a-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span><span class="sxs-lookup"><span data-stu-id="e505a-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="e505a-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span><span class="sxs-lookup"><span data-stu-id="e505a-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasbs:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="e505a-148">Use the following to run the **pigbatch.pig** file using the pig command.</span><span class="sxs-lookup"><span data-stu-id="e505a-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="e505a-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span><span class="sxs-lookup"><span data-stu-id="e505a-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a><span data-ttu-id="e505a-150">Summary</span><span class="sxs-lookup"><span data-stu-id="e505a-150">Summary</span></span>
<span data-ttu-id="e505a-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span><span class="sxs-lookup"><span data-stu-id="e505a-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="e505a-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="e505a-152">Next steps</span></span>
<span data-ttu-id="e505a-153">For general information about Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e505a-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="e505a-154">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e505a-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="e505a-155">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e505a-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="e505a-156">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e505a-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e505a-157">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e505a-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
