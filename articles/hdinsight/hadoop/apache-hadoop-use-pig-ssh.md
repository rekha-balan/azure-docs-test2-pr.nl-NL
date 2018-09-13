---
title: Use Hadoop Pig with SSH on an HDInsight cluster - Azure
description: Learn how connect to a Linux-based Hadoop cluster with SSH, and then use the Pig command to run Pig Latin statements interactively, or as a batch job.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/27/2018
ms.author: jasonh
ms.openlocfilehash: 4d380c44511ad330542402499829c19de62bd39a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856817"
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="7f03a-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span><span class="sxs-lookup"><span data-stu-id="7f03a-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="7f03a-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7f03a-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="7f03a-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span><span class="sxs-lookup"><span data-stu-id="7f03a-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f03a-106">The steps in this document require a Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7f03a-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7f03a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="7f03a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7f03a-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7f03a-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a id="ssh"></a><span data-ttu-id="7f03a-109">Connect with SSH</span><span class="sxs-lookup"><span data-stu-id="7f03a-109">Connect with SSH</span></span>

<span data-ttu-id="7f03a-110">Use SSH to connect to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7f03a-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="7f03a-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="7f03a-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

```bash
ssh sshuser@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="7f03a-112">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7f03a-112">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a id="pig"></a><span data-ttu-id="7f03a-113">Use the Pig command</span><span class="sxs-lookup"><span data-stu-id="7f03a-113">Use the Pig command</span></span>

1. <span data-ttu-id="7f03a-114">Once connected, start the Pig command-line interface (CLI) by using the following command:</span><span class="sxs-lookup"><span data-stu-id="7f03a-114">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

    ```bash
    pig
    ```

    <span data-ttu-id="7f03a-115">After a moment, the prompt changes to`grunt>`.</span><span class="sxs-lookup"><span data-stu-id="7f03a-115">After a moment, the prompt changes to`grunt>`.</span></span>

2. <span data-ttu-id="7f03a-116">Enter the following statement:</span><span class="sxs-lookup"><span data-stu-id="7f03a-116">Enter the following statement:</span></span>

    ```piglatin
    LOGS = LOAD '/example/data/sample.log';
    ```

    <span data-ttu-id="7f03a-117">This command loads the contents of the sample.log file into LOGS.</span><span class="sxs-lookup"><span data-stu-id="7f03a-117">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="7f03a-118">You can view the contents of the file by using the following statement:</span><span class="sxs-lookup"><span data-stu-id="7f03a-118">You can view the contents of the file by using the following statement:</span></span>

    ```piglatin
    DUMP LOGS;
    ```

3. <span data-ttu-id="7f03a-119">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span><span class="sxs-lookup"><span data-stu-id="7f03a-119">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

    ```piglatin
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    ```

    <span data-ttu-id="7f03a-120">You can use **DUMP** to view the data after the transformation.</span><span class="sxs-lookup"><span data-stu-id="7f03a-120">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="7f03a-121">In this case, use `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="7f03a-121">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="7f03a-122">Continue applying transformations by using the statements in the following table:</span><span class="sxs-lookup"><span data-stu-id="7f03a-122">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="7f03a-123">Pig Latin statement</span><span class="sxs-lookup"><span data-stu-id="7f03a-123">Pig Latin statement</span></span> | <span data-ttu-id="7f03a-124">What the statement does</span><span class="sxs-lookup"><span data-stu-id="7f03a-124">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="7f03a-125">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="7f03a-125">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="7f03a-126">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="7f03a-126">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="7f03a-127">Creates a set of data that contains each unique log level value and how many times it occurs.</span><span class="sxs-lookup"><span data-stu-id="7f03a-127">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="7f03a-128">The data set is stored into `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="7f03a-128">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="7f03a-129">Orders the log levels by count (descending) and stores into `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="7f03a-129">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="7f03a-130">Use `DUMP` to view the result of the transformation after each step.</span><span class="sxs-lookup"><span data-stu-id="7f03a-130">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="7f03a-131">You can also save the results of a transformation by using the `STORE` statement.</span><span class="sxs-lookup"><span data-stu-id="7f03a-131">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="7f03a-132">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span><span class="sxs-lookup"><span data-stu-id="7f03a-132">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

    ```piglatin
    STORE RESULT into '/example/data/pigout';
    ```

   > [!NOTE]
   > <span data-ttu-id="7f03a-133">The data is stored in the specified directory in files named `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="7f03a-133">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="7f03a-134">If the directory already exists, you receive an error.</span><span class="sxs-lookup"><span data-stu-id="7f03a-134">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="7f03a-135">To exit the grunt prompt, enter the following statement:</span><span class="sxs-lookup"><span data-stu-id="7f03a-135">To exit the grunt prompt, enter the following statement:</span></span>

    ```piglatin
    QUIT;
    ```

### <a name="pig-latin-batch-files"></a><span data-ttu-id="7f03a-136">Pig Latin batch files</span><span class="sxs-lookup"><span data-stu-id="7f03a-136">Pig Latin batch files</span></span>

<span data-ttu-id="7f03a-137">You can also use the Pig command to run Pig Latin contained in a file.</span><span class="sxs-lookup"><span data-stu-id="7f03a-137">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="7f03a-138">After exiting the grunt prompt, use the following command to create file named `pigbatch.pig`:</span><span class="sxs-lookup"><span data-stu-id="7f03a-138">After exiting the grunt prompt, use the following command to create file named `pigbatch.pig`:</span></span>

    ```bash
    nano ~/pigbatch.pig
    ```

2. <span data-ttu-id="7f03a-139">Type or paste the following lines:</span><span class="sxs-lookup"><span data-stu-id="7f03a-139">Type or paste the following lines:</span></span>

    ```piglatin
    LOGS = LOAD '/example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;
    ```

    <span data-ttu-id="7f03a-140">When finished, use __Ctrl__ + __X__, __Y__, and then __Enter__ to save the file.</span><span class="sxs-lookup"><span data-stu-id="7f03a-140">When finished, use __Ctrl__ + __X__, __Y__, and then __Enter__ to save the file.</span></span>

3. <span data-ttu-id="7f03a-141">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span><span class="sxs-lookup"><span data-stu-id="7f03a-141">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

    ```bash
    pig ~/pigbatch.pig
    ```

    <span data-ttu-id="7f03a-142">Once the batch job finishes, you see the following output:</span><span class="sxs-lookup"><span data-stu-id="7f03a-142">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a><span data-ttu-id="7f03a-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f03a-143">Next steps</span></span>

<span data-ttu-id="7f03a-144">For general information on Pig in HDInsight, see the following document:</span><span class="sxs-lookup"><span data-stu-id="7f03a-144">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="7f03a-145">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f03a-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="7f03a-146">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="7f03a-146">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="7f03a-147">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f03a-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7f03a-148">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f03a-148">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
