---
title: Microsoft Translator Text API Detect Method | Microsoft Docs
description: Use the Microsoft Translator Text API Detect method.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: microsoft translator
ms.topic: article
ms.date: 03/29/2018
ms.author: v-jansko
ms.openlocfilehash: 7e81e91230e1ada4423d77d22134b1b64df65d9d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866931"
---
# <a name="text-api-30-detect"></a><span data-ttu-id="5700c-103">Text API 3.0: Detect</span><span class="sxs-lookup"><span data-stu-id="5700c-103">Text API 3.0: Detect</span></span>

<span data-ttu-id="5700c-104">Identifies the language of a piece of text.</span><span class="sxs-lookup"><span data-stu-id="5700c-104">Identifies the language of a piece of text.</span></span>

## <a name="request-url"></a><span data-ttu-id="5700c-105">Request URL</span><span class="sxs-lookup"><span data-stu-id="5700c-105">Request URL</span></span>

<span data-ttu-id="5700c-106">Send a `POST` request to:</span><span class="sxs-lookup"><span data-stu-id="5700c-106">Send a `POST` request to:</span></span>

```HTTP
https://api.cognitive.microsofttranslator.com/detect?api-version=3.0
```

## <a name="request-parameters"></a><span data-ttu-id="5700c-107">Request parameters</span><span class="sxs-lookup"><span data-stu-id="5700c-107">Request parameters</span></span>

<span data-ttu-id="5700c-108">Request parameters passed on the query string are:</span><span class="sxs-lookup"><span data-stu-id="5700c-108">Request parameters passed on the query string are:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="5700c-109">Query parameter</span><span class="sxs-lookup"><span data-stu-id="5700c-109">Query parameter</span></span></th>
  <th><span data-ttu-id="5700c-110">Description</span><span class="sxs-lookup"><span data-stu-id="5700c-110">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="5700c-111">api-version</span><span class="sxs-lookup"><span data-stu-id="5700c-111">api-version</span></span></td>
    <td><span data-ttu-id="5700c-112">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="5700c-112">*Required parameter*.</span></span><br/><span data-ttu-id="5700c-113">Version of the API requested by the client.</span><span class="sxs-lookup"><span data-stu-id="5700c-113">Version of the API requested by the client.</span></span> <span data-ttu-id="5700c-114">Value must be `3.0`.</span><span class="sxs-lookup"><span data-stu-id="5700c-114">Value must be `3.0`.</span></span></td>
  </tr>
</table> 

<span data-ttu-id="5700c-115">Request headers include:</span><span class="sxs-lookup"><span data-stu-id="5700c-115">Request headers include:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="5700c-116">Headers</span><span class="sxs-lookup"><span data-stu-id="5700c-116">Headers</span></span></th>
  <th><span data-ttu-id="5700c-117">Description</span><span class="sxs-lookup"><span data-stu-id="5700c-117">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="5700c-118">_One authorization_</span><span class="sxs-lookup"><span data-stu-id="5700c-118">_One authorization_</span></span><br/><span data-ttu-id="5700c-119">_header_</span><span class="sxs-lookup"><span data-stu-id="5700c-119">_header_</span></span></td>
    <td><span data-ttu-id="5700c-120">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="5700c-120">*Required request header*.</span></span><br/><span data-ttu-id="5700c-121">See [available options for authentication](./v3-0-reference.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="5700c-121">See [available options for authentication](./v3-0-reference.md#authentication).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5700c-122">Content-Type</span><span class="sxs-lookup"><span data-stu-id="5700c-122">Content-Type</span></span></td>
    <td><span data-ttu-id="5700c-123">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="5700c-123">*Required request header*.</span></span><br/><span data-ttu-id="5700c-124">Specifies the content type of the payload.</span><span class="sxs-lookup"><span data-stu-id="5700c-124">Specifies the content type of the payload.</span></span> <span data-ttu-id="5700c-125">Possible values are: `application/json`.</span><span class="sxs-lookup"><span data-stu-id="5700c-125">Possible values are: `application/json`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5700c-126">Content-Length</span><span class="sxs-lookup"><span data-stu-id="5700c-126">Content-Length</span></span></td>
    <td><span data-ttu-id="5700c-127">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="5700c-127">*Required request header*.</span></span><br/><span data-ttu-id="5700c-128">The length of the request body.</span><span class="sxs-lookup"><span data-stu-id="5700c-128">The length of the request body.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5700c-129">X-ClientTraceId</span><span class="sxs-lookup"><span data-stu-id="5700c-129">X-ClientTraceId</span></span></td>
    <td><span data-ttu-id="5700c-130">*Optional*.</span><span class="sxs-lookup"><span data-stu-id="5700c-130">*Optional*.</span></span><br/><span data-ttu-id="5700c-131">A client-generated GUID to uniquely identify the request.</span><span class="sxs-lookup"><span data-stu-id="5700c-131">A client-generated GUID to uniquely identify the request.</span></span> <span data-ttu-id="5700c-132">Note that you can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="5700c-132">Note that you can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="request-body"></a><span data-ttu-id="5700c-133">Request body</span><span class="sxs-lookup"><span data-stu-id="5700c-133">Request body</span></span>

<span data-ttu-id="5700c-134">The body of the request is a JSON array.</span><span class="sxs-lookup"><span data-stu-id="5700c-134">The body of the request is a JSON array.</span></span> <span data-ttu-id="5700c-135">Each array element is a JSON object with a string property named `Text`.</span><span class="sxs-lookup"><span data-stu-id="5700c-135">Each array element is a JSON object with a string property named `Text`.</span></span> <span data-ttu-id="5700c-136">Language detection is applied to the value of the `Text` property.</span><span class="sxs-lookup"><span data-stu-id="5700c-136">Language detection is applied to the value of the `Text` property.</span></span> <span data-ttu-id="5700c-137">A sample request body looks like that:</span><span class="sxs-lookup"><span data-stu-id="5700c-137">A sample request body looks like that:</span></span>

```json
[
    { "Text": "Ich würde wirklich gern Ihr Auto um den Block fahren ein paar Mal." }
]
```

<span data-ttu-id="5700c-138">The following limitations apply:</span><span class="sxs-lookup"><span data-stu-id="5700c-138">The following limitations apply:</span></span>

* <span data-ttu-id="5700c-139">The array can have at most 100 elements.</span><span class="sxs-lookup"><span data-stu-id="5700c-139">The array can have at most 100 elements.</span></span>
* <span data-ttu-id="5700c-140">The text value of an array element cannot exceed 10,000 characters including spaces.</span><span class="sxs-lookup"><span data-stu-id="5700c-140">The text value of an array element cannot exceed 10,000 characters including spaces.</span></span>
* <span data-ttu-id="5700c-141">The entire text included in the request cannot exceed 50,000 characters including spaces.</span><span class="sxs-lookup"><span data-stu-id="5700c-141">The entire text included in the request cannot exceed 50,000 characters including spaces.</span></span>

## <a name="response-body"></a><span data-ttu-id="5700c-142">Response body</span><span class="sxs-lookup"><span data-stu-id="5700c-142">Response body</span></span>

<span data-ttu-id="5700c-143">A successful response is a JSON array with one result for each string in the input array.</span><span class="sxs-lookup"><span data-stu-id="5700c-143">A successful response is a JSON array with one result for each string in the input array.</span></span> <span data-ttu-id="5700c-144">A result object includes the following properties:</span><span class="sxs-lookup"><span data-stu-id="5700c-144">A result object includes the following properties:</span></span>

  * <span data-ttu-id="5700c-145">`language`: Code of the detected language.</span><span class="sxs-lookup"><span data-stu-id="5700c-145">`language`: Code of the detected language.</span></span>

  * <span data-ttu-id="5700c-146">`score`: A float value indicating the confidence in the result.</span><span class="sxs-lookup"><span data-stu-id="5700c-146">`score`: A float value indicating the confidence in the result.</span></span> <span data-ttu-id="5700c-147">The score is between zero and one and a low score indicates a low confidence.</span><span class="sxs-lookup"><span data-stu-id="5700c-147">The score is between zero and one and a low score indicates a low confidence.</span></span>

  * <span data-ttu-id="5700c-148">`isTranslationSupported`: A boolean value which is true if the detected language is one of the languages supported for text translation.</span><span class="sxs-lookup"><span data-stu-id="5700c-148">`isTranslationSupported`: A boolean value which is true if the detected language is one of the languages supported for text translation.</span></span>

  * <span data-ttu-id="5700c-149">`isTransliterationSupported`: A boolean value which is true if the detected language is one of the languages supported for transliteration.</span><span class="sxs-lookup"><span data-stu-id="5700c-149">`isTransliterationSupported`: A boolean value which is true if the detected language is one of the languages supported for transliteration.</span></span>
  
  * <span data-ttu-id="5700c-150">`alternatives`: An array of other possible languages.</span><span class="sxs-lookup"><span data-stu-id="5700c-150">`alternatives`: An array of other possible languages.</span></span> <span data-ttu-id="5700c-151">Each element of the array is another object with the same properties listed above: `language`, `score`, `isTranslationSupported` and `isTransliterationSupported`.</span><span class="sxs-lookup"><span data-stu-id="5700c-151">Each element of the array is another object with the same properties listed above: `language`, `score`, `isTranslationSupported` and `isTransliterationSupported`.</span></span>

<span data-ttu-id="5700c-152">An example JSON response is:</span><span class="sxs-lookup"><span data-stu-id="5700c-152">An example JSON response is:</span></span>

```json
[
  {
    "language": "de",
    "score": 0.92,
    "isTranslationSupported": true,
    "isTransliterationSupported": false,
    "alternatives": [
      {
        "language": "pt",
        "score": 0.23,
        "isTranslationSupported": true,
        "isTransliterationSupported": false
      },
      {
        "language": "sk",
        "score": 0.23,
        "isTranslationSupported": true,
        "isTransliterationSupported": false
      }
    ]
  }
]
```

## <a name="response-headers"></a><span data-ttu-id="5700c-153">Response headers</span><span class="sxs-lookup"><span data-stu-id="5700c-153">Response headers</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="5700c-154">Headers</span><span class="sxs-lookup"><span data-stu-id="5700c-154">Headers</span></span></th>
  <th><span data-ttu-id="5700c-155">Description</span><span class="sxs-lookup"><span data-stu-id="5700c-155">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="5700c-156">X-RequestId</span><span class="sxs-lookup"><span data-stu-id="5700c-156">X-RequestId</span></span></td>
    <td><span data-ttu-id="5700c-157">Value generated by the service to identify the request.</span><span class="sxs-lookup"><span data-stu-id="5700c-157">Value generated by the service to identify the request.</span></span> <span data-ttu-id="5700c-158">It is used for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="5700c-158">It is used for troubleshooting purposes.</span></span></td>
  </tr>
</table> 

## <a name="response-status-codes"></a><span data-ttu-id="5700c-159">Response status codes</span><span class="sxs-lookup"><span data-stu-id="5700c-159">Response status codes</span></span>

<span data-ttu-id="5700c-160">The following are the possible HTTP status codes that a request returns.</span><span class="sxs-lookup"><span data-stu-id="5700c-160">The following are the possible HTTP status codes that a request returns.</span></span> 

<table width="100%">
  <th width="20%"><span data-ttu-id="5700c-161">Status Code</span><span class="sxs-lookup"><span data-stu-id="5700c-161">Status Code</span></span></th>
  <th><span data-ttu-id="5700c-162">Description</span><span class="sxs-lookup"><span data-stu-id="5700c-162">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="5700c-163">200</span><span class="sxs-lookup"><span data-stu-id="5700c-163">200</span></span></td>
    <td><span data-ttu-id="5700c-164">Success.</span><span class="sxs-lookup"><span data-stu-id="5700c-164">Success.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5700c-165">400</span><span class="sxs-lookup"><span data-stu-id="5700c-165">400</span></span></td>
    <td><span data-ttu-id="5700c-166">One of the query parameters is missing or not valid.</span><span class="sxs-lookup"><span data-stu-id="5700c-166">One of the query parameters is missing or not valid.</span></span> <span data-ttu-id="5700c-167">Correct request parameters before retrying.</span><span class="sxs-lookup"><span data-stu-id="5700c-167">Correct request parameters before retrying.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5700c-168">401</span><span class="sxs-lookup"><span data-stu-id="5700c-168">401</span></span></td>
    <td><span data-ttu-id="5700c-169">The request could not be authenticated.</span><span class="sxs-lookup"><span data-stu-id="5700c-169">The request could not be authenticated.</span></span> <span data-ttu-id="5700c-170">Check that credentials are specified and valid.</span><span class="sxs-lookup"><span data-stu-id="5700c-170">Check that credentials are specified and valid.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5700c-171">403</span><span class="sxs-lookup"><span data-stu-id="5700c-171">403</span></span></td>
    <td><span data-ttu-id="5700c-172">The request is not authorized.</span><span class="sxs-lookup"><span data-stu-id="5700c-172">The request is not authorized.</span></span> <span data-ttu-id="5700c-173">Check the details error message.</span><span class="sxs-lookup"><span data-stu-id="5700c-173">Check the details error message.</span></span> <span data-ttu-id="5700c-174">This often indicates that all free translations provided with a trial subscription have been used up.</span><span class="sxs-lookup"><span data-stu-id="5700c-174">This often indicates that all free translations provided with a trial subscription have been used up.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5700c-175">429</span><span class="sxs-lookup"><span data-stu-id="5700c-175">429</span></span></td>
    <td><span data-ttu-id="5700c-176">The caller is sending too many requests.</span><span class="sxs-lookup"><span data-stu-id="5700c-176">The caller is sending too many requests.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5700c-177">500</span><span class="sxs-lookup"><span data-stu-id="5700c-177">500</span></span></td>
    <td><span data-ttu-id="5700c-178">An unexpected error occurred.</span><span class="sxs-lookup"><span data-stu-id="5700c-178">An unexpected error occurred.</span></span> <span data-ttu-id="5700c-179">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="5700c-179">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="5700c-180">503</span><span class="sxs-lookup"><span data-stu-id="5700c-180">503</span></span></td>
    <td><span data-ttu-id="5700c-181">Server temporarily unavailable.</span><span class="sxs-lookup"><span data-stu-id="5700c-181">Server temporarily unavailable.</span></span> <span data-ttu-id="5700c-182">Retry the request.</span><span class="sxs-lookup"><span data-stu-id="5700c-182">Retry the request.</span></span> <span data-ttu-id="5700c-183">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="5700c-183">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="examples"></a><span data-ttu-id="5700c-184">Examples</span><span class="sxs-lookup"><span data-stu-id="5700c-184">Examples</span></span>

<span data-ttu-id="5700c-185">The following example shows how to retrieve languages supported for text translation.</span><span class="sxs-lookup"><span data-stu-id="5700c-185">The following example shows how to retrieve languages supported for text translation.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="5700c-186">curl</span><span class="sxs-lookup"><span data-stu-id="5700c-186">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/detect?api-version=3.0" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'What language is this text written in?'}]"
```

---
