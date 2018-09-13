---
title: Quickstart with Azure Application Insights | Microsoft Docs
description: Provides instructions to quickly setup a Java Web App for monitoring with Application Insights
services: application-insights
keywords: ''
author: mrbullwinkle
ms.author: mbullwin
ms.reviewer: lagayhar
ms.date: 07/11/2018
ms.service: application-insights
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
ms.openlocfilehash: b36e4598f5ff20b921c5cd150ae19be233cc2d14
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857088"
---
# <a name="start-monitoring-your-java-web-application"></a><span data-ttu-id="12468-103">Start Monitoring Your Java Web Application</span><span class="sxs-lookup"><span data-stu-id="12468-103">Start Monitoring Your Java Web Application</span></span>

<span data-ttu-id="12468-104">With Azure Application Insights, you can easily monitor your web application for availability, performance, and usage.</span><span class="sxs-lookup"><span data-stu-id="12468-104">With Azure Application Insights, you can easily monitor your web application for availability, performance, and usage.</span></span> <span data-ttu-id="12468-105">You can also quickly identify and diagnose errors in your application without waiting for a user to report them.</span><span class="sxs-lookup"><span data-stu-id="12468-105">You can also quickly identify and diagnose errors in your application without waiting for a user to report them.</span></span> <span data-ttu-id="12468-106">With the Application Insights Java SDK, you can monitor common third-party packages including MongoDB, MySQL, and Redis.</span><span class="sxs-lookup"><span data-stu-id="12468-106">With the Application Insights Java SDK, you can monitor common third-party packages including MongoDB, MySQL, and Redis.</span></span>

<span data-ttu-id="12468-107">This quickstart guides you through adding the Application Insights SDK to an existing Java Dynamic Web Project.</span><span class="sxs-lookup"><span data-stu-id="12468-107">This quickstart guides you through adding the Application Insights SDK to an existing Java Dynamic Web Project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12468-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="12468-108">Prerequisites</span></span>

<span data-ttu-id="12468-109">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="12468-109">To complete this quickstart:</span></span>

- <span data-ttu-id="12468-110">Install JRE 1.7 or 1.8</span><span class="sxs-lookup"><span data-stu-id="12468-110">Install JRE 1.7 or 1.8</span></span>
- <span data-ttu-id="12468-111">Install [Free Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="12468-111">Install [Free Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="12468-112">This quickstart uses Eclipse Oxygen (4.7)</span><span class="sxs-lookup"><span data-stu-id="12468-112">This quickstart uses Eclipse Oxygen (4.7)</span></span>
- <span data-ttu-id="12468-113">You will need an Azure Subscription and an existing Java Dynamic Web Project</span><span class="sxs-lookup"><span data-stu-id="12468-113">You will need an Azure Subscription and an existing Java Dynamic Web Project</span></span>
 
<span data-ttu-id="12468-114">If you don't have a Java Dynamic Web Project, you can create one with the [Create a Java web app quickstart](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-java).</span><span class="sxs-lookup"><span data-stu-id="12468-114">If you don't have a Java Dynamic Web Project, you can create one with the [Create a Java web app quickstart](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-java).</span></span>

<span data-ttu-id="12468-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="12468-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="12468-116">If you prefer the Spring framework try the [configure a Spring Boot initializer app to use Application Insights guide](https://docs.microsoft.com/java/azure/spring-framework/configure-spring-boot-java-applicationinsights)</span><span class="sxs-lookup"><span data-stu-id="12468-116">If you prefer the Spring framework try the [configure a Spring Boot initializer app to use Application Insights guide](https://docs.microsoft.com/java/azure/spring-framework/configure-spring-boot-java-applicationinsights)</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="12468-117">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="12468-117">Log in to the Azure portal</span></span>

<span data-ttu-id="12468-118">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="12468-118">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="enable-application-insights"></a><span data-ttu-id="12468-119">Enable Application Insights</span><span class="sxs-lookup"><span data-stu-id="12468-119">Enable Application Insights</span></span>

<span data-ttu-id="12468-120">Application Insights can gather telemetry data from any internet-connected application, regardless of whether it's running on-premises or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="12468-120">Application Insights can gather telemetry data from any internet-connected application, regardless of whether it's running on-premises or in the cloud.</span></span> <span data-ttu-id="12468-121">Use the following steps to start viewing this data.</span><span class="sxs-lookup"><span data-stu-id="12468-121">Use the following steps to start viewing this data.</span></span>

1. <span data-ttu-id="12468-122">Select **Create a resource** > **Monitoring + Management** > **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="12468-122">Select **Create a resource** > **Monitoring + Management** > **Application Insights**.</span></span>

   ![Adding Application Insights Resource](./media/app-insights-java-quick-start/001-j.png)

   <span data-ttu-id="12468-124">A configuration box appears; use the following table to fill out the input fields.</span><span class="sxs-lookup"><span data-stu-id="12468-124">A configuration box appears; use the following table to fill out the input fields.</span></span>

    | <span data-ttu-id="12468-125">Settings</span><span class="sxs-lookup"><span data-stu-id="12468-125">Settings</span></span>        | <span data-ttu-id="12468-126">Value</span><span class="sxs-lookup"><span data-stu-id="12468-126">Value</span></span>           | <span data-ttu-id="12468-127">Description</span><span class="sxs-lookup"><span data-stu-id="12468-127">Description</span></span>  |
   | ------------- |:-------------|:-----|
   | <span data-ttu-id="12468-128">**Name**</span><span class="sxs-lookup"><span data-stu-id="12468-128">**Name**</span></span>      | <span data-ttu-id="12468-129">Globally Unique Value</span><span class="sxs-lookup"><span data-stu-id="12468-129">Globally Unique Value</span></span> | <span data-ttu-id="12468-130">Name that identifies the app you are monitoring</span><span class="sxs-lookup"><span data-stu-id="12468-130">Name that identifies the app you are monitoring</span></span> |
   | <span data-ttu-id="12468-131">**Application Type**</span><span class="sxs-lookup"><span data-stu-id="12468-131">**Application Type**</span></span> | <span data-ttu-id="12468-132">Java web application</span><span class="sxs-lookup"><span data-stu-id="12468-132">Java web application</span></span> | <span data-ttu-id="12468-133">Type of app you are monitoring</span><span class="sxs-lookup"><span data-stu-id="12468-133">Type of app you are monitoring</span></span> |
   | <span data-ttu-id="12468-134">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="12468-134">**Resource Group**</span></span>     | <span data-ttu-id="12468-135">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="12468-135">myResourceGroup</span></span>      | <span data-ttu-id="12468-136">Name for the new resource group to host App Insights data</span><span class="sxs-lookup"><span data-stu-id="12468-136">Name for the new resource group to host App Insights data</span></span> |
   | <span data-ttu-id="12468-137">**Location**</span><span class="sxs-lookup"><span data-stu-id="12468-137">**Location**</span></span> | <span data-ttu-id="12468-138">East US</span><span class="sxs-lookup"><span data-stu-id="12468-138">East US</span></span> | <span data-ttu-id="12468-139">Choose a location near you, or near where your app is hosted</span><span class="sxs-lookup"><span data-stu-id="12468-139">Choose a location near you, or near where your app is hosted</span></span> |

2. <span data-ttu-id="12468-140">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="12468-140">Click **Create**.</span></span>

## <a name="install-app-insights-plugin"></a><span data-ttu-id="12468-141">Install App Insights Plugin</span><span class="sxs-lookup"><span data-stu-id="12468-141">Install App Insights Plugin</span></span>

1. <span data-ttu-id="12468-142">Launch **Eclipse** > Click **Help** > Select **Install New Software**.</span><span class="sxs-lookup"><span data-stu-id="12468-142">Launch **Eclipse** > Click **Help** > Select **Install New Software**.</span></span>

   ![New App Insights resource form](./media/app-insights-java-quick-start/000-j.png)

2. <span data-ttu-id="12468-144">Copy ```http://dl.microsoft.com/eclipse``` into the "Work With" field > Check **Azure Toolkit for Java** > Select **Application Insights Plugin for Java** > **Uncheck** "Contact all update sites during install to find required software."</span><span class="sxs-lookup"><span data-stu-id="12468-144">Copy ```http://dl.microsoft.com/eclipse``` into the "Work With" field > Check **Azure Toolkit for Java** > Select **Application Insights Plugin for Java** > **Uncheck** "Contact all update sites during install to find required software."</span></span>

3. <span data-ttu-id="12468-145">Once the installation is complete, you will be prompted to **Restart Eclipse**.</span><span class="sxs-lookup"><span data-stu-id="12468-145">Once the installation is complete, you will be prompted to **Restart Eclipse**.</span></span>

## <a name="configure-app-insights-plugin"></a><span data-ttu-id="12468-146">Configure App Insights Plugin</span><span class="sxs-lookup"><span data-stu-id="12468-146">Configure App Insights Plugin</span></span>

1. <span data-ttu-id="12468-147">Launch **Eclipse** > Open your **Project** > Right-click the project name in the **Project Explorer** > Select **Azure** > Click **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="12468-147">Launch **Eclipse** > Open your **Project** > Right-click the project name in the **Project Explorer** > Select **Azure** > Click **Sign In**.</span></span>

2. <span data-ttu-id="12468-148">Select Authentication Method **Interactive** > Click **Sign In** > When prompted enter your **Azure credentials** > Select Your **Azure Subscription**.</span><span class="sxs-lookup"><span data-stu-id="12468-148">Select Authentication Method **Interactive** > Click **Sign In** > When prompted enter your **Azure credentials** > Select Your **Azure Subscription**.</span></span>

3. <span data-ttu-id="12468-149">Right-click your project name in **Project Explorer** > Select **Azure** > Click **Configure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="12468-149">Right-click your project name in **Project Explorer** > Select **Azure** > Click **Configure Application Insights**.</span></span>

4. <span data-ttu-id="12468-150">Check **Enable telemetry with Application Insights** > Select the App Insights resource and associated **Instrumentation Key** you want to link to your Java app.</span><span class="sxs-lookup"><span data-stu-id="12468-150">Check **Enable telemetry with Application Insights** > Select the App Insights resource and associated **Instrumentation Key** you want to link to your Java app.</span></span>

   ![Eclipse Azure Config Menu](./media/app-insights-java-quick-start/0007-j.png)

> [!NOTE]
> <span data-ttu-id="12468-152">The Application Insights SDK for Java is capable of capturing and visualizing live metrics, but when you first enable telemetry collection it can take a few minutes before data begins appearing in the portal.</span><span class="sxs-lookup"><span data-stu-id="12468-152">The Application Insights SDK for Java is capable of capturing and visualizing live metrics, but when you first enable telemetry collection it can take a few minutes before data begins appearing in the portal.</span></span> <span data-ttu-id="12468-153">If this app is a low-traffic test app, keep in mind that most metrics are only captured when there are active requests or operations.</span><span class="sxs-lookup"><span data-stu-id="12468-153">If this app is a low-traffic test app, keep in mind that most metrics are only captured when there are active requests or operations.</span></span>

## <a name="start-monitoring-in-the-azure-portal"></a><span data-ttu-id="12468-154">Start monitoring in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="12468-154">Start monitoring in the Azure portal</span></span>

1. <span data-ttu-id="12468-155">You can now reopen the Application Insights **Overview** page in the Azure portal, where you retrieved your instrumentation key, to view details about your currently running application.</span><span class="sxs-lookup"><span data-stu-id="12468-155">You can now reopen the Application Insights **Overview** page in the Azure portal, where you retrieved your instrumentation key, to view details about your currently running application.</span></span>

   ![Application Insights Overview Menu](./media/app-insights-java-quick-start/overview-001.png)

2. <span data-ttu-id="12468-157">Click **Application map** for a visual layout of the dependency relationships between your application components.</span><span class="sxs-lookup"><span data-stu-id="12468-157">Click **Application map** for a visual layout of the dependency relationships between your application components.</span></span> <span data-ttu-id="12468-158">Each component shows KPIs such as load, performance, failures, and alerts.</span><span class="sxs-lookup"><span data-stu-id="12468-158">Each component shows KPIs such as load, performance, failures, and alerts.</span></span>

   ![Application Map](./media/app-insights-java-quick-start/application-map-001.png)

3. <span data-ttu-id="12468-160">Click on the **App Analytics** icon ![Application Map icon](./media/app-insights-java-quick-start/006.png).</span><span class="sxs-lookup"><span data-stu-id="12468-160">Click on the **App Analytics** icon ![Application Map icon](./media/app-insights-java-quick-start/006.png).</span></span> <span data-ttu-id="12468-161">This opens **Application Insights Analytics**, which provides a rich query language for analyzing all data collected by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="12468-161">This opens **Application Insights Analytics**, which provides a rich query language for analyzing all data collected by Application Insights.</span></span> <span data-ttu-id="12468-162">In this case, a query is generated for you that renders the request count as a chart.</span><span class="sxs-lookup"><span data-stu-id="12468-162">In this case, a query is generated for you that renders the request count as a chart.</span></span> <span data-ttu-id="12468-163">You can write your own queries to analyze other data.</span><span class="sxs-lookup"><span data-stu-id="12468-163">You can write your own queries to analyze other data.</span></span>

   ![Analytics graph of user requests over a period of time](./media/app-insights-java-quick-start/0010-j.png)

4. <span data-ttu-id="12468-165">Return to the **Overview** page and examine the KPI graphs.</span><span class="sxs-lookup"><span data-stu-id="12468-165">Return to the **Overview** page and examine the KPI graphs.</span></span>  <span data-ttu-id="12468-166">This dashboard provides statistics about your application health, including the number of incoming requests, the duration of those requests, and any failures that occur.</span><span class="sxs-lookup"><span data-stu-id="12468-166">This dashboard provides statistics about your application health, including the number of incoming requests, the duration of those requests, and any failures that occur.</span></span>

   ![Health Overview timeline graphs](./media/app-insights-java-quick-start/overview-perf.png)

   <span data-ttu-id="12468-168">To enable the **Page View Load Time** chart to populate with **client-side telemetry** data, add this script to each page that you want to track:</span><span class="sxs-lookup"><span data-stu-id="12468-168">To enable the **Page View Load Time** chart to populate with **client-side telemetry** data, add this script to each page that you want to track:</span></span>

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
        instrumentationKey:"<instrumentation key>"
    });

    window.appInsights=appInsights;
    appInsights.trackPageView();
   </script>
    ```

5. <span data-ttu-id="12468-169">Click on **Live Stream**.</span><span class="sxs-lookup"><span data-stu-id="12468-169">Click on **Live Stream**.</span></span> <span data-ttu-id="12468-170">Here you find live metrics related to the performance of your Java web app.</span><span class="sxs-lookup"><span data-stu-id="12468-170">Here you find live metrics related to the performance of your Java web app.</span></span> <span data-ttu-id="12468-171">**Live Metrics Stream** includes data regarding the number of incoming requests, the duration of those requests, and any failures that occur.</span><span class="sxs-lookup"><span data-stu-id="12468-171">**Live Metrics Stream** includes data regarding the number of incoming requests, the duration of those requests, and any failures that occur.</span></span> <span data-ttu-id="12468-172">You can also monitor critical performance metrics, such as processor and memory in real-time.</span><span class="sxs-lookup"><span data-stu-id="12468-172">You can also monitor critical performance metrics, such as processor and memory in real-time.</span></span>

   ![Server metrics graphs](./media/app-insights-java-quick-start/livemetricsjava.png)

<span data-ttu-id="12468-174">To learn more about monitoring Java, check out the [additional App Insights Java documentation](.\app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="12468-174">To learn more about monitoring Java, check out the [additional App Insights Java documentation](.\app-insights-java-get-started.md).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="12468-175">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="12468-175">Clean up resources</span></span>

<span data-ttu-id="12468-176">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quick start.</span><span class="sxs-lookup"><span data-stu-id="12468-176">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="12468-177">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="12468-177">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>

1. <span data-ttu-id="12468-178">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="12468-178">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span>
2. <span data-ttu-id="12468-179">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="12468-179">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12468-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="12468-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="12468-181">Find and diagnose performance problems</span><span class="sxs-lookup"><span data-stu-id="12468-181">Find and diagnose performance problems</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)