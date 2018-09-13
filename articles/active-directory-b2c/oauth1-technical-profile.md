---
title: Define a OAuth1 technical profile in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define a OAuth1 technical profile in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 10c90b060c184bb911ac149640e8a9570b59e2fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856294"
---
# <a name="define-a-oauth1-technical-profile-in-an-azure-active-directory-b2c-custom-policy"></a><span data-ttu-id="0df10-103">Define a OAuth1 technical profile in an Azure Active Directory B2C custom policy</span><span class="sxs-lookup"><span data-stu-id="0df10-103">Define a OAuth1 technical profile in an Azure Active Directory B2C custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="0df10-104">Azure Active Directory (Azure AD) B2C provides support for the [OAuth 1.0 protocol](http://tools.ietf.org/html/rfc5849) identity provider.</span><span class="sxs-lookup"><span data-stu-id="0df10-104">Azure Active Directory (Azure AD) B2C provides support for the [OAuth 1.0 protocol](http://tools.ietf.org/html/rfc5849) identity provider.</span></span> <span data-ttu-id="0df10-105">This article describes the specifics of a technical profile for interacting with a claims provider that supports this standardized protocol.</span><span class="sxs-lookup"><span data-stu-id="0df10-105">This article describes the specifics of a technical profile for interacting with a claims provider that supports this standardized protocol.</span></span> <span data-ttu-id="0df10-106">With OAuth1 technical profile you can federate with an OAuth1 based identity provider, such as Twitter, allowing you users to sign-in with their existing social or enterprise identities.</span><span class="sxs-lookup"><span data-stu-id="0df10-106">With OAuth1 technical profile you can federate with an OAuth1 based identity provider, such as Twitter, allowing you users to sign-in with their existing social or enterprise identities.</span></span>

## <a name="protocol"></a><span data-ttu-id="0df10-107">Protocol</span><span class="sxs-lookup"><span data-stu-id="0df10-107">Protocol</span></span>

<span data-ttu-id="0df10-108">The **Name** attribute of the **Protocol** element needs to be set to `OAuth1`.</span><span class="sxs-lookup"><span data-stu-id="0df10-108">The **Name** attribute of the **Protocol** element needs to be set to `OAuth1`.</span></span> <span data-ttu-id="0df10-109">For example, the protocol for the **Twitter-OAUTH1** technical profile is `OAuth1`.</span><span class="sxs-lookup"><span data-stu-id="0df10-109">For example, the protocol for the **Twitter-OAUTH1** technical profile is `OAuth1`.</span></span>

```XML
<TechnicalProfile Id="Twitter-OAUTH1">
  <DisplayName>Twitter</DisplayName>
  <Protocol Name="OAuth1" />
  ...    
```

## <a name="input-claims"></a><span data-ttu-id="0df10-110">Input claims</span><span class="sxs-lookup"><span data-stu-id="0df10-110">Input claims</span></span>

<span data-ttu-id="0df10-111">The **InputClaims** and **InputClaimsTransformations**  elements are empty or absent.</span><span class="sxs-lookup"><span data-stu-id="0df10-111">The **InputClaims** and **InputClaimsTransformations**  elements are empty or absent.</span></span>

## <a name="output-claims"></a><span data-ttu-id="0df10-112">Output claims</span><span class="sxs-lookup"><span data-stu-id="0df10-112">Output claims</span></span>

<span data-ttu-id="0df10-113">The **OutputClaims** element contains a list of claims returned by the OAuth1 identity provider.</span><span class="sxs-lookup"><span data-stu-id="0df10-113">The **OutputClaims** element contains a list of claims returned by the OAuth1 identity provider.</span></span> <span data-ttu-id="0df10-114">You may need to map the name of the claim defined in your policy to the name defined in the identity provider.</span><span class="sxs-lookup"><span data-stu-id="0df10-114">You may need to map the name of the claim defined in your policy to the name defined in the identity provider.</span></span> <span data-ttu-id="0df10-115">You can also include claims that aren't returned by the identity provider as long as you set the **DefaultValue** attribute.</span><span class="sxs-lookup"><span data-stu-id="0df10-115">You can also include claims that aren't returned by the identity provider as long as you set the **DefaultValue** attribute.</span></span>

<span data-ttu-id="0df10-116">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span><span class="sxs-lookup"><span data-stu-id="0df10-116">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span></span>

<span data-ttu-id="0df10-117">The following example shows the claims returned by the Twitter identity provider:</span><span class="sxs-lookup"><span data-stu-id="0df10-117">The following example shows the claims returned by the Twitter identity provider:</span></span>

- <span data-ttu-id="0df10-118">The **user_id** claim that is mapped to the **socialIdpUserId** claim.</span><span class="sxs-lookup"><span data-stu-id="0df10-118">The **user_id** claim that is mapped to the **socialIdpUserId** claim.</span></span>
- <span data-ttu-id="0df10-119">The **screen_name** claim that is mapped to the **displayName** claim.</span><span class="sxs-lookup"><span data-stu-id="0df10-119">The **screen_name** claim that is mapped to the **displayName** claim.</span></span>
- <span data-ttu-id="0df10-120">The **email** claim without name mapping.</span><span class="sxs-lookup"><span data-stu-id="0df10-120">The **email** claim without name mapping.</span></span>

<span data-ttu-id="0df10-121">The technical profile also returns claims that aren't returned by the identity provider:</span><span class="sxs-lookup"><span data-stu-id="0df10-121">The technical profile also returns claims that aren't returned by the identity provider:</span></span> 

- <span data-ttu-id="0df10-122">The **identityProvider** claim that contains the name of the identity provider.</span><span class="sxs-lookup"><span data-stu-id="0df10-122">The **identityProvider** claim that contains the name of the identity provider.</span></span>
- <span data-ttu-id="0df10-123">The **authenticationSource** claim with a default value of `socialIdpAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="0df10-123">The **authenticationSource** claim with a default value of `socialIdpAuthentication`.</span></span>

```xml
<OutputClaims>
  <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="user_id" />
  <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="screen_name" />
  <OutputClaim ClaimTypeReferenceId="email" />
  <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="twitter.com" />
  <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
</OutputClaims>
```

## <a name="metadata"></a><span data-ttu-id="0df10-124">Metadata</span><span class="sxs-lookup"><span data-stu-id="0df10-124">Metadata</span></span>

| <span data-ttu-id="0df10-125">Attribute</span><span class="sxs-lookup"><span data-stu-id="0df10-125">Attribute</span></span> | <span data-ttu-id="0df10-126">Required</span><span class="sxs-lookup"><span data-stu-id="0df10-126">Required</span></span> | <span data-ttu-id="0df10-127">Description</span><span class="sxs-lookup"><span data-stu-id="0df10-127">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="0df10-128">client_id</span><span class="sxs-lookup"><span data-stu-id="0df10-128">client_id</span></span> | <span data-ttu-id="0df10-129">Yes</span><span class="sxs-lookup"><span data-stu-id="0df10-129">Yes</span></span> | <span data-ttu-id="0df10-130">The application identifier of the identity provider.</span><span class="sxs-lookup"><span data-stu-id="0df10-130">The application identifier of the identity provider.</span></span> |
| <span data-ttu-id="0df10-131">ProviderName</span><span class="sxs-lookup"><span data-stu-id="0df10-131">ProviderName</span></span> | <span data-ttu-id="0df10-132">No</span><span class="sxs-lookup"><span data-stu-id="0df10-132">No</span></span> | <span data-ttu-id="0df10-133">The name of the identity provider.</span><span class="sxs-lookup"><span data-stu-id="0df10-133">The name of the identity provider.</span></span> |
| <span data-ttu-id="0df10-134">request_token_endpoint</span><span class="sxs-lookup"><span data-stu-id="0df10-134">request_token_endpoint</span></span> | <span data-ttu-id="0df10-135">Yes</span><span class="sxs-lookup"><span data-stu-id="0df10-135">Yes</span></span> | <span data-ttu-id="0df10-136">The URL of the request token endpoint as per RFC 5849.</span><span class="sxs-lookup"><span data-stu-id="0df10-136">The URL of the request token endpoint as per RFC 5849.</span></span> |
| <span data-ttu-id="0df10-137">authorization_endpoint</span><span class="sxs-lookup"><span data-stu-id="0df10-137">authorization_endpoint</span></span> | <span data-ttu-id="0df10-138">Yes</span><span class="sxs-lookup"><span data-stu-id="0df10-138">Yes</span></span> | <span data-ttu-id="0df10-139">The URL of the authorization endpoint as per RFC 5849.</span><span class="sxs-lookup"><span data-stu-id="0df10-139">The URL of the authorization endpoint as per RFC 5849.</span></span> |
| <span data-ttu-id="0df10-140">access_token_endpoint</span><span class="sxs-lookup"><span data-stu-id="0df10-140">access_token_endpoint</span></span> | <span data-ttu-id="0df10-141">Yes</span><span class="sxs-lookup"><span data-stu-id="0df10-141">Yes</span></span> | <span data-ttu-id="0df10-142">The URL of the token endpoint as per RFC 5849.</span><span class="sxs-lookup"><span data-stu-id="0df10-142">The URL of the token endpoint as per RFC 5849.</span></span> |
| <span data-ttu-id="0df10-143">ClaimsEndpoint</span><span class="sxs-lookup"><span data-stu-id="0df10-143">ClaimsEndpoint</span></span> | <span data-ttu-id="0df10-144">No</span><span class="sxs-lookup"><span data-stu-id="0df10-144">No</span></span> | <span data-ttu-id="0df10-145">The URL of the user information endpoint.</span><span class="sxs-lookup"><span data-stu-id="0df10-145">The URL of the user information endpoint.</span></span> | 
| <span data-ttu-id="0df10-146">ClaimsResponseFormat</span><span class="sxs-lookup"><span data-stu-id="0df10-146">ClaimsResponseFormat</span></span> | <span data-ttu-id="0df10-147">No</span><span class="sxs-lookup"><span data-stu-id="0df10-147">No</span></span> | <span data-ttu-id="0df10-148">The claims response format.</span><span class="sxs-lookup"><span data-stu-id="0df10-148">The claims response format.</span></span>|

## <a name="cryptographic-keys"></a><span data-ttu-id="0df10-149">Cryptographic keys</span><span class="sxs-lookup"><span data-stu-id="0df10-149">Cryptographic keys</span></span>

<span data-ttu-id="0df10-150">The **CryptographicKeys** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="0df10-150">The **CryptographicKeys** element contains the following attribute:</span></span>

| <span data-ttu-id="0df10-151">Attribute</span><span class="sxs-lookup"><span data-stu-id="0df10-151">Attribute</span></span> | <span data-ttu-id="0df10-152">Required</span><span class="sxs-lookup"><span data-stu-id="0df10-152">Required</span></span> | <span data-ttu-id="0df10-153">Description</span><span class="sxs-lookup"><span data-stu-id="0df10-153">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="0df10-154">client_secret</span><span class="sxs-lookup"><span data-stu-id="0df10-154">client_secret</span></span> | <span data-ttu-id="0df10-155">Yes</span><span class="sxs-lookup"><span data-stu-id="0df10-155">Yes</span></span> | <span data-ttu-id="0df10-156">The client secret of the identity provider application.</span><span class="sxs-lookup"><span data-stu-id="0df10-156">The client secret of the identity provider application.</span></span>   | 

## <a name="redirect-uri"></a><span data-ttu-id="0df10-157">Redirect URI</span><span class="sxs-lookup"><span data-stu-id="0df10-157">Redirect URI</span></span>

<span data-ttu-id="0df10-158">When you configure the redirect URL of your identity provider, enter `https://login.microsoftonline.com/te/tenant/policyId/oauth1/authresp`.</span><span class="sxs-lookup"><span data-stu-id="0df10-158">When you configure the redirect URL of your identity provider, enter `https://login.microsoftonline.com/te/tenant/policyId/oauth1/authresp`.</span></span> <span data-ttu-id="0df10-159">Make sure to replace **tenant** with your tenant name (for example, contosob2c.onmicrosoft.com) and **policyId** with the identifier of your policy (for example, b2c_1a_policy).</span><span class="sxs-lookup"><span data-stu-id="0df10-159">Make sure to replace **tenant** with your tenant name (for example, contosob2c.onmicrosoft.com) and **policyId** with the identifier of your policy (for example, b2c_1a_policy).</span></span> <span data-ttu-id="0df10-160">The redirect URI needs to be in all lowercase.</span><span class="sxs-lookup"><span data-stu-id="0df10-160">The redirect URI needs to be in all lowercase.</span></span> <span data-ttu-id="0df10-161">You should add a redirect UR for all policies that use the identity provider login.</span><span class="sxs-lookup"><span data-stu-id="0df10-161">You should add a redirect UR for all policies that use the identity provider login.</span></span> 

<span data-ttu-id="0df10-162">If you are using the **b2clogin.com** domain instead of **login.microsoftonline.com** Make sure to use b2clogin.com instead of login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="0df10-162">If you are using the **b2clogin.com** domain instead of **login.microsoftonline.com** Make sure to use b2clogin.com instead of login.microsoftonline.com.</span></span>

<span data-ttu-id="0df10-163">Examples:</span><span class="sxs-lookup"><span data-stu-id="0df10-163">Examples:</span></span>

- [<span data-ttu-id="0df10-164">Add Twitter as an OAuth1 identity provider by using custom policies</span><span class="sxs-lookup"><span data-stu-id="0df10-164">Add Twitter as an OAuth1 identity provider by using custom policies</span></span>](active-directory-b2c-custom-setup-twitter-idp.md)













