---
title: Adjust quotas and limits in Azure Data Lake Analytics
description: Learn how to adjust and increase quotas and limits in Azure Data Lake Analytics (ADLA) accounts.
services: data-lake-analytics
ms.service: data-lake-analytics
author: omidm1
ms.author: omidm
ms.reviewer: jasonwhowell
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.topic: conceptual
ms.date: 03/15/2018
ms.openlocfilehash: 4629b52f3b2c9e351ddc2a68a40c5178a9a73950
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44815950"
---
# <a name="adjust-quotas-and-limits-in-azure-data-lake-analytics"></a><span data-ttu-id="f80fb-103">Adjust quotas and limits in Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f80fb-103">Adjust quotas and limits in Azure Data Lake Analytics</span></span>

<span data-ttu-id="f80fb-104">Learn how to adjust and increase the quota and limits in Azure Data Lake Analytics (ADLA) accounts.</span><span class="sxs-lookup"><span data-stu-id="f80fb-104">Learn how to adjust and increase the quota and limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="f80fb-105">Knowing these limits may help you understand your U-SQL job behavior.</span><span class="sxs-lookup"><span data-stu-id="f80fb-105">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="f80fb-106">All quota limits are soft, so you can increase the maximum limits by contacting Azure support.</span><span class="sxs-lookup"><span data-stu-id="f80fb-106">All quota limits are soft, so you can increase the maximum limits by contacting Azure support.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="f80fb-107">Azure subscriptions limits</span><span class="sxs-lookup"><span data-stu-id="f80fb-107">Azure subscriptions limits</span></span>

<span data-ttu-id="f80fb-108">**Maximum number of ADLA accounts per subscription per region:**  5</span><span class="sxs-lookup"><span data-stu-id="f80fb-108">**Maximum number of ADLA accounts per subscription per region:**  5</span></span>

<span data-ttu-id="f80fb-109">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span><span class="sxs-lookup"><span data-stu-id="f80fb-109">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> 

<span data-ttu-id="f80fb-110">If you want to go beyond this limit, you can try these options:</span><span class="sxs-lookup"><span data-stu-id="f80fb-110">If you want to go beyond this limit, you can try these options:</span></span>
* <span data-ttu-id="f80fb-111">choose another region if suitable</span><span class="sxs-lookup"><span data-stu-id="f80fb-111">choose another region if suitable</span></span>
* <span data-ttu-id="f80fb-112">contact Azure support by [opening a support ticket](#increase-maximum-quota-limits) to request a quota increase.</span><span class="sxs-lookup"><span data-stu-id="f80fb-112">contact Azure support by [opening a support ticket](#increase-maximum-quota-limits) to request a quota increase.</span></span>

## <a name="default-adla-account-limits"></a><span data-ttu-id="f80fb-113">Default ADLA account limits</span><span class="sxs-lookup"><span data-stu-id="f80fb-113">Default ADLA account limits</span></span>

<span data-ttu-id="f80fb-114">**Maximum number of Analytics Units (AUs) per account:** 32</span><span class="sxs-lookup"><span data-stu-id="f80fb-114">**Maximum number of Analytics Units (AUs) per account:** 32</span></span>

<span data-ttu-id="f80fb-115">This is the maximum number of AUs that can run concurrently in your account.</span><span class="sxs-lookup"><span data-stu-id="f80fb-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="f80fb-116">If your total number of running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span><span class="sxs-lookup"><span data-stu-id="f80fb-116">If your total number of running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="f80fb-117">For example:</span><span class="sxs-lookup"><span data-stu-id="f80fb-117">For example:</span></span>

* <span data-ttu-id="f80fb-118">If you have only one job running with 32 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span><span class="sxs-lookup"><span data-stu-id="f80fb-118">If you have only one job running with 32 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="f80fb-119">If you already have four jobs running and each is using 8 AUs, when you submit a fifth job that needs 8 AUs it waits in the job queue until there are 8 AUs available.</span><span class="sxs-lookup"><span data-stu-id="f80fb-119">If you already have four jobs running and each is using 8 AUs, when you submit a fifth job that needs 8 AUs it waits in the job queue until there are 8 AUs available.</span></span>

<span data-ttu-id="f80fb-120">**Maximum number of Analytics Units (AUs) per job:** 32</span><span class="sxs-lookup"><span data-stu-id="f80fb-120">**Maximum number of Analytics Units (AUs) per job:** 32</span></span>

<span data-ttu-id="f80fb-121">This is the default maximum number of AUs that each individual job can be assigned in your account.</span><span class="sxs-lookup"><span data-stu-id="f80fb-121">This is the default maximum number of AUs that each individual job can be assigned in your account.</span></span> <span data-ttu-id="f80fb-122">Jobs that are assigned more than this limit will be rejected, unless the submitter is affected by a compute policy (job submission limit) that gives them more AUs per job.</span><span class="sxs-lookup"><span data-stu-id="f80fb-122">Jobs that are assigned more than this limit will be rejected, unless the submitter is affected by a compute policy (job submission limit) that gives them more AUs per job.</span></span> <span data-ttu-id="f80fb-123">The upper bound of this value is the AU limit for the account.</span><span class="sxs-lookup"><span data-stu-id="f80fb-123">The upper bound of this value is the AU limit for the account.</span></span>

<span data-ttu-id="f80fb-124">**Maximum number of concurrent U-SQL jobs per account:** 20</span><span class="sxs-lookup"><span data-stu-id="f80fb-124">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="f80fb-125">This is the maximum number of jobs that can run concurrently in your account.</span><span class="sxs-lookup"><span data-stu-id="f80fb-125">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="f80fb-126">Above this value, newer jobs are queued automatically.</span><span class="sxs-lookup"><span data-stu-id="f80fb-126">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-account-limits"></a><span data-ttu-id="f80fb-127">Adjust ADLA account limits</span><span class="sxs-lookup"><span data-stu-id="f80fb-127">Adjust ADLA account limits</span></span>

1. <span data-ttu-id="f80fb-128">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f80fb-128">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f80fb-129">Choose an existing ADLA account.</span><span class="sxs-lookup"><span data-stu-id="f80fb-129">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="f80fb-130">Click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="f80fb-130">Click **Properties**.</span></span>
4. <span data-ttu-id="f80fb-131">Adjust the values for **Maximum AUs**, **Maximum number of running jobs**, and **Job submission limits** to suit your needs.</span><span class="sxs-lookup"><span data-stu-id="f80fb-131">Adjust the values for **Maximum AUs**, **Maximum number of running jobs**, and **Job submission limits** to suit your needs.</span></span>

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="f80fb-132">Increase maximum quota limits</span><span class="sxs-lookup"><span data-stu-id="f80fb-132">Increase maximum quota limits</span></span>

<span data-ttu-id="f80fb-133">You can find more information about Azure limits in the [Azure service-specific limits documentation](../azure-subscription-service-limits.md#data-lake-analytics-limits).</span><span class="sxs-lookup"><span data-stu-id="f80fb-133">You can find more information about Azure limits in the [Azure service-specific limits documentation](../azure-subscription-service-limits.md#data-lake-analytics-limits).</span></span>

1. <span data-ttu-id="f80fb-134">Open a support request in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f80fb-134">Open a support request in Azure portal.</span></span>

    ![Azure Data Lake Analytics portal page](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure Data Lake Analytics portal page](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="f80fb-137">Select the issue type **Quota**.</span><span class="sxs-lookup"><span data-stu-id="f80fb-137">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="f80fb-138">Select your **Subscription** (make sure it is not a "trial" subscription).</span><span class="sxs-lookup"><span data-stu-id="f80fb-138">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="f80fb-139">Select quota type **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f80fb-139">Select quota type **Data Lake Analytics**.</span></span>

    ![Azure Data Lake Analytics portal page](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="f80fb-141">In the problem page, explain your requested increase limit with **Details** of why you need this extra capacity.</span><span class="sxs-lookup"><span data-stu-id="f80fb-141">In the problem page, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Azure Data Lake Analytics portal page](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="f80fb-143">Verify your contact information and create the support request.</span><span class="sxs-lookup"><span data-stu-id="f80fb-143">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="f80fb-144">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="f80fb-144">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f80fb-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="f80fb-145">Next steps</span></span>

* [<span data-ttu-id="f80fb-146">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f80fb-146">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="f80fb-147">Manage Azure Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f80fb-147">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="f80fb-148">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span><span class="sxs-lookup"><span data-stu-id="f80fb-148">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
