---
title: Use MapReduce and PowerShell with Hadoop | Microsoft Docs
description: Learn how to use PowerShell to remotely run MapReduce jobs with Hadoop on HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: larryfr
ms.openlocfilehash: 936212bf634a0245ea70318fcad703a87bf63c5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661895"
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="5b902-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b902-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="5b902-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5b902-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <a id="prereq"></a><span data-ttu-id="5b902-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5b902-105">Prerequisites</span></span>

* <span data-ttu-id="5b902-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span><span class="sxs-lookup"><span data-stu-id="5b902-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5b902-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="5b902-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5b902-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="5b902-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="5b902-109">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="5b902-109">**A workstation with Azure PowerShell**.</span></span>

## <a id="powershell"></a><span data-ttu-id="5b902-110">Run a MapReduce job using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b902-110">Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="5b902-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b902-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="5b902-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5b902-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="5b902-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5b902-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="5b902-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5b902-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="5b902-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span><span class="sxs-lookup"><span data-stu-id="5b902-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="5b902-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="5b902-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="5b902-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="5b902-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="5b902-118">It waits until the job completes or the wait time is exceeded.</span><span class="sxs-lookup"><span data-stu-id="5b902-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="5b902-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span><span class="sxs-lookup"><span data-stu-id="5b902-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="5b902-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5b902-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="5b902-121">Using an editor, save the following code as **mapreducejob.ps1**..</span><span class="sxs-lookup"><span data-stu-id="5b902-121">Using an editor, save the following code as **mapreducejob.ps1**..</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="5b902-122">Open a new **Azure PowerShell** command prompt.</span><span class="sxs-lookup"><span data-stu-id="5b902-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="5b902-123">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span><span class="sxs-lookup"><span data-stu-id="5b902-123">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="5b902-124">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="5b902-124">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="5b902-125">You may also be prompted to authenticate to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5b902-125">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="5b902-126">When the job completes, you receive output similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="5b902-126">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="5b902-127">This output indicates that the job completed successfully.</span><span class="sxs-lookup"><span data-stu-id="5b902-127">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5b902-128">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="5b902-128">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="5b902-129">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span><span class="sxs-lookup"><span data-stu-id="5b902-129">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="5b902-130">View output</span><span class="sxs-lookup"><span data-stu-id="5b902-130">View output</span></span>

<span data-ttu-id="5b902-131">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span><span class="sxs-lookup"><span data-stu-id="5b902-131">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="5b902-132">The output files of a MapReduce job are immutable.</span><span class="sxs-lookup"><span data-stu-id="5b902-132">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="5b902-133">So if you rerun this sample, you need to change the name of the output file.</span><span class="sxs-lookup"><span data-stu-id="5b902-133">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <a id="troubleshooting"></a><span data-ttu-id="5b902-134">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="5b902-134">Troubleshooting</span></span>

<span data-ttu-id="5b902-135">If no information is returned when the job completes, an error may have occurred during processing.</span><span class="sxs-lookup"><span data-stu-id="5b902-135">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="5b902-136">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span><span class="sxs-lookup"><span data-stu-id="5b902-136">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="5b902-137">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span><span class="sxs-lookup"><span data-stu-id="5b902-137">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <a id="summary"></a><span data-ttu-id="5b902-138">Summary</span><span class="sxs-lookup"><span data-stu-id="5b902-138">Summary</span></span>

<span data-ttu-id="5b902-139">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span><span class="sxs-lookup"><span data-stu-id="5b902-139">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="5b902-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b902-140">Next steps</span></span>

<span data-ttu-id="5b902-141">For general information about MapReduce jobs in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5b902-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="5b902-142">Use MapReduce on HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="5b902-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="5b902-143">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5b902-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5b902-144">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b902-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5b902-145">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="5b902-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
