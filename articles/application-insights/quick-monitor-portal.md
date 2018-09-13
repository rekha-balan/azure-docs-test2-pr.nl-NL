---
title: Monitor your ASP.NET Web App  with Azure Application Insights | Microsoft Docs
description: Provides instructions to quickly setup a ASP.NET Web App for monitoring with Application Insights
services: application-insights
keywords: ''
author: mrbullwinkle
ms.author: mbullwin
ms.date: 06/13/2018
ms.service: application-insights
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
ms.openlocfilehash: db8aa2d1bb5d79b5d2c9b04789b4ac18fbec5897
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868969"
---
# <a name="start-monitoring-your-aspnet-web-application"></a><span data-ttu-id="a156a-103">Start monitoring your ASP.NET Web Application</span><span class="sxs-lookup"><span data-stu-id="a156a-103">Start monitoring your ASP.NET Web Application</span></span>

<span data-ttu-id="a156a-104">With Azure Application Insights, you can easily monitor your web application for availability, performance, and usage.</span><span class="sxs-lookup"><span data-stu-id="a156a-104">With Azure Application Insights, you can easily monitor your web application for availability, performance, and usage.</span></span>  <span data-ttu-id="a156a-105">You can also quickly identify and diagnose errors in your application without waiting for a user to report them.</span><span class="sxs-lookup"><span data-stu-id="a156a-105">You can also quickly identify and diagnose errors in your application without waiting for a user to report them.</span></span>  <span data-ttu-id="a156a-106">With the information that you collect from Application Insights about the performance and effectiveness of your app, you can make informed choices to maintain and improve your application.</span><span class="sxs-lookup"><span data-stu-id="a156a-106">With the information that you collect from Application Insights about the performance and effectiveness of your app, you can make informed choices to maintain and improve your application.</span></span>

<span data-ttu-id="a156a-107">This quickstart shows how to add Application Insights to an existing ASP.NET web application and start analyzing live statistics, which is just one of the various methods you can use to analyze your application.</span><span class="sxs-lookup"><span data-stu-id="a156a-107">This quickstart shows how to add Application Insights to an existing ASP.NET web application and start analyzing live statistics, which is just one of the various methods you can use to analyze your application.</span></span> <span data-ttu-id="a156a-108">If you do not have a ASP.NET web application, you can create one following the [Create a ASP.NET Web App quickstart](../app-service/app-service-web-get-started-dotnet-framework.md).</span><span class="sxs-lookup"><span data-stu-id="a156a-108">If you do not have a ASP.NET web application, you can create one following the [Create a ASP.NET Web App quickstart](../app-service/app-service-web-get-started-dotnet-framework.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a156a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a156a-109">Prerequisites</span></span>
<span data-ttu-id="a156a-110">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="a156a-110">To complete this quickstart:</span></span>

- <span data-ttu-id="a156a-111">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span><span class="sxs-lookup"><span data-stu-id="a156a-111">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="a156a-112">ASP.NET and web development</span><span class="sxs-lookup"><span data-stu-id="a156a-112">ASP.NET and web development</span></span>
    - <span data-ttu-id="a156a-113">Azure development</span><span class="sxs-lookup"><span data-stu-id="a156a-113">Azure development</span></span>


<span data-ttu-id="a156a-114">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="a156a-114">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="enable-application-insights"></a><span data-ttu-id="a156a-115">Enable Application Insights</span><span class="sxs-lookup"><span data-stu-id="a156a-115">Enable Application Insights</span></span>

1. <span data-ttu-id="a156a-116">Open your project in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a156a-116">Open your project in Visual Studio 2017.</span></span>
2. <span data-ttu-id="a156a-117">Select **Configure Application Insights** from the Project menu.</span><span class="sxs-lookup"><span data-stu-id="a156a-117">Select **Configure Application Insights** from the Project menu.</span></span> <span data-ttu-id="a156a-118">Visual Studio adds the Application Insights SDK to your application.</span><span class="sxs-lookup"><span data-stu-id="a156a-118">Visual Studio adds the Application Insights SDK to your application.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a156a-119">The process to add Application Insights varies by ASP.NET template type.</span><span class="sxs-lookup"><span data-stu-id="a156a-119">The process to add Application Insights varies by ASP.NET template type.</span></span> <span data-ttu-id="a156a-120">If you are using the **Empty** or **Azure Mobile App** template select **Project** > **Add Application Insights Telemetry**.</span><span class="sxs-lookup"><span data-stu-id="a156a-120">If you are using the **Empty** or **Azure Mobile App** template select **Project** > **Add Application Insights Telemetry**.</span></span> <span data-ttu-id="a156a-121">For all other ASP.NET templates consult the instructions in the step above.</span><span class="sxs-lookup"><span data-stu-id="a156a-121">For all other ASP.NET templates consult the instructions in the step above.</span></span> 

3. <span data-ttu-id="a156a-122">Click **Get Started** (earlier versions of Visual Studio have a **Start Free** button instead).</span><span class="sxs-lookup"><span data-stu-id="a156a-122">Click **Get Started** (earlier versions of Visual Studio have a **Start Free** button instead).</span></span>

    ![Adding Application Insights to Visual Studio](./media/quick-monitor-portal/add-application-insights-b.png)

4. <span data-ttu-id="a156a-124">Select your subscription and click **Register**.</span><span class="sxs-lookup"><span data-stu-id="a156a-124">Select your subscription and click **Register**.</span></span>

5. <span data-ttu-id="a156a-125">Run your application by either selecting **Start Debugging** from the **Debug** menu or by pressing the F5 key.</span><span class="sxs-lookup"><span data-stu-id="a156a-125">Run your application by either selecting **Start Debugging** from the **Debug** menu or by pressing the F5 key.</span></span>

## <a name="confirm-app-configuration"></a><span data-ttu-id="a156a-126">Confirm app configuration</span><span class="sxs-lookup"><span data-stu-id="a156a-126">Confirm app configuration</span></span>

<span data-ttu-id="a156a-127">Application Insights gathers telemetry data for your application regardless of where it's running.</span><span class="sxs-lookup"><span data-stu-id="a156a-127">Application Insights gathers telemetry data for your application regardless of where it's running.</span></span> <span data-ttu-id="a156a-128">Use the following steps to start viewing this data.</span><span class="sxs-lookup"><span data-stu-id="a156a-128">Use the following steps to start viewing this data.</span></span>

1. <span data-ttu-id="a156a-129">Open Application Insights by clicking **View** -> **Other Windows** -> **Application Insights Search**.</span><span class="sxs-lookup"><span data-stu-id="a156a-129">Open Application Insights by clicking **View** -> **Other Windows** -> **Application Insights Search**.</span></span>  <span data-ttu-id="a156a-130">You see the telemetry from your current session.</span><span class="sxs-lookup"><span data-stu-id="a156a-130">You see the telemetry from your current session.</span></span><BR><br><span data-ttu-id="a156a-131">![Telemetry in Visual Studio](./media/quick-monitor-portal/telemetry-in-vs.png)</span><span class="sxs-lookup"><span data-stu-id="a156a-131">![Telemetry in Visual Studio](./media/quick-monitor-portal/telemetry-in-vs.png)</span></span>

2. <span data-ttu-id="a156a-132">Click on the first request in the list (GET Home/Index in this example) to see the request details.</span><span class="sxs-lookup"><span data-stu-id="a156a-132">Click on the first request in the list (GET Home/Index in this example) to see the request details.</span></span> <span data-ttu-id="a156a-133">Notice that the status code and response time are both included along with other valuable information about the request.</span><span class="sxs-lookup"><span data-stu-id="a156a-133">Notice that the status code and response time are both included along with other valuable information about the request.</span></span><br><br>![Response details in Visual Studio](media/quick-monitor-portal/request-details.png)

## <a name="start-monitoring-in-the-azure-portal"></a><span data-ttu-id="a156a-135">Start monitoring in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a156a-135">Start monitoring in the Azure portal</span></span>

<span data-ttu-id="a156a-136">You can now open Application Insights in the Azure portal to view various details about your running application.</span><span class="sxs-lookup"><span data-stu-id="a156a-136">You can now open Application Insights in the Azure portal to view various details about your running application.</span></span>

1. <span data-ttu-id="a156a-137">Right-click on **Connected Services Application Insights** folder in Solution Explorer and click **Open Application Insights Portal**.</span><span class="sxs-lookup"><span data-stu-id="a156a-137">Right-click on **Connected Services Application Insights** folder in Solution Explorer and click **Open Application Insights Portal**.</span></span>  <span data-ttu-id="a156a-138">You see some information about your application and a variety of options.</span><span class="sxs-lookup"><span data-stu-id="a156a-138">You see some information about your application and a variety of options.</span></span>

    ![Application Map](media/quick-monitor-portal/overview-001.png)

2. <span data-ttu-id="a156a-140">Click on **Application map** to get a visual layout of the dependency relationships between your application components.</span><span class="sxs-lookup"><span data-stu-id="a156a-140">Click on **Application map** to get a visual layout of the dependency relationships between your application components.</span></span>  <span data-ttu-id="a156a-141">Each component shows KPIs such as load, performance, failures, and alerts.</span><span class="sxs-lookup"><span data-stu-id="a156a-141">Each component shows KPIs such as load, performance, failures, and alerts.</span></span>

    ![Application Map](media/quick-monitor-portal/application-map-001.png)

3. <span data-ttu-id="a156a-143">Click on the **App Analytics** icon ![Application Map](media/quick-monitor-portal/app-analytics-icon.png) on one of the application components.</span><span class="sxs-lookup"><span data-stu-id="a156a-143">Click on the **App Analytics** icon ![Application Map](media/quick-monitor-portal/app-analytics-icon.png) on one of the application components.</span></span>  <span data-ttu-id="a156a-144">This opens **Application Insights Analytics**, which provides a rich query language for analyzing all data collected by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a156a-144">This opens **Application Insights Analytics**, which provides a rich query language for analyzing all data collected by Application Insights.</span></span>  <span data-ttu-id="a156a-145">In this case, a query is generated for you that renders the request count as a chart.</span><span class="sxs-lookup"><span data-stu-id="a156a-145">In this case, a query is generated for you that renders the request count as a chart.</span></span>  <span data-ttu-id="a156a-146">You can write your own queries to analyze other data.</span><span class="sxs-lookup"><span data-stu-id="a156a-146">You can write your own queries to analyze other data.</span></span>

    ![Analytics](media/quick-monitor-portal/analytics.png)

4. <span data-ttu-id="a156a-148">Return to the **Overview** page and click on **Live Stream**.</span><span class="sxs-lookup"><span data-stu-id="a156a-148">Return to the **Overview** page and click on **Live Stream**.</span></span>  <span data-ttu-id="a156a-149">This shows live statistics about your application as it's running.</span><span class="sxs-lookup"><span data-stu-id="a156a-149">This shows live statistics about your application as it's running.</span></span>  <span data-ttu-id="a156a-150">This includes such information as the number of incoming requests, the duration of those requests, and any failures that occur.</span><span class="sxs-lookup"><span data-stu-id="a156a-150">This includes such information as the number of incoming requests, the duration of those requests, and any failures that occur.</span></span>  <span data-ttu-id="a156a-151">You can also inspect critical performance metrics such as processor and memory.</span><span class="sxs-lookup"><span data-stu-id="a156a-151">You can also inspect critical performance metrics such as processor and memory.</span></span>

    ![Live Stream](media/quick-monitor-portal/live-stream.png)

<span data-ttu-id="a156a-153">If you are ready to host your application in Azure, you can publish it now.</span><span class="sxs-lookup"><span data-stu-id="a156a-153">If you are ready to host your application in Azure, you can publish it now.</span></span> <span data-ttu-id="a156a-154">Follow the steps described in [Create an ASP.NET Web App Quickstart](../app-service/app-service-web-get-started-dotnet.md#update-the-app-and-redeploy).</span><span class="sxs-lookup"><span data-stu-id="a156a-154">Follow the steps described in [Create an ASP.NET Web App Quickstart](../app-service/app-service-web-get-started-dotnet.md#update-the-app-and-redeploy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a156a-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="a156a-155">Next steps</span></span>
<span data-ttu-id="a156a-156">In this quick start, you’ve enabled your application for monitoring by Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a156a-156">In this quick start, you’ve enabled your application for monitoring by Azure Application Insights.</span></span>  <span data-ttu-id="a156a-157">Continue to the tutorials to learn how to use it to monitor statistics and detect issues in your application.</span><span class="sxs-lookup"><span data-stu-id="a156a-157">Continue to the tutorials to learn how to use it to monitor statistics and detect issues in your application.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a156a-158">Azure Application Insights tutorials</span><span class="sxs-lookup"><span data-stu-id="a156a-158">Azure Application Insights tutorials</span></span>](app-insights-tutorial-runtime-exceptions.md)
