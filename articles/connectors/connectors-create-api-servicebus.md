---
title: Send and receive messages with Azure Service Bus - Azure Logic Apps | Microsoft Docs
description: Set up enterprise cloud messaging with Azure Service Bus in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.topic: article
tags: connectors
ms.date: 08/25/2018
ms.openlocfilehash: 813df5b4ef37ad1264df48863aa8f0ed5a4d4789
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825578"
---
# <a name="exchange-messages-in-the-cloud-with-azure-service-bus-and-azure-logic-apps"></a><span data-ttu-id="86d23-103">Exchange messages in the cloud with Azure Service Bus and Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="86d23-103">Exchange messages in the cloud with Azure Service Bus and Azure Logic Apps</span></span>

<span data-ttu-id="86d23-104">With Azure Logic Apps and the Azure Service Bus connector, you can create automated tasks and workflows that transfer data, such as sales and purchase orders, journals, and inventory movements across applications for your organization.</span><span class="sxs-lookup"><span data-stu-id="86d23-104">With Azure Logic Apps and the Azure Service Bus connector, you can create automated tasks and workflows that transfer data, such as sales and purchase orders, journals, and inventory movements across applications for your organization.</span></span> <span data-ttu-id="86d23-105">The connector not only monitors, sends, and manages messages, but also performs actions with queues, sessions, topics, subscriptions, and so on, for example:</span><span class="sxs-lookup"><span data-stu-id="86d23-105">The connector not only monitors, sends, and manages messages, but also performs actions with queues, sessions, topics, subscriptions, and so on, for example:</span></span>

* <span data-ttu-id="86d23-106">Monitor when messages arrive (auto-complete) or are received (peek-lock) in queues, topics, and topic subscriptions.</span><span class="sxs-lookup"><span data-stu-id="86d23-106">Monitor when messages arrive (auto-complete) or are received (peek-lock) in queues, topics, and topic subscriptions.</span></span> 
* <span data-ttu-id="86d23-107">Send messages.</span><span class="sxs-lookup"><span data-stu-id="86d23-107">Send messages.</span></span>
* <span data-ttu-id="86d23-108">Create and delete topic subscriptions.</span><span class="sxs-lookup"><span data-stu-id="86d23-108">Create and delete topic subscriptions.</span></span>
* <span data-ttu-id="86d23-109">Manage messages in queues and topic subscriptions, for example, get, get deferred, complete, defer, abandon, and dead-letter.</span><span class="sxs-lookup"><span data-stu-id="86d23-109">Manage messages in queues and topic subscriptions, for example, get, get deferred, complete, defer, abandon, and dead-letter.</span></span>
* <span data-ttu-id="86d23-110">Renew locks on messages and sessions in queues and topic subscriptions.</span><span class="sxs-lookup"><span data-stu-id="86d23-110">Renew locks on messages and sessions in queues and topic subscriptions.</span></span>
* <span data-ttu-id="86d23-111">Close sessions in queues and topics.</span><span class="sxs-lookup"><span data-stu-id="86d23-111">Close sessions in queues and topics.</span></span>

<span data-ttu-id="86d23-112">You can use triggers that get responses from Service Bus and make the output available to other actions in your logic apps.</span><span class="sxs-lookup"><span data-stu-id="86d23-112">You can use triggers that get responses from Service Bus and make the output available to other actions in your logic apps.</span></span> <span data-ttu-id="86d23-113">You can also have other actions use the output from Service Bus actions.</span><span class="sxs-lookup"><span data-stu-id="86d23-113">You can also have other actions use the output from Service Bus actions.</span></span> <span data-ttu-id="86d23-114">If you're new to Service Bus and Logic Apps, review [What is Azure Service Bus?](../service-bus-messaging/service-bus-messaging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="86d23-114">If you're new to Service Bus and Logic Apps, review [What is Azure Service Bus?](../service-bus-messaging/service-bus-messaging-overview.md)</span></span> <span data-ttu-id="86d23-115">and [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86d23-115">and [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86d23-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="86d23-116">Prerequisites</span></span>

* <span data-ttu-id="86d23-117">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="86d23-117">An Azure subscription.</span></span> <span data-ttu-id="86d23-118">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="86d23-118">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="86d23-119">A Service Bus namespace and messaging entity, such as a queue.</span><span class="sxs-lookup"><span data-stu-id="86d23-119">A Service Bus namespace and messaging entity, such as a queue.</span></span> <span data-ttu-id="86d23-120">If you don't have these items, learn how to [create your Service Bus namespace and a queue](../service-bus-messaging/service-bus-create-namespace-portal.md).</span><span class="sxs-lookup"><span data-stu-id="86d23-120">If you don't have these items, learn how to [create your Service Bus namespace and a queue](../service-bus-messaging/service-bus-create-namespace-portal.md).</span></span> 

  <span data-ttu-id="86d23-121">These items must exist in the same Azure subscription as your logic apps that use these items.</span><span class="sxs-lookup"><span data-stu-id="86d23-121">These items must exist in the same Azure subscription as your logic apps that use these items.</span></span>

* <span data-ttu-id="86d23-122">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="86d23-122">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="86d23-123">The logic app where you want to use Service Bus.</span><span class="sxs-lookup"><span data-stu-id="86d23-123">The logic app where you want to use Service Bus.</span></span> <span data-ttu-id="86d23-124">Your logic app must exist in the same Azure subscription as your service bus.</span><span class="sxs-lookup"><span data-stu-id="86d23-124">Your logic app must exist in the same Azure subscription as your service bus.</span></span> <span data-ttu-id="86d23-125">To start with a Service Bus trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="86d23-125">To start with a Service Bus trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="86d23-126">To use a Service Bus action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span><span class="sxs-lookup"><span data-stu-id="86d23-126">To use a Service Bus action, start your logic app with another trigger, for example, the **Recurrence** trigger.</span></span>

<a name="permissions-connection-string"></a>

## <a name="check-permissions"></a><span data-ttu-id="86d23-127">Check permissions</span><span class="sxs-lookup"><span data-stu-id="86d23-127">Check permissions</span></span>

<span data-ttu-id="86d23-128">Confirm that your logic app has permissions for accessing your Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="86d23-128">Confirm that your logic app has permissions for accessing your Service Bus namespace.</span></span> 

1. <span data-ttu-id="86d23-129">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86d23-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="86d23-130">Go to your Service Bus *namespace*.</span><span class="sxs-lookup"><span data-stu-id="86d23-130">Go to your Service Bus *namespace*.</span></span> <span data-ttu-id="86d23-131">On the namespace page, under **Settings**, select **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="86d23-131">On the namespace page, under **Settings**, select **Shared access policies**.</span></span> <span data-ttu-id="86d23-132">Under **Claims**, check that you have **Manage** permissions for that namespace</span><span class="sxs-lookup"><span data-stu-id="86d23-132">Under **Claims**, check that you have **Manage** permissions for that namespace</span></span>

   ![Manage permissions for your Service Bus namespace](./media/connectors-create-api-azure-service-bus/azure-service-bus-namespace.png)

3. <span data-ttu-id="86d23-134">Get the connection string for your Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="86d23-134">Get the connection string for your Service Bus namespace.</span></span> <span data-ttu-id="86d23-135">You need this string when you enter your connection information in your logic app.</span><span class="sxs-lookup"><span data-stu-id="86d23-135">You need this string when you enter your connection information in your logic app.</span></span>

   1. <span data-ttu-id="86d23-136">Select **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="86d23-136">Select **RootManageSharedAccessKey**.</span></span> 
   
   1. <span data-ttu-id="86d23-137">Next to your primary connection string, choose the copy button.</span><span class="sxs-lookup"><span data-stu-id="86d23-137">Next to your primary connection string, choose the copy button.</span></span> <span data-ttu-id="86d23-138">Save the connection string for later use.</span><span class="sxs-lookup"><span data-stu-id="86d23-138">Save the connection string for later use.</span></span>

      ![Copy Service Bus namespace connection string](./media/connectors-create-api-azure-service-bus/find-service-bus-connection-string.png)

   > [!TIP]
   > <span data-ttu-id="86d23-140">To confirm whether your connection string is associated with your Service Bus namespace or a messaging entity, such as a queue, search the connection string for the `EntityPath` parameter.</span><span class="sxs-lookup"><span data-stu-id="86d23-140">To confirm whether your connection string is associated with your Service Bus namespace or a messaging entity, such as a queue, search the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="86d23-141">If you find this parameter, the connection string is for a specific entity, and isn't the correct string to use with your logic app.</span><span class="sxs-lookup"><span data-stu-id="86d23-141">If you find this parameter, the connection string is for a specific entity, and isn't the correct string to use with your logic app.</span></span>

## <a name="add-trigger-or-action"></a><span data-ttu-id="86d23-142">Add trigger or action</span><span class="sxs-lookup"><span data-stu-id="86d23-142">Add trigger or action</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="86d23-143">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="86d23-143">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="86d23-144">To add a *trigger* to a blank logic app, in the search box, enter "Azure Service Bus" as your filter.</span><span class="sxs-lookup"><span data-stu-id="86d23-144">To add a *trigger* to a blank logic app, in the search box, enter "Azure Service Bus" as your filter.</span></span> <span data-ttu-id="86d23-145">Under the triggers list, select the trigger you want.</span><span class="sxs-lookup"><span data-stu-id="86d23-145">Under the triggers list, select the trigger you want.</span></span> 

   <span data-ttu-id="86d23-146">For example, to trigger your logic app when a new item gets sent to a Service Bus queue, select this trigger: **When a message is received in a queue (auto-complete)**</span><span class="sxs-lookup"><span data-stu-id="86d23-146">For example, to trigger your logic app when a new item gets sent to a Service Bus queue, select this trigger: **When a message is received in a queue (auto-complete)**</span></span>

   ![Select Service Bus trigger](./media/connectors-create-api-azure-service-bus/select-service-bus-trigger.png)

   > [!NOTE]
   > <span data-ttu-id="86d23-148">Some triggers can return one or messages, for example, the trigger, **When one or more messages arrive in a queue (auto-complete)**.</span><span class="sxs-lookup"><span data-stu-id="86d23-148">Some triggers can return one or messages, for example, the trigger, **When one or more messages arrive in a queue (auto-complete)**.</span></span> <span data-ttu-id="86d23-149">When these triggers fire, they return between one and the number of messages specified by the trigger's **Maximum message count** property.</span><span class="sxs-lookup"><span data-stu-id="86d23-149">When these triggers fire, they return between one and the number of messages specified by the trigger's **Maximum message count** property.</span></span>

   <span data-ttu-id="86d23-150">*All Service Bus triggers are long-polling triggers*, which means when the trigger fires, the trigger processes all the messages and then waits 30 seconds for more messages to appear in the queue or topic subscription.</span><span class="sxs-lookup"><span data-stu-id="86d23-150">*All Service Bus triggers are long-polling triggers*, which means when the trigger fires, the trigger processes all the messages and then waits 30 seconds for more messages to appear in the queue or topic subscription.</span></span> 
   <span data-ttu-id="86d23-151">If no messages appear in 30 seconds, the trigger run is skipped.</span><span class="sxs-lookup"><span data-stu-id="86d23-151">If no messages appear in 30 seconds, the trigger run is skipped.</span></span> 
   <span data-ttu-id="86d23-152">Otherwise, the trigger continues reading messages until the queue or topic subscription is empty.</span><span class="sxs-lookup"><span data-stu-id="86d23-152">Otherwise, the trigger continues reading messages until the queue or topic subscription is empty.</span></span> <span data-ttu-id="86d23-153">The next trigger poll is based on the recurrence interval specified in the trigger's properties.</span><span class="sxs-lookup"><span data-stu-id="86d23-153">The next trigger poll is based on the recurrence interval specified in the trigger's properties.</span></span>

1. <span data-ttu-id="86d23-154">To add an *action* to an existing logic app, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="86d23-154">To add an *action* to an existing logic app, follow these steps:</span></span> 

   1. <span data-ttu-id="86d23-155">Under the last step where you want to add an action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="86d23-155">Under the last step where you want to add an action, choose **New step**.</span></span> 

      <span data-ttu-id="86d23-156">To add an action between steps, move your pointer over the arrow between steps.</span><span class="sxs-lookup"><span data-stu-id="86d23-156">To add an action between steps, move your pointer over the arrow between steps.</span></span> 
      <span data-ttu-id="86d23-157">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="86d23-157">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span></span>

   1. <span data-ttu-id="86d23-158">In the search box, enter "Azure Service Bus" as your filter.</span><span class="sxs-lookup"><span data-stu-id="86d23-158">In the search box, enter "Azure Service Bus" as your filter.</span></span> 
   <span data-ttu-id="86d23-159">Under the actions list, select the action you want.</span><span class="sxs-lookup"><span data-stu-id="86d23-159">Under the actions list, select the action you want.</span></span> 
 
      <span data-ttu-id="86d23-160">For example, select this action: **Send message**</span><span class="sxs-lookup"><span data-stu-id="86d23-160">For example, select this action: **Send message**</span></span>

      ![Select Service Bus action](./media/connectors-create-api-azure-service-bus/select-service-bus-send-message-action.png) 

1. <span data-ttu-id="86d23-162">If you're connecting your logic app to your Service Bus namespace for the first time, the Logic App Designer now prompts you for your connection information.</span><span class="sxs-lookup"><span data-stu-id="86d23-162">If you're connecting your logic app to your Service Bus namespace for the first time, the Logic App Designer now prompts you for your connection information.</span></span> 

   1. <span data-ttu-id="86d23-163">Provide a name for your connection, and select your Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="86d23-163">Provide a name for your connection, and select your Service Bus namespace.</span></span>

      ![Create Service Bus connection, part 1](./media/connectors-create-api-azure-service-bus/create-service-bus-connection-1.png)

      <span data-ttu-id="86d23-165">To manually enter the connection string instead, choose **Manually enter connection information**.</span><span class="sxs-lookup"><span data-stu-id="86d23-165">To manually enter the connection string instead, choose **Manually enter connection information**.</span></span> 
      <span data-ttu-id="86d23-166">If you don't have your connection string, learn [how to find your connection string](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="86d23-166">If you don't have your connection string, learn [how to find your connection string](#permissions-connection-string).</span></span>

   1. <span data-ttu-id="86d23-167">Now select your Service Bus policy, and then choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="86d23-167">Now select your Service Bus policy, and then choose **Create**.</span></span>

      ![Create Service Bus connection, part 2](./media/connectors-create-api-azure-service-bus/create-service-bus-connection-2.png)

1. <span data-ttu-id="86d23-169">For this example, select the messaging entity you want, such as a queue or topic.</span><span class="sxs-lookup"><span data-stu-id="86d23-169">For this example, select the messaging entity you want, such as a queue or topic.</span></span> <span data-ttu-id="86d23-170">In this example, select your Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="86d23-170">In this example, select your Service Bus queue.</span></span> 
   
   ![Select Service Bus queue](./media/connectors-create-api-azure-service-bus/service-bus-select-queue.png)

1. <span data-ttu-id="86d23-172">Provide the necessary details for your trigger or action.</span><span class="sxs-lookup"><span data-stu-id="86d23-172">Provide the necessary details for your trigger or action.</span></span> <span data-ttu-id="86d23-173">For this example, follow the relevant steps for your trigger or action:</span><span class="sxs-lookup"><span data-stu-id="86d23-173">For this example, follow the relevant steps for your trigger or action:</span></span> 

   * <span data-ttu-id="86d23-174">**For the sample trigger**: Set the polling interval and frequency for checking the queue.</span><span class="sxs-lookup"><span data-stu-id="86d23-174">**For the sample trigger**: Set the polling interval and frequency for checking the queue.</span></span>

     ![Set up polling interval](./media/connectors-create-api-azure-service-bus/service-bus-trigger-details.png)

     <span data-ttu-id="86d23-176">When you're done, continue building your logic app's workflow by adding the actions you want.</span><span class="sxs-lookup"><span data-stu-id="86d23-176">When you're done, continue building your logic app's workflow by adding the actions you want.</span></span> <span data-ttu-id="86d23-177">For example, you can add an action that sends email when a new message arrives.</span><span class="sxs-lookup"><span data-stu-id="86d23-177">For example, you can add an action that sends email when a new message arrives.</span></span>
     <span data-ttu-id="86d23-178">When your trigger checks your queue and finds a new message, your logic app runs your selected actions for the found message.</span><span class="sxs-lookup"><span data-stu-id="86d23-178">When your trigger checks your queue and finds a new message, your logic app runs your selected actions for the found message.</span></span>

   * <span data-ttu-id="86d23-179">**For the sample action**: Enter the message content and any other details.</span><span class="sxs-lookup"><span data-stu-id="86d23-179">**For the sample action**: Enter the message content and any other details.</span></span> 

     ![Provide message content and details](./media/connectors-create-api-azure-service-bus/service-bus-send-message-details.png)

     <span data-ttu-id="86d23-181">When you're done, continue building your logic app's workflow by adding any other actions you want.</span><span class="sxs-lookup"><span data-stu-id="86d23-181">When you're done, continue building your logic app's workflow by adding any other actions you want.</span></span> <span data-ttu-id="86d23-182">For example, you can add an action that sends email confirming your message was sent.</span><span class="sxs-lookup"><span data-stu-id="86d23-182">For example, you can add an action that sends email confirming your message was sent.</span></span>

1. <span data-ttu-id="86d23-183">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="86d23-183">Save your logic app.</span></span> <span data-ttu-id="86d23-184">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="86d23-184">On the designer toolbar, choose **Save**.</span></span>

## <a name="connector-reference"></a><span data-ttu-id="86d23-185">Connector reference</span><span class="sxs-lookup"><span data-stu-id="86d23-185">Connector reference</span></span>

<span data-ttu-id="86d23-186">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="86d23-186">For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/servicebus/).</span></span>

## <a name="get-support"></a><span data-ttu-id="86d23-187">Get support</span><span class="sxs-lookup"><span data-stu-id="86d23-187">Get support</span></span>

* <span data-ttu-id="86d23-188">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="86d23-188">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="86d23-189">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="86d23-189">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86d23-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="86d23-190">Next steps</span></span>

* <span data-ttu-id="86d23-191">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="86d23-191">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>