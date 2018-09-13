---
title: Webhook connector for Azure Logic Apps | Microsoft Docs
description: How to use webhook actions and triggers to perform actions like Filter Array from logic apps
services: logic-apps
author: jeffhollan
manager: anneta
editor: ''
documentationcenter: ''
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: c3c87fae4fa8e719834db45d7bca0c8a1260ae02
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661295"
---
# <a name="get-started-with-the-webhook-connector"></a><span data-ttu-id="a8862-103">Get started with the webhook connector</span><span class="sxs-lookup"><span data-stu-id="a8862-103">Get started with the webhook connector</span></span>

<span data-ttu-id="a8862-104">With the webhook action and trigger, you can start, pause, and resume flows to perform these tasks:</span><span class="sxs-lookup"><span data-stu-id="a8862-104">With the webhook action and trigger, you can start, pause, and resume flows to perform these tasks:</span></span>

* <span data-ttu-id="a8862-105">Trigger from an [Azure Event Hub](https://github.com/logicappsio/EventHubAPI) when an item is received</span><span class="sxs-lookup"><span data-stu-id="a8862-105">Trigger from an [Azure Event Hub](https://github.com/logicappsio/EventHubAPI) when an item is received</span></span>
* <span data-ttu-id="a8862-106">Wait for an approval before continuing a workflow</span><span class="sxs-lookup"><span data-stu-id="a8862-106">Wait for an approval before continuing a workflow</span></span>

<span data-ttu-id="a8862-107">Learn more about [how to create custom APIs that support a webhook](../logic-apps/logic-apps-create-api-app.md).</span><span class="sxs-lookup"><span data-stu-id="a8862-107">Learn more about [how to create custom APIs that support a webhook](../logic-apps/logic-apps-create-api-app.md).</span></span>

## <a name="use-the-webhook-trigger"></a><span data-ttu-id="a8862-108">Use the webhook trigger</span><span class="sxs-lookup"><span data-stu-id="a8862-108">Use the webhook trigger</span></span>

<span data-ttu-id="a8862-109">A [*trigger*](connectors-overview.md) is an event that starts a logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="a8862-109">A [*trigger*](connectors-overview.md) is an event that starts a logic app workflow.</span></span> <span data-ttu-id="a8862-110">A webhook trigger is event-based and doesn't rely on polling for new items.</span><span class="sxs-lookup"><span data-stu-id="a8862-110">A webhook trigger is event-based and doesn't rely on polling for new items.</span></span> <span data-ttu-id="a8862-111">Like the [request trigger](connectors-native-reqres.md), the logic app fires the instant that an event happens.</span><span class="sxs-lookup"><span data-stu-id="a8862-111">Like the [request trigger](connectors-native-reqres.md), the logic app fires the instant that an event happens.</span></span> <span data-ttu-id="a8862-112">The webhook trigger registers a *callback URL* to a service and uses that URL to fire the logic app as needed.</span><span class="sxs-lookup"><span data-stu-id="a8862-112">The webhook trigger registers a *callback URL* to a service and uses that URL to fire the logic app as needed.</span></span>

<span data-ttu-id="a8862-113">Here's an example that shows how to set up an HTTP trigger in the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="a8862-113">Here's an example that shows how to set up an HTTP trigger in the Logic App Designer.</span></span> <span data-ttu-id="a8862-114">The steps assume that you have already deployed or are accessing an API that follows the [webhook subscribe and unsubscribe pattern in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-triggers).</span><span class="sxs-lookup"><span data-stu-id="a8862-114">The steps assume that you have already deployed or are accessing an API that follows the [webhook subscribe and unsubscribe pattern in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-triggers).</span></span> <span data-ttu-id="a8862-115">The subscribe call is made whenever a logic app is saved with a new webhook, or switched from disabled to enabled.</span><span class="sxs-lookup"><span data-stu-id="a8862-115">The subscribe call is made whenever a logic app is saved with a new webhook, or switched from disabled to enabled.</span></span> <span data-ttu-id="a8862-116">The unsubscribe call is made when a logic app webhook trigger is removed and saved, or switched from enabled to disabled.</span><span class="sxs-lookup"><span data-stu-id="a8862-116">The unsubscribe call is made when a logic app webhook trigger is removed and saved, or switched from enabled to disabled.</span></span>

<span data-ttu-id="a8862-117">**To add the webhook trigger**</span><span class="sxs-lookup"><span data-stu-id="a8862-117">**To add the webhook trigger**</span></span>

1. <span data-ttu-id="a8862-118">Add the **HTTP Webhook** trigger as the first step in a logic app.</span><span class="sxs-lookup"><span data-stu-id="a8862-118">Add the **HTTP Webhook** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="a8862-119">Fill in the parameters for the webhook subscribe and unsubscribe calls.</span><span class="sxs-lookup"><span data-stu-id="a8862-119">Fill in the parameters for the webhook subscribe and unsubscribe calls.</span></span>

   <span data-ttu-id="a8862-120">This step follows the same pattern as the [HTTP action](connectors-native-http.md) format.</span><span class="sxs-lookup"><span data-stu-id="a8862-120">This step follows the same pattern as the [HTTP action](connectors-native-http.md) format.</span></span>

     ![HTTP Trigger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-webhook/using-trigger.png)

3. <span data-ttu-id="a8862-122">Add at least one action.</span><span class="sxs-lookup"><span data-stu-id="a8862-122">Add at least one action.</span></span>
4. <span data-ttu-id="a8862-123">Click **Save** to publish the logic app.</span><span class="sxs-lookup"><span data-stu-id="a8862-123">Click **Save** to publish the logic app.</span></span> <span data-ttu-id="a8862-124">This step calls the subscribe endpoint with the callback URL needed to trigger this logic app.</span><span class="sxs-lookup"><span data-stu-id="a8862-124">This step calls the subscribe endpoint with the callback URL needed to trigger this logic app.</span></span>
5. <span data-ttu-id="a8862-125">Whenever the service makes an `HTTP POST` to the callback URL, the logic app fires, and includes any data passed into the request.</span><span class="sxs-lookup"><span data-stu-id="a8862-125">Whenever the service makes an `HTTP POST` to the callback URL, the logic app fires, and includes any data passed into the request.</span></span>

## <a name="use-the-webhook-action"></a><span data-ttu-id="a8862-126">Use the webhook action</span><span class="sxs-lookup"><span data-stu-id="a8862-126">Use the webhook action</span></span>

<span data-ttu-id="a8862-127">An [*action*](connectors-overview.md) is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="a8862-127">An [*action*](connectors-overview.md) is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="a8862-128">A webhook action registers a *callback URL* with a service and waits until the URL is called before resuming.</span><span class="sxs-lookup"><span data-stu-id="a8862-128">A webhook action registers a *callback URL* with a service and waits until the URL is called before resuming.</span></span> <span data-ttu-id="a8862-129">The ["Send Approval Email"](connectors-create-api-office365-outlook.md) is an example of a connector that follows this pattern.</span><span class="sxs-lookup"><span data-stu-id="a8862-129">The ["Send Approval Email"](connectors-create-api-office365-outlook.md) is an example of a connector that follows this pattern.</span></span> <span data-ttu-id="a8862-130">You can extend this pattern into any service through the webhook action.</span><span class="sxs-lookup"><span data-stu-id="a8862-130">You can extend this pattern into any service through the webhook action.</span></span> 

<span data-ttu-id="a8862-131">Here's an example that shows how to set up a webhook action in the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="a8862-131">Here's an example that shows how to set up a webhook action in the Logic App Designer.</span></span> <span data-ttu-id="a8862-132">These steps assume that you have already deployed or are accessing an API that follows the [webhook subscribe and unsubscribe pattern used in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-actions).</span><span class="sxs-lookup"><span data-stu-id="a8862-132">These steps assume that you have already deployed or are accessing an API that follows the [webhook subscribe and unsubscribe pattern used in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-actions).</span></span> <span data-ttu-id="a8862-133">The subscribe call is made when a logic app executes the webhook action.</span><span class="sxs-lookup"><span data-stu-id="a8862-133">The subscribe call is made when a logic app executes the webhook action.</span></span> <span data-ttu-id="a8862-134">The unsubscribe call is made when a run is canceled while waiting for a response, or before the logic app times out.</span><span class="sxs-lookup"><span data-stu-id="a8862-134">The unsubscribe call is made when a run is canceled while waiting for a response, or before the logic app times out.</span></span>

<span data-ttu-id="a8862-135">**To add a webhook action**</span><span class="sxs-lookup"><span data-stu-id="a8862-135">**To add a webhook action**</span></span>

1. <span data-ttu-id="a8862-136">Choose **New Step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="a8862-136">Choose **New Step** > **Add an action**.</span></span>

2. <span data-ttu-id="a8862-137">In the search box, type "webhook" to find the **HTTP Webhook** action.</span><span class="sxs-lookup"><span data-stu-id="a8862-137">In the search box, type "webhook" to find the **HTTP Webhook** action.</span></span>

    ![Select query action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-webhook/using-action-1.png)

3. <span data-ttu-id="a8862-139">Fill in the parameters for the webhook subscribe and unsubscribe calls</span><span class="sxs-lookup"><span data-stu-id="a8862-139">Fill in the parameters for the webhook subscribe and unsubscribe calls</span></span>

   <span data-ttu-id="a8862-140">This step follows the same pattern as the [HTTP action](connectors-native-http.md) format.</span><span class="sxs-lookup"><span data-stu-id="a8862-140">This step follows the same pattern as the [HTTP action](connectors-native-http.md) format.</span></span>

     ![Complete query action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-webhook/using-action-2.png)
   
   <span data-ttu-id="a8862-142">At runtime, the logic app calls the subscribe endpoint after reaching that step.</span><span class="sxs-lookup"><span data-stu-id="a8862-142">At runtime, the logic app calls the subscribe endpoint after reaching that step.</span></span>

4. <span data-ttu-id="a8862-143">Click **Save** to publish the logic app.</span><span class="sxs-lookup"><span data-stu-id="a8862-143">Click **Save** to publish the logic app.</span></span>

## <a name="technical-details"></a><span data-ttu-id="a8862-144">Technical details</span><span class="sxs-lookup"><span data-stu-id="a8862-144">Technical details</span></span>

<span data-ttu-id="a8862-145">Here are more details about the triggers and actions that webhook supports.</span><span class="sxs-lookup"><span data-stu-id="a8862-145">Here are more details about the triggers and actions that webhook supports.</span></span>

## <a name="webhook-triggers"></a><span data-ttu-id="a8862-146">Webhook triggers</span><span class="sxs-lookup"><span data-stu-id="a8862-146">Webhook triggers</span></span>

| <span data-ttu-id="a8862-147">Action</span><span class="sxs-lookup"><span data-stu-id="a8862-147">Action</span></span> | <span data-ttu-id="a8862-148">Description</span><span class="sxs-lookup"><span data-stu-id="a8862-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a8862-149">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="a8862-149">HTTP Webhook</span></span> |<span data-ttu-id="a8862-150">Subscribe a callback URL to a service that can call the URL to fire logic app as needed.</span><span class="sxs-lookup"><span data-stu-id="a8862-150">Subscribe a callback URL to a service that can call the URL to fire logic app as needed.</span></span> |

### <a name="trigger-details"></a><span data-ttu-id="a8862-151">Trigger details</span><span class="sxs-lookup"><span data-stu-id="a8862-151">Trigger details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="a8862-152">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="a8862-152">HTTP Webhook</span></span>

<span data-ttu-id="a8862-153">Subscribe a callback URL to a service that can call the URL to fire logic app as needed.</span><span class="sxs-lookup"><span data-stu-id="a8862-153">Subscribe a callback URL to a service that can call the URL to fire logic app as needed.</span></span>
<span data-ttu-id="a8862-154">An \* means required field.</span><span class="sxs-lookup"><span data-stu-id="a8862-154">An \* means required field.</span></span>

| <span data-ttu-id="a8862-155">Display Name</span><span class="sxs-lookup"><span data-stu-id="a8862-155">Display Name</span></span> | <span data-ttu-id="a8862-156">Property Name</span><span class="sxs-lookup"><span data-stu-id="a8862-156">Property Name</span></span> | <span data-ttu-id="a8862-157">Description</span><span class="sxs-lookup"><span data-stu-id="a8862-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a8862-158">Subscribe Method\*</span><span class="sxs-lookup"><span data-stu-id="a8862-158">Subscribe Method\*</span></span> |<span data-ttu-id="a8862-159">method</span><span class="sxs-lookup"><span data-stu-id="a8862-159">method</span></span> |<span data-ttu-id="a8862-160">HTTP Method to use for subscribe request</span><span class="sxs-lookup"><span data-stu-id="a8862-160">HTTP Method to use for subscribe request</span></span> |
| <span data-ttu-id="a8862-161">Subscribe URI\*</span><span class="sxs-lookup"><span data-stu-id="a8862-161">Subscribe URI\*</span></span> |<span data-ttu-id="a8862-162">uri</span><span class="sxs-lookup"><span data-stu-id="a8862-162">uri</span></span> |<span data-ttu-id="a8862-163">HTTP URI to use for subscribe request</span><span class="sxs-lookup"><span data-stu-id="a8862-163">HTTP URI to use for subscribe request</span></span> |
| <span data-ttu-id="a8862-164">Unsubscribe Method\*</span><span class="sxs-lookup"><span data-stu-id="a8862-164">Unsubscribe Method\*</span></span> |<span data-ttu-id="a8862-165">method</span><span class="sxs-lookup"><span data-stu-id="a8862-165">method</span></span> |<span data-ttu-id="a8862-166">HTTP method to use for unsubscribe request</span><span class="sxs-lookup"><span data-stu-id="a8862-166">HTTP method to use for unsubscribe request</span></span> |
| <span data-ttu-id="a8862-167">Unsubscribe URI\*</span><span class="sxs-lookup"><span data-stu-id="a8862-167">Unsubscribe URI\*</span></span> |<span data-ttu-id="a8862-168">uri</span><span class="sxs-lookup"><span data-stu-id="a8862-168">uri</span></span> |<span data-ttu-id="a8862-169">HTTP URI to use for unsubscribe request</span><span class="sxs-lookup"><span data-stu-id="a8862-169">HTTP URI to use for unsubscribe request</span></span> |
| <span data-ttu-id="a8862-170">Subscribe Body</span><span class="sxs-lookup"><span data-stu-id="a8862-170">Subscribe Body</span></span> |<span data-ttu-id="a8862-171">body</span><span class="sxs-lookup"><span data-stu-id="a8862-171">body</span></span> |<span data-ttu-id="a8862-172">HTTP request body for subscribe</span><span class="sxs-lookup"><span data-stu-id="a8862-172">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="a8862-173">Subscribe Headers</span><span class="sxs-lookup"><span data-stu-id="a8862-173">Subscribe Headers</span></span> |<span data-ttu-id="a8862-174">headers</span><span class="sxs-lookup"><span data-stu-id="a8862-174">headers</span></span> |<span data-ttu-id="a8862-175">HTTP request headers for subscribe</span><span class="sxs-lookup"><span data-stu-id="a8862-175">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="a8862-176">Subscribe Authentication</span><span class="sxs-lookup"><span data-stu-id="a8862-176">Subscribe Authentication</span></span> |<span data-ttu-id="a8862-177">authentication</span><span class="sxs-lookup"><span data-stu-id="a8862-177">authentication</span></span> |<span data-ttu-id="a8862-178">HTTP authentication to use for subscribe.</span><span class="sxs-lookup"><span data-stu-id="a8862-178">HTTP authentication to use for subscribe.</span></span> <span data-ttu-id="a8862-179">[See HTTP connector](connectors-native-http.md#authentication) for details</span><span class="sxs-lookup"><span data-stu-id="a8862-179">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="a8862-180">Unsubscribe Body</span><span class="sxs-lookup"><span data-stu-id="a8862-180">Unsubscribe Body</span></span> |<span data-ttu-id="a8862-181">body</span><span class="sxs-lookup"><span data-stu-id="a8862-181">body</span></span> |<span data-ttu-id="a8862-182">HTTP request body for unsubscribe</span><span class="sxs-lookup"><span data-stu-id="a8862-182">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="a8862-183">Unsubscribe Headers</span><span class="sxs-lookup"><span data-stu-id="a8862-183">Unsubscribe Headers</span></span> |<span data-ttu-id="a8862-184">headers</span><span class="sxs-lookup"><span data-stu-id="a8862-184">headers</span></span> |<span data-ttu-id="a8862-185">HTTP request headers for unsubscribe</span><span class="sxs-lookup"><span data-stu-id="a8862-185">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="a8862-186">Unsubscribe Authentication</span><span class="sxs-lookup"><span data-stu-id="a8862-186">Unsubscribe Authentication</span></span> |<span data-ttu-id="a8862-187">authentication</span><span class="sxs-lookup"><span data-stu-id="a8862-187">authentication</span></span> |<span data-ttu-id="a8862-188">HTTP authentication to use for unsubscribe.</span><span class="sxs-lookup"><span data-stu-id="a8862-188">HTTP authentication to use for unsubscribe.</span></span> <span data-ttu-id="a8862-189">[See HTTP connector](connectors-native-http.md#authentication) for details</span><span class="sxs-lookup"><span data-stu-id="a8862-189">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="a8862-190">**Output Details**</span><span class="sxs-lookup"><span data-stu-id="a8862-190">**Output Details**</span></span>

<span data-ttu-id="a8862-191">Webhook request</span><span class="sxs-lookup"><span data-stu-id="a8862-191">Webhook request</span></span>

| <span data-ttu-id="a8862-192">Property Name</span><span class="sxs-lookup"><span data-stu-id="a8862-192">Property Name</span></span> | <span data-ttu-id="a8862-193">Data Type</span><span class="sxs-lookup"><span data-stu-id="a8862-193">Data Type</span></span> | <span data-ttu-id="a8862-194">Description</span><span class="sxs-lookup"><span data-stu-id="a8862-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a8862-195">Headers</span><span class="sxs-lookup"><span data-stu-id="a8862-195">Headers</span></span> |<span data-ttu-id="a8862-196">object</span><span class="sxs-lookup"><span data-stu-id="a8862-196">object</span></span> |<span data-ttu-id="a8862-197">Webhook request headers</span><span class="sxs-lookup"><span data-stu-id="a8862-197">Webhook request headers</span></span> |
| <span data-ttu-id="a8862-198">Body</span><span class="sxs-lookup"><span data-stu-id="a8862-198">Body</span></span> |<span data-ttu-id="a8862-199">object</span><span class="sxs-lookup"><span data-stu-id="a8862-199">object</span></span> |<span data-ttu-id="a8862-200">Webhook request object</span><span class="sxs-lookup"><span data-stu-id="a8862-200">Webhook request object</span></span> |
| <span data-ttu-id="a8862-201">Status Code</span><span class="sxs-lookup"><span data-stu-id="a8862-201">Status Code</span></span> |<span data-ttu-id="a8862-202">int</span><span class="sxs-lookup"><span data-stu-id="a8862-202">int</span></span> |<span data-ttu-id="a8862-203">Webhook request status code</span><span class="sxs-lookup"><span data-stu-id="a8862-203">Webhook request status code</span></span> |

## <a name="webhook-actions"></a><span data-ttu-id="a8862-204">Webhook actions</span><span class="sxs-lookup"><span data-stu-id="a8862-204">Webhook actions</span></span>

| <span data-ttu-id="a8862-205">Action</span><span class="sxs-lookup"><span data-stu-id="a8862-205">Action</span></span> | <span data-ttu-id="a8862-206">Description</span><span class="sxs-lookup"><span data-stu-id="a8862-206">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a8862-207">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="a8862-207">HTTP Webhook</span></span> |<span data-ttu-id="a8862-208">Subscribe a callback URL to a service that can call the URL to resume a workflow step as needed.</span><span class="sxs-lookup"><span data-stu-id="a8862-208">Subscribe a callback URL to a service that can call the URL to resume a workflow step as needed.</span></span> |

### <a name="action-details"></a><span data-ttu-id="a8862-209">Action details</span><span class="sxs-lookup"><span data-stu-id="a8862-209">Action details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="a8862-210">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="a8862-210">HTTP Webhook</span></span>

<span data-ttu-id="a8862-211">Subscribe a callback URL to a service that can call the URL to resume a workflow step as needed.</span><span class="sxs-lookup"><span data-stu-id="a8862-211">Subscribe a callback URL to a service that can call the URL to resume a workflow step as needed.</span></span>
<span data-ttu-id="a8862-212">An \* means required field.</span><span class="sxs-lookup"><span data-stu-id="a8862-212">An \* means required field.</span></span>

| <span data-ttu-id="a8862-213">Display Name</span><span class="sxs-lookup"><span data-stu-id="a8862-213">Display Name</span></span> | <span data-ttu-id="a8862-214">Property Name</span><span class="sxs-lookup"><span data-stu-id="a8862-214">Property Name</span></span> | <span data-ttu-id="a8862-215">Description</span><span class="sxs-lookup"><span data-stu-id="a8862-215">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a8862-216">Subscribe Method\*</span><span class="sxs-lookup"><span data-stu-id="a8862-216">Subscribe Method\*</span></span> |<span data-ttu-id="a8862-217">method</span><span class="sxs-lookup"><span data-stu-id="a8862-217">method</span></span> |<span data-ttu-id="a8862-218">HTTP Method to use for subscribe request</span><span class="sxs-lookup"><span data-stu-id="a8862-218">HTTP Method to use for subscribe request</span></span> |
| <span data-ttu-id="a8862-219">Subscribe URI\*</span><span class="sxs-lookup"><span data-stu-id="a8862-219">Subscribe URI\*</span></span> |<span data-ttu-id="a8862-220">uri</span><span class="sxs-lookup"><span data-stu-id="a8862-220">uri</span></span> |<span data-ttu-id="a8862-221">HTTP URI to use for subscribe request</span><span class="sxs-lookup"><span data-stu-id="a8862-221">HTTP URI to use for subscribe request</span></span> |
| <span data-ttu-id="a8862-222">Unsubscribe Method\*</span><span class="sxs-lookup"><span data-stu-id="a8862-222">Unsubscribe Method\*</span></span> |<span data-ttu-id="a8862-223">method</span><span class="sxs-lookup"><span data-stu-id="a8862-223">method</span></span> |<span data-ttu-id="a8862-224">HTTP method to use for unsubscribe request</span><span class="sxs-lookup"><span data-stu-id="a8862-224">HTTP method to use for unsubscribe request</span></span> |
| <span data-ttu-id="a8862-225">Unsubscribe URI\*</span><span class="sxs-lookup"><span data-stu-id="a8862-225">Unsubscribe URI\*</span></span> |<span data-ttu-id="a8862-226">uri</span><span class="sxs-lookup"><span data-stu-id="a8862-226">uri</span></span> |<span data-ttu-id="a8862-227">HTTP URI to use for unsubscribe request</span><span class="sxs-lookup"><span data-stu-id="a8862-227">HTTP URI to use for unsubscribe request</span></span> |
| <span data-ttu-id="a8862-228">Subscribe Body</span><span class="sxs-lookup"><span data-stu-id="a8862-228">Subscribe Body</span></span> |<span data-ttu-id="a8862-229">body</span><span class="sxs-lookup"><span data-stu-id="a8862-229">body</span></span> |<span data-ttu-id="a8862-230">HTTP request body for subscribe</span><span class="sxs-lookup"><span data-stu-id="a8862-230">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="a8862-231">Subscribe Headers</span><span class="sxs-lookup"><span data-stu-id="a8862-231">Subscribe Headers</span></span> |<span data-ttu-id="a8862-232">headers</span><span class="sxs-lookup"><span data-stu-id="a8862-232">headers</span></span> |<span data-ttu-id="a8862-233">HTTP request headers for subscribe</span><span class="sxs-lookup"><span data-stu-id="a8862-233">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="a8862-234">Subscribe Authentication</span><span class="sxs-lookup"><span data-stu-id="a8862-234">Subscribe Authentication</span></span> |<span data-ttu-id="a8862-235">authentication</span><span class="sxs-lookup"><span data-stu-id="a8862-235">authentication</span></span> |<span data-ttu-id="a8862-236">HTTP authentication to use for subscribe.</span><span class="sxs-lookup"><span data-stu-id="a8862-236">HTTP authentication to use for subscribe.</span></span> <span data-ttu-id="a8862-237">[See HTTP connector](connectors-native-http.md#authentication) for details</span><span class="sxs-lookup"><span data-stu-id="a8862-237">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="a8862-238">Unsubscribe Body</span><span class="sxs-lookup"><span data-stu-id="a8862-238">Unsubscribe Body</span></span> |<span data-ttu-id="a8862-239">body</span><span class="sxs-lookup"><span data-stu-id="a8862-239">body</span></span> |<span data-ttu-id="a8862-240">HTTP request body for unsubscribe</span><span class="sxs-lookup"><span data-stu-id="a8862-240">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="a8862-241">Unsubscribe Headers</span><span class="sxs-lookup"><span data-stu-id="a8862-241">Unsubscribe Headers</span></span> |<span data-ttu-id="a8862-242">headers</span><span class="sxs-lookup"><span data-stu-id="a8862-242">headers</span></span> |<span data-ttu-id="a8862-243">HTTP request headers for unsubscribe</span><span class="sxs-lookup"><span data-stu-id="a8862-243">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="a8862-244">Unsubscribe Authentication</span><span class="sxs-lookup"><span data-stu-id="a8862-244">Unsubscribe Authentication</span></span> |<span data-ttu-id="a8862-245">authentication</span><span class="sxs-lookup"><span data-stu-id="a8862-245">authentication</span></span> |<span data-ttu-id="a8862-246">HTTP authentication to use for unsubscribe.</span><span class="sxs-lookup"><span data-stu-id="a8862-246">HTTP authentication to use for unsubscribe.</span></span> <span data-ttu-id="a8862-247">[See HTTP connector](connectors-native-http.md#authentication) for details</span><span class="sxs-lookup"><span data-stu-id="a8862-247">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="a8862-248">**Output Details**</span><span class="sxs-lookup"><span data-stu-id="a8862-248">**Output Details**</span></span>

<span data-ttu-id="a8862-249">Webhook request</span><span class="sxs-lookup"><span data-stu-id="a8862-249">Webhook request</span></span>

| <span data-ttu-id="a8862-250">Property Name</span><span class="sxs-lookup"><span data-stu-id="a8862-250">Property Name</span></span> | <span data-ttu-id="a8862-251">Data Type</span><span class="sxs-lookup"><span data-stu-id="a8862-251">Data Type</span></span> | <span data-ttu-id="a8862-252">Description</span><span class="sxs-lookup"><span data-stu-id="a8862-252">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a8862-253">Headers</span><span class="sxs-lookup"><span data-stu-id="a8862-253">Headers</span></span> |<span data-ttu-id="a8862-254">object</span><span class="sxs-lookup"><span data-stu-id="a8862-254">object</span></span> |<span data-ttu-id="a8862-255">Webhook request headers</span><span class="sxs-lookup"><span data-stu-id="a8862-255">Webhook request headers</span></span> |
| <span data-ttu-id="a8862-256">Body</span><span class="sxs-lookup"><span data-stu-id="a8862-256">Body</span></span> |<span data-ttu-id="a8862-257">object</span><span class="sxs-lookup"><span data-stu-id="a8862-257">object</span></span> |<span data-ttu-id="a8862-258">Webhook request object</span><span class="sxs-lookup"><span data-stu-id="a8862-258">Webhook request object</span></span> |
| <span data-ttu-id="a8862-259">Status Code</span><span class="sxs-lookup"><span data-stu-id="a8862-259">Status Code</span></span> |<span data-ttu-id="a8862-260">int</span><span class="sxs-lookup"><span data-stu-id="a8862-260">int</span></span> |<span data-ttu-id="a8862-261">Webhook request status code</span><span class="sxs-lookup"><span data-stu-id="a8862-261">Webhook request status code</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a8862-262">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8862-262">Next steps</span></span>

* [<span data-ttu-id="a8862-263">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="a8862-263">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="a8862-264">Find other connectors</span><span class="sxs-lookup"><span data-stu-id="a8862-264">Find other connectors</span></span>](apis-list.md)


