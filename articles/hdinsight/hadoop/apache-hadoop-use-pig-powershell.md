---
title: Use Hadoop Pig with PowerShell in HDInsight - Azure
description: Learn how to submit Pig jobs to a Hadoop cluster on HDInsight using Azure PowerShell.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: jasonh
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ff08e632c1bfd8eb4040e4e746ce08335eba8b08
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868555"
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="c7e46-103">Use Azure PowerShell to run Pig jobs with HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7e46-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="c7e46-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c7e46-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="c7e46-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span><span class="sxs-lookup"><span data-stu-id="c7e46-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="c7e46-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span><span class="sxs-lookup"><span data-stu-id="c7e46-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="c7e46-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="c7e46-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <a id="prereq"></a><span data-ttu-id="c7e46-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7e46-108">Prerequisites</span></span>

* <span data-ttu-id="c7e46-109">**An Azure HDInsight cluster**</span><span class="sxs-lookup"><span data-stu-id="c7e46-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c7e46-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="c7e46-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c7e46-111">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c7e46-111">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c7e46-112">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c7e46-112">**A workstation with Azure PowerShell**.</span></span>

## <a id="powershell"></a><span data-ttu-id="c7e46-113">Run a Pig job</span><span class="sxs-lookup"><span data-stu-id="c7e46-113">Run a Pig job</span></span>

<span data-ttu-id="c7e46-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7e46-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="c7e46-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c7e46-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="c7e46-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="c7e46-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="c7e46-117">**Connect-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription.</span><span class="sxs-lookup"><span data-stu-id="c7e46-117">**Connect-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription.</span></span>
* <span data-ttu-id="c7e46-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements.</span><span class="sxs-lookup"><span data-stu-id="c7e46-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements.</span></span>
* <span data-ttu-id="c7e46-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight and starts the job.</span><span class="sxs-lookup"><span data-stu-id="c7e46-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight and starts the job.</span></span> <span data-ttu-id="c7e46-120">A *job* object is returned.</span><span class="sxs-lookup"><span data-stu-id="c7e46-120">A *job* object is returned.</span></span>
* <span data-ttu-id="c7e46-121">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="c7e46-121">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="c7e46-122">It waits until the job has completed, or the wait time has been exceeded.</span><span class="sxs-lookup"><span data-stu-id="c7e46-122">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="c7e46-123">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span><span class="sxs-lookup"><span data-stu-id="c7e46-123">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="c7e46-124">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c7e46-124">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="c7e46-125">Using an editor, save the following code as **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="c7e46-125">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="c7e46-126">Open a new Windows PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="c7e46-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="c7e46-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span><span class="sxs-lookup"><span data-stu-id="c7e46-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="c7e46-128">You are prompted to log in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c7e46-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="c7e46-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c7e46-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="c7e46-130">When the job completes, it should return information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="c7e46-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a><span data-ttu-id="c7e46-131">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="c7e46-131">Troubleshooting</span></span>

<span data-ttu-id="c7e46-132">If no information is returned when the job completes, view the error logs.</span><span class="sxs-lookup"><span data-stu-id="c7e46-132">If no information is returned when the job completes, view the error logs.</span></span> <span data-ttu-id="c7e46-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span><span class="sxs-lookup"><span data-stu-id="c7e46-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="c7e46-134">This cmdlet returns the information that was written to STDERR during job processing.</span><span class="sxs-lookup"><span data-stu-id="c7e46-134">This cmdlet returns the information that was written to STDERR during job processing.</span></span>

## <a id="summary"></a><span data-ttu-id="c7e46-135">Summary</span><span class="sxs-lookup"><span data-stu-id="c7e46-135">Summary</span></span>
<span data-ttu-id="c7e46-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span><span class="sxs-lookup"><span data-stu-id="c7e46-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="c7e46-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7e46-137">Next steps</span></span>
<span data-ttu-id="c7e46-138">For general information about Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c7e46-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="c7e46-139">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7e46-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="c7e46-140">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c7e46-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c7e46-141">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7e46-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c7e46-142">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7e46-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
