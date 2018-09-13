---
title: Send alerts from Azure Application Insights | Microsoft Docs
description: Tutorial to send alerts in response to errors in your application using Azure Application Insights.
keywords: ''
author: mrbullwinkle
ms.author: mbullwin
ms.date: 09/20/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: tutorial
manager: carmonm
ms.openlocfilehash: 39e2f136e30ebb6dcfc003c435382f3384af1052
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857989"
---
# <a name="monitor-and-alert-on-application-health-with-azure-application-insights"></a><span data-ttu-id="ee3a0-103">Monitor and alert on application health with Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="ee3a0-103">Monitor and alert on application health with Azure Application Insights</span></span>

<span data-ttu-id="ee3a0-104">Azure Application Insights allows you to monitor your application and send you alerts when it is either unavailable, experiencing failures, or suffering from performance issues.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-104">Azure Application Insights allows you to monitor your application and send you alerts when it is either unavailable, experiencing failures, or suffering from performance issues.</span></span>  <span data-ttu-id="ee3a0-105">This tutorial takes you through the process of creating tests to continuously check the availability of your application and to send different kinds of alerts in response to detected issues.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-105">This tutorial takes you through the process of creating tests to continuously check the availability of your application and to send different kinds of alerts in response to detected issues.</span></span>  <span data-ttu-id="ee3a0-106">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="ee3a0-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ee3a0-107">Create availability test to continuously check the response of the application</span><span class="sxs-lookup"><span data-stu-id="ee3a0-107">Create availability test to continuously check the response of the application</span></span>
> * <span data-ttu-id="ee3a0-108">Send mail to administrators when a problem occurs</span><span class="sxs-lookup"><span data-stu-id="ee3a0-108">Send mail to administrators when a problem occurs</span></span>
> * <span data-ttu-id="ee3a0-109">Create alerts based on performance metrics</span><span class="sxs-lookup"><span data-stu-id="ee3a0-109">Create alerts based on performance metrics</span></span> 
> * <span data-ttu-id="ee3a0-110">Use a Logic App to send summarized telemetry on a schedule.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-110">Use a Logic App to send summarized telemetry on a schedule.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ee3a0-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ee3a0-111">Prerequisites</span></span>

<span data-ttu-id="ee3a0-112">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="ee3a0-112">To complete this tutorial:</span></span>

- <span data-ttu-id="ee3a0-113">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span><span class="sxs-lookup"><span data-stu-id="ee3a0-113">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="ee3a0-114">ASP.NET and web development</span><span class="sxs-lookup"><span data-stu-id="ee3a0-114">ASP.NET and web development</span></span>
    - <span data-ttu-id="ee3a0-115">Azure development</span><span class="sxs-lookup"><span data-stu-id="ee3a0-115">Azure development</span></span>
    - <span data-ttu-id="ee3a0-116">Deploy a .NET application to Azure and [enable the Application Insights SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="ee3a0-116">Deploy a .NET application to Azure and [enable the Application Insights SDK](app-insights-asp-net.md).</span></span> 


## <a name="log-in-to-azure"></a><span data-ttu-id="ee3a0-117">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="ee3a0-117">Log in to Azure</span></span>
<span data-ttu-id="ee3a0-118">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee3a0-118">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>

## <a name="create-availability-test"></a><span data-ttu-id="ee3a0-119">Create availability test</span><span class="sxs-lookup"><span data-stu-id="ee3a0-119">Create availability test</span></span>
<span data-ttu-id="ee3a0-120">Availability tests in Application Insights allow you to automatically test your application from various locations around the world.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-120">Availability tests in Application Insights allow you to automatically test your application from various locations around the world.</span></span>   <span data-ttu-id="ee3a0-121">In this tutorial, you will perform a simple test to ensure that the application is available.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-121">In this tutorial, you will perform a simple test to ensure that the application is available.</span></span>  <span data-ttu-id="ee3a0-122">You could also create a complete walkthrough to test its detailed operation.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-122">You could also create a complete walkthrough to test its detailed operation.</span></span> 

1. <span data-ttu-id="ee3a0-123">Select **Application Insights** and then select your subscription.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-123">Select **Application Insights** and then select your subscription.</span></span>  
1. <span data-ttu-id="ee3a0-124">Select **Availability** under the **Investigate** menu and then click **Add test**.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-124">Select **Availability** under the **Investigate** menu and then click **Add test**.</span></span>
 
    ![Add availability test](media/app-insights-tutorial-alert/add-test.png)

2. <span data-ttu-id="ee3a0-126">Type in a name for the test and leave the other defaults.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-126">Type in a name for the test and leave the other defaults.</span></span>  <span data-ttu-id="ee3a0-127">This requests the home page of the application every 5 minutes from 5 different geographic locations.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-127">This requests the home page of the application every 5 minutes from 5 different geographic locations.</span></span> 
3. <span data-ttu-id="ee3a0-128">Select **Alerts** to open the **Alerts** panel where you can define details for how to respond if the test fails.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-128">Select **Alerts** to open the **Alerts** panel where you can define details for how to respond if the test fails.</span></span> <span data-ttu-id="ee3a0-129">Type in an email address to send when the alert criteria is met.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-129">Type in an email address to send when the alert criteria is met.</span></span>  <span data-ttu-id="ee3a0-130">You could optionally type in the address of a webhook to call when the alert criteria is met.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-130">You could optionally type in the address of a webhook to call when the alert criteria is met.</span></span>

    ![Create test](media/app-insights-tutorial-alert/create-test.png)
 
4. <span data-ttu-id="ee3a0-132">Return to the test panel, and after a few minutes you should start seeing results from the availability test.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-132">Return to the test panel, and after a few minutes you should start seeing results from the availability test.</span></span>  <span data-ttu-id="ee3a0-133">Click on the test name to view details from each location.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-133">Click on the test name to view details from each location.</span></span>  <span data-ttu-id="ee3a0-134">The scatter chart shows the success and duration of each test.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-134">The scatter chart shows the success and duration of each test.</span></span>

    ![Test details](media/app-insights-tutorial-alert/test-details.png)

5.  <span data-ttu-id="ee3a0-136">You can drill down in to the details of any particular test by clicking on its dot in the scatter chart.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-136">You can drill down in to the details of any particular test by clicking on its dot in the scatter chart.</span></span>  <span data-ttu-id="ee3a0-137">The example below shows the details for a failed request.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-137">The example below shows the details for a failed request.</span></span>

    ![Test result](media/app-insights-tutorial-alert/test-result.png)
  
6. <span data-ttu-id="ee3a0-139">If the alert criteria is met, a mail similar to the one below is sent to the address that you specified.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-139">If the alert criteria is met, a mail similar to the one below is sent to the address that you specified.</span></span>

    ![Alert mail](media/app-insights-tutorial-alert/alert-mail.png)


## <a name="create-an-alert-from-metrics"></a><span data-ttu-id="ee3a0-141">Create an alert from metrics</span><span class="sxs-lookup"><span data-stu-id="ee3a0-141">Create an alert from metrics</span></span>
<span data-ttu-id="ee3a0-142">In addition to sending alerts from an availability test, you can create an alert from any performance metrics that are being collected for your application.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-142">In addition to sending alerts from an availability test, you can create an alert from any performance metrics that are being collected for your application.</span></span>

2. <span data-ttu-id="ee3a0-143">Select **Alerts** from the **Configure** menu.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-143">Select **Alerts** from the **Configure** menu.</span></span>  <span data-ttu-id="ee3a0-144">This opens the Azure Alerts panel.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-144">This opens the Azure Alerts panel.</span></span>  <span data-ttu-id="ee3a0-145">There may be other alert rules configured here for other services.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-145">There may be other alert rules configured here for other services.</span></span>
3. <span data-ttu-id="ee3a0-146">Click **Add metric alert**.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-146">Click **Add metric alert**.</span></span>  <span data-ttu-id="ee3a0-147">This opens the panel to create a new alert rule.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-147">This opens the panel to create a new alert rule.</span></span>

    ![Add metric alert](media/app-insights-tutorial-alert/add-metric-alert.png)

4. <span data-ttu-id="ee3a0-149">Type in a **Name** for the alert rule, and select your application in the dropdown for **Resource**.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-149">Type in a **Name** for the alert rule, and select your application in the dropdown for **Resource**.</span></span>
5. <span data-ttu-id="ee3a0-150">Select a **Metric** to sample.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-150">Select a **Metric** to sample.</span></span>  <span data-ttu-id="ee3a0-151">A graph is displayed to indicate the value of this request over the past 24 hours.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-151">A graph is displayed to indicate the value of this request over the past 24 hours.</span></span>  <span data-ttu-id="ee3a0-152">This assists you in setting the condition for the metric.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-152">This assists you in setting the condition for the metric.</span></span>

    ![Add alert rule](media/app-insights-tutorial-alert/add-alert-01.png)

6. <span data-ttu-id="ee3a0-154">Specify a **Condition** and **Threshold** for the alert.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-154">Specify a **Condition** and **Threshold** for the alert.</span></span> <span data-ttu-id="ee3a0-155">This is the number of times that the metric must be exceeded for an alert to be created.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-155">This is the number of times that the metric must be exceeded for an alert to be created.</span></span> 
6. <span data-ttu-id="ee3a0-156">Under **Notify via** check the **Email owners, contributors, and readers** box to send a mail to these users when the alert condition is met and add the email address of any additional recipients.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-156">Under **Notify via** check the **Email owners, contributors, and readers** box to send a mail to these users when the alert condition is met and add the email address of any additional recipients.</span></span>  <span data-ttu-id="ee3a0-157">You can also specify a webhook or a logic app here that runs when the condition is met.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-157">You can also specify a webhook or a logic app here that runs when the condition is met.</span></span>  <span data-ttu-id="ee3a0-158">These could be used to attempt to mitigate the detected issue or</span><span class="sxs-lookup"><span data-stu-id="ee3a0-158">These could be used to attempt to mitigate the detected issue or</span></span> 

    ![Add alert rule](media/app-insights-tutorial-alert/add-alert-02.png)


## <a name="proactively-send-information"></a><span data-ttu-id="ee3a0-160">Proactively send information</span><span class="sxs-lookup"><span data-stu-id="ee3a0-160">Proactively send information</span></span>
<span data-ttu-id="ee3a0-161">Alerts are created in reaction to a particular set of issues identified in your application, and you typically reserve alerts for critical conditions requiring immediate attention.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-161">Alerts are created in reaction to a particular set of issues identified in your application, and you typically reserve alerts for critical conditions requiring immediate attention.</span></span>  <span data-ttu-id="ee3a0-162">You can proactively receive information about your application with a Logic App that runs automatically on a schedule.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-162">You can proactively receive information about your application with a Logic App that runs automatically on a schedule.</span></span>  <span data-ttu-id="ee3a0-163">For example, you could have a mail sent to administrators daily with summary information that requires further evaluation.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-163">For example, you could have a mail sent to administrators daily with summary information that requires further evaluation.</span></span>

<span data-ttu-id="ee3a0-164">For details on creating a Logic App with Application Insights, see [Automate Application Insights processes by using Logic Apps](automate-with-logic-apps.md)</span><span class="sxs-lookup"><span data-stu-id="ee3a0-164">For details on creating a Logic App with Application Insights, see [Automate Application Insights processes by using Logic Apps](automate-with-logic-apps.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee3a0-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="ee3a0-165">Next steps</span></span>
<span data-ttu-id="ee3a0-166">Now that you've learned how to alert on issues, advance to the next tutorial to learn how to analyze how users are interacting with your application.</span><span class="sxs-lookup"><span data-stu-id="ee3a0-166">Now that you've learned how to alert on issues, advance to the next tutorial to learn how to analyze how users are interacting with your application.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee3a0-167">Understand users</span><span class="sxs-lookup"><span data-stu-id="ee3a0-167">Understand users</span></span>](app-insights-tutorial-users.md)