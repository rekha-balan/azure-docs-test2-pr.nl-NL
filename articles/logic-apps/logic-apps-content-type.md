---
title: Handle content types - Azure Logic Apps | Microsoft Docs
description: How Azure Logic Apps deals with content types at design and runtime
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: ''
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: jehollan
ms.openlocfilehash: f35a494f33561353a5c090275a55663036d9d457
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563791"
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="2b503-103">Handle content types in logic apps</span><span class="sxs-lookup"><span data-stu-id="2b503-103">Handle content types in logic apps</span></span>

<span data-ttu-id="2b503-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span><span class="sxs-lookup"><span data-stu-id="2b503-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="2b503-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span><span class="sxs-lookup"><span data-stu-id="2b503-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="2b503-106">Others might require casting or conversions as necessary.</span><span class="sxs-lookup"><span data-stu-id="2b503-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="2b503-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span><span class="sxs-lookup"><span data-stu-id="2b503-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="2b503-108">Content-Type Header</span><span class="sxs-lookup"><span data-stu-id="2b503-108">Content-Type Header</span></span>

<span data-ttu-id="2b503-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="2b503-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="2b503-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="2b503-110">Application/JSON</span></span>

<span data-ttu-id="2b503-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span><span class="sxs-lookup"><span data-stu-id="2b503-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="2b503-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span><span class="sxs-lookup"><span data-stu-id="2b503-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="2b503-113">Also, JSON content can be parsed by default without needing any casting.</span><span class="sxs-lookup"><span data-stu-id="2b503-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="2b503-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span><span class="sxs-lookup"><span data-stu-id="2b503-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="2b503-115">No additional casting is needed.</span><span class="sxs-lookup"><span data-stu-id="2b503-115">No additional casting is needed.</span></span> <span data-ttu-id="2b503-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="2b503-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="2b503-117">Schema and schema generator</span><span class="sxs-lookup"><span data-stu-id="2b503-117">Schema and schema generator</span></span>

<span data-ttu-id="2b503-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span><span class="sxs-lookup"><span data-stu-id="2b503-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="2b503-119">This schema lets the designer generate tokens so you can consume the content of the request.</span><span class="sxs-lookup"><span data-stu-id="2b503-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="2b503-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span><span class="sxs-lookup"><span data-stu-id="2b503-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Schema](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="2b503-122">'Parse JSON' action</span><span class="sxs-lookup"><span data-stu-id="2b503-122">'Parse JSON' action</span></span>

<span data-ttu-id="2b503-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span><span class="sxs-lookup"><span data-stu-id="2b503-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="2b503-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span><span class="sxs-lookup"><span data-stu-id="2b503-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="2b503-125">This tool makes consuming data from Service Bus, DocumentDB, and so on, much easier.</span><span class="sxs-lookup"><span data-stu-id="2b503-125">This tool makes consuming data from Service Bus, DocumentDB, and so on, much easier.</span></span>

![Parse JSON](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="2b503-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="2b503-127">Text/plain</span></span>

<span data-ttu-id="2b503-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span><span class="sxs-lookup"><span data-stu-id="2b503-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="2b503-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span><span class="sxs-lookup"><span data-stu-id="2b503-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="2b503-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="2b503-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="2b503-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span><span class="sxs-lookup"><span data-stu-id="2b503-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="2b503-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="2b503-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="2b503-133">Application/xml and Application/octet-stream and converter functions</span><span class="sxs-lookup"><span data-stu-id="2b503-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="2b503-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span><span class="sxs-lookup"><span data-stu-id="2b503-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="2b503-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="2b503-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="2b503-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span><span class="sxs-lookup"><span data-stu-id="2b503-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="2b503-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span><span class="sxs-lookup"><span data-stu-id="2b503-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="2b503-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span><span class="sxs-lookup"><span data-stu-id="2b503-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="2b503-139">`@json()` - casts data to `application/json`</span><span class="sxs-lookup"><span data-stu-id="2b503-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="2b503-140">`@xml()` - casts data to `application/xml`</span><span class="sxs-lookup"><span data-stu-id="2b503-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="2b503-141">`@binary()` - casts data to `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="2b503-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="2b503-142">`@string()` - casts data to `text/plain`</span><span class="sxs-lookup"><span data-stu-id="2b503-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="2b503-143">`@base64()` - converts content to a base64 string</span><span class="sxs-lookup"><span data-stu-id="2b503-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="2b503-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span><span class="sxs-lookup"><span data-stu-id="2b503-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="2b503-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="2b503-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="2b503-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span><span class="sxs-lookup"><span data-stu-id="2b503-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="2b503-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span><span class="sxs-lookup"><span data-stu-id="2b503-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="2b503-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="2b503-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="2b503-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="2b503-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="2b503-150">Other content types</span><span class="sxs-lookup"><span data-stu-id="2b503-150">Other content types</span></span>

<span data-ttu-id="2b503-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span><span class="sxs-lookup"><span data-stu-id="2b503-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="2b503-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span><span class="sxs-lookup"><span data-stu-id="2b503-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="2b503-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span><span class="sxs-lookup"><span data-stu-id="2b503-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Currently, there isn't a native function for form data, so you could still use this data in a workflow by manually accessing the data with a function like `@string(body('formdataAction'))`. If you wanted the outgoing request to also have the `application/x-www-url-formencoded` content type header, you could add the request to the action body without any casting like `@body('formdataAction')`. However, this method only works if the body is the only parameter in the `body` input. <span data-ttu-id="2b503-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span><span class="sxs-lookup"><span data-stu-id="2b503-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>



