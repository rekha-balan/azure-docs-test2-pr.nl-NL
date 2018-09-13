---
title: Understanding custom policies of the starter pack in Azure Active Directory B2C | Microsoft Docs
description: A topic on Azure Active Directory B2C custom policies.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/25/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: ebcd7a677acde12558b0f566bce9172a0d00233b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867743"
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="bd1e2-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span><span class="sxs-lookup"><span data-stu-id="bd1e2-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="bd1e2-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="bd1e2-105">As such, it more particularly focuses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-105">As such, it more particularly focuses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd1e2-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="bd1e2-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="bd1e2-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="bd1e2-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="bd1e2-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="bd1e2-111">Claims schemas</span><span class="sxs-lookup"><span data-stu-id="bd1e2-111">Claims schemas</span></span>

<span data-ttu-id="bd1e2-112">This claims schemas is divided into three sections:</span><span class="sxs-lookup"><span data-stu-id="bd1e2-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="bd1e2-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="bd1e2-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="bd1e2-115">**Please do not modify these claims**.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="bd1e2-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="bd1e2-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd1e2-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="bd1e2-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the custom policy.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the custom policy.</span></span> <span data-ttu-id="bd1e2-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="bd1e2-121">The available claim types are listed below.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="bd1e2-122">Claims that are required for the user journeys</span><span class="sxs-lookup"><span data-stu-id="bd1e2-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="bd1e2-123">The following claims are required for user journeys to work properly:</span><span class="sxs-lookup"><span data-stu-id="bd1e2-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="bd1e2-124">Claims type</span><span class="sxs-lookup"><span data-stu-id="bd1e2-124">Claims type</span></span> | <span data-ttu-id="bd1e2-125">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="bd1e2-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-126">*UserId*</span></span> | <span data-ttu-id="bd1e2-127">Username</span><span class="sxs-lookup"><span data-stu-id="bd1e2-127">Username</span></span> |
| <span data-ttu-id="bd1e2-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-128">*signInName*</span></span> | <span data-ttu-id="bd1e2-129">Sign in name</span><span class="sxs-lookup"><span data-stu-id="bd1e2-129">Sign in name</span></span> |
| <span data-ttu-id="bd1e2-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-130">*tenantId*</span></span> | <span data-ttu-id="bd1e2-131">Tenant identifier (ID) of the user object in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bd1e2-131">Tenant identifier (ID) of the user object in Azure AD B2C</span></span> |
| <span data-ttu-id="bd1e2-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-132">*objectId*</span></span> | <span data-ttu-id="bd1e2-133">Object identifier (ID) of the user object in Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bd1e2-133">Object identifier (ID) of the user object in Azure AD B2C</span></span> |
| <span data-ttu-id="bd1e2-134">*password*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-134">*password*</span></span> | <span data-ttu-id="bd1e2-135">Password</span><span class="sxs-lookup"><span data-stu-id="bd1e2-135">Password</span></span> |
| <span data-ttu-id="bd1e2-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-136">*newPassword*</span></span> | |
| <span data-ttu-id="bd1e2-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="bd1e2-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-138">*passwordPolicies*</span></span> | <span data-ttu-id="bd1e2-139">Password policies used by Azure AD B2C to determine password strength, expiry, etc.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-139">Password policies used by Azure AD B2C to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="bd1e2-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-140">*sub*</span></span> | |
| <span data-ttu-id="bd1e2-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="bd1e2-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-142">*identityProvider*</span></span> | |
| <span data-ttu-id="bd1e2-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-143">*displayName*</span></span> | |
| <span data-ttu-id="bd1e2-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="bd1e2-145">User's telephone number</span><span class="sxs-lookup"><span data-stu-id="bd1e2-145">User's telephone number</span></span> |
| <span data-ttu-id="bd1e2-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="bd1e2-147">*email*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-147">*email*</span></span> | <span data-ttu-id="bd1e2-148">Email address that can be used to contact the user</span><span class="sxs-lookup"><span data-stu-id="bd1e2-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="bd1e2-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="bd1e2-150">Email address that the user can use to sign in</span><span class="sxs-lookup"><span data-stu-id="bd1e2-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="bd1e2-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-151">*otherMails*</span></span> | <span data-ttu-id="bd1e2-152">Email addresses that can be used to contact the user</span><span class="sxs-lookup"><span data-stu-id="bd1e2-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="bd1e2-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-153">*userPrincipalName*</span></span> | <span data-ttu-id="bd1e2-154">Username as stored in the Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bd1e2-154">Username as stored in the Azure AD B2C</span></span> |
| <span data-ttu-id="bd1e2-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-155">*upnUserName*</span></span> | <span data-ttu-id="bd1e2-156">Username for creating user principal name</span><span class="sxs-lookup"><span data-stu-id="bd1e2-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="bd1e2-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-157">*mailNickName*</span></span> | <span data-ttu-id="bd1e2-158">User's mail nick name as stored in the Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bd1e2-158">User's mail nick name as stored in the Azure AD B2C</span></span> |
| <span data-ttu-id="bd1e2-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-159">*newUser*</span></span> | |
| <span data-ttu-id="bd1e2-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="bd1e2-161">Claim that specifies whether attributes were collected from the user</span><span class="sxs-lookup"><span data-stu-id="bd1e2-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="bd1e2-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="bd1e2-163">Claim that specifies whether a new phone number was collected from the user</span><span class="sxs-lookup"><span data-stu-id="bd1e2-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="bd1e2-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-164">*authenticationSource*</span></span> | <span data-ttu-id="bd1e2-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span><span class="sxs-lookup"><span data-stu-id="bd1e2-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="bd1e2-166">Claims required for query string parameters and other special parameters</span><span class="sxs-lookup"><span data-stu-id="bd1e2-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="bd1e2-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span><span class="sxs-lookup"><span data-stu-id="bd1e2-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="bd1e2-168">Claims type</span><span class="sxs-lookup"><span data-stu-id="bd1e2-168">Claims type</span></span> | <span data-ttu-id="bd1e2-169">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="bd1e2-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-170">*nux*</span></span> | <span data-ttu-id="bd1e2-171">Special parameter passed for local account authentication to login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="bd1e2-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="bd1e2-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-172">*nca*</span></span> | <span data-ttu-id="bd1e2-173">Special parameter passed for local account authentication to login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="bd1e2-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="bd1e2-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-174">*prompt*</span></span> | <span data-ttu-id="bd1e2-175">Special parameter passed for local account authentication to login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="bd1e2-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="bd1e2-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-176">*mkt*</span></span> | <span data-ttu-id="bd1e2-177">Special parameter passed for local account authentication to login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="bd1e2-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="bd1e2-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-178">*lc*</span></span> | <span data-ttu-id="bd1e2-179">Special parameter passed for local account authentication to login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="bd1e2-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="bd1e2-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-180">*grant_type*</span></span> | <span data-ttu-id="bd1e2-181">Special parameter passed for local account authentication to login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="bd1e2-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="bd1e2-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-182">*scope*</span></span> | <span data-ttu-id="bd1e2-183">Special parameter passed for local account authentication to login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="bd1e2-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="bd1e2-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-184">*client_id*</span></span> | <span data-ttu-id="bd1e2-185">Special parameter passed for local account authentication to login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="bd1e2-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="bd1e2-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-186">*objectIdFromSession*</span></span> | <span data-ttu-id="bd1e2-187">Parameter provided by the default session management provider to indicate that the object ID has been retrieved from an SSO session</span><span class="sxs-lookup"><span data-stu-id="bd1e2-187">Parameter provided by the default session management provider to indicate that the object ID has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="bd1e2-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-188">*isActiveMFASession*</span></span> | <span data-ttu-id="bd1e2-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span><span class="sxs-lookup"><span data-stu-id="bd1e2-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="bd1e2-190">Additional (optional) claims that can be collected</span><span class="sxs-lookup"><span data-stu-id="bd1e2-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="bd1e2-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="bd1e2-192">As outlined before, additional claims can be added to this list.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="bd1e2-193">Claims type</span><span class="sxs-lookup"><span data-stu-id="bd1e2-193">Claims type</span></span> | <span data-ttu-id="bd1e2-194">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="bd1e2-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-195">*givenName*</span></span> | <span data-ttu-id="bd1e2-196">User's given name (also known as first name)</span><span class="sxs-lookup"><span data-stu-id="bd1e2-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="bd1e2-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-197">*surname*</span></span> | <span data-ttu-id="bd1e2-198">User's surname (also known as family name or last name)</span><span class="sxs-lookup"><span data-stu-id="bd1e2-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="bd1e2-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-199">*Extension_picture*</span></span> | <span data-ttu-id="bd1e2-200">User's picture from social</span><span class="sxs-lookup"><span data-stu-id="bd1e2-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="bd1e2-201">Claim transformations</span><span class="sxs-lookup"><span data-stu-id="bd1e2-201">Claim transformations</span></span>

<span data-ttu-id="bd1e2-202">The available claim transformations are listed below.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="bd1e2-203">Claim transformation</span><span class="sxs-lookup"><span data-stu-id="bd1e2-203">Claim transformation</span></span> | <span data-ttu-id="bd1e2-204">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="bd1e2-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="bd1e2-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="bd1e2-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="bd1e2-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="bd1e2-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="bd1e2-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="bd1e2-211">Content definitions</span><span class="sxs-lookup"><span data-stu-id="bd1e2-211">Content definitions</span></span>

<span data-ttu-id="bd1e2-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="bd1e2-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="bd1e2-214">Claims provider</span><span class="sxs-lookup"><span data-stu-id="bd1e2-214">Claims provider</span></span> | <span data-ttu-id="bd1e2-215">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="bd1e2-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-216">*Facebook*</span></span> | |
| <span data-ttu-id="bd1e2-217">*Local Account SignIn*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="bd1e2-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="bd1e2-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="bd1e2-220">*Self Asserted*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="bd1e2-221">*Local Account*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-221">*Local Account*</span></span> | |
| <span data-ttu-id="bd1e2-222">*Session Management*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-222">*Session Management*</span></span> | |
| <span data-ttu-id="bd1e2-223">*Trustframework Policy Engine*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="bd1e2-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="bd1e2-225">*Token Issuer*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="bd1e2-226">Technical profiles</span><span class="sxs-lookup"><span data-stu-id="bd1e2-226">Technical profiles</span></span>

<span data-ttu-id="bd1e2-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="bd1e2-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="bd1e2-229">Technical profiles for Facebook</span><span class="sxs-lookup"><span data-stu-id="bd1e2-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="bd1e2-230">Technical profile</span><span class="sxs-lookup"><span data-stu-id="bd1e2-230">Technical profile</span></span> | <span data-ttu-id="bd1e2-231">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="bd1e2-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="bd1e2-233">Technical profiles for Local Account Signin</span><span class="sxs-lookup"><span data-stu-id="bd1e2-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="bd1e2-234">Technical profile</span><span class="sxs-lookup"><span data-stu-id="bd1e2-234">Technical profile</span></span> | <span data-ttu-id="bd1e2-235">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="bd1e2-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="bd1e2-237">Technical profiles for Phone Factor</span><span class="sxs-lookup"><span data-stu-id="bd1e2-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="bd1e2-238">Technical profile</span><span class="sxs-lookup"><span data-stu-id="bd1e2-238">Technical profile</span></span> | <span data-ttu-id="bd1e2-239">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="bd1e2-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="bd1e2-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="bd1e2-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="bd1e2-243">Technical profiles for Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd1e2-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="bd1e2-244">Technical profile</span><span class="sxs-lookup"><span data-stu-id="bd1e2-244">Technical profile</span></span> | <span data-ttu-id="bd1e2-245">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="bd1e2-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-246">*AAD-Common*</span></span> | <span data-ttu-id="bd1e2-247">Technical profile included by the other AAD-xxx technical profiles</span><span class="sxs-lookup"><span data-stu-id="bd1e2-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="bd1e2-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="bd1e2-249">Technical profile for social logins</span><span class="sxs-lookup"><span data-stu-id="bd1e2-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="bd1e2-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="bd1e2-251">Technical profile for social logins</span><span class="sxs-lookup"><span data-stu-id="bd1e2-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="bd1e2-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="bd1e2-253">Technical profile for social logins</span><span class="sxs-lookup"><span data-stu-id="bd1e2-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="bd1e2-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="bd1e2-255">Technical profile for local accounts</span><span class="sxs-lookup"><span data-stu-id="bd1e2-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="bd1e2-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="bd1e2-257">Technical profile for local accounts</span><span class="sxs-lookup"><span data-stu-id="bd1e2-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="bd1e2-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="bd1e2-259">Technical profile for updating user record using objectId</span><span class="sxs-lookup"><span data-stu-id="bd1e2-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="bd1e2-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="bd1e2-261">Technical profile for updating user record using objectId</span><span class="sxs-lookup"><span data-stu-id="bd1e2-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="bd1e2-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="bd1e2-263">Technical profile for updating user record using objectId</span><span class="sxs-lookup"><span data-stu-id="bd1e2-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="bd1e2-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="bd1e2-265">Technical profile is used to read data after user authenticates</span><span class="sxs-lookup"><span data-stu-id="bd1e2-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="bd1e2-266">Technical profiles for Self Asserted</span><span class="sxs-lookup"><span data-stu-id="bd1e2-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="bd1e2-267">Technical profile</span><span class="sxs-lookup"><span data-stu-id="bd1e2-267">Technical profile</span></span> | <span data-ttu-id="bd1e2-268">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="bd1e2-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="bd1e2-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="bd1e2-271">Technical profiles for Local Account</span><span class="sxs-lookup"><span data-stu-id="bd1e2-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="bd1e2-272">Technical profile</span><span class="sxs-lookup"><span data-stu-id="bd1e2-272">Technical profile</span></span> | <span data-ttu-id="bd1e2-273">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="bd1e2-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="bd1e2-275">Technical profiles for Session Management</span><span class="sxs-lookup"><span data-stu-id="bd1e2-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="bd1e2-276">Technical profile</span><span class="sxs-lookup"><span data-stu-id="bd1e2-276">Technical profile</span></span> | <span data-ttu-id="bd1e2-277">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="bd1e2-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="bd1e2-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="bd1e2-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="bd1e2-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span><span class="sxs-lookup"><span data-stu-id="bd1e2-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="bd1e2-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="bd1e2-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-the-trust-framework-policy-engine"></a><span data-ttu-id="bd1e2-284">Technical profiles for the trust framework policy engine</span><span class="sxs-lookup"><span data-stu-id="bd1e2-284">Technical profiles for the trust framework policy engine</span></span>

<span data-ttu-id="bd1e2-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="bd1e2-286">Technical profiles for Token Issuer</span><span class="sxs-lookup"><span data-stu-id="bd1e2-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="bd1e2-287">Technical profile</span><span class="sxs-lookup"><span data-stu-id="bd1e2-287">Technical profile</span></span> | <span data-ttu-id="bd1e2-288">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="bd1e2-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="bd1e2-290">User journeys</span><span class="sxs-lookup"><span data-stu-id="bd1e2-290">User journeys</span></span>

<span data-ttu-id="bd1e2-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="bd1e2-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span><span class="sxs-lookup"><span data-stu-id="bd1e2-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="bd1e2-293">User journey</span><span class="sxs-lookup"><span data-stu-id="bd1e2-293">User journey</span></span> | <span data-ttu-id="bd1e2-294">Description</span><span class="sxs-lookup"><span data-stu-id="bd1e2-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="bd1e2-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-295">*SignUp*</span></span> | |
| <span data-ttu-id="bd1e2-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-296">*SignIn*</span></span> | |
| <span data-ttu-id="bd1e2-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="bd1e2-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-298">*EditProfile*</span></span> | |
| <span data-ttu-id="bd1e2-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="bd1e2-299">*PasswordReset*</span></span> | |
