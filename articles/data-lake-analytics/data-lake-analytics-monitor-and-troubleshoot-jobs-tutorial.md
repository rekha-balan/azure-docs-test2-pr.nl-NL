---
title: Troubleshoot Azure Data Lake Analytics jobs using Azure Portal | Microsoft Docs
description: 'Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e003d985fa6b4861d314352598e0ef29573cbb7a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564200"
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="23f9a-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="23f9a-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="23f9a-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="23f9a-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="23f9a-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span><span class="sxs-lookup"><span data-stu-id="23f9a-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

<span data-ttu-id="23f9a-106">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="23f9a-106">**Prerequisites**</span></span>

<span data-ttu-id="23f9a-107">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="23f9a-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="23f9a-108">**Basic knowledge of Data Lake Analytics job process**.</span><span class="sxs-lookup"><span data-stu-id="23f9a-108">**Basic knowledge of Data Lake Analytics job process**.</span></span> <span data-ttu-id="23f9a-109">See [Get started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="23f9a-109">See [Get started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="23f9a-110">**A Data Lake Analytics account**.</span><span class="sxs-lookup"><span data-stu-id="23f9a-110">**A Data Lake Analytics account**.</span></span> <span data-ttu-id="23f9a-111">See [Get started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md#create-data-lake-analytics-account).</span><span class="sxs-lookup"><span data-stu-id="23f9a-111">See [Get started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md#create-data-lake-analytics-account).</span></span>
* <span data-ttu-id="23f9a-112">**Copy the sample data to the default Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="23f9a-112">**Copy the sample data to the default Data Lake Store account**.</span></span>  <span data-ttu-id="23f9a-113">See [Prepare source data](data-lake-analytics-get-started-portal.md#prepare-source-data)</span><span class="sxs-lookup"><span data-stu-id="23f9a-113">See [Prepare source data](data-lake-analytics-get-started-portal.md#prepare-source-data)</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="23f9a-114">Submit a Data Lake Analytics job</span><span class="sxs-lookup"><span data-stu-id="23f9a-114">Submit a Data Lake Analytics job</span></span>
<span data-ttu-id="23f9a-115">Now you will create a U-SQL job with a bad source file name.</span><span class="sxs-lookup"><span data-stu-id="23f9a-115">Now you will create a U-SQL job with a bad source file name.</span></span>  

<span data-ttu-id="23f9a-116">**To submit the job**</span><span class="sxs-lookup"><span data-stu-id="23f9a-116">**To submit the job**</span></span>

1. <span data-ttu-id="23f9a-117">From the Azure Portal, click **Microsoft Azure** in the upper left corner.</span><span class="sxs-lookup"><span data-stu-id="23f9a-117">From the Azure Portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="23f9a-118">Click the tile with your Data Lake Analytics account name.</span><span class="sxs-lookup"><span data-stu-id="23f9a-118">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="23f9a-119">It was pinned here when the account was created.</span><span class="sxs-lookup"><span data-stu-id="23f9a-119">It was pinned here when the account was created.</span></span>
   <span data-ttu-id="23f9a-120">If the account is not pinned there, see [Open an Analytics account from portal](data-lake-analytics-manage-use-portal.md#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="23f9a-120">If the account is not pinned there, see [Open an Analytics account from portal](data-lake-analytics-manage-use-portal.md#access-adla-account).</span></span>
3. <span data-ttu-id="23f9a-121">Click **New Job** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="23f9a-121">Click **New Job** from the top menu.</span></span>
4. <span data-ttu-id="23f9a-122">Enter a Job name, and the following U-SQL script:</span><span class="sxs-lookup"><span data-stu-id="23f9a-122">Enter a Job name, and the following U-SQL script:</span></span>

        @searchlog =
            EXTRACT UserId          int,
                    Start           DateTime,
                    Region          string,
                    Query           string,
                    Duration        int?,
                    Urls            string,
                    ClickedUrls     string
            FROM "/Samples/Data/SearchLog.tsv1"
            USING Extractors.Tsv();

        OUTPUT @searchlog   
            TO "/output/SearchLog-from-adls.csv"
        USING Outputters.Csv();

    <span data-ttu-id="23f9a-123">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="23f9a-123">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>
5. <span data-ttu-id="23f9a-124">Click **Submit Job** from the top.</span><span class="sxs-lookup"><span data-stu-id="23f9a-124">Click **Submit Job** from the top.</span></span> <span data-ttu-id="23f9a-125">A new Job Details pane opens.</span><span class="sxs-lookup"><span data-stu-id="23f9a-125">A new Job Details pane opens.</span></span> <span data-ttu-id="23f9a-126">On the title bar, it shows the job status.</span><span class="sxs-lookup"><span data-stu-id="23f9a-126">On the title bar, it shows the job status.</span></span> <span data-ttu-id="23f9a-127">It takes a few minutes to finish.</span><span class="sxs-lookup"><span data-stu-id="23f9a-127">It takes a few minutes to finish.</span></span> <span data-ttu-id="23f9a-128">You can click **Refresh** to get the latest status.</span><span class="sxs-lookup"><span data-stu-id="23f9a-128">You can click **Refresh** to get the latest status.</span></span>
6. <span data-ttu-id="23f9a-129">Wait until the job status is changed to **Failed**.</span><span class="sxs-lookup"><span data-stu-id="23f9a-129">Wait until the job status is changed to **Failed**.</span></span>  <span data-ttu-id="23f9a-130">If the job is **Succeeded**, it is because you didn't remove the /Samples folder.</span><span class="sxs-lookup"><span data-stu-id="23f9a-130">If the job is **Succeeded**, it is because you didn't remove the /Samples folder.</span></span> <span data-ttu-id="23f9a-131">See the **Prerequisite** section at the beginning of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="23f9a-131">See the **Prerequisite** section at the beginning of the tutorial.</span></span>

<span data-ttu-id="23f9a-132">You might be wondering - why it takes so long for a small job.</span><span class="sxs-lookup"><span data-stu-id="23f9a-132">You might be wondering - why it takes so long for a small job.</span></span>  <span data-ttu-id="23f9a-133">Remember Data Lake Analytics is designed to process big data.</span><span class="sxs-lookup"><span data-stu-id="23f9a-133">Remember Data Lake Analytics is designed to process big data.</span></span>  <span data-ttu-id="23f9a-134">It shines when processing a large amount of data using its distributed system.</span><span class="sxs-lookup"><span data-stu-id="23f9a-134">It shines when processing a large amount of data using its distributed system.</span></span>

<span data-ttu-id="23f9a-135">Let's assume you submitted the job, and close the portal.</span><span class="sxs-lookup"><span data-stu-id="23f9a-135">Let's assume you submitted the job, and close the portal.</span></span>  <span data-ttu-id="23f9a-136">In the next section, you will learn how to troubleshoot the job.</span><span class="sxs-lookup"><span data-stu-id="23f9a-136">In the next section, you will learn how to troubleshoot the job.</span></span>

## <a name="troubleshoot-the-job"></a><span data-ttu-id="23f9a-137">Troubleshoot the job</span><span class="sxs-lookup"><span data-stu-id="23f9a-137">Troubleshoot the job</span></span>
<span data-ttu-id="23f9a-138">In the last section, you have submitted a job, and the job failed.</span><span class="sxs-lookup"><span data-stu-id="23f9a-138">In the last section, you have submitted a job, and the job failed.</span></span>  

<span data-ttu-id="23f9a-139">**To see all the jobs**</span><span class="sxs-lookup"><span data-stu-id="23f9a-139">**To see all the jobs**</span></span>

1. <span data-ttu-id="23f9a-140">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span><span class="sxs-lookup"><span data-stu-id="23f9a-140">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="23f9a-141">Click the tile with your Data Lake Analytics account name.</span><span class="sxs-lookup"><span data-stu-id="23f9a-141">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="23f9a-142">The job summary is shown on the **Job Management** tile.</span><span class="sxs-lookup"><span data-stu-id="23f9a-142">The job summary is shown on the **Job Management** tile.</span></span>

    ![Azure Data Lake Analytics job management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="23f9a-144">The job Management gives you a glance of the job status.</span><span class="sxs-lookup"><span data-stu-id="23f9a-144">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="23f9a-145">Notice there is a failed job.</span><span class="sxs-lookup"><span data-stu-id="23f9a-145">Notice there is a failed job.</span></span>
3. <span data-ttu-id="23f9a-146">Click the **Job Management** tile to see the jobs.</span><span class="sxs-lookup"><span data-stu-id="23f9a-146">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="23f9a-147">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span><span class="sxs-lookup"><span data-stu-id="23f9a-147">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="23f9a-148">You shall see your failed job in the **Ended** section.</span><span class="sxs-lookup"><span data-stu-id="23f9a-148">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="23f9a-149">It shall be first one in the list.</span><span class="sxs-lookup"><span data-stu-id="23f9a-149">It shall be first one in the list.</span></span> <span data-ttu-id="23f9a-150">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span><span class="sxs-lookup"><span data-stu-id="23f9a-150">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Azure Data Lake Analytics filter jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="23f9a-152">Click the failed job from the list to open the job details in a new blade:</span><span class="sxs-lookup"><span data-stu-id="23f9a-152">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Azure Data Lake Analytics failed job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="23f9a-154">Notice the **Resubmit** button.</span><span class="sxs-lookup"><span data-stu-id="23f9a-154">Notice the **Resubmit** button.</span></span> <span data-ttu-id="23f9a-155">After you fix the problem, you can resubmit the job.</span><span class="sxs-lookup"><span data-stu-id="23f9a-155">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="23f9a-156">Click highlighted part from the previous screenshot to open the error details.</span><span class="sxs-lookup"><span data-stu-id="23f9a-156">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="23f9a-157">You shall see something like:</span><span class="sxs-lookup"><span data-stu-id="23f9a-157">You shall see something like:</span></span>

    ![Azure Data Lake Analytics failed job details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="23f9a-159">It tells you the source folder is not found.</span><span class="sxs-lookup"><span data-stu-id="23f9a-159">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="23f9a-160">Click **Duplicate Script**.</span><span class="sxs-lookup"><span data-stu-id="23f9a-160">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="23f9a-161">Update the **FROM** path to the following:</span><span class="sxs-lookup"><span data-stu-id="23f9a-161">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="23f9a-162">"/Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="23f9a-162">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="23f9a-163">Click **Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="23f9a-163">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="23f9a-164">See also</span><span class="sxs-lookup"><span data-stu-id="23f9a-164">See also</span></span>
* [<span data-ttu-id="23f9a-165">Azure Data Lake Analytics overview</span><span class="sxs-lookup"><span data-stu-id="23f9a-165">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="23f9a-166">Get started with Azure Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="23f9a-166">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="23f9a-167">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="23f9a-167">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="23f9a-168">Manage Azure Data Lake Analytics using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="23f9a-168">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)




