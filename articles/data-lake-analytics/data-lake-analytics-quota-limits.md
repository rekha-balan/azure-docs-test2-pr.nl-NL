---
title: Azure Data Lake Analytics Quota Limits | Microsoft Docs
description: Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) account. Knowing these limits may help you understand your U-SQL job behavior. All these limits are soft and you can always increase the max limits by reaching out to us.
services: data-lake-analytics
keywords: Azure Data Lake Analytics
documentationcenter: ''
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/16/2016
ms.author: omidm
ms.openlocfilehash: e161a78e0ccbcc7731e3627a519e5a338059c5bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550952"
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="96658-106">Azure Data Lake Analytics Quota Limits</span><span class="sxs-lookup"><span data-stu-id="96658-106">Azure Data Lake Analytics Quota Limits</span></span>
<span data-ttu-id="96658-107">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) account.</span><span class="sxs-lookup"><span data-stu-id="96658-107">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) account.</span></span> <span data-ttu-id="96658-108">Knowing these limits may help you understand your U-SQL job behavior.</span><span class="sxs-lookup"><span data-stu-id="96658-108">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="96658-109">All these limits are soft and you can always increase the max limits by reaching out to us.</span><span class="sxs-lookup"><span data-stu-id="96658-109">All these limits are soft and you can always increase the max limits by reaching out to us.</span></span>

<span data-ttu-id="96658-110">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="96658-110">**Prerequisites**</span></span>

<span data-ttu-id="96658-111">Before you begin this tutorial, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="96658-111">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="96658-112">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="96658-112">**An Azure subscription**.</span></span> <span data-ttu-id="96658-113">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96658-113">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="96658-114">**A Data Lake Analytics account**.</span><span class="sxs-lookup"><span data-stu-id="96658-114">**A Data Lake Analytics account**.</span></span> <span data-ttu-id="96658-115">See [Get started with Azure Data Lake Analytics using Azure Portal](https://azure.microsoft.com/en-us/documentation/articles/data-lake-analytics-get-started-portal/#create-adl-analytics-account).</span><span class="sxs-lookup"><span data-stu-id="96658-115">See [Get started with Azure Data Lake Analytics using Azure Portal](https://azure.microsoft.com/en-us/documentation/articles/data-lake-analytics-get-started-portal/#create-adl-analytics-account).</span></span>
* <span data-ttu-id="96658-116">**Basic knowledge of Data Lake Analytics job process**.</span><span class="sxs-lookup"><span data-stu-id="96658-116">**Basic knowledge of Data Lake Analytics job process**.</span></span> <span data-ttu-id="96658-117">See [Get started with Azure Data Lake Analytics using Azure Portal](https://azure.microsoft.com/en-us/documentation/articles/data-lake-analytics-get-started-portal/).</span><span class="sxs-lookup"><span data-stu-id="96658-117">See [Get started with Azure Data Lake Analytics using Azure Portal](https://azure.microsoft.com/en-us/documentation/articles/data-lake-analytics-get-started-portal/).</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="quota-limits"></a><span data-ttu-id="96658-118">Quota limits:</span><span class="sxs-lookup"><span data-stu-id="96658-118">Quota limits:</span></span>
<span data-ttu-id="96658-119">The list below outlines the current quota limits of the system:</span><span class="sxs-lookup"><span data-stu-id="96658-119">The list below outlines the current quota limits of the system:</span></span>

<span data-ttu-id="96658-120">**Azure Subscriptions limits:** The following limit applies to Azure subscriptions:</span><span class="sxs-lookup"><span data-stu-id="96658-120">**Azure Subscriptions limits:** The following limit applies to Azure subscriptions:</span></span>
* <span data-ttu-id="96658-121">**Max number of ADLA accounts per subscription:**  5.</span><span class="sxs-lookup"><span data-stu-id="96658-121">**Max number of ADLA accounts per subscription:**  5.</span></span> <span data-ttu-id="96658-122">This is the maximum number of ADLA accounts you can create per subscription.</span><span class="sxs-lookup"><span data-stu-id="96658-122">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="96658-123">You receive this error “You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name” when you try to create the sixth ADLA accounts.</span><span class="sxs-lookup"><span data-stu-id="96658-123">You receive this error “You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name” when you try to create the sixth ADLA accounts.</span></span> <span data-ttu-id="96658-124">You can easily fix this by either deleting used ADLA accounts under your subscription or reaching out to us by opening a support ticket.</span><span class="sxs-lookup"><span data-stu-id="96658-124">You can easily fix this by either deleting used ADLA accounts under your subscription or reaching out to us by opening a support ticket.</span></span>

<span data-ttu-id="96658-125">**ADLA Account limits:**</span><span class="sxs-lookup"><span data-stu-id="96658-125">**ADLA Account limits:**</span></span>
* <span data-ttu-id="96658-126">**Max number of Analytics Units (AUs) per account:** 250.</span><span class="sxs-lookup"><span data-stu-id="96658-126">**Max number of Analytics Units (AUs) per account:** 250.</span></span> <span data-ttu-id="96658-127">This is the maximum number of AUs that can run concurrently in your account.</span><span class="sxs-lookup"><span data-stu-id="96658-127">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="96658-128">Your total running AUs cross all the jobs can’t go beyond this.</span><span class="sxs-lookup"><span data-stu-id="96658-128">Your total running AUs cross all the jobs can’t go beyond this.</span></span> <span data-ttu-id="96658-129">Exceeding this value causes newer jobs to be queued automatically.</span><span class="sxs-lookup"><span data-stu-id="96658-129">Exceeding this value causes newer jobs to be queued automatically.</span></span> <span data-ttu-id="96658-130">For example:</span><span class="sxs-lookup"><span data-stu-id="96658-130">For example:</span></span>
    * <span data-ttu-id="96658-131">You may have only one job running with 250 AUs, when you submit the second job, this job stands in the job queue until the first one is completed.</span><span class="sxs-lookup"><span data-stu-id="96658-131">You may have only one job running with 250 AUs, when you submit the second job, this job stands in the job queue until the first one is completed.</span></span>
    * <span data-ttu-id="96658-132">You may already have 5 jobs running and each submitted with 50 AUs, when you submit the sixth one with say 20 AUs, it waits in the job queue and start to run when 20 AUs are available.</span><span class="sxs-lookup"><span data-stu-id="96658-132">You may already have 5 jobs running and each submitted with 50 AUs, when you submit the sixth one with say 20 AUs, it waits in the job queue and start to run when 20 AUs are available.</span></span>
* <span data-ttu-id="96658-133">**Max number of concurrent U-SQL jobs per account:** 20.</span><span class="sxs-lookup"><span data-stu-id="96658-133">**Max number of concurrent U-SQL jobs per account:** 20.</span></span> <span data-ttu-id="96658-134">This is the maximum number of jobs that can run concurrently in your account.</span><span class="sxs-lookup"><span data-stu-id="96658-134">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="96658-135">Exceeding this value causes newer jobs to be queued automatically.</span><span class="sxs-lookup"><span data-stu-id="96658-135">Exceeding this value causes newer jobs to be queued automatically.</span></span>

<span data-ttu-id="96658-136">**To adjust ADLA Quota limits per account:**</span><span class="sxs-lookup"><span data-stu-id="96658-136">**To adjust ADLA Quota limits per account:**</span></span>
1. <span data-ttu-id="96658-137">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96658-137">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="96658-138">Choose the ADLA account you already created</span><span class="sxs-lookup"><span data-stu-id="96658-138">Choose the ADLA account you already created</span></span>
3. <span data-ttu-id="96658-139">Click **Properties**</span><span class="sxs-lookup"><span data-stu-id="96658-139">Click **Properties**</span></span>
4. <span data-ttu-id="96658-140">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span><span class="sxs-lookup"><span data-stu-id="96658-140">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

<span data-ttu-id="96658-142">**To increase the max quota limits:**</span><span class="sxs-lookup"><span data-stu-id="96658-142">**To increase the max quota limits:**</span></span>
1. <span data-ttu-id="96658-143">Open a support request in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="96658-143">Open a support request in Azure Portal.</span></span>

    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="96658-146">Select the issue type as **Quota**</span><span class="sxs-lookup"><span data-stu-id="96658-146">Select the issue type as **Quota**</span></span>
3. <span data-ttu-id="96658-147">Select your **Subscription** (Make sure it is not a “trial” subscription).</span><span class="sxs-lookup"><span data-stu-id="96658-147">Select your **Subscription** (Make sure it is not a “trial” subscription).</span></span>
4. <span data-ttu-id="96658-148">Select quota type as **Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="96658-148">Select quota type as **Data Lake Analytics**</span></span>

    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5.  <span data-ttu-id="96658-150">In the problem blade, please explain your requested increase limit and **Details** of why you need this extra capacity.</span><span class="sxs-lookup"><span data-stu-id="96658-150">In the problem blade, please explain your requested increase limit and **Details** of why you need this extra capacity.</span></span>

    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6.  <span data-ttu-id="96658-152">Verify your contact information and Create the support request.</span><span class="sxs-lookup"><span data-stu-id="96658-152">Verify your contact information and Create the support request.</span></span>

<span data-ttu-id="96658-153">We review your request and try to accommodate your business needs ASAP.</span><span class="sxs-lookup"><span data-stu-id="96658-153">We review your request and try to accommodate your business needs ASAP.</span></span>

## <a name="see-also"></a><span data-ttu-id="96658-154">See also</span><span class="sxs-lookup"><span data-stu-id="96658-154">See also</span></span>
* [<span data-ttu-id="96658-155">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="96658-155">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="96658-156">Get started with Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="96658-156">Get started with Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="96658-157">Manage Azure Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="96658-157">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="96658-158">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span><span class="sxs-lookup"><span data-stu-id="96658-158">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)





