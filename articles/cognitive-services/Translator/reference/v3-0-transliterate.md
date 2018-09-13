---
title: Microsoft Translator Text API Transliterate Method | Microsoft Docs
description: Use the Microsoft Translator Text API Transliterate method.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: microsoft translator
ms.topic: article
ms.date: 03/29/2018
ms.author: v-jansko
ms.openlocfilehash: fdd6fa9236f0c02685198b6de3228c444993dad6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871550"
---
# <a name="text-api-30-transliterate"></a><span data-ttu-id="f5e61-103">Text API 3.0: Transliterate</span><span class="sxs-lookup"><span data-stu-id="f5e61-103">Text API 3.0: Transliterate</span></span>

<span data-ttu-id="f5e61-104">Converts text in one language from one script to another script.</span><span class="sxs-lookup"><span data-stu-id="f5e61-104">Converts text in one language from one script to another script.</span></span>

## <a name="request-url"></a><span data-ttu-id="f5e61-105">Request URL</span><span class="sxs-lookup"><span data-stu-id="f5e61-105">Request URL</span></span>

<span data-ttu-id="f5e61-106">Send a `POST` request to:</span><span class="sxs-lookup"><span data-stu-id="f5e61-106">Send a `POST` request to:</span></span>

```HTTP
https://api.cognitive.microsofttranslator.com/transliterate?api-version=3.0
```

## <a name="request-parameters"></a><span data-ttu-id="f5e61-107">Request parameters</span><span class="sxs-lookup"><span data-stu-id="f5e61-107">Request parameters</span></span>

<span data-ttu-id="f5e61-108">Request parameters passed on the query string are:</span><span class="sxs-lookup"><span data-stu-id="f5e61-108">Request parameters passed on the query string are:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="f5e61-109">Query parameter</span><span class="sxs-lookup"><span data-stu-id="f5e61-109">Query parameter</span></span></th>
  <th><span data-ttu-id="f5e61-110">Description</span><span class="sxs-lookup"><span data-stu-id="f5e61-110">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="f5e61-111">api-version</span><span class="sxs-lookup"><span data-stu-id="f5e61-111">api-version</span></span></td>
    <td><span data-ttu-id="f5e61-112">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="f5e61-112">*Required parameter*.</span></span><br/><span data-ttu-id="f5e61-113">Version of the API requested by the client.</span><span class="sxs-lookup"><span data-stu-id="f5e61-113">Version of the API requested by the client.</span></span> <span data-ttu-id="f5e61-114">Value must be `3.0`.</span><span class="sxs-lookup"><span data-stu-id="f5e61-114">Value must be `3.0`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-115">language</span><span class="sxs-lookup"><span data-stu-id="f5e61-115">language</span></span></td>
    <td><span data-ttu-id="f5e61-116">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="f5e61-116">*Required parameter*.</span></span><br/><span data-ttu-id="f5e61-117">Specifies the language of the text to convert from one script to another.</span><span class="sxs-lookup"><span data-stu-id="f5e61-117">Specifies the language of the text to convert from one script to another.</span></span> <span data-ttu-id="f5e61-118">Possible languages are listed in the `transliteration` scope obtained by querying the service for its [supported languages](.\v3-0-languages.md).</span><span class="sxs-lookup"><span data-stu-id="f5e61-118">Possible languages are listed in the `transliteration` scope obtained by querying the service for its [supported languages](.\v3-0-languages.md).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-119">fromScript</span><span class="sxs-lookup"><span data-stu-id="f5e61-119">fromScript</span></span></td>
    <td><span data-ttu-id="f5e61-120">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="f5e61-120">*Required parameter*.</span></span><br/><span data-ttu-id="f5e61-121">Specifies the script used by the input text.</span><span class="sxs-lookup"><span data-stu-id="f5e61-121">Specifies the script used by the input text.</span></span> <span data-ttu-id="f5e61-122">Lookup [supported languages](.\v3-0-languages.md) using the `transliteration` scope, to find input scripts available for the selected language.</span><span class="sxs-lookup"><span data-stu-id="f5e61-122">Lookup [supported languages](.\v3-0-languages.md) using the `transliteration` scope, to find input scripts available for the selected language.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-123">toScript</span><span class="sxs-lookup"><span data-stu-id="f5e61-123">toScript</span></span></td>
    <td><span data-ttu-id="f5e61-124">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="f5e61-124">*Required parameter*.</span></span><br/><span data-ttu-id="f5e61-125">Specifies the output script.</span><span class="sxs-lookup"><span data-stu-id="f5e61-125">Specifies the output script.</span></span> <span data-ttu-id="f5e61-126">Lookup [supported languages](.\v3-0-languages.md) using the `transliteration` scope, to find output scripts available for the selected combination of input language and input script.</span><span class="sxs-lookup"><span data-stu-id="f5e61-126">Lookup [supported languages](.\v3-0-languages.md) using the `transliteration` scope, to find output scripts available for the selected combination of input language and input script.</span></span></td>
  </tr>
</table> 

<span data-ttu-id="f5e61-127">Request headers include:</span><span class="sxs-lookup"><span data-stu-id="f5e61-127">Request headers include:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="f5e61-128">Headers</span><span class="sxs-lookup"><span data-stu-id="f5e61-128">Headers</span></span></th>
  <th><span data-ttu-id="f5e61-129">Description</span><span class="sxs-lookup"><span data-stu-id="f5e61-129">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="f5e61-130">_One authorization_</span><span class="sxs-lookup"><span data-stu-id="f5e61-130">_One authorization_</span></span><br/><span data-ttu-id="f5e61-131">_header_</span><span class="sxs-lookup"><span data-stu-id="f5e61-131">_header_</span></span></td>
    <td><span data-ttu-id="f5e61-132">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="f5e61-132">*Required request header*.</span></span><br/><span data-ttu-id="f5e61-133">See [available options for authentication](./v3-0-reference.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="f5e61-133">See [available options for authentication](./v3-0-reference.md#authentication).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-134">Content-Type</span><span class="sxs-lookup"><span data-stu-id="f5e61-134">Content-Type</span></span></td>
    <td><span data-ttu-id="f5e61-135">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="f5e61-135">*Required request header*.</span></span><br/><span data-ttu-id="f5e61-136">Specifies the content type of the payload.</span><span class="sxs-lookup"><span data-stu-id="f5e61-136">Specifies the content type of the payload.</span></span> <span data-ttu-id="f5e61-137">Possible values are: `application/json`.</span><span class="sxs-lookup"><span data-stu-id="f5e61-137">Possible values are: `application/json`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-138">Content-Length</span><span class="sxs-lookup"><span data-stu-id="f5e61-138">Content-Length</span></span></td>
    <td><span data-ttu-id="f5e61-139">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="f5e61-139">*Required request header*.</span></span><br/><span data-ttu-id="f5e61-140">The length of the request body.</span><span class="sxs-lookup"><span data-stu-id="f5e61-140">The length of the request body.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-141">X-ClientTraceId</span><span class="sxs-lookup"><span data-stu-id="f5e61-141">X-ClientTraceId</span></span></td>
    <td><span data-ttu-id="f5e61-142">*Optional*.</span><span class="sxs-lookup"><span data-stu-id="f5e61-142">*Optional*.</span></span><br/><span data-ttu-id="f5e61-143">A client-generated GUID to uniquely identify the request.</span><span class="sxs-lookup"><span data-stu-id="f5e61-143">A client-generated GUID to uniquely identify the request.</span></span> <span data-ttu-id="f5e61-144">Note that you can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="f5e61-144">Note that you can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="request-body"></a><span data-ttu-id="f5e61-145">Request body</span><span class="sxs-lookup"><span data-stu-id="f5e61-145">Request body</span></span>

<span data-ttu-id="f5e61-146">The body of the request is a JSON array.</span><span class="sxs-lookup"><span data-stu-id="f5e61-146">The body of the request is a JSON array.</span></span> <span data-ttu-id="f5e61-147">Each array element is a JSON object with a string property named `Text`, which represents the string to convert.</span><span class="sxs-lookup"><span data-stu-id="f5e61-147">Each array element is a JSON object with a string property named `Text`, which represents the string to convert.</span></span>

```json
[
    {"Text":"こんにちは"},
    {"Text":"さようなら"}
]
```

<span data-ttu-id="f5e61-148">The following limitations apply:</span><span class="sxs-lookup"><span data-stu-id="f5e61-148">The following limitations apply:</span></span>

* <span data-ttu-id="f5e61-149">The array can have at most 10 elements.</span><span class="sxs-lookup"><span data-stu-id="f5e61-149">The array can have at most 10 elements.</span></span>
* <span data-ttu-id="f5e61-150">The text value of an array element cannot exceed 1,000 characters including spaces.</span><span class="sxs-lookup"><span data-stu-id="f5e61-150">The text value of an array element cannot exceed 1,000 characters including spaces.</span></span>
* <span data-ttu-id="f5e61-151">The entire text included in the request cannot exceed 5,000 characters including spaces.</span><span class="sxs-lookup"><span data-stu-id="f5e61-151">The entire text included in the request cannot exceed 5,000 characters including spaces.</span></span>

## <a name="response-body"></a><span data-ttu-id="f5e61-152">Response body</span><span class="sxs-lookup"><span data-stu-id="f5e61-152">Response body</span></span>

<span data-ttu-id="f5e61-153">A successful response is a JSON array with one result for each element in the input array.</span><span class="sxs-lookup"><span data-stu-id="f5e61-153">A successful response is a JSON array with one result for each element in the input array.</span></span> <span data-ttu-id="f5e61-154">A result object includes the following properties:</span><span class="sxs-lookup"><span data-stu-id="f5e61-154">A result object includes the following properties:</span></span>

  * <span data-ttu-id="f5e61-155">`text`: A string which is the result of converting the input string to the output script.</span><span class="sxs-lookup"><span data-stu-id="f5e61-155">`text`: A string which is the result of converting the input string to the output script.</span></span>
  
  * <span data-ttu-id="f5e61-156">`script`: A string specifying the script used in the output.</span><span class="sxs-lookup"><span data-stu-id="f5e61-156">`script`: A string specifying the script used in the output.</span></span>

<span data-ttu-id="f5e61-157">An example JSON response is:</span><span class="sxs-lookup"><span data-stu-id="f5e61-157">An example JSON response is:</span></span>

```json
[
    {"text":"konnnichiha","script":"Latn"},
    {"text":"sayounara","script":"Latn"}
]
```

## <a name="response-headers"></a><span data-ttu-id="f5e61-158">Response headers</span><span class="sxs-lookup"><span data-stu-id="f5e61-158">Response headers</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="f5e61-159">Headers</span><span class="sxs-lookup"><span data-stu-id="f5e61-159">Headers</span></span></th>
  <th><span data-ttu-id="f5e61-160">Description</span><span class="sxs-lookup"><span data-stu-id="f5e61-160">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="f5e61-161">X-RequestId</span><span class="sxs-lookup"><span data-stu-id="f5e61-161">X-RequestId</span></span></td>
    <td><span data-ttu-id="f5e61-162">Value generated by the service to identify the request.</span><span class="sxs-lookup"><span data-stu-id="f5e61-162">Value generated by the service to identify the request.</span></span> <span data-ttu-id="f5e61-163">It is used for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="f5e61-163">It is used for troubleshooting purposes.</span></span></td>
  </tr>
</table> 

## <a name="response-status-codes"></a><span data-ttu-id="f5e61-164">Response status codes</span><span class="sxs-lookup"><span data-stu-id="f5e61-164">Response status codes</span></span>

<span data-ttu-id="f5e61-165">The following are the possible HTTP status codes that a request returns.</span><span class="sxs-lookup"><span data-stu-id="f5e61-165">The following are the possible HTTP status codes that a request returns.</span></span> 

<table width="100%">
  <th width="20%"><span data-ttu-id="f5e61-166">Status Code</span><span class="sxs-lookup"><span data-stu-id="f5e61-166">Status Code</span></span></th>
  <th><span data-ttu-id="f5e61-167">Description</span><span class="sxs-lookup"><span data-stu-id="f5e61-167">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="f5e61-168">200</span><span class="sxs-lookup"><span data-stu-id="f5e61-168">200</span></span></td>
    <td><span data-ttu-id="f5e61-169">Success.</span><span class="sxs-lookup"><span data-stu-id="f5e61-169">Success.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-170">400</span><span class="sxs-lookup"><span data-stu-id="f5e61-170">400</span></span></td>
    <td><span data-ttu-id="f5e61-171">One of the query parameters is missing or not valid.</span><span class="sxs-lookup"><span data-stu-id="f5e61-171">One of the query parameters is missing or not valid.</span></span> <span data-ttu-id="f5e61-172">Correct request parameters before retrying.</span><span class="sxs-lookup"><span data-stu-id="f5e61-172">Correct request parameters before retrying.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-173">401</span><span class="sxs-lookup"><span data-stu-id="f5e61-173">401</span></span></td>
    <td><span data-ttu-id="f5e61-174">The request could not be authenticated.</span><span class="sxs-lookup"><span data-stu-id="f5e61-174">The request could not be authenticated.</span></span> <span data-ttu-id="f5e61-175">Check that credentials are specified and valid.</span><span class="sxs-lookup"><span data-stu-id="f5e61-175">Check that credentials are specified and valid.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-176">403</span><span class="sxs-lookup"><span data-stu-id="f5e61-176">403</span></span></td>
    <td><span data-ttu-id="f5e61-177">The request is not authorized.</span><span class="sxs-lookup"><span data-stu-id="f5e61-177">The request is not authorized.</span></span> <span data-ttu-id="f5e61-178">Check the details error message.</span><span class="sxs-lookup"><span data-stu-id="f5e61-178">Check the details error message.</span></span> <span data-ttu-id="f5e61-179">This often indicates that all free translations provided with a trial subscription have been used up.</span><span class="sxs-lookup"><span data-stu-id="f5e61-179">This often indicates that all free translations provided with a trial subscription have been used up.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-180">429</span><span class="sxs-lookup"><span data-stu-id="f5e61-180">429</span></span></td>
    <td><span data-ttu-id="f5e61-181">The caller is sending too many requests.</span><span class="sxs-lookup"><span data-stu-id="f5e61-181">The caller is sending too many requests.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-182">500</span><span class="sxs-lookup"><span data-stu-id="f5e61-182">500</span></span></td>
    <td><span data-ttu-id="f5e61-183">An unexpected error occurred.</span><span class="sxs-lookup"><span data-stu-id="f5e61-183">An unexpected error occurred.</span></span> <span data-ttu-id="f5e61-184">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="f5e61-184">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f5e61-185">503</span><span class="sxs-lookup"><span data-stu-id="f5e61-185">503</span></span></td>
    <td><span data-ttu-id="f5e61-186">Server temporarily unavailable.</span><span class="sxs-lookup"><span data-stu-id="f5e61-186">Server temporarily unavailable.</span></span> <span data-ttu-id="f5e61-187">Retry the request.</span><span class="sxs-lookup"><span data-stu-id="f5e61-187">Retry the request.</span></span> <span data-ttu-id="f5e61-188">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="f5e61-188">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="examples"></a><span data-ttu-id="f5e61-189">Examples</span><span class="sxs-lookup"><span data-stu-id="f5e61-189">Examples</span></span>

<span data-ttu-id="f5e61-190">The following example shows how to convert two Japanese strings into Romanized Japanese.</span><span class="sxs-lookup"><span data-stu-id="f5e61-190">The following example shows how to convert two Japanese strings into Romanized Japanese.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="f5e61-191">curl</span><span class="sxs-lookup"><span data-stu-id="f5e61-191">curl</span></span>](#tab/curl)

<span data-ttu-id="f5e61-192">The JSON payload for the request in this example:</span><span class="sxs-lookup"><span data-stu-id="f5e61-192">The JSON payload for the request in this example:</span></span>

```
[{"text":"こんにちは","script":"jpan"},{"text":"さようなら","script":"jpan"}]
```

<span data-ttu-id="f5e61-193">If you are using cUrl in a command-line window that does not support Unicode characters, take the following JSON payload and save it into a file named `request.txt`.</span><span class="sxs-lookup"><span data-stu-id="f5e61-193">If you are using cUrl in a command-line window that does not support Unicode characters, take the following JSON payload and save it into a file named `request.txt`.</span></span> <span data-ttu-id="f5e61-194">Be sure to save the file with `UTF-8` encoding.</span><span class="sxs-lookup"><span data-stu-id="f5e61-194">Be sure to save the file with `UTF-8` encoding.</span></span>

```
curl -X POST "https://api.cognitive.microsofttranslator.com/transliterate?api-version=3.0&language=ja&fromScript=Jpan&toScript=Latn" -H "X-ClientTraceId: 875030C7-5380-40B8-8A03-63DACCF69C11" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d @request.txt
```

---
