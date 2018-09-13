---
title: Collect Azure Activity Logs into Log Analytics across subscriptions | Microsoft Docs
description: Use Event Hubs and Logic Apps to collect data from the Azure Activity Log and send it to an Azure Log Analytics workspace in a different tenant.
services: log-analytics, logic-apps, event-hubs
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/26/2018
ms.author: richrund; bwren
ms.component: na
ms.openlocfilehash: c2bb802213d903290a0168623d7e6a302ba0e324
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864619"
---
# <a name="collect-azure-activity-logs-into-log-analytics-across-subscriptions"></a><span data-ttu-id="f06d1-103">Collect Azure Activity Logs into Log Analytics across subscriptions</span><span class="sxs-lookup"><span data-stu-id="f06d1-103">Collect Azure Activity Logs into Log Analytics across subscriptions</span></span>

<span data-ttu-id="f06d1-104">This article steps through a method to collect Azure Activity Logs into a Log Analytics workspace using the Azure Log Analytics Data Collector connector for Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="f06d1-104">This article steps through a method to collect Azure Activity Logs into a Log Analytics workspace using the Azure Log Analytics Data Collector connector for Logic Apps.</span></span> <span data-ttu-id="f06d1-105">Use the process in this article when you need to send logs to a workspace in a different Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f06d1-105">Use the process in this article when you need to send logs to a workspace in a different Azure Active Directory.</span></span> <span data-ttu-id="f06d1-106">For example, if you are a managed service provider, you may want to collect activity logs from a customer's subscription and store them in a Log Analytics workspace in your own subscription.</span><span class="sxs-lookup"><span data-stu-id="f06d1-106">For example, if you are a managed service provider, you may want to collect activity logs from a customer's subscription and store them in a Log Analytics workspace in your own subscription.</span></span>

<span data-ttu-id="f06d1-107">If the Log Analytics workspace is in the same Azure subscription, or in a different subscription but in the same Azure Active Directory, use the steps in the [Azure activity log solution](../log-analytics/log-analytics-activity.md) to collect Azure activity logs.</span><span class="sxs-lookup"><span data-stu-id="f06d1-107">If the Log Analytics workspace is in the same Azure subscription, or in a different subscription but in the same Azure Active Directory, use the steps in the [Azure activity log solution](../log-analytics/log-analytics-activity.md) to collect Azure activity logs.</span></span>

## <a name="overview"></a><span data-ttu-id="f06d1-108">Overview</span><span class="sxs-lookup"><span data-stu-id="f06d1-108">Overview</span></span>

<span data-ttu-id="f06d1-109">The strategy used in this scenario is to have Azure Activity Log send events to an [Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md) where a [Logic App](../logic-apps/logic-apps-overview.md) sends them to your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="f06d1-109">The strategy used in this scenario is to have Azure Activity Log send events to an [Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md) where a [Logic App](../logic-apps/logic-apps-overview.md) sends them to your Log Analytics workspace.</span></span> 

![image of data flow from activity log to log analytics](media/log-analytics-activity-logs-subscriptions/data-flow-overview.png)

<span data-ttu-id="f06d1-111">Advantages of this approach include:</span><span class="sxs-lookup"><span data-stu-id="f06d1-111">Advantages of this approach include:</span></span>
- <span data-ttu-id="f06d1-112">Low latency since the Azure Activity Log is streamed into the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="f06d1-112">Low latency since the Azure Activity Log is streamed into the Event Hub.</span></span>  <span data-ttu-id="f06d1-113">The Logic App is then triggered and posts the data to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f06d1-113">The Logic App is then triggered and posts the data to Log Analytics.</span></span> 
- <span data-ttu-id="f06d1-114">Minimal code is required, and there is no server infrastructure to deploy.</span><span class="sxs-lookup"><span data-stu-id="f06d1-114">Minimal code is required, and there is no server infrastructure to deploy.</span></span>

<span data-ttu-id="f06d1-115">This article steps you through how to:</span><span class="sxs-lookup"><span data-stu-id="f06d1-115">This article steps you through how to:</span></span>
1. <span data-ttu-id="f06d1-116">Create an Event Hub.</span><span class="sxs-lookup"><span data-stu-id="f06d1-116">Create an Event Hub.</span></span> 
2. <span data-ttu-id="f06d1-117">Export activity logs to an Event Hub using Azure Activity Log export profile.</span><span class="sxs-lookup"><span data-stu-id="f06d1-117">Export activity logs to an Event Hub using Azure Activity Log export profile.</span></span>
3. <span data-ttu-id="f06d1-118">Create a Logic App to read from the Event Hub and send events to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f06d1-118">Create a Logic App to read from the Event Hub and send events to Log Analytics.</span></span>

## <a name="requirements"></a><span data-ttu-id="f06d1-119">Requirements</span><span class="sxs-lookup"><span data-stu-id="f06d1-119">Requirements</span></span>
<span data-ttu-id="f06d1-120">Following are the requirements for the Azure resources used in this scenario.</span><span class="sxs-lookup"><span data-stu-id="f06d1-120">Following are the requirements for the Azure resources used in this scenario.</span></span>

- <span data-ttu-id="f06d1-121">The Event Hub namespace does not have to be in the same subscription as the subscription emitting logs.</span><span class="sxs-lookup"><span data-stu-id="f06d1-121">The Event Hub namespace does not have to be in the same subscription as the subscription emitting logs.</span></span> <span data-ttu-id="f06d1-122">The user who configures the setting must have appropriate access permissions to both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="f06d1-122">The user who configures the setting must have appropriate access permissions to both subscriptions.</span></span> <span data-ttu-id="f06d1-123">If you have multiple subscriptions in the same Azure Active directory, you can send the activity logs for all subscriptions to a single event hub.</span><span class="sxs-lookup"><span data-stu-id="f06d1-123">If you have multiple subscriptions in the same Azure Active directory, you can send the activity logs for all subscriptions to a single event hub.</span></span>
- <span data-ttu-id="f06d1-124">The Logic App can be in a different subscription from the event hub and does not need to be in the same Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f06d1-124">The Logic App can be in a different subscription from the event hub and does not need to be in the same Azure Active Directory.</span></span> <span data-ttu-id="f06d1-125">The Logic App reads from the Event Hub using the Event Hub's shared access key.</span><span class="sxs-lookup"><span data-stu-id="f06d1-125">The Logic App reads from the Event Hub using the Event Hub's shared access key.</span></span>
- <span data-ttu-id="f06d1-126">The Log Analytics workspace can be in a different subscription and Azure Active Directory from the Logic App, but for simplicity we recommend that they are in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="f06d1-126">The Log Analytics workspace can be in a different subscription and Azure Active Directory from the Logic App, but for simplicity we recommend that they are in the same subscription.</span></span> <span data-ttu-id="f06d1-127">The Logic App sends to Log Analytics using the Log Analytics workspace ID and key.</span><span class="sxs-lookup"><span data-stu-id="f06d1-127">The Logic App sends to Log Analytics using the Log Analytics workspace ID and key.</span></span>



## <a name="step-1---create-an-event-hub"></a><span data-ttu-id="f06d1-128">Step 1 - Create an Event Hub</span><span class="sxs-lookup"><span data-stu-id="f06d1-128">Step 1 - Create an Event Hub</span></span>

<!-- Follow the steps in [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) to create your event hub. -->

1. <span data-ttu-id="f06d1-129">In the Azure portal, select **Create a resource** > **Internet of Things** > **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-129">In the Azure portal, select **Create a resource** > **Internet of Things** > **Event Hubs**.</span></span>

   ![Marketplace new event hub](media/log-analytics-activity-logs-subscriptions/marketplace-new-event-hub.png)

3. <span data-ttu-id="f06d1-131">Under **Create namespace**, either enter a new namespace or selecting an existing one.</span><span class="sxs-lookup"><span data-stu-id="f06d1-131">Under **Create namespace**, either enter a new namespace or selecting an existing one.</span></span> <span data-ttu-id="f06d1-132">The system immediately checks to see if the name is available.</span><span class="sxs-lookup"><span data-stu-id="f06d1-132">The system immediately checks to see if the name is available.</span></span>

   ![image of create event hub dialog](media/log-analytics-activity-logs-subscriptions/create-event-hub1.png)

4. <span data-ttu-id="f06d1-134">Choose the pricing tier (Basic or Standard), an Azure subscription, resource group, and location for the new resource.</span><span class="sxs-lookup"><span data-stu-id="f06d1-134">Choose the pricing tier (Basic or Standard), an Azure subscription, resource group, and location for the new resource.</span></span>  <span data-ttu-id="f06d1-135">Click **Create** to create the namespace.</span><span class="sxs-lookup"><span data-stu-id="f06d1-135">Click **Create** to create the namespace.</span></span> <span data-ttu-id="f06d1-136">You may have to wait a few minutes for the system to fully provision the resources.</span><span class="sxs-lookup"><span data-stu-id="f06d1-136">You may have to wait a few minutes for the system to fully provision the resources.</span></span>
6. <span data-ttu-id="f06d1-137">Click the namespace you just created from the list.</span><span class="sxs-lookup"><span data-stu-id="f06d1-137">Click the namespace you just created from the list.</span></span>
7. <span data-ttu-id="f06d1-138">Select **Shared access policies**, and then click **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-138">Select **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>

   ![image of event hub shared access policies](media/log-analytics-activity-logs-subscriptions/create-event-hub7.png)
   
8. <span data-ttu-id="f06d1-140">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="f06d1-140">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> 

   ![image of event hub shared access key](media/log-analytics-activity-logs-subscriptions/create-event-hub8.png)

9. <span data-ttu-id="f06d1-142">In a temporary location, such as Notepad, keep a copy the Event Hub name and either the primary or secondary Event Hub connection string.</span><span class="sxs-lookup"><span data-stu-id="f06d1-142">In a temporary location, such as Notepad, keep a copy the Event Hub name and either the primary or secondary Event Hub connection string.</span></span> <span data-ttu-id="f06d1-143">The Logic App requires these values.</span><span class="sxs-lookup"><span data-stu-id="f06d1-143">The Logic App requires these values.</span></span>  <span data-ttu-id="f06d1-144">For the Event Hub connection string, you can use the **RootManageSharedAccessKey** connection string or create a separate one.</span><span class="sxs-lookup"><span data-stu-id="f06d1-144">For the Event Hub connection string, you can use the **RootManageSharedAccessKey** connection string or create a separate one.</span></span>  <span data-ttu-id="f06d1-145">The connection string  you use must start with `Endpoint=sb://` and be for a policy that has the **Manage** access policy.</span><span class="sxs-lookup"><span data-stu-id="f06d1-145">The connection string  you use must start with `Endpoint=sb://` and be for a policy that has the **Manage** access policy.</span></span>


## <a name="step-2---export-activity-logs-to-event-hub"></a><span data-ttu-id="f06d1-146">Step 2 - Export Activity Logs to Event Hub</span><span class="sxs-lookup"><span data-stu-id="f06d1-146">Step 2 - Export Activity Logs to Event Hub</span></span>

<span data-ttu-id="f06d1-147">To enable streaming of the Activity Log, you pick an Event Hub Namespace and a shared access policy for that namespace.</span><span class="sxs-lookup"><span data-stu-id="f06d1-147">To enable streaming of the Activity Log, you pick an Event Hub Namespace and a shared access policy for that namespace.</span></span> <span data-ttu-id="f06d1-148">An Event Hub is created in that namespace when the first new Activity Log event occurs.</span><span class="sxs-lookup"><span data-stu-id="f06d1-148">An Event Hub is created in that namespace when the first new Activity Log event occurs.</span></span> 

<span data-ttu-id="f06d1-149">You can use an event hub namespace that is not in the same subscription as the subscription emitting logs, however the subscriptions must be in the same Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f06d1-149">You can use an event hub namespace that is not in the same subscription as the subscription emitting logs, however the subscriptions must be in the same Azure Active Directory.</span></span> <span data-ttu-id="f06d1-150">The user who configures the setting must have the appropriate RBAC to access both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="f06d1-150">The user who configures the setting must have the appropriate RBAC to access both subscriptions.</span></span> 

1. <span data-ttu-id="f06d1-151">In the Azure portal, select **Monitor** > **Activity Log**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-151">In the Azure portal, select **Monitor** > **Activity Log**.</span></span>
3. <span data-ttu-id="f06d1-152">Click the **Export** button at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="f06d1-152">Click the **Export** button at the top of the page.</span></span>

   ![image of azure monitor in navigation](media/log-analytics-activity-logs-subscriptions/activity-log-blade.png)

4. <span data-ttu-id="f06d1-154">Select the **Subscription** to export from, and then click **Select all** in the **Regions** drop-down to select events for resources in all regions.</span><span class="sxs-lookup"><span data-stu-id="f06d1-154">Select the **Subscription** to export from, and then click **Select all** in the **Regions** drop-down to select events for resources in all regions.</span></span> <span data-ttu-id="f06d1-155">Click the **Export to an event hub** check box.</span><span class="sxs-lookup"><span data-stu-id="f06d1-155">Click the **Export to an event hub** check box.</span></span>
7. <span data-ttu-id="f06d1-156">Click **Service bus namespace**, and then select the **Subscription** with the event hub, the **event hub namespace**, and an **event hub policy name**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-156">Click **Service bus namespace**, and then select the **Subscription** with the event hub, the **event hub namespace**, and an **event hub policy name**.</span></span>

    ![image of export to event hub page](media/log-analytics-activity-logs-subscriptions/export-activity-log2.png)

11. <span data-ttu-id="f06d1-158">Click **OK** and then **Save** to save these settings.</span><span class="sxs-lookup"><span data-stu-id="f06d1-158">Click **OK** and then **Save** to save these settings.</span></span> <span data-ttu-id="f06d1-159">The settings are immediately be applied to your subscription.</span><span class="sxs-lookup"><span data-stu-id="f06d1-159">The settings are immediately be applied to your subscription.</span></span>

<!-- Follow the steps in [stream the Azure Activity Log to Event Hubs](../monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs.md) to configure a log profile that writes activity logs to an event hub. -->

## <a name="step-3---create-logic-app"></a><span data-ttu-id="f06d1-160">Step 3 - Create Logic App</span><span class="sxs-lookup"><span data-stu-id="f06d1-160">Step 3 - Create Logic App</span></span>

<span data-ttu-id="f06d1-161">Once the activity logs are writing to the event hub, you create a Logic App to collect the logs from the event hub and write them to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f06d1-161">Once the activity logs are writing to the event hub, you create a Logic App to collect the logs from the event hub and write them to Log Analytics.</span></span>

<span data-ttu-id="f06d1-162">The Logic App includes the following:</span><span class="sxs-lookup"><span data-stu-id="f06d1-162">The Logic App includes the following:</span></span>
- <span data-ttu-id="f06d1-163">An [Event Hub connector](https://docs.microsoft.com/connectors/eventhubs/) trigger to read from the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="f06d1-163">An [Event Hub connector](https://docs.microsoft.com/connectors/eventhubs/) trigger to read from the Event Hub.</span></span>
- <span data-ttu-id="f06d1-164">A [Parse JSON action](../logic-apps/logic-apps-content-type.md) to extract the JSON events.</span><span class="sxs-lookup"><span data-stu-id="f06d1-164">A [Parse JSON action](../logic-apps/logic-apps-content-type.md) to extract the JSON events.</span></span>
- <span data-ttu-id="f06d1-165">A [Compose action](../logic-apps/logic-apps-workflow-actions-triggers.md#compose-action) to convert the JSON to an object.</span><span class="sxs-lookup"><span data-stu-id="f06d1-165">A [Compose action](../logic-apps/logic-apps-workflow-actions-triggers.md#compose-action) to convert the JSON to an object.</span></span>
- <span data-ttu-id="f06d1-166">A [Log Analytics send data connector](https://docs.microsoft.com/connectors/azureloganalyticsdatacollector/) to post the data to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f06d1-166">A [Log Analytics send data connector](https://docs.microsoft.com/connectors/azureloganalyticsdatacollector/) to post the data to Log Analytics.</span></span>

   ![image of adding event hub trigger in logic apps](media/log-analytics-activity-logs-subscriptions/log-analytics-logic-apps-activity-log-overview.png)

### <a name="logic-app-requirements"></a><span data-ttu-id="f06d1-168">Logic App Requirements</span><span class="sxs-lookup"><span data-stu-id="f06d1-168">Logic App Requirements</span></span>
<span data-ttu-id="f06d1-169">Before creating your Logic App, make sure you have the following information from previous steps:</span><span class="sxs-lookup"><span data-stu-id="f06d1-169">Before creating your Logic App, make sure you have the following information from previous steps:</span></span>
- <span data-ttu-id="f06d1-170">Event Hub name</span><span class="sxs-lookup"><span data-stu-id="f06d1-170">Event Hub name</span></span>
- <span data-ttu-id="f06d1-171">Event Hub connection string (either the primary or secondary) for the Event Hub namespace.</span><span class="sxs-lookup"><span data-stu-id="f06d1-171">Event Hub connection string (either the primary or secondary) for the Event Hub namespace.</span></span>
- <span data-ttu-id="f06d1-172">Log Analytics workspace ID</span><span class="sxs-lookup"><span data-stu-id="f06d1-172">Log Analytics workspace ID</span></span>
- <span data-ttu-id="f06d1-173">Log Analytics shared key</span><span class="sxs-lookup"><span data-stu-id="f06d1-173">Log Analytics shared key</span></span>

<span data-ttu-id="f06d1-174">To get the event Hub name and connection string, follow the steps in [Check Event Hubs namespace permissions and find the connection string](../connectors/connectors-create-api-azure-event-hubs.md#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="f06d1-174">To get the event Hub name and connection string, follow the steps in [Check Event Hubs namespace permissions and find the connection string](../connectors/connectors-create-api-azure-event-hubs.md#permissions-connection-string).</span></span>


### <a name="create-a-new-blank-logic-app"></a><span data-ttu-id="f06d1-175">Create a new blank Logic App</span><span class="sxs-lookup"><span data-stu-id="f06d1-175">Create a new blank Logic App</span></span>

1. <span data-ttu-id="f06d1-176">In the Azure portal, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-176">In the Azure portal, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span></span>

    ![Marketplace new logic app](media/log-analytics-activity-logs-subscriptions/marketplace-new-logic-app.png)

2. <span data-ttu-id="f06d1-178">Enter the settings in the table below.</span><span class="sxs-lookup"><span data-stu-id="f06d1-178">Enter the settings in the table below.</span></span>

    ![Create logic app](media/log-analytics-activity-logs-subscriptions/create-logic-app.png)

   |<span data-ttu-id="f06d1-180">Setting</span><span class="sxs-lookup"><span data-stu-id="f06d1-180">Setting</span></span> | <span data-ttu-id="f06d1-181">Description</span><span class="sxs-lookup"><span data-stu-id="f06d1-181">Description</span></span>  |
   |:---|:---|
   | <span data-ttu-id="f06d1-182">Name</span><span class="sxs-lookup"><span data-stu-id="f06d1-182">Name</span></span>           | <span data-ttu-id="f06d1-183">Unique name for the logic app.</span><span class="sxs-lookup"><span data-stu-id="f06d1-183">Unique name for the logic app.</span></span> |
   | <span data-ttu-id="f06d1-184">Subscription</span><span class="sxs-lookup"><span data-stu-id="f06d1-184">Subscription</span></span>   | <span data-ttu-id="f06d1-185">Select the Azure subscription that will contain the logic app.</span><span class="sxs-lookup"><span data-stu-id="f06d1-185">Select the Azure subscription that will contain the logic app.</span></span> |
   | <span data-ttu-id="f06d1-186">Resource Group</span><span class="sxs-lookup"><span data-stu-id="f06d1-186">Resource Group</span></span> | <span data-ttu-id="f06d1-187">Select an existing Azure resource group or create a new one for the logic app.</span><span class="sxs-lookup"><span data-stu-id="f06d1-187">Select an existing Azure resource group or create a new one for the logic app.</span></span> |
   | <span data-ttu-id="f06d1-188">Location</span><span class="sxs-lookup"><span data-stu-id="f06d1-188">Location</span></span>       | <span data-ttu-id="f06d1-189">Select the datacenter region for deploying your logic app.</span><span class="sxs-lookup"><span data-stu-id="f06d1-189">Select the datacenter region for deploying your logic app.</span></span> |
   | <span data-ttu-id="f06d1-190">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f06d1-190">Log Analytics</span></span>  | <span data-ttu-id="f06d1-191">Select if you want to log the status of each run of your logic app in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f06d1-191">Select if you want to log the status of each run of your logic app in Log Analytics.</span></span>  |

    
3. <span data-ttu-id="f06d1-192">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-192">Select **Create**.</span></span> <span data-ttu-id="f06d1-193">When **Deployment Succeeded** notification displays, click on **Go to resource** to open your Logic App.</span><span class="sxs-lookup"><span data-stu-id="f06d1-193">When **Deployment Succeeded** notification displays, click on **Go to resource** to open your Logic App.</span></span>

4. <span data-ttu-id="f06d1-194">Under **Templates**, choose **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-194">Under **Templates**, choose **Blank Logic App**.</span></span> 

<span data-ttu-id="f06d1-195">The Logic Apps Designer now shows you available connectors and their triggers, which you use for starting your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="f06d1-195">The Logic Apps Designer now shows you available connectors and their triggers, which you use for starting your logic app workflow.</span></span>

<!-- Learn [how to create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md). -->

### <a name="add-event-hub-trigger"></a><span data-ttu-id="f06d1-196">Add Event Hub trigger</span><span class="sxs-lookup"><span data-stu-id="f06d1-196">Add Event Hub trigger</span></span>

1. <span data-ttu-id="f06d1-197">In the search box for the Logic App Designer, type *event hubs* for your filter.</span><span class="sxs-lookup"><span data-stu-id="f06d1-197">In the search box for the Logic App Designer, type *event hubs* for your filter.</span></span> <span data-ttu-id="f06d1-198">Select the trigger **Event Hubs - When events are available in Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-198">Select the trigger **Event Hubs - When events are available in Event Hub**.</span></span>

   ![image of adding event hub trigger in logic apps](media/log-analytics-activity-logs-subscriptions/logic-apps-event-hub-add-trigger.png)

2. <span data-ttu-id="f06d1-200">When you're prompted for credentials, connect to your Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="f06d1-200">When you're prompted for credentials, connect to your Event Hubs namespace.</span></span> <span data-ttu-id="f06d1-201">Enter a name for your connection and then the connection string that you copied.</span><span class="sxs-lookup"><span data-stu-id="f06d1-201">Enter a name for your connection and then the connection string that you copied.</span></span>  <span data-ttu-id="f06d1-202">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-202">Select **Create**.</span></span>

   ![image of adding event hub connection in logic apps](media/log-analytics-activity-logs-subscriptions/logic-apps-event-hub-add-connection.png)

3. <span data-ttu-id="f06d1-204">After you create the connection, edit the settings for the trigger.</span><span class="sxs-lookup"><span data-stu-id="f06d1-204">After you create the connection, edit the settings for the trigger.</span></span> <span data-ttu-id="f06d1-205">Start by selecting **insights-operational-logs** from the **Event Hub name** drop-down.</span><span class="sxs-lookup"><span data-stu-id="f06d1-205">Start by selecting **insights-operational-logs** from the **Event Hub name** drop-down.</span></span>

   ![When events are available dialog](media/log-analytics-activity-logs-subscriptions/logic-apps-event-hub-read-events.png)

5. <span data-ttu-id="f06d1-207">Expand **Show advanced options** and change **Content type** to *application/json*</span><span class="sxs-lookup"><span data-stu-id="f06d1-207">Expand **Show advanced options** and change **Content type** to *application/json*</span></span>

   ![Event hub configuration dialog](media/log-analytics-activity-logs-subscriptions/logic-apps-event-hub-configuration.png)

### <a name="add-parse-json-action"></a><span data-ttu-id="f06d1-209">Add Parse JSON action</span><span class="sxs-lookup"><span data-stu-id="f06d1-209">Add Parse JSON action</span></span>

<span data-ttu-id="f06d1-210">The output from the Event Hub contains a JSON payload with an array of records.</span><span class="sxs-lookup"><span data-stu-id="f06d1-210">The output from the Event Hub contains a JSON payload with an array of records.</span></span> <span data-ttu-id="f06d1-211">The [Parse JSON](../logic-apps/logic-apps-content-type.md) action is used to extract just the array of records for sending to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f06d1-211">The [Parse JSON](../logic-apps/logic-apps-content-type.md) action is used to extract just the array of records for sending to Log Analytics.</span></span>

1. <span data-ttu-id="f06d1-212">Click **New step** > **Add an action**</span><span class="sxs-lookup"><span data-stu-id="f06d1-212">Click **New step** > **Add an action**</span></span>
2. <span data-ttu-id="f06d1-213">In the search box, type *parse json* for your filter.</span><span class="sxs-lookup"><span data-stu-id="f06d1-213">In the search box, type *parse json* for your filter.</span></span> <span data-ttu-id="f06d1-214">Select the action **Data Operations - Parse JSON**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-214">Select the action **Data Operations - Parse JSON**.</span></span>

   ![Adding parse json action in logic apps](media/log-analytics-activity-logs-subscriptions/logic-apps-add-parse-json-action.png)

3. <span data-ttu-id="f06d1-216">Click in the **Content** field and then select *Body*.</span><span class="sxs-lookup"><span data-stu-id="f06d1-216">Click in the **Content** field and then select *Body*.</span></span>

4. <span data-ttu-id="f06d1-217">Copy and paste the following schema into the **Schema** field.</span><span class="sxs-lookup"><span data-stu-id="f06d1-217">Copy and paste the following schema into the **Schema** field.</span></span>  <span data-ttu-id="f06d1-218">This schema matches the output from the Event Hub action.</span><span class="sxs-lookup"><span data-stu-id="f06d1-218">This schema matches the output from the Event Hub action.</span></span>  

   ![Parse json dialog](media/log-analytics-activity-logs-subscriptions/logic-apps-parse-json-configuration.png)

``` json-schema
{
    "properties": {
        "body": {
            "properties": {
                "ContentData": {
                    "type": "string"
                },
                "Properties": {
                    "properties": {
                        "ProfileName": {
                            "type": "string"
                        },
                        "x-opt-enqueued-time": {
                            "type": "string"
                        },
                        "x-opt-offset": {
                            "type": "string"
                        },
                        "x-opt-sequence-number": {
                            "type": "number"
                        }
                    },
                    "type": "object"
                },
                "SystemProperties": {
                    "properties": {
                        "EnqueuedTimeUtc": {
                            "type": "string"
                        },
                        "Offset": {
                            "type": "string"
                        },
                        "PartitionKey": {},
                        "SequenceNumber": {
                            "type": "number"
                        }
                    },
                    "type": "object"
                }
            },
            "type": "object"
        },
        "headers": {
            "properties": {
                "Cache-Control": {
                    "type": "string"
                },
                "Content-Length": {
                    "type": "string"
                },
                "Content-Type": {
                    "type": "string"
                },
                "Date": {
                    "type": "string"
                },
                "Expires": {
                    "type": "string"
                },
                "Location": {
                    "type": "string"
                },
                "Pragma": {
                    "type": "string"
                },
                "Retry-After": {
                    "type": "string"
                },
                "Timing-Allow-Origin": {
                    "type": "string"
                },
                "Transfer-Encoding": {
                    "type": "string"
                },
                "Vary": {
                    "type": "string"
                },
                "X-AspNet-Version": {
                    "type": "string"
                },
                "X-Powered-By": {
                    "type": "string"
                },
                "x-ms-request-id": {
                    "type": "string"
                }
            },
            "type": "object"
        }
    },
    "type": "object"
}
```

>[!TIP]
> <span data-ttu-id="f06d1-220">You can get a sample payload by clicking **Run** and looking at the **Raw Output** from the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="f06d1-220">You can get a sample payload by clicking **Run** and looking at the **Raw Output** from the Event Hub.</span></span>  <span data-ttu-id="f06d1-221">You can then use this output with **Use sample payload to generate schema** in the **Parse JSON** activity to generate the schema.</span><span class="sxs-lookup"><span data-stu-id="f06d1-221">You can then use this output with **Use sample payload to generate schema** in the **Parse JSON** activity to generate the schema.</span></span>

### <a name="add-compose-action"></a><span data-ttu-id="f06d1-222">Add Compose action</span><span class="sxs-lookup"><span data-stu-id="f06d1-222">Add Compose action</span></span>
<span data-ttu-id="f06d1-223">The [Compose](../logic-apps/logic-apps-workflow-actions-triggers.md#compose-action) action takes the JSON output and creates an object that can be used by the Log Analytics action.</span><span class="sxs-lookup"><span data-stu-id="f06d1-223">The [Compose](../logic-apps/logic-apps-workflow-actions-triggers.md#compose-action) action takes the JSON output and creates an object that can be used by the Log Analytics action.</span></span>

1. <span data-ttu-id="f06d1-224">Click **New step** > **Add an action**</span><span class="sxs-lookup"><span data-stu-id="f06d1-224">Click **New step** > **Add an action**</span></span>
2. <span data-ttu-id="f06d1-225">Type *compose* for your filter and then select the action **Data Operations - Compose**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-225">Type *compose* for your filter and then select the action **Data Operations - Compose**.</span></span>

    ![Add Compose action](media/log-analytics-activity-logs-subscriptions/logic-apps-add-compose-action.png)

3. <span data-ttu-id="f06d1-227">Click the **Inputs** field and select **Body** under the **Parse JSON** activity.</span><span class="sxs-lookup"><span data-stu-id="f06d1-227">Click the **Inputs** field and select **Body** under the **Parse JSON** activity.</span></span>


### <a name="add-log-analytics-send-data-action"></a><span data-ttu-id="f06d1-228">Add Log Analytics Send Data action</span><span class="sxs-lookup"><span data-stu-id="f06d1-228">Add Log Analytics Send Data action</span></span>
<span data-ttu-id="f06d1-229">The [Azure Log Analytics Data Collector](https://docs.microsoft.com/connectors/azureloganalyticsdatacollector/) action takes the object from the Compose action and sends it to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f06d1-229">The [Azure Log Analytics Data Collector](https://docs.microsoft.com/connectors/azureloganalyticsdatacollector/) action takes the object from the Compose action and sends it to Log Analytics.</span></span>

1. <span data-ttu-id="f06d1-230">Click **New step** > **Add an action**</span><span class="sxs-lookup"><span data-stu-id="f06d1-230">Click **New step** > **Add an action**</span></span>
2. <span data-ttu-id="f06d1-231">Type *log analytics* for your filter and then select the action **Azure Log Analytics Data Collector - Send Data**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-231">Type *log analytics* for your filter and then select the action **Azure Log Analytics Data Collector - Send Data**.</span></span>

   ![Adding log analytics send data action in logic apps](media/log-analytics-activity-logs-subscriptions/logic-apps-send-data-to-log-analytics-connector.png)

3. <span data-ttu-id="f06d1-233">Enter a name for your connection and paste in the **Workspace ID** and **Workspace Key** for your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="f06d1-233">Enter a name for your connection and paste in the **Workspace ID** and **Workspace Key** for your Log Analytics workspace.</span></span>  <span data-ttu-id="f06d1-234">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-234">Click **Create**.</span></span>

   ![Adding log analytics connection in logic apps](media/log-analytics-activity-logs-subscriptions/logic-apps-log-analytics-add-connection.png)

4. <span data-ttu-id="f06d1-236">After you create the connection, edit the settings in the table below.</span><span class="sxs-lookup"><span data-stu-id="f06d1-236">After you create the connection, edit the settings in the table below.</span></span> 

    ![Configure send data action](media/log-analytics-activity-logs-subscriptions/logic-apps-send-data-to-log-analytics-configuration.png)

   |<span data-ttu-id="f06d1-238">Setting</span><span class="sxs-lookup"><span data-stu-id="f06d1-238">Setting</span></span>        | <span data-ttu-id="f06d1-239">Value</span><span class="sxs-lookup"><span data-stu-id="f06d1-239">Value</span></span>           | <span data-ttu-id="f06d1-240">Description</span><span class="sxs-lookup"><span data-stu-id="f06d1-240">Description</span></span>  |
   |---------------|---------------------------|--------------|
   |<span data-ttu-id="f06d1-241">JSON Request body</span><span class="sxs-lookup"><span data-stu-id="f06d1-241">JSON Request body</span></span>  | <span data-ttu-id="f06d1-242">**Output** from the **Compose** action</span><span class="sxs-lookup"><span data-stu-id="f06d1-242">**Output** from the **Compose** action</span></span> | <span data-ttu-id="f06d1-243">Retrieves the records from the body of the Compose action.</span><span class="sxs-lookup"><span data-stu-id="f06d1-243">Retrieves the records from the body of the Compose action.</span></span> |
   | <span data-ttu-id="f06d1-244">Custom Log Name</span><span class="sxs-lookup"><span data-stu-id="f06d1-244">Custom Log Name</span></span> | <span data-ttu-id="f06d1-245">AzureActivity</span><span class="sxs-lookup"><span data-stu-id="f06d1-245">AzureActivity</span></span> | <span data-ttu-id="f06d1-246">Name of the custom log table to create in Log Analytics to hold the imported data.</span><span class="sxs-lookup"><span data-stu-id="f06d1-246">Name of the custom log table to create in Log Analytics to hold the imported data.</span></span> |
   | <span data-ttu-id="f06d1-247">Time-generated-field</span><span class="sxs-lookup"><span data-stu-id="f06d1-247">Time-generated-field</span></span> | <span data-ttu-id="f06d1-248">time</span><span class="sxs-lookup"><span data-stu-id="f06d1-248">time</span></span> | <span data-ttu-id="f06d1-249">Don't select the JSON field for **time** - just type the word time.</span><span class="sxs-lookup"><span data-stu-id="f06d1-249">Don't select the JSON field for **time** - just type the word time.</span></span> <span data-ttu-id="f06d1-250">If you select the JSON field the designer puts the **Send Data** action into a *For Each* loop, which is not what you want.</span><span class="sxs-lookup"><span data-stu-id="f06d1-250">If you select the JSON field the designer puts the **Send Data** action into a *For Each* loop, which is not what you want.</span></span> |




10. <span data-ttu-id="f06d1-251">Click **Save** to save the changes you've made to your Logic App.</span><span class="sxs-lookup"><span data-stu-id="f06d1-251">Click **Save** to save the changes you've made to your Logic App.</span></span>

## <a name="step-4---test-and-troubleshoot-the-logic-app"></a><span data-ttu-id="f06d1-252">Step 4 - Test and troubleshoot the Logic App</span><span class="sxs-lookup"><span data-stu-id="f06d1-252">Step 4 - Test and troubleshoot the Logic App</span></span>
<span data-ttu-id="f06d1-253">With the workflow complete, you can test in the designer to verify that it's working without error.</span><span class="sxs-lookup"><span data-stu-id="f06d1-253">With the workflow complete, you can test in the designer to verify that it's working without error.</span></span>

<span data-ttu-id="f06d1-254">In the Logic App Designer, click **Run** to test the Logic App.</span><span class="sxs-lookup"><span data-stu-id="f06d1-254">In the Logic App Designer, click **Run** to test the Logic App.</span></span> <span data-ttu-id="f06d1-255">Each step in the Logic App shows a status icon, with a white check mark in a green circle indicating success.</span><span class="sxs-lookup"><span data-stu-id="f06d1-255">Each step in the Logic App shows a status icon, with a white check mark in a green circle indicating success.</span></span>

   ![Test logic app](media/log-analytics-activity-logs-subscriptions/test-logic-app.png)

<span data-ttu-id="f06d1-257">To see detailed information on each step, click on the step name to expand it.</span><span class="sxs-lookup"><span data-stu-id="f06d1-257">To see detailed information on each step, click on the step name to expand it.</span></span> <span data-ttu-id="f06d1-258">Click on **Show raw inputs** and **Show raw outputs** to see more information on the data received and sent at each step.</span><span class="sxs-lookup"><span data-stu-id="f06d1-258">Click on **Show raw inputs** and **Show raw outputs** to see more information on the data received and sent at each step.</span></span>

## <a name="step-5---view-azure-activity-log-in-log-analytics"></a><span data-ttu-id="f06d1-259">Step 5 - View Azure Activity Log in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f06d1-259">Step 5 - View Azure Activity Log in Log Analytics</span></span>
<span data-ttu-id="f06d1-260">The final step is to check the Log Analytics workspace to make sure that data is being collected as expected.</span><span class="sxs-lookup"><span data-stu-id="f06d1-260">The final step is to check the Log Analytics workspace to make sure that data is being collected as expected.</span></span>

1. <span data-ttu-id="f06d1-261">In the Azure portal, click **All services** found in the upper left-hand corner.</span><span class="sxs-lookup"><span data-stu-id="f06d1-261">In the Azure portal, click **All services** found in the upper left-hand corner.</span></span> <span data-ttu-id="f06d1-262">In the list of resources, type **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-262">In the list of resources, type **Log Analytics**.</span></span> <span data-ttu-id="f06d1-263">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="f06d1-263">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="f06d1-264">Select **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f06d1-264">Select **Log Analytics**.</span></span>
2. <span data-ttu-id="f06d1-265">In your list of Log Analytics workspaces, select your workspace.</span><span class="sxs-lookup"><span data-stu-id="f06d1-265">In your list of Log Analytics workspaces, select your workspace.</span></span>
3.  <span data-ttu-id="f06d1-266">Click the **Log Search** tile and on the Log Search pane, in the query field type `AzureActivity_CL` and then hit enter or click the search button to the right of the query field.</span><span class="sxs-lookup"><span data-stu-id="f06d1-266">Click the **Log Search** tile and on the Log Search pane, in the query field type `AzureActivity_CL` and then hit enter or click the search button to the right of the query field.</span></span> <span data-ttu-id="f06d1-267">If you didn't name your custom log *AzureActivity*, type the name you chose and append `_CL`.</span><span class="sxs-lookup"><span data-stu-id="f06d1-267">If you didn't name your custom log *AzureActivity*, type the name you chose and append `_CL`.</span></span>

>[!NOTE]
> <span data-ttu-id="f06d1-268">The first time a new custom log is sent to Log Analytics it may take up to an hour for the custom log to be searchable.</span><span class="sxs-lookup"><span data-stu-id="f06d1-268">The first time a new custom log is sent to Log Analytics it may take up to an hour for the custom log to be searchable.</span></span>

>[!NOTE]
> <span data-ttu-id="f06d1-269">The activity logs are written to a custom table and do not appear in the [Activity Log solution](./log-analytics-activity.md).</span><span class="sxs-lookup"><span data-stu-id="f06d1-269">The activity logs are written to a custom table and do not appear in the [Activity Log solution](./log-analytics-activity.md).</span></span>


![Test logic app](media/log-analytics-activity-logs-subscriptions/log-analytics-results.png)

## <a name="next-steps"></a><span data-ttu-id="f06d1-271">Next steps</span><span class="sxs-lookup"><span data-stu-id="f06d1-271">Next steps</span></span>

<span data-ttu-id="f06d1-272">In this article, you’ve created a logic app to read Azure Activity Logs from an Event Hub and send them to Log Analytics for analysis.</span><span class="sxs-lookup"><span data-stu-id="f06d1-272">In this article, you’ve created a logic app to read Azure Activity Logs from an Event Hub and send them to Log Analytics for analysis.</span></span> <span data-ttu-id="f06d1-273">To learn more about visualizing data in Log Analytics, including creating dashboards, review the tutorial for Visualize data.</span><span class="sxs-lookup"><span data-stu-id="f06d1-273">To learn more about visualizing data in Log Analytics, including creating dashboards, review the tutorial for Visualize data.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f06d1-274">Visualize Log Search data tutorial</span><span class="sxs-lookup"><span data-stu-id="f06d1-274">Visualize Log Search data tutorial</span></span>](./log-analytics-tutorial-dashboards.md)
