---
title: Service Map solution self paced demo | Microsoft Docs
description: Service Map is a solution in Operations Management Suite (OMS) that automatically discovers application components on Windows and Linux systems and maps the communication between services.  This is a self paced demo that walks through using Service Map to identify and diagnose a simulated problem in a web application.
services: operations-management-suite
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 0897dde19089da0928f29d2e7aed1bc5b992d418
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552760"
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a><span data-ttu-id="7f97b-104">Operations Management Suite (OMS) self paced demo - Service Map</span><span class="sxs-lookup"><span data-stu-id="7f97b-104">Operations Management Suite (OMS) self paced demo - Service Map</span></span>
<span data-ttu-id="7f97b-105">This is a self paced demo that walks through using the [Service Map solution](operations-management-suite-service-map.md) in Operations Management Suite (OMS) to identify and diagnose a simulated problem in a web application.</span><span class="sxs-lookup"><span data-stu-id="7f97b-105">This is a self paced demo that walks through using the [Service Map solution](operations-management-suite-service-map.md) in Operations Management Suite (OMS) to identify and diagnose a simulated problem in a web application.</span></span>  <span data-ttu-id="7f97b-106">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span><span class="sxs-lookup"><span data-stu-id="7f97b-106">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span>  <span data-ttu-id="7f97b-107">It also consolidates data collected by other OMS services to assist you in analyzing performance and identifying issues.</span><span class="sxs-lookup"><span data-stu-id="7f97b-107">It also consolidates data collected by other OMS services to assist you in analyzing performance and identifying issues.</span></span>  <span data-ttu-id="7f97b-108">You'll also use [log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md) to drill down on collected data in order to identify the root problem.</span><span class="sxs-lookup"><span data-stu-id="7f97b-108">You'll also use [log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md) to drill down on collected data in order to identify the root problem.</span></span>


## <a name="scenario-description"></a><span data-ttu-id="7f97b-109">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7f97b-109">Scenario description</span></span>
<span data-ttu-id="7f97b-110">You've just received a notification that the ACME Customer Portal application is having performance issues.</span><span class="sxs-lookup"><span data-stu-id="7f97b-110">You've just received a notification that the ACME Customer Portal application is having performance issues.</span></span>  <span data-ttu-id="7f97b-111">The only information that you have is that these issues started about 4:00 am PST today.</span><span class="sxs-lookup"><span data-stu-id="7f97b-111">The only information that you have is that these issues started about 4:00 am PST today.</span></span>  <span data-ttu-id="7f97b-112">You aren't entirely sure of all the components that the portal is dependent on other than a set of web servers.</span><span class="sxs-lookup"><span data-stu-id="7f97b-112">You aren't entirely sure of all the components that the portal is dependent on other than a set of web servers.</span></span>  

## <a name="components-and-features-used"></a><span data-ttu-id="7f97b-113">Components and features used</span><span class="sxs-lookup"><span data-stu-id="7f97b-113">Components and features used</span></span>
- [<span data-ttu-id="7f97b-114">Service Map solution</span><span class="sxs-lookup"><span data-stu-id="7f97b-114">Service Map solution</span></span>](operations-management-suite-service-map.md)
- [<span data-ttu-id="7f97b-115">Log Analytics log searches</span><span class="sxs-lookup"><span data-stu-id="7f97b-115">Log Analytics log searches</span></span>](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a><span data-ttu-id="7f97b-116">Walk through</span><span class="sxs-lookup"><span data-stu-id="7f97b-116">Walk through</span></span>

### <a name="1-connect-to-the-oms-experience-center"></a><span data-ttu-id="7f97b-117">1. Connect to the OMS Experience Center</span><span class="sxs-lookup"><span data-stu-id="7f97b-117">1. Connect to the OMS Experience Center</span></span>
<span data-ttu-id="7f97b-118">This walk through uses the [Operations Management Suite Experience Center](https://experience.mms.microsoft.com/) which provides a complete OMS environment with sample data.</span><span class="sxs-lookup"><span data-stu-id="7f97b-118">This walk through uses the [Operations Management Suite Experience Center](https://experience.mms.microsoft.com/) which provides a complete OMS environment with sample data.</span></span> <span data-ttu-id="7f97b-119">Start by following this link, provide your information and then select the **Insight and Analytics** scenario.</span><span class="sxs-lookup"><span data-stu-id="7f97b-119">Start by following this link, provide your information and then select the **Insight and Analytics** scenario.</span></span>


### <a name="2-start-service-map"></a><span data-ttu-id="7f97b-120">2. Start Service Map</span><span class="sxs-lookup"><span data-stu-id="7f97b-120">2. Start Service Map</span></span>
<span data-ttu-id="7f97b-121">Start the Service Map solution by clicking on the **Service Map** tile.</span><span class="sxs-lookup"><span data-stu-id="7f97b-121">Start the Service Map solution by clicking on the **Service Map** tile.</span></span>

![Service Map Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/tile.png)

<span data-ttu-id="7f97b-123">The Service Map console is displayed.</span><span class="sxs-lookup"><span data-stu-id="7f97b-123">The Service Map console is displayed.</span></span>  <span data-ttu-id="7f97b-124">In the left pane is a list of computers in your environment with the Service Map agent installed.</span><span class="sxs-lookup"><span data-stu-id="7f97b-124">In the left pane is a list of computers in your environment with the Service Map agent installed.</span></span>  <span data-ttu-id="7f97b-125">You'll select the computer that you want to view from this list.</span><span class="sxs-lookup"><span data-stu-id="7f97b-125">You'll select the computer that you want to view from this list.</span></span>

![Computer list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a><span data-ttu-id="7f97b-127">3. View computer</span><span class="sxs-lookup"><span data-stu-id="7f97b-127">3. View computer</span></span>
<span data-ttu-id="7f97b-128">We know that the web servers are called AcmeWFE001 and AcmeWFE002, so this seems like a reasonable place to start.</span><span class="sxs-lookup"><span data-stu-id="7f97b-128">We know that the web servers are called AcmeWFE001 and AcmeWFE002, so this seems like a reasonable place to start.</span></span>  <span data-ttu-id="7f97b-129">Click on **AcmeWFE001**.</span><span class="sxs-lookup"><span data-stu-id="7f97b-129">Click on **AcmeWFE001**.</span></span>  <span data-ttu-id="7f97b-130">This displays the map for AcmeWFE001 and all of its dependencies.</span><span class="sxs-lookup"><span data-stu-id="7f97b-130">This displays the map for AcmeWFE001 and all of its dependencies.</span></span>  <span data-ttu-id="7f97b-131">You can see which processes are running on the selected computer and which external services they communicate with.</span><span class="sxs-lookup"><span data-stu-id="7f97b-131">You can see which processes are running on the selected computer and which external services they communicate with.</span></span>

![Web server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/web-server.png)

<span data-ttu-id="7f97b-133">We're concerned about the performance of our web application so click on the **AcmeAppPool (IIS App Pool)** process.</span><span class="sxs-lookup"><span data-stu-id="7f97b-133">We're concerned about the performance of our web application so click on the **AcmeAppPool (IIS App Pool)** process.</span></span>  <span data-ttu-id="7f97b-134">This displays the details for this process and highlights its dependencies.</span><span class="sxs-lookup"><span data-stu-id="7f97b-134">This displays the details for this process and highlights its dependencies.</span></span>  

![App Pool](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a><span data-ttu-id="7f97b-136">4. Change time window</span><span class="sxs-lookup"><span data-stu-id="7f97b-136">4. Change time window</span></span>

<span data-ttu-id="7f97b-137">We heard that the problem started at 4:00 AM so let's have a look at what was happening at that time.</span><span class="sxs-lookup"><span data-stu-id="7f97b-137">We heard that the problem started at 4:00 AM so let's have a look at what was happening at that time.</span></span> <span data-ttu-id="7f97b-138">Click on **Time Range** and change the time to 4:00 AM PST (keep the current date and adjust for your local time zone) with a duration of 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="7f97b-138">Click on **Time Range** and change the time to 4:00 AM PST (keep the current date and adjust for your local time zone) with a duration of 20 minutes.</span></span>

![Time Picker](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a><span data-ttu-id="7f97b-140">5. View alert</span><span class="sxs-lookup"><span data-stu-id="7f97b-140">5. View alert</span></span>

<span data-ttu-id="7f97b-141">We now see that the **acmetomcat** dependency has an alert displayed, so that's our potential problem.</span><span class="sxs-lookup"><span data-stu-id="7f97b-141">We now see that the **acmetomcat** dependency has an alert displayed, so that's our potential problem.</span></span>  <span data-ttu-id="7f97b-142">Click on the alert icon in **acmetomcat** to show the details for the alert.</span><span class="sxs-lookup"><span data-stu-id="7f97b-142">Click on the alert icon in **acmetomcat** to show the details for the alert.</span></span>  <span data-ttu-id="7f97b-143">We can see that we have critical CPU utilization and can expand it for more detail.</span><span class="sxs-lookup"><span data-stu-id="7f97b-143">We can see that we have critical CPU utilization and can expand it for more detail.</span></span>  <span data-ttu-id="7f97b-144">This is probably what's causing our slow performance.</span><span class="sxs-lookup"><span data-stu-id="7f97b-144">This is probably what's causing our slow performance.</span></span> 

![Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a><span data-ttu-id="7f97b-146">6. View performance</span><span class="sxs-lookup"><span data-stu-id="7f97b-146">6. View performance</span></span>

<span data-ttu-id="7f97b-147">Let's have a closer look at **acmetomcat**.</span><span class="sxs-lookup"><span data-stu-id="7f97b-147">Let's have a closer look at **acmetomcat**.</span></span>  <span data-ttu-id="7f97b-148">Click in the top right of **acmetomcat** and select **Load Server Map** to show the detail and dependencies for this machine.</span><span class="sxs-lookup"><span data-stu-id="7f97b-148">Click in the top right of **acmetomcat** and select **Load Server Map** to show the detail and dependencies for this machine.</span></span> <span data-ttu-id="7f97b-149">We can then look a bit more into those performance counters to verify our suspicion.</span><span class="sxs-lookup"><span data-stu-id="7f97b-149">We can then look a bit more into those performance counters to verify our suspicion.</span></span>  <span data-ttu-id="7f97b-150">Select the **Performance** tab to display the [performance counters collected by Log Analytics](../log-analytics/log-analytics-data-sources-performance-counters.md) over the time range.</span><span class="sxs-lookup"><span data-stu-id="7f97b-150">Select the **Performance** tab to display the [performance counters collected by Log Analytics](../log-analytics/log-analytics-data-sources-performance-counters.md) over the time range.</span></span>  <span data-ttu-id="7f97b-151">We can see that we're getting periodic spikes in the processor and memory.</span><span class="sxs-lookup"><span data-stu-id="7f97b-151">We can see that we're getting periodic spikes in the processor and memory.</span></span>

![Performance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a><span data-ttu-id="7f97b-153">7. View change tracking</span><span class="sxs-lookup"><span data-stu-id="7f97b-153">7. View change tracking</span></span>
<span data-ttu-id="7f97b-154">Let's see if we can find out what might have caused this high utilization.</span><span class="sxs-lookup"><span data-stu-id="7f97b-154">Let's see if we can find out what might have caused this high utilization.</span></span>  <span data-ttu-id="7f97b-155">Click on the **Summary** tab.  This provides information that OMS has collected from the computer such as failed connections, critical alerts, and software changes.</span><span class="sxs-lookup"><span data-stu-id="7f97b-155">Click on the **Summary** tab.  This provides information that OMS has collected from the computer such as failed connections, critical alerts, and software changes.</span></span>  <span data-ttu-id="7f97b-156">Sections with interesting recent information should already be expanded, and you can expand other sections to inspect information that they contain.</span><span class="sxs-lookup"><span data-stu-id="7f97b-156">Sections with interesting recent information should already be expanded, and you can expand other sections to inspect information that they contain.</span></span>


<span data-ttu-id="7f97b-157">If **Change Tracking** isn't already open, then expand it.</span><span class="sxs-lookup"><span data-stu-id="7f97b-157">If **Change Tracking** isn't already open, then expand it.</span></span>  <span data-ttu-id="7f97b-158">This shows information collected by the [Change Tracking solution](../log-analytics/log-analytics-change-tracking.md).</span><span class="sxs-lookup"><span data-stu-id="7f97b-158">This shows information collected by the [Change Tracking solution](../log-analytics/log-analytics-change-tracking.md).</span></span>  <span data-ttu-id="7f97b-159">It looks like there was a software change made during this time window.</span><span class="sxs-lookup"><span data-stu-id="7f97b-159">It looks like there was a software change made during this time window.</span></span>  <span data-ttu-id="7f97b-160">Click on **Software** to get details.</span><span class="sxs-lookup"><span data-stu-id="7f97b-160">Click on **Software** to get details.</span></span>  <span data-ttu-id="7f97b-161">A backup process was added to the machine just after 4:00 AM, so this appears to be the culprit for the excessive resources being consumed.</span><span class="sxs-lookup"><span data-stu-id="7f97b-161">A backup process was added to the machine just after 4:00 AM, so this appears to be the culprit for the excessive resources being consumed.</span></span>

![Change tracking](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a><span data-ttu-id="7f97b-163">8. View details in Log Search</span><span class="sxs-lookup"><span data-stu-id="7f97b-163">8. View details in Log Search</span></span>
<span data-ttu-id="7f97b-164">We can further verify this by looking at the detailed performance information collected in the Log Analytics repository.</span><span class="sxs-lookup"><span data-stu-id="7f97b-164">We can further verify this by looking at the detailed performance information collected in the Log Analytics repository.</span></span>  <span data-ttu-id="7f97b-165">Click on the **Alerts** tab again and then on one of the **High CPU** alerts.</span><span class="sxs-lookup"><span data-stu-id="7f97b-165">Click on the **Alerts** tab again and then on one of the **High CPU** alerts.</span></span>  <span data-ttu-id="7f97b-166">Click on  **Show in Log Search**.</span><span class="sxs-lookup"><span data-stu-id="7f97b-166">Click on  **Show in Log Search**.</span></span>  <span data-ttu-id="7f97b-167">This opens the Log Search window where you can perform [log searches](../log-analytics/log-analytics-log-searches.md) against any data stored in the repository.</span><span class="sxs-lookup"><span data-stu-id="7f97b-167">This opens the Log Search window where you can perform [log searches](../log-analytics/log-analytics-log-searches.md) against any data stored in the repository.</span></span>  <span data-ttu-id="7f97b-168">Service Map already filled in a queriy for us to retrieve the alert we're interested in.</span><span class="sxs-lookup"><span data-stu-id="7f97b-168">Service Map already filled in a queriy for us to retrieve the alert we're interested in.</span></span>  

![Log search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a><span data-ttu-id="7f97b-170">9. Open saved search</span><span class="sxs-lookup"><span data-stu-id="7f97b-170">9. Open saved search</span></span>
<span data-ttu-id="7f97b-171">Let's see if we can get some more detail on the performance collection that generated this alert and verify our suspicion that the problems are being caused by that backup process.</span><span class="sxs-lookup"><span data-stu-id="7f97b-171">Let's see if we can get some more detail on the performance collection that generated this alert and verify our suspicion that the problems are being caused by that backup process.</span></span>  <span data-ttu-id="7f97b-172">Change the time range to **6 hours**.</span><span class="sxs-lookup"><span data-stu-id="7f97b-172">Change the time range to **6 hours**.</span></span>  <span data-ttu-id="7f97b-173">Then click on **Favorites** and scroll down to the saved searches for **Service Map**.</span><span class="sxs-lookup"><span data-stu-id="7f97b-173">Then click on **Favorites** and scroll down to the saved searches for **Service Map**.</span></span>  <span data-ttu-id="7f97b-174">These are queries that we created specifically for this analysis.</span><span class="sxs-lookup"><span data-stu-id="7f97b-174">These are queries that we created specifically for this analysis.</span></span>  <span data-ttu-id="7f97b-175">Click on **Top 5 Processes by CPU for acmetomcat**.</span><span class="sxs-lookup"><span data-stu-id="7f97b-175">Click on **Top 5 Processes by CPU for acmetomcat**.</span></span>

![Saved search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/operations-management-suite-walkthrough-servicemap/saved-search.png)


<span data-ttu-id="7f97b-177">This query returns a list of the top 5 processes consuming processor on **acmetomcat**.</span><span class="sxs-lookup"><span data-stu-id="7f97b-177">This query returns a list of the top 5 processes consuming processor on **acmetomcat**.</span></span>  <span data-ttu-id="7f97b-178">You can inspect the query to get an introduction to the query language used for log searches.</span><span class="sxs-lookup"><span data-stu-id="7f97b-178">You can inspect the query to get an introduction to the query language used for log searches.</span></span>  <span data-ttu-id="7f97b-179">If you were interested in the processes on other computers, you could modify the query to retrieve that information.</span><span class="sxs-lookup"><span data-stu-id="7f97b-179">If you were interested in the processes on other computers, you could modify the query to retrieve that information.</span></span>

<span data-ttu-id="7f97b-180">In this case, we can see that the backup process is consistently consuming about 60% of the app server’s CPU.</span><span class="sxs-lookup"><span data-stu-id="7f97b-180">In this case, we can see that the backup process is consistently consuming about 60% of the app server’s CPU.</span></span>  <span data-ttu-id="7f97b-181">It's pretty obvious that this new process is responsible for our performance problem.</span><span class="sxs-lookup"><span data-stu-id="7f97b-181">It's pretty obvious that this new process is responsible for our performance problem.</span></span>  <span data-ttu-id="7f97b-182">Our solution would obviously be to remove this new backup software off the application server.</span><span class="sxs-lookup"><span data-stu-id="7f97b-182">Our solution would obviously be to remove this new backup software off the application server.</span></span>  <span data-ttu-id="7f97b-183">We could actually leverage Desired State Configuration (DSC) managed by Azure Automation to define policies that ensure this process never runs on these critical systems.</span><span class="sxs-lookup"><span data-stu-id="7f97b-183">We could actually leverage Desired State Configuration (DSC) managed by Azure Automation to define policies that ensure this process never runs on these critical systems.</span></span>


## <a name="summary-points"></a><span data-ttu-id="7f97b-184">Summary points</span><span class="sxs-lookup"><span data-stu-id="7f97b-184">Summary points</span></span>
- <span data-ttu-id="7f97b-185">[Service Map](operations-management-suite-service-map.md) provides you with a view of your entire application even if you don't know all of its servers and dependencies.</span><span class="sxs-lookup"><span data-stu-id="7f97b-185">[Service Map](operations-management-suite-service-map.md) provides you with a view of your entire application even if you don't know all of its servers and dependencies.</span></span>
- <span data-ttu-id="7f97b-186">Service Map surfaces data collected by other OMS solutions to help you identify issues with your application and its underlying infrastructure.</span><span class="sxs-lookup"><span data-stu-id="7f97b-186">Service Map surfaces data collected by other OMS solutions to help you identify issues with your application and its underlying infrastructure.</span></span>
- <span data-ttu-id="7f97b-187">[Log searches](../log-analytics/log-analytics-log-searches.md) allow you to drill down into specific data collected in the Log Analytics repository.</span><span class="sxs-lookup"><span data-stu-id="7f97b-187">[Log searches](../log-analytics/log-analytics-log-searches.md) allow you to drill down into specific data collected in the Log Analytics repository.</span></span>    

## <a name="next-steps"></a><span data-ttu-id="7f97b-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f97b-188">Next steps</span></span>
- <span data-ttu-id="7f97b-189">Learn more about [Service Map](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="7f97b-189">Learn more about [Service Map](operations-management-suite-service-map.md).</span></span>
- <span data-ttu-id="7f97b-190">[Deploy and configure](operations-management-suite-service-map-configure.md) Service Map.</span><span class="sxs-lookup"><span data-stu-id="7f97b-190">[Deploy and configure](operations-management-suite-service-map-configure.md) Service Map.</span></span>
- <span data-ttu-id="7f97b-191">Learn about [Log Analytics](../log-analytics/log-analytics-overview.md) which is required for Service Map and stores operational data stored by agents.</span><span class="sxs-lookup"><span data-stu-id="7f97b-191">Learn about [Log Analytics](../log-analytics/log-analytics-overview.md) which is required for Service Map and stores operational data stored by agents.</span></span>









