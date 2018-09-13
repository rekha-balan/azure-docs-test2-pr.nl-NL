---
title: Set up event monitor with Azure Event Hubs for Azure Logic Apps | Microsoft Docs
description: Monitor data streams to receive events and send events for Azure Logic Apps with Azure Event Hubs
services: logic-apps
keywords: data stream, event monitor, event hubs
author: ecfan
manager: anneta
editor: ''
documentationcenter: ''
tags: connectors
ms.assetid: ''
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: a35e5193fc89860dd367f34d36e5a9d515faee39
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552895"
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="a29c3-104">Monitor, receive, and send events with the Event Hubs connector</span><span class="sxs-lookup"><span data-stu-id="a29c3-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="a29c3-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span><span class="sxs-lookup"><span data-stu-id="a29c3-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="a29c3-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="a29c3-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="a29c3-107">Requirements</span><span class="sxs-lookup"><span data-stu-id="a29c3-107">Requirements</span></span>

* <span data-ttu-id="a29c3-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="a29c3-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="a29c3-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="a29c3-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="a29c3-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span><span class="sxs-lookup"><span data-stu-id="a29c3-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="a29c3-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a29c3-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="a29c3-112">Check Event Hubs namespace permissions and find the connection string</span><span class="sxs-lookup"><span data-stu-id="a29c3-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="a29c3-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="a29c3-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="a29c3-114">This connection authorizes your logic app to access data.</span><span class="sxs-lookup"><span data-stu-id="a29c3-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="a29c3-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="a29c3-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="a29c3-116">To check your permissions and get the connection string, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="a29c3-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="a29c3-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="a29c3-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="a29c3-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span><span class="sxs-lookup"><span data-stu-id="a29c3-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="a29c3-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="a29c3-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="a29c3-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span><span class="sxs-lookup"><span data-stu-id="a29c3-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Manage permissions for your Event Hub namespace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="a29c3-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="a29c3-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="a29c3-123">Next to your primary key connection string, choose the copy button.</span><span class="sxs-lookup"><span data-stu-id="a29c3-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![Copy Event Hubs namespace connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="a29c3-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span><span class="sxs-lookup"><span data-stu-id="a29c3-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="a29c3-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span><span class="sxs-lookup"><span data-stu-id="a29c3-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="a29c3-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="a29c3-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="a29c3-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="a29c3-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![Enter connection string for Event Hubs namespace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="a29c3-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span><span class="sxs-lookup"><span data-stu-id="a29c3-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="a29c3-131">You can then continue with the other steps in your logic app.</span><span class="sxs-lookup"><span data-stu-id="a29c3-131">You can then continue with the other steps in your logic app.</span></span>

    ![Event Hubs namespace connection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="a29c3-133">Start workflow when your Event Hub receives new events</span><span class="sxs-lookup"><span data-stu-id="a29c3-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="a29c3-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span><span class="sxs-lookup"><span data-stu-id="a29c3-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="a29c3-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span><span class="sxs-lookup"><span data-stu-id="a29c3-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="a29c3-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span><span class="sxs-lookup"><span data-stu-id="a29c3-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="a29c3-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span><span class="sxs-lookup"><span data-stu-id="a29c3-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="a29c3-138">Select this trigger: **When events are available in Event Hub**</span><span class="sxs-lookup"><span data-stu-id="a29c3-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Select trigger for when your Event Hub receives new events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="a29c3-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span><span class="sxs-lookup"><span data-stu-id="a29c3-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="a29c3-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="a29c3-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="a29c3-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="a29c3-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![Enter connection string for Event Hubs namespace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="a29c3-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span><span class="sxs-lookup"><span data-stu-id="a29c3-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Trigger settings for when your Event Hub receives new events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="a29c3-146">Enter or select the name for the Event Hub that you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="a29c3-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="a29c3-147">Select the frequency and interval for how often you want to check the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="a29c3-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="a29c3-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="a29c3-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Specify Event Hub or consumer group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="a29c3-150">You've now set up a trigger to start a workflow for your logic app.</span><span class="sxs-lookup"><span data-stu-id="a29c3-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="a29c3-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span><span class="sxs-lookup"><span data-stu-id="a29c3-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="a29c3-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span><span class="sxs-lookup"><span data-stu-id="a29c3-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="a29c3-153">Send events to your Event Hub from your logic app</span><span class="sxs-lookup"><span data-stu-id="a29c3-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="a29c3-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="a29c3-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="a29c3-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span><span class="sxs-lookup"><span data-stu-id="a29c3-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="a29c3-156">To send an event to your Event Hub from your logic app, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="a29c3-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="a29c3-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="a29c3-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Choose "New Step", then "Add an action"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="a29c3-159">Now you can find and select an action to perform.</span><span class="sxs-lookup"><span data-stu-id="a29c3-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="a29c3-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span><span class="sxs-lookup"><span data-stu-id="a29c3-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="a29c3-161">In the search box, enter `event hubs` for your filter.</span><span class="sxs-lookup"><span data-stu-id="a29c3-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="a29c3-162">Select this action: **Send event**</span><span class="sxs-lookup"><span data-stu-id="a29c3-162">Select this action: **Send event**</span></span>

    ![Select "Event Hubs - Send event" action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="a29c3-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span><span class="sxs-lookup"><span data-stu-id="a29c3-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="a29c3-165">Enter any other optional details about the event, such as content for that event.</span><span class="sxs-lookup"><span data-stu-id="a29c3-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="a29c3-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="a29c3-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![Enter Event Hub name and optional event details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="a29c3-168">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="a29c3-168">Save your changes.</span></span>

    ![Save your logic app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="a29c3-170">You've now set up an action to send events from your logic app.</span><span class="sxs-lookup"><span data-stu-id="a29c3-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="technical-details"></a><span data-ttu-id="a29c3-171">Technical details</span><span class="sxs-lookup"><span data-stu-id="a29c3-171">Technical details</span></span>

### <a name="triggers"></a><span data-ttu-id="a29c3-172">Triggers</span><span class="sxs-lookup"><span data-stu-id="a29c3-172">Triggers</span></span>

| <span data-ttu-id="a29c3-173">Trigger</span><span class="sxs-lookup"><span data-stu-id="a29c3-173">Trigger</span></span> | <span data-ttu-id="a29c3-174">Description</span><span class="sxs-lookup"><span data-stu-id="a29c3-174">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a29c3-175">When events are available in Event Hub</span><span class="sxs-lookup"><span data-stu-id="a29c3-175">When events are available in Event Hub</span></span> | <span data-ttu-id="a29c3-176">Trigger a workflow when events are available in the specified Event Hub.</span><span class="sxs-lookup"><span data-stu-id="a29c3-176">Trigger a workflow when events are available in the specified Event Hub.</span></span> |

### <a name="actions"></a><span data-ttu-id="a29c3-177">Actions</span><span class="sxs-lookup"><span data-stu-id="a29c3-177">Actions</span></span>

| <span data-ttu-id="a29c3-178">Action</span><span class="sxs-lookup"><span data-stu-id="a29c3-178">Action</span></span> | <span data-ttu-id="a29c3-179">Description</span><span class="sxs-lookup"><span data-stu-id="a29c3-179">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a29c3-180">Send an event</span><span class="sxs-lookup"><span data-stu-id="a29c3-180">Send an event</span></span> | <span data-ttu-id="a29c3-181">Send an event to the specified Event Hub.</span><span class="sxs-lookup"><span data-stu-id="a29c3-181">Send an event to the specified Event Hub.</span></span> |

## <a name="get-help"></a><span data-ttu-id="a29c3-182">Get help</span><span class="sxs-lookup"><span data-stu-id="a29c3-182">Get help</span></span>

<span data-ttu-id="a29c3-183">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="a29c3-183">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="a29c3-184">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="a29c3-184">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a29c3-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="a29c3-185">Next steps</span></span>

*  [<span data-ttu-id="a29c3-186">Find other connectors for Azure Logic apps</span><span class="sxs-lookup"><span data-stu-id="a29c3-186">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)











