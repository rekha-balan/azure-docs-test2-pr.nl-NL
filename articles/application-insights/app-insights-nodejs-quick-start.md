---
title: Quickstart with Azure Application Insights | Microsoft Docs
description: Provides instructions to quickly setup a Node.js Web App for monitoring with Application Insights
services: application-insights
keywords: ''
author: mrbullwinkle
ms.author: mbullwin
ms.date: 07/11/2018
ms.service: application-insights
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
ms.openlocfilehash: 8bc725a5d9e3e9cdf82a01693aed83bff1f16c04
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857065"
---
# <a name="start-monitoring-your-nodejs-web-application"></a><span data-ttu-id="9c2ce-103">Start Monitoring Your Node.js Web Application</span><span class="sxs-lookup"><span data-stu-id="9c2ce-103">Start Monitoring Your Node.js Web Application</span></span>

<span data-ttu-id="9c2ce-104">With Azure Application Insights, you can easily monitor your web application for availability, performance, and usage.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-104">With Azure Application Insights, you can easily monitor your web application for availability, performance, and usage.</span></span> <span data-ttu-id="9c2ce-105">You can also quickly identify and diagnose errors in your application without waiting for a user to report them.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-105">You can also quickly identify and diagnose errors in your application without waiting for a user to report them.</span></span> <span data-ttu-id="9c2ce-106">With the version 0.20 SDK release onward, you can monitor common third-party packages, including MongoDB, MySQL, and Redis.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-106">With the version 0.20 SDK release onward, you can monitor common third-party packages, including MongoDB, MySQL, and Redis.</span></span>

<span data-ttu-id="9c2ce-107">This quickstart guides you through adding the version 0.22 Application Insights SDK for Node.js to an existing Node.js web application.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-107">This quickstart guides you through adding the version 0.22 Application Insights SDK for Node.js to an existing Node.js web application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c2ce-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9c2ce-108">Prerequisites</span></span>

<span data-ttu-id="9c2ce-109">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="9c2ce-109">To complete this quickstart:</span></span>

- <span data-ttu-id="9c2ce-110">You need an Azure Subscription and an existing Node.js web application.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-110">You need an Azure Subscription and an existing Node.js web application.</span></span>

<span data-ttu-id="9c2ce-111">If you don't have a Node.js web application, you can create one by following the [Create a Node.js web app quickstart](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-nodejs).</span><span class="sxs-lookup"><span data-stu-id="9c2ce-111">If you don't have a Node.js web application, you can create one by following the [Create a Node.js web app quickstart](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-nodejs).</span></span>

<span data-ttu-id="9c2ce-112">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-112">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="9c2ce-113">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9c2ce-113">Log in to the Azure portal</span></span>

<span data-ttu-id="9c2ce-114">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c2ce-114">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="enable-application-insights"></a><span data-ttu-id="9c2ce-115">Enable Application Insights</span><span class="sxs-lookup"><span data-stu-id="9c2ce-115">Enable Application Insights</span></span>

<span data-ttu-id="9c2ce-116">Application Insights can gather telemetry data from any internet-connected application, regardless of whether it's running on-premises or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-116">Application Insights can gather telemetry data from any internet-connected application, regardless of whether it's running on-premises or in the cloud.</span></span> <span data-ttu-id="9c2ce-117">Use the following steps to start viewing this data.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-117">Use the following steps to start viewing this data.</span></span>

1. <span data-ttu-id="9c2ce-118">Select **Create a resource** > **Monitoring + Management** > **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-118">Select **Create a resource** > **Monitoring + Management** > **Application Insights**.</span></span>

   ![Adding Application Insights Resource](./media/app-insights-nodejs-quick-start/001-u.png)

   <span data-ttu-id="9c2ce-120">A configuration box appears; use the following table to fill out the input fields.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-120">A configuration box appears; use the following table to fill out the input fields.</span></span>

    | <span data-ttu-id="9c2ce-121">Settings</span><span class="sxs-lookup"><span data-stu-id="9c2ce-121">Settings</span></span>        | <span data-ttu-id="9c2ce-122">Value</span><span class="sxs-lookup"><span data-stu-id="9c2ce-122">Value</span></span>           | <span data-ttu-id="9c2ce-123">Description</span><span class="sxs-lookup"><span data-stu-id="9c2ce-123">Description</span></span>  |
   | ------------- |:-------------|:-----|
   | <span data-ttu-id="9c2ce-124">**Name**</span><span class="sxs-lookup"><span data-stu-id="9c2ce-124">**Name**</span></span>      | <span data-ttu-id="9c2ce-125">Globally Unique Value</span><span class="sxs-lookup"><span data-stu-id="9c2ce-125">Globally Unique Value</span></span> | <span data-ttu-id="9c2ce-126">Name that identifies the app you are monitoring</span><span class="sxs-lookup"><span data-stu-id="9c2ce-126">Name that identifies the app you are monitoring</span></span> |
   | <span data-ttu-id="9c2ce-127">**Application Type**</span><span class="sxs-lookup"><span data-stu-id="9c2ce-127">**Application Type**</span></span> | <span data-ttu-id="9c2ce-128">Node.js Application</span><span class="sxs-lookup"><span data-stu-id="9c2ce-128">Node.js Application</span></span> | <span data-ttu-id="9c2ce-129">Type of app you are monitoring</span><span class="sxs-lookup"><span data-stu-id="9c2ce-129">Type of app you are monitoring</span></span> |
   | <span data-ttu-id="9c2ce-130">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="9c2ce-130">**Resource Group**</span></span>     | <span data-ttu-id="9c2ce-131">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9c2ce-131">myResourceGroup</span></span>      | <span data-ttu-id="9c2ce-132">Name for the new resource group to host App Insights data</span><span class="sxs-lookup"><span data-stu-id="9c2ce-132">Name for the new resource group to host App Insights data</span></span> |
   | <span data-ttu-id="9c2ce-133">**Location**</span><span class="sxs-lookup"><span data-stu-id="9c2ce-133">**Location**</span></span> | <span data-ttu-id="9c2ce-134">East US</span><span class="sxs-lookup"><span data-stu-id="9c2ce-134">East US</span></span> | <span data-ttu-id="9c2ce-135">Choose a location near you, or near where your app is hosted</span><span class="sxs-lookup"><span data-stu-id="9c2ce-135">Choose a location near you, or near where your app is hosted</span></span> |

2. <span data-ttu-id="9c2ce-136">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-136">Click **Create**.</span></span>

## <a name="configure-app-insights-sdk"></a><span data-ttu-id="9c2ce-137">Configure App Insights SDK</span><span class="sxs-lookup"><span data-stu-id="9c2ce-137">Configure App Insights SDK</span></span>

1. <span data-ttu-id="9c2ce-138">Select **Overview** > **Essentials** > Copy your application's **Instrumentation Key**.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-138">Select **Overview** > **Essentials** > Copy your application's **Instrumentation Key**.</span></span>

   ![New App Insights resource form](./media/app-insights-nodejs-quick-start/instrumentation-key-001.png)

2. <span data-ttu-id="9c2ce-140">Add the Application Insights SDK for Node.js to your application.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-140">Add the Application Insights SDK for Node.js to your application.</span></span> <span data-ttu-id="9c2ce-141">From your app's root folder run:</span><span class="sxs-lookup"><span data-stu-id="9c2ce-141">From your app's root folder run:</span></span>

   ```bash
   npm install applicationinsights --save
   ```

3. <span data-ttu-id="9c2ce-142">Edit your app's first .js file and add the two lines below to the topmost part of your script.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-142">Edit your app's first .js file and add the two lines below to the topmost part of your script.</span></span> <span data-ttu-id="9c2ce-143">If you are using the [Node.js quickstart app](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-nodejs), you would modify the index.js file.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-143">If you are using the [Node.js quickstart app](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-nodejs), you would modify the index.js file.</span></span> <span data-ttu-id="9c2ce-144">Replace &lt;instrumentation_key&gt; with your application's instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-144">Replace &lt;instrumentation_key&gt; with your application's instrumentation key.</span></span> 

   ```JavaScript
   const appInsights = require('applicationinsights');
   appInsights.setup('<instrumentation_key>').start();
   ```

4. <span data-ttu-id="9c2ce-145">Restart your app.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-145">Restart your app.</span></span>

> [!NOTE]
> <span data-ttu-id="9c2ce-146">It takes 3-5 minutes before data begins appearing in the portal.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-146">It takes 3-5 minutes before data begins appearing in the portal.</span></span> <span data-ttu-id="9c2ce-147">If this app is a low-traffic test app, keep in mind that most metrics are only captured when there are active requests or operations occurring.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-147">If this app is a low-traffic test app, keep in mind that most metrics are only captured when there are active requests or operations occurring.</span></span>

## <a name="start-monitoring-in-the-azure-portal"></a><span data-ttu-id="9c2ce-148">Start monitoring in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9c2ce-148">Start monitoring in the Azure portal</span></span>

1. <span data-ttu-id="9c2ce-149">You can now reopen the Application Insights **Overview** page in the Azure portal, where you retrieved your instrumentation key, to view details about your currently running application.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-149">You can now reopen the Application Insights **Overview** page in the Azure portal, where you retrieved your instrumentation key, to view details about your currently running application.</span></span>

   ![Application Insights Overview Menu](./media/app-insights-nodejs-quick-start/overview-001.png)

2. <span data-ttu-id="9c2ce-151">Click **App map** for a visual layout of the dependency relationships between your application components.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-151">Click **App map** for a visual layout of the dependency relationships between your application components.</span></span> <span data-ttu-id="9c2ce-152">Each component shows KPIs such as load, performance, failures, and alerts.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-152">Each component shows KPIs such as load, performance, failures, and alerts.</span></span>

   ![Application Map](./media/app-insights-nodejs-quick-start/application-map.png)

3. <span data-ttu-id="9c2ce-154">Click on the **App Analytics** icon ![Application Map icon](./media/app-insights-nodejs-quick-start/006.png).</span><span class="sxs-lookup"><span data-stu-id="9c2ce-154">Click on the **App Analytics** icon ![Application Map icon](./media/app-insights-nodejs-quick-start/006.png).</span></span>  <span data-ttu-id="9c2ce-155">This opens **Application Insights Analytics**, which provides a rich query language for analyzing all data collected by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-155">This opens **Application Insights Analytics**, which provides a rich query language for analyzing all data collected by Application Insights.</span></span> <span data-ttu-id="9c2ce-156">In this case, a query is generated for you that renders the request count as a chart.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-156">In this case, a query is generated for you that renders the request count as a chart.</span></span> <span data-ttu-id="9c2ce-157">You can write your own queries to analyze other data.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-157">You can write your own queries to analyze other data.</span></span>

   ![Analytics graph of user requests over a period of time](./media/app-insights-nodejs-quick-start/007-Black.png)

4. <span data-ttu-id="9c2ce-159">Return to the **Overview** page and examine the KPI graphs.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-159">Return to the **Overview** page and examine the KPI graphs.</span></span>  <span data-ttu-id="9c2ce-160">This dashboard provides statistics about your application health, including the number of incoming requests, the duration of those requests, and any failures that occur.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-160">This dashboard provides statistics about your application health, including the number of incoming requests, the duration of those requests, and any failures that occur.</span></span> 

   ![Health Overview timeline graphs](./media/app-insights-nodejs-quick-start/overview-perf.png)

   <span data-ttu-id="9c2ce-162">To enable the **Page View Load Time** chart to populate with **client-side telemetry** data, add this script to each page that you want to track:</span><span class="sxs-lookup"><span data-stu-id="9c2ce-162">To enable the **Page View Load Time** chart to populate with **client-side telemetry** data, add this script to each page that you want to track:</span></span>

   ```HTML
   <!-- 
   To collect user behavior analytics tools about your application, 
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

5. <span data-ttu-id="9c2ce-163">Click on **Browser** from under the **Investigate** header.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-163">Click on **Browser** from under the **Investigate** header.</span></span> <span data-ttu-id="9c2ce-164">Here you find metrics related to the performance of your app's pages.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-164">Here you find metrics related to the performance of your app's pages.</span></span> <span data-ttu-id="9c2ce-165">You can click **Add new chart** to create additional custom views or select **Edit** to modify the existing chart types, height, color palette, groupings, and metrics.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-165">You can click **Add new chart** to create additional custom views or select **Edit** to modify the existing chart types, height, color palette, groupings, and metrics.</span></span>

   ![Server metrics graph](./media/app-insights-nodejs-quick-start/009-Black.png)

<span data-ttu-id="9c2ce-167">To learn more about monitoring Node.js, check out the [additional App Insights Node.js documentation](app-insights-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9c2ce-167">To learn more about monitoring Node.js, check out the [additional App Insights Node.js documentation](app-insights-nodejs.md).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9c2ce-168">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="9c2ce-168">Clean up resources</span></span>

<span data-ttu-id="9c2ce-169">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quick start.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-169">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="9c2ce-170">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-170">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>

1. <span data-ttu-id="9c2ce-171">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-171">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span>
2. <span data-ttu-id="9c2ce-172">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="9c2ce-172">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c2ce-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c2ce-173">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9c2ce-174">Find and diagnose performance problems</span><span class="sxs-lookup"><span data-stu-id="9c2ce-174">Find and diagnose performance problems</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)
