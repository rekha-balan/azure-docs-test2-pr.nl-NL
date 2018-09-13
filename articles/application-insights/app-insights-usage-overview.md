---
title: Usage analysis with Azure Application Insights | Microsoft docs
description: Understand your users and what they do with your app.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 10/10/2017
ms.author: mbullwin
ms.openlocfilehash: d5b580df531e2f0c61ac1d43cfd5ae353f314fce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871336"
---
# <a name="usage-analysis-with-application-insights"></a><span data-ttu-id="e7d1a-103">Usage analysis with Application Insights</span><span class="sxs-lookup"><span data-stu-id="e7d1a-103">Usage analysis with Application Insights</span></span>

<span data-ttu-id="e7d1a-104">Which features of your web or mobile app are most popular?</span><span class="sxs-lookup"><span data-stu-id="e7d1a-104">Which features of your web or mobile app are most popular?</span></span> <span data-ttu-id="e7d1a-105">Do your users achieve their goals with your app?</span><span class="sxs-lookup"><span data-stu-id="e7d1a-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="e7d1a-106">Do they drop out at particular points, and do they return later?</span><span class="sxs-lookup"><span data-stu-id="e7d1a-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="e7d1a-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your app.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your app.</span></span> <span data-ttu-id="e7d1a-108">Every time you update your app, you can assess how well it works for users.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="e7d1a-109">With this knowledge, you can make data driven decisions about your next development cycles.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="e7d1a-110">Send telemetry from your app</span><span class="sxs-lookup"><span data-stu-id="e7d1a-110">Send telemetry from your app</span></span>

<span data-ttu-id="e7d1a-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="e7d1a-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="e7d1a-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="e7d1a-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="e7d1a-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="e7d1a-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copy the script into the head of your master web page.](./media/app-insights-usage-overview/02-monitor-web-page.png)

3. <span data-ttu-id="e7d1a-117">**Mobile app code:** Use the App Center SDK to collect events from your app, then send copies of these events to Application Insights for analysis by [following this guide](app-insights-mobile-center-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="e7d1a-117">**Mobile app code:** Use the App Center SDK to collect events from your app, then send copies of these events to Application Insights for analysis by [following this guide](app-insights-mobile-center-quickstart.md).</span></span>

4. <span data-ttu-id="e7d1a-118">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-118">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="e7d1a-119">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-119">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="e7d1a-120">Include user and session ID in your telemetry</span><span class="sxs-lookup"><span data-stu-id="e7d1a-120">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="e7d1a-121">To track users over time, Application Insights requires a way to identify them.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-121">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="e7d1a-122">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-122">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="e7d1a-123">Start sending user and session IDs using [this process](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="e7d1a-123">Start sending user and session IDs using [this process](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="e7d1a-124">Explore usage demographics and statistics</span><span class="sxs-lookup"><span data-stu-id="e7d1a-124">Explore usage demographics and statistics</span></span>
<span data-ttu-id="e7d1a-125">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-125">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="e7d1a-126">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-126">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="e7d1a-127">You can also add your own filters.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-127">You can also add your own filters.</span></span>

![Users](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="e7d1a-129">Insights on the right point out interesting patterns in the set of data.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-129">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="e7d1a-130">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-130">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="e7d1a-131">For web apps, users are counted by using cookies.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-131">For web apps, users are counted by using cookies.</span></span> <span data-ttu-id="e7d1a-132">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-132">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.</span></span>
* <span data-ttu-id="e7d1a-133">The **Sessions** report counts the number of user sessions that access your site.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-133">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="e7d1a-134">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-134">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="e7d1a-135">More about the Users, Sessions, and Events tools</span><span class="sxs-lookup"><span data-stu-id="e7d1a-135">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="e7d1a-136">Page views</span><span class="sxs-lookup"><span data-stu-id="e7d1a-136">Page views</span></span>

<span data-ttu-id="e7d1a-137">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span><span class="sxs-lookup"><span data-stu-id="e7d1a-137">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![From the Overview blade, click the Page views chart](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="e7d1a-139">The example above is from a games web site.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-139">The example above is from a games web site.</span></span> <span data-ttu-id="e7d1a-140">From the charts, we can instantly see:</span><span class="sxs-lookup"><span data-stu-id="e7d1a-140">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="e7d1a-141">Usage hasn't improved in the past week.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-141">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="e7d1a-142">Maybe we should think about search engine optimization?</span><span class="sxs-lookup"><span data-stu-id="e7d1a-142">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="e7d1a-143">Tennis is the most popular game page.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-143">Tennis is the most popular game page.</span></span> <span data-ttu-id="e7d1a-144">Let's focus on further improvements to this page.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-144">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="e7d1a-145">On average, users visit the Tennis page about three times per week.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-145">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="e7d1a-146">(There are about three times more sessions than users.)</span><span class="sxs-lookup"><span data-stu-id="e7d1a-146">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="e7d1a-147">Most users visit the site during the U.S. working week, and in working hours.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-147">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="e7d1a-148">Perhaps we should provide a "quick hide" button on the web page.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-148">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="e7d1a-149">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-149">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="e7d1a-150">None of the recent deployments had a noticeable effect on usage.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-150">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="e7d1a-151">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span><span class="sxs-lookup"><span data-stu-id="e7d1a-151">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="e7d1a-152">Open the **Events** tool in the Application Insights resource menu.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-152">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="e7d1a-153">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-153">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="e7d1a-154">In the "Who used" dropdown, select "Any Page View".</span><span class="sxs-lookup"><span data-stu-id="e7d1a-154">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="e7d1a-155">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-155">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="e7d1a-156">Retention - how many users come back?</span><span class="sxs-lookup"><span data-stu-id="e7d1a-156">Retention - how many users come back?</span></span>

<span data-ttu-id="e7d1a-157">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-157">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="e7d1a-158">Understand what specific features cause users to come back more than others</span><span class="sxs-lookup"><span data-stu-id="e7d1a-158">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="e7d1a-159">Form hypotheses based on real user data</span><span class="sxs-lookup"><span data-stu-id="e7d1a-159">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="e7d1a-160">Determine whether retention is a problem in your product</span><span class="sxs-lookup"><span data-stu-id="e7d1a-160">Determine whether retention is a problem in your product</span></span> 

![Retention](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="e7d1a-162">The retention controls on top allow you to define specific events and time range to calculate retention.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-162">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="e7d1a-163">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-163">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="e7d1a-164">The graph on the bottom represents individual retention in a given time period.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-164">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="e7d1a-165">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-165">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="e7d1a-166">More about the Retention tool</span><span class="sxs-lookup"><span data-stu-id="e7d1a-166">More about the Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="e7d1a-167">Custom business events</span><span class="sxs-lookup"><span data-stu-id="e7d1a-167">Custom business events</span></span>

<span data-ttu-id="e7d1a-168">To get a clear understanding of what users do with your app, it's useful to insert lines of code to log custom events.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-168">To get a clear understanding of what users do with your app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="e7d1a-169">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-169">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="e7d1a-170">Although in some cases, page views can represent useful events, it isn't true in general.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-170">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="e7d1a-171">A user can open a product page without buying the product.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-171">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="e7d1a-172">With specific business events, you can chart your users' progress through your site.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-172">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="e7d1a-173">You can find out their preferences for different options, and where they drop out or have difficulties.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-173">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="e7d1a-174">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-174">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="e7d1a-175">Events can be logged from the client side of the app:</span><span class="sxs-lookup"><span data-stu-id="e7d1a-175">Events can be logged from the client side of the app:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="e7d1a-176">Or from the server side:</span><span class="sxs-lookup"><span data-stu-id="e7d1a-176">Or from the server side:</span></span>

```csharp
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="e7d1a-177">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-177">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="e7d1a-178">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-178">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="e7d1a-179">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="e7d1a-179">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="e7d1a-180">Slice and dice events</span><span class="sxs-lookup"><span data-stu-id="e7d1a-180">Slice and dice events</span></span>

<span data-ttu-id="e7d1a-181">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-181">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="e7d1a-182">![Users](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="e7d1a-182">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="e7d1a-183">Design the telemetry with the app</span><span class="sxs-lookup"><span data-stu-id="e7d1a-183">Design the telemetry with the app</span></span>

<span data-ttu-id="e7d1a-184">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-184">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="e7d1a-185">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-185">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="e7d1a-186">A | B Testing</span><span class="sxs-lookup"><span data-stu-id="e7d1a-186">A | B Testing</span></span>
<span data-ttu-id="e7d1a-187">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-187">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="e7d1a-188">Measure the success of each, and then move to a unified version.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-188">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="e7d1a-189">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-189">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="e7d1a-190">You can do that by defining properties in the active TelemetryContext.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-190">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="e7d1a-191">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-191">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="e7d1a-192">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-192">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="e7d1a-193">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="e7d1a-193">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```csharp


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="e7d1a-194">In the web app initializer such as Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="e7d1a-194">In the web app initializer such as Global.asax.cs:</span></span>

```csharp

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="e7d1a-195">All new TelemetryClients automatically add the property value you specify.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-195">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="e7d1a-196">Individual telemetry events can override the default values.</span><span class="sxs-lookup"><span data-stu-id="e7d1a-196">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7d1a-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="e7d1a-197">Next steps</span></span>
   - [<span data-ttu-id="e7d1a-198">Users, Sessions, Events</span><span class="sxs-lookup"><span data-stu-id="e7d1a-198">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="e7d1a-199">Funnels</span><span class="sxs-lookup"><span data-stu-id="e7d1a-199">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="e7d1a-200">Retention</span><span class="sxs-lookup"><span data-stu-id="e7d1a-200">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="e7d1a-201">User Flows</span><span class="sxs-lookup"><span data-stu-id="e7d1a-201">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="e7d1a-202">Workbooks</span><span class="sxs-lookup"><span data-stu-id="e7d1a-202">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="e7d1a-203">Add user context</span><span class="sxs-lookup"><span data-stu-id="e7d1a-203">Add user context</span></span>](app-insights-usage-send-user-context.md)
