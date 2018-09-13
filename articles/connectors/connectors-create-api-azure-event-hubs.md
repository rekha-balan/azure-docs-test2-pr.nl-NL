---
title: Connect to Azure Event Hubs - Azure Logic Apps | Microsoft Docs
description: Manage and monitor events with Azure Event Hubs and Azure Logic Apps
author: ecfan
manager: jeconnoc
ms.author: estfan
ms.date: 05/21/2018
ms.topic: article
ms.service: logic-apps
services: logic-apps
ms.reviewer: klam, LADocs
ms.suite: integration
tags: connectors
ms.openlocfilehash: 86fc1c3542bea1be840041bb73df15631c066c7e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824439"
---
# <a name="monitor-receive-and-send-events-with-azure-event-hubs-and-azure-logic-apps"></a><span data-ttu-id="96eb6-103">Monitor, receive, and send events with Azure Event Hubs and Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="96eb6-103">Monitor, receive, and send events with Azure Event Hubs and Azure Logic Apps</span></span> 

<span data-ttu-id="96eb6-104">This article shows how you can monitor and manage events sent to [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) from inside a logic app with the Azure Event Hubs connector.</span><span class="sxs-lookup"><span data-stu-id="96eb6-104">This article shows how you can monitor and manage events sent to [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) from inside a logic app with the Azure Event Hubs connector.</span></span> <span data-ttu-id="96eb6-105">That way, you can create logic apps that automate tasks and workflows for checking, sending, and receiving events from your Event Hub.</span><span class="sxs-lookup"><span data-stu-id="96eb6-105">That way, you can create logic apps that automate tasks and workflows for checking, sending, and receiving events from your Event Hub.</span></span> 

<span data-ttu-id="96eb6-106">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="96eb6-106">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> <span data-ttu-id="96eb6-107">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="96eb6-107">If you're new to logic apps, review [What is Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Quickstart: Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>
<span data-ttu-id="96eb6-108">For connector-specific technical information, see the <a href="https://docs.microsoft.com/connectors/eventhubs/" target="blank">Azure Event Hubs connector reference</a>.</span><span class="sxs-lookup"><span data-stu-id="96eb6-108">For connector-specific technical information, see the <a href="https://docs.microsoft.com/connectors/eventhubs/" target="blank">Azure Event Hubs connector reference</a>.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96eb6-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="96eb6-109">Prerequisites</span></span>

* <span data-ttu-id="96eb6-110">An [Azure Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="96eb6-110">An [Azure Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md)</span></span>

* <span data-ttu-id="96eb6-111">The logic app where you want to access your Event Hub.</span><span class="sxs-lookup"><span data-stu-id="96eb6-111">The logic app where you want to access your Event Hub.</span></span> <span data-ttu-id="96eb6-112">To start your logic app with an Azure Event Hubs trigger, you need a [blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="96eb6-112">To start your logic app with an Azure Event Hubs trigger, you need a [blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> 

<a name="permissions-connection-string"></a>

## <a name="check-permissions-and-get-connection-string"></a><span data-ttu-id="96eb6-113">Check permissions and get connection string</span><span class="sxs-lookup"><span data-stu-id="96eb6-113">Check permissions and get connection string</span></span>

<span data-ttu-id="96eb6-114">For your logic app to access your Event Hub, check your permissions and get the connection string for your Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="96eb6-114">For your logic app to access your Event Hub, check your permissions and get the connection string for your Event Hubs namespace.</span></span>

1. <span data-ttu-id="96eb6-115">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span><span class="sxs-lookup"><span data-stu-id="96eb6-115">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span> 

2. <span data-ttu-id="96eb6-116">Go to your Event Hubs *namespace*, not a specific Event Hub.</span><span class="sxs-lookup"><span data-stu-id="96eb6-116">Go to your Event Hubs *namespace*, not a specific Event Hub.</span></span> <span data-ttu-id="96eb6-117">On the namespace page, under **Settings**, choose **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="96eb6-117">On the namespace page, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="96eb6-118">Under **Claims**, check that you have **Manage** permissions for that namespace.</span><span class="sxs-lookup"><span data-stu-id="96eb6-118">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

   ![Manage permissions for your Event Hub namespace](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3. <span data-ttu-id="96eb6-120">If you want to later manually enter your connection information, get the connection string for your Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="96eb6-120">If you want to later manually enter your connection information, get the connection string for your Event Hubs namespace.</span></span> 

   1. <span data-ttu-id="96eb6-121">Under **Policy**, choose **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="96eb6-121">Under **Policy**, choose **RootManageSharedAccessKey**.</span></span> 

   2. <span data-ttu-id="96eb6-122">Find your primary key's connection string.</span><span class="sxs-lookup"><span data-stu-id="96eb6-122">Find your primary key's connection string.</span></span> <span data-ttu-id="96eb6-123">Choose the copy button, and save the connection string for later use.</span><span class="sxs-lookup"><span data-stu-id="96eb6-123">Choose the copy button, and save the connection string for later use.</span></span>

      ![Copy Event Hubs namespace connection string](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

      > [!TIP]
      > <span data-ttu-id="96eb6-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific event hub, make sure the connection string doesn't have the `EntityPath` parameter.</span><span class="sxs-lookup"><span data-stu-id="96eb6-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific event hub, make sure the connection string doesn't have the `EntityPath` parameter.</span></span> <span data-ttu-id="96eb6-126">If you find this parameter, the connection string is for a specific Event Hub "entity" and is not the correct string to use with your logic app.</span><span class="sxs-lookup"><span data-stu-id="96eb6-126">If you find this parameter, the connection string is for a specific Event Hub "entity" and is not the correct string to use with your logic app.</span></span>

4. <span data-ttu-id="96eb6-127">Now continue with [Add an Event Hubs trigger](#add-trigger) or [Add an Event Hubs action](#add-action).</span><span class="sxs-lookup"><span data-stu-id="96eb6-127">Now continue with [Add an Event Hubs trigger](#add-trigger) or [Add an Event Hubs action](#add-action).</span></span>

<a name="add-trigger"></a>

## <a name="add-an-event-hubs-trigger"></a><span data-ttu-id="96eb6-128">Add an Event Hubs trigger</span><span class="sxs-lookup"><span data-stu-id="96eb6-128">Add an Event Hubs trigger</span></span>

<span data-ttu-id="96eb6-129">In Azure Logic Apps, every logic app must start with a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts), which fires when a specific event happens or when a specific condition is met.</span><span class="sxs-lookup"><span data-stu-id="96eb6-129">In Azure Logic Apps, every logic app must start with a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts), which fires when a specific event happens or when a specific condition is met.</span></span> <span data-ttu-id="96eb6-130">Each time the trigger fires, the Logic Apps engine creates a logic app instance and starts running your app's workflow.</span><span class="sxs-lookup"><span data-stu-id="96eb6-130">Each time the trigger fires, the Logic Apps engine creates a logic app instance and starts running your app's workflow.</span></span>

<span data-ttu-id="96eb6-131">This example shows how you can start a logic app workflow when new events are sent to your Event Hub.</span><span class="sxs-lookup"><span data-stu-id="96eb6-131">This example shows how you can start a logic app workflow when new events are sent to your Event Hub.</span></span> 

1. <span data-ttu-id="96eb6-132">In the Azure portal or Visual Studio, create a blank logic app, which opens Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="96eb6-132">In the Azure portal or Visual Studio, create a blank logic app, which opens Logic Apps Designer.</span></span> <span data-ttu-id="96eb6-133">This example uses the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="96eb6-133">This example uses the Azure portal.</span></span>

2. <span data-ttu-id="96eb6-134">In the search box, enter "event hubs" as your filter.</span><span class="sxs-lookup"><span data-stu-id="96eb6-134">In the search box, enter "event hubs" as your filter.</span></span> <span data-ttu-id="96eb6-135">From the triggers list, select the trigger you want.</span><span class="sxs-lookup"><span data-stu-id="96eb6-135">From the triggers list, select the trigger you want.</span></span> 

   <span data-ttu-id="96eb6-136">This example uses this trigger: **Event Hubs - When events are available in Event Hub**</span><span class="sxs-lookup"><span data-stu-id="96eb6-136">This example uses this trigger: **Event Hubs - When events are available in Event Hub**</span></span>

   ![Select trigger](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

3. <span data-ttu-id="96eb6-138">If you're prompted for connection details, [create your Event Hubs connection now](#create-connection).</span><span class="sxs-lookup"><span data-stu-id="96eb6-138">If you're prompted for connection details, [create your Event Hubs connection now](#create-connection).</span></span> <span data-ttu-id="96eb6-139">Or, if your connection already exists, provide the necessary information for the trigger.</span><span class="sxs-lookup"><span data-stu-id="96eb6-139">Or, if your connection already exists, provide the necessary information for the trigger.</span></span>

   1. <span data-ttu-id="96eb6-140">From the **Event Hub name** list, select the Event Hub you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="96eb6-140">From the **Event Hub name** list, select the Event Hub you want to monitor.</span></span>

      ![Specify Event Hub or consumer group](./media/connectors-create-api-azure-event-hubs/select-event-hub.png)

   2. <span data-ttu-id="96eb6-142">Select the interval and frequency for how often you want the trigger to check the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="96eb6-142">Select the interval and frequency for how often you want the trigger to check the Event Hub.</span></span>
 
   3. <span data-ttu-id="96eb6-143">To optionally select some of the advanced trigger options, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="96eb6-143">To optionally select some of the advanced trigger options, choose **Show advanced options**.</span></span>
   
      ![Trigger advanced options](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-advanced.png)

      | <span data-ttu-id="96eb6-145">Property</span><span class="sxs-lookup"><span data-stu-id="96eb6-145">Property</span></span> | <span data-ttu-id="96eb6-146">Details</span><span class="sxs-lookup"><span data-stu-id="96eb6-146">Details</span></span> | 
      |----------|---------| 
      | <span data-ttu-id="96eb6-147">Content type</span><span class="sxs-lookup"><span data-stu-id="96eb6-147">Content type</span></span>  | <span data-ttu-id="96eb6-148">Select the event's content type.</span><span class="sxs-lookup"><span data-stu-id="96eb6-148">Select the event's content type.</span></span> <span data-ttu-id="96eb6-149">The default is "application/octet-stream".</span><span class="sxs-lookup"><span data-stu-id="96eb6-149">The default is "application/octet-stream".</span></span> |
      | <span data-ttu-id="96eb6-150">Content schema</span><span class="sxs-lookup"><span data-stu-id="96eb6-150">Content schema</span></span> | <span data-ttu-id="96eb6-151">Enter the content schema in JSON for the events that are read from the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="96eb6-151">Enter the content schema in JSON for the events that are read from the Event Hub.</span></span> |
      | <span data-ttu-id="96eb6-152">Consumer group name</span><span class="sxs-lookup"><span data-stu-id="96eb6-152">Consumer group name</span></span> | <span data-ttu-id="96eb6-153">Enter the Event Hub [consumer group name](../event-hubs/event-hubs-features.md#consumer-groups) for reading events.</span><span class="sxs-lookup"><span data-stu-id="96eb6-153">Enter the Event Hub [consumer group name](../event-hubs/event-hubs-features.md#consumer-groups) for reading events.</span></span> <span data-ttu-id="96eb6-154">If not specified, the default consumer group is used.</span><span class="sxs-lookup"><span data-stu-id="96eb6-154">If not specified, the default consumer group is used.</span></span> |
      | <span data-ttu-id="96eb6-155">Minimum partition key</span><span class="sxs-lookup"><span data-stu-id="96eb6-155">Minimum partition key</span></span> | <span data-ttu-id="96eb6-156">Enter the minimum [partition](../event-hubs/event-hubs-features.md#partitions) ID to read.</span><span class="sxs-lookup"><span data-stu-id="96eb6-156">Enter the minimum [partition](../event-hubs/event-hubs-features.md#partitions) ID to read.</span></span> <span data-ttu-id="96eb6-157">By default, all partitions are read.</span><span class="sxs-lookup"><span data-stu-id="96eb6-157">By default, all partitions are read.</span></span> |
      | <span data-ttu-id="96eb6-158">Maximum partition key</span><span class="sxs-lookup"><span data-stu-id="96eb6-158">Maximum partition key</span></span> | <span data-ttu-id="96eb6-159">Enter the maximum [partition](../event-hubs/event-hubs-features.md#partitions) ID to read.</span><span class="sxs-lookup"><span data-stu-id="96eb6-159">Enter the maximum [partition](../event-hubs/event-hubs-features.md#partitions) ID to read.</span></span> <span data-ttu-id="96eb6-160">By default, all partitions are read.</span><span class="sxs-lookup"><span data-stu-id="96eb6-160">By default, all partitions are read.</span></span> |
      | <span data-ttu-id="96eb6-161">Maximum events count</span><span class="sxs-lookup"><span data-stu-id="96eb6-161">Maximum events count</span></span> | <span data-ttu-id="96eb6-162">Enter a value for the maximum number of events.</span><span class="sxs-lookup"><span data-stu-id="96eb6-162">Enter a value for the maximum number of events.</span></span> <span data-ttu-id="96eb6-163">The trigger returns between one and the number of events specified by this property.</span><span class="sxs-lookup"><span data-stu-id="96eb6-163">The trigger returns between one and the number of events specified by this property.</span></span> |
      |||

4. <span data-ttu-id="96eb6-164">When you're done, on the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="96eb6-164">When you're done, on the designer toolbar, choose **Save**.</span></span>

5. <span data-ttu-id="96eb6-165">Now continue adding one or more actions to your logic app for the tasks you want to perform with the trigger results.</span><span class="sxs-lookup"><span data-stu-id="96eb6-165">Now continue adding one or more actions to your logic app for the tasks you want to perform with the trigger results.</span></span>

> [!NOTE]
> <span data-ttu-id="96eb6-166">All Event Hub triggers are *long-polling* triggers, which means that when a trigger fires, the trigger processes all the events and then waits for 30 seconds for more events to appear in your Event Hub.</span><span class="sxs-lookup"><span data-stu-id="96eb6-166">All Event Hub triggers are *long-polling* triggers, which means that when a trigger fires, the trigger processes all the events and then waits for 30 seconds for more events to appear in your Event Hub.</span></span>
> <span data-ttu-id="96eb6-167">If no events are received in 30 seconds, the trigger run is skipped.</span><span class="sxs-lookup"><span data-stu-id="96eb6-167">If no events are received in 30 seconds, the trigger run is skipped.</span></span> <span data-ttu-id="96eb6-168">Otherwise, the trigger continues reading events until your Event Hub is empty.</span><span class="sxs-lookup"><span data-stu-id="96eb6-168">Otherwise, the trigger continues reading events until your Event Hub is empty.</span></span>
> <span data-ttu-id="96eb6-169">The next trigger poll happens based on the recurrence interval that you specify in the trigger's properties.</span><span class="sxs-lookup"><span data-stu-id="96eb6-169">The next trigger poll happens based on the recurrence interval that you specify in the trigger's properties.</span></span>

<a name="add-action"></a>

## <a name="add-an-event-hubs-action"></a><span data-ttu-id="96eb6-170">Add an Event Hubs action</span><span class="sxs-lookup"><span data-stu-id="96eb6-170">Add an Event Hubs action</span></span>

<span data-ttu-id="96eb6-171">In Azure Logic Apps, an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) is a step in your workflow that follows a trigger or another action.</span><span class="sxs-lookup"><span data-stu-id="96eb6-171">In Azure Logic Apps, an [action](../logic-apps/logic-apps-overview.md#logic-app-concepts) is a step in your workflow that follows a trigger or another action.</span></span> <span data-ttu-id="96eb6-172">For this example, the logic app starts with an Event Hubs trigger that checks for new events in your Event Hub.</span><span class="sxs-lookup"><span data-stu-id="96eb6-172">For this example, the logic app starts with an Event Hubs trigger that checks for new events in your Event Hub.</span></span> 

1. <span data-ttu-id="96eb6-173">In the Azure portal or Visual Studio, open your logic app in Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="96eb6-173">In the Azure portal or Visual Studio, open your logic app in Logic Apps Designer.</span></span> <span data-ttu-id="96eb6-174">This example uses the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="96eb6-174">This example uses the Azure portal.</span></span>

2. <span data-ttu-id="96eb6-175">Under the trigger or action, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="96eb6-175">Under the trigger or action, choose **New step** > **Add an action**.</span></span>

   <span data-ttu-id="96eb6-176">To add an action between existing steps, move your mouse over the connecting arrow.</span><span class="sxs-lookup"><span data-stu-id="96eb6-176">To add an action between existing steps, move your mouse over the connecting arrow.</span></span> 
   <span data-ttu-id="96eb6-177">Choose the plus sign (**+**) that appears, and then choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="96eb6-177">Choose the plus sign (**+**) that appears, and then choose **Add an action**.</span></span>

3. <span data-ttu-id="96eb6-178">In the search box, enter "event hubs" as your filter.</span><span class="sxs-lookup"><span data-stu-id="96eb6-178">In the search box, enter "event hubs" as your filter.</span></span>
<span data-ttu-id="96eb6-179">From the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="96eb6-179">From the actions list, select the action you want.</span></span> 

   <span data-ttu-id="96eb6-180">For this example, select this action: **Event Hubs - Send event**</span><span class="sxs-lookup"><span data-stu-id="96eb6-180">For this example, select this action: **Event Hubs - Send event**</span></span>

   ![Select "Event Hubs - Send event"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

4. <span data-ttu-id="96eb6-182">If you're prompted for connection details, [create your Event Hubs connection now](#create-connection).</span><span class="sxs-lookup"><span data-stu-id="96eb6-182">If you're prompted for connection details, [create your Event Hubs connection now](#create-connection).</span></span> <span data-ttu-id="96eb6-183">Or, if your connection already exists, provide the necessary information for the action.</span><span class="sxs-lookup"><span data-stu-id="96eb6-183">Or, if your connection already exists, provide the necessary information for the action.</span></span>

   | <span data-ttu-id="96eb6-184">Property</span><span class="sxs-lookup"><span data-stu-id="96eb6-184">Property</span></span> | <span data-ttu-id="96eb6-185">Required</span><span class="sxs-lookup"><span data-stu-id="96eb6-185">Required</span></span> | <span data-ttu-id="96eb6-186">Description</span><span class="sxs-lookup"><span data-stu-id="96eb6-186">Description</span></span> | 
   |----------|----------|-------------|
   | <span data-ttu-id="96eb6-187">Event Hub name</span><span class="sxs-lookup"><span data-stu-id="96eb6-187">Event Hub name</span></span> | <span data-ttu-id="96eb6-188">Yes</span><span class="sxs-lookup"><span data-stu-id="96eb6-188">Yes</span></span> | <span data-ttu-id="96eb6-189">Select the Event Hub where you want to send the event</span><span class="sxs-lookup"><span data-stu-id="96eb6-189">Select the Event Hub where you want to send the event</span></span> | 
   | <span data-ttu-id="96eb6-190">Event content</span><span class="sxs-lookup"><span data-stu-id="96eb6-190">Event content</span></span> | <span data-ttu-id="96eb6-191">No</span><span class="sxs-lookup"><span data-stu-id="96eb6-191">No</span></span> | <span data-ttu-id="96eb6-192">The content for the event you want to send</span><span class="sxs-lookup"><span data-stu-id="96eb6-192">The content for the event you want to send</span></span> | 
   | <span data-ttu-id="96eb6-193">Properties</span><span class="sxs-lookup"><span data-stu-id="96eb6-193">Properties</span></span> | <span data-ttu-id="96eb6-194">No</span><span class="sxs-lookup"><span data-stu-id="96eb6-194">No</span></span> | <span data-ttu-id="96eb6-195">The app properties and values to send</span><span class="sxs-lookup"><span data-stu-id="96eb6-195">The app properties and values to send</span></span> | 
   |||| 

   <span data-ttu-id="96eb6-196">For example:</span><span class="sxs-lookup"><span data-stu-id="96eb6-196">For example:</span></span> 

   ![Select Event Hub name and provide event content](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

5. <span data-ttu-id="96eb6-198">When you're done, on the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="96eb6-198">When you're done, on the designer toolbar, choose **Save**.</span></span>

<a name="create-connection"></a>

## <a name="connect-to-your-event-hub"></a><span data-ttu-id="96eb6-199">Connect to your Event Hub</span><span class="sxs-lookup"><span data-stu-id="96eb6-199">Connect to your Event Hub</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)] 

1. <span data-ttu-id="96eb6-200">When you're prompted for connection information, provide these details:</span><span class="sxs-lookup"><span data-stu-id="96eb6-200">When you're prompted for connection information, provide these details:</span></span>

   | <span data-ttu-id="96eb6-201">Property</span><span class="sxs-lookup"><span data-stu-id="96eb6-201">Property</span></span> | <span data-ttu-id="96eb6-202">Required</span><span class="sxs-lookup"><span data-stu-id="96eb6-202">Required</span></span> | <span data-ttu-id="96eb6-203">Value</span><span class="sxs-lookup"><span data-stu-id="96eb6-203">Value</span></span> | <span data-ttu-id="96eb6-204">Description</span><span class="sxs-lookup"><span data-stu-id="96eb6-204">Description</span></span> | 
   |----------|----------|-------|-------------|
   | <span data-ttu-id="96eb6-205">Connection Name</span><span class="sxs-lookup"><span data-stu-id="96eb6-205">Connection Name</span></span> | <span data-ttu-id="96eb6-206">Yes</span><span class="sxs-lookup"><span data-stu-id="96eb6-206">Yes</span></span> | <span data-ttu-id="96eb6-207"><*connection-name*></span><span class="sxs-lookup"><span data-stu-id="96eb6-207"><*connection-name*></span></span> | <span data-ttu-id="96eb6-208">The name to create for your connection</span><span class="sxs-lookup"><span data-stu-id="96eb6-208">The name to create for your connection</span></span> |
   | <span data-ttu-id="96eb6-209">Event Hubs Namespace</span><span class="sxs-lookup"><span data-stu-id="96eb6-209">Event Hubs Namespace</span></span> | <span data-ttu-id="96eb6-210">Yes</span><span class="sxs-lookup"><span data-stu-id="96eb6-210">Yes</span></span> | <span data-ttu-id="96eb6-211"><*event-hubs-namespace*></span><span class="sxs-lookup"><span data-stu-id="96eb6-211"><*event-hubs-namespace*></span></span> | <span data-ttu-id="96eb6-212">Select the Event Hubs namespace you want to use.</span><span class="sxs-lookup"><span data-stu-id="96eb6-212">Select the Event Hubs namespace you want to use.</span></span> | 
   |||||  

   <span data-ttu-id="96eb6-213">For example:</span><span class="sxs-lookup"><span data-stu-id="96eb6-213">For example:</span></span>

   ![Create Event Hub connection](./media/connectors-create-api-azure-event-hubs/create-event-hubs-connection-1.png)

   <span data-ttu-id="96eb6-215">To manually enter the connection string, choose **Manually enter connection information**.</span><span class="sxs-lookup"><span data-stu-id="96eb6-215">To manually enter the connection string, choose **Manually enter connection information**.</span></span> 
   <span data-ttu-id="96eb6-216">Learn [how to find your connection string](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="96eb6-216">Learn [how to find your connection string](#permissions-connection-string).</span></span>

2. <span data-ttu-id="96eb6-217">Select the Event Hubs policy to use, if not already selected.</span><span class="sxs-lookup"><span data-stu-id="96eb6-217">Select the Event Hubs policy to use, if not already selected.</span></span> <span data-ttu-id="96eb6-218">Choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="96eb6-218">Choose **Create**.</span></span>

   ![Create Event Hub connection, part 2](./media/connectors-create-api-azure-event-hubs/create-event-hubs-connection-2.png)

3. <span data-ttu-id="96eb6-220">After you create your connection, continue with [Add Event Hubs trigger](#add-trigger) or [Add Event Hubs action](#add-action).</span><span class="sxs-lookup"><span data-stu-id="96eb6-220">After you create your connection, continue with [Add Event Hubs trigger](#add-trigger) or [Add Event Hubs action](#add-action).</span></span>

## <a name="connector-reference"></a><span data-ttu-id="96eb6-221">Connector reference</span><span class="sxs-lookup"><span data-stu-id="96eb6-221">Connector reference</span></span>

<span data-ttu-id="96eb6-222">For technical details, such as triggers, actions, and limits, as described by the connector's Swagger file, see the [connector's reference page](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="96eb6-222">For technical details, such as triggers, actions, and limits, as described by the connector's Swagger file, see the [connector's reference page](/connectors/eventhubs/).</span></span> 

## <a name="get-support"></a><span data-ttu-id="96eb6-223">Get support</span><span class="sxs-lookup"><span data-stu-id="96eb6-223">Get support</span></span>

* <span data-ttu-id="96eb6-224">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="96eb6-224">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="96eb6-225">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="96eb6-225">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96eb6-226">Next steps</span><span class="sxs-lookup"><span data-stu-id="96eb6-226">Next steps</span></span>

* <span data-ttu-id="96eb6-227">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="96eb6-227">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>