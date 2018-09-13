---
title: Use MapReduce and PowerShell with Hadoop - Azure HDInsight
description: Learn how to use PowerShell to remotely run MapReduce jobs with Hadoop on HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: jasonh
ms.openlocfilehash: 5f2b6f11a611446ca13dff074b36a4040fb27d62
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966576"
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="c4c6f-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4c6f-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="c4c6f-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <a id="prereq"></a><span data-ttu-id="c4c6f-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c4c6f-105">Prerequisites</span></span>

* <span data-ttu-id="c4c6f-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span><span class="sxs-lookup"><span data-stu-id="c4c6f-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c4c6f-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c4c6f-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c4c6f-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c4c6f-109">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-109">**A workstation with Azure PowerShell**.</span></span>

## <a id="powershell"></a><span data-ttu-id="c4c6f-110">Run a MapReduce job</span><span class="sxs-lookup"><span data-stu-id="c4c6f-110">Run a MapReduce job</span></span>

<span data-ttu-id="c4c6f-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="c4c6f-112">Internally, PowerShell makes REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-112">Internally, PowerShell makes REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="c4c6f-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="c4c6f-114">**Connect-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-114">**Connect-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="c4c6f-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="c4c6f-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight and starts the job.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight and starts the job.</span></span> <span data-ttu-id="c4c6f-117">A *job* object is returned.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-117">A *job* object is returned.</span></span>

* <span data-ttu-id="c4c6f-118">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-118">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="c4c6f-119">It waits until the job completes or the wait time is exceeded.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-119">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="c4c6f-120">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-120">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="c4c6f-121">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-121">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="c4c6f-122">Using an editor, save the following code as **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-122">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="c4c6f-123">Open a new **Azure PowerShell** command prompt.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="c4c6f-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span><span class="sxs-lookup"><span data-stu-id="c4c6f-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="c4c6f-125">When you run the script, you are prompted for the name of the HDInsight cluster and the cluster login.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-125">When you run the script, you are prompted for the name of the HDInsight cluster and the cluster login.</span></span> <span data-ttu-id="c4c6f-126">You may also be prompted to authenticate to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="c4c6f-127">When the job completes, you receive output similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="c4c6f-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="c4c6f-128">This output indicates that the job completed successfully.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4c6f-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="c4c6f-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="c4c6f-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="c4c6f-131">View output</span><span class="sxs-lookup"><span data-stu-id="c4c6f-131">View output</span></span>

<span data-ttu-id="c4c6f-132">To see the words and counts produced by the job, open the **output.txt** file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-132">To see the words and counts produced by the job, open the **output.txt** file in a text editor.</span></span>

> [!NOTE]
> <span data-ttu-id="c4c6f-133">The output files of a MapReduce job are immutable.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="c4c6f-134">So if you rerun this sample, you need to change the name of the output file.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <a id="troubleshooting"></a><span data-ttu-id="c4c6f-135">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="c4c6f-135">Troubleshooting</span></span>

<span data-ttu-id="c4c6f-136">If no information is returned when the job completes, view errors for the job.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-136">If no information is returned when the job completes, view errors for the job.</span></span> <span data-ttu-id="c4c6f-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="c4c6f-138">This cmdlet returns the information that was written to STDERR as the job runs.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-138">This cmdlet returns the information that was written to STDERR as the job runs.</span></span>

## <a id="summary"></a><span data-ttu-id="c4c6f-139">Summary</span><span class="sxs-lookup"><span data-stu-id="c4c6f-139">Summary</span></span>

<span data-ttu-id="c4c6f-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span><span class="sxs-lookup"><span data-stu-id="c4c6f-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="c4c6f-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4c6f-141">Next steps</span></span>

<span data-ttu-id="c4c6f-142">For general information about MapReduce jobs in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c4c6f-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="c4c6f-143">Use MapReduce on HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="c4c6f-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c4c6f-144">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c4c6f-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c4c6f-145">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4c6f-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c4c6f-146">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4c6f-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
