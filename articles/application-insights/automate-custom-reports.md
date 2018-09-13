---
title: Automate custom reports with Azure Application Insights data
description: Automate custom daily/weekly/monthly reports with Azure Application Insights data
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 06/25/2018
ms.reviewer: sdash
ms.author: mbullwin
ms.openlocfilehash: 9f08f134fc23ec7f7ad80e356832c54b937de3e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965925"
---
# <a name="automate-custom-reports-with-azure-application-insights-data"></a><span data-ttu-id="18ffd-103">Automate custom reports with Azure Application Insights data</span><span class="sxs-lookup"><span data-stu-id="18ffd-103">Automate custom reports with Azure Application Insights data</span></span>

<span data-ttu-id="18ffd-104">Periodical reports help keep a team informed on how their business critical services are doing.</span><span class="sxs-lookup"><span data-stu-id="18ffd-104">Periodical reports help keep a team informed on how their business critical services are doing.</span></span> <span data-ttu-id="18ffd-105">Developers, DevOps/SRE teams, and their managers can be productive with automated reports reliably delivering insights without requiring everyone to sign in the portal.</span><span class="sxs-lookup"><span data-stu-id="18ffd-105">Developers, DevOps/SRE teams, and their managers can be productive with automated reports reliably delivering insights without requiring everyone to sign in the portal.</span></span> <span data-ttu-id="18ffd-106">Such reports can also help identify gradual increases in latencies, load or failure rates that may not trigger any alert rules.</span><span class="sxs-lookup"><span data-stu-id="18ffd-106">Such reports can also help identify gradual increases in latencies, load or failure rates that may not trigger any alert rules.</span></span>

<span data-ttu-id="18ffd-107">Each enterprise has its unique reporting needs, such as:</span><span class="sxs-lookup"><span data-stu-id="18ffd-107">Each enterprise has its unique reporting needs, such as:</span></span> 

* <span data-ttu-id="18ffd-108">Specific percentile aggregations of metrics, or custom metrics in a report.</span><span class="sxs-lookup"><span data-stu-id="18ffd-108">Specific percentile aggregations of metrics, or custom metrics in a report.</span></span>
* <span data-ttu-id="18ffd-109">Have different reports for daily, weekly, and monthly roll-ups of data for different audiences.</span><span class="sxs-lookup"><span data-stu-id="18ffd-109">Have different reports for daily, weekly, and monthly roll-ups of data for different audiences.</span></span>
* <span data-ttu-id="18ffd-110">Segmentation by custom attributes like region, or environment.</span><span class="sxs-lookup"><span data-stu-id="18ffd-110">Segmentation by custom attributes like region, or environment.</span></span> 
* <span data-ttu-id="18ffd-111">Group some AI resources together in a single report, even if they may be in different subscriptions or resource groups etc.</span><span class="sxs-lookup"><span data-stu-id="18ffd-111">Group some AI resources together in a single report, even if they may be in different subscriptions or resource groups etc.</span></span>
* <span data-ttu-id="18ffd-112">Separate reports containing sensitive metrics sent to selective audience.</span><span class="sxs-lookup"><span data-stu-id="18ffd-112">Separate reports containing sensitive metrics sent to selective audience.</span></span>
* <span data-ttu-id="18ffd-113">Reports to stakeholders who may not have access to the portal resources.</span><span class="sxs-lookup"><span data-stu-id="18ffd-113">Reports to stakeholders who may not have access to the portal resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="18ffd-114">The weekly Application Insights digest email did not allow any customization, and will be discontinued in favor of the custom options listed below.</span><span class="sxs-lookup"><span data-stu-id="18ffd-114">The weekly Application Insights digest email did not allow any customization, and will be discontinued in favor of the custom options listed below.</span></span> <span data-ttu-id="18ffd-115">The last weekly digest email will be sent on June 11, 2018.</span><span class="sxs-lookup"><span data-stu-id="18ffd-115">The last weekly digest email will be sent on June 11, 2018.</span></span> <span data-ttu-id="18ffd-116">Please configure one of the following options to get similar custom reports (use the query suggested below).</span><span class="sxs-lookup"><span data-stu-id="18ffd-116">Please configure one of the following options to get similar custom reports (use the query suggested below).</span></span>

## <a name="to-automate-custom-report-emails"></a><span data-ttu-id="18ffd-117">To automate custom report emails</span><span class="sxs-lookup"><span data-stu-id="18ffd-117">To automate custom report emails</span></span>

<span data-ttu-id="18ffd-118">You can [programmatically query Application Insights](https://dev.applicationinsights.io/) data to generate custom reports on a schedule.</span><span class="sxs-lookup"><span data-stu-id="18ffd-118">You can [programmatically query Application Insights](https://dev.applicationinsights.io/) data to generate custom reports on a schedule.</span></span> <span data-ttu-id="18ffd-119">The following options can help you get started quickly:</span><span class="sxs-lookup"><span data-stu-id="18ffd-119">The following options can help you get started quickly:</span></span>

* [<span data-ttu-id="18ffd-120">Automate reports with Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="18ffd-120">Automate reports with Microsoft Flow</span></span>](app-insights-automate-with-flow.md)
* [<span data-ttu-id="18ffd-121">Automate reports with Logic Apps</span><span class="sxs-lookup"><span data-stu-id="18ffd-121">Automate reports with Logic Apps</span></span>](automate-with-logic-apps.md)
* <span data-ttu-id="18ffd-122">Use the "Application Insights scheduled digest" [Azure function](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) template in the Monitoring scenario.</span><span class="sxs-lookup"><span data-stu-id="18ffd-122">Use the "Application Insights scheduled digest" [Azure function](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) template in the Monitoring scenario.</span></span> <span data-ttu-id="18ffd-123">This function uses SendGrid to deliver the email.</span><span class="sxs-lookup"><span data-stu-id="18ffd-123">This function uses SendGrid to deliver the email.</span></span> 

    ![Azure function template](./media/automate-custom-reports/azure-function-template.png)

## <a name="sample-query-for-a-weekly-digest-email"></a><span data-ttu-id="18ffd-125">Sample query for a weekly digest email</span><span class="sxs-lookup"><span data-stu-id="18ffd-125">Sample query for a weekly digest email</span></span>
<span data-ttu-id="18ffd-126">The following query shows joining across multiple datasets for a weekly digest email like report.</span><span class="sxs-lookup"><span data-stu-id="18ffd-126">The following query shows joining across multiple datasets for a weekly digest email like report.</span></span> <span data-ttu-id="18ffd-127">Customize it as required and use it with any of the options listed above to automate a weekly report.</span><span class="sxs-lookup"><span data-stu-id="18ffd-127">Customize it as required and use it with any of the options listed above to automate a weekly report.</span></span>   

```AIQL
let period=7d;
requests
| where timestamp > ago(period)
| summarize Row = 1, TotalRequests = sum(itemCount), FailedRequests = sum(toint(success == 'False')),
    RequestsDuration = iff(isnan(avg(duration)), '------', tostring(toint(avg(duration) * 100) / 100.0))
| join (
dependencies
| where timestamp > ago(period)
| summarize Row = 1, TotalDependencies = sum(itemCount), FailedDependencies = sum(success == 'False'),
    DependenciesDuration = iff(isnan(avg(duration)), '------', tostring(toint(avg(duration) * 100) / 100.0))
) on Row | join (
pageViews
| where timestamp > ago(period)
| summarize Row = 1, TotalViews = sum(itemCount)
) on Row | join (
exceptions
| where timestamp > ago(period)
| summarize Row = 1, TotalExceptions = sum(itemCount)
) on Row | join (
availabilityResults
| where timestamp > ago(period)
| summarize Row = 1, OverallAvailability = iff(isnan(avg(toint(success))), '------', tostring(toint(avg(toint(success)) * 10000) / 100.0)),
    AvailabilityDuration = iff(isnan(avg(duration)), '------', tostring(toint(avg(duration) * 100) / 100.0))
) on Row
| project TotalRequests, FailedRequests, RequestsDuration, TotalDependencies, FailedDependencies, DependenciesDuration, TotalViews, TotalExceptions, OverallAvailability, AvailabilityDuration
```

## <a name="application-insights-scheduled-digest-report"></a><span data-ttu-id="18ffd-128">Application Insights scheduled digest report</span><span class="sxs-lookup"><span data-stu-id="18ffd-128">Application Insights scheduled digest report</span></span>

1. <span data-ttu-id="18ffd-129">From the Azure portal, select **Create a Resource** > **Compute** > **Function App**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-129">From the Azure portal, select **Create a Resource** > **Compute** > **Function App**.</span></span>

   ![Create an Azure Resource Function App screenshot](./media/automate-custom-reports/function-app-01.png)

2. <span data-ttu-id="18ffd-131">Enter appropriate info for your app and select _Create_.</span><span class="sxs-lookup"><span data-stu-id="18ffd-131">Enter appropriate info for your app and select _Create_.</span></span> <span data-ttu-id="18ffd-132">(Application Insights _On_ is required only if you want to monitor your new Function App with Application Insights)</span><span class="sxs-lookup"><span data-stu-id="18ffd-132">(Application Insights _On_ is required only if you want to monitor your new Function App with Application Insights)</span></span>

   ![Create an Azure Resource Function App Settings screenshot](./media/automate-custom-reports/function-app-02.png)

3. <span data-ttu-id="18ffd-134">Once your new Function App has completed deployment, select **Go to resource**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-134">Once your new Function App has completed deployment, select **Go to resource**.</span></span>

4. <span data-ttu-id="18ffd-135">Select **New function**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-135">Select **New function**.</span></span>

   ![Create a new Function screenshot](./media/automate-custom-reports/function-app-03.png)

5. <span data-ttu-id="18ffd-137">Select the **_Application Insights scheduled digest template_**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-137">Select the **_Application Insights scheduled digest template_**.</span></span>

   ![New Function Application Insights Template screenshot](./media/automate-custom-reports/function-app-04.png)

6. <span data-ttu-id="18ffd-139">Enter an appropriate recipient e-mail address for your report and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-139">Enter an appropriate recipient e-mail address for your report and select **Create**.</span></span>

   ![Function Settings screenshot](./media/automate-custom-reports/function-app-05.png)

7. <span data-ttu-id="18ffd-141">Select your **Function App** > **Platform features** > **Application settings**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-141">Select your **Function App** > **Platform features** > **Application settings**.</span></span>

    ![Azure Function Application settings screenshot](./media/automate-custom-reports/function-app-07.png)

8. <span data-ttu-id="18ffd-143">Create three new application settings with appropriate corresponding values ``AI_APP_ID``, ``AI_APP_KEY``, and ``SendGridAPI``.</span><span class="sxs-lookup"><span data-stu-id="18ffd-143">Create three new application settings with appropriate corresponding values ``AI_APP_ID``, ``AI_APP_KEY``, and ``SendGridAPI``.</span></span> <span data-ttu-id="18ffd-144">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-144">Select **Save**.</span></span>

     ![Function integration interface screenshot](./media/automate-custom-reports/function-app-08.png)
    
    <span data-ttu-id="18ffd-146">(The AI_ values can be found under API Access for the Application Insights Resource you want to report on.</span><span class="sxs-lookup"><span data-stu-id="18ffd-146">(The AI_ values can be found under API Access for the Application Insights Resource you want to report on.</span></span> <span data-ttu-id="18ffd-147">If you don't have an Application Insights API Key, there is the option to **Create API Key**.)</span><span class="sxs-lookup"><span data-stu-id="18ffd-147">If you don't have an Application Insights API Key, there is the option to **Create API Key**.)</span></span>
    
    * <span data-ttu-id="18ffd-148">AI_APP_ID = Application ID</span><span class="sxs-lookup"><span data-stu-id="18ffd-148">AI_APP_ID = Application ID</span></span>
    * <span data-ttu-id="18ffd-149">AI_APP_KEY = API Key</span><span class="sxs-lookup"><span data-stu-id="18ffd-149">AI_APP_KEY = API Key</span></span>
    * <span data-ttu-id="18ffd-150">SendGridAPI =SendGrid API Key</span><span class="sxs-lookup"><span data-stu-id="18ffd-150">SendGridAPI =SendGrid API Key</span></span>

    > [!NOTE]
    > <span data-ttu-id="18ffd-151">If you don't have a SendGrid account you can create one.</span><span class="sxs-lookup"><span data-stu-id="18ffd-151">If you don't have a SendGrid account you can create one.</span></span> <span data-ttu-id="18ffd-152">SendGrid's documentation for Azure Functions is [here](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-sendgrid).</span><span class="sxs-lookup"><span data-stu-id="18ffd-152">SendGrid's documentation for Azure Functions is [here](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-sendgrid).</span></span> <span data-ttu-id="18ffd-153">If just want a minimal explanation of how to setup SendGrid and generate an API key one is provided at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="18ffd-153">If just want a minimal explanation of how to setup SendGrid and generate an API key one is provided at the end of this article.</span></span> 

9. <span data-ttu-id="18ffd-154">Select **Integrate** and under Outputs click **SendGrid ($return)**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-154">Select **Integrate** and under Outputs click **SendGrid ($return)**.</span></span>

     ![Output screenshot](./media/automate-custom-reports/function-app-09.png)

10. <span data-ttu-id="18ffd-156">Under the **SendGridAPI Key App Setting**, select your newly created App Setting for **SendGridAPI**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-156">Under the **SendGridAPI Key App Setting**, select your newly created App Setting for **SendGridAPI**.</span></span>

     ![Run Function App screenshot](./media/automate-custom-reports/function-app-010.png)

11. <span data-ttu-id="18ffd-158">Run and test your Function App.</span><span class="sxs-lookup"><span data-stu-id="18ffd-158">Run and test your Function App.</span></span>

     ![Test Screenshot](./media/automate-custom-reports/function-app-11.png)

12. <span data-ttu-id="18ffd-160">Check your e-mail to confirm that the message was sent/received successfully.</span><span class="sxs-lookup"><span data-stu-id="18ffd-160">Check your e-mail to confirm that the message was sent/received successfully.</span></span>

     ![E-mail subject line screenshot](./media/automate-custom-reports/function-app-12.png)

## <a name="sendgrid-with-azure"></a><span data-ttu-id="18ffd-162">SendGrid with Azure</span><span class="sxs-lookup"><span data-stu-id="18ffd-162">SendGrid with Azure</span></span>

<span data-ttu-id="18ffd-163">These steps only apply if you don't already have a SendGrid account configured.</span><span class="sxs-lookup"><span data-stu-id="18ffd-163">These steps only apply if you don't already have a SendGrid account configured.</span></span>

1. <span data-ttu-id="18ffd-164">From the Azure portal select **Create a resource** search for **SendGrid Email Delivery** > Click **Create** > and fill out the SendGrid specific create instructions.</span><span class="sxs-lookup"><span data-stu-id="18ffd-164">From the Azure portal select **Create a resource** search for **SendGrid Email Delivery** > Click **Create** > and fill out the SendGrid specific create instructions.</span></span> 

     ![Create SendGrid Resource Screenshot](./media/automate-custom-reports/function-app-13.png)

2. <span data-ttu-id="18ffd-166">Once created under SendGrid Accounts select **Manage**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-166">Once created under SendGrid Accounts select **Manage**.</span></span>

     ![Settings API Key Screenshot](./media/automate-custom-reports/function-app-14.png)

3. <span data-ttu-id="18ffd-168">This will launch SendGrid's site.</span><span class="sxs-lookup"><span data-stu-id="18ffd-168">This will launch SendGrid's site.</span></span> <span data-ttu-id="18ffd-169">Select **Settings** > **API Keys**.</span><span class="sxs-lookup"><span data-stu-id="18ffd-169">Select **Settings** > **API Keys**.</span></span>

     ![Create and View API Key App Screenshot](./media/automate-custom-reports/function-app-15.png)

4. <span data-ttu-id="18ffd-171">Create an API Key > choose **Create & View** (Please review SendGrid's documentation on restricted access to determine what level of permissions is appropriate for your API Key.</span><span class="sxs-lookup"><span data-stu-id="18ffd-171">Create an API Key > choose **Create & View** (Please review SendGrid's documentation on restricted access to determine what level of permissions is appropriate for your API Key.</span></span> <span data-ttu-id="18ffd-172">Full Access is selected here for example purposes only.)</span><span class="sxs-lookup"><span data-stu-id="18ffd-172">Full Access is selected here for example purposes only.)</span></span>

   ![Full access screenshot](./media/automate-custom-reports/function-app-16.png)

5. <span data-ttu-id="18ffd-174">Copy the entire key, this value is what you need in your Function App settings as the value for SendGridAPI</span><span class="sxs-lookup"><span data-stu-id="18ffd-174">Copy the entire key, this value is what you need in your Function App settings as the value for SendGridAPI</span></span>

   ![Copy API key screenshot](./media/automate-custom-reports/function-app-17.png)

## <a name="next-steps"></a><span data-ttu-id="18ffd-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="18ffd-176">Next steps</span></span>

* <span data-ttu-id="18ffd-177">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="18ffd-177">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
* <span data-ttu-id="18ffd-178">Learn more about [programmatically querying Application Insights data](https://dev.applicationinsights.io/)</span><span class="sxs-lookup"><span data-stu-id="18ffd-178">Learn more about [programmatically querying Application Insights data](https://dev.applicationinsights.io/)</span></span>
* <span data-ttu-id="18ffd-179">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="18ffd-179">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>
* <span data-ttu-id="18ffd-180">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="18ffd-180">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>
