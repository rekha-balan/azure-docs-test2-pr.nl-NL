---
title: Use Hadoop Pig with Remote Desktop in HDInsight - Azure
description: Learn how to use the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based Hadoop cluster in HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 01/17/2017
ms.author: jasonh
ROBOTS: NOINDEX
ms.openlocfilehash: 224722c61a653eae55bc1351e91e6288bc793fb6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855622"
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="92005-103">Run Pig jobs from a Remote Desktop connection</span><span class="sxs-lookup"><span data-stu-id="92005-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="92005-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="92005-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="92005-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span><span class="sxs-lookup"><span data-stu-id="92005-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92005-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span><span class="sxs-lookup"><span data-stu-id="92005-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="92005-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="92005-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="92005-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="92005-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="92005-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](apache-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span><span class="sxs-lookup"><span data-stu-id="92005-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](apache-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <a id="prereq"></a><span data-ttu-id="92005-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="92005-110">Prerequisites</span></span>
<span data-ttu-id="92005-111">To complete the steps in this article, you will need the following.</span><span class="sxs-lookup"><span data-stu-id="92005-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="92005-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span><span class="sxs-lookup"><span data-stu-id="92005-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="92005-113">A client computer running Windows 10, Windows 8, or Windows 7</span><span class="sxs-lookup"><span data-stu-id="92005-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <a id="connect"></a><span data-ttu-id="92005-114">Connect with Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="92005-114">Connect with Remote Desktop</span></span>
<span data-ttu-id="92005-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](../hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="92005-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](../hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <a id="pig"></a><span data-ttu-id="92005-116">Use the Pig command</span><span class="sxs-lookup"><span data-stu-id="92005-116">Use the Pig command</span></span>
1. <span data-ttu-id="92005-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span><span class="sxs-lookup"><span data-stu-id="92005-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="92005-118">Use the following to start the Pig command:</span><span class="sxs-lookup"><span data-stu-id="92005-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="92005-119">You will be presented with a `grunt>` prompt.</span><span class="sxs-lookup"><span data-stu-id="92005-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="92005-120">Enter the following statement:</span><span class="sxs-lookup"><span data-stu-id="92005-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="92005-121">This command loads the contents of the sample.log file into the LOGS file.</span><span class="sxs-lookup"><span data-stu-id="92005-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="92005-122">You can view the contents of the file by using the following command:</span><span class="sxs-lookup"><span data-stu-id="92005-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="92005-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span><span class="sxs-lookup"><span data-stu-id="92005-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="92005-124">You can use **DUMP** to view the data after the transformation.</span><span class="sxs-lookup"><span data-stu-id="92005-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="92005-125">In this case, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="92005-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="92005-126">Continue applying transformations by using the following statements.</span><span class="sxs-lookup"><span data-stu-id="92005-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="92005-127">Use `DUMP` to view the result of the transformation after each step.</span><span class="sxs-lookup"><span data-stu-id="92005-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="92005-128">Statement</span><span class="sxs-lookup"><span data-stu-id="92005-128">Statement</span></span></th><th><span data-ttu-id="92005-129">What it does</span><span class="sxs-lookup"><span data-stu-id="92005-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="92005-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="92005-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="92005-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="92005-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="92005-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="92005-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="92005-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="92005-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="92005-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="92005-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="92005-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span><span class="sxs-lookup"><span data-stu-id="92005-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="92005-136">This is stored into FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="92005-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="92005-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="92005-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="92005-138">Orders the log levels by count (descending,) and stores into RESULT</span><span class="sxs-lookup"><span data-stu-id="92005-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
</table>

6. <span data-ttu-id="92005-139">You can also save the results of a transformation by using the `STORE` statement.</span><span class="sxs-lookup"><span data-stu-id="92005-139">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="92005-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span><span class="sxs-lookup"><span data-stu-id="92005-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="92005-141">The data is stored in the specified directory in files named **part-nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="92005-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="92005-142">If the directory already exists, you will receive an error message.</span><span class="sxs-lookup"><span data-stu-id="92005-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
   
7. <span data-ttu-id="92005-143">To exit the grunt prompt, enter the following statement.</span><span class="sxs-lookup"><span data-stu-id="92005-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="92005-144">Pig Latin batch files</span><span class="sxs-lookup"><span data-stu-id="92005-144">Pig Latin batch files</span></span>
<span data-ttu-id="92005-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span><span class="sxs-lookup"><span data-stu-id="92005-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="92005-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span><span class="sxs-lookup"><span data-stu-id="92005-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="92005-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span><span class="sxs-lookup"><span data-stu-id="92005-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="92005-148">Use the following to run the **pigbatch.pig** file using the pig command.</span><span class="sxs-lookup"><span data-stu-id="92005-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="92005-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span><span class="sxs-lookup"><span data-stu-id="92005-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a><span data-ttu-id="92005-150">Summary</span><span class="sxs-lookup"><span data-stu-id="92005-150">Summary</span></span>
<span data-ttu-id="92005-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span><span class="sxs-lookup"><span data-stu-id="92005-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="92005-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="92005-152">Next steps</span></span>
<span data-ttu-id="92005-153">For general information about Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="92005-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="92005-154">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="92005-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="92005-155">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="92005-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="92005-156">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="92005-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="92005-157">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="92005-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
