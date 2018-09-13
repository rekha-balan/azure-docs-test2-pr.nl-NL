---
title: Quickstart with Azure Application Insights | Microsoft Docs
description: Provides instructions to quickly setup a mobile app for monitoring with Application Insights and App Center
services: application-insights
keywords: ''
author: mrbullwinkle
ms.author: mbullwin
ms.date: 07/11/2018
ms.service: application-insights
ms.reviewer: daviste
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
ms.openlocfilehash: e69cf8753fb0cc9326e047ec97cbe08ee6f26610
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865730"
---
# <a name="start-analyzing-your-mobile-app-with-app-center-and-application-insights"></a><span data-ttu-id="ae738-103">Start analyzing your mobile app with App Center and Application Insights</span><span class="sxs-lookup"><span data-stu-id="ae738-103">Start analyzing your mobile app with App Center and Application Insights</span></span>

<span data-ttu-id="ae738-104">This quickstart guides you through connecting your app's App Center instance to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae738-104">This quickstart guides you through connecting your app's App Center instance to Application Insights.</span></span> <span data-ttu-id="ae738-105">With Application Insights, you can query, segment, filter, and analyze your telemetry with more powerful tools than are available from the [Analytics](https://docs.microsoft.com/mobile-center/analytics/) service of App Center.</span><span class="sxs-lookup"><span data-stu-id="ae738-105">With Application Insights, you can query, segment, filter, and analyze your telemetry with more powerful tools than are available from the [Analytics](https://docs.microsoft.com/mobile-center/analytics/) service of App Center.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae738-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae738-106">Prerequisites</span></span>

<span data-ttu-id="ae738-107">To complete this quickstart, you need:</span><span class="sxs-lookup"><span data-stu-id="ae738-107">To complete this quickstart, you need:</span></span>

- <span data-ttu-id="ae738-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ae738-108">An Azure subscription.</span></span>
- <span data-ttu-id="ae738-109">An iOS, Android, Xamarin, Universal Windows, or React Native app.</span><span class="sxs-lookup"><span data-stu-id="ae738-109">An iOS, Android, Xamarin, Universal Windows, or React Native app.</span></span>
 
<span data-ttu-id="ae738-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="ae738-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="onboard-to-app-center"></a><span data-ttu-id="ae738-111">Onboard to App Center</span><span class="sxs-lookup"><span data-stu-id="ae738-111">Onboard to App Center</span></span>

<span data-ttu-id="ae738-112">Before you can use Application Insights with your mobile app, you need to onboard your app to [App Center](https://docs.microsoft.com/mobile-center/).</span><span class="sxs-lookup"><span data-stu-id="ae738-112">Before you can use Application Insights with your mobile app, you need to onboard your app to [App Center](https://docs.microsoft.com/mobile-center/).</span></span> <span data-ttu-id="ae738-113">Application Insights does not receive telemetry from your mobile app directly.</span><span class="sxs-lookup"><span data-stu-id="ae738-113">Application Insights does not receive telemetry from your mobile app directly.</span></span> <span data-ttu-id="ae738-114">Instead, your app sends custom event telemetry to App Center.</span><span class="sxs-lookup"><span data-stu-id="ae738-114">Instead, your app sends custom event telemetry to App Center.</span></span> <span data-ttu-id="ae738-115">Then, App Center continuously exports copies of these custom events into Application Insights as the events are received.</span><span class="sxs-lookup"><span data-stu-id="ae738-115">Then, App Center continuously exports copies of these custom events into Application Insights as the events are received.</span></span>

<span data-ttu-id="ae738-116">To onboard your app, follow the App Center quickstart for each platform your app supports.</span><span class="sxs-lookup"><span data-stu-id="ae738-116">To onboard your app, follow the App Center quickstart for each platform your app supports.</span></span> <span data-ttu-id="ae738-117">Create separate App Center instances for each platform:</span><span class="sxs-lookup"><span data-stu-id="ae738-117">Create separate App Center instances for each platform:</span></span>

* <span data-ttu-id="ae738-118">[iOS](https://docs.microsoft.com/mobile-center/sdk/getting-started/ios).</span><span class="sxs-lookup"><span data-stu-id="ae738-118">[iOS](https://docs.microsoft.com/mobile-center/sdk/getting-started/ios).</span></span>
* <span data-ttu-id="ae738-119">[Android](https://docs.microsoft.com/mobile-center/sdk/getting-started/android).</span><span class="sxs-lookup"><span data-stu-id="ae738-119">[Android](https://docs.microsoft.com/mobile-center/sdk/getting-started/android).</span></span>
* <span data-ttu-id="ae738-120">[Xamarin](https://docs.microsoft.com/mobile-center/sdk/getting-started/xamarin).</span><span class="sxs-lookup"><span data-stu-id="ae738-120">[Xamarin](https://docs.microsoft.com/mobile-center/sdk/getting-started/xamarin).</span></span>
* <span data-ttu-id="ae738-121">[Universal Windows](https://docs.microsoft.com/mobile-center/sdk/getting-started/uwp).</span><span class="sxs-lookup"><span data-stu-id="ae738-121">[Universal Windows](https://docs.microsoft.com/mobile-center/sdk/getting-started/uwp).</span></span>
* <span data-ttu-id="ae738-122">[React Native](https://docs.microsoft.com/mobile-center/sdk/getting-started/react-native).</span><span class="sxs-lookup"><span data-stu-id="ae738-122">[React Native](https://docs.microsoft.com/mobile-center/sdk/getting-started/react-native).</span></span>

## <a name="track-events-in-your-app"></a><span data-ttu-id="ae738-123">Track events in your app</span><span class="sxs-lookup"><span data-stu-id="ae738-123">Track events in your app</span></span>

<span data-ttu-id="ae738-124">After your app is onboarded to App Center, it needs to be modified to send custom event telemetry using the App Center SDK.</span><span class="sxs-lookup"><span data-stu-id="ae738-124">After your app is onboarded to App Center, it needs to be modified to send custom event telemetry using the App Center SDK.</span></span> <span data-ttu-id="ae738-125">Custom events are the only type of App Center telemetry that is exported to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae738-125">Custom events are the only type of App Center telemetry that is exported to Application Insights.</span></span>

<span data-ttu-id="ae738-126">To send custom events from iOS apps, use the `trackEvent` or `trackEvent:withProperties` methods in the App Center SDK.</span><span class="sxs-lookup"><span data-stu-id="ae738-126">To send custom events from iOS apps, use the `trackEvent` or `trackEvent:withProperties` methods in the App Center SDK.</span></span> [<span data-ttu-id="ae738-127">Learn more about tracking events from iOS apps.</span><span class="sxs-lookup"><span data-stu-id="ae738-127">Learn more about tracking events from iOS apps.</span></span>](https://docs.microsoft.com/mobile-center/sdk/analytics/ios)

```Swift
MSAnalytics.trackEvent("Video clicked")
```

<span data-ttu-id="ae738-128">To send custom events from Android apps, use the `trackEvent` method in the App Center SDK.</span><span class="sxs-lookup"><span data-stu-id="ae738-128">To send custom events from Android apps, use the `trackEvent` method in the App Center SDK.</span></span> [<span data-ttu-id="ae738-129">Learn more about tracking events from Android apps.</span><span class="sxs-lookup"><span data-stu-id="ae738-129">Learn more about tracking events from Android apps.</span></span>](https://docs.microsoft.com/mobile-center/sdk/analytics/android)

```Java
Analytics.trackEvent("Video clicked")
```

<span data-ttu-id="ae738-130">To send custom events from other app platforms, use the `trackEvent` methods in their App Center SDKs.</span><span class="sxs-lookup"><span data-stu-id="ae738-130">To send custom events from other app platforms, use the `trackEvent` methods in their App Center SDKs.</span></span>

<span data-ttu-id="ae738-131">To make sure your custom events are being received, go to the **Events** tab under the **Analytics** section in App Center.</span><span class="sxs-lookup"><span data-stu-id="ae738-131">To make sure your custom events are being received, go to the **Events** tab under the **Analytics** section in App Center.</span></span> <span data-ttu-id="ae738-132">It can take a couple minutes for events to show up from when they're sent from your app.</span><span class="sxs-lookup"><span data-stu-id="ae738-132">It can take a couple minutes for events to show up from when they're sent from your app.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="ae738-133">Create an Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="ae738-133">Create an Application Insights resource</span></span>

<span data-ttu-id="ae738-134">Once your app is sending custom events and these events are being received by App Center, you need to create an App Center-type Application Insights resource in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="ae738-134">Once your app is sending custom events and these events are being received by App Center, you need to create an App Center-type Application Insights resource in the Azure portal:</span></span>

1. <span data-ttu-id="ae738-135">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ae738-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ae738-136">Select **Create a resource** > **Management Tools** > **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="ae738-136">Select **Create a resource** > **Management Tools** > **Application Insights**.</span></span>

    ![Adding Application Insights resource](./media/app-insights-mobile-center-quickstart/add-b.png)

    <span data-ttu-id="ae738-138">A configuration box will appear.</span><span class="sxs-lookup"><span data-stu-id="ae738-138">A configuration box will appear.</span></span> <span data-ttu-id="ae738-139">Use the table below to fill out the input fields.</span><span class="sxs-lookup"><span data-stu-id="ae738-139">Use the table below to fill out the input fields.</span></span>

    | <span data-ttu-id="ae738-140">Settings</span><span class="sxs-lookup"><span data-stu-id="ae738-140">Settings</span></span>        |  <span data-ttu-id="ae738-141">Value</span><span class="sxs-lookup"><span data-stu-id="ae738-141">Value</span></span>           | <span data-ttu-id="ae738-142">Description</span><span class="sxs-lookup"><span data-stu-id="ae738-142">Description</span></span>  |
   | ------------- |:-------------|:-----|
   | <span data-ttu-id="ae738-143">**Name**</span><span class="sxs-lookup"><span data-stu-id="ae738-143">**Name**</span></span>      | <span data-ttu-id="ae738-144">Some globally unique value, like "myApp-iOS"</span><span class="sxs-lookup"><span data-stu-id="ae738-144">Some globally unique value, like "myApp-iOS"</span></span> | <span data-ttu-id="ae738-145">Name that identifies the app you are monitoring</span><span class="sxs-lookup"><span data-stu-id="ae738-145">Name that identifies the app you are monitoring</span></span> |
   | <span data-ttu-id="ae738-146">**Application Type**</span><span class="sxs-lookup"><span data-stu-id="ae738-146">**Application Type**</span></span> | <span data-ttu-id="ae738-147">App Center application</span><span class="sxs-lookup"><span data-stu-id="ae738-147">App Center application</span></span> | <span data-ttu-id="ae738-148">Type of app you are monitoring</span><span class="sxs-lookup"><span data-stu-id="ae738-148">Type of app you are monitoring</span></span> |
   | <span data-ttu-id="ae738-149">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="ae738-149">**Resource Group**</span></span>     | <span data-ttu-id="ae738-150">A new resource group, or an existing one from the menu</span><span class="sxs-lookup"><span data-stu-id="ae738-150">A new resource group, or an existing one from the menu</span></span> | <span data-ttu-id="ae738-151">The resource group in which to create the new Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="ae738-151">The resource group in which to create the new Application Insights resource</span></span> |
   | <span data-ttu-id="ae738-152">**Location**</span><span class="sxs-lookup"><span data-stu-id="ae738-152">**Location**</span></span> | <span data-ttu-id="ae738-153">A location from the menu</span><span class="sxs-lookup"><span data-stu-id="ae738-153">A location from the menu</span></span> | <span data-ttu-id="ae738-154">Choose a location near you, or near where your app is hosted</span><span class="sxs-lookup"><span data-stu-id="ae738-154">Choose a location near you, or near where your app is hosted</span></span> |

3. <span data-ttu-id="ae738-155">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ae738-155">Click **Create**.</span></span>

<span data-ttu-id="ae738-156">If your app supports multiple platforms (iOS, Android, etc.), it's best to create separate Application Insights resources, one for each platform.</span><span class="sxs-lookup"><span data-stu-id="ae738-156">If your app supports multiple platforms (iOS, Android, etc.), it's best to create separate Application Insights resources, one for each platform.</span></span>

## <a name="export-to-application-insights"></a><span data-ttu-id="ae738-157">Export to Application Insights</span><span class="sxs-lookup"><span data-stu-id="ae738-157">Export to Application Insights</span></span>

<span data-ttu-id="ae738-158">In your new Application Insights resource on the **Overview** page in the **Essentials** section at the top, copy the instrumentation key for this resource.</span><span class="sxs-lookup"><span data-stu-id="ae738-158">In your new Application Insights resource on the **Overview** page in the **Essentials** section at the top, copy the instrumentation key for this resource.</span></span>

<span data-ttu-id="ae738-159">In the App Center instance for your app:</span><span class="sxs-lookup"><span data-stu-id="ae738-159">In the App Center instance for your app:</span></span>

1. <span data-ttu-id="ae738-160">On the **Settings** page, click **Export**.</span><span class="sxs-lookup"><span data-stu-id="ae738-160">On the **Settings** page, click **Export**.</span></span>
2. <span data-ttu-id="ae738-161">Choose **New Export**, pick **Application Insights**, then click **Customize**.</span><span class="sxs-lookup"><span data-stu-id="ae738-161">Choose **New Export**, pick **Application Insights**, then click **Customize**.</span></span>
3. <span data-ttu-id="ae738-162">Paste your Application Insights instrumentation key into the box.</span><span class="sxs-lookup"><span data-stu-id="ae738-162">Paste your Application Insights instrumentation key into the box.</span></span>
4. <span data-ttu-id="ae738-163">Consent to increasing the usage of the Azure subscription containing your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="ae738-163">Consent to increasing the usage of the Azure subscription containing your Application Insights resource.</span></span> <span data-ttu-id="ae738-164">Each Application Insights resource is free for the first 1 GB of data received per month.</span><span class="sxs-lookup"><span data-stu-id="ae738-164">Each Application Insights resource is free for the first 1 GB of data received per month.</span></span> [<span data-ttu-id="ae738-165">Learn more about Application Insights pricing.</span><span class="sxs-lookup"><span data-stu-id="ae738-165">Learn more about Application Insights pricing.</span></span>](https://azure.microsoft.com/pricing/details/application-insights/)

<span data-ttu-id="ae738-166">Remember to repeat this process for each platform your app supports.</span><span class="sxs-lookup"><span data-stu-id="ae738-166">Remember to repeat this process for each platform your app supports.</span></span>

<span data-ttu-id="ae738-167">Once [export](https://docs.microsoft.com/mobile-center/analytics/export) is set up, each custom event received by App Center is copied into Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae738-167">Once [export](https://docs.microsoft.com/mobile-center/analytics/export) is set up, each custom event received by App Center is copied into Application Insights.</span></span> <span data-ttu-id="ae738-168">It can take several minutes for events to reach Application Insights, so if they don't show up immediately, wait a bit before diagnosing further.</span><span class="sxs-lookup"><span data-stu-id="ae738-168">It can take several minutes for events to reach Application Insights, so if they don't show up immediately, wait a bit before diagnosing further.</span></span>

<span data-ttu-id="ae738-169">To give you more data when you first connect, the most recent 48 hours of custom events in App Center are automatically exported to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae738-169">To give you more data when you first connect, the most recent 48 hours of custom events in App Center are automatically exported to Application Insights.</span></span>

## <a name="start-monitoring-your-app"></a><span data-ttu-id="ae738-170">Start monitoring your app</span><span class="sxs-lookup"><span data-stu-id="ae738-170">Start monitoring your app</span></span>

<span data-ttu-id="ae738-171">Application Insights can query, segment, filter, and analyze the custom event telemetry from your apps, beyond the analytics tools App Center provides.</span><span class="sxs-lookup"><span data-stu-id="ae738-171">Application Insights can query, segment, filter, and analyze the custom event telemetry from your apps, beyond the analytics tools App Center provides.</span></span>

1. <span data-ttu-id="ae738-172">**Query your custom event telemetry.**</span><span class="sxs-lookup"><span data-stu-id="ae738-172">**Query your custom event telemetry.**</span></span> <span data-ttu-id="ae738-173">From the Application Insights **Overview** page, choose **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ae738-173">From the Application Insights **Overview** page, choose **Analytics**.</span></span> 

   ![Analytics button in Application Insights](./media/app-insights-mobile-center-quickstart/analytics.png)

   <span data-ttu-id="ae738-175">The Application Insights Analytics portal associated with your Application Insights resource will open.</span><span class="sxs-lookup"><span data-stu-id="ae738-175">The Application Insights Analytics portal associated with your Application Insights resource will open.</span></span> <span data-ttu-id="ae738-176">The Analytics portal lets you directly query your data using the Log Analytics query language, so you can ask arbitrarily complex questions about your app and its users.</span><span class="sxs-lookup"><span data-stu-id="ae738-176">The Analytics portal lets you directly query your data using the Log Analytics query language, so you can ask arbitrarily complex questions about your app and its users.</span></span>
   
   <span data-ttu-id="ae738-177">Open a new tab in the Analytics portal, then paste in the following query.</span><span class="sxs-lookup"><span data-stu-id="ae738-177">Open a new tab in the Analytics portal, then paste in the following query.</span></span> <span data-ttu-id="ae738-178">It returns a count of how many distinct users have sent each custom event from your app in the last 24 hours, sorted by these distinct counts.</span><span class="sxs-lookup"><span data-stu-id="ae738-178">It returns a count of how many distinct users have sent each custom event from your app in the last 24 hours, sorted by these distinct counts.</span></span>

   ```AIQL
   customEvents
   | where timestamp >= ago(24h)
   | summarize dcount(user_Id) by name 
   | order by dcount_user_Id desc 
   ```

   ![Analytics portal](./media/app-insights-mobile-center-quickstart/analytics-portal.png)

   1. <span data-ttu-id="ae738-180">Select the query by clicking anywhere on the query in the text editor.</span><span class="sxs-lookup"><span data-stu-id="ae738-180">Select the query by clicking anywhere on the query in the text editor.</span></span>
   2. <span data-ttu-id="ae738-181">Then click **Go** to run the query.</span><span class="sxs-lookup"><span data-stu-id="ae738-181">Then click **Go** to run the query.</span></span> 

   <span data-ttu-id="ae738-182">Learn more about [Application Insights Analytics](app-insights-analytics.md) and the [Log Analytics query language](https://docs.loganalytics.io/docs/Language-Reference).</span><span class="sxs-lookup"><span data-stu-id="ae738-182">Learn more about [Application Insights Analytics](app-insights-analytics.md) and the [Log Analytics query language](https://docs.loganalytics.io/docs/Language-Reference).</span></span>


2. <span data-ttu-id="ae738-183">**Segment and filter your custom event telemetry.**</span><span class="sxs-lookup"><span data-stu-id="ae738-183">**Segment and filter your custom event telemetry.**</span></span> <span data-ttu-id="ae738-184">From the Application Insights **Overview** page, choose **Users** in the table of contents.</span><span class="sxs-lookup"><span data-stu-id="ae738-184">From the Application Insights **Overview** page, choose **Users** in the table of contents.</span></span>

   ![Users tool icon](./media/app-insights-mobile-center-quickstart/users-icon.png)

   <span data-ttu-id="ae738-186">The Users tool shows how many users of your app clicked certain buttons, visited certain screens, or performed any other action that you are tracking as an event with the App Center SDK.</span><span class="sxs-lookup"><span data-stu-id="ae738-186">The Users tool shows how many users of your app clicked certain buttons, visited certain screens, or performed any other action that you are tracking as an event with the App Center SDK.</span></span> <span data-ttu-id="ae738-187">If you've been looking for a way to segment and filter your App Center events, the Users tool is a great choice.</span><span class="sxs-lookup"><span data-stu-id="ae738-187">If you've been looking for a way to segment and filter your App Center events, the Users tool is a great choice.</span></span>

   ![Users tool](./media/app-insights-mobile-center-quickstart/users.png) 

   <span data-ttu-id="ae738-189">For example, segment your usage by geography by choosing **Country or region** in the **Split by** dropdown menu.</span><span class="sxs-lookup"><span data-stu-id="ae738-189">For example, segment your usage by geography by choosing **Country or region** in the **Split by** dropdown menu.</span></span>

3. <span data-ttu-id="ae738-190">**Analyze conversion, retention, and navigation patterns in your app.**</span><span class="sxs-lookup"><span data-stu-id="ae738-190">**Analyze conversion, retention, and navigation patterns in your app.**</span></span> <span data-ttu-id="ae738-191">From the Application Insights **Overview** page, choose **User Flows** in the table of contents.</span><span class="sxs-lookup"><span data-stu-id="ae738-191">From the Application Insights **Overview** page, choose **User Flows** in the table of contents.</span></span>

   ![User Flows tool](./media/app-insights-mobile-center-quickstart/user-flows.png)

   <span data-ttu-id="ae738-193">The User Flows tool visualizes which events users send after some starting event.</span><span class="sxs-lookup"><span data-stu-id="ae738-193">The User Flows tool visualizes which events users send after some starting event.</span></span> <span data-ttu-id="ae738-194">It's useful for getting an overall picture of how users navigate through your app.</span><span class="sxs-lookup"><span data-stu-id="ae738-194">It's useful for getting an overall picture of how users navigate through your app.</span></span> <span data-ttu-id="ae738-195">It can also reveal places where many users are churning from your app, or repeating the same actions over and over.</span><span class="sxs-lookup"><span data-stu-id="ae738-195">It can also reveal places where many users are churning from your app, or repeating the same actions over and over.</span></span>

   <span data-ttu-id="ae738-196">In addition to User Flows, Application Insights has several other user behavior analytics tools to answer specific questions:</span><span class="sxs-lookup"><span data-stu-id="ae738-196">In addition to User Flows, Application Insights has several other user behavior analytics tools to answer specific questions:</span></span>

   * <span data-ttu-id="ae738-197">**Funnels** for analyzing and monitoring conversion rates.</span><span class="sxs-lookup"><span data-stu-id="ae738-197">**Funnels** for analyzing and monitoring conversion rates.</span></span>
   * <span data-ttu-id="ae738-198">**Retention** for analyzing how well your app retains users over time.</span><span class="sxs-lookup"><span data-stu-id="ae738-198">**Retention** for analyzing how well your app retains users over time.</span></span>
   * <span data-ttu-id="ae738-199">**Workbooks** for combining visualizations and text into a shareable report.</span><span class="sxs-lookup"><span data-stu-id="ae738-199">**Workbooks** for combining visualizations and text into a shareable report.</span></span>
   * <span data-ttu-id="ae738-200">**Cohorts** for naming and saving specific groups of users or events so they can be easily referenced from other analytics tools.</span><span class="sxs-lookup"><span data-stu-id="ae738-200">**Cohorts** for naming and saving specific groups of users or events so they can be easily referenced from other analytics tools.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="ae738-201">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ae738-201">Clean up resources</span></span>

<span data-ttu-id="ae738-202">If you do not want to continue using Application Insights with App Center, turn off export in App Center and delete the Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="ae738-202">If you do not want to continue using Application Insights with App Center, turn off export in App Center and delete the Application Insights resource.</span></span> <span data-ttu-id="ae738-203">This will prevent you from being charged further by Application Insights for this resource.</span><span class="sxs-lookup"><span data-stu-id="ae738-203">This will prevent you from being charged further by Application Insights for this resource.</span></span>

<span data-ttu-id="ae738-204">To turn off export in App Center:</span><span class="sxs-lookup"><span data-stu-id="ae738-204">To turn off export in App Center:</span></span>

1. <span data-ttu-id="ae738-205">In App Center, go to **Settings** and choose **Export**.</span><span class="sxs-lookup"><span data-stu-id="ae738-205">In App Center, go to **Settings** and choose **Export**.</span></span>
2. <span data-ttu-id="ae738-206">Click the Application Insights export you want to delete, then click **Delete export** at the bottom and confirm.</span><span class="sxs-lookup"><span data-stu-id="ae738-206">Click the Application Insights export you want to delete, then click **Delete export** at the bottom and confirm.</span></span>

<span data-ttu-id="ae738-207">To delete the Application Insights resource:</span><span class="sxs-lookup"><span data-stu-id="ae738-207">To delete the Application Insights resource:</span></span>

1. <span data-ttu-id="ae738-208">In the left-hand menu of the Azure portal, click **Resource groups** and then choose the resource group in which your Application Insights resource was created.</span><span class="sxs-lookup"><span data-stu-id="ae738-208">In the left-hand menu of the Azure portal, click **Resource groups** and then choose the resource group in which your Application Insights resource was created.</span></span>
2. <span data-ttu-id="ae738-209">Open the Application Insights resource you want to delete.</span><span class="sxs-lookup"><span data-stu-id="ae738-209">Open the Application Insights resource you want to delete.</span></span> <span data-ttu-id="ae738-210">Then click **Delete** in the top menu of the resource and confirm.</span><span class="sxs-lookup"><span data-stu-id="ae738-210">Then click **Delete** in the top menu of the resource and confirm.</span></span> <span data-ttu-id="ae738-211">This will permanently delete the copy of the data that was exported to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ae738-211">This will permanently delete the copy of the data that was exported to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae738-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae738-212">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae738-213">Understand how customers are using your app</span><span class="sxs-lookup"><span data-stu-id="ae738-213">Understand how customers are using your app</span></span>](app-insights-usage-overview.md)
