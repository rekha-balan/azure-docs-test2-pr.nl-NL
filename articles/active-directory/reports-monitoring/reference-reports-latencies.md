---
title: Azure Active Directory reporting latencies | Microsoft Docs
description: Learn about the amount of time it takes for reporting events to show up in your Azure portal
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 12/15/2017
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 66e974e80fa6f5e002b1f54584ea48e22a7b13ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855597"
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="35f42-103">Azure Active Directory reporting latencies</span><span class="sxs-lookup"><span data-stu-id="35f42-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="35f42-104">With [reporting](../active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span><span class="sxs-lookup"><span data-stu-id="35f42-104">With [reporting](../active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="35f42-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span><span class="sxs-lookup"><span data-stu-id="35f42-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="35f42-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="35f42-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="35f42-107">Activity reports</span><span class="sxs-lookup"><span data-stu-id="35f42-107">Activity reports</span></span>

<span data-ttu-id="35f42-108">There are two areas of activity reporting:</span><span class="sxs-lookup"><span data-stu-id="35f42-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="35f42-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span><span class="sxs-lookup"><span data-stu-id="35f42-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="35f42-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span><span class="sxs-lookup"><span data-stu-id="35f42-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="35f42-111">The following table lists the latency information for activity reports.</span><span class="sxs-lookup"><span data-stu-id="35f42-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="35f42-112">Report</span><span class="sxs-lookup"><span data-stu-id="35f42-112">Report</span></span> | <span data-ttu-id="35f42-113">Latency (95%)</span><span class="sxs-lookup"><span data-stu-id="35f42-113">Latency (95%)</span></span> |<span data-ttu-id="35f42-114">Latency (99%)</span><span class="sxs-lookup"><span data-stu-id="35f42-114">Latency (99%)</span></span>|
| :-- | --- | --- | 
| <span data-ttu-id="35f42-115">Audit logs</span><span class="sxs-lookup"><span data-stu-id="35f42-115">Audit logs</span></span> | <span data-ttu-id="35f42-116">2 mins</span><span class="sxs-lookup"><span data-stu-id="35f42-116">2 mins</span></span>  | <span data-ttu-id="35f42-117">5 mins</span><span class="sxs-lookup"><span data-stu-id="35f42-117">5 mins</span></span>  |
| <span data-ttu-id="35f42-118">Sign-ins</span><span class="sxs-lookup"><span data-stu-id="35f42-118">Sign-ins</span></span> | <span data-ttu-id="35f42-119">2 mins</span><span class="sxs-lookup"><span data-stu-id="35f42-119">2 mins</span></span>  | <span data-ttu-id="35f42-120">5 mins</span><span class="sxs-lookup"><span data-stu-id="35f42-120">5 mins</span></span> |







## <a name="security-reports"></a><span data-ttu-id="35f42-121">Security reports</span><span class="sxs-lookup"><span data-stu-id="35f42-121">Security reports</span></span>

<span data-ttu-id="35f42-122">There are two areas of security reporting:</span><span class="sxs-lookup"><span data-stu-id="35f42-122">There are two areas of security reporting:</span></span>

- <span data-ttu-id="35f42-123">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="35f42-123">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="35f42-124">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="35f42-124">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="35f42-125">The following table lists the latency information for security reports.</span><span class="sxs-lookup"><span data-stu-id="35f42-125">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="35f42-126">Report</span><span class="sxs-lookup"><span data-stu-id="35f42-126">Report</span></span> | <span data-ttu-id="35f42-127">Minimum</span><span class="sxs-lookup"><span data-stu-id="35f42-127">Minimum</span></span> | <span data-ttu-id="35f42-128">Average</span><span class="sxs-lookup"><span data-stu-id="35f42-128">Average</span></span> | <span data-ttu-id="35f42-129">Maximum</span><span class="sxs-lookup"><span data-stu-id="35f42-129">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="35f42-130">Users at risk</span><span class="sxs-lookup"><span data-stu-id="35f42-130">Users at risk</span></span>          | <span data-ttu-id="35f42-131">5 minutes</span><span class="sxs-lookup"><span data-stu-id="35f42-131">5 minutes</span></span>   | <span data-ttu-id="35f42-132">15 minutes</span><span class="sxs-lookup"><span data-stu-id="35f42-132">15 minutes</span></span>  | <span data-ttu-id="35f42-133">2 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-133">2 hours</span></span>  |
| <span data-ttu-id="35f42-134">Risky sign-ins</span><span class="sxs-lookup"><span data-stu-id="35f42-134">Risky sign-ins</span></span>         | <span data-ttu-id="35f42-135">5 minutes</span><span class="sxs-lookup"><span data-stu-id="35f42-135">5 minutes</span></span>   | <span data-ttu-id="35f42-136">15 minutes</span><span class="sxs-lookup"><span data-stu-id="35f42-136">15 minutes</span></span>  | <span data-ttu-id="35f42-137">2 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-137">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="35f42-138">Risk events</span><span class="sxs-lookup"><span data-stu-id="35f42-138">Risk events</span></span>

<span data-ttu-id="35f42-139">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span><span class="sxs-lookup"><span data-stu-id="35f42-139">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="35f42-140">Each detected suspicious action is stored in a record called risk event.</span><span class="sxs-lookup"><span data-stu-id="35f42-140">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="35f42-141">The following table lists the latency information for risk events.</span><span class="sxs-lookup"><span data-stu-id="35f42-141">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="35f42-142">Report</span><span class="sxs-lookup"><span data-stu-id="35f42-142">Report</span></span> | <span data-ttu-id="35f42-143">Minimum</span><span class="sxs-lookup"><span data-stu-id="35f42-143">Minimum</span></span> | <span data-ttu-id="35f42-144">Average</span><span class="sxs-lookup"><span data-stu-id="35f42-144">Average</span></span> | <span data-ttu-id="35f42-145">Maximum</span><span class="sxs-lookup"><span data-stu-id="35f42-145">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="35f42-146">Sign-ins from anonymous IP addresses</span><span class="sxs-lookup"><span data-stu-id="35f42-146">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="35f42-147">5 minutes</span><span class="sxs-lookup"><span data-stu-id="35f42-147">5 minutes</span></span> |<span data-ttu-id="35f42-148">15 Minutes</span><span class="sxs-lookup"><span data-stu-id="35f42-148">15 Minutes</span></span> |<span data-ttu-id="35f42-149">2 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-149">2 hours</span></span> |
| <span data-ttu-id="35f42-150">Sign-ins from unfamiliar locations</span><span class="sxs-lookup"><span data-stu-id="35f42-150">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="35f42-151">5 minutes</span><span class="sxs-lookup"><span data-stu-id="35f42-151">5 minutes</span></span> |<span data-ttu-id="35f42-152">15 Minutes</span><span class="sxs-lookup"><span data-stu-id="35f42-152">15 Minutes</span></span> |<span data-ttu-id="35f42-153">2 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-153">2 hours</span></span> |
| <span data-ttu-id="35f42-154">Users with leaked credentials</span><span class="sxs-lookup"><span data-stu-id="35f42-154">Users with leaked credentials</span></span> |<span data-ttu-id="35f42-155">2 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-155">2 hours</span></span> |<span data-ttu-id="35f42-156">4 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-156">4 hours</span></span> |<span data-ttu-id="35f42-157">8 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-157">8 hours</span></span> |
| <span data-ttu-id="35f42-158">Impossible travel to atypical locations</span><span class="sxs-lookup"><span data-stu-id="35f42-158">Impossible travel to atypical locations</span></span> |<span data-ttu-id="35f42-159">5 minutes</span><span class="sxs-lookup"><span data-stu-id="35f42-159">5 minutes</span></span> |<span data-ttu-id="35f42-160">1 hour</span><span class="sxs-lookup"><span data-stu-id="35f42-160">1 hour</span></span> |<span data-ttu-id="35f42-161">8 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-161">8 hours</span></span>  |
| <span data-ttu-id="35f42-162">Sign-ins from infected devices</span><span class="sxs-lookup"><span data-stu-id="35f42-162">Sign-ins from infected devices</span></span> |<span data-ttu-id="35f42-163">2 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-163">2 hours</span></span> |<span data-ttu-id="35f42-164">4 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-164">4 hours</span></span> |<span data-ttu-id="35f42-165">8 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-165">8 hours</span></span>  |
| <span data-ttu-id="35f42-166">Sign-ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="35f42-166">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="35f42-167">2 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-167">2 hours</span></span> |<span data-ttu-id="35f42-168">4 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-168">4 hours</span></span> |<span data-ttu-id="35f42-169">8 hours</span><span class="sxs-lookup"><span data-stu-id="35f42-169">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="35f42-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="35f42-170">Next steps</span></span>

<span data-ttu-id="35f42-171">If you want to know more about the activity reports in the Azure portal, see:</span><span class="sxs-lookup"><span data-stu-id="35f42-171">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="35f42-172">Sign-in activity reports in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="35f42-172">Sign-in activity reports in the Azure Active Directory portal</span></span>](concept-sign-ins.md)
- [<span data-ttu-id="35f42-173">Audit activity reports in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="35f42-173">Audit activity reports in the Azure Active Directory portal</span></span>](concept-audit-logs.md)

<span data-ttu-id="35f42-174">If you want to know more about the security reports in the Azure portal, see:</span><span class="sxs-lookup"><span data-stu-id="35f42-174">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="35f42-175">Users at risk security report in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="35f42-175">Users at risk security report in the Azure Active Directory portal</span></span>](concept-user-at-risk.md)
- [<span data-ttu-id="35f42-176">Risky sign-ins report in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="35f42-176">Risky sign-ins report in the Azure Active Directory portal</span></span>](concept-risky-sign-ins.md)

<span data-ttu-id="35f42-177">If you want to know more about risk events, see [Azure Active Directory risk events](concept-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="35f42-177">If you want to know more about risk events, see [Azure Active Directory risk events](concept-risk-events.md).</span></span>
