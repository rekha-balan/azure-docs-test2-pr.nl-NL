---
title: Communicate with any endpoint over HTTP - Azure Logic Apps | Microsoft Docs
description: Create logic apps that can communicate with any endpoint over HTTP
services: logic-apps
author: jeffhollan
manager: anneta
editor: ''
documentationcenter: ''
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 57dbd4c7d29da2f42855ff0cc55052f5f695f79a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554127"
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="5215c-103">Get started with the HTTP action</span><span class="sxs-lookup"><span data-stu-id="5215c-103">Get started with the HTTP action</span></span>

<span data-ttu-id="5215c-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span><span class="sxs-lookup"><span data-stu-id="5215c-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="5215c-105">You can:</span><span class="sxs-lookup"><span data-stu-id="5215c-105">You can:</span></span>

* <span data-ttu-id="5215c-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span><span class="sxs-lookup"><span data-stu-id="5215c-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="5215c-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span><span class="sxs-lookup"><span data-stu-id="5215c-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="5215c-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5215c-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="5215c-109">Use the HTTP trigger</span><span class="sxs-lookup"><span data-stu-id="5215c-109">Use the HTTP trigger</span></span>
<span data-ttu-id="5215c-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="5215c-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="5215c-111">[Learn more about triggers](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5215c-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="5215c-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="5215c-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="5215c-113">Add the HTTP trigger in your logic app.</span><span class="sxs-lookup"><span data-stu-id="5215c-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="5215c-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span><span class="sxs-lookup"><span data-stu-id="5215c-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="5215c-115">Modify the recurrence interval on how frequently it should poll.</span><span class="sxs-lookup"><span data-stu-id="5215c-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="5215c-116">The logic app now fires with any content that is returned during each check.</span><span class="sxs-lookup"><span data-stu-id="5215c-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![HTTP trigger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="5215c-118">How the HTTP trigger works</span><span class="sxs-lookup"><span data-stu-id="5215c-118">How the HTTP trigger works</span></span>

<span data-ttu-id="5215c-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span><span class="sxs-lookup"><span data-stu-id="5215c-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="5215c-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span><span class="sxs-lookup"><span data-stu-id="5215c-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="5215c-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span><span class="sxs-lookup"><span data-stu-id="5215c-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="5215c-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span><span class="sxs-lookup"><span data-stu-id="5215c-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="5215c-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="5215c-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="5215c-124">Use the HTTP action</span><span class="sxs-lookup"><span data-stu-id="5215c-124">Use the HTTP action</span></span>

<span data-ttu-id="5215c-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="5215c-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="5215c-126">[Learn more about actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5215c-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="5215c-127">Choose **New Step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="5215c-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="5215c-128">In the action search box, type **http** to list the HTTP actions.</span><span class="sxs-lookup"><span data-stu-id="5215c-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![Select the HTTP action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="5215c-130">Add any required parameters for the HTTP call.</span><span class="sxs-lookup"><span data-stu-id="5215c-130">Add any required parameters for the HTTP call.</span></span>
   
    ![Complete the HTTP action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="5215c-132">On the designer toolbar, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5215c-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="5215c-133">Your logic app is saved and published (activated) at the same time.</span><span class="sxs-lookup"><span data-stu-id="5215c-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="5215c-134">HTTP trigger</span><span class="sxs-lookup"><span data-stu-id="5215c-134">HTTP trigger</span></span>
<span data-ttu-id="5215c-135">Here are the details for the trigger that this connector supports.</span><span class="sxs-lookup"><span data-stu-id="5215c-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="5215c-136">The HTTP connector has one trigger.</span><span class="sxs-lookup"><span data-stu-id="5215c-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="5215c-137">Trigger</span><span class="sxs-lookup"><span data-stu-id="5215c-137">Trigger</span></span> | <span data-ttu-id="5215c-138">Description</span><span class="sxs-lookup"><span data-stu-id="5215c-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5215c-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="5215c-139">HTTP</span></span> |<span data-ttu-id="5215c-140">Makes an HTTP call and returns the response content.</span><span class="sxs-lookup"><span data-stu-id="5215c-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="5215c-141">HTTP action</span><span class="sxs-lookup"><span data-stu-id="5215c-141">HTTP action</span></span>
<span data-ttu-id="5215c-142">Here are the details for the action that this connector supports.</span><span class="sxs-lookup"><span data-stu-id="5215c-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="5215c-143">The HTTP connector has one possible action.</span><span class="sxs-lookup"><span data-stu-id="5215c-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="5215c-144">Action</span><span class="sxs-lookup"><span data-stu-id="5215c-144">Action</span></span> | <span data-ttu-id="5215c-145">Description</span><span class="sxs-lookup"><span data-stu-id="5215c-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5215c-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="5215c-146">HTTP</span></span> |<span data-ttu-id="5215c-147">Makes an HTTP call and returns the response content.</span><span class="sxs-lookup"><span data-stu-id="5215c-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="5215c-148">HTTP details</span><span class="sxs-lookup"><span data-stu-id="5215c-148">HTTP details</span></span>
<span data-ttu-id="5215c-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span><span class="sxs-lookup"><span data-stu-id="5215c-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="5215c-150">HTTP request</span><span class="sxs-lookup"><span data-stu-id="5215c-150">HTTP request</span></span>
<span data-ttu-id="5215c-151">The following are input fields for the action, which makes an HTTP outbound request.</span><span class="sxs-lookup"><span data-stu-id="5215c-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="5215c-152">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="5215c-152">A \* means that it is a required field.</span></span>

| <span data-ttu-id="5215c-153">Display name</span><span class="sxs-lookup"><span data-stu-id="5215c-153">Display name</span></span> | <span data-ttu-id="5215c-154">Property name</span><span class="sxs-lookup"><span data-stu-id="5215c-154">Property name</span></span> | <span data-ttu-id="5215c-155">Description</span><span class="sxs-lookup"><span data-stu-id="5215c-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5215c-156">Method\*</span><span class="sxs-lookup"><span data-stu-id="5215c-156">Method\*</span></span> |<span data-ttu-id="5215c-157">method</span><span class="sxs-lookup"><span data-stu-id="5215c-157">method</span></span> |<span data-ttu-id="5215c-158">The HTTP verb to use</span><span class="sxs-lookup"><span data-stu-id="5215c-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="5215c-159">URI\*</span><span class="sxs-lookup"><span data-stu-id="5215c-159">URI\*</span></span> |<span data-ttu-id="5215c-160">uri</span><span class="sxs-lookup"><span data-stu-id="5215c-160">uri</span></span> |<span data-ttu-id="5215c-161">The URI for the HTTP request</span><span class="sxs-lookup"><span data-stu-id="5215c-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="5215c-162">Headers</span><span class="sxs-lookup"><span data-stu-id="5215c-162">Headers</span></span> |<span data-ttu-id="5215c-163">headers</span><span class="sxs-lookup"><span data-stu-id="5215c-163">headers</span></span> |<span data-ttu-id="5215c-164">A JSON object of HTTP headers to include</span><span class="sxs-lookup"><span data-stu-id="5215c-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="5215c-165">Body</span><span class="sxs-lookup"><span data-stu-id="5215c-165">Body</span></span> |<span data-ttu-id="5215c-166">body</span><span class="sxs-lookup"><span data-stu-id="5215c-166">body</span></span> |<span data-ttu-id="5215c-167">The HTTP request body</span><span class="sxs-lookup"><span data-stu-id="5215c-167">The HTTP request body</span></span> |
| <span data-ttu-id="5215c-168">Authentication</span><span class="sxs-lookup"><span data-stu-id="5215c-168">Authentication</span></span> |<span data-ttu-id="5215c-169">authentication</span><span class="sxs-lookup"><span data-stu-id="5215c-169">authentication</span></span> |<span data-ttu-id="5215c-170">Details in the [Authentication](#authentication) section</span><span class="sxs-lookup"><span data-stu-id="5215c-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="5215c-171">Output details</span><span class="sxs-lookup"><span data-stu-id="5215c-171">Output details</span></span>
<span data-ttu-id="5215c-172">The following are output details for the HTTP response.</span><span class="sxs-lookup"><span data-stu-id="5215c-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="5215c-173">Property name</span><span class="sxs-lookup"><span data-stu-id="5215c-173">Property name</span></span> | <span data-ttu-id="5215c-174">Data type</span><span class="sxs-lookup"><span data-stu-id="5215c-174">Data type</span></span> | <span data-ttu-id="5215c-175">Description</span><span class="sxs-lookup"><span data-stu-id="5215c-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5215c-176">Headers</span><span class="sxs-lookup"><span data-stu-id="5215c-176">Headers</span></span> |<span data-ttu-id="5215c-177">object</span><span class="sxs-lookup"><span data-stu-id="5215c-177">object</span></span> |<span data-ttu-id="5215c-178">Response headers</span><span class="sxs-lookup"><span data-stu-id="5215c-178">Response headers</span></span> |
| <span data-ttu-id="5215c-179">Body</span><span class="sxs-lookup"><span data-stu-id="5215c-179">Body</span></span> |<span data-ttu-id="5215c-180">object</span><span class="sxs-lookup"><span data-stu-id="5215c-180">object</span></span> |<span data-ttu-id="5215c-181">Response object</span><span class="sxs-lookup"><span data-stu-id="5215c-181">Response object</span></span> |
| <span data-ttu-id="5215c-182">Status Code</span><span class="sxs-lookup"><span data-stu-id="5215c-182">Status Code</span></span> |<span data-ttu-id="5215c-183">int</span><span class="sxs-lookup"><span data-stu-id="5215c-183">int</span></span> |<span data-ttu-id="5215c-184">HTTP status code</span><span class="sxs-lookup"><span data-stu-id="5215c-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="5215c-185">Authentication</span><span class="sxs-lookup"><span data-stu-id="5215c-185">Authentication</span></span>
<span data-ttu-id="5215c-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span><span class="sxs-lookup"><span data-stu-id="5215c-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="5215c-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span><span class="sxs-lookup"><span data-stu-id="5215c-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="5215c-188">The following types of authentication are configurable:</span><span class="sxs-lookup"><span data-stu-id="5215c-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="5215c-189">Basic authentication</span><span class="sxs-lookup"><span data-stu-id="5215c-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="5215c-190">Client certificate authentication</span><span class="sxs-lookup"><span data-stu-id="5215c-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="5215c-191">Azure Active Directory (Azure AD) OAuth authentication</span><span class="sxs-lookup"><span data-stu-id="5215c-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="5215c-192">Basic authentication</span><span class="sxs-lookup"><span data-stu-id="5215c-192">Basic authentication</span></span>

<span data-ttu-id="5215c-193">The following authentication object is needed for basic authentication.</span><span class="sxs-lookup"><span data-stu-id="5215c-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="5215c-194">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="5215c-194">A \* means that it is a required field.</span></span>

| <span data-ttu-id="5215c-195">Property name</span><span class="sxs-lookup"><span data-stu-id="5215c-195">Property name</span></span> | <span data-ttu-id="5215c-196">Data type</span><span class="sxs-lookup"><span data-stu-id="5215c-196">Data type</span></span> | <span data-ttu-id="5215c-197">Description</span><span class="sxs-lookup"><span data-stu-id="5215c-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5215c-198">Type\*</span><span class="sxs-lookup"><span data-stu-id="5215c-198">Type\*</span></span> |<span data-ttu-id="5215c-199">type</span><span class="sxs-lookup"><span data-stu-id="5215c-199">type</span></span> |<span data-ttu-id="5215c-200">Type of authentication (must be `Basic` for basic authentication)</span><span class="sxs-lookup"><span data-stu-id="5215c-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="5215c-201">Username\*</span><span class="sxs-lookup"><span data-stu-id="5215c-201">Username\*</span></span> |<span data-ttu-id="5215c-202">username</span><span class="sxs-lookup"><span data-stu-id="5215c-202">username</span></span> |<span data-ttu-id="5215c-203">User name to authenticate</span><span class="sxs-lookup"><span data-stu-id="5215c-203">User name to authenticate</span></span> |
| <span data-ttu-id="5215c-204">Password\*</span><span class="sxs-lookup"><span data-stu-id="5215c-204">Password\*</span></span> |<span data-ttu-id="5215c-205">password</span><span class="sxs-lookup"><span data-stu-id="5215c-205">password</span></span> |<span data-ttu-id="5215c-206">Password to authenticate</span><span class="sxs-lookup"><span data-stu-id="5215c-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="5215c-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="5215c-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="5215c-208">For example:</span><span class="sxs-lookup"><span data-stu-id="5215c-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="5215c-209">Client certificate authentication</span><span class="sxs-lookup"><span data-stu-id="5215c-209">Client certificate authentication</span></span>

<span data-ttu-id="5215c-210">The following authentication object is needed for client certificate authentication.</span><span class="sxs-lookup"><span data-stu-id="5215c-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="5215c-211">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="5215c-211">A \* means that it is a required field.</span></span>

| <span data-ttu-id="5215c-212">Property name</span><span class="sxs-lookup"><span data-stu-id="5215c-212">Property name</span></span> | <span data-ttu-id="5215c-213">Data type</span><span class="sxs-lookup"><span data-stu-id="5215c-213">Data type</span></span> | <span data-ttu-id="5215c-214">Description</span><span class="sxs-lookup"><span data-stu-id="5215c-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5215c-215">Type\*</span><span class="sxs-lookup"><span data-stu-id="5215c-215">Type\*</span></span> |<span data-ttu-id="5215c-216">type</span><span class="sxs-lookup"><span data-stu-id="5215c-216">type</span></span> |<span data-ttu-id="5215c-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span><span class="sxs-lookup"><span data-stu-id="5215c-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="5215c-218">PFX\*</span><span class="sxs-lookup"><span data-stu-id="5215c-218">PFX\*</span></span> |<span data-ttu-id="5215c-219">pfx</span><span class="sxs-lookup"><span data-stu-id="5215c-219">pfx</span></span> |<span data-ttu-id="5215c-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span><span class="sxs-lookup"><span data-stu-id="5215c-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="5215c-221">Password\*</span><span class="sxs-lookup"><span data-stu-id="5215c-221">Password\*</span></span> |<span data-ttu-id="5215c-222">password</span><span class="sxs-lookup"><span data-stu-id="5215c-222">password</span></span> |<span data-ttu-id="5215c-223">The password to access the PFX file</span><span class="sxs-lookup"><span data-stu-id="5215c-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="5215c-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="5215c-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="5215c-225">For example:</span><span class="sxs-lookup"><span data-stu-id="5215c-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="5215c-226">Azure AD OAuth authentication</span><span class="sxs-lookup"><span data-stu-id="5215c-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="5215c-227">The following authentication object is needed for Azure AD OAuth authentication.</span><span class="sxs-lookup"><span data-stu-id="5215c-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="5215c-228">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="5215c-228">A \* means that it is a required field.</span></span>

| <span data-ttu-id="5215c-229">Property name</span><span class="sxs-lookup"><span data-stu-id="5215c-229">Property name</span></span> | <span data-ttu-id="5215c-230">Data type</span><span class="sxs-lookup"><span data-stu-id="5215c-230">Data type</span></span> | <span data-ttu-id="5215c-231">Description</span><span class="sxs-lookup"><span data-stu-id="5215c-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5215c-232">Type\*</span><span class="sxs-lookup"><span data-stu-id="5215c-232">Type\*</span></span> |<span data-ttu-id="5215c-233">type</span><span class="sxs-lookup"><span data-stu-id="5215c-233">type</span></span> |<span data-ttu-id="5215c-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span><span class="sxs-lookup"><span data-stu-id="5215c-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="5215c-235">Tenant\*</span><span class="sxs-lookup"><span data-stu-id="5215c-235">Tenant\*</span></span> |<span data-ttu-id="5215c-236">tenant</span><span class="sxs-lookup"><span data-stu-id="5215c-236">tenant</span></span> |<span data-ttu-id="5215c-237">The tenant identifier for the Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="5215c-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="5215c-238">Audience\*</span><span class="sxs-lookup"><span data-stu-id="5215c-238">Audience\*</span></span> |<span data-ttu-id="5215c-239">audience</span><span class="sxs-lookup"><span data-stu-id="5215c-239">audience</span></span> |<span data-ttu-id="5215c-240">The resource you are requesting authorization to use.</span><span class="sxs-lookup"><span data-stu-id="5215c-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="5215c-241">For example: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="5215c-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="5215c-242">Client ID\*</span><span class="sxs-lookup"><span data-stu-id="5215c-242">Client ID\*</span></span> |<span data-ttu-id="5215c-243">clientId</span><span class="sxs-lookup"><span data-stu-id="5215c-243">clientId</span></span> |<span data-ttu-id="5215c-244">The client identifier for the Azure AD application</span><span class="sxs-lookup"><span data-stu-id="5215c-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="5215c-245">Secret\*</span><span class="sxs-lookup"><span data-stu-id="5215c-245">Secret\*</span></span> |<span data-ttu-id="5215c-246">secret</span><span class="sxs-lookup"><span data-stu-id="5215c-246">secret</span></span> |<span data-ttu-id="5215c-247">The secret of the client that is requesting the token</span><span class="sxs-lookup"><span data-stu-id="5215c-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="5215c-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span><span class="sxs-lookup"><span data-stu-id="5215c-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="5215c-249">For example:</span><span class="sxs-lookup"><span data-stu-id="5215c-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="5215c-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="5215c-250">Next steps</span></span>
<span data-ttu-id="5215c-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5215c-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5215c-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5215c-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>




