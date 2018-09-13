---
title: Define an Azure Active Directory technical profile in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define an Azure Active Directory technical profile in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: cf7b051703e01493f365c1850ab815747321230b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867956"
---
# <a name="define-an-azure-active-directory-technical-profile-in-an-azure-active-directory-b2c-custom-policy"></a><span data-ttu-id="4d359-103">Define an Azure Active Directory technical profile in an Azure Active Directory B2C custom policy</span><span class="sxs-lookup"><span data-stu-id="4d359-103">Define an Azure Active Directory technical profile in an Azure Active Directory B2C custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="4d359-104">Azure Active Directory (Azure AD) B2C provides support for the Azure Active Directory user management.</span><span class="sxs-lookup"><span data-stu-id="4d359-104">Azure Active Directory (Azure AD) B2C provides support for the Azure Active Directory user management.</span></span> <span data-ttu-id="4d359-105">This article describes the specifics of a technical profile for interacting with a claims provider that supports this standardized protocol.</span><span class="sxs-lookup"><span data-stu-id="4d359-105">This article describes the specifics of a technical profile for interacting with a claims provider that supports this standardized protocol.</span></span>

## <a name="protocol"></a><span data-ttu-id="4d359-106">Protocol</span><span class="sxs-lookup"><span data-stu-id="4d359-106">Protocol</span></span>

<span data-ttu-id="4d359-107">The **Name** attribute of the **Protocol** element needs to be set to `Proprietary`.</span><span class="sxs-lookup"><span data-stu-id="4d359-107">The **Name** attribute of the **Protocol** element needs to be set to `Proprietary`.</span></span> <span data-ttu-id="4d359-108">The **handler** attribute must contain the fully qualified name of the protocol handler assembly `Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`.</span><span class="sxs-lookup"><span data-stu-id="4d359-108">The **handler** attribute must contain the fully qualified name of the protocol handler assembly `Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`.</span></span>

<span data-ttu-id="4d359-109">All Azure AD technical profiles include the **AAD-Common** technical profile.</span><span class="sxs-lookup"><span data-stu-id="4d359-109">All Azure AD technical profiles include the **AAD-Common** technical profile.</span></span> <span data-ttu-id="4d359-110">The following technical profiles don't specify the protocol because the protocol is configured in the **AAD-Common** technical profile:</span><span class="sxs-lookup"><span data-stu-id="4d359-110">The following technical profiles don't specify the protocol because the protocol is configured in the **AAD-Common** technical profile:</span></span>

- <span data-ttu-id="4d359-111">**AAD-UserReadUsingAlternativeSecurityId** and **AAD-UserReadUsingAlternativeSecurityId-NoError** - Look up a social account in the directory.</span><span class="sxs-lookup"><span data-stu-id="4d359-111">**AAD-UserReadUsingAlternativeSecurityId** and **AAD-UserReadUsingAlternativeSecurityId-NoError** - Look up a social account in the directory.</span></span>
- <span data-ttu-id="4d359-112">**AAD-UserWriteUsingAlternativeSecurityId** - Create a new social account.</span><span class="sxs-lookup"><span data-stu-id="4d359-112">**AAD-UserWriteUsingAlternativeSecurityId** - Create a new social account.</span></span>
- <span data-ttu-id="4d359-113">**AAD-UserReadUsingEmailAddress** - Look up a local account in the directory.</span><span class="sxs-lookup"><span data-stu-id="4d359-113">**AAD-UserReadUsingEmailAddress** - Look up a local account in the directory.</span></span> 
- <span data-ttu-id="4d359-114">**AAD-UserWriteUsingLogonEmail** - Create a new local account.</span><span class="sxs-lookup"><span data-stu-id="4d359-114">**AAD-UserWriteUsingLogonEmail** - Create a new local account.</span></span>
- <span data-ttu-id="4d359-115">**AAD-UserWritePasswordUsingObjectId** - Update a password of a local account.</span><span class="sxs-lookup"><span data-stu-id="4d359-115">**AAD-UserWritePasswordUsingObjectId** - Update a password of a local account.</span></span>
- <span data-ttu-id="4d359-116">**AAD-UserWriteProfileUsingObjectId** - Update a user profile of a local or social account.</span><span class="sxs-lookup"><span data-stu-id="4d359-116">**AAD-UserWriteProfileUsingObjectId** - Update a user profile of a local or social account.</span></span>
- <span data-ttu-id="4d359-117">**AAD-UserReadUsingObjectId** - Read a user profile of a local or social account.</span><span class="sxs-lookup"><span data-stu-id="4d359-117">**AAD-UserReadUsingObjectId** - Read a user profile of a local or social account.</span></span>
- <span data-ttu-id="4d359-118">**AAD-UserWritePhoneNumberUsingObjectId** - Write the MFA phone number of a local or social account</span><span class="sxs-lookup"><span data-stu-id="4d359-118">**AAD-UserWritePhoneNumberUsingObjectId** - Write the MFA phone number of a local or social account</span></span>

<span data-ttu-id="4d359-119">The following example shows the **AAD-Common** technical profile:</span><span class="sxs-lookup"><span data-stu-id="4d359-119">The following example shows the **AAD-Common** technical profile:</span></span>

```XML
<TechnicalProfile Id="AAD-Common">
  <DisplayName>Azure Active Directory</DisplayName>
  <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />

  <CryptographicKeys>
    <Key Id="issuer_secret" StorageReferenceId="B2C_1A_TokenSigningKeyContainer" />
  </CryptographicKeys>

  <!-- We need this here to suppress the SelfAsserted provider from invoking SSO on validation profiles. -->
  <IncludeInSso>false</IncludeInSso>
  <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
</TechnicalProfile>
```

## <a name="input-claims"></a><span data-ttu-id="4d359-120">Input claims</span><span class="sxs-lookup"><span data-stu-id="4d359-120">Input claims</span></span>

<span data-ttu-id="4d359-121">The following technical profiles include **InputClaims** for social and local accounts:</span><span class="sxs-lookup"><span data-stu-id="4d359-121">The following technical profiles include **InputClaims** for social and local accounts:</span></span>

- <span data-ttu-id="4d359-122">The social account technical profiles **AAD-UserReadUsingAlternativeSecurityId** and **AAD-UserWriteUsingAlternativeSecurityId** includes the **AlternativeSecurityId** claim.</span><span class="sxs-lookup"><span data-stu-id="4d359-122">The social account technical profiles **AAD-UserReadUsingAlternativeSecurityId** and **AAD-UserWriteUsingAlternativeSecurityId** includes the **AlternativeSecurityId** claim.</span></span> <span data-ttu-id="4d359-123">This claim contains the social account user identifier.</span><span class="sxs-lookup"><span data-stu-id="4d359-123">This claim contains the social account user identifier.</span></span>
- <span data-ttu-id="4d359-124">The local account technical profiles **AAD-UserReadUsingEmailAddress** and **AAD-UserWriteUsingLogonEmail** includes the **email** claim.</span><span class="sxs-lookup"><span data-stu-id="4d359-124">The local account technical profiles **AAD-UserReadUsingEmailAddress** and **AAD-UserWriteUsingLogonEmail** includes the **email** claim.</span></span> <span data-ttu-id="4d359-125">This claim contains the sign-in name of the local account.</span><span class="sxs-lookup"><span data-stu-id="4d359-125">This claim contains the sign-in name of the local account.</span></span>
- <span data-ttu-id="4d359-126">The unified (local and social) technical profiles **AAD-UserReadUsingObjectId**, **AAD-UserWritePasswordUsingObjectId**, **AAD-UserWriteProfileUsingObjectId**, and **AAD-UserWritePhoneNumberUsingObjectId** includes the **objectId** claim.</span><span class="sxs-lookup"><span data-stu-id="4d359-126">The unified (local and social) technical profiles **AAD-UserReadUsingObjectId**, **AAD-UserWritePasswordUsingObjectId**, **AAD-UserWriteProfileUsingObjectId**, and **AAD-UserWritePhoneNumberUsingObjectId** includes the **objectId** claim.</span></span> <span data-ttu-id="4d359-127">The unique identifier of an account.</span><span class="sxs-lookup"><span data-stu-id="4d359-127">The unique identifier of an account.</span></span>

<span data-ttu-id="4d359-128">The **InputClaimsTransformations** element may contain a collection of **InputClaimsTransformation** elements that are used to modify the input claims or generate new ones.</span><span class="sxs-lookup"><span data-stu-id="4d359-128">The **InputClaimsTransformations** element may contain a collection of **InputClaimsTransformation** elements that are used to modify the input claims or generate new ones.</span></span>

## <a name="output-claims"></a><span data-ttu-id="4d359-129">Output claims</span><span class="sxs-lookup"><span data-stu-id="4d359-129">Output claims</span></span>

<span data-ttu-id="4d359-130">The **OutputClaims** element contains a list of claims returned by the Azure AD technical profile.</span><span class="sxs-lookup"><span data-stu-id="4d359-130">The **OutputClaims** element contains a list of claims returned by the Azure AD technical profile.</span></span> <span data-ttu-id="4d359-131">You may need to map the name of the claim defined in your policy to the name defined in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4d359-131">You may need to map the name of the claim defined in your policy to the name defined in Azure Active Directory.</span></span> <span data-ttu-id="4d359-132">You can also include claims that aren't returned by the Azure Active Directory, as long as you set the `DefaultValue` attribute.</span><span class="sxs-lookup"><span data-stu-id="4d359-132">You can also include claims that aren't returned by the Azure Active Directory, as long as you set the `DefaultValue` attribute.</span></span>

<span data-ttu-id="4d359-133">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span><span class="sxs-lookup"><span data-stu-id="4d359-133">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.</span></span>

<span data-ttu-id="4d359-134">For example, the **AAD-UserWriteUsingLogonEmail** technical profile creates a local account and returns the following claims:</span><span class="sxs-lookup"><span data-stu-id="4d359-134">For example, the **AAD-UserWriteUsingLogonEmail** technical profile creates a local account and returns the following claims:</span></span>

- <span data-ttu-id="4d359-135">**objectId**, which is identifier of the new account</span><span class="sxs-lookup"><span data-stu-id="4d359-135">**objectId**, which is identifier of the new account</span></span>
- <span data-ttu-id="4d359-136">**newUser**, which indicates whether the user is new</span><span class="sxs-lookup"><span data-stu-id="4d359-136">**newUser**, which indicates whether the user is new</span></span>
- <span data-ttu-id="4d359-137">**authenticationSource**, which sets authentication to `localAccountAuthentication`</span><span class="sxs-lookup"><span data-stu-id="4d359-137">**authenticationSource**, which sets authentication to `localAccountAuthentication`</span></span>
- <span data-ttu-id="4d359-138">**userPrincipalName**, which is the user principal name of the new account</span><span class="sxs-lookup"><span data-stu-id="4d359-138">**userPrincipalName**, which is the user principal name of the new account</span></span>
- <span data-ttu-id="4d359-139">**signInNames.emailAddress**, which is the account sign-in name, similar to the **email** input claim</span><span class="sxs-lookup"><span data-stu-id="4d359-139">**signInNames.emailAddress**, which is the account sign-in name, similar to the **email** input claim</span></span>

```xml
<OutputClaims>
  <OutputClaim ClaimTypeReferenceId="objectId" />
  <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
  <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
  <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
  <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
</OutputClaims>
```

## <a name="persistedclaims"></a><span data-ttu-id="4d359-140">PersistedClaims</span><span class="sxs-lookup"><span data-stu-id="4d359-140">PersistedClaims</span></span>

<span data-ttu-id="4d359-141">The **PersistedClaims** element contains all of the values that should be persisted by Azure AD with possible mapping information between a claim type already defined in the ClaimsSchema section in the policy and the Azure AD attribute name.</span><span class="sxs-lookup"><span data-stu-id="4d359-141">The **PersistedClaims** element contains all of the values that should be persisted by Azure AD with possible mapping information between a claim type already defined in the ClaimsSchema section in the policy and the Azure AD attribute name.</span></span> 

<span data-ttu-id="4d359-142">The **AAD-UserWriteUsingLogonEmail** technical profile, which creates new local account, persists following claims:</span><span class="sxs-lookup"><span data-stu-id="4d359-142">The **AAD-UserWriteUsingLogonEmail** technical profile, which creates new local account, persists following claims:</span></span>

```XML
  <PersistedClaims>
    <!-- Required claims -->
    <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
    <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password"/>
    <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
    <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />

    <!-- Optional claims. -->
    <PersistedClaim ClaimTypeReferenceId="givenName" />
    <PersistedClaim ClaimTypeReferenceId="surname" />
  </PersistedClaims>
```

<span data-ttu-id="4d359-143">The name of the claim is the name of the Azure AD attribute unless the **PartnerClaimType** attribute is specified, which contains the Azure AD attribute name.</span><span class="sxs-lookup"><span data-stu-id="4d359-143">The name of the claim is the name of the Azure AD attribute unless the **PartnerClaimType** attribute is specified, which contains the Azure AD attribute name.</span></span>

## <a name="requirements-of-an-operation"></a><span data-ttu-id="4d359-144">Requirements of an operation</span><span class="sxs-lookup"><span data-stu-id="4d359-144">Requirements of an operation</span></span>

- <span data-ttu-id="4d359-145">There must be exactly one **InputClaim** element in the claims bag for all Azure AD technical profiles.</span><span class="sxs-lookup"><span data-stu-id="4d359-145">There must be exactly one **InputClaim** element in the claims bag for all Azure AD technical profiles.</span></span> 
- <span data-ttu-id="4d359-146">If the operation is `Write` or `DeleteClaims`, then it must also appear in a **PersistedClaims** element.</span><span class="sxs-lookup"><span data-stu-id="4d359-146">If the operation is `Write` or `DeleteClaims`, then it must also appear in a **PersistedClaims** element.</span></span>
- <span data-ttu-id="4d359-147">The value of the **userPrincipalName** claim must be in the format of `user@tenant.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="4d359-147">The value of the **userPrincipalName** claim must be in the format of `user@tenant.onmicrosoft.com`.</span></span>
- <span data-ttu-id="4d359-148">The **displayName** claim is required and cannot be an empty string.</span><span class="sxs-lookup"><span data-stu-id="4d359-148">The **displayName** claim is required and cannot be an empty string.</span></span>

## <a name="azure-ad-technical-provider-operations"></a><span data-ttu-id="4d359-149">Azure AD technical provider operations</span><span class="sxs-lookup"><span data-stu-id="4d359-149">Azure AD technical provider operations</span></span>

### <a name="read"></a><span data-ttu-id="4d359-150">Read</span><span class="sxs-lookup"><span data-stu-id="4d359-150">Read</span></span>

<span data-ttu-id="4d359-151">The **Read** operation reads data about a single user account.</span><span class="sxs-lookup"><span data-stu-id="4d359-151">The **Read** operation reads data about a single user account.</span></span> <span data-ttu-id="4d359-152">To read user data, you need to provide a key as an input claim, such as **objectId**, **userPrincipalName**, **signInNames** (any type, user name and email-based account) or **alternativeSecurityId**.</span><span class="sxs-lookup"><span data-stu-id="4d359-152">To read user data, you need to provide a key as an input claim, such as **objectId**, **userPrincipalName**, **signInNames** (any type, user name and email-based account) or **alternativeSecurityId**.</span></span>  

<span data-ttu-id="4d359-153">The following technical profile reads data about a user account using the user's objectId:</span><span class="sxs-lookup"><span data-stu-id="4d359-153">The following technical profile reads data about a user account using the user's objectId:</span></span>

```XML
<TechnicalProfile Id="AAD-UserReadUsingObjectId">
  <Metadata>
    <Item Key="Operation">Read</Item>
    <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
  </Metadata>
  <IncludeInSso>false</IncludeInSso>
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
  </InputClaims>
  <OutputClaims>

    <!-- Required claims -->
    <OutputClaim ClaimTypeReferenceId="strongAuthenticationPhoneNumber" />

    <!-- Optional claims -->
    <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    <OutputClaim ClaimTypeReferenceId="displayName" />
    <OutputClaim ClaimTypeReferenceId="otherMails" />
    <OutputClaim ClaimTypeReferenceId="givenName" />
    <OutputClaim ClaimTypeReferenceId="surname" />
  </OutputClaims>
  <IncludeTechnicalProfile ReferenceId="AAD-Common" />
</TechnicalProfile>
```

### <a name="write"></a><span data-ttu-id="4d359-154">Write</span><span class="sxs-lookup"><span data-stu-id="4d359-154">Write</span></span>

<span data-ttu-id="4d359-155">The **Write** operation creates or updates a single user account.</span><span class="sxs-lookup"><span data-stu-id="4d359-155">The **Write** operation creates or updates a single user account.</span></span> <span data-ttu-id="4d359-156">To write a user account, you need to provide a key as an input claim, such as **objectId**, **userPrincipalName**, **signInNames.emailAddress**, or **alternativeSecurityId**.</span><span class="sxs-lookup"><span data-stu-id="4d359-156">To write a user account, you need to provide a key as an input claim, such as **objectId**, **userPrincipalName**, **signInNames.emailAddress**, or **alternativeSecurityId**.</span></span>  

<span data-ttu-id="4d359-157">The following technical profile creates new social account:</span><span class="sxs-lookup"><span data-stu-id="4d359-157">The following technical profile creates new social account:</span></span>

```XML
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
  <Metadata>
    <Item Key="Operation">Write</Item>
    <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    <Item Key="UserMessageIfClaimsPrincipalAlreadyExists">You are already registered, please press the back button and sign in instead.</Item>
  </Metadata>
  <IncludeInSso>false</IncludeInSso>
  <InputClaimsTransformations>
    <InputClaimsTransformation ReferenceId="CreateOtherMailsFromEmail" />
  </InputClaimsTransformations>
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="AlternativeSecurityId" PartnerClaimType="alternativeSecurityId" Required="true" />
  </InputClaims>
  <PersistedClaims>
    <!-- Required claims -->
    <PersistedClaim ClaimTypeReferenceId="alternativeSecurityId" />
    <PersistedClaim ClaimTypeReferenceId="userPrincipalName" />
    <PersistedClaim ClaimTypeReferenceId="mailNickName" DefaultValue="unknown" />
    <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />

    <!-- Optional claims -->
    <PersistedClaim ClaimTypeReferenceId="otherMails" />
    <PersistedClaim ClaimTypeReferenceId="givenName" />
    <PersistedClaim ClaimTypeReferenceId="surname" />
  </PersistedClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="objectId" />
    <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
    <OutputClaim ClaimTypeReferenceId="otherMails" />
  </OutputClaims>
  <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
</TechnicalProfile>
```

### <a name="deleteclaims"></a><span data-ttu-id="4d359-158">DeleteClaims</span><span class="sxs-lookup"><span data-stu-id="4d359-158">DeleteClaims</span></span>

<span data-ttu-id="4d359-159">The **DeleteClaims** operation clears the information from a provided list of claims.</span><span class="sxs-lookup"><span data-stu-id="4d359-159">The **DeleteClaims** operation clears the information from a provided list of claims.</span></span> <span data-ttu-id="4d359-160">To delete information from claims, you need to provide a key as an input claim, such as **objectId**, **userPrincipalName**, **signInNames.emailAddress** or **alternativeSecurityId**.</span><span class="sxs-lookup"><span data-stu-id="4d359-160">To delete information from claims, you need to provide a key as an input claim, such as **objectId**, **userPrincipalName**, **signInNames.emailAddress** or **alternativeSecurityId**.</span></span>  

<span data-ttu-id="4d359-161">The following technical profile deletes claims:</span><span class="sxs-lookup"><span data-stu-id="4d359-161">The following technical profile deletes claims:</span></span>

```XML
<TechnicalProfile Id="AAD-DeleteClaimsUsingObjectId">
  <Metadata>
    <Item Key="Operation">DeleteClaims</Item>
  </Metadata>
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
  </InputClaims>
  <PersistedClaims>
    <PersistedClaim ClaimTypeReferenceId="objectId" />
    <PersistedClaim ClaimTypeReferenceId="Verified.strongAuthenticationPhoneNumber" PartnerClaimType="strongAuthenticationPhoneNumber" />
  </PersistedClaims>
  <OutputClaims />
  <IncludeTechnicalProfile ReferenceId="AAD-Common" />
</TechnicalProfile>
```

### <a name="deleteclaimsprincipal"></a><span data-ttu-id="4d359-162">DeleteClaimsPrincipal</span><span class="sxs-lookup"><span data-stu-id="4d359-162">DeleteClaimsPrincipal</span></span>

<span data-ttu-id="4d359-163">The **DeleteClaimsPrincipal** operation deletes a single user account from the directory.</span><span class="sxs-lookup"><span data-stu-id="4d359-163">The **DeleteClaimsPrincipal** operation deletes a single user account from the directory.</span></span> <span data-ttu-id="4d359-164">To delete a user account, you need to provide a key as an input claim, such as **objectId**, **userPrincipalName**, **signInNames.emailAddress** or **alternativeSecurityId**.</span><span class="sxs-lookup"><span data-stu-id="4d359-164">To delete a user account, you need to provide a key as an input claim, such as **objectId**, **userPrincipalName**, **signInNames.emailAddress** or **alternativeSecurityId**.</span></span>  

<span data-ttu-id="4d359-165">The following technical profile deletes a user account from the directory using the user principal name:</span><span class="sxs-lookup"><span data-stu-id="4d359-165">The following technical profile deletes a user account from the directory using the user principal name:</span></span>

```XML
<TechnicalProfile Id="AAD-DeleteUserUsingObjectId">
  <Metadata>
    <Item Key="Operation">DeleteClaimsPrincipal</Item>
  </Metadata>
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
  </InputClaims>
  <OutputClaims/>
  <IncludeTechnicalProfile ReferenceId="AAD-Common" />
</TechnicalProfile>
```

<span data-ttu-id="4d359-166">The following technical profile deletes a social user account using **alternativeSecurityId**:</span><span class="sxs-lookup"><span data-stu-id="4d359-166">The following technical profile deletes a social user account using **alternativeSecurityId**:</span></span>

```XML
<TechnicalProfile Id="AAD-DeleteUserUsingAlternativeSecurityId">
  <Metadata>
    <Item Key="Operation">DeleteClaimsPrincipal</Item>
  </Metadata>
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="alternativeSecurityId" Required="true" />
  </InputClaims>
  <OutputClaims/>
  <IncludeTechnicalProfile ReferenceId="AAD-Common" />
</TechnicalProfile>
```
## <a name="metadata"></a><span data-ttu-id="4d359-167">Metadata</span><span class="sxs-lookup"><span data-stu-id="4d359-167">Metadata</span></span>

| <span data-ttu-id="4d359-168">Attribute</span><span class="sxs-lookup"><span data-stu-id="4d359-168">Attribute</span></span> | <span data-ttu-id="4d359-169">Required</span><span class="sxs-lookup"><span data-stu-id="4d359-169">Required</span></span> | <span data-ttu-id="4d359-170">Description</span><span class="sxs-lookup"><span data-stu-id="4d359-170">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="4d359-171">Operation</span><span class="sxs-lookup"><span data-stu-id="4d359-171">Operation</span></span> | <span data-ttu-id="4d359-172">Yes</span><span class="sxs-lookup"><span data-stu-id="4d359-172">Yes</span></span> | <span data-ttu-id="4d359-173">The operation to be performed.</span><span class="sxs-lookup"><span data-stu-id="4d359-173">The operation to be performed.</span></span> <span data-ttu-id="4d359-174">Possible values: `Read`, `Write`, `DeleteClaims`, or `DeleteClaimsPrincipal`.</span><span class="sxs-lookup"><span data-stu-id="4d359-174">Possible values: `Read`, `Write`, `DeleteClaims`, or `DeleteClaimsPrincipal`.</span></span> | 
| <span data-ttu-id="4d359-175">RaiseErrorIfClaimsPrincipalDoesNotExist</span><span class="sxs-lookup"><span data-stu-id="4d359-175">RaiseErrorIfClaimsPrincipalDoesNotExist</span></span> | <span data-ttu-id="4d359-176">No</span><span class="sxs-lookup"><span data-stu-id="4d359-176">No</span></span> | <span data-ttu-id="4d359-177">Raise an error if the user object does not exist in the directory.</span><span class="sxs-lookup"><span data-stu-id="4d359-177">Raise an error if the user object does not exist in the directory.</span></span> <span data-ttu-id="4d359-178">Possible values: `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="4d359-178">Possible values: `true` or `false`.</span></span> | 
| <span data-ttu-id="4d359-179">UserMessageIfClaimsPrincipalDoesNotExist</span><span class="sxs-lookup"><span data-stu-id="4d359-179">UserMessageIfClaimsPrincipalDoesNotExist</span></span> | <span data-ttu-id="4d359-180">No</span><span class="sxs-lookup"><span data-stu-id="4d359-180">No</span></span> | <span data-ttu-id="4d359-181">If an error is to be raised (see the RaiseErrorIfClaimsPrincipalDoesNotExist attribute description), specify the message to show to the user if user object does not exist.</span><span class="sxs-lookup"><span data-stu-id="4d359-181">If an error is to be raised (see the RaiseErrorIfClaimsPrincipalDoesNotExist attribute description), specify the message to show to the user if user object does not exist.</span></span> <span data-ttu-id="4d359-182">The value can be [localized](localization.md).</span><span class="sxs-lookup"><span data-stu-id="4d359-182">The value can be [localized](localization.md).</span></span>| 
| <span data-ttu-id="4d359-183">RaiseErrorIfClaimsPrincipalAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="4d359-183">RaiseErrorIfClaimsPrincipalAlreadyExists</span></span> | <span data-ttu-id="4d359-184">No</span><span class="sxs-lookup"><span data-stu-id="4d359-184">No</span></span> | <span data-ttu-id="4d359-185">Raise an error if the user object already exists.</span><span class="sxs-lookup"><span data-stu-id="4d359-185">Raise an error if the user object already exists.</span></span> <span data-ttu-id="4d359-186">Possible values: `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="4d359-186">Possible values: `true` or `false`.</span></span>| 
| <span data-ttu-id="4d359-187">UserMessageIfClaimsPrincipalAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="4d359-187">UserMessageIfClaimsPrincipalAlreadyExists</span></span> | <span data-ttu-id="4d359-188">No</span><span class="sxs-lookup"><span data-stu-id="4d359-188">No</span></span> | <span data-ttu-id="4d359-189">If an error is to be raised (see RaiseErrorIfClaimsPrincipalAlreadyExists attribute description), specify the message to show to the user if user object already exists.</span><span class="sxs-lookup"><span data-stu-id="4d359-189">If an error is to be raised (see RaiseErrorIfClaimsPrincipalAlreadyExists attribute description), specify the message to show to the user if user object already exists.</span></span> <span data-ttu-id="4d359-190">The value can be [localized](localization.md).</span><span class="sxs-lookup"><span data-stu-id="4d359-190">The value can be [localized](localization.md).</span></span>| 
| <span data-ttu-id="4d359-191">ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="4d359-191">ApplicationObjectId</span></span> | <span data-ttu-id="4d359-192">No</span><span class="sxs-lookup"><span data-stu-id="4d359-192">No</span></span> | <span data-ttu-id="4d359-193">The application object identifier for extension attributes.</span><span class="sxs-lookup"><span data-stu-id="4d359-193">The application object identifier for extension attributes.</span></span> <span data-ttu-id="4d359-194">Value: ObjectId of an application.</span><span class="sxs-lookup"><span data-stu-id="4d359-194">Value: ObjectId of an application.</span></span> <span data-ttu-id="4d359-195">For more information, see [Use custom attributes in a custom profile edit policy](active-directory-b2c-create-custom-attributes-profile-edit-custom.md).</span><span class="sxs-lookup"><span data-stu-id="4d359-195">For more information, see [Use custom attributes in a custom profile edit policy](active-directory-b2c-create-custom-attributes-profile-edit-custom.md).</span></span> | 
| <span data-ttu-id="4d359-196">ClientId</span><span class="sxs-lookup"><span data-stu-id="4d359-196">ClientId</span></span> | <span data-ttu-id="4d359-197">No</span><span class="sxs-lookup"><span data-stu-id="4d359-197">No</span></span> | <span data-ttu-id="4d359-198">The client identifier for accessing the tenant as a third party.</span><span class="sxs-lookup"><span data-stu-id="4d359-198">The client identifier for accessing the tenant as a third party.</span></span> <span data-ttu-id="4d359-199">For more information, see [Use custom attributes in a custom profile edit policy](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)</span><span class="sxs-lookup"><span data-stu-id="4d359-199">For more information, see [Use custom attributes in a custom profile edit policy](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)</span></span> | 














