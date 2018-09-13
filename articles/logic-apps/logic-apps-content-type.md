---
title: Handle content types - Azure Logic Apps | Microsoft Docs
description: Learn how Logic Apps handles content types at design time and run time
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: article
ms.date: 07/20/2018
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: 82eb9c895f016efe569651dc89885d2e4850fd59
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44787025"
---
# <a name="handle-content-types-in-azure-logic-apps"></a><span data-ttu-id="83654-103">Handle content types in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="83654-103">Handle content types in Azure Logic Apps</span></span>

<span data-ttu-id="83654-104">Various content types can flow through a logic app, for example, JSON, XML, flat files, and binary data.</span><span class="sxs-lookup"><span data-stu-id="83654-104">Various content types can flow through a logic app, for example, JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="83654-105">While Logic Apps supports all content types, some have native support and don't require casting or conversion in your logic apps.</span><span class="sxs-lookup"><span data-stu-id="83654-105">While Logic Apps supports all content types, some have native support and don't require casting or conversion in your logic apps.</span></span> <span data-ttu-id="83654-106">Other types might require casting or conversion as necessary.</span><span class="sxs-lookup"><span data-stu-id="83654-106">Other types might require casting or conversion as necessary.</span></span> <span data-ttu-id="83654-107">This article describes how Logic Apps handles content types and how you can correctly cast or convert these types when necessary.</span><span class="sxs-lookup"><span data-stu-id="83654-107">This article describes how Logic Apps handles content types and how you can correctly cast or convert these types when necessary.</span></span>

<span data-ttu-id="83654-108">To determine the appropriate way for handling content types, Logic Apps relies on the `Content-Type` header value in HTTP calls, for example:</span><span class="sxs-lookup"><span data-stu-id="83654-108">To determine the appropriate way for handling content types, Logic Apps relies on the `Content-Type` header value in HTTP calls, for example:</span></span>

* <span data-ttu-id="83654-109">[application/json](#application-json) (native type)</span><span class="sxs-lookup"><span data-stu-id="83654-109">[application/json](#application-json) (native type)</span></span>
* <span data-ttu-id="83654-110">[text/plain](#text-plain) (native type)</span><span class="sxs-lookup"><span data-stu-id="83654-110">[text/plain](#text-plain) (native type)</span></span>
* [<span data-ttu-id="83654-111">application/xml and application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="83654-111">application/xml and application/octet-stream</span></span>](#application-xml-octet-stream)
* [<span data-ttu-id="83654-112">Other content types</span><span class="sxs-lookup"><span data-stu-id="83654-112">Other content types</span></span>](#other-content-types)

<a name="application-json"></a>

## <a name="applicationjson"></a><span data-ttu-id="83654-113">application/json</span><span class="sxs-lookup"><span data-stu-id="83654-113">application/json</span></span>

<span data-ttu-id="83654-114">Logic Apps stores and handles any request with the *application/json* content type as a JavaScript Notation (JSON) object.</span><span class="sxs-lookup"><span data-stu-id="83654-114">Logic Apps stores and handles any request with the *application/json* content type as a JavaScript Notation (JSON) object.</span></span> <span data-ttu-id="83654-115">By default, you can parse JSON content without any casting.</span><span class="sxs-lookup"><span data-stu-id="83654-115">By default, you can parse JSON content without any casting.</span></span> <span data-ttu-id="83654-116">To parse a request that has a header with the "application/json" content type, you can use an expression.</span><span class="sxs-lookup"><span data-stu-id="83654-116">To parse a request that has a header with the "application/json" content type, you can use an expression.</span></span> <span data-ttu-id="83654-117">This example returns the value `dog` from the `animal-type` array without casting:</span><span class="sxs-lookup"><span data-stu-id="83654-117">This example returns the value `dog` from the `animal-type` array without casting:</span></span> 
 
`@body('myAction')['animal-type'][0]` 
  
  ```json
  {
    "client": {
       "name": "Fido",
       "animal-type": [ "dog", "cat", "rabbit", "snake" ]
    }
  }
  ```

<span data-ttu-id="83654-118">If you're working with JSON data that doesn't specify a header, you can manually cast that data to JSON by using the [json() function](../logic-apps/workflow-definition-language-functions-reference.md#json), for example:</span><span class="sxs-lookup"><span data-stu-id="83654-118">If you're working with JSON data that doesn't specify a header, you can manually cast that data to JSON by using the [json() function](../logic-apps/workflow-definition-language-functions-reference.md#json), for example:</span></span> 
  
`@json(triggerBody())['animal-type']`

### <a name="create-tokens-for-json-properties"></a><span data-ttu-id="83654-119">Create tokens for JSON properties</span><span class="sxs-lookup"><span data-stu-id="83654-119">Create tokens for JSON properties</span></span>

<span data-ttu-id="83654-120">Logic Apps provides the capability for you to generate user-friendly tokens that represent the properties in JSON content so you can reference and use those properties more easily in your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="83654-120">Logic Apps provides the capability for you to generate user-friendly tokens that represent the properties in JSON content so you can reference and use those properties more easily in your logic app's workflow.</span></span>

* <span data-ttu-id="83654-121">**Request trigger**</span><span class="sxs-lookup"><span data-stu-id="83654-121">**Request trigger**</span></span>

  <span data-ttu-id="83654-122">When you use this trigger in the Logic App Designer, you can provide a JSON schema that describes the payload you expect to receive.</span><span class="sxs-lookup"><span data-stu-id="83654-122">When you use this trigger in the Logic App Designer, you can provide a JSON schema that describes the payload you expect to receive.</span></span> 
  <span data-ttu-id="83654-123">The designer parses JSON content by using this schema and generates user-friendly tokens that represent the properties in your JSON content.</span><span class="sxs-lookup"><span data-stu-id="83654-123">The designer parses JSON content by using this schema and generates user-friendly tokens that represent the properties in your JSON content.</span></span> 
  <span data-ttu-id="83654-124">You can then easily reference and use those properties throughout your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="83654-124">You can then easily reference and use those properties throughout your logic app's workflow.</span></span> 
  
  <span data-ttu-id="83654-125">If you don't have a schema, you can generate the schema.</span><span class="sxs-lookup"><span data-stu-id="83654-125">If you don't have a schema, you can generate the schema.</span></span> 
  
  1. <span data-ttu-id="83654-126">In the Request trigger, select **Use sample payload to generate schema**.</span><span class="sxs-lookup"><span data-stu-id="83654-126">In the Request trigger, select **Use sample payload to generate schema**.</span></span>  
  
  2. <span data-ttu-id="83654-127">Under **Enter or paste a sample JSON payload**, provide a sample payload and then choose **Done**.</span><span class="sxs-lookup"><span data-stu-id="83654-127">Under **Enter or paste a sample JSON payload**, provide a sample payload and then choose **Done**.</span></span> <span data-ttu-id="83654-128">For example:</span><span class="sxs-lookup"><span data-stu-id="83654-128">For example:</span></span> 

     ![Provide sample JSON payload](./media/logic-apps-content-type/request-trigger.png)

     <span data-ttu-id="83654-130">The generated schema now appears in your trigger.</span><span class="sxs-lookup"><span data-stu-id="83654-130">The generated schema now appears in your trigger.</span></span>

     ![Provide sample JSON payload](./media/logic-apps-content-type/generated-schema.png)

     <span data-ttu-id="83654-132">Here is the underlying definition for your Request trigger in the code view editor:</span><span class="sxs-lookup"><span data-stu-id="83654-132">Here is the underlying definition for your Request trigger in the code view editor:</span></span>

     ```json
     "triggers": { 
        "manual": {
           "type": "Request",
           "kind": "Http",
           "inputs": { 
              "schema": {
                 "type": "object",
                 "properties": {
                    "client": {
                       "type": "object",
                       "properties": {
                          "animal-type": {
                             "type": "array",
                             "items": {
                                "type": "string"
                             },
                          },
                          "name": {
                             "type": "string"
                          }
                       }
                    }
                 }
              }
           }
        }
     }
     ```

  3. <span data-ttu-id="83654-133">In your request, make sure you include a `Content-Type` header and set the header's value to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="83654-133">In your request, make sure you include a `Content-Type` header and set the header's value to `application/json`.</span></span>

* <span data-ttu-id="83654-134">**Parse JSON action**</span><span class="sxs-lookup"><span data-stu-id="83654-134">**Parse JSON action**</span></span>

  <span data-ttu-id="83654-135">When you use this action in the Logic App Designer, you can parse JSON output and generate user-friendly tokens that represent the properties in your JSON content.</span><span class="sxs-lookup"><span data-stu-id="83654-135">When you use this action in the Logic App Designer, you can parse JSON output and generate user-friendly tokens that represent the properties in your JSON content.</span></span> 
  <span data-ttu-id="83654-136">You can then easily reference and use those properties throughout your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="83654-136">You can then easily reference and use those properties throughout your logic app's workflow.</span></span> <span data-ttu-id="83654-137">Similar to the Request trigger, you can provide or generate a JSON schema that describes the JSON content you want to parse.</span><span class="sxs-lookup"><span data-stu-id="83654-137">Similar to the Request trigger, you can provide or generate a JSON schema that describes the JSON content you want to parse.</span></span> 
  <span data-ttu-id="83654-138">That way, you can more easily consume data from Azure Service Bus, Azure Cosmos DB, and so on.</span><span class="sxs-lookup"><span data-stu-id="83654-138">That way, you can more easily consume data from Azure Service Bus, Azure Cosmos DB, and so on.</span></span>

  ![Parse JSON](./media/logic-apps-content-type/parse-json.png)

<a name="text-plain"></a>

## <a name="textplain"></a><span data-ttu-id="83654-140">text/plain</span><span class="sxs-lookup"><span data-stu-id="83654-140">text/plain</span></span>

<span data-ttu-id="83654-141">When your logic app receives HTTP messages that have the `Content-Type` header set to `text/plain`, your logic app stores those messages in raw form.</span><span class="sxs-lookup"><span data-stu-id="83654-141">When your logic app receives HTTP messages that have the `Content-Type` header set to `text/plain`, your logic app stores those messages in raw form.</span></span> <span data-ttu-id="83654-142">If you include these messages in subsequent actions without casting, requests go out with the `Content-Type` header set to `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="83654-142">If you include these messages in subsequent actions without casting, requests go out with the `Content-Type` header set to `text/plain`.</span></span> 

<span data-ttu-id="83654-143">For example, when you're working with a flat file, you might get an HTTP request with the `Content-Type` header set to `text/plain` content type:</span><span class="sxs-lookup"><span data-stu-id="83654-143">For example, when you're working with a flat file, you might get an HTTP request with the `Content-Type` header set to `text/plain` content type:</span></span>

`Date,Name,Address`</br>
`Oct-1,Frank,123 Ave`

<span data-ttu-id="83654-144">If you then send this request on in a later action as the body for another request, for example, `@body('flatfile')`, that second request also has a `Content-Type` header that's set to `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="83654-144">If you then send this request on in a later action as the body for another request, for example, `@body('flatfile')`, that second request also has a `Content-Type` header that's set to `text/plain`.</span></span> <span data-ttu-id="83654-145">If you're working with data that is plain text but didn't specify a header, you can manually cast that data to text by using the [string() function](../logic-apps/workflow-definition-language-functions-reference.md#string) such as this expression:</span><span class="sxs-lookup"><span data-stu-id="83654-145">If you're working with data that is plain text but didn't specify a header, you can manually cast that data to text by using the [string() function](../logic-apps/workflow-definition-language-functions-reference.md#string) such as this expression:</span></span> 

`@string(triggerBody())`

<a name="application-xml-octet-stream"></a>

## <a name="applicationxml-and-applicationoctet-stream"></a><span data-ttu-id="83654-146">application/xml and application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="83654-146">application/xml and application/octet-stream</span></span>

<span data-ttu-id="83654-147">Logic Apps always preserves the `Content-Type` in a received HTTP request or response.</span><span class="sxs-lookup"><span data-stu-id="83654-147">Logic Apps always preserves the `Content-Type` in a received HTTP request or response.</span></span> <span data-ttu-id="83654-148">So if your logic app receives content with `Content-Type` set to `application/octet-stream`, and you include that content in a later action without casting, the outgoing request also has `Content-Type` set to `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="83654-148">So if your logic app receives content with `Content-Type` set to `application/octet-stream`, and you include that content in a later action without casting, the outgoing request also has `Content-Type` set to `application/octet-stream`.</span></span> <span data-ttu-id="83654-149">That way, Logic Apps can guarantee that data doesn't get lost while moving through the workflow.</span><span class="sxs-lookup"><span data-stu-id="83654-149">That way, Logic Apps can guarantee that data doesn't get lost while moving through the workflow.</span></span> <span data-ttu-id="83654-150">However, the action state, or inputs and outputs, is stored in a JSON object while the state moves through the workflow.</span><span class="sxs-lookup"><span data-stu-id="83654-150">However, the action state, or inputs and outputs, is stored in a JSON object while the state moves through the workflow.</span></span> 

## <a name="converter-functions"></a><span data-ttu-id="83654-151">Converter functions</span><span class="sxs-lookup"><span data-stu-id="83654-151">Converter functions</span></span>

<span data-ttu-id="83654-152">To preserve some data types, Logic Apps converts content to a binary base64-encoded string with appropriate metadata that preserves both the `$content` payload and the `$content-type`, which are automatically converted.</span><span class="sxs-lookup"><span data-stu-id="83654-152">To preserve some data types, Logic Apps converts content to a binary base64-encoded string with appropriate metadata that preserves both the `$content` payload and the `$content-type`, which are automatically converted.</span></span> 

<span data-ttu-id="83654-153">This list describes how Logic Apps converts content when you use these [functions](../logic-apps/workflow-definition-language-functions-reference.md):</span><span class="sxs-lookup"><span data-stu-id="83654-153">This list describes how Logic Apps converts content when you use these [functions](../logic-apps/workflow-definition-language-functions-reference.md):</span></span>

* <span data-ttu-id="83654-154">`json()`: Casts data to `application/json`</span><span class="sxs-lookup"><span data-stu-id="83654-154">`json()`: Casts data to `application/json`</span></span>
* <span data-ttu-id="83654-155">`xml()`: Casts data to `application/xml`</span><span class="sxs-lookup"><span data-stu-id="83654-155">`xml()`: Casts data to `application/xml`</span></span>
* <span data-ttu-id="83654-156">`binary()`: Casts data to `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="83654-156">`binary()`: Casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="83654-157">`string()`: Casts data to `text/plain`</span><span class="sxs-lookup"><span data-stu-id="83654-157">`string()`: Casts data to `text/plain`</span></span>
* <span data-ttu-id="83654-158">`base64()`: Converts content to a base64 string</span><span class="sxs-lookup"><span data-stu-id="83654-158">`base64()`: Converts content to a base64 string</span></span>
* <span data-ttu-id="83654-159">`base64toString()`: Converts a base64 encoded string to `text/plain`</span><span class="sxs-lookup"><span data-stu-id="83654-159">`base64toString()`: Converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="83654-160">`base64toBinary()`: Converts a base64 encoded string to `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="83654-160">`base64toBinary()`: Converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="83654-161">`encodeDataUri()`: Encodes a string as a dataUri byte array</span><span class="sxs-lookup"><span data-stu-id="83654-161">`encodeDataUri()`: Encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="83654-162">`decodeDataUri()`: Decodes a `dataUri` into a byte array</span><span class="sxs-lookup"><span data-stu-id="83654-162">`decodeDataUri()`: Decodes a `dataUri` into a byte array</span></span>

<span data-ttu-id="83654-163">For example, if you receive an HTTP request where `Content-Type` set to `application/xml`, such as this content:</span><span class="sxs-lookup"><span data-stu-id="83654-163">For example, if you receive an HTTP request where `Content-Type` set to `application/xml`, such as this content:</span></span>

```html
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="83654-164">You can cast this content by using the `@xml(triggerBody())` expression with the `xml()` and `triggerBody()` functions and then use this content later.</span><span class="sxs-lookup"><span data-stu-id="83654-164">You can cast this content by using the `@xml(triggerBody())` expression with the `xml()` and `triggerBody()` functions and then use this content later.</span></span> <span data-ttu-id="83654-165">Or, you can use the `@xpath(xml(triggerBody()), '/CustomerName')` expression with the `xpath()` and `xml()` functions.</span><span class="sxs-lookup"><span data-stu-id="83654-165">Or, you can use the `@xpath(xml(triggerBody()), '/CustomerName')` expression with the `xpath()` and `xml()` functions.</span></span> 

## <a name="other-content-types"></a><span data-ttu-id="83654-166">Other content types</span><span class="sxs-lookup"><span data-stu-id="83654-166">Other content types</span></span>

<span data-ttu-id="83654-167">Logic Apps works with and supports other content types, but might require that you manually get the message body by decoding the `$content` variable.</span><span class="sxs-lookup"><span data-stu-id="83654-167">Logic Apps works with and supports other content types, but might require that you manually get the message body by decoding the `$content` variable.</span></span>

<span data-ttu-id="83654-168">For example, suppose your logic app gets triggered by a request with the `application/x-www-url-formencoded` content type.</span><span class="sxs-lookup"><span data-stu-id="83654-168">For example, suppose your logic app gets triggered by a request with the `application/x-www-url-formencoded` content type.</span></span> <span data-ttu-id="83654-169">To preserve all the data, the `$content` variable in the request body has a payload that's encoded as a base64 string:</span><span class="sxs-lookup"><span data-stu-id="83654-169">To preserve all the data, the `$content` variable in the request body has a payload that's encoded as a base64 string:</span></span>

`CustomerName=Frank&Address=123+Avenue`

<span data-ttu-id="83654-170">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span><span class="sxs-lookup"><span data-stu-id="83654-170">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```json
"body": {
   "$content-type": "application/x-www-url-formencoded",
   "$content": "AAB1241BACDFA=="
}
```

<span data-ttu-id="83654-171">Logic Apps provides native functions for handling form data, for example:</span><span class="sxs-lookup"><span data-stu-id="83654-171">Logic Apps provides native functions for handling form data, for example:</span></span> 

* [<span data-ttu-id="83654-172">triggerFormDataValue()</span><span class="sxs-lookup"><span data-stu-id="83654-172">triggerFormDataValue()</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#triggerFormDataValue)
* [<span data-ttu-id="83654-173">triggerFormDataMultiValues()</span><span class="sxs-lookup"><span data-stu-id="83654-173">triggerFormDataMultiValues()</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#triggerFormDataMultiValues)
* [<span data-ttu-id="83654-174">formDataValue()</span><span class="sxs-lookup"><span data-stu-id="83654-174">formDataValue()</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#formDataValue) 
* [<span data-ttu-id="83654-175">formDataMultiValues()</span><span class="sxs-lookup"><span data-stu-id="83654-175">formDataMultiValues()</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#formDataMultiValues)

<span data-ttu-id="83654-176">Or, you can manually access the data by using an expression such as this example:</span><span class="sxs-lookup"><span data-stu-id="83654-176">Or, you can manually access the data by using an expression such as this example:</span></span>

`@string(body('formdataAction'))` 

<span data-ttu-id="83654-177">If you wanted the outgoing request to have the same `application/x-www-url-formencoded` content type header, you can add the request to the action's body without any casting by using an expression such as `@body('formdataAction')`.</span><span class="sxs-lookup"><span data-stu-id="83654-177">If you wanted the outgoing request to have the same `application/x-www-url-formencoded` content type header, you can add the request to the action's body without any casting by using an expression such as `@body('formdataAction')`.</span></span> <span data-ttu-id="83654-178">However, this method only works when the body is the only parameter in the `body` input.</span><span class="sxs-lookup"><span data-stu-id="83654-178">However, this method only works when the body is the only parameter in the `body` input.</span></span> <span data-ttu-id="83654-179">If you try to use the `@body('formdataAction')` expression in an `application/json` request, you get a runtime error because the body is sent encoded.</span><span class="sxs-lookup"><span data-stu-id="83654-179">If you try to use the `@body('formdataAction')` expression in an `application/json` request, you get a runtime error because the body is sent encoded.</span></span>
