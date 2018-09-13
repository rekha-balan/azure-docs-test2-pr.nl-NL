---
title: Service quotas and limits for Azure Batch AI | Microsoft Docs
description: Learn about default Azure Batch AI quotas, limits, and constraints, and how to request quota increases
services: batch-ai
documentationcenter: ''
author: johnwu10
manager: jeconnoc
editor: ''
ms.service: batch-ai
ms.topic: article
ms.date: 08/08/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: cade124cefbd4e2e63ab4cb6fa4f22b3bd672ad0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867912"
---
# <a name="batch-ai-service-quotas-and-limits"></a><span data-ttu-id="cc193-103">Batch AI service quotas and limits</span><span class="sxs-lookup"><span data-stu-id="cc193-103">Batch AI service quotas and limits</span></span>

<span data-ttu-id="cc193-104">As with other Azure services, there are limits on certain resources associated with the Batch AI service.</span><span class="sxs-lookup"><span data-stu-id="cc193-104">As with other Azure services, there are limits on certain resources associated with the Batch AI service.</span></span> <span data-ttu-id="cc193-105">In Batch AI, these limits are default quotas applied at the subscription level for each region where the service is [available](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="cc193-105">In Batch AI, these limits are default quotas applied at the subscription level for each region where the service is [available](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="cc193-106">This article discusses those defaults, and how you can request quota increases.</span><span class="sxs-lookup"><span data-stu-id="cc193-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="cc193-107">Keep these quotas in mind as you design and scale up your Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="cc193-107">Keep these quotas in mind as you design and scale up your Batch AI resources.</span></span> <span data-ttu-id="cc193-108">For example, if your cluster doesn't reach the target number of nodes you specified, then you might have reached a Batch AI cores limit for your subscription.</span><span class="sxs-lookup"><span data-stu-id="cc193-108">For example, if your cluster doesn't reach the target number of nodes you specified, then you might have reached a Batch AI cores limit for your subscription.</span></span>

<span data-ttu-id="cc193-109">If you plan to run production workloads in Batch AI, you may need to increase one or more of the quotas above the default.</span><span class="sxs-lookup"><span data-stu-id="cc193-109">If you plan to run production workloads in Batch AI, you may need to increase one or more of the quotas above the default.</span></span>

> [!NOTE]
> <span data-ttu-id="cc193-110">A quota is a credit limit, not a capacity guarantee.</span><span class="sxs-lookup"><span data-stu-id="cc193-110">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="cc193-111">If you have large-scale capacity needs, please contact Azure support.</span><span class="sxs-lookup"><span data-stu-id="cc193-111">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="cc193-112">Resource quotas</span><span class="sxs-lookup"><span data-stu-id="cc193-112">Resource quotas</span></span>

[!INCLUDE [azure-batch-ai-limits](../../includes/azure-batch-ai-limits.md)]

## <a name="other-limits"></a><span data-ttu-id="cc193-113">Other limits</span><span class="sxs-lookup"><span data-stu-id="cc193-113">Other limits</span></span>

<span data-ttu-id="cc193-114">The following are strict limits, which cannot be exceeded once hit.</span><span class="sxs-lookup"><span data-stu-id="cc193-114">The following are strict limits, which cannot be exceeded once hit.</span></span>

| <span data-ttu-id="cc193-115">**Resource**</span><span class="sxs-lookup"><span data-stu-id="cc193-115">**Resource**</span></span> | <span data-ttu-id="cc193-116">**Maximum limit**</span><span class="sxs-lookup"><span data-stu-id="cc193-116">**Maximum limit**</span></span> |
| --- | --- |
| <span data-ttu-id="cc193-117">Maximum workspaces per resource group</span><span class="sxs-lookup"><span data-stu-id="cc193-117">Maximum workspaces per resource group</span></span> | <span data-ttu-id="cc193-118">800</span><span class="sxs-lookup"><span data-stu-id="cc193-118">800</span></span> |
| <span data-ttu-id="cc193-119">Maximum cluster size</span><span class="sxs-lookup"><span data-stu-id="cc193-119">Maximum cluster size</span></span> | <span data-ttu-id="cc193-120">100 nodes</span><span class="sxs-lookup"><span data-stu-id="cc193-120">100 nodes</span></span> |
| <span data-ttu-id="cc193-121">Maximum GPU MPI processes per node</span><span class="sxs-lookup"><span data-stu-id="cc193-121">Maximum GPU MPI processes per node</span></span> | <span data-ttu-id="cc193-122">1-4</span><span class="sxs-lookup"><span data-stu-id="cc193-122">1-4</span></span> |
| <span data-ttu-id="cc193-123">Maximum GPU workers per node</span><span class="sxs-lookup"><span data-stu-id="cc193-123">Maximum GPU workers per node</span></span> | <span data-ttu-id="cc193-124">1-4</span><span class="sxs-lookup"><span data-stu-id="cc193-124">1-4</span></span> |
| <span data-ttu-id="cc193-125">Maximum job lifetime</span><span class="sxs-lookup"><span data-stu-id="cc193-125">Maximum job lifetime</span></span> | <span data-ttu-id="cc193-126">7 days<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="cc193-126">7 days<sup>1</sup></span></span> |
| <span data-ttu-id="cc193-127">Maximum parameter servers per node</span><span class="sxs-lookup"><span data-stu-id="cc193-127">Maximum parameter servers per node</span></span> | <span data-ttu-id="cc193-128">1</span><span class="sxs-lookup"><span data-stu-id="cc193-128">1</span></span> |

<span data-ttu-id="cc193-129"><sup>1</sup> The maximum lifetime refers to the time that a job begins running and when it completes.</span><span class="sxs-lookup"><span data-stu-id="cc193-129"><sup>1</sup> The maximum lifetime refers to the time that a job begins running and when it completes.</span></span> <span data-ttu-id="cc193-130">Completed jobs persist indefinitely; data for jobs not completed within the maximum lifetime is not accessible.</span><span class="sxs-lookup"><span data-stu-id="cc193-130">Completed jobs persist indefinitely; data for jobs not completed within the maximum lifetime is not accessible.</span></span>

## <a name="view-batch-ai-quotas"></a><span data-ttu-id="cc193-131">View Batch AI quotas</span><span class="sxs-lookup"><span data-stu-id="cc193-131">View Batch AI quotas</span></span>

<span data-ttu-id="cc193-132">View your current Batch AI subscription quotas in the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="cc193-132">View your current Batch AI subscription quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="cc193-133">On the left pane, click on **All services**.</span><span class="sxs-lookup"><span data-stu-id="cc193-133">On the left pane, click on **All services**.</span></span> <span data-ttu-id="cc193-134">Then search for **Batch AI** and click to open the service.</span><span class="sxs-lookup"><span data-stu-id="cc193-134">Then search for **Batch AI** and click to open the service.</span></span>
2. <span data-ttu-id="cc193-135">Click on **Usage + quotas** on the Batch AI menu.</span><span class="sxs-lookup"><span data-stu-id="cc193-135">Click on **Usage + quotas** on the Batch AI menu.</span></span>
3. <span data-ttu-id="cc193-136">Select your subscription to view the quota limits.</span><span class="sxs-lookup"><span data-stu-id="cc193-136">Select your subscription to view the quota limits.</span></span>

## <a name="increase-a-batch-ai-cores-quota"></a><span data-ttu-id="cc193-137">Increase a Batch AI cores quota</span><span class="sxs-lookup"><span data-stu-id="cc193-137">Increase a Batch AI cores quota</span></span>

<span data-ttu-id="cc193-138">Follow these steps to request a quota increase for your Batch AI subscription using the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="cc193-138">Follow these steps to request a quota increase for your Batch AI subscription using the [Azure portal][portal].</span></span> 

1. <span data-ttu-id="cc193-139">On the left pane, click on **All services**.</span><span class="sxs-lookup"><span data-stu-id="cc193-139">On the left pane, click on **All services**.</span></span> <span data-ttu-id="cc193-140">Then search for **Batch AI** and click to open the service.</span><span class="sxs-lookup"><span data-stu-id="cc193-140">Then search for **Batch AI** and click to open the service.</span></span>
2. <span data-ttu-id="cc193-141">Click on **New support request** on the Batch AI menu.</span><span class="sxs-lookup"><span data-stu-id="cc193-141">Click on **New support request** on the Batch AI menu.</span></span>
3. <span data-ttu-id="cc193-142">In **Basics**:</span><span class="sxs-lookup"><span data-stu-id="cc193-142">In **Basics**:</span></span>
   
    <span data-ttu-id="cc193-143">a.</span><span class="sxs-lookup"><span data-stu-id="cc193-143">a.</span></span> <span data-ttu-id="cc193-144">**Issue Type** > **Quota**</span><span class="sxs-lookup"><span data-stu-id="cc193-144">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="cc193-145">b.</span><span class="sxs-lookup"><span data-stu-id="cc193-145">b.</span></span> <span data-ttu-id="cc193-146">**Subscription** > Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="cc193-146">**Subscription** > Select your subscription.</span></span>
   
    <span data-ttu-id="cc193-147">c.</span><span class="sxs-lookup"><span data-stu-id="cc193-147">c.</span></span> <span data-ttu-id="cc193-148">**Quota type** > **Batch AI**</span><span class="sxs-lookup"><span data-stu-id="cc193-148">**Quota type** > **Batch AI**</span></span>
   
    <span data-ttu-id="cc193-149">d.</span><span class="sxs-lookup"><span data-stu-id="cc193-149">d.</span></span> <span data-ttu-id="cc193-150">**Support plan** > Select your support plan.</span><span class="sxs-lookup"><span data-stu-id="cc193-150">**Support plan** > Select your support plan.</span></span>

    <span data-ttu-id="cc193-151">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cc193-151">Click **Next**.</span></span>
4. <span data-ttu-id="cc193-152">In **Problem**:</span><span class="sxs-lookup"><span data-stu-id="cc193-152">In **Problem**:</span></span>
   
    <span data-ttu-id="cc193-153">a.</span><span class="sxs-lookup"><span data-stu-id="cc193-153">a.</span></span> <span data-ttu-id="cc193-154">Select a **Severity** according to your [business impact][support_sev].</span><span class="sxs-lookup"><span data-stu-id="cc193-154">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="cc193-155">b.</span><span class="sxs-lookup"><span data-stu-id="cc193-155">b.</span></span> <span data-ttu-id="cc193-156">In **Quota Details**, specify the location, quota type, and resource type.</span><span class="sxs-lookup"><span data-stu-id="cc193-156">In **Quota Details**, specify the location, quota type, and resource type.</span></span> <span data-ttu-id="cc193-157">Specify the new limit you want to request.</span><span class="sxs-lookup"><span data-stu-id="cc193-157">Specify the new limit you want to request.</span></span> <span data-ttu-id="cc193-158">Click **Save and continue**.</span><span class="sxs-lookup"><span data-stu-id="cc193-158">Click **Save and continue**.</span></span>

    <span data-ttu-id="cc193-159">c.</span><span class="sxs-lookup"><span data-stu-id="cc193-159">c.</span></span> <span data-ttu-id="cc193-160">Optional - Upload any relevant files with more information regarding your reason for increase.</span><span class="sxs-lookup"><span data-stu-id="cc193-160">Optional - Upload any relevant files with more information regarding your reason for increase.</span></span>
   
    <span data-ttu-id="cc193-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cc193-161">Click **Next**.</span></span>
5. <span data-ttu-id="cc193-162">In **Contact information**:</span><span class="sxs-lookup"><span data-stu-id="cc193-162">In **Contact information**:</span></span>
   
    <span data-ttu-id="cc193-163">a.</span><span class="sxs-lookup"><span data-stu-id="cc193-163">a.</span></span> <span data-ttu-id="cc193-164">Select a **Preferred contact method**.</span><span class="sxs-lookup"><span data-stu-id="cc193-164">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="cc193-165">b.</span><span class="sxs-lookup"><span data-stu-id="cc193-165">b.</span></span> <span data-ttu-id="cc193-166">Verify and enter the required contact details.</span><span class="sxs-lookup"><span data-stu-id="cc193-166">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="cc193-167">Click **Create** to submit the support request.</span><span class="sxs-lookup"><span data-stu-id="cc193-167">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="cc193-168">Once you've submitted your support request, Azure support will contact you.</span><span class="sxs-lookup"><span data-stu-id="cc193-168">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="cc193-169">Completing the request can take up to 2 business days.</span><span class="sxs-lookup"><span data-stu-id="cc193-169">Completing the request can take up to 2 business days.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cc193-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc193-170">Next steps</span></span>

<span data-ttu-id="cc193-171">After becoming familiar with the quota limits, check out the following articles for getting started with using Batch AI.</span><span class="sxs-lookup"><span data-stu-id="cc193-171">After becoming familiar with the quota limits, check out the following articles for getting started with using Batch AI.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="cc193-172">[Batch AI quick start tutorial](quickstart-tensorflow-training-cli.md)
> [Batch AI recipes](https://github.com/Azure/BatchAI/tree/master/recipes)
> [Learn more about Batch AI resources](resource-concepts.md)</span><span class="sxs-lookup"><span data-stu-id="cc193-172">[Batch AI quick start tutorial](quickstart-tensorflow-training-cli.md)
[Batch AI recipes](https://github.com/Azure/BatchAI/tree/master/recipes)
[Learn more about Batch AI resources](resource-concepts.md)</span></span>

[portal]: https://portal.azure.com
[support_sev]: http://aka.ms/supportseverity