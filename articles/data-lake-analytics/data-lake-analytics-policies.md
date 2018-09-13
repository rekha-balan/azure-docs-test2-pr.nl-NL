---
title: Manage Azure Data Lake Analytics policies
description: Learn how to use policies to control usage of a Data Lake Analytics account.
services: data-lake-analytics
ms.service: data-lake-analytics
author: saveenr
ms.author: saveenr
ms.reviewer: jasonwhowell
ms.assetid: 0a6102d1-7554-4df2-b487-4dae9a7287b6
ms.topic: conceptual
ms.date: 04/30/2018
ms.openlocfilehash: f84cb59e7d4fd7d8301d22348ca066a7f9d9e94e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868226"
---
# <a name="manage-azure-data-lake-analytics-using-policies"></a><span data-ttu-id="665f6-103">Manage Azure Data Lake Analytics using policies</span><span class="sxs-lookup"><span data-stu-id="665f6-103">Manage Azure Data Lake Analytics using policies</span></span>

<span data-ttu-id="665f6-104">Using account policies, you can control how resources an Azure Data Lake Analytics account are used.</span><span class="sxs-lookup"><span data-stu-id="665f6-104">Using account policies, you can control how resources an Azure Data Lake Analytics account are used.</span></span> <span data-ttu-id="665f6-105">These policies allow you to control the cost of using Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="665f6-105">These policies allow you to control the cost of using Azure Data Lake Analytics.</span></span> <span data-ttu-id="665f6-106">For example, with these policies you can prevent unexpected cost spikes by limiting how many AUs the account can simultaneously use.</span><span class="sxs-lookup"><span data-stu-id="665f6-106">For example, with these policies you can prevent unexpected cost spikes by limiting how many AUs the account can simultaneously use.</span></span>

## <a name="account-level-policies"></a><span data-ttu-id="665f6-107">Account-level policies</span><span class="sxs-lookup"><span data-stu-id="665f6-107">Account-level policies</span></span>

<span data-ttu-id="665f6-108">These policies apply to all jobs in a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="665f6-108">These policies apply to all jobs in a Data Lake Analytics account.</span></span>

### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="665f6-109">Maximum number of AUs in a Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="665f6-109">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="665f6-110">A policy controls the total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span><span class="sxs-lookup"><span data-stu-id="665f6-110">A policy controls the total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="665f6-111">By default, the value is set to 250.</span><span class="sxs-lookup"><span data-stu-id="665f6-111">By default, the value is set to 250.</span></span> <span data-ttu-id="665f6-112">For example, if this value is set to 250 AUs, you can have one job running with 250 AUs assigned to it, or 10 jobs running with 25 AUs each.</span><span class="sxs-lookup"><span data-stu-id="665f6-112">For example, if this value is set to 250 AUs, you can have one job running with 250 AUs assigned to it, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="665f6-113">Additional jobs that are submitted are queued until the running jobs are finished.</span><span class="sxs-lookup"><span data-stu-id="665f6-113">Additional jobs that are submitted are queued until the running jobs are finished.</span></span> <span data-ttu-id="665f6-114">When running jobs are finished, AUs are freed up for the queued jobs to run.</span><span class="sxs-lookup"><span data-stu-id="665f6-114">When running jobs are finished, AUs are freed up for the queued jobs to run.</span></span>

<span data-ttu-id="665f6-115">To change the number of AUs for your Data Lake Analytics account:</span><span class="sxs-lookup"><span data-stu-id="665f6-115">To change the number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="665f6-116">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="665f6-116">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="665f6-117">Click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="665f6-117">Click **Properties**.</span></span>
3. <span data-ttu-id="665f6-118">Under **Maximum AUs**, move the slider to select a value, or enter the value in the text box.</span><span class="sxs-lookup"><span data-stu-id="665f6-118">Under **Maximum AUs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="665f6-119">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="665f6-119">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="665f6-120">If you need more than the default (250) AUs, in the portal, click **Help+Support** to submit a support request.</span><span class="sxs-lookup"><span data-stu-id="665f6-120">If you need more than the default (250) AUs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="665f6-121">The number of AUs available in your Data Lake Analytics account can be increased.</span><span class="sxs-lookup"><span data-stu-id="665f6-121">The number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="665f6-122">Maximum number of jobs that can run simultaneously</span><span class="sxs-lookup"><span data-stu-id="665f6-122">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="665f6-123">A policy controls how many jobs can run at the same time.</span><span class="sxs-lookup"><span data-stu-id="665f6-123">A policy controls how many jobs can run at the same time.</span></span> <span data-ttu-id="665f6-124">By default, this value is set to 20.</span><span class="sxs-lookup"><span data-stu-id="665f6-124">By default, this value is set to 20.</span></span> <span data-ttu-id="665f6-125">If your Data Lake Analytics has AUs available, new jobs are scheduled to run immediately until the total number of running jobs reaches the value of this policy.</span><span class="sxs-lookup"><span data-stu-id="665f6-125">If your Data Lake Analytics has AUs available, new jobs are scheduled to run immediately until the total number of running jobs reaches the value of this policy.</span></span> <span data-ttu-id="665f6-126">When you reach the maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span><span class="sxs-lookup"><span data-stu-id="665f6-126">When you reach the maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="665f6-127">To change the number of jobs that can run simultaneously:</span><span class="sxs-lookup"><span data-stu-id="665f6-127">To change the number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="665f6-128">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="665f6-128">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="665f6-129">Click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="665f6-129">Click **Properties**.</span></span>
3. <span data-ttu-id="665f6-130">Under **Maximum Number of Running Jobs**, move the slider to select a value, or enter the value in the text box.</span><span class="sxs-lookup"><span data-stu-id="665f6-130">Under **Maximum Number of Running Jobs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="665f6-131">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="665f6-131">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="665f6-132">If you need to run more than the default (20) number of jobs, in the portal, click **Help+Support** to submit a support request.</span><span class="sxs-lookup"><span data-stu-id="665f6-132">If you need to run more than the default (20) number of jobs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="665f6-133">The number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span><span class="sxs-lookup"><span data-stu-id="665f6-133">The number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

### <a name="how-long-to-keep-job-metadata-and-resources"></a><span data-ttu-id="665f6-134">How long to keep job metadata and resources</span><span class="sxs-lookup"><span data-stu-id="665f6-134">How long to keep job metadata and resources</span></span> 
<span data-ttu-id="665f6-135">When your users run U-SQL jobs, the Data Lake Analytics service retains all related files.</span><span class="sxs-lookup"><span data-stu-id="665f6-135">When your users run U-SQL jobs, the Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="665f6-136">Related files include the U-SQL script, the DLL files referenced in the U-SQL script, compiled resources, and statistics.</span><span class="sxs-lookup"><span data-stu-id="665f6-136">Related files include the U-SQL script, the DLL files referenced in the U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="665f6-137">The files are in the /system/ folder of the default Azure Data Lake Storage account.</span><span class="sxs-lookup"><span data-stu-id="665f6-137">The files are in the /system/ folder of the default Azure Data Lake Storage account.</span></span> <span data-ttu-id="665f6-138">This policy controls how long these resources are stored before they are automatically deleted (the default is 30 days).</span><span class="sxs-lookup"><span data-stu-id="665f6-138">This policy controls how long these resources are stored before they are automatically deleted (the default is 30 days).</span></span> <span data-ttu-id="665f6-139">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in the future.</span><span class="sxs-lookup"><span data-stu-id="665f6-139">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in the future.</span></span>

<span data-ttu-id="665f6-140">To change how long to keep job metadata and resources:</span><span class="sxs-lookup"><span data-stu-id="665f6-140">To change how long to keep job metadata and resources:</span></span>

1. <span data-ttu-id="665f6-141">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="665f6-141">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="665f6-142">Click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="665f6-142">Click **Properties**.</span></span>
3. <span data-ttu-id="665f6-143">Under **Days to Retain Job Queries**, move the slider to select a value, or enter the value in the text box.</span><span class="sxs-lookup"><span data-stu-id="665f6-143">Under **Days to Retain Job Queries**, move the slider to select a value, or enter the value in the text box.</span></span>  
4. <span data-ttu-id="665f6-144">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="665f6-144">Click **Save**.</span></span>

## <a name="job-level-policies"></a><span data-ttu-id="665f6-145">Job-level policies</span><span class="sxs-lookup"><span data-stu-id="665f6-145">Job-level policies</span></span>

<span data-ttu-id="665f6-146">With job-level policies, you can control the maximum AUs and the maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span><span class="sxs-lookup"><span data-stu-id="665f6-146">With job-level policies, you can control the maximum AUs and the maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="665f6-147">This policy lets you control the costs incurred by users.</span><span class="sxs-lookup"><span data-stu-id="665f6-147">This policy lets you control the costs incurred by users.</span></span> <span data-ttu-id="665f6-148">It also lets you control the effect that scheduled jobs might have on high-priority production jobs that are running in the same Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="665f6-148">It also lets you control the effect that scheduled jobs might have on high-priority production jobs that are running in the same Data Lake Analytics account.</span></span>

<span data-ttu-id="665f6-149">Data Lake Analytics has two policies that you can set at the job level:</span><span class="sxs-lookup"><span data-stu-id="665f6-149">Data Lake Analytics has two policies that you can set at the job level:</span></span>

* <span data-ttu-id="665f6-150">**AU limit per job**: Users can only submit jobs that have up to this number of AUs.</span><span class="sxs-lookup"><span data-stu-id="665f6-150">**AU limit per job**: Users can only submit jobs that have up to this number of AUs.</span></span> <span data-ttu-id="665f6-151">By default, this limit is the same as the maximum AU limit for the account.</span><span class="sxs-lookup"><span data-stu-id="665f6-151">By default, this limit is the same as the maximum AU limit for the account.</span></span>
* <span data-ttu-id="665f6-152">**Priority**: Users can only submit jobs that have a priority lower than or equal to this value.</span><span class="sxs-lookup"><span data-stu-id="665f6-152">**Priority**: Users can only submit jobs that have a priority lower than or equal to this value.</span></span> <span data-ttu-id="665f6-153">A higher number indicates a lower priority.</span><span class="sxs-lookup"><span data-stu-id="665f6-153">A higher number indicates a lower priority.</span></span> <span data-ttu-id="665f6-154">By default, this limit is set to 1, which is the highest possible priority.</span><span class="sxs-lookup"><span data-stu-id="665f6-154">By default, this limit is set to 1, which is the highest possible priority.</span></span>

<span data-ttu-id="665f6-155">There is a default policy set on every account.</span><span class="sxs-lookup"><span data-stu-id="665f6-155">There is a default policy set on every account.</span></span> <span data-ttu-id="665f6-156">The default policy applies to all users of the account.</span><span class="sxs-lookup"><span data-stu-id="665f6-156">The default policy applies to all users of the account.</span></span> <span data-ttu-id="665f6-157">You can set additional policies for specific users and groups.</span><span class="sxs-lookup"><span data-stu-id="665f6-157">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="665f6-158">Account-level policies and job-level policies apply simultaneously.</span><span class="sxs-lookup"><span data-stu-id="665f6-158">Account-level policies and job-level policies apply simultaneously.</span></span>
>

### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="665f6-159">Add a policy for a specific user or group</span><span class="sxs-lookup"><span data-stu-id="665f6-159">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="665f6-160">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="665f6-160">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="665f6-161">Click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="665f6-161">Click **Properties**.</span></span>
3. <span data-ttu-id="665f6-162">Under **Job Submission Limits**, click the **Add Policy** button.</span><span class="sxs-lookup"><span data-stu-id="665f6-162">Under **Job Submission Limits**, click the **Add Policy** button.</span></span> <span data-ttu-id="665f6-163">Then, select or enter the following settings:</span><span class="sxs-lookup"><span data-stu-id="665f6-163">Then, select or enter the following settings:</span></span>
    1. <span data-ttu-id="665f6-164">**Compute Policy Name**: Enter a policy name, to remind you of the purpose of the policy.</span><span class="sxs-lookup"><span data-stu-id="665f6-164">**Compute Policy Name**: Enter a policy name, to remind you of the purpose of the policy.</span></span>
    2. <span data-ttu-id="665f6-165">**Select User or Group**: Select the user or group this policy applies to.</span><span class="sxs-lookup"><span data-stu-id="665f6-165">**Select User or Group**: Select the user or group this policy applies to.</span></span>
    3. <span data-ttu-id="665f6-166">**Set the Job AU Limit**: Set the AU limit that applies to the selected user or group.</span><span class="sxs-lookup"><span data-stu-id="665f6-166">**Set the Job AU Limit**: Set the AU limit that applies to the selected user or group.</span></span>
    4. <span data-ttu-id="665f6-167">**Set the Priority Limit**: Set the priority limit that applies to the selected user or group.</span><span class="sxs-lookup"><span data-stu-id="665f6-167">**Set the Priority Limit**: Set the priority limit that applies to the selected user or group.</span></span>

4. <span data-ttu-id="665f6-168">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="665f6-168">Click **Ok**.</span></span>

5. <span data-ttu-id="665f6-169">The new policy is listed in the **Default** policy table, under **Job Submission Limits**.</span><span class="sxs-lookup"><span data-stu-id="665f6-169">The new policy is listed in the **Default** policy table, under **Job Submission Limits**.</span></span> 

### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="665f6-170">Delete or edit an existing policy</span><span class="sxs-lookup"><span data-stu-id="665f6-170">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="665f6-171">In the Azure portal, go to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="665f6-171">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="665f6-172">Click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="665f6-172">Click **Properties**.</span></span>
3. <span data-ttu-id="665f6-173">Under **Job Submission Limits**, find the policy you want to edit.</span><span class="sxs-lookup"><span data-stu-id="665f6-173">Under **Job Submission Limits**, find the policy you want to edit.</span></span>
4.  <span data-ttu-id="665f6-174">To see the **Delete** and **Edit** options, in the rightmost column of the table, click `...`.</span><span class="sxs-lookup"><span data-stu-id="665f6-174">To see the **Delete** and **Edit** options, in the rightmost column of the table, click `...`.</span></span>

## <a name="additional-resources-for-job-policies"></a><span data-ttu-id="665f6-175">Additional resources for job policies</span><span class="sxs-lookup"><span data-stu-id="665f6-175">Additional resources for job policies</span></span>
* [<span data-ttu-id="665f6-176">Policy overview blog post</span><span class="sxs-lookup"><span data-stu-id="665f6-176">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="665f6-177">Account-level policies blog post</span><span class="sxs-lookup"><span data-stu-id="665f6-177">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="665f6-178">Job-level policies blog post</span><span class="sxs-lookup"><span data-stu-id="665f6-178">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="665f6-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="665f6-179">Next steps</span></span>

* [<span data-ttu-id="665f6-180">Overview of Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="665f6-180">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="665f6-181">Get started with Data Lake Analytics by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="665f6-181">Get started with Data Lake Analytics by using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="665f6-182">Manage Azure Data Lake Analytics by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="665f6-182">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

