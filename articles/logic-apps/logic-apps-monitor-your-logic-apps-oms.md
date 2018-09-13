---
title: Monitor logic app runs with Log Analytics - Azure Logic Apps | Microsoft Docs
description: Get insights and debugging data about your logic app runs with Log Analytics for troubleshooting and diagnostics
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.date: 06/19/2018
ms.openlocfilehash: 1aa55728b222c2838026cf5b06175736c5c84194
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856236"
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-log-analytics"></a><span data-ttu-id="a6bc7-103">Monitor and get insights about logic app runs with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a6bc7-103">Monitor and get insights about logic app runs with Log Analytics</span></span>

<span data-ttu-id="a6bc7-104">For monitoring and richer debugging information, you can turn on Log Analytics at the same time when you create a logic app.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-104">For monitoring and richer debugging information, you can turn on Log Analytics at the same time when you create a logic app.</span></span> <span data-ttu-id="a6bc7-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through the Azure portal.</span></span> <span data-ttu-id="a6bc7-106">When you add the Logic Apps Management solution, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-106">When you add the Logic Apps Management solution, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="a6bc7-107">This article shows how to turn on Log Analytics so you can view runtime events and data for your logic app run.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-107">This article shows how to turn on Log Analytics so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="a6bc7-108">To monitor your existing logic apps, follow these steps to [turn on diagnostic logging and send logic app runtime data to Log Analytics](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="a6bc7-108">To monitor your existing logic apps, follow these steps to [turn on diagnostic logging and send logic app runtime data to Log Analytics](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="a6bc7-109">Requirements</span><span class="sxs-lookup"><span data-stu-id="a6bc7-109">Requirements</span></span>

<span data-ttu-id="a6bc7-110">Before you start, you need to have a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-110">Before you start, you need to have a Log Analytics workspace.</span></span> <span data-ttu-id="a6bc7-111">Learn [how to create a Log Analytics workspace](../log-analytics/log-analytics-quick-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="a6bc7-111">Learn [how to create a Log Analytics workspace](../log-analytics/log-analytics-quick-create-workspace.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="a6bc7-112">Turn on diagnostics logging when creating logic apps</span><span class="sxs-lookup"><span data-stu-id="a6bc7-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="a6bc7-113">In [Azure portal](https://portal.azure.com), create a logic app.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="a6bc7-114">Choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-114">Choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span></span>

   ![Create a logic app](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="a6bc7-116">In the **Create logic app** page, perform these tasks as shown:</span><span class="sxs-lookup"><span data-stu-id="a6bc7-116">In the **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="a6bc7-117">Provide a name for your logic app and select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="a6bc7-118">Create or select an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="a6bc7-119">Set **Log Analytics** to **On**.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-119">Set **Log Analytics** to **On**.</span></span> 
   <span data-ttu-id="a6bc7-120">Select the Log Analytics workspace where you want to send data for your logic app runs.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-120">Select the Log Analytics workspace where you want to send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="a6bc7-121">When you're ready, choose **Pin to dashboard** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-121">When you're ready, choose **Pin to dashboard** > **Create**.</span></span>

      ![Create logic app](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="a6bc7-123">After you finish this step, Azure creates your logic app, which is now associated with your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-123">After you finish this step, Azure creates your logic app, which is now associated with your Log Analytics workspace.</span></span> 
      <span data-ttu-id="a6bc7-124">Also, this step also automatically installs the Logic Apps Management solution in your workspace.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-124">Also, this step also automatically installs the Logic Apps Management solution in your workspace.</span></span>

3. <span data-ttu-id="a6bc7-125">To view your logic app runs, [continue with these steps](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="a6bc7-125">To view your logic app runs, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-the-logic-apps-management-solution"></a><span data-ttu-id="a6bc7-126">Install the Logic Apps Management solution</span><span class="sxs-lookup"><span data-stu-id="a6bc7-126">Install the Logic Apps Management solution</span></span>

<span data-ttu-id="a6bc7-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="a6bc7-128">You already have the Logic Apps Management solution installed.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-128">You already have the Logic Apps Management solution installed.</span></span>

1. <span data-ttu-id="a6bc7-129">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-129">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="a6bc7-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span><span class="sxs-lookup"><span data-stu-id="a6bc7-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Choose "Log Analytics"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="a6bc7-132">Under **Log Analytics**, find and select your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-132">Under **Log Analytics**, find and select your Log Analytics workspace.</span></span> 

   ![Select your Log Analytics workspace](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="a6bc7-134">Under **Management**, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-134">Under **Management**, choose **Overview**.</span></span>

   ![Choose "OMS Portal"](media/logic-apps-monitor-your-logic-apps-oms/ibiza-portal-page.png)

4. <span data-ttu-id="a6bc7-136">On the Overview page, choose **Add** to open the Management Solutions tile.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-136">On the Overview page, choose **Add** to open the Management Solutions tile.</span></span> 

   ![Choose "Logic Apps Management"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

5. <span data-ttu-id="a6bc7-138">Scroll through the list of **Management Solutions**, choose **Logic Apps Management** solution, and choose **Create** to install it to the Overview page.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-138">Scroll through the list of **Management Solutions**, choose **Logic Apps Management** solution, and choose **Create** to install it to the Overview page.</span></span>

   ![Choose "Add" for "Logic Apps Management"](media/logic-apps-monitor-your-logic-apps-oms/create-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-log-analytics-workspace"></a><span data-ttu-id="a6bc7-140">View your logic app runs in your Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="a6bc7-140">View your logic app runs in your Log Analytics workspace</span></span>

1. <span data-ttu-id="a6bc7-141">To view the count and status for your logic app runs, go to the overview page for your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-141">To view the count and status for your logic app runs, go to the overview page for your Log Analytics workspace.</span></span> <span data-ttu-id="a6bc7-142">Review the details on the **Logic Apps Management** tile.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-142">Review the details on the **Logic Apps Management** tile.</span></span>

   ![Overview tile showing logic app run count and status](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

2. <span data-ttu-id="a6bc7-144">To view a summary with more details about your logic app runs, choose the **Logic Apps Management** tile.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-144">To view a summary with more details about your logic app runs, choose the **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="a6bc7-145">Here, your logic app runs are grouped by name or by execution status.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-145">Here, your logic app runs are grouped by name or by execution status.</span></span> <span data-ttu-id="a6bc7-146">You can also see details about the failures in actions or triggers for the logic app runs.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-146">You can also see details about the failures in actions or triggers for the logic app runs.</span></span>

   ![Status summary for your logic app runs](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="a6bc7-148">To view all the runs for a specific logic app or status, select the row for a logic app or a status.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-148">To view all the runs for a specific logic app or status, select the row for a logic app or a status.</span></span>

   <span data-ttu-id="a6bc7-149">Here is an example that shows all the runs for a specific logic app:</span><span class="sxs-lookup"><span data-stu-id="a6bc7-149">Here is an example that shows all the runs for a specific logic app:</span></span>

   ![View runs for a logic app or a status](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   <span data-ttu-id="a6bc7-151">There are two advanced options on this page:</span><span class="sxs-lookup"><span data-stu-id="a6bc7-151">There are two advanced options on this page:</span></span>
   * <span data-ttu-id="a6bc7-152">**Tracked properties:** This column shows tracked properties, which are grouped by actions, for the logic app.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-152">**Tracked properties:** This column shows tracked properties, which are grouped by actions, for the logic app.</span></span> <span data-ttu-id="a6bc7-153">To view the tracked properties, choose **View**.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-153">To view the tracked properties, choose **View**.</span></span> <span data-ttu-id="a6bc7-154">You can search the tracked properties by using the column filter.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-154">You can search the tracked properties by using the column filter.</span></span>
   
     ![View tracked properties for a logic app](media/logic-apps-monitor-your-logic-apps-oms/logic-app-tracked-properties.png)

     <span data-ttu-id="a6bc7-156">Any newly added tracked properties might take 10-15 minutes before they appear first time.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-156">Any newly added tracked properties might take 10-15 minutes before they appear first time.</span></span> <span data-ttu-id="a6bc7-157">Learn [how to add tracked properties to your logic app](logic-apps-monitor-your-logic-apps.md#azure-diagnostics-event-settings-and-details).</span><span class="sxs-lookup"><span data-stu-id="a6bc7-157">Learn [how to add tracked properties to your logic app](logic-apps-monitor-your-logic-apps.md#azure-diagnostics-event-settings-and-details).</span></span>

   * <span data-ttu-id="a6bc7-158">**Resubmit:** You can resubmit one or more logic app runs that failed, succeeded, or are still running.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-158">**Resubmit:** You can resubmit one or more logic app runs that failed, succeeded, or are still running.</span></span> <span data-ttu-id="a6bc7-159">Select the checkboxes for the runs that you want to resubmit, and choose **Resubmit**.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-159">Select the checkboxes for the runs that you want to resubmit, and choose **Resubmit**.</span></span> 

     ![Resubmit logic app runs](media/logic-apps-monitor-your-logic-apps-oms/logic-app-resubmit.png)

4. <span data-ttu-id="a6bc7-161">To filter these results, you can perform both client-side and server-side filtering.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-161">To filter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="a6bc7-162">Client-side filter: For each column, choose the filters that you want.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-162">Client-side filter: For each column, choose the filters that you want.</span></span> 
   <span data-ttu-id="a6bc7-163">Here are some examples:</span><span class="sxs-lookup"><span data-stu-id="a6bc7-163">Here are some examples:</span></span>

     ![Example column filters](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="a6bc7-165">Server-side filter: To choose a specific time window or to limit the number of runs that appear, use the scope control at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-165">Server-side filter: To choose a specific time window or to limit the number of runs that appear, use the scope control at the top of the page.</span></span> 
   <span data-ttu-id="a6bc7-166">By default, only 1,000 records appear at a time.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-166">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Change the time window](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="a6bc7-168">To view all the actions and their details for a specific run, select a row for a logic app run.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-168">To view all the actions and their details for a specific run, select a row for a logic app run.</span></span>

   <span data-ttu-id="a6bc7-169">Here is an example that shows all the actions for a specific logic app run:</span><span class="sxs-lookup"><span data-stu-id="a6bc7-169">Here is an example that shows all the actions for a specific logic app run:</span></span>

   ![View actions for a logic app run](media/logic-apps-monitor-your-logic-apps-oms/logic-app-action-details.png)
   
6. <span data-ttu-id="a6bc7-171">On any results page, to view the query behind the results or to see all results, choose **See All**, which opens the Log Search page.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-171">On any results page, to view the query behind the results or to see all results, choose **See All**, which opens the Log Search page.</span></span>
   
   ![See All on Results pages](media/logic-apps-monitor-your-logic-apps-oms/logic-app-seeall.png)
   
   <span data-ttu-id="a6bc7-173">On the Log Search page,</span><span class="sxs-lookup"><span data-stu-id="a6bc7-173">On the Log Search page,</span></span>
   * <span data-ttu-id="a6bc7-174">To view the query results in a table, choose **Table**.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-174">To view the query results in a table, choose **Table**.</span></span>
   * <span data-ttu-id="a6bc7-175">To change the query, you can edit the query string in the search bar.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-175">To change the query, you can edit the query string in the search bar.</span></span> 
   <span data-ttu-id="a6bc7-176">For a better experience, choose **Advanced Analytics**.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-176">For a better experience, choose **Advanced Analytics**.</span></span>

     ![View actions and details for a logic app run](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)
     
     <span data-ttu-id="a6bc7-178">Here on the Azure Log Analytics page, you can update queries and view the results from the table.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-178">Here on the Azure Log Analytics page, you can update queries and view the results from the table.</span></span> 
     <span data-ttu-id="a6bc7-179">This query uses [Kusto query language](https://docs.loganalytics.io/docs/Language-Reference), which you can edit if you want to view different results.</span><span class="sxs-lookup"><span data-stu-id="a6bc7-179">This query uses [Kusto query language](https://docs.loganalytics.io/docs/Language-Reference), which you can edit if you want to view different results.</span></span> 

     ![Azure Log Analytics - query view](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="a6bc7-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6bc7-181">Next steps</span></span>

* [<span data-ttu-id="a6bc7-182">Monitor B2B messages</span><span class="sxs-lookup"><span data-stu-id="a6bc7-182">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)

