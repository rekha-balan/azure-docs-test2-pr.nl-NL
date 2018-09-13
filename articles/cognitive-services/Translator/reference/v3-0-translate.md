---
title: Microsoft Translator Text API Translate Method | Microsoft Docs
titleSuffix: Cognitive Services
description: Use the Microsoft Translator Text API Translate method.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: microsoft translator
ms.topic: article
ms.date: 03/29/2018
ms.author: v-jansko
ms.openlocfilehash: d8d5e1e2fac747fa733f1d92c08008b7eac2a1bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870861"
---
# <a name="text-api-30-translate"></a><span data-ttu-id="25782-103">Text API 3.0: Translate</span><span class="sxs-lookup"><span data-stu-id="25782-103">Text API 3.0: Translate</span></span>

<span data-ttu-id="25782-104">Translates text.</span><span class="sxs-lookup"><span data-stu-id="25782-104">Translates text.</span></span>

## <a name="request-url"></a><span data-ttu-id="25782-105">Request URL</span><span class="sxs-lookup"><span data-stu-id="25782-105">Request URL</span></span>

<span data-ttu-id="25782-106">Send a `POST` request to:</span><span class="sxs-lookup"><span data-stu-id="25782-106">Send a `POST` request to:</span></span>

```HTTP
https://api.cognitive.microsofttranslator.com/translate?api-version=3.0
```

## <a name="request-parameters"></a><span data-ttu-id="25782-107">Request parameters</span><span class="sxs-lookup"><span data-stu-id="25782-107">Request parameters</span></span>

<span data-ttu-id="25782-108">Request parameters passed on the query string are:</span><span class="sxs-lookup"><span data-stu-id="25782-108">Request parameters passed on the query string are:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="25782-109">Query parameter</span><span class="sxs-lookup"><span data-stu-id="25782-109">Query parameter</span></span></th>
  <th><span data-ttu-id="25782-110">Description</span><span class="sxs-lookup"><span data-stu-id="25782-110">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="25782-111">api-version</span><span class="sxs-lookup"><span data-stu-id="25782-111">api-version</span></span></td>
    <td><span data-ttu-id="25782-112">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-112">*Required parameter*.</span></span><br/><span data-ttu-id="25782-113">Version of the API requested by the client.</span><span class="sxs-lookup"><span data-stu-id="25782-113">Version of the API requested by the client.</span></span> <span data-ttu-id="25782-114">Value must be `3.0`.</span><span class="sxs-lookup"><span data-stu-id="25782-114">Value must be `3.0`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-115">from</span><span class="sxs-lookup"><span data-stu-id="25782-115">from</span></span></td>
    <td><span data-ttu-id="25782-116">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-116">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-117">Specifies the language of the input text.</span><span class="sxs-lookup"><span data-stu-id="25782-117">Specifies the language of the input text.</span></span> <span data-ttu-id="25782-118">Find which languages are available to translate from by looking up [supported languages](.\v3-0-languages.md) using the `translation` scope.</span><span class="sxs-lookup"><span data-stu-id="25782-118">Find which languages are available to translate from by looking up [supported languages](.\v3-0-languages.md) using the `translation` scope.</span></span> <span data-ttu-id="25782-119">If the `from` parameter is not specified, automatic language detection is applied to determine the source language.</span><span class="sxs-lookup"><span data-stu-id="25782-119">If the `from` parameter is not specified, automatic language detection is applied to determine the source language.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-120">to</span><span class="sxs-lookup"><span data-stu-id="25782-120">to</span></span></td>
    <td><span data-ttu-id="25782-121">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-121">*Required parameter*.</span></span><br/><span data-ttu-id="25782-122">Specifies the language of the output text.</span><span class="sxs-lookup"><span data-stu-id="25782-122">Specifies the language of the output text.</span></span> <span data-ttu-id="25782-123">The target language must be one of the [supported languages](.\v3-0-languages.md) included in the `translation` scope.</span><span class="sxs-lookup"><span data-stu-id="25782-123">The target language must be one of the [supported languages](.\v3-0-languages.md) included in the `translation` scope.</span></span> <span data-ttu-id="25782-124">For example, use `to=de` to translate to German.</span><span class="sxs-lookup"><span data-stu-id="25782-124">For example, use `to=de` to translate to German.</span></span><br/><span data-ttu-id="25782-125">It's possible to translate to multiple languages simultaneously by repeating the parameter in the query string.</span><span class="sxs-lookup"><span data-stu-id="25782-125">It's possible to translate to multiple languages simultaneously by repeating the parameter in the query string.</span></span> <span data-ttu-id="25782-126">For example, use `to=de&to=it` to translate to German and Italian.</span><span class="sxs-lookup"><span data-stu-id="25782-126">For example, use `to=de&to=it` to translate to German and Italian.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-127">textType</span><span class="sxs-lookup"><span data-stu-id="25782-127">textType</span></span></td>
    <td><span data-ttu-id="25782-128">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-128">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-129">Defines whether the text being translated is plain text or HTML text.</span><span class="sxs-lookup"><span data-stu-id="25782-129">Defines whether the text being translated is plain text or HTML text.</span></span> <span data-ttu-id="25782-130">Any HTML needs to be a well-formed, complete element.</span><span class="sxs-lookup"><span data-stu-id="25782-130">Any HTML needs to be a well-formed, complete element.</span></span> <span data-ttu-id="25782-131">Possible values are: `plain` (default) or `html`.</span><span class="sxs-lookup"><span data-stu-id="25782-131">Possible values are: `plain` (default) or `html`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-132">category</span><span class="sxs-lookup"><span data-stu-id="25782-132">category</span></span></td>
    <td><span data-ttu-id="25782-133">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-133">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-134">A string specifying the category (domain) of the translation.</span><span class="sxs-lookup"><span data-stu-id="25782-134">A string specifying the category (domain) of the translation.</span></span> <span data-ttu-id="25782-135">This parameter is used to get translations from a customized system built with [Custom Translator](../customization.md).</span><span class="sxs-lookup"><span data-stu-id="25782-135">This parameter is used to get translations from a customized system built with [Custom Translator](../customization.md).</span></span> <span data-ttu-id="25782-136">Default value is: `general`.</span><span class="sxs-lookup"><span data-stu-id="25782-136">Default value is: `general`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-137">profanityAction</span><span class="sxs-lookup"><span data-stu-id="25782-137">profanityAction</span></span></td>
    <td><span data-ttu-id="25782-138">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-138">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-139">Specifies how profanities should be treated in translations.</span><span class="sxs-lookup"><span data-stu-id="25782-139">Specifies how profanities should be treated in translations.</span></span> <span data-ttu-id="25782-140">Possible values are: `NoAction` (default), `Marked` or `Deleted`.</span><span class="sxs-lookup"><span data-stu-id="25782-140">Possible values are: `NoAction` (default), `Marked` or `Deleted`.</span></span> <span data-ttu-id="25782-141">To understand ways to treat profanity, see [Profanity handling](#handle-profanity).</span><span class="sxs-lookup"><span data-stu-id="25782-141">To understand ways to treat profanity, see [Profanity handling](#handle-profanity).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-142">profanityMarker</span><span class="sxs-lookup"><span data-stu-id="25782-142">profanityMarker</span></span></td>
    <td><span data-ttu-id="25782-143">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-143">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-144">Specifies how profanities should be marked in translations.</span><span class="sxs-lookup"><span data-stu-id="25782-144">Specifies how profanities should be marked in translations.</span></span> <span data-ttu-id="25782-145">Possible values are: `Asterisk` (default) or `Tag`.</span><span class="sxs-lookup"><span data-stu-id="25782-145">Possible values are: `Asterisk` (default) or `Tag`.</span></span> <span data-ttu-id="25782-146">To understand ways to treat profanity, see [Profanity handling](#handle-profanity).</span><span class="sxs-lookup"><span data-stu-id="25782-146">To understand ways to treat profanity, see [Profanity handling](#handle-profanity).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-147">includeAlignment</span><span class="sxs-lookup"><span data-stu-id="25782-147">includeAlignment</span></span></td>
    <td><span data-ttu-id="25782-148">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-148">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-149">Specifies whether to include alignment projection from source text to translated text.</span><span class="sxs-lookup"><span data-stu-id="25782-149">Specifies whether to include alignment projection from source text to translated text.</span></span> <span data-ttu-id="25782-150">Possible values are: `true` or `false` (default).</span><span class="sxs-lookup"><span data-stu-id="25782-150">Possible values are: `true` or `false` (default).</span></span> </td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-151">includeSentenceLength</span><span class="sxs-lookup"><span data-stu-id="25782-151">includeSentenceLength</span></span></td>
    <td><span data-ttu-id="25782-152">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-152">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-153">Specifies whether to include sentence boundaries for the input text and the translated text.</span><span class="sxs-lookup"><span data-stu-id="25782-153">Specifies whether to include sentence boundaries for the input text and the translated text.</span></span> <span data-ttu-id="25782-154">Possible values are: `true` or `false` (default).</span><span class="sxs-lookup"><span data-stu-id="25782-154">Possible values are: `true` or `false` (default).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-155">suggestedFrom</span><span class="sxs-lookup"><span data-stu-id="25782-155">suggestedFrom</span></span></td>
    <td><span data-ttu-id="25782-156">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-156">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-157">Specifies a fallback language if the language of the input text can't be identified.</span><span class="sxs-lookup"><span data-stu-id="25782-157">Specifies a fallback language if the language of the input text can't be identified.</span></span> <span data-ttu-id="25782-158">Language auto-detection is applied when the `from` parameter is omitted.</span><span class="sxs-lookup"><span data-stu-id="25782-158">Language auto-detection is applied when the `from` parameter is omitted.</span></span> <span data-ttu-id="25782-159">If detection fails, the `suggestedFrom` language will be assumed.</span><span class="sxs-lookup"><span data-stu-id="25782-159">If detection fails, the `suggestedFrom` language will be assumed.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-160">fromScript</span><span class="sxs-lookup"><span data-stu-id="25782-160">fromScript</span></span></td>
    <td><span data-ttu-id="25782-161">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-161">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-162">Specifies the script of the input text.</span><span class="sxs-lookup"><span data-stu-id="25782-162">Specifies the script of the input text.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-163">toScript</span><span class="sxs-lookup"><span data-stu-id="25782-163">toScript</span></span></td>
    <td><span data-ttu-id="25782-164">*Optional parameter*.</span><span class="sxs-lookup"><span data-stu-id="25782-164">*Optional parameter*.</span></span><br/><span data-ttu-id="25782-165">Specifies the script of the translated text.</span><span class="sxs-lookup"><span data-stu-id="25782-165">Specifies the script of the translated text.</span></span></td>
  </tr>
</table> 

<span data-ttu-id="25782-166">Request headers include:</span><span class="sxs-lookup"><span data-stu-id="25782-166">Request headers include:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="25782-167">Headers</span><span class="sxs-lookup"><span data-stu-id="25782-167">Headers</span></span></th>
  <th><span data-ttu-id="25782-168">Description</span><span class="sxs-lookup"><span data-stu-id="25782-168">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="25782-169">_One authorization_</span><span class="sxs-lookup"><span data-stu-id="25782-169">_One authorization_</span></span><br/><span data-ttu-id="25782-170">_header_</span><span class="sxs-lookup"><span data-stu-id="25782-170">_header_</span></span></td>
    <td><span data-ttu-id="25782-171">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="25782-171">*Required request header*.</span></span><br/><span data-ttu-id="25782-172">See [available options for authentication](./v3-0-reference.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="25782-172">See [available options for authentication](./v3-0-reference.md#authentication).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-173">Content-Type</span><span class="sxs-lookup"><span data-stu-id="25782-173">Content-Type</span></span></td>
    <td><span data-ttu-id="25782-174">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="25782-174">*Required request header*.</span></span><br/><span data-ttu-id="25782-175">Specifies the content type of the payload.</span><span class="sxs-lookup"><span data-stu-id="25782-175">Specifies the content type of the payload.</span></span> <span data-ttu-id="25782-176">Possible values are: `application/json`.</span><span class="sxs-lookup"><span data-stu-id="25782-176">Possible values are: `application/json`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-177">Content-Length</span><span class="sxs-lookup"><span data-stu-id="25782-177">Content-Length</span></span></td>
    <td><span data-ttu-id="25782-178">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="25782-178">*Required request header*.</span></span><br/><span data-ttu-id="25782-179">The length of the request body.</span><span class="sxs-lookup"><span data-stu-id="25782-179">The length of the request body.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-180">X-ClientTraceId</span><span class="sxs-lookup"><span data-stu-id="25782-180">X-ClientTraceId</span></span></td>
    <td><span data-ttu-id="25782-181">*Optional*.</span><span class="sxs-lookup"><span data-stu-id="25782-181">*Optional*.</span></span><br/><span data-ttu-id="25782-182">A client-generated GUID to uniquely identify the request.</span><span class="sxs-lookup"><span data-stu-id="25782-182">A client-generated GUID to uniquely identify the request.</span></span> <span data-ttu-id="25782-183">You can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="25782-183">You can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="request-body"></a><span data-ttu-id="25782-184">Request body</span><span class="sxs-lookup"><span data-stu-id="25782-184">Request body</span></span>

<span data-ttu-id="25782-185">The body of the request is a JSON array.</span><span class="sxs-lookup"><span data-stu-id="25782-185">The body of the request is a JSON array.</span></span> <span data-ttu-id="25782-186">Each array element is a JSON object with a string property named `Text`, which represents the string to translate.</span><span class="sxs-lookup"><span data-stu-id="25782-186">Each array element is a JSON object with a string property named `Text`, which represents the string to translate.</span></span>

```json
[
    {"Text":"I would really like to drive your car around the block a few times."}
]
```

<span data-ttu-id="25782-187">The following limitations apply:</span><span class="sxs-lookup"><span data-stu-id="25782-187">The following limitations apply:</span></span>

* <span data-ttu-id="25782-188">The array can have at most 25 elements.</span><span class="sxs-lookup"><span data-stu-id="25782-188">The array can have at most 25 elements.</span></span>
* <span data-ttu-id="25782-189">The entire text included in the request cannot exceed 5,000 characters including spaces.</span><span class="sxs-lookup"><span data-stu-id="25782-189">The entire text included in the request cannot exceed 5,000 characters including spaces.</span></span>

## <a name="response-body"></a><span data-ttu-id="25782-190">Response body</span><span class="sxs-lookup"><span data-stu-id="25782-190">Response body</span></span>

<span data-ttu-id="25782-191">A successful response is a JSON array with one result for each string in the input array.</span><span class="sxs-lookup"><span data-stu-id="25782-191">A successful response is a JSON array with one result for each string in the input array.</span></span> <span data-ttu-id="25782-192">A result object includes the following properties:</span><span class="sxs-lookup"><span data-stu-id="25782-192">A result object includes the following properties:</span></span>

  * <span data-ttu-id="25782-193">`detectedLanguage`: An object describing the detected language through the following properties:</span><span class="sxs-lookup"><span data-stu-id="25782-193">`detectedLanguage`: An object describing the detected language through the following properties:</span></span>

      * <span data-ttu-id="25782-194">`language`: A string representing the code of the detected language.</span><span class="sxs-lookup"><span data-stu-id="25782-194">`language`: A string representing the code of the detected language.</span></span>

      * <span data-ttu-id="25782-195">`score`: A float value indicating the confidence in the result.</span><span class="sxs-lookup"><span data-stu-id="25782-195">`score`: A float value indicating the confidence in the result.</span></span> <span data-ttu-id="25782-196">The score is between zero and one and a low score indicates a low confidence.</span><span class="sxs-lookup"><span data-stu-id="25782-196">The score is between zero and one and a low score indicates a low confidence.</span></span>

    <span data-ttu-id="25782-197">The `detectedLanguage` property is only present in the result object when language auto-detection is requested.</span><span class="sxs-lookup"><span data-stu-id="25782-197">The `detectedLanguage` property is only present in the result object when language auto-detection is requested.</span></span>

  * <span data-ttu-id="25782-198">`translations`: An array of translation results.</span><span class="sxs-lookup"><span data-stu-id="25782-198">`translations`: An array of translation results.</span></span> <span data-ttu-id="25782-199">The size of the array matches the number of target languages specified through the `to` query parameter.</span><span class="sxs-lookup"><span data-stu-id="25782-199">The size of the array matches the number of target languages specified through the `to` query parameter.</span></span> <span data-ttu-id="25782-200">Each element in the array includes:</span><span class="sxs-lookup"><span data-stu-id="25782-200">Each element in the array includes:</span></span>

    * <span data-ttu-id="25782-201">`to`: A string representing the language code of the target language.</span><span class="sxs-lookup"><span data-stu-id="25782-201">`to`: A string representing the language code of the target language.</span></span>

    * <span data-ttu-id="25782-202">`text`: A string giving the translated text.</span><span class="sxs-lookup"><span data-stu-id="25782-202">`text`: A string giving the translated text.</span></span>

    * <span data-ttu-id="25782-203">`transliteration`: An object giving the translated text in the script specified by the `toScript` parameter.</span><span class="sxs-lookup"><span data-stu-id="25782-203">`transliteration`: An object giving the translated text in the script specified by the `toScript` parameter.</span></span>

      * <span data-ttu-id="25782-204">`script`: A string specifying the target script.</span><span class="sxs-lookup"><span data-stu-id="25782-204">`script`: A string specifying the target script.</span></span>   

      * <span data-ttu-id="25782-205">`text`: A string giving the translated text in the target script.</span><span class="sxs-lookup"><span data-stu-id="25782-205">`text`: A string giving the translated text in the target script.</span></span>

    <span data-ttu-id="25782-206">The `transliteration` object is not included if transliteration does not take place.</span><span class="sxs-lookup"><span data-stu-id="25782-206">The `transliteration` object is not included if transliteration does not take place.</span></span>

    * <span data-ttu-id="25782-207">`alignment`: An object with a single string property named `proj`, which maps input text to translated text.</span><span class="sxs-lookup"><span data-stu-id="25782-207">`alignment`: An object with a single string property named `proj`, which maps input text to translated text.</span></span> <span data-ttu-id="25782-208">The alignment information is only provided when the request parameter `includeAlignment` is `true`.</span><span class="sxs-lookup"><span data-stu-id="25782-208">The alignment information is only provided when the request parameter `includeAlignment` is `true`.</span></span> <span data-ttu-id="25782-209">Alignment is returned as a string value of the following format: `[[SourceTextStartIndex]:[SourceTextEndIndex]–[TgtTextStartIndex]:[TgtTextEndIndex]]`.</span><span class="sxs-lookup"><span data-stu-id="25782-209">Alignment is returned as a string value of the following format: `[[SourceTextStartIndex]:[SourceTextEndIndex]–[TgtTextStartIndex]:[TgtTextEndIndex]]`.</span></span>  <span data-ttu-id="25782-210">The colon separates start and end index, the dash separates the languages, and space separates the words.</span><span class="sxs-lookup"><span data-stu-id="25782-210">The colon separates start and end index, the dash separates the languages, and space separates the words.</span></span> <span data-ttu-id="25782-211">One word may align with zero, one, or multiple words in the other language, and the aligned words may be non-contiguous.</span><span class="sxs-lookup"><span data-stu-id="25782-211">One word may align with zero, one, or multiple words in the other language, and the aligned words may be non-contiguous.</span></span> <span data-ttu-id="25782-212">When no alignment information is available, the alignment element will be empty.</span><span class="sxs-lookup"><span data-stu-id="25782-212">When no alignment information is available, the alignment element will be empty.</span></span> <span data-ttu-id="25782-213">See [Obtain alignment information](#obtain-alignment-information) for an example and restrictions.</span><span class="sxs-lookup"><span data-stu-id="25782-213">See [Obtain alignment information](#obtain-alignment-information) for an example and restrictions.</span></span>

    * <span data-ttu-id="25782-214">`sentLen`: An object returning sentence boundaries in the input and output texts.</span><span class="sxs-lookup"><span data-stu-id="25782-214">`sentLen`: An object returning sentence boundaries in the input and output texts.</span></span>

      * <span data-ttu-id="25782-215">`srcSentLen`: An integer array representing the lengths of the sentences in the input text.</span><span class="sxs-lookup"><span data-stu-id="25782-215">`srcSentLen`: An integer array representing the lengths of the sentences in the input text.</span></span> <span data-ttu-id="25782-216">The length of the array is the number of sentences, and the values are the length of each sentence.</span><span class="sxs-lookup"><span data-stu-id="25782-216">The length of the array is the number of sentences, and the values are the length of each sentence.</span></span>

      * <span data-ttu-id="25782-217">`transSentLen`:  An integer array representing the lengths of the sentences in the translated text.</span><span class="sxs-lookup"><span data-stu-id="25782-217">`transSentLen`:  An integer array representing the lengths of the sentences in the translated text.</span></span> <span data-ttu-id="25782-218">The length of the array is the number of sentences, and the values are the length of each sentence.</span><span class="sxs-lookup"><span data-stu-id="25782-218">The length of the array is the number of sentences, and the values are the length of each sentence.</span></span>

    <span data-ttu-id="25782-219">Sentence boundaries are only included when the request parameter `includeSentenceLength` is `true`.</span><span class="sxs-lookup"><span data-stu-id="25782-219">Sentence boundaries are only included when the request parameter `includeSentenceLength` is `true`.</span></span>

  * <span data-ttu-id="25782-220">`sourceText`: An object with a single string property named `text`, which gives the input text in the default script of the source language.</span><span class="sxs-lookup"><span data-stu-id="25782-220">`sourceText`: An object with a single string property named `text`, which gives the input text in the default script of the source language.</span></span> <span data-ttu-id="25782-221">`sourceText` property is present only when the input is expressed in a script that's not the usual script for the language.</span><span class="sxs-lookup"><span data-stu-id="25782-221">`sourceText` property is present only when the input is expressed in a script that's not the usual script for the language.</span></span> <span data-ttu-id="25782-222">For example, if the input were Arabic written in Latin script, then `sourceText.text` would be the same Arabic text converted into Arab script.</span><span class="sxs-lookup"><span data-stu-id="25782-222">For example, if the input were Arabic written in Latin script, then `sourceText.text` would be the same Arabic text converted into Arab script.</span></span>

<span data-ttu-id="25782-223">Example of JSON responses are provided in the [examples](#examples) section.</span><span class="sxs-lookup"><span data-stu-id="25782-223">Example of JSON responses are provided in the [examples](#examples) section.</span></span>

## <a name="response-status-codes"></a><span data-ttu-id="25782-224">Response status codes</span><span class="sxs-lookup"><span data-stu-id="25782-224">Response status codes</span></span>

<span data-ttu-id="25782-225">The following are the possible HTTP status codes that a request returns.</span><span class="sxs-lookup"><span data-stu-id="25782-225">The following are the possible HTTP status codes that a request returns.</span></span> 

<table width="100%">
  <th width="20%"><span data-ttu-id="25782-226">Status Code</span><span class="sxs-lookup"><span data-stu-id="25782-226">Status Code</span></span></th>
  <th><span data-ttu-id="25782-227">Description</span><span class="sxs-lookup"><span data-stu-id="25782-227">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="25782-228">200</span><span class="sxs-lookup"><span data-stu-id="25782-228">200</span></span></td>
    <td><span data-ttu-id="25782-229">Success.</span><span class="sxs-lookup"><span data-stu-id="25782-229">Success.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-230">400</span><span class="sxs-lookup"><span data-stu-id="25782-230">400</span></span></td>
    <td><span data-ttu-id="25782-231">One of the query parameters is missing or not valid.</span><span class="sxs-lookup"><span data-stu-id="25782-231">One of the query parameters is missing or not valid.</span></span> <span data-ttu-id="25782-232">Correct request parameters before retrying.</span><span class="sxs-lookup"><span data-stu-id="25782-232">Correct request parameters before retrying.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-233">401</span><span class="sxs-lookup"><span data-stu-id="25782-233">401</span></span></td>
    <td><span data-ttu-id="25782-234">The request could not be authenticated.</span><span class="sxs-lookup"><span data-stu-id="25782-234">The request could not be authenticated.</span></span> <span data-ttu-id="25782-235">Check that credentials are specified and valid.</span><span class="sxs-lookup"><span data-stu-id="25782-235">Check that credentials are specified and valid.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-236">403</span><span class="sxs-lookup"><span data-stu-id="25782-236">403</span></span></td>
    <td><span data-ttu-id="25782-237">The request is not authorized.</span><span class="sxs-lookup"><span data-stu-id="25782-237">The request is not authorized.</span></span> <span data-ttu-id="25782-238">Check the details error message.</span><span class="sxs-lookup"><span data-stu-id="25782-238">Check the details error message.</span></span> <span data-ttu-id="25782-239">This often indicates that all free translations provided with a trial subscription have been used up.</span><span class="sxs-lookup"><span data-stu-id="25782-239">This often indicates that all free translations provided with a trial subscription have been used up.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-240">429</span><span class="sxs-lookup"><span data-stu-id="25782-240">429</span></span></td>
    <td><span data-ttu-id="25782-241">The caller is sending too many requests.</span><span class="sxs-lookup"><span data-stu-id="25782-241">The caller is sending too many requests.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-242">500</span><span class="sxs-lookup"><span data-stu-id="25782-242">500</span></span></td>
    <td><span data-ttu-id="25782-243">An unexpected error occurred.</span><span class="sxs-lookup"><span data-stu-id="25782-243">An unexpected error occurred.</span></span> <span data-ttu-id="25782-244">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="25782-244">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="25782-245">503</span><span class="sxs-lookup"><span data-stu-id="25782-245">503</span></span></td>
    <td><span data-ttu-id="25782-246">Server temporarily unavailable.</span><span class="sxs-lookup"><span data-stu-id="25782-246">Server temporarily unavailable.</span></span> <span data-ttu-id="25782-247">Retry the request.</span><span class="sxs-lookup"><span data-stu-id="25782-247">Retry the request.</span></span> <span data-ttu-id="25782-248">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="25782-248">If the error persists, report it with: date and time of the failure, request identifier from response header `X-RequestId`, and client identifier from request header `X-ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="examples"></a><span data-ttu-id="25782-249">Examples</span><span class="sxs-lookup"><span data-stu-id="25782-249">Examples</span></span>

### <a name="translate-a-single-input"></a><span data-ttu-id="25782-250">Translate a single input</span><span class="sxs-lookup"><span data-stu-id="25782-250">Translate a single input</span></span>

<span data-ttu-id="25782-251">This example shows how to translate a single sentence from English to Simplified Chinese.</span><span class="sxs-lookup"><span data-stu-id="25782-251">This example shows how to translate a single sentence from English to Simplified Chinese.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-252">curl</span><span class="sxs-lookup"><span data-stu-id="25782-252">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=en&to=zh-Hans" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'Hello, what is your name?'}]"
```

---

<span data-ttu-id="25782-253">The response body is:</span><span class="sxs-lookup"><span data-stu-id="25782-253">The response body is:</span></span>

```
[
    {
        "translations":[
            {"text":"你好, 你叫什么名字？","to":"zh-Hans"}
        ]
    }
]
```

<span data-ttu-id="25782-254">The `translations` array includes one element, which provides the translation of the single piece of text in the input.</span><span class="sxs-lookup"><span data-stu-id="25782-254">The `translations` array includes one element, which provides the translation of the single piece of text in the input.</span></span>

### <a name="translate-a-single-input-with-language-auto-detection"></a><span data-ttu-id="25782-255">Translate a single input with language auto-detection</span><span class="sxs-lookup"><span data-stu-id="25782-255">Translate a single input with language auto-detection</span></span>

<span data-ttu-id="25782-256">This example shows how to translate a single sentence from English to Simplified Chinese.</span><span class="sxs-lookup"><span data-stu-id="25782-256">This example shows how to translate a single sentence from English to Simplified Chinese.</span></span> <span data-ttu-id="25782-257">The request does not specify the input language.</span><span class="sxs-lookup"><span data-stu-id="25782-257">The request does not specify the input language.</span></span> <span data-ttu-id="25782-258">Auto-detection of the source language is used instead.</span><span class="sxs-lookup"><span data-stu-id="25782-258">Auto-detection of the source language is used instead.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-259">curl</span><span class="sxs-lookup"><span data-stu-id="25782-259">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&to=zh-Hans" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'Hello, what is your name?'}]"
```

---

<span data-ttu-id="25782-260">The response body is:</span><span class="sxs-lookup"><span data-stu-id="25782-260">The response body is:</span></span>

```
[
    {
        "detectedLanguage": {"language": "en", "score": 1.0},
        "translations":[
            {"text": "你好, 你叫什么名字？", "to": "zh-Hans"}
        ]
    }
]
```
<span data-ttu-id="25782-261">The response is similar to the response from the previous example.</span><span class="sxs-lookup"><span data-stu-id="25782-261">The response is similar to the response from the previous example.</span></span> <span data-ttu-id="25782-262">Since language auto-detection was requested, the response also includes information about the language detected for the input text.</span><span class="sxs-lookup"><span data-stu-id="25782-262">Since language auto-detection was requested, the response also includes information about the language detected for the input text.</span></span> 

### <a name="translate-with-transliteration"></a><span data-ttu-id="25782-263">Translate with transliteration</span><span class="sxs-lookup"><span data-stu-id="25782-263">Translate with transliteration</span></span>

<span data-ttu-id="25782-264">Let's extend the previous example by adding transliteration.</span><span class="sxs-lookup"><span data-stu-id="25782-264">Let's extend the previous example by adding transliteration.</span></span> <span data-ttu-id="25782-265">The following request asks for a Chinese translation written in Latin script.</span><span class="sxs-lookup"><span data-stu-id="25782-265">The following request asks for a Chinese translation written in Latin script.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-266">curl</span><span class="sxs-lookup"><span data-stu-id="25782-266">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&to=zh-Latn" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'Hello, what is your name?'}]"
```

---

<span data-ttu-id="25782-267">The response body is:</span><span class="sxs-lookup"><span data-stu-id="25782-267">The response body is:</span></span>

```
[
    {
        "detectedLanguage":{"language":"en","score":1.0},
        "translations":[
            {
                "text":"你好, 你叫什么名字？",
                "transliteration":{"text":"nǐ hǎo , nǐ jiào shén me míng zì ？","script":"Latn"},
                "to":"zh-Hans"
            }
        ]
    }
]
```

<span data-ttu-id="25782-268">The translation result now includes a `transliteration` property, which gives the translated text using Latin characters.</span><span class="sxs-lookup"><span data-stu-id="25782-268">The translation result now includes a `transliteration` property, which gives the translated text using Latin characters.</span></span>

### <a name="translate-multiple-pieces-of-text"></a><span data-ttu-id="25782-269">Translate multiple pieces of text</span><span class="sxs-lookup"><span data-stu-id="25782-269">Translate multiple pieces of text</span></span>

<span data-ttu-id="25782-270">Translating multiple strings at once is simply a matter of specifying an array of strings in the request body.</span><span class="sxs-lookup"><span data-stu-id="25782-270">Translating multiple strings at once is simply a matter of specifying an array of strings in the request body.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-271">curl</span><span class="sxs-lookup"><span data-stu-id="25782-271">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=en&to=zh-Hans" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'Hello, what is your name?'}, {'Text':'I am fine, thank you.'}]"
```

---

<span data-ttu-id="25782-272">The response body is:</span><span class="sxs-lookup"><span data-stu-id="25782-272">The response body is:</span></span>

```
[
    {
        "translations":[
            {"text":"你好, 你叫什么名字？","to":"zh-Hans"}
        ]
    },            
    {
        "translations":[
            {"text":"我很好，谢谢你。","to":"zh-Hans"}
        ]
    }
]
```

### <a name="translate-to-multiple-languages"></a><span data-ttu-id="25782-273">Translate to multiple languages</span><span class="sxs-lookup"><span data-stu-id="25782-273">Translate to multiple languages</span></span>

<span data-ttu-id="25782-274">This example shows how to translate the same input to several languages in one request.</span><span class="sxs-lookup"><span data-stu-id="25782-274">This example shows how to translate the same input to several languages in one request.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-275">curl</span><span class="sxs-lookup"><span data-stu-id="25782-275">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=en&to=zh-Hans&to=de" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'Hello, what is your name?'}]"
```

---

<span data-ttu-id="25782-276">The response body is:</span><span class="sxs-lookup"><span data-stu-id="25782-276">The response body is:</span></span>

```
[
    {
        "translations":[
            {"text":"你好, 你叫什么名字？","to":"zh-Hans"},
            {"text":"Hallo, was ist dein Name?","to":"de"}
        ]
    }
]
```

### <a name="handle-profanity"></a><span data-ttu-id="25782-277">Handle profanity</span><span class="sxs-lookup"><span data-stu-id="25782-277">Handle profanity</span></span>

<span data-ttu-id="25782-278">Normally the Translator service will retain profanity that is present in the source in the translation.</span><span class="sxs-lookup"><span data-stu-id="25782-278">Normally the Translator service will retain profanity that is present in the source in the translation.</span></span> <span data-ttu-id="25782-279">The degree of profanity and the context that makes words profane differ between cultures, and as a result the degree of profanity in the target language may be amplified or reduced.</span><span class="sxs-lookup"><span data-stu-id="25782-279">The degree of profanity and the context that makes words profane differ between cultures, and as a result the degree of profanity in the target language may be amplified or reduced.</span></span>

<span data-ttu-id="25782-280">If you want to avoid getting profanity in the translation, regardless of the presence of profanity in the source text, you can use the profanity filtering option.</span><span class="sxs-lookup"><span data-stu-id="25782-280">If you want to avoid getting profanity in the translation, regardless of the presence of profanity in the source text, you can use the profanity filtering option.</span></span> <span data-ttu-id="25782-281">The option allows you to choose whether you want to see profanity deleted, whether you want to mark profanities with appropriate tags (giving you the option to add your own post-processing), or you want no action taken.</span><span class="sxs-lookup"><span data-stu-id="25782-281">The option allows you to choose whether you want to see profanity deleted, whether you want to mark profanities with appropriate tags (giving you the option to add your own post-processing), or you want no action taken.</span></span> <span data-ttu-id="25782-282">The accepted values of `ProfanityAction` are `Deleted`, `Marked` and `NoAction` (default).</span><span class="sxs-lookup"><span data-stu-id="25782-282">The accepted values of `ProfanityAction` are `Deleted`, `Marked` and `NoAction` (default).</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="25782-283">ProfanityAction</span><span class="sxs-lookup"><span data-stu-id="25782-283">ProfanityAction</span></span></th>
  <th><span data-ttu-id="25782-284">Action</span><span class="sxs-lookup"><span data-stu-id="25782-284">Action</span></span></th>
  <tr>
    <td>`NoAction`</td>
    <td><span data-ttu-id="25782-285">This is the default behavior.</span><span class="sxs-lookup"><span data-stu-id="25782-285">This is the default behavior.</span></span> <span data-ttu-id="25782-286">Profanity will pass from source to target.</span><span class="sxs-lookup"><span data-stu-id="25782-286">Profanity will pass from source to target.</span></span><br/><br/><span data-ttu-id="25782-287">
    \*\*Example Source (Japanese)\*\*: 彼はジャッカスです。</span><span class="sxs-lookup"><span data-stu-id="25782-287">
    \*\*Example Source (Japanese)\*\*: 彼はジャッカスです。</span></span><br/><span data-ttu-id="25782-288">
    \*\*Example Translation (English)\*\*: He is a jackass.</span><span class="sxs-lookup"><span data-stu-id="25782-288">
    \*\*Example Translation (English)\*\*: He is a jackass.</span></span>
    </td>
  </tr>
  <tr>
    <td>`Deleted`</td>
    <td><span data-ttu-id="25782-289">Profane words will be removed from the output without replacement.</span><span class="sxs-lookup"><span data-stu-id="25782-289">Profane words will be removed from the output without replacement.</span></span><br/><br/><span data-ttu-id="25782-290">
    \*\*Example Source (Japanese)\*\*: 彼はジャッカスです。</span><span class="sxs-lookup"><span data-stu-id="25782-290">
    \*\*Example Source (Japanese)\*\*: 彼はジャッカスです。</span></span><br/><span data-ttu-id="25782-291">
    \*\*Example Translation (English)\*\*: He is a.</span><span class="sxs-lookup"><span data-stu-id="25782-291">
    \*\*Example Translation (English)\*\*: He is a.</span></span>
    </td>
  </tr>
  <tr>
    <td>`Marked`</td>
    <td><span data-ttu-id="25782-292">Profane words are replaced by a marker in the output.</span><span class="sxs-lookup"><span data-stu-id="25782-292">Profane words are replaced by a marker in the output.</span></span> <span data-ttu-id="25782-293">The marker depends on the `ProfanityMarker` parameter.</span><span class="sxs-lookup"><span data-stu-id="25782-293">The marker depends on the `ProfanityMarker` parameter.</span></span><br/><br/>
<span data-ttu-id="25782-294">For `ProfanityMarker=Asterisk`, profane words are replaced with `***`:</span><span class="sxs-lookup"><span data-stu-id="25782-294">For `ProfanityMarker=Asterisk`, profane words are replaced with `***`:</span></span><br/><span data-ttu-id="25782-295">
    \*\*Example Source (Japanese)\*\*: 彼はジャッカスです。</span><span class="sxs-lookup"><span data-stu-id="25782-295">
    \*\*Example Source (Japanese)\*\*: 彼はジャッカスです。</span></span><br/><span data-ttu-id="25782-296">
    \*\*Example Translation (English)\*\*: He is a \*\*\*.</span><span class="sxs-lookup"><span data-stu-id="25782-296">
    \*\*Example Translation (English)\*\*: He is a \*\*\*.</span></span><br/><br/>
<span data-ttu-id="25782-297">For `ProfanityMarker=Tag`, profane words are surrounded by XML tags &lt;profanity&gt; and &lt;/profanity&gt;:</span><span class="sxs-lookup"><span data-stu-id="25782-297">For `ProfanityMarker=Tag`, profane words are surrounded by XML tags &lt;profanity&gt; and &lt;/profanity&gt;:</span></span><br/><span data-ttu-id="25782-298">
    \*\*Example Source (Japanese)\*\*: 彼はジャッカスです。</span><span class="sxs-lookup"><span data-stu-id="25782-298">
    \*\*Example Source (Japanese)\*\*: 彼はジャッカスです。</span></span><br/><span data-ttu-id="25782-299">
    \*\*Example Translation (English)\*\*: He is a &lt;profanity&gt;jackass&lt;/profanity&gt;.</span><span class="sxs-lookup"><span data-stu-id="25782-299">
    \*\*Example Translation (English)\*\*: He is a &lt;profanity&gt;jackass&lt;/profanity&gt;.</span></span>
  </tr>
</table> 

<span data-ttu-id="25782-300">For example:</span><span class="sxs-lookup"><span data-stu-id="25782-300">For example:</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-301">curl</span><span class="sxs-lookup"><span data-stu-id="25782-301">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=en&to=de&profanityAction=Marked" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'This is a fucking good idea.'}]"
```

---

<span data-ttu-id="25782-302">This returns:</span><span class="sxs-lookup"><span data-stu-id="25782-302">This returns:</span></span>

```
[
    {
        "translations":[
            {"text":"Das ist eine *** gute Idee.","to":"de"}
        ]
    }
]
```

<span data-ttu-id="25782-303">Compare with:</span><span class="sxs-lookup"><span data-stu-id="25782-303">Compare with:</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-304">curl</span><span class="sxs-lookup"><span data-stu-id="25782-304">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=en&to=de&profanityAction=Marked&profanityMarker=Tag" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'This is a fucking good idea.'}]"
```

---

<span data-ttu-id="25782-305">That last request returns:</span><span class="sxs-lookup"><span data-stu-id="25782-305">That last request returns:</span></span>

```
[
    {
        "translations":[
            {"text":"Das ist eine <profanity>verdammt</profanity> gute Idee.","to":"de"}
        ]
    }
]
```

### <a name="translate-content-with-markup-and-decide-whats-translated"></a><span data-ttu-id="25782-306">Translate content with markup and decide what's translated</span><span class="sxs-lookup"><span data-stu-id="25782-306">Translate content with markup and decide what's translated</span></span>

<span data-ttu-id="25782-307">It's common to translate content which includes markup such as content from an HTML page or content from an XML document.</span><span class="sxs-lookup"><span data-stu-id="25782-307">It's common to translate content which includes markup such as content from an HTML page or content from an XML document.</span></span> <span data-ttu-id="25782-308">Include query parameter `textType=html` when translating content with tags.</span><span class="sxs-lookup"><span data-stu-id="25782-308">Include query parameter `textType=html` when translating content with tags.</span></span> <span data-ttu-id="25782-309">In addition, it's sometimes useful to exclude specific content from translation.</span><span class="sxs-lookup"><span data-stu-id="25782-309">In addition, it's sometimes useful to exclude specific content from translation.</span></span> <span data-ttu-id="25782-310">You can use the attribute `class=notranslate` to specify content that should remain in its original language.</span><span class="sxs-lookup"><span data-stu-id="25782-310">You can use the attribute `class=notranslate` to specify content that should remain in its original language.</span></span> <span data-ttu-id="25782-311">In the following example, the content inside the first `div` element will not be translated, while the content in the second `div` element will be translated.</span><span class="sxs-lookup"><span data-stu-id="25782-311">In the following example, the content inside the first `div` element will not be translated, while the content in the second `div` element will be translated.</span></span>

```
<div class="notranslate">This will not be translated.</div>
<div>This will be translated. </div>
```

<span data-ttu-id="25782-312">Here is a sample request to illustrate.</span><span class="sxs-lookup"><span data-stu-id="25782-312">Here is a sample request to illustrate.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-313">curl</span><span class="sxs-lookup"><span data-stu-id="25782-313">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=en&to=zh-Hans&textType=html" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'<div class=\"notranslate\">This will not be translated.</div><div>This will be translated.</div>'}]"
```

---

<span data-ttu-id="25782-314">The response is:</span><span class="sxs-lookup"><span data-stu-id="25782-314">The response is:</span></span>

```
[
    {
        "translations":[
            {"text":"<div class=\"notranslate\">This will not be translated.</div><div>这将被翻译。</div>","to":"zh-Hans"}
        ]
    }
]
```

### <a name="obtain-alignment-information"></a><span data-ttu-id="25782-315">Obtain alignment information</span><span class="sxs-lookup"><span data-stu-id="25782-315">Obtain alignment information</span></span>

<span data-ttu-id="25782-316">To receive alignment information, specify `includeAlignment=true` on the query string.</span><span class="sxs-lookup"><span data-stu-id="25782-316">To receive alignment information, specify `includeAlignment=true` on the query string.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-317">curl</span><span class="sxs-lookup"><span data-stu-id="25782-317">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=en&to=fr&includeAlignment=true" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'The answer lies in machine translation.'}]"
```

---

<span data-ttu-id="25782-318">The response is:</span><span class="sxs-lookup"><span data-stu-id="25782-318">The response is:</span></span>

```
[
    {
        "translations":[
            {
                "text":"La réponse se trouve dans la traduction automatique.",
                "to":"fr",
                "alignment":{"proj":"0:2-0:1 4:9-3:9 11:14-11:19 16:17-21:24 19:25-40:50 27:37-29:38 38:38-51:51"}
            }
        ]
    }
]
```

<span data-ttu-id="25782-319">The alignment information starts with `0:2-0:1`, which means that the first three characters in the source text (`The`) map to the first two characters in the translated text (`La`).</span><span class="sxs-lookup"><span data-stu-id="25782-319">The alignment information starts with `0:2-0:1`, which means that the first three characters in the source text (`The`) map to the first two characters in the translated text (`La`).</span></span>

<span data-ttu-id="25782-320">Note the following restrictions:</span><span class="sxs-lookup"><span data-stu-id="25782-320">Note the following restrictions:</span></span>

* <span data-ttu-id="25782-321">Alignment is only returned for a subset of the language pairs:</span><span class="sxs-lookup"><span data-stu-id="25782-321">Alignment is only returned for a subset of the language pairs:</span></span>
  - <span data-ttu-id="25782-322">from English to any other language;</span><span class="sxs-lookup"><span data-stu-id="25782-322">from English to any other language;</span></span>
  - <span data-ttu-id="25782-323">from any other language to English except for Chinese Simplified, Chinese Traditional, and Latvian to English;</span><span class="sxs-lookup"><span data-stu-id="25782-323">from any other language to English except for Chinese Simplified, Chinese Traditional, and Latvian to English;</span></span>
  - <span data-ttu-id="25782-324">from Japanese to Korean or from Korean to Japanese.</span><span class="sxs-lookup"><span data-stu-id="25782-324">from Japanese to Korean or from Korean to Japanese.</span></span>
* <span data-ttu-id="25782-325">You will not receive alignment if the sentence is a canned translation.</span><span class="sxs-lookup"><span data-stu-id="25782-325">You will not receive alignment if the sentence is a canned translation.</span></span> <span data-ttu-id="25782-326">Example of a canned translation is "This is a test", "I love you" and other high frequency sentences.</span><span class="sxs-lookup"><span data-stu-id="25782-326">Example of a canned translation is "This is a test", "I love you" and other high frequency sentences.</span></span>

### <a name="obtain-sentence-boundaries"></a><span data-ttu-id="25782-327">Obtain sentence boundaries</span><span class="sxs-lookup"><span data-stu-id="25782-327">Obtain sentence boundaries</span></span>

<span data-ttu-id="25782-328">To receive information about sentence length in the source text and translated text, specify `includeSentenceLength=true` on the query string.</span><span class="sxs-lookup"><span data-stu-id="25782-328">To receive information about sentence length in the source text and translated text, specify `includeSentenceLength=true` on the query string.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="25782-329">curl</span><span class="sxs-lookup"><span data-stu-id="25782-329">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=en&to=fr&includeSentenceLength=true" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'The answer lies in machine translation. The best machine translation technology cannot always provide translations tailored to a site or users like a human. Simply copy and paste a code snippet anywhere.'}]"
```

---

<span data-ttu-id="25782-330">The response is:</span><span class="sxs-lookup"><span data-stu-id="25782-330">The response is:</span></span>

```
[
    {
        "translations":[
            {
                "text":"La réponse se trouve dans la traduction automatique. La meilleure technologie de traduction automatique ne peut pas toujours fournir des traductions adaptées à un site ou des utilisateurs comme un être humain. Il suffit de copier et coller un extrait de code n’importe où.",
                "to":"fr",
                "sentLen":{"srcSentLen":[40,117,46],"transSentLen":[53,157,62]}
            }
        ]
    }
]
```

### <a name="translate-with-dynamic-dictionary"></a><span data-ttu-id="25782-331">Translate with dynamic dictionary</span><span class="sxs-lookup"><span data-stu-id="25782-331">Translate with dynamic dictionary</span></span>

<span data-ttu-id="25782-332">If you already know the translation you want to apply to a word or a phrase, you can supply it as markup within the request.</span><span class="sxs-lookup"><span data-stu-id="25782-332">If you already know the translation you want to apply to a word or a phrase, you can supply it as markup within the request.</span></span> <span data-ttu-id="25782-333">The dynamic dictionary is only safe for compound nouns like proper names and product names.</span><span class="sxs-lookup"><span data-stu-id="25782-333">The dynamic dictionary is only safe for compound nouns like proper names and product names.</span></span>

<span data-ttu-id="25782-334">The markup to supply uses the following syntax.</span><span class="sxs-lookup"><span data-stu-id="25782-334">The markup to supply uses the following syntax.</span></span>

``` 
<mstrans:dictionary translation=”translation of phrase”>phrase</mstrans:dictionary>
```

<span data-ttu-id="25782-335">For example, consider the English sentence "The word wordomatic is a dictionary entry."</span><span class="sxs-lookup"><span data-stu-id="25782-335">For example, consider the English sentence "The word wordomatic is a dictionary entry."</span></span> <span data-ttu-id="25782-336">To preserve the word _wordomatic_ in the translation, send the request:</span><span class="sxs-lookup"><span data-stu-id="25782-336">To preserve the word _wordomatic_ in the translation, send the request:</span></span>

```
curl -X POST "https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=en&to=de" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'The word <mstrans:dictionary translation=\"wordomatic\">word or phrase</mstrans:dictionary> is a dictionary entry.'}]"
```

<span data-ttu-id="25782-337">The result is:</span><span class="sxs-lookup"><span data-stu-id="25782-337">The result is:</span></span>

```
[
    {
        "translations":[
            {"text":"Das Wort "wordomatic" ist ein Wörterbucheintrag.","to":"de"}
        ]
    }
]
```

<span data-ttu-id="25782-338">This feature works the same way with `textType=text` or with `textType=html`.</span><span class="sxs-lookup"><span data-stu-id="25782-338">This feature works the same way with `textType=text` or with `textType=html`.</span></span> <span data-ttu-id="25782-339">The feature should be used sparingly.</span><span class="sxs-lookup"><span data-stu-id="25782-339">The feature should be used sparingly.</span></span> <span data-ttu-id="25782-340">The appropriate and far better way of customizing translation is by using Custom Translator.</span><span class="sxs-lookup"><span data-stu-id="25782-340">The appropriate and far better way of customizing translation is by using Custom Translator.</span></span> <span data-ttu-id="25782-341">Custom Translator makes full use of context and statistical probabilities.</span><span class="sxs-lookup"><span data-stu-id="25782-341">Custom Translator makes full use of context and statistical probabilities.</span></span> <span data-ttu-id="25782-342">If you have or can afford to create training data that shows your work or phrase in context, you get much better results.</span><span class="sxs-lookup"><span data-stu-id="25782-342">If you have or can afford to create training data that shows your work or phrase in context, you get much better results.</span></span> <span data-ttu-id="25782-343">[Learn more about Custom Translator](../customization.md).</span><span class="sxs-lookup"><span data-stu-id="25782-343">[Learn more about Custom Translator](../customization.md).</span></span>
 





