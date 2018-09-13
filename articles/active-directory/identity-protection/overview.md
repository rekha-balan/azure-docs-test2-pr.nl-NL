---
title: Azure Active Directory Identity Protection | Microsoft Docs
description: Learn how Azure AD Identity Protection enables you to limit the ability of an attacker to exploit a compromised identity or device and to secure an identity or a device that was previously suspected or known to be compromised.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.component: conditional-access
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 791abd52ff4c016fe873288008e9d9b6adec6480
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866864"
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="4899e-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4899e-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="4899e-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span><span class="sxs-lookup"><span data-stu-id="4899e-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="4899e-106">Detect potential vulnerabilities affecting your organization’s identities</span><span class="sxs-lookup"><span data-stu-id="4899e-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="4899e-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span><span class="sxs-lookup"><span data-stu-id="4899e-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="4899e-108">Investigate suspicious incidents and take appropriate action to resolve them</span><span class="sxs-lookup"><span data-stu-id="4899e-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="4899e-109">Getting started</span><span class="sxs-lookup"><span data-stu-id="4899e-109">Getting started</span></span>

<span data-ttu-id="4899e-110">Microsoft has secured cloud-based identities for more than a decade.</span><span class="sxs-lookup"><span data-stu-id="4899e-110">Microsoft has secured cloud-based identities for more than a decade.</span></span> <span data-ttu-id="4899e-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span><span class="sxs-lookup"><span data-stu-id="4899e-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="4899e-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span><span class="sxs-lookup"><span data-stu-id="4899e-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="4899e-113">Over the years, attackers have become increasingly effective in leveraging third-party breaches and using sophisticated phishing attacks.</span><span class="sxs-lookup"><span data-stu-id="4899e-113">Over the years, attackers have become increasingly effective in leveraging third-party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="4899e-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span><span class="sxs-lookup"><span data-stu-id="4899e-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="4899e-115">As a consequence of this, you need to:</span><span class="sxs-lookup"><span data-stu-id="4899e-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="4899e-116">Protect all identities regardless of their privilege level</span><span class="sxs-lookup"><span data-stu-id="4899e-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="4899e-117">Proactively prevent compromised identities from being abused</span><span class="sxs-lookup"><span data-stu-id="4899e-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="4899e-118">Discovering compromised identities is no easy task.</span><span class="sxs-lookup"><span data-stu-id="4899e-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="4899e-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span><span class="sxs-lookup"><span data-stu-id="4899e-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="4899e-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span><span class="sxs-lookup"><span data-stu-id="4899e-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="4899e-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span><span class="sxs-lookup"><span data-stu-id="4899e-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="4899e-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span><span class="sxs-lookup"><span data-stu-id="4899e-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="4899e-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span><span class="sxs-lookup"><span data-stu-id="4899e-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="4899e-124">Identity Protection capabilities</span><span class="sxs-lookup"><span data-stu-id="4899e-124">Identity Protection capabilities</span></span>

<span data-ttu-id="4899e-125">**Detecting vulnerabilities and risky accounts:**</span><span class="sxs-lookup"><span data-stu-id="4899e-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="4899e-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="4899e-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="4899e-127">Calculating sign-in risk levels</span><span class="sxs-lookup"><span data-stu-id="4899e-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="4899e-128">Calculating user risk levels</span><span class="sxs-lookup"><span data-stu-id="4899e-128">Calculating user risk levels</span></span>


<span data-ttu-id="4899e-129">**Investigating risk events:**</span><span class="sxs-lookup"><span data-stu-id="4899e-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="4899e-130">Sending notifications for risk events</span><span class="sxs-lookup"><span data-stu-id="4899e-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="4899e-131">Investigating risk events using relevant and contextual information</span><span class="sxs-lookup"><span data-stu-id="4899e-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="4899e-132">Providing basic workflows to track investigations</span><span class="sxs-lookup"><span data-stu-id="4899e-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="4899e-133">Providing easy access to remediation actions such as password reset</span><span class="sxs-lookup"><span data-stu-id="4899e-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="4899e-134">**Risk-based conditional access policies:**</span><span class="sxs-lookup"><span data-stu-id="4899e-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="4899e-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges</span><span class="sxs-lookup"><span data-stu-id="4899e-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges</span></span>
* <span data-ttu-id="4899e-136">Policy to block or secure risky user accounts</span><span class="sxs-lookup"><span data-stu-id="4899e-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="4899e-137">Policy to require users to register for multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="4899e-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="4899e-138">Identity Protection roles</span><span class="sxs-lookup"><span data-stu-id="4899e-138">Identity Protection roles</span></span>

<span data-ttu-id="4899e-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span><span class="sxs-lookup"><span data-stu-id="4899e-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="4899e-140">Azure AD Identity Protection supports 3 directory roles:</span><span class="sxs-lookup"><span data-stu-id="4899e-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="4899e-141">Role</span><span class="sxs-lookup"><span data-stu-id="4899e-141">Role</span></span>                         | <span data-ttu-id="4899e-142">Can do</span><span class="sxs-lookup"><span data-stu-id="4899e-142">Can do</span></span>                          | <span data-ttu-id="4899e-143">Cannot do</span><span class="sxs-lookup"><span data-stu-id="4899e-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="4899e-144">Global administrator</span><span class="sxs-lookup"><span data-stu-id="4899e-144">Global administrator</span></span>         | <span data-ttu-id="4899e-145">Full access to Identity Protection, Onboard Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4899e-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="4899e-146">Security administrator</span><span class="sxs-lookup"><span data-stu-id="4899e-146">Security administrator</span></span>       | <span data-ttu-id="4899e-147">Full access to Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4899e-147">Full access to Identity Protection</span></span> | <span data-ttu-id="4899e-148">Onboard Identity Protection,  reset passwords for a user</span><span class="sxs-lookup"><span data-stu-id="4899e-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="4899e-149">Security reader</span><span class="sxs-lookup"><span data-stu-id="4899e-149">Security reader</span></span>              | <span data-ttu-id="4899e-150">Read-only access to Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4899e-150">Read-only access to Identity Protection</span></span> | <span data-ttu-id="4899e-151">Onboard Identity Protection, remediate users, configure policies,  reset passwords</span><span class="sxs-lookup"><span data-stu-id="4899e-151">Onboard Identity Protection, remediate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="4899e-152">For more details, see [Assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="4899e-152">For more details, see [Assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md)</span></span>



## <a name="detection"></a><span data-ttu-id="4899e-153">Detection</span><span class="sxs-lookup"><span data-stu-id="4899e-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="4899e-154">Vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="4899e-154">Vulnerabilities</span></span>

<span data-ttu-id="4899e-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span><span class="sxs-lookup"><span data-stu-id="4899e-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="4899e-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="4899e-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="4899e-157">Risk events</span><span class="sxs-lookup"><span data-stu-id="4899e-157">Risk events</span></span>

<span data-ttu-id="4899e-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span><span class="sxs-lookup"><span data-stu-id="4899e-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="4899e-159">The system creates a record for each detected suspicious action.</span><span class="sxs-lookup"><span data-stu-id="4899e-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="4899e-160">These records are also known as risk events.</span><span class="sxs-lookup"><span data-stu-id="4899e-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="4899e-161">For more details, see [Azure Active Directory risk events](../active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="4899e-161">For more details, see [Azure Active Directory risk events](../active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="4899e-162">Investigation</span><span class="sxs-lookup"><span data-stu-id="4899e-162">Investigation</span></span>
<span data-ttu-id="4899e-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span><span class="sxs-lookup"><span data-stu-id="4899e-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="4899e-164">![Remediation](./media/overview/1000.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="4899e-164">![Remediation](./media/overview/1000.png "Remediation")</span></span>

<span data-ttu-id="4899e-165">The dashboard gives you access to:</span><span class="sxs-lookup"><span data-stu-id="4899e-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="4899e-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span><span class="sxs-lookup"><span data-stu-id="4899e-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="4899e-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span><span class="sxs-lookup"><span data-stu-id="4899e-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="4899e-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span><span class="sxs-lookup"><span data-stu-id="4899e-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="4899e-169">You can tie your investigation activities to the [notifications](notifications.md) Azure Active Directory Protection sends per email.</span><span class="sxs-lookup"><span data-stu-id="4899e-169">You can tie your investigation activities to the [notifications](notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="4899e-170">The following sections provide you with more details and the steps that are related to an investigation.</span><span class="sxs-lookup"><span data-stu-id="4899e-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="4899e-171">Risky sign-ins</span><span class="sxs-lookup"><span data-stu-id="4899e-171">Risky sign-ins</span></span>

<span data-ttu-id="4899e-172">Azure Active Directory detects [risk event types](../reports-monitoring/concept-risk-events.md#risk-event-types) in real-time and offline.</span><span class="sxs-lookup"><span data-stu-id="4899e-172">Azure Active Directory detects [risk event types](../reports-monitoring/concept-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="4899e-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span><span class="sxs-lookup"><span data-stu-id="4899e-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="4899e-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="4899e-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="4899e-175">Sign-in risk level</span><span class="sxs-lookup"><span data-stu-id="4899e-175">Sign-in risk level</span></span>

<span data-ttu-id="4899e-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="4899e-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="4899e-177">Mitigating sign-in risk events</span><span class="sxs-lookup"><span data-stu-id="4899e-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="4899e-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span><span class="sxs-lookup"><span data-stu-id="4899e-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="4899e-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span><span class="sxs-lookup"><span data-stu-id="4899e-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="4899e-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policies.</span><span class="sxs-lookup"><span data-stu-id="4899e-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policies.</span></span> <span data-ttu-id="4899e-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="4899e-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="4899e-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span><span class="sxs-lookup"><span data-stu-id="4899e-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="4899e-183">Sign-in risk security policy</span><span class="sxs-lookup"><span data-stu-id="4899e-183">Sign-in risk security policy</span></span>
<span data-ttu-id="4899e-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span><span class="sxs-lookup"><span data-stu-id="4899e-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="4899e-185">![Sign-in risk policy](./media/overview/1014.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-185">![Sign-in risk policy](./media/overview/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="4899e-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span><span class="sxs-lookup"><span data-stu-id="4899e-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="4899e-187">Set the users and groups the policy applies to:</span><span class="sxs-lookup"><span data-stu-id="4899e-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="4899e-188">![Sign-in risk policy](./media/overview/1015.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-188">![Sign-in risk policy](./media/overview/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="4899e-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span><span class="sxs-lookup"><span data-stu-id="4899e-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="4899e-190">![Sign-in risk policy](./media/overview/1016.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-190">![Sign-in risk policy](./media/overview/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="4899e-191">Set the controls to be enforced when the policy triggers:</span><span class="sxs-lookup"><span data-stu-id="4899e-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="4899e-192">![Sign-in risk policy](./media/overview/1017.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-192">![Sign-in risk policy](./media/overview/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="4899e-193">Switch the state of your policy:</span><span class="sxs-lookup"><span data-stu-id="4899e-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="4899e-194">![MFA Registration](./media/overview/403.png "MFA Registration")</span><span class="sxs-lookup"><span data-stu-id="4899e-194">![MFA Registration](./media/overview/403.png "MFA Registration")</span></span>
* <span data-ttu-id="4899e-195">Review and evaluate the impact of a change before activating it:</span><span class="sxs-lookup"><span data-stu-id="4899e-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="4899e-196">![Sign-in risk policy](./media/overview/1018.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-196">![Sign-in risk policy](./media/overview/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="4899e-197">What you need to know</span><span class="sxs-lookup"><span data-stu-id="4899e-197">What you need to know</span></span>
<span data-ttu-id="4899e-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span><span class="sxs-lookup"><span data-stu-id="4899e-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="4899e-199">![Sign-in risk policy](./media/overview/1017.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-199">![Sign-in risk policy](./media/overview/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="4899e-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="4899e-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="4899e-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span><span class="sxs-lookup"><span data-stu-id="4899e-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="4899e-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span><span class="sxs-lookup"><span data-stu-id="4899e-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="4899e-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span><span class="sxs-lookup"><span data-stu-id="4899e-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="4899e-204">Require the affected users to login in a non-risky session to perform a MFA registration</span><span class="sxs-lookup"><span data-stu-id="4899e-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="4899e-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span><span class="sxs-lookup"><span data-stu-id="4899e-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="4899e-206">Best practices</span><span class="sxs-lookup"><span data-stu-id="4899e-206">Best practices</span></span>
<span data-ttu-id="4899e-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span><span class="sxs-lookup"><span data-stu-id="4899e-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="4899e-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span><span class="sxs-lookup"><span data-stu-id="4899e-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="4899e-209">When setting the policy,</span><span class="sxs-lookup"><span data-stu-id="4899e-209">When setting the policy,</span></span>

* <span data-ttu-id="4899e-210">Exclude users who do not/cannot have multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="4899e-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="4899e-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span><span class="sxs-lookup"><span data-stu-id="4899e-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="4899e-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span><span class="sxs-lookup"><span data-stu-id="4899e-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="4899e-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span><span class="sxs-lookup"><span data-stu-id="4899e-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="4899e-214">Use a **Low**  threshold if your organization requires greater security.</span><span class="sxs-lookup"><span data-stu-id="4899e-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="4899e-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span><span class="sxs-lookup"><span data-stu-id="4899e-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="4899e-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span><span class="sxs-lookup"><span data-stu-id="4899e-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="4899e-217">The sign-in risk policy is:</span><span class="sxs-lookup"><span data-stu-id="4899e-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="4899e-218">Applied to all browser traffic and sign-ins using modern authentication.</span><span class="sxs-lookup"><span data-stu-id="4899e-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="4899e-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span><span class="sxs-lookup"><span data-stu-id="4899e-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="4899e-220">The **Risk Events** page in the Identity Protection console lists all events:</span><span class="sxs-lookup"><span data-stu-id="4899e-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="4899e-221">This policy was applied to</span><span class="sxs-lookup"><span data-stu-id="4899e-221">This policy was applied to</span></span>
* <span data-ttu-id="4899e-222">You can review the activity and determine whether the action was appropriate or not</span><span class="sxs-lookup"><span data-stu-id="4899e-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="4899e-223">For an overview of the related user experience, see:</span><span class="sxs-lookup"><span data-stu-id="4899e-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="4899e-224">Risky sign-in recovery</span><span class="sxs-lookup"><span data-stu-id="4899e-224">Risky sign-in recovery</span></span>](flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="4899e-225">Risky sign-in blocked</span><span class="sxs-lookup"><span data-stu-id="4899e-225">Risky sign-in blocked</span></span>](flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="4899e-226">Sign-in experiences with Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4899e-226">Sign-in experiences with Azure AD Identity Protection</span></span>](flows.md)  

<span data-ttu-id="4899e-227">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="4899e-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="4899e-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span><span class="sxs-lookup"><span data-stu-id="4899e-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="4899e-229">![User risk policy](./media/overview/1014.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-229">![User risk policy](./media/overview/1014.png "User risk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="4899e-230">Users flagged for risk</span><span class="sxs-lookup"><span data-stu-id="4899e-230">Users flagged for risk</span></span>

<span data-ttu-id="4899e-231">All active [risk events](../reports-monitoring/concept-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span><span class="sxs-lookup"><span data-stu-id="4899e-231">All active [risk events](../reports-monitoring/concept-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="4899e-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="4899e-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Users flagged for risk](./media/overview/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="4899e-234">User risk level</span><span class="sxs-lookup"><span data-stu-id="4899e-234">User risk level</span></span>

<span data-ttu-id="4899e-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span><span class="sxs-lookup"><span data-stu-id="4899e-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="4899e-236">It is calculated based on the user risk events that are associated with a user's identity.</span><span class="sxs-lookup"><span data-stu-id="4899e-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="4899e-237">The status of a risk event is either **Active** or **Closed**.</span><span class="sxs-lookup"><span data-stu-id="4899e-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="4899e-238">Only risk events that are **Active** contribute to the user risk level calculation.</span><span class="sxs-lookup"><span data-stu-id="4899e-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="4899e-239">The user risk level is calculated using the following inputs:</span><span class="sxs-lookup"><span data-stu-id="4899e-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="4899e-240">Active risk events impacting the user</span><span class="sxs-lookup"><span data-stu-id="4899e-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="4899e-241">Risk level of these events</span><span class="sxs-lookup"><span data-stu-id="4899e-241">Risk level of these events</span></span>
* <span data-ttu-id="4899e-242">Whether any remediation actions have been taken</span><span class="sxs-lookup"><span data-stu-id="4899e-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="4899e-243">![User risks](./media/overview/1031.png "User risks")</span><span class="sxs-lookup"><span data-stu-id="4899e-243">![User risks](./media/overview/1031.png "User risks")</span></span>

<span data-ttu-id="4899e-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span><span class="sxs-lookup"><span data-stu-id="4899e-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="4899e-245">Closing risk events manually</span><span class="sxs-lookup"><span data-stu-id="4899e-245">Closing risk events manually</span></span>

<span data-ttu-id="4899e-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span><span class="sxs-lookup"><span data-stu-id="4899e-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="4899e-247">However, this might not always be possible.</span><span class="sxs-lookup"><span data-stu-id="4899e-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="4899e-248">This is, for example, the case, when:</span><span class="sxs-lookup"><span data-stu-id="4899e-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="4899e-249">A user with Active risk events has been deleted</span><span class="sxs-lookup"><span data-stu-id="4899e-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="4899e-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span><span class="sxs-lookup"><span data-stu-id="4899e-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="4899e-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span><span class="sxs-lookup"><span data-stu-id="4899e-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="4899e-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span><span class="sxs-lookup"><span data-stu-id="4899e-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="4899e-253">![Actions](./media/overview/34.png "Actions")</span><span class="sxs-lookup"><span data-stu-id="4899e-253">![Actions](./media/overview/34.png "Actions")</span></span>

* <span data-ttu-id="4899e-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span><span class="sxs-lookup"><span data-stu-id="4899e-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="4899e-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span><span class="sxs-lookup"><span data-stu-id="4899e-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="4899e-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span><span class="sxs-lookup"><span data-stu-id="4899e-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="4899e-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span><span class="sxs-lookup"><span data-stu-id="4899e-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="4899e-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span><span class="sxs-lookup"><span data-stu-id="4899e-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="4899e-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span><span class="sxs-lookup"><span data-stu-id="4899e-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="4899e-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span><span class="sxs-lookup"><span data-stu-id="4899e-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="4899e-261">Ignored events do not contribute to user risk.</span><span class="sxs-lookup"><span data-stu-id="4899e-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="4899e-262">This option should only be used under unusual circumstances.</span><span class="sxs-lookup"><span data-stu-id="4899e-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="4899e-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span><span class="sxs-lookup"><span data-stu-id="4899e-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="4899e-264">Reactivated risk events contribute to the user risk level calculation.</span><span class="sxs-lookup"><span data-stu-id="4899e-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="4899e-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span><span class="sxs-lookup"><span data-stu-id="4899e-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="4899e-266">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="4899e-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="4899e-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span><span class="sxs-lookup"><span data-stu-id="4899e-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="4899e-268">![Manual password reset](./media/overview/1002.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="4899e-268">![Manual password reset](./media/overview/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="4899e-269">In the **Risk events** list, click a risk.</span><span class="sxs-lookup"><span data-stu-id="4899e-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="4899e-270">![Manual password reset](./media/overview/1003.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="4899e-270">![Manual password reset](./media/overview/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="4899e-271">On the risk blade, right-click a user.</span><span class="sxs-lookup"><span data-stu-id="4899e-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="4899e-272">![Manual password reset](./media/overview/1004.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="4899e-272">![Manual password reset](./media/overview/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="4899e-273">Closing all risk events for a user manually</span><span class="sxs-lookup"><span data-stu-id="4899e-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="4899e-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span><span class="sxs-lookup"><span data-stu-id="4899e-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="4899e-275">![Actions](./media/overview/2222.png "Actions")</span><span class="sxs-lookup"><span data-stu-id="4899e-275">![Actions](./media/overview/2222.png "Actions")</span></span>

<span data-ttu-id="4899e-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span><span class="sxs-lookup"><span data-stu-id="4899e-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="4899e-277">Remediating user risk events</span><span class="sxs-lookup"><span data-stu-id="4899e-277">Remediating user risk events</span></span>

<span data-ttu-id="4899e-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span><span class="sxs-lookup"><span data-stu-id="4899e-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="4899e-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span><span class="sxs-lookup"><span data-stu-id="4899e-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="4899e-280">To remediate user risk events, you can:</span><span class="sxs-lookup"><span data-stu-id="4899e-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="4899e-281">Perform a secure password reset to remediate user risk events manually</span><span class="sxs-lookup"><span data-stu-id="4899e-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="4899e-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span><span class="sxs-lookup"><span data-stu-id="4899e-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="4899e-283">Re-image the infected device</span><span class="sxs-lookup"><span data-stu-id="4899e-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="4899e-284">Manual secure password reset</span><span class="sxs-lookup"><span data-stu-id="4899e-284">Manual secure password reset</span></span>
<span data-ttu-id="4899e-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span><span class="sxs-lookup"><span data-stu-id="4899e-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="4899e-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span><span class="sxs-lookup"><span data-stu-id="4899e-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="4899e-287">The related dialog provides two different methods to reset a password:</span><span class="sxs-lookup"><span data-stu-id="4899e-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="4899e-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="4899e-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="4899e-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span><span class="sxs-lookup"><span data-stu-id="4899e-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="4899e-290">This option isn't available if the user account is not already registered multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="4899e-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="4899e-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span><span class="sxs-lookup"><span data-stu-id="4899e-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="4899e-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span><span class="sxs-lookup"><span data-stu-id="4899e-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="4899e-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span><span class="sxs-lookup"><span data-stu-id="4899e-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="4899e-294">![Policy](./media/overview/1005.png "Policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-294">![Policy](./media/overview/1005.png "Policy")</span></span>

<span data-ttu-id="4899e-295">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="4899e-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="4899e-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span><span class="sxs-lookup"><span data-stu-id="4899e-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="4899e-297">![Manual password reset](./media/overview/1006.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="4899e-297">![Manual password reset](./media/overview/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="4899e-298">From the list of users, select a user with at least one risk events.</span><span class="sxs-lookup"><span data-stu-id="4899e-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="4899e-299">![Manual password reset](./media/overview/1007.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="4899e-299">![Manual password reset](./media/overview/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="4899e-300">On the user blade, click **Reset password**.</span><span class="sxs-lookup"><span data-stu-id="4899e-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="4899e-301">![Manual password reset](./media/overview/1008.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="4899e-301">![Manual password reset](./media/overview/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="4899e-302">User risk security policy</span><span class="sxs-lookup"><span data-stu-id="4899e-302">User risk security policy</span></span>
<span data-ttu-id="4899e-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span><span class="sxs-lookup"><span data-stu-id="4899e-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="4899e-304">![User risk policy](./media/overview/1009.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-304">![User risk policy](./media/overview/1009.png "User risk policy")</span></span>

<span data-ttu-id="4899e-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span><span class="sxs-lookup"><span data-stu-id="4899e-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="4899e-306">Set the users and groups the policy applies to:</span><span class="sxs-lookup"><span data-stu-id="4899e-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="4899e-307">![User risk policy](./media/overview/1010.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-307">![User risk policy](./media/overview/1010.png "User risk policy")</span></span>
* <span data-ttu-id="4899e-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span><span class="sxs-lookup"><span data-stu-id="4899e-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="4899e-309">![User risk policy](./media/overview/1011.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-309">![User risk policy](./media/overview/1011.png "User risk policy")</span></span>
* <span data-ttu-id="4899e-310">Set the controls to be enforced when the policy triggers:</span><span class="sxs-lookup"><span data-stu-id="4899e-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="4899e-311">![User risk policy](./media/overview/1012.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-311">![User risk policy](./media/overview/1012.png "User risk policy")</span></span>
* <span data-ttu-id="4899e-312">Switch the state of your policy:</span><span class="sxs-lookup"><span data-stu-id="4899e-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="4899e-313">![User risk policy](./media/overview/403.png "MFA Registration")</span><span class="sxs-lookup"><span data-stu-id="4899e-313">![User risk policy](./media/overview/403.png "MFA Registration")</span></span>
* <span data-ttu-id="4899e-314">Review and evaluate the impact of a change before activating it:</span><span class="sxs-lookup"><span data-stu-id="4899e-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="4899e-315">![User risk policy](./media/overview/1013.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-315">![User risk policy](./media/overview/1013.png "User risk policy")</span></span>

<span data-ttu-id="4899e-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span><span class="sxs-lookup"><span data-stu-id="4899e-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="4899e-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span><span class="sxs-lookup"><span data-stu-id="4899e-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="4899e-318">When setting the policy,</span><span class="sxs-lookup"><span data-stu-id="4899e-318">When setting the policy,</span></span>

* <span data-ttu-id="4899e-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span><span class="sxs-lookup"><span data-stu-id="4899e-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="4899e-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span><span class="sxs-lookup"><span data-stu-id="4899e-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="4899e-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span><span class="sxs-lookup"><span data-stu-id="4899e-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="4899e-322">Use a **Low** threshold if your organization requires greater security.</span><span class="sxs-lookup"><span data-stu-id="4899e-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="4899e-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span><span class="sxs-lookup"><span data-stu-id="4899e-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="4899e-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span><span class="sxs-lookup"><span data-stu-id="4899e-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="4899e-325">For an overview of the related user experience, see:</span><span class="sxs-lookup"><span data-stu-id="4899e-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="4899e-326">[Compromised account recovery flow](flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="4899e-326">[Compromised account recovery flow](flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="4899e-327">[Compromised account blocked flow](flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="4899e-327">[Compromised account blocked flow](flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="4899e-328">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="4899e-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="4899e-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span><span class="sxs-lookup"><span data-stu-id="4899e-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="4899e-330">![User risk policy](./media/overview/1009.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-330">![User risk policy](./media/overview/1009.png "User risk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="4899e-331">Mitigating user risk events</span><span class="sxs-lookup"><span data-stu-id="4899e-331">Mitigating user risk events</span></span>
<span data-ttu-id="4899e-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span><span class="sxs-lookup"><span data-stu-id="4899e-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="4899e-333">Blocking a sign-in:</span><span class="sxs-lookup"><span data-stu-id="4899e-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="4899e-334">Prevents the generation of new user risk events for the affected user</span><span class="sxs-lookup"><span data-stu-id="4899e-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="4899e-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span><span class="sxs-lookup"><span data-stu-id="4899e-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="4899e-336">Multi-factor authentication registration policy</span><span class="sxs-lookup"><span data-stu-id="4899e-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="4899e-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span><span class="sxs-lookup"><span data-stu-id="4899e-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="4899e-338">It provides a second layer of security to user sign-ins and transactions.</span><span class="sxs-lookup"><span data-stu-id="4899e-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="4899e-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span><span class="sxs-lookup"><span data-stu-id="4899e-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="4899e-340">Delivers strong authentication with a range of easy verification options</span><span class="sxs-lookup"><span data-stu-id="4899e-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="4899e-341">Plays a key role in preparing your organization to protect and recover from account compromises</span><span class="sxs-lookup"><span data-stu-id="4899e-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="4899e-342">![User risk policy](./media/overview/1019.png "User risk policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-342">![User risk policy](./media/overview/1019.png "User risk policy")</span></span>

<span data-ttu-id="4899e-343">For more details, see [What is Azure Multi-Factor Authentication?](../authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4899e-343">For more details, see [What is Azure Multi-Factor Authentication?](../authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="4899e-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span><span class="sxs-lookup"><span data-stu-id="4899e-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="4899e-345">Set the users and groups the policy applies to:</span><span class="sxs-lookup"><span data-stu-id="4899e-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="4899e-346">![MFA policy](./media/overview/1020.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-346">![MFA policy](./media/overview/1020.png "MFA policy")</span></span>
* <span data-ttu-id="4899e-347">Set the controls to be enforced when the policy triggers::</span><span class="sxs-lookup"><span data-stu-id="4899e-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="4899e-348">![MFA policy](./media/overview/1021.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-348">![MFA policy](./media/overview/1021.png "MFA policy")</span></span>
* <span data-ttu-id="4899e-349">Switch the state of your policy:</span><span class="sxs-lookup"><span data-stu-id="4899e-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="4899e-350">![MFA policy](./media/overview/403.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-350">![MFA policy](./media/overview/403.png "MFA policy")</span></span>
* <span data-ttu-id="4899e-351">View the current registration status:</span><span class="sxs-lookup"><span data-stu-id="4899e-351">View the current registration status:</span></span>

    <span data-ttu-id="4899e-352">![MFA policy](./media/overview/1022.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-352">![MFA policy](./media/overview/1022.png "MFA policy")</span></span>

<span data-ttu-id="4899e-353">For an overview of the related user experience, see:</span><span class="sxs-lookup"><span data-stu-id="4899e-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="4899e-354">[Multi-factor authentication registration flow](flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="4899e-354">[Multi-factor authentication registration flow](flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="4899e-355">[Sign-in experiences with Azure AD Identity Protection](flows.md).</span><span class="sxs-lookup"><span data-stu-id="4899e-355">[Sign-in experiences with Azure AD Identity Protection](flows.md).</span></span>  

<span data-ttu-id="4899e-356">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="4899e-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="4899e-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span><span class="sxs-lookup"><span data-stu-id="4899e-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="4899e-358">![MFA policy](./media/overview/1019.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="4899e-358">![MFA policy](./media/overview/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="4899e-359">Next steps</span><span class="sxs-lookup"><span data-stu-id="4899e-359">Next steps</span></span>
* [<span data-ttu-id="4899e-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span><span class="sxs-lookup"><span data-stu-id="4899e-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="4899e-361">Enabling Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4899e-361">Enabling Azure Active Directory Identity Protection</span></span>](enable.md)

* [<span data-ttu-id="4899e-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4899e-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](vulnerabilities.md)

* [<span data-ttu-id="4899e-363">Azure Active Directory risk events</span><span class="sxs-lookup"><span data-stu-id="4899e-363">Azure Active Directory risk events</span></span>](../active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="4899e-364">Azure Active Directory Identity Protection notifications</span><span class="sxs-lookup"><span data-stu-id="4899e-364">Azure Active Directory Identity Protection notifications</span></span>](notifications.md)

* [<span data-ttu-id="4899e-365">Azure Active Directory Identity Protection playbook</span><span class="sxs-lookup"><span data-stu-id="4899e-365">Azure Active Directory Identity Protection playbook</span></span>](playbook.md)

* [<span data-ttu-id="4899e-366">Azure Active Directory Identity Protection glossary</span><span class="sxs-lookup"><span data-stu-id="4899e-366">Azure Active Directory Identity Protection glossary</span></span>](glossary.md)

* [<span data-ttu-id="4899e-367">Sign-in experiences with Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4899e-367">Sign-in experiences with Azure AD Identity Protection</span></span>](flows.md)

* [<span data-ttu-id="4899e-368">Azure Active Directory Identity Protection - How to unblock users</span><span class="sxs-lookup"><span data-stu-id="4899e-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](howto-unblock-user.md)

* [<span data-ttu-id="4899e-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="4899e-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](graph-get-started.md)
