---
title: Microsoft Translator Text API BreakSentence Method | Microsoft Docs
description: Use the Microsoft Translator Text API BreakSentence method.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: microsoft translator
ms.topic: article
ms.date: 03/29/2018
ms.author: v-jansko
ms.openlocfilehash: 8ce6644d21b397ea0e7f2e71e3c3a5a96638eec5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969138"
---
# <a name="text-api-30-breaksentence"></a><span data-ttu-id="923af-103">Text API 3.0: BreakSentence</span><span class="sxs-lookup"><span data-stu-id="923af-103">Text API 3.0: BreakSentence</span></span>

<span data-ttu-id="923af-104">Identifies the positioning of sentence boundaries in a piece of text.</span><span class="sxs-lookup"><span data-stu-id="923af-104">Identifies the positioning of sentence boundaries in a piece of text.</span></span>

## <a name="request-url"></a><span data-ttu-id="923af-105">Request URL</span><span class="sxs-lookup"><span data-stu-id="923af-105">Request URL</span></span>

<span data-ttu-id="923af-106">Send a `POST` request to:</span><span class="sxs-lookup"><span data-stu-id="923af-106">Send a `POST` request to:</span></span>

```HTTP
https://api.cognitive.microsofttranslator.com/breaksentence?api-version=3.0
```

## <a name="request-parameters"></a><span data-ttu-id="923af-107">Request parameters</span><span class="sxs-lookup"><span data-stu-id="923af-107">Request parameters</span></span>

<span data-ttu-id="923af-108">Request parameters passed on the query string are:</span><span class="sxs-lookup"><span data-stu-id="923af-108">Request parameters passed on the query string are:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="923af-109">Query parameter</span><span class="sxs-lookup"><span data-stu-id="923af-109">Query parameter</span></span></th>
  <th><span data-ttu-id="923af-110">Description</span><span class="sxs-lookup"><span data-stu-id="923af-110">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="923af-111">api-version</span><span class="sxs-lookup"><span data-stu-id="923af-111">api-version</span></span></td>
    <td><span data-ttu-id="923af-112">*Required query parameter*.</span><span class="sxs-lookup"><span data-stu-id="923af-112">*Required query parameter*.</span></span><br/><span data-ttu-id="923af-113">Version of the API requested by the client.</span><span class="sxs-lookup"><span data-stu-id="923af-113">Version of the API requested by the client.</span></span> <span data-ttu-id="923af-114">Value must be `3.0`.</span><span class="sxs-lookup"><span data-stu-id="923af-114">Value must be `3.0`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-115">language</span><span class="sxs-lookup"><span data-stu-id="923af-115">language</span></span></td>
    <td><span data-ttu-id="923af-116">*Optional query parameter*.</span><span class="sxs-lookup"><span data-stu-id="923af-116">*Optional query parameter*.</span></span><br/><span data-ttu-id="923af-117">Language tag identifying the language of the input text.</span><span class="sxs-lookup"><span data-stu-id="923af-117">Language tag identifying the language of the input text.</span></span> <span data-ttu-id="923af-118">If a code is not specified, automatic language detection will be applied.</span><span class="sxs-lookup"><span data-stu-id="923af-118">If a code is not specified, automatic language detection will be applied.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-119">script</span><span class="sxs-lookup"><span data-stu-id="923af-119">script</span></span></td>
    <td><span data-ttu-id="923af-120">*Optional query parameter*.</span><span class="sxs-lookup"><span data-stu-id="923af-120">*Optional query parameter*.</span></span><br/><span data-ttu-id="923af-121">Script tag identifying the script used by the input text.</span><span class="sxs-lookup"><span data-stu-id="923af-121">Script tag identifying the script used by the input text.</span></span> <span data-ttu-id="923af-122">If a script is not specified, the default script of the language will be assumed.</span><span class="sxs-lookup"><span data-stu-id="923af-122">If a script is not specified, the default script of the language will be assumed.</span></span></td>
  </tr>
</table> 

<span data-ttu-id="923af-123">Request headers include:</span><span class="sxs-lookup"><span data-stu-id="923af-123">Request headers include:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="923af-124">Headers</span><span class="sxs-lookup"><span data-stu-id="923af-124">Headers</span></span></th>
  <th><span data-ttu-id="923af-125">Description</span><span class="sxs-lookup"><span data-stu-id="923af-125">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="923af-126">_One authorization_</span><span class="sxs-lookup"><span data-stu-id="923af-126">_One authorization_</span></span><br/><span data-ttu-id="923af-127">_header_</span><span class="sxs-lookup"><span data-stu-id="923af-127">_header_</span></span></td>
    <td><span data-ttu-id="923af-128">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="923af-128">*Required request header*.</span></span><br/><span data-ttu-id="923af-129">See [available options for authentication](./v3-0-reference.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="923af-129">See [available options for authentication](./v3-0-reference.md#authentication).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-130">Content-Type</span><span class="sxs-lookup"><span data-stu-id="923af-130">Content-Type</span></span></td>
    <td><span data-ttu-id="923af-131">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="923af-131">*Required request header*.</span></span><br/><span data-ttu-id="923af-132">Specifies the content type of the payload.</span><span class="sxs-lookup"><span data-stu-id="923af-132">Specifies the content type of the payload.</span></span> <span data-ttu-id="923af-133">Possible values are: `application/json`.</span><span class="sxs-lookup"><span data-stu-id="923af-133">Possible values are: `application/json`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-134">Content-Length</span><span class="sxs-lookup"><span data-stu-id="923af-134">Content-Length</span></span></td>
    <td><span data-ttu-id="923af-135">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="923af-135">*Required request header*.</span></span><br/><span data-ttu-id="923af-136">The length of the request body.</span><span class="sxs-lookup"><span data-stu-id="923af-136">The length of the request body.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-137">X-ClientTraceId</span><span class="sxs-lookup"><span data-stu-id="923af-137">X-ClientTraceId</span></span></td>
    <td><span data-ttu-id="923af-138">*Optional*.</span><span class="sxs-lookup"><span data-stu-id="923af-138">*Optional*.</span></span><br/><span data-ttu-id="923af-139">A client-generated GUID to uniquely identify the request.</span><span class="sxs-lookup"><span data-stu-id="923af-139">A client-generated GUID to uniquely identify the request.</span></span> <span data-ttu-id="923af-140">Note that you can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="923af-140">Note that you can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="request-body"></a><span data-ttu-id="923af-141">Request body</span><span class="sxs-lookup"><span data-stu-id="923af-141">Request body</span></span>

<span data-ttu-id="923af-142">The body of the request is a JSON array.</span><span class="sxs-lookup"><span data-stu-id="923af-142">The body of the request is a JSON array.</span></span> <span data-ttu-id="923af-143">Each array element is a JSON object with a string property named `Text`.</span><span class="sxs-lookup"><span data-stu-id="923af-143">Each array element is a JSON object with a string property named `Text`.</span></span> <span data-ttu-id="923af-144">Sentence boundaries are computed for the value of the `Text` property.</span><span class="sxs-lookup"><span data-stu-id="923af-144">Sentence boundaries are computed for the value of the `Text` property.</span></span> <span data-ttu-id="923af-145">A sample request body with one piece of text looks like that:</span><span class="sxs-lookup"><span data-stu-id="923af-145">A sample request body with one piece of text looks like that:</span></span>

```json
[
    { "Text": "How are you? I am fine. What did you do today?" }
]
```

<span data-ttu-id="923af-146">The following limitations apply:</span><span class="sxs-lookup"><span data-stu-id="923af-146">The following limitations apply:</span></span>

* <span data-ttu-id="923af-147">The array can have at most 100 elements.</span><span class="sxs-lookup"><span data-stu-id="923af-147">The array can have at most 100 elements.</span></span>
* <span data-ttu-id="923af-148">The text value of an array element cannot exceed 10,000 characters including spaces.</span><span class="sxs-lookup"><span data-stu-id="923af-148">The text value of an array element cannot exceed 10,000 characters including spaces.</span></span>
* <span data-ttu-id="923af-149">The entire text included in the request cannot exceed 50,000 characters including spaces.</span><span class="sxs-lookup"><span data-stu-id="923af-149">The entire text included in the request cannot exceed 50,000 characters including spaces.</span></span>
* <span data-ttu-id="923af-150">If the `language` query parameter is specified, then all array elements must be in the same language.</span><span class="sxs-lookup"><span data-stu-id="923af-150">If the `language` query parameter is specified, then all array elements must be in the same language.</span></span> <span data-ttu-id="923af-151">Otherwise, language auto-detection is applied to each array element independently.</span><span class="sxs-lookup"><span data-stu-id="923af-151">Otherwise, language auto-detection is applied to each array element independently.</span></span>

## <a name="response-body"></a><span data-ttu-id="923af-152">Response body</span><span class="sxs-lookup"><span data-stu-id="923af-152">Response body</span></span>

<span data-ttu-id="923af-153">A successful response is a JSON array with one result for each string in the input array.</span><span class="sxs-lookup"><span data-stu-id="923af-153">A successful response is a JSON array with one result for each string in the input array.</span></span> <span data-ttu-id="923af-154">A result object includes the following properties:</span><span class="sxs-lookup"><span data-stu-id="923af-154">A result object includes the following properties:</span></span>

  * <span data-ttu-id="923af-155">`sentLen`: An array of integers representing the lengths of the sentences in the text element.</span><span class="sxs-lookup"><span data-stu-id="923af-155">`sentLen`: An array of integers representing the lengths of the sentences in the text element.</span></span> <span data-ttu-id="923af-156">The length of the array is the number of sentences, and the values are the length of each sentence.</span><span class="sxs-lookup"><span data-stu-id="923af-156">The length of the array is the number of sentences, and the values are the length of each sentence.</span></span> 

  * <span data-ttu-id="923af-157">`detectedLanguage`: An object describing the detected language through the following properties:</span><span class="sxs-lookup"><span data-stu-id="923af-157">`detectedLanguage`: An object describing the detected language through the following properties:</span></span>

     * <span data-ttu-id="923af-158">`language`: Code of the detected language.</span><span class="sxs-lookup"><span data-stu-id="923af-158">`language`: Code of the detected language.</span></span>

     * <span data-ttu-id="923af-159">`score`: A float value indicating the confidence in the result.</span><span class="sxs-lookup"><span data-stu-id="923af-159">`score`: A float value indicating the confidence in the result.</span></span> <span data-ttu-id="923af-160">The score is between zero and one and a low score indicates a low confidence.</span><span class="sxs-lookup"><span data-stu-id="923af-160">The score is between zero and one and a low score indicates a low confidence.</span></span>
     
    <span data-ttu-id="923af-161">Note that the `detectedLanguage` property is only present in the result object when language auto-detection is requested.</span><span class="sxs-lookup"><span data-stu-id="923af-161">Note that the `detectedLanguage` property is only present in the result object when language auto-detection is requested.</span></span>

<span data-ttu-id="923af-162">An example JSON response is:</span><span class="sxs-lookup"><span data-stu-id="923af-162">An example JSON response is:</span></span>

```json
[
  {
    "sentenceLengths": [ 13, 11, 22 ]
    "detectedLanguage": {
      "language": "en",
      "score": 401
    },
  }
]
```

## <a name="response-headers"></a><span data-ttu-id="923af-163">Response headers</span><span class="sxs-lookup"><span data-stu-id="923af-163">Response headers</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="923af-164">Headers</span><span class="sxs-lookup"><span data-stu-id="923af-164">Headers</span></span></th>
  <th><span data-ttu-id="923af-165">Description</span><span class="sxs-lookup"><span data-stu-id="923af-165">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="923af-166">X-RequestId</span><span class="sxs-lookup"><span data-stu-id="923af-166">X-RequestId</span></span></td>
    <td><span data-ttu-id="923af-167">Value generated by the service to identify the request.</span><span class="sxs-lookup"><span data-stu-id="923af-167">Value generated by the service to identify the request.</span></span> <span data-ttu-id="923af-168">It is used for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="923af-168">It is used for troubleshooting purposes.</span></span></td>
  </tr>
</table> 

## <a name="response-status-codes"></a><span data-ttu-id="923af-169">Response status codes</span><span class="sxs-lookup"><span data-stu-id="923af-169">Response status codes</span></span>

<span data-ttu-id="923af-170">The following are the possible HTTP status codes that a request returns.</span><span class="sxs-lookup"><span data-stu-id="923af-170">The following are the possible HTTP status codes that a request returns.</span></span> 

<table width="100%">
  <th width="20%"><span data-ttu-id="923af-171">Status Code</span><span class="sxs-lookup"><span data-stu-id="923af-171">Status Code</span></span></th>
  <th><span data-ttu-id="923af-172">Description</span><span class="sxs-lookup"><span data-stu-id="923af-172">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="923af-173">200</span><span class="sxs-lookup"><span data-stu-id="923af-173">200</span></span></td>
    <td><span data-ttu-id="923af-174">Success.</span><span class="sxs-lookup"><span data-stu-id="923af-174">Success.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-175">400</span><span class="sxs-lookup"><span data-stu-id="923af-175">400</span></span></td>
    <td><span data-ttu-id="923af-176">One of the query parameters is missing or not valid.</span><span class="sxs-lookup"><span data-stu-id="923af-176">One of the query parameters is missing or not valid.</span></span> <span data-ttu-id="923af-177">Correct request parameters before retrying.</span><span class="sxs-lookup"><span data-stu-id="923af-177">Correct request parameters before retrying.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-178">401</span><span class="sxs-lookup"><span data-stu-id="923af-178">401</span></span></td>
    <td><span data-ttu-id="923af-179">The request could not be authenticated.</span><span class="sxs-lookup"><span data-stu-id="923af-179">The request could not be authenticated.</span></span> <span data-ttu-id="923af-180">Check that credentials are specified and valid.</span><span class="sxs-lookup"><span data-stu-id="923af-180">Check that credentials are specified and valid.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-181">403</span><span class="sxs-lookup"><span data-stu-id="923af-181">403</span></span></td>
    <td><span data-ttu-id="923af-182">The request is not authorized.</span><span class="sxs-lookup"><span data-stu-id="923af-182">The request is not authorized.</span></span> <span data-ttu-id="923af-183">Check the details error message.</span><span class="sxs-lookup"><span data-stu-id="923af-183">Check the details error message.</span></span> <span data-ttu-id="923af-184">This often indicates that all free translations provided with a trial subscription have been used up.</span><span class="sxs-lookup"><span data-stu-id="923af-184">This often indicates that all free translations provided with a trial subscription have been used up.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-185">429</span><span class="sxs-lookup"><span data-stu-id="923af-185">429</span></span></td>
    <td><span data-ttu-id="923af-186">The caller is sending too many requests.</span><span class="sxs-lookup"><span data-stu-id="923af-186">The caller is sending too many requests.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-187">500</span><span class="sxs-lookup"><span data-stu-id="923af-187">500</span></span></td>
    <td><span data-ttu-id="923af-188">An unexpected error occurred.</span><span class="sxs-lookup"><span data-stu-id="923af-188">An unexpected error occurred.</span></span> <span data-ttu-id="923af-189">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="923af-189">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="923af-190">503</span><span class="sxs-lookup"><span data-stu-id="923af-190">503</span></span></td>
    <td><span data-ttu-id="923af-191">Server temporarily unavailable.</span><span class="sxs-lookup"><span data-stu-id="923af-191">Server temporarily unavailable.</span></span> <span data-ttu-id="923af-192">Retry the request.</span><span class="sxs-lookup"><span data-stu-id="923af-192">Retry the request.</span></span> <span data-ttu-id="923af-193">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="923af-193">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="examples"></a><span data-ttu-id="923af-194">Examples</span><span class="sxs-lookup"><span data-stu-id="923af-194">Examples</span></span>

<span data-ttu-id="923af-195">The following example shows how to obtain sentence boundaries for a single sentence.</span><span class="sxs-lookup"><span data-stu-id="923af-195">The following example shows how to obtain sentence boundaries for a single sentence.</span></span> <span data-ttu-id="923af-196">The language of the sentence is automatically detected by the service.</span><span class="sxs-lookup"><span data-stu-id="923af-196">The language of the sentence is automatically detected by the service.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="923af-197">curl</span><span class="sxs-lookup"><span data-stu-id="923af-197">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/breaksentence?api-version=3.0" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'How are you? I am fine. What did you do today?'}]"
```

---

