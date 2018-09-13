---
title: Workflow actions and triggers - Azure Logic Apps | Microsoft Docs
description: ''
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: ''
documentationcenter: ''
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: mandia
ms.openlocfilehash: 4ce452ce4f0c81e619cf028bdde587ba3e1e0b9c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555759"
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="e1ebf-102">Workflow actions and triggers for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e1ebf-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="e1ebf-103">Logic apps consist of triggers and actions.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="e1ebf-104">There are six types of triggers.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-104">There are six types of triggers.</span></span> <span data-ttu-id="e1ebf-105">Each type has different interface and different behavior.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="e1ebf-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="e1ebf-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="e1ebf-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="e1ebf-108">Triggers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-108">Triggers</span></span>  

<span data-ttu-id="e1ebf-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="e1ebf-110">Here are the two different ways to initiate a run of your workflow:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-110">Here are the two different ways to initiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="e1ebf-111">A polling trigger</span><span class="sxs-lookup"><span data-stu-id="e1ebf-111">A polling trigger</span></span>  

-   <span data-ttu-id="e1ebf-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="e1ebf-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="e1ebf-113">All triggers contain these top-level elements:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="e1ebf-114">Trigger types and their inputs</span><span class="sxs-lookup"><span data-stu-id="e1ebf-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="e1ebf-115">You can use these types of triggers:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="e1ebf-116">**Request** \- Makes the logic app an endpoint for you to call</span><span class="sxs-lookup"><span data-stu-id="e1ebf-116">**Request** \- Makes the logic app an endpoint for you to call</span></span>  
  
-   <span data-ttu-id="e1ebf-117">**Recurrence** \- Fires based on a defined schedule</span><span class="sxs-lookup"><span data-stu-id="e1ebf-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="e1ebf-118">**HTTP** \- Polls an HTTP web endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="e1ebf-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span><span class="sxs-lookup"><span data-stu-id="e1ebf-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="e1ebf-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="e1ebf-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="e1ebf-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span><span class="sxs-lookup"><span data-stu-id="e1ebf-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span></span>  
  
-   <span data-ttu-id="e1ebf-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span><span class="sxs-lookup"><span data-stu-id="e1ebf-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span></span>       
    <span data-ttu-id="e1ebf-123">Each trigger type has a different set of **inputs** that defines its behavior.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="e1ebf-124">Request trigger</span><span class="sxs-lookup"><span data-stu-id="e1ebf-124">Request trigger</span></span>  

<span data-ttu-id="e1ebf-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span></span> <span data-ttu-id="e1ebf-126">A request trigger looks like this example:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="e1ebf-127">There is also an optional property called **schema**:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="e1ebf-128">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-128">Element name</span></span>|<span data-ttu-id="e1ebf-129">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-129">Required</span></span>|<span data-ttu-id="e1ebf-130">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="e1ebf-131">schema</span><span class="sxs-lookup"><span data-stu-id="e1ebf-131">schema</span></span>|<span data-ttu-id="e1ebf-132">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-132">No</span></span>|<span data-ttu-id="e1ebf-133">A JSON schema that validates the incoming request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-133">A JSON schema that validates the incoming request.</span></span> <span data-ttu-id="e1ebf-134">Useful for helping subsequent workflow steps know which properties to reference.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-134">Useful for helping subsequent workflow steps know which properties to reference.</span></span>|

<span data-ttu-id="e1ebf-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span></span> <span data-ttu-id="e1ebf-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="e1ebf-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="e1ebf-137">Recurrence trigger</span><span class="sxs-lookup"><span data-stu-id="e1ebf-137">Recurrence trigger</span></span>  

<span data-ttu-id="e1ebf-138">A Recurrence trigger is one that runs based on a defined schedule.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="e1ebf-139">Such a trigger might look like this example:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="e1ebf-140">As you can see, it is a simple way to run a workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-140">As you can see, it is a simple way to run a workflow.</span></span>  
  
|<span data-ttu-id="e1ebf-141">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-141">Element name</span></span>|<span data-ttu-id="e1ebf-142">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-142">Required</span></span>|<span data-ttu-id="e1ebf-143">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="e1ebf-144">frequency</span><span class="sxs-lookup"><span data-stu-id="e1ebf-144">frequency</span></span>|<span data-ttu-id="e1ebf-145">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-145">Yes</span></span>|<span data-ttu-id="e1ebf-146">How often the trigger executes.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-146">How often the trigger executes.</span></span> <span data-ttu-id="e1ebf-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span><span class="sxs-lookup"><span data-stu-id="e1ebf-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="e1ebf-148">interval</span><span class="sxs-lookup"><span data-stu-id="e1ebf-148">interval</span></span>|<span data-ttu-id="e1ebf-149">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-149">Yes</span></span>|<span data-ttu-id="e1ebf-150">Interval of the given frequency for the recurrence</span><span class="sxs-lookup"><span data-stu-id="e1ebf-150">Interval of the given frequency for the recurrence</span></span>|  
|<span data-ttu-id="e1ebf-151">startTime</span><span class="sxs-lookup"><span data-stu-id="e1ebf-151">startTime</span></span>|<span data-ttu-id="e1ebf-152">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-152">No</span></span>|<span data-ttu-id="e1ebf-153">If a startTime is provided without a UTC offset, this timeZone is used.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="e1ebf-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="e1ebf-154">timeZone</span></span>|<span data-ttu-id="e1ebf-155">no</span><span class="sxs-lookup"><span data-stu-id="e1ebf-155">no</span></span>|<span data-ttu-id="e1ebf-156">If a startTime is provided without a UTC offset, this timeZone is used.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="e1ebf-157">You can also schedule a trigger to start executing at some point in the future.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-157">You can also schedule a trigger to start executing at some point in the future.</span></span> <span data-ttu-id="e1ebf-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="e1ebf-159">HTTP trigger</span><span class="sxs-lookup"><span data-stu-id="e1ebf-159">HTTP trigger</span></span>  

<span data-ttu-id="e1ebf-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span></span> <span data-ttu-id="e1ebf-161">The inputs object takes the set of parameters required to construct an HTTP call:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-161">The inputs object takes the set of parameters required to construct an HTTP call:</span></span>  
  
|<span data-ttu-id="e1ebf-162">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-162">Element name</span></span>|<span data-ttu-id="e1ebf-163">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-163">Required</span></span>|<span data-ttu-id="e1ebf-164">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-164">Description</span></span>|<span data-ttu-id="e1ebf-165">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="e1ebf-166">method</span><span class="sxs-lookup"><span data-stu-id="e1ebf-166">method</span></span>|<span data-ttu-id="e1ebf-167">yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-167">yes</span></span>|<span data-ttu-id="e1ebf-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span><span class="sxs-lookup"><span data-stu-id="e1ebf-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="e1ebf-169">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-169">String</span></span>|  
|<span data-ttu-id="e1ebf-170">uri</span><span class="sxs-lookup"><span data-stu-id="e1ebf-170">uri</span></span>|<span data-ttu-id="e1ebf-171">yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-171">yes</span></span>|<span data-ttu-id="e1ebf-172">The http or https endpoint that is called.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-172">The http or https endpoint that is called.</span></span> <span data-ttu-id="e1ebf-173">Maximum of 2 kilobytes.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="e1ebf-174">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-174">String</span></span>|  
|<span data-ttu-id="e1ebf-175">queries</span><span class="sxs-lookup"><span data-stu-id="e1ebf-175">queries</span></span>|<span data-ttu-id="e1ebf-176">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-176">No</span></span>|<span data-ttu-id="e1ebf-177">An object representing the query parameters to add to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-177">An object representing the query parameters to add to the URL.</span></span> <span data-ttu-id="e1ebf-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|<span data-ttu-id="e1ebf-179">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-179">Object</span></span>|  
|<span data-ttu-id="e1ebf-180">headers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-180">headers</span></span>|<span data-ttu-id="e1ebf-181">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-181">No</span></span>|<span data-ttu-id="e1ebf-182">An object representing each of the headers that is sent to the request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-182">An object representing each of the headers that is sent to the request.</span></span> <span data-ttu-id="e1ebf-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="e1ebf-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="e1ebf-184">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-184">Object</span></span>|  
|<span data-ttu-id="e1ebf-185">body</span><span class="sxs-lookup"><span data-stu-id="e1ebf-185">body</span></span>|<span data-ttu-id="e1ebf-186">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-186">No</span></span>|<span data-ttu-id="e1ebf-187">An object representing the payload that is sent to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-187">An object representing the payload that is sent to the endpoint.</span></span>|<span data-ttu-id="e1ebf-188">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-188">Object</span></span>|  
|<span data-ttu-id="e1ebf-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="e1ebf-189">retryPolicy</span></span>|<span data-ttu-id="e1ebf-190">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-190">No</span></span>|<span data-ttu-id="e1ebf-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="e1ebf-192">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-192">Object</span></span>|  
|<span data-ttu-id="e1ebf-193">authentication</span><span class="sxs-lookup"><span data-stu-id="e1ebf-193">authentication</span></span>|<span data-ttu-id="e1ebf-194">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-194">No</span></span>|<span data-ttu-id="e1ebf-195">Represents the method that the request should be authenticated.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-195">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="e1ebf-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="e1ebf-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="e1ebf-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="e1ebf-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="e1ebf-198">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-198">Object</span></span>|  
  
<span data-ttu-id="e1ebf-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span></span> <span data-ttu-id="e1ebf-200">It requires the following fields:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-200">It requires the following fields:</span></span>  
  
|<span data-ttu-id="e1ebf-201">Response</span><span class="sxs-lookup"><span data-stu-id="e1ebf-201">Response</span></span>|<span data-ttu-id="e1ebf-202">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="e1ebf-203">Status code</span><span class="sxs-lookup"><span data-stu-id="e1ebf-203">Status code</span></span>|<span data-ttu-id="e1ebf-204">Status code 200 \(OK\) to cause a run.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-204">Status code 200 \(OK\) to cause a run.</span></span> <span data-ttu-id="e1ebf-205">Any other status code doesn't cause a run.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="e1ebf-206">Retry\-after header</span><span class="sxs-lookup"><span data-stu-id="e1ebf-206">Retry\-after header</span></span>|<span data-ttu-id="e1ebf-207">Number of seconds until the logic app polls the endpoint again.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-207">Number of seconds until the logic app polls the endpoint again.</span></span>|  
|<span data-ttu-id="e1ebf-208">Location header</span><span class="sxs-lookup"><span data-stu-id="e1ebf-208">Location header</span></span>|<span data-ttu-id="e1ebf-209">The URL to call on the next polling interval.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-209">The URL to call on the next polling interval.</span></span> <span data-ttu-id="e1ebf-210">If not specified, the original URL is used.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-210">If not specified, the original URL is used.</span></span>|  
  
<span data-ttu-id="e1ebf-211">Here are some examples of different behaviors for different types of requests:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="e1ebf-212">Response code</span><span class="sxs-lookup"><span data-stu-id="e1ebf-212">Response code</span></span>|<span data-ttu-id="e1ebf-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="e1ebf-213">Retry\-After</span></span>|<span data-ttu-id="e1ebf-214">Behavior</span><span class="sxs-lookup"><span data-stu-id="e1ebf-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="e1ebf-215">200</span><span class="sxs-lookup"><span data-stu-id="e1ebf-215">200</span></span>|<span data-ttu-id="e1ebf-216">\(none\)</span><span class="sxs-lookup"><span data-stu-id="e1ebf-216">\(none\)</span></span>|<span data-ttu-id="e1ebf-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span></span>|  
|<span data-ttu-id="e1ebf-218">202</span><span class="sxs-lookup"><span data-stu-id="e1ebf-218">202</span></span>|<span data-ttu-id="e1ebf-219">60</span><span class="sxs-lookup"><span data-stu-id="e1ebf-219">60</span></span>|<span data-ttu-id="e1ebf-220">Do not trigger the workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-220">Do not trigger the workflow.</span></span> <span data-ttu-id="e1ebf-221">The next attempt happens in one minute.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-221">The next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="e1ebf-222">200</span><span class="sxs-lookup"><span data-stu-id="e1ebf-222">200</span></span>|<span data-ttu-id="e1ebf-223">10</span><span class="sxs-lookup"><span data-stu-id="e1ebf-223">10</span></span>|<span data-ttu-id="e1ebf-224">Run the workflow, and check again for more content in 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-224">Run the workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="e1ebf-225">400</span><span class="sxs-lookup"><span data-stu-id="e1ebf-225">400</span></span>|<span data-ttu-id="e1ebf-226">\(none\)</span><span class="sxs-lookup"><span data-stu-id="e1ebf-226">\(none\)</span></span>|<span data-ttu-id="e1ebf-227">Bad request, do not run the workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-227">Bad request, do not run the workflow.</span></span> <span data-ttu-id="e1ebf-228">If there is no **Retry Policy** defined, then the default policy is used.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-228">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="e1ebf-229">After the number of retries has been reached, the trigger is no longer valid.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-229">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
|<span data-ttu-id="e1ebf-230">500</span><span class="sxs-lookup"><span data-stu-id="e1ebf-230">500</span></span>|<span data-ttu-id="e1ebf-231">\(none\)</span><span class="sxs-lookup"><span data-stu-id="e1ebf-231">\(none\)</span></span>|<span data-ttu-id="e1ebf-232">Server error, do not run the workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-232">Server error, do not run the workflow.</span></span>  <span data-ttu-id="e1ebf-233">If there is no **Retry Policy** defined, then the default policy is used.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-233">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="e1ebf-234">After the number of retries has been reached, the trigger is no longer valid.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-234">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="e1ebf-235">The outputs of an HTTP trigger look like this example:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-235">The outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="e1ebf-236">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-236">Element name</span></span>|<span data-ttu-id="e1ebf-237">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-237">Description</span></span>|<span data-ttu-id="e1ebf-238">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="e1ebf-239">headers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-239">headers</span></span>|<span data-ttu-id="e1ebf-240">The headers of the http response.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-240">The headers of the http response.</span></span>|<span data-ttu-id="e1ebf-241">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-241">Object</span></span>|  
|<span data-ttu-id="e1ebf-242">body</span><span class="sxs-lookup"><span data-stu-id="e1ebf-242">body</span></span>|<span data-ttu-id="e1ebf-243">The body of the http response.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-243">The body of the http response.</span></span>|<span data-ttu-id="e1ebf-244">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="e1ebf-245">API Connection trigger</span><span class="sxs-lookup"><span data-stu-id="e1ebf-245">API Connection trigger</span></span>  

<span data-ttu-id="e1ebf-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="e1ebf-247">However, the parameters for identifying the action are different.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-247">However, the parameters for identifying the action are different.</span></span> <span data-ttu-id="e1ebf-248">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="e1ebf-249">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-249">Element name</span></span>|<span data-ttu-id="e1ebf-250">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-250">Required</span></span>|<span data-ttu-id="e1ebf-251">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-251">Type</span></span>|<span data-ttu-id="e1ebf-252">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-253">host</span><span class="sxs-lookup"><span data-stu-id="e1ebf-253">host</span></span>|<span data-ttu-id="e1ebf-254">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-254">Yes</span></span>||<span data-ttu-id="e1ebf-255">The ApiApp hosted gateway and id.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-255">The ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="e1ebf-256">method</span><span class="sxs-lookup"><span data-stu-id="e1ebf-256">method</span></span>|<span data-ttu-id="e1ebf-257">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-257">Yes</span></span>|<span data-ttu-id="e1ebf-258">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-258">String</span></span>|<span data-ttu-id="e1ebf-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span><span class="sxs-lookup"><span data-stu-id="e1ebf-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="e1ebf-260">queries</span><span class="sxs-lookup"><span data-stu-id="e1ebf-260">queries</span></span>|<span data-ttu-id="e1ebf-261">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-261">No</span></span>|<span data-ttu-id="e1ebf-262">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-262">Object</span></span>|<span data-ttu-id="e1ebf-263">Represents the query parameters to be added to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-263">Represents the query parameters to be added to the URL.</span></span> <span data-ttu-id="e1ebf-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="e1ebf-265">headers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-265">headers</span></span>|<span data-ttu-id="e1ebf-266">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-266">No</span></span>|<span data-ttu-id="e1ebf-267">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-267">Object</span></span>|<span data-ttu-id="e1ebf-268">Represents each of the headers that is sent to the request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-268">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="e1ebf-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="e1ebf-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="e1ebf-270">body</span><span class="sxs-lookup"><span data-stu-id="e1ebf-270">body</span></span>|<span data-ttu-id="e1ebf-271">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-271">No</span></span>|<span data-ttu-id="e1ebf-272">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-272">Object</span></span>|<span data-ttu-id="e1ebf-273">Represents the payload that is sent to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-273">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="e1ebf-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="e1ebf-274">retryPolicy</span></span>|<span data-ttu-id="e1ebf-275">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-275">No</span></span>|<span data-ttu-id="e1ebf-276">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-276">Object</span></span>|<span data-ttu-id="e1ebf-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="e1ebf-278">authentication</span><span class="sxs-lookup"><span data-stu-id="e1ebf-278">authentication</span></span>|<span data-ttu-id="e1ebf-279">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-279">No</span></span>|<span data-ttu-id="e1ebf-280">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-280">Object</span></span>|<span data-ttu-id="e1ebf-281">Represents the method that the request should be authenticated.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-281">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="e1ebf-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span><span class="sxs-lookup"><span data-stu-id="e1ebf-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="e1ebf-283">The properties for host are:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-283">The properties for host are:</span></span>  
  
|<span data-ttu-id="e1ebf-284">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-284">Element name</span></span>|<span data-ttu-id="e1ebf-285">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-285">Required</span></span>|<span data-ttu-id="e1ebf-286">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="e1ebf-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="e1ebf-287">api runtimeUrl</span></span>|<span data-ttu-id="e1ebf-288">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-288">Yes</span></span>|<span data-ttu-id="e1ebf-289">The endpoint of the managed API.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-289">The endpoint of the managed API.</span></span>|  
|<span data-ttu-id="e1ebf-290">connection name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-290">connection name</span></span>||<span data-ttu-id="e1ebf-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span></span>|
  
<span data-ttu-id="e1ebf-292">The outputs of an API connection trigger are:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-292">The outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="e1ebf-293">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-293">Element name</span></span>|<span data-ttu-id="e1ebf-294">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-294">Type</span></span>|<span data-ttu-id="e1ebf-295">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="e1ebf-296">headers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-296">headers</span></span>|<span data-ttu-id="e1ebf-297">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-297">Object</span></span>|<span data-ttu-id="e1ebf-298">The headers of the http response.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-298">The headers of the http response.</span></span>|  
|<span data-ttu-id="e1ebf-299">body</span><span class="sxs-lookup"><span data-stu-id="e1ebf-299">body</span></span>|<span data-ttu-id="e1ebf-300">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-300">Object</span></span>|<span data-ttu-id="e1ebf-301">The body of the http response.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-301">The body of the http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="e1ebf-302">HTTPWebhook trigger</span><span class="sxs-lookup"><span data-stu-id="e1ebf-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="e1ebf-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span></span> <span data-ttu-id="e1ebf-304">Here's an example of what an HTTPWebhook trigger might look like:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="e1ebf-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="e1ebf-306">The properties of a Webhook are as follows:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-306">The properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="e1ebf-307">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-307">Element name</span></span>|<span data-ttu-id="e1ebf-308">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-308">Required</span></span>|<span data-ttu-id="e1ebf-309">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="e1ebf-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="e1ebf-310">subscribe</span></span>|<span data-ttu-id="e1ebf-311">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-311">No</span></span>|<span data-ttu-id="e1ebf-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span></span>|  
|<span data-ttu-id="e1ebf-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="e1ebf-313">unsubscribe</span></span>|<span data-ttu-id="e1ebf-314">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-314">No</span></span>|<span data-ttu-id="e1ebf-315">The outgoing request when the trigger is deleted.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-315">The outgoing request when the trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="e1ebf-316">**Subscribe** is the outgoing call that's made to start listening to events.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-316">**Subscribe** is the outgoing call that's made to start listening to events.</span></span> <span data-ttu-id="e1ebf-317">This call starts with the same set of parameters that the normal HTTP actions do.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-317">This call starts with the same set of parameters that the normal HTTP actions do.</span></span> <span data-ttu-id="e1ebf-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span></span>
  
    <span data-ttu-id="e1ebf-319">To support this call, there is a new function: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-319">To support this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="e1ebf-320">This function returns a unique URL for this specific trigger in this workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="e1ebf-321">It represents the unique identifier for the endpoints that use the Service REST.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-321">It represents the unique identifier for the endpoints that use the Service REST.</span></span>  
  
-   <span data-ttu-id="e1ebf-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="e1ebf-323">Deleting or disabling the trigger</span><span class="sxs-lookup"><span data-stu-id="e1ebf-323">Deleting or disabling the trigger</span></span>  
  
    -   <span data-ttu-id="e1ebf-324">Deleting or disabling the workflow</span><span class="sxs-lookup"><span data-stu-id="e1ebf-324">Deleting or disabling the workflow</span></span>  
  
    -   <span data-ttu-id="e1ebf-325">Deleting or disabling the subscription</span><span class="sxs-lookup"><span data-stu-id="e1ebf-325">Deleting or disabling the subscription</span></span>  
  
    <span data-ttu-id="e1ebf-326">The logic app automatically calls the unsubscribe action.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-326">The logic app automatically calls the unsubscribe action.</span></span> <span data-ttu-id="e1ebf-327">The parameters to this function are the same as the HTTP trigger.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-327">The parameters to this function are the same as the HTTP trigger.</span></span>  
  
    <span data-ttu-id="e1ebf-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span></span>  
  
|<span data-ttu-id="e1ebf-329">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-329">Element name</span></span>|<span data-ttu-id="e1ebf-330">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-330">Type</span></span>|<span data-ttu-id="e1ebf-331">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="e1ebf-332">headers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-332">headers</span></span>|<span data-ttu-id="e1ebf-333">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-333">Object</span></span>|<span data-ttu-id="e1ebf-334">The headers of the http request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-334">The headers of the http request.</span></span>|  
|<span data-ttu-id="e1ebf-335">body</span><span class="sxs-lookup"><span data-stu-id="e1ebf-335">body</span></span>|<span data-ttu-id="e1ebf-336">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-336">Object</span></span>|<span data-ttu-id="e1ebf-337">The body of the http request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-337">The body of the http request.</span></span>|  

<span data-ttu-id="e1ebf-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="e1ebf-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="e1ebf-339">Conditions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-339">Conditions</span></span>  

<span data-ttu-id="e1ebf-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span></span> <span data-ttu-id="e1ebf-341">For example:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="e1ebf-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span></span> <span data-ttu-id="e1ebf-343">Finally, conditions may reference the status code of the trigger.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-343">Finally, conditions may reference the status code of the trigger.</span></span> <span data-ttu-id="e1ebf-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="e1ebf-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="e1ebf-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="e1ebf-347">Start multiple runs for a request</span><span class="sxs-lookup"><span data-stu-id="e1ebf-347">Start multiple runs for a request</span></span>

<span data-ttu-id="e1ebf-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="e1ebf-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span></span> <span data-ttu-id="e1ebf-350">For example, imagine you have an API that returns the following response:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-350">For example, imagine you have an API that returns the following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="e1ebf-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="e1ebf-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span></span> <span data-ttu-id="e1ebf-353">The trigger outputs look like this example:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-353">The trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="e1ebf-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="e1ebf-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="e1ebf-356">Single run instance</span><span class="sxs-lookup"><span data-stu-id="e1ebf-356">Single run instance</span></span>

<span data-ttu-id="e1ebf-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span></span> <span data-ttu-id="e1ebf-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span></span>

<span data-ttu-id="e1ebf-359">You can configure this setting through the operation options:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-359">You can configure this setting through the operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="e1ebf-360">Types and inputs</span><span class="sxs-lookup"><span data-stu-id="e1ebf-360">Types and inputs</span></span>  

<span data-ttu-id="e1ebf-361">There are many types of actions, each with unique behavior.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="e1ebf-362">Collection actions may contain many other actions within itself.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="e1ebf-363">Standard actions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-363">Standard actions</span></span>  

-   <span data-ttu-id="e1ebf-364">**HTTP** This action calls an HTTP web endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="e1ebf-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="e1ebf-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="e1ebf-367">**Response** \- This action defines a response for an incoming call.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="e1ebf-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="e1ebf-369">**Workflow** \- This action represents a nested workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="e1ebf-370">**Function** \- This action represents an Azure Function.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="e1ebf-371">Collection actions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-371">Collection actions</span></span>

-   <span data-ttu-id="e1ebf-372">**Scope** \- This action is a logical grouping of other actions.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="e1ebf-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span></span>

-   <span data-ttu-id="e1ebf-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="e1ebf-375">**Until** \- This looping action executes inner actions until a condition results to true.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-375">**Until** \- This looping action executes inner actions until a condition results to true.</span></span>
  
<span data-ttu-id="e1ebf-376">Each type of action has a different set of **inputs** that define an action's behavior.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="e1ebf-377">HTTP action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-377">HTTP action</span></span>  

<span data-ttu-id="e1ebf-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span></span> <span data-ttu-id="e1ebf-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span></span>  
  
|<span data-ttu-id="e1ebf-380">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-380">Element name</span></span>|<span data-ttu-id="e1ebf-381">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-381">Required</span></span>|<span data-ttu-id="e1ebf-382">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-382">Type</span></span>|<span data-ttu-id="e1ebf-383">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-384">method</span><span class="sxs-lookup"><span data-stu-id="e1ebf-384">method</span></span>|<span data-ttu-id="e1ebf-385">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-385">Yes</span></span>|<span data-ttu-id="e1ebf-386">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-386">String</span></span>|<span data-ttu-id="e1ebf-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span><span class="sxs-lookup"><span data-stu-id="e1ebf-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="e1ebf-388">uri</span><span class="sxs-lookup"><span data-stu-id="e1ebf-388">uri</span></span>|<span data-ttu-id="e1ebf-389">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-389">Yes</span></span>|<span data-ttu-id="e1ebf-390">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-390">String</span></span>|<span data-ttu-id="e1ebf-391">The http or https endpoint that is called.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-391">The http or https endpoint that is called.</span></span> <span data-ttu-id="e1ebf-392">Maximum length is 2 kilobytes.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="e1ebf-393">queries</span><span class="sxs-lookup"><span data-stu-id="e1ebf-393">queries</span></span>|<span data-ttu-id="e1ebf-394">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-394">No</span></span>|<span data-ttu-id="e1ebf-395">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-395">Object</span></span>|<span data-ttu-id="e1ebf-396">Represents the query parameters to add to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-396">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="e1ebf-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="e1ebf-398">headers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-398">headers</span></span>|<span data-ttu-id="e1ebf-399">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-399">No</span></span>|<span data-ttu-id="e1ebf-400">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-400">Object</span></span>|<span data-ttu-id="e1ebf-401">Represents each of the headers that is sent to the request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-401">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="e1ebf-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="e1ebf-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="e1ebf-403">body</span><span class="sxs-lookup"><span data-stu-id="e1ebf-403">body</span></span>|<span data-ttu-id="e1ebf-404">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-404">No</span></span>|<span data-ttu-id="e1ebf-405">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-405">Object</span></span>|<span data-ttu-id="e1ebf-406">Represents the payload that is sent to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-406">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="e1ebf-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="e1ebf-407">retryPolicy</span></span>|<span data-ttu-id="e1ebf-408">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-408">No</span></span>|<span data-ttu-id="e1ebf-409">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-409">Object</span></span>|<span data-ttu-id="e1ebf-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="e1ebf-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-411">operationsOptions</span></span>|<span data-ttu-id="e1ebf-412">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-412">No</span></span>|<span data-ttu-id="e1ebf-413">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-413">String</span></span>|<span data-ttu-id="e1ebf-414">Defines the set of special behaviors to override.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-414">Defines the set of special behaviors to override.</span></span>|  
|<span data-ttu-id="e1ebf-415">authentication</span><span class="sxs-lookup"><span data-stu-id="e1ebf-415">authentication</span></span>|<span data-ttu-id="e1ebf-416">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-416">No</span></span>|<span data-ttu-id="e1ebf-417">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-417">Object</span></span>|<span data-ttu-id="e1ebf-418">Represents the method that the request should be authenticated.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-418">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="e1ebf-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="e1ebf-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="e1ebf-420">Beyond scheduler, there is one more supported property: `authority`.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="e1ebf-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="e1ebf-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="e1ebf-422">HTTP actions \(and API Connection\) actions support retry policies.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="e1ebf-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span></span> <span data-ttu-id="e1ebf-424">This policy is described using the *retryPolicy* object defined as shown here:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-424">This policy is described using the *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="e1ebf-425">The retry interval is specified in the ISO 8601 format.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-425">The retry interval is specified in the ISO 8601 format.</span></span> <span data-ttu-id="e1ebf-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span></span> <span data-ttu-id="e1ebf-427">The default and maximum retry count is four hours.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-427">The default and maximum retry count is four hours.</span></span> <span data-ttu-id="e1ebf-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="e1ebf-429">To disable the retry policy, set its type to `None`.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-429">To disable the retry policy, set its type to `None`.</span></span>  
  
<span data-ttu-id="e1ebf-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="e1ebf-431">Asynchronous patterns</span><span class="sxs-lookup"><span data-stu-id="e1ebf-431">Asynchronous patterns</span></span>

<span data-ttu-id="e1ebf-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="e1ebf-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span><span class="sxs-lookup"><span data-stu-id="e1ebf-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="e1ebf-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span></span> <span data-ttu-id="e1ebf-435">In this case, the output of the action is based on the initial 202 response from the server.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-435">In this case, the output of the action is based on the initial 202 response from the server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="e1ebf-436">Asynchronous Limits</span><span class="sxs-lookup"><span data-stu-id="e1ebf-436">Asynchronous Limits</span></span>

<span data-ttu-id="e1ebf-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span></span>  <span data-ttu-id="e1ebf-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="e1ebf-439">The limit timeout is specified in ISO 8601 format.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-439">The limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="e1ebf-440">Limits can be specified with the following syntax:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-440">Limits can be specified with the following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="e1ebf-441">API Connection</span><span class="sxs-lookup"><span data-stu-id="e1ebf-441">API Connection</span></span>  

<span data-ttu-id="e1ebf-442">API Connection is an action that references a Microsoft-managed connector.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="e1ebf-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span></span>

|<span data-ttu-id="e1ebf-444">Element name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-444">Element name</span></span>|<span data-ttu-id="e1ebf-445">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-445">Required</span></span>|<span data-ttu-id="e1ebf-446">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-446">Type</span></span>|<span data-ttu-id="e1ebf-447">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-448">host</span><span class="sxs-lookup"><span data-stu-id="e1ebf-448">host</span></span>|<span data-ttu-id="e1ebf-449">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-449">Yes</span></span>|<span data-ttu-id="e1ebf-450">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-450">Object</span></span>|<span data-ttu-id="e1ebf-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span></span>|
|<span data-ttu-id="e1ebf-452">method</span><span class="sxs-lookup"><span data-stu-id="e1ebf-452">method</span></span>|<span data-ttu-id="e1ebf-453">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-453">Yes</span></span>|<span data-ttu-id="e1ebf-454">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-454">String</span></span>|<span data-ttu-id="e1ebf-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span><span class="sxs-lookup"><span data-stu-id="e1ebf-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="e1ebf-456">path</span><span class="sxs-lookup"><span data-stu-id="e1ebf-456">path</span></span>|<span data-ttu-id="e1ebf-457">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-457">Yes</span></span>|<span data-ttu-id="e1ebf-458">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-458">String</span></span>|<span data-ttu-id="e1ebf-459">The path of the API operation.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-459">The path of the API operation.</span></span>|  
|<span data-ttu-id="e1ebf-460">queries</span><span class="sxs-lookup"><span data-stu-id="e1ebf-460">queries</span></span>|<span data-ttu-id="e1ebf-461">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-461">No</span></span>|<span data-ttu-id="e1ebf-462">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-462">Object</span></span>|<span data-ttu-id="e1ebf-463">Represents the query parameters to add to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-463">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="e1ebf-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="e1ebf-465">headers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-465">headers</span></span>|<span data-ttu-id="e1ebf-466">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-466">No</span></span>|<span data-ttu-id="e1ebf-467">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-467">Object</span></span>|<span data-ttu-id="e1ebf-468">Represents each of the headers that is sent to the request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-468">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="e1ebf-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="e1ebf-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="e1ebf-470">body</span><span class="sxs-lookup"><span data-stu-id="e1ebf-470">body</span></span>|<span data-ttu-id="e1ebf-471">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-471">No</span></span>|<span data-ttu-id="e1ebf-472">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-472">Object</span></span>|<span data-ttu-id="e1ebf-473">Represents the payload that is sent to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-473">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="e1ebf-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="e1ebf-474">retryPolicy</span></span>|<span data-ttu-id="e1ebf-475">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-475">No</span></span>|<span data-ttu-id="e1ebf-476">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-476">Object</span></span>|<span data-ttu-id="e1ebf-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="e1ebf-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-478">operationsOptions</span></span>|<span data-ttu-id="e1ebf-479">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-479">No</span></span>|<span data-ttu-id="e1ebf-480">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-480">String</span></span>|<span data-ttu-id="e1ebf-481">Defines the set of special behaviors to override.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-481">Defines the set of special behaviors to override.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="e1ebf-482">API Connection webhook action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="e1ebf-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="e1ebf-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="e1ebf-484">Response action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-484">Response action</span></span>  

<span data-ttu-id="e1ebf-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="e1ebf-486">The response action has special restrictions that don't apply to other actions.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-486">The response action has special restrictions that don't apply to other actions.</span></span> <span data-ttu-id="e1ebf-487">Specifically:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-487">Specifically:</span></span>  
  
-   <span data-ttu-id="e1ebf-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span></span>  
  
-   <span data-ttu-id="e1ebf-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span></span>  
  
-   <span data-ttu-id="e1ebf-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="e1ebf-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="e1ebf-492">Wait action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-492">Wait action</span></span>  

<span data-ttu-id="e1ebf-493">The `wait` action suspends workflow execution for the specified interval.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-493">The `wait` action suspends workflow execution for the specified interval.</span></span> <span data-ttu-id="e1ebf-494">For example, to wait 15 minutes, you can use this snippet:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-494">For example, to wait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="e1ebf-495">Alternatively, to wait until a specific moment in time, you can use this example:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-495">Alternatively, to wait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="e1ebf-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span></span>  
  
|<span data-ttu-id="e1ebf-497">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-497">Name</span></span>|<span data-ttu-id="e1ebf-498">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-498">Required</span></span>|<span data-ttu-id="e1ebf-499">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-499">Type</span></span>|<span data-ttu-id="e1ebf-500">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-501">interval</span><span class="sxs-lookup"><span data-stu-id="e1ebf-501">interval</span></span>|<span data-ttu-id="e1ebf-502">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-502">No</span></span>|<span data-ttu-id="e1ebf-503">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-503">Object</span></span>|<span data-ttu-id="e1ebf-504">The wait duration based on amount of time.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-504">The wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="e1ebf-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="e1ebf-505">interval unit</span></span>|<span data-ttu-id="e1ebf-506">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-506">Yes</span></span>|<span data-ttu-id="e1ebf-507">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-507">String</span></span>|<span data-ttu-id="e1ebf-508">One of these intervals: second, minute, hour, day, week, month, year.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="e1ebf-509">interval count</span><span class="sxs-lookup"><span data-stu-id="e1ebf-509">interval count</span></span>|<span data-ttu-id="e1ebf-510">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-510">Yes</span></span>|<span data-ttu-id="e1ebf-511">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-511">String</span></span>|<span data-ttu-id="e1ebf-512">Duration based on the given internal unit.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-512">Duration based on the given internal unit.</span></span>|  
|<span data-ttu-id="e1ebf-513">until</span><span class="sxs-lookup"><span data-stu-id="e1ebf-513">until</span></span>|<span data-ttu-id="e1ebf-514">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-514">No</span></span>|<span data-ttu-id="e1ebf-515">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-515">Object</span></span>|<span data-ttu-id="e1ebf-516">The wait duration based on a point in time.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-516">The wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="e1ebf-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="e1ebf-517">until timestamp</span></span>|<span data-ttu-id="e1ebf-518">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-518">Yes</span></span>|<span data-ttu-id="e1ebf-519">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-519">String</span></span>|<span data-ttu-id="e1ebf-520">String&#124;The point in time in UTC when the wait expires.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-520">String&#124;The point in time in UTC when the wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="e1ebf-521">Query action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-521">Query action</span></span>

<span data-ttu-id="e1ebf-522">The `query` action lets you filter an array based on a condition.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-522">The `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="e1ebf-523">For example, to select numbers greater than 2, you can use:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-523">For example, to select numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="e1ebf-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ebf-525">If no values satisfy the `where` condition, the result is an empty array.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-525">If no values satisfy the `where` condition, the result is an empty array.</span></span>

|<span data-ttu-id="e1ebf-526">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-526">Name</span></span>|<span data-ttu-id="e1ebf-527">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-527">Required</span></span>|<span data-ttu-id="e1ebf-528">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-528">Type</span></span>|<span data-ttu-id="e1ebf-529">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="e1ebf-530">from</span><span class="sxs-lookup"><span data-stu-id="e1ebf-530">from</span></span>|<span data-ttu-id="e1ebf-531">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-531">Yes</span></span>|<span data-ttu-id="e1ebf-532">Array</span><span class="sxs-lookup"><span data-stu-id="e1ebf-532">Array</span></span>|<span data-ttu-id="e1ebf-533">The source array.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-533">The source array.</span></span>|
|<span data-ttu-id="e1ebf-534">where</span><span class="sxs-lookup"><span data-stu-id="e1ebf-534">where</span></span>|<span data-ttu-id="e1ebf-535">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-535">Yes</span></span>|<span data-ttu-id="e1ebf-536">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-536">String</span></span>|<span data-ttu-id="e1ebf-537">The condition to apply to each element of the source array.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-537">The condition to apply to each element of the source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="e1ebf-538">Select action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-538">Select action</span></span>

<span data-ttu-id="e1ebf-539">The `select` action lets you project each element of an array into a new value.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-539">The `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="e1ebf-540">For example, to convert an array of numbers into an array of objects, you can use:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-540">For example, to convert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="e1ebf-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span></span> <span data-ttu-id="e1ebf-542">If the input is an empty array, the output is also an empty array.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-542">If the input is an empty array, the output is also an empty array.</span></span>

|<span data-ttu-id="e1ebf-543">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-543">Name</span></span>|<span data-ttu-id="e1ebf-544">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-544">Required</span></span>|<span data-ttu-id="e1ebf-545">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-545">Type</span></span>|<span data-ttu-id="e1ebf-546">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="e1ebf-547">from</span><span class="sxs-lookup"><span data-stu-id="e1ebf-547">from</span></span>|<span data-ttu-id="e1ebf-548">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-548">Yes</span></span>|<span data-ttu-id="e1ebf-549">Array</span><span class="sxs-lookup"><span data-stu-id="e1ebf-549">Array</span></span>|<span data-ttu-id="e1ebf-550">The source array.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-550">The source array.</span></span>|
|<span data-ttu-id="e1ebf-551">select</span><span class="sxs-lookup"><span data-stu-id="e1ebf-551">select</span></span>|<span data-ttu-id="e1ebf-552">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-552">Yes</span></span>|<span data-ttu-id="e1ebf-553">Any</span><span class="sxs-lookup"><span data-stu-id="e1ebf-553">Any</span></span>|<span data-ttu-id="e1ebf-554">The projection to apply to each element of the source array.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-554">The projection to apply to each element of the source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="e1ebf-555">Terminate action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-555">Terminate action</span></span>

<span data-ttu-id="e1ebf-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="e1ebf-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="e1ebf-558">Actions already completed are not affected by the terminate action.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-558">Actions already completed are not affected by the terminate action.</span></span>

|<span data-ttu-id="e1ebf-559">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-559">Name</span></span>|<span data-ttu-id="e1ebf-560">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-560">Required</span></span>|<span data-ttu-id="e1ebf-561">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-561">Type</span></span>|<span data-ttu-id="e1ebf-562">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="e1ebf-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="e1ebf-563">runStatus</span></span>|<span data-ttu-id="e1ebf-564">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-564">Yes</span></span>|<span data-ttu-id="e1ebf-565">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-565">String</span></span>|<span data-ttu-id="e1ebf-566">The target run status.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-566">The target run status.</span></span> <span data-ttu-id="e1ebf-567">Either **Failed** or **Cancelled**.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="e1ebf-568">runError</span><span class="sxs-lookup"><span data-stu-id="e1ebf-568">runError</span></span>|<span data-ttu-id="e1ebf-569">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-569">No</span></span>|<span data-ttu-id="e1ebf-570">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-570">Object</span></span>|<span data-ttu-id="e1ebf-571">The error details.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-571">The error details.</span></span> <span data-ttu-id="e1ebf-572">Only supported when **runStatus** is set to **Failed**.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-572">Only supported when **runStatus** is set to **Failed**.</span></span>|
|<span data-ttu-id="e1ebf-573">runError code</span><span class="sxs-lookup"><span data-stu-id="e1ebf-573">runError code</span></span>|<span data-ttu-id="e1ebf-574">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-574">No</span></span>|<span data-ttu-id="e1ebf-575">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-575">String</span></span>|<span data-ttu-id="e1ebf-576">The run error code.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-576">The run error code.</span></span>|
|<span data-ttu-id="e1ebf-577">runError message</span><span class="sxs-lookup"><span data-stu-id="e1ebf-577">runError message</span></span>|<span data-ttu-id="e1ebf-578">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-578">No</span></span>|<span data-ttu-id="e1ebf-579">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-579">String</span></span>|<span data-ttu-id="e1ebf-580">The run error message.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-580">The run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="e1ebf-581">Compose action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-581">Compose action</span></span>

<span data-ttu-id="e1ebf-582">The Compose action lets you construct an arbitrary object.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-582">The Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="e1ebf-583">The output of the compose action is the result of evaluating its inputs.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-583">The output of the compose action is the result of evaluating its inputs.</span></span> <span data-ttu-id="e1ebf-584">For example, you can use the compose action to merge outputs of multiple actions:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-584">For example, you can use the compose action to merge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="e1ebf-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="e1ebf-586">Table action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-586">Table action</span></span>

<span data-ttu-id="e1ebf-587">The `table` allows you to convert an array of items into a **CVS** or **HTML** table.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-587">The `table` allows you to convert an array of items into a **CVS** or **HTML** table.</span></span>

<span data-ttu-id="e1ebf-588">Suppose @triggerBody() is</span><span class="sxs-lookup"><span data-stu-id="e1ebf-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="e1ebf-589">And let the action be defined as</span><span class="sxs-lookup"><span data-stu-id="e1ebf-589">And let the action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="e1ebf-590">The above would produce</span><span class="sxs-lookup"><span data-stu-id="e1ebf-590">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="e1ebf-591">id</span><span class="sxs-lookup"><span data-stu-id="e1ebf-591">id</span></span></th><th><span data-ttu-id="e1ebf-592">name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="e1ebf-593">0</span><span class="sxs-lookup"><span data-stu-id="e1ebf-593">0</span></span></td><td><span data-ttu-id="e1ebf-594">apples</span><span class="sxs-lookup"><span data-stu-id="e1ebf-594">apples</span></span></td></tr><tr><td><span data-ttu-id="e1ebf-595">1</span><span class="sxs-lookup"><span data-stu-id="e1ebf-595">1</span></span></td><td><span data-ttu-id="e1ebf-596">oranges</span><span class="sxs-lookup"><span data-stu-id="e1ebf-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="e1ebf-597">"</span><span class="sxs-lookup"><span data-stu-id="e1ebf-597">"</span></span>

<span data-ttu-id="e1ebf-598">In order to cusomize the table, you can specify the columns explicitly.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-598">In order to cusomize the table, you can specify the columns explicitly.</span></span> <span data-ttu-id="e1ebf-599">For example:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="e1ebf-600">The above would produce</span><span class="sxs-lookup"><span data-stu-id="e1ebf-600">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="e1ebf-601">produce id</span><span class="sxs-lookup"><span data-stu-id="e1ebf-601">produce id</span></span></th><th><span data-ttu-id="e1ebf-602">description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="e1ebf-603">0</span><span class="sxs-lookup"><span data-stu-id="e1ebf-603">0</span></span></td><td><span data-ttu-id="e1ebf-604">fresh apples</span><span class="sxs-lookup"><span data-stu-id="e1ebf-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="e1ebf-605">1</span><span class="sxs-lookup"><span data-stu-id="e1ebf-605">1</span></span></td><td><span data-ttu-id="e1ebf-606">fresh oranges</span><span class="sxs-lookup"><span data-stu-id="e1ebf-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="e1ebf-607">"</span><span class="sxs-lookup"><span data-stu-id="e1ebf-607">"</span></span>

<span data-ttu-id="e1ebf-608">If the `from` property value is an empty array, the output is an empty table.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-608">If the `from` property value is an empty array, the output is an empty table.</span></span>

|<span data-ttu-id="e1ebf-609">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-609">Name</span></span>|<span data-ttu-id="e1ebf-610">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-610">Required</span></span>|<span data-ttu-id="e1ebf-611">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-611">Type</span></span>|<span data-ttu-id="e1ebf-612">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="e1ebf-613">from</span><span class="sxs-lookup"><span data-stu-id="e1ebf-613">from</span></span>|<span data-ttu-id="e1ebf-614">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-614">Yes</span></span>|<span data-ttu-id="e1ebf-615">Array</span><span class="sxs-lookup"><span data-stu-id="e1ebf-615">Array</span></span>|<span data-ttu-id="e1ebf-616">The source array.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-616">The source array.</span></span>|
|<span data-ttu-id="e1ebf-617">format</span><span class="sxs-lookup"><span data-stu-id="e1ebf-617">format</span></span>|<span data-ttu-id="e1ebf-618">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-618">Yes</span></span>|<span data-ttu-id="e1ebf-619">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-619">String</span></span>|<span data-ttu-id="e1ebf-620">The format, either **CVS** or **HTML**.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-620">The format, either **CVS** or **HTML**.</span></span>|
|<span data-ttu-id="e1ebf-621">columns</span><span class="sxs-lookup"><span data-stu-id="e1ebf-621">columns</span></span>|<span data-ttu-id="e1ebf-622">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-622">No</span></span>|<span data-ttu-id="e1ebf-623">Array</span><span class="sxs-lookup"><span data-stu-id="e1ebf-623">Array</span></span>|<span data-ttu-id="e1ebf-624">The columns.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-624">The columns.</span></span> <span data-ttu-id="e1ebf-625">Allows to override the default shape of the table.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-625">Allows to override the default shape of the table.</span></span>|
|<span data-ttu-id="e1ebf-626">column header</span><span class="sxs-lookup"><span data-stu-id="e1ebf-626">column header</span></span>|<span data-ttu-id="e1ebf-627">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-627">No</span></span>|<span data-ttu-id="e1ebf-628">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-628">String</span></span>|<span data-ttu-id="e1ebf-629">The header of the column.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-629">The header of the column.</span></span>|
|<span data-ttu-id="e1ebf-630">column value</span><span class="sxs-lookup"><span data-stu-id="e1ebf-630">column value</span></span>|<span data-ttu-id="e1ebf-631">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-631">Yes</span></span>|<span data-ttu-id="e1ebf-632">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-632">String</span></span>|<span data-ttu-id="e1ebf-633">The value of the column.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-633">The value of the column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="e1ebf-634">Workflow action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-634">Workflow action</span></span>   

|<span data-ttu-id="e1ebf-635">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-635">Name</span></span>|<span data-ttu-id="e1ebf-636">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-636">Required</span></span>|<span data-ttu-id="e1ebf-637">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-637">Type</span></span>|<span data-ttu-id="e1ebf-638">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-639">host id</span><span class="sxs-lookup"><span data-stu-id="e1ebf-639">host id</span></span>|<span data-ttu-id="e1ebf-640">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-640">Yes</span></span>|<span data-ttu-id="e1ebf-641">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-641">String</span></span>|<span data-ttu-id="e1ebf-642">The resource ID of the workflow that you want to call.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-642">The resource ID of the workflow that you want to call.</span></span>|  
|<span data-ttu-id="e1ebf-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="e1ebf-643">host triggerName</span></span>|<span data-ttu-id="e1ebf-644">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-644">Yes</span></span>|<span data-ttu-id="e1ebf-645">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-645">String</span></span>|<span data-ttu-id="e1ebf-646">The name of the trigger that you want to invoke.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-646">The name of the trigger that you want to invoke.</span></span>|  
|<span data-ttu-id="e1ebf-647">queries</span><span class="sxs-lookup"><span data-stu-id="e1ebf-647">queries</span></span>|<span data-ttu-id="e1ebf-648">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-648">No</span></span>|<span data-ttu-id="e1ebf-649">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-649">Object</span></span>|<span data-ttu-id="e1ebf-650">Represents the query parameters to add to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-650">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="e1ebf-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="e1ebf-652">headers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-652">headers</span></span>|<span data-ttu-id="e1ebf-653">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-653">No</span></span>|<span data-ttu-id="e1ebf-654">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-654">Object</span></span>|<span data-ttu-id="e1ebf-655">Represents each of the headers that is sent to the request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-655">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="e1ebf-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="e1ebf-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="e1ebf-657">body</span><span class="sxs-lookup"><span data-stu-id="e1ebf-657">body</span></span>|<span data-ttu-id="e1ebf-658">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-658">No</span></span>|<span data-ttu-id="e1ebf-659">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-659">Object</span></span>|<span data-ttu-id="e1ebf-660">Represents the payload sent to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-660">Represents the payload sent to the endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="e1ebf-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span></span>  
  
<span data-ttu-id="e1ebf-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span></span> <span data-ttu-id="e1ebf-663">If you have not defined any `response` action, then the outputs are empty.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-663">If you have not defined any `response` action, then the outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="e1ebf-664">Function action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-664">Function action</span></span>   

|<span data-ttu-id="e1ebf-665">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-665">Name</span></span>|<span data-ttu-id="e1ebf-666">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-666">Required</span></span>|<span data-ttu-id="e1ebf-667">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-667">Type</span></span>|<span data-ttu-id="e1ebf-668">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-669">function id</span><span class="sxs-lookup"><span data-stu-id="e1ebf-669">function id</span></span>|<span data-ttu-id="e1ebf-670">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-670">Yes</span></span>|<span data-ttu-id="e1ebf-671">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-671">String</span></span>|<span data-ttu-id="e1ebf-672">The resource ID of the function that you want to invoke.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-672">The resource ID of the function that you want to invoke.</span></span>|  
|<span data-ttu-id="e1ebf-673">method</span><span class="sxs-lookup"><span data-stu-id="e1ebf-673">method</span></span>|<span data-ttu-id="e1ebf-674">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-674">No</span></span>|<span data-ttu-id="e1ebf-675">String</span><span class="sxs-lookup"><span data-stu-id="e1ebf-675">String</span></span>|<span data-ttu-id="e1ebf-676">The HTTP method used to invoke the function.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-676">The HTTP method used to invoke the function.</span></span> <span data-ttu-id="e1ebf-677">By default, it is `POST` when not specified.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="e1ebf-678">queries</span><span class="sxs-lookup"><span data-stu-id="e1ebf-678">queries</span></span>|<span data-ttu-id="e1ebf-679">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-679">No</span></span>|<span data-ttu-id="e1ebf-680">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-680">Object</span></span>|<span data-ttu-id="e1ebf-681">Represents the query parameters to add to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-681">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="e1ebf-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="e1ebf-683">headers</span><span class="sxs-lookup"><span data-stu-id="e1ebf-683">headers</span></span>|<span data-ttu-id="e1ebf-684">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-684">No</span></span>|<span data-ttu-id="e1ebf-685">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-685">Object</span></span>|<span data-ttu-id="e1ebf-686">Represents each of the headers that is sent to the request.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-686">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="e1ebf-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="e1ebf-688">body</span><span class="sxs-lookup"><span data-stu-id="e1ebf-688">body</span></span>|<span data-ttu-id="e1ebf-689">No</span><span class="sxs-lookup"><span data-stu-id="e1ebf-689">No</span></span>|<span data-ttu-id="e1ebf-690">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-690">Object</span></span>|<span data-ttu-id="e1ebf-691">Represents the payload sent to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-691">Represents the payload sent to the endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="e1ebf-692">When you save the logic app, we perform some checks on the referenced function:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-692">When you save the logic app, we perform some checks on the referenced function:</span></span>
-   <span data-ttu-id="e1ebf-693">You need to have access to the function.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-693">You need to have access to the function.</span></span>
-   <span data-ttu-id="e1ebf-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="e1ebf-695">It should not have any route defined.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="e1ebf-696">Only "function" and "anonymous" authorization level is allowed.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="e1ebf-697">The trigger URL is retrieved, cached, and used at runtime.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-697">The trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="e1ebf-698">So if any operation invalidates the cached URL, the action fails at runtime.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-698">So if any operation invalidates the cached URL, the action fails at runtime.</span></span> <span data-ttu-id="e1ebf-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="e1ebf-700">Collection actions (scopes and loops)</span><span class="sxs-lookup"><span data-stu-id="e1ebf-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="e1ebf-701">Some action types can contain actions within themselves.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="e1ebf-702">Reference actions within a collection can be referenced directly outside of the collection.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-702">Reference actions within a collection can be referenced directly outside of the collection.</span></span> <span data-ttu-id="e1ebf-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="e1ebf-704">Actions within a collection can `runAfter` only other actions within the same collection.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-704">Actions within a collection can `runAfter` only other actions within the same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="e1ebf-705">Scope action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-705">Scope action</span></span>

<span data-ttu-id="e1ebf-706">The `scope` action lets you logically group actions in a workflow.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-706">The `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="e1ebf-707">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-707">Name</span></span>|<span data-ttu-id="e1ebf-708">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-708">Required</span></span>|<span data-ttu-id="e1ebf-709">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-709">Type</span></span>|<span data-ttu-id="e1ebf-710">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-711">actions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-711">actions</span></span>|<span data-ttu-id="e1ebf-712">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-712">Yes</span></span>|<span data-ttu-id="e1ebf-713">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-713">Object</span></span>|<span data-ttu-id="e1ebf-714">Inner actions to execute within the scope</span><span class="sxs-lookup"><span data-stu-id="e1ebf-714">Inner actions to execute within the scope</span></span>|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a><span data-ttu-id="e1ebf-715">ForEach action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-715">ForEach action</span></span>

<span data-ttu-id="e1ebf-716">This looping action iterates through an array and performs inner actions for each item.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="e1ebf-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span><span class="sxs-lookup"><span data-stu-id="e1ebf-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="e1ebf-718">You can set execution rules using the `operationOptions` parameter.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-718">You can set execution rules using the `operationOptions` parameter.</span></span>

|<span data-ttu-id="e1ebf-719">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-719">Name</span></span>|<span data-ttu-id="e1ebf-720">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-720">Required</span></span>|<span data-ttu-id="e1ebf-721">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-721">Type</span></span>|<span data-ttu-id="e1ebf-722">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-723">actions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-723">actions</span></span>|<span data-ttu-id="e1ebf-724">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-724">Yes</span></span>|<span data-ttu-id="e1ebf-725">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-725">Object</span></span>|<span data-ttu-id="e1ebf-726">Inner actions to execute within the loop</span><span class="sxs-lookup"><span data-stu-id="e1ebf-726">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="e1ebf-727">foreach</span><span class="sxs-lookup"><span data-stu-id="e1ebf-727">foreach</span></span>|<span data-ttu-id="e1ebf-728">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-728">Yes</span></span>|<span data-ttu-id="e1ebf-729">string</span><span class="sxs-lookup"><span data-stu-id="e1ebf-729">string</span></span>|<span data-ttu-id="e1ebf-730">The array to iterate over</span><span class="sxs-lookup"><span data-stu-id="e1ebf-730">The array to iterate over</span></span>|
|<span data-ttu-id="e1ebf-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-731">operationOptions</span></span>|<span data-ttu-id="e1ebf-732">no</span><span class="sxs-lookup"><span data-stu-id="e1ebf-732">no</span></span>|<span data-ttu-id="e1ebf-733">string</span><span class="sxs-lookup"><span data-stu-id="e1ebf-733">string</span></span>|<span data-ttu-id="e1ebf-734">Any operation options for behavior.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-734">Any operation options for behavior.</span></span> <span data-ttu-id="e1ebf-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span><span class="sxs-lookup"><span data-stu-id="e1ebf-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span></span>|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="e1ebf-736">Until action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-736">Until action</span></span>

<span data-ttu-id="e1ebf-737">This looping action executes inner actions until a condition results to true.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-737">This looping action executes inner actions until a condition results to true.</span></span>

|<span data-ttu-id="e1ebf-738">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-738">Name</span></span>|<span data-ttu-id="e1ebf-739">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-739">Required</span></span>|<span data-ttu-id="e1ebf-740">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-740">Type</span></span>|<span data-ttu-id="e1ebf-741">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-742">actions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-742">actions</span></span>|<span data-ttu-id="e1ebf-743">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-743">Yes</span></span>|<span data-ttu-id="e1ebf-744">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-744">Object</span></span>|<span data-ttu-id="e1ebf-745">Inner actions to execute within the loop</span><span class="sxs-lookup"><span data-stu-id="e1ebf-745">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="e1ebf-746">expression</span><span class="sxs-lookup"><span data-stu-id="e1ebf-746">expression</span></span>|<span data-ttu-id="e1ebf-747">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-747">Yes</span></span>|<span data-ttu-id="e1ebf-748">string</span><span class="sxs-lookup"><span data-stu-id="e1ebf-748">string</span></span>|<span data-ttu-id="e1ebf-749">The expression to evaluate after each iteration</span><span class="sxs-lookup"><span data-stu-id="e1ebf-749">The expression to evaluate after each iteration</span></span>|
|<span data-ttu-id="e1ebf-750">limit</span><span class="sxs-lookup"><span data-stu-id="e1ebf-750">limit</span></span>|<span data-ttu-id="e1ebf-751">yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-751">yes</span></span>|<span data-ttu-id="e1ebf-752">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-752">Object</span></span>|<span data-ttu-id="e1ebf-753">The limits for the loop - at least one limit must be defined</span><span class="sxs-lookup"><span data-stu-id="e1ebf-753">The limits for the loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="e1ebf-754">count</span><span class="sxs-lookup"><span data-stu-id="e1ebf-754">count</span></span>|<span data-ttu-id="e1ebf-755">no</span><span class="sxs-lookup"><span data-stu-id="e1ebf-755">no</span></span>|<span data-ttu-id="e1ebf-756">int</span><span class="sxs-lookup"><span data-stu-id="e1ebf-756">int</span></span>|<span data-ttu-id="e1ebf-757">The limit to the number of iterations that can be performed</span><span class="sxs-lookup"><span data-stu-id="e1ebf-757">The limit to the number of iterations that can be performed</span></span>|
|<span data-ttu-id="e1ebf-758">timeout</span><span class="sxs-lookup"><span data-stu-id="e1ebf-758">timeout</span></span>|<span data-ttu-id="e1ebf-759">no</span><span class="sxs-lookup"><span data-stu-id="e1ebf-759">no</span></span>|<span data-ttu-id="e1ebf-760">string</span><span class="sxs-lookup"><span data-stu-id="e1ebf-760">string</span></span>|<span data-ttu-id="e1ebf-761">The timeout for how long it should loop.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-761">The timeout for how long it should loop.</span></span>  <span data-ttu-id="e1ebf-762">ISO 8601 format</span><span class="sxs-lookup"><span data-stu-id="e1ebf-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="e1ebf-763">Conditions - If Action</span><span class="sxs-lookup"><span data-stu-id="e1ebf-763">Conditions - If Action</span></span>

<span data-ttu-id="e1ebf-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span></span>

|<span data-ttu-id="e1ebf-765">Name</span><span class="sxs-lookup"><span data-stu-id="e1ebf-765">Name</span></span>|<span data-ttu-id="e1ebf-766">Required</span><span class="sxs-lookup"><span data-stu-id="e1ebf-766">Required</span></span>|<span data-ttu-id="e1ebf-767">Type</span><span class="sxs-lookup"><span data-stu-id="e1ebf-767">Type</span></span>|<span data-ttu-id="e1ebf-768">Description</span><span class="sxs-lookup"><span data-stu-id="e1ebf-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="e1ebf-769">actions</span><span class="sxs-lookup"><span data-stu-id="e1ebf-769">actions</span></span>|<span data-ttu-id="e1ebf-770">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-770">Yes</span></span>|<span data-ttu-id="e1ebf-771">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-771">Object</span></span>|<span data-ttu-id="e1ebf-772">Inner actions to execute when expression evaluates to `true`</span><span class="sxs-lookup"><span data-stu-id="e1ebf-772">Inner actions to execute when expression evaluates to `true`</span></span>|
|<span data-ttu-id="e1ebf-773">expression</span><span class="sxs-lookup"><span data-stu-id="e1ebf-773">expression</span></span>|<span data-ttu-id="e1ebf-774">Yes</span><span class="sxs-lookup"><span data-stu-id="e1ebf-774">Yes</span></span>|<span data-ttu-id="e1ebf-775">string</span><span class="sxs-lookup"><span data-stu-id="e1ebf-775">string</span></span>|<span data-ttu-id="e1ebf-776">The expression to evaluate</span><span class="sxs-lookup"><span data-stu-id="e1ebf-776">The expression to evaluate</span></span>|
|<span data-ttu-id="e1ebf-777">else</span><span class="sxs-lookup"><span data-stu-id="e1ebf-777">else</span></span>|<span data-ttu-id="e1ebf-778">no</span><span class="sxs-lookup"><span data-stu-id="e1ebf-778">no</span></span>|<span data-ttu-id="e1ebf-779">Object</span><span class="sxs-lookup"><span data-stu-id="e1ebf-779">Object</span></span>|<span data-ttu-id="e1ebf-780">Inner actions to execute when expression evaluates to `false`</span><span class="sxs-lookup"><span data-stu-id="e1ebf-780">Inner actions to execute when expression evaluates to `false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="e1ebf-781">The following table shows examples of how conditions can use expressions in an action:</span><span class="sxs-lookup"><span data-stu-id="e1ebf-781">The following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="e1ebf-782">JSON value</span><span class="sxs-lookup"><span data-stu-id="e1ebf-782">JSON value</span></span>|<span data-ttu-id="e1ebf-783">Result</span><span class="sxs-lookup"><span data-stu-id="e1ebf-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="e1ebf-784">Any value that would evaluate to true causes this condition to pass.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-784">Any value that would evaluate to true causes this condition to pass.</span></span> <span data-ttu-id="e1ebf-785">Only Boolean expressions are supported.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="e1ebf-786">To convert other types to Boolean, use functions `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-786">To convert other types to Boolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="e1ebf-787">Comparison functions are supported.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-787">Comparison functions are supported.</span></span> <span data-ttu-id="e1ebf-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="e1ebf-789">Logic functions are also supported to create nested Boolean expressions.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-789">Logic functions are also supported to create nested Boolean expressions.</span></span> <span data-ttu-id="e1ebf-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="e1ebf-791">You can use array functions to check if an array has any items.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-791">You can use array functions to check if an array has any items.</span></span> <span data-ttu-id="e1ebf-792">In this case, the action executes when the errors array is empty.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-792">In this case, the action executes when the errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="e1ebf-793">Error - not a valid condition because @ is required for conditions.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="e1ebf-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span></span> <span data-ttu-id="e1ebf-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span><span class="sxs-lookup"><span data-stu-id="e1ebf-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1ebf-796">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1ebf-796">Next steps</span></span>

[<span data-ttu-id="e1ebf-797">Workflow Service REST API</span><span class="sxs-lookup"><span data-stu-id="e1ebf-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
