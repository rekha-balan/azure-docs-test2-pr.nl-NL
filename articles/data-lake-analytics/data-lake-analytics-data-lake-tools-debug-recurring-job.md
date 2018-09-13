---
title: Debug recurring jobs in Azure Data Lake Analytics
description: Learn how to use Azure Data Lake Tools for Visual Studio to debug an abnormal recurring job.
services: data-lake-analytics
author: yanancai
ms.author: yanacai
ms.reviewer: jasonwhowell
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.topic: conceptual
ms.date: 05/20/2018
ms.openlocfilehash: 33c3b91e7bf9fa64e3ba3f98a9396045753d0c2a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855884"
---
# <a name="troubleshoot-an-abnormal-recurring-job"></a><span data-ttu-id="8897b-103">Troubleshoot an abnormal recurring job</span><span class="sxs-lookup"><span data-stu-id="8897b-103">Troubleshoot an abnormal recurring job</span></span>

<span data-ttu-id="8897b-104">This article shows how to use [Azure Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs) to troubleshoot problems with recurring jobs.</span><span class="sxs-lookup"><span data-stu-id="8897b-104">This article shows how to use [Azure Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs) to troubleshoot problems with recurring jobs.</span></span> <span data-ttu-id="8897b-105">Learn more about pipeline and recurring jobs from the [Azure Data Lake and Azure HDInsight blog](https://blogs.msdn.microsoft.com/azuredatalake/2017/09/19/managing-pipeline-recurring-jobs-in-azure-data-lake-analytics-made-easy/).</span><span class="sxs-lookup"><span data-stu-id="8897b-105">Learn more about pipeline and recurring jobs from the [Azure Data Lake and Azure HDInsight blog](https://blogs.msdn.microsoft.com/azuredatalake/2017/09/19/managing-pipeline-recurring-jobs-in-azure-data-lake-analytics-made-easy/).</span></span>

<span data-ttu-id="8897b-106">Recurring jobs usually share the same query logic and similar input data.</span><span class="sxs-lookup"><span data-stu-id="8897b-106">Recurring jobs usually share the same query logic and similar input data.</span></span> <span data-ttu-id="8897b-107">For example, imagine that you have a recurring job running every Monday morning at 8 A.M.</span><span class="sxs-lookup"><span data-stu-id="8897b-107">For example, imagine that you have a recurring job running every Monday morning at 8 A.M.</span></span> <span data-ttu-id="8897b-108">to count last week’s weekly active user.</span><span class="sxs-lookup"><span data-stu-id="8897b-108">to count last week’s weekly active user.</span></span> <span data-ttu-id="8897b-109">The scripts for these jobs share one script template that contains the query logic.</span><span class="sxs-lookup"><span data-stu-id="8897b-109">The scripts for these jobs share one script template that contains the query logic.</span></span> <span data-ttu-id="8897b-110">The inputs for these jobs are the usage data for last week.</span><span class="sxs-lookup"><span data-stu-id="8897b-110">The inputs for these jobs are the usage data for last week.</span></span> <span data-ttu-id="8897b-111">Sharing the same query logic and similar input usually means that performance of these jobs is similar and stable.</span><span class="sxs-lookup"><span data-stu-id="8897b-111">Sharing the same query logic and similar input usually means that performance of these jobs is similar and stable.</span></span> <span data-ttu-id="8897b-112">If one of your recurring jobs suddenly performs abnormally, fails, or slows down a lot, you might want to:</span><span class="sxs-lookup"><span data-stu-id="8897b-112">If one of your recurring jobs suddenly performs abnormally, fails, or slows down a lot, you might want to:</span></span>

- <span data-ttu-id="8897b-113">See the statistics reports for the previous runs of the recurring job to see what happened.</span><span class="sxs-lookup"><span data-stu-id="8897b-113">See the statistics reports for the previous runs of the recurring job to see what happened.</span></span>
- <span data-ttu-id="8897b-114">Compare the abnormal job with a normal one to figure out what has been changed.</span><span class="sxs-lookup"><span data-stu-id="8897b-114">Compare the abnormal job with a normal one to figure out what has been changed.</span></span>

<span data-ttu-id="8897b-115">**Related Job View** in Azure Data Lake Tools for Visual Studio helps you accelerate the troubleshooting progress with both cases.</span><span class="sxs-lookup"><span data-stu-id="8897b-115">**Related Job View** in Azure Data Lake Tools for Visual Studio helps you accelerate the troubleshooting progress with both cases.</span></span>

## <a name="step-1-find-recurring-jobs-and-open-related-job-view"></a><span data-ttu-id="8897b-116">Step 1: Find recurring jobs and open Related Job View</span><span class="sxs-lookup"><span data-stu-id="8897b-116">Step 1: Find recurring jobs and open Related Job View</span></span>

<span data-ttu-id="8897b-117">To use Related Job View to troubleshoot a recurring job problem, you need to first find the recurring job in Visual Studio and then open Related Job View.</span><span class="sxs-lookup"><span data-stu-id="8897b-117">To use Related Job View to troubleshoot a recurring job problem, you need to first find the recurring job in Visual Studio and then open Related Job View.</span></span>

### <a name="case-1-you-have-the-url-for-the-recurring-job"></a><span data-ttu-id="8897b-118">Case 1: You have the URL for the recurring job</span><span class="sxs-lookup"><span data-stu-id="8897b-118">Case 1: You have the URL for the recurring job</span></span>

<span data-ttu-id="8897b-119">Through **Tools** > **Data Lake** > **Job View**, you can paste the job URL to open Job View in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8897b-119">Through **Tools** > **Data Lake** > **Job View**, you can paste the job URL to open Job View in Visual Studio.</span></span> <span data-ttu-id="8897b-120">Select **View Related Jobs** to open Related Job View.</span><span class="sxs-lookup"><span data-stu-id="8897b-120">Select **View Related Jobs** to open Related Job View.</span></span>

![View Related Jobs link in Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-debug-recurring-job/view-related-job.png)
 
### <a name="case-2-you-have-the-pipeline-for-the-recurring-job-but-not-the-url"></a><span data-ttu-id="8897b-122">Case 2: You have the pipeline for the recurring job, but not the URL</span><span class="sxs-lookup"><span data-stu-id="8897b-122">Case 2: You have the pipeline for the recurring job, but not the URL</span></span>

<span data-ttu-id="8897b-123">In Visual Studio, you can open Pipeline Browser through Server Explorer > your Azure Data Lake Analytics account > **Pipelines**.</span><span class="sxs-lookup"><span data-stu-id="8897b-123">In Visual Studio, you can open Pipeline Browser through Server Explorer > your Azure Data Lake Analytics account > **Pipelines**.</span></span> <span data-ttu-id="8897b-124">(If you can't find this node in Server Explorer, [download the latest plug-in](http://aka.ms/adltoolsvs).)</span><span class="sxs-lookup"><span data-stu-id="8897b-124">(If you can't find this node in Server Explorer, [download the latest plug-in](http://aka.ms/adltoolsvs).)</span></span> 

![Selecting the Pipelines node](./media/data-lake-analytics-data-lake-tools-debug-recurring-job/pipeline-browser.png)

<span data-ttu-id="8897b-126">In Pipeline Browser, all pipelines for the Data Lake Analytics account are listed at left.</span><span class="sxs-lookup"><span data-stu-id="8897b-126">In Pipeline Browser, all pipelines for the Data Lake Analytics account are listed at left.</span></span> <span data-ttu-id="8897b-127">You can expand the pipelines to find all recurring jobs, and then select the one that has problems.</span><span class="sxs-lookup"><span data-stu-id="8897b-127">You can expand the pipelines to find all recurring jobs, and then select the one that has problems.</span></span> <span data-ttu-id="8897b-128">Related Job View opens at right.</span><span class="sxs-lookup"><span data-stu-id="8897b-128">Related Job View opens at right.</span></span>

![Selecting a pipeline and opening Related Job View](./media/data-lake-analytics-data-lake-tools-debug-recurring-job/recurring-job-view.png)

## <a name="step-2-analyze-a-statistics-report"></a><span data-ttu-id="8897b-130">Step 2: Analyze a statistics report</span><span class="sxs-lookup"><span data-stu-id="8897b-130">Step 2: Analyze a statistics report</span></span>

<span data-ttu-id="8897b-131">A summary and a statistics report are shown at top of Related Job View.</span><span class="sxs-lookup"><span data-stu-id="8897b-131">A summary and a statistics report are shown at top of Related Job View.</span></span> <span data-ttu-id="8897b-132">There, you can find the potential root cause of the problem.</span><span class="sxs-lookup"><span data-stu-id="8897b-132">There, you can find the potential root cause of the problem.</span></span> 

1.  <span data-ttu-id="8897b-133">In the report, the X-axis shows the job submission time.</span><span class="sxs-lookup"><span data-stu-id="8897b-133">In the report, the X-axis shows the job submission time.</span></span> <span data-ttu-id="8897b-134">Use it to find the abnormal job.</span><span class="sxs-lookup"><span data-stu-id="8897b-134">Use it to find the abnormal job.</span></span>
2.  <span data-ttu-id="8897b-135">Use the process in the following diagram to check statistics and get insights about the problem and the possible solutions.</span><span class="sxs-lookup"><span data-stu-id="8897b-135">Use the process in the following diagram to check statistics and get insights about the problem and the possible solutions.</span></span>

![Process diagram for checking statistics](./media/data-lake-analytics-data-lake-tools-debug-recurring-job/recurring-job-metrics-debugging-flow.png)

## <a name="step-3-compare-the-abnormal-job-to-a-normal-job"></a><span data-ttu-id="8897b-137">Step 3: Compare the abnormal job to a normal job</span><span class="sxs-lookup"><span data-stu-id="8897b-137">Step 3: Compare the abnormal job to a normal job</span></span>

<span data-ttu-id="8897b-138">You can find all submitted recurring jobs through the job list at the bottom of Related Job View.</span><span class="sxs-lookup"><span data-stu-id="8897b-138">You can find all submitted recurring jobs through the job list at the bottom of Related Job View.</span></span> <span data-ttu-id="8897b-139">To find more insights and potential solutions, right-click the abnormal job.</span><span class="sxs-lookup"><span data-stu-id="8897b-139">To find more insights and potential solutions, right-click the abnormal job.</span></span> <span data-ttu-id="8897b-140">Use the Job Diff view to compare the abnormal job with a previous normal one.</span><span class="sxs-lookup"><span data-stu-id="8897b-140">Use the Job Diff view to compare the abnormal job with a previous normal one.</span></span>

![Shortcut menu for comparing jobs](./media/data-lake-analytics-data-lake-tools-debug-recurring-job/compare-job.png)

<span data-ttu-id="8897b-142">Pay attention to the big differences between these two jobs.</span><span class="sxs-lookup"><span data-stu-id="8897b-142">Pay attention to the big differences between these two jobs.</span></span> <span data-ttu-id="8897b-143">Those differences are probably causing the performance problems.</span><span class="sxs-lookup"><span data-stu-id="8897b-143">Those differences are probably causing the performance problems.</span></span> <span data-ttu-id="8897b-144">To check further, use the steps in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="8897b-144">To check further, use the steps in the following diagram:</span></span>

![Process diagram for checking differences between jobs](./media/data-lake-analytics-data-lake-tools-debug-recurring-job/recurring-job-diff-debugging-flow.png)

## <a name="next-steps"></a><span data-ttu-id="8897b-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="8897b-146">Next steps</span></span>

* [<span data-ttu-id="8897b-147">Resolve data-skew problems</span><span class="sxs-lookup"><span data-stu-id="8897b-147">Resolve data-skew problems</span></span>](data-lake-analytics-data-lake-tools-data-skew-solutions.md)
* [<span data-ttu-id="8897b-148">Debug user-defined C# code for failed U-SQL jobs</span><span class="sxs-lookup"><span data-stu-id="8897b-148">Debug user-defined C# code for failed U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
