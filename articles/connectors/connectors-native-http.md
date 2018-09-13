---
title: Connect to any HTTP endpoint with Azure Logic Apps | Microsoft Docs
description: Automate tasks and workflows that communicate with any HTTP endpoint by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.topic: article
tags: connectors
ms.date: 08/25/2018
ms.openlocfilehash: 95a039c990dc9b6c852a69518f0a71c51a4747b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818186"
---
# <a name="call-http-or-https-endpoints-with-azure-logic-apps"></a><span data-ttu-id="a96fa-103">Call HTTP or HTTPS endpoints with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a96fa-103">Call HTTP or HTTPS endpoints with Azure Logic Apps</span></span>

<span data-ttu-id="a96fa-104">With Azure Logic Apps and the Hypertext Transfer Protocol (HTTP) connector, you can automate workflows that communicate with any HTTP or HTTPS endpoint by building logic apps.</span><span class="sxs-lookup"><span data-stu-id="a96fa-104">With Azure Logic Apps and the Hypertext Transfer Protocol (HTTP) connector, you can automate workflows that communicate with any HTTP or HTTPS endpoint by building logic apps.</span></span> <span data-ttu-id="a96fa-105">For example, you can monitor the service endpoint for your website.</span><span class="sxs-lookup"><span data-stu-id="a96fa-105">For example, you can monitor the service endpoint for your website.</span></span> <span data-ttu-id="a96fa-106">When an event happens at that endpoint, such as your website going down, the event triggers your logic app's workflow and runs the specified actions.</span><span class="sxs-lookup"><span data-stu-id="a96fa-106">When an event happens at that endpoint, such as your website going down, the event triggers your logic app's workflow and runs the specified actions.</span></span> 

<span data-ttu-id="a96fa-107">You can use the HTTP trigger as the first step in your worklfow for checking or *polling* an endpoint on a regular schedule.</span><span class="sxs-lookup"><span data-stu-id="a96fa-107">You can use the HTTP trigger as the first step in your worklfow for checking or *polling* an endpoint on a regular schedule.</span></span> <span data-ttu-id="a96fa-108">On each check, the trigger sends a call or *request* to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="a96fa-108">On each check, the trigger sends a call or *request* to the endpoint.</span></span> <span data-ttu-id="a96fa-109">The endpoint's response determines whether your logic app's workflow runs.</span><span class="sxs-lookup"><span data-stu-id="a96fa-109">The endpoint's response determines whether your logic app's workflow runs.</span></span> <span data-ttu-id="a96fa-110">The trigger passes along any content from the response to the actions in your logic app.</span><span class="sxs-lookup"><span data-stu-id="a96fa-110">The trigger passes along any content from the response to the actions in your logic app.</span></span> 

<span data-ttu-id="a96fa-111">You can use the HTTP action as any other step in your workflow for calling the endpoint when you want.</span><span class="sxs-lookup"><span data-stu-id="a96fa-111">You can use the HTTP action as any other step in your workflow for calling the endpoint when you want.</span></span> <span data-ttu-id="a96fa-112">The endpoint's response determines how your workflow's remaining actions run.</span><span class="sxs-lookup"><span data-stu-id="a96fa-112">The endpoint's response determines how your workflow's remaining actions run.</span></span>

<span data-ttu-id="a96fa-113">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a96fa-113">If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a96fa-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a96fa-114">Prerequisites</span></span>

* <span data-ttu-id="a96fa-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a96fa-115">An Azure subscription.</span></span> <span data-ttu-id="a96fa-116">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="a96fa-116">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span> 

* <span data-ttu-id="a96fa-117">The URL for the target endpoint you want to call</span><span class="sxs-lookup"><span data-stu-id="a96fa-117">The URL for the target endpoint you want to call</span></span> 

* <span data-ttu-id="a96fa-118">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="a96fa-118">Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)</span></span>

* <span data-ttu-id="a96fa-119">The logic app from where you want to call the target endpoint To start with the HTTP trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="a96fa-119">The logic app from where you want to call the target endpoint To start with the HTTP trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> <span data-ttu-id="a96fa-120">To use the HTTP action, start your logic app with a trigger.</span><span class="sxs-lookup"><span data-stu-id="a96fa-120">To use the HTTP action, start your logic app with a trigger.</span></span>

## <a name="add-http-trigger"></a><span data-ttu-id="a96fa-121">Add HTTP trigger</span><span class="sxs-lookup"><span data-stu-id="a96fa-121">Add HTTP trigger</span></span>

1. <span data-ttu-id="a96fa-122">Sign in to the [Azure portal](https://portal.azure.com), and open your blank logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="a96fa-122">Sign in to the [Azure portal](https://portal.azure.com), and open your blank logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="a96fa-123">In the search box, enter "http" as your filter.</span><span class="sxs-lookup"><span data-stu-id="a96fa-123">In the search box, enter "http" as your filter.</span></span> <span data-ttu-id="a96fa-124">Under the triggers list, select the **HTTP** trigger.</span><span class="sxs-lookup"><span data-stu-id="a96fa-124">Under the triggers list, select the **HTTP** trigger.</span></span> 

   ![Select HTTP trigger](./media/connectors-native-http/select-http-trigger.png)

1. <span data-ttu-id="a96fa-126">Provide the [HTTP trigger's parameters and values](../logic-apps/logic-apps-workflow-actions-triggers.md##http-trigger) you want to include in the call to the target endpoint.</span><span class="sxs-lookup"><span data-stu-id="a96fa-126">Provide the [HTTP trigger's parameters and values](../logic-apps/logic-apps-workflow-actions-triggers.md##http-trigger) you want to include in the call to the target endpoint.</span></span> <span data-ttu-id="a96fa-127">Set up recurrence for how often you want the trigger to check the target endpont.</span><span class="sxs-lookup"><span data-stu-id="a96fa-127">Set up recurrence for how often you want the trigger to check the target endpont.</span></span>

   ![Enter HTTP trigger parameters](./media/connectors-native-http/http-trigger-parameters.png)

   <span data-ttu-id="a96fa-129">For more information about the HTTP trigger, parameters, and values, see [Trigger and action types reference](../logic-apps/logic-apps-workflow-actions-triggers.md##http-trigger).</span><span class="sxs-lookup"><span data-stu-id="a96fa-129">For more information about the HTTP trigger, parameters, and values, see [Trigger and action types reference](../logic-apps/logic-apps-workflow-actions-triggers.md##http-trigger).</span></span>

1. <span data-ttu-id="a96fa-130">Continue building your logic app's workflow with actions that run when the trigger fires.</span><span class="sxs-lookup"><span data-stu-id="a96fa-130">Continue building your logic app's workflow with actions that run when the trigger fires.</span></span>

## <a name="add-http-action"></a><span data-ttu-id="a96fa-131">Add HTTP action</span><span class="sxs-lookup"><span data-stu-id="a96fa-131">Add HTTP action</span></span>

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. <span data-ttu-id="a96fa-132">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span><span class="sxs-lookup"><span data-stu-id="a96fa-132">Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.</span></span>

1. <span data-ttu-id="a96fa-133">Under the last step where you want to add the HTTP action, choose **New step**.</span><span class="sxs-lookup"><span data-stu-id="a96fa-133">Under the last step where you want to add the HTTP action, choose **New step**.</span></span> 

   <span data-ttu-id="a96fa-134">In this example, the logic app starts with the HTTP trigger as the first step.</span><span class="sxs-lookup"><span data-stu-id="a96fa-134">In this example, the logic app starts with the HTTP trigger as the first step.</span></span>

1. <span data-ttu-id="a96fa-135">In the search box, enter "http" as your filter.</span><span class="sxs-lookup"><span data-stu-id="a96fa-135">In the search box, enter "http" as your filter.</span></span> <span data-ttu-id="a96fa-136">Under the actions list, select the **HTTP** action.</span><span class="sxs-lookup"><span data-stu-id="a96fa-136">Under the actions list, select the **HTTP** action.</span></span>

   ![Select HTTP action](./media/connectors-native-http/select-http-action.png)

   <span data-ttu-id="a96fa-138">To add an action between steps, move your pointer over the arrow between steps.</span><span class="sxs-lookup"><span data-stu-id="a96fa-138">To add an action between steps, move your pointer over the arrow between steps.</span></span> 
   <span data-ttu-id="a96fa-139">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="a96fa-139">Choose the plus sign (**+**) that appears, and then select **Add an action**.</span></span>

1. <span data-ttu-id="a96fa-140">Provide the [HTTP action's parameters and values](../logic-apps/logic-apps-workflow-actions-triggers.md##http-action) you want to include in the call to the target endpoint.</span><span class="sxs-lookup"><span data-stu-id="a96fa-140">Provide the [HTTP action's parameters and values](../logic-apps/logic-apps-workflow-actions-triggers.md##http-action) you want to include in the call to the target endpoint.</span></span> 

   ![Enter HTTP action parameters](./media/connectors-native-http/http-action-parameters.png)

1. <span data-ttu-id="a96fa-142">When you're done, make sure you save your logic app.</span><span class="sxs-lookup"><span data-stu-id="a96fa-142">When you're done, make sure you save your logic app.</span></span> <span data-ttu-id="a96fa-143">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a96fa-143">On the designer toolbar, choose **Save**.</span></span> 

## <a name="authentication"></a><span data-ttu-id="a96fa-144">Authentication</span><span class="sxs-lookup"><span data-stu-id="a96fa-144">Authentication</span></span>

<span data-ttu-id="a96fa-145">To set authentication, choose **Show advanced options** inside the action or trigger.</span><span class="sxs-lookup"><span data-stu-id="a96fa-145">To set authentication, choose **Show advanced options** inside the action or trigger.</span></span> <span data-ttu-id="a96fa-146">For more information about available authentication types for HTTP triggers and actions, see [Trigger and action types reference](../logic-apps/logic-apps-workflow-actions-triggers.md#connector-authentication).</span><span class="sxs-lookup"><span data-stu-id="a96fa-146">For more information about available authentication types for HTTP triggers and actions, see [Trigger and action types reference](../logic-apps/logic-apps-workflow-actions-triggers.md#connector-authentication).</span></span>

## <a name="get-support"></a><span data-ttu-id="a96fa-147">Get support</span><span class="sxs-lookup"><span data-stu-id="a96fa-147">Get support</span></span>

* <span data-ttu-id="a96fa-148">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="a96fa-148">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="a96fa-149">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="a96fa-149">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a96fa-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="a96fa-150">Next steps</span></span>

* <span data-ttu-id="a96fa-151">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="a96fa-151">Learn about other [Logic Apps connectors](../connectors/apis-list.md)</span></span>
