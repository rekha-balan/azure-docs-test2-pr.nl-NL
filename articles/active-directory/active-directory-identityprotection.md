---
title: Azure Active Directory Identity Protection | Microsoft Docs
description: Learn how Azure AD Identity Protection enables you to limit the ability of an attacker to exploit a compromised identity or device and to secure an identity or a device that was previously suspected or known to be compromised.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: 52b0b61e0784c39f148a1989d3d6740ee1d7c409
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564469"
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="ce743-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ce743-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="ce743-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span><span class="sxs-lookup"><span data-stu-id="ce743-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="ce743-106">Detect potential vulnerabilities affecting your organization’s identities</span><span class="sxs-lookup"><span data-stu-id="ce743-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="ce743-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span><span class="sxs-lookup"><span data-stu-id="ce743-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="ce743-108">Investigate suspicious incidents and take appropriate action to resolve them</span><span class="sxs-lookup"><span data-stu-id="ce743-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="ce743-109">Getting started</span><span class="sxs-lookup"><span data-stu-id="ce743-109">Getting started</span></span>

<span data-ttu-id="ce743-110">Microsoft secures cloud-based identities for more than a decade.</span><span class="sxs-lookup"><span data-stu-id="ce743-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="ce743-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span><span class="sxs-lookup"><span data-stu-id="ce743-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="ce743-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span><span class="sxs-lookup"><span data-stu-id="ce743-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="ce743-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span><span class="sxs-lookup"><span data-stu-id="ce743-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="ce743-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span><span class="sxs-lookup"><span data-stu-id="ce743-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="ce743-115">As a consequence of this, you need to:</span><span class="sxs-lookup"><span data-stu-id="ce743-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="ce743-116">Protect all identities regardless of their privilege level</span><span class="sxs-lookup"><span data-stu-id="ce743-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="ce743-117">Proactively prevent compromised identities from being abused</span><span class="sxs-lookup"><span data-stu-id="ce743-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="ce743-118">Discovering compromised identities is no easy task.</span><span class="sxs-lookup"><span data-stu-id="ce743-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="ce743-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span><span class="sxs-lookup"><span data-stu-id="ce743-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="ce743-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span><span class="sxs-lookup"><span data-stu-id="ce743-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="ce743-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span><span class="sxs-lookup"><span data-stu-id="ce743-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="ce743-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span><span class="sxs-lookup"><span data-stu-id="ce743-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="ce743-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span><span class="sxs-lookup"><span data-stu-id="ce743-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="ce743-124">Identity Protection capabilities</span><span class="sxs-lookup"><span data-stu-id="ce743-124">Identity Protection capabilities</span></span>

<span data-ttu-id="ce743-125">**Detecting vulnerabilities and risky accounts:**</span><span class="sxs-lookup"><span data-stu-id="ce743-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="ce743-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="ce743-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="ce743-127">Calculating sign-in risk levels</span><span class="sxs-lookup"><span data-stu-id="ce743-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="ce743-128">Calculating user risk levels</span><span class="sxs-lookup"><span data-stu-id="ce743-128">Calculating user risk levels</span></span>


<span data-ttu-id="ce743-129">**Investigating risk events:**</span><span class="sxs-lookup"><span data-stu-id="ce743-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="ce743-130">Sending notifications for risk events</span><span class="sxs-lookup"><span data-stu-id="ce743-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="ce743-131">Investigating risk events using relevant and contextual information</span><span class="sxs-lookup"><span data-stu-id="ce743-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="ce743-132">Providing basic workflows to track investigations</span><span class="sxs-lookup"><span data-stu-id="ce743-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="ce743-133">Providing easy access to remediation actions such as password reset</span><span class="sxs-lookup"><span data-stu-id="ce743-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="ce743-134">**Risk-based conditional access policies:**</span><span class="sxs-lookup"><span data-stu-id="ce743-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="ce743-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span><span class="sxs-lookup"><span data-stu-id="ce743-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="ce743-136">Policy to block or secure risky user accounts</span><span class="sxs-lookup"><span data-stu-id="ce743-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="ce743-137">Policy to require users to register for multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="ce743-137">Policy to require users to register for multi-factor authentication</span></span>

## <a name="detection"></a><span data-ttu-id="ce743-138">Detection</span><span class="sxs-lookup"><span data-stu-id="ce743-138">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="ce743-139">Vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="ce743-139">Vulnerabilities</span></span>

<span data-ttu-id="ce743-140">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span><span class="sxs-lookup"><span data-stu-id="ce743-140">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="ce743-141">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="ce743-141">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="ce743-142">Risk events</span><span class="sxs-lookup"><span data-stu-id="ce743-142">Risk events</span></span>

<span data-ttu-id="ce743-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span><span class="sxs-lookup"><span data-stu-id="ce743-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="ce743-144">The system creates a record for each detected suspicious action.</span><span class="sxs-lookup"><span data-stu-id="ce743-144">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="ce743-145">These records are also known as risk events.</span><span class="sxs-lookup"><span data-stu-id="ce743-145">These records are also known as risk events.</span></span>  
<span data-ttu-id="ce743-146">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="ce743-146">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="ce743-147">Investigation</span><span class="sxs-lookup"><span data-stu-id="ce743-147">Investigation</span></span>
<span data-ttu-id="ce743-148">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span><span class="sxs-lookup"><span data-stu-id="ce743-148">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="ce743-149">![Remediation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1000.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="ce743-149">![Remediation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="ce743-150">The dashboard gives you access to:</span><span class="sxs-lookup"><span data-stu-id="ce743-150">The dashboard gives you access to:</span></span>

* <span data-ttu-id="ce743-151">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span><span class="sxs-lookup"><span data-stu-id="ce743-151">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="ce743-152">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span><span class="sxs-lookup"><span data-stu-id="ce743-152">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="ce743-153">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span><span class="sxs-lookup"><span data-stu-id="ce743-153">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="ce743-154">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span><span class="sxs-lookup"><span data-stu-id="ce743-154">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="ce743-155">The following sections provide you with more details and the steps that are related to an investigation.</span><span class="sxs-lookup"><span data-stu-id="ce743-155">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="ce743-156">Risky sign-ins</span><span class="sxs-lookup"><span data-stu-id="ce743-156">Risky sign-ins</span></span>

<span data-ttu-id="ce743-157">Aure Active Directory detects some [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time.</span><span class="sxs-lookup"><span data-stu-id="ce743-157">Aure Active Directory detects some [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time.</span></span> <span data-ttu-id="ce743-158">All real-time risk events that have been detected during a sign-in of a user contribute to a logical concept called *risky sign-in*.</span><span class="sxs-lookup"><span data-stu-id="ce743-158">All real-time risk events that have been detected during a sign-in of a user contribute to a logical concept called *risky sign-in*.</span></span> <span data-ttu-id="ce743-159">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="ce743-159">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span> <span data-ttu-id="ce743-160">The lifecycle of a risky sign-in ends when a user signs out.</span><span class="sxs-lookup"><span data-stu-id="ce743-160">The lifecycle of a risky sign-in ends when a user signs out.</span></span>

### <a name="sign-in-risk-level"></a><span data-ttu-id="ce743-161">Sign-in risk level</span><span class="sxs-lookup"><span data-stu-id="ce743-161">Sign-in risk level</span></span>

<span data-ttu-id="ce743-162">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="ce743-162">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="ce743-163">Mitigating sign-in risk events</span><span class="sxs-lookup"><span data-stu-id="ce743-163">Mitigating sign-in risk events</span></span>

<span data-ttu-id="ce743-164">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span><span class="sxs-lookup"><span data-stu-id="ce743-164">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="ce743-165">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span><span class="sxs-lookup"><span data-stu-id="ce743-165">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="ce743-166">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span><span class="sxs-lookup"><span data-stu-id="ce743-166">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="ce743-167">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="ce743-167">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="ce743-168">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span><span class="sxs-lookup"><span data-stu-id="ce743-168">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="ce743-169">Sign-in risk security policy</span><span class="sxs-lookup"><span data-stu-id="ce743-169">Sign-in risk security policy</span></span>
<span data-ttu-id="ce743-170">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span><span class="sxs-lookup"><span data-stu-id="ce743-170">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="ce743-171">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-171">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="ce743-172">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span><span class="sxs-lookup"><span data-stu-id="ce743-172">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="ce743-173">Set the users and groups the policy applies to:</span><span class="sxs-lookup"><span data-stu-id="ce743-173">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="ce743-174">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-174">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="ce743-175">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span><span class="sxs-lookup"><span data-stu-id="ce743-175">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="ce743-176">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-176">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="ce743-177">Set the controls to be enforced when the policy triggers:</span><span class="sxs-lookup"><span data-stu-id="ce743-177">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="ce743-178">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-178">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="ce743-179">Switch the state of your policy:</span><span class="sxs-lookup"><span data-stu-id="ce743-179">Switch the state of your policy:</span></span>

    <span data-ttu-id="ce743-180">![MFA Registration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/403.png "MFA Registration")</span><span class="sxs-lookup"><span data-stu-id="ce743-180">![MFA Registration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="ce743-181">Review and evaluate the impact of a change before activating it:</span><span class="sxs-lookup"><span data-stu-id="ce743-181">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="ce743-182">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-182">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="ce743-183">What you need to know</span><span class="sxs-lookup"><span data-stu-id="ce743-183">What you need to know</span></span>
<span data-ttu-id="ce743-184">You can configure a sign-in risk security policy to require multi-factor authentication:</span><span class="sxs-lookup"><span data-stu-id="ce743-184">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="ce743-185">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-185">![Sign-in risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="ce743-186">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="ce743-186">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="ce743-187">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span><span class="sxs-lookup"><span data-stu-id="ce743-187">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="ce743-188">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span><span class="sxs-lookup"><span data-stu-id="ce743-188">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="ce743-189">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span><span class="sxs-lookup"><span data-stu-id="ce743-189">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="ce743-190">Require the affected users to login in a non-risky session to perform a MFA registration</span><span class="sxs-lookup"><span data-stu-id="ce743-190">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="ce743-191">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span><span class="sxs-lookup"><span data-stu-id="ce743-191">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="ce743-192">Best practices</span><span class="sxs-lookup"><span data-stu-id="ce743-192">Best practices</span></span>
<span data-ttu-id="ce743-193">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span><span class="sxs-lookup"><span data-stu-id="ce743-193">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="ce743-194">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span><span class="sxs-lookup"><span data-stu-id="ce743-194">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="ce743-195">When setting the policy,</span><span class="sxs-lookup"><span data-stu-id="ce743-195">When setting the policy,</span></span>

* <span data-ttu-id="ce743-196">Exclude users who do not/cannot have multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="ce743-196">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="ce743-197">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span><span class="sxs-lookup"><span data-stu-id="ce743-197">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="ce743-198">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span><span class="sxs-lookup"><span data-stu-id="ce743-198">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="ce743-199">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span><span class="sxs-lookup"><span data-stu-id="ce743-199">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="ce743-200">Use a **Low**  threshold if your organization requires greater security.</span><span class="sxs-lookup"><span data-stu-id="ce743-200">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="ce743-201">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span><span class="sxs-lookup"><span data-stu-id="ce743-201">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="ce743-202">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span><span class="sxs-lookup"><span data-stu-id="ce743-202">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="ce743-203">The sign-in risk policy is:</span><span class="sxs-lookup"><span data-stu-id="ce743-203">The sign-in risk policy is:</span></span>

* <span data-ttu-id="ce743-204">Applied to all browser traffic and sign-ins using modern authentication.</span><span class="sxs-lookup"><span data-stu-id="ce743-204">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="ce743-205">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span><span class="sxs-lookup"><span data-stu-id="ce743-205">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="ce743-206">The **Risk Events** page in the Identity Protection console lists all events:</span><span class="sxs-lookup"><span data-stu-id="ce743-206">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="ce743-207">This policy was applied to</span><span class="sxs-lookup"><span data-stu-id="ce743-207">This policy was applied to</span></span>
* <span data-ttu-id="ce743-208">You can review the activity and determine whether the action was appropriate or not</span><span class="sxs-lookup"><span data-stu-id="ce743-208">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="ce743-209">For an overview of the related user experience, see:</span><span class="sxs-lookup"><span data-stu-id="ce743-209">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="ce743-210">Risky sign-in recovery</span><span class="sxs-lookup"><span data-stu-id="ce743-210">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="ce743-211">Risky sign-in blocked</span><span class="sxs-lookup"><span data-stu-id="ce743-211">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="ce743-212">Sign-in experiences with Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ce743-212">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="ce743-213">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="ce743-213">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="ce743-214">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span><span class="sxs-lookup"><span data-stu-id="ce743-214">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="ce743-215">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1014.png "User ridk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-215">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="ce743-216">Users flagged for risk</span><span class="sxs-lookup"><span data-stu-id="ce743-216">Users flagged for risk</span></span>

<span data-ttu-id="ce743-217">All [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called *users flagged for risk*.</span><span class="sxs-lookup"><span data-stu-id="ce743-217">All [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called *users flagged for risk*.</span></span> <span data-ttu-id="ce743-218">A *user flag for risk* or *risky user* is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="ce743-218">A *user flag for risk* or *risky user* is an indicator for a user account that might have been compromised.</span></span>   

![Users flagged for risk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="ce743-220">User risk level</span><span class="sxs-lookup"><span data-stu-id="ce743-220">User risk level</span></span>

<span data-ttu-id="ce743-221">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span><span class="sxs-lookup"><span data-stu-id="ce743-221">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="ce743-222">It is calculated based on the user risk events that are associated with a user's identity.</span><span class="sxs-lookup"><span data-stu-id="ce743-222">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="ce743-223">The status of a risk event is either **Active** or **Closed**.</span><span class="sxs-lookup"><span data-stu-id="ce743-223">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="ce743-224">Only risk events that are **Active** contribute to the user risk level calculation.</span><span class="sxs-lookup"><span data-stu-id="ce743-224">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="ce743-225">The user risk level is calculated using the following inputs:</span><span class="sxs-lookup"><span data-stu-id="ce743-225">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="ce743-226">Active risk events impacting the user</span><span class="sxs-lookup"><span data-stu-id="ce743-226">Active risk events impacting the user</span></span>
* <span data-ttu-id="ce743-227">Risk level of these events</span><span class="sxs-lookup"><span data-stu-id="ce743-227">Risk level of these events</span></span>
* <span data-ttu-id="ce743-228">Whether any remediation actions have been taken</span><span class="sxs-lookup"><span data-stu-id="ce743-228">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="ce743-229">![User risks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1031.png "User risks")</span><span class="sxs-lookup"><span data-stu-id="ce743-229">![User risks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="ce743-230">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span><span class="sxs-lookup"><span data-stu-id="ce743-230">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="ce743-231">Closing risk events manually</span><span class="sxs-lookup"><span data-stu-id="ce743-231">Closing risk events manually</span></span>

<span data-ttu-id="ce743-232">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span><span class="sxs-lookup"><span data-stu-id="ce743-232">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="ce743-233">However, this might not always be possible.</span><span class="sxs-lookup"><span data-stu-id="ce743-233">However, this might not always be possible.</span></span>  
<span data-ttu-id="ce743-234">This is, for example, the case, when:</span><span class="sxs-lookup"><span data-stu-id="ce743-234">This is, for example, the case, when:</span></span>

* <span data-ttu-id="ce743-235">A user with Active risk events has been deleted</span><span class="sxs-lookup"><span data-stu-id="ce743-235">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="ce743-236">An investigation reveals that a reported risk event has been perform by the legitimate user</span><span class="sxs-lookup"><span data-stu-id="ce743-236">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="ce743-237">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span><span class="sxs-lookup"><span data-stu-id="ce743-237">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="ce743-238">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span><span class="sxs-lookup"><span data-stu-id="ce743-238">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="ce743-239">![Actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/34.png "Actions")</span><span class="sxs-lookup"><span data-stu-id="ce743-239">![Actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="ce743-240">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span><span class="sxs-lookup"><span data-stu-id="ce743-240">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="ce743-241">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span><span class="sxs-lookup"><span data-stu-id="ce743-241">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="ce743-242">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span><span class="sxs-lookup"><span data-stu-id="ce743-242">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="ce743-243">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span><span class="sxs-lookup"><span data-stu-id="ce743-243">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="ce743-244">This will help the machine learning algorithms to improve the classification of similar events in the future.</span><span class="sxs-lookup"><span data-stu-id="ce743-244">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="ce743-245">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span><span class="sxs-lookup"><span data-stu-id="ce743-245">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="ce743-246">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span><span class="sxs-lookup"><span data-stu-id="ce743-246">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="ce743-247">Ignored events do not contribute to user risk.</span><span class="sxs-lookup"><span data-stu-id="ce743-247">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="ce743-248">This option should only be used under unusual circumstances.</span><span class="sxs-lookup"><span data-stu-id="ce743-248">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="ce743-249">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span><span class="sxs-lookup"><span data-stu-id="ce743-249">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="ce743-250">Reactivated risk events contribute to the user risk level calculation.</span><span class="sxs-lookup"><span data-stu-id="ce743-250">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="ce743-251">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span><span class="sxs-lookup"><span data-stu-id="ce743-251">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="ce743-252">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="ce743-252">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="ce743-253">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span><span class="sxs-lookup"><span data-stu-id="ce743-253">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="ce743-254">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1002.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="ce743-254">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="ce743-255">In the **Risk events** list, click a risk.</span><span class="sxs-lookup"><span data-stu-id="ce743-255">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="ce743-256">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1003.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="ce743-256">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="ce743-257">On the risk blade, right-click a user.</span><span class="sxs-lookup"><span data-stu-id="ce743-257">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="ce743-258">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1004.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="ce743-258">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="ce743-259">Closing all risk events for a user manually</span><span class="sxs-lookup"><span data-stu-id="ce743-259">Closing all risk events for a user manually</span></span>
<span data-ttu-id="ce743-260">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span><span class="sxs-lookup"><span data-stu-id="ce743-260">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="ce743-261">![Actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/2222.png "Actions")</span><span class="sxs-lookup"><span data-stu-id="ce743-261">![Actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="ce743-262">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span><span class="sxs-lookup"><span data-stu-id="ce743-262">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="ce743-263">Remediating user risk events</span><span class="sxs-lookup"><span data-stu-id="ce743-263">Remediating user risk events</span></span>

<span data-ttu-id="ce743-264">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span><span class="sxs-lookup"><span data-stu-id="ce743-264">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="ce743-265">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span><span class="sxs-lookup"><span data-stu-id="ce743-265">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="ce743-266">To remediate user risk events, you can:</span><span class="sxs-lookup"><span data-stu-id="ce743-266">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="ce743-267">Perform a secure password reset to remediate user risk events manually</span><span class="sxs-lookup"><span data-stu-id="ce743-267">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="ce743-268">Configure a user risk security policy to mitigate or remediate user risk events automatically</span><span class="sxs-lookup"><span data-stu-id="ce743-268">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="ce743-269">Re-image the infected device</span><span class="sxs-lookup"><span data-stu-id="ce743-269">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="ce743-270">Manual secure password reset</span><span class="sxs-lookup"><span data-stu-id="ce743-270">Manual secure password reset</span></span>
<span data-ttu-id="ce743-271">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span><span class="sxs-lookup"><span data-stu-id="ce743-271">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="ce743-272">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span><span class="sxs-lookup"><span data-stu-id="ce743-272">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="ce743-273">The related dialog provides two different methods to reset a password:</span><span class="sxs-lookup"><span data-stu-id="ce743-273">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="ce743-274">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="ce743-274">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="ce743-275">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span><span class="sxs-lookup"><span data-stu-id="ce743-275">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="ce743-276">This option isn't available if the user account is not already registered multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="ce743-276">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="ce743-277">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span><span class="sxs-lookup"><span data-stu-id="ce743-277">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="ce743-278">Send the new temporary password to an alternate email address for the user or to the user's manager.</span><span class="sxs-lookup"><span data-stu-id="ce743-278">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="ce743-279">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span><span class="sxs-lookup"><span data-stu-id="ce743-279">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="ce743-280">![Policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1005.png "Policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-280">![Policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="ce743-281">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="ce743-281">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="ce743-282">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span><span class="sxs-lookup"><span data-stu-id="ce743-282">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="ce743-283">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1006.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="ce743-283">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="ce743-284">From the list of users, select a user with at least one risk events.</span><span class="sxs-lookup"><span data-stu-id="ce743-284">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="ce743-285">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1007.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="ce743-285">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="ce743-286">On the user blade, click **Reset password**.</span><span class="sxs-lookup"><span data-stu-id="ce743-286">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="ce743-287">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1008.png "Manual password reset")</span><span class="sxs-lookup"><span data-stu-id="ce743-287">![Manual password reset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="ce743-288">User risk security policy</span><span class="sxs-lookup"><span data-stu-id="ce743-288">User risk security policy</span></span>
<span data-ttu-id="ce743-289">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span><span class="sxs-lookup"><span data-stu-id="ce743-289">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="ce743-290">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1009.png "User ridk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-290">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="ce743-291">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span><span class="sxs-lookup"><span data-stu-id="ce743-291">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="ce743-292">Set the users and groups the policy applies to:</span><span class="sxs-lookup"><span data-stu-id="ce743-292">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="ce743-293">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1010.png "User ridk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-293">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="ce743-294">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span><span class="sxs-lookup"><span data-stu-id="ce743-294">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="ce743-295">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1011.png "User ridk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-295">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="ce743-296">Set the controls to be enforced when the policy triggers:</span><span class="sxs-lookup"><span data-stu-id="ce743-296">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="ce743-297">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1012.png "User ridk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-297">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="ce743-298">Switch the state of your policy:</span><span class="sxs-lookup"><span data-stu-id="ce743-298">Switch the state of your policy:</span></span>

    <span data-ttu-id="ce743-299">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/403.png "MFA Registration")</span><span class="sxs-lookup"><span data-stu-id="ce743-299">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="ce743-300">Review and evaluate the impact of a change before activating it:</span><span class="sxs-lookup"><span data-stu-id="ce743-300">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="ce743-301">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1013.png "User ridk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-301">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="ce743-302">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span><span class="sxs-lookup"><span data-stu-id="ce743-302">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="ce743-303">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span><span class="sxs-lookup"><span data-stu-id="ce743-303">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="ce743-304">When setting the policy,</span><span class="sxs-lookup"><span data-stu-id="ce743-304">When setting the policy,</span></span>

* <span data-ttu-id="ce743-305">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span><span class="sxs-lookup"><span data-stu-id="ce743-305">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="ce743-306">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span><span class="sxs-lookup"><span data-stu-id="ce743-306">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="ce743-307">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span><span class="sxs-lookup"><span data-stu-id="ce743-307">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="ce743-308">Use a **Low** threshold if your organization requires greater security.</span><span class="sxs-lookup"><span data-stu-id="ce743-308">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="ce743-309">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span><span class="sxs-lookup"><span data-stu-id="ce743-309">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="ce743-310">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span><span class="sxs-lookup"><span data-stu-id="ce743-310">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="ce743-311">For an overview of the related user experience, see:</span><span class="sxs-lookup"><span data-stu-id="ce743-311">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="ce743-312">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="ce743-312">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="ce743-313">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="ce743-313">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="ce743-314">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="ce743-314">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="ce743-315">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span><span class="sxs-lookup"><span data-stu-id="ce743-315">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="ce743-316">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1009.png "User ridk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-316">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="ce743-317">Mitigating user risk events</span><span class="sxs-lookup"><span data-stu-id="ce743-317">Mitigating user risk events</span></span>
<span data-ttu-id="ce743-318">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span><span class="sxs-lookup"><span data-stu-id="ce743-318">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="ce743-319">Blocking a sign-in:</span><span class="sxs-lookup"><span data-stu-id="ce743-319">Blocking a sign-in:</span></span>

* <span data-ttu-id="ce743-320">Prevents the generation of new user risk events for the affected user</span><span class="sxs-lookup"><span data-stu-id="ce743-320">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="ce743-321">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span><span class="sxs-lookup"><span data-stu-id="ce743-321">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="ce743-322">Multi-factor authentication registration policy</span><span class="sxs-lookup"><span data-stu-id="ce743-322">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="ce743-323">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span><span class="sxs-lookup"><span data-stu-id="ce743-323">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="ce743-324">It provides a second layer of security to user sign-ins and transactions.</span><span class="sxs-lookup"><span data-stu-id="ce743-324">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="ce743-325">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span><span class="sxs-lookup"><span data-stu-id="ce743-325">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="ce743-326">Delivers strong authentication with a range of easy verification options</span><span class="sxs-lookup"><span data-stu-id="ce743-326">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="ce743-327">Plays a key role in preparing your organization to protect and recover from account compromises</span><span class="sxs-lookup"><span data-stu-id="ce743-327">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="ce743-328">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1019.png "User ridk policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-328">![User ridk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="ce743-329">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ce743-329">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="ce743-330">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span><span class="sxs-lookup"><span data-stu-id="ce743-330">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="ce743-331">Set the users and groups the policy applies to:</span><span class="sxs-lookup"><span data-stu-id="ce743-331">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="ce743-332">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1020.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-332">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="ce743-333">Set the controls to be enforced when the policy triggers::</span><span class="sxs-lookup"><span data-stu-id="ce743-333">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="ce743-334">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1021.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-334">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="ce743-335">Switch the state of your policy:</span><span class="sxs-lookup"><span data-stu-id="ce743-335">Switch the state of your policy:</span></span>

    <span data-ttu-id="ce743-336">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/403.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-336">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="ce743-337">View the current registration status:</span><span class="sxs-lookup"><span data-stu-id="ce743-337">View the current registration status:</span></span>

    <span data-ttu-id="ce743-338">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1022.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-338">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="ce743-339">For an overview of the related user experience, see:</span><span class="sxs-lookup"><span data-stu-id="ce743-339">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="ce743-340">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="ce743-340">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="ce743-341">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="ce743-341">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="ce743-342">**To open the related configuration dialog**:</span><span class="sxs-lookup"><span data-stu-id="ce743-342">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="ce743-343">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span><span class="sxs-lookup"><span data-stu-id="ce743-343">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="ce743-344">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1019.png "MFA policy")</span><span class="sxs-lookup"><span data-stu-id="ce743-344">![MFA policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce743-345">Next steps</span><span class="sxs-lookup"><span data-stu-id="ce743-345">Next steps</span></span>
* [<span data-ttu-id="ce743-346">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span><span class="sxs-lookup"><span data-stu-id="ce743-346">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="ce743-347">Enabling Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ce743-347">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="ce743-348">Vulnerabilities detected by Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ce743-348">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="ce743-349">Azure Active Directory risk events</span><span class="sxs-lookup"><span data-stu-id="ce743-349">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="ce743-350">Azure Active Directory Identity Protection notifications</span><span class="sxs-lookup"><span data-stu-id="ce743-350">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="ce743-351">Azure Active Directory Identity Protection playbook</span><span class="sxs-lookup"><span data-stu-id="ce743-351">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="ce743-352">Azure Active Directory Identity Protection glossary</span><span class="sxs-lookup"><span data-stu-id="ce743-352">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="ce743-353">Sign-in experiences with Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ce743-353">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="ce743-354">Azure Active Directory Identity Protection - How to unblock users</span><span class="sxs-lookup"><span data-stu-id="ce743-354">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="ce743-355">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="ce743-355">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)

































