---
title: Set Alerts in Azure Application Insights | Microsoft Docs
description: Get notified about slow response times, exceptions, and other performance or usage changes in your web app.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 678d47b35b752fbdf6a1275e06df717a7f00a16e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553315"
---
# <a name="set-alerts-in-application-insights"></a><span data-ttu-id="3a1d5-103">Set Alerts in Application Insights</span><span class="sxs-lookup"><span data-stu-id="3a1d5-103">Set Alerts in Application Insights</span></span>
<span data-ttu-id="3a1d5-104">[Azure Application Insights][start] can alert you to changes in performance or usage metrics in your web app.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-104">[Azure Application Insights][start] can alert you to changes in performance or usage metrics in your web app.</span></span> 

<span data-ttu-id="3a1d5-105">Application Insights monitors your live app on a [wide variety of platforms][platforms] to help you diagnose performance issues and understand usage patterns.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-105">Application Insights monitors your live app on a [wide variety of platforms][platforms] to help you diagnose performance issues and understand usage patterns.</span></span>

<span data-ttu-id="3a1d5-106">There are three kinds of alerts:</span><span class="sxs-lookup"><span data-stu-id="3a1d5-106">There are three kinds of alerts:</span></span>

* <span data-ttu-id="3a1d5-107">**Metric alerts** tell you when a metric crosses a threshold value for some period - such as response times, exception counts, CPU usage, or page views.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-107">**Metric alerts** tell you when a metric crosses a threshold value for some period - such as response times, exception counts, CPU usage, or page views.</span></span> 
* <span data-ttu-id="3a1d5-108">[**Web tests**][availability] tell you when your site is unavailable on the internet, or responding slowly.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-108">[**Web tests**][availability] tell you when your site is unavailable on the internet, or responding slowly.</span></span> <span data-ttu-id="3a1d5-109">[Learn more][availability].</span><span class="sxs-lookup"><span data-stu-id="3a1d5-109">[Learn more][availability].</span></span>
* <span data-ttu-id="3a1d5-110">[**Proactive diagnostics**](app-insights-proactive-diagnostics.md) are configured automatically to notify you about unusual performance patterns.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-110">[**Proactive diagnostics**](app-insights-proactive-diagnostics.md) are configured automatically to notify you about unusual performance patterns.</span></span>

<span data-ttu-id="3a1d5-111">We focus on metric alerts in this article.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-111">We focus on metric alerts in this article.</span></span>

## <a name="set-a-metric-alert"></a><span data-ttu-id="3a1d5-112">Set a Metric alert</span><span class="sxs-lookup"><span data-stu-id="3a1d5-112">Set a Metric alert</span></span>
<span data-ttu-id="3a1d5-113">Open the Alert rules blade, and then use the add button.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-113">Open the Alert rules blade, and then use the add button.</span></span> 

![In the Alert rules blade, choose Add Alert.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-alerts/01-set-metric.png)

* <span data-ttu-id="3a1d5-116">Set the resource before the other properties.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-116">Set the resource before the other properties.</span></span> <span data-ttu-id="3a1d5-117">**Choose the "(components)" resource** if you want to set alerts on performance or usage metrics.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-117">**Choose the "(components)" resource** if you want to set alerts on performance or usage metrics.</span></span>
* <span data-ttu-id="3a1d5-118">The name that you give to the alert must be unique within the resource group (not just your application).</span><span class="sxs-lookup"><span data-stu-id="3a1d5-118">The name that you give to the alert must be unique within the resource group (not just your application).</span></span>
* <span data-ttu-id="3a1d5-119">Be careful to note the units in which you're asked to enter the threshold value.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-119">Be careful to note the units in which you're asked to enter the threshold value.</span></span>
* <span data-ttu-id="3a1d5-120">If you check the box "Email owners...", alerts will be sent by email to everyone who has access to this resource group.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-120">If you check the box "Email owners...", alerts will be sent by email to everyone who has access to this resource group.</span></span> <span data-ttu-id="3a1d5-121">To expand this set of people, add them to the [resource group or subscription](app-insights-resources-roles-access-control.md) (not the resource).</span><span class="sxs-lookup"><span data-stu-id="3a1d5-121">To expand this set of people, add them to the [resource group or subscription](app-insights-resources-roles-access-control.md) (not the resource).</span></span>
* <span data-ttu-id="3a1d5-122">If you specify "Additional emails", alerts will be sent to those individuals or groups (whether or not you checked the "email owners..." box).</span><span class="sxs-lookup"><span data-stu-id="3a1d5-122">If you specify "Additional emails", alerts will be sent to those individuals or groups (whether or not you checked the "email owners..." box).</span></span> 
* <span data-ttu-id="3a1d5-123">Set a [webhook address](../monitoring-and-diagnostics/insights-webhooks-alerts.md) if you have set up a web app that responds to alerts.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-123">Set a [webhook address](../monitoring-and-diagnostics/insights-webhooks-alerts.md) if you have set up a web app that responds to alerts.</span></span> <span data-ttu-id="3a1d5-124">It will be called both when the alert is Activated (that is, triggered) and when it is Resolved.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-124">It will be called both when the alert is Activated (that is, triggered) and when it is Resolved.</span></span> <span data-ttu-id="3a1d5-125">(But note that at present, query parameters are not passed through as webhook properties.)</span><span class="sxs-lookup"><span data-stu-id="3a1d5-125">(But note that at present, query parameters are not passed through as webhook properties.)</span></span>
* <span data-ttu-id="3a1d5-126">You can Disable or Enable the alert: see the buttons at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-126">You can Disable or Enable the alert: see the buttons at the top of the blade.</span></span>

<span data-ttu-id="3a1d5-127">*I don't see the Add Alert button.*</span><span class="sxs-lookup"><span data-stu-id="3a1d5-127">*I don't see the Add Alert button.*</span></span> 

* <span data-ttu-id="3a1d5-128">Are you using an organizational account?</span><span class="sxs-lookup"><span data-stu-id="3a1d5-128">Are you using an organizational account?</span></span> <span data-ttu-id="3a1d5-129">You can set alerts if you have owner or contributor access to this application resource.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-129">You can set alerts if you have owner or contributor access to this application resource.</span></span> <span data-ttu-id="3a1d5-130">Take a look at the Access Control blade.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-130">Take a look at the Access Control blade.</span></span> <span data-ttu-id="3a1d5-131">[Learn about access control][roles].</span><span class="sxs-lookup"><span data-stu-id="3a1d5-131">[Learn about access control][roles].</span></span>

> [!NOTE]
> <span data-ttu-id="3a1d5-132">In the alerts blade, you'll see that there's already an alert set up: [Proactive Diagnostics](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3a1d5-132">In the alerts blade, you'll see that there's already an alert set up: [Proactive Diagnostics](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="3a1d5-133">This is an automatic alert that monitors one particular metric, request failure rate.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-133">This is an automatic alert that monitors one particular metric, request failure rate.</span></span> <span data-ttu-id="3a1d5-134">Unless you decide to disable the proactive alert, you don't need to set your own alert on request failure rate.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-134">Unless you decide to disable the proactive alert, you don't need to set your own alert on request failure rate.</span></span> 
> 
> 

## <a name="see-your-alerts"></a><span data-ttu-id="3a1d5-135">See your alerts</span><span class="sxs-lookup"><span data-stu-id="3a1d5-135">See your alerts</span></span>
<span data-ttu-id="3a1d5-136">You get an email when an alert changes state between inactive and active.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-136">You get an email when an alert changes state between inactive and active.</span></span> 

<span data-ttu-id="3a1d5-137">The current state of each alert is shown in the Alert rules blade.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-137">The current state of each alert is shown in the Alert rules blade.</span></span>

<span data-ttu-id="3a1d5-138">There's a summary of recent activity in the alerts drop-down:</span><span class="sxs-lookup"><span data-stu-id="3a1d5-138">There's a summary of recent activity in the alerts drop-down:</span></span>

![Alerts drop-down](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-alerts/010-alert-drop.png)

<span data-ttu-id="3a1d5-140">The history of state changes is in the Activity Log:</span><span class="sxs-lookup"><span data-stu-id="3a1d5-140">The history of state changes is in the Activity Log:</span></span>

![On the Overview blade, click Settings, Audit logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a><span data-ttu-id="3a1d5-142">How alerts work</span><span class="sxs-lookup"><span data-stu-id="3a1d5-142">How alerts work</span></span>
* <span data-ttu-id="3a1d5-143">An alert has three states: "Never activated", "Activated", and "Resolved."</span><span class="sxs-lookup"><span data-stu-id="3a1d5-143">An alert has three states: "Never activated", "Activated", and "Resolved."</span></span> <span data-ttu-id="3a1d5-144">Activated means the condition you specified was true, when it was last evaluated.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-144">Activated means the condition you specified was true, when it was last evaluated.</span></span>
* <span data-ttu-id="3a1d5-145">A notification is generated when an alert changes state.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-145">A notification is generated when an alert changes state.</span></span> <span data-ttu-id="3a1d5-146">(If the alert condition was already true when you created the alert, you might not get a notification until the condition goes false.)</span><span class="sxs-lookup"><span data-stu-id="3a1d5-146">(If the alert condition was already true when you created the alert, you might not get a notification until the condition goes false.)</span></span>
* <span data-ttu-id="3a1d5-147">Each notification generates an email if you checked the emails box, or provided email addresses.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-147">Each notification generates an email if you checked the emails box, or provided email addresses.</span></span> <span data-ttu-id="3a1d5-148">You can also look at the Notifications drop-down list.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-148">You can also look at the Notifications drop-down list.</span></span>
* <span data-ttu-id="3a1d5-149">An alert is evaluated each time a metric arrives, but not otherwise.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-149">An alert is evaluated each time a metric arrives, but not otherwise.</span></span>
* <span data-ttu-id="3a1d5-150">The evaluation aggregates the metric over the preceding period, and then compares it to the threshold to determine the new state.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-150">The evaluation aggregates the metric over the preceding period, and then compares it to the threshold to determine the new state.</span></span>
* <span data-ttu-id="3a1d5-151">The period that you choose specifies the interval over which metrics are aggregated.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-151">The period that you choose specifies the interval over which metrics are aggregated.</span></span> <span data-ttu-id="3a1d5-152">It doesn't affect how often the alert is evaluated: that depends on the frequency of arrival of metrics.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-152">It doesn't affect how often the alert is evaluated: that depends on the frequency of arrival of metrics.</span></span>
* <span data-ttu-id="3a1d5-153">If no data arrives for a particular metric for some time, the gap has different effects on alert evaluation and on the charts in metric explorer.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-153">If no data arrives for a particular metric for some time, the gap has different effects on alert evaluation and on the charts in metric explorer.</span></span> <span data-ttu-id="3a1d5-154">In metric explorer, if no data is seen for longer than the chart's sampling interval, the chart shows a value of 0.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-154">In metric explorer, if no data is seen for longer than the chart's sampling interval, the chart shows a value of 0.</span></span> <span data-ttu-id="3a1d5-155">But an alert based on the same metric is not be re-evaluated, and the alert's state remains unchanged.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-155">But an alert based on the same metric is not be re-evaluated, and the alert's state remains unchanged.</span></span> 
  
    <span data-ttu-id="3a1d5-156">When data eventually arrives, the chart jumps back to a non-zero value.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-156">When data eventually arrives, the chart jumps back to a non-zero value.</span></span> <span data-ttu-id="3a1d5-157">The alert evaluates based on the data available for the period you specified.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-157">The alert evaluates based on the data available for the period you specified.</span></span> <span data-ttu-id="3a1d5-158">If the new data point is the only one available in the period, the aggregate is based just on that data point.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-158">If the new data point is the only one available in the period, the aggregate is based just on that data point.</span></span>
* <span data-ttu-id="3a1d5-159">An alert can flicker frequently between alert and healthy states, even if you set a long period.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-159">An alert can flicker frequently between alert and healthy states, even if you set a long period.</span></span> <span data-ttu-id="3a1d5-160">This can happen if the metric value hovers around the threshold.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-160">This can happen if the metric value hovers around the threshold.</span></span> <span data-ttu-id="3a1d5-161">There is no hysteresis in the threshold: the transition to alert happens at the same value as the transition to healthy.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-161">There is no hysteresis in the threshold: the transition to alert happens at the same value as the transition to healthy.</span></span>

## <a name="what-are-good-alerts-to-set"></a><span data-ttu-id="3a1d5-162">What are good alerts to set?</span><span class="sxs-lookup"><span data-stu-id="3a1d5-162">What are good alerts to set?</span></span>
<span data-ttu-id="3a1d5-163">It depends on your application.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-163">It depends on your application.</span></span> <span data-ttu-id="3a1d5-164">To start with, it's best not to set too many metrics.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-164">To start with, it's best not to set too many metrics.</span></span> <span data-ttu-id="3a1d5-165">Spend some time looking at your metric charts while your app is running, to get a feel for how it behaves normally.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-165">Spend some time looking at your metric charts while your app is running, to get a feel for how it behaves normally.</span></span> <span data-ttu-id="3a1d5-166">This helps you find ways to improve its performance.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-166">This helps you find ways to improve its performance.</span></span> <span data-ttu-id="3a1d5-167">Then set up alerts to tell you when the metrics go outside the normal zone.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-167">Then set up alerts to tell you when the metrics go outside the normal zone.</span></span> 

<span data-ttu-id="3a1d5-168">Popular alerts include:</span><span class="sxs-lookup"><span data-stu-id="3a1d5-168">Popular alerts include:</span></span>

* <span data-ttu-id="3a1d5-169">[Browser metrics][client], especially Browser **page load times**, are good for web applications.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-169">[Browser metrics][client], especially Browser **page load times**, are good for web applications.</span></span> <span data-ttu-id="3a1d5-170">If your page has a lot of scripts, you'll want to look out for **browser exceptions**.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-170">If your page has a lot of scripts, you'll want to look out for **browser exceptions**.</span></span> <span data-ttu-id="3a1d5-171">In order to get these metrics and alerts, you have to set up [web page monitoring][client].</span><span class="sxs-lookup"><span data-stu-id="3a1d5-171">In order to get these metrics and alerts, you have to set up [web page monitoring][client].</span></span>
* <span data-ttu-id="3a1d5-172">**Server response time** for the server side of web applications.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-172">**Server response time** for the server side of web applications.</span></span> <span data-ttu-id="3a1d5-173">As well as setting up alerts, keep an eye on this metric to see if it varies disproportionately with high request rates: that might indicate that your app is running out of resources.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-173">As well as setting up alerts, keep an eye on this metric to see if it varies disproportionately with high request rates: that might indicate that your app is running out of resources.</span></span> 
* <span data-ttu-id="3a1d5-174">**Server exceptions** - to see them, you have to do some [additional setup](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="3a1d5-174">**Server exceptions** - to see them, you have to do some [additional setup](app-insights-asp-net-exceptions.md).</span></span>

<span data-ttu-id="3a1d5-175">Don't forget that [proactive failure rate diagnostics](app-insights-proactive-failure-diagnostics.md) automatically monitor the rate at which your app responds to requests with failure codes.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-175">Don't forget that [proactive failure rate diagnostics](app-insights-proactive-failure-diagnostics.md) automatically monitor the rate at which your app responds to requests with failure codes.</span></span> 

## <a name="automation"></a><span data-ttu-id="3a1d5-176">Automation</span><span class="sxs-lookup"><span data-stu-id="3a1d5-176">Automation</span></span>
* [<span data-ttu-id="3a1d5-177">Use PowerShell to automate setting up alerts</span><span class="sxs-lookup"><span data-stu-id="3a1d5-177">Use PowerShell to automate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="3a1d5-178">Use webhooks to automate responding to alerts</span><span class="sxs-lookup"><span data-stu-id="3a1d5-178">Use webhooks to automate responding to alerts</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a><span data-ttu-id="3a1d5-179">Video</span><span class="sxs-lookup"><span data-stu-id="3a1d5-179">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a><span data-ttu-id="3a1d5-180">See also</span><span class="sxs-lookup"><span data-stu-id="3a1d5-180">See also</span></span>
* [<span data-ttu-id="3a1d5-181">Availability web tests</span><span class="sxs-lookup"><span data-stu-id="3a1d5-181">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="3a1d5-182">Automate setting up alerts</span><span class="sxs-lookup"><span data-stu-id="3a1d5-182">Automate setting up alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="3a1d5-183">Proactive diagnostics</span><span class="sxs-lookup"><span data-stu-id="3a1d5-183">Proactive diagnostics</span></span>](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md




