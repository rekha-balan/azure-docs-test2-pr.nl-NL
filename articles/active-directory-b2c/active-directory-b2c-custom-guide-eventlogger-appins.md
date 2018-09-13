---
title: Track user behavior by using events in Application Insights from Azure Active Directory B2C | Microsoft Docs
description: Step-by-step guide to enable event logs in Application Insights from Azure AD B2C user journeys by using custom policies (preview)
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.date: 04/16/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: c77feed3b86358c74f741b53aa03ecb454dc9a62
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868219"
---
# <a name="track-user-behavior-in-azure-ad-b2c-journeys-by-using-application-insights"></a><span data-ttu-id="b1d6e-103">Track user behavior in Azure AD B2C journeys by using Application Insights</span><span class="sxs-lookup"><span data-stu-id="b1d6e-103">Track user behavior in Azure AD B2C journeys by using Application Insights</span></span>

<span data-ttu-id="b1d6e-104">Azure Active Directory B2C (Azure AD B2C) works well with Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-104">Azure Active Directory B2C (Azure AD B2C) works well with Azure Application Insights.</span></span> <span data-ttu-id="b1d6e-105">They provide detailed and customized event logs for your custom-created user journeys.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-105">They provide detailed and customized event logs for your custom-created user journeys.</span></span> <span data-ttu-id="b1d6e-106">This article shows how to get started so you can:</span><span class="sxs-lookup"><span data-stu-id="b1d6e-106">This article shows how to get started so you can:</span></span>

* <span data-ttu-id="b1d6e-107">Gain insights on user behavior.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-107">Gain insights on user behavior.</span></span>
* <span data-ttu-id="b1d6e-108">Troubleshoot your own policies in development or in production.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-108">Troubleshoot your own policies in development or in production.</span></span>
* <span data-ttu-id="b1d6e-109">Measure performance.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-109">Measure performance.</span></span>
* <span data-ttu-id="b1d6e-110">Create notifications from Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-110">Create notifications from Application Insights.</span></span>

> [!NOTE]
> <span data-ttu-id="b1d6e-111">This feature is in preview.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-111">This feature is in preview.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="b1d6e-112">How it works</span><span class="sxs-lookup"><span data-stu-id="b1d6e-112">How it works</span></span>

<span data-ttu-id="b1d6e-113">The Identity Experience Framework in Azure AD B2C now includes the provider `Handler="Web.TPEngine.Providers.UserJourneyContextProvider, Web.TPEngine, Version=1.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-113">The Identity Experience Framework in Azure AD B2C now includes the provider `Handler="Web.TPEngine.Providers.UserJourneyContextProvider, Web.TPEngine, Version=1.0.0.0`.</span></span>  <span data-ttu-id="b1d6e-114">It sends event data directly to Application Insights by using the instrumentation key provided to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-114">It sends event data directly to Application Insights by using the instrumentation key provided to Azure AD B2C.</span></span>

<span data-ttu-id="b1d6e-115">A technical profile uses this provider to define an event from B2C.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-115">A technical profile uses this provider to define an event from B2C.</span></span>  <span data-ttu-id="b1d6e-116">The profile specifies the name of the event, the claims that will be recorded, and the instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-116">The profile specifies the name of the event, the claims that will be recorded, and the instrumentation key.</span></span>  <span data-ttu-id="b1d6e-117">To post an event, the technical profile is then added as an `orchestration step` or as a `validation technical profile` in a custom user journey.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-117">To post an event, the technical profile is then added as an `orchestration step` or as a `validation technical profile` in a custom user journey.</span></span>

<span data-ttu-id="b1d6e-118">Application Insights can unify the events by using a correlation ID to record a user session.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-118">Application Insights can unify the events by using a correlation ID to record a user session.</span></span> <span data-ttu-id="b1d6e-119">Application Insights makes the event and session available within seconds and presents many visualization, export, and analytical tools.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-119">Application Insights makes the event and session available within seconds and presents many visualization, export, and analytical tools.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1d6e-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b1d6e-120">Prerequisites</span></span>

<span data-ttu-id="b1d6e-121">Complete the steps in [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b1d6e-121">Complete the steps in [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="b1d6e-122">This article assumes that you're using the custom policy starter pack.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-122">This article assumes that you're using the custom policy starter pack.</span></span> <span data-ttu-id="b1d6e-123">But the starter pack isn't required.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-123">But the starter pack isn't required.</span></span>

## <a name="step-1-create-an-application-insights-resource-and-get-the-instrumentation-key"></a><span data-ttu-id="b1d6e-124">Step 1.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-124">Step 1.</span></span> <span data-ttu-id="b1d6e-125">Create an Application Insights resource and get the instrumentation key</span><span class="sxs-lookup"><span data-stu-id="b1d6e-125">Create an Application Insights resource and get the instrumentation key</span></span>

<span data-ttu-id="b1d6e-126">When you're using Application Insights with Azure AD B2C, the only requirement is to create a resource and obtain an instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-126">When you're using Application Insights with Azure AD B2C, the only requirement is to create a resource and obtain an instrumentation key.</span></span> <span data-ttu-id="b1d6e-127">You create a resource in the [Azure portal.](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b1d6e-127">You create a resource in the [Azure portal.](https://portal.azure.com)</span></span>

1. <span data-ttu-id="b1d6e-128">In the Azure portal, within your subscription tenant, select **+ Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-128">In the Azure portal, within your subscription tenant, select **+ Create a resource**.</span></span> <span data-ttu-id="b1d6e-129">This tenant is not your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-129">This tenant is not your Azure AD B2C tenant.</span></span>  
2. <span data-ttu-id="b1d6e-130">Search for and select **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-130">Search for and select **Application Insights**.</span></span>  
3. <span data-ttu-id="b1d6e-131">Create a resource that uses **ASP.NET web application** as **Application Type**, under a subscription of your preference.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-131">Create a resource that uses **ASP.NET web application** as **Application Type**, under a subscription of your preference.</span></span>
4. <span data-ttu-id="b1d6e-132">After you create the Application Insights resource, open it and note the instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-132">After you create the Application Insights resource, open it and note the instrumentation key.</span></span>

![Application Insights Overview and Instrumentation Key](./media/active-directory-b2c-custom-guide-eventlogger-appins/app-ins-key.png)

## <a name="step-2-add-new-claimtype-definitions-to-your-trust-framework-extension-file"></a><span data-ttu-id="b1d6e-134">Step 2.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-134">Step 2.</span></span> <span data-ttu-id="b1d6e-135">Add new ClaimType definitions to your trust framework extension file</span><span class="sxs-lookup"><span data-stu-id="b1d6e-135">Add new ClaimType definitions to your trust framework extension file</span></span>

<span data-ttu-id="b1d6e-136">Open the extension file from the starter pack and add the following elements to the `<BuildingBlocks>` node.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-136">Open the extension file from the starter pack and add the following elements to the `<BuildingBlocks>` node.</span></span> <span data-ttu-id="b1d6e-137">The file name is typically `yourtenant.onmicrosoft.com-B2C_1A_TrustFrameworkExtensions.xml`</span><span class="sxs-lookup"><span data-stu-id="b1d6e-137">The file name is typically `yourtenant.onmicrosoft.com-B2C_1A_TrustFrameworkExtensions.xml`</span></span>

```xml
<ClaimsSchema>
  <ClaimType Id="EventType">
    <DisplayName>EventType</DisplayName>
    <DataType>string</DataType>
    <AdminHelpText />
    <UserHelpText />
  </ClaimType>
  <ClaimType Id="PolicyId">
    <DisplayName>PolicyId</DisplayName>
    <DataType>string</DataType>
    <AdminHelpText />
    <UserHelpText />
  </ClaimType>
  <ClaimType Id="Culture">
    <DisplayName>Culture</DisplayName>
    <DataType>string</DataType>
    <AdminHelpText />
    <UserHelpText />
  </ClaimType>
  <ClaimType Id="CorrelationId">
    <DisplayName>CorrelationId</DisplayName>
    <DataType>string</DataType>
    <AdminHelpText />
    <UserHelpText />
  </ClaimType>
  <!--Additional claims used for passing claims to Application Insights Provider -->
  <ClaimType Id="federatedUser">
    <DisplayName>federatedUser</DisplayName>
    <DataType>boolean</DataType>
    <UserHelpText />
  </ClaimType>
  <ClaimType Id="parsedDomain">
    <DisplayName>Parsed Domain</DisplayName>
    <DataType>string</DataType>
    <UserHelpText>The domain portion of the email address.</UserHelpText>
  </ClaimType>
  <ClaimType Id="userInLocalDirectory">
    <DisplayName>userInLocalDirectory</DisplayName>
    <DataType>boolean</DataType>
    <UserHelpText />
  </ClaimType>
</ClaimsSchema>
```

## <a name="step-3-add-new-technical-profiles-that-use-the-application-insights-provider"></a><span data-ttu-id="b1d6e-138">Step 3.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-138">Step 3.</span></span> <span data-ttu-id="b1d6e-139">Add new technical profiles that use the Application Insights provider</span><span class="sxs-lookup"><span data-stu-id="b1d6e-139">Add new technical profiles that use the Application Insights provider</span></span>

<span data-ttu-id="b1d6e-140">Technical profiles can be considered functions in the Identity Experience Framework of Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-140">Technical profiles can be considered functions in the Identity Experience Framework of Azure AD B2C.</span></span> <span data-ttu-id="b1d6e-141">This example defines five technical profiles to open a session and post events:</span><span class="sxs-lookup"><span data-stu-id="b1d6e-141">This example defines five technical profiles to open a session and post events:</span></span>

| <span data-ttu-id="b1d6e-142">Technical Profile</span><span class="sxs-lookup"><span data-stu-id="b1d6e-142">Technical Profile</span></span> | <span data-ttu-id="b1d6e-143">Task</span><span class="sxs-lookup"><span data-stu-id="b1d6e-143">Task</span></span> |
| ----------------- | -----|
| <span data-ttu-id="b1d6e-144">AzureInsights-Common</span><span class="sxs-lookup"><span data-stu-id="b1d6e-144">AzureInsights-Common</span></span> | <span data-ttu-id="b1d6e-145">Creates a common set of parameters to be included in all AzureInsights technical profiles</span><span class="sxs-lookup"><span data-stu-id="b1d6e-145">Creates a common set of parameters to be included in all AzureInsights technical profiles</span></span> | 
| <span data-ttu-id="b1d6e-146">JourneyContextForInsights</span><span class="sxs-lookup"><span data-stu-id="b1d6e-146">JourneyContextForInsights</span></span> | <span data-ttu-id="b1d6e-147">Opens the session in Application Insights and sends a correlation ID</span><span class="sxs-lookup"><span data-stu-id="b1d6e-147">Opens the session in Application Insights and sends a correlation ID</span></span> |
| <span data-ttu-id="b1d6e-148">AzureInsights-SignInRequest</span><span class="sxs-lookup"><span data-stu-id="b1d6e-148">AzureInsights-SignInRequest</span></span> | <span data-ttu-id="b1d6e-149">Creates a `SignIn` event with a set of claims when a sign-in request has been received</span><span class="sxs-lookup"><span data-stu-id="b1d6e-149">Creates a `SignIn` event with a set of claims when a sign-in request has been received</span></span> | 
| <span data-ttu-id="b1d6e-150">AzureInsights-UserSignup</span><span class="sxs-lookup"><span data-stu-id="b1d6e-150">AzureInsights-UserSignup</span></span> | <span data-ttu-id="b1d6e-151">Creates a UserSignup event when the user triggers the sign-up option in a sign-up/sign-in journey</span><span class="sxs-lookup"><span data-stu-id="b1d6e-151">Creates a UserSignup event when the user triggers the sign-up option in a sign-up/sign-in journey</span></span> | 
| <span data-ttu-id="b1d6e-152">AzureInsights-SignInComplete</span><span class="sxs-lookup"><span data-stu-id="b1d6e-152">AzureInsights-SignInComplete</span></span> | <span data-ttu-id="b1d6e-153">Records the successful completion of an authentication when a token has been sent to the relying party application</span><span class="sxs-lookup"><span data-stu-id="b1d6e-153">Records the successful completion of an authentication when a token has been sent to the relying party application</span></span> | 

<span data-ttu-id="b1d6e-154">Add the profiles to the extension file from the starter pack by adding these elements to the `<ClaimsProviders>` node.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-154">Add the profiles to the extension file from the starter pack by adding these elements to the `<ClaimsProviders>` node.</span></span>  <span data-ttu-id="b1d6e-155">The file name is typically `yourtenant.onmicrosoft.com-B2C_1A_TrustFrameworkExtensions.xml`</span><span class="sxs-lookup"><span data-stu-id="b1d6e-155">The file name is typically `yourtenant.onmicrosoft.com-B2C_1A_TrustFrameworkExtensions.xml`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1d6e-156">Change the instrumentation key in the `ApplicationInsights-Common` technical profile to the GUID that your Application Insights resource provides.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-156">Change the instrumentation key in the `ApplicationInsights-Common` technical profile to the GUID that your Application Insights resource provides.</span></span>

```xml
<ClaimsProvider>
  <DisplayName>Application Insights</DisplayName>
  <TechnicalProfiles>
    <TechnicalProfile Id="JourneyContextForInsights">
      <DisplayName>Application Insights</DisplayName>
      <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.UserJourneyContextProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="CorrelationId" />
      </OutputClaims>
    </TechnicalProfile>
    <TechnicalProfile Id="AzureInsights-SignInRequest">
      <InputClaims>
        <!-- An input claim with a PartnerClaimType="eventName" is required. This is used by the AzureApplicationInsightsProvider to create an event with the specified value. -->
        <InputClaim ClaimTypeReferenceId="EventType" PartnerClaimType="eventName" DefaultValue="SignInRequest" />
      </InputClaims>
      <IncludeTechnicalProfile ReferenceId="AzureInsights-Common" />
    </TechnicalProfile>
    <TechnicalProfile Id="AzureInsights-SignInComplete">
      <InputClaims>
        <InputClaim ClaimTypeReferenceId="EventType" PartnerClaimType="eventName" DefaultValue="SignInComplete" />
        <InputClaim ClaimTypeReferenceId="federatedUser" PartnerClaimType="{property:FederatedUser}" DefaultValue="false" />
        <InputClaim ClaimTypeReferenceId="parsedDomain" PartnerClaimType="{property:FederationPartner}" DefaultValue="Not Applicable" />
      </InputClaims>
      <IncludeTechnicalProfile ReferenceId="AzureInsights-Common" />
    </TechnicalProfile>
    <TechnicalProfile Id="AzureInsights-UserSignup">
      <InputClaims>
        <InputClaim ClaimTypeReferenceId="EventType" PartnerClaimType="eventName" DefaultValue="UserSignup" />
      </InputClaims>
      <IncludeTechnicalProfile ReferenceId="AzureInsights-Common" />
    </TechnicalProfile>
    <TechnicalProfile Id="AzureInsights-Common">
      <DisplayName>Alternate Email</DisplayName>
      <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.Insights.AzureApplicationInsightsProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
      <Metadata>
        <!-- The ApplicationInsights instrumentation key which will be used for logging the events -->
        <Item Key="InstrumentationKey">xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</Item>
        <!-- A Boolean that indicates whether developer mode is enabled. This controls how events are buffered. In a development environment with minimal event volume, enabling developer mode results in events being sent immediately to ApplicationInsights. -->
        <Item Key="DeveloperMode">false</Item>
        <!-- A Boolean that indicates whether telemetry should be enabled or not. -->
        <Item Key="DisableTelemetry ">false</Item>
      </Metadata>
      <InputClaims>
        <!-- Properties of an event are added through the syntax {property:NAME}, where NAME is property being added to the event. DefaultValue can be either a static value or a value that's resolved by one of the supported DefaultClaimResolvers. -->
        <InputClaim ClaimTypeReferenceId="PolicyId" PartnerClaimType="{property:Policy}" DefaultValue="{Policy:PolicyId}" />
        <InputClaim ClaimTypeReferenceId="CorrelationId" PartnerClaimType="{property:JourneyId}" />
        <InputClaim ClaimTypeReferenceId="Culture" PartnerClaimType="{property:Culture}" DefaultValue="{Culture:RFC5646}" />
      </InputClaims>
    </TechnicalProfile>
  </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="step-4-add-the-technical-profiles-for-application-insights-as-orchestration-steps-in-an-existing-user-journey"></a><span data-ttu-id="b1d6e-157">Step 4.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-157">Step 4.</span></span> <span data-ttu-id="b1d6e-158">Add the technical profiles for Application Insights as orchestration steps in an existing user journey</span><span class="sxs-lookup"><span data-stu-id="b1d6e-158">Add the technical profiles for Application Insights as orchestration steps in an existing user journey</span></span>

<span data-ttu-id="b1d6e-159">Call `JournyeContextForInsights` as orchestration step 1:</span><span class="sxs-lookup"><span data-stu-id="b1d6e-159">Call `JournyeContextForInsights` as orchestration step 1:</span></span>

```xml
<!-- Initialize a session with Application Insights -->
<OrchestrationStep Order="1" Type="ClaimsExchange">
  <ClaimsExchanges>
    <ClaimsExchange Id="JourneyContextForInsights" TechnicalProfileReferenceId="JourneyContextForInsights" />
  </ClaimsExchanges>
</OrchestrationStep>
```

<span data-ttu-id="b1d6e-160">Call `Azure-Insights-SignInRequest` as orchestration step 2 to track that a sign-in/sign-up request has been received:</span><span class="sxs-lookup"><span data-stu-id="b1d6e-160">Call `Azure-Insights-SignInRequest` as orchestration step 2 to track that a sign-in/sign-up request has been received:</span></span>

```xml
<!-- Track that we have received a sign in request -->
<OrchestrationStep Order="2" Type="ClaimsExchange">
  <ClaimsExchanges>
    <ClaimsExchange Id="TrackSignInRequest" TechnicalProfileReferenceId="AzureInsights-SignInRequest" />
  </ClaimsExchanges>
</OrchestrationStep>
```

<span data-ttu-id="b1d6e-161">Immediately *before* the `SendClaims` orchestration step, add a new step that calls `Azure-Insights-UserSignup`.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-161">Immediately *before* the `SendClaims` orchestration step, add a new step that calls `Azure-Insights-UserSignup`.</span></span> <span data-ttu-id="b1d6e-162">It's triggered when the user selects the sign-up button in a sign-up/sign-in journey.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-162">It's triggered when the user selects the sign-up button in a sign-up/sign-in journey.</span></span>

```xml
<!-- Handles the user clicking the sign up link in the local account sign in page -->
<OrchestrationStep Order="9" Type="ClaimsExchange">
  <Preconditions>
    <Precondition Type="ClaimsExist" ExecuteActionsIf="false">
      <Value>newUser</Value>
      <Action>SkipThisOrchestrationStep</Action>
    </Precondition>
    <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
      <Value>newUser</Value>
      <Value>false</Value>
      <Action>SkipThisOrchestrationStep</Action>
    </Precondition>
  </Preconditions>
  <ClaimsExchanges>
    <ClaimsExchange Id="TrackUserSignUp" TechnicalProfileReferenceId="AzureInsights-UserSignup" />
  </ClaimsExchanges>
```

<span data-ttu-id="b1d6e-163">Immediately after the `SendClaims` orchestration step, call `Azure-Insights-SignInComplete`.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-163">Immediately after the `SendClaims` orchestration step, call `Azure-Insights-SignInComplete`.</span></span> <span data-ttu-id="b1d6e-164">This step reflects a successfully completed journey.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-164">This step reflects a successfully completed journey.</span></span>

```xml
<!-- Track that we have successfully sent a token -->
<OrchestrationStep Order="11" Type="ClaimsExchange">
  <ClaimsExchanges>
    <ClaimsExchange Id="TrackSignInComplete" TechnicalProfileReferenceId="AzureInsights-SignInComplete" />
  </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="b1d6e-165">After you add the new orchestration steps, renumber the steps sequentially without skipping any integers from 1 to N.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-165">After you add the new orchestration steps, renumber the steps sequentially without skipping any integers from 1 to N.</span></span>


## <a name="step-5-upload-your-modified-extensions-file-run-the-policy-and-view-events-in-application-insights"></a><span data-ttu-id="b1d6e-166">Step 5.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-166">Step 5.</span></span> <span data-ttu-id="b1d6e-167">Upload your modified extensions file, run the policy, and view events in Application Insights</span><span class="sxs-lookup"><span data-stu-id="b1d6e-167">Upload your modified extensions file, run the policy, and view events in Application Insights</span></span>

<span data-ttu-id="b1d6e-168">Save and upload the new trust framework extension file.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-168">Save and upload the new trust framework extension file.</span></span> <span data-ttu-id="b1d6e-169">Then, call the relying party policy from your application or use `Run Now` in the Azure AD B2C interface.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-169">Then, call the relying party policy from your application or use `Run Now` in the Azure AD B2C interface.</span></span> <span data-ttu-id="b1d6e-170">In seconds, your events are available in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-170">In seconds, your events are available in Application Insights.</span></span>

1. <span data-ttu-id="b1d6e-171">Open the **Application Insights** resource in your Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-171">Open the **Application Insights** resource in your Azure Active Directory tenant.</span></span>
2. <span data-ttu-id="b1d6e-172">Select **Usage** > **Events**.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-172">Select **Usage** > **Events**.</span></span>
3. <span data-ttu-id="b1d6e-173">Set **During** to **Last hour** and **By** to **3 minutes**.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-173">Set **During** to **Last hour** and **By** to **3 minutes**.</span></span>  <span data-ttu-id="b1d6e-174">You might need to select **Refresh** to view results.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-174">You might need to select **Refresh** to view results.</span></span>

![Application Insights USAGE-Events Blase](./media/active-directory-b2c-custom-guide-eventlogger-appins/app-ins-graphic.png)

##  <a name="next-steps"></a><span data-ttu-id="b1d6e-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1d6e-176">Next steps</span></span>

<span data-ttu-id="b1d6e-177">Add claim types and events to your user journey to fit your needs.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-177">Add claim types and events to your user journey to fit your needs.</span></span> <span data-ttu-id="b1d6e-178">Here is a list of possible claims, using additional claims resolvers</span><span class="sxs-lookup"><span data-stu-id="b1d6e-178">Here is a list of possible claims, using additional claims resolvers</span></span>

### <a name="culture-specific-claims"></a><span data-ttu-id="b1d6e-179">Culture-specific claims</span><span class="sxs-lookup"><span data-stu-id="b1d6e-179">Culture-specific claims</span></span>

```xml
Referenced using: {Culture:One of the property names below}
```

| <span data-ttu-id="b1d6e-180">Claim</span><span class="sxs-lookup"><span data-stu-id="b1d6e-180">Claim</span></span> | <span data-ttu-id="b1d6e-181">Definition</span><span class="sxs-lookup"><span data-stu-id="b1d6e-181">Definition</span></span> | <span data-ttu-id="b1d6e-182">Example</span><span class="sxs-lookup"><span data-stu-id="b1d6e-182">Example</span></span> |
| ----- | -----------| --------|
| <span data-ttu-id="b1d6e-183">LanguageName</span><span class="sxs-lookup"><span data-stu-id="b1d6e-183">LanguageName</span></span> | <span data-ttu-id="b1d6e-184">The two letter ISO code for the language</span><span class="sxs-lookup"><span data-stu-id="b1d6e-184">The two letter ISO code for the language</span></span> | <span data-ttu-id="b1d6e-185">en</span><span class="sxs-lookup"><span data-stu-id="b1d6e-185">en</span></span> |
| <span data-ttu-id="b1d6e-186">RegionName</span><span class="sxs-lookup"><span data-stu-id="b1d6e-186">RegionName</span></span> | <span data-ttu-id="b1d6e-187">The two letter ISO code for the region</span><span class="sxs-lookup"><span data-stu-id="b1d6e-187">The two letter ISO code for the region</span></span> | <span data-ttu-id="b1d6e-188">US</span><span class="sxs-lookup"><span data-stu-id="b1d6e-188">US</span></span> |
| <span data-ttu-id="b1d6e-189">RFC5646</span><span class="sxs-lookup"><span data-stu-id="b1d6e-189">RFC5646</span></span> | <span data-ttu-id="b1d6e-190">The RFC5646 language code</span><span class="sxs-lookup"><span data-stu-id="b1d6e-190">The RFC5646 language code</span></span> | <span data-ttu-id="b1d6e-191">en-US</span><span class="sxs-lookup"><span data-stu-id="b1d6e-191">en-US</span></span> |
| <span data-ttu-id="b1d6e-192">LCID</span><span class="sxs-lookup"><span data-stu-id="b1d6e-192">LCID</span></span>   | <span data-ttu-id="b1d6e-193">The LCID of language code</span><span class="sxs-lookup"><span data-stu-id="b1d6e-193">The LCID of language code</span></span> | <span data-ttu-id="b1d6e-194">1033</span><span class="sxs-lookup"><span data-stu-id="b1d6e-194">1033</span></span> |

### <a name="policy-specific-claims"></a><span data-ttu-id="b1d6e-195">Policy-specific claims</span><span class="sxs-lookup"><span data-stu-id="b1d6e-195">Policy-specific claims</span></span>

```xml
Referenced using {Policy:One of the property names below}
```

| <span data-ttu-id="b1d6e-196">Claim</span><span class="sxs-lookup"><span data-stu-id="b1d6e-196">Claim</span></span> | <span data-ttu-id="b1d6e-197">Definition</span><span class="sxs-lookup"><span data-stu-id="b1d6e-197">Definition</span></span> | <span data-ttu-id="b1d6e-198">Example</span><span class="sxs-lookup"><span data-stu-id="b1d6e-198">Example</span></span> |
| ----- | -----------| --------|
| <span data-ttu-id="b1d6e-199">TrustFrameworkTenantId</span><span class="sxs-lookup"><span data-stu-id="b1d6e-199">TrustFrameworkTenantId</span></span> | <span data-ttu-id="b1d6e-200">The trustframework tenant id</span><span class="sxs-lookup"><span data-stu-id="b1d6e-200">The trustframework tenant id</span></span> | <span data-ttu-id="b1d6e-201">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-201">N/A</span></span> |
| <span data-ttu-id="b1d6e-202">RelyingPartyTenantId</span><span class="sxs-lookup"><span data-stu-id="b1d6e-202">RelyingPartyTenantId</span></span> | <span data-ttu-id="b1d6e-203">The tenant id of the relying party</span><span class="sxs-lookup"><span data-stu-id="b1d6e-203">The tenant id of the relying party</span></span> | <span data-ttu-id="b1d6e-204">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-204">N/A</span></span> |
| <span data-ttu-id="b1d6e-205">PolicyId</span><span class="sxs-lookup"><span data-stu-id="b1d6e-205">PolicyId</span></span> | <span data-ttu-id="b1d6e-206">The policy id of the policy</span><span class="sxs-lookup"><span data-stu-id="b1d6e-206">The policy id of the policy</span></span> | <span data-ttu-id="b1d6e-207">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-207">N/A</span></span> |
| <span data-ttu-id="b1d6e-208">TenantObjectId</span><span class="sxs-lookup"><span data-stu-id="b1d6e-208">TenantObjectId</span></span> | <span data-ttu-id="b1d6e-209">The tenant object id of the policy</span><span class="sxs-lookup"><span data-stu-id="b1d6e-209">The tenant object id of the policy</span></span> | <span data-ttu-id="b1d6e-210">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-210">N/A</span></span> |

### <a name="openid-connect-specific-claims"></a><span data-ttu-id="b1d6e-211">OpenID Connect-specific claims</span><span class="sxs-lookup"><span data-stu-id="b1d6e-211">OpenID Connect-specific claims</span></span>

```xml
Referenced using {OIDC:One of the property names below}
```

| <span data-ttu-id="b1d6e-212">Claim</span><span class="sxs-lookup"><span data-stu-id="b1d6e-212">Claim</span></span> | <span data-ttu-id="b1d6e-213">OpenIdConnect parameter</span><span class="sxs-lookup"><span data-stu-id="b1d6e-213">OpenIdConnect parameter</span></span> | <span data-ttu-id="b1d6e-214">Example</span><span class="sxs-lookup"><span data-stu-id="b1d6e-214">Example</span></span> |
| ----- | ----------------------- | --------|
| <span data-ttu-id="b1d6e-215">Prompt</span><span class="sxs-lookup"><span data-stu-id="b1d6e-215">Prompt</span></span> | <span data-ttu-id="b1d6e-216">prompt</span><span class="sxs-lookup"><span data-stu-id="b1d6e-216">prompt</span></span> | <span data-ttu-id="b1d6e-217">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-217">N/A</span></span> |
| <span data-ttu-id="b1d6e-218">LoginHint</span><span class="sxs-lookup"><span data-stu-id="b1d6e-218">LoginHint</span></span> |  <span data-ttu-id="b1d6e-219">login_hint</span><span class="sxs-lookup"><span data-stu-id="b1d6e-219">login_hint</span></span> | <span data-ttu-id="b1d6e-220">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-220">N/A</span></span> |
| <span data-ttu-id="b1d6e-221">DomainHint</span><span class="sxs-lookup"><span data-stu-id="b1d6e-221">DomainHint</span></span> | <span data-ttu-id="b1d6e-222">domain_hint</span><span class="sxs-lookup"><span data-stu-id="b1d6e-222">domain_hint</span></span> | <span data-ttu-id="b1d6e-223">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-223">N/A</span></span> |
|  <span data-ttu-id="b1d6e-224">MaxAge</span><span class="sxs-lookup"><span data-stu-id="b1d6e-224">MaxAge</span></span> | <span data-ttu-id="b1d6e-225">max_age</span><span class="sxs-lookup"><span data-stu-id="b1d6e-225">max_age</span></span> | <span data-ttu-id="b1d6e-226">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-226">N/A</span></span> |
| <span data-ttu-id="b1d6e-227">ClientId</span><span class="sxs-lookup"><span data-stu-id="b1d6e-227">ClientId</span></span> | <span data-ttu-id="b1d6e-228">client_id</span><span class="sxs-lookup"><span data-stu-id="b1d6e-228">client_id</span></span> | <span data-ttu-id="b1d6e-229">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-229">N/A</span></span> |
| <span data-ttu-id="b1d6e-230">Username</span><span class="sxs-lookup"><span data-stu-id="b1d6e-230">Username</span></span> | <span data-ttu-id="b1d6e-231">login_hint</span><span class="sxs-lookup"><span data-stu-id="b1d6e-231">login_hint</span></span> | <span data-ttu-id="b1d6e-232">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-232">N/A</span></span> |
|  <span data-ttu-id="b1d6e-233">Resource</span><span class="sxs-lookup"><span data-stu-id="b1d6e-233">Resource</span></span> | <span data-ttu-id="b1d6e-234">resource</span><span class="sxs-lookup"><span data-stu-id="b1d6e-234">resource</span></span>| <span data-ttu-id="b1d6e-235">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-235">N/A</span></span> |
| <span data-ttu-id="b1d6e-236">AuthenticationContextReferences</span><span class="sxs-lookup"><span data-stu-id="b1d6e-236">AuthenticationContextReferences</span></span> | <span data-ttu-id="b1d6e-237">acr_values</span><span class="sxs-lookup"><span data-stu-id="b1d6e-237">acr_values</span></span> | <span data-ttu-id="b1d6e-238">N/A</span><span class="sxs-lookup"><span data-stu-id="b1d6e-238">N/A</span></span> |

### <a name="non-protocol-parameters-included-with-oidc--oauth2-requests"></a><span data-ttu-id="b1d6e-239">Non-protocol parameters included with OIDC & OAuth2 requests</span><span class="sxs-lookup"><span data-stu-id="b1d6e-239">Non-protocol parameters included with OIDC & OAuth2 requests</span></span>

```xml
Referenced using { OAUTH-KV:Querystring parameter name }
```

<span data-ttu-id="b1d6e-240">Any parameter name included as part of an OIDC or OAuth2 request can be mapped to a claim in the user journey.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-240">Any parameter name included as part of an OIDC or OAuth2 request can be mapped to a claim in the user journey.</span></span> <span data-ttu-id="b1d6e-241">You can then record it in the event.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-241">You can then record it in the event.</span></span> <span data-ttu-id="b1d6e-242">For example, the request from the application might include a query string parameter with a name of `app_session`, `loyalty_number` or `any_string`.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-242">For example, the request from the application might include a query string parameter with a name of `app_session`, `loyalty_number` or `any_string`.</span></span>

<span data-ttu-id="b1d6e-243">Here's a sample request from the application:</span><span class="sxs-lookup"><span data-stu-id="b1d6e-243">Here's a sample request from the application:</span></span>

```
https://sampletenant.b2clogin.com/tfp/sampletenant.onmicrosoft.com/B2C_1A_signup_signin/oauth2/v2.0/authorize?client_id=e1d2612f-c2bc-4599-8e7b-d874eaca1ae1&nonce=defaultNonce&redirect_uri=https%3A%2F%2Fjwt.ms&scope=openid&response_type=id_token&prompt=login&app_session=0a2b45c&loyalty_number=1234567

```
<span data-ttu-id="b1d6e-244">You can then add the claims by adding an `Input Claim` element to the Application Insights event.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-244">You can then add the claims by adding an `Input Claim` element to the Application Insights event.</span></span> <span data-ttu-id="b1d6e-245">Properties of an event are added through the syntax {property:NAME}, where NAME is property being added to the event.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-245">Properties of an event are added through the syntax {property:NAME}, where NAME is property being added to the event.</span></span> <span data-ttu-id="b1d6e-246">For example:</span><span class="sxs-lookup"><span data-stu-id="b1d6e-246">For example:</span></span>

```
<InputClaim ClaimTypeReferenceId="app_session" PartnerClaimType="{property:app_session}" DefaultValue="{OAUTH-KV:app_session}" />
<InputClaim ClaimTypeReferenceId="loyalty_number" PartnerClaimType="{property:loyalty_number}" DefaultValue="{OAUTH-KV:loyalty_number}" />
```

### <a name="other-system-claims"></a><span data-ttu-id="b1d6e-247">Other system claims</span><span class="sxs-lookup"><span data-stu-id="b1d6e-247">Other system claims</span></span>

<span data-ttu-id="b1d6e-248">Some system claims must be added to the claims bag before they are available to record as events.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-248">Some system claims must be added to the claims bag before they are available to record as events.</span></span> <span data-ttu-id="b1d6e-249">The technical profile `SimpleUJContext` must be called as an orchestration step or a validation technical profile before these claims are available.</span><span class="sxs-lookup"><span data-stu-id="b1d6e-249">The technical profile `SimpleUJContext` must be called as an orchestration step or a validation technical profile before these claims are available.</span></span>

```xml
<ClaimsProvider>
  <DisplayName>User Journey Context Provider</DisplayName>
  <TechnicalProfiles>
    <TechnicalProfile Id="SimpleUJContext">
      <DisplayName>User Journey Context Provide</DisplayName>
      <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.UserJourneyContextProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="IP-Address" />
        <OutputClaim ClaimTypeReferenceId="CorrelationId" />
        <OutputClaim ClaimTypeReferenceId="DateTimeInUtc" />
        <OutputClaim ClaimTypeReferenceId="Build" />
      </OutputClaims>
    </TechnicalProfile>
  </TechnicalProfiles>
</ClaimsProvider>
```


