---
title: Use request and response actions | Microsoft Docs
description: Overview of the request and response trigger and action in an Azure logic app
services: ''
documentationcenter: ''
author: jeffhollan
manager: erikre
editor: ''
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 5b6aafada87dee5bb5bd5a7ce392770411f7520e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552327"
---
# <a name="get-started-with-the-request-and-response-components"></a><span data-ttu-id="c9ca1-103">Get started with the request and response components</span><span class="sxs-lookup"><span data-stu-id="c9ca1-103">Get started with the request and response components</span></span>
<span data-ttu-id="c9ca1-104">With the request and response components in a logic app, you can respond in real time to events.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-104">With the request and response components in a logic app, you can respond in real time to events.</span></span>

<span data-ttu-id="c9ca1-105">For example, you can:</span><span class="sxs-lookup"><span data-stu-id="c9ca1-105">For example, you can:</span></span>

* <span data-ttu-id="c9ca1-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="c9ca1-107">Trigger a logic app from an external webhook event.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="c9ca1-108">Call a logic app with a request and response action from within another logic app.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="c9ca1-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c9ca1-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-request-trigger"></a><span data-ttu-id="c9ca1-110">Use the HTTP Request trigger</span><span class="sxs-lookup"><span data-stu-id="c9ca1-110">Use the HTTP Request trigger</span></span>
<span data-ttu-id="c9ca1-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="c9ca1-112">[Learn more about triggers](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9ca1-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="c9ca1-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span></span>

1. <span data-ttu-id="c9ca1-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="c9ca1-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span></span> <span data-ttu-id="c9ca1-116">This allows the designer to generate tokens for properties in the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-116">This allows the designer to generate tokens for properties in the HTTP request.</span></span>
2. <span data-ttu-id="c9ca1-117">Add another action so that you can save the logic app.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-117">Add another action so that you can save the logic app.</span></span>
3. <span data-ttu-id="c9ca1-118">After saving the logic app, you can get the HTTP request URL from the request card.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-118">After saving the logic app, you can get the HTTP request URL from the request card.</span></span>
4. <span data-ttu-id="c9ca1-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="c9ca1-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span> <span data-ttu-id="c9ca1-121">You can use the response action to customize a response.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-121">You can use the response action to customize a response.</span></span>
> 
> 

![Response trigger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a><span data-ttu-id="c9ca1-123">Use the HTTP Response action</span><span class="sxs-lookup"><span data-stu-id="c9ca1-123">Use the HTTP Response action</span></span>
<span data-ttu-id="c9ca1-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="c9ca1-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span>  <span data-ttu-id="c9ca1-126">You can add a response action at any step within the workflow.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-126">You can add a response action at any step within the workflow.</span></span> <span data-ttu-id="c9ca1-127">The logic app only keeps the incoming request open for one minute for a response.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-127">The logic app only keeps the incoming request open for one minute for a response.</span></span>  <span data-ttu-id="c9ca1-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span></span>

<span data-ttu-id="c9ca1-129">Here's how to add an HTTP Response action:</span><span class="sxs-lookup"><span data-stu-id="c9ca1-129">Here's how to add an HTTP Response action:</span></span>

1. <span data-ttu-id="c9ca1-130">Select the **New Step** button.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-130">Select the **New Step** button.</span></span>
2. <span data-ttu-id="c9ca1-131">Choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="c9ca1-132">In the action search box, type **response** to list the Response action.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-132">In the action search box, type **response** to list the Response action.</span></span>
   
    ![Select the response action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="c9ca1-134">Add in any parameters that are required for the HTTP response message.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-134">Add in any parameters that are required for the HTTP response message.</span></span>
   
    ![Complete the response action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="c9ca1-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span><span class="sxs-lookup"><span data-stu-id="c9ca1-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="c9ca1-137">Request trigger</span><span class="sxs-lookup"><span data-stu-id="c9ca1-137">Request trigger</span></span>
<span data-ttu-id="c9ca1-138">Here are the details for the trigger that this connector supports.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-138">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="c9ca1-139">There is a single request trigger.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-139">There is a single request trigger.</span></span>

| <span data-ttu-id="c9ca1-140">Trigger</span><span class="sxs-lookup"><span data-stu-id="c9ca1-140">Trigger</span></span> | <span data-ttu-id="c9ca1-141">Description</span><span class="sxs-lookup"><span data-stu-id="c9ca1-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c9ca1-142">Request</span><span class="sxs-lookup"><span data-stu-id="c9ca1-142">Request</span></span> |<span data-ttu-id="c9ca1-143">Occurs when an HTTP request is received</span><span class="sxs-lookup"><span data-stu-id="c9ca1-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="c9ca1-144">Response action</span><span class="sxs-lookup"><span data-stu-id="c9ca1-144">Response action</span></span>
<span data-ttu-id="c9ca1-145">Here are the details for the action that this connector supports.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-145">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="c9ca1-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="c9ca1-147">Action</span><span class="sxs-lookup"><span data-stu-id="c9ca1-147">Action</span></span> | <span data-ttu-id="c9ca1-148">Description</span><span class="sxs-lookup"><span data-stu-id="c9ca1-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c9ca1-149">Response</span><span class="sxs-lookup"><span data-stu-id="c9ca1-149">Response</span></span> |<span data-ttu-id="c9ca1-150">Returns a response to the correlated HTTP request</span><span class="sxs-lookup"><span data-stu-id="c9ca1-150">Returns a response to the correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="c9ca1-151">Trigger and action details</span><span class="sxs-lookup"><span data-stu-id="c9ca1-151">Trigger and action details</span></span>
<span data-ttu-id="c9ca1-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="c9ca1-153">Request trigger</span><span class="sxs-lookup"><span data-stu-id="c9ca1-153">Request trigger</span></span>
<span data-ttu-id="c9ca1-154">The following is an input field for the trigger from an incoming HTTP request.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-154">The following is an input field for the trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="c9ca1-155">Display name</span><span class="sxs-lookup"><span data-stu-id="c9ca1-155">Display name</span></span> | <span data-ttu-id="c9ca1-156">Property name</span><span class="sxs-lookup"><span data-stu-id="c9ca1-156">Property name</span></span> | <span data-ttu-id="c9ca1-157">Description</span><span class="sxs-lookup"><span data-stu-id="c9ca1-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c9ca1-158">JSON Schema</span><span class="sxs-lookup"><span data-stu-id="c9ca1-158">JSON Schema</span></span> |<span data-ttu-id="c9ca1-159">schema</span><span class="sxs-lookup"><span data-stu-id="c9ca1-159">schema</span></span> |<span data-ttu-id="c9ca1-160">The JSON schema of the HTTP request body</span><span class="sxs-lookup"><span data-stu-id="c9ca1-160">The JSON schema of the HTTP request body</span></span> |

<br>

<span data-ttu-id="c9ca1-161">**Output details**</span><span class="sxs-lookup"><span data-stu-id="c9ca1-161">**Output details**</span></span>

<span data-ttu-id="c9ca1-162">The following are output details for the request.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-162">The following are output details for the request.</span></span>

| <span data-ttu-id="c9ca1-163">Property name</span><span class="sxs-lookup"><span data-stu-id="c9ca1-163">Property name</span></span> | <span data-ttu-id="c9ca1-164">Data type</span><span class="sxs-lookup"><span data-stu-id="c9ca1-164">Data type</span></span> | <span data-ttu-id="c9ca1-165">Description</span><span class="sxs-lookup"><span data-stu-id="c9ca1-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c9ca1-166">Headers</span><span class="sxs-lookup"><span data-stu-id="c9ca1-166">Headers</span></span> |<span data-ttu-id="c9ca1-167">object</span><span class="sxs-lookup"><span data-stu-id="c9ca1-167">object</span></span> |<span data-ttu-id="c9ca1-168">Request headers</span><span class="sxs-lookup"><span data-stu-id="c9ca1-168">Request headers</span></span> |
| <span data-ttu-id="c9ca1-169">Body</span><span class="sxs-lookup"><span data-stu-id="c9ca1-169">Body</span></span> |<span data-ttu-id="c9ca1-170">object</span><span class="sxs-lookup"><span data-stu-id="c9ca1-170">object</span></span> |<span data-ttu-id="c9ca1-171">Request object</span><span class="sxs-lookup"><span data-stu-id="c9ca1-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="c9ca1-172">Response action</span><span class="sxs-lookup"><span data-stu-id="c9ca1-172">Response action</span></span>
<span data-ttu-id="c9ca1-173">The following are input fields for the HTTP Response action.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-173">The following are input fields for the HTTP Response action.</span></span> <span data-ttu-id="c9ca1-174">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="c9ca1-174">A \* means that it is a required field.</span></span>

| <span data-ttu-id="c9ca1-175">Display name</span><span class="sxs-lookup"><span data-stu-id="c9ca1-175">Display name</span></span> | <span data-ttu-id="c9ca1-176">Property name</span><span class="sxs-lookup"><span data-stu-id="c9ca1-176">Property name</span></span> | <span data-ttu-id="c9ca1-177">Description</span><span class="sxs-lookup"><span data-stu-id="c9ca1-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c9ca1-178">Status Code\*</span><span class="sxs-lookup"><span data-stu-id="c9ca1-178">Status Code\*</span></span> |<span data-ttu-id="c9ca1-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="c9ca1-179">statusCode</span></span> |<span data-ttu-id="c9ca1-180">The HTTP status code</span><span class="sxs-lookup"><span data-stu-id="c9ca1-180">The HTTP status code</span></span> |
| <span data-ttu-id="c9ca1-181">Headers</span><span class="sxs-lookup"><span data-stu-id="c9ca1-181">Headers</span></span> |<span data-ttu-id="c9ca1-182">headers</span><span class="sxs-lookup"><span data-stu-id="c9ca1-182">headers</span></span> |<span data-ttu-id="c9ca1-183">A JSON object of any response headers to include</span><span class="sxs-lookup"><span data-stu-id="c9ca1-183">A JSON object of any response headers to include</span></span> |
| <span data-ttu-id="c9ca1-184">Body</span><span class="sxs-lookup"><span data-stu-id="c9ca1-184">Body</span></span> |<span data-ttu-id="c9ca1-185">body</span><span class="sxs-lookup"><span data-stu-id="c9ca1-185">body</span></span> |<span data-ttu-id="c9ca1-186">The response body</span><span class="sxs-lookup"><span data-stu-id="c9ca1-186">The response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c9ca1-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9ca1-187">Next steps</span></span>
<span data-ttu-id="c9ca1-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c9ca1-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="c9ca1-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c9ca1-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>




