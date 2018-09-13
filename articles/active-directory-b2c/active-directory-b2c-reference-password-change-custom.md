---
title: Self-service password change in Azure Active Directory B2C | Microsoft Docs
description: A topic demonstrating how to set up self-service password change for your consumers in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 09/05/2016
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 491b3988a6581387c71b4214907e689119fcb979
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870175"
---
# <a name="azure-active-directory-b2c-configure-password-change-in-custom-policies"></a><span data-ttu-id="e6411-103">Azure Active Directory B2C: Configure password change in custom policies</span><span class="sxs-lookup"><span data-stu-id="e6411-103">Azure Active Directory B2C: Configure password change in custom policies</span></span>  
[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="e6411-104">With the password change feature, signed-in consumers (using local accounts) can change their passwords without having to prove their authenticity by email verification as described in the [self-service password reset flow.](active-directory-b2c-reference-sspr.md)</span><span class="sxs-lookup"><span data-stu-id="e6411-104">With the password change feature, signed-in consumers (using local accounts) can change their passwords without having to prove their authenticity by email verification as described in the [self-service password reset flow.](active-directory-b2c-reference-sspr.md)</span></span> <span data-ttu-id="e6411-105">If the session expires by the time the consumer gets to password change flow, user is prompted to sign in again.</span><span class="sxs-lookup"><span data-stu-id="e6411-105">If the session expires by the time the consumer gets to password change flow, user is prompted to sign in again.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e6411-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e6411-106">Prerequisites</span></span>

<span data-ttu-id="e6411-107">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6411-107">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="how-to-configure-password-change-in-custom-policy"></a><span data-ttu-id="e6411-108">How to configure password change in custom policy</span><span class="sxs-lookup"><span data-stu-id="e6411-108">How to configure password change in custom policy</span></span>

<span data-ttu-id="e6411-109">To configure password change in custom policy make the following changes in your trust framework extensions policy,</span><span class="sxs-lookup"><span data-stu-id="e6411-109">To configure password change in custom policy make the following changes in your trust framework extensions policy,</span></span> 

## <a name="define-a-claimtype-oldpassword"></a><span data-ttu-id="e6411-110">Define a ClaimType 'oldPassword'</span><span class="sxs-lookup"><span data-stu-id="e6411-110">Define a ClaimType 'oldPassword'</span></span>

<span data-ttu-id="e6411-111">The overall structure of your custom policy must include a `ClaimsSchema`and define a new `ClaimType` 'oldPassword' as below,</span><span class="sxs-lookup"><span data-stu-id="e6411-111">The overall structure of your custom policy must include a `ClaimsSchema`and define a new `ClaimType` 'oldPassword' as below,</span></span> 

```XML
  <BuildingBlocks>
    <ClaimsSchema>
      <ClaimType Id="oldPassword">
        <DisplayName>Old Password</DisplayName>
        <DataType>string</DataType>
        <UserHelpText>Enter password</UserHelpText>
        <UserInputType>Password</UserInputType>
      </ClaimType>
    </ClaimsSchema>
  </BuildingBlocks>
```

<span data-ttu-id="e6411-112">The purpose of these elements is as follows:</span><span class="sxs-lookup"><span data-stu-id="e6411-112">The purpose of these elements is as follows:</span></span>

- <span data-ttu-id="e6411-113">The `ClaimsSchema` defines which claim is being validated.</span><span class="sxs-lookup"><span data-stu-id="e6411-113">The `ClaimsSchema` defines which claim is being validated.</span></span>  <span data-ttu-id="e6411-114">In this case, the 'old password' will be validated.</span><span class="sxs-lookup"><span data-stu-id="e6411-114">In this case, the 'old password' will be validated.</span></span> 

## <a name="add-a-password-change-claims-provider-with-its-supporting-elements"></a><span data-ttu-id="e6411-115">Add a password change claims provider with its supporting elements</span><span class="sxs-lookup"><span data-stu-id="e6411-115">Add a password change claims provider with its supporting elements</span></span>

<span data-ttu-id="e6411-116">Password change claims provider will</span><span class="sxs-lookup"><span data-stu-id="e6411-116">Password change claims provider will</span></span>

1. <span data-ttu-id="e6411-117">Authenticate the user against the old password</span><span class="sxs-lookup"><span data-stu-id="e6411-117">Authenticate the user against the old password</span></span>
2. <span data-ttu-id="e6411-118">And if 'new password' matches 'confirm new password', this value is stored in B2C datastore and hence the password is successfully changed.</span><span class="sxs-lookup"><span data-stu-id="e6411-118">And if 'new password' matches 'confirm new password', this value is stored in B2C datastore and hence the password is successfully changed.</span></span> 

![img](images/passwordchange.jpg)

<span data-ttu-id="e6411-120">Add the following claims provider to your extensions policy.</span><span class="sxs-lookup"><span data-stu-id="e6411-120">Add the following claims provider to your extensions policy.</span></span> 

```XML
<ClaimsProviders>
    <ClaimsProvider>
      <DisplayName>Local Account SignIn</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="login-NonInteractive">
          <Metadata>
           <Item Key="client_id">ProxyIdentityExperienceFrameworkAppId</Item>
           <Item Key="IdTokenAudience">IdentityExperienceFrameworkAppId</Item>
          </Metadata>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="client_id" DefaultValue="ProxyIdentityExperienceFrameworkAppID" />
            <InputClaim ClaimTypeReferenceId="resource_id" PartnerClaimType="resource" DefaultValue="IdentityExperienceFrameworkAppID" />
          </InputClaims>
        </TechnicalProfile>
        <TechnicalProfile Id="login-NonInteractive-PasswordChange">
          <DisplayName>Local Account SignIn</DisplayName>
          <Protocol Name="OpenIdConnect" />
          <Metadata>
            <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">We can't seem to find your account</Item>
            <Item Key="UserMessageIfInvalidPassword">Your password is incorrect</Item>
            <Item Key="UserMessageIfOldPasswordUsed">Looks like you used an old password</Item>
            <Item Key="ProviderName">https://sts.windows.net/</Item>
            <Item Key="METADATA">https://{tenant}.b2clogin.com/{tenant}.onmicrosoft.com/.well-known/openid-configuration</Item>
            <Item Key="authorization_endpoint">https://{tenant}.b2clogin.com/{tenant}.onmicrosoft.com/oauth2/token</Item>
            <Item Key="response_types">id_token</Item>
            <Item Key="response_mode">query</Item>
            <Item Key="scope">email openid</Item>
            <Item Key="UsePolicyInRedirectUri">false</Item>
            <Item Key="HttpBinding">POST</Item>
            <Item Key="client_id">ProxyIdentityExperienceFrameworkAppId</Item>
            <Item Key="IdTokenAudience">IdentityExperienceFrameworkAppId</Item>
          </Metadata>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="signInName" PartnerClaimType="username" Required="true" />
            <InputClaim ClaimTypeReferenceId="oldPassword" PartnerClaimType="password" Required="true" />
            <InputClaim ClaimTypeReferenceId="grant_type" DefaultValue="password" />
            <InputClaim ClaimTypeReferenceId="scope" DefaultValue="openid" />
            <InputClaim ClaimTypeReferenceId="nca" PartnerClaimType="nca" DefaultValue="1" />
            <InputClaim ClaimTypeReferenceId="client_id" DefaultValue="ProxyIdentityExperienceFrameworkAppID" />
            <InputClaim ClaimTypeReferenceId="resource_id" PartnerClaimType="resource" DefaultValue="IdentityExperienceFrameworkAppID" />
          </InputClaims>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="oid" />
            <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid" />
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
            <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
            <OutputClaim ClaimTypeReferenceId="userPrincipalName" PartnerClaimType="upn" />
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
          </OutputClaims>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    <ClaimsProvider>
      <DisplayName>Local Account Password Change</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="LocalAccountWritePasswordChangeUsingObjectId">
          <DisplayName>Change password (username)</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="issuer_secret" StorageReferenceId="B2C_1A_TokenSigningKeyContainer" />
          </CryptographicKeys>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" />
          </InputClaims>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="oldPassword" Required="true" />
            <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
            <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="login-NonInteractive-PasswordChange" />
            <ValidationTechnicalProfile ReferenceId="AAD-UserWritePasswordUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
  </ClaimsProviders>
```



### <a name="add-the-application-ids-to-your-custom-policy"></a><span data-ttu-id="e6411-121">Add the application IDs to your custom policy</span><span class="sxs-lookup"><span data-stu-id="e6411-121">Add the application IDs to your custom policy</span></span>

<span data-ttu-id="e6411-122">Add the application IDs to the extensions file (`TrustFrameworkExtensions.xml`):</span><span class="sxs-lookup"><span data-stu-id="e6411-122">Add the application IDs to the extensions file (`TrustFrameworkExtensions.xml`):</span></span>

1. <span data-ttu-id="e6411-123">In the extensions file (TrustFrameworkExtensions.xml), find the element `<TechnicalProfile Id="login-NonInteractive">` and `<TechnicalProfile Id="login-NonInteractive-PasswordChange">`</span><span class="sxs-lookup"><span data-stu-id="e6411-123">In the extensions file (TrustFrameworkExtensions.xml), find the element `<TechnicalProfile Id="login-NonInteractive">` and `<TechnicalProfile Id="login-NonInteractive-PasswordChange">`</span></span>

2. <span data-ttu-id="e6411-124">Replace all instances of `IdentityExperienceFrameworkAppId` with the application ID of the Identity Experience Framework application as described in [Getting started](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6411-124">Replace all instances of `IdentityExperienceFrameworkAppId` with the application ID of the Identity Experience Framework application as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="e6411-125">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="e6411-125">Here is an example:</span></span>

   ```
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```

3. <span data-ttu-id="e6411-126">Replace all instances of `ProxyIdentityExperienceFrameworkAppId` with the application ID of the Proxy Identity Experience Framework application as described in [Getting started](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6411-126">Replace all instances of `ProxyIdentityExperienceFrameworkAppId` with the application ID of the Proxy Identity Experience Framework application as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>

4. <span data-ttu-id="e6411-127">Save your extensions file.</span><span class="sxs-lookup"><span data-stu-id="e6411-127">Save your extensions file.</span></span>



## <a name="create-a-password-change-user-journey"></a><span data-ttu-id="e6411-128">Create a password change user journey</span><span class="sxs-lookup"><span data-stu-id="e6411-128">Create a password change user journey</span></span>

```XML
 <UserJourneys>
    <UserJourney Id="PasswordChange">
      <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
          <ClaimsProviderSelections>
            <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
          </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
          <ClaimsExchanges>
            <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
          </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
          <ClaimsExchanges>
            <ClaimsExchange Id="NewCredentials" TechnicalProfileReferenceId="LocalAccountWritePasswordChangeUsingObjectId" />
          </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
      </OrchestrationSteps>
      <ClientDefinition ReferenceId="DefaultWeb" />
    </UserJourney>
  </UserJourneys>
```

<span data-ttu-id="e6411-129">You are done modifying the extension file.</span><span class="sxs-lookup"><span data-stu-id="e6411-129">You are done modifying the extension file.</span></span> <span data-ttu-id="e6411-130">Save and upload this file.</span><span class="sxs-lookup"><span data-stu-id="e6411-130">Save and upload this file.</span></span> <span data-ttu-id="e6411-131">Ensure that all validations succeed.</span><span class="sxs-lookup"><span data-stu-id="e6411-131">Ensure that all validations succeed.</span></span>



## <a name="create-a-relying-party-rp-file"></a><span data-ttu-id="e6411-132">Create a relying party (RP) file</span><span class="sxs-lookup"><span data-stu-id="e6411-132">Create a relying party (RP) file</span></span>

<span data-ttu-id="e6411-133">Next, update the relying party (RP) file that initiates the user journey that you created:</span><span class="sxs-lookup"><span data-stu-id="e6411-133">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="e6411-134">Make a copy of ProfileEdit.xml in your working directory.</span><span class="sxs-lookup"><span data-stu-id="e6411-134">Make a copy of ProfileEdit.xml in your working directory.</span></span> <span data-ttu-id="e6411-135">Then, rename it (for example, PasswordChange.xml).</span><span class="sxs-lookup"><span data-stu-id="e6411-135">Then, rename it (for example, PasswordChange.xml).</span></span>
2. <span data-ttu-id="e6411-136">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span><span class="sxs-lookup"><span data-stu-id="e6411-136">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="e6411-137">This is the name of your policy (for example, PasswordChange).</span><span class="sxs-lookup"><span data-stu-id="e6411-137">This is the name of your policy (for example, PasswordChange).</span></span>
3. <span data-ttu-id="e6411-138">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, PasswordChange).</span><span class="sxs-lookup"><span data-stu-id="e6411-138">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, PasswordChange).</span></span>
4. <span data-ttu-id="e6411-139">Save your changes, and then upload the file.</span><span class="sxs-lookup"><span data-stu-id="e6411-139">Save your changes, and then upload the file.</span></span>
5. <span data-ttu-id="e6411-140">To test the custom policy that you uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span><span class="sxs-lookup"><span data-stu-id="e6411-140">To test the custom policy that you uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span>




## <a name="link-to-password-change-sample-policy"></a><span data-ttu-id="e6411-141">Link to password change sample policy</span><span class="sxs-lookup"><span data-stu-id="e6411-141">Link to password change sample policy</span></span>

<span data-ttu-id="e6411-142">You can find the sample policy [here](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/password-change).</span><span class="sxs-lookup"><span data-stu-id="e6411-142">You can find the sample policy [here](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/password-change).</span></span> 










