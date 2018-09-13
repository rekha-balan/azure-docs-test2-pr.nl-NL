---
title: Diagnose run-time exceptions using Azure Application Insights | Microsoft Docs
description: Tutorial to find and diagnose run-time exceptions in your application using Azure Application Insights.
services: application-insights
keywords: ''
author: mrbullwinkle
ms.author: mbullwin
ms.date: 09/19/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: tutorial
manager: carmonm
ms.openlocfilehash: f45cb6a47756fae7b75d8c3df80a0bc754742063
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867766"
---
# <a name="find-and-diagnose-run-time-exceptions-with-azure-application-insights"></a><span data-ttu-id="e003e-103">Find and diagnose run-time exceptions with Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="e003e-103">Find and diagnose run-time exceptions with Azure Application Insights</span></span>

<span data-ttu-id="e003e-104">Azure Application Insights collects telemetry from your application to help identify and diagnose run-time exceptions.</span><span class="sxs-lookup"><span data-stu-id="e003e-104">Azure Application Insights collects telemetry from your application to help identify and diagnose run-time exceptions.</span></span>  <span data-ttu-id="e003e-105">This tutorial takes you through this process with your application.</span><span class="sxs-lookup"><span data-stu-id="e003e-105">This tutorial takes you through this process with your application.</span></span>  <span data-ttu-id="e003e-106">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="e003e-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e003e-107">Modify your project to enable exception tracking</span><span class="sxs-lookup"><span data-stu-id="e003e-107">Modify your project to enable exception tracking</span></span>
> * <span data-ttu-id="e003e-108">Identify exceptions for different components of your application</span><span class="sxs-lookup"><span data-stu-id="e003e-108">Identify exceptions for different components of your application</span></span>
> * <span data-ttu-id="e003e-109">View details of an exception</span><span class="sxs-lookup"><span data-stu-id="e003e-109">View details of an exception</span></span>
> * <span data-ttu-id="e003e-110">Download a snapshot of the exception to Visual Studio for debugging</span><span class="sxs-lookup"><span data-stu-id="e003e-110">Download a snapshot of the exception to Visual Studio for debugging</span></span>
> * <span data-ttu-id="e003e-111">Analyze details of failed requests using query language</span><span class="sxs-lookup"><span data-stu-id="e003e-111">Analyze details of failed requests using query language</span></span>
> * <span data-ttu-id="e003e-112">Create a new work item to correct the faulty code</span><span class="sxs-lookup"><span data-stu-id="e003e-112">Create a new work item to correct the faulty code</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e003e-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e003e-113">Prerequisites</span></span>

<span data-ttu-id="e003e-114">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="e003e-114">To complete this tutorial:</span></span>

- <span data-ttu-id="e003e-115">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span><span class="sxs-lookup"><span data-stu-id="e003e-115">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="e003e-116">ASP.NET and web development</span><span class="sxs-lookup"><span data-stu-id="e003e-116">ASP.NET and web development</span></span>
    - <span data-ttu-id="e003e-117">Azure development</span><span class="sxs-lookup"><span data-stu-id="e003e-117">Azure development</span></span>
- <span data-ttu-id="e003e-118">Download and install the [Visual Studio Snapshot Debugger](http://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="e003e-118">Download and install the [Visual Studio Snapshot Debugger](http://aka.ms/snapshotdebugger).</span></span>
- <span data-ttu-id="e003e-119">Enable [Visual Studio Snapshot Debugger](https://docs.microsoft.com/azure/application-insights/app-insights-snapshot-debugger)</span><span class="sxs-lookup"><span data-stu-id="e003e-119">Enable [Visual Studio Snapshot Debugger](https://docs.microsoft.com/azure/application-insights/app-insights-snapshot-debugger)</span></span>
- <span data-ttu-id="e003e-120">Deploy a .NET application to Azure and [enable the Application Insights SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="e003e-120">Deploy a .NET application to Azure and [enable the Application Insights SDK](app-insights-asp-net.md).</span></span> 
- <span data-ttu-id="e003e-121">The tutorial tracks the identification of an exception in your application, so modify your code in your development or test environment to generate an exception.</span><span class="sxs-lookup"><span data-stu-id="e003e-121">The tutorial tracks the identification of an exception in your application, so modify your code in your development or test environment to generate an exception.</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="e003e-122">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="e003e-122">Log in to Azure</span></span>
<span data-ttu-id="e003e-123">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e003e-123">Log in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>


## <a name="analyze-failures"></a><span data-ttu-id="e003e-124">Analyze failures</span><span class="sxs-lookup"><span data-stu-id="e003e-124">Analyze failures</span></span>
<span data-ttu-id="e003e-125">Application Insights collects any failures in your application and lets you view their frequency across different operations to help you focus your efforts on those with the highest impact.</span><span class="sxs-lookup"><span data-stu-id="e003e-125">Application Insights collects any failures in your application and lets you view their frequency across different operations to help you focus your efforts on those with the highest impact.</span></span>  <span data-ttu-id="e003e-126">You can then drill down on details of these failures to identify root cause.</span><span class="sxs-lookup"><span data-stu-id="e003e-126">You can then drill down on details of these failures to identify root cause.</span></span>   

1. <span data-ttu-id="e003e-127">Select **Application Insights** and then your subscription.</span><span class="sxs-lookup"><span data-stu-id="e003e-127">Select **Application Insights** and then your subscription.</span></span>  
2. <span data-ttu-id="e003e-128">To open the **Failures** panel either select **Failures** under the **Investigate** menu or click the **Failed requests** graph.</span><span class="sxs-lookup"><span data-stu-id="e003e-128">To open the **Failures** panel either select **Failures** under the **Investigate** menu or click the **Failed requests** graph.</span></span>

    ![Failed requests](media/app-insights-tutorial-runtime-exceptions/failed-requests.png)

3. <span data-ttu-id="e003e-130">The **Failed requests** panel shows the count of failed requests and the number of users affected for each operation for the application.</span><span class="sxs-lookup"><span data-stu-id="e003e-130">The **Failed requests** panel shows the count of failed requests and the number of users affected for each operation for the application.</span></span>  <span data-ttu-id="e003e-131">By sorting this information by user you can identify those failures that most impact users.</span><span class="sxs-lookup"><span data-stu-id="e003e-131">By sorting this information by user you can identify those failures that most impact users.</span></span>  <span data-ttu-id="e003e-132">In this example, the **GET Employees/Create** and **GET Customers/Details** are likely candidates to investigate because of their large number of failures and impacted users.</span><span class="sxs-lookup"><span data-stu-id="e003e-132">In this example, the **GET Employees/Create** and **GET Customers/Details** are likely candidates to investigate because of their large number of failures and impacted users.</span></span>  <span data-ttu-id="e003e-133">Selecting an operation shows further information about this operation in the right panel.</span><span class="sxs-lookup"><span data-stu-id="e003e-133">Selecting an operation shows further information about this operation in the right panel.</span></span>

    ![Failed requests panel](media/app-insights-tutorial-runtime-exceptions/failed-requests-blade.png)

4. <span data-ttu-id="e003e-135">Reduce the time window to zoom in on the period where the failure rate shows a spike.</span><span class="sxs-lookup"><span data-stu-id="e003e-135">Reduce the time window to zoom in on the period where the failure rate shows a spike.</span></span>

    ![Failed requests window](media/app-insights-tutorial-runtime-exceptions/failed-requests-window.png)

5. <span data-ttu-id="e003e-137">See the related samples by clicking on the button with the number of filtered results.</span><span class="sxs-lookup"><span data-stu-id="e003e-137">See the related samples by clicking on the button with the number of filtered results.</span></span> <span data-ttu-id="e003e-138">The "suggested" samples have related telemetry from all components, even if sampling may have been in effect in any of them.</span><span class="sxs-lookup"><span data-stu-id="e003e-138">The "suggested" samples have related telemetry from all components, even if sampling may have been in effect in any of them.</span></span> <span data-ttu-id="e003e-139">Click on a search result to see the details of the failure.</span><span class="sxs-lookup"><span data-stu-id="e003e-139">Click on a search result to see the details of the failure.</span></span>

    ![Failed request samples](media/app-insights-tutorial-runtime-exceptions/failed-requests-search.png)

6. <span data-ttu-id="e003e-141">The details of the failed request shows the Gantt chart which shows that there were two dependency failures in this transaction, which also attributed to over 50% of the total duration of the transaction.</span><span class="sxs-lookup"><span data-stu-id="e003e-141">The details of the failed request shows the Gantt chart which shows that there were two dependency failures in this transaction, which also attributed to over 50% of the total duration of the transaction.</span></span> <span data-ttu-id="e003e-142">This experience presents all telemetry, across components of a distributed application that are related to this operation ID.</span><span class="sxs-lookup"><span data-stu-id="e003e-142">This experience presents all telemetry, across components of a distributed application that are related to this operation ID.</span></span> <span data-ttu-id="e003e-143">[Learn more about the new experience](app-insights-transaction-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="e003e-143">[Learn more about the new experience](app-insights-transaction-diagnostics.md).</span></span> <span data-ttu-id="e003e-144">You can select any of the items to see its details on the right side.</span><span class="sxs-lookup"><span data-stu-id="e003e-144">You can select any of the items to see its details on the right side.</span></span> 

    ![Failed request details](media/app-insights-tutorial-runtime-exceptions/failed-request-details.png)

7. <span data-ttu-id="e003e-146">The operations detail also shows a FormatException which appears to have caused the failure.</span><span class="sxs-lookup"><span data-stu-id="e003e-146">The operations detail also shows a FormatException which appears to have caused the failure.</span></span>  <span data-ttu-id="e003e-147">You can see that it's due to an invalid zip code.</span><span class="sxs-lookup"><span data-stu-id="e003e-147">You can see that it's due to an invalid zip code.</span></span> <span data-ttu-id="e003e-148">You can open the debug snapshot to see code level debug information in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e003e-148">You can open the debug snapshot to see code level debug information in Visual Studio.</span></span>

    ![Exception details](media/app-insights-tutorial-runtime-exceptions/failed-requests-exception.png)

## <a name="identify-failing-code"></a><span data-ttu-id="e003e-150">Identify failing code</span><span class="sxs-lookup"><span data-stu-id="e003e-150">Identify failing code</span></span>
<span data-ttu-id="e003e-151">The Snapshot Debugger collects snapshots of the most frequent exceptions in your application to assist you in diagnosing its root cause in production.</span><span class="sxs-lookup"><span data-stu-id="e003e-151">The Snapshot Debugger collects snapshots of the most frequent exceptions in your application to assist you in diagnosing its root cause in production.</span></span>  <span data-ttu-id="e003e-152">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span><span class="sxs-lookup"><span data-stu-id="e003e-152">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="e003e-153">You can then debug the source code by downloading the snapshot and opening it in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e003e-153">You can then debug the source code by downloading the snapshot and opening it in Visual Studio 2017.</span></span>

1. <span data-ttu-id="e003e-154">In the properties of the exception, click **Open debug snapshot**.</span><span class="sxs-lookup"><span data-stu-id="e003e-154">In the properties of the exception, click **Open debug snapshot**.</span></span>
2. <span data-ttu-id="e003e-155">The **Debug Snapshot** panel opens with the call stack for the request.</span><span class="sxs-lookup"><span data-stu-id="e003e-155">The **Debug Snapshot** panel opens with the call stack for the request.</span></span>  <span data-ttu-id="e003e-156">Click any method to view the values of all local variables at the time of the request.</span><span class="sxs-lookup"><span data-stu-id="e003e-156">Click any method to view the values of all local variables at the time of the request.</span></span>  <span data-ttu-id="e003e-157">Starting from the top method in this example, we can see local variables that have no value.</span><span class="sxs-lookup"><span data-stu-id="e003e-157">Starting from the top method in this example, we can see local variables that have no value.</span></span>

    ![Debug snapshot](media/app-insights-tutorial-runtime-exceptions/debug-snapshot-01.png)

4. <span data-ttu-id="e003e-159">The first call that has valid values is **ValidZipCode**, and we can see that a zip code was provided with letters that isn't able to be translated into an integer.</span><span class="sxs-lookup"><span data-stu-id="e003e-159">The first call that has valid values is **ValidZipCode**, and we can see that a zip code was provided with letters that isn't able to be translated into an integer.</span></span>  <span data-ttu-id="e003e-160">This appears to be the error in the code that needs to be corrected.</span><span class="sxs-lookup"><span data-stu-id="e003e-160">This appears to be the error in the code that needs to be corrected.</span></span>

    ![Debug snapshot](media/app-insights-tutorial-runtime-exceptions/debug-snapshot-02.png)

5. <span data-ttu-id="e003e-162">To download this snapshot into Visual Studio where we can locate the actual code that needs to be corrected, click **Download Snapshot**.</span><span class="sxs-lookup"><span data-stu-id="e003e-162">To download this snapshot into Visual Studio where we can locate the actual code that needs to be corrected, click **Download Snapshot**.</span></span>
6. <span data-ttu-id="e003e-163">The snapshot is loaded into Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e003e-163">The snapshot is loaded into Visual Studio.</span></span>
7. <span data-ttu-id="e003e-164">You can now run a debug session in Visual Studio that quickly identifies the line of code that caused the exception.</span><span class="sxs-lookup"><span data-stu-id="e003e-164">You can now run a debug session in Visual Studio that quickly identifies the line of code that caused the exception.</span></span>

    ![Exception in code](media/app-insights-tutorial-runtime-exceptions/exception-code.png)


## <a name="use-analytics-data"></a><span data-ttu-id="e003e-166">Use analytics data</span><span class="sxs-lookup"><span data-stu-id="e003e-166">Use analytics data</span></span>
<span data-ttu-id="e003e-167">All data collected by Application Insights is stored in Azure Log Analytics, which provides a rich query language that allows you to analyze the data in a variety of ways.</span><span class="sxs-lookup"><span data-stu-id="e003e-167">All data collected by Application Insights is stored in Azure Log Analytics, which provides a rich query language that allows you to analyze the data in a variety of ways.</span></span>  <span data-ttu-id="e003e-168">We can use this data to analyze the requests that generated the exception we're researching.</span><span class="sxs-lookup"><span data-stu-id="e003e-168">We can use this data to analyze the requests that generated the exception we're researching.</span></span> 

8. <span data-ttu-id="e003e-169">Click the CodeLens information above the code to view telemetry provided by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e003e-169">Click the CodeLens information above the code to view telemetry provided by Application Insights.</span></span>

    ![Code](media/app-insights-tutorial-runtime-exceptions/codelens.png)

9. <span data-ttu-id="e003e-171">Click **Analyze impact** to open Application Insights Analytics.</span><span class="sxs-lookup"><span data-stu-id="e003e-171">Click **Analyze impact** to open Application Insights Analytics.</span></span>  <span data-ttu-id="e003e-172">It's populated with several queries that provide details on failed requests such as impacted users, browsers, and regions.</span><span class="sxs-lookup"><span data-stu-id="e003e-172">It's populated with several queries that provide details on failed requests such as impacted users, browsers, and regions.</span></span><br><br><span data-ttu-id="e003e-173">![Analytics](media/app-insights-tutorial-runtime-exceptions/analytics.png)</span><span class="sxs-lookup"><span data-stu-id="e003e-173">![Analytics](media/app-insights-tutorial-runtime-exceptions/analytics.png)</span></span><br>

## <a name="add-work-item"></a><span data-ttu-id="e003e-174">Add work item</span><span class="sxs-lookup"><span data-stu-id="e003e-174">Add work item</span></span>
<span data-ttu-id="e003e-175">If you connect Application Insights to a tracking system such as Azure DevOps or GitHub, you can create a work item directly from Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e003e-175">If you connect Application Insights to a tracking system such as Azure DevOps or GitHub, you can create a work item directly from Application Insights.</span></span>

1. <span data-ttu-id="e003e-176">Return to the **Exception Properties** panel in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e003e-176">Return to the **Exception Properties** panel in Application Insights.</span></span>
2. <span data-ttu-id="e003e-177">Click **New Work Item**.</span><span class="sxs-lookup"><span data-stu-id="e003e-177">Click **New Work Item**.</span></span>
3. <span data-ttu-id="e003e-178">The **New Work Item** panel opens with details about the exception already populated.</span><span class="sxs-lookup"><span data-stu-id="e003e-178">The **New Work Item** panel opens with details about the exception already populated.</span></span>  <span data-ttu-id="e003e-179">You can add any additional information before saving it.</span><span class="sxs-lookup"><span data-stu-id="e003e-179">You can add any additional information before saving it.</span></span>

    ![New Work Item](media/app-insights-tutorial-runtime-exceptions/new-work-item.png)

## <a name="next-steps"></a><span data-ttu-id="e003e-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="e003e-181">Next steps</span></span>
<span data-ttu-id="e003e-182">Now that you've learned how to identify run-time exceptions, advance to the next tutorial to learn how to identify and diagnose performance issues.</span><span class="sxs-lookup"><span data-stu-id="e003e-182">Now that you've learned how to identify run-time exceptions, advance to the next tutorial to learn how to identify and diagnose performance issues.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e003e-183">Identify performance issues</span><span class="sxs-lookup"><span data-stu-id="e003e-183">Identify performance issues</span></span>](app-insights-tutorial-performance.md)