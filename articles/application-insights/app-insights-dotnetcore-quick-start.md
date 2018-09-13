---
title: Quickstart with Azure Application Insights | Microsoft Docs
description: Provides instructions to quickly setup a ASP.NET Core Web App for monitoring with Application Insights
services: application-insights
keywords: ''
author: mrbullwinkle
ms.author: mbullwin
ms.date: 07/11/2018
ms.service: application-insights
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
ms.openlocfilehash: 008e61841611f36c440bb4896ae5a85d0bf4d874
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968664"
---
# <a name="start-monitoring-your-aspnet-core-web-application"></a><span data-ttu-id="db1b9-103">Start Monitoring Your ASP.NET Core Web Application</span><span class="sxs-lookup"><span data-stu-id="db1b9-103">Start Monitoring Your ASP.NET Core Web Application</span></span>

<span data-ttu-id="db1b9-104">With Azure Application Insights, you can easily monitor your web application for availability, performance, and usage.</span><span class="sxs-lookup"><span data-stu-id="db1b9-104">With Azure Application Insights, you can easily monitor your web application for availability, performance, and usage.</span></span> <span data-ttu-id="db1b9-105">You can also quickly identify and diagnose errors in your application without waiting for a user to report them.</span><span class="sxs-lookup"><span data-stu-id="db1b9-105">You can also quickly identify and diagnose errors in your application without waiting for a user to report them.</span></span> 

<span data-ttu-id="db1b9-106">This quickstart guides you through adding the Application Insights SDK to an existing ASP.Net Core web application.</span><span class="sxs-lookup"><span data-stu-id="db1b9-106">This quickstart guides you through adding the Application Insights SDK to an existing ASP.Net Core web application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="db1b9-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="db1b9-107">Prerequisites</span></span>

<span data-ttu-id="db1b9-108">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="db1b9-108">To complete this quickstart:</span></span>

- <span data-ttu-id="db1b9-109">[Install Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span><span class="sxs-lookup"><span data-stu-id="db1b9-109">[Install Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
  - <span data-ttu-id="db1b9-110">ASP.NET and web development</span><span class="sxs-lookup"><span data-stu-id="db1b9-110">ASP.NET and web development</span></span>
  - <span data-ttu-id="db1b9-111">Azure development</span><span class="sxs-lookup"><span data-stu-id="db1b9-111">Azure development</span></span>
- [<span data-ttu-id="db1b9-112">Install .NET Core 2.0 SDK</span><span class="sxs-lookup"><span data-stu-id="db1b9-112">Install .NET Core 2.0 SDK</span></span>](https://www.microsoft.com/net/core)
- <span data-ttu-id="db1b9-113">You will need an Azure subscription and an existing .NET Core web application.</span><span class="sxs-lookup"><span data-stu-id="db1b9-113">You will need an Azure subscription and an existing .NET Core web application.</span></span>

<span data-ttu-id="db1b9-114">If you don't have a ASP.NET Core web application, you can use our step-by-step guide to [create a ASP.NET Core app and add Application Insights.](app-insights-asp-net-core.md)</span><span class="sxs-lookup"><span data-stu-id="db1b9-114">If you don't have a ASP.NET Core web application, you can use our step-by-step guide to [create a ASP.NET Core app and add Application Insights.](app-insights-asp-net-core.md)</span></span>

<span data-ttu-id="db1b9-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="db1b9-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="db1b9-116">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="db1b9-116">Log in to the Azure portal</span></span>

<span data-ttu-id="db1b9-117">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="db1b9-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="enable-application-insights"></a><span data-ttu-id="db1b9-118">Enable Application Insights</span><span class="sxs-lookup"><span data-stu-id="db1b9-118">Enable Application Insights</span></span>

<span data-ttu-id="db1b9-119">Application Insights can gather telemetry data from any internet-connected application, regardless of whether it's running on-premises or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="db1b9-119">Application Insights can gather telemetry data from any internet-connected application, regardless of whether it's running on-premises or in the cloud.</span></span> <span data-ttu-id="db1b9-120">Use the following steps to start viewing this data.</span><span class="sxs-lookup"><span data-stu-id="db1b9-120">Use the following steps to start viewing this data.</span></span>

1. <span data-ttu-id="db1b9-121">Select **Create a resource** > **Monitoring + Management** > **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="db1b9-121">Select **Create a resource** > **Monitoring + Management** > **Application Insights**.</span></span>

   ![Adding Application Insights Resource](./media/app-insights-dotnetcore-quick-start/0001-dc.png)

    <span data-ttu-id="db1b9-123">A configuration box appears; use the following table to fill out the input fields.</span><span class="sxs-lookup"><span data-stu-id="db1b9-123">A configuration box appears; use the following table to fill out the input fields.</span></span>

    | <span data-ttu-id="db1b9-124">Settings</span><span class="sxs-lookup"><span data-stu-id="db1b9-124">Settings</span></span>        |  <span data-ttu-id="db1b9-125">Value</span><span class="sxs-lookup"><span data-stu-id="db1b9-125">Value</span></span>           | <span data-ttu-id="db1b9-126">Description</span><span class="sxs-lookup"><span data-stu-id="db1b9-126">Description</span></span>  |
   | ------------- |:-------------|:-----|
   | <span data-ttu-id="db1b9-127">**Name**</span><span class="sxs-lookup"><span data-stu-id="db1b9-127">**Name**</span></span>      | <span data-ttu-id="db1b9-128">Globally Unique Value</span><span class="sxs-lookup"><span data-stu-id="db1b9-128">Globally Unique Value</span></span> | <span data-ttu-id="db1b9-129">Name that identifies the app you are monitoring</span><span class="sxs-lookup"><span data-stu-id="db1b9-129">Name that identifies the app you are monitoring</span></span> |
   | <span data-ttu-id="db1b9-130">**Application Type**</span><span class="sxs-lookup"><span data-stu-id="db1b9-130">**Application Type**</span></span> | <span data-ttu-id="db1b9-131">ASP.NET web application</span><span class="sxs-lookup"><span data-stu-id="db1b9-131">ASP.NET web application</span></span> | <span data-ttu-id="db1b9-132">Type of app you are monitoring</span><span class="sxs-lookup"><span data-stu-id="db1b9-132">Type of app you are monitoring</span></span> |
   | <span data-ttu-id="db1b9-133">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="db1b9-133">**Resource Group**</span></span>     | <span data-ttu-id="db1b9-134">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="db1b9-134">myResourceGroup</span></span>      | <span data-ttu-id="db1b9-135">Name for the new resource group to host App Insights data</span><span class="sxs-lookup"><span data-stu-id="db1b9-135">Name for the new resource group to host App Insights data</span></span> |
   | <span data-ttu-id="db1b9-136">**Location**</span><span class="sxs-lookup"><span data-stu-id="db1b9-136">**Location**</span></span> | <span data-ttu-id="db1b9-137">East US</span><span class="sxs-lookup"><span data-stu-id="db1b9-137">East US</span></span> | <span data-ttu-id="db1b9-138">Choose a location near you, or near where your app is hosted</span><span class="sxs-lookup"><span data-stu-id="db1b9-138">Choose a location near you, or near where your app is hosted</span></span> |

2. <span data-ttu-id="db1b9-139">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="db1b9-139">Click **Create**.</span></span>

## <a name="configure-app-insights-sdk"></a><span data-ttu-id="db1b9-140">Configure App Insights SDK</span><span class="sxs-lookup"><span data-stu-id="db1b9-140">Configure App Insights SDK</span></span>

1. <span data-ttu-id="db1b9-141">Open your ASP.NET Core Web App **project** in Visual Studio > Right-click on the AppName in the **Solution Explorer** > Select **Add** > **Application Insights Telemetry**.</span><span class="sxs-lookup"><span data-stu-id="db1b9-141">Open your ASP.NET Core Web App **project** in Visual Studio > Right-click on the AppName in the **Solution Explorer** > Select **Add** > **Application Insights Telemetry**.</span></span>

    ![Add Application Insights Telemetry](./media/app-insights-dotnetcore-quick-start/0001.png)

2. <span data-ttu-id="db1b9-143">Click the **Start Free** button > Select the **Existing resource** you created in the Azure portal > Click **Register**.</span><span class="sxs-lookup"><span data-stu-id="db1b9-143">Click the **Start Free** button > Select the **Existing resource** you created in the Azure portal > Click **Register**.</span></span>

3. <span data-ttu-id="db1b9-144">Select **Debug** > **Start without Debugging** (Ctrl+F5) to Launch your app</span><span class="sxs-lookup"><span data-stu-id="db1b9-144">Select **Debug** > **Start without Debugging** (Ctrl+F5) to Launch your app</span></span>

> [!NOTE]
> <span data-ttu-id="db1b9-145">It takes 3-5 minutes before data begins appearing in the portal.</span><span class="sxs-lookup"><span data-stu-id="db1b9-145">It takes 3-5 minutes before data begins appearing in the portal.</span></span> <span data-ttu-id="db1b9-146">If this app is a low-traffic test app, keep in mind that most metrics are only captured when there are active requests or operations.</span><span class="sxs-lookup"><span data-stu-id="db1b9-146">If this app is a low-traffic test app, keep in mind that most metrics are only captured when there are active requests or operations.</span></span>

## <a name="start-monitoring-in-the-azure-portal"></a><span data-ttu-id="db1b9-147">Start monitoring in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="db1b9-147">Start monitoring in the Azure portal</span></span>

1. <span data-ttu-id="db1b9-148">You can now reopen the Application Insights **Overview** page in the Azure portal by selecting **Project** > **Application Insights** > **Open Application Insights Portal**, to view details about your currently running application.</span><span class="sxs-lookup"><span data-stu-id="db1b9-148">You can now reopen the Application Insights **Overview** page in the Azure portal by selecting **Project** > **Application Insights** > **Open Application Insights Portal**, to view details about your currently running application.</span></span>

   ![Application Insights Overview Menu](./media/app-insights-dotnetcore-quick-start/overview-001.png)

2. <span data-ttu-id="db1b9-150">Click **Application map** for a visual layout of the dependency relationships between your application components.</span><span class="sxs-lookup"><span data-stu-id="db1b9-150">Click **Application map** for a visual layout of the dependency relationships between your application components.</span></span> <span data-ttu-id="db1b9-151">Each component shows KPIs such as load, performance, failures, and alerts.</span><span class="sxs-lookup"><span data-stu-id="db1b9-151">Each component shows KPIs such as load, performance, failures, and alerts.</span></span>

   ![Application Map](./media/app-insights-dotnetcore-quick-start/application-map.png)

3. <span data-ttu-id="db1b9-153">Click on the **App Analytics** icon ![Application Map icon](./media/app-insights-dotnetcore-quick-start/006.png).</span><span class="sxs-lookup"><span data-stu-id="db1b9-153">Click on the **App Analytics** icon ![Application Map icon](./media/app-insights-dotnetcore-quick-start/006.png).</span></span>  <span data-ttu-id="db1b9-154">This opens **Application Insights Analytics**, which provides a rich query language for analyzing all data collected by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="db1b9-154">This opens **Application Insights Analytics**, which provides a rich query language for analyzing all data collected by Application Insights.</span></span> <span data-ttu-id="db1b9-155">In this case, a query is generated for you that renders the request count as a chart.</span><span class="sxs-lookup"><span data-stu-id="db1b9-155">In this case, a query is generated for you that renders the request count as a chart.</span></span> <span data-ttu-id="db1b9-156">You can write your own queries to analyze other data.</span><span class="sxs-lookup"><span data-stu-id="db1b9-156">You can write your own queries to analyze other data.</span></span>

   ![Analytics graph of user requests over a period of time](./media/app-insights-dotnetcore-quick-start/0007-dc.png)

4. <span data-ttu-id="db1b9-158">Return to the **Overview** page and examine the KPI Dashobards.</span><span class="sxs-lookup"><span data-stu-id="db1b9-158">Return to the **Overview** page and examine the KPI Dashobards.</span></span>  <span data-ttu-id="db1b9-159">This dashboard provides statistics about your application health, including the number of incoming requests, the duration of those requests, and any failures that occur.</span><span class="sxs-lookup"><span data-stu-id="db1b9-159">This dashboard provides statistics about your application health, including the number of incoming requests, the duration of those requests, and any failures that occur.</span></span> 

   ![Health Overview timeline graphs](./media/app-insights-dotnetcore-quick-start/overview-graphs.png)

   <span data-ttu-id="db1b9-161">To enable the **Page View Load Time** chart to populate with **client-side telemetry** data, add this script to each page that you want to track:</span><span class="sxs-lookup"><span data-stu-id="db1b9-161">To enable the **Page View Load Time** chart to populate with **client-side telemetry** data, add this script to each page that you want to track:</span></span>

   ```HTML
   <!-- 
   To collect user behavior analytics about your application, 
   insert the following script into each page you want to track.
   Place this code immediately before the closing </head> tag,
   and before any other scripts. Your first data will appear 
   automatically in just a few seconds.
   -->
   <script type="text/javascript">
     var appInsights=window.appInsights||function(config){
       function i(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s="AuthenticatedUserContext",h="start",c="stop",l="Track",a=l+"Event",v=l+"Page",y=u.createElement(o),r,f;y.src=config.url||"https://az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(y);try{t.cookie=u.cookie}catch(p){}for(t.queue=[],t.version="1.0",r=["Event","Exception","Metric","PageView","Trace","Dependency"];r.length;)i("track"+r.pop());return i("set"+s),i("clear"+s),i(h+a),i(c+a),i(h+v),i(c+v),i("flush"),config.disableExceptionTracking||(r="onerror",i("_"+r),f=e[r],e[r]=function(config,i,u,e,o){var s=f&&f(config,i,u,e,o);return s!==!0&&t["_"+r](config,i,u,e,o),s}),t
       }({
           instrumentationKey:"<insert instrumentation key>"
       });
       
       window.appInsights=appInsights;
       appInsights.trackPageView();
   </script>
   ```

5. <span data-ttu-id="db1b9-162">Click on **Browser** from under the **Investigate** header.</span><span class="sxs-lookup"><span data-stu-id="db1b9-162">Click on **Browser** from under the **Investigate** header.</span></span> <span data-ttu-id="db1b9-163">Here you find metrics related to the performance of your app's pages .</span><span class="sxs-lookup"><span data-stu-id="db1b9-163">Here you find metrics related to the performance of your app's pages .</span></span> <span data-ttu-id="db1b9-164">You can click **Add new chart** to create additional custom views or select **Edit** to modify the existing chart types, height, color palette, groupings, and metrics.</span><span class="sxs-lookup"><span data-stu-id="db1b9-164">You can click **Add new chart** to create additional custom views or select **Edit** to modify the existing chart types, height, color palette, groupings, and metrics.</span></span>

   ![Server metrics graph](./media/app-insights-dotnetcore-quick-start/009-Black.png)

## <a name="clean-up-resources"></a><span data-ttu-id="db1b9-166">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="db1b9-166">Clean up resources</span></span>

<span data-ttu-id="db1b9-167">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quick start.</span><span class="sxs-lookup"><span data-stu-id="db1b9-167">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="db1b9-168">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="db1b9-168">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>

1. <span data-ttu-id="db1b9-169">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="db1b9-169">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span>
2. <span data-ttu-id="db1b9-170">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="db1b9-170">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db1b9-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="db1b9-171">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db1b9-172">Find and diagnose run-time exceptions</span><span class="sxs-lookup"><span data-stu-id="db1b9-172">Find and diagnose run-time exceptions</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-tutorial-runtime-exceptions)
