---
title: Microsoft Translator Text API Dictionary Examples Method | Microsoft Docs
description: Use the Microsoft Translator Text API Dictionary Examples method.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: microsoft translator
ms.topic: article
ms.date: 03/29/2018
ms.author: v-jansko
ms.openlocfilehash: 9960f3be42090edaec1df935d70e4c1a0d25b691
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866933"
---
# <a name="text-api-30-dictionary-examples"></a><span data-ttu-id="b843f-103">Text API 3.0: Dictionary Examples</span><span class="sxs-lookup"><span data-stu-id="b843f-103">Text API 3.0: Dictionary Examples</span></span>

<span data-ttu-id="b843f-104">Provides examples that show how terms in the dictionary are used in context.</span><span class="sxs-lookup"><span data-stu-id="b843f-104">Provides examples that show how terms in the dictionary are used in context.</span></span> <span data-ttu-id="b843f-105">This operation is used in tandem with [Dictionary lookup](.\v3-0-dictionary-lookup.md).</span><span class="sxs-lookup"><span data-stu-id="b843f-105">This operation is used in tandem with [Dictionary lookup](.\v3-0-dictionary-lookup.md).</span></span>

## <a name="request-url"></a><span data-ttu-id="b843f-106">Request URL</span><span class="sxs-lookup"><span data-stu-id="b843f-106">Request URL</span></span>

<span data-ttu-id="b843f-107">Send a `POST` request to:</span><span class="sxs-lookup"><span data-stu-id="b843f-107">Send a `POST` request to:</span></span>

```HTTP
https://api.cognitive.microsofttranslator.com/dictionary/examples?api-version=3.0
```

## <a name="request-parameters"></a><span data-ttu-id="b843f-108">Request parameters</span><span class="sxs-lookup"><span data-stu-id="b843f-108">Request parameters</span></span>

<span data-ttu-id="b843f-109">Request parameters passed on the query string are:</span><span class="sxs-lookup"><span data-stu-id="b843f-109">Request parameters passed on the query string are:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="b843f-110">Query parameter</span><span class="sxs-lookup"><span data-stu-id="b843f-110">Query parameter</span></span></th>
  <th><span data-ttu-id="b843f-111">Description</span><span class="sxs-lookup"><span data-stu-id="b843f-111">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="b843f-112">api-version</span><span class="sxs-lookup"><span data-stu-id="b843f-112">api-version</span></span></td>
    <td><span data-ttu-id="b843f-113">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="b843f-113">*Required parameter*.</span></span><br/><span data-ttu-id="b843f-114">Version of the API requested by the client.</span><span class="sxs-lookup"><span data-stu-id="b843f-114">Version of the API requested by the client.</span></span> <span data-ttu-id="b843f-115">Value must be `3.0`.</span><span class="sxs-lookup"><span data-stu-id="b843f-115">Value must be `3.0`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b843f-116">from</span><span class="sxs-lookup"><span data-stu-id="b843f-116">from</span></span></td>
    <td><span data-ttu-id="b843f-117">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="b843f-117">*Required parameter*.</span></span><br/><span data-ttu-id="b843f-118">Specifies the language of the input text.</span><span class="sxs-lookup"><span data-stu-id="b843f-118">Specifies the language of the input text.</span></span> <span data-ttu-id="b843f-119">The source language must be one of the [supported languages](.\v3-0-languages.md) included in the `dictionary` scope.</span><span class="sxs-lookup"><span data-stu-id="b843f-119">The source language must be one of the [supported languages](.\v3-0-languages.md) included in the `dictionary` scope.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b843f-120">to</span><span class="sxs-lookup"><span data-stu-id="b843f-120">to</span></span></td>
    <td><span data-ttu-id="b843f-121">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="b843f-121">*Required parameter*.</span></span><br/><span data-ttu-id="b843f-122">Specifies the language of the output text.</span><span class="sxs-lookup"><span data-stu-id="b843f-122">Specifies the language of the output text.</span></span> <span data-ttu-id="b843f-123">The target language must be one of the [supported languages](.\v3-0-languages.md) included in the `dictionary` scope.</span><span class="sxs-lookup"><span data-stu-id="b843f-123">The target language must be one of the [supported languages](.\v3-0-languages.md) included in the `dictionary` scope.</span></span></td>
  </tr>
</table>

<span data-ttu-id="b843f-124">Request headers include:</span><span class="sxs-lookup"><span data-stu-id="b843f-124">Request headers include:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="b843f-125">Headers</span><span class="sxs-lookup"><span data-stu-id="b843f-125">Headers</span></span></th>
  <th><span data-ttu-id="b843f-126">Description</span><span class="sxs-lookup"><span data-stu-id="b843f-126">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="b843f-127">_One authorization_</span><span class="sxs-lookup"><span data-stu-id="b843f-127">_One authorization_</span></span><br/><span data-ttu-id="b843f-128">_header_</span><span class="sxs-lookup"><span data-stu-id="b843f-128">_header_</span></span></td>
    <td><span data-ttu-id="b843f-129">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="b843f-129">*Required request header*.</span></span><br/><span data-ttu-id="b843f-130">See [available options for authentication](./v3-0-reference.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="b843f-130">See [available options for authentication](./v3-0-reference.md#authentication).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b843f-131">Content-Type</span><span class="sxs-lookup"><span data-stu-id="b843f-131">Content-Type</span></span></td>
    <td><span data-ttu-id="b843f-132">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="b843f-132">*Required request header*.</span></span><br/><span data-ttu-id="b843f-133">Specifies the content type of the payload.</span><span class="sxs-lookup"><span data-stu-id="b843f-133">Specifies the content type of the payload.</span></span> <span data-ttu-id="b843f-134">Possible values are: `application/json`.</span><span class="sxs-lookup"><span data-stu-id="b843f-134">Possible values are: `application/json`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b843f-135">Content-Length</span><span class="sxs-lookup"><span data-stu-id="b843f-135">Content-Length</span></span></td>
    <td><span data-ttu-id="b843f-136">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="b843f-136">*Required request header*.</span></span><br/><span data-ttu-id="b843f-137">The length of the request body.</span><span class="sxs-lookup"><span data-stu-id="b843f-137">The length of the request body.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="b843f-138">X-ClientTraceId</span><span class="sxs-lookup"><span data-stu-id="b843f-138">X-ClientTraceId</span></span></td>
    <td><span data-ttu-id="b843f-139">*Optional*.</span><span class="sxs-lookup"><span data-stu-id="b843f-139">*Optional*.</span></span><br/><span data-ttu-id="b843f-140">A client-generated GUID to uniquely identify the request.</span><span class="sxs-lookup"><span data-stu-id="b843f-140">A client-generated GUID to uniquely identify the request.</span></span> <span data-ttu-id="b843f-141">You can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="b843f-141">You can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="request-body"></a><span data-ttu-id="b843f-142">Request body</span><span class="sxs-lookup"><span data-stu-id="b843f-142">Request body</span></span>

<span data-ttu-id="b843f-143">The body of the request is a JSON array.</span><span class="sxs-lookup"><span data-stu-id="b843f-143">The body of the request is a JSON array.</span></span> <span data-ttu-id="b843f-144">Each array element is a JSON object with the following properties:</span><span class="sxs-lookup"><span data-stu-id="b843f-144">Each array element is a JSON object with the following properties:</span></span>

  * <span data-ttu-id="b843f-145">`Text`: A string specifying the term to lookup.</span><span class="sxs-lookup"><span data-stu-id="b843f-145">`Text`: A string specifying the term to lookup.</span></span> <span data-ttu-id="b843f-146">This should be the value of a `normalizedText` field from the back-translations of a previous [Dictionary lookup](.\v3-0-dictionary-lookup.md) request.</span><span class="sxs-lookup"><span data-stu-id="b843f-146">This should be the value of a `normalizedText` field from the back-translations of a previous [Dictionary lookup](.\v3-0-dictionary-lookup.md) request.</span></span> <span data-ttu-id="b843f-147">It can also be the value of the `normalizedSource` field.</span><span class="sxs-lookup"><span data-stu-id="b843f-147">It can also be the value of the `normalizedSource` field.</span></span>

  * <span data-ttu-id="b843f-148">`Translation`: A string specifying the translated text previously returned by the [Dictionary lookup](.\v3-0-dictionary-lookup.md) operation.</span><span class="sxs-lookup"><span data-stu-id="b843f-148">`Translation`: A string specifying the translated text previously returned by the [Dictionary lookup](.\v3-0-dictionary-lookup.md) operation.</span></span> <span data-ttu-id="b843f-149">This should be the value from the `normalizedTarget` field in the `translations` list of the [Dictionary lookup](.\v3-0-dictionary-lookup.md) response.</span><span class="sxs-lookup"><span data-stu-id="b843f-149">This should be the value from the `normalizedTarget` field in the `translations` list of the [Dictionary lookup](.\v3-0-dictionary-lookup.md) response.</span></span> <span data-ttu-id="b843f-150">The service will return examples for the specific source-target word-pair.</span><span class="sxs-lookup"><span data-stu-id="b843f-150">The service will return examples for the specific source-target word-pair.</span></span>

<span data-ttu-id="b843f-151">An example is:</span><span class="sxs-lookup"><span data-stu-id="b843f-151">An example is:</span></span>

```json
[
    {"Text":"fly", "Translation":"volar"}
]
```

<span data-ttu-id="b843f-152">The following limitations apply:</span><span class="sxs-lookup"><span data-stu-id="b843f-152">The following limitations apply:</span></span>

* <span data-ttu-id="b843f-153">The array can have at most 10 elements.</span><span class="sxs-lookup"><span data-stu-id="b843f-153">The array can have at most 10 elements.</span></span>
* <span data-ttu-id="b843f-154">The text value of an array element cannot exceed 100 characters including spaces.</span><span class="sxs-lookup"><span data-stu-id="b843f-154">The text value of an array element cannot exceed 100 characters including spaces.</span></span>

## <a name="response-body"></a><span data-ttu-id="b843f-155">Response body</span><span class="sxs-lookup"><span data-stu-id="b843f-155">Response body</span></span>

<span data-ttu-id="b843f-156">A successful response is a JSON array with one result for each string in the input array.</span><span class="sxs-lookup"><span data-stu-id="b843f-156">A successful response is a JSON array with one result for each string in the input array.</span></span> <span data-ttu-id="b843f-157">A result object includes the following properties:</span><span class="sxs-lookup"><span data-stu-id="b843f-157">A result object includes the following properties:</span></span>

  * <span data-ttu-id="b843f-158">`normalizedSource`: A string giving the normalized form of the source term.</span><span class="sxs-lookup"><span data-stu-id="b843f-158">`normalizedSource`: A string giving the normalized form of the source term.</span></span> <span data-ttu-id="b843f-159">Generally, this should be identical to the value of the `Text` field at the matching list index in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="b843f-159">Generally, this should be identical to the value of the `Text` field at the matching list index in the body of the request.</span></span>
    
  * <span data-ttu-id="b843f-160">`normalizedTarget`: A string giving the normalized form of the target term.</span><span class="sxs-lookup"><span data-stu-id="b843f-160">`normalizedTarget`: A string giving the normalized form of the target term.</span></span> <span data-ttu-id="b843f-161">Generally, this should be identical to the value of the `Translation` field at the matching list index in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="b843f-161">Generally, this should be identical to the value of the `Translation` field at the matching list index in the body of the request.</span></span>
  
  * <span data-ttu-id="b843f-162">`examples`: A list of examples for the (source term, target term) pair.</span><span class="sxs-lookup"><span data-stu-id="b843f-162">`examples`: A list of examples for the (source term, target term) pair.</span></span> <span data-ttu-id="b843f-163">Each element of the list is an object with the following properties:</span><span class="sxs-lookup"><span data-stu-id="b843f-163">Each element of the list is an object with the following properties:</span></span>

    * <span data-ttu-id="b843f-164">`sourcePrefix`: The string to concatenate _before_ the value of `sourceTerm` to form a complete example.</span><span class="sxs-lookup"><span data-stu-id="b843f-164">`sourcePrefix`: The string to concatenate _before_ the value of `sourceTerm` to form a complete example.</span></span> <span data-ttu-id="b843f-165">Do not add a space character, since it is already there when it should be.</span><span class="sxs-lookup"><span data-stu-id="b843f-165">Do not add a space character, since it is already there when it should be.</span></span> <span data-ttu-id="b843f-166">This value may be an empty string.</span><span class="sxs-lookup"><span data-stu-id="b843f-166">This value may be an empty string.</span></span>

    * <span data-ttu-id="b843f-167">`sourceTerm`: A string equal to the actual term looked up.</span><span class="sxs-lookup"><span data-stu-id="b843f-167">`sourceTerm`: A string equal to the actual term looked up.</span></span> <span data-ttu-id="b843f-168">The string is added with `sourcePrefix` and `sourceSuffix` to form the complete example.</span><span class="sxs-lookup"><span data-stu-id="b843f-168">The string is added with `sourcePrefix` and `sourceSuffix` to form the complete example.</span></span> <span data-ttu-id="b843f-169">Its value is separated so it can be marked in a user interface, e.g., by bolding it.</span><span class="sxs-lookup"><span data-stu-id="b843f-169">Its value is separated so it can be marked in a user interface, e.g., by bolding it.</span></span>

    * <span data-ttu-id="b843f-170">`sourceSuffix`: The string to concatenate _after_ the value of `sourceTerm` to form a complete example.</span><span class="sxs-lookup"><span data-stu-id="b843f-170">`sourceSuffix`: The string to concatenate _after_ the value of `sourceTerm` to form a complete example.</span></span> <span data-ttu-id="b843f-171">Do not add a space character, since it is already there when it should be.</span><span class="sxs-lookup"><span data-stu-id="b843f-171">Do not add a space character, since it is already there when it should be.</span></span> <span data-ttu-id="b843f-172">This value may be an empty string.</span><span class="sxs-lookup"><span data-stu-id="b843f-172">This value may be an empty string.</span></span>

    * <span data-ttu-id="b843f-173">`targetPrefix`: A string similar to `sourcePrefix` but for the target.</span><span class="sxs-lookup"><span data-stu-id="b843f-173">`targetPrefix`: A string similar to `sourcePrefix` but for the target.</span></span>

    * <span data-ttu-id="b843f-174">`targetTerm`: A string similar to `sourceTerm` but for the target.</span><span class="sxs-lookup"><span data-stu-id="b843f-174">`targetTerm`: A string similar to `sourceTerm` but for the target.</span></span>

    * <span data-ttu-id="b843f-175">`targetSuffix`: A string similar to `sourceSuffix` but for the target.</span><span class="sxs-lookup"><span data-stu-id="b843f-175">`targetSuffix`: A string similar to `sourceSuffix` but for the target.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b843f-176">If there are no examples in the dictionary, the response is 200 (OK) but the `examples` list is an empty list.</span><span class="sxs-lookup"><span data-stu-id="b843f-176">If there are no examples in the dictionary, the response is 200 (OK) but the `examples` list is an empty list.</span></span>

## <a name="examples"></a><span data-ttu-id="b843f-177">Examples</span><span class="sxs-lookup"><span data-stu-id="b843f-177">Examples</span></span>

<span data-ttu-id="b843f-178">This example shows how to lookup examples for the pair made up of the English term `fly` and its Spanish translation `volar`.</span><span class="sxs-lookup"><span data-stu-id="b843f-178">This example shows how to lookup examples for the pair made up of the English term `fly` and its Spanish translation `volar`.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="b843f-179">curl</span><span class="sxs-lookup"><span data-stu-id="b843f-179">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/dictionary/examples?api-version=3.0&from=en&to=es" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'fly', 'Translation':'volar'}]"
```

---

<span data-ttu-id="b843f-180">The response body (abbreviated for clarity) is:</span><span class="sxs-lookup"><span data-stu-id="b843f-180">The response body (abbreviated for clarity) is:</span></span>

```
[
    {
        "normalizedSource":"fly",
        "normalizedTarget":"volar",
        "examples":[
            {
                "sourcePrefix":"They need machines to ",
                "sourceTerm":"fly",
                "sourceSuffix":".",
                "targetPrefix":"Necesitan máquinas para ",
                "targetTerm":"volar",
                "targetSuffix":"."
            },      
            {
                "sourcePrefix":"That should really ",
                "sourceTerm":"fly",
                "sourceSuffix":".",
                "targetPrefix":"Eso realmente debe ",
                "targetTerm":"volar",
                "targetSuffix":"."
            },
            //
            // ...list abbreviated for documentation clarity
            //
        ]
    }
]
```
