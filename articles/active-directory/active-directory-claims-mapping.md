---
title: Claims mapping in Azure Active Directory (public preview)| Microsoft Docs
description: This page describes Azure Active Directory claims mapping.
services: active-directory
author: billmath
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: e6d2d8dfd6f7a40158b098983bd34bbd5d8271f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870784"
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a><span data-ttu-id="ab973-103">Claims mapping in Azure Active Directory (public preview)</span><span class="sxs-lookup"><span data-stu-id="ab973-103">Claims mapping in Azure Active Directory (public preview)</span></span>

>[!NOTE]
><span data-ttu-id="ab973-104">This feature replaces and supersedes the [claims customization](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) offered through the portal today.</span><span class="sxs-lookup"><span data-stu-id="ab973-104">This feature replaces and supersedes the [claims customization](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) offered through the portal today.</span></span> <span data-ttu-id="ab973-105">If you customize claims using the portal in addition to the Graph/PowerShell method detailed in this document on the same application, tokens issued for that application will ignore the configuration in the portal.</span><span class="sxs-lookup"><span data-stu-id="ab973-105">If you customize claims using the portal in addition to the Graph/PowerShell method detailed in this document on the same application, tokens issued for that application will ignore the configuration in the portal.</span></span>
<span data-ttu-id="ab973-106">Configurations made through the methods detailed in this document will not be reflected in the portal.</span><span class="sxs-lookup"><span data-stu-id="ab973-106">Configurations made through the methods detailed in this document will not be reflected in the portal.</span></span>

<span data-ttu-id="ab973-107">This feature is used by tenant admins to customize the claims emitted in tokens for a specific application in their tenant.</span><span class="sxs-lookup"><span data-stu-id="ab973-107">This feature is used by tenant admins to customize the claims emitted in tokens for a specific application in their tenant.</span></span> <span data-ttu-id="ab973-108">You can use claims mapping policies to:</span><span class="sxs-lookup"><span data-stu-id="ab973-108">You can use claims mapping policies to:</span></span>

- <span data-ttu-id="ab973-109">Select which claims are included in tokens.</span><span class="sxs-lookup"><span data-stu-id="ab973-109">Select which claims are included in tokens.</span></span>
- <span data-ttu-id="ab973-110">Create claim types that do not already exist.</span><span class="sxs-lookup"><span data-stu-id="ab973-110">Create claim types that do not already exist.</span></span>
- <span data-ttu-id="ab973-111">Choose or change the source of data emitted in specific claims.</span><span class="sxs-lookup"><span data-stu-id="ab973-111">Choose or change the source of data emitted in specific claims.</span></span>

>[!NOTE]
><span data-ttu-id="ab973-112">This capability currently is in public preview.</span><span class="sxs-lookup"><span data-stu-id="ab973-112">This capability currently is in public preview.</span></span> <span data-ttu-id="ab973-113">Be prepared to revert or remove any changes.</span><span class="sxs-lookup"><span data-stu-id="ab973-113">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="ab973-114">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span><span class="sxs-lookup"><span data-stu-id="ab973-114">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="ab973-115">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span><span class="sxs-lookup"><span data-stu-id="ab973-115">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span> <span data-ttu-id="ab973-116">This feature supports configuring claim mapping policies for WS-Fed, SAML, OAuth and OpenID Connect protocols.</span><span class="sxs-lookup"><span data-stu-id="ab973-116">This feature supports configuring claim mapping policies for WS-Fed, SAML, OAuth and OpenID Connect protocols.</span></span>

## <a name="claims-mapping-policy-type"></a><span data-ttu-id="ab973-117">Claims mapping policy type</span><span class="sxs-lookup"><span data-stu-id="ab973-117">Claims mapping policy type</span></span>
<span data-ttu-id="ab973-118">In Azure AD, a **Policy** object represents a set of rules enforced on individual applications, or on all applications in an organization.</span><span class="sxs-lookup"><span data-stu-id="ab973-118">In Azure AD, a **Policy** object represents a set of rules enforced on individual applications, or on all applications in an organization.</span></span> <span data-ttu-id="ab973-119">Each type of policy has a unique structure, with a set of properties that are then applied to objects to which they are assigned.</span><span class="sxs-lookup"><span data-stu-id="ab973-119">Each type of policy has a unique structure, with a set of properties that are then applied to objects to which they are assigned.</span></span>

<span data-ttu-id="ab973-120">A claims mapping policy is a type of **Policy** object that modifies the claims emitted in tokens issued for specific applications.</span><span class="sxs-lookup"><span data-stu-id="ab973-120">A claims mapping policy is a type of **Policy** object that modifies the claims emitted in tokens issued for specific applications.</span></span>

## <a name="claim-sets"></a><span data-ttu-id="ab973-121">Claim sets</span><span class="sxs-lookup"><span data-stu-id="ab973-121">Claim sets</span></span>
<span data-ttu-id="ab973-122">There are certain sets of claims that define how and when they are used in tokens.</span><span class="sxs-lookup"><span data-stu-id="ab973-122">There are certain sets of claims that define how and when they are used in tokens.</span></span>

### <a name="core-claim-set"></a><span data-ttu-id="ab973-123">Core claim set</span><span class="sxs-lookup"><span data-stu-id="ab973-123">Core claim set</span></span>
<span data-ttu-id="ab973-124">Claims in the core claim set are present in every token, regardless of policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-124">Claims in the core claim set are present in every token, regardless of policy.</span></span> <span data-ttu-id="ab973-125">These claims are also considered restricted, and cannot be modified.</span><span class="sxs-lookup"><span data-stu-id="ab973-125">These claims are also considered restricted, and cannot be modified.</span></span>

### <a name="basic-claim-set"></a><span data-ttu-id="ab973-126">Basic claim set</span><span class="sxs-lookup"><span data-stu-id="ab973-126">Basic claim set</span></span>
<span data-ttu-id="ab973-127">The basic claim set includes the claims that are emitted by default for tokens (in addition to the core claim set).</span><span class="sxs-lookup"><span data-stu-id="ab973-127">The basic claim set includes the claims that are emitted by default for tokens (in addition to the core claim set).</span></span> <span data-ttu-id="ab973-128">These claims can be omitted or modified by using the claims mapping policies.</span><span class="sxs-lookup"><span data-stu-id="ab973-128">These claims can be omitted or modified by using the claims mapping policies.</span></span>

### <a name="restricted-claim-set"></a><span data-ttu-id="ab973-129">Restricted claim set</span><span class="sxs-lookup"><span data-stu-id="ab973-129">Restricted claim set</span></span>
<span data-ttu-id="ab973-130">Restricted claims cannot be modified by using policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-130">Restricted claims cannot be modified by using policy.</span></span> <span data-ttu-id="ab973-131">The data source cannot be changed, and no transformation is applied when generating these claims.</span><span class="sxs-lookup"><span data-stu-id="ab973-131">The data source cannot be changed, and no transformation is applied when generating these claims.</span></span>

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a><span data-ttu-id="ab973-132">Table 1: JSON Web Token (JWT) restricted claim set</span><span class="sxs-lookup"><span data-stu-id="ab973-132">Table 1: JSON Web Token (JWT) restricted claim set</span></span>
|<span data-ttu-id="ab973-133">Claim type (name)</span><span class="sxs-lookup"><span data-stu-id="ab973-133">Claim type (name)</span></span>|
| ----- |
|<span data-ttu-id="ab973-134">_claim_names</span><span class="sxs-lookup"><span data-stu-id="ab973-134">_claim_names</span></span>|
|<span data-ttu-id="ab973-135">_claim_sources</span><span class="sxs-lookup"><span data-stu-id="ab973-135">_claim_sources</span></span>|
|<span data-ttu-id="ab973-136">access_token</span><span class="sxs-lookup"><span data-stu-id="ab973-136">access_token</span></span>|
|<span data-ttu-id="ab973-137">account_type</span><span class="sxs-lookup"><span data-stu-id="ab973-137">account_type</span></span>|
|<span data-ttu-id="ab973-138">acr</span><span class="sxs-lookup"><span data-stu-id="ab973-138">acr</span></span>|
|<span data-ttu-id="ab973-139">actor</span><span class="sxs-lookup"><span data-stu-id="ab973-139">actor</span></span>|
|<span data-ttu-id="ab973-140">actortoken</span><span class="sxs-lookup"><span data-stu-id="ab973-140">actortoken</span></span>|
|<span data-ttu-id="ab973-141">aio</span><span class="sxs-lookup"><span data-stu-id="ab973-141">aio</span></span>|
|<span data-ttu-id="ab973-142">altsecid</span><span class="sxs-lookup"><span data-stu-id="ab973-142">altsecid</span></span>|
|<span data-ttu-id="ab973-143">amr</span><span class="sxs-lookup"><span data-stu-id="ab973-143">amr</span></span>|
|<span data-ttu-id="ab973-144">app_chain</span><span class="sxs-lookup"><span data-stu-id="ab973-144">app_chain</span></span>|
|<span data-ttu-id="ab973-145">app_displayname</span><span class="sxs-lookup"><span data-stu-id="ab973-145">app_displayname</span></span>|
|<span data-ttu-id="ab973-146">app_res</span><span class="sxs-lookup"><span data-stu-id="ab973-146">app_res</span></span>|
|<span data-ttu-id="ab973-147">appctx</span><span class="sxs-lookup"><span data-stu-id="ab973-147">appctx</span></span>|
|<span data-ttu-id="ab973-148">appctxsender</span><span class="sxs-lookup"><span data-stu-id="ab973-148">appctxsender</span></span>|
|<span data-ttu-id="ab973-149">appid</span><span class="sxs-lookup"><span data-stu-id="ab973-149">appid</span></span>|
|<span data-ttu-id="ab973-150">appidacr</span><span class="sxs-lookup"><span data-stu-id="ab973-150">appidacr</span></span>|
|<span data-ttu-id="ab973-151">assertion</span><span class="sxs-lookup"><span data-stu-id="ab973-151">assertion</span></span>|
|<span data-ttu-id="ab973-152">at_hash</span><span class="sxs-lookup"><span data-stu-id="ab973-152">at_hash</span></span>|
|<span data-ttu-id="ab973-153">aud</span><span class="sxs-lookup"><span data-stu-id="ab973-153">aud</span></span>|
|<span data-ttu-id="ab973-154">auth_data</span><span class="sxs-lookup"><span data-stu-id="ab973-154">auth_data</span></span>|
|<span data-ttu-id="ab973-155">auth_time</span><span class="sxs-lookup"><span data-stu-id="ab973-155">auth_time</span></span>|
|<span data-ttu-id="ab973-156">authorization_code</span><span class="sxs-lookup"><span data-stu-id="ab973-156">authorization_code</span></span>|
|<span data-ttu-id="ab973-157">azp</span><span class="sxs-lookup"><span data-stu-id="ab973-157">azp</span></span>|
|<span data-ttu-id="ab973-158">azpacr</span><span class="sxs-lookup"><span data-stu-id="ab973-158">azpacr</span></span>|
|<span data-ttu-id="ab973-159">c_hash</span><span class="sxs-lookup"><span data-stu-id="ab973-159">c_hash</span></span>|
|<span data-ttu-id="ab973-160">ca_enf</span><span class="sxs-lookup"><span data-stu-id="ab973-160">ca_enf</span></span>|
|<span data-ttu-id="ab973-161">cc</span><span class="sxs-lookup"><span data-stu-id="ab973-161">cc</span></span>|
|<span data-ttu-id="ab973-162">cert_token_use</span><span class="sxs-lookup"><span data-stu-id="ab973-162">cert_token_use</span></span>|
|<span data-ttu-id="ab973-163">client_id</span><span class="sxs-lookup"><span data-stu-id="ab973-163">client_id</span></span>|
|<span data-ttu-id="ab973-164">cloud_graph_host_name</span><span class="sxs-lookup"><span data-stu-id="ab973-164">cloud_graph_host_name</span></span>|
|<span data-ttu-id="ab973-165">cloud_instance_name</span><span class="sxs-lookup"><span data-stu-id="ab973-165">cloud_instance_name</span></span>|
|<span data-ttu-id="ab973-166">cnf</span><span class="sxs-lookup"><span data-stu-id="ab973-166">cnf</span></span>|
|<span data-ttu-id="ab973-167">code</span><span class="sxs-lookup"><span data-stu-id="ab973-167">code</span></span>|
|<span data-ttu-id="ab973-168">controls</span><span class="sxs-lookup"><span data-stu-id="ab973-168">controls</span></span>|
|<span data-ttu-id="ab973-169">credential_keys</span><span class="sxs-lookup"><span data-stu-id="ab973-169">credential_keys</span></span>|
|<span data-ttu-id="ab973-170">csr</span><span class="sxs-lookup"><span data-stu-id="ab973-170">csr</span></span>|
|<span data-ttu-id="ab973-171">csr_type</span><span class="sxs-lookup"><span data-stu-id="ab973-171">csr_type</span></span>|
|<span data-ttu-id="ab973-172">deviceid</span><span class="sxs-lookup"><span data-stu-id="ab973-172">deviceid</span></span>|
|<span data-ttu-id="ab973-173">dns_names</span><span class="sxs-lookup"><span data-stu-id="ab973-173">dns_names</span></span>|
|<span data-ttu-id="ab973-174">domain_dns_name</span><span class="sxs-lookup"><span data-stu-id="ab973-174">domain_dns_name</span></span>|
|<span data-ttu-id="ab973-175">domain_netbios_name</span><span class="sxs-lookup"><span data-stu-id="ab973-175">domain_netbios_name</span></span>|
|<span data-ttu-id="ab973-176">e_exp</span><span class="sxs-lookup"><span data-stu-id="ab973-176">e_exp</span></span>|
|<span data-ttu-id="ab973-177">email</span><span class="sxs-lookup"><span data-stu-id="ab973-177">email</span></span>|
|<span data-ttu-id="ab973-178">endpoint</span><span class="sxs-lookup"><span data-stu-id="ab973-178">endpoint</span></span>|
|<span data-ttu-id="ab973-179">enfpolids</span><span class="sxs-lookup"><span data-stu-id="ab973-179">enfpolids</span></span>|
|<span data-ttu-id="ab973-180">exp</span><span class="sxs-lookup"><span data-stu-id="ab973-180">exp</span></span>|
|<span data-ttu-id="ab973-181">expires_on</span><span class="sxs-lookup"><span data-stu-id="ab973-181">expires_on</span></span>|
|<span data-ttu-id="ab973-182">grant_type</span><span class="sxs-lookup"><span data-stu-id="ab973-182">grant_type</span></span>|
|<span data-ttu-id="ab973-183">graph</span><span class="sxs-lookup"><span data-stu-id="ab973-183">graph</span></span>|
|<span data-ttu-id="ab973-184">group_sids</span><span class="sxs-lookup"><span data-stu-id="ab973-184">group_sids</span></span>|
|<span data-ttu-id="ab973-185">groups</span><span class="sxs-lookup"><span data-stu-id="ab973-185">groups</span></span>|
|<span data-ttu-id="ab973-186">hasgroups</span><span class="sxs-lookup"><span data-stu-id="ab973-186">hasgroups</span></span>|
|<span data-ttu-id="ab973-187">hash_alg</span><span class="sxs-lookup"><span data-stu-id="ab973-187">hash_alg</span></span>|
|<span data-ttu-id="ab973-188">home_oid</span><span class="sxs-lookup"><span data-stu-id="ab973-188">home_oid</span></span>|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier|
|<span data-ttu-id="ab973-189">iat</span><span class="sxs-lookup"><span data-stu-id="ab973-189">iat</span></span>|
|<span data-ttu-id="ab973-190">identityprovider</span><span class="sxs-lookup"><span data-stu-id="ab973-190">identityprovider</span></span>|
|<span data-ttu-id="ab973-191">idp</span><span class="sxs-lookup"><span data-stu-id="ab973-191">idp</span></span>|
|<span data-ttu-id="ab973-192">in_corp</span><span class="sxs-lookup"><span data-stu-id="ab973-192">in_corp</span></span>|
|<span data-ttu-id="ab973-193">instance</span><span class="sxs-lookup"><span data-stu-id="ab973-193">instance</span></span>|
|<span data-ttu-id="ab973-194">ipaddr</span><span class="sxs-lookup"><span data-stu-id="ab973-194">ipaddr</span></span>|
|<span data-ttu-id="ab973-195">isbrowserhostedapp</span><span class="sxs-lookup"><span data-stu-id="ab973-195">isbrowserhostedapp</span></span>|
|<span data-ttu-id="ab973-196">iss</span><span class="sxs-lookup"><span data-stu-id="ab973-196">iss</span></span>|
|<span data-ttu-id="ab973-197">jwk</span><span class="sxs-lookup"><span data-stu-id="ab973-197">jwk</span></span>|
|<span data-ttu-id="ab973-198">key_id</span><span class="sxs-lookup"><span data-stu-id="ab973-198">key_id</span></span>|
|<span data-ttu-id="ab973-199">key_type</span><span class="sxs-lookup"><span data-stu-id="ab973-199">key_type</span></span>|
|<span data-ttu-id="ab973-200">mam_compliance_url</span><span class="sxs-lookup"><span data-stu-id="ab973-200">mam_compliance_url</span></span>|
|<span data-ttu-id="ab973-201">mam_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="ab973-201">mam_enrollment_url</span></span>|
|<span data-ttu-id="ab973-202">mam_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="ab973-202">mam_terms_of_use_url</span></span>|
|<span data-ttu-id="ab973-203">mdm_compliance_url</span><span class="sxs-lookup"><span data-stu-id="ab973-203">mdm_compliance_url</span></span>|
|<span data-ttu-id="ab973-204">mdm_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="ab973-204">mdm_enrollment_url</span></span>|
|<span data-ttu-id="ab973-205">mdm_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="ab973-205">mdm_terms_of_use_url</span></span>|
|<span data-ttu-id="ab973-206">nameid</span><span class="sxs-lookup"><span data-stu-id="ab973-206">nameid</span></span>|
|<span data-ttu-id="ab973-207">nbf</span><span class="sxs-lookup"><span data-stu-id="ab973-207">nbf</span></span>|
|<span data-ttu-id="ab973-208">netbios_name</span><span class="sxs-lookup"><span data-stu-id="ab973-208">netbios_name</span></span>|
|<span data-ttu-id="ab973-209">nonce</span><span class="sxs-lookup"><span data-stu-id="ab973-209">nonce</span></span>|
|<span data-ttu-id="ab973-210">oid</span><span class="sxs-lookup"><span data-stu-id="ab973-210">oid</span></span>|
|<span data-ttu-id="ab973-211">on_prem_id</span><span class="sxs-lookup"><span data-stu-id="ab973-211">on_prem_id</span></span>|
|<span data-ttu-id="ab973-212">onprem_sam_account_name</span><span class="sxs-lookup"><span data-stu-id="ab973-212">onprem_sam_account_name</span></span>|
|<span data-ttu-id="ab973-213">onprem_sid</span><span class="sxs-lookup"><span data-stu-id="ab973-213">onprem_sid</span></span>|
|<span data-ttu-id="ab973-214">openid2_id</span><span class="sxs-lookup"><span data-stu-id="ab973-214">openid2_id</span></span>|
|<span data-ttu-id="ab973-215">password</span><span class="sxs-lookup"><span data-stu-id="ab973-215">password</span></span>|
|<span data-ttu-id="ab973-216">platf</span><span class="sxs-lookup"><span data-stu-id="ab973-216">platf</span></span>|
|<span data-ttu-id="ab973-217">polids</span><span class="sxs-lookup"><span data-stu-id="ab973-217">polids</span></span>|
|<span data-ttu-id="ab973-218">pop_jwk</span><span class="sxs-lookup"><span data-stu-id="ab973-218">pop_jwk</span></span>|
|<span data-ttu-id="ab973-219">preferred_username</span><span class="sxs-lookup"><span data-stu-id="ab973-219">preferred_username</span></span>|
|<span data-ttu-id="ab973-220">previous_refresh_token</span><span class="sxs-lookup"><span data-stu-id="ab973-220">previous_refresh_token</span></span>|
|<span data-ttu-id="ab973-221">primary_sid</span><span class="sxs-lookup"><span data-stu-id="ab973-221">primary_sid</span></span>|
|<span data-ttu-id="ab973-222">puid</span><span class="sxs-lookup"><span data-stu-id="ab973-222">puid</span></span>|
|<span data-ttu-id="ab973-223">pwd_exp</span><span class="sxs-lookup"><span data-stu-id="ab973-223">pwd_exp</span></span>|
|<span data-ttu-id="ab973-224">pwd_url</span><span class="sxs-lookup"><span data-stu-id="ab973-224">pwd_url</span></span>|
|<span data-ttu-id="ab973-225">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="ab973-225">redirect_uri</span></span>|
|<span data-ttu-id="ab973-226">refresh_token</span><span class="sxs-lookup"><span data-stu-id="ab973-226">refresh_token</span></span>|
|<span data-ttu-id="ab973-227">refreshtoken</span><span class="sxs-lookup"><span data-stu-id="ab973-227">refreshtoken</span></span>|
|<span data-ttu-id="ab973-228">request_nonce</span><span class="sxs-lookup"><span data-stu-id="ab973-228">request_nonce</span></span>|
|<span data-ttu-id="ab973-229">resource</span><span class="sxs-lookup"><span data-stu-id="ab973-229">resource</span></span>|
|<span data-ttu-id="ab973-230">role</span><span class="sxs-lookup"><span data-stu-id="ab973-230">role</span></span>|
|<span data-ttu-id="ab973-231">roles</span><span class="sxs-lookup"><span data-stu-id="ab973-231">roles</span></span>|
|<span data-ttu-id="ab973-232">scope</span><span class="sxs-lookup"><span data-stu-id="ab973-232">scope</span></span>|
|<span data-ttu-id="ab973-233">scp</span><span class="sxs-lookup"><span data-stu-id="ab973-233">scp</span></span>|
|<span data-ttu-id="ab973-234">sid</span><span class="sxs-lookup"><span data-stu-id="ab973-234">sid</span></span>|
|<span data-ttu-id="ab973-235">signature</span><span class="sxs-lookup"><span data-stu-id="ab973-235">signature</span></span>|
|<span data-ttu-id="ab973-236">signin_state</span><span class="sxs-lookup"><span data-stu-id="ab973-236">signin_state</span></span>|
|<span data-ttu-id="ab973-237">src1</span><span class="sxs-lookup"><span data-stu-id="ab973-237">src1</span></span>|
|<span data-ttu-id="ab973-238">src2</span><span class="sxs-lookup"><span data-stu-id="ab973-238">src2</span></span>|
|<span data-ttu-id="ab973-239">sub</span><span class="sxs-lookup"><span data-stu-id="ab973-239">sub</span></span>|
|<span data-ttu-id="ab973-240">tbid</span><span class="sxs-lookup"><span data-stu-id="ab973-240">tbid</span></span>|
|<span data-ttu-id="ab973-241">tenant_display_name</span><span class="sxs-lookup"><span data-stu-id="ab973-241">tenant_display_name</span></span>|
|<span data-ttu-id="ab973-242">tenant_region_scope</span><span class="sxs-lookup"><span data-stu-id="ab973-242">tenant_region_scope</span></span>|
|<span data-ttu-id="ab973-243">thumbnail_photo</span><span class="sxs-lookup"><span data-stu-id="ab973-243">thumbnail_photo</span></span>|
|<span data-ttu-id="ab973-244">tid</span><span class="sxs-lookup"><span data-stu-id="ab973-244">tid</span></span>|
|<span data-ttu-id="ab973-245">tokenAutologonEnabled</span><span class="sxs-lookup"><span data-stu-id="ab973-245">tokenAutologonEnabled</span></span>|
|<span data-ttu-id="ab973-246">trustedfordelegation</span><span class="sxs-lookup"><span data-stu-id="ab973-246">trustedfordelegation</span></span>|
|<span data-ttu-id="ab973-247">unique_name</span><span class="sxs-lookup"><span data-stu-id="ab973-247">unique_name</span></span>|
|<span data-ttu-id="ab973-248">upn</span><span class="sxs-lookup"><span data-stu-id="ab973-248">upn</span></span>|
|<span data-ttu-id="ab973-249">user_setting_sync_url</span><span class="sxs-lookup"><span data-stu-id="ab973-249">user_setting_sync_url</span></span>|
|<span data-ttu-id="ab973-250">username</span><span class="sxs-lookup"><span data-stu-id="ab973-250">username</span></span>|
|<span data-ttu-id="ab973-251">uti</span><span class="sxs-lookup"><span data-stu-id="ab973-251">uti</span></span>|
|<span data-ttu-id="ab973-252">ver</span><span class="sxs-lookup"><span data-stu-id="ab973-252">ver</span></span>|
|<span data-ttu-id="ab973-253">verified_primary_email</span><span class="sxs-lookup"><span data-stu-id="ab973-253">verified_primary_email</span></span>|
|<span data-ttu-id="ab973-254">verified_secondary_email</span><span class="sxs-lookup"><span data-stu-id="ab973-254">verified_secondary_email</span></span>|
|<span data-ttu-id="ab973-255">wids</span><span class="sxs-lookup"><span data-stu-id="ab973-255">wids</span></span>|
|<span data-ttu-id="ab973-256">win_ver</span><span class="sxs-lookup"><span data-stu-id="ab973-256">win_ver</span></span>|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a><span data-ttu-id="ab973-257">Table 2: Security Assertion Markup Language (SAML) restricted claim set</span><span class="sxs-lookup"><span data-stu-id="ab973-257">Table 2: Security Assertion Markup Language (SAML) restricted claim set</span></span>
|<span data-ttu-id="ab973-258">Claim type (URI)</span><span class="sxs-lookup"><span data-stu-id="ab973-258">Claim type (URI)</span></span>|
| ----- |
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.microsoft.com/identity/claims/accesstoken|
|http://schemas.microsoft.com/identity/claims/openid2_id|
|http://schemas.microsoft.com/identity/claims/identityprovider|
|http://schemas.microsoft.com/identity/claims/objectidentifier|
|http://schemas.microsoft.com/identity/claims/puid|
|<span data-ttu-id="ab973-259">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span><span class="sxs-lookup"><span data-stu-id="ab973-259">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span></span> |
|http://schemas.microsoft.com/identity/claims/tenantid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groups|
|http://schemas.microsoft.com/claims/groups.link|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/role|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier|
|http://schemas.microsoft.com/identity/claims/scope|

## <a name="claims-mapping-policy-properties"></a><span data-ttu-id="ab973-260">Claims mapping policy properties</span><span class="sxs-lookup"><span data-stu-id="ab973-260">Claims mapping policy properties</span></span>
<span data-ttu-id="ab973-261">Use the properties of a claims mapping policy to control which claims are emitted, and where the data is sourced from.</span><span class="sxs-lookup"><span data-stu-id="ab973-261">Use the properties of a claims mapping policy to control which claims are emitted, and where the data is sourced from.</span></span> <span data-ttu-id="ab973-262">If no policy is set, the system issues tokens containing the core claim set, the basic claim set, and any [optional claims](develop/active-directory-optional-claims.md) that the application has chosen to receive.</span><span class="sxs-lookup"><span data-stu-id="ab973-262">If no policy is set, the system issues tokens containing the core claim set, the basic claim set, and any [optional claims](develop/active-directory-optional-claims.md) that the application has chosen to receive.</span></span>

### <a name="include-basic-claim-set"></a><span data-ttu-id="ab973-263">Include basic claim set</span><span class="sxs-lookup"><span data-stu-id="ab973-263">Include basic claim set</span></span>

<span data-ttu-id="ab973-264">**String:** IncludeBasicClaimSet</span><span class="sxs-lookup"><span data-stu-id="ab973-264">**String:** IncludeBasicClaimSet</span></span>

<span data-ttu-id="ab973-265">**Data type:** Boolean (True or False)</span><span class="sxs-lookup"><span data-stu-id="ab973-265">**Data type:** Boolean (True or False)</span></span>

<span data-ttu-id="ab973-266">**Summary:** This property determines whether the basic claim set is included in tokens affected by this policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-266">**Summary:** This property determines whether the basic claim set is included in tokens affected by this policy.</span></span> 

- <span data-ttu-id="ab973-267">If set to True, all claims in the basic claim set are emitted in tokens affected by the policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-267">If set to True, all claims in the basic claim set are emitted in tokens affected by the policy.</span></span> 
- <span data-ttu-id="ab973-268">If set to False, claims in the basic claim set are not in the tokens, unless they are individually added in the claims schema property of the same policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-268">If set to False, claims in the basic claim set are not in the tokens, unless they are individually added in the claims schema property of the same policy.</span></span>

>[!NOTE] 
><span data-ttu-id="ab973-269">Claims in the core claim set are present in every token, regardless of what this property is set to.</span><span class="sxs-lookup"><span data-stu-id="ab973-269">Claims in the core claim set are present in every token, regardless of what this property is set to.</span></span> 

### <a name="claims-schema"></a><span data-ttu-id="ab973-270">Claims schema</span><span class="sxs-lookup"><span data-stu-id="ab973-270">Claims schema</span></span>

<span data-ttu-id="ab973-271">**String:** ClaimsSchema</span><span class="sxs-lookup"><span data-stu-id="ab973-271">**String:** ClaimsSchema</span></span>

<span data-ttu-id="ab973-272">**Data type:** JSON blob with one or more claim schema entries</span><span class="sxs-lookup"><span data-stu-id="ab973-272">**Data type:** JSON blob with one or more claim schema entries</span></span>

<span data-ttu-id="ab973-273">**Summary:** This property defines which claims are present in the tokens affected by the policy, in addition to the basic claim set and the core claim set.</span><span class="sxs-lookup"><span data-stu-id="ab973-273">**Summary:** This property defines which claims are present in the tokens affected by the policy, in addition to the basic claim set and the core claim set.</span></span>
<span data-ttu-id="ab973-274">For each claim schema entry defined in this property, certain information is required.</span><span class="sxs-lookup"><span data-stu-id="ab973-274">For each claim schema entry defined in this property, certain information is required.</span></span> <span data-ttu-id="ab973-275">You must specify where the data is coming from (**Value** or **Source/ID pair**), and which claim the data is emitted as (**Claim Type**).</span><span class="sxs-lookup"><span data-stu-id="ab973-275">You must specify where the data is coming from (**Value** or **Source/ID pair**), and which claim the data is emitted as (**Claim Type**).</span></span>

### <a name="claim-schema-entry-elements"></a><span data-ttu-id="ab973-276">Claim schema entry elements</span><span class="sxs-lookup"><span data-stu-id="ab973-276">Claim schema entry elements</span></span>

<span data-ttu-id="ab973-277">**Value:** The Value element defines a static value as the data to be emitted in the claim.</span><span class="sxs-lookup"><span data-stu-id="ab973-277">**Value:** The Value element defines a static value as the data to be emitted in the claim.</span></span>

<span data-ttu-id="ab973-278">**Source/ID pair:** The Source and ID elements define where the data in the claim is sourced from.</span><span class="sxs-lookup"><span data-stu-id="ab973-278">**Source/ID pair:** The Source and ID elements define where the data in the claim is sourced from.</span></span> 

<span data-ttu-id="ab973-279">The Source element must be set to one of the following:</span><span class="sxs-lookup"><span data-stu-id="ab973-279">The Source element must be set to one of the following:</span></span> 


- <span data-ttu-id="ab973-280">"user": The data in the claim is a property on the User object.</span><span class="sxs-lookup"><span data-stu-id="ab973-280">"user": The data in the claim is a property on the User object.</span></span> 
- <span data-ttu-id="ab973-281">"application": The data in the claim is a property on the application (client) service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-281">"application": The data in the claim is a property on the application (client) service principal.</span></span> 
- <span data-ttu-id="ab973-282">"resource": The data in the claim is a property on the resource service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-282">"resource": The data in the claim is a property on the resource service principal.</span></span>
- <span data-ttu-id="ab973-283">"audience": The data in the claim is a property on the service principal that is the audience of the token (either the client or resource service principal).</span><span class="sxs-lookup"><span data-stu-id="ab973-283">"audience": The data in the claim is a property on the service principal that is the audience of the token (either the client or resource service principal).</span></span>
- <span data-ttu-id="ab973-284">“company”: The data in the claim is a property on the resource tenant’s Company object.</span><span class="sxs-lookup"><span data-stu-id="ab973-284">“company”: The data in the claim is a property on the resource tenant’s Company object.</span></span>
- <span data-ttu-id="ab973-285">"transformation": The data in the claim is from claims transformation (see the "Claims transformation" section later in this article).</span><span class="sxs-lookup"><span data-stu-id="ab973-285">"transformation": The data in the claim is from claims transformation (see the "Claims transformation" section later in this article).</span></span> 

<span data-ttu-id="ab973-286">If the source is transformation, the **TransformationID** element must be included in this claim definition as well.</span><span class="sxs-lookup"><span data-stu-id="ab973-286">If the source is transformation, the **TransformationID** element must be included in this claim definition as well.</span></span>

<span data-ttu-id="ab973-287">The ID element identifies which property on the source provides the value for the claim.</span><span class="sxs-lookup"><span data-stu-id="ab973-287">The ID element identifies which property on the source provides the value for the claim.</span></span> <span data-ttu-id="ab973-288">The following table lists the values of ID valid for each value of Source.</span><span class="sxs-lookup"><span data-stu-id="ab973-288">The following table lists the values of ID valid for each value of Source.</span></span>

#### <a name="table-3-valid-id-values-per-source"></a><span data-ttu-id="ab973-289">Table 3: Valid ID values per source</span><span class="sxs-lookup"><span data-stu-id="ab973-289">Table 3: Valid ID values per source</span></span>
|<span data-ttu-id="ab973-290">Source</span><span class="sxs-lookup"><span data-stu-id="ab973-290">Source</span></span>|<span data-ttu-id="ab973-291">ID</span><span class="sxs-lookup"><span data-stu-id="ab973-291">ID</span></span>|<span data-ttu-id="ab973-292">Description</span><span class="sxs-lookup"><span data-stu-id="ab973-292">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="ab973-293">User</span><span class="sxs-lookup"><span data-stu-id="ab973-293">User</span></span>|<span data-ttu-id="ab973-294">surname</span><span class="sxs-lookup"><span data-stu-id="ab973-294">surname</span></span>|<span data-ttu-id="ab973-295">Family Name</span><span class="sxs-lookup"><span data-stu-id="ab973-295">Family Name</span></span>|
|<span data-ttu-id="ab973-296">User</span><span class="sxs-lookup"><span data-stu-id="ab973-296">User</span></span>|<span data-ttu-id="ab973-297">givenname</span><span class="sxs-lookup"><span data-stu-id="ab973-297">givenname</span></span>|<span data-ttu-id="ab973-298">Given Name</span><span class="sxs-lookup"><span data-stu-id="ab973-298">Given Name</span></span>|
|<span data-ttu-id="ab973-299">User</span><span class="sxs-lookup"><span data-stu-id="ab973-299">User</span></span>|<span data-ttu-id="ab973-300">displayname</span><span class="sxs-lookup"><span data-stu-id="ab973-300">displayname</span></span>|<span data-ttu-id="ab973-301">Display Name</span><span class="sxs-lookup"><span data-stu-id="ab973-301">Display Name</span></span>|
|<span data-ttu-id="ab973-302">User</span><span class="sxs-lookup"><span data-stu-id="ab973-302">User</span></span>|<span data-ttu-id="ab973-303">objectid</span><span class="sxs-lookup"><span data-stu-id="ab973-303">objectid</span></span>|<span data-ttu-id="ab973-304">ObjectID</span><span class="sxs-lookup"><span data-stu-id="ab973-304">ObjectID</span></span>|
|<span data-ttu-id="ab973-305">User</span><span class="sxs-lookup"><span data-stu-id="ab973-305">User</span></span>|<span data-ttu-id="ab973-306">mail</span><span class="sxs-lookup"><span data-stu-id="ab973-306">mail</span></span>|<span data-ttu-id="ab973-307">Email Address</span><span class="sxs-lookup"><span data-stu-id="ab973-307">Email Address</span></span>|
|<span data-ttu-id="ab973-308">User</span><span class="sxs-lookup"><span data-stu-id="ab973-308">User</span></span>|<span data-ttu-id="ab973-309">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ab973-309">userprincipalname</span></span>|<span data-ttu-id="ab973-310">User Principal Name</span><span class="sxs-lookup"><span data-stu-id="ab973-310">User Principal Name</span></span>|
|<span data-ttu-id="ab973-311">User</span><span class="sxs-lookup"><span data-stu-id="ab973-311">User</span></span>|<span data-ttu-id="ab973-312">department</span><span class="sxs-lookup"><span data-stu-id="ab973-312">department</span></span>|<span data-ttu-id="ab973-313">Department</span><span class="sxs-lookup"><span data-stu-id="ab973-313">Department</span></span>|
|<span data-ttu-id="ab973-314">User</span><span class="sxs-lookup"><span data-stu-id="ab973-314">User</span></span>|<span data-ttu-id="ab973-315">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="ab973-315">onpremisessamaccountname</span></span>|<span data-ttu-id="ab973-316">On Premises Sam Account Name</span><span class="sxs-lookup"><span data-stu-id="ab973-316">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="ab973-317">User</span><span class="sxs-lookup"><span data-stu-id="ab973-317">User</span></span>|<span data-ttu-id="ab973-318">netbiosname</span><span class="sxs-lookup"><span data-stu-id="ab973-318">netbiosname</span></span>|<span data-ttu-id="ab973-319">NetBios Name</span><span class="sxs-lookup"><span data-stu-id="ab973-319">NetBios Name</span></span>|
|<span data-ttu-id="ab973-320">User</span><span class="sxs-lookup"><span data-stu-id="ab973-320">User</span></span>|<span data-ttu-id="ab973-321">dnsdomainname</span><span class="sxs-lookup"><span data-stu-id="ab973-321">dnsdomainname</span></span>|<span data-ttu-id="ab973-322">Dns Domain Name</span><span class="sxs-lookup"><span data-stu-id="ab973-322">Dns Domain Name</span></span>|
|<span data-ttu-id="ab973-323">User</span><span class="sxs-lookup"><span data-stu-id="ab973-323">User</span></span>|<span data-ttu-id="ab973-324">onpremisesecurityidentifier</span><span class="sxs-lookup"><span data-stu-id="ab973-324">onpremisesecurityidentifier</span></span>|<span data-ttu-id="ab973-325">on-premises Security Identifier</span><span class="sxs-lookup"><span data-stu-id="ab973-325">on-premises Security Identifier</span></span>|
|<span data-ttu-id="ab973-326">User</span><span class="sxs-lookup"><span data-stu-id="ab973-326">User</span></span>|<span data-ttu-id="ab973-327">companyname</span><span class="sxs-lookup"><span data-stu-id="ab973-327">companyname</span></span>|<span data-ttu-id="ab973-328">Organization Name</span><span class="sxs-lookup"><span data-stu-id="ab973-328">Organization Name</span></span>|
|<span data-ttu-id="ab973-329">User</span><span class="sxs-lookup"><span data-stu-id="ab973-329">User</span></span>|<span data-ttu-id="ab973-330">streetaddress</span><span class="sxs-lookup"><span data-stu-id="ab973-330">streetaddress</span></span>|<span data-ttu-id="ab973-331">Street Address</span><span class="sxs-lookup"><span data-stu-id="ab973-331">Street Address</span></span>|
|<span data-ttu-id="ab973-332">User</span><span class="sxs-lookup"><span data-stu-id="ab973-332">User</span></span>|<span data-ttu-id="ab973-333">postalcode</span><span class="sxs-lookup"><span data-stu-id="ab973-333">postalcode</span></span>|<span data-ttu-id="ab973-334">Postal Code</span><span class="sxs-lookup"><span data-stu-id="ab973-334">Postal Code</span></span>|
|<span data-ttu-id="ab973-335">User</span><span class="sxs-lookup"><span data-stu-id="ab973-335">User</span></span>|<span data-ttu-id="ab973-336">preferredlanguange</span><span class="sxs-lookup"><span data-stu-id="ab973-336">preferredlanguange</span></span>|<span data-ttu-id="ab973-337">Preferred Language</span><span class="sxs-lookup"><span data-stu-id="ab973-337">Preferred Language</span></span>|
|<span data-ttu-id="ab973-338">User</span><span class="sxs-lookup"><span data-stu-id="ab973-338">User</span></span>|<span data-ttu-id="ab973-339">onpremisesuserprincipalname</span><span class="sxs-lookup"><span data-stu-id="ab973-339">onpremisesuserprincipalname</span></span>|<span data-ttu-id="ab973-340">on-premises UPN</span><span class="sxs-lookup"><span data-stu-id="ab973-340">on-premises UPN</span></span>|
|<span data-ttu-id="ab973-341">User</span><span class="sxs-lookup"><span data-stu-id="ab973-341">User</span></span>|<span data-ttu-id="ab973-342">mailnickname</span><span class="sxs-lookup"><span data-stu-id="ab973-342">mailnickname</span></span>|<span data-ttu-id="ab973-343">Mail Nickname</span><span class="sxs-lookup"><span data-stu-id="ab973-343">Mail Nickname</span></span>|
|<span data-ttu-id="ab973-344">User</span><span class="sxs-lookup"><span data-stu-id="ab973-344">User</span></span>|<span data-ttu-id="ab973-345">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="ab973-345">extensionattribute1</span></span>|<span data-ttu-id="ab973-346">Extension Attribute 1</span><span class="sxs-lookup"><span data-stu-id="ab973-346">Extension Attribute 1</span></span>|
|<span data-ttu-id="ab973-347">User</span><span class="sxs-lookup"><span data-stu-id="ab973-347">User</span></span>|<span data-ttu-id="ab973-348">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="ab973-348">extensionattribute2</span></span>|<span data-ttu-id="ab973-349">Extension Attribute 2</span><span class="sxs-lookup"><span data-stu-id="ab973-349">Extension Attribute 2</span></span>|
|<span data-ttu-id="ab973-350">User</span><span class="sxs-lookup"><span data-stu-id="ab973-350">User</span></span>|<span data-ttu-id="ab973-351">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="ab973-351">extensionattribute3</span></span>|<span data-ttu-id="ab973-352">Extension Attribute 3</span><span class="sxs-lookup"><span data-stu-id="ab973-352">Extension Attribute 3</span></span>|
|<span data-ttu-id="ab973-353">User</span><span class="sxs-lookup"><span data-stu-id="ab973-353">User</span></span>|<span data-ttu-id="ab973-354">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="ab973-354">extensionattribute4</span></span>|<span data-ttu-id="ab973-355">Extension Attribute 4</span><span class="sxs-lookup"><span data-stu-id="ab973-355">Extension Attribute 4</span></span>|
|<span data-ttu-id="ab973-356">User</span><span class="sxs-lookup"><span data-stu-id="ab973-356">User</span></span>|<span data-ttu-id="ab973-357">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="ab973-357">extensionattribute5</span></span>|<span data-ttu-id="ab973-358">Extension Attribute 5</span><span class="sxs-lookup"><span data-stu-id="ab973-358">Extension Attribute 5</span></span>|
|<span data-ttu-id="ab973-359">User</span><span class="sxs-lookup"><span data-stu-id="ab973-359">User</span></span>|<span data-ttu-id="ab973-360">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="ab973-360">extensionattribute6</span></span>|<span data-ttu-id="ab973-361">Extension Attribute 6</span><span class="sxs-lookup"><span data-stu-id="ab973-361">Extension Attribute 6</span></span>|
|<span data-ttu-id="ab973-362">User</span><span class="sxs-lookup"><span data-stu-id="ab973-362">User</span></span>|<span data-ttu-id="ab973-363">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="ab973-363">extensionattribute7</span></span>|<span data-ttu-id="ab973-364">Extension Attribute 7</span><span class="sxs-lookup"><span data-stu-id="ab973-364">Extension Attribute 7</span></span>|
|<span data-ttu-id="ab973-365">User</span><span class="sxs-lookup"><span data-stu-id="ab973-365">User</span></span>|<span data-ttu-id="ab973-366">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="ab973-366">extensionattribute8</span></span>|<span data-ttu-id="ab973-367">Extension Attribute 8</span><span class="sxs-lookup"><span data-stu-id="ab973-367">Extension Attribute 8</span></span>|
|<span data-ttu-id="ab973-368">User</span><span class="sxs-lookup"><span data-stu-id="ab973-368">User</span></span>|<span data-ttu-id="ab973-369">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="ab973-369">extensionattribute9</span></span>|<span data-ttu-id="ab973-370">Extension Attribute 9</span><span class="sxs-lookup"><span data-stu-id="ab973-370">Extension Attribute 9</span></span>|
|<span data-ttu-id="ab973-371">User</span><span class="sxs-lookup"><span data-stu-id="ab973-371">User</span></span>|<span data-ttu-id="ab973-372">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="ab973-372">extensionattribute10</span></span>|<span data-ttu-id="ab973-373">Extension Attribute 10</span><span class="sxs-lookup"><span data-stu-id="ab973-373">Extension Attribute 10</span></span>|
|<span data-ttu-id="ab973-374">User</span><span class="sxs-lookup"><span data-stu-id="ab973-374">User</span></span>|<span data-ttu-id="ab973-375">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="ab973-375">extensionattribute11</span></span>|<span data-ttu-id="ab973-376">Extension Attribute 11</span><span class="sxs-lookup"><span data-stu-id="ab973-376">Extension Attribute 11</span></span>|
|<span data-ttu-id="ab973-377">User</span><span class="sxs-lookup"><span data-stu-id="ab973-377">User</span></span>|<span data-ttu-id="ab973-378">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="ab973-378">extensionattribute12</span></span>|<span data-ttu-id="ab973-379">Extension Attribute 12</span><span class="sxs-lookup"><span data-stu-id="ab973-379">Extension Attribute 12</span></span>|
|<span data-ttu-id="ab973-380">User</span><span class="sxs-lookup"><span data-stu-id="ab973-380">User</span></span>|<span data-ttu-id="ab973-381">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="ab973-381">extensionattribute13</span></span>|<span data-ttu-id="ab973-382">Extension Attribute 13</span><span class="sxs-lookup"><span data-stu-id="ab973-382">Extension Attribute 13</span></span>|
|<span data-ttu-id="ab973-383">User</span><span class="sxs-lookup"><span data-stu-id="ab973-383">User</span></span>|<span data-ttu-id="ab973-384">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="ab973-384">extensionattribute14</span></span>|<span data-ttu-id="ab973-385">Extension Attribute 14</span><span class="sxs-lookup"><span data-stu-id="ab973-385">Extension Attribute 14</span></span>|
|<span data-ttu-id="ab973-386">User</span><span class="sxs-lookup"><span data-stu-id="ab973-386">User</span></span>|<span data-ttu-id="ab973-387">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="ab973-387">extensionattribute15</span></span>|<span data-ttu-id="ab973-388">Extension Attribute 15</span><span class="sxs-lookup"><span data-stu-id="ab973-388">Extension Attribute 15</span></span>|
|<span data-ttu-id="ab973-389">User</span><span class="sxs-lookup"><span data-stu-id="ab973-389">User</span></span>|<span data-ttu-id="ab973-390">othermail</span><span class="sxs-lookup"><span data-stu-id="ab973-390">othermail</span></span>|<span data-ttu-id="ab973-391">Other Mail</span><span class="sxs-lookup"><span data-stu-id="ab973-391">Other Mail</span></span>|
|<span data-ttu-id="ab973-392">User</span><span class="sxs-lookup"><span data-stu-id="ab973-392">User</span></span>|<span data-ttu-id="ab973-393">country</span><span class="sxs-lookup"><span data-stu-id="ab973-393">country</span></span>|<span data-ttu-id="ab973-394">Country</span><span class="sxs-lookup"><span data-stu-id="ab973-394">Country</span></span>|
|<span data-ttu-id="ab973-395">User</span><span class="sxs-lookup"><span data-stu-id="ab973-395">User</span></span>|<span data-ttu-id="ab973-396">city</span><span class="sxs-lookup"><span data-stu-id="ab973-396">city</span></span>|<span data-ttu-id="ab973-397">City</span><span class="sxs-lookup"><span data-stu-id="ab973-397">City</span></span>|
|<span data-ttu-id="ab973-398">User</span><span class="sxs-lookup"><span data-stu-id="ab973-398">User</span></span>|<span data-ttu-id="ab973-399">state</span><span class="sxs-lookup"><span data-stu-id="ab973-399">state</span></span>|<span data-ttu-id="ab973-400">State</span><span class="sxs-lookup"><span data-stu-id="ab973-400">State</span></span>|
|<span data-ttu-id="ab973-401">User</span><span class="sxs-lookup"><span data-stu-id="ab973-401">User</span></span>|<span data-ttu-id="ab973-402">jobtitle</span><span class="sxs-lookup"><span data-stu-id="ab973-402">jobtitle</span></span>|<span data-ttu-id="ab973-403">Job Title</span><span class="sxs-lookup"><span data-stu-id="ab973-403">Job Title</span></span>|
|<span data-ttu-id="ab973-404">User</span><span class="sxs-lookup"><span data-stu-id="ab973-404">User</span></span>|<span data-ttu-id="ab973-405">employeeid</span><span class="sxs-lookup"><span data-stu-id="ab973-405">employeeid</span></span>|<span data-ttu-id="ab973-406">Employee ID</span><span class="sxs-lookup"><span data-stu-id="ab973-406">Employee ID</span></span>|
|<span data-ttu-id="ab973-407">User</span><span class="sxs-lookup"><span data-stu-id="ab973-407">User</span></span>|<span data-ttu-id="ab973-408">facsimiletelephonenumber</span><span class="sxs-lookup"><span data-stu-id="ab973-408">facsimiletelephonenumber</span></span>|<span data-ttu-id="ab973-409">Facsimile Telephone Number</span><span class="sxs-lookup"><span data-stu-id="ab973-409">Facsimile Telephone Number</span></span>|
|<span data-ttu-id="ab973-410">application, resource, audience</span><span class="sxs-lookup"><span data-stu-id="ab973-410">application, resource, audience</span></span>|<span data-ttu-id="ab973-411">displayname</span><span class="sxs-lookup"><span data-stu-id="ab973-411">displayname</span></span>|<span data-ttu-id="ab973-412">Display Name</span><span class="sxs-lookup"><span data-stu-id="ab973-412">Display Name</span></span>|
|<span data-ttu-id="ab973-413">application, resource, audience</span><span class="sxs-lookup"><span data-stu-id="ab973-413">application, resource, audience</span></span>|<span data-ttu-id="ab973-414">objected</span><span class="sxs-lookup"><span data-stu-id="ab973-414">objected</span></span>|<span data-ttu-id="ab973-415">ObjectID</span><span class="sxs-lookup"><span data-stu-id="ab973-415">ObjectID</span></span>|
|<span data-ttu-id="ab973-416">application, resource, audience</span><span class="sxs-lookup"><span data-stu-id="ab973-416">application, resource, audience</span></span>|<span data-ttu-id="ab973-417">tags</span><span class="sxs-lookup"><span data-stu-id="ab973-417">tags</span></span>|<span data-ttu-id="ab973-418">Service Principal Tag</span><span class="sxs-lookup"><span data-stu-id="ab973-418">Service Principal Tag</span></span>|
|<span data-ttu-id="ab973-419">Company</span><span class="sxs-lookup"><span data-stu-id="ab973-419">Company</span></span>|<span data-ttu-id="ab973-420">tenantcountry</span><span class="sxs-lookup"><span data-stu-id="ab973-420">tenantcountry</span></span>|<span data-ttu-id="ab973-421">Tenant’s country</span><span class="sxs-lookup"><span data-stu-id="ab973-421">Tenant’s country</span></span>|

<span data-ttu-id="ab973-422">**TransformationID:** The TransformationID element must be provided only if the Source element is set to “transformation”.</span><span class="sxs-lookup"><span data-stu-id="ab973-422">**TransformationID:** The TransformationID element must be provided only if the Source element is set to “transformation”.</span></span>

- <span data-ttu-id="ab973-423">This element must match the ID element of the transformation entry in the **ClaimsTransformation** property that defines how the data for this claim is generated.</span><span class="sxs-lookup"><span data-stu-id="ab973-423">This element must match the ID element of the transformation entry in the **ClaimsTransformation** property that defines how the data for this claim is generated.</span></span>

<span data-ttu-id="ab973-424">**Claim Type:** The **JwtClaimType** and **SamlClaimType** elements define which claim this claim schema entry refers to.</span><span class="sxs-lookup"><span data-stu-id="ab973-424">**Claim Type:** The **JwtClaimType** and **SamlClaimType** elements define which claim this claim schema entry refers to.</span></span>

- <span data-ttu-id="ab973-425">The JwtClaimType must contain the name of the claim to be emitted in JWTs.</span><span class="sxs-lookup"><span data-stu-id="ab973-425">The JwtClaimType must contain the name of the claim to be emitted in JWTs.</span></span>
- <span data-ttu-id="ab973-426">The SamlClaimType must contain the URI of the claim to be emitted in SAML tokens.</span><span class="sxs-lookup"><span data-stu-id="ab973-426">The SamlClaimType must contain the URI of the claim to be emitted in SAML tokens.</span></span>

>[!NOTE]
><span data-ttu-id="ab973-427">Names and URIs of claims in the restricted claim set cannot be used for the claim type elements.</span><span class="sxs-lookup"><span data-stu-id="ab973-427">Names and URIs of claims in the restricted claim set cannot be used for the claim type elements.</span></span> <span data-ttu-id="ab973-428">For more information, see the "Exceptions and restrictions" section later in this article.</span><span class="sxs-lookup"><span data-stu-id="ab973-428">For more information, see the "Exceptions and restrictions" section later in this article.</span></span>

### <a name="claims-transformation"></a><span data-ttu-id="ab973-429">Claims transformation</span><span class="sxs-lookup"><span data-stu-id="ab973-429">Claims transformation</span></span>

<span data-ttu-id="ab973-430">**String:** ClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="ab973-430">**String:** ClaimsTransformation</span></span>

<span data-ttu-id="ab973-431">**Data type:** JSON blob, with one or more transformation entries</span><span class="sxs-lookup"><span data-stu-id="ab973-431">**Data type:** JSON blob, with one or more transformation entries</span></span> 

<span data-ttu-id="ab973-432">**Summary:** Use this property to apply common transformations to source data, to generate the output data for claims specified in the Claims Schema.</span><span class="sxs-lookup"><span data-stu-id="ab973-432">**Summary:** Use this property to apply common transformations to source data, to generate the output data for claims specified in the Claims Schema.</span></span>

<span data-ttu-id="ab973-433">**ID:** Use the ID element to reference this transformation entry in the TransformationID Claims Schema entry.</span><span class="sxs-lookup"><span data-stu-id="ab973-433">**ID:** Use the ID element to reference this transformation entry in the TransformationID Claims Schema entry.</span></span> <span data-ttu-id="ab973-434">This value must be unique for each transformation entry within this policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-434">This value must be unique for each transformation entry within this policy.</span></span>

<span data-ttu-id="ab973-435">**TransformationMethod:** The TransformationMethod element identifies which operation is performed to generate the data for the claim.</span><span class="sxs-lookup"><span data-stu-id="ab973-435">**TransformationMethod:** The TransformationMethod element identifies which operation is performed to generate the data for the claim.</span></span>

<span data-ttu-id="ab973-436">Based on the method chosen, a set of inputs and outputs is expected.</span><span class="sxs-lookup"><span data-stu-id="ab973-436">Based on the method chosen, a set of inputs and outputs is expected.</span></span> <span data-ttu-id="ab973-437">These are defined by using the **InputClaims**, **InputParameters** and **OutputClaims** elements.</span><span class="sxs-lookup"><span data-stu-id="ab973-437">These are defined by using the **InputClaims**, **InputParameters** and **OutputClaims** elements.</span></span>

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a><span data-ttu-id="ab973-438">Table 4: Transformation methods and expected inputs and outputs</span><span class="sxs-lookup"><span data-stu-id="ab973-438">Table 4: Transformation methods and expected inputs and outputs</span></span>
|<span data-ttu-id="ab973-439">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="ab973-439">TransformationMethod</span></span>|<span data-ttu-id="ab973-440">Expected input</span><span class="sxs-lookup"><span data-stu-id="ab973-440">Expected input</span></span>|<span data-ttu-id="ab973-441">Expected output</span><span class="sxs-lookup"><span data-stu-id="ab973-441">Expected output</span></span>|<span data-ttu-id="ab973-442">Description</span><span class="sxs-lookup"><span data-stu-id="ab973-442">Description</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="ab973-443">Join</span><span class="sxs-lookup"><span data-stu-id="ab973-443">Join</span></span>|<span data-ttu-id="ab973-444">string1, string2, separator</span><span class="sxs-lookup"><span data-stu-id="ab973-444">string1, string2, separator</span></span>|<span data-ttu-id="ab973-445">outputClaim</span><span class="sxs-lookup"><span data-stu-id="ab973-445">outputClaim</span></span>|<span data-ttu-id="ab973-446">Joins input strings by using a separator in between.</span><span class="sxs-lookup"><span data-stu-id="ab973-446">Joins input strings by using a separator in between.</span></span> <span data-ttu-id="ab973-447">For example: string1:"foo@bar.com" , string2:"sandbox" , separator:"." results in outputClaim:"foo@bar.com.sandbox"</span><span class="sxs-lookup"><span data-stu-id="ab973-447">For example: string1:"foo@bar.com" , string2:"sandbox" , separator:"." results in outputClaim:"foo@bar.com.sandbox"</span></span>|
|<span data-ttu-id="ab973-448">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="ab973-448">ExtractMailPrefix</span></span>|<span data-ttu-id="ab973-449">mail</span><span class="sxs-lookup"><span data-stu-id="ab973-449">mail</span></span>|<span data-ttu-id="ab973-450">outputClaim</span><span class="sxs-lookup"><span data-stu-id="ab973-450">outputClaim</span></span>|<span data-ttu-id="ab973-451">Extracts the local part of an email address.</span><span class="sxs-lookup"><span data-stu-id="ab973-451">Extracts the local part of an email address.</span></span> <span data-ttu-id="ab973-452">For example: mail:"foo@bar.com" results in outputClaim:"foo".</span><span class="sxs-lookup"><span data-stu-id="ab973-452">For example: mail:"foo@bar.com" results in outputClaim:"foo".</span></span> <span data-ttu-id="ab973-453">If no \@ sign is present, then the orignal input string is returned as is.</span><span class="sxs-lookup"><span data-stu-id="ab973-453">If no \@ sign is present, then the orignal input string is returned as is.</span></span>|

<span data-ttu-id="ab973-454">**InputClaims:** Use an InputClaims element to pass the data from a claim schema entry to a transformation.</span><span class="sxs-lookup"><span data-stu-id="ab973-454">**InputClaims:** Use an InputClaims element to pass the data from a claim schema entry to a transformation.</span></span> <span data-ttu-id="ab973-455">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span><span class="sxs-lookup"><span data-stu-id="ab973-455">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="ab973-456">**ClaimTypeReferenceId** is joined with ID element of the claim schema entry to find the appropriate input claim.</span><span class="sxs-lookup"><span data-stu-id="ab973-456">**ClaimTypeReferenceId** is joined with ID element of the claim schema entry to find the appropriate input claim.</span></span> 
- <span data-ttu-id="ab973-457">**TransformationClaimType** is used to give a unique name to this input.</span><span class="sxs-lookup"><span data-stu-id="ab973-457">**TransformationClaimType** is used to give a unique name to this input.</span></span> <span data-ttu-id="ab973-458">This name must match one of the expected inputs for the transformation method.</span><span class="sxs-lookup"><span data-stu-id="ab973-458">This name must match one of the expected inputs for the transformation method.</span></span>

<span data-ttu-id="ab973-459">**InputParameters:** Use an InputParameters element to pass a constant value to a transformation.</span><span class="sxs-lookup"><span data-stu-id="ab973-459">**InputParameters:** Use an InputParameters element to pass a constant value to a transformation.</span></span> <span data-ttu-id="ab973-460">It has two attributes: **Value** and **ID**.</span><span class="sxs-lookup"><span data-stu-id="ab973-460">It has two attributes: **Value** and **ID**.</span></span>

- <span data-ttu-id="ab973-461">**Value** is the actual constant value to be passed.</span><span class="sxs-lookup"><span data-stu-id="ab973-461">**Value** is the actual constant value to be passed.</span></span>
- <span data-ttu-id="ab973-462">**ID** is used to give a unique name to this input.</span><span class="sxs-lookup"><span data-stu-id="ab973-462">**ID** is used to give a unique name to this input.</span></span> <span data-ttu-id="ab973-463">This name must match one of the expected inputs for the transformation method.</span><span class="sxs-lookup"><span data-stu-id="ab973-463">This name must match one of the expected inputs for the transformation method.</span></span>

<span data-ttu-id="ab973-464">**OutputClaims:** Use an OutputClaims element to hold the data generated by a transformation, and tie it to a claim schema entry.</span><span class="sxs-lookup"><span data-stu-id="ab973-464">**OutputClaims:** Use an OutputClaims element to hold the data generated by a transformation, and tie it to a claim schema entry.</span></span> <span data-ttu-id="ab973-465">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span><span class="sxs-lookup"><span data-stu-id="ab973-465">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="ab973-466">**ClaimTypeReferenceId** is joined with the ID of the claim schema entry to find the appropriate output claim.</span><span class="sxs-lookup"><span data-stu-id="ab973-466">**ClaimTypeReferenceId** is joined with the ID of the claim schema entry to find the appropriate output claim.</span></span>
- <span data-ttu-id="ab973-467">**TransformationClaimType** is used to give a unique name to this output.</span><span class="sxs-lookup"><span data-stu-id="ab973-467">**TransformationClaimType** is used to give a unique name to this output.</span></span> <span data-ttu-id="ab973-468">This name must match one of the expected outputs for the transformation method.</span><span class="sxs-lookup"><span data-stu-id="ab973-468">This name must match one of the expected outputs for the transformation method.</span></span>

### <a name="exceptions-and-restrictions"></a><span data-ttu-id="ab973-469">Exceptions and restrictions</span><span class="sxs-lookup"><span data-stu-id="ab973-469">Exceptions and restrictions</span></span>

<span data-ttu-id="ab973-470">**SAML NameID and UPN:** The attributes from which you source the NameID and UPN values, and the claims transformations that are permitted, are limited.</span><span class="sxs-lookup"><span data-stu-id="ab973-470">**SAML NameID and UPN:** The attributes from which you source the NameID and UPN values, and the claims transformations that are permitted, are limited.</span></span>

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a><span data-ttu-id="ab973-471">Table 5: Attributes allowed as a data source for SAML NameID</span><span class="sxs-lookup"><span data-stu-id="ab973-471">Table 5: Attributes allowed as a data source for SAML NameID</span></span>
|<span data-ttu-id="ab973-472">Source</span><span class="sxs-lookup"><span data-stu-id="ab973-472">Source</span></span>|<span data-ttu-id="ab973-473">ID</span><span class="sxs-lookup"><span data-stu-id="ab973-473">ID</span></span>|<span data-ttu-id="ab973-474">Description</span><span class="sxs-lookup"><span data-stu-id="ab973-474">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="ab973-475">User</span><span class="sxs-lookup"><span data-stu-id="ab973-475">User</span></span>|<span data-ttu-id="ab973-476">mail</span><span class="sxs-lookup"><span data-stu-id="ab973-476">mail</span></span>|<span data-ttu-id="ab973-477">Email Address</span><span class="sxs-lookup"><span data-stu-id="ab973-477">Email Address</span></span>|
|<span data-ttu-id="ab973-478">User</span><span class="sxs-lookup"><span data-stu-id="ab973-478">User</span></span>|<span data-ttu-id="ab973-479">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ab973-479">userprincipalname</span></span>|<span data-ttu-id="ab973-480">User Principal Name</span><span class="sxs-lookup"><span data-stu-id="ab973-480">User Principal Name</span></span>|
|<span data-ttu-id="ab973-481">User</span><span class="sxs-lookup"><span data-stu-id="ab973-481">User</span></span>|<span data-ttu-id="ab973-482">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="ab973-482">onpremisessamaccountname</span></span>|<span data-ttu-id="ab973-483">On Premises Sam Account Name</span><span class="sxs-lookup"><span data-stu-id="ab973-483">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="ab973-484">User</span><span class="sxs-lookup"><span data-stu-id="ab973-484">User</span></span>|<span data-ttu-id="ab973-485">employeeid</span><span class="sxs-lookup"><span data-stu-id="ab973-485">employeeid</span></span>|<span data-ttu-id="ab973-486">Employee ID</span><span class="sxs-lookup"><span data-stu-id="ab973-486">Employee ID</span></span>|
|<span data-ttu-id="ab973-487">User</span><span class="sxs-lookup"><span data-stu-id="ab973-487">User</span></span>|<span data-ttu-id="ab973-488">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="ab973-488">extensionattribute1</span></span>|<span data-ttu-id="ab973-489">Extension Attribute 1</span><span class="sxs-lookup"><span data-stu-id="ab973-489">Extension Attribute 1</span></span>|
|<span data-ttu-id="ab973-490">User</span><span class="sxs-lookup"><span data-stu-id="ab973-490">User</span></span>|<span data-ttu-id="ab973-491">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="ab973-491">extensionattribute2</span></span>|<span data-ttu-id="ab973-492">Extension Attribute 2</span><span class="sxs-lookup"><span data-stu-id="ab973-492">Extension Attribute 2</span></span>|
|<span data-ttu-id="ab973-493">User</span><span class="sxs-lookup"><span data-stu-id="ab973-493">User</span></span>|<span data-ttu-id="ab973-494">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="ab973-494">extensionattribute3</span></span>|<span data-ttu-id="ab973-495">Extension Attribute 3</span><span class="sxs-lookup"><span data-stu-id="ab973-495">Extension Attribute 3</span></span>|
|<span data-ttu-id="ab973-496">User</span><span class="sxs-lookup"><span data-stu-id="ab973-496">User</span></span>|<span data-ttu-id="ab973-497">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="ab973-497">extensionattribute4</span></span>|<span data-ttu-id="ab973-498">Extension Attribute 4</span><span class="sxs-lookup"><span data-stu-id="ab973-498">Extension Attribute 4</span></span>|
|<span data-ttu-id="ab973-499">User</span><span class="sxs-lookup"><span data-stu-id="ab973-499">User</span></span>|<span data-ttu-id="ab973-500">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="ab973-500">extensionattribute5</span></span>|<span data-ttu-id="ab973-501">Extension Attribute 5</span><span class="sxs-lookup"><span data-stu-id="ab973-501">Extension Attribute 5</span></span>|
|<span data-ttu-id="ab973-502">User</span><span class="sxs-lookup"><span data-stu-id="ab973-502">User</span></span>|<span data-ttu-id="ab973-503">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="ab973-503">extensionattribute6</span></span>|<span data-ttu-id="ab973-504">Extension Attribute 6</span><span class="sxs-lookup"><span data-stu-id="ab973-504">Extension Attribute 6</span></span>|
|<span data-ttu-id="ab973-505">User</span><span class="sxs-lookup"><span data-stu-id="ab973-505">User</span></span>|<span data-ttu-id="ab973-506">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="ab973-506">extensionattribute7</span></span>|<span data-ttu-id="ab973-507">Extension Attribute 7</span><span class="sxs-lookup"><span data-stu-id="ab973-507">Extension Attribute 7</span></span>|
|<span data-ttu-id="ab973-508">User</span><span class="sxs-lookup"><span data-stu-id="ab973-508">User</span></span>|<span data-ttu-id="ab973-509">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="ab973-509">extensionattribute8</span></span>|<span data-ttu-id="ab973-510">Extension Attribute 8</span><span class="sxs-lookup"><span data-stu-id="ab973-510">Extension Attribute 8</span></span>|
|<span data-ttu-id="ab973-511">User</span><span class="sxs-lookup"><span data-stu-id="ab973-511">User</span></span>|<span data-ttu-id="ab973-512">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="ab973-512">extensionattribute9</span></span>|<span data-ttu-id="ab973-513">Extension Attribute 9</span><span class="sxs-lookup"><span data-stu-id="ab973-513">Extension Attribute 9</span></span>|
|<span data-ttu-id="ab973-514">User</span><span class="sxs-lookup"><span data-stu-id="ab973-514">User</span></span>|<span data-ttu-id="ab973-515">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="ab973-515">extensionattribute10</span></span>|<span data-ttu-id="ab973-516">Extension Attribute 10</span><span class="sxs-lookup"><span data-stu-id="ab973-516">Extension Attribute 10</span></span>|
|<span data-ttu-id="ab973-517">User</span><span class="sxs-lookup"><span data-stu-id="ab973-517">User</span></span>|<span data-ttu-id="ab973-518">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="ab973-518">extensionattribute11</span></span>|<span data-ttu-id="ab973-519">Extension Attribute 11</span><span class="sxs-lookup"><span data-stu-id="ab973-519">Extension Attribute 11</span></span>|
|<span data-ttu-id="ab973-520">User</span><span class="sxs-lookup"><span data-stu-id="ab973-520">User</span></span>|<span data-ttu-id="ab973-521">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="ab973-521">extensionattribute12</span></span>|<span data-ttu-id="ab973-522">Extension Attribute 12</span><span class="sxs-lookup"><span data-stu-id="ab973-522">Extension Attribute 12</span></span>|
|<span data-ttu-id="ab973-523">User</span><span class="sxs-lookup"><span data-stu-id="ab973-523">User</span></span>|<span data-ttu-id="ab973-524">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="ab973-524">extensionattribute13</span></span>|<span data-ttu-id="ab973-525">Extension Attribute 13</span><span class="sxs-lookup"><span data-stu-id="ab973-525">Extension Attribute 13</span></span>|
|<span data-ttu-id="ab973-526">User</span><span class="sxs-lookup"><span data-stu-id="ab973-526">User</span></span>|<span data-ttu-id="ab973-527">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="ab973-527">extensionattribute14</span></span>|<span data-ttu-id="ab973-528">Extension Attribute 14</span><span class="sxs-lookup"><span data-stu-id="ab973-528">Extension Attribute 14</span></span>|
|<span data-ttu-id="ab973-529">User</span><span class="sxs-lookup"><span data-stu-id="ab973-529">User</span></span>|<span data-ttu-id="ab973-530">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="ab973-530">extensionattribute15</span></span>|<span data-ttu-id="ab973-531">Extension Attribute 15</span><span class="sxs-lookup"><span data-stu-id="ab973-531">Extension Attribute 15</span></span>|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a><span data-ttu-id="ab973-532">Table 6: Transformation methods allowed for SAML NameID</span><span class="sxs-lookup"><span data-stu-id="ab973-532">Table 6: Transformation methods allowed for SAML NameID</span></span>
|<span data-ttu-id="ab973-533">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="ab973-533">TransformationMethod</span></span>|<span data-ttu-id="ab973-534">Restrictions</span><span class="sxs-lookup"><span data-stu-id="ab973-534">Restrictions</span></span>|
| ----- | ----- |
|<span data-ttu-id="ab973-535">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="ab973-535">ExtractMailPrefix</span></span>|<span data-ttu-id="ab973-536">None</span><span class="sxs-lookup"><span data-stu-id="ab973-536">None</span></span>|
|<span data-ttu-id="ab973-537">Join</span><span class="sxs-lookup"><span data-stu-id="ab973-537">Join</span></span>|<span data-ttu-id="ab973-538">The suffix being joined must be a verified domain of the resource tenant.</span><span class="sxs-lookup"><span data-stu-id="ab973-538">The suffix being joined must be a verified domain of the resource tenant.</span></span>|

### <a name="custom-signing-key"></a><span data-ttu-id="ab973-539">Custom signing key</span><span class="sxs-lookup"><span data-stu-id="ab973-539">Custom signing key</span></span>
<span data-ttu-id="ab973-540">A custom signing key must be assigned to the service principal object for a claims mapping policy to take effect.</span><span class="sxs-lookup"><span data-stu-id="ab973-540">A custom signing key must be assigned to the service principal object for a claims mapping policy to take effect.</span></span> <span data-ttu-id="ab973-541">All tokens issued that have been impacted by the policy are signed with this key.</span><span class="sxs-lookup"><span data-stu-id="ab973-541">All tokens issued that have been impacted by the policy are signed with this key.</span></span> <span data-ttu-id="ab973-542">Applications must be configured to accept tokens signed with this key.</span><span class="sxs-lookup"><span data-stu-id="ab973-542">Applications must be configured to accept tokens signed with this key.</span></span> <span data-ttu-id="ab973-543">This ensures acknowledgment that tokens have been modified by the creator of the claims mapping policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-543">This ensures acknowledgment that tokens have been modified by the creator of the claims mapping policy.</span></span> <span data-ttu-id="ab973-544">This protects applications from claims mapping policies created by malicious actors.</span><span class="sxs-lookup"><span data-stu-id="ab973-544">This protects applications from claims mapping policies created by malicious actors.</span></span>

### <a name="cross-tenant-scenarios"></a><span data-ttu-id="ab973-545">Cross-tenant scenarios</span><span class="sxs-lookup"><span data-stu-id="ab973-545">Cross-tenant scenarios</span></span>
<span data-ttu-id="ab973-546">Claims mapping policies do not apply to guest users.</span><span class="sxs-lookup"><span data-stu-id="ab973-546">Claims mapping policies do not apply to guest users.</span></span> <span data-ttu-id="ab973-547">If a guest user attempts to access an application with a claims mapping policy assigned to its service principal, the default token is issued (the policy has no effect).</span><span class="sxs-lookup"><span data-stu-id="ab973-547">If a guest user attempts to access an application with a claims mapping policy assigned to its service principal, the default token is issued (the policy has no effect).</span></span>

## <a name="claims-mapping-policy-assignment"></a><span data-ttu-id="ab973-548">Claims mapping policy assignment</span><span class="sxs-lookup"><span data-stu-id="ab973-548">Claims mapping policy assignment</span></span>
<span data-ttu-id="ab973-549">Claims mapping policies can only be assigned to service principal objects.</span><span class="sxs-lookup"><span data-stu-id="ab973-549">Claims mapping policies can only be assigned to service principal objects.</span></span>

### <a name="example-claims-mapping-policies"></a><span data-ttu-id="ab973-550">Example claims mapping policies</span><span class="sxs-lookup"><span data-stu-id="ab973-550">Example claims mapping policies</span></span>

<span data-ttu-id="ab973-551">In Azure AD, many scenarios are possible when you can customize claims emitted in tokens for specific service principals.</span><span class="sxs-lookup"><span data-stu-id="ab973-551">In Azure AD, many scenarios are possible when you can customize claims emitted in tokens for specific service principals.</span></span> <span data-ttu-id="ab973-552">In this section, we walk through a few common scenarios that can help you grasp how to use the claims mapping policy type.</span><span class="sxs-lookup"><span data-stu-id="ab973-552">In this section, we walk through a few common scenarios that can help you grasp how to use the claims mapping policy type.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="ab973-553">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ab973-553">Prerequisites</span></span>
<span data-ttu-id="ab973-554">In the following examples, you create, update, link, and delete policies for service principals.</span><span class="sxs-lookup"><span data-stu-id="ab973-554">In the following examples, you create, update, link, and delete policies for service principals.</span></span> <span data-ttu-id="ab973-555">If you are new to Azure AD, we recommend that you learn about how to get an Azure AD tenant before you proceed with these examples.</span><span class="sxs-lookup"><span data-stu-id="ab973-555">If you are new to Azure AD, we recommend that you learn about how to get an Azure AD tenant before you proceed with these examples.</span></span> 

<span data-ttu-id="ab973-556">To get started, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="ab973-556">To get started, do the following steps:</span></span>


1. <span data-ttu-id="ab973-557">Download the latest [Azure AD PowerShell Module public preview release](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).</span><span class="sxs-lookup"><span data-stu-id="ab973-557">Download the latest [Azure AD PowerShell Module public preview release](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).</span></span>
2.  <span data-ttu-id="ab973-558">Run the Connect command to sign in to your Azure AD admin account.</span><span class="sxs-lookup"><span data-stu-id="ab973-558">Run the Connect command to sign in to your Azure AD admin account.</span></span> <span data-ttu-id="ab973-559">Run this command each time you start a new session.</span><span class="sxs-lookup"><span data-stu-id="ab973-559">Run this command each time you start a new session.</span></span>
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  <span data-ttu-id="ab973-560">To see all policies that have been created in your organization, run the following command.</span><span class="sxs-lookup"><span data-stu-id="ab973-560">To see all policies that have been created in your organization, run the following command.</span></span> <span data-ttu-id="ab973-561">We recommend that you run this command after most operations in the following scenarios, to check that your policies are being created as expected.</span><span class="sxs-lookup"><span data-stu-id="ab973-561">We recommend that you run this command after most operations in the following scenarios, to check that your policies are being created as expected.</span></span>
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-to-omit-the-basic-claims-from-tokens-issued-to-a-service-principal"></a><span data-ttu-id="ab973-562">Example: Create and assign a policy to omit the basic claims from tokens issued to a service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-562">Example: Create and assign a policy to omit the basic claims from tokens issued to a service principal.</span></span>
<span data-ttu-id="ab973-563">In this example, you create a policy that removes the basic claim set from tokens issued to linked service principals.</span><span class="sxs-lookup"><span data-stu-id="ab973-563">In this example, you create a policy that removes the basic claim set from tokens issued to linked service principals.</span></span>


1. <span data-ttu-id="ab973-564">Create a claims mapping policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-564">Create a claims mapping policy.</span></span> <span data-ttu-id="ab973-565">This policy, linked to specific service principals, removes the basic claim set from tokens.</span><span class="sxs-lookup"><span data-stu-id="ab973-565">This policy, linked to specific service principals, removes the basic claim set from tokens.</span></span>
    1. <span data-ttu-id="ab973-566">To create the policy, run this command:</span><span class="sxs-lookup"><span data-stu-id="ab973-566">To create the policy, run this command:</span></span> 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. <span data-ttu-id="ab973-567">To see your new policy, and to get the policy ObjectId, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ab973-567">To see your new policy, and to get the policy ObjectId, run the following command:</span></span>
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="ab973-568">Assign the policy to your service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-568">Assign the policy to your service principal.</span></span> <span data-ttu-id="ab973-569">You also need to get the ObjectId of your service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-569">You also need to get the ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="ab973-570">To see all your organization's service principals, you can query Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ab973-570">To see all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="ab973-571">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="ab973-571">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span></span>
    2.  <span data-ttu-id="ab973-572">When you have the ObjectId of your service principal, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ab973-572">When you have the ObjectId of your service principal, run the following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
#### <a name="example-create-and-assign-a-policy-to-include-the-employeeid-and-tenantcountry-as-claims-in-tokens-issued-to-a-service-principal"></a><span data-ttu-id="ab973-573">Example: Create and assign a policy to include the EmployeeID and TenantCountry as claims in tokens issued to a service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-573">Example: Create and assign a policy to include the EmployeeID and TenantCountry as claims in tokens issued to a service principal.</span></span>
<span data-ttu-id="ab973-574">In this example, you create a policy that adds the EmployeeID and TenantCountry to tokens issued to linked service principals.</span><span class="sxs-lookup"><span data-stu-id="ab973-574">In this example, you create a policy that adds the EmployeeID and TenantCountry to tokens issued to linked service principals.</span></span> <span data-ttu-id="ab973-575">The EmployeeID is emitted as the name claim type in both SAML tokens and JWTs.</span><span class="sxs-lookup"><span data-stu-id="ab973-575">The EmployeeID is emitted as the name claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="ab973-576">The TenantCountry is emitted as the country claim type in both SAML tokens and JWTs.</span><span class="sxs-lookup"><span data-stu-id="ab973-576">The TenantCountry is emitted as the country claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="ab973-577">In this example, we continue to include the basic claims set in the tokens.</span><span class="sxs-lookup"><span data-stu-id="ab973-577">In this example, we continue to include the basic claims set in the tokens.</span></span>

1. <span data-ttu-id="ab973-578">Create a claims mapping policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-578">Create a claims mapping policy.</span></span> <span data-ttu-id="ab973-579">This policy, linked to specific service principals, adds the EmployeeID and TenantCountry claims to tokens.</span><span class="sxs-lookup"><span data-stu-id="ab973-579">This policy, linked to specific service principals, adds the EmployeeID and TenantCountry claims to tokens.</span></span>
    1. <span data-ttu-id="ab973-580">To create the policy, run this command:</span><span class="sxs-lookup"><span data-stu-id="ab973-580">To create the policy, run this command:</span></span>  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":"tenantcountry","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample" -Type "ClaimsMappingPolicy"
    ```
    
    2. <span data-ttu-id="ab973-581">To see your new policy, and to get the policy ObjectId, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ab973-581">To see your new policy, and to get the policy ObjectId, run the following command:</span></span>
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="ab973-582">Assign the policy to your service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-582">Assign the policy to your service principal.</span></span> <span data-ttu-id="ab973-583">You also need to get the ObjectId of your service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-583">You also need to get the ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="ab973-584">To see all your organization's service principals, you can query Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ab973-584">To see all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="ab973-585">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="ab973-585">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span></span>
    2.  <span data-ttu-id="ab973-586">When you have the ObjectId of your service principal, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ab973-586">When you have the ObjectId of your service principal, run the following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-to-a-service-principal"></a><span data-ttu-id="ab973-587">Example: Create and assign a policy that uses a claims transformation in tokens issued to a service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-587">Example: Create and assign a policy that uses a claims transformation in tokens issued to a service principal.</span></span>
<span data-ttu-id="ab973-588">In this example, you create a policy that emits a custom claim “JoinedData” to JWTs issued to linked service principals.</span><span class="sxs-lookup"><span data-stu-id="ab973-588">In this example, you create a policy that emits a custom claim “JoinedData” to JWTs issued to linked service principals.</span></span> <span data-ttu-id="ab973-589">This claim contains a value created by joining the data stored in the extensionattribute1 attribute on the user object with “.sandbox”.</span><span class="sxs-lookup"><span data-stu-id="ab973-589">This claim contains a value created by joining the data stored in the extensionattribute1 attribute on the user object with “.sandbox”.</span></span> <span data-ttu-id="ab973-590">In this example, we exclude the basic claims set in the tokens.</span><span class="sxs-lookup"><span data-stu-id="ab973-590">In this example, we exclude the basic claims set in the tokens.</span></span>


1. <span data-ttu-id="ab973-591">Create a claims mapping policy.</span><span class="sxs-lookup"><span data-stu-id="ab973-591">Create a claims mapping policy.</span></span> <span data-ttu-id="ab973-592">This policy, linked to specific service principals, adds the EmployeeID and TenantCountry claims to tokens.</span><span class="sxs-lookup"><span data-stu-id="ab973-592">This policy, linked to specific service principals, adds the EmployeeID and TenantCountry claims to tokens.</span></span>
    1. <span data-ttu-id="ab973-593">To create the policy, run this command:</span><span class="sxs-lookup"><span data-stu-id="ab973-593">To create the policy, run this command:</span></span> 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformations":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"ID":"string2","Value":"sandbox"},{"ID":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample" -Type "ClaimsMappingPolicy" 
    ```
    
    2. <span data-ttu-id="ab973-594">To see your new policy, and to get the policy ObjectId, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ab973-594">To see your new policy, and to get the policy ObjectId, run the following command:</span></span> 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="ab973-595">Assign the policy to your service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-595">Assign the policy to your service principal.</span></span> <span data-ttu-id="ab973-596">You also need to get the ObjectId of your service principal.</span><span class="sxs-lookup"><span data-stu-id="ab973-596">You also need to get the ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="ab973-597">To see all your organization's service principals, you can query Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ab973-597">To see all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="ab973-598">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="ab973-598">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span></span>
    2.  <span data-ttu-id="ab973-599">When you have the ObjectId of your service principal, run the following command:</span><span class="sxs-lookup"><span data-stu-id="ab973-599">When you have the ObjectId of your service principal, run the following command:</span></span> 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
