---
title: Define a RESTful technical profile in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define a RESTful technical profile in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 930cdddd8a9e039fa9c29a348a0a66eb25d254fe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870951"
---
# <a name="define-a-restful-technical-profile-in-an-azure-active-directory-b2c-custom-policy"></a><span data-ttu-id="c2153-103">Define a RESTful technical profile in an Azure Active Directory B2C custom policy</span><span class="sxs-lookup"><span data-stu-id="c2153-103">Define a RESTful technical profile in an Azure Active Directory B2C custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="c2153-104">Azure Active Directory (Azure AD) B2C provides support for your own RESTful service.</span><span class="sxs-lookup"><span data-stu-id="c2153-104">Azure Active Directory (Azure AD) B2C provides support for your own RESTful service.</span></span> <span data-ttu-id="c2153-105">Azure AD B2C sends data to the RESTful service in an input claims collection and receives data back in an output claims collection.</span><span class="sxs-lookup"><span data-stu-id="c2153-105">Azure AD B2C sends data to the RESTful service in an input claims collection and receives data back in an output claims collection.</span></span> <span data-ttu-id="c2153-106">With RESTful service integration, you can:</span><span class="sxs-lookup"><span data-stu-id="c2153-106">With RESTful service integration, you can:</span></span>

- <span data-ttu-id="c2153-107">**Validate user input data** - Prevents malformed data from persisting into Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c2153-107">**Validate user input data** - Prevents malformed data from persisting into Azure AD B2C.</span></span> <span data-ttu-id="c2153-108">If the value from the user is not valid, your RESTful service returns an error message that instructs the user to provide an entry.</span><span class="sxs-lookup"><span data-stu-id="c2153-108">If the value from the user is not valid, your RESTful service returns an error message that instructs the user to provide an entry.</span></span> <span data-ttu-id="c2153-109">For example, you can verify that the email address provided by the user exists in your customer's database.</span><span class="sxs-lookup"><span data-stu-id="c2153-109">For example, you can verify that the email address provided by the user exists in your customer's database.</span></span>
- <span data-ttu-id="c2153-110">**Overwrite input claims** - Enables you to reformat values in input claims.</span><span class="sxs-lookup"><span data-stu-id="c2153-110">**Overwrite input claims** - Enables you to reformat values in input claims.</span></span> <span data-ttu-id="c2153-111">For example, if a user enters the first name in all lowercase or all uppercase letters, you can format the name with only the first letter capitalized.</span><span class="sxs-lookup"><span data-stu-id="c2153-111">For example, if a user enters the first name in all lowercase or all uppercase letters, you can format the name with only the first letter capitalized.</span></span>
- <span data-ttu-id="c2153-112">**Enrich user data** - Enables you to further integrate with corporate line-of-business applications.</span><span class="sxs-lookup"><span data-stu-id="c2153-112">**Enrich user data** - Enables you to further integrate with corporate line-of-business applications.</span></span> <span data-ttu-id="c2153-113">For example, your RESTful service can receive the user's email address, query the customer's database, and return the user's loyalty number to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c2153-113">For example, your RESTful service can receive the user's email address, query the customer's database, and return the user's loyalty number to Azure AD B2C.</span></span> <span data-ttu-id="c2153-114">The return claims can be stored, evaluated in the next Orchestration Steps, or included in the access token.</span><span class="sxs-lookup"><span data-stu-id="c2153-114">The return claims can be stored, evaluated in the next Orchestration Steps, or included in the access token.</span></span>
- <span data-ttu-id="c2153-115">**Run custom business logic** - Enables you to send push notifications, update corporate databases, run a user migration process, manage permissions, audit databases, and perform other actions.</span><span class="sxs-lookup"><span data-stu-id="c2153-115">**Run custom business logic** - Enables you to send push notifications, update corporate databases, run a user migration process, manage permissions, audit databases, and perform other actions.</span></span>

<span data-ttu-id="c2153-116">Your policy may send input claims to your REST API.</span><span class="sxs-lookup"><span data-stu-id="c2153-116">Your policy may send input claims to your REST API.</span></span> <span data-ttu-id="c2153-117">The REST API may also return output claims that you can use later in your policy, or it can throw an error message.</span><span class="sxs-lookup"><span data-stu-id="c2153-117">The REST API may also return output claims that you can use later in your policy, or it can throw an error message.</span></span> <span data-ttu-id="c2153-118">You can design the integration with the RESTful services in the following ways:</span><span class="sxs-lookup"><span data-stu-id="c2153-118">You can design the integration with the RESTful services in the following ways:</span></span>

- <span data-ttu-id="c2153-119">**Validation technical profile** - A validation technical profile calls the RESTful service.</span><span class="sxs-lookup"><span data-stu-id="c2153-119">**Validation technical profile** - A validation technical profile calls the RESTful service.</span></span> <span data-ttu-id="c2153-120">The validation technical profile validates the user-provided data before the user journey continues.</span><span class="sxs-lookup"><span data-stu-id="c2153-120">The validation technical profile validates the user-provided data before the user journey continues.</span></span> <span data-ttu-id="c2153-121">With the validation technical profile, an error message is display on a self-asserted page and returned in output claims.</span><span class="sxs-lookup"><span data-stu-id="c2153-121">With the validation technical profile, an error message is display on a self-asserted page and returned in output claims.</span></span>
- <span data-ttu-id="c2153-122">**Claims exchange** - A call is made to the RESTful service through an orchestration step.</span><span class="sxs-lookup"><span data-stu-id="c2153-122">**Claims exchange** - A call is made to the RESTful service through an orchestration step.</span></span> <span data-ttu-id="c2153-123">In this scenario, there is no user-interface to render the error message.</span><span class="sxs-lookup"><span data-stu-id="c2153-123">In this scenario, there is no user-interface to render the error message.</span></span> <span data-ttu-id="c2153-124">If your REST API returns an error, the user is redirected back to the relying party application with the error message.</span><span class="sxs-lookup"><span data-stu-id="c2153-124">If your REST API returns an error, the user is redirected back to the relying party application with the error message.</span></span>

## <a name="protocol"></a><span data-ttu-id="c2153-125">Protocol</span><span class="sxs-lookup"><span data-stu-id="c2153-125">Protocol</span></span>

<span data-ttu-id="c2153-126">The **Name** attribute of the **Protocol** element needs to be set to `Proprietary`.</span><span class="sxs-lookup"><span data-stu-id="c2153-126">The **Name** attribute of the **Protocol** element needs to be set to `Proprietary`.</span></span> <span data-ttu-id="c2153-127">The **handler** attribute must contain the fully qualified name of the protocol handler assembly that is used by Azure AD B2C: `Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`.</span><span class="sxs-lookup"><span data-stu-id="c2153-127">The **handler** attribute must contain the fully qualified name of the protocol handler assembly that is used by Azure AD B2C: `Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`.</span></span>

<span data-ttu-id="c2153-128">The following example shows a RESTful technical profile:</span><span class="sxs-lookup"><span data-stu-id="c2153-128">The following example shows a RESTful technical profile:</span></span>

```XML
<TechnicalProfile Id="REST-UserMembershipValidator">
  <DisplayName>Validate user input data and return loyaltyNumber claim</DisplayName>
  <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  ...    
```

## <a name="input-claims"></a><span data-ttu-id="c2153-129">Input claims</span><span class="sxs-lookup"><span data-stu-id="c2153-129">Input claims</span></span>

<span data-ttu-id="c2153-130">The **InputClaims** element contains a list of claims to send to the REST API.</span><span class="sxs-lookup"><span data-stu-id="c2153-130">The **InputClaims** element contains a list of claims to send to the REST API.</span></span> <span data-ttu-id="c2153-131">You can also map the name of your claim to the name defined in the REST API.</span><span class="sxs-lookup"><span data-stu-id="c2153-131">You can also map the name of your claim to the name defined in the REST API.</span></span> <span data-ttu-id="c2153-132">Following example shows the mapping between your policy and the REST API.</span><span class="sxs-lookup"><span data-stu-id="c2153-132">Following example shows the mapping between your policy and the REST API.</span></span> <span data-ttu-id="c2153-133">The **givenName** claim is sent to the REST API as **firstName**, while **surname** is sent as **lastName**.</span><span class="sxs-lookup"><span data-stu-id="c2153-133">The **givenName** claim is sent to the REST API as **firstName**, while **surname** is sent as **lastName**.</span></span> <span data-ttu-id="c2153-134">The **email** claim is set as is.</span><span class="sxs-lookup"><span data-stu-id="c2153-134">The **email** claim is set as is.</span></span>

```XML
<InputClaims>
  <InputClaim ClaimTypeReferenceId="email" />
  <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="firstName" />
  <InputClaim ClaimTypeReferenceId="surname" PartnerClaimType="lastName" />
</InputClaims>
```

<span data-ttu-id="c2153-135">The **InputClaimsTransformations** element may contain a collection of **InputClaimsTransformation** elements that are used to modify the input claims or generate new ones before sending to the REST API.</span><span class="sxs-lookup"><span data-stu-id="c2153-135">The **InputClaimsTransformations** element may contain a collection of **InputClaimsTransformation** elements that are used to modify the input claims or generate new ones before sending to the REST API.</span></span>

## <a name="output-claims"></a><span data-ttu-id="c2153-136">Output claims</span><span class="sxs-lookup"><span data-stu-id="c2153-136">Output claims</span></span>

<span data-ttu-id="c2153-137">The **OutputClaims** element contains a list of claims returned by the REST API.</span><span class="sxs-lookup"><span data-stu-id="c2153-137">The **OutputClaims** element contains a list of claims returned by the REST API.</span></span> <span data-ttu-id="c2153-138">You may need to map the name of the claim defined in your policy to the name defined in the REST API.</span><span class="sxs-lookup"><span data-stu-id="c2153-138">You may need to map the name of the claim defined in your policy to the name defined in the REST API.</span></span> <span data-ttu-id="c2153-139">You can also include claims that aren't returned by the REST API identity provider, as long as you set the `DefaultValue` attribute.</span><span class="sxs-lookup"><span data-stu-id="c2153-139">You can also include claims that aren't returned by the REST API identity provider, as long as you set the `DefaultValue` attribute.</span></span>

<span data-ttu-id="c2153-140">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span><span class="sxs-lookup"><span data-stu-id="c2153-140">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span></span>

<span data-ttu-id="c2153-141">The following example shows the claim returned by the REST API:</span><span class="sxs-lookup"><span data-stu-id="c2153-141">The following example shows the claim returned by the REST API:</span></span>

- <span data-ttu-id="c2153-142">The **MembershipId** claim that is mapped to the **loyaltyNumber** claim name.</span><span class="sxs-lookup"><span data-stu-id="c2153-142">The **MembershipId** claim that is mapped to the **loyaltyNumber** claim name.</span></span>

<span data-ttu-id="c2153-143">The technical profile also returns claims, that aren't returned by the identity provider:</span><span class="sxs-lookup"><span data-stu-id="c2153-143">The technical profile also returns claims, that aren't returned by the identity provider:</span></span> 

- <span data-ttu-id="c2153-144">The **loyaltyNumberIsNew** claim that has a default value set to `true`.</span><span class="sxs-lookup"><span data-stu-id="c2153-144">The **loyaltyNumberIsNew** claim that has a default value set to `true`.</span></span>

```xml
<OutputClaims>
  <OutputClaim ClaimTypeReferenceId="loyaltyNumber" PartnerClaimType="MembershipId" />
  <OutputClaim ClaimTypeReferenceId="loyaltyNumberIsNew" DefaultValue="true" />
</OutputClaims>
```

## <a name="metadata"></a><span data-ttu-id="c2153-145">Metadata</span><span class="sxs-lookup"><span data-stu-id="c2153-145">Metadata</span></span>

| <span data-ttu-id="c2153-146">Attribute</span><span class="sxs-lookup"><span data-stu-id="c2153-146">Attribute</span></span> | <span data-ttu-id="c2153-147">Required</span><span class="sxs-lookup"><span data-stu-id="c2153-147">Required</span></span> | <span data-ttu-id="c2153-148">Description</span><span class="sxs-lookup"><span data-stu-id="c2153-148">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="c2153-149">ServiceUrl</span><span class="sxs-lookup"><span data-stu-id="c2153-149">ServiceUrl</span></span> | <span data-ttu-id="c2153-150">Yes</span><span class="sxs-lookup"><span data-stu-id="c2153-150">Yes</span></span> | <span data-ttu-id="c2153-151">The URL of the REST API endpoint.</span><span class="sxs-lookup"><span data-stu-id="c2153-151">The URL of the REST API endpoint.</span></span> | 
| <span data-ttu-id="c2153-152">AuthenticationType</span><span class="sxs-lookup"><span data-stu-id="c2153-152">AuthenticationType</span></span> | <span data-ttu-id="c2153-153">Yes</span><span class="sxs-lookup"><span data-stu-id="c2153-153">Yes</span></span> | <span data-ttu-id="c2153-154">The type of authentication being performed by the RESTful claims provider.</span><span class="sxs-lookup"><span data-stu-id="c2153-154">The type of authentication being performed by the RESTful claims provider.</span></span> <span data-ttu-id="c2153-155">Possible values: `None`, `Basic`, or `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="c2153-155">Possible values: `None`, `Basic`, or `ClientCertificate`.</span></span> <span data-ttu-id="c2153-156">The `None` value indicates that the REST API is not anonymous.</span><span class="sxs-lookup"><span data-stu-id="c2153-156">The `None` value indicates that the REST API is not anonymous.</span></span> <span data-ttu-id="c2153-157">The `Basic` value indicates that the REST API is secured with HTTP basic authentication.</span><span class="sxs-lookup"><span data-stu-id="c2153-157">The `Basic` value indicates that the REST API is secured with HTTP basic authentication.</span></span> <span data-ttu-id="c2153-158">Only verified users, including Azure AD B2C, can access your API.</span><span class="sxs-lookup"><span data-stu-id="c2153-158">Only verified users, including Azure AD B2C, can access your API.</span></span> <span data-ttu-id="c2153-159">The `ClientCertificate` (recommended) value indicates that the REST API restricts access using client certificate authentication.</span><span class="sxs-lookup"><span data-stu-id="c2153-159">The `ClientCertificate` (recommended) value indicates that the REST API restricts access using client certificate authentication.</span></span> <span data-ttu-id="c2153-160">Only services that have the appropriate certificates, such as Azure AD B2C can access your service.</span><span class="sxs-lookup"><span data-stu-id="c2153-160">Only services that have the appropriate certificates, such as Azure AD B2C can access your service.</span></span> | 
| <span data-ttu-id="c2153-161">SendClaimsIn</span><span class="sxs-lookup"><span data-stu-id="c2153-161">SendClaimsIn</span></span> | <span data-ttu-id="c2153-162">No</span><span class="sxs-lookup"><span data-stu-id="c2153-162">No</span></span> | <span data-ttu-id="c2153-163">Specifies how the input claims are sent to the RESTful claims provider.</span><span class="sxs-lookup"><span data-stu-id="c2153-163">Specifies how the input claims are sent to the RESTful claims provider.</span></span> <span data-ttu-id="c2153-164">Possible values: `Body` (default), `Form`, `Header`, or `QueryString`.</span><span class="sxs-lookup"><span data-stu-id="c2153-164">Possible values: `Body` (default), `Form`, `Header`, or `QueryString`.</span></span> <span data-ttu-id="c2153-165">The `Body` value is the input claim that is sent in the request body in JSON format.</span><span class="sxs-lookup"><span data-stu-id="c2153-165">The `Body` value is the input claim that is sent in the request body in JSON format.</span></span> <span data-ttu-id="c2153-166">The `Form` value is the input claim that is sent in the request body in an ampersand '&' separated key value format.</span><span class="sxs-lookup"><span data-stu-id="c2153-166">The `Form` value is the input claim that is sent in the request body in an ampersand '&' separated key value format.</span></span> <span data-ttu-id="c2153-167">The `Header` value is the input claim that is sent in the request header.</span><span class="sxs-lookup"><span data-stu-id="c2153-167">The `Header` value is the input claim that is sent in the request header.</span></span> <span data-ttu-id="c2153-168">The `QueryString` value is the input claim that is sent in the request query string.</span><span class="sxs-lookup"><span data-stu-id="c2153-168">The `QueryString` value is the input claim that is sent in the request query string.</span></span> | 
| <span data-ttu-id="c2153-169">ClaimsFormat</span><span class="sxs-lookup"><span data-stu-id="c2153-169">ClaimsFormat</span></span> | <span data-ttu-id="c2153-170">No</span><span class="sxs-lookup"><span data-stu-id="c2153-170">No</span></span> | <span data-ttu-id="c2153-171">Specifies the format for the output claims.</span><span class="sxs-lookup"><span data-stu-id="c2153-171">Specifies the format for the output claims.</span></span> <span data-ttu-id="c2153-172">Possible values: `Body` (default), `Form`, `Header`, or `QueryString`.</span><span class="sxs-lookup"><span data-stu-id="c2153-172">Possible values: `Body` (default), `Form`, `Header`, or `QueryString`.</span></span> <span data-ttu-id="c2153-173">The `Body` value is the output claim that is sent in the request body in JSON format.</span><span class="sxs-lookup"><span data-stu-id="c2153-173">The `Body` value is the output claim that is sent in the request body in JSON format.</span></span> <span data-ttu-id="c2153-174">The `Form` value is the output claim that is sent in the request body in an ampersand '&' separated key value format.</span><span class="sxs-lookup"><span data-stu-id="c2153-174">The `Form` value is the output claim that is sent in the request body in an ampersand '&' separated key value format.</span></span> <span data-ttu-id="c2153-175">The `Header` value is the output claim that is sent in the request header.</span><span class="sxs-lookup"><span data-stu-id="c2153-175">The `Header` value is the output claim that is sent in the request header.</span></span> <span data-ttu-id="c2153-176">The `QueryString` value is the output claim that is sent in the request query string.</span><span class="sxs-lookup"><span data-stu-id="c2153-176">The `QueryString` value is the output claim that is sent in the request query string.</span></span> | 
| <span data-ttu-id="c2153-177">DebugMode</span><span class="sxs-lookup"><span data-stu-id="c2153-177">DebugMode</span></span> | <span data-ttu-id="c2153-178">No</span><span class="sxs-lookup"><span data-stu-id="c2153-178">No</span></span> | <span data-ttu-id="c2153-179">Runs the technical profile in debug mode.</span><span class="sxs-lookup"><span data-stu-id="c2153-179">Runs the technical profile in debug mode.</span></span> <span data-ttu-id="c2153-180">In debug mode, the REST API can return more information.</span><span class="sxs-lookup"><span data-stu-id="c2153-180">In debug mode, the REST API can return more information.</span></span> <span data-ttu-id="c2153-181">See the returning error message section.</span><span class="sxs-lookup"><span data-stu-id="c2153-181">See the returning error message section.</span></span> | 

## <a name="cryptographic-keys"></a><span data-ttu-id="c2153-182">Cryptographic keys</span><span class="sxs-lookup"><span data-stu-id="c2153-182">Cryptographic keys</span></span>

<span data-ttu-id="c2153-183">If the type of authentication is set to `None`, the **CryptographicKeys** element is not used.</span><span class="sxs-lookup"><span data-stu-id="c2153-183">If the type of authentication is set to `None`, the **CryptographicKeys** element is not used.</span></span>

```XML
<TechnicalProfile Id="REST-API-SignUp">
  <DisplayName>Validate user's input data and return loyaltyNumber claim</DisplayName>
  <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  <Metadata>
    <Item Key="ServiceUrl">https://your-app-name.azurewebsites.NET/api/identity/signup</Item>
    <Item Key="AuthenticationType">None</Item>
    <Item Key="SendClaimsIn">Body</Item>
  </Metadata>
</TechnicalProfile>
```

<span data-ttu-id="c2153-184">If the type of authentication is set to `Basic`, the **CryptographicKeys** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="c2153-184">If the type of authentication is set to `Basic`, the **CryptographicKeys** element contains the following attributes:</span></span>

| <span data-ttu-id="c2153-185">Attribute</span><span class="sxs-lookup"><span data-stu-id="c2153-185">Attribute</span></span> | <span data-ttu-id="c2153-186">Required</span><span class="sxs-lookup"><span data-stu-id="c2153-186">Required</span></span> | <span data-ttu-id="c2153-187">Description</span><span class="sxs-lookup"><span data-stu-id="c2153-187">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="c2153-188">BasicAuthenticationUsername</span><span class="sxs-lookup"><span data-stu-id="c2153-188">BasicAuthenticationUsername</span></span> | <span data-ttu-id="c2153-189">Yes</span><span class="sxs-lookup"><span data-stu-id="c2153-189">Yes</span></span> | <span data-ttu-id="c2153-190">The username that is used to authenticate.</span><span class="sxs-lookup"><span data-stu-id="c2153-190">The username that is used to authenticate.</span></span> | 
| <span data-ttu-id="c2153-191">BasicAuthenticationPassword</span><span class="sxs-lookup"><span data-stu-id="c2153-191">BasicAuthenticationPassword</span></span> | <span data-ttu-id="c2153-192">Yes</span><span class="sxs-lookup"><span data-stu-id="c2153-192">Yes</span></span> | <span data-ttu-id="c2153-193">The password that is used to authenticate.</span><span class="sxs-lookup"><span data-stu-id="c2153-193">The password that is used to authenticate.</span></span> |

<span data-ttu-id="c2153-194">The following example shows a technical profile with basic authentication:</span><span class="sxs-lookup"><span data-stu-id="c2153-194">The following example shows a technical profile with basic authentication:</span></span>

```XML
<TechnicalProfile Id="REST-API-SignUp">
  <DisplayName>Validate user's input data and return loyaltyNumber claim</DisplayName>
  <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  <Metadata>
    <Item Key="ServiceUrl">https://your-app-name.azurewebsites.NET/api/identity/signup</Item>
    <Item Key="AuthenticationType">Basic</Item>
    <Item Key="SendClaimsIn">Body</Item>
  </Metadata>
  <CryptographicKeys>
    <Key Id="BasicAuthenticationUsername" StorageReferenceId="B2C_1A_B2cRestClientId" />
    <Key Id="BasicAuthenticationPassword" StorageReferenceId="B2C_1A_B2cRestClientSecret" />
  </CryptographicKeys>
</TechnicalProfile>
```

<span data-ttu-id="c2153-195">If the type of authentication is set to `ClientCertificate`, the **CryptographicKeys** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="c2153-195">If the type of authentication is set to `ClientCertificate`, the **CryptographicKeys** element contains the following attribute:</span></span>

| <span data-ttu-id="c2153-196">Attribute</span><span class="sxs-lookup"><span data-stu-id="c2153-196">Attribute</span></span> | <span data-ttu-id="c2153-197">Required</span><span class="sxs-lookup"><span data-stu-id="c2153-197">Required</span></span> | <span data-ttu-id="c2153-198">Description</span><span class="sxs-lookup"><span data-stu-id="c2153-198">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="c2153-199">ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="c2153-199">ClientCertificate</span></span> | <span data-ttu-id="c2153-200">Yes</span><span class="sxs-lookup"><span data-stu-id="c2153-200">Yes</span></span> | <span data-ttu-id="c2153-201">The X509 certificate (RSA key set) to use to authenticate.</span><span class="sxs-lookup"><span data-stu-id="c2153-201">The X509 certificate (RSA key set) to use to authenticate.</span></span> | 

```XML
<TechnicalProfile Id="REST-API-SignUp">
  <DisplayName>Validate user's input data and return loyaltyNumber claim</DisplayName>
  <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  <Metadata>
    <Item Key="ServiceUrl">https://your-app-name.azurewebsites.NET/api/identity/signup</Item>
    <Item Key="AuthenticationType">ClientCertificate</Item>
    <Item Key="SendClaimsIn">Body</Item>
  </Metadata>
  <CryptographicKeys>
    <Key Id="ClientCertificate" StorageReferenceId="B2C_1A_B2cRestClientCertificate" />
  </CryptographicKeys>
</TechnicalProfile>
```

## <a name="returning-error-message"></a><span data-ttu-id="c2153-202">Returning error message</span><span class="sxs-lookup"><span data-stu-id="c2153-202">Returning error message</span></span>

<span data-ttu-id="c2153-203">Your REST API may need to return an error message, such as 'The user was not found in the CRM system'.</span><span class="sxs-lookup"><span data-stu-id="c2153-203">Your REST API may need to return an error message, such as 'The user was not found in the CRM system'.</span></span> <span data-ttu-id="c2153-204">In an error occurs, the REST API should return an HTTP 409 error message (Conflict response status code) with following attributes:</span><span class="sxs-lookup"><span data-stu-id="c2153-204">In an error occurs, the REST API should return an HTTP 409 error message (Conflict response status code) with following attributes:</span></span>

| <span data-ttu-id="c2153-205">Attribute</span><span class="sxs-lookup"><span data-stu-id="c2153-205">Attribute</span></span> | <span data-ttu-id="c2153-206">Required</span><span class="sxs-lookup"><span data-stu-id="c2153-206">Required</span></span> | <span data-ttu-id="c2153-207">Description</span><span class="sxs-lookup"><span data-stu-id="c2153-207">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="c2153-208">version</span><span class="sxs-lookup"><span data-stu-id="c2153-208">version</span></span> | <span data-ttu-id="c2153-209">Yes</span><span class="sxs-lookup"><span data-stu-id="c2153-209">Yes</span></span> | <span data-ttu-id="c2153-210">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c2153-210">1.0.0</span></span> | 
| <span data-ttu-id="c2153-211">status</span><span class="sxs-lookup"><span data-stu-id="c2153-211">status</span></span> | <span data-ttu-id="c2153-212">Yes</span><span class="sxs-lookup"><span data-stu-id="c2153-212">Yes</span></span> | <span data-ttu-id="c2153-213">409</span><span class="sxs-lookup"><span data-stu-id="c2153-213">409</span></span> | 
| <span data-ttu-id="c2153-214">code</span><span class="sxs-lookup"><span data-stu-id="c2153-214">code</span></span> | <span data-ttu-id="c2153-215">No</span><span class="sxs-lookup"><span data-stu-id="c2153-215">No</span></span> | <span data-ttu-id="c2153-216">An error code from the RESTful endpoint provider, which is displayed when `DebugMode` is enabled.</span><span class="sxs-lookup"><span data-stu-id="c2153-216">An error code from the RESTful endpoint provider, which is displayed when `DebugMode` is enabled.</span></span> | 
| <span data-ttu-id="c2153-217">requestId</span><span class="sxs-lookup"><span data-stu-id="c2153-217">requestId</span></span> | <span data-ttu-id="c2153-218">No</span><span class="sxs-lookup"><span data-stu-id="c2153-218">No</span></span> | <span data-ttu-id="c2153-219">A request identifier from the RESTful endpoint provider, which is displayed when `DebugMode` is enabled.</span><span class="sxs-lookup"><span data-stu-id="c2153-219">A request identifier from the RESTful endpoint provider, which is displayed when `DebugMode` is enabled.</span></span> | 
| <span data-ttu-id="c2153-220">userMessage</span><span class="sxs-lookup"><span data-stu-id="c2153-220">userMessage</span></span> | <span data-ttu-id="c2153-221">Yes</span><span class="sxs-lookup"><span data-stu-id="c2153-221">Yes</span></span> | <span data-ttu-id="c2153-222">An error message that is shown to the user.</span><span class="sxs-lookup"><span data-stu-id="c2153-222">An error message that is shown to the user.</span></span> | 
| <span data-ttu-id="c2153-223">developerMessage</span><span class="sxs-lookup"><span data-stu-id="c2153-223">developerMessage</span></span> | <span data-ttu-id="c2153-224">No</span><span class="sxs-lookup"><span data-stu-id="c2153-224">No</span></span> | <span data-ttu-id="c2153-225">The verbose description of the problem and how to fix it, which is displayed when `DebugMode` is enabled.</span><span class="sxs-lookup"><span data-stu-id="c2153-225">The verbose description of the problem and how to fix it, which is displayed when `DebugMode` is enabled.</span></span> | 
| <span data-ttu-id="c2153-226">moreInfo</span><span class="sxs-lookup"><span data-stu-id="c2153-226">moreInfo</span></span> | <span data-ttu-id="c2153-227">No</span><span class="sxs-lookup"><span data-stu-id="c2153-227">No</span></span> | <span data-ttu-id="c2153-228">A URI that points to additional information, which is displayed when `DebugMode` is enabled.</span><span class="sxs-lookup"><span data-stu-id="c2153-228">A URI that points to additional information, which is displayed when `DebugMode` is enabled.</span></span> | 

<span data-ttu-id="c2153-229">The following example shows a REST API that returns an error message formatted in JSON:</span><span class="sxs-lookup"><span data-stu-id="c2153-229">The following example shows a REST API that returns an error message formatted in JSON:</span></span>

```JSON
{
  "version": "1.0.0",
  "status": 409,
  "code": "API12345",
  "requestId": "50f0bd91-2ff4-4b8f-828f-00f170519ddb",
  "userMessage": "Message for the user", 
  "developerMessage": "Verbose description of problem and how to fix it.", 
  "moreInfo": "https://restapi/error/API12345/moreinfo" 
}
```

<span data-ttu-id="c2153-230">The following example shows a C# class that returns an error message:</span><span class="sxs-lookup"><span data-stu-id="c2153-230">The following example shows a C# class that returns an error message:</span></span>

```C#
public class ResponseContent
{
  public string version { get; set; }
  public int status { get; set; }
  public string code { get; set; }
  public string userMessage { get; set; }
  public string developerMessage { get; set; }
  public string requestId { get; set; }
  public string moreInfo { get; set; }
}
```

## <a name="examples"></a><span data-ttu-id="c2153-231">Examples:</span><span class="sxs-lookup"><span data-stu-id="c2153-231">Examples:</span></span>
- [<span data-ttu-id="c2153-232">Integrate REST API claims exchanges in your Azure AD B2C user journey as validation of user input</span><span class="sxs-lookup"><span data-stu-id="c2153-232">Integrate REST API claims exchanges in your Azure AD B2C user journey as validation of user input</span></span>](active-directory-b2c-custom-rest-api-netfw.md) 
- [<span data-ttu-id="c2153-233">Secure your RESTful services by using HTTP basic authentication</span><span class="sxs-lookup"><span data-stu-id="c2153-233">Secure your RESTful services by using HTTP basic authentication</span></span>](active-directory-b2c-custom-rest-api-netfw-secure-basic.md)
- [<span data-ttu-id="c2153-234">Secure your RESTful service by using client certificates</span><span class="sxs-lookup"><span data-stu-id="c2153-234">Secure your RESTful service by using client certificates</span></span>](active-directory-b2c-custom-rest-api-netfw-secure-cert.md)
- [<span data-ttu-id="c2153-235">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span><span class="sxs-lookup"><span data-stu-id="c2153-235">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>](active-directory-b2c-rest-api-validation-custom.md)

 














