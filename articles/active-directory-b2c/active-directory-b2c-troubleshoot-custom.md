---
title: Application Insights to troubleshoot Custom Policies in Azure Active Directory B2C | Microsoft Docs
description: how to setup Application Insights to trace the execution of custom policies.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/04/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: e4b33552c4b070164b55a84f1d8586422aced2f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865537"
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="c9c31-103">Azure Active Directory B2C: Collecting Logs</span><span class="sxs-lookup"><span data-stu-id="c9c31-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="c9c31-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span><span class="sxs-lookup"><span data-stu-id="c9c31-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="c9c31-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span><span class="sxs-lookup"><span data-stu-id="c9c31-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="c9c31-106">Do not use development mode  in production.</span><span class="sxs-lookup"><span data-stu-id="c9c31-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="c9c31-107">Logs collect all claims sent to and from the identity providers during development.</span><span class="sxs-lookup"><span data-stu-id="c9c31-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="c9c31-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span><span class="sxs-lookup"><span data-stu-id="c9c31-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="c9c31-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span><span class="sxs-lookup"><span data-stu-id="c9c31-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="c9c31-110">Use Application Insights</span><span class="sxs-lookup"><span data-stu-id="c9c31-110">Use Application Insights</span></span>

<span data-ttu-id="c9c31-111">Azure AD B2C supports a feature for sending data to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c31-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="c9c31-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span><span class="sxs-lookup"><span data-stu-id="c9c31-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="c9c31-113">Setup Application Insights</span><span class="sxs-lookup"><span data-stu-id="c9c31-113">Setup Application Insights</span></span>

1. <span data-ttu-id="c9c31-114">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9c31-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c9c31-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span><span class="sxs-lookup"><span data-stu-id="c9c31-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="c9c31-116">Click **+ New** in the left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c9c31-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="c9c31-117">Search for and select **Application Insights**, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c9c31-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="c9c31-118">Complete the form and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c9c31-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="c9c31-119">Select **General** for the **Application Type**.</span><span class="sxs-lookup"><span data-stu-id="c9c31-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="c9c31-120">Once the resource has been created, open the Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="c9c31-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="c9c31-121">Find **Properties** in the left-menu, and click on it.</span><span class="sxs-lookup"><span data-stu-id="c9c31-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="c9c31-122">Copy the **Instrumentation Key** and save it for the next section.</span><span class="sxs-lookup"><span data-stu-id="c9c31-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="c9c31-123">Set up the custom policy</span><span class="sxs-lookup"><span data-stu-id="c9c31-123">Set up the custom policy</span></span>

1. <span data-ttu-id="c9c31-124">Open the RP file (for example, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="c9c31-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="c9c31-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span><span class="sxs-lookup"><span data-stu-id="c9c31-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="c9c31-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span><span class="sxs-lookup"><span data-stu-id="c9c31-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="c9c31-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="UserJourney Id from your extensions policy, or equivalent (for example:SignUpOrSigninWithAAD" />`</span><span class="sxs-lookup"><span data-stu-id="c9c31-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="UserJourney Id from your extensions policy, or equivalent (for example:SignUpOrSigninWithAAD" />`</span></span>
2. <span data-ttu-id="c9c31-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span><span class="sxs-lookup"><span data-stu-id="c9c31-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="c9c31-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span><span class="sxs-lookup"><span data-stu-id="c9c31-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="c9c31-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span><span class="sxs-lookup"><span data-stu-id="c9c31-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="c9c31-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span><span class="sxs-lookup"><span data-stu-id="c9c31-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="c9c31-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c31-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="c9c31-133">Sample:</span><span class="sxs-lookup"><span data-stu-id="c9c31-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="UserJourney ID from your extensions policy, or equivalent (for example: SignUpOrSigninWithAzureAD)" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="c9c31-134">Upload the policy.</span><span class="sxs-lookup"><span data-stu-id="c9c31-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="c9c31-135">See the logs in Application Insights</span><span class="sxs-lookup"><span data-stu-id="c9c31-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="c9c31-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c31-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="c9c31-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9c31-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="c9c31-138">In the **Overview** menu, click on **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="c9c31-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="c9c31-139">Open a new tab in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9c31-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="c9c31-140">Here is a list of queries you can use to see the logs</span><span class="sxs-lookup"><span data-stu-id="c9c31-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="c9c31-141">Query</span><span class="sxs-lookup"><span data-stu-id="c9c31-141">Query</span></span> | <span data-ttu-id="c9c31-142">Description</span><span class="sxs-lookup"><span data-stu-id="c9c31-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="c9c31-143">traces</span><span class="sxs-lookup"><span data-stu-id="c9c31-143">traces</span></span> | <span data-ttu-id="c9c31-144">See all of the logs generated by Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c9c31-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="c9c31-145">traces \| where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="c9c31-145">traces \| where timestamp > ago(1d)</span></span> | <span data-ttu-id="c9c31-146">See all of the logs generated by Azure AD B2C for the last day</span><span class="sxs-lookup"><span data-stu-id="c9c31-146">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="c9c31-147">The entries may be long.</span><span class="sxs-lookup"><span data-stu-id="c9c31-147">The entries may be long.</span></span>  <span data-ttu-id="c9c31-148">Export to CSV for a closer look.</span><span class="sxs-lookup"><span data-stu-id="c9c31-148">Export to CSV for a closer look.</span></span>

<span data-ttu-id="c9c31-149">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="c9c31-149">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="c9c31-150">The community has developed a user journey viewer to help identity developers.</span><span class="sxs-lookup"><span data-stu-id="c9c31-150">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="c9c31-151">It is not supported by Microsoft and made available strictly as-is.</span><span class="sxs-lookup"><span data-stu-id="c9c31-151">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="c9c31-152">It reads from your Application Insights instance and provides a well-structured view of the user journey events.</span><span class="sxs-lookup"><span data-stu-id="c9c31-152">It reads from your Application Insights instance and provides a well-structured view of the user journey events.</span></span>  <span data-ttu-id="c9c31-153">You obtain the source code and deploy it in your own solution.</span><span class="sxs-lookup"><span data-stu-id="c9c31-153">You obtain the source code and deploy it in your own solution.</span></span>

<span data-ttu-id="c9c31-154">The version of the viewer that reads events from Application Insights is located [here](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/wingtipgamesb2c/src/WingTipUserJourneyPlayerWebApplication)</span><span class="sxs-lookup"><span data-stu-id="c9c31-154">The version of the viewer that reads events from Application Insights is located [here](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/wingtipgamesb2c/src/WingTipUserJourneyPlayerWebApplication)</span></span>

>[!NOTE]
><span data-ttu-id="c9c31-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span><span class="sxs-lookup"><span data-stu-id="c9c31-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="c9c31-156">Do not use development mode in production.</span><span class="sxs-lookup"><span data-stu-id="c9c31-156">Do not use development mode in production.</span></span>  <span data-ttu-id="c9c31-157">Logs collect all claims sent to and from the identity providers during development.</span><span class="sxs-lookup"><span data-stu-id="c9c31-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="c9c31-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span><span class="sxs-lookup"><span data-stu-id="c9c31-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="c9c31-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span><span class="sxs-lookup"><span data-stu-id="c9c31-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="c9c31-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span><span class="sxs-lookup"><span data-stu-id="c9c31-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="c9c31-161">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c9c31-161">Next Steps</span></span>

<span data-ttu-id="c9c31-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span><span class="sxs-lookup"><span data-stu-id="c9c31-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
