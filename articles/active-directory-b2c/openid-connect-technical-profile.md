---
title: Define a OpenId Connect technical profile in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define a OpenId Connect technical profile in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 40922080857563b86d538586b90513381edb5d89
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864710"
---
# <a name="define-a-openid-connect-technical-profile-in-an-azure-active-directory-b2c-custom-policy"></a><span data-ttu-id="e1494-103">Define a OpenId Connect technical profile in an Azure Active Directory B2C custom policy</span><span class="sxs-lookup"><span data-stu-id="e1494-103">Define a OpenId Connect technical profile in an Azure Active Directory B2C custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="e1494-104">Azure Active Directory (Azure AD) B2C provides support for the [OpenId Connect](http://openid.net/2015/04/17/openid-connect-certification-program/) protocol identity provider.</span><span class="sxs-lookup"><span data-stu-id="e1494-104">Azure Active Directory (Azure AD) B2C provides support for the [OpenId Connect](http://openid.net/2015/04/17/openid-connect-certification-program/) protocol identity provider.</span></span> <span data-ttu-id="e1494-105">OpenID Connect 1.0 defines an identity layer on top of OAuth 2.0 and represents the state of the art in modern authentication protocols.</span><span class="sxs-lookup"><span data-stu-id="e1494-105">OpenID Connect 1.0 defines an identity layer on top of OAuth 2.0 and represents the state of the art in modern authentication protocols.</span></span>  <span data-ttu-id="e1494-106">With OpenId Connect technical profile you can federate with an OpenId Connect based identity provider, such as Azure AD, allowing you users to sign-in with their existing social or enterprise identities.</span><span class="sxs-lookup"><span data-stu-id="e1494-106">With OpenId Connect technical profile you can federate with an OpenId Connect based identity provider, such as Azure AD, allowing you users to sign-in with their existing social or enterprise identities.</span></span>

## <a name="protocol"></a><span data-ttu-id="e1494-107">Protocol</span><span class="sxs-lookup"><span data-stu-id="e1494-107">Protocol</span></span>

<span data-ttu-id="e1494-108">The **Name** attribute of the **Protocol** element needs to be set to `OpenIdConnect`.</span><span class="sxs-lookup"><span data-stu-id="e1494-108">The **Name** attribute of the **Protocol** element needs to be set to `OpenIdConnect`.</span></span> <span data-ttu-id="e1494-109">For example, the protocol for the **MSA-OIDC** technical profile is `OpenIdConnect`:</span><span class="sxs-lookup"><span data-stu-id="e1494-109">For example, the protocol for the **MSA-OIDC** technical profile is `OpenIdConnect`:</span></span>

```XML
<TechnicalProfile Id="MSA-OIDC">
  <DisplayName>Microsoft Account</DisplayName>
  <Protocol Name="OpenIdConnect" />
  ...    
```

## <a name="input-claims"></a><span data-ttu-id="e1494-110">Input claims</span><span class="sxs-lookup"><span data-stu-id="e1494-110">Input claims</span></span>

<span data-ttu-id="e1494-111">The **InputClaims** and **InputClaimsTransformations** elements are not required.</span><span class="sxs-lookup"><span data-stu-id="e1494-111">The **InputClaims** and **InputClaimsTransformations** elements are not required.</span></span> <span data-ttu-id="e1494-112">But you may want to send additional parameters to your identity provider.</span><span class="sxs-lookup"><span data-stu-id="e1494-112">But you may want to send additional parameters to your identity provider.</span></span> <span data-ttu-id="e1494-113">The following example adds the **domain_hint** query string parameter with the value of `contoso.com` to the authorization request.</span><span class="sxs-lookup"><span data-stu-id="e1494-113">The following example adds the **domain_hint** query string parameter with the value of `contoso.com` to the authorization request.</span></span>

```XML
<InputClaims>
  <InputClaim ClaimTypeReferenceId="domain_hint" DefaultValue="contoso.com" />
</InputClaims>
```

## <a name="output-claims"></a><span data-ttu-id="e1494-114">Output claims</span><span class="sxs-lookup"><span data-stu-id="e1494-114">Output claims</span></span>

<span data-ttu-id="e1494-115">The **OutputClaims** element contains a list of claims returned by the OpenId Connect identity provider.</span><span class="sxs-lookup"><span data-stu-id="e1494-115">The **OutputClaims** element contains a list of claims returned by the OpenId Connect identity provider.</span></span> <span data-ttu-id="e1494-116">You may need to map the name of the claim defined in your policy to the name defined in the identity provider.</span><span class="sxs-lookup"><span data-stu-id="e1494-116">You may need to map the name of the claim defined in your policy to the name defined in the identity provider.</span></span> <span data-ttu-id="e1494-117">You can also include claims that aren't returned by the identity provider, as long as you set the `DefaultValue` attribute.</span><span class="sxs-lookup"><span data-stu-id="e1494-117">You can also include claims that aren't returned by the identity provider, as long as you set the `DefaultValue` attribute.</span></span>

<span data-ttu-id="e1494-118">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span><span class="sxs-lookup"><span data-stu-id="e1494-118">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span></span>

<span data-ttu-id="e1494-119">The following example shows the claims returned by the Microsoft Account identity provider:</span><span class="sxs-lookup"><span data-stu-id="e1494-119">The following example shows the claims returned by the Microsoft Account identity provider:</span></span>

- <span data-ttu-id="e1494-120">The **sub** claim that is mapped to the **socialIdpUserId** claim.</span><span class="sxs-lookup"><span data-stu-id="e1494-120">The **sub** claim that is mapped to the **socialIdpUserId** claim.</span></span>
- <span data-ttu-id="e1494-121">The **name** claim that is mapped to the **displayName** claim.</span><span class="sxs-lookup"><span data-stu-id="e1494-121">The **name** claim that is mapped to the **displayName** claim.</span></span>
- <span data-ttu-id="e1494-122">The **email** without name mapping.</span><span class="sxs-lookup"><span data-stu-id="e1494-122">The **email** without name mapping.</span></span>

<span data-ttu-id="e1494-123">The technical profile also returns claims that aren't returned by the identity provider:</span><span class="sxs-lookup"><span data-stu-id="e1494-123">The technical profile also returns claims that aren't returned by the identity provider:</span></span>

- <span data-ttu-id="e1494-124">The **identityProvider** claim that contains the name of the identity provider.</span><span class="sxs-lookup"><span data-stu-id="e1494-124">The **identityProvider** claim that contains the name of the identity provider.</span></span>
- <span data-ttu-id="e1494-125">The **authenticationSource** claim with a default value of **socialIdpAuthentication**.</span><span class="sxs-lookup"><span data-stu-id="e1494-125">The **authenticationSource** claim with a default value of **socialIdpAuthentication**.</span></span>

```xml
<OutputClaims>
  <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
  <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
  <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
  <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
  <OutputClaim ClaimTypeReferenceId="email" />
</OutputClaims>
```

## <a name="metadata"></a><span data-ttu-id="e1494-126">Metadata</span><span class="sxs-lookup"><span data-stu-id="e1494-126">Metadata</span></span>

| <span data-ttu-id="e1494-127">Attribute</span><span class="sxs-lookup"><span data-stu-id="e1494-127">Attribute</span></span> | <span data-ttu-id="e1494-128">Required</span><span class="sxs-lookup"><span data-stu-id="e1494-128">Required</span></span> | <span data-ttu-id="e1494-129">Description</span><span class="sxs-lookup"><span data-stu-id="e1494-129">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="e1494-130">client_id</span><span class="sxs-lookup"><span data-stu-id="e1494-130">client_id</span></span> | <span data-ttu-id="e1494-131">Yes</span><span class="sxs-lookup"><span data-stu-id="e1494-131">Yes</span></span> | <span data-ttu-id="e1494-132">The application identifier of the identity provider.</span><span class="sxs-lookup"><span data-stu-id="e1494-132">The application identifier of the identity provider.</span></span> |
| <span data-ttu-id="e1494-133">IdTokenAudience</span><span class="sxs-lookup"><span data-stu-id="e1494-133">IdTokenAudience</span></span> | <span data-ttu-id="e1494-134">No</span><span class="sxs-lookup"><span data-stu-id="e1494-134">No</span></span> | <span data-ttu-id="e1494-135">The audience of the id_token.</span><span class="sxs-lookup"><span data-stu-id="e1494-135">The audience of the id_token.</span></span> <span data-ttu-id="e1494-136">If specified, Azure AD B2C checks whether the token is in a claim returned by the identity provider and is equal to the one specified.</span><span class="sxs-lookup"><span data-stu-id="e1494-136">If specified, Azure AD B2C checks whether the token is in a claim returned by the identity provider and is equal to the one specified.</span></span> |
| <span data-ttu-id="e1494-137">METADATA</span><span class="sxs-lookup"><span data-stu-id="e1494-137">METADATA</span></span> | <span data-ttu-id="e1494-138">Yes</span><span class="sxs-lookup"><span data-stu-id="e1494-138">Yes</span></span> | <span data-ttu-id="e1494-139">A URL that points to a JSON configuration document formatted according to the OpenID Connect Discovery specification, which is also known as a well-known openid configuration endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1494-139">A URL that points to a JSON configuration document formatted according to the OpenID Connect Discovery specification, which is also known as a well-known openid configuration endpoint.</span></span> |
| <span data-ttu-id="e1494-140">ProviderName</span><span class="sxs-lookup"><span data-stu-id="e1494-140">ProviderName</span></span> | <span data-ttu-id="e1494-141">No</span><span class="sxs-lookup"><span data-stu-id="e1494-141">No</span></span> | <span data-ttu-id="e1494-142">The name of the identity provider.</span><span class="sxs-lookup"><span data-stu-id="e1494-142">The name of the identity provider.</span></span> |
| <span data-ttu-id="e1494-143">response_types</span><span class="sxs-lookup"><span data-stu-id="e1494-143">response_types</span></span> | <span data-ttu-id="e1494-144">No</span><span class="sxs-lookup"><span data-stu-id="e1494-144">No</span></span> | <span data-ttu-id="e1494-145">The response type according to the OpenID Connect Core 1.0 specification.</span><span class="sxs-lookup"><span data-stu-id="e1494-145">The response type according to the OpenID Connect Core 1.0 specification.</span></span> <span data-ttu-id="e1494-146">Possible values: `id_token`, `code`, or `token`.</span><span class="sxs-lookup"><span data-stu-id="e1494-146">Possible values: `id_token`, `code`, or `token`.</span></span> |
| <span data-ttu-id="e1494-147">response_mode</span><span class="sxs-lookup"><span data-stu-id="e1494-147">response_mode</span></span> | <span data-ttu-id="e1494-148">No</span><span class="sxs-lookup"><span data-stu-id="e1494-148">No</span></span> | <span data-ttu-id="e1494-149">The method that the identity provider uses to send the result back to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e1494-149">The method that the identity provider uses to send the result back to Azure AD B2C.</span></span> <span data-ttu-id="e1494-150">Possible values: `query`, `form_post` (default), or `fragment`.</span><span class="sxs-lookup"><span data-stu-id="e1494-150">Possible values: `query`, `form_post` (default), or `fragment`.</span></span> |
| <span data-ttu-id="e1494-151">scope</span><span class="sxs-lookup"><span data-stu-id="e1494-151">scope</span></span> | <span data-ttu-id="e1494-152">No</span><span class="sxs-lookup"><span data-stu-id="e1494-152">No</span></span> | <span data-ttu-id="e1494-153">The scope of the access request defined according to the OpenID Connect Core 1.0 specification.</span><span class="sxs-lookup"><span data-stu-id="e1494-153">The scope of the access request defined according to the OpenID Connect Core 1.0 specification.</span></span> <span data-ttu-id="e1494-154">Such as `openid`, `profile`, and `email`.</span><span class="sxs-lookup"><span data-stu-id="e1494-154">Such as `openid`, `profile`, and `email`.</span></span> |
| <span data-ttu-id="e1494-155">HttpBinding</span><span class="sxs-lookup"><span data-stu-id="e1494-155">HttpBinding</span></span> | <span data-ttu-id="e1494-156">No</span><span class="sxs-lookup"><span data-stu-id="e1494-156">No</span></span> | <span data-ttu-id="e1494-157">The expected HTTP binding to the access token and claims token endpoints.</span><span class="sxs-lookup"><span data-stu-id="e1494-157">The expected HTTP binding to the access token and claims token endpoints.</span></span> <span data-ttu-id="e1494-158">Possible values: `GET` or `POST`.</span><span class="sxs-lookup"><span data-stu-id="e1494-158">Possible values: `GET` or `POST`.</span></span>  |
| <span data-ttu-id="e1494-159">ValidTokenIssuerPrefixes</span><span class="sxs-lookup"><span data-stu-id="e1494-159">ValidTokenIssuerPrefixes</span></span> | <span data-ttu-id="e1494-160">No</span><span class="sxs-lookup"><span data-stu-id="e1494-160">No</span></span> | <span data-ttu-id="e1494-161">A key that can be used to sign in to each of the tenants when using a multi-tenant identity provider such as Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1494-161">A key that can be used to sign in to each of the tenants when using a multi-tenant identity provider such as Azure Active Directory.</span></span> |
| <span data-ttu-id="e1494-162">UsePolicyInRedirectUri</span><span class="sxs-lookup"><span data-stu-id="e1494-162">UsePolicyInRedirectUri</span></span> | <span data-ttu-id="e1494-163">No</span><span class="sxs-lookup"><span data-stu-id="e1494-163">No</span></span> | <span data-ttu-id="e1494-164">Indicates whether to use a policy when constructing the redirect URI.</span><span class="sxs-lookup"><span data-stu-id="e1494-164">Indicates whether to use a policy when constructing the redirect URI.</span></span> <span data-ttu-id="e1494-165">When you configure your application in the identity provider, you need to specify the redirect URI.</span><span class="sxs-lookup"><span data-stu-id="e1494-165">When you configure your application in the identity provider, you need to specify the redirect URI.</span></span> <span data-ttu-id="e1494-166">The redirect URI points to Azure AD B2C, `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` (login.microsoftonline.com may change with your-tenant-name.b2clogin.com).</span><span class="sxs-lookup"><span data-stu-id="e1494-166">The redirect URI points to Azure AD B2C, `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` (login.microsoftonline.com may change with your-tenant-name.b2clogin.com).</span></span>  <span data-ttu-id="e1494-167">If you specify `false`, you need to add a redirect URI for each policy you use.</span><span class="sxs-lookup"><span data-stu-id="e1494-167">If you specify `false`, you need to add a redirect URI for each policy you use.</span></span> <span data-ttu-id="e1494-168">For example: `https://login.microsoftonline.com/te/{tenant}/{policy}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="e1494-168">For example: `https://login.microsoftonline.com/te/{tenant}/{policy}/oauth2/authresp`.</span></span> |
| <span data-ttu-id="e1494-169">MarkAsFailureOnStatusCode5xx</span><span class="sxs-lookup"><span data-stu-id="e1494-169">MarkAsFailureOnStatusCode5xx</span></span> | <span data-ttu-id="e1494-170">No</span><span class="sxs-lookup"><span data-stu-id="e1494-170">No</span></span> | <span data-ttu-id="e1494-171">Indicates whether a request to an external service should be marked as a failure if the Http status code is in the 5xx range.</span><span class="sxs-lookup"><span data-stu-id="e1494-171">Indicates whether a request to an external service should be marked as a failure if the Http status code is in the 5xx range.</span></span> <span data-ttu-id="e1494-172">The default is `false`.</span><span class="sxs-lookup"><span data-stu-id="e1494-172">The default is `false`.</span></span> |
| <span data-ttu-id="e1494-173">DiscoverMetadataByTokenIssuer</span><span class="sxs-lookup"><span data-stu-id="e1494-173">DiscoverMetadataByTokenIssuer</span></span> | <span data-ttu-id="e1494-174">No</span><span class="sxs-lookup"><span data-stu-id="e1494-174">No</span></span> | <span data-ttu-id="e1494-175">Indicates whether the OIDC metadata should be discovered by using the issuer in the JWT token.</span><span class="sxs-lookup"><span data-stu-id="e1494-175">Indicates whether the OIDC metadata should be discovered by using the issuer in the JWT token.</span></span> |

## <a name="cryptographic-keys"></a><span data-ttu-id="e1494-176">Cryptographic keys</span><span class="sxs-lookup"><span data-stu-id="e1494-176">Cryptographic keys</span></span>

<span data-ttu-id="e1494-177">The **CryptographicKeys** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="e1494-177">The **CryptographicKeys** element contains the following attribute:</span></span>

| <span data-ttu-id="e1494-178">Attribute</span><span class="sxs-lookup"><span data-stu-id="e1494-178">Attribute</span></span> | <span data-ttu-id="e1494-179">Required</span><span class="sxs-lookup"><span data-stu-id="e1494-179">Required</span></span> | <span data-ttu-id="e1494-180">Description</span><span class="sxs-lookup"><span data-stu-id="e1494-180">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="e1494-181">client_secret</span><span class="sxs-lookup"><span data-stu-id="e1494-181">client_secret</span></span> | <span data-ttu-id="e1494-182">Yes</span><span class="sxs-lookup"><span data-stu-id="e1494-182">Yes</span></span> | <span data-ttu-id="e1494-183">The client secret of the identity provider application.</span><span class="sxs-lookup"><span data-stu-id="e1494-183">The client secret of the identity provider application.</span></span> <span data-ttu-id="e1494-184">The cryptographic key is required only if the **response_types** metadata is set to `code`.</span><span class="sxs-lookup"><span data-stu-id="e1494-184">The cryptographic key is required only if the **response_types** metadata is set to `code`.</span></span> <span data-ttu-id="e1494-185">In this case, Azure AD B2C makes another call to exchange the authorization code for an access token.</span><span class="sxs-lookup"><span data-stu-id="e1494-185">In this case, Azure AD B2C makes another call to exchange the authorization code for an access token.</span></span> <span data-ttu-id="e1494-186">If the metadata is set to `id_token` you can omit the cryptographic key.</span><span class="sxs-lookup"><span data-stu-id="e1494-186">If the metadata is set to `id_token` you can omit the cryptographic key.</span></span>  |  

## <a name="redirect-uri"></a><span data-ttu-id="e1494-187">Redirect Uri</span><span class="sxs-lookup"><span data-stu-id="e1494-187">Redirect Uri</span></span>
 
<span data-ttu-id="e1494-188">When you configure the redirect URI of your identity provider, enter `https://login.microsoftonline.com/te/tenant/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="e1494-188">When you configure the redirect URI of your identity provider, enter `https://login.microsoftonline.com/te/tenant/oauth2/authresp`.</span></span> <span data-ttu-id="e1494-189">Make sure to replace **tenant** with your tenant's name (for example, contosob2c.onmicrosoft.com) or the tenant's Id. The redirect URI needs to be in all lowercase.</span><span class="sxs-lookup"><span data-stu-id="e1494-189">Make sure to replace **tenant** with your tenant's name (for example, contosob2c.onmicrosoft.com) or the tenant's Id. The redirect URI needs to be in all lowercase.</span></span>

<span data-ttu-id="e1494-190">If you are using the **b2clogin.com** domain instead of **login.microsoftonline.com** Make sure to use b2clogin.com instead of login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="e1494-190">If you are using the **b2clogin.com** domain instead of **login.microsoftonline.com** Make sure to use b2clogin.com instead of login.microsoftonline.com.</span></span>

<span data-ttu-id="e1494-191">Examples:</span><span class="sxs-lookup"><span data-stu-id="e1494-191">Examples:</span></span>

- [<span data-ttu-id="e1494-192">Add Microsoft Account (MSA) as an identity provider using custom policies</span><span class="sxs-lookup"><span data-stu-id="e1494-192">Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>](active-directory-b2c-custom-setup-msa-idp.md)
- [<span data-ttu-id="e1494-193">Sign in by using Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e1494-193">Sign in by using Azure AD accounts</span></span>](active-directory-b2c-setup-aad-custom.md)
- [<span data-ttu-id="e1494-194">Allow users to sign in to a multi-tenant Azure AD identity provider using custom policies</span><span class="sxs-lookup"><span data-stu-id="e1494-194">Allow users to sign in to a multi-tenant Azure AD identity provider using custom policies</span></span>](active-directory-b2c-setup-commonaad-custom.md)

 














