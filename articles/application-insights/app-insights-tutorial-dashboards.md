---
title: Create custom dashboards in Azure Application Insights | Microsoft Docs
description: Tutorial to create custom KPI dashboards using Azure Application Insights.
keywords: ''
services: application-insights
author: mrbullwinkle
ms.author: mbullwin
ms.date: 09/20/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: tutorial
manager: carmonm
ms.openlocfilehash: 50d2545d5145f1d93a1ea9fed3e4f98b474d41b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868547"
---
# <a name="create-custom-kpi-dashboards-using-azure-application-insights"></a><span data-ttu-id="77f63-103">Create custom KPI dashboards using Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="77f63-103">Create custom KPI dashboards using Azure Application Insights</span></span>

<span data-ttu-id="77f63-104">You can create multiple dashboards in the Azure portal that each include tiles visualizing data from multiple Azure resources across different resource groups and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="77f63-104">You can create multiple dashboards in the Azure portal that each include tiles visualizing data from multiple Azure resources across different resource groups and subscriptions.</span></span>  <span data-ttu-id="77f63-105">You can pin different charts and views from Azure Application Insights to create custom dashboards that provide you with complete picture of the health and performance of your application.</span><span class="sxs-lookup"><span data-stu-id="77f63-105">You can pin different charts and views from Azure Application Insights to create custom dashboards that provide you with complete picture of the health and performance of your application.</span></span>  <span data-ttu-id="77f63-106">This tutorial walks you through the creation of a custom dashboard that includes multiple types of data and visualizations from Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="77f63-106">This tutorial walks you through the creation of a custom dashboard that includes multiple types of data and visualizations from Azure Application Insights.</span></span>  <span data-ttu-id="77f63-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="77f63-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77f63-108">Create a custom dashboard in Azure</span><span class="sxs-lookup"><span data-stu-id="77f63-108">Create a custom dashboard in Azure</span></span>
> * <span data-ttu-id="77f63-109">Add a tile from the Tile Gallery</span><span class="sxs-lookup"><span data-stu-id="77f63-109">Add a tile from the Tile Gallery</span></span>
> * <span data-ttu-id="77f63-110">Add standard metrics in Application Insights to the dashboard</span><span class="sxs-lookup"><span data-stu-id="77f63-110">Add standard metrics in Application Insights to the dashboard</span></span> 
> * <span data-ttu-id="77f63-111">Add a custom metric chart Application Insights to the dashboard</span><span class="sxs-lookup"><span data-stu-id="77f63-111">Add a custom metric chart Application Insights to the dashboard</span></span>
> * <span data-ttu-id="77f63-112">Add the results of an Analytics query to the dashboard</span><span class="sxs-lookup"><span data-stu-id="77f63-112">Add the results of an Analytics query to the dashboard</span></span> 



## <a name="prerequisites"></a><span data-ttu-id="77f63-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="77f63-113">Prerequisites</span></span>

<span data-ttu-id="77f63-114">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="77f63-114">To complete this tutorial:</span></span>

- <span data-ttu-id="77f63-115">Deploy a .NET application to Azure and [enable the Application Insights SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="77f63-115">Deploy a .NET application to Azure and [enable the Application Insights SDK](app-insights-asp-net.md).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="77f63-116">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="77f63-116">Log in to Azure</span></span>
<span data-ttu-id="77f63-117">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77f63-117">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>

## <a name="create-a-new-dashboard"></a><span data-ttu-id="77f63-118">Create a new dashboard</span><span class="sxs-lookup"><span data-stu-id="77f63-118">Create a new dashboard</span></span>
<span data-ttu-id="77f63-119">A single dashboard can contain resources from multiple applications, resource groups, and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="77f63-119">A single dashboard can contain resources from multiple applications, resource groups, and subscriptions.</span></span>  <span data-ttu-id="77f63-120">Start the tutorial by creating a new dashboard for your application.</span><span class="sxs-lookup"><span data-stu-id="77f63-120">Start the tutorial by creating a new dashboard for your application.</span></span>  

2.  <span data-ttu-id="77f63-121">On the main screen of the portal, select **New dashboard**.</span><span class="sxs-lookup"><span data-stu-id="77f63-121">On the main screen of the portal, select **New dashboard**.</span></span>

    ![New dashboard](media/app-insights-tutorial-dashboards/new-dashboard.png)

3. <span data-ttu-id="77f63-123">Type a name for the dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-123">Type a name for the dashboard.</span></span>
4. <span data-ttu-id="77f63-124">Have a look at the **Tile Gallery** for a variety of tiles that you can add to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-124">Have a look at the **Tile Gallery** for a variety of tiles that you can add to your dashboard.</span></span>  <span data-ttu-id="77f63-125">In addition to adding tiles from the gallery you can pin charts and other views directly from Application Insights to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-125">In addition to adding tiles from the gallery you can pin charts and other views directly from Application Insights to the dashboard.</span></span>
5. <span data-ttu-id="77f63-126">Locate the **Markdown** tile and drag it on to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-126">Locate the **Markdown** tile and drag it on to your dashboard.</span></span>  <span data-ttu-id="77f63-127">This tile allows you to add text formatted in markdown which is ideal for adding descriptive text to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-127">This tile allows you to add text formatted in markdown which is ideal for adding descriptive text to your dashboard.</span></span>
6. <span data-ttu-id="77f63-128">Add text to the tile's properties and resize it on the dashboard canvas.</span><span class="sxs-lookup"><span data-stu-id="77f63-128">Add text to the tile's properties and resize it on the dashboard canvas.</span></span>
    
    ![Edit markdown tile](media/app-insights-tutorial-dashboards/edit-markdown.png)

6. <span data-ttu-id="77f63-130">Click **Done customizing** at the top of the screen to exit tile customization mode and then **Publish changes** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="77f63-130">Click **Done customizing** at the top of the screen to exit tile customization mode and then **Publish changes** to save your changes.</span></span>

    ![Dashboard with markdown tile](media/app-insights-tutorial-dashboards/dashboard-01.png)


## <a name="add-health-overview"></a><span data-ttu-id="77f63-132">Add health overview</span><span class="sxs-lookup"><span data-stu-id="77f63-132">Add health overview</span></span>
<span data-ttu-id="77f63-133">A dashboard with just static text isn't very interesting, so now add a tile from Application Insights to show information about your application.</span><span class="sxs-lookup"><span data-stu-id="77f63-133">A dashboard with just static text isn't very interesting, so now add a tile from Application Insights to show information about your application.</span></span>  <span data-ttu-id="77f63-134">You can add Application Insights tiles from the Tile Gallery, or you can pin them directly from Application Insights screens.</span><span class="sxs-lookup"><span data-stu-id="77f63-134">You can add Application Insights tiles from the Tile Gallery, or you can pin them directly from Application Insights screens.</span></span>  <span data-ttu-id="77f63-135">This allows you to configure charts and views that you're already familiar with before pinning them to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-135">This allows you to configure charts and views that you're already familiar with before pinning them to your dashboard.</span></span>  <span data-ttu-id="77f63-136">Start by adding the standard health overview for your application.</span><span class="sxs-lookup"><span data-stu-id="77f63-136">Start by adding the standard health overview for your application.</span></span>  <span data-ttu-id="77f63-137">This requires no configuration and allows minimal customization in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-137">This requires no configuration and allows minimal customization in the dashboard.</span></span>


1. <span data-ttu-id="77f63-138">Select **Application Insights** in the Azure menu and then select your application.</span><span class="sxs-lookup"><span data-stu-id="77f63-138">Select **Application Insights** in the Azure menu and then select your application.</span></span>
2. <span data-ttu-id="77f63-139">In the **Overview timeline**, select the context menu and click **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="77f63-139">In the **Overview timeline**, select the context menu and click **Pin to dashboard**.</span></span>  <span data-ttu-id="77f63-140">This adds the tile to the last dashboard that you were viewing.</span><span class="sxs-lookup"><span data-stu-id="77f63-140">This adds the tile to the last dashboard that you were viewing.</span></span>  

    ![Pin Overview timeline](media/app-insights-tutorial-dashboards/pin-overview-timeline.png)
 
3. <span data-ttu-id="77f63-142">At the top of the screen, click **View dashboard** to return to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-142">At the top of the screen, click **View dashboard** to return to your dashboard.</span></span>
4. <span data-ttu-id="77f63-143">The Overview timeline is now added to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-143">The Overview timeline is now added to your dashboard.</span></span>  <span data-ttu-id="77f63-144">Click and drag it into position and then click **Done customizing** and **Publish changes**.</span><span class="sxs-lookup"><span data-stu-id="77f63-144">Click and drag it into position and then click **Done customizing** and **Publish changes**.</span></span>  <span data-ttu-id="77f63-145">Your dashboard now has a tile with some useful information.</span><span class="sxs-lookup"><span data-stu-id="77f63-145">Your dashboard now has a tile with some useful information.</span></span>

    ![Dashboard with Overview timeline](media/app-insights-tutorial-dashboards/dashboard-02.png)



## <a name="add-custom-metric-chart"></a><span data-ttu-id="77f63-147">Add custom metric chart</span><span class="sxs-lookup"><span data-stu-id="77f63-147">Add custom metric chart</span></span>
<span data-ttu-id="77f63-148">The **Metrics** panel allows you to graph a metric collected by Application Insights over time with optional filters and grouping.</span><span class="sxs-lookup"><span data-stu-id="77f63-148">The **Metrics** panel allows you to graph a metric collected by Application Insights over time with optional filters and grouping.</span></span>  <span data-ttu-id="77f63-149">Like everything else in Application Insights, you can add this chart to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-149">Like everything else in Application Insights, you can add this chart to the dashboard.</span></span>  <span data-ttu-id="77f63-150">This does require you to do a little customization first.</span><span class="sxs-lookup"><span data-stu-id="77f63-150">This does require you to do a little customization first.</span></span>

1. <span data-ttu-id="77f63-151">Select **Application Insights** in the Azure menu and then select your application.</span><span class="sxs-lookup"><span data-stu-id="77f63-151">Select **Application Insights** in the Azure menu and then select your application.</span></span>
1. <span data-ttu-id="77f63-152">Select **Metrics**.</span><span class="sxs-lookup"><span data-stu-id="77f63-152">Select **Metrics**.</span></span>  
2. <span data-ttu-id="77f63-153">An empty chart has already been created, and you're prompted to add a metric.</span><span class="sxs-lookup"><span data-stu-id="77f63-153">An empty chart has already been created, and you're prompted to add a metric.</span></span>  <span data-ttu-id="77f63-154">Add a metric to the chart and optionally add a filter and a grouping.</span><span class="sxs-lookup"><span data-stu-id="77f63-154">Add a metric to the chart and optionally add a filter and a grouping.</span></span>  <span data-ttu-id="77f63-155">The example below shows the number of server requests grouped by success.</span><span class="sxs-lookup"><span data-stu-id="77f63-155">The example below shows the number of server requests grouped by success.</span></span>  <span data-ttu-id="77f63-156">This gives a running view of successful and unsuccessful requests.</span><span class="sxs-lookup"><span data-stu-id="77f63-156">This gives a running view of successful and unsuccessful requests.</span></span>

    ![Add metric](media/app-insights-tutorial-dashboards/metrics-chart.png)

4. <span data-ttu-id="77f63-158">Select the context menu for the chart and select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="77f63-158">Select the context menu for the chart and select **Pin to dashboard**.</span></span>  <span data-ttu-id="77f63-159">This adds the view to the last dashboard that you were working with.</span><span class="sxs-lookup"><span data-stu-id="77f63-159">This adds the view to the last dashboard that you were working with.</span></span>

    ![Pin metric chart](media/app-insights-tutorial-dashboards/pin-metrics-chart.png)

3. <span data-ttu-id="77f63-161">At the top of the screen, click **View dashboard** to return to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-161">At the top of the screen, click **View dashboard** to return to your dashboard.</span></span>

4. <span data-ttu-id="77f63-162">The Timeline Metrics Chart is now added to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-162">The Timeline Metrics Chart is now added to your dashboard.</span></span> <span data-ttu-id="77f63-163">Click and drag it into position and then click **Done customizing** and then **Publish changes**.</span><span class="sxs-lookup"><span data-stu-id="77f63-163">Click and drag it into position and then click **Done customizing** and then **Publish changes**.</span></span> 

    ![Dashboard with metrics](media/app-insights-tutorial-dashboards/dashboard-03.png)


## <a name="metrics-explorer"></a><span data-ttu-id="77f63-165">Metrics Explorer</span><span class="sxs-lookup"><span data-stu-id="77f63-165">Metrics Explorer</span></span>
<span data-ttu-id="77f63-166">**Metrics Explorer** is similar to Metrics although it allows significantly more customization when added to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-166">**Metrics Explorer** is similar to Metrics although it allows significantly more customization when added to the dashboard.</span></span>  <span data-ttu-id="77f63-167">Which you use to graph your metrics depends on your particular preference and requirements.</span><span class="sxs-lookup"><span data-stu-id="77f63-167">Which you use to graph your metrics depends on your particular preference and requirements.</span></span>

1. <span data-ttu-id="77f63-168">Select **Application Insights** in the Azure menu and then select your application.</span><span class="sxs-lookup"><span data-stu-id="77f63-168">Select **Application Insights** in the Azure menu and then select your application.</span></span>
1. <span data-ttu-id="77f63-169">Select **Metrics Explorer**.</span><span class="sxs-lookup"><span data-stu-id="77f63-169">Select **Metrics Explorer**.</span></span> 
2. <span data-ttu-id="77f63-170">Click to edit the chart and select one or more metrics and optionally a detailed configuration.</span><span class="sxs-lookup"><span data-stu-id="77f63-170">Click to edit the chart and select one or more metrics and optionally a detailed configuration.</span></span>  <span data-ttu-id="77f63-171">The example displays a line chart tracking average page response time.</span><span class="sxs-lookup"><span data-stu-id="77f63-171">The example displays a line chart tracking average page response time.</span></span>
3. <span data-ttu-id="77f63-172">Click the pin icon in the top right to add the chart to your dashboard and then drag it into position.</span><span class="sxs-lookup"><span data-stu-id="77f63-172">Click the pin icon in the top right to add the chart to your dashboard and then drag it into position.</span></span>

    ![Metrics Explorer](media/app-insights-tutorial-dashboards/metrics-explorer.png)

4. <span data-ttu-id="77f63-174">The Metrics Explorer tile allows more customization once it's added to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-174">The Metrics Explorer tile allows more customization once it's added to the dashboard.</span></span>  <span data-ttu-id="77f63-175">Right click the tile and select **Edit title** to add a custom title.</span><span class="sxs-lookup"><span data-stu-id="77f63-175">Right click the tile and select **Edit title** to add a custom title.</span></span>  <span data-ttu-id="77f63-176">Go ahead and make other customizations if you want.</span><span class="sxs-lookup"><span data-stu-id="77f63-176">Go ahead and make other customizations if you want.</span></span>

    ![Dashboard with metrics explorer](media/app-insights-tutorial-dashboards/dashboard-04a.png)

5. <span data-ttu-id="77f63-178">You now have the Metrics Explorer chart added to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-178">You now have the Metrics Explorer chart added to your dashboard.</span></span>

    ![Dashboard with metrics explorer](media/app-insights-tutorial-dashboards/dashboard-04.png)

## <a name="add-analytics-query"></a><span data-ttu-id="77f63-180">Add Analytics query</span><span class="sxs-lookup"><span data-stu-id="77f63-180">Add Analytics query</span></span>
<span data-ttu-id="77f63-181">Azure Application Insights Analytics provides a rich query language that allows you to analyze all of the data collected Application Insights.</span><span class="sxs-lookup"><span data-stu-id="77f63-181">Azure Application Insights Analytics provides a rich query language that allows you to analyze all of the data collected Application Insights.</span></span>  <span data-ttu-id="77f63-182">Just like charts and other views, you can add the output of an Analytics query to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-182">Just like charts and other views, you can add the output of an Analytics query to your dashboard.</span></span>   

<span data-ttu-id="77f63-183">Since Azure Applications Insights Analytics is a separate service, you need to share your dashboard for it to include an Analytics query.</span><span class="sxs-lookup"><span data-stu-id="77f63-183">Since Azure Applications Insights Analytics is a separate service, you need to share your dashboard for it to include an Analytics query.</span></span>  <span data-ttu-id="77f63-184">When you share an Azure dashboard, you publish it as an Azure resource which can make it available to other users and resources.</span><span class="sxs-lookup"><span data-stu-id="77f63-184">When you share an Azure dashboard, you publish it as an Azure resource which can make it available to other users and resources.</span></span>  

1. <span data-ttu-id="77f63-185">At the top of the dashboard screen, click **Share**.</span><span class="sxs-lookup"><span data-stu-id="77f63-185">At the top of the dashboard screen, click **Share**.</span></span>

    ![Publish dashboard](media/app-insights-tutorial-dashboards/publish-dashboard.png)

2. <span data-ttu-id="77f63-187">Keep the **Dashboard name** the same and select the **Subscription Name** to share the dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-187">Keep the **Dashboard name** the same and select the **Subscription Name** to share the dashboard.</span></span>  <span data-ttu-id="77f63-188">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="77f63-188">Click **Publish**.</span></span>  <span data-ttu-id="77f63-189">The dashboard is now available to other services and subscriptions.</span><span class="sxs-lookup"><span data-stu-id="77f63-189">The dashboard is now available to other services and subscriptions.</span></span>  <span data-ttu-id="77f63-190">You can optionally define specific users who should have access to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-190">You can optionally define specific users who should have access to the dashboard.</span></span>
1. <span data-ttu-id="77f63-191">Select **Application Insights** in the Azure menu and then select your application.</span><span class="sxs-lookup"><span data-stu-id="77f63-191">Select **Application Insights** in the Azure menu and then select your application.</span></span>
2. <span data-ttu-id="77f63-192">Click **Analytics** at the top of the screen to open the Analytics portal.</span><span class="sxs-lookup"><span data-stu-id="77f63-192">Click **Analytics** at the top of the screen to open the Analytics portal.</span></span>

    ![Start Analytics](media/app-insights-tutorial-dashboards/start-analytics.png)

3. <span data-ttu-id="77f63-194">Type the following query, which returns the top 10 most requested pages and their request count:</span><span class="sxs-lookup"><span data-stu-id="77f63-194">Type the following query, which returns the top 10 most requested pages and their request count:</span></span>

    ```
    requests
    | summarize count() by name
    | sort by count_ desc
    | take 10 
    ```

4. <span data-ttu-id="77f63-195">Click **Go** to validate the results of the query.</span><span class="sxs-lookup"><span data-stu-id="77f63-195">Click **Go** to validate the results of the query.</span></span>
5. <span data-ttu-id="77f63-196">Click the pin icon and select the name of your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-196">Click the pin icon and select the name of your dashboard.</span></span>  <span data-ttu-id="77f63-197">The reason that this option has you select a dashboard unlike the previous steps where the last dashboard was used is because the Analytics console is a separate service and needs to select from all available shared dashboards.</span><span class="sxs-lookup"><span data-stu-id="77f63-197">The reason that this option has you select a dashboard unlike the previous steps where the last dashboard was used is because the Analytics console is a separate service and needs to select from all available shared dashboards.</span></span>

    ![Pin Analytics query](media/app-insights-tutorial-dashboards/analytics-pin.png)

5. <span data-ttu-id="77f63-199">Before you go back to the dashboard, add another query, but this time render it as a chart so you see the different ways to visualize an Analytics query in a dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-199">Before you go back to the dashboard, add another query, but this time render it as a chart so you see the different ways to visualize an Analytics query in a dashboard.</span></span>  <span data-ttu-id="77f63-200">Start with the following query that summarizes the top 10 operations with the most exceptions.</span><span class="sxs-lookup"><span data-stu-id="77f63-200">Start with the following query that summarizes the top 10 operations with the most exceptions.</span></span>

    ```
    exceptions
    | summarize count() by operation_Name
    | sort by count_ desc
    | take 10 
    ```

6. <span data-ttu-id="77f63-201">Select **Chart** and then change to a **Doughnut** to visualize the output.</span><span class="sxs-lookup"><span data-stu-id="77f63-201">Select **Chart** and then change to a **Doughnut** to visualize the output.</span></span>

    ![Analytics chart](media/app-insights-tutorial-dashboards/analytics-chart.png)

6. <span data-ttu-id="77f63-203">Click the pin icon to pin the chart to your dashboard and this time select the link to return to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="77f63-203">Click the pin icon to pin the chart to your dashboard and this time select the link to return to your dashboard.</span></span>
4. <span data-ttu-id="77f63-204">The results of the queries are now added to your dashboard in the format that you selected.</span><span class="sxs-lookup"><span data-stu-id="77f63-204">The results of the queries are now added to your dashboard in the format that you selected.</span></span>  <span data-ttu-id="77f63-205">Click and drag each into position and then click **Done editing**.</span><span class="sxs-lookup"><span data-stu-id="77f63-205">Click and drag each into position and then click **Done editing**.</span></span>
5. <span data-ttu-id="77f63-206">Right click each of the tiles and select **Edit Title** to give them a descriptive title.</span><span class="sxs-lookup"><span data-stu-id="77f63-206">Right click each of the tiles and select **Edit Title** to give them a descriptive title.</span></span>

    ![Dashboard with Analytics](media/app-insights-tutorial-dashboards/dashboard-05.png)

5. <span data-ttu-id="77f63-208">Click **Publish changes** to commit the changes to your dashboard that now includes a variety of charts and visualizations from Application Insights.</span><span class="sxs-lookup"><span data-stu-id="77f63-208">Click **Publish changes** to commit the changes to your dashboard that now includes a variety of charts and visualizations from Application Insights.</span></span>


## <a name="next-steps"></a><span data-ttu-id="77f63-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="77f63-209">Next steps</span></span>
<span data-ttu-id="77f63-210">Now that you've learned how to create custom dashboards, have a look at the rest of the Application Insights documentation including a case study.</span><span class="sxs-lookup"><span data-stu-id="77f63-210">Now that you've learned how to create custom dashboards, have a look at the rest of the Application Insights documentation including a case study.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="77f63-211">Deep diagnostics</span><span class="sxs-lookup"><span data-stu-id="77f63-211">Deep diagnostics</span></span>](app-insights-devops.md)
