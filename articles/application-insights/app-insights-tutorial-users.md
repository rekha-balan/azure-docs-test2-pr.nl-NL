---
title: Understand your customers in Azure Application Insights | Microsoft Docs
description: Tutorial on using Azure Application Insights to understand how customers are using your application.
keywords: ''
services: application-insights
author: mrbullwinkle
ms.author: mbullwin
ms.date: 09/20/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: tutorial
manager: carmonm
ms.openlocfilehash: db61c300ad82270e59d315fa3372d9e4390c7a21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868970"
---
# <a name="use-azure-application-insights-to-understand-how-customers-are-using-your-application"></a><span data-ttu-id="54cb4-103">Use Azure Application Insights to understand how customers are using your application</span><span class="sxs-lookup"><span data-stu-id="54cb4-103">Use Azure Application Insights to understand how customers are using your application</span></span>

<span data-ttu-id="54cb4-104">Azure Application Insights collects usage information to help you understand how your users interact with your application.</span><span class="sxs-lookup"><span data-stu-id="54cb4-104">Azure Application Insights collects usage information to help you understand how your users interact with your application.</span></span>  <span data-ttu-id="54cb4-105">This tutorial walks you through the different resources that are available to analyze this information.</span><span class="sxs-lookup"><span data-stu-id="54cb4-105">This tutorial walks you through the different resources that are available to analyze this information.</span></span>  <span data-ttu-id="54cb4-106">You will learn how to:</span><span class="sxs-lookup"><span data-stu-id="54cb4-106">You will learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="54cb4-107">Analyze details about users accessing your application</span><span class="sxs-lookup"><span data-stu-id="54cb4-107">Analyze details about users accessing your application</span></span>
> * <span data-ttu-id="54cb4-108">Use session information to analyze how customers use your application</span><span class="sxs-lookup"><span data-stu-id="54cb4-108">Use session information to analyze how customers use your application</span></span>
> * <span data-ttu-id="54cb4-109">Define funnels that let you compare your desired user activity to their actual activity</span><span class="sxs-lookup"><span data-stu-id="54cb4-109">Define funnels that let you compare your desired user activity to their actual activity</span></span> 
> * <span data-ttu-id="54cb4-110">Create a workbook to consolidate visualizations and queries into a single document</span><span class="sxs-lookup"><span data-stu-id="54cb4-110">Create a workbook to consolidate visualizations and queries into a single document</span></span>
> * <span data-ttu-id="54cb4-111">Group similar users to analyze them together</span><span class="sxs-lookup"><span data-stu-id="54cb4-111">Group similar users to analyze them together</span></span>
> * <span data-ttu-id="54cb4-112">Learn which users are returning to your application</span><span class="sxs-lookup"><span data-stu-id="54cb4-112">Learn which users are returning to your application</span></span>
> * <span data-ttu-id="54cb4-113">Inspect how users navigate through your application</span><span class="sxs-lookup"><span data-stu-id="54cb4-113">Inspect how users navigate through your application</span></span>


## <a name="prerequisites"></a><span data-ttu-id="54cb4-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="54cb4-114">Prerequisites</span></span>

<span data-ttu-id="54cb4-115">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="54cb4-115">To complete this tutorial:</span></span>

- <span data-ttu-id="54cb4-116">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span><span class="sxs-lookup"><span data-stu-id="54cb4-116">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="54cb4-117">ASP.NET and web development</span><span class="sxs-lookup"><span data-stu-id="54cb4-117">ASP.NET and web development</span></span>
    - <span data-ttu-id="54cb4-118">Azure development</span><span class="sxs-lookup"><span data-stu-id="54cb4-118">Azure development</span></span>
- <span data-ttu-id="54cb4-119">Download and install the [Visual Studio Snapshot Debugger](http://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="54cb4-119">Download and install the [Visual Studio Snapshot Debugger](http://aka.ms/snapshotdebugger).</span></span>
- <span data-ttu-id="54cb4-120">Deploy a .NET application to Azure and [enable the Application Insights SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="54cb4-120">Deploy a .NET application to Azure and [enable the Application Insights SDK](app-insights-asp-net.md).</span></span> 
- <span data-ttu-id="54cb4-121">[Send telemetry from your application](app-insights-usage-overview.md#send-telemetry-from-your-app) for adding custom events/page views</span><span class="sxs-lookup"><span data-stu-id="54cb4-121">[Send telemetry from your application](app-insights-usage-overview.md#send-telemetry-from-your-app) for adding custom events/page views</span></span>
- <span data-ttu-id="54cb4-122">Send [user context](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context) to track what a user does over time and fully utilize the usage features.</span><span class="sxs-lookup"><span data-stu-id="54cb4-122">Send [user context](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context) to track what a user does over time and fully utilize the usage features.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="54cb4-123">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="54cb4-123">Log in to Azure</span></span>
<span data-ttu-id="54cb4-124">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="54cb4-124">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>

## <a name="get-information-about-your-users"></a><span data-ttu-id="54cb4-125">Get information about your users</span><span class="sxs-lookup"><span data-stu-id="54cb4-125">Get information about your users</span></span>
<span data-ttu-id="54cb4-126">The **Users** panel allows you to understand important details about your users in a variety of ways.</span><span class="sxs-lookup"><span data-stu-id="54cb4-126">The **Users** panel allows you to understand important details about your users in a variety of ways.</span></span> <span data-ttu-id="54cb4-127">You can use this panel to understand such information as where your users are connecting from, details of their client, and what areas of your application they're accessing.</span><span class="sxs-lookup"><span data-stu-id="54cb4-127">You can use this panel to understand such information as where your users are connecting from, details of their client, and what areas of your application they're accessing.</span></span> 

1. <span data-ttu-id="54cb4-128">Select **Application Insights** and then select your subscription.</span><span class="sxs-lookup"><span data-stu-id="54cb4-128">Select **Application Insights** and then select your subscription.</span></span>
2. <span data-ttu-id="54cb4-129">Select **Users** in the menu.</span><span class="sxs-lookup"><span data-stu-id="54cb4-129">Select **Users** in the menu.</span></span>
3. <span data-ttu-id="54cb4-130">The default view shows the number of unique users that have connected to your application over the past 24 hours.</span><span class="sxs-lookup"><span data-stu-id="54cb4-130">The default view shows the number of unique users that have connected to your application over the past 24 hours.</span></span>  <span data-ttu-id="54cb4-131">You can change the time window and set various other criteria to filter this information.</span><span class="sxs-lookup"><span data-stu-id="54cb4-131">You can change the time window and set various other criteria to filter this information.</span></span>

    ![Query Builder](media\app-insights-tutorial-users\QueryBuilder.png)

6. <span data-ttu-id="54cb4-133">Click the **During** dropdown and change the time window to 7 days.</span><span class="sxs-lookup"><span data-stu-id="54cb4-133">Click the **During** dropdown and change the time window to 7 days.</span></span>  <span data-ttu-id="54cb4-134">This increases the data included in the different charts in the panel.</span><span class="sxs-lookup"><span data-stu-id="54cb4-134">This increases the data included in the different charts in the panel.</span></span>

    ![Change Time Range](media\app-insights-tutorial-users\TimeRange.png)

4. <span data-ttu-id="54cb4-136">Click the **Split by** dropdown to add a breakdown by a user property to the graph.</span><span class="sxs-lookup"><span data-stu-id="54cb4-136">Click the **Split by** dropdown to add a breakdown by a user property to the graph.</span></span>  <span data-ttu-id="54cb4-137">Select **Country or region**.</span><span class="sxs-lookup"><span data-stu-id="54cb4-137">Select **Country or region**.</span></span>  <span data-ttu-id="54cb4-138">The graph includes the same data but allows you to view a breakdown of the number of users for each country.</span><span class="sxs-lookup"><span data-stu-id="54cb4-138">The graph includes the same data but allows you to view a breakdown of the number of users for each country.</span></span>

    ![Country or Region graph](media\app-insights-tutorial-users\CountryorRegion.png)

5. <span data-ttu-id="54cb4-140">Position the cursor over different bars in the chart and note that the count for each country reflects only the time window represented by that bar.</span><span class="sxs-lookup"><span data-stu-id="54cb4-140">Position the cursor over different bars in the chart and note that the count for each country reflects only the time window represented by that bar.</span></span>
6. <span data-ttu-id="54cb4-141">Have a look at the **Insights** column at the right that perform analysis on your user data.</span><span class="sxs-lookup"><span data-stu-id="54cb4-141">Have a look at the **Insights** column at the right that perform analysis on your user data.</span></span>  <span data-ttu-id="54cb4-142">This provides information such as the number of unique sessions over the time period and records with common properties that make up significant of the user data</span><span class="sxs-lookup"><span data-stu-id="54cb4-142">This provides information such as the number of unique sessions over the time period and records with common properties that make up significant of the user data</span></span> 

    ![Insights column](media\app-insights-tutorial-users\insights.png)


## <a name="analyze-user-sessions"></a><span data-ttu-id="54cb4-144">Analyze user sessions</span><span class="sxs-lookup"><span data-stu-id="54cb4-144">Analyze user sessions</span></span>
<span data-ttu-id="54cb4-145">The **Sessions** panel is similar to the **Users** panel.</span><span class="sxs-lookup"><span data-stu-id="54cb4-145">The **Sessions** panel is similar to the **Users** panel.</span></span>  <span data-ttu-id="54cb4-146">Where **Users** helps you understand details about the users accessing your application, **Sessions** helps you understand how those users used your application.</span><span class="sxs-lookup"><span data-stu-id="54cb4-146">Where **Users** helps you understand details about the users accessing your application, **Sessions** helps you understand how those users used your application.</span></span>  

1. <span data-ttu-id="54cb4-147">Select **Sessions** in the menu.</span><span class="sxs-lookup"><span data-stu-id="54cb4-147">Select **Sessions** in the menu.</span></span>
2. <span data-ttu-id="54cb4-148">Have a look at the graph and note that you have the same options to filter and break down the data as in the **Users** panel.</span><span class="sxs-lookup"><span data-stu-id="54cb4-148">Have a look at the graph and note that you have the same options to filter and break down the data as in the **Users** panel.</span></span>

    ![Sessions Query Builder](media\app-insights-tutorial-users\SessionsBuilder.png)

3. <span data-ttu-id="54cb4-150">The **Sample of these sessions** pane on the right lists sessions that include a large number of events.</span><span class="sxs-lookup"><span data-stu-id="54cb4-150">The **Sample of these sessions** pane on the right lists sessions that include a large number of events.</span></span>  <span data-ttu-id="54cb4-151">These are interesting sessions to analyze.</span><span class="sxs-lookup"><span data-stu-id="54cb4-151">These are interesting sessions to analyze.</span></span>

    ![Sample of these sessions](media\app-insights-tutorial-users\SessionsSample.png)

4. <span data-ttu-id="54cb4-153">Click on one of the sessions to view its **Session Timeline**, which shows every action in the sessions.</span><span class="sxs-lookup"><span data-stu-id="54cb4-153">Click on one of the sessions to view its **Session Timeline**, which shows every action in the sessions.</span></span>  <span data-ttu-id="54cb4-154">This can help you identify information such as the sessions with a large number of exceptions.</span><span class="sxs-lookup"><span data-stu-id="54cb4-154">This can help you identify information such as the sessions with a large number of exceptions.</span></span>

    ![Sessions Timeline](media\app-insights-tutorial-users\SessionsTimeline.png)

## <a name="group-together-similar-users"></a><span data-ttu-id="54cb4-156">Group together similar users</span><span class="sxs-lookup"><span data-stu-id="54cb4-156">Group together similar users</span></span>
<span data-ttu-id="54cb4-157">A **Cohort** is a set of users groupd on similar characteristics.</span><span class="sxs-lookup"><span data-stu-id="54cb4-157">A **Cohort** is a set of users groupd on similar characteristics.</span></span>  <span data-ttu-id="54cb4-158">You can use cohorts to filter data in other panels allowing you to analyze particular groups of users.</span><span class="sxs-lookup"><span data-stu-id="54cb4-158">You can use cohorts to filter data in other panels allowing you to analyze particular groups of users.</span></span>  <span data-ttu-id="54cb4-159">For example, you might want to analyze only users who completed a purchase.</span><span class="sxs-lookup"><span data-stu-id="54cb4-159">For example, you might want to analyze only users who completed a purchase.</span></span>

1.  <span data-ttu-id="54cb4-160">Select **Cohorts** in the menu.</span><span class="sxs-lookup"><span data-stu-id="54cb4-160">Select **Cohorts** in the menu.</span></span>
2.  <span data-ttu-id="54cb4-161">Click **New** to create a new cohort.</span><span class="sxs-lookup"><span data-stu-id="54cb4-161">Click **New** to create a new cohort.</span></span>
3.  <span data-ttu-id="54cb4-162">Select the **Who used** dropdown and select an action.</span><span class="sxs-lookup"><span data-stu-id="54cb4-162">Select the **Who used** dropdown and select an action.</span></span>  <span data-ttu-id="54cb4-163">Only users who performed this action within the time window of the report will be included.</span><span class="sxs-lookup"><span data-stu-id="54cb4-163">Only users who performed this action within the time window of the report will be included.</span></span>

    ![Cohort who performed specified actions](media\app-insights-tutorial-users\CohortsDropdown.png)

4.  <span data-ttu-id="54cb4-165">Select **Users** in the menu.</span><span class="sxs-lookup"><span data-stu-id="54cb4-165">Select **Users** in the menu.</span></span>
5.  <span data-ttu-id="54cb4-166">In the **Show** dropdown, select the cohort you just created.</span><span class="sxs-lookup"><span data-stu-id="54cb4-166">In the **Show** dropdown, select the cohort you just created.</span></span>  <span data-ttu-id="54cb4-167">The data for the graph is limited to those users.</span><span class="sxs-lookup"><span data-stu-id="54cb4-167">The data for the graph is limited to those users.</span></span>

    ![Cohort in users tool](media\app-insights-tutorial-users\UsersCohort.png)


## <a name="compare-desired-activity-to-reality"></a><span data-ttu-id="54cb4-169">Compare desired activity to reality</span><span class="sxs-lookup"><span data-stu-id="54cb4-169">Compare desired activity to reality</span></span>
<span data-ttu-id="54cb4-170">While the previous panels are focused on what users of your application did, **Funnels** focus on what you want users to do.</span><span class="sxs-lookup"><span data-stu-id="54cb4-170">While the previous panels are focused on what users of your application did, **Funnels** focus on what you want users to do.</span></span>  <span data-ttu-id="54cb4-171">A funnel represents a set of steps in your application and the percentage of users who move between steps.</span><span class="sxs-lookup"><span data-stu-id="54cb4-171">A funnel represents a set of steps in your application and the percentage of users who move between steps.</span></span>  <span data-ttu-id="54cb4-172">For example, you could create a funnel that measures the percentage of users who connect to your application who search product.</span><span class="sxs-lookup"><span data-stu-id="54cb4-172">For example, you could create a funnel that measures the percentage of users who connect to your application who search product.</span></span>  <span data-ttu-id="54cb4-173">You can then see the percentage of users who add that product to a shopping cart, and then the percentage of those who complete a purchase.</span><span class="sxs-lookup"><span data-stu-id="54cb4-173">You can then see the percentage of users who add that product to a shopping cart, and then the percentage of those who complete a purchase.</span></span>

1. <span data-ttu-id="54cb4-174">Select **Funnels** in the menu and then click **New**.</span><span class="sxs-lookup"><span data-stu-id="54cb4-174">Select **Funnels** in the menu and then click **New**.</span></span> 

    ![](media\app-insights-tutorial-users\funnelsnew.png)

2. <span data-ttu-id="54cb4-175">Type in a **Funnel Name**.</span><span class="sxs-lookup"><span data-stu-id="54cb4-175">Type in a **Funnel Name**.</span></span>
3. <span data-ttu-id="54cb4-176">Create a funnel with at least two steps by selecting an action for each step.</span><span class="sxs-lookup"><span data-stu-id="54cb4-176">Create a funnel with at least two steps by selecting an action for each step.</span></span>  <span data-ttu-id="54cb4-177">The list of actions is built from usage data collected by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="54cb4-177">The list of actions is built from usage data collected by Application Insights.</span></span>

    ![](media\app-insights-tutorial-users\funnelsedit.png)

4. <span data-ttu-id="54cb4-178">Click **Save** to save the funnel and then view its results.</span><span class="sxs-lookup"><span data-stu-id="54cb4-178">Click **Save** to save the funnel and then view its results.</span></span>  <span data-ttu-id="54cb4-179">The window to the right of the funnel shows the most common events before the first activity and after the last activity to help you understand user tendencies around the particular sequence.</span><span class="sxs-lookup"><span data-stu-id="54cb4-179">The window to the right of the funnel shows the most common events before the first activity and after the last activity to help you understand user tendencies around the particular sequence.</span></span>

    ![](media\app-insights-tutorial-users\funnelsright.png)


## <a name="learn-which-customers-return"></a><span data-ttu-id="54cb4-180">Learn which customers return</span><span class="sxs-lookup"><span data-stu-id="54cb4-180">Learn which customers return</span></span>
<span data-ttu-id="54cb4-181">**Retention** helps you understand which users are coming back to your application.</span><span class="sxs-lookup"><span data-stu-id="54cb4-181">**Retention** helps you understand which users are coming back to your application.</span></span>  

1. <span data-ttu-id="54cb4-182">Select **Retention** in the menu.</span><span class="sxs-lookup"><span data-stu-id="54cb4-182">Select **Retention** in the menu.</span></span>
2. <span data-ttu-id="54cb4-183">By default, the analyzed information includes users who performed any action and then returned to perform any action.</span><span class="sxs-lookup"><span data-stu-id="54cb4-183">By default, the analyzed information includes users who performed any action and then returned to perform any action.</span></span>  <span data-ttu-id="54cb4-184">You can change this filter to any include, for example, only those users who returned after completing a purchase.</span><span class="sxs-lookup"><span data-stu-id="54cb4-184">You can change this filter to any include, for example, only those users who returned after completing a purchase.</span></span>

    ![](media\app-insights-tutorial-users\retentionquery.png)

3. <span data-ttu-id="54cb4-185">The returning users that match the criteria are shown in graphical and table form for different time durations.</span><span class="sxs-lookup"><span data-stu-id="54cb4-185">The returning users that match the criteria are shown in graphical and table form for different time durations.</span></span>  <span data-ttu-id="54cb4-186">The typical pattern is for a gradual drop in returning users over time.</span><span class="sxs-lookup"><span data-stu-id="54cb4-186">The typical pattern is for a gradual drop in returning users over time.</span></span>  <span data-ttu-id="54cb4-187">A sudden drop from one time period to the next might raise a concern.</span><span class="sxs-lookup"><span data-stu-id="54cb4-187">A sudden drop from one time period to the next might raise a concern.</span></span> 

    ![](media\app-insights-tutorial-users\retentiongraph.png)

## <a name="analyze-user-navigation"></a><span data-ttu-id="54cb4-188">Analyze user navigation</span><span class="sxs-lookup"><span data-stu-id="54cb4-188">Analyze user navigation</span></span>
<span data-ttu-id="54cb4-189">A **User flow** visualizes how users navigate between the pages and features of your application.</span><span class="sxs-lookup"><span data-stu-id="54cb4-189">A **User flow** visualizes how users navigate between the pages and features of your application.</span></span>  <span data-ttu-id="54cb4-190">This helps you answer questions such as where users typically move from a particular page, how they typically exit your application, and if there are any actions that are regularly repeated.</span><span class="sxs-lookup"><span data-stu-id="54cb4-190">This helps you answer questions such as where users typically move from a particular page, how they typically exit your application, and if there are any actions that are regularly repeated.</span></span>

1.  <span data-ttu-id="54cb4-191">Select **User flows** in the menu.</span><span class="sxs-lookup"><span data-stu-id="54cb4-191">Select **User flows** in the menu.</span></span>
2.  <span data-ttu-id="54cb4-192">Click **New** to create a new user flow and then click **Edit** to edit its details.</span><span class="sxs-lookup"><span data-stu-id="54cb4-192">Click **New** to create a new user flow and then click **Edit** to edit its details.</span></span>
3.  <span data-ttu-id="54cb4-193">Increase the **Time Range** to 7 days and then select an initial event.</span><span class="sxs-lookup"><span data-stu-id="54cb4-193">Increase the **Time Range** to 7 days and then select an initial event.</span></span>  <span data-ttu-id="54cb4-194">The flow will track user sessions that start with that event.</span><span class="sxs-lookup"><span data-stu-id="54cb4-194">The flow will track user sessions that start with that event.</span></span>

    ![](media\app-insights-tutorial-users\flowsedit.png)

4.  <span data-ttu-id="54cb4-195">The user flow is displayed, and you can see the different user paths and their session counts.</span><span class="sxs-lookup"><span data-stu-id="54cb4-195">The user flow is displayed, and you can see the different user paths and their session counts.</span></span>  <span data-ttu-id="54cb4-196">Blue lines indicate an action that the user performed after the current action.</span><span class="sxs-lookup"><span data-stu-id="54cb4-196">Blue lines indicate an action that the user performed after the current action.</span></span>  <span data-ttu-id="54cb4-197">A red line indicates the end of the user session.</span><span class="sxs-lookup"><span data-stu-id="54cb4-197">A red line indicates the end of the user session.</span></span>

    ![](media\app-insights-tutorial-users\flows.png)

5.  <span data-ttu-id="54cb4-198">To remove an event from the flow, click the **x** in the corner of the action and then click **Create Graph**.</span><span class="sxs-lookup"><span data-stu-id="54cb4-198">To remove an event from the flow, click the **x** in the corner of the action and then click **Create Graph**.</span></span>  <span data-ttu-id="54cb4-199">The graph is redrawn with any instances of that event removed.</span><span class="sxs-lookup"><span data-stu-id="54cb4-199">The graph is redrawn with any instances of that event removed.</span></span>  <span data-ttu-id="54cb4-200">Click **Edit** to see that the event is now added to **Excluded events**.</span><span class="sxs-lookup"><span data-stu-id="54cb4-200">Click **Edit** to see that the event is now added to **Excluded events**.</span></span>

    ![](media\app-insights-tutorial-users\flowsexclude.png)

## <a name="consolidate-usage-data"></a><span data-ttu-id="54cb4-201">Consolidate usage data</span><span class="sxs-lookup"><span data-stu-id="54cb4-201">Consolidate usage data</span></span>
<span data-ttu-id="54cb4-202">**Workbooks** combine data visualizations, Analytics queries, and text into interactive documents.</span><span class="sxs-lookup"><span data-stu-id="54cb4-202">**Workbooks** combine data visualizations, Analytics queries, and text into interactive documents.</span></span>  <span data-ttu-id="54cb4-203">You can use workbooks to group together common usage information, consolidate information from a particular incident, or report back to your team on your application's usage.</span><span class="sxs-lookup"><span data-stu-id="54cb4-203">You can use workbooks to group together common usage information, consolidate information from a particular incident, or report back to your team on your application's usage.</span></span>

1.  <span data-ttu-id="54cb4-204">Select **Workbooks** in the menu.</span><span class="sxs-lookup"><span data-stu-id="54cb4-204">Select **Workbooks** in the menu.</span></span>
2.  <span data-ttu-id="54cb4-205">Click **New** to create a new workbook.</span><span class="sxs-lookup"><span data-stu-id="54cb4-205">Click **New** to create a new workbook.</span></span>
3.  <span data-ttu-id="54cb4-206">A query is already provided that includes all usage data in the last day displayed as a bar chart.</span><span class="sxs-lookup"><span data-stu-id="54cb4-206">A query is already provided that includes all usage data in the last day displayed as a bar chart.</span></span>  <span data-ttu-id="54cb4-207">You can use this query, manually edit it, or click **Sample queries** to select from other useful queries.</span><span class="sxs-lookup"><span data-stu-id="54cb4-207">You can use this query, manually edit it, or click **Sample queries** to select from other useful queries.</span></span>

    ![](media\app-insights-tutorial-users\samplequeries.png)

4.  <span data-ttu-id="54cb4-208">Click **Done editing**.</span><span class="sxs-lookup"><span data-stu-id="54cb4-208">Click **Done editing**.</span></span>
5.  <span data-ttu-id="54cb4-209">Click **Edit** in the top pane to edit the text at the top of the workbook.</span><span class="sxs-lookup"><span data-stu-id="54cb4-209">Click **Edit** in the top pane to edit the text at the top of the workbook.</span></span>  <span data-ttu-id="54cb4-210">This is formatted using markdown.</span><span class="sxs-lookup"><span data-stu-id="54cb4-210">This is formatted using markdown.</span></span>

    ![](media\app-insights-tutorial-users\markdown.png)

6.  <span data-ttu-id="54cb4-211">Click **Add users** to add a graph with user information.</span><span class="sxs-lookup"><span data-stu-id="54cb4-211">Click **Add users** to add a graph with user information.</span></span>  <span data-ttu-id="54cb4-212">Edit the details of the graph if you want and then click **Done editing** to save it.</span><span class="sxs-lookup"><span data-stu-id="54cb4-212">Edit the details of the graph if you want and then click **Done editing** to save it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="54cb4-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="54cb4-213">Next steps</span></span>
<span data-ttu-id="54cb4-214">Now that you've learned how to analyze your users, advance to the next tutorial to learn how to create custom dashboards that combine this information with other useful data about your application.</span><span class="sxs-lookup"><span data-stu-id="54cb4-214">Now that you've learned how to analyze your users, advance to the next tutorial to learn how to create custom dashboards that combine this information with other useful data about your application.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="54cb4-215">Create custom dashboards</span><span class="sxs-lookup"><span data-stu-id="54cb4-215">Create custom dashboards</span></span>](app-insights-tutorial-dashboards.md)
