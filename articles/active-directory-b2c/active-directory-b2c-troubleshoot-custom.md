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
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: Collecting Logs

This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.

>[!NOTE]
>Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies. Do not use development mode  in production.  Logs collect all claims sent to and from the identity providers during development.  If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.  These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.


## <a name="use-application-insights"></a>Use Application Insights

Azure AD B2C supports a feature for sending data to Application Insights.  Application Insights provides a way to diagnose exceptions and visualize application performance issues.

### <a name="setup-application-insights"></a>Setup Application Insights

1. Go to the [Azure portal](https://portal.azure.com). Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).
1. Click **+ New** in the left-hand navigation menu.
1. Search for and select **Application Insights**, then click **Create**.
1. Complete the form and click **Create**. Select **General** for the **Application Type**.
1. Once the resource has been created, open the Application Insights resource.
1. Find **Properties** in the left-menu, and click on it.
1. Copy the **Instrumentation Key** and save it for the next section.

### <a name="set-up-the-custom-policy"></a>Set up the custom policy

1. Open the RP file (for example, SignUpOrSignin.xml).
1. Add the following attributes to the `<TrustFrameworkPolicy>` element:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node. It must be located immediately after the `<DefaultUserJourney ReferenceId="UserJourney Id from your extensions policy, or equivalent (for example:SignUpOrSigninWithAAD" />`
2. Add the following node as a child of the `<UserJourneyBehaviors>` element. Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.
  * `ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).
  * `ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.
Sample:

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

3. Upload the policy.

### <a name="see-the-logs-in-application-insights"></a>See the logs in Application Insights

>[!NOTE]
> There is a short delay (less than five minutes) before you can see new logs in Application Insights.

1. Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).
1. In the **Overview** menu, click on **Analytics**.
1. Open a new tab in Application Insights.
1. Here is a list of queries you can use to see the logs

| Query | Description |
|---------------------|--------------------|
traces | See all of the logs generated by Azure AD B2C |
traces \| where timestamp > ago(1d) | See all of the logs generated by Azure AD B2C for the last day

The entries may be long.  Export to CSV for a closer look.

You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>The community has developed a user journey viewer to help identity developers.  It is not supported by Microsoft and made available strictly as-is.  It reads from your Application Insights instance and provides a well-structured view of the user journey events.  You obtain the source code and deploy it in your own solution.

The version of the viewer that reads events from Application Insights is located [here](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/wingtipgamesb2c/src/WingTipUserJourneyPlayerWebApplication)

>[!NOTE]
>Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies. Do not use development mode in production.  Logs collect all claims sent to and from the identity providers during development.  If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.  These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.

[Github Repository for Unsupported Custom Policy Samples and Related tools](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Next Steps

Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.