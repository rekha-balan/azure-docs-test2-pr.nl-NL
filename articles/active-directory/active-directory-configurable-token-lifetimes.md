---
title: Configurable token lifetimes in Azure Active Directory | Microsoft Docs
description: Learn how to set lifetimes for tokens issued by Azure AD.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2016
ms.author: billmath
ms.openlocfilehash: 7d0c5f83d907af9109e27d69806d6106d4bc3214
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548835"
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a><span data-ttu-id="955dd-103">Configurable token lifetimes in Azure Active Directory (Public Preview)</span><span class="sxs-lookup"><span data-stu-id="955dd-103">Configurable token lifetimes in Azure Active Directory (Public Preview)</span></span>
<span data-ttu-id="955dd-104">You can specify the lifetime of a token issued by Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="955dd-104">You can specify the lifetime of a token issued by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="955dd-105">You can set token lifetimes for all apps in your organization, for a multi-tenant (multi-organization) application, or for a specific service principal in your organization.</span><span class="sxs-lookup"><span data-stu-id="955dd-105">You can set token lifetimes for all apps in your organization, for a multi-tenant (multi-organization) application, or for a specific service principal in your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="955dd-106">This capability currently is in Public Preview.</span><span class="sxs-lookup"><span data-stu-id="955dd-106">This capability currently is in Public Preview.</span></span> <span data-ttu-id="955dd-107">Be prepared to revert or remove any changes.</span><span class="sxs-lookup"><span data-stu-id="955dd-107">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="955dd-108">The feature is available in any Azure Active Directory subscription during Public Preview.</span><span class="sxs-lookup"><span data-stu-id="955dd-108">The feature is available in any Azure Active Directory subscription during Public Preview.</span></span> <span data-ttu-id="955dd-109">However, when the feature becomes generally available, some aspects of the feature might require an [Azure Active Directory Premium](active-directory-get-started-premium.md) subscription.</span><span class="sxs-lookup"><span data-stu-id="955dd-109">However, when the feature becomes generally available, some aspects of the feature might require an [Azure Active Directory Premium](active-directory-get-started-premium.md) subscription.</span></span>
>
>

<span data-ttu-id="955dd-110">In Azure AD, a policy object represents a set of rules that are enforced on individual applications or on all applications in an organization.</span><span class="sxs-lookup"><span data-stu-id="955dd-110">In Azure AD, a policy object represents a set of rules that are enforced on individual applications or on all applications in an organization.</span></span> <span data-ttu-id="955dd-111">Each policy type has a unique structure, with a set of properties that are applied to objects to which they are assigned.</span><span class="sxs-lookup"><span data-stu-id="955dd-111">Each policy type has a unique structure, with a set of properties that are applied to objects to which they are assigned.</span></span>

<span data-ttu-id="955dd-112">You can designate a policy as the default policy for your organization.</span><span class="sxs-lookup"><span data-stu-id="955dd-112">You can designate a policy as the default policy for your organization.</span></span> <span data-ttu-id="955dd-113">The policy is applied to any application in the organization, as long as it is not overridden by a policy with a higher priority.</span><span class="sxs-lookup"><span data-stu-id="955dd-113">The policy is applied to any application in the organization, as long as it is not overridden by a policy with a higher priority.</span></span> <span data-ttu-id="955dd-114">You also can assign a policy to specific applications.</span><span class="sxs-lookup"><span data-stu-id="955dd-114">You also can assign a policy to specific applications.</span></span> <span data-ttu-id="955dd-115">The order of priority varies by policy type.</span><span class="sxs-lookup"><span data-stu-id="955dd-115">The order of priority varies by policy type.</span></span>


## <a name="token-types"></a><span data-ttu-id="955dd-116">Token types</span><span class="sxs-lookup"><span data-stu-id="955dd-116">Token types</span></span>

<span data-ttu-id="955dd-117">You can set token lifetime policies for refresh tokens, access tokens, session tokens, and ID tokens.</span><span class="sxs-lookup"><span data-stu-id="955dd-117">You can set token lifetime policies for refresh tokens, access tokens, session tokens, and ID tokens.</span></span>

### <a name="access-tokens"></a><span data-ttu-id="955dd-118">Access tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-118">Access tokens</span></span>
<span data-ttu-id="955dd-119">Clients use access tokens to access a protected resource.</span><span class="sxs-lookup"><span data-stu-id="955dd-119">Clients use access tokens to access a protected resource.</span></span> <span data-ttu-id="955dd-120">An access token can be used only for a specific combination of user, client, and resource.</span><span class="sxs-lookup"><span data-stu-id="955dd-120">An access token can be used only for a specific combination of user, client, and resource.</span></span> <span data-ttu-id="955dd-121">Access tokens cannot be revoked and are valid until their expiry.</span><span class="sxs-lookup"><span data-stu-id="955dd-121">Access tokens cannot be revoked and are valid until their expiry.</span></span> <span data-ttu-id="955dd-122">A malicious actor that has obtained an access token can use it for extent of its lifetime.</span><span class="sxs-lookup"><span data-stu-id="955dd-122">A malicious actor that has obtained an access token can use it for extent of its lifetime.</span></span> <span data-ttu-id="955dd-123">Adjusting the lifetime of an access token is a trade-off between improving system performance and increasing the amount of time that the client retains access after the user’s account is disabled.</span><span class="sxs-lookup"><span data-stu-id="955dd-123">Adjusting the lifetime of an access token is a trade-off between improving system performance and increasing the amount of time that the client retains access after the user’s account is disabled.</span></span> <span data-ttu-id="955dd-124">Improved system performance is achieved by reducing the number of times a client needs to acquire a fresh access token.</span><span class="sxs-lookup"><span data-stu-id="955dd-124">Improved system performance is achieved by reducing the number of times a client needs to acquire a fresh access token.</span></span>

### <a name="refresh-tokens"></a><span data-ttu-id="955dd-125">Refresh tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-125">Refresh tokens</span></span>
<span data-ttu-id="955dd-126">When a client acquires an access token to access a protected resource, the client receives both a refresh token and an access token.</span><span class="sxs-lookup"><span data-stu-id="955dd-126">When a client acquires an access token to access a protected resource, the client receives both a refresh token and an access token.</span></span> <span data-ttu-id="955dd-127">The refresh token is used to obtain new access/refresh token pairs when the current access token expires.</span><span class="sxs-lookup"><span data-stu-id="955dd-127">The refresh token is used to obtain new access/refresh token pairs when the current access token expires.</span></span> <span data-ttu-id="955dd-128">A refresh token is bound to a combination of user and client.</span><span class="sxs-lookup"><span data-stu-id="955dd-128">A refresh token is bound to a combination of user and client.</span></span> <span data-ttu-id="955dd-129">A refresh token can be revoked, and the token's validity is checked every time the token is used.</span><span class="sxs-lookup"><span data-stu-id="955dd-129">A refresh token can be revoked, and the token's validity is checked every time the token is used.</span></span>

<span data-ttu-id="955dd-130">It's important to make a distinction between confidential clients and public clients.</span><span class="sxs-lookup"><span data-stu-id="955dd-130">It's important to make a distinction between confidential clients and public clients.</span></span> <span data-ttu-id="955dd-131">For more information about different types of clients, see [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="955dd-131">For more information about different types of clients, see [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).</span></span>

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a><span data-ttu-id="955dd-132">Token lifetimes with confidential client refresh tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-132">Token lifetimes with confidential client refresh tokens</span></span>
<span data-ttu-id="955dd-133">Confidential clients are applications that can securely store a client password (secret).</span><span class="sxs-lookup"><span data-stu-id="955dd-133">Confidential clients are applications that can securely store a client password (secret).</span></span> <span data-ttu-id="955dd-134">They can prove that requests are coming from the client application and not from a malicious actor.</span><span class="sxs-lookup"><span data-stu-id="955dd-134">They can prove that requests are coming from the client application and not from a malicious actor.</span></span> <span data-ttu-id="955dd-135">For example, a web app is a confidential client because it can store a client secret on the web server.</span><span class="sxs-lookup"><span data-stu-id="955dd-135">For example, a web app is a confidential client because it can store a client secret on the web server.</span></span> <span data-ttu-id="955dd-136">It is not exposed.</span><span class="sxs-lookup"><span data-stu-id="955dd-136">It is not exposed.</span></span> <span data-ttu-id="955dd-137">Because these flows are more secure, the default lifetimes of refresh tokens issued to these flows is `until-revoked`, cannot be changed by using policy, and will not be revoked on voluntary password resets.</span><span class="sxs-lookup"><span data-stu-id="955dd-137">Because these flows are more secure, the default lifetimes of refresh tokens issued to these flows is `until-revoked`, cannot be changed by using policy, and will not be revoked on voluntary password resets.</span></span>

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a><span data-ttu-id="955dd-138">Token lifetimes with public client refresh tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-138">Token lifetimes with public client refresh tokens</span></span>

<span data-ttu-id="955dd-139">Public clients cannot securely store a client password (secret).</span><span class="sxs-lookup"><span data-stu-id="955dd-139">Public clients cannot securely store a client password (secret).</span></span> <span data-ttu-id="955dd-140">For example, an iOS/Android app cannot obfuscate a secret from the resource owner, so it is considered a public client.</span><span class="sxs-lookup"><span data-stu-id="955dd-140">For example, an iOS/Android app cannot obfuscate a secret from the resource owner, so it is considered a public client.</span></span> <span data-ttu-id="955dd-141">You can set policies on resources to prevent refresh tokens from public clients older than a specified period from obtaining a new access/refresh token pair.</span><span class="sxs-lookup"><span data-stu-id="955dd-141">You can set policies on resources to prevent refresh tokens from public clients older than a specified period from obtaining a new access/refresh token pair.</span></span> <span data-ttu-id="955dd-142">(To do this, use the Refresh Token Max Inactive Time property.) You also can use policies to set a period beyond which the refresh tokens are no longer accepted.</span><span class="sxs-lookup"><span data-stu-id="955dd-142">(To do this, use the Refresh Token Max Inactive Time property.) You also can use policies to set a period beyond which the refresh tokens are no longer accepted.</span></span> <span data-ttu-id="955dd-143">(To do this, use the Refresh Token Max Age property.) You can adjust the lifetime of a refresh token to control when and how often the user is required to reenter credentials, instead of being silently reauthenticated, when using a public client application.</span><span class="sxs-lookup"><span data-stu-id="955dd-143">(To do this, use the Refresh Token Max Age property.) You can adjust the lifetime of a refresh token to control when and how often the user is required to reenter credentials, instead of being silently reauthenticated, when using a public client application.</span></span>

### <a name="id-tokens"></a><span data-ttu-id="955dd-144">ID tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-144">ID tokens</span></span>
<span data-ttu-id="955dd-145">ID tokens are passed to websites and native clients.</span><span class="sxs-lookup"><span data-stu-id="955dd-145">ID tokens are passed to websites and native clients.</span></span> <span data-ttu-id="955dd-146">ID tokens contain profile information about a user.</span><span class="sxs-lookup"><span data-stu-id="955dd-146">ID tokens contain profile information about a user.</span></span> <span data-ttu-id="955dd-147">An ID token is bound to a specific combination of user and client.</span><span class="sxs-lookup"><span data-stu-id="955dd-147">An ID token is bound to a specific combination of user and client.</span></span> <span data-ttu-id="955dd-148">ID tokens are considered valid until their expiry.</span><span class="sxs-lookup"><span data-stu-id="955dd-148">ID tokens are considered valid until their expiry.</span></span> <span data-ttu-id="955dd-149">Usually, a web application matches a user’s session lifetime in the application to the lifetime of the ID token issued for the user.</span><span class="sxs-lookup"><span data-stu-id="955dd-149">Usually, a web application matches a user’s session lifetime in the application to the lifetime of the ID token issued for the user.</span></span> <span data-ttu-id="955dd-150">You can adjust the lifetime of an ID token to control how often the web application expires the application session, and how often it requires the user to be reauthenticated with Azure AD (either silently or interactively).</span><span class="sxs-lookup"><span data-stu-id="955dd-150">You can adjust the lifetime of an ID token to control how often the web application expires the application session, and how often it requires the user to be reauthenticated with Azure AD (either silently or interactively).</span></span>

### <a name="single-sign-on-session-tokens"></a><span data-ttu-id="955dd-151">Single sign-on session tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-151">Single sign-on session tokens</span></span>
<span data-ttu-id="955dd-152">When a user authenticates with Azure AD and selects the **Keep me signed in** check box, a single sign-on session (SSO) is established with the user’s browser and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="955dd-152">When a user authenticates with Azure AD and selects the **Keep me signed in** check box, a single sign-on session (SSO) is established with the user’s browser and Azure AD.</span></span> <span data-ttu-id="955dd-153">The SSO token, in the form of a cookie, represents this session.</span><span class="sxs-lookup"><span data-stu-id="955dd-153">The SSO token, in the form of a cookie, represents this session.</span></span> <span data-ttu-id="955dd-154">Note that the SSO session token is not bound to a specific resource/client application.</span><span class="sxs-lookup"><span data-stu-id="955dd-154">Note that the SSO session token is not bound to a specific resource/client application.</span></span> <span data-ttu-id="955dd-155">SSO session tokens can be revoked, and their validity is checked every time they are used.</span><span class="sxs-lookup"><span data-stu-id="955dd-155">SSO session tokens can be revoked, and their validity is checked every time they are used.</span></span>

<span data-ttu-id="955dd-156">Azure AD uses two kinds of SSO session tokens: persistent and nonpersistent.</span><span class="sxs-lookup"><span data-stu-id="955dd-156">Azure AD uses two kinds of SSO session tokens: persistent and nonpersistent.</span></span> <span data-ttu-id="955dd-157">Persistent session tokens are stored as persistent cookies by the browser.</span><span class="sxs-lookup"><span data-stu-id="955dd-157">Persistent session tokens are stored as persistent cookies by the browser.</span></span> <span data-ttu-id="955dd-158">Nonpersistent session tokens are stored as session cookies.</span><span class="sxs-lookup"><span data-stu-id="955dd-158">Nonpersistent session tokens are stored as session cookies.</span></span> <span data-ttu-id="955dd-159">(Session cookies are destroyed when the browser is closed.)</span><span class="sxs-lookup"><span data-stu-id="955dd-159">(Session cookies are destroyed when the browser is closed.)</span></span>

<span data-ttu-id="955dd-160">Nonpersistent session tokens have a lifetime of 24 hours.</span><span class="sxs-lookup"><span data-stu-id="955dd-160">Nonpersistent session tokens have a lifetime of 24 hours.</span></span> <span data-ttu-id="955dd-161">Persistent tokens have a lifetime of 180 days.</span><span class="sxs-lookup"><span data-stu-id="955dd-161">Persistent tokens have a lifetime of 180 days.</span></span> <span data-ttu-id="955dd-162">Any time an SSO session token is used within its validity period, the validity period is extended another 24 hours or 180 days, depending on the token type.</span><span class="sxs-lookup"><span data-stu-id="955dd-162">Any time an SSO session token is used within its validity period, the validity period is extended another 24 hours or 180 days, depending on the token type.</span></span> <span data-ttu-id="955dd-163">If an SSO session token is not used within its validity period, it is considered expired and is no longer accepted.</span><span class="sxs-lookup"><span data-stu-id="955dd-163">If an SSO session token is not used within its validity period, it is considered expired and is no longer accepted.</span></span>

<span data-ttu-id="955dd-164">You can use a policy to set the time after the first session token was issued beyond which the session token is no longer accepted.</span><span class="sxs-lookup"><span data-stu-id="955dd-164">You can use a policy to set the time after the first session token was issued beyond which the session token is no longer accepted.</span></span> <span data-ttu-id="955dd-165">(To do this, use the Session Token Max Age property.) You can adjust the lifetime of a session token to control when and how often a user is required to reenter credentials, instead of being silently authenticated, when using a web application.</span><span class="sxs-lookup"><span data-stu-id="955dd-165">(To do this, use the Session Token Max Age property.) You can adjust the lifetime of a session token to control when and how often a user is required to reenter credentials, instead of being silently authenticated, when using a web application.</span></span>

### <a name="token-lifetime-policy-properties"></a><span data-ttu-id="955dd-166">Token lifetime policy properties</span><span class="sxs-lookup"><span data-stu-id="955dd-166">Token lifetime policy properties</span></span>
<span data-ttu-id="955dd-167">A token lifetime policy is a type of policy object that contains token lifetime rules.</span><span class="sxs-lookup"><span data-stu-id="955dd-167">A token lifetime policy is a type of policy object that contains token lifetime rules.</span></span> <span data-ttu-id="955dd-168">Use the properties of the policy to control specified token lifetimes.</span><span class="sxs-lookup"><span data-stu-id="955dd-168">Use the properties of the policy to control specified token lifetimes.</span></span> <span data-ttu-id="955dd-169">If no policy is set, the system enforces the default lifetime value.</span><span class="sxs-lookup"><span data-stu-id="955dd-169">If no policy is set, the system enforces the default lifetime value.</span></span>

### <a name="configurable-token-lifetime-properties"></a><span data-ttu-id="955dd-170">Configurable token lifetime properties</span><span class="sxs-lookup"><span data-stu-id="955dd-170">Configurable token lifetime properties</span></span>
| <span data-ttu-id="955dd-171">Property</span><span class="sxs-lookup"><span data-stu-id="955dd-171">Property</span></span> | <span data-ttu-id="955dd-172">Policy property string</span><span class="sxs-lookup"><span data-stu-id="955dd-172">Policy property string</span></span> | <span data-ttu-id="955dd-173">Affects</span><span class="sxs-lookup"><span data-stu-id="955dd-173">Affects</span></span> | <span data-ttu-id="955dd-174">Default</span><span class="sxs-lookup"><span data-stu-id="955dd-174">Default</span></span> | <span data-ttu-id="955dd-175">Minimum</span><span class="sxs-lookup"><span data-stu-id="955dd-175">Minimum</span></span> | <span data-ttu-id="955dd-176">Maximum</span><span class="sxs-lookup"><span data-stu-id="955dd-176">Maximum</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="955dd-177">Access Token Lifetime</span><span class="sxs-lookup"><span data-stu-id="955dd-177">Access Token Lifetime</span></span> |<span data-ttu-id="955dd-178">AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="955dd-178">AccessTokenLifetime</span></span> |<span data-ttu-id="955dd-179">Access tokens, ID tokens, SAML2 tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-179">Access tokens, ID tokens, SAML2 tokens</span></span> |<span data-ttu-id="955dd-180">1 hour</span><span class="sxs-lookup"><span data-stu-id="955dd-180">1 hour</span></span> |<span data-ttu-id="955dd-181">10 minutes</span><span class="sxs-lookup"><span data-stu-id="955dd-181">10 minutes</span></span> |<span data-ttu-id="955dd-182">1 day</span><span class="sxs-lookup"><span data-stu-id="955dd-182">1 day</span></span> |
| <span data-ttu-id="955dd-183">Refresh Token Max Inactive Time</span><span class="sxs-lookup"><span data-stu-id="955dd-183">Refresh Token Max Inactive Time</span></span> |<span data-ttu-id="955dd-184">MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="955dd-184">MaxInactiveTime</span></span> |<span data-ttu-id="955dd-185">Refresh tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-185">Refresh tokens</span></span> |<span data-ttu-id="955dd-186">14 days</span><span class="sxs-lookup"><span data-stu-id="955dd-186">14 days</span></span> |<span data-ttu-id="955dd-187">10 minutes</span><span class="sxs-lookup"><span data-stu-id="955dd-187">10 minutes</span></span> |<span data-ttu-id="955dd-188">90 days</span><span class="sxs-lookup"><span data-stu-id="955dd-188">90 days</span></span> |
| <span data-ttu-id="955dd-189">Single-Factor Refresh Token Max Age</span><span class="sxs-lookup"><span data-stu-id="955dd-189">Single-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="955dd-190">MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="955dd-190">MaxAgeSingleFactor</span></span> |<span data-ttu-id="955dd-191">Refresh tokens (for any users)</span><span class="sxs-lookup"><span data-stu-id="955dd-191">Refresh tokens (for any users)</span></span> |<span data-ttu-id="955dd-192">90 days</span><span class="sxs-lookup"><span data-stu-id="955dd-192">90 days</span></span> |<span data-ttu-id="955dd-193">10 minutes</span><span class="sxs-lookup"><span data-stu-id="955dd-193">10 minutes</span></span> |<span data-ttu-id="955dd-194">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="955dd-194">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="955dd-195">Multi-Factor Refresh Token Max Age</span><span class="sxs-lookup"><span data-stu-id="955dd-195">Multi-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="955dd-196">MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="955dd-196">MaxAgeMultiFactor</span></span> |<span data-ttu-id="955dd-197">Refresh tokens (for any users)</span><span class="sxs-lookup"><span data-stu-id="955dd-197">Refresh tokens (for any users)</span></span> |<span data-ttu-id="955dd-198">90 days</span><span class="sxs-lookup"><span data-stu-id="955dd-198">90 days</span></span> |<span data-ttu-id="955dd-199">10 minutes</span><span class="sxs-lookup"><span data-stu-id="955dd-199">10 minutes</span></span> |<span data-ttu-id="955dd-200">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="955dd-200">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="955dd-201">Single-Factor Session Token Max Age</span><span class="sxs-lookup"><span data-stu-id="955dd-201">Single-Factor Session Token Max Age</span></span> |<span data-ttu-id="955dd-202">MaxAgeSessionSingleFactor<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="955dd-202">MaxAgeSessionSingleFactor<sup>2</sup></span></span> |<span data-ttu-id="955dd-203">Session tokens (persistent and nonpersistent)</span><span class="sxs-lookup"><span data-stu-id="955dd-203">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="955dd-204">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="955dd-204">Until-revoked</span></span> |<span data-ttu-id="955dd-205">10 minutes</span><span class="sxs-lookup"><span data-stu-id="955dd-205">10 minutes</span></span> |<span data-ttu-id="955dd-206">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="955dd-206">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="955dd-207">Multi-Factor Session Token Max Age</span><span class="sxs-lookup"><span data-stu-id="955dd-207">Multi-Factor Session Token Max Age</span></span> |<span data-ttu-id="955dd-208">MaxAgeSessionMultiFactor<sup>3</sup></span><span class="sxs-lookup"><span data-stu-id="955dd-208">MaxAgeSessionMultiFactor<sup>3</sup></span></span> |<span data-ttu-id="955dd-209">Session tokens (persistent and nonpersistent)</span><span class="sxs-lookup"><span data-stu-id="955dd-209">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="955dd-210">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="955dd-210">Until-revoked</span></span> |<span data-ttu-id="955dd-211">10 minutes</span><span class="sxs-lookup"><span data-stu-id="955dd-211">10 minutes</span></span> |<span data-ttu-id="955dd-212">Until-revoked<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="955dd-212">Until-revoked<sup>1</sup></span></span> |

* <span data-ttu-id="955dd-213"><sup>1</sup>365 days is the maximum explicit length that can be set for these attributes.</span><span class="sxs-lookup"><span data-stu-id="955dd-213"><sup>1</sup>365 days is the maximum explicit length that can be set for these attributes.</span></span>
* <span data-ttu-id="955dd-214"><sup>2</sup>If  **MaxAgeSessionSingleFactor** is not set, this value takes the **MaxAgeSingleFactor** value.</span><span class="sxs-lookup"><span data-stu-id="955dd-214"><sup>2</sup>If  **MaxAgeSessionSingleFactor** is not set, this value takes the **MaxAgeSingleFactor** value.</span></span> <span data-ttu-id="955dd-215">If neither parameter is set, the property takes the default value (until-revoked).</span><span class="sxs-lookup"><span data-stu-id="955dd-215">If neither parameter is set, the property takes the default value (until-revoked).</span></span>
* <span data-ttu-id="955dd-216"><sup>3</sup>If  **MaxAgeSessionMultiFactor** is not set, this value takes the **MaxAgeMultiFactor** value.</span><span class="sxs-lookup"><span data-stu-id="955dd-216"><sup>3</sup>If  **MaxAgeSessionMultiFactor** is not set, this value takes the **MaxAgeMultiFactor** value.</span></span> <span data-ttu-id="955dd-217">If neither parameter is set, the property takes the default value (until-revoked).</span><span class="sxs-lookup"><span data-stu-id="955dd-217">If neither parameter is set, the property takes the default value (until-revoked).</span></span>

### <a name="exceptions"></a><span data-ttu-id="955dd-218">Exceptions</span><span class="sxs-lookup"><span data-stu-id="955dd-218">Exceptions</span></span>
| <span data-ttu-id="955dd-219">Property</span><span class="sxs-lookup"><span data-stu-id="955dd-219">Property</span></span> | <span data-ttu-id="955dd-220">Affects</span><span class="sxs-lookup"><span data-stu-id="955dd-220">Affects</span></span> | <span data-ttu-id="955dd-221">Default</span><span class="sxs-lookup"><span data-stu-id="955dd-221">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="955dd-222">Refresh Token Max Inactive Time (issued for federated users who have insufficient revocation information)</span><span class="sxs-lookup"><span data-stu-id="955dd-222">Refresh Token Max Inactive Time (issued for federated users who have insufficient revocation information)</span></span> |<span data-ttu-id="955dd-223">Refresh tokens (issued for federated users who have insufficient revocation information)</span><span class="sxs-lookup"><span data-stu-id="955dd-223">Refresh tokens (issued for federated users who have insufficient revocation information)</span></span> |<span data-ttu-id="955dd-224">12 hours</span><span class="sxs-lookup"><span data-stu-id="955dd-224">12 hours</span></span> |
| <span data-ttu-id="955dd-225">Refresh Token Max Inactive Time (issued for confidential clients)</span><span class="sxs-lookup"><span data-stu-id="955dd-225">Refresh Token Max Inactive Time (issued for confidential clients)</span></span> |<span data-ttu-id="955dd-226">Refresh tokens (issued for confidential clients)</span><span class="sxs-lookup"><span data-stu-id="955dd-226">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="955dd-227">90 days</span><span class="sxs-lookup"><span data-stu-id="955dd-227">90 days</span></span> |
| <span data-ttu-id="955dd-228">Refresh Token Max Age (issued for confidential clients)</span><span class="sxs-lookup"><span data-stu-id="955dd-228">Refresh Token Max Age (issued for confidential clients)</span></span> |<span data-ttu-id="955dd-229">Refresh tokens (issued for confidential clients)</span><span class="sxs-lookup"><span data-stu-id="955dd-229">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="955dd-230">Until-revoked</span><span class="sxs-lookup"><span data-stu-id="955dd-230">Until-revoked</span></span> |

### <a name="policy-evaluation-and-prioritization"></a><span data-ttu-id="955dd-231">Policy evaluation and prioritization</span><span class="sxs-lookup"><span data-stu-id="955dd-231">Policy evaluation and prioritization</span></span>
<span data-ttu-id="955dd-232">You can create and then assign a token lifetime policy to a specific application, to your organization, and to service principals.</span><span class="sxs-lookup"><span data-stu-id="955dd-232">You can create and then assign a token lifetime policy to a specific application, to your organization, and to service principals.</span></span> <span data-ttu-id="955dd-233">Multiple policies might apply to a specific application.</span><span class="sxs-lookup"><span data-stu-id="955dd-233">Multiple policies might apply to a specific application.</span></span> <span data-ttu-id="955dd-234">The token lifetime policy that takes effect follows these rules:</span><span class="sxs-lookup"><span data-stu-id="955dd-234">The token lifetime policy that takes effect follows these rules:</span></span>

* <span data-ttu-id="955dd-235">If a policy is explicitly assigned to the service principal, it is enforced.</span><span class="sxs-lookup"><span data-stu-id="955dd-235">If a policy is explicitly assigned to the service principal, it is enforced.</span></span>
* <span data-ttu-id="955dd-236">If no policy is explicitly assigned to the service principal, a policy explicitly assigned to the parent organization of the service principal is enforced.</span><span class="sxs-lookup"><span data-stu-id="955dd-236">If no policy is explicitly assigned to the service principal, a policy explicitly assigned to the parent organization of the service principal is enforced.</span></span>
* <span data-ttu-id="955dd-237">If no policy is explicitly assigned to the service principal or to the organization, the policy assigned to the application is enforced.</span><span class="sxs-lookup"><span data-stu-id="955dd-237">If no policy is explicitly assigned to the service principal or to the organization, the policy assigned to the application is enforced.</span></span>
* <span data-ttu-id="955dd-238">If no policy has been assigned to the service principal, the organization, or the application object, the default values is enforced.</span><span class="sxs-lookup"><span data-stu-id="955dd-238">If no policy has been assigned to the service principal, the organization, or the application object, the default values is enforced.</span></span> <span data-ttu-id="955dd-239">(See the table in [Configurable token lifetime properties](#configurable-token-lifetime-properties).)</span><span class="sxs-lookup"><span data-stu-id="955dd-239">(See the table in [Configurable token lifetime properties](#configurable-token-lifetime-properties).)</span></span>

<span data-ttu-id="955dd-240">For more information about the relationship between application objects and service principal objects, see [Application and service principal objects in Azure Active Directory](active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="955dd-240">For more information about the relationship between application objects and service principal objects, see [Application and service principal objects in Azure Active Directory](active-directory-application-objects.md).</span></span>

<span data-ttu-id="955dd-241">A token’s validity is evaluated at the time the token is used.</span><span class="sxs-lookup"><span data-stu-id="955dd-241">A token’s validity is evaluated at the time the token is used.</span></span> <span data-ttu-id="955dd-242">The policy with the highest priority on the application that is being accessed takes effect.</span><span class="sxs-lookup"><span data-stu-id="955dd-242">The policy with the highest priority on the application that is being accessed takes effect.</span></span>

> [!NOTE]
> <span data-ttu-id="955dd-243">Here's an example scenario.</span><span class="sxs-lookup"><span data-stu-id="955dd-243">Here's an example scenario.</span></span>
>
> <span data-ttu-id="955dd-244">A user wants to access two web applications: Web Application A and Web Application B.</span><span class="sxs-lookup"><span data-stu-id="955dd-244">A user wants to access two web applications: Web Application A and Web Application B.</span></span>
> 
> <span data-ttu-id="955dd-245">Factors:</span><span class="sxs-lookup"><span data-stu-id="955dd-245">Factors:</span></span>
> * <span data-ttu-id="955dd-246">Both web applications are in the same parent organization.</span><span class="sxs-lookup"><span data-stu-id="955dd-246">Both web applications are in the same parent organization.</span></span>
> * <span data-ttu-id="955dd-247">Token Lifetime Policy 1 with a Session Token Max Age of eight hours is set as the parent organization’s default.</span><span class="sxs-lookup"><span data-stu-id="955dd-247">Token Lifetime Policy 1 with a Session Token Max Age of eight hours is set as the parent organization’s default.</span></span>
> * <span data-ttu-id="955dd-248">Web Application A is a regular-use web application and isn’t linked to any policies.</span><span class="sxs-lookup"><span data-stu-id="955dd-248">Web Application A is a regular-use web application and isn’t linked to any policies.</span></span>
> * <span data-ttu-id="955dd-249">Web Application B is used for highly sensitive processes.</span><span class="sxs-lookup"><span data-stu-id="955dd-249">Web Application B is used for highly sensitive processes.</span></span> <span data-ttu-id="955dd-250">Its service principal is linked to Token Lifetime Policy 2, which has a Session Token Max Age of 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="955dd-250">Its service principal is linked to Token Lifetime Policy 2, which has a Session Token Max Age of 30 minutes.</span></span>
>
> <span data-ttu-id="955dd-251">At 12:00 PM, the user starts a new browser session and tries to access Web Application A. The user is redirected to Azure AD and is asked to sign in.</span><span class="sxs-lookup"><span data-stu-id="955dd-251">At 12:00 PM, the user starts a new browser session and tries to access Web Application A. The user is redirected to Azure AD and is asked to sign in.</span></span> <span data-ttu-id="955dd-252">This creates a cookie that has a session token in the browser.</span><span class="sxs-lookup"><span data-stu-id="955dd-252">This creates a cookie that has a session token in the browser.</span></span> <span data-ttu-id="955dd-253">The user is redirected back to Web Application A with an ID token that allows the user to access the application.</span><span class="sxs-lookup"><span data-stu-id="955dd-253">The user is redirected back to Web Application A with an ID token that allows the user to access the application.</span></span>
>
> <span data-ttu-id="955dd-254">At 12:15 PM, the user tries to access Web Application B. The browser redirects to Azure AD, which detects the session cookie.</span><span class="sxs-lookup"><span data-stu-id="955dd-254">At 12:15 PM, the user tries to access Web Application B. The browser redirects to Azure AD, which detects the session cookie.</span></span> <span data-ttu-id="955dd-255">Web Application B’s service principal is linked to Token Lifetime Policy 2, but it's also part of the parent organization, with default Token Lifetime Policy 1.</span><span class="sxs-lookup"><span data-stu-id="955dd-255">Web Application B’s service principal is linked to Token Lifetime Policy 2, but it's also part of the parent organization, with default Token Lifetime Policy 1.</span></span> <span data-ttu-id="955dd-256">Token Lifetime Policy 2 takes effect because policies linked to service principals have a higher priority than organization default policies.</span><span class="sxs-lookup"><span data-stu-id="955dd-256">Token Lifetime Policy 2 takes effect because policies linked to service principals have a higher priority than organization default policies.</span></span> <span data-ttu-id="955dd-257">The session token was originally issued within the last 30 minutes, so it is considered valid.</span><span class="sxs-lookup"><span data-stu-id="955dd-257">The session token was originally issued within the last 30 minutes, so it is considered valid.</span></span> <span data-ttu-id="955dd-258">The user is redirected back to Web Application B with an ID token that grants them access.</span><span class="sxs-lookup"><span data-stu-id="955dd-258">The user is redirected back to Web Application B with an ID token that grants them access.</span></span>
>
> <span data-ttu-id="955dd-259">At 1:00 PM, the user tries to access Web Application A. The user is redirected to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="955dd-259">At 1:00 PM, the user tries to access Web Application A. The user is redirected to Azure AD.</span></span> <span data-ttu-id="955dd-260">Web Application A is not linked to any policies, but because it is in an organization with default Token Lifetime Policy 1, that policy takes effect.</span><span class="sxs-lookup"><span data-stu-id="955dd-260">Web Application A is not linked to any policies, but because it is in an organization with default Token Lifetime Policy 1, that policy takes effect.</span></span> <span data-ttu-id="955dd-261">The session cookie that was originally issued within the last eight hours is detected.</span><span class="sxs-lookup"><span data-stu-id="955dd-261">The session cookie that was originally issued within the last eight hours is detected.</span></span> <span data-ttu-id="955dd-262">The user is silently redirected back to Web Application A with a new ID token.</span><span class="sxs-lookup"><span data-stu-id="955dd-262">The user is silently redirected back to Web Application A with a new ID token.</span></span> <span data-ttu-id="955dd-263">The user is not required to authenticate.</span><span class="sxs-lookup"><span data-stu-id="955dd-263">The user is not required to authenticate.</span></span>
>
> <span data-ttu-id="955dd-264">Immediately afterward, the user tries to access Web Application B. The user is redirected to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="955dd-264">Immediately afterward, the user tries to access Web Application B. The user is redirected to Azure AD.</span></span> <span data-ttu-id="955dd-265">As before, Token Lifetime Policy 2 takes effect.</span><span class="sxs-lookup"><span data-stu-id="955dd-265">As before, Token Lifetime Policy 2 takes effect.</span></span> <span data-ttu-id="955dd-266">Because the token was issued more than 30 minutes ago, the user is prompted to reenter their sign-in credentials.</span><span class="sxs-lookup"><span data-stu-id="955dd-266">Because the token was issued more than 30 minutes ago, the user is prompted to reenter their sign-in credentials.</span></span> <span data-ttu-id="955dd-267">A brand-new session token and ID token are issued.</span><span class="sxs-lookup"><span data-stu-id="955dd-267">A brand-new session token and ID token are issued.</span></span> <span data-ttu-id="955dd-268">The user can then access Web Application B.</span><span class="sxs-lookup"><span data-stu-id="955dd-268">The user can then access Web Application B.</span></span>
>
>

## <a name="configurable-policy-property-details"></a><span data-ttu-id="955dd-269">Configurable policy property details</span><span class="sxs-lookup"><span data-stu-id="955dd-269">Configurable policy property details</span></span>
### <a name="access-token-lifetime"></a><span data-ttu-id="955dd-270">Access Token Lifetime</span><span class="sxs-lookup"><span data-stu-id="955dd-270">Access Token Lifetime</span></span>
<span data-ttu-id="955dd-271">**String:** AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="955dd-271">**String:** AccessTokenLifetime</span></span>

<span data-ttu-id="955dd-272">**Affects:** Access tokens, ID tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-272">**Affects:** Access tokens, ID tokens</span></span>

<span data-ttu-id="955dd-273">**Summary:** This policy controls how long access and ID tokens for this resource are considered valid.</span><span class="sxs-lookup"><span data-stu-id="955dd-273">**Summary:** This policy controls how long access and ID tokens for this resource are considered valid.</span></span> <span data-ttu-id="955dd-274">Reducing the Access Token Lifetime property mitigates the risk of an access token or ID token being used by a malicious actor for an extended period of time.</span><span class="sxs-lookup"><span data-stu-id="955dd-274">Reducing the Access Token Lifetime property mitigates the risk of an access token or ID token being used by a malicious actor for an extended period of time.</span></span> <span data-ttu-id="955dd-275">(These tokens cannot be revoked.) The trade-off is that performance is adversely affected, because the tokens have to be replaced more often.</span><span class="sxs-lookup"><span data-stu-id="955dd-275">(These tokens cannot be revoked.) The trade-off is that performance is adversely affected, because the tokens have to be replaced more often.</span></span>

### <a name="refresh-token-max-inactive-time"></a><span data-ttu-id="955dd-276">Refresh Token Max Inactive Time</span><span class="sxs-lookup"><span data-stu-id="955dd-276">Refresh Token Max Inactive Time</span></span>
<span data-ttu-id="955dd-277">**String:** MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="955dd-277">**String:** MaxInactiveTime</span></span>

<span data-ttu-id="955dd-278">**Affects:** Refresh tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-278">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="955dd-279">**Summary:** This policy controls how old a refresh token can be before a client can no longer use it to retrieve a new access/refresh token pair when attempting to access this resource.</span><span class="sxs-lookup"><span data-stu-id="955dd-279">**Summary:** This policy controls how old a refresh token can be before a client can no longer use it to retrieve a new access/refresh token pair when attempting to access this resource.</span></span> <span data-ttu-id="955dd-280">Because a new refresh token usually is returned when a refresh token is used, this policy prevents access if the client tries to access any resource by using the current refresh token during the specified period of time.</span><span class="sxs-lookup"><span data-stu-id="955dd-280">Because a new refresh token usually is returned when a refresh token is used, this policy prevents access if the client tries to access any resource by using the current refresh token during the specified period of time.</span></span>

<span data-ttu-id="955dd-281">This policy forces users who have not been active on their client to reauthenticate to retrieve a new refresh token.</span><span class="sxs-lookup"><span data-stu-id="955dd-281">This policy forces users who have not been active on their client to reauthenticate to retrieve a new refresh token.</span></span>

<span data-ttu-id="955dd-282">The Refresh Token Max Inactive Time property must be set to a lower value than the Single-Factor Token Max Age and the Multi-Factor Refresh Token Max Age properties.</span><span class="sxs-lookup"><span data-stu-id="955dd-282">The Refresh Token Max Inactive Time property must be set to a lower value than the Single-Factor Token Max Age and the Multi-Factor Refresh Token Max Age properties.</span></span>

### <a name="single-factor-refresh-token-max-age"></a><span data-ttu-id="955dd-283">Single-Factor Refresh Token Max Age</span><span class="sxs-lookup"><span data-stu-id="955dd-283">Single-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="955dd-284">**String:** MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="955dd-284">**String:** MaxAgeSingleFactor</span></span>

<span data-ttu-id="955dd-285">**Affects:** Refresh tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-285">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="955dd-286">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using only a single factor.</span><span class="sxs-lookup"><span data-stu-id="955dd-286">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="955dd-287">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span><span class="sxs-lookup"><span data-stu-id="955dd-287">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span></span> <span data-ttu-id="955dd-288">(This is true as long as the current refresh token is not revoked, and it is not left unused for longer than the inactive time.) At that point, the user is forced to reauthenticate to receive a new refresh token.</span><span class="sxs-lookup"><span data-stu-id="955dd-288">(This is true as long as the current refresh token is not revoked, and it is not left unused for longer than the inactive time.) At that point, the user is forced to reauthenticate to receive a new refresh token.</span></span>

<span data-ttu-id="955dd-289">Reducing the max age forces users to authenticate more often.</span><span class="sxs-lookup"><span data-stu-id="955dd-289">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="955dd-290">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or lesser than the Multi-Factor Refresh Token Max Age property.</span><span class="sxs-lookup"><span data-stu-id="955dd-290">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or lesser than the Multi-Factor Refresh Token Max Age property.</span></span>

### <a name="multi-factor-refresh-token-max-age"></a><span data-ttu-id="955dd-291">Multi-Factor Refresh Token Max Age</span><span class="sxs-lookup"><span data-stu-id="955dd-291">Multi-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="955dd-292">**String:** MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="955dd-292">**String:** MaxAgeMultiFactor</span></span>

<span data-ttu-id="955dd-293">**Affects:** Refresh tokens</span><span class="sxs-lookup"><span data-stu-id="955dd-293">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="955dd-294">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using multiple factors.</span><span class="sxs-lookup"><span data-stu-id="955dd-294">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="955dd-295">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span><span class="sxs-lookup"><span data-stu-id="955dd-295">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span></span> <span data-ttu-id="955dd-296">(This is true as long as the current refresh token is not revoked, and it is not unused for longer than the inactive time.) At that point, users are forced to reauthenticate to receive a new refresh token.</span><span class="sxs-lookup"><span data-stu-id="955dd-296">(This is true as long as the current refresh token is not revoked, and it is not unused for longer than the inactive time.) At that point, users are forced to reauthenticate to receive a new refresh token.</span></span>

<span data-ttu-id="955dd-297">Reducing the max age forces users to authenticate more often.</span><span class="sxs-lookup"><span data-stu-id="955dd-297">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="955dd-298">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Refresh Token Max Age property.</span><span class="sxs-lookup"><span data-stu-id="955dd-298">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Refresh Token Max Age property.</span></span>

### <a name="single-factor-session-token-max-age"></a><span data-ttu-id="955dd-299">Single-Factor Session Token Max Age</span><span class="sxs-lookup"><span data-stu-id="955dd-299">Single-Factor Session Token Max Age</span></span>
<span data-ttu-id="955dd-300">**String:** MaxAgeSessionSingleFactor</span><span class="sxs-lookup"><span data-stu-id="955dd-300">**String:** MaxAgeSessionSingleFactor</span></span>

<span data-ttu-id="955dd-301">**Affects:** Session tokens (persistent and nonpersistent)</span><span class="sxs-lookup"><span data-stu-id="955dd-301">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="955dd-302">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after they last authenticated successfully by using only a single factor.</span><span class="sxs-lookup"><span data-stu-id="955dd-302">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="955dd-303">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span><span class="sxs-lookup"><span data-stu-id="955dd-303">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span></span> <span data-ttu-id="955dd-304">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span><span class="sxs-lookup"><span data-stu-id="955dd-304">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span></span>

<span data-ttu-id="955dd-305">Reducing the max age forces users to authenticate more often.</span><span class="sxs-lookup"><span data-stu-id="955dd-305">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="955dd-306">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or less than the Multi-Factor Session Token Max Age property.</span><span class="sxs-lookup"><span data-stu-id="955dd-306">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or less than the Multi-Factor Session Token Max Age property.</span></span>

### <a name="multi-factor-session-token-max-age"></a><span data-ttu-id="955dd-307">Multi-Factor Session Token Max Age</span><span class="sxs-lookup"><span data-stu-id="955dd-307">Multi-Factor Session Token Max Age</span></span>
<span data-ttu-id="955dd-308">**String:** MaxAgeSessionMultiFactor</span><span class="sxs-lookup"><span data-stu-id="955dd-308">**String:** MaxAgeSessionMultiFactor</span></span>

<span data-ttu-id="955dd-309">**Affects:** Session tokens (persistent and nonpersistent)</span><span class="sxs-lookup"><span data-stu-id="955dd-309">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="955dd-310">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after the last time they authenticated successfully by using multiple factors.</span><span class="sxs-lookup"><span data-stu-id="955dd-310">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after the last time they authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="955dd-311">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span><span class="sxs-lookup"><span data-stu-id="955dd-311">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span></span> <span data-ttu-id="955dd-312">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span><span class="sxs-lookup"><span data-stu-id="955dd-312">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span></span>

<span data-ttu-id="955dd-313">Reducing the max age forces users to authenticate more often.</span><span class="sxs-lookup"><span data-stu-id="955dd-313">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="955dd-314">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Session Token Max Age property.</span><span class="sxs-lookup"><span data-stu-id="955dd-314">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Session Token Max Age property.</span></span>

## <a name="example-token-lifetime-policies"></a><span data-ttu-id="955dd-315">Example token lifetime policies</span><span class="sxs-lookup"><span data-stu-id="955dd-315">Example token lifetime policies</span></span>
<span data-ttu-id="955dd-316">Many scenarios are possible in Azure AD when you can create and manage token lifetimes for apps, service principals, and your overall organization.</span><span class="sxs-lookup"><span data-stu-id="955dd-316">Many scenarios are possible in Azure AD when you can create and manage token lifetimes for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="955dd-317">In this section, we walk through a few common policy scenarios that can help you impose new rules for:</span><span class="sxs-lookup"><span data-stu-id="955dd-317">In this section, we walk through a few common policy scenarios that can help you impose new rules for:</span></span>

* <span data-ttu-id="955dd-318">Token Lifetime</span><span class="sxs-lookup"><span data-stu-id="955dd-318">Token Lifetime</span></span>
* <span data-ttu-id="955dd-319">Token Max Inactive Time</span><span class="sxs-lookup"><span data-stu-id="955dd-319">Token Max Inactive Time</span></span>
* <span data-ttu-id="955dd-320">Token Max Age</span><span class="sxs-lookup"><span data-stu-id="955dd-320">Token Max Age</span></span>

<span data-ttu-id="955dd-321">In the examples, you can learn how to:</span><span class="sxs-lookup"><span data-stu-id="955dd-321">In the examples, you can learn how to:</span></span>

* <span data-ttu-id="955dd-322">Manage an organization's default policy</span><span class="sxs-lookup"><span data-stu-id="955dd-322">Manage an organization's default policy</span></span>
* <span data-ttu-id="955dd-323">Create a policy for web sign-in</span><span class="sxs-lookup"><span data-stu-id="955dd-323">Create a policy for web sign-in</span></span>
* <span data-ttu-id="955dd-324">Create a policy for a native app that calls a web API</span><span class="sxs-lookup"><span data-stu-id="955dd-324">Create a policy for a native app that calls a web API</span></span>
* <span data-ttu-id="955dd-325">Manage an advanced policy</span><span class="sxs-lookup"><span data-stu-id="955dd-325">Manage an advanced policy</span></span>

### <a name="prerequisites"></a><span data-ttu-id="955dd-326">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="955dd-326">Prerequisites</span></span>
<span data-ttu-id="955dd-327">In the following examples, you create, update, link, and delete policies for apps, service principals, and your overall organization.</span><span class="sxs-lookup"><span data-stu-id="955dd-327">In the following examples, you create, update, link, and delete policies for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="955dd-328">If you are new to Azure AD, we recommend that you learn about [how to get an Azure AD tenant](active-directory-howto-tenant.md) before you proceed with these examples.</span><span class="sxs-lookup"><span data-stu-id="955dd-328">If you are new to Azure AD, we recommend that you learn about [how to get an Azure AD tenant](active-directory-howto-tenant.md) before you proceed with these examples.</span></span>  

<span data-ttu-id="955dd-329">To get started, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="955dd-329">To get started, do the following steps:</span></span>

1. <span data-ttu-id="955dd-330">Download the latest [Azure AD PowerShell Module Public Preview release](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="955dd-330">Download the latest [Azure AD PowerShell Module Public Preview release](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>
2. <span data-ttu-id="955dd-331">Run the `Connect` command to sign in to your Azure AD admin account.</span><span class="sxs-lookup"><span data-stu-id="955dd-331">Run the `Connect` command to sign in to your Azure AD admin account.</span></span> <span data-ttu-id="955dd-332">Run this command each time you start a new session.</span><span class="sxs-lookup"><span data-stu-id="955dd-332">Run this command each time you start a new session.</span></span>

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. <span data-ttu-id="955dd-333">To see all policies that have been created in your organization, run the following command.</span><span class="sxs-lookup"><span data-stu-id="955dd-333">To see all policies that have been created in your organization, run the following command.</span></span> <span data-ttu-id="955dd-334">Run this command after most operations in the following scenarios.</span><span class="sxs-lookup"><span data-stu-id="955dd-334">Run this command after most operations in the following scenarios.</span></span> <span data-ttu-id="955dd-335">Running the command also helps you get the \*\* \*\* of your policies.</span><span class="sxs-lookup"><span data-stu-id="955dd-335">Running the command also helps you get the \*\* \*\* of your policies.</span></span>

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a><span data-ttu-id="955dd-336">Example: Manage an organization's default policy</span><span class="sxs-lookup"><span data-stu-id="955dd-336">Example: Manage an organization's default policy</span></span>
<span data-ttu-id="955dd-337">In this example, you create a policy that lets your users sign in less frequently across your entire organization.</span><span class="sxs-lookup"><span data-stu-id="955dd-337">In this example, you create a policy that lets your users sign in less frequently across your entire organization.</span></span> <span data-ttu-id="955dd-338">To do this, create a token lifetime policy for Single-Factor Refresh Tokens, which is applied across your organization.</span><span class="sxs-lookup"><span data-stu-id="955dd-338">To do this, create a token lifetime policy for Single-Factor Refresh Tokens, which is applied across your organization.</span></span> <span data-ttu-id="955dd-339">The policy is applied to every application in your organization, and to each service principal that doesn’t already have a policy set.</span><span class="sxs-lookup"><span data-stu-id="955dd-339">The policy is applied to every application in your organization, and to each service principal that doesn’t already have a policy set.</span></span>

1. <span data-ttu-id="955dd-340">Create a token lifetime policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-340">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="955dd-341">Set the Single-Factor Refresh Token to "until-revoked."</span><span class="sxs-lookup"><span data-stu-id="955dd-341">Set the Single-Factor Refresh Token to "until-revoked."</span></span> <span data-ttu-id="955dd-342">The token doesn't expire until access is revoked.</span><span class="sxs-lookup"><span data-stu-id="955dd-342">The token doesn't expire until access is revoked.</span></span> <span data-ttu-id="955dd-343">Create the following policy definition:</span><span class="sxs-lookup"><span data-stu-id="955dd-343">Create the following policy definition:</span></span>

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  <span data-ttu-id="955dd-344">To create the policy, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-344">To create the policy, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  <span data-ttu-id="955dd-345">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-345">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="955dd-346">Update the policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-346">Update the policy.</span></span>

    <span data-ttu-id="955dd-347">You might decide that the first policy you set in this example is not as strict as your service requires.</span><span class="sxs-lookup"><span data-stu-id="955dd-347">You might decide that the first policy you set in this example is not as strict as your service requires.</span></span> <span data-ttu-id="955dd-348">To set your Single-Factor Refresh Token to expire in two days, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-348">To set your Single-Factor Refresh Token to expire in two days, run the following command:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a><span data-ttu-id="955dd-349">Example: Create a policy for web sign-in</span><span class="sxs-lookup"><span data-stu-id="955dd-349">Example: Create a policy for web sign-in</span></span>

<span data-ttu-id="955dd-350">In this example, you create a policy that requires users to authenticate more frequently in your web app.</span><span class="sxs-lookup"><span data-stu-id="955dd-350">In this example, you create a policy that requires users to authenticate more frequently in your web app.</span></span> <span data-ttu-id="955dd-351">This policy sets the lifetime of the access/ID tokens and the max age of a multi-factor session token to the service principal of your web app.</span><span class="sxs-lookup"><span data-stu-id="955dd-351">This policy sets the lifetime of the access/ID tokens and the max age of a multi-factor session token to the service principal of your web app.</span></span>

1. <span data-ttu-id="955dd-352">Create a token lifetime policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-352">Create a token lifetime policy.</span></span>

    <span data-ttu-id="955dd-353">This policy, for web sign-in, sets the access/ID token lifetime and the max single-factor session token age to two hours.</span><span class="sxs-lookup"><span data-stu-id="955dd-353">This policy, for web sign-in, sets the access/ID token lifetime and the max single-factor session token age to two hours.</span></span>

    1.  <span data-ttu-id="955dd-354">To create the policy, run this command:</span><span class="sxs-lookup"><span data-stu-id="955dd-354">To create the policy, run this command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="955dd-355">To see your new policy, and to get the policy **ObjectId**, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-355">To see your new policy, and to get the policy **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  <span data-ttu-id="955dd-356">Assign the policy to your service principal.</span><span class="sxs-lookup"><span data-stu-id="955dd-356">Assign the policy to your service principal.</span></span> <span data-ttu-id="955dd-357">You also need to get the **ObjectId** of your service principal.</span><span class="sxs-lookup"><span data-stu-id="955dd-357">You also need to get the **ObjectId** of your service principal.</span></span> 

    1.  <span data-ttu-id="955dd-358">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span><span class="sxs-lookup"><span data-stu-id="955dd-358">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="955dd-359">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in to your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="955dd-359">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in to your Azure AD account.</span></span>

    2.  <span data-ttu-id="955dd-360">When you have the **ObjectId** of your service principal, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-360">When you have the **ObjectId** of your service principal, run the following command:</span></span>

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a><span data-ttu-id="955dd-361">Example: Create a policy for a native app that calls a web API</span><span class="sxs-lookup"><span data-stu-id="955dd-361">Example: Create a policy for a native app that calls a web API</span></span>
<span data-ttu-id="955dd-362">In this example, you create a policy that requires users to authenticate less frequently.</span><span class="sxs-lookup"><span data-stu-id="955dd-362">In this example, you create a policy that requires users to authenticate less frequently.</span></span> <span data-ttu-id="955dd-363">The policy also lengthens the amount of time a user can be inactive before the user must reauthenticate.</span><span class="sxs-lookup"><span data-stu-id="955dd-363">The policy also lengthens the amount of time a user can be inactive before the user must reauthenticate.</span></span> <span data-ttu-id="955dd-364">The policy is applied to the web API.</span><span class="sxs-lookup"><span data-stu-id="955dd-364">The policy is applied to the web API.</span></span> <span data-ttu-id="955dd-365">When the native app requests the web API as a resource, this policy is applied.</span><span class="sxs-lookup"><span data-stu-id="955dd-365">When the native app requests the web API as a resource, this policy is applied.</span></span>

1. <span data-ttu-id="955dd-366">Create a token lifetime policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-366">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="955dd-367">To create a strict policy for a web API, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-367">To create a strict policy for a web API, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="955dd-368">To see your new policy, and to get the policy **ObjectId**, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-368">To see your new policy, and to get the policy **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="955dd-369">Assign the policy to your web API.</span><span class="sxs-lookup"><span data-stu-id="955dd-369">Assign the policy to your web API.</span></span> <span data-ttu-id="955dd-370">You also need to get the **ObjectId** of your application.</span><span class="sxs-lookup"><span data-stu-id="955dd-370">You also need to get the **ObjectId** of your application.</span></span> <span data-ttu-id="955dd-371">The best way to find your app's **ObjectId** is to use the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="955dd-371">The best way to find your app's **ObjectId** is to use the [Azure portal](https://portal.azure.com/).</span></span>

   <span data-ttu-id="955dd-372">When you have the **ObjectId** of your app, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-372">When you have the **ObjectId** of your app, run the following command:</span></span>

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of the Application> -RefObjectId <ObjectId of the Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a><span data-ttu-id="955dd-373">Example: Manage an advanced policy</span><span class="sxs-lookup"><span data-stu-id="955dd-373">Example: Manage an advanced policy</span></span>
<span data-ttu-id="955dd-374">In this example, you create a few policies, to learn how the priority system works.</span><span class="sxs-lookup"><span data-stu-id="955dd-374">In this example, you create a few policies, to learn how the priority system works.</span></span> <span data-ttu-id="955dd-375">You also can learn how to manage multiple policies that are applied to several objects.</span><span class="sxs-lookup"><span data-stu-id="955dd-375">You also can learn how to manage multiple policies that are applied to several objects.</span></span>

1. <span data-ttu-id="955dd-376">Create a token lifetime policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-376">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="955dd-377">To create an organization default policy that sets the Single-Factor Refresh Token lifetime to 30 days, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-377">To create an organization default policy that sets the Single-Factor Refresh Token lifetime to 30 days, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="955dd-378">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-378">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="955dd-379">Assign the policy to a service principal.</span><span class="sxs-lookup"><span data-stu-id="955dd-379">Assign the policy to a service principal.</span></span>

    <span data-ttu-id="955dd-380">Now, you have a policy that applies to the entire organization.</span><span class="sxs-lookup"><span data-stu-id="955dd-380">Now, you have a policy that applies to the entire organization.</span></span> <span data-ttu-id="955dd-381">You might want to preserve this 30-day policy for a specific service principal, but change the organization default policy to the upper limit of "until-revoked."</span><span class="sxs-lookup"><span data-stu-id="955dd-381">You might want to preserve this 30-day policy for a specific service principal, but change the organization default policy to the upper limit of "until-revoked."</span></span>

    1.  <span data-ttu-id="955dd-382">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span><span class="sxs-lookup"><span data-stu-id="955dd-382">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="955dd-383">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in by using your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="955dd-383">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in by using your Azure AD account.</span></span>

    2.  <span data-ttu-id="955dd-384">When you have the **ObjectId** of your service principal, run the following command:</span><span class="sxs-lookup"><span data-stu-id="955dd-384">When you have the **ObjectId** of your service principal, run the following command:</span></span>

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
            ```
        
3. <span data-ttu-id="955dd-385">Set the `IsOrganizationDefault` flag to false:</span><span class="sxs-lookup"><span data-stu-id="955dd-385">Set the `IsOrganizationDefault` flag to false:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. <span data-ttu-id="955dd-386">Create a new organization default policy:</span><span class="sxs-lookup"><span data-stu-id="955dd-386">Create a new organization default policy:</span></span>

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    <span data-ttu-id="955dd-387">You now have the original policy linked to your service principal, and the new policy is set as your organization default policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-387">You now have the original policy linked to your service principal, and the new policy is set as your organization default policy.</span></span> <span data-ttu-id="955dd-388">It's important to remember that policies applied to service principals have priority over organization default policies.</span><span class="sxs-lookup"><span data-stu-id="955dd-388">It's important to remember that policies applied to service principals have priority over organization default policies.</span></span>

## <a name="cmdlet-reference"></a><span data-ttu-id="955dd-389">Cmdlet reference</span><span class="sxs-lookup"><span data-stu-id="955dd-389">Cmdlet reference</span></span>

### <a name="manage-policies"></a><span data-ttu-id="955dd-390">Manage policies</span><span class="sxs-lookup"><span data-stu-id="955dd-390">Manage policies</span></span>

<span data-ttu-id="955dd-391">You can use the following cmdlets to manage policies.</span><span class="sxs-lookup"><span data-stu-id="955dd-391">You can use the following cmdlets to manage policies.</span></span>

#### <a name="new-azureadpolicy"></a><span data-ttu-id="955dd-392">New-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-392">New-AzureADPolicy</span></span>

<span data-ttu-id="955dd-393">Creates a new policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-393">Creates a new policy.</span></span>

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| <span data-ttu-id="955dd-394">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-394">Parameters</span></span> | <span data-ttu-id="955dd-395">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-395">Description</span></span> | <span data-ttu-id="955dd-396">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-396">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Definition</code> |<span data-ttu-id="955dd-397">Array of stringified JSON that contains all the policy's rules.</span><span class="sxs-lookup"><span data-stu-id="955dd-397">Array of stringified JSON that contains all the policy's rules.</span></span> | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="955dd-398">String of the policy name.</span><span class="sxs-lookup"><span data-stu-id="955dd-398">String of the policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |<span data-ttu-id="955dd-399">If true, sets the policy as the organization's default policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-399">If true, sets the policy as the organization's default policy.</span></span> <span data-ttu-id="955dd-400">If false, does nothing.</span><span class="sxs-lookup"><span data-stu-id="955dd-400">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |<span data-ttu-id="955dd-401">Type of policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-401">Type of policy.</span></span> <span data-ttu-id="955dd-402">For token lifetimes, always use "TokenLifetimePolicy."</span><span class="sxs-lookup"><span data-stu-id="955dd-402">For token lifetimes, always use "TokenLifetimePolicy."</span></span> | `-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="955dd-403"><code>&#8209;AlternativeIdentifier</code> [Optional]</span><span class="sxs-lookup"><span data-stu-id="955dd-403"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="955dd-404">Sets an alternative ID for the policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-404">Sets an alternative ID for the policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a><span data-ttu-id="955dd-405">Get-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-405">Get-AzureADPolicy</span></span>
<span data-ttu-id="955dd-406">Gets all Azure AD policies or a specified policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-406">Gets all Azure AD policies or a specified policy.</span></span>

```PowerShell
Get-AzureADPolicy
```

| <span data-ttu-id="955dd-407">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-407">Parameters</span></span> | <span data-ttu-id="955dd-408">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-408">Description</span></span> | <span data-ttu-id="955dd-409">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-409">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="955dd-410"><code>&#8209;Id</code> [Optional]</span><span class="sxs-lookup"><span data-stu-id="955dd-410"><code>&#8209;Id</code> [Optional]</span></span> |<span data-ttu-id="955dd-411">**ObjectId (Id)** of the policy you want.</span><span class="sxs-lookup"><span data-stu-id="955dd-411">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a><span data-ttu-id="955dd-412">Get-AzureADPolicyAppliedObject</span><span class="sxs-lookup"><span data-stu-id="955dd-412">Get-AzureADPolicyAppliedObject</span></span>
<span data-ttu-id="955dd-413">Gets all apps and service principals that are linked to a policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-413">Gets all apps and service principals that are linked to a policy.</span></span>

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| <span data-ttu-id="955dd-414">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-414">Parameters</span></span> | <span data-ttu-id="955dd-415">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-415">Description</span></span> | <span data-ttu-id="955dd-416">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-416">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="955dd-417">**ObjectId (Id)** of the policy you want.</span><span class="sxs-lookup"><span data-stu-id="955dd-417">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a><span data-ttu-id="955dd-418">Set-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-418">Set-AzureADPolicy</span></span>
<span data-ttu-id="955dd-419">Updates an existing policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-419">Updates an existing policy.</span></span>

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| <span data-ttu-id="955dd-420">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-420">Parameters</span></span> | <span data-ttu-id="955dd-421">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-421">Description</span></span> | <span data-ttu-id="955dd-422">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-422">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="955dd-423">**ObjectId (Id)** of the policy you want.</span><span class="sxs-lookup"><span data-stu-id="955dd-423">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="955dd-424">String of the policy name.</span><span class="sxs-lookup"><span data-stu-id="955dd-424">String of the policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <span data-ttu-id="955dd-425"><code>&#8209;Definition</code> [Optional]</span><span class="sxs-lookup"><span data-stu-id="955dd-425"><code>&#8209;Definition</code> [Optional]</span></span> |<span data-ttu-id="955dd-426">Array of stringified JSON that contains all the policy's rules.</span><span class="sxs-lookup"><span data-stu-id="955dd-426">Array of stringified JSON that contains all the policy's rules.</span></span> |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <span data-ttu-id="955dd-427"><code>&#8209;IsOrganizationDefault</code> [Optional]</span><span class="sxs-lookup"><span data-stu-id="955dd-427"><code>&#8209;IsOrganizationDefault</code> [Optional]</span></span> |<span data-ttu-id="955dd-428">If true, sets the policy as the organization's default policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-428">If true, sets the policy as the organization's default policy.</span></span> <span data-ttu-id="955dd-429">If false, does nothing.</span><span class="sxs-lookup"><span data-stu-id="955dd-429">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <span data-ttu-id="955dd-430"><code>&#8209;Type</code> [Optional]</span><span class="sxs-lookup"><span data-stu-id="955dd-430"><code>&#8209;Type</code> [Optional]</span></span> |<span data-ttu-id="955dd-431">Type of policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-431">Type of policy.</span></span> <span data-ttu-id="955dd-432">For token lifetimes, always use "TokenLifetimePolicy."</span><span class="sxs-lookup"><span data-stu-id="955dd-432">For token lifetimes, always use "TokenLifetimePolicy."</span></span> |`-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="955dd-433"><code>&#8209;AlternativeIdentifier</code> [Optional]</span><span class="sxs-lookup"><span data-stu-id="955dd-433"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="955dd-434">Sets an alternative ID for the policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-434">Sets an alternative ID for the policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a><span data-ttu-id="955dd-435">Remove-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-435">Remove-AzureADPolicy</span></span>
<span data-ttu-id="955dd-436">Deletes the specified policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-436">Deletes the specified policy.</span></span>

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| <span data-ttu-id="955dd-437">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-437">Parameters</span></span> | <span data-ttu-id="955dd-438">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-438">Description</span></span> | <span data-ttu-id="955dd-439">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-439">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="955dd-440">**ObjectId (Id)** of the policy you want.</span><span class="sxs-lookup"><span data-stu-id="955dd-440">**ObjectId (Id)** of the policy you want.</span></span> | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a><span data-ttu-id="955dd-441">Application policies</span><span class="sxs-lookup"><span data-stu-id="955dd-441">Application policies</span></span>
<span data-ttu-id="955dd-442">You can use the following cmdlets for application policies.</span><span class="sxs-lookup"><span data-stu-id="955dd-442">You can use the following cmdlets for application policies.</span></span></br></br>

#### <a name="add-azureadapplicationpolicy"></a><span data-ttu-id="955dd-443">Add-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-443">Add-AzureADApplicationPolicy</span></span>
<span data-ttu-id="955dd-444">Links the specified policy to an application.</span><span class="sxs-lookup"><span data-stu-id="955dd-444">Links the specified policy to an application.</span></span>

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="955dd-445">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-445">Parameters</span></span> | <span data-ttu-id="955dd-446">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-446">Description</span></span> | <span data-ttu-id="955dd-447">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-447">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="955dd-448">**ObjectId (Id)** of the application.</span><span class="sxs-lookup"><span data-stu-id="955dd-448">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="955dd-449">**ObjectId** of the policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-449">**ObjectId** of the policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a><span data-ttu-id="955dd-450">Get-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-450">Get-AzureADApplicationPolicy</span></span>
<span data-ttu-id="955dd-451">Gets the policy that is assigned to an application.</span><span class="sxs-lookup"><span data-stu-id="955dd-451">Gets the policy that is assigned to an application.</span></span>

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| <span data-ttu-id="955dd-452">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-452">Parameters</span></span> | <span data-ttu-id="955dd-453">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-453">Description</span></span> | <span data-ttu-id="955dd-454">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-454">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="955dd-455">**ObjectId (Id)** of the application.</span><span class="sxs-lookup"><span data-stu-id="955dd-455">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a><span data-ttu-id="955dd-456">Remove-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-456">Remove-AzureADApplicationPolicy</span></span>
<span data-ttu-id="955dd-457">Removes a policy from an application.</span><span class="sxs-lookup"><span data-stu-id="955dd-457">Removes a policy from an application.</span></span>

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="955dd-458">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-458">Parameters</span></span> | <span data-ttu-id="955dd-459">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-459">Description</span></span> | <span data-ttu-id="955dd-460">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-460">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="955dd-461">**ObjectId (Id)** of the application.</span><span class="sxs-lookup"><span data-stu-id="955dd-461">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="955dd-462">**ObjectId** of the policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-462">**ObjectId** of the policy.</span></span> | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a><span data-ttu-id="955dd-463">Service principal policies</span><span class="sxs-lookup"><span data-stu-id="955dd-463">Service principal policies</span></span>
<span data-ttu-id="955dd-464">You can use the following cmdlets for service principal policies.</span><span class="sxs-lookup"><span data-stu-id="955dd-464">You can use the following cmdlets for service principal policies.</span></span>

#### <a name="add-azureadserviceprincipalpolicy"></a><span data-ttu-id="955dd-465">Add-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-465">Add-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="955dd-466">Links the specified policy to a service principal.</span><span class="sxs-lookup"><span data-stu-id="955dd-466">Links the specified policy to a service principal.</span></span>

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="955dd-467">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-467">Parameters</span></span> | <span data-ttu-id="955dd-468">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-468">Description</span></span> | <span data-ttu-id="955dd-469">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-469">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="955dd-470">**ObjectId (Id)** of the application.</span><span class="sxs-lookup"><span data-stu-id="955dd-470">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="955dd-471">**ObjectId** of the policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-471">**ObjectId** of the policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a><span data-ttu-id="955dd-472">Get-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-472">Get-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="955dd-473">Gets any policy linked to the specified service principal.</span><span class="sxs-lookup"><span data-stu-id="955dd-473">Gets any policy linked to the specified service principal.</span></span>

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| <span data-ttu-id="955dd-474">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-474">Parameters</span></span> | <span data-ttu-id="955dd-475">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-475">Description</span></span> | <span data-ttu-id="955dd-476">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-476">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="955dd-477">**ObjectId (Id)** of the application.</span><span class="sxs-lookup"><span data-stu-id="955dd-477">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a><span data-ttu-id="955dd-478">Remove-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="955dd-478">Remove-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="955dd-479">Removes the policy from the specified service principal.</span><span class="sxs-lookup"><span data-stu-id="955dd-479">Removes the policy from the specified service principal.</span></span>

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="955dd-480">Parameters</span><span class="sxs-lookup"><span data-stu-id="955dd-480">Parameters</span></span> | <span data-ttu-id="955dd-481">Description</span><span class="sxs-lookup"><span data-stu-id="955dd-481">Description</span></span> | <span data-ttu-id="955dd-482">Example</span><span class="sxs-lookup"><span data-stu-id="955dd-482">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="955dd-483">**ObjectId (Id)** of the application.</span><span class="sxs-lookup"><span data-stu-id="955dd-483">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="955dd-484">**ObjectId** of the policy.</span><span class="sxs-lookup"><span data-stu-id="955dd-484">**ObjectId** of the policy.</span></span> | `-PolicyId <ObjectId of Policy>` |
