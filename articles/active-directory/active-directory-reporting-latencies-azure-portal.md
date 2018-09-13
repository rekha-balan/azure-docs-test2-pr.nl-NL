---
title: Azure Active Directory reporting latencies | Microsoft Docs
description: Learn about the amount of time it takes for reporting events to show up in your Azure portal
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/07/2017
ms.author: markvi;dhanyahk
ms.openlocfilehash: 1c6b79c5f67cee5d62c9879bdeec926091253af6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552431"
---
# <a name="azure-active-directory-reporting-latencies---preview"></a><span data-ttu-id="ed55c-103">Azure Active Directory reporting latencies - preview</span><span class="sxs-lookup"><span data-stu-id="ed55c-103">Azure Active Directory reporting latencies - preview</span></span>

<span data-ttu-id="ed55c-104">With reporting in the Azure Active Directory [preview](active-directory-preview-explainer.md), you get all the information you need to determine how your environment is doing.</span><span class="sxs-lookup"><span data-stu-id="ed55c-104">With reporting in the Azure Active Directory [preview](active-directory-preview-explainer.md), you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="ed55c-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span><span class="sxs-lookup"><span data-stu-id="ed55c-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="ed55c-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ed55c-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="ed55c-107">Activity reports</span><span class="sxs-lookup"><span data-stu-id="ed55c-107">Activity reports</span></span>

<span data-ttu-id="ed55c-108">There are two areas of activity reporting:</span><span class="sxs-lookup"><span data-stu-id="ed55c-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="ed55c-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span><span class="sxs-lookup"><span data-stu-id="ed55c-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="ed55c-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span><span class="sxs-lookup"><span data-stu-id="ed55c-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="ed55c-111">The following table lists the latency information for activity reports.</span><span class="sxs-lookup"><span data-stu-id="ed55c-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="ed55c-112">Report</span><span class="sxs-lookup"><span data-stu-id="ed55c-112">Report</span></span> | <span data-ttu-id="ed55c-113">Minimum</span><span class="sxs-lookup"><span data-stu-id="ed55c-113">Minimum</span></span> | <span data-ttu-id="ed55c-114">Average</span><span class="sxs-lookup"><span data-stu-id="ed55c-114">Average</span></span> | <span data-ttu-id="ed55c-115">Maximum</span><span class="sxs-lookup"><span data-stu-id="ed55c-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="ed55c-116">Audit logs</span><span class="sxs-lookup"><span data-stu-id="ed55c-116">Audit logs</span></span>             | <span data-ttu-id="ed55c-117">30 minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-117">30 minutes</span></span>  | <span data-ttu-id="ed55c-118">45 Minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-118">45 Minutes</span></span> | <span data-ttu-id="ed55c-119">1 hour</span><span class="sxs-lookup"><span data-stu-id="ed55c-119">1 hour</span></span>     |
| <span data-ttu-id="ed55c-120">Sign-ins</span><span class="sxs-lookup"><span data-stu-id="ed55c-120">Sign-ins</span></span>               | <span data-ttu-id="ed55c-121">15 minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-121">15 minutes</span></span>  | <span data-ttu-id="ed55c-122">15 minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-122">15 minutes</span></span> | <span data-ttu-id="ed55c-123">2 hours\*</span><span class="sxs-lookup"><span data-stu-id="ed55c-123">2 hours\*</span></span>   |

>[!NOTE]
> <span data-ttu-id="ed55c-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span><span class="sxs-lookup"><span data-stu-id="ed55c-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="ed55c-125">Security reports</span><span class="sxs-lookup"><span data-stu-id="ed55c-125">Security reports</span></span>

<span data-ttu-id="ed55c-126">There are two areas of security reporting:</span><span class="sxs-lookup"><span data-stu-id="ed55c-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="ed55c-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="ed55c-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="ed55c-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="ed55c-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="ed55c-129">The following table lists the latency information for security reports.</span><span class="sxs-lookup"><span data-stu-id="ed55c-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="ed55c-130">Report</span><span class="sxs-lookup"><span data-stu-id="ed55c-130">Report</span></span> | <span data-ttu-id="ed55c-131">Minimum</span><span class="sxs-lookup"><span data-stu-id="ed55c-131">Minimum</span></span> | <span data-ttu-id="ed55c-132">Average</span><span class="sxs-lookup"><span data-stu-id="ed55c-132">Average</span></span> | <span data-ttu-id="ed55c-133">Maximum</span><span class="sxs-lookup"><span data-stu-id="ed55c-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="ed55c-134">Users at risk</span><span class="sxs-lookup"><span data-stu-id="ed55c-134">Users at risk</span></span>          | <span data-ttu-id="ed55c-135">5 minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-135">5 minutes</span></span>   | <span data-ttu-id="ed55c-136">15 minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-136">15 minutes</span></span>  | <span data-ttu-id="ed55c-137">2 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-137">2 hours</span></span>  |
| <span data-ttu-id="ed55c-138">Risky sign-ins</span><span class="sxs-lookup"><span data-stu-id="ed55c-138">Risky sign-ins</span></span>         | <span data-ttu-id="ed55c-139">5 minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-139">5 minutes</span></span>   | <span data-ttu-id="ed55c-140">15 minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-140">15 minutes</span></span>  | <span data-ttu-id="ed55c-141">2 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="ed55c-142">Risk events</span><span class="sxs-lookup"><span data-stu-id="ed55c-142">Risk events</span></span>

<span data-ttu-id="ed55c-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span><span class="sxs-lookup"><span data-stu-id="ed55c-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="ed55c-144">Each detected suspicious action is stored in a record called risk event.</span><span class="sxs-lookup"><span data-stu-id="ed55c-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="ed55c-145">The following table lists the latency information for risk events.</span><span class="sxs-lookup"><span data-stu-id="ed55c-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="ed55c-146">Report</span><span class="sxs-lookup"><span data-stu-id="ed55c-146">Report</span></span> | <span data-ttu-id="ed55c-147">Minimum</span><span class="sxs-lookup"><span data-stu-id="ed55c-147">Minimum</span></span> | <span data-ttu-id="ed55c-148">Average</span><span class="sxs-lookup"><span data-stu-id="ed55c-148">Average</span></span> | <span data-ttu-id="ed55c-149">Maximum</span><span class="sxs-lookup"><span data-stu-id="ed55c-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="ed55c-150">Sign-ins from anonymous IP addresses</span><span class="sxs-lookup"><span data-stu-id="ed55c-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="ed55c-151">5 minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-151">5 minutes</span></span> |<span data-ttu-id="ed55c-152">15 Minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-152">15 Minutes</span></span> |<span data-ttu-id="ed55c-153">2 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-153">2 hours</span></span> |
| <span data-ttu-id="ed55c-154">Sign-ins from unfamiliar locations</span><span class="sxs-lookup"><span data-stu-id="ed55c-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="ed55c-155">5 minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-155">5 minutes</span></span> |<span data-ttu-id="ed55c-156">15 Minutes</span><span class="sxs-lookup"><span data-stu-id="ed55c-156">15 Minutes</span></span> |<span data-ttu-id="ed55c-157">2 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-157">2 hours</span></span> |
| <span data-ttu-id="ed55c-158">Users with leaked credentials</span><span class="sxs-lookup"><span data-stu-id="ed55c-158">Users with leaked credentials</span></span> |<span data-ttu-id="ed55c-159">2 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-159">2 hours</span></span> |<span data-ttu-id="ed55c-160">4 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-160">4 hours</span></span> |<span data-ttu-id="ed55c-161">8 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-161">8 hours</span></span> |
| <span data-ttu-id="ed55c-162">Impossible travel to atypical locations</span><span class="sxs-lookup"><span data-stu-id="ed55c-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="ed55c-163">2 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-163">2 hours</span></span> |<span data-ttu-id="ed55c-164">4 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-164">4 hours</span></span> |<span data-ttu-id="ed55c-165">8 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-165">8 hours</span></span>  |
| <span data-ttu-id="ed55c-166">Sign-ins from infected devices</span><span class="sxs-lookup"><span data-stu-id="ed55c-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="ed55c-167">2 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-167">2 hours</span></span> |<span data-ttu-id="ed55c-168">4 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-168">4 hours</span></span> |<span data-ttu-id="ed55c-169">8 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-169">8 hours</span></span>  |
| <span data-ttu-id="ed55c-170">Sign-ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="ed55c-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="ed55c-171">2 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-171">2 hours</span></span> |<span data-ttu-id="ed55c-172">4 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-172">4 hours</span></span> |<span data-ttu-id="ed55c-173">8 hours</span><span class="sxs-lookup"><span data-stu-id="ed55c-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="ed55c-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="ed55c-174">Next steps</span></span>

<span data-ttu-id="ed55c-175">If you want to know more about the activity reports in the Azure portal, see:</span><span class="sxs-lookup"><span data-stu-id="ed55c-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="ed55c-176">Sign-in activity reports in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="ed55c-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="ed55c-177">Audit activity reports in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="ed55c-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="ed55c-178">If you want to know more about the security reports in the Azure portal, see:</span><span class="sxs-lookup"><span data-stu-id="ed55c-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="ed55c-179">Users at risk security report in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="ed55c-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="ed55c-180">Risky sign-ins report in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="ed55c-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="ed55c-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="ed55c-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>