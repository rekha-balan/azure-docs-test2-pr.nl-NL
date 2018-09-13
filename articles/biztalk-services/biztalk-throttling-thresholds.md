---
title: Learn about Throttling in BizTalk Services | Microsoft Docs
description: Learn about throttling thresholds and resulting runtime behaviors for BizTalk Services. Throttling is based on memory usage and number of messages. MABS, WABS
services: biztalk-services
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: e14f42497d5ee0c89fe1fa0824431e2d82e6555a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552151"
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="659b1-105">BizTalk Services: Throttling</span><span class="sxs-lookup"><span data-stu-id="659b1-105">BizTalk Services: Throttling</span></span>
<span data-ttu-id="659b1-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span><span class="sxs-lookup"><span data-stu-id="659b1-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="659b1-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span><span class="sxs-lookup"><span data-stu-id="659b1-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="659b1-108">Throttling Thresholds</span><span class="sxs-lookup"><span data-stu-id="659b1-108">Throttling Thresholds</span></span>
<span data-ttu-id="659b1-109">The following table lists the throttling source and thresholds:</span><span class="sxs-lookup"><span data-stu-id="659b1-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="659b1-110">Description</span><span class="sxs-lookup"><span data-stu-id="659b1-110">Description</span></span> | <span data-ttu-id="659b1-111">Low Threshold</span><span class="sxs-lookup"><span data-stu-id="659b1-111">Low Threshold</span></span> | <span data-ttu-id="659b1-112">High Threshold</span><span class="sxs-lookup"><span data-stu-id="659b1-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="659b1-113">Memory</span><span class="sxs-lookup"><span data-stu-id="659b1-113">Memory</span></span> |<span data-ttu-id="659b1-114">% of total system memory available/PageFileBytes.</span><span class="sxs-lookup"><span data-stu-id="659b1-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="659b1-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span><span class="sxs-lookup"><span data-stu-id="659b1-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="659b1-116">60%</span><span class="sxs-lookup"><span data-stu-id="659b1-116">60%</span></span> |<span data-ttu-id="659b1-117">70%</span><span class="sxs-lookup"><span data-stu-id="659b1-117">70%</span></span> |
| <span data-ttu-id="659b1-118">Message Processing</span><span class="sxs-lookup"><span data-stu-id="659b1-118">Message Processing</span></span> |<span data-ttu-id="659b1-119">Number of messages processing simultaneously</span><span class="sxs-lookup"><span data-stu-id="659b1-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="659b1-120">40 \* number of cores</span><span class="sxs-lookup"><span data-stu-id="659b1-120">40 \* number of cores</span></span> |<span data-ttu-id="659b1-121">100 \* number of cores</span><span class="sxs-lookup"><span data-stu-id="659b1-121">100 \* number of cores</span></span> |

<span data-ttu-id="659b1-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span><span class="sxs-lookup"><span data-stu-id="659b1-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="659b1-123">Throttling stops when the low threshold is reached.</span><span class="sxs-lookup"><span data-stu-id="659b1-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="659b1-124">For example, your service is using 65% system memory.</span><span class="sxs-lookup"><span data-stu-id="659b1-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="659b1-125">In this situation, the service does not throttle.</span><span class="sxs-lookup"><span data-stu-id="659b1-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="659b1-126">Your service starts using 70% system memory.</span><span class="sxs-lookup"><span data-stu-id="659b1-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="659b1-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span><span class="sxs-lookup"><span data-stu-id="659b1-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="659b1-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span><span class="sxs-lookup"><span data-stu-id="659b1-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="659b1-129">Runtime Behavior</span><span class="sxs-lookup"><span data-stu-id="659b1-129">Runtime Behavior</span></span>
<span data-ttu-id="659b1-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span><span class="sxs-lookup"><span data-stu-id="659b1-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="659b1-131">Throttling is per role instance.</span><span class="sxs-lookup"><span data-stu-id="659b1-131">Throttling is per role instance.</span></span> <span data-ttu-id="659b1-132">For example:</span><span class="sxs-lookup"><span data-stu-id="659b1-132">For example:</span></span><br/>
  <span data-ttu-id="659b1-133">RoleInstanceA is throttling.</span><span class="sxs-lookup"><span data-stu-id="659b1-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="659b1-134">RoleInstanceB is not throttling.</span><span class="sxs-lookup"><span data-stu-id="659b1-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="659b1-135">In this situation, messages in RoleInstanceB are processed as expected.</span><span class="sxs-lookup"><span data-stu-id="659b1-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="659b1-136">Messages in RoleInstanceA are discarded and fail with the following error:</span><span class="sxs-lookup"><span data-stu-id="659b1-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/>
  <span data-ttu-id="659b1-137">**Server is busy. Please try again.**</span><span class="sxs-lookup"><span data-stu-id="659b1-137">**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="659b1-138">Any pull sources do not poll or download a message.</span><span class="sxs-lookup"><span data-stu-id="659b1-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="659b1-139">For example:</span><span class="sxs-lookup"><span data-stu-id="659b1-139">For example:</span></span><br/>
  <span data-ttu-id="659b1-140">A pipeline pulls messages from an external FTP source.</span><span class="sxs-lookup"><span data-stu-id="659b1-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="659b1-141">The role instance doing the pull gets into a throttling state.</span><span class="sxs-lookup"><span data-stu-id="659b1-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="659b1-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span><span class="sxs-lookup"><span data-stu-id="659b1-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="659b1-143">A response is sent to the client so the client can resubmit the message.</span><span class="sxs-lookup"><span data-stu-id="659b1-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="659b1-144">You must wait until the throttling is resolved.</span><span class="sxs-lookup"><span data-stu-id="659b1-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="659b1-145">Specifically, you must wait until the low threshold is reached.</span><span class="sxs-lookup"><span data-stu-id="659b1-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="659b1-146">Important notes</span><span class="sxs-lookup"><span data-stu-id="659b1-146">Important notes</span></span>
* <span data-ttu-id="659b1-147">Throttling cannot be disabled.</span><span class="sxs-lookup"><span data-stu-id="659b1-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="659b1-148">Throttling thresholds cannot be modified.</span><span class="sxs-lookup"><span data-stu-id="659b1-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="659b1-149">Throttling is implemented system-wide.</span><span class="sxs-lookup"><span data-stu-id="659b1-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="659b1-150">The Azure SQL Database Server also has built-in throttling.</span><span class="sxs-lookup"><span data-stu-id="659b1-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="659b1-151">Additional Azure BizTalk Services topics</span><span class="sxs-lookup"><span data-stu-id="659b1-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="659b1-152">Installing the Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="659b1-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="659b1-153">Tutorials: Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="659b1-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="659b1-154">How do I Start Using the Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="659b1-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="659b1-155">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="659b1-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="659b1-156">See Also</span><span class="sxs-lookup"><span data-stu-id="659b1-156">See Also</span></span>
* [<span data-ttu-id="659b1-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span><span class="sxs-lookup"><span data-stu-id="659b1-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="659b1-158">BizTalk Services: Provisioning Using Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="659b1-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="659b1-159">BizTalk Services: Provisioning Status Chart</span><span class="sxs-lookup"><span data-stu-id="659b1-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="659b1-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span><span class="sxs-lookup"><span data-stu-id="659b1-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="659b1-161">BizTalk Services: Backup and Restore</span><span class="sxs-lookup"><span data-stu-id="659b1-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="659b1-162">BizTalk Services: Issuer Name and Issuer Key</span><span class="sxs-lookup"><span data-stu-id="659b1-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

