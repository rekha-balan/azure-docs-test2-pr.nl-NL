---
title: Microsoft Genomics:Troubleshooting Guide | Microsoft Docs
titleSuffix: Azure
description: Learn more about troubleshooting strategies
keywords: troubleshooting, error, debugging
services: microsoft-genomics
author: grhuynh
manager: jhubbard
editor: jasonwhowell
ms.author: grhuynh
ms.service: microsoft-genomics
ms.workload: genomics
ms.topic: article
ms.date: 07/18/2018
ms.openlocfilehash: 9bd1690003fd37b6c2edd0f0421cf8d0e74f8cb5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856687"
---
# <a name="troubleshooting-guide"></a><span data-ttu-id="d7f47-104">Troubleshooting guide</span><span class="sxs-lookup"><span data-stu-id="d7f47-104">Troubleshooting guide</span></span>
<span data-ttu-id="d7f47-105">This overview describes strategies to address common issues when using the Microsoft Genomics service.</span><span class="sxs-lookup"><span data-stu-id="d7f47-105">This overview describes strategies to address common issues when using the Microsoft Genomics service.</span></span> <span data-ttu-id="d7f47-106">For general FAQ, see [Common questions](frequently-asked-questions-genomics.md).</span><span class="sxs-lookup"><span data-stu-id="d7f47-106">For general FAQ, see [Common questions](frequently-asked-questions-genomics.md).</span></span> 


## <a name="how-do-i-check-my-job-status"></a><span data-ttu-id="d7f47-107">How do I check my job status?</span><span class="sxs-lookup"><span data-stu-id="d7f47-107">How do I check my job status?</span></span>
<span data-ttu-id="d7f47-108">You can check the status of your workflow by calling `msgen status` from the command line, as shown.</span><span class="sxs-lookup"><span data-stu-id="d7f47-108">You can check the status of your workflow by calling `msgen status` from the command line, as shown.</span></span> 

```
msgen status -u URL -k KEY -w ID [-f CONFIG] 
```

<span data-ttu-id="d7f47-109">There are three required arguments:</span><span class="sxs-lookup"><span data-stu-id="d7f47-109">There are three required arguments:</span></span>
* <span data-ttu-id="d7f47-110">URL - the base URI for the API</span><span class="sxs-lookup"><span data-stu-id="d7f47-110">URL - the base URI for the API</span></span>
* <span data-ttu-id="d7f47-111">KEY - the access key for your Genomics account.</span><span class="sxs-lookup"><span data-stu-id="d7f47-111">KEY - the access key for your Genomics account.</span></span> 
* <span data-ttu-id="d7f47-112">ID - the workflow ID</span><span class="sxs-lookup"><span data-stu-id="d7f47-112">ID - the workflow ID</span></span>

<span data-ttu-id="d7f47-113">To find your URL and KEY, go to Azure portal and open your Genomics account page.</span><span class="sxs-lookup"><span data-stu-id="d7f47-113">To find your URL and KEY, go to Azure portal and open your Genomics account page.</span></span> <span data-ttu-id="d7f47-114">Under the **Management** heading, choose **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="d7f47-114">Under the **Management** heading, choose **Access keys**.</span></span> <span data-ttu-id="d7f47-115">There, you find both the API URL and your access keys.</span><span class="sxs-lookup"><span data-stu-id="d7f47-115">There, you find both the API URL and your access keys.</span></span>

<span data-ttu-id="d7f47-116">Alternatively, you can include the path to the config file instead of directly entering the URL and KEY.</span><span class="sxs-lookup"><span data-stu-id="d7f47-116">Alternatively, you can include the path to the config file instead of directly entering the URL and KEY.</span></span> <span data-ttu-id="d7f47-117">Note that if you include these arguments in the command line as well as the config file, the command-line arguments will take precedence.</span><span class="sxs-lookup"><span data-stu-id="d7f47-117">Note that if you include these arguments in the command line as well as the config file, the command-line arguments will take precedence.</span></span> 

<span data-ttu-id="d7f47-118">After calling `msgen status`, a user-friendly message will be displayed, describing whether the workflow succeeded or giving a reason for the job failure.</span><span class="sxs-lookup"><span data-stu-id="d7f47-118">After calling `msgen status`, a user-friendly message will be displayed, describing whether the workflow succeeded or giving a reason for the job failure.</span></span> 


## <a name="get-more-information-about-my-workflow-status"></a><span data-ttu-id="d7f47-119">Get more information about my workflow status</span><span class="sxs-lookup"><span data-stu-id="d7f47-119">Get more information about my workflow status</span></span>

<span data-ttu-id="d7f47-120">To get more information about why a job might not have succeeded, you can explore the log files produced during the workflow.</span><span class="sxs-lookup"><span data-stu-id="d7f47-120">To get more information about why a job might not have succeeded, you can explore the log files produced during the workflow.</span></span> <span data-ttu-id="d7f47-121">In your output container, you should see a `[youroutputfilename].logs.zip` folder.</span><span class="sxs-lookup"><span data-stu-id="d7f47-121">In your output container, you should see a `[youroutputfilename].logs.zip` folder.</span></span>  <span data-ttu-id="d7f47-122">Unzipping this folder, you will see the following items:</span><span class="sxs-lookup"><span data-stu-id="d7f47-122">Unzipping this folder, you will see the following items:</span></span>

* <span data-ttu-id="d7f47-123">outputFileList.txt - a list of the output files produced during the workflow</span><span class="sxs-lookup"><span data-stu-id="d7f47-123">outputFileList.txt - a list of the output files produced during the workflow</span></span>
* <span data-ttu-id="d7f47-124">standarderror.txt - this file is blank.</span><span class="sxs-lookup"><span data-stu-id="d7f47-124">standarderror.txt - this file is blank.</span></span>
* <span data-ttu-id="d7f47-125">standardoutput.txt - contains top-level logging of the workflow.</span><span class="sxs-lookup"><span data-stu-id="d7f47-125">standardoutput.txt - contains top-level logging of the workflow.</span></span> 
* <span data-ttu-id="d7f47-126">GATK log files - all other files in the `logs` folder</span><span class="sxs-lookup"><span data-stu-id="d7f47-126">GATK log files - all other files in the `logs` folder</span></span>

<span data-ttu-id="d7f47-127">The `standardoutput.txt` file is a good place to start to determine why your workflow did not succeed, as it includes more low-level information of the workflow.</span><span class="sxs-lookup"><span data-stu-id="d7f47-127">The `standardoutput.txt` file is a good place to start to determine why your workflow did not succeed, as it includes more low-level information of the workflow.</span></span> 

## <a name="common-issues-and-how-to-resolve-them"></a><span data-ttu-id="d7f47-128">Common issues and how to resolve them</span><span class="sxs-lookup"><span data-stu-id="d7f47-128">Common issues and how to resolve them</span></span>
<span data-ttu-id="d7f47-129">This section briefly highlights common issues and how to resolve them.</span><span class="sxs-lookup"><span data-stu-id="d7f47-129">This section briefly highlights common issues and how to resolve them.</span></span>

### <a name="fastq-files-are-unmatched"></a><span data-ttu-id="d7f47-130">Fastq files are unmatched</span><span class="sxs-lookup"><span data-stu-id="d7f47-130">Fastq files are unmatched</span></span>
<span data-ttu-id="d7f47-131">Fastq files should only differ by the trailing /1 or /2 in the sample identifier.</span><span class="sxs-lookup"><span data-stu-id="d7f47-131">Fastq files should only differ by the trailing /1 or /2 in the sample identifier.</span></span> <span data-ttu-id="d7f47-132">If you have accidentally submitted unmatched FASTQ files, you might see the following error messages when calling `msgen status`.</span><span class="sxs-lookup"><span data-stu-id="d7f47-132">If you have accidentally submitted unmatched FASTQ files, you might see the following error messages when calling `msgen status`.</span></span>
* `Encountered an unmatched read`
* `Error reading a FASTQ file, make sure the input files are valid and paired correctly` 

<span data-ttu-id="d7f47-133">To resolve this, review if the fastq files submitted to the workflow are actually a matched set.</span><span class="sxs-lookup"><span data-stu-id="d7f47-133">To resolve this, review if the fastq files submitted to the workflow are actually a matched set.</span></span> 


### <a name="error-uploading-bam-file-output-blob-already-exists-and-the-overwrite-option-was-set-to-false"></a><span data-ttu-id="d7f47-134">Error uploading .bam file.</span><span class="sxs-lookup"><span data-stu-id="d7f47-134">Error uploading .bam file.</span></span> <span data-ttu-id="d7f47-135">Output blob already exists and the overwrite option was set to False.</span><span class="sxs-lookup"><span data-stu-id="d7f47-135">Output blob already exists and the overwrite option was set to False.</span></span>
<span data-ttu-id="d7f47-136">If you see the following error message, `Error uploading .bam file. Output blob already exists and the overwrite option was set to False`, the output folder already contains an output file with the same name.</span><span class="sxs-lookup"><span data-stu-id="d7f47-136">If you see the following error message, `Error uploading .bam file. Output blob already exists and the overwrite option was set to False`, the output folder already contains an output file with the same name.</span></span>  <span data-ttu-id="d7f47-137">Either delete the existing output file or turn on the overwrite option in the config file.</span><span class="sxs-lookup"><span data-stu-id="d7f47-137">Either delete the existing output file or turn on the overwrite option in the config file.</span></span> <span data-ttu-id="d7f47-138">Then, resubmit your workflow.</span><span class="sxs-lookup"><span data-stu-id="d7f47-138">Then, resubmit your workflow.</span></span>

### <a name="when-to-contact-microsoft-genomics-support"></a><span data-ttu-id="d7f47-139">When to contact Microsoft Genomics support</span><span class="sxs-lookup"><span data-stu-id="d7f47-139">When to contact Microsoft Genomics support</span></span>
<span data-ttu-id="d7f47-140">If you see the following error messages, an internal error occurred.</span><span class="sxs-lookup"><span data-stu-id="d7f47-140">If you see the following error messages, an internal error occurred.</span></span> 

* `Error locating input files on worker machine`
* `Process management failure`

<span data-ttu-id="d7f47-141">Try to resubmit your workflow.</span><span class="sxs-lookup"><span data-stu-id="d7f47-141">Try to resubmit your workflow.</span></span> <span data-ttu-id="d7f47-142">If you continue to have job failures, or if you have any other questions, contact Microsoft Genomics support from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d7f47-142">If you continue to have job failures, or if you have any other questions, contact Microsoft Genomics support from the Azure portal.</span></span> <span data-ttu-id="d7f47-143">Additional information on how to submit a support request can be found [here](file-support-ticket-genomics.md).</span><span class="sxs-lookup"><span data-stu-id="d7f47-143">Additional information on how to submit a support request can be found [here](file-support-ticket-genomics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7f47-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7f47-144">Next steps</span></span>
<span data-ttu-id="d7f47-145">In this article, you learned how to troubleshoot and resolve common issues with the Microsoft Genomics service.</span><span class="sxs-lookup"><span data-stu-id="d7f47-145">In this article, you learned how to troubleshoot and resolve common issues with the Microsoft Genomics service.</span></span> <span data-ttu-id="d7f47-146">For more information and more general FAQ, see [Common questions](frequently-asked-questions-genomics.md).</span><span class="sxs-lookup"><span data-stu-id="d7f47-146">For more information and more general FAQ, see [Common questions](frequently-asked-questions-genomics.md).</span></span> 
