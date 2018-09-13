---
title: Manage SSO and token customization with custom policies in Azure Active Directory B2C | Microsoft Docs
description: Learn about managing SSO and token customization with custom policies.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 05/02/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 811fb8b2de59c9d324ab4acb8b0f51b4cec80aee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965525"
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="2d6ce-103">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span><span class="sxs-lookup"><span data-stu-id="2d6ce-103">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="2d6ce-104">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-104">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="2d6ce-105">To learn what each setting does, see the documentation [here](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="2d6ce-105">To learn what each setting does, see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="2d6ce-106">Token lifetimes and claims configuration</span><span class="sxs-lookup"><span data-stu-id="2d6ce-106">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="2d6ce-107">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-107">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="2d6ce-108">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-108">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="2d6ce-109">Inside, you'll need to put the information that affects your token lifetimes.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-109">Inside, you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="2d6ce-110">The XML looks like this example:</span><span class="sxs-lookup"><span data-stu-id="2d6ce-110">The XML looks like this example:</span></span>

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

<span data-ttu-id="2d6ce-111">**Access token lifetimes** - The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-111">**Access token lifetimes** - The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="2d6ce-112">The default value in built-in is 3600 seconds (60 minutes).</span><span class="sxs-lookup"><span data-stu-id="2d6ce-112">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="2d6ce-113">**ID token lifetime** - The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-113">**ID token lifetime** - The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="2d6ce-114">The default value in built-in is 3600 seconds (60 minutes).</span><span class="sxs-lookup"><span data-stu-id="2d6ce-114">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="2d6ce-115">**Refresh token lifetime** - The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-115">**Refresh token lifetime** - The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="2d6ce-116">The default value in built-in is 1209600 seconds (14 days).</span><span class="sxs-lookup"><span data-stu-id="2d6ce-116">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="2d6ce-117">**Refresh token sliding window lifetime** - If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-117">**Refresh token sliding window lifetime** - If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="2d6ce-118">The default value in built-in is 7776000 (90 days).</span><span class="sxs-lookup"><span data-stu-id="2d6ce-118">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="2d6ce-119">If you don't want to enforce a sliding window lifetime, replace this line with:</span><span class="sxs-lookup"><span data-stu-id="2d6ce-119">If you don't want to enforce a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="2d6ce-120">**Issuer (iss) claim** - If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="2d6ce-120">**Issuer (iss) claim** - If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="2d6ce-121">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-121">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="2d6ce-122">**Setting claim representing policy ID** - The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span><span class="sxs-lookup"><span data-stu-id="2d6ce-122">**Setting claim representing policy ID** - The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="2d6ce-123">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-123">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="2d6ce-124">In your `<OutputClaims>` item, add this element:</span><span class="sxs-lookup"><span data-stu-id="2d6ce-124">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="2d6ce-125">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="2d6ce-125">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="2d6ce-126">**Subject (sub) claim** - This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span><span class="sxs-lookup"><span data-stu-id="2d6ce-126">**Subject (sub) claim** - This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="2d6ce-127">Replace this line</span><span class="sxs-lookup"><span data-stu-id="2d6ce-127">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="2d6ce-128">with this line:</span><span class="sxs-lookup"><span data-stu-id="2d6ce-128">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="2d6ce-129">Session behavior and SSO</span><span class="sxs-lookup"><span data-stu-id="2d6ce-129">Session behavior and SSO</span></span>

<span data-ttu-id="2d6ce-130">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-130">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="2d6ce-131">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-131">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="2d6ce-132">The inside of your `<UserJourneyBehavors>` element should look like this:</span><span class="sxs-lookup"><span data-stu-id="2d6ce-132">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="2d6ce-133">**Single sign on (SSO) configuration** - To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-133">**Single sign on (SSO) configuration** - To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="2d6ce-134">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-134">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="2d6ce-135">**Web app session lifetime (minutes)** - To change the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-135">**Web app session lifetime (minutes)** - To change the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="2d6ce-136">The default value in built-in policies is 86400 seconds (1440 minutes).</span><span class="sxs-lookup"><span data-stu-id="2d6ce-136">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="2d6ce-137">**Web app session time-out** - To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-137">**Web app session time-out** - To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="2d6ce-138">The applicable values are `Absolute` and `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="2d6ce-138">The applicable values are `Absolute` and `Rolling`.</span></span>
