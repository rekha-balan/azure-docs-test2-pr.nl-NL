---
title: RelyingParty - Azure Active Directory B2C | Microsoft Docs
description: Specify the RelyingParty element of a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: af02f7185ddaec55047397ca1c8684f962112d61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870979"
---
# <a name="relyingparty"></a><span data-ttu-id="b4cd9-103">RelyingParty</span><span class="sxs-lookup"><span data-stu-id="b4cd9-103">RelyingParty</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="b4cd9-104">The **RelyingParty** element specifies the user journey to enforce for the current request to Azure Active Directory (Azure AD) B2C.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-104">The **RelyingParty** element specifies the user journey to enforce for the current request to Azure Active Directory (Azure AD) B2C.</span></span> <span data-ttu-id="b4cd9-105">It also specifies the list of claims that the relying party (RP) application needs as part of the issued token.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-105">It also specifies the list of claims that the relying party (RP) application needs as part of the issued token.</span></span> <span data-ttu-id="b4cd9-106">An RP application, such as a web, mobile, or desktop application, calls the RP policy file.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-106">An RP application, such as a web, mobile, or desktop application, calls the RP policy file.</span></span> <span data-ttu-id="b4cd9-107">The RP policy file executes a specific task, such as signing in, resetting a password, or editing a profile.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-107">The RP policy file executes a specific task, such as signing in, resetting a password, or editing a profile.</span></span> <span data-ttu-id="b4cd9-108">Multiple applications can use the same RP policy and a single application can use multiple policies.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-108">Multiple applications can use the same RP policy and a single application can use multiple policies.</span></span> <span data-ttu-id="b4cd9-109">All RP applications receive the same token with claims, and the user goes through the same user journey.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-109">All RP applications receive the same token with claims, and the user goes through the same user journey.</span></span>

<span data-ttu-id="b4cd9-110">The following example shows a **RelyingParty** element in the *B2C_1A_signup_signin* policy file:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-110">The following example shows a **RelyingParty** element in the *B2C_1A_signup_signin* policy file:</span></span>

```XML
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<TrustFrameworkPolicy
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
  PolicySchemaVersion="0.3.0.0"
  TenantId="your-tenant.onmicrosoft.com"
  PolicyId="B2C_1A_signup_signin"
  PublicPolicyUri="http://your-tenant.onmicrosoft.com/B2C_1A_signup_signin">

  <BasePolicy>
    <TenantId>your-tenant.onmicrosoft.com</TenantId>
    <PolicyId>B2C_1A_TrustFrameworkExtensions</PolicyId>
  </BasePolicy>

  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <UserJourneyBehaviors>
      <SingleSignOn Scope="TrustFramework" />
      <SessionExpiryType>Rolling</SessionExpiryType>
      <SessionExpiryInSeconds>300</SessionExpiryInSeconds>
      <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="your-application-insights-key" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      <ContentDefinitionParameters>
        <Parameter Name="campaignId">{OAUTH-KV:campaignId}</Parameter>
      </ContentDefinitionParameters>
    </UserJourneyBehaviors>
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Description>The policy profile</Description> 
      <Protocol Name="OpenIdConnect" />
      <Metadata>collection of key/value pairs of data</Metadata>
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="loyaltyNumber" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ...
```

<span data-ttu-id="b4cd9-111">The optional **RelyingParty** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-111">The optional **RelyingParty** element contains the following elements:</span></span>

| <span data-ttu-id="b4cd9-112">Element</span><span class="sxs-lookup"><span data-stu-id="b4cd9-112">Element</span></span> | <span data-ttu-id="b4cd9-113">Occurrences</span><span class="sxs-lookup"><span data-stu-id="b4cd9-113">Occurrences</span></span> | <span data-ttu-id="b4cd9-114">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-114">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="b4cd9-115">DefaultUserJourney</span><span class="sxs-lookup"><span data-stu-id="b4cd9-115">DefaultUserJourney</span></span> | <span data-ttu-id="b4cd9-116">1:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-116">1:1</span></span> | <span data-ttu-id="b4cd9-117">The default user journey for the RP application.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-117">The default user journey for the RP application.</span></span> |
| <span data-ttu-id="b4cd9-118">UserJourneyBehaviors</span><span class="sxs-lookup"><span data-stu-id="b4cd9-118">UserJourneyBehaviors</span></span> | <span data-ttu-id="b4cd9-119">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-119">0:1</span></span> | <span data-ttu-id="b4cd9-120">The scope of the user journey behaviors.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-120">The scope of the user journey behaviors.</span></span> |
| <span data-ttu-id="b4cd9-121">TechnicalProfile</span><span class="sxs-lookup"><span data-stu-id="b4cd9-121">TechnicalProfile</span></span> | <span data-ttu-id="b4cd9-122">1:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-122">1:1</span></span> | <span data-ttu-id="b4cd9-123">A technical profile that's supported by the RP application.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-123">A technical profile that's supported by the RP application.</span></span> <span data-ttu-id="b4cd9-124">The technical profile provides a contract for the RP application to contact Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-124">The technical profile provides a contract for the RP application to contact Azure AD B2C.</span></span> |

## <a name="defaultuserjourney"></a><span data-ttu-id="b4cd9-125">DefaultUserJourney</span><span class="sxs-lookup"><span data-stu-id="b4cd9-125">DefaultUserJourney</span></span>

<span data-ttu-id="b4cd9-126">The `DefaultUserJourney` element specifies a reference to the identifier of the user journey that is usually defined in the Base or Extensions policy.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-126">The `DefaultUserJourney` element specifies a reference to the identifier of the user journey that is usually defined in the Base or Extensions policy.</span></span> <span data-ttu-id="b4cd9-127">The following examples show the sign-up or sign-in user journey specified in the **RelyingParty** element:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-127">The following examples show the sign-up or sign-in user journey specified in the **RelyingParty** element:</span></span>

<span data-ttu-id="b4cd9-128">*B2C_1A_signup_signin* policy:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-128">*B2C_1A_signup_signin* policy:</span></span>

```XML
<RelyingParty>
  <DefaultUserJourney ReferenceId="SignUpOrSignIn">
  ...
```

<span data-ttu-id="b4cd9-129">*B2C_1A_TrustFrameWorkBase* or *B2C_1A_TrustFrameworkExtensionPolicy*:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-129">*B2C_1A_TrustFrameWorkBase* or *B2C_1A_TrustFrameworkExtensionPolicy*:</span></span>

```XML
<UserJourneys>
  <UserJourney Id="SignOrSignIn">
  ...
```

<span data-ttu-id="b4cd9-130">The **DefaultUserJourney** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-130">The **DefaultUserJourney** element contains the following attribute:</span></span>

| <span data-ttu-id="b4cd9-131">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4cd9-131">Attribute</span></span> | <span data-ttu-id="b4cd9-132">Required</span><span class="sxs-lookup"><span data-stu-id="b4cd9-132">Required</span></span> | <span data-ttu-id="b4cd9-133">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-133">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4cd9-134">ReferenceId</span><span class="sxs-lookup"><span data-stu-id="b4cd9-134">ReferenceId</span></span> | <span data-ttu-id="b4cd9-135">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-135">Yes</span></span> | <span data-ttu-id="b4cd9-136">An identifier of the user journey in the policy.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-136">An identifier of the user journey in the policy.</span></span> <span data-ttu-id="b4cd9-137">For more informaiton, see [user journeys](userjourneys.md)</span><span class="sxs-lookup"><span data-stu-id="b4cd9-137">For more informaiton, see [user journeys](userjourneys.md)</span></span> |

## <a name="userjourneybehaviors"></a><span data-ttu-id="b4cd9-138">UserJourneyBehaviors</span><span class="sxs-lookup"><span data-stu-id="b4cd9-138">UserJourneyBehaviors</span></span>

<span data-ttu-id="b4cd9-139">The **UserJourneyBehaviors** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-139">The **UserJourneyBehaviors** element contains the following elements:</span></span>

| <span data-ttu-id="b4cd9-140">Element</span><span class="sxs-lookup"><span data-stu-id="b4cd9-140">Element</span></span> | <span data-ttu-id="b4cd9-141">Occurrences</span><span class="sxs-lookup"><span data-stu-id="b4cd9-141">Occurrences</span></span> | <span data-ttu-id="b4cd9-142">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-142">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="b4cd9-143">SingleSignOn</span><span class="sxs-lookup"><span data-stu-id="b4cd9-143">SingleSignOn</span></span> | <span data-ttu-id="b4cd9-144">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-144">0:1</span></span> | <span data-ttu-id="b4cd9-145">The scope of the single sign-on (SSO) session behavior of a user journey.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-145">The scope of the single sign-on (SSO) session behavior of a user journey.</span></span> |
| <span data-ttu-id="b4cd9-146">SessionExpiryType</span><span class="sxs-lookup"><span data-stu-id="b4cd9-146">SessionExpiryType</span></span> |<span data-ttu-id="b4cd9-147">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-147">0:1</span></span> | <span data-ttu-id="b4cd9-148">The authentication behavior of the session.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-148">The authentication behavior of the session.</span></span> <span data-ttu-id="b4cd9-149">Possible values: `Rolling` or `Absolute`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-149">Possible values: `Rolling` or `Absolute`.</span></span> <span data-ttu-id="b4cd9-150">The `Rolling` value (default) indicates that the user remains signed in as long as the user is continually active in the application.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-150">The `Rolling` value (default) indicates that the user remains signed in as long as the user is continually active in the application.</span></span> <span data-ttu-id="b4cd9-151">The `Absolute` value indicates that the user is forced to reauthenticate after the time period specified by application session lifetime.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-151">The `Absolute` value indicates that the user is forced to reauthenticate after the time period specified by application session lifetime.</span></span> |
| <span data-ttu-id="b4cd9-152">SessionExpiryInSeconds</span><span class="sxs-lookup"><span data-stu-id="b4cd9-152">SessionExpiryInSeconds</span></span> | <span data-ttu-id="b4cd9-153">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-153">0:1</span></span> | <span data-ttu-id="b4cd9-154">The lifetime of Azure AD B2C's session cookie specified as an integer stored on the user's browser upon successful authentication.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-154">The lifetime of Azure AD B2C's session cookie specified as an integer stored on the user's browser upon successful authentication.</span></span> |
| <span data-ttu-id="b4cd9-155">JourneyInsights</span><span class="sxs-lookup"><span data-stu-id="b4cd9-155">JourneyInsights</span></span> | <span data-ttu-id="b4cd9-156">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-156">0:1</span></span> | <span data-ttu-id="b4cd9-157">The Azure Application Insights instrumentation key to be used.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-157">The Azure Application Insights instrumentation key to be used.</span></span> |
| <span data-ttu-id="b4cd9-158">ContentDefinitionParameters</span><span class="sxs-lookup"><span data-stu-id="b4cd9-158">ContentDefinitionParameters</span></span> | <span data-ttu-id="b4cd9-159">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-159">0:1</span></span> | <span data-ttu-id="b4cd9-160">The list of key value pairs to be appended to the content definition load URI.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-160">The list of key value pairs to be appended to the content definition load URI.</span></span> |

### <a name="singlesignon"></a><span data-ttu-id="b4cd9-161">SingleSignOn</span><span class="sxs-lookup"><span data-stu-id="b4cd9-161">SingleSignOn</span></span>

<span data-ttu-id="b4cd9-162">The **SingleSignOn** element contains in the following attribute:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-162">The **SingleSignOn** element contains in the following attribute:</span></span>

| <span data-ttu-id="b4cd9-163">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4cd9-163">Attribute</span></span> | <span data-ttu-id="b4cd9-164">Required</span><span class="sxs-lookup"><span data-stu-id="b4cd9-164">Required</span></span> | <span data-ttu-id="b4cd9-165">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-165">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4cd9-166">Scope</span><span class="sxs-lookup"><span data-stu-id="b4cd9-166">Scope</span></span> | <span data-ttu-id="b4cd9-167">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-167">Yes</span></span> | <span data-ttu-id="b4cd9-168">The scope of the single sign-on behavior.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-168">The scope of the single sign-on behavior.</span></span> <span data-ttu-id="b4cd9-169">Possible values: `Suppressed`, `Tenant`, `Application`, or `Policy`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-169">Possible values: `Suppressed`, `Tenant`, `Application`, or `Policy`.</span></span> <span data-ttu-id="b4cd9-170">The `Suppressed` value indicates that the behavior is suppressed.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-170">The `Suppressed` value indicates that the behavior is suppressed.</span></span> <span data-ttu-id="b4cd9-171">For example, in the case of a single sign-on session, no session is maintained for the user and the user is always prompted for an identity provider selection.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-171">For example, in the case of a single sign-on session, no session is maintained for the user and the user is always prompted for an identity provider selection.</span></span> <span data-ttu-id="b4cd9-172">The `TrustFramework` value indicates that the behavior is applied for all policies in the trust framework.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-172">The `TrustFramework` value indicates that the behavior is applied for all policies in the trust framework.</span></span> <span data-ttu-id="b4cd9-173">For example, a user navigating through two policy journeys for a trust framework is not prompted for an identity provider selection.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-173">For example, a user navigating through two policy journeys for a trust framework is not prompted for an identity provider selection.</span></span> <span data-ttu-id="b4cd9-174">The `Tenant` value indicates that the behavior is applied to all policies in the tenant.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-174">The `Tenant` value indicates that the behavior is applied to all policies in the tenant.</span></span> <span data-ttu-id="b4cd9-175">For example, a user navigating through two policy journeys for a tenant is not prompted for an identity provider selection.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-175">For example, a user navigating through two policy journeys for a tenant is not prompted for an identity provider selection.</span></span> <span data-ttu-id="b4cd9-176">The `Application` value indicates that the behavior is applied to all policies for the application making the request.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-176">The `Application` value indicates that the behavior is applied to all policies for the application making the request.</span></span> <span data-ttu-id="b4cd9-177">For example, a user navigating through two policy journeys for an application is not prompted for an identity provider selection.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-177">For example, a user navigating through two policy journeys for an application is not prompted for an identity provider selection.</span></span> <span data-ttu-id="b4cd9-178">The `Policy` value indicates that the behavior only applies to a policy.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-178">The `Policy` value indicates that the behavior only applies to a policy.</span></span> <span data-ttu-id="b4cd9-179">For example, a user navigating through two policy journeys for a trust framework is prompted for an identity provider selection when switching between policies.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-179">For example, a user navigating through two policy journeys for a trust framework is prompted for an identity provider selection when switching between policies.</span></span> |

## <a name="journeyinsights"></a><span data-ttu-id="b4cd9-180">JourneyInsights</span><span class="sxs-lookup"><span data-stu-id="b4cd9-180">JourneyInsights</span></span>

<span data-ttu-id="b4cd9-181">The **JourneyInsights** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-181">The **JourneyInsights** element contains the following attributes:</span></span>

| <span data-ttu-id="b4cd9-182">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4cd9-182">Attribute</span></span> | <span data-ttu-id="b4cd9-183">Required</span><span class="sxs-lookup"><span data-stu-id="b4cd9-183">Required</span></span> | <span data-ttu-id="b4cd9-184">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-184">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4cd9-185">TelemetryEngine</span><span class="sxs-lookup"><span data-stu-id="b4cd9-185">TelemetryEngine</span></span> | <span data-ttu-id="b4cd9-186">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-186">Yes</span></span> | <span data-ttu-id="b4cd9-187">The value must be `ApplicationInsights`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-187">The value must be `ApplicationInsights`.</span></span> | 
| <span data-ttu-id="b4cd9-188">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="b4cd9-188">InstrumentationKey</span></span> | <span data-ttu-id="b4cd9-189">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-189">Yes</span></span> | <span data-ttu-id="b4cd9-190">The string that contains the instrumentation key for the application insights element.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-190">The string that contains the instrumentation key for the application insights element.</span></span> |
| <span data-ttu-id="b4cd9-191">DeveloperMode</span><span class="sxs-lookup"><span data-stu-id="b4cd9-191">DeveloperMode</span></span> | <span data-ttu-id="b4cd9-192">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-192">Yes</span></span> | <span data-ttu-id="b4cd9-193">Possible values: `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-193">Possible values: `true` or `false`.</span></span> <span data-ttu-id="b4cd9-194">If `true`, Application Insights expedites the telemetry through the processing pipeline.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-194">If `true`, Application Insights expedites the telemetry through the processing pipeline.</span></span> <span data-ttu-id="b4cd9-195">This setting is good for development, but constrained at high volumes The detailed activity logs are designed only to aid in development of custom policies.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-195">This setting is good for development, but constrained at high volumes The detailed activity logs are designed only to aid in development of custom policies.</span></span> <span data-ttu-id="b4cd9-196">Do not use development mode in production.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-196">Do not use development mode in production.</span></span> <span data-ttu-id="b4cd9-197">Logs collect all claims sent to and from the identity providers during development.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-197">Logs collect all claims sent to and from the identity providers during development.</span></span> <span data-ttu-id="b4cd9-198">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-198">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span> <span data-ttu-id="b4cd9-199">These detailed logs are only collected when this value is set to `true`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-199">These detailed logs are only collected when this value is set to `true`.</span></span>|
| <span data-ttu-id="b4cd9-200">ClientEnabled</span><span class="sxs-lookup"><span data-stu-id="b4cd9-200">ClientEnabled</span></span> | <span data-ttu-id="b4cd9-201">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-201">Yes</span></span> | <span data-ttu-id="b4cd9-202">Possible values: `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-202">Possible values: `true` or `false`.</span></span> <span data-ttu-id="b4cd9-203">If `true`, sends the Application Insights client-side script for tracking page view and client-side errors.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-203">If `true`, sends the Application Insights client-side script for tracking page view and client-side errors.</span></span> | 
| <span data-ttu-id="b4cd9-204">ServerEnabled</span><span class="sxs-lookup"><span data-stu-id="b4cd9-204">ServerEnabled</span></span> | <span data-ttu-id="b4cd9-205">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-205">Yes</span></span> | <span data-ttu-id="b4cd9-206">Possible values: `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-206">Possible values: `true` or `false`.</span></span> <span data-ttu-id="b4cd9-207">If `true`, sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-207">If `true`, sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span> | 
| <span data-ttu-id="b4cd9-208">TelemetryVersion</span><span class="sxs-lookup"><span data-stu-id="b4cd9-208">TelemetryVersion</span></span> | <span data-ttu-id="b4cd9-209">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-209">Yes</span></span> | <span data-ttu-id="b4cd9-210">The value must be `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-210">The value must be `1.0.0`.</span></span> | 

<span data-ttu-id="b4cd9-211">For more information, see [Collecting Logs](active-directory-b2c-troubleshoot-custom.md)</span><span class="sxs-lookup"><span data-stu-id="b4cd9-211">For more information, see [Collecting Logs](active-directory-b2c-troubleshoot-custom.md)</span></span>

## <a name="contentdefinitionparameters"></a><span data-ttu-id="b4cd9-212">ContentDefinitionParameters</span><span class="sxs-lookup"><span data-stu-id="b4cd9-212">ContentDefinitionParameters</span></span>

<span data-ttu-id="b4cd9-213">By using custom policies in Azure AD B2C, you can send a parameter in a query string.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-213">By using custom policies in Azure AD B2C, you can send a parameter in a query string.</span></span> <span data-ttu-id="b4cd9-214">By passing the parameter to your HTML endpoint, you can dynamically change the page content.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-214">By passing the parameter to your HTML endpoint, you can dynamically change the page content.</span></span> <span data-ttu-id="b4cd9-215">For example, you can change the background image on the Azure AD B2C sign-up or sign-in page, based on a parameter that you pass from your web or mobile application.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-215">For example, you can change the background image on the Azure AD B2C sign-up or sign-in page, based on a parameter that you pass from your web or mobile application.</span></span> <span data-ttu-id="b4cd9-216">Azure AD B2C passes the query string parameters to your dynamic HTML file, such as aspx file.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-216">Azure AD B2C passes the query string parameters to your dynamic HTML file, such as aspx file.</span></span> 

<span data-ttu-id="b4cd9-217">The following example passes a parameter named `campaignId` with a value of `hawaii` in the query string:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-217">The following example passes a parameter named `campaignId` with a value of `hawaii` in the query string:</span></span>

`https://login.microsoft.com/contoso.onmicrosoft.com/oauth2/v2.0/authorize?pB2C_1A_signup_signin&client_id=a415078a-0402-4ce3-a9c6-ec1947fcfb3f&nonce=defaultNonce&redirect_uri=http%3A%2F%2Fjwt.io%2F&scope=openid&response_type=id_token&prompt=login&campaignId=hawaii`

<span data-ttu-id="b4cd9-218">The **ContentDefinitionParameters** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-218">The **ContentDefinitionParameters** element contains the following element:</span></span>

| <span data-ttu-id="b4cd9-219">Element</span><span class="sxs-lookup"><span data-stu-id="b4cd9-219">Element</span></span> | <span data-ttu-id="b4cd9-220">Occurrences</span><span class="sxs-lookup"><span data-stu-id="b4cd9-220">Occurrences</span></span> | <span data-ttu-id="b4cd9-221">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-221">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="b4cd9-222">ContentDefinitionParameter</span><span class="sxs-lookup"><span data-stu-id="b4cd9-222">ContentDefinitionParameter</span></span> | <span data-ttu-id="b4cd9-223">0:n</span><span class="sxs-lookup"><span data-stu-id="b4cd9-223">0:n</span></span> | <span data-ttu-id="b4cd9-224">A string that contains the key value pair that's appended to the query string of a content definition load URI.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-224">A string that contains the key value pair that's appended to the query string of a content definition load URI.</span></span> |

<span data-ttu-id="b4cd9-225">The **ContentDefinitionParameter** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-225">The **ContentDefinitionParameter** element contains the following attribute:</span></span>

| <span data-ttu-id="b4cd9-226">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4cd9-226">Attribute</span></span> | <span data-ttu-id="b4cd9-227">Required</span><span class="sxs-lookup"><span data-stu-id="b4cd9-227">Required</span></span> | <span data-ttu-id="b4cd9-228">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-228">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4cd9-229">Name</span><span class="sxs-lookup"><span data-stu-id="b4cd9-229">Name</span></span> | <span data-ttu-id="b4cd9-230">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-230">Yes</span></span> | <span data-ttu-id="b4cd9-231">The name of the key value pair.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-231">The name of the key value pair.</span></span> |

<span data-ttu-id="b4cd9-232">For more information, see [Configure the UI with dynamic content by using custom policies](active-directory-b2c-ui-customization-custom-dynamic.md)</span><span class="sxs-lookup"><span data-stu-id="b4cd9-232">For more information, see [Configure the UI with dynamic content by using custom policies](active-directory-b2c-ui-customization-custom-dynamic.md)</span></span>

## <a name="technicalprofile"></a><span data-ttu-id="b4cd9-233">TechnicalProfile</span><span class="sxs-lookup"><span data-stu-id="b4cd9-233">TechnicalProfile</span></span>

<span data-ttu-id="b4cd9-234">The **TechnicalProfile** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-234">The **TechnicalProfile** element contains the following attribute:</span></span>

| <span data-ttu-id="b4cd9-235">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4cd9-235">Attribute</span></span> | <span data-ttu-id="b4cd9-236">Required</span><span class="sxs-lookup"><span data-stu-id="b4cd9-236">Required</span></span> | <span data-ttu-id="b4cd9-237">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-237">Description</span></span> |
| --------- | -------- | ----------- | 
| <span data-ttu-id="b4cd9-238">Id</span><span class="sxs-lookup"><span data-stu-id="b4cd9-238">Id</span></span> | <span data-ttu-id="b4cd9-239">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-239">Yes</span></span> | <span data-ttu-id="b4cd9-240">The value must be `PolicyProfile`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-240">The value must be `PolicyProfile`.</span></span> |

<span data-ttu-id="b4cd9-241">The **TechnicalProfile** contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-241">The **TechnicalProfile** contains the following elements:</span></span>

| <span data-ttu-id="b4cd9-242">Element</span><span class="sxs-lookup"><span data-stu-id="b4cd9-242">Element</span></span> | <span data-ttu-id="b4cd9-243">Occurrences</span><span class="sxs-lookup"><span data-stu-id="b4cd9-243">Occurrences</span></span> | <span data-ttu-id="b4cd9-244">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-244">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="b4cd9-245">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b4cd9-245">DisplayName</span></span> | <span data-ttu-id="b4cd9-246">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-246">0:1</span></span> | <span data-ttu-id="b4cd9-247">The string that contains the name of the technical profile that is displayed to users.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-247">The string that contains the name of the technical profile that is displayed to users.</span></span> |
| <span data-ttu-id="b4cd9-248">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-248">Description</span></span> | <span data-ttu-id="b4cd9-249">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-249">0:1</span></span> | <span data-ttu-id="b4cd9-250">The string that contains the description of the technical profile that is displayed to users.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-250">The string that contains the description of the technical profile that is displayed to users.</span></span> |
| <span data-ttu-id="b4cd9-251">Protocol</span><span class="sxs-lookup"><span data-stu-id="b4cd9-251">Protocol</span></span> | <span data-ttu-id="b4cd9-252">1:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-252">1:1</span></span> | <span data-ttu-id="b4cd9-253">The protocol used for the federation.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-253">The protocol used for the federation.</span></span> |
| <span data-ttu-id="b4cd9-254">Metadata</span><span class="sxs-lookup"><span data-stu-id="b4cd9-254">Metadata</span></span> | <span data-ttu-id="b4cd9-255">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-255">0:1</span></span> | <span data-ttu-id="b4cd9-256">The collection of *Item* of key/value pairs utilized by the protocol for communicating with the endpoint in the course of a transaction to configure interaction between the relying party and other community participants.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-256">The collection of *Item* of key/value pairs utilized by the protocol for communicating with the endpoint in the course of a transaction to configure interaction between the relying party and other community participants.</span></span> |
| <span data-ttu-id="b4cd9-257">OutputClaims</span><span class="sxs-lookup"><span data-stu-id="b4cd9-257">OutputClaims</span></span> | <span data-ttu-id="b4cd9-258">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-258">0:1</span></span> | <span data-ttu-id="b4cd9-259">A list of claim types that are taken as output in the technical profile.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-259">A list of claim types that are taken as output in the technical profile.</span></span> <span data-ttu-id="b4cd9-260">Each of these elements contains reference to a **ClaimType** already defined in the **ClaimsSchema** section or in a policy from which this policy file inherits.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-260">Each of these elements contains reference to a **ClaimType** already defined in the **ClaimsSchema** section or in a policy from which this policy file inherits.</span></span> |
| <span data-ttu-id="b4cd9-261">SubjectNamingInfo</span><span class="sxs-lookup"><span data-stu-id="b4cd9-261">SubjectNamingInfo</span></span> | <span data-ttu-id="b4cd9-262">0:1</span><span class="sxs-lookup"><span data-stu-id="b4cd9-262">0:1</span></span> | <span data-ttu-id="b4cd9-263">The subject name used in tokens.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-263">The subject name used in tokens.</span></span> |

<span data-ttu-id="b4cd9-264">The **Protocol** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-264">The **Protocol** element contains the following attribute:</span></span>

| <span data-ttu-id="b4cd9-265">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4cd9-265">Attribute</span></span> | <span data-ttu-id="b4cd9-266">Required</span><span class="sxs-lookup"><span data-stu-id="b4cd9-266">Required</span></span> | <span data-ttu-id="b4cd9-267">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-267">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4cd9-268">Name</span><span class="sxs-lookup"><span data-stu-id="b4cd9-268">Name</span></span> | <span data-ttu-id="b4cd9-269">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-269">Yes</span></span> | <span data-ttu-id="b4cd9-270">The name of a valid protocol supported by Azure AD B2C that is used as part of the technical profile.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-270">The name of a valid protocol supported by Azure AD B2C that is used as part of the technical profile.</span></span> <span data-ttu-id="b4cd9-271">Possible values: `OpenIdConnect` or `SAML2`.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-271">Possible values: `OpenIdConnect` or `SAML2`.</span></span> <span data-ttu-id="b4cd9-272">The `OpenIdConnect` value represents the OpenID Connect 1.0 protocol standard as per OpenID foundation specification.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-272">The `OpenIdConnect` value represents the OpenID Connect 1.0 protocol standard as per OpenID foundation specification.</span></span> <span data-ttu-id="b4cd9-273">The `SAML2` represents the SAML 2.0 protocol standard as per OASIS specification.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-273">The `SAML2` represents the SAML 2.0 protocol standard as per OASIS specification.</span></span> <span data-ttu-id="b4cd9-274">Do not use a SAML token in production.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-274">Do not use a SAML token in production.</span></span> |

## <a name="outputclaims"></a><span data-ttu-id="b4cd9-275">OutputClaims</span><span class="sxs-lookup"><span data-stu-id="b4cd9-275">OutputClaims</span></span>

<span data-ttu-id="b4cd9-276">The **OutputClaims** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-276">The **OutputClaims** element contains the following element:</span></span>

| <span data-ttu-id="b4cd9-277">Element</span><span class="sxs-lookup"><span data-stu-id="b4cd9-277">Element</span></span> | <span data-ttu-id="b4cd9-278">Occurrences</span><span class="sxs-lookup"><span data-stu-id="b4cd9-278">Occurrences</span></span> | <span data-ttu-id="b4cd9-279">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-279">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="b4cd9-280">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="b4cd9-280">OutputClaim</span></span> | <span data-ttu-id="b4cd9-281">0:n</span><span class="sxs-lookup"><span data-stu-id="b4cd9-281">0:n</span></span> | <span data-ttu-id="b4cd9-282">The name of an expected claim type in the supported list for the policy to which the relying party subscribes.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-282">The name of an expected claim type in the supported list for the policy to which the relying party subscribes.</span></span> <span data-ttu-id="b4cd9-283">This claim serves as an output for the technical profile.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-283">This claim serves as an output for the technical profile.</span></span> |

<span data-ttu-id="b4cd9-284">The **OutputClaim** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-284">The **OutputClaim** element contains the following attributes:</span></span>

| <span data-ttu-id="b4cd9-285">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4cd9-285">Attribute</span></span> | <span data-ttu-id="b4cd9-286">Required</span><span class="sxs-lookup"><span data-stu-id="b4cd9-286">Required</span></span> | <span data-ttu-id="b4cd9-287">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-287">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4cd9-288">ClaimTypeReferenceId</span><span class="sxs-lookup"><span data-stu-id="b4cd9-288">ClaimTypeReferenceId</span></span> | <span data-ttu-id="b4cd9-289">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-289">Yes</span></span> | <span data-ttu-id="b4cd9-290">A reference to a **ClaimType** already defined in the **ClaimsSchema** section in the policy file.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-290">A reference to a **ClaimType** already defined in the **ClaimsSchema** section in the policy file.</span></span> |
| <span data-ttu-id="b4cd9-291">DefaultValue</span><span class="sxs-lookup"><span data-stu-id="b4cd9-291">DefaultValue</span></span> | <span data-ttu-id="b4cd9-292">No</span><span class="sxs-lookup"><span data-stu-id="b4cd9-292">No</span></span> | <span data-ttu-id="b4cd9-293">A default value that can be used if the claim value is empty.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-293">A default value that can be used if the claim value is empty.</span></span> |
| <span data-ttu-id="b4cd9-294">PartnerClaimType</span><span class="sxs-lookup"><span data-stu-id="b4cd9-294">PartnerClaimType</span></span> | <span data-ttu-id="b4cd9-295">No</span><span class="sxs-lookup"><span data-stu-id="b4cd9-295">No</span></span> | <span data-ttu-id="b4cd9-296">Sends the claim in a different name as configured in the ClaimType definition.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-296">Sends the claim in a different name as configured in the ClaimType definition.</span></span> |

### <a name="subjectnaminginfo"></a><span data-ttu-id="b4cd9-297">SubjectNamingInfo</span><span class="sxs-lookup"><span data-stu-id="b4cd9-297">SubjectNamingInfo</span></span>

<span data-ttu-id="b4cd9-298">With the **SubjectNameingInfo** element, you control the value of the token subject:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-298">With the **SubjectNameingInfo** element, you control the value of the token subject:</span></span>
- <span data-ttu-id="b4cd9-299">**JTW token** - the `sub` claim.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-299">**JTW token** - the `sub` claim.</span></span> <span data-ttu-id="b4cd9-300">This is a principal about which the token asserts information, such as the user of an application.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-300">This is a principal about which the token asserts information, such as the user of an application.</span></span> <span data-ttu-id="b4cd9-301">This value is immutable and cannot be reassigned or reused.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-301">This value is immutable and cannot be reassigned or reused.</span></span> <span data-ttu-id="b4cd9-302">It can be used to perform safe authorization checks, such as when the token is used to access a resource.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-302">It can be used to perform safe authorization checks, such as when the token is used to access a resource.</span></span> <span data-ttu-id="b4cd9-303">By default, the subject claim is populated with the object ID of the user in the directory.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-303">By default, the subject claim is populated with the object ID of the user in the directory.</span></span> <span data-ttu-id="b4cd9-304">For more information, see [Token, session and single sign-on configuration](active-directory-b2c-token-session-sso.md).</span><span class="sxs-lookup"><span data-stu-id="b4cd9-304">For more information, see [Token, session and single sign-on configuration](active-directory-b2c-token-session-sso.md).</span></span>
- <span data-ttu-id="b4cd9-305">**SAML token** - the `<Subject><NameID>` element which identifies the subject element.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-305">**SAML token** - the `<Subject><NameID>` element which identifies the subject element.</span></span>

<span data-ttu-id="b4cd9-306">The **SubjectNamingInfo** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-306">The **SubjectNamingInfo** element contains the following attribute:</span></span>

| <span data-ttu-id="b4cd9-307">Attribute</span><span class="sxs-lookup"><span data-stu-id="b4cd9-307">Attribute</span></span> | <span data-ttu-id="b4cd9-308">Required</span><span class="sxs-lookup"><span data-stu-id="b4cd9-308">Required</span></span> | <span data-ttu-id="b4cd9-309">Description</span><span class="sxs-lookup"><span data-stu-id="b4cd9-309">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="b4cd9-310">ClaimType</span><span class="sxs-lookup"><span data-stu-id="b4cd9-310">ClaimType</span></span> | <span data-ttu-id="b4cd9-311">Yes</span><span class="sxs-lookup"><span data-stu-id="b4cd9-311">Yes</span></span> | <span data-ttu-id="b4cd9-312">A reference to an output claim's **PartnerClaimType**.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-312">A reference to an output claim's **PartnerClaimType**.</span></span> <span data-ttu-id="b4cd9-313">The output claims must be defined in the relying party policy **OutputClaims** collection.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-313">The output claims must be defined in the relying party policy **OutputClaims** collection.</span></span> |

<span data-ttu-id="b4cd9-314">The following example shows how to define an OpenId Connect relying party.</span><span class="sxs-lookup"><span data-stu-id="b4cd9-314">The following example shows how to define an OpenId Connect relying party.</span></span> <span data-ttu-id="b4cd9-315">The subject name info is configured as the `objectId`:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-315">The subject name info is configured as the `objectId`:</span></span>

```XML
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
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
  </TechnicalProfile>
</RelyingParty>
```
<span data-ttu-id="b4cd9-316">The JWT token includes the `sub` claim with the user objectId:</span><span class="sxs-lookup"><span data-stu-id="b4cd9-316">The JWT token includes the `sub` claim with the user objectId:</span></span>

```JSON
{
  ...
  "sub": "6fbbd70d-262b-4b50-804c-257ae1706ef2",
  ...
}
```


