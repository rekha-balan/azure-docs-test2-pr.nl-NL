---
title: Call, trigger, or nest workflows with HTTP endpoints - Azure Logic Apps | Microsoft Docs
description: Set up HTTP endpoints to call, trigger, or nest workflows for Azure Logic Apps
services: logic-apps
keywords: workflows, HTTP endpoints
author: jeffhollan
manager: anneta
editor: ''
documentationcenter: ''
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: jehollan; LADocs
ms.openlocfilehash: 871f585bc29b5ebfa5456a7332bfc5c22bdd7955
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660698"
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="8c1f2-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span><span class="sxs-lookup"><span data-stu-id="8c1f2-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="8c1f2-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="8c1f2-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="8c1f2-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="8c1f2-108">Request</span><span class="sxs-lookup"><span data-stu-id="8c1f2-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="8c1f2-109">API Connection Webhook</span><span class="sxs-lookup"><span data-stu-id="8c1f2-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection)

* [<span data-ttu-id="8c1f2-110">HTTP Webhook</span><span class="sxs-lookup"><span data-stu-id="8c1f2-110">HTTP Webhook</span></span>](../connectors/connectors-native-http.md)

   > [!NOTE]
   > <span data-ttu-id="8c1f2-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="8c1f2-112">Set up an HTTP endpoint for your logic app</span><span class="sxs-lookup"><span data-stu-id="8c1f2-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="8c1f2-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="8c1f2-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="8c1f2-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="8c1f2-115">Go to your logic app, and open Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-115">Go to your logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="8c1f2-116">Add a trigger that lets your logic app receive incoming requests.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="8c1f2-117">For example, add the **Request** trigger to your logic app.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-117">For example, add the **Request** trigger to your logic app.</span></span>

3.  <span data-ttu-id="8c1f2-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span></span>

    <span data-ttu-id="8c1f2-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span></span> 
    <span data-ttu-id="8c1f2-120">More about [tokens generated from JSON schemas](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="8c1f2-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="8c1f2-121">For this example, enter the schema shown in the designer:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-121">For this example, enter the schema shown in the designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Add the Request action][1]

    > [!TIP]
    > 
    > <span data-ttu-id="8c1f2-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span></span> 
    > <span data-ttu-id="8c1f2-124">Enter your sample payload, and choose **Done**.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="8c1f2-125">For example, this sample payload:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="8c1f2-126">generates this schema:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="8c1f2-127">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-127">Save your logic app.</span></span> <span data-ttu-id="8c1f2-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span></span>

    ![Generated callback URL for endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="8c1f2-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="8c1f2-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span></span> <span data-ttu-id="8c1f2-132">Under **Trigger History**, select your trigger:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-132">Under **Trigger History**, select your trigger:</span></span>

    ![Get HTTP endpoint URL from Azure portal][2]

    <span data-ttu-id="8c1f2-134">Or you can get the URL by making this call:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-134">Or you can get the URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-the-http-method-for-your-trigger"></a><span data-ttu-id="8c1f2-135">Change the HTTP method for your trigger</span><span class="sxs-lookup"><span data-stu-id="8c1f2-135">Change the HTTP method for your trigger</span></span>

<span data-ttu-id="8c1f2-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="8c1f2-137">You can specify only one method type.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="8c1f2-138">On your **Request** trigger, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="8c1f2-139">Open the **Method** list.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-139">Open the **Method** list.</span></span> <span data-ttu-id="8c1f2-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8c1f2-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Change HTTP method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="8c1f2-143">Accept parameters through your HTTP endpoint URL</span><span class="sxs-lookup"><span data-stu-id="8c1f2-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="8c1f2-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="8c1f2-145">On your **Request** trigger, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="8c1f2-146">Under **Method**, specify the HTTP method that you want your request to use.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-146">Under **Method**, specify the HTTP method that you want your request to use.</span></span> <span data-ttu-id="8c1f2-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8c1f2-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="8c1f2-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Specify the HTTP method and relative path for parameter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="8c1f2-151">To use the parameter, add a **Response** action to your logic app.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-151">To use the parameter, add a **Response** action to your logic app.</span></span> <span data-ttu-id="8c1f2-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span><span class="sxs-lookup"><span data-stu-id="8c1f2-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="8c1f2-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="8c1f2-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="8c1f2-155">The dynamic content list should appear and show the `customerID` token for you to select.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-155">The dynamic content list should appear and show the `customerID` token for you to select.</span></span>

    ![Add parameter to response body](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="8c1f2-157">Your **Body** should look like this example:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-157">Your **Body** should look like this example:</span></span>

    ![Response body with parameter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="8c1f2-159">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-159">Save your logic app.</span></span> 

    <span data-ttu-id="8c1f2-160">Your HTTP endpoint URL now includes the relative path, for example:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-160">Your HTTP endpoint URL now includes the relative path, for example:</span></span> 

    <span data-ttu-id="8c1f2-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="8c1f2-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="8c1f2-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="8c1f2-163">Your browser should show this text:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="8c1f2-164">Tokens generated from JSON schemas for your logic app</span><span class="sxs-lookup"><span data-stu-id="8c1f2-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="8c1f2-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="8c1f2-166">You can then use those tokens for passing data through your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="8c1f2-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span></span> 

<span data-ttu-id="8c1f2-168">Here is the complete JSON schema:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-168">Here is the complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="8c1f2-169">Create nested workflows for logic apps</span><span class="sxs-lookup"><span data-stu-id="8c1f2-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="8c1f2-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="8c1f2-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span></span> <span data-ttu-id="8c1f2-172">You can then select from eligible logic apps.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-172">You can then select from eligible logic apps.</span></span>

![Add another logic app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="8c1f2-174">Call or trigger logic apps through HTTP endpoints</span><span class="sxs-lookup"><span data-stu-id="8c1f2-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="8c1f2-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span></span> <span data-ttu-id="8c1f2-176">Logic apps have built-in support for direct-access endpoints.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="8c1f2-177">Reference content from an incoming request</span><span class="sxs-lookup"><span data-stu-id="8c1f2-177">Reference content from an incoming request</span></span>

<span data-ttu-id="8c1f2-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span></span> <span data-ttu-id="8c1f2-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span></span> <span data-ttu-id="8c1f2-180">You can't reference this content inside the workflow without converting that content.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-180">You can't reference this content inside the workflow without converting that content.</span></span> <span data-ttu-id="8c1f2-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span></span> <span data-ttu-id="8c1f2-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="8c1f2-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="8c1f2-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span></span> <span data-ttu-id="8c1f2-184">The output might look like this example:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-184">The output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="8c1f2-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span></span> 

## <a name="respond-to-requests"></a><span data-ttu-id="8c1f2-186">Respond to requests</span><span class="sxs-lookup"><span data-stu-id="8c1f2-186">Respond to requests</span></span>

<span data-ttu-id="8c1f2-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span></span> <span data-ttu-id="8c1f2-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span></span> <span data-ttu-id="8c1f2-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="8c1f2-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="8c1f2-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span></span> <span data-ttu-id="8c1f2-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="8c1f2-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-the-response"></a><span data-ttu-id="8c1f2-194">Construct the response</span><span class="sxs-lookup"><span data-stu-id="8c1f2-194">Construct the response</span></span>

<span data-ttu-id="8c1f2-195">You can include more than one header and any type of content in the response body.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-195">You can include more than one header and any type of content in the response body.</span></span> <span data-ttu-id="8c1f2-196">In our example response, the header specifies that the response has content type `application/json`.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-196">In our example response, the header specifies that the response has content type `application/json`.</span></span> <span data-ttu-id="8c1f2-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span></span>

![HTTP Response action][3]

<span data-ttu-id="8c1f2-199">Responses have these properties:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-199">Responses have these properties:</span></span>

| <span data-ttu-id="8c1f2-200">Property</span><span class="sxs-lookup"><span data-stu-id="8c1f2-200">Property</span></span> | <span data-ttu-id="8c1f2-201">Description</span><span class="sxs-lookup"><span data-stu-id="8c1f2-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c1f2-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="8c1f2-202">statusCode</span></span> |<span data-ttu-id="8c1f2-203">Specifies the HTTP status code for responding to the incoming request.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-203">Specifies the HTTP status code for responding to the incoming request.</span></span> <span data-ttu-id="8c1f2-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="8c1f2-205">However, 3xx status codes are not permitted.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="8c1f2-206">headers</span><span class="sxs-lookup"><span data-stu-id="8c1f2-206">headers</span></span> |<span data-ttu-id="8c1f2-207">Defines any number of headers to include in the response.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-207">Defines any number of headers to include in the response.</span></span> |
| <span data-ttu-id="8c1f2-208">body</span><span class="sxs-lookup"><span data-stu-id="8c1f2-208">body</span></span> |<span data-ttu-id="8c1f2-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="8c1f2-210">Here's what the JSON schema looks like now for the **Response** action:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-210">Here's what the JSON schema looks like now for the **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="8c1f2-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="8c1f2-212">Q & A</span><span class="sxs-lookup"><span data-stu-id="8c1f2-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="8c1f2-213">Q: What about URL security?</span><span class="sxs-lookup"><span data-stu-id="8c1f2-213">Q: What about URL security?</span></span>

<span data-ttu-id="8c1f2-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="8c1f2-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="8c1f2-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="8c1f2-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span></span> <span data-ttu-id="8c1f2-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span><span class="sxs-lookup"><span data-stu-id="8c1f2-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="8c1f2-218">Q: Can I configure HTTP endpoints further?</span><span class="sxs-lookup"><span data-stu-id="8c1f2-218">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="8c1f2-219">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="8c1f2-219">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="8c1f2-220">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-220">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="8c1f2-221">Change the request method</span><span class="sxs-lookup"><span data-stu-id="8c1f2-221">Change the request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="8c1f2-222">Change the URL segments of the request</span><span class="sxs-lookup"><span data-stu-id="8c1f2-222">Change the URL segments of the request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="8c1f2-223">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span><span class="sxs-lookup"><span data-stu-id="8c1f2-223">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="8c1f2-224">Set up policy to check for Basic authentication</span><span class="sxs-lookup"><span data-stu-id="8c1f2-224">Set up policy to check for Basic authentication</span></span>

#### <a name="q-what-changed-when-the-schema-migrated-from-the-december-1-2014-preview"></a><span data-ttu-id="8c1f2-225">Q: What changed when the schema migrated from the December 1, 2014 preview?</span><span class="sxs-lookup"><span data-stu-id="8c1f2-225">Q: What changed when the schema migrated from the December 1, 2014 preview?</span></span>

<span data-ttu-id="8c1f2-226">A: Here's a summary about these changes:</span><span class="sxs-lookup"><span data-stu-id="8c1f2-226">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="8c1f2-227">December 1, 2014 preview</span><span class="sxs-lookup"><span data-stu-id="8c1f2-227">December 1, 2014 preview</span></span> | <span data-ttu-id="8c1f2-228">June 1, 2016</span><span class="sxs-lookup"><span data-stu-id="8c1f2-228">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="8c1f2-229">Click **HTTP Listener** API App</span><span class="sxs-lookup"><span data-stu-id="8c1f2-229">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="8c1f2-230">Click **Manual trigger** (no API App required)</span><span class="sxs-lookup"><span data-stu-id="8c1f2-230">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="8c1f2-231">HTTP Listener setting "*Sends response automatically*"</span><span class="sxs-lookup"><span data-stu-id="8c1f2-231">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="8c1f2-232">Either include a **Response** action or not in the workflow definition</span><span class="sxs-lookup"><span data-stu-id="8c1f2-232">Either include a **Response** action or not in the workflow definition</span></span> |
| <span data-ttu-id="8c1f2-233">Configure Basic or OAuth authentication</span><span class="sxs-lookup"><span data-stu-id="8c1f2-233">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="8c1f2-234">via API Management</span><span class="sxs-lookup"><span data-stu-id="8c1f2-234">via API Management</span></span> |
| <span data-ttu-id="8c1f2-235">Configure HTTP method</span><span class="sxs-lookup"><span data-stu-id="8c1f2-235">Configure HTTP method</span></span> |<span data-ttu-id="8c1f2-236">Under **Show advanced options**, choose an HTTP method</span><span class="sxs-lookup"><span data-stu-id="8c1f2-236">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="8c1f2-237">Configure relative path</span><span class="sxs-lookup"><span data-stu-id="8c1f2-237">Configure relative path</span></span> |<span data-ttu-id="8c1f2-238">Under **Show advanced options**, add a relative path</span><span class="sxs-lookup"><span data-stu-id="8c1f2-238">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="8c1f2-239">Reference the incoming body through `@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="8c1f2-239">Reference the incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="8c1f2-240">Reference through `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="8c1f2-240">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="8c1f2-241">**Send HTTP response** action on the HTTP Listener</span><span class="sxs-lookup"><span data-stu-id="8c1f2-241">**Send HTTP response** action on the HTTP Listener</span></span> |<span data-ttu-id="8c1f2-242">Click **Respond to HTTP request** (no API App required)</span><span class="sxs-lookup"><span data-stu-id="8c1f2-242">Click **Respond to HTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="8c1f2-243">Get help</span><span class="sxs-lookup"><span data-stu-id="8c1f2-243">Get help</span></span>

<span data-ttu-id="8c1f2-244">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="8c1f2-244">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="8c1f2-245">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="8c1f2-245">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c1f2-246">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c1f2-246">Next steps</span></span>

* [<span data-ttu-id="8c1f2-247">Author logic app definitions</span><span class="sxs-lookup"><span data-stu-id="8c1f2-247">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="8c1f2-248">Handle errors and exceptions</span><span class="sxs-lookup"><span data-stu-id="8c1f2-248">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/manualtrigger.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/response.png









