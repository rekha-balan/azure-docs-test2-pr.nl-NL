---
title: Use Hadoop Pig with PowerShell in HDInsight | Microsoft Docs
description: Learn how to submit Pig jobs to a Hadoop cluster on HDInsight using Azure PowerShell.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: dcc248d398f2e2aa0f563a0868e80b1e7ee6a3fb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550484"
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="20951-103">Use Azure PowerShell to run Pig jobs with HDInsight</span><span class="sxs-lookup"><span data-stu-id="20951-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="20951-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="20951-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="20951-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span><span class="sxs-lookup"><span data-stu-id="20951-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="20951-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span><span class="sxs-lookup"><span data-stu-id="20951-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="20951-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="20951-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <a id="prereq"></a><span data-ttu-id="20951-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="20951-108">Prerequisites</span></span>

* <span data-ttu-id="20951-109">**An Azure HDInsight cluster**</span><span class="sxs-lookup"><span data-stu-id="20951-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="20951-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="20951-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="20951-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="20951-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="20951-112">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="20951-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a><span data-ttu-id="20951-113">Run Pig jobs using PowerShell</span><span class="sxs-lookup"><span data-stu-id="20951-113">Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="20951-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="20951-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="20951-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="20951-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="20951-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="20951-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="20951-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="20951-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="20951-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span><span class="sxs-lookup"><span data-stu-id="20951-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="20951-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span><span class="sxs-lookup"><span data-stu-id="20951-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="20951-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="20951-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="20951-121">It waits until the job has completed, or the wait time has been exceeded.</span><span class="sxs-lookup"><span data-stu-id="20951-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="20951-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span><span class="sxs-lookup"><span data-stu-id="20951-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="20951-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="20951-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="20951-124">Using an editor, save the following code as **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="20951-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="20951-125">Open a new Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="20951-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="20951-126">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span><span class="sxs-lookup"><span data-stu-id="20951-126">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="20951-127">You are prompted to log in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="20951-127">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="20951-128">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="20951-128">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="20951-129">When the job completes, it should return information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="20951-129">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a><span data-ttu-id="20951-130">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="20951-130">Troubleshooting</span></span>

<span data-ttu-id="20951-131">If no information is returned when the job completes, an error may have occurred during processing.</span><span class="sxs-lookup"><span data-stu-id="20951-131">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="20951-132">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span><span class="sxs-lookup"><span data-stu-id="20951-132">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="20951-133">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span><span class="sxs-lookup"><span data-stu-id="20951-133">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <a id="summary"></a><span data-ttu-id="20951-134">Summary</span><span class="sxs-lookup"><span data-stu-id="20951-134">Summary</span></span>
<span data-ttu-id="20951-135">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span><span class="sxs-lookup"><span data-stu-id="20951-135">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="20951-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="20951-136">Next steps</span></span>
<span data-ttu-id="20951-137">For general information about Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="20951-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="20951-138">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="20951-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="20951-139">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="20951-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="20951-140">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="20951-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="20951-141">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="20951-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
