---
title: Handle large messages in Azure Logic Apps | Microsoft Docs
description: Learn how to handle large message sizes with chunking in logic apps
services: logic-apps
documentationcenter: ''
author: shae-hurst
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: logic-apps
ms.workload: logic-apps
ms.devlang: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.date: 4/27/2018
ms.author: shhurst
ms.openlocfilehash: 6064db5455d92d15dca0e2a4a78285f0aeade904
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968147"
---
# <a name="handle-large-messages-with-chunking-in-logic-apps"></a><span data-ttu-id="d9a4e-103">Handle large messages with chunking in Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d9a4e-103">Handle large messages with chunking in Logic Apps</span></span>

<span data-ttu-id="d9a4e-104">When handling messages, Logic Apps limits message content to a maximum size.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-104">When handling messages, Logic Apps limits message content to a maximum size.</span></span> <span data-ttu-id="d9a4e-105">This limit helps reduce overhead created by storing and processing large messages.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-105">This limit helps reduce overhead created by storing and processing large messages.</span></span> <span data-ttu-id="d9a4e-106">To handle messages larger than this limit, Logic Apps can *chunk* a large message into smaller messages.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-106">To handle messages larger than this limit, Logic Apps can *chunk* a large message into smaller messages.</span></span> <span data-ttu-id="d9a4e-107">That way, you can still transfer large files using Logic Apps under specific conditions.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-107">That way, you can still transfer large files using Logic Apps under specific conditions.</span></span> <span data-ttu-id="d9a4e-108">When communicating with other services through connectors or HTTP, Logic Apps can consume large messages but *only* in chunks.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-108">When communicating with other services through connectors or HTTP, Logic Apps can consume large messages but *only* in chunks.</span></span> <span data-ttu-id="d9a4e-109">This condition means connectors must also support chunking, or the underlying HTTP message exchange between Logic Apps and these services must use chunking.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-109">This condition means connectors must also support chunking, or the underlying HTTP message exchange between Logic Apps and these services must use chunking.</span></span>

<span data-ttu-id="d9a4e-110">This article shows how you can set up chunking support for messages that are larger than the limit.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-110">This article shows how you can set up chunking support for messages that are larger than the limit.</span></span>

## <a name="what-makes-messages-large"></a><span data-ttu-id="d9a4e-111">What makes messages "large"?</span><span class="sxs-lookup"><span data-stu-id="d9a4e-111">What makes messages "large"?</span></span>

<span data-ttu-id="d9a4e-112">Messages are "large" based on the service handling those messages.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-112">Messages are "large" based on the service handling those messages.</span></span> <span data-ttu-id="d9a4e-113">The exact size limit on large messages differs across Logic Apps and connectors.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-113">The exact size limit on large messages differs across Logic Apps and connectors.</span></span> <span data-ttu-id="d9a4e-114">Both Logic Apps and connectors can't directly consume large messages, which must be chunked.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-114">Both Logic Apps and connectors can't directly consume large messages, which must be chunked.</span></span> <span data-ttu-id="d9a4e-115">For the Logic Apps message size limit, see [Logic Apps limits and configuration](../logic-apps/logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="d9a4e-115">For the Logic Apps message size limit, see [Logic Apps limits and configuration](../logic-apps/logic-apps-limits-and-config.md).</span></span>
<span data-ttu-id="d9a4e-116">For each connector's message size limit, see the [connector's specific technical details](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d9a4e-116">For each connector's message size limit, see the [connector's specific technical details](../connectors/apis-list.md).</span></span>

### <a name="chunked-message-handling-for-logic-apps"></a><span data-ttu-id="d9a4e-117">Chunked message handling for Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d9a4e-117">Chunked message handling for Logic Apps</span></span>

<span data-ttu-id="d9a4e-118">Logic Apps can't directly use outputs from chunked messages that are larger than the message size limit.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-118">Logic Apps can't directly use outputs from chunked messages that are larger than the message size limit.</span></span> <span data-ttu-id="d9a4e-119">Only actions that support chunking can access the message content in these outputs.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-119">Only actions that support chunking can access the message content in these outputs.</span></span> <span data-ttu-id="d9a4e-120">So, an action that handles large messages must meet *either* these criteria:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-120">So, an action that handles large messages must meet *either* these criteria:</span></span>

* <span data-ttu-id="d9a4e-121">Natively support chunking when that action belongs to a connector.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-121">Natively support chunking when that action belongs to a connector.</span></span> 
* <span data-ttu-id="d9a4e-122">Have chunking support enabled in that action's runtime configuration.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-122">Have chunking support enabled in that action's runtime configuration.</span></span> 

<span data-ttu-id="d9a4e-123">Otherwise, you get a runtime error when you try to access large content output.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-123">Otherwise, you get a runtime error when you try to access large content output.</span></span> <span data-ttu-id="d9a4e-124">To enable chunking, see [Set up chunking support](#set-up-chunking).</span><span class="sxs-lookup"><span data-stu-id="d9a4e-124">To enable chunking, see [Set up chunking support](#set-up-chunking).</span></span>

### <a name="chunked-message-handling-for-connectors"></a><span data-ttu-id="d9a4e-125">Chunked message handling for connectors</span><span class="sxs-lookup"><span data-stu-id="d9a4e-125">Chunked message handling for connectors</span></span>

<span data-ttu-id="d9a4e-126">Services that communicate with Logic Apps can have their own message size limits.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-126">Services that communicate with Logic Apps can have their own message size limits.</span></span> <span data-ttu-id="d9a4e-127">These limits are often smaller than the Logic Apps limit.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-127">These limits are often smaller than the Logic Apps limit.</span></span> <span data-ttu-id="d9a4e-128">For example, assuming that a connector supports chunking, a connector might consider a 30-MB message as large, while Logic Apps does not.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-128">For example, assuming that a connector supports chunking, a connector might consider a 30-MB message as large, while Logic Apps does not.</span></span> <span data-ttu-id="d9a4e-129">To comply with this connector's limit, Logic Apps splits any message larger than 30 MB into smaller chunks.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-129">To comply with this connector's limit, Logic Apps splits any message larger than 30 MB into smaller chunks.</span></span>

<span data-ttu-id="d9a4e-130">For connectors that support chunking, the underlying chunking protocol is invisible to end users.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-130">For connectors that support chunking, the underlying chunking protocol is invisible to end users.</span></span> <span data-ttu-id="d9a4e-131">However, not all connectors support chunking, so these connectors generate runtime errors when incoming messages exceed the connectors' size limits.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-131">However, not all connectors support chunking, so these connectors generate runtime errors when incoming messages exceed the connectors' size limits.</span></span>

<a name="set-up-chunking"></a>

## <a name="set-up-chunking-over-http"></a><span data-ttu-id="d9a4e-132">Set up chunking over HTTP</span><span class="sxs-lookup"><span data-stu-id="d9a4e-132">Set up chunking over HTTP</span></span>

<span data-ttu-id="d9a4e-133">In generic HTTP scenarios, you can split up large content downloads and uploads over HTTP, so that your logic app and an endpoint can exchange large messages.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-133">In generic HTTP scenarios, you can split up large content downloads and uploads over HTTP, so that your logic app and an endpoint can exchange large messages.</span></span> <span data-ttu-id="d9a4e-134">However, you must chunk messages in the way that Logic Apps expects.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-134">However, you must chunk messages in the way that Logic Apps expects.</span></span> 

<span data-ttu-id="d9a4e-135">If an endpoint has enabled chunking for downloads or uploads, the HTTP actions in your logic app automatically chunk large messages.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-135">If an endpoint has enabled chunking for downloads or uploads, the HTTP actions in your logic app automatically chunk large messages.</span></span> <span data-ttu-id="d9a4e-136">Otherwise, you must set up chunking support on the endpoint.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-136">Otherwise, you must set up chunking support on the endpoint.</span></span> <span data-ttu-id="d9a4e-137">If you don't own or control the endpoint or connector, you might not have the option to set up chunking.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-137">If you don't own or control the endpoint or connector, you might not have the option to set up chunking.</span></span>

<span data-ttu-id="d9a4e-138">Also, if an HTTP action doesn't already enable chunking, you must also set up chunking in the action's `runTimeConfiguration` property.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-138">Also, if an HTTP action doesn't already enable chunking, you must also set up chunking in the action's `runTimeConfiguration` property.</span></span> <span data-ttu-id="d9a4e-139">You can set this property inside the action, either directly in the code view editor as described later, or in the Logic Apps Designer as described here:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-139">You can set this property inside the action, either directly in the code view editor as described later, or in the Logic Apps Designer as described here:</span></span>

1. <span data-ttu-id="d9a4e-140">In the HTTP action's upper-right corner, choose the ellipsis button (**...**), and then choose **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-140">In the HTTP action's upper-right corner, choose the ellipsis button (**...**), and then choose **Settings**.</span></span>

   ![On the action, open the settings menu](./media/logic-apps-handle-large-messages/http-settings.png)

2. <span data-ttu-id="d9a4e-142">Under **Content Transfer**, set **Allow chunking** to **On**.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-142">Under **Content Transfer**, set **Allow chunking** to **On**.</span></span>

   ![Turn on chunking](./media/logic-apps-handle-large-messages/set-up-chunking.png)

3. <span data-ttu-id="d9a4e-144">To continue setting up chunking for downloads or uploads, continue with the following sections.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-144">To continue setting up chunking for downloads or uploads, continue with the following sections.</span></span>

<a name="download-chunks"></a>

## <a name="download-content-in-chunks"></a><span data-ttu-id="d9a4e-145">Download content in chunks</span><span class="sxs-lookup"><span data-stu-id="d9a4e-145">Download content in chunks</span></span>

<span data-ttu-id="d9a4e-146">Many endpoints automatically send large messages in chunks when downloaded through an HTTP GET request.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-146">Many endpoints automatically send large messages in chunks when downloaded through an HTTP GET request.</span></span> <span data-ttu-id="d9a4e-147">To download chunked messages from an endpoint over HTTP, the endpoint must support partial content requests, or *chunked downloads*.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-147">To download chunked messages from an endpoint over HTTP, the endpoint must support partial content requests, or *chunked downloads*.</span></span> <span data-ttu-id="d9a4e-148">When your logic app sends an HTTP GET request to an endpoint for downloading content, and the endpoint responds with a "206" status code, the response contains chunked content.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-148">When your logic app sends an HTTP GET request to an endpoint for downloading content, and the endpoint responds with a "206" status code, the response contains chunked content.</span></span> <span data-ttu-id="d9a4e-149">Logic Apps can't control whether an endpoint supports partial requests.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-149">Logic Apps can't control whether an endpoint supports partial requests.</span></span> <span data-ttu-id="d9a4e-150">However, when your logic app gets the first "206" response, your logic app automatically sends multiple requests to download all the content.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-150">However, when your logic app gets the first "206" response, your logic app automatically sends multiple requests to download all the content.</span></span>

<span data-ttu-id="d9a4e-151">To check whether an endpoint can support partial content, send a HEAD request.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-151">To check whether an endpoint can support partial content, send a HEAD request.</span></span> <span data-ttu-id="d9a4e-152">This request helps you determine whether the response contains the `Accept-Ranges` header.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-152">This request helps you determine whether the response contains the `Accept-Ranges` header.</span></span> <span data-ttu-id="d9a4e-153">That way, if the endpoint supports chunked downloads but doesn't send chunked content, you can *suggest* this option by setting the `Range` header in your HTTP GET request.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-153">That way, if the endpoint supports chunked downloads but doesn't send chunked content, you can *suggest* this option by setting the `Range` header in your HTTP GET request.</span></span> 

<span data-ttu-id="d9a4e-154">These steps describe the detailed process Logic Apps uses for downloading chunked content from an endpoint to your logic app:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-154">These steps describe the detailed process Logic Apps uses for downloading chunked content from an endpoint to your logic app:</span></span>

1. <span data-ttu-id="d9a4e-155">Your logic app sends an HTTP GET request to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-155">Your logic app sends an HTTP GET request to the endpoint.</span></span>

   <span data-ttu-id="d9a4e-156">The request header can optionally include a `Range` field that describes a byte range for requesting content chunks.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-156">The request header can optionally include a `Range` field that describes a byte range for requesting content chunks.</span></span>

2. <span data-ttu-id="d9a4e-157">The endpoint responds with the "206" status code and an HTTP message body.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-157">The endpoint responds with the "206" status code and an HTTP message body.</span></span>

    <span data-ttu-id="d9a4e-158">Details about the content in this chunk appear in the response's `Content-Range` header,  including information that helps Logic Apps determine the start and end for the chunk,  plus the total size of the entire content before chunking.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-158">Details about the content in this chunk appear in the response's `Content-Range` header,  including information that helps Logic Apps determine the start and end for the chunk,  plus the total size of the entire content before chunking.</span></span>

3. <span data-ttu-id="d9a4e-159">Your logic app automatically sends follow-up HTTP GET requests.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-159">Your logic app automatically sends follow-up HTTP GET requests.</span></span>

    <span data-ttu-id="d9a4e-160">Your logic app sends follow-up GET requests until the entire content is retrieved.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-160">Your logic app sends follow-up GET requests until the entire content is retrieved.</span></span>

<span data-ttu-id="d9a4e-161">For example, this action definition shows an HTTP GET request that sets the `Range` header.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-161">For example, this action definition shows an HTTP GET request that sets the `Range` header.</span></span> <span data-ttu-id="d9a4e-162">The header *suggests* that the endpoint should respond with chunked content:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-162">The header *suggests* that the endpoint should respond with chunked content:</span></span>

```json
"getAction": {
    "inputs": {
        "headers": {
            "Range": "bytes=0-1023"
        },
       "method": "GET",
       "uri": "http://myAPIendpoint/api/downloadContent"
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="d9a4e-163">The GET request sets the "Range" header to "bytes=0-1023", which is the range of bytes.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-163">The GET request sets the "Range" header to "bytes=0-1023", which is the range of bytes.</span></span> <span data-ttu-id="d9a4e-164">If the endpoint supports requests for partial content, the endpoint responds with a content chunk from the requested range.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-164">If the endpoint supports requests for partial content, the endpoint responds with a content chunk from the requested range.</span></span> <span data-ttu-id="d9a4e-165">Based on the endpoint, the exact format for the "Range" header field can differ.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-165">Based on the endpoint, the exact format for the "Range" header field can differ.</span></span>

<a name="upload-chunks"></a>

## <a name="upload-content-in-chunks"></a><span data-ttu-id="d9a4e-166">Upload content in chunks</span><span class="sxs-lookup"><span data-stu-id="d9a4e-166">Upload content in chunks</span></span>

<span data-ttu-id="d9a4e-167">To upload chunked content from an HTTP action, the action must have enabled chunking support through the action's `runtimeConfiguration` property.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-167">To upload chunked content from an HTTP action, the action must have enabled chunking support through the action's `runtimeConfiguration` property.</span></span> <span data-ttu-id="d9a4e-168">This setting permits the action to start the chunking protocol.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-168">This setting permits the action to start the chunking protocol.</span></span> <span data-ttu-id="d9a4e-169">Your logic app can then send an initial POST or PUT message to the target endpoint.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-169">Your logic app can then send an initial POST or PUT message to the target endpoint.</span></span> <span data-ttu-id="d9a4e-170">After the endpoint responds with a suggested chunk size, your logic app follows up by sending HTTP PATCH requests that contain the content chunks.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-170">After the endpoint responds with a suggested chunk size, your logic app follows up by sending HTTP PATCH requests that contain the content chunks.</span></span>

<span data-ttu-id="d9a4e-171">These steps describe the detailed process Logic Apps uses for uploading chunked content from your logic app to an endpoint:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-171">These steps describe the detailed process Logic Apps uses for uploading chunked content from your logic app to an endpoint:</span></span>

1. <span data-ttu-id="d9a4e-172">Your logic app sends an initial HTTP POST or PUT request with an empty message body.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-172">Your logic app sends an initial HTTP POST or PUT request with an empty message body.</span></span> <span data-ttu-id="d9a4e-173">The request header, includes this information about the content that your logic app wants to upload in chunks:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-173">The request header, includes this information about the content that your logic app wants to upload in chunks:</span></span>

   | <span data-ttu-id="d9a4e-174">Logic Apps request header field</span><span class="sxs-lookup"><span data-stu-id="d9a4e-174">Logic Apps request header field</span></span> | <span data-ttu-id="d9a4e-175">Value</span><span class="sxs-lookup"><span data-stu-id="d9a4e-175">Value</span></span> | <span data-ttu-id="d9a4e-176">Type</span><span class="sxs-lookup"><span data-stu-id="d9a4e-176">Type</span></span> | <span data-ttu-id="d9a4e-177">Description</span><span class="sxs-lookup"><span data-stu-id="d9a4e-177">Description</span></span> |
   |---------------------------------|-------|------|-------------|
   | <span data-ttu-id="d9a4e-178">**x-ms-transfer-mode**</span><span class="sxs-lookup"><span data-stu-id="d9a4e-178">**x-ms-transfer-mode**</span></span> | <span data-ttu-id="d9a4e-179">chunked</span><span class="sxs-lookup"><span data-stu-id="d9a4e-179">chunked</span></span> | <span data-ttu-id="d9a4e-180">String</span><span class="sxs-lookup"><span data-stu-id="d9a4e-180">String</span></span> | <span data-ttu-id="d9a4e-181">Indicates that the content is uploaded in chunks</span><span class="sxs-lookup"><span data-stu-id="d9a4e-181">Indicates that the content is uploaded in chunks</span></span> |
   | <span data-ttu-id="d9a4e-182">**x-ms-content-length**</span><span class="sxs-lookup"><span data-stu-id="d9a4e-182">**x-ms-content-length**</span></span> | <span data-ttu-id="d9a4e-183"><*content-length*></span><span class="sxs-lookup"><span data-stu-id="d9a4e-183"><*content-length*></span></span> | <span data-ttu-id="d9a4e-184">Integer</span><span class="sxs-lookup"><span data-stu-id="d9a4e-184">Integer</span></span> | <span data-ttu-id="d9a4e-185">The entire content size in bytes before chunking</span><span class="sxs-lookup"><span data-stu-id="d9a4e-185">The entire content size in bytes before chunking</span></span> |
   ||||

2. <span data-ttu-id="d9a4e-186">The endpoint responds with "200" success status code and this optional information:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-186">The endpoint responds with "200" success status code and this optional information:</span></span>

   | <span data-ttu-id="d9a4e-187">Endpoint response header field</span><span class="sxs-lookup"><span data-stu-id="d9a4e-187">Endpoint response header field</span></span> | <span data-ttu-id="d9a4e-188">Type</span><span class="sxs-lookup"><span data-stu-id="d9a4e-188">Type</span></span> | <span data-ttu-id="d9a4e-189">Required</span><span class="sxs-lookup"><span data-stu-id="d9a4e-189">Required</span></span> | <span data-ttu-id="d9a4e-190">Description</span><span class="sxs-lookup"><span data-stu-id="d9a4e-190">Description</span></span> |
   |--------------------------------|------|----------|-------------|
   | <span data-ttu-id="d9a4e-191">**x-ms-chunk-size**</span><span class="sxs-lookup"><span data-stu-id="d9a4e-191">**x-ms-chunk-size**</span></span> | <span data-ttu-id="d9a4e-192">Integer</span><span class="sxs-lookup"><span data-stu-id="d9a4e-192">Integer</span></span> | <span data-ttu-id="d9a4e-193">No</span><span class="sxs-lookup"><span data-stu-id="d9a4e-193">No</span></span> | <span data-ttu-id="d9a4e-194">The suggested chunk size in bytes</span><span class="sxs-lookup"><span data-stu-id="d9a4e-194">The suggested chunk size in bytes</span></span> |
   | <span data-ttu-id="d9a4e-195">**Location**</span><span class="sxs-lookup"><span data-stu-id="d9a4e-195">**Location**</span></span> | <span data-ttu-id="d9a4e-196">String</span><span class="sxs-lookup"><span data-stu-id="d9a4e-196">String</span></span> | <span data-ttu-id="d9a4e-197">No</span><span class="sxs-lookup"><span data-stu-id="d9a4e-197">No</span></span> | <span data-ttu-id="d9a4e-198">The URL location where to send the HTTP PATCH messages</span><span class="sxs-lookup"><span data-stu-id="d9a4e-198">The URL location where to send the HTTP PATCH messages</span></span> |
   ||||

3. <span data-ttu-id="d9a4e-199">Your logic app creates and sends follow-up HTTP PATCH messages - each with this information:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-199">Your logic app creates and sends follow-up HTTP PATCH messages - each with this information:</span></span>

   * <span data-ttu-id="d9a4e-200">A content chunk based on **x-ms-chunk-size** or some internally calculated size until all the content totaling **x-ms-content-length** is sequentially uploaded</span><span class="sxs-lookup"><span data-stu-id="d9a4e-200">A content chunk based on **x-ms-chunk-size** or some internally calculated size until all the content totaling **x-ms-content-length** is sequentially uploaded</span></span>

   * <span data-ttu-id="d9a4e-201">These header details about the content chunk sent in each PATCH message:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-201">These header details about the content chunk sent in each PATCH message:</span></span>

     | <span data-ttu-id="d9a4e-202">Logic Apps request header field</span><span class="sxs-lookup"><span data-stu-id="d9a4e-202">Logic Apps request header field</span></span> | <span data-ttu-id="d9a4e-203">Value</span><span class="sxs-lookup"><span data-stu-id="d9a4e-203">Value</span></span> | <span data-ttu-id="d9a4e-204">Type</span><span class="sxs-lookup"><span data-stu-id="d9a4e-204">Type</span></span> | <span data-ttu-id="d9a4e-205">Description</span><span class="sxs-lookup"><span data-stu-id="d9a4e-205">Description</span></span> |
     |---------------------------------|-------|------|-------------|
     | <span data-ttu-id="d9a4e-206">**Content-Range**</span><span class="sxs-lookup"><span data-stu-id="d9a4e-206">**Content-Range**</span></span> | <span data-ttu-id="d9a4e-207"><*range*></span><span class="sxs-lookup"><span data-stu-id="d9a4e-207"><*range*></span></span> | <span data-ttu-id="d9a4e-208">String</span><span class="sxs-lookup"><span data-stu-id="d9a4e-208">String</span></span> | <span data-ttu-id="d9a4e-209">The byte range for the current content chunk, including the starting value, ending value, and the total content size, for example: "bytes=0-1023/10100"</span><span class="sxs-lookup"><span data-stu-id="d9a4e-209">The byte range for the current content chunk, including the starting value, ending value, and the total content size, for example: "bytes=0-1023/10100"</span></span> |
     | <span data-ttu-id="d9a4e-210">**Content-Type**</span><span class="sxs-lookup"><span data-stu-id="d9a4e-210">**Content-Type**</span></span> | <span data-ttu-id="d9a4e-211"><*content-type*></span><span class="sxs-lookup"><span data-stu-id="d9a4e-211"><*content-type*></span></span> | <span data-ttu-id="d9a4e-212">String</span><span class="sxs-lookup"><span data-stu-id="d9a4e-212">String</span></span> | <span data-ttu-id="d9a4e-213">The type of chunked content</span><span class="sxs-lookup"><span data-stu-id="d9a4e-213">The type of chunked content</span></span> |
     | <span data-ttu-id="d9a4e-214">**Content-Length**</span><span class="sxs-lookup"><span data-stu-id="d9a4e-214">**Content-Length**</span></span> | <span data-ttu-id="d9a4e-215"><*content-length*></span><span class="sxs-lookup"><span data-stu-id="d9a4e-215"><*content-length*></span></span> | <span data-ttu-id="d9a4e-216">String</span><span class="sxs-lookup"><span data-stu-id="d9a4e-216">String</span></span> | <span data-ttu-id="d9a4e-217">The length of size in bytes of the current chunk</span><span class="sxs-lookup"><span data-stu-id="d9a4e-217">The length of size in bytes of the current chunk</span></span> |
     |||||

4. <span data-ttu-id="d9a4e-218">After each PATCH request, the endpoint confirms the receipt for each chunk by responding with the "200" status code.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-218">After each PATCH request, the endpoint confirms the receipt for each chunk by responding with the "200" status code.</span></span>

<span data-ttu-id="d9a4e-219">For example, this action definition shows an HTTP POST request for uploading chunked content to an endpoint.</span><span class="sxs-lookup"><span data-stu-id="d9a4e-219">For example, this action definition shows an HTTP POST request for uploading chunked content to an endpoint.</span></span> <span data-ttu-id="d9a4e-220">In the action's `runTimeConfiguration` property, the `contentTransfer` property sets `transferMode` to `chunked`:</span><span class="sxs-lookup"><span data-stu-id="d9a4e-220">In the action's `runTimeConfiguration` property, the `contentTransfer` property sets `transferMode` to `chunked`:</span></span>

```json
"postAction": {
    "runtimeConfiguration": {
        "contentTransfer": {
            "transferMode": "chunked"
        }
    },
    "inputs": {
        "method": "POST",
        "uri": "http://myAPIendpoint/api/action",
        "body": "@body('getAction')"
    },
    "runAfter": {
    "getAction": ["Succeeded"]
    },
    "type": "Http"
}
```