---
title: Sign-in experiences with Azure AD Identity Protection| Microsoft Docs
description: Provides an overview of the user experience when Identity Protection has mitigated or remediated a user or when multi-factor authentication is required by a policy.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.component: conditional-access
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c1c681e2c7ccd6b5fd3eaa3639853d99cb1e0b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965480"
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="33826-104">Sign-in experiences with Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="33826-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="33826-105">With Azure Active Directory Identity Protection, you can:</span><span class="sxs-lookup"><span data-stu-id="33826-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="33826-106">require users to register for multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="33826-106">require users to register for multi-factor authentication</span></span>
* <span data-ttu-id="33826-107">handle risky sign-ins and compromised users</span><span class="sxs-lookup"><span data-stu-id="33826-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="33826-108">The response of the system to these issues has an impact on a user's sign-in experience because directly signing-in by providing a user name and a password won't be possible anymore.</span><span class="sxs-lookup"><span data-stu-id="33826-108">The response of the system to these issues has an impact on a user's sign-in experience because directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="33826-109">Additional steps are required to get a user safely back into business.</span><span class="sxs-lookup"><span data-stu-id="33826-109">Additional steps are required to get a user safely back into business.</span></span>

<span data-ttu-id="33826-110">This article gives you an overview of a user's sign-in experience for all cases that can occur.</span><span class="sxs-lookup"><span data-stu-id="33826-110">This article gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="33826-111">**Multi-factor authentication**</span><span class="sxs-lookup"><span data-stu-id="33826-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="33826-112">Multi-factor authentication registration</span><span class="sxs-lookup"><span data-stu-id="33826-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="33826-113">**Sign-in at risk**</span><span class="sxs-lookup"><span data-stu-id="33826-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="33826-114">Risky sign-in recovery</span><span class="sxs-lookup"><span data-stu-id="33826-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="33826-115">Risky sign-in blocked</span><span class="sxs-lookup"><span data-stu-id="33826-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="33826-116">Multi-factor authentication registration during a risky sign-in</span><span class="sxs-lookup"><span data-stu-id="33826-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="33826-117">**User at risk**</span><span class="sxs-lookup"><span data-stu-id="33826-117">**User at risk**</span></span>

* <span data-ttu-id="33826-118">Compromised account recovery</span><span class="sxs-lookup"><span data-stu-id="33826-118">Compromised account recovery</span></span>
* <span data-ttu-id="33826-119">Compromised account blocked</span><span class="sxs-lookup"><span data-stu-id="33826-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="33826-120">Multi-factor authentication registration</span><span class="sxs-lookup"><span data-stu-id="33826-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="33826-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span><span class="sxs-lookup"><span data-stu-id="33826-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span></span> <span data-ttu-id="33826-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span><span class="sxs-lookup"><span data-stu-id="33826-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span></span> <span data-ttu-id="33826-123">No help desk or administrator involvement is needed to recover from account compromise.</span><span class="sxs-lookup"><span data-stu-id="33826-123">No help desk or administrator involvement is needed to recover from account compromise.</span></span> <span data-ttu-id="33826-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="33826-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="33826-125">Administrators can set a policy that requires users to set up their accounts for additional security verification.</span><span class="sxs-lookup"><span data-stu-id="33826-125">Administrators can set a policy that requires users to set up their accounts for additional security verification.</span></span> <span data-ttu-id="33826-126">This policy allows users to skip multi-factor authentication registration for up to 14 days.</span><span class="sxs-lookup"><span data-stu-id="33826-126">This policy allows users to skip multi-factor authentication registration for up to 14 days.</span></span> <span data-ttu-id="33826-127">The 14-day grace period is not configurable.</span><span class="sxs-lookup"><span data-stu-id="33826-127">The 14-day grace period is not configurable.</span></span>

<span data-ttu-id="33826-128">**The multi-factor authentication registration has three steps:**</span><span class="sxs-lookup"><span data-stu-id="33826-128">**The multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="33826-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="33826-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="33826-130">![Remediation](./media/flows/140.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-130">![Remediation](./media/flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="33826-131">To set up multi-factor authentication, you need to let the system know how you want to be contacted.</span><span class="sxs-lookup"><span data-stu-id="33826-131">To set up multi-factor authentication, you need to let the system know how you want to be contacted.</span></span>
   
    <span data-ttu-id="33826-132">![Remediation](./media/flows/141.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-132">![Remediation](./media/flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="33826-133">The system submits a challenge to you and you need to respond.</span><span class="sxs-lookup"><span data-stu-id="33826-133">The system submits a challenge to you and you need to respond.</span></span>
   
    <span data-ttu-id="33826-134">![Remediation](./media/flows/142.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-134">![Remediation](./media/flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="33826-135">Risky sign-in recovery</span><span class="sxs-lookup"><span data-stu-id="33826-135">Risky sign-in recovery</span></span>
<span data-ttu-id="33826-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign in.</span><span class="sxs-lookup"><span data-stu-id="33826-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign in.</span></span> 

<span data-ttu-id="33826-137">**The risky sign-in flow has two steps:**</span><span class="sxs-lookup"><span data-stu-id="33826-137">**The risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="33826-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span><span class="sxs-lookup"><span data-stu-id="33826-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="33826-139">![Remediation](./media/flows/120.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-139">![Remediation](./media/flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="33826-140">The user is required to prove their identity by solving a security challenge.</span><span class="sxs-lookup"><span data-stu-id="33826-140">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="33826-141">If the user is registered for multi-factor authentication they need to round trip a security code to their phone number.</span><span class="sxs-lookup"><span data-stu-id="33826-141">If the user is registered for multi-factor authentication they need to round trip a security code to their phone number.</span></span> <span data-ttu-id="33826-142">Since this is just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span><span class="sxs-lookup"><span data-stu-id="33826-142">Since this is just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span></span> 
   
    <span data-ttu-id="33826-143">![Remediation](./media/flows/121.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-143">![Remediation](./media/flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="33826-144">Risky sign-in blocked</span><span class="sxs-lookup"><span data-stu-id="33826-144">Risky sign-in blocked</span></span>
<span data-ttu-id="33826-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span><span class="sxs-lookup"><span data-stu-id="33826-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span></span> <span data-ttu-id="33826-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span><span class="sxs-lookup"><span data-stu-id="33826-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="33826-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span><span class="sxs-lookup"><span data-stu-id="33826-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="33826-148">![Remediation](./media/flows/200.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-148">![Remediation](./media/flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="33826-149">Compromised account recovery</span><span class="sxs-lookup"><span data-stu-id="33826-149">Compromised account recovery</span></span>
<span data-ttu-id="33826-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign in.</span><span class="sxs-lookup"><span data-stu-id="33826-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign in.</span></span> 

<span data-ttu-id="33826-151">**The user compromise recovery flow has three steps:**</span><span class="sxs-lookup"><span data-stu-id="33826-151">**The user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="33826-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span><span class="sxs-lookup"><span data-stu-id="33826-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="33826-153">![Remediation](./media/flows/101.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-153">![Remediation](./media/flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="33826-154">The user is required to prove their identity by solving a security challenge.</span><span class="sxs-lookup"><span data-stu-id="33826-154">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="33826-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span><span class="sxs-lookup"><span data-stu-id="33826-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="33826-156">They will need to round trip a security code to their phone number.</span><span class="sxs-lookup"><span data-stu-id="33826-156">They will need to round trip a security code to their phone number.</span></span> 
   
   <span data-ttu-id="33826-157">![Remediation](./media/flows/110.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-157">![Remediation](./media/flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="33826-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span><span class="sxs-lookup"><span data-stu-id="33826-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span></span> 
   <span data-ttu-id="33826-159">Screenshots of this experience are below.</span><span class="sxs-lookup"><span data-stu-id="33826-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="33826-160">![Remediation](./media/flows/111.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-160">![Remediation](./media/flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="33826-161">Compromised account blocked</span><span class="sxs-lookup"><span data-stu-id="33826-161">Compromised account blocked</span></span>
<span data-ttu-id="33826-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span><span class="sxs-lookup"><span data-stu-id="33826-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span></span> <span data-ttu-id="33826-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span><span class="sxs-lookup"><span data-stu-id="33826-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="33826-164">![Remediation](./media/flows/104.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-164">![Remediation](./media/flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="33826-165">Reset password</span><span class="sxs-lookup"><span data-stu-id="33826-165">Reset password</span></span>
<span data-ttu-id="33826-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span><span class="sxs-lookup"><span data-stu-id="33826-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="33826-167">The users will have to change their password during a next sign-in.</span><span class="sxs-lookup"><span data-stu-id="33826-167">The users will have to change their password during a next sign-in.</span></span>

<span data-ttu-id="33826-168">![Remediation](./media/flows/160.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="33826-168">![Remediation](./media/flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="33826-169">See also</span><span class="sxs-lookup"><span data-stu-id="33826-169">See also</span></span>
* [<span data-ttu-id="33826-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="33826-170">Azure Active Directory Identity Protection</span></span>](../active-directory-identityprotection.md) 

