---
title: Azure Active Directory Identity Protection Glossary | Microsoft Docs
description: Azure Active Directory Identity Protection Glossary
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy, glossary
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: markvi
ms.openlocfilehash: a3ee24eb2adc25651828a351fe815afc2fad8393
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553398"
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="611ec-104">Azure Active Directory Identity Protection Glossary</span><span class="sxs-lookup"><span data-stu-id="611ec-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="611ec-105">At risk (User)</span><span class="sxs-lookup"><span data-stu-id="611ec-105">At risk (User)</span></span>
<span data-ttu-id="611ec-106">A user with one or more active risk events.</span><span class="sxs-lookup"><span data-stu-id="611ec-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="611ec-107">Atypical sign-in location</span><span class="sxs-lookup"><span data-stu-id="611ec-107">Atypical sign-in location</span></span>
<span data-ttu-id="611ec-108">A sign-in from a geographic location that is not typical for the specific user, similar users, or the tenant.</span><span class="sxs-lookup"><span data-stu-id="611ec-108">A sign-in from a geographic location that is not typical for the specific user, similar users, or the tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="611ec-109">Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="611ec-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="611ec-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span><span class="sxs-lookup"><span data-stu-id="611ec-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="611ec-111">Conditional access</span><span class="sxs-lookup"><span data-stu-id="611ec-111">Conditional access</span></span>
<span data-ttu-id="611ec-112">A policy for securing access to resources.</span><span class="sxs-lookup"><span data-stu-id="611ec-112">A policy for securing access to resources.</span></span> <span data-ttu-id="611ec-113">Conditional access rules are stored in the Azure Active Directory and are evaluated by Azure AD before granting access to the resource.</span><span class="sxs-lookup"><span data-stu-id="611ec-113">Conditional access rules are stored in the Azure Active Directory and are evaluated by Azure AD before granting access to the resource.</span></span>  <span data-ttu-id="611ec-114">Example rules include restricting access based on user location, device health or user authentication method.</span><span class="sxs-lookup"><span data-stu-id="611ec-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="611ec-115">Credentials</span><span class="sxs-lookup"><span data-stu-id="611ec-115">Credentials</span></span>
<span data-ttu-id="611ec-116">Information that includes identification and proof of identification that is used to gain access to local and network resources.</span><span class="sxs-lookup"><span data-stu-id="611ec-116">Information that includes identification and proof of identification that is used to gain access to local and network resources.</span></span> <span data-ttu-id="611ec-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span><span class="sxs-lookup"><span data-stu-id="611ec-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="611ec-118">Event</span><span class="sxs-lookup"><span data-stu-id="611ec-118">Event</span></span>
<span data-ttu-id="611ec-119">A record of an activity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="611ec-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="611ec-120">False-positive (risk event)</span><span class="sxs-lookup"><span data-stu-id="611ec-120">False-positive (risk event)</span></span>
<span data-ttu-id="611ec-121">A risk event status set manually by an Identity Protection user, indicating that the risk event was investigated and was incorrectly flagged as a risk event.</span><span class="sxs-lookup"><span data-stu-id="611ec-121">A risk event status set manually by an Identity Protection user, indicating that the risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="611ec-122">Identity</span><span class="sxs-lookup"><span data-stu-id="611ec-122">Identity</span></span>
<span data-ttu-id="611ec-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span><span class="sxs-lookup"><span data-stu-id="611ec-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="611ec-124">Identity risk event</span><span class="sxs-lookup"><span data-stu-id="611ec-124">Identity risk event</span></span>
<span data-ttu-id="611ec-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span><span class="sxs-lookup"><span data-stu-id="611ec-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="611ec-126">Ignored (risk event)</span><span class="sxs-lookup"><span data-stu-id="611ec-126">Ignored (risk event)</span></span>
<span data-ttu-id="611ec-127">A risk event status set manually by an Identity Protection user, indicating that the risk event is closed without taking a remediation action.</span><span class="sxs-lookup"><span data-stu-id="611ec-127">A risk event status set manually by an Identity Protection user, indicating that the risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="611ec-128">Impossible travel from atypical locations</span><span class="sxs-lookup"><span data-stu-id="611ec-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="611ec-129">A risk event triggered when two sign-ins for the same user are detected, where at least one of them is from an atypical sign-in location, and where the time between the sign-ins is shorter than the minimum time it would take to physically travel between these locations.</span><span class="sxs-lookup"><span data-stu-id="611ec-129">A risk event triggered when two sign-ins for the same user are detected, where at least one of them is from an atypical sign-in location, and where the time between the sign-ins is shorter than the minimum time it would take to physically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="611ec-130">Investigation</span><span class="sxs-lookup"><span data-stu-id="611ec-130">Investigation</span></span>
<span data-ttu-id="611ec-131">The process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary, understand if and how the identity was compromised, and understand how the compromised identity was used.</span><span class="sxs-lookup"><span data-stu-id="611ec-131">The process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary, understand if and how the identity was compromised, and understand how the compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="611ec-132">Leaked credentials</span><span class="sxs-lookup"><span data-stu-id="611ec-132">Leaked credentials</span></span>
<span data-ttu-id="611ec-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in the Dark   web by our researchers.</span><span class="sxs-lookup"><span data-stu-id="611ec-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in the Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="611ec-134">Mitigation</span><span class="sxs-lookup"><span data-stu-id="611ec-134">Mitigation</span></span>
<span data-ttu-id="611ec-135">An action to limit or eliminate the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span><span class="sxs-lookup"><span data-stu-id="611ec-135">An action to limit or eliminate the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="611ec-136">A mitigation does not resolve previous risk events associated with the identity or device.</span><span class="sxs-lookup"><span data-stu-id="611ec-136">A mitigation does not resolve previous risk events associated with the identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="611ec-137">Multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="611ec-137">Multi-factor authentication</span></span>
<span data-ttu-id="611ec-138">An authentication method that requires two or more authentication methods, which may include something the user has, such a certificate; something the user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span><span class="sxs-lookup"><span data-stu-id="611ec-138">An authentication method that requires two or more authentication methods, which may include something the user has, such a certificate; something the user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="611ec-139">Offline detection</span><span class="sxs-lookup"><span data-stu-id="611ec-139">Offline detection</span></span>
<span data-ttu-id="611ec-140">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt after the fact, for an event that has already happened.</span><span class="sxs-lookup"><span data-stu-id="611ec-140">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt after the fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="611ec-141">Policy condition</span><span class="sxs-lookup"><span data-stu-id="611ec-141">Policy condition</span></span>
<span data-ttu-id="611ec-142">A part of a security policy which defines the entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in the policy or excluded from it.</span><span class="sxs-lookup"><span data-stu-id="611ec-142">A part of a security policy which defines the entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in the policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="611ec-143">Policy rule</span><span class="sxs-lookup"><span data-stu-id="611ec-143">Policy rule</span></span>
<span data-ttu-id="611ec-144">The part of a security policy which describes the circumstances that would trigger the policy, and the actions taken when the policy is triggered.</span><span class="sxs-lookup"><span data-stu-id="611ec-144">The part of a security policy which describes the circumstances that would trigger the policy, and the actions taken when the policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="611ec-145">Prevention</span><span class="sxs-lookup"><span data-stu-id="611ec-145">Prevention</span></span>
<span data-ttu-id="611ec-146">An action to prevent damage to the organization through abuse of an identity or device suspected or know to be compromised.</span><span class="sxs-lookup"><span data-stu-id="611ec-146">An action to prevent damage to the organization through abuse of an identity or device suspected or know to be compromised.</span></span> <span data-ttu-id="611ec-147">A prevention action does not secure the device or identity, and does not resolve previous risk events.</span><span class="sxs-lookup"><span data-stu-id="611ec-147">A prevention action does not secure the device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="611ec-148">Privileged (user)</span><span class="sxs-lookup"><span data-stu-id="611ec-148">Privileged (user)</span></span>
<span data-ttu-id="611ec-149">A user that at the time of a risk event, had permanent or temporary admin permissions to one or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span><span class="sxs-lookup"><span data-stu-id="611ec-149">A user that at the time of a risk event, had permanent or temporary admin permissions to one or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="611ec-150">Real-time</span><span class="sxs-lookup"><span data-stu-id="611ec-150">Real-time</span></span>
<span data-ttu-id="611ec-151">See Real-time detection.</span><span class="sxs-lookup"><span data-stu-id="611ec-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="611ec-152">Real-time detection</span><span class="sxs-lookup"><span data-stu-id="611ec-152">Real-time detection</span></span>
<span data-ttu-id="611ec-153">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt before the event is allowed to proceed.</span><span class="sxs-lookup"><span data-stu-id="611ec-153">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt before the event is allowed to proceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="611ec-154">Remediated (risk event)</span><span class="sxs-lookup"><span data-stu-id="611ec-154">Remediated (risk event)</span></span>
<span data-ttu-id="611ec-155">A risk event status set automatically by Identity Protection, indicating that the risk event was remediated using the standard remediation action for this type of risk event.</span><span class="sxs-lookup"><span data-stu-id="611ec-155">A risk event status set automatically by Identity Protection, indicating that the risk event was remediated using the standard remediation action for this type of risk event.</span></span> <span data-ttu-id="611ec-156">For example, when the user password is reset, many risk events that indicate that the previous password was compromised are automatically remediated.</span><span class="sxs-lookup"><span data-stu-id="611ec-156">For example, when the user password is reset, many risk events that indicate that the previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="611ec-157">Remediation</span><span class="sxs-lookup"><span data-stu-id="611ec-157">Remediation</span></span>
<span data-ttu-id="611ec-158">An action to secure an identity or a device that were previously suspected or known to be compromised.</span><span class="sxs-lookup"><span data-stu-id="611ec-158">An action to secure an identity or a device that were previously suspected or known to be compromised.</span></span> <span data-ttu-id="611ec-159">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span><span class="sxs-lookup"><span data-stu-id="611ec-159">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="611ec-160">Resolved (risk event)</span><span class="sxs-lookup"><span data-stu-id="611ec-160">Resolved (risk event)</span></span>
<span data-ttu-id="611ec-161">A risk event status set manually by an Identity Protection user, indicating that the user took an appropriate remediation action outside Identity Protection, and that the risk event should be considered closed.</span><span class="sxs-lookup"><span data-stu-id="611ec-161">A risk event status set manually by an Identity Protection user, indicating that the user took an appropriate remediation action outside Identity Protection, and that the risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="611ec-162">Risk event status</span><span class="sxs-lookup"><span data-stu-id="611ec-162">Risk event status</span></span>
<span data-ttu-id="611ec-163">A property of a risk event, indicating whether the event is active, and if closed, the reason for closing it.</span><span class="sxs-lookup"><span data-stu-id="611ec-163">A property of a risk event, indicating whether the event is active, and if closed, the reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="611ec-164">Risk event type</span><span class="sxs-lookup"><span data-stu-id="611ec-164">Risk event type</span></span>
<span data-ttu-id="611ec-165">A category for the risk event, indicating the type of anomaly that caused the event to be considered risky.</span><span class="sxs-lookup"><span data-stu-id="611ec-165">A category for the risk event, indicating the type of anomaly that caused the event to be considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="611ec-166">Risk level (risk event)</span><span class="sxs-lookup"><span data-stu-id="611ec-166">Risk level (risk event)</span></span>
<span data-ttu-id="611ec-167">An indication (High, Medium, or Low) of the severity of the risk event to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span><span class="sxs-lookup"><span data-stu-id="611ec-167">An indication (High, Medium, or Low) of the severity of the risk event to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="611ec-168">Risk level (sign-in)</span><span class="sxs-lookup"><span data-stu-id="611ec-168">Risk level (sign-in)</span></span>
<span data-ttu-id="611ec-169">An indication (High, Medium, or Low) of the likelihood that for a specific sign-in, someone else is attempting to use the user’s identity.</span><span class="sxs-lookup"><span data-stu-id="611ec-169">An indication (High, Medium, or Low) of the likelihood that for a specific sign-in, someone else is attempting to use the user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="611ec-170">Risk level (user compromise)</span><span class="sxs-lookup"><span data-stu-id="611ec-170">Risk level (user compromise)</span></span>
<span data-ttu-id="611ec-171">An indication (High, Medium, or Low) of the likelihood that an identity has been compromised.</span><span class="sxs-lookup"><span data-stu-id="611ec-171">An indication (High, Medium, or Low) of the likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="611ec-172">Risk level (vulnerability)</span><span class="sxs-lookup"><span data-stu-id="611ec-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="611ec-173">An indication (High, Medium, or Low) of the severity of the vulnerability to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span><span class="sxs-lookup"><span data-stu-id="611ec-173">An indication (High, Medium, or Low) of the severity of the vulnerability to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="611ec-174">Secure (identity)</span><span class="sxs-lookup"><span data-stu-id="611ec-174">Secure (identity)</span></span>
<span data-ttu-id="611ec-175">Take remediation action such as a password change or machine reimaging to restore a potentially compromised identity to an uncompromised state.</span><span class="sxs-lookup"><span data-stu-id="611ec-175">Take remediation action such as a password change or machine reimaging to restore a potentially compromised identity to an uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="611ec-176">Security policy</span><span class="sxs-lookup"><span data-stu-id="611ec-176">Security policy</span></span>
<span data-ttu-id="611ec-177">A collection of policy rules and condition.</span><span class="sxs-lookup"><span data-stu-id="611ec-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="611ec-178">A policy can be applied to entities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span><span class="sxs-lookup"><span data-stu-id="611ec-178">A policy can be applied to entities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="611ec-179">When a policy is enabled, it is evaluated whenever an entity included in the policy is issued a token for a resource.</span><span class="sxs-lookup"><span data-stu-id="611ec-179">When a policy is enabled, it is evaluated whenever an entity included in the policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="611ec-180">Sign in (v)</span><span class="sxs-lookup"><span data-stu-id="611ec-180">Sign in (v)</span></span>
<span data-ttu-id="611ec-181">To authenticate to an identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="611ec-181">To authenticate to an identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="611ec-182">Sign-in (n)</span><span class="sxs-lookup"><span data-stu-id="611ec-182">Sign-in (n)</span></span>
<span data-ttu-id="611ec-183">The process or action of authenticating an identity in Azure Active Directory, and the event that captures this operation.</span><span class="sxs-lookup"><span data-stu-id="611ec-183">The process or action of authenticating an identity in Azure Active Directory, and the event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="611ec-184">Sign-in from anonymous IP address</span><span class="sxs-lookup"><span data-stu-id="611ec-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="611ec-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span><span class="sxs-lookup"><span data-stu-id="611ec-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="611ec-186">Sign-in from infected device</span><span class="sxs-lookup"><span data-stu-id="611ec-186">Sign-in from infected device</span></span>
<span data-ttu-id="611ec-187">A risk event triggered when a sign-in originates from an IP address which is known to be used by one or more compromised devices, which are actively attempting to communicate with a bot server.</span><span class="sxs-lookup"><span data-stu-id="611ec-187">A risk event triggered when a sign-in originates from an IP address which is known to be used by one or more compromised devices, which are actively attempting to communicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="611ec-188">Sign-in from IP address with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="611ec-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="611ec-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span><span class="sxs-lookup"><span data-stu-id="611ec-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="611ec-190">Sign-in from unfamiliar location</span><span class="sxs-lookup"><span data-stu-id="611ec-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="611ec-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span><span class="sxs-lookup"><span data-stu-id="611ec-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="611ec-192">Sign-in risk</span><span class="sxs-lookup"><span data-stu-id="611ec-192">Sign-in risk</span></span>
<span data-ttu-id="611ec-193">See Risk level (sign-in)</span><span class="sxs-lookup"><span data-stu-id="611ec-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="611ec-194">Sign-in risk policy</span><span class="sxs-lookup"><span data-stu-id="611ec-194">Sign-in risk policy</span></span>
<span data-ttu-id="611ec-195">A conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span><span class="sxs-lookup"><span data-stu-id="611ec-195">A conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="611ec-196">User compromise risk</span><span class="sxs-lookup"><span data-stu-id="611ec-196">User compromise risk</span></span>
<span data-ttu-id="611ec-197">See Risk level (user compromise)</span><span class="sxs-lookup"><span data-stu-id="611ec-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="611ec-198">User risk</span><span class="sxs-lookup"><span data-stu-id="611ec-198">User risk</span></span>
<span data-ttu-id="611ec-199">See Risk level (user compromise).</span><span class="sxs-lookup"><span data-stu-id="611ec-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="611ec-200">User risk policy</span><span class="sxs-lookup"><span data-stu-id="611ec-200">User risk policy</span></span>
<span data-ttu-id="611ec-201">A conditional access policy that considers the sign-in and applies mitigations based on predefined conditions and rules.</span><span class="sxs-lookup"><span data-stu-id="611ec-201">A conditional access policy that considers the sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="611ec-202">Users flagged for risk</span><span class="sxs-lookup"><span data-stu-id="611ec-202">Users flagged for risk</span></span>
<span data-ttu-id="611ec-203">Users that have risk events which are either active or remediated</span><span class="sxs-lookup"><span data-stu-id="611ec-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="611ec-204">Vulnerability</span><span class="sxs-lookup"><span data-stu-id="611ec-204">Vulnerability</span></span>
<span data-ttu-id="611ec-205">A configuration or condition in Azure Active Directory which makes the directory susceptible to exploits or threats.</span><span class="sxs-lookup"><span data-stu-id="611ec-205">A configuration or condition in Azure Active Directory which makes the directory susceptible to exploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="611ec-206">See also</span><span class="sxs-lookup"><span data-stu-id="611ec-206">See also</span></span>
* [<span data-ttu-id="611ec-207">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="611ec-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

