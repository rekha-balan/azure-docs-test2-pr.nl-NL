---
title: Define a self-asserted technical profile in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define a self-asserted technical profile in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: e9472f0fb6ca7c9924df57bb61a3f234bc7d4b13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965809"
---
# <a name="define-a-self-asserted-technical-profile-in-an-azure-active-directory-b2c-custom-policy"></a><span data-ttu-id="058fa-103">Define a self-asserted technical profile in an Azure Active Directory B2C custom policy</span><span class="sxs-lookup"><span data-stu-id="058fa-103">Define a self-asserted technical profile in an Azure Active Directory B2C custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="058fa-104">All interactions in Azure Active Directory (Azure AD) B2C where the user is expected to provide input are self-asserted technical profiles.</span><span class="sxs-lookup"><span data-stu-id="058fa-104">All interactions in Azure Active Directory (Azure AD) B2C where the user is expected to provide input are self-asserted technical profiles.</span></span> <span data-ttu-id="058fa-105">For example, a sign-up page, sign-in page, or password reset page.</span><span class="sxs-lookup"><span data-stu-id="058fa-105">For example, a sign-up page, sign-in page, or password reset page.</span></span>

## <a name="protocol"></a><span data-ttu-id="058fa-106">Protocol</span><span class="sxs-lookup"><span data-stu-id="058fa-106">Protocol</span></span>

<span data-ttu-id="058fa-107">The **Name** attribute of the **Protocol** element needs to be set to `Proprietary`.</span><span class="sxs-lookup"><span data-stu-id="058fa-107">The **Name** attribute of the **Protocol** element needs to be set to `Proprietary`.</span></span> <span data-ttu-id="058fa-108">The **handler** attribute must contain the fully qualified name of the protocol handler assembly that is used by Azure AD B2C, for self-asserted: `Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`</span><span class="sxs-lookup"><span data-stu-id="058fa-108">The **handler** attribute must contain the fully qualified name of the protocol handler assembly that is used by Azure AD B2C, for self-asserted: `Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`</span></span>

<span data-ttu-id="058fa-109">The following example shows a self-asserted technical profile for email sign-up:</span><span class="sxs-lookup"><span data-stu-id="058fa-109">The following example shows a self-asserted technical profile for email sign-up:</span></span>

```XML
<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
  <DisplayName>Email signup</DisplayName>
  <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
```
 
## <a name="input-claims"></a><span data-ttu-id="058fa-110">Input claims</span><span class="sxs-lookup"><span data-stu-id="058fa-110">Input claims</span></span>

<span data-ttu-id="058fa-111">In a self-asserted technical profile, you can use the **InputClaims** and **InputClaimsTransformations** elements to prepopulate the value of the claims that appear on the self-asserted page (output claims).</span><span class="sxs-lookup"><span data-stu-id="058fa-111">In a self-asserted technical profile, you can use the **InputClaims** and **InputClaimsTransformations** elements to prepopulate the value of the claims that appear on the self-asserted page (output claims).</span></span> <span data-ttu-id="058fa-112">For example, in the edit profile policy, the user journey first reads the user profile from the Azure AD B2C directory service, then the self-asserted technical profile sets the input claims with the user data stored in the user profile.</span><span class="sxs-lookup"><span data-stu-id="058fa-112">For example, in the edit profile policy, the user journey first reads the user profile from the Azure AD B2C directory service, then the self-asserted technical profile sets the input claims with the user data stored in the user profile.</span></span> <span data-ttu-id="058fa-113">These claims are collected from the user profile and then presented to the user who can then edit the existing data.</span><span class="sxs-lookup"><span data-stu-id="058fa-113">These claims are collected from the user profile and then presented to the user who can then edit the existing data.</span></span>

```XML
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
...
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
    <InputClaim ClaimTypeReferenceId="userPrincipalName" />
    <InputClaim ClaimTypeReferenceId="givenName" />
    <InputClaim ClaimTypeReferenceId="surname" />
  </InputClaims>
```


## <a name="output-claims"></a><span data-ttu-id="058fa-114">Output claims</span><span class="sxs-lookup"><span data-stu-id="058fa-114">Output claims</span></span>

<span data-ttu-id="058fa-115">The **OutputClaims** element contains a list of claims to be presented to collect data from the user.</span><span class="sxs-lookup"><span data-stu-id="058fa-115">The **OutputClaims** element contains a list of claims to be presented to collect data from the user.</span></span> <span data-ttu-id="058fa-116">To prepopulate the output claims with some values, use the input claims that were previously described.</span><span class="sxs-lookup"><span data-stu-id="058fa-116">To prepopulate the output claims with some values, use the input claims that were previously described.</span></span> <span data-ttu-id="058fa-117">The element may also contain a default value.</span><span class="sxs-lookup"><span data-stu-id="058fa-117">The element may also contain a default value.</span></span> <span data-ttu-id="058fa-118">The order of the claims in **OutputClaims** controls the order that Azure AD B2C renders the claims on the screen.</span><span class="sxs-lookup"><span data-stu-id="058fa-118">The order of the claims in **OutputClaims** controls the order that Azure AD B2C renders the claims on the screen.</span></span> <span data-ttu-id="058fa-119">The **DefaultValue** attribute takes effect only if the claim has never been set before.</span><span class="sxs-lookup"><span data-stu-id="058fa-119">The **DefaultValue** attribute takes effect only if the claim has never been set before.</span></span> <span data-ttu-id="058fa-120">But, if it has been set before in a previous orchestration step, even if the user leaves the value empty, the default value does not take effect.</span><span class="sxs-lookup"><span data-stu-id="058fa-120">But, if it has been set before in a previous orchestration step, even if the user leaves the value empty, the default value does not take effect.</span></span> <span data-ttu-id="058fa-121">To force the use of a default value, set the **AlwaysUseDefaultValue** attribute to `true`.</span><span class="sxs-lookup"><span data-stu-id="058fa-121">To force the use of a default value, set the **AlwaysUseDefaultValue** attribute to `true`.</span></span> <span data-ttu-id="058fa-122">To force the user to provide a value for a specific output claim, set the **Required** attribute of the **OutputClaims** element to `true`.</span><span class="sxs-lookup"><span data-stu-id="058fa-122">To force the user to provide a value for a specific output claim, set the **Required** attribute of the **OutputClaims** element to `true`.</span></span>

<span data-ttu-id="058fa-123">The **ClaimType** element in the **OutputClaims** collection needs to set the **UserInputType** element to any user input type supported by Azure AD B2C, such as `TextBox` or `DropdownSingleSelect`.</span><span class="sxs-lookup"><span data-stu-id="058fa-123">The **ClaimType** element in the **OutputClaims** collection needs to set the **UserInputType** element to any user input type supported by Azure AD B2C, such as `TextBox` or `DropdownSingleSelect`.</span></span> <span data-ttu-id="058fa-124">Or the **OutputClaim** element must set a **DefaultValue**.</span><span class="sxs-lookup"><span data-stu-id="058fa-124">Or the **OutputClaim** element must set a **DefaultValue**.</span></span>  

<span data-ttu-id="058fa-125">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span><span class="sxs-lookup"><span data-stu-id="058fa-125">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span></span>

<span data-ttu-id="058fa-126">The following output claim is always set to `live.com`:</span><span class="sxs-lookup"><span data-stu-id="058fa-126">The following output claim is always set to `live.com`:</span></span>

```XML
<OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" AlwaysUseDefaultValue="true" />
```

### <a name="use-case"></a><span data-ttu-id="058fa-127">Use case</span><span class="sxs-lookup"><span data-stu-id="058fa-127">Use case</span></span>

<span data-ttu-id="058fa-128">There are four scenarios for output claims:</span><span class="sxs-lookup"><span data-stu-id="058fa-128">There are four scenarios for output claims:</span></span>

- <span data-ttu-id="058fa-129">**Collecting the output claims from the user** - When you need to collect information from the user, such as date of birth, you should add the claim to the **OutputClaims** collection.</span><span class="sxs-lookup"><span data-stu-id="058fa-129">**Collecting the output claims from the user** - When you need to collect information from the user, such as date of birth, you should add the claim to the **OutputClaims** collection.</span></span> <span data-ttu-id="058fa-130">The claims that are presented to the user must specify the **UserInputType**, such as `TextBox` or `DropdownSingleSelect`.</span><span class="sxs-lookup"><span data-stu-id="058fa-130">The claims that are presented to the user must specify the **UserInputType**, such as `TextBox` or `DropdownSingleSelect`.</span></span> <span data-ttu-id="058fa-131">If the self-asserted technical profile contains a validation technical profile that outputs the same claim, Azure AD B2C does not present the claim to the user.</span><span class="sxs-lookup"><span data-stu-id="058fa-131">If the self-asserted technical profile contains a validation technical profile that outputs the same claim, Azure AD B2C does not present the claim to the user.</span></span> <span data-ttu-id="058fa-132">If there is no any output claim to present to the user, Azure AD B2C skips the technical profile.</span><span class="sxs-lookup"><span data-stu-id="058fa-132">If there is no any output claim to present to the user, Azure AD B2C skips the technical profile.</span></span>
- <span data-ttu-id="058fa-133">**Setting a default value in an output claim** - Without collecting data from the user or returning the data from the validation technical profile.</span><span class="sxs-lookup"><span data-stu-id="058fa-133">**Setting a default value in an output claim** - Without collecting data from the user or returning the data from the validation technical profile.</span></span> <span data-ttu-id="058fa-134">The `LocalAccountSignUpWithLogonEmail` self-asserted technical profile sets the **executed-SelfAsserted-Input** claim to `true`.</span><span class="sxs-lookup"><span data-stu-id="058fa-134">The `LocalAccountSignUpWithLogonEmail` self-asserted technical profile sets the **executed-SelfAsserted-Input** claim to `true`.</span></span>
- <span data-ttu-id="058fa-135">**A validation technical profile returns the output claims** - Your technical profile may call a validation technical profile that returns some claims.</span><span class="sxs-lookup"><span data-stu-id="058fa-135">**A validation technical profile returns the output claims** - Your technical profile may call a validation technical profile that returns some claims.</span></span> <span data-ttu-id="058fa-136">You may want to bubble up the claims and return them to the next orchestration steps in the user journey.</span><span class="sxs-lookup"><span data-stu-id="058fa-136">You may want to bubble up the claims and return them to the next orchestration steps in the user journey.</span></span> <span data-ttu-id="058fa-137">For example, when signing in with a local account, the self-asserted technical profile named `SelfAsserted-LocalAccountSignin-Email` calls the validation technical profile named `login-NonInteractive`.</span><span class="sxs-lookup"><span data-stu-id="058fa-137">For example, when signing in with a local account, the self-asserted technical profile named `SelfAsserted-LocalAccountSignin-Email` calls the validation technical profile named `login-NonInteractive`.</span></span> <span data-ttu-id="058fa-138">This technical profile validates the user credentials and also returns the user profile.</span><span class="sxs-lookup"><span data-stu-id="058fa-138">This technical profile validates the user credentials and also returns the user profile.</span></span> <span data-ttu-id="058fa-139">Such as 'userPrincipalName', 'displayName', 'givenName' and 'surName'.</span><span class="sxs-lookup"><span data-stu-id="058fa-139">Such as 'userPrincipalName', 'displayName', 'givenName' and 'surName'.</span></span>
- <span data-ttu-id="058fa-140">**Output the claims via output claims transformation**</span><span class="sxs-lookup"><span data-stu-id="058fa-140">**Output the claims via output claims transformation**</span></span>

<span data-ttu-id="058fa-141">In the following example, the `LocalAccountSignUpWithLogonEmail` self-asserted technical profile demonstrates the use of output claims and sets **executed-SelfAsserted-Input** to `true`.</span><span class="sxs-lookup"><span data-stu-id="058fa-141">In the following example, the `LocalAccountSignUpWithLogonEmail` self-asserted technical profile demonstrates the use of output claims and sets **executed-SelfAsserted-Input** to `true`.</span></span> <span data-ttu-id="058fa-142">The `objectId`, `authenticationSource`, `newUser` claims are output of the `AAD-UserWriteUsingLogonEmail` validation technical profile and are not shown to the user.</span><span class="sxs-lookup"><span data-stu-id="058fa-142">The `objectId`, `authenticationSource`, `newUser` claims are output of the `AAD-UserWriteUsingLogonEmail` validation technical profile and are not shown to the user.</span></span>

```XML
<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
  <DisplayName>Email signup</DisplayName>
  <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  <Metadata>
    <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
    <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
    <Item Key="language.button_continue">Create</Item>
  </Metadata>
  <CryptographicKeys>
    <Key Id="issuer_secret" StorageReferenceId="B2C_1A_TokenSigningKeyContainer" />
  </CryptographicKeys>
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="email" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="objectId" />
    <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
    <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
    <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
    <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
    <OutputClaim ClaimTypeReferenceId="authenticationSource" />
    <OutputClaim ClaimTypeReferenceId="newUser" />

    <!-- Optional claims, to be collected from the user -->
    <OutputClaim ClaimTypeReferenceId="displayName" />
    <OutputClaim ClaimTypeReferenceId="givenName" />
    <OutputClaim ClaimTypeReferenceId="surName" />
  </OutputClaims>
  <ValidationTechnicalProfiles>
    <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
  </ValidationTechnicalProfiles>
  <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
</TechnicalProfile>

```

## <a name="persist-claims"></a><span data-ttu-id="058fa-143">Persist claims</span><span class="sxs-lookup"><span data-stu-id="058fa-143">Persist claims</span></span>

<span data-ttu-id="058fa-144">If the **PersistedClaims** element is absent, the self-asserted technical profile doesn't persist the data to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="058fa-144">If the **PersistedClaims** element is absent, the self-asserted technical profile doesn't persist the data to Azure AD B2C.</span></span> <span data-ttu-id="058fa-145">Instead, a call is made to a validation technical profile that's responsible for persisting the data.</span><span class="sxs-lookup"><span data-stu-id="058fa-145">Instead, a call is made to a validation technical profile that's responsible for persisting the data.</span></span> <span data-ttu-id="058fa-146">For example, the sign-up policy uses the `LocalAccountSignUpWithLogonEmail` self-asserted technical profile to collect the new user profile.</span><span class="sxs-lookup"><span data-stu-id="058fa-146">For example, the sign-up policy uses the `LocalAccountSignUpWithLogonEmail` self-asserted technical profile to collect the new user profile.</span></span> <span data-ttu-id="058fa-147">The `LocalAccountSignUpWithLogonEmail` technical profile calls the validation technical profile to create the account in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="058fa-147">The `LocalAccountSignUpWithLogonEmail` technical profile calls the validation technical profile to create the account in Azure AD B2C.</span></span>

## <a name="validation-technical-profiles"></a><span data-ttu-id="058fa-148">Validation technical profiles</span><span class="sxs-lookup"><span data-stu-id="058fa-148">Validation technical profiles</span></span>

<span data-ttu-id="058fa-149">A validation technical profile is used for validating some or all of the output claims of the referencing technical profile.</span><span class="sxs-lookup"><span data-stu-id="058fa-149">A validation technical profile is used for validating some or all of the output claims of the referencing technical profile.</span></span> <span data-ttu-id="058fa-150">The input claims of the validation technical profile must appear in the output claims of the self-asserted technical profile.</span><span class="sxs-lookup"><span data-stu-id="058fa-150">The input claims of the validation technical profile must appear in the output claims of the self-asserted technical profile.</span></span> <span data-ttu-id="058fa-151">The validation technical profile validates the user input and can return an error to the user.</span><span class="sxs-lookup"><span data-stu-id="058fa-151">The validation technical profile validates the user input and can return an error to the user.</span></span> 

<span data-ttu-id="058fa-152">The validation technical profile can be any technical profile in the policy, such as [Azure Active Directory](active-directory-technical-profile.md) or a [REST API](restful-technical-profile.md) technical profiles.</span><span class="sxs-lookup"><span data-stu-id="058fa-152">The validation technical profile can be any technical profile in the policy, such as [Azure Active Directory](active-directory-technical-profile.md) or a [REST API](restful-technical-profile.md) technical profiles.</span></span> <span data-ttu-id="058fa-153">In the previous example, the `LocalAccountSignUpWithLogonEmail` technical profile validates that the signinName does not exist in the directory.</span><span class="sxs-lookup"><span data-stu-id="058fa-153">In the previous example, the `LocalAccountSignUpWithLogonEmail` technical profile validates that the signinName does not exist in the directory.</span></span> <span data-ttu-id="058fa-154">If not, the validation technical profile creates a local account and returns the objectId, authenticationSource, newUser.</span><span class="sxs-lookup"><span data-stu-id="058fa-154">If not, the validation technical profile creates a local account and returns the objectId, authenticationSource, newUser.</span></span> <span data-ttu-id="058fa-155">The `SelfAsserted-LocalAccountSignin-Email` technical profile calls the `login-NonInteractive` validation technical profile to validate the user credentials.</span><span class="sxs-lookup"><span data-stu-id="058fa-155">The `SelfAsserted-LocalAccountSignin-Email` technical profile calls the `login-NonInteractive` validation technical profile to validate the user credentials.</span></span>

<span data-ttu-id="058fa-156">You can also call a REST API technical profile with your business logic, overwrite input claims, or enrich user data by further integrating with corporate line-of-business application.</span><span class="sxs-lookup"><span data-stu-id="058fa-156">You can also call a REST API technical profile with your business logic, overwrite input claims, or enrich user data by further integrating with corporate line-of-business application.</span></span> <span data-ttu-id="058fa-157">For more information, see [Validation technical profile](validation-technical-profile.md)</span><span class="sxs-lookup"><span data-stu-id="058fa-157">For more information, see [Validation technical profile](validation-technical-profile.md)</span></span>

## <a name="metadata"></a><span data-ttu-id="058fa-158">Metadata</span><span class="sxs-lookup"><span data-stu-id="058fa-158">Metadata</span></span>

| <span data-ttu-id="058fa-159">Attribute</span><span class="sxs-lookup"><span data-stu-id="058fa-159">Attribute</span></span> | <span data-ttu-id="058fa-160">Required</span><span class="sxs-lookup"><span data-stu-id="058fa-160">Required</span></span> | <span data-ttu-id="058fa-161">Description</span><span class="sxs-lookup"><span data-stu-id="058fa-161">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="058fa-162">setting.showContinueButton</span><span class="sxs-lookup"><span data-stu-id="058fa-162">setting.showContinueButton</span></span> | <span data-ttu-id="058fa-163">No</span><span class="sxs-lookup"><span data-stu-id="058fa-163">No</span></span> | <span data-ttu-id="058fa-164">Displays the continue button.</span><span class="sxs-lookup"><span data-stu-id="058fa-164">Displays the continue button.</span></span> <span data-ttu-id="058fa-165">Possible values: `true` (default), or `false`</span><span class="sxs-lookup"><span data-stu-id="058fa-165">Possible values: `true` (default), or `false`</span></span> |
| <span data-ttu-id="058fa-166">setting.showCancelButton</span><span class="sxs-lookup"><span data-stu-id="058fa-166">setting.showCancelButton</span></span> | <span data-ttu-id="058fa-167">No</span><span class="sxs-lookup"><span data-stu-id="058fa-167">No</span></span> | <span data-ttu-id="058fa-168">Displays the cancel button.</span><span class="sxs-lookup"><span data-stu-id="058fa-168">Displays the cancel button.</span></span> <span data-ttu-id="058fa-169">Possible values: `true` (default), or `false`</span><span class="sxs-lookup"><span data-stu-id="058fa-169">Possible values: `true` (default), or `false`</span></span> |
| <span data-ttu-id="058fa-170">setting.operatingMode</span><span class="sxs-lookup"><span data-stu-id="058fa-170">setting.operatingMode</span></span> | <span data-ttu-id="058fa-171">No</span><span class="sxs-lookup"><span data-stu-id="058fa-171">No</span></span> | <span data-ttu-id="058fa-172">For a sign-in page, this property controls the behavior of the username field, such as input validation and error messages.</span><span class="sxs-lookup"><span data-stu-id="058fa-172">For a sign-in page, this property controls the behavior of the username field, such as input validation and error messages.</span></span> <span data-ttu-id="058fa-173">Expected values: `Username` or `Email`.</span><span class="sxs-lookup"><span data-stu-id="058fa-173">Expected values: `Username` or `Email`.</span></span> |
| <span data-ttu-id="058fa-174">ContentDefinitionReferenceId</span><span class="sxs-lookup"><span data-stu-id="058fa-174">ContentDefinitionReferenceId</span></span> | <span data-ttu-id="058fa-175">Yes</span><span class="sxs-lookup"><span data-stu-id="058fa-175">Yes</span></span> | <span data-ttu-id="058fa-176">The identifier of the [content definition](contentdefinitions.md) associated with this technical profile.</span><span class="sxs-lookup"><span data-stu-id="058fa-176">The identifier of the [content definition](contentdefinitions.md) associated with this technical profile.</span></span> |
| <span data-ttu-id="058fa-177">EnforceEmailVerification</span><span class="sxs-lookup"><span data-stu-id="058fa-177">EnforceEmailVerification</span></span> | <span data-ttu-id="058fa-178">No</span><span class="sxs-lookup"><span data-stu-id="058fa-178">No</span></span> | <span data-ttu-id="058fa-179">For sign-up or profile edit, enforces email verification.</span><span class="sxs-lookup"><span data-stu-id="058fa-179">For sign-up or profile edit, enforces email verification.</span></span> <span data-ttu-id="058fa-180">Possible values: `true` (default), or `false`.</span><span class="sxs-lookup"><span data-stu-id="058fa-180">Possible values: `true` (default), or `false`.</span></span> | 
| <span data-ttu-id="058fa-181">setting.showSignupLink</span><span class="sxs-lookup"><span data-stu-id="058fa-181">setting.showSignupLink</span></span> | <span data-ttu-id="058fa-182">No</span><span class="sxs-lookup"><span data-stu-id="058fa-182">No</span></span> | <span data-ttu-id="058fa-183">Displays the sign-up button.</span><span class="sxs-lookup"><span data-stu-id="058fa-183">Displays the sign-up button.</span></span> <span data-ttu-id="058fa-184">Possible values: `true` (default), or `false`</span><span class="sxs-lookup"><span data-stu-id="058fa-184">Possible values: `true` (default), or `false`</span></span> |
| <span data-ttu-id="058fa-185">SignUpTarget</span><span class="sxs-lookup"><span data-stu-id="058fa-185">SignUpTarget</span></span> | <span data-ttu-id="058fa-186">No</span><span class="sxs-lookup"><span data-stu-id="058fa-186">No</span></span> | <span data-ttu-id="058fa-187">The signup target exchange identifier.</span><span class="sxs-lookup"><span data-stu-id="058fa-187">The signup target exchange identifier.</span></span> <span data-ttu-id="058fa-188">When the user clicks the sign-up button, Azure AD B2C executes the specified exchange identifier.</span><span class="sxs-lookup"><span data-stu-id="058fa-188">When the user clicks the sign-up button, Azure AD B2C executes the specified exchange identifier.</span></span> |

## <a name="cryptographic-keys"></a><span data-ttu-id="058fa-189">Cryptographic keys</span><span class="sxs-lookup"><span data-stu-id="058fa-189">Cryptographic keys</span></span>

<span data-ttu-id="058fa-190">The **CryptographicKeys** element is not used.</span><span class="sxs-lookup"><span data-stu-id="058fa-190">The **CryptographicKeys** element is not used.</span></span>













