---
title: Modify sign up in custom policies and configure self asserted provider | Microsoft Docs
description: A walkthrough on adding claims to sign up and configure the user input
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/29/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 37492e22b5615ae0b266bc8b2bb6d8f039fdaabe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857830"
---
# <a name="azure-active-directory-b2c-modify-sign-up-to-add-new-claims-and-configure-user-input"></a><span data-ttu-id="11b08-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span><span class="sxs-lookup"><span data-stu-id="11b08-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="11b08-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span><span class="sxs-lookup"><span data-stu-id="11b08-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span></span>  <span data-ttu-id="11b08-105">You will configure the entry as a dropdown, and define if it is required.</span><span class="sxs-lookup"><span data-stu-id="11b08-105">You will configure the entry as a dropdown, and define if it is required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11b08-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="11b08-106">Prerequisites</span></span>

* <span data-ttu-id="11b08-107">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="11b08-107">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="11b08-108">Test the signup/signin user journey to signup a new local account before proceeding.</span><span class="sxs-lookup"><span data-stu-id="11b08-108">Test the signup/signin user journey to signup a new local account before proceeding.</span></span>


<span data-ttu-id="11b08-109">Gathering initial data from your users is achieved via signup/signin.</span><span class="sxs-lookup"><span data-stu-id="11b08-109">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="11b08-110">Additional claims can be gathered later via profile edit user journeys.</span><span class="sxs-lookup"><span data-stu-id="11b08-110">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="11b08-111">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="11b08-111">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="11b08-112">The steps below apply anytime this provider is used.</span><span class="sxs-lookup"><span data-stu-id="11b08-112">The steps below apply anytime this provider is used.</span></span>


## <a name="define-the-claim-its-display-name-and-the-user-input-type"></a><span data-ttu-id="11b08-113">Define the claim, its display name and the user input type</span><span class="sxs-lookup"><span data-stu-id="11b08-113">Define the claim, its display name and the user input type</span></span>
<span data-ttu-id="11b08-114">Lets ask the user for their city.</span><span class="sxs-lookup"><span data-stu-id="11b08-114">Lets ask the user for their city.</span></span>  <span data-ttu-id="11b08-115">Add the following element to the `<ClaimsSchema>` element in the TrustFrameworkBase policy file:</span><span class="sxs-lookup"><span data-stu-id="11b08-115">Add the following element to the `<ClaimsSchema>` element in the TrustFrameworkBase policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="11b08-116">There are additional choices you can make here to customize the claim.</span><span class="sxs-lookup"><span data-stu-id="11b08-116">There are additional choices you can make here to customize the claim.</span></span>  <span data-ttu-id="11b08-117">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span><span class="sxs-lookup"><span data-stu-id="11b08-117">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="11b08-118">This guide will be published soon in the reference section.</span><span class="sxs-lookup"><span data-stu-id="11b08-118">This guide will be published soon in the reference section.</span></span>

* <span data-ttu-id="11b08-119">`<DisplayName>` is a string that defines the user-facing *label*</span><span class="sxs-lookup"><span data-stu-id="11b08-119">`<DisplayName>` is a string that defines the user-facing *label*</span></span>

* <span data-ttu-id="11b08-120">`<UserHelpText>` helps the user understand what is required</span><span class="sxs-lookup"><span data-stu-id="11b08-120">`<UserHelpText>` helps the user understand what is required</span></span>

* <span data-ttu-id="11b08-121">`<UserInputType>` has the following four options highlighted below:</span><span class="sxs-lookup"><span data-stu-id="11b08-121">`<UserInputType>` has the following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="11b08-122">`RadioSingleSelectduration` - Enforces a single selection.</span><span class="sxs-lookup"><span data-stu-id="11b08-122">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * <span data-ttu-id="11b08-123">`DropdownSingleSelect` - Allows the selection of only valid value.</span><span class="sxs-lookup"><span data-stu-id="11b08-123">`DropdownSingleSelect` - Allows the selection of only valid value.</span></span>

![Screen shot of dropdown option](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* <span data-ttu-id="11b08-125">`CheckboxMultiSelect` Allows for the selection of one or more values.</span><span class="sxs-lookup"><span data-stu-id="11b08-125">`CheckboxMultiSelect` Allows for the selection of one or more values.</span></span>

![Screenshot of multiselect option](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-the-claim-to-the-sign-upsign-in-user-journey"></a><span data-ttu-id="11b08-127">Add the claim to the sign up/sign in user journey</span><span class="sxs-lookup"><span data-stu-id="11b08-127">Add the claim to the sign up/sign in user journey</span></span>

1. <span data-ttu-id="11b08-128">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span><span class="sxs-lookup"><span data-stu-id="11b08-128">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="11b08-129">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="11b08-129">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span></span>

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
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
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. <span data-ttu-id="11b08-130">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span><span class="sxs-lookup"><span data-stu-id="11b08-130">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span></span> <span data-ttu-id="11b08-131">You may skip this step if you prefer not to persist the claim in the directory for future use.</span><span class="sxs-lookup"><span data-stu-id="11b08-131">You may skip this step if you prefer not to persist the claim in the directory for future use.</span></span>

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. <span data-ttu-id="11b08-132">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="11b08-132">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for the provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. <span data-ttu-id="11b08-133">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span><span class="sxs-lookup"><span data-stu-id="11b08-133">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span></span>

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="11b08-134">Test the custom policy using "Run Now"</span><span class="sxs-lookup"><span data-stu-id="11b08-134">Test the custom policy using "Run Now"</span></span>

1. <span data-ttu-id="11b08-135">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span><span class="sxs-lookup"><span data-stu-id="11b08-135">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="11b08-136">Select the custom policy that you uploaded, and click the **Run now** button.</span><span class="sxs-lookup"><span data-stu-id="11b08-136">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="11b08-137">You should be able to sign up using an email address.</span><span class="sxs-lookup"><span data-stu-id="11b08-137">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="11b08-138">The signup screen in test mode should look similar to this:</span><span class="sxs-lookup"><span data-stu-id="11b08-138">The signup screen in test mode should look similar to this:</span></span>

![Screenshot of modified sign-up option](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="11b08-140">The token back to your application will now include the `city` claim as shown below</span><span class="sxs-lookup"><span data-stu-id="11b08-140">The token back to your application will now include the `city` claim as shown below</span></span>
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://contoso.b2clogin.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="11b08-141">Optional: Remove email verification from signup journey</span><span class="sxs-lookup"><span data-stu-id="11b08-141">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="11b08-142">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="11b08-142">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="11b08-143">The email address will be required but not verified, unless “Required” = true is removed.</span><span class="sxs-lookup"><span data-stu-id="11b08-143">The email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="11b08-144">Carefully consider if this option is right for your use cases!</span><span class="sxs-lookup"><span data-stu-id="11b08-144">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="11b08-145">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span><span class="sxs-lookup"><span data-stu-id="11b08-145">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="11b08-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="11b08-146">Next steps</span></span>

<span data-ttu-id="11b08-147">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span><span class="sxs-lookup"><span data-stu-id="11b08-147">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span></span> <span data-ttu-id="11b08-148">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span><span class="sxs-lookup"><span data-stu-id="11b08-148">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
