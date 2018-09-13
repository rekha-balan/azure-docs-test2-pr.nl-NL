---
title: Service quotas and limits for Azure Batch | Microsoft Docs
description: Learn about default Azure Batch quotas, limits, and constraints, and how to request quota increases
services: batch
documentationcenter: ''
author: tamram
manager: timlt
editor: ''
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f6308101de57274796e0533317359dc1133f431
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555121"
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="a7770-103">Batch service quotas and limits</span><span class="sxs-lookup"><span data-stu-id="a7770-103">Batch service quotas and limits</span></span>

<span data-ttu-id="a7770-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span><span class="sxs-lookup"><span data-stu-id="a7770-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="a7770-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span><span class="sxs-lookup"><span data-stu-id="a7770-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="a7770-106">This article discusses those defaults, and how you can request quota increases.</span><span class="sxs-lookup"><span data-stu-id="a7770-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="a7770-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span><span class="sxs-lookup"><span data-stu-id="a7770-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="a7770-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account.</span><span class="sxs-lookup"><span data-stu-id="a7770-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account.</span></span>

<span data-ttu-id="a7770-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span><span class="sxs-lookup"><span data-stu-id="a7770-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="a7770-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span><span class="sxs-lookup"><span data-stu-id="a7770-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="a7770-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span><span class="sxs-lookup"><span data-stu-id="a7770-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="a7770-112">A quota is a credit limit, not a capacity guarantee.</span><span class="sxs-lookup"><span data-stu-id="a7770-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="a7770-113">If you have large-scale capacity needs, please contact Azure support.</span><span class="sxs-lookup"><span data-stu-id="a7770-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="a7770-114">Resource quotas</span><span class="sxs-lookup"><span data-stu-id="a7770-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="other-limits"></a><span data-ttu-id="a7770-115">Other limits</span><span class="sxs-lookup"><span data-stu-id="a7770-115">Other limits</span></span>
| <span data-ttu-id="a7770-116">**Resource**</span><span class="sxs-lookup"><span data-stu-id="a7770-116">**Resource**</span></span> | <span data-ttu-id="a7770-117">**Maximum Limit**</span><span class="sxs-lookup"><span data-stu-id="a7770-117">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="a7770-118">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span><span class="sxs-lookup"><span data-stu-id="a7770-118">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="a7770-119">4 x number of node cores</span><span class="sxs-lookup"><span data-stu-id="a7770-119">4 x number of node cores</span></span> |
| <span data-ttu-id="a7770-120">[Applications](batch-application-packages.md) per Batch account</span><span class="sxs-lookup"><span data-stu-id="a7770-120">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="a7770-121">20</span><span class="sxs-lookup"><span data-stu-id="a7770-121">20</span></span> |
| <span data-ttu-id="a7770-122">Application packages per application</span><span class="sxs-lookup"><span data-stu-id="a7770-122">Application packages per application</span></span> |<span data-ttu-id="a7770-123">40</span><span class="sxs-lookup"><span data-stu-id="a7770-123">40</span></span> |
| <span data-ttu-id="a7770-124">Application package size (each)</span><span class="sxs-lookup"><span data-stu-id="a7770-124">Application package size (each)</span></span> |<span data-ttu-id="a7770-125">Approx. 195GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a7770-125">Approx. 195GB<sup>1</sup></span></span> |

<span data-ttu-id="a7770-126"><sup>1</sup> Azure Storage limit for maximum block blob size</span><span class="sxs-lookup"><span data-stu-id="a7770-126"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="a7770-127">View Batch quotas</span><span class="sxs-lookup"><span data-stu-id="a7770-127">View Batch quotas</span></span>
<span data-ttu-id="a7770-128">View your Batch account quotas in the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="a7770-128">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="a7770-129">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span><span class="sxs-lookup"><span data-stu-id="a7770-129">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="a7770-130">Select **Properties** on the Batch account's menu blade</span><span class="sxs-lookup"><span data-stu-id="a7770-130">Select **Properties** on the Batch account's menu blade</span></span>
3. <span data-ttu-id="a7770-131">The Properties blade displays the **quotas** currently applied to the Batch account</span><span class="sxs-lookup"><span data-stu-id="a7770-131">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![Batch account quotas][account_quotas]

## <a name="increase-a-quota"></a><span data-ttu-id="a7770-133">Increase a quota</span><span class="sxs-lookup"><span data-stu-id="a7770-133">Increase a quota</span></span>
<span data-ttu-id="a7770-134">Follow these steps to request a quota increase using the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="a7770-134">Follow these steps to request a quota increase using the [Azure portal][portal].</span></span>

1. <span data-ttu-id="a7770-135">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span><span class="sxs-lookup"><span data-stu-id="a7770-135">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="a7770-136">Select **New support request** > **Basics**.</span><span class="sxs-lookup"><span data-stu-id="a7770-136">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="a7770-137">On the **Basics** blade:</span><span class="sxs-lookup"><span data-stu-id="a7770-137">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="a7770-138">a.</span><span class="sxs-lookup"><span data-stu-id="a7770-138">a.</span></span> <span data-ttu-id="a7770-139">**Issue Type** > **Quota**</span><span class="sxs-lookup"><span data-stu-id="a7770-139">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="a7770-140">b.</span><span class="sxs-lookup"><span data-stu-id="a7770-140">b.</span></span> <span data-ttu-id="a7770-141">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="a7770-141">Select your subscription.</span></span>
   
    <span data-ttu-id="a7770-142">c.</span><span class="sxs-lookup"><span data-stu-id="a7770-142">c.</span></span> <span data-ttu-id="a7770-143">**Quota type** > **Batch**</span><span class="sxs-lookup"><span data-stu-id="a7770-143">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="a7770-144">d.</span><span class="sxs-lookup"><span data-stu-id="a7770-144">d.</span></span> <span data-ttu-id="a7770-145">**Support plan** > **Quota support - Included**</span><span class="sxs-lookup"><span data-stu-id="a7770-145">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="a7770-146">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a7770-146">Click **Next**.</span></span>
4. <span data-ttu-id="a7770-147">On the **Problem** blade:</span><span class="sxs-lookup"><span data-stu-id="a7770-147">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="a7770-148">a.</span><span class="sxs-lookup"><span data-stu-id="a7770-148">a.</span></span> <span data-ttu-id="a7770-149">Select a **Severity** according to your [business impact][support_sev].</span><span class="sxs-lookup"><span data-stu-id="a7770-149">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="a7770-150">b.</span><span class="sxs-lookup"><span data-stu-id="a7770-150">b.</span></span> <span data-ttu-id="a7770-151">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span><span class="sxs-lookup"><span data-stu-id="a7770-151">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="a7770-152">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a7770-152">Click **Next**.</span></span>
5. <span data-ttu-id="a7770-153">On the **Contact information** blade:</span><span class="sxs-lookup"><span data-stu-id="a7770-153">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="a7770-154">a.</span><span class="sxs-lookup"><span data-stu-id="a7770-154">a.</span></span> <span data-ttu-id="a7770-155">Select a **Preferred contact method**.</span><span class="sxs-lookup"><span data-stu-id="a7770-155">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="a7770-156">b.</span><span class="sxs-lookup"><span data-stu-id="a7770-156">b.</span></span> <span data-ttu-id="a7770-157">Verify and enter the required contact details.</span><span class="sxs-lookup"><span data-stu-id="a7770-157">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="a7770-158">Click **Create** to submit the support request.</span><span class="sxs-lookup"><span data-stu-id="a7770-158">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="a7770-159">Once you've submitted your support request, Azure support will contact you.</span><span class="sxs-lookup"><span data-stu-id="a7770-159">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="a7770-160">Note that completing the request can take up to 2 business days.</span><span class="sxs-lookup"><span data-stu-id="a7770-160">Note that completing the request can take up to 2 business days.</span></span>

## <a name="related-topics"></a><span data-ttu-id="a7770-161">Related topics</span><span class="sxs-lookup"><span data-stu-id="a7770-161">Related topics</span></span>
* [<span data-ttu-id="a7770-162">Create an Azure Batch account using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a7770-162">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="a7770-163">Azure Batch feature overview</span><span class="sxs-lookup"><span data-stu-id="a7770-163">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="a7770-164">Azure subscription and service limits, quotas, and constraints</span><span class="sxs-lookup"><span data-stu-id="a7770-164">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-quota-limit/accountquota_portal.PNG

