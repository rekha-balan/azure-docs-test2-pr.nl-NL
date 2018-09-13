---
title: Microsoft Translator Text API Dictionary Lookup Method | Microsoft Docs
description: Use the Microsoft Translator Text API Dictionary Lookup method.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.technology: microsoft translator
ms.topic: article
ms.date: 03/29/2018
ms.author: v-jansko
ms.openlocfilehash: 5a186f60dc099b095c00056d965aa92618c2c708
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866208"
---
# <a name="text-api-30-dictionary-lookup"></a><span data-ttu-id="a7ad1-103">Text API 3.0: Dictionary Lookup</span><span class="sxs-lookup"><span data-stu-id="a7ad1-103">Text API 3.0: Dictionary Lookup</span></span>

<span data-ttu-id="a7ad1-104">Provides alternative translations for a word and a small number of idiomatic phrases.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-104">Provides alternative translations for a word and a small number of idiomatic phrases.</span></span> <span data-ttu-id="a7ad1-105">Each translation has a part-of-speech and a list of back-translations.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-105">Each translation has a part-of-speech and a list of back-translations.</span></span> <span data-ttu-id="a7ad1-106">The back-translations enable a user to understand the translation in context.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-106">The back-translations enable a user to understand the translation in context.</span></span> <span data-ttu-id="a7ad1-107">The [Dictionary Example](.\v3-0-dictionary-examples.md) operation allows further drill down to see example uses of each translation pair.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-107">The [Dictionary Example](.\v3-0-dictionary-examples.md) operation allows further drill down to see example uses of each translation pair.</span></span>

## <a name="request-url"></a><span data-ttu-id="a7ad1-108">Request URL</span><span class="sxs-lookup"><span data-stu-id="a7ad1-108">Request URL</span></span>

<span data-ttu-id="a7ad1-109">Send a `POST` request to:</span><span class="sxs-lookup"><span data-stu-id="a7ad1-109">Send a `POST` request to:</span></span>

```HTTP
https://api.cognitive.microsofttranslator.com/dictionary/lookup?api-version=3.0
```

## <a name="request-parameters"></a><span data-ttu-id="a7ad1-110">Request parameters</span><span class="sxs-lookup"><span data-stu-id="a7ad1-110">Request parameters</span></span>

<span data-ttu-id="a7ad1-111">Request parameters passed on the query string are:</span><span class="sxs-lookup"><span data-stu-id="a7ad1-111">Request parameters passed on the query string are:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="a7ad1-112">Query parameter</span><span class="sxs-lookup"><span data-stu-id="a7ad1-112">Query parameter</span></span></th>
  <th><span data-ttu-id="a7ad1-113">Description</span><span class="sxs-lookup"><span data-stu-id="a7ad1-113">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="a7ad1-114">api-version</span><span class="sxs-lookup"><span data-stu-id="a7ad1-114">api-version</span></span></td>
    <td><span data-ttu-id="a7ad1-115">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-115">*Required parameter*.</span></span><br/><span data-ttu-id="a7ad1-116">Version of the API requested by the client.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-116">Version of the API requested by the client.</span></span> <span data-ttu-id="a7ad1-117">Value must be `3.0`.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-117">Value must be `3.0`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="a7ad1-118">from</span><span class="sxs-lookup"><span data-stu-id="a7ad1-118">from</span></span></td>
    <td><span data-ttu-id="a7ad1-119">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-119">*Required parameter*.</span></span><br/><span data-ttu-id="a7ad1-120">Specifies the language of the input text.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-120">Specifies the language of the input text.</span></span> <span data-ttu-id="a7ad1-121">The source language must be one of the [supported languages](.\v3-0-languages.md) included in the `dictionary` scope.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-121">The source language must be one of the [supported languages](.\v3-0-languages.md) included in the `dictionary` scope.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="a7ad1-122">to</span><span class="sxs-lookup"><span data-stu-id="a7ad1-122">to</span></span></td>
    <td><span data-ttu-id="a7ad1-123">*Required parameter*.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-123">*Required parameter*.</span></span><br/><span data-ttu-id="a7ad1-124">Specifies the language of the output text.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-124">Specifies the language of the output text.</span></span> <span data-ttu-id="a7ad1-125">The target language must be one of the [supported languages](.\v3-0-languages.md) included in the `dictionary` scope.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-125">The target language must be one of the [supported languages](.\v3-0-languages.md) included in the `dictionary` scope.</span></span></td>
  </tr>
</table>

<span data-ttu-id="a7ad1-126">Request headers include:</span><span class="sxs-lookup"><span data-stu-id="a7ad1-126">Request headers include:</span></span>

<table width="100%">
  <th width="20%"><span data-ttu-id="a7ad1-127">Headers</span><span class="sxs-lookup"><span data-stu-id="a7ad1-127">Headers</span></span></th>
  <th><span data-ttu-id="a7ad1-128">Description</span><span class="sxs-lookup"><span data-stu-id="a7ad1-128">Description</span></span></th>
  <tr>
    <td><span data-ttu-id="a7ad1-129">_One authorization_</span><span class="sxs-lookup"><span data-stu-id="a7ad1-129">_One authorization_</span></span><br/><span data-ttu-id="a7ad1-130">_header_</span><span class="sxs-lookup"><span data-stu-id="a7ad1-130">_header_</span></span></td>
    <td><span data-ttu-id="a7ad1-131">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-131">*Required request header*.</span></span><br/><span data-ttu-id="a7ad1-132">See [available options for authentication](./v3-0-reference.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="a7ad1-132">See [available options for authentication](./v3-0-reference.md#authentication).</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="a7ad1-133">Content-Type</span><span class="sxs-lookup"><span data-stu-id="a7ad1-133">Content-Type</span></span></td>
    <td><span data-ttu-id="a7ad1-134">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-134">*Required request header*.</span></span><br/><span data-ttu-id="a7ad1-135">Specifies the content type of the payload.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-135">Specifies the content type of the payload.</span></span> <span data-ttu-id="a7ad1-136">Possible values are: `application/json`.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-136">Possible values are: `application/json`.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="a7ad1-137">Content-Length</span><span class="sxs-lookup"><span data-stu-id="a7ad1-137">Content-Length</span></span></td>
    <td><span data-ttu-id="a7ad1-138">*Required request header*.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-138">*Required request header*.</span></span><br/><span data-ttu-id="a7ad1-139">The length of the request body.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-139">The length of the request body.</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="a7ad1-140">X-ClientTraceId</span><span class="sxs-lookup"><span data-stu-id="a7ad1-140">X-ClientTraceId</span></span></td>
    <td><span data-ttu-id="a7ad1-141">*Optional*.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-141">*Optional*.</span></span><br/><span data-ttu-id="a7ad1-142">A client-generated GUID to uniquely identify the request.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-142">A client-generated GUID to uniquely identify the request.</span></span> <span data-ttu-id="a7ad1-143">You can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-143">You can omit this header if you include the trace ID in the query string using a query parameter named `ClientTraceId`.</span></span></td>
  </tr>
</table> 

## <a name="request-body"></a><span data-ttu-id="a7ad1-144">Request body</span><span class="sxs-lookup"><span data-stu-id="a7ad1-144">Request body</span></span>

<span data-ttu-id="a7ad1-145">The body of the request is a JSON array.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-145">The body of the request is a JSON array.</span></span> <span data-ttu-id="a7ad1-146">Each array element is a JSON object with a string property named `Text`, which represents the term to lookup.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-146">Each array element is a JSON object with a string property named `Text`, which represents the term to lookup.</span></span>

```json
[
    {"Text":"fly"}
]
```

<span data-ttu-id="a7ad1-147">The following limitations apply:</span><span class="sxs-lookup"><span data-stu-id="a7ad1-147">The following limitations apply:</span></span>

* <span data-ttu-id="a7ad1-148">The array can have at most 10 elements.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-148">The array can have at most 10 elements.</span></span>
* <span data-ttu-id="a7ad1-149">The text value of an array element cannot exceed 100 characters including spaces.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-149">The text value of an array element cannot exceed 100 characters including spaces.</span></span>

## <a name="response-body"></a><span data-ttu-id="a7ad1-150">Response body</span><span class="sxs-lookup"><span data-stu-id="a7ad1-150">Response body</span></span>

<span data-ttu-id="a7ad1-151">A successful response is a JSON array with one result for each string in the input array.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-151">A successful response is a JSON array with one result for each string in the input array.</span></span> <span data-ttu-id="a7ad1-152">A result object includes the following properties:</span><span class="sxs-lookup"><span data-stu-id="a7ad1-152">A result object includes the following properties:</span></span>

  * <span data-ttu-id="a7ad1-153">`normalizedSource`: A string giving the normalized form of the source term.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-153">`normalizedSource`: A string giving the normalized form of the source term.</span></span> <span data-ttu-id="a7ad1-154">For example, if the request is "JOHN", the normalized form will be "john".</span><span class="sxs-lookup"><span data-stu-id="a7ad1-154">For example, if the request is "JOHN", the normalized form will be "john".</span></span> <span data-ttu-id="a7ad1-155">The content of this field becomes the input to [lookup examples](.\v3-0-dictionary-examples.md).</span><span class="sxs-lookup"><span data-stu-id="a7ad1-155">The content of this field becomes the input to [lookup examples](.\v3-0-dictionary-examples.md).</span></span>
    
  * <span data-ttu-id="a7ad1-156">`displaySource`: A string giving the source term in a form best suited for end-user display.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-156">`displaySource`: A string giving the source term in a form best suited for end-user display.</span></span> <span data-ttu-id="a7ad1-157">For example, if the input is "JOHN", the display form will reflect the usual spelling of the name: "John".</span><span class="sxs-lookup"><span data-stu-id="a7ad1-157">For example, if the input is "JOHN", the display form will reflect the usual spelling of the name: "John".</span></span> 

  * <span data-ttu-id="a7ad1-158">`translations`: A list of translations for the source term.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-158">`translations`: A list of translations for the source term.</span></span> <span data-ttu-id="a7ad1-159">Each element of the list is an object with the following properties:</span><span class="sxs-lookup"><span data-stu-id="a7ad1-159">Each element of the list is an object with the following properties:</span></span>

    * <span data-ttu-id="a7ad1-160">`normalizedTarget`: A string giving the normalized form of this term in the target language.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-160">`normalizedTarget`: A string giving the normalized form of this term in the target language.</span></span> <span data-ttu-id="a7ad1-161">This value should be used as input to [lookup examples](.\v3-0-dictionary-examples.md).</span><span class="sxs-lookup"><span data-stu-id="a7ad1-161">This value should be used as input to [lookup examples](.\v3-0-dictionary-examples.md).</span></span>

    * <span data-ttu-id="a7ad1-162">`displayTarget`: A string giving the term in the target language and in a form best suited for end-user display.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-162">`displayTarget`: A string giving the term in the target language and in a form best suited for end-user display.</span></span> <span data-ttu-id="a7ad1-163">Generally, this will only differ from the `normalizedTarget` in terms of capitalization.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-163">Generally, this will only differ from the `normalizedTarget` in terms of capitalization.</span></span> <span data-ttu-id="a7ad1-164">For example, a proper noun like "Juan" will have `normalizedTarget = "juan"` and `displayTarget = "Juan"`.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-164">For example, a proper noun like "Juan" will have `normalizedTarget = "juan"` and `displayTarget = "Juan"`.</span></span>

    * <span data-ttu-id="a7ad1-165">`posTag`: A string associating this term with a part-of-speech tag.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-165">`posTag`: A string associating this term with a part-of-speech tag.</span></span>

        | <span data-ttu-id="a7ad1-166">Tag name</span><span class="sxs-lookup"><span data-stu-id="a7ad1-166">Tag name</span></span> | <span data-ttu-id="a7ad1-167">Description</span><span class="sxs-lookup"><span data-stu-id="a7ad1-167">Description</span></span>  |
        |----------|--------------|
        | <span data-ttu-id="a7ad1-168">ADJ</span><span class="sxs-lookup"><span data-stu-id="a7ad1-168">ADJ</span></span>      | <span data-ttu-id="a7ad1-169">Adjectives</span><span class="sxs-lookup"><span data-stu-id="a7ad1-169">Adjectives</span></span>   |
        | <span data-ttu-id="a7ad1-170">ADV</span><span class="sxs-lookup"><span data-stu-id="a7ad1-170">ADV</span></span>      | <span data-ttu-id="a7ad1-171">Adverbs</span><span class="sxs-lookup"><span data-stu-id="a7ad1-171">Adverbs</span></span>      |
        | <span data-ttu-id="a7ad1-172">CONJ</span><span class="sxs-lookup"><span data-stu-id="a7ad1-172">CONJ</span></span>     | <span data-ttu-id="a7ad1-173">Conjunctions</span><span class="sxs-lookup"><span data-stu-id="a7ad1-173">Conjunctions</span></span> |
        | <span data-ttu-id="a7ad1-174">DET</span><span class="sxs-lookup"><span data-stu-id="a7ad1-174">DET</span></span>      | <span data-ttu-id="a7ad1-175">Determiners</span><span class="sxs-lookup"><span data-stu-id="a7ad1-175">Determiners</span></span>  |
        | <span data-ttu-id="a7ad1-176">MODAL</span><span class="sxs-lookup"><span data-stu-id="a7ad1-176">MODAL</span></span>    | <span data-ttu-id="a7ad1-177">Verbs</span><span class="sxs-lookup"><span data-stu-id="a7ad1-177">Verbs</span></span>        |
        | <span data-ttu-id="a7ad1-178">NOUN</span><span class="sxs-lookup"><span data-stu-id="a7ad1-178">NOUN</span></span>     | <span data-ttu-id="a7ad1-179">Nouns</span><span class="sxs-lookup"><span data-stu-id="a7ad1-179">Nouns</span></span>        |
        | <span data-ttu-id="a7ad1-180">PREP</span><span class="sxs-lookup"><span data-stu-id="a7ad1-180">PREP</span></span>     | <span data-ttu-id="a7ad1-181">Prepositions</span><span class="sxs-lookup"><span data-stu-id="a7ad1-181">Prepositions</span></span> |
        | <span data-ttu-id="a7ad1-182">PRON</span><span class="sxs-lookup"><span data-stu-id="a7ad1-182">PRON</span></span>     | <span data-ttu-id="a7ad1-183">Pronouns</span><span class="sxs-lookup"><span data-stu-id="a7ad1-183">Pronouns</span></span>     |
        | <span data-ttu-id="a7ad1-184">VERB</span><span class="sxs-lookup"><span data-stu-id="a7ad1-184">VERB</span></span>     | <span data-ttu-id="a7ad1-185">Verbs</span><span class="sxs-lookup"><span data-stu-id="a7ad1-185">Verbs</span></span>        |
        | <span data-ttu-id="a7ad1-186">OTHER</span><span class="sxs-lookup"><span data-stu-id="a7ad1-186">OTHER</span></span>    | <span data-ttu-id="a7ad1-187">Other</span><span class="sxs-lookup"><span data-stu-id="a7ad1-187">Other</span></span>        |

        <span data-ttu-id="a7ad1-188">As an implementation note, these tags were determined by part-of-speech tagging the English side, and then taking the most frequent tag for each source/target pair.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-188">As an implementation note, these tags were determined by part-of-speech tagging the English side, and then taking the most frequent tag for each source/target pair.</span></span> <span data-ttu-id="a7ad1-189">So if people frequently translate a Spanish word to a different part-of-speech tag in English, tags may end up being wrong (with respect to the Spanish word).</span><span class="sxs-lookup"><span data-stu-id="a7ad1-189">So if people frequently translate a Spanish word to a different part-of-speech tag in English, tags may end up being wrong (with respect to the Spanish word).</span></span>

    * <span data-ttu-id="a7ad1-190">`confidence`: A value between 0.0 and 1.0 which represents the "confidence" (or perhaps more accurately, "probability in the training data") of that translation pair.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-190">`confidence`: A value between 0.0 and 1.0 which represents the "confidence" (or perhaps more accurately, "probability in the training data") of that translation pair.</span></span> <span data-ttu-id="a7ad1-191">The sum of confidence scores for one source word may or may not sum to 1.0.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-191">The sum of confidence scores for one source word may or may not sum to 1.0.</span></span> 

    * <span data-ttu-id="a7ad1-192">`prefixWord`: A string giving the word to display as a prefix of the translation.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-192">`prefixWord`: A string giving the word to display as a prefix of the translation.</span></span> <span data-ttu-id="a7ad1-193">Currently, this is the gendered determiner of nouns, in languages that have gendered determiners.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-193">Currently, this is the gendered determiner of nouns, in languages that have gendered determiners.</span></span> <span data-ttu-id="a7ad1-194">For example, the prefix of the Spanish word "mosca" is "la", since "mosca" is a feminine noun in Spanish.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-194">For example, the prefix of the Spanish word "mosca" is "la", since "mosca" is a feminine noun in Spanish.</span></span> <span data-ttu-id="a7ad1-195">This is only dependent on the translation, and not on the source.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-195">This is only dependent on the translation, and not on the source.</span></span> <span data-ttu-id="a7ad1-196">If there is no prefix, it will be the empty string.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-196">If there is no prefix, it will be the empty string.</span></span>
    
    * <span data-ttu-id="a7ad1-197">`backTranslations`: A list of "back translations" of the target.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-197">`backTranslations`: A list of "back translations" of the target.</span></span> <span data-ttu-id="a7ad1-198">For example, source words that the target can translate to.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-198">For example, source words that the target can translate to.</span></span> <span data-ttu-id="a7ad1-199">The list is guaranteed to contain the source word that was requested (e.g., if the source word being looked up is "fly", then it is guaranteed that "fly" will be in the `backTranslations` list).</span><span class="sxs-lookup"><span data-stu-id="a7ad1-199">The list is guaranteed to contain the source word that was requested (e.g., if the source word being looked up is "fly", then it is guaranteed that "fly" will be in the `backTranslations` list).</span></span> <span data-ttu-id="a7ad1-200">However, it is not guaranteed to be in the first position, and often will not be.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-200">However, it is not guaranteed to be in the first position, and often will not be.</span></span> <span data-ttu-id="a7ad1-201">Each element of the `backTranslations` list is an object described by the following properties:</span><span class="sxs-lookup"><span data-stu-id="a7ad1-201">Each element of the `backTranslations` list is an object described by the following properties:</span></span>

        * <span data-ttu-id="a7ad1-202">`normalizedText`: A string giving the normalized form of the source term that is a back-translation of the target.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-202">`normalizedText`: A string giving the normalized form of the source term that is a back-translation of the target.</span></span> <span data-ttu-id="a7ad1-203">This value should be used as input to [lookup examples](.\v3-0-dictionary-examples.md).</span><span class="sxs-lookup"><span data-stu-id="a7ad1-203">This value should be used as input to [lookup examples](.\v3-0-dictionary-examples.md).</span></span>        

        * <span data-ttu-id="a7ad1-204">`displayText`: A string giving the source term that is a back-translation of the target in a form best suited for end-user display.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-204">`displayText`: A string giving the source term that is a back-translation of the target in a form best suited for end-user display.</span></span>

        * <span data-ttu-id="a7ad1-205">`numExamples`: An integer representing the number of examples that are available for this translation pair.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-205">`numExamples`: An integer representing the number of examples that are available for this translation pair.</span></span> <span data-ttu-id="a7ad1-206">Actual examples must be retrieved with a separate call to [lookup examples](.\v3-0-dictionary-examples.md).</span><span class="sxs-lookup"><span data-stu-id="a7ad1-206">Actual examples must be retrieved with a separate call to [lookup examples](.\v3-0-dictionary-examples.md).</span></span> <span data-ttu-id="a7ad1-207">The number is mostly intended to facilitate display in a UX.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-207">The number is mostly intended to facilitate display in a UX.</span></span> <span data-ttu-id="a7ad1-208">For example, a user interface may add a hyperlink to the back-translation if the number of examples is greater than zero and show the back-translation as plain text if there are no examples.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-208">For example, a user interface may add a hyperlink to the back-translation if the number of examples is greater than zero and show the back-translation as plain text if there are no examples.</span></span> <span data-ttu-id="a7ad1-209">Note that the actual number of examples returned by a call to [lookup examples](.\v3-0-dictionary-examples.md) may be less than `numExamples`, because additional filtering may be applied on the fly to remove "bad" examples.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-209">Note that the actual number of examples returned by a call to [lookup examples](.\v3-0-dictionary-examples.md) may be less than `numExamples`, because additional filtering may be applied on the fly to remove "bad" examples.</span></span>
        
        * <span data-ttu-id="a7ad1-210">`frequencyCount`: An integer representing the frequency of this translation pair in the data.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-210">`frequencyCount`: An integer representing the frequency of this translation pair in the data.</span></span> <span data-ttu-id="a7ad1-211">The main purpose of this field is to provide a user interface with a means to sort back-translations so the most frequent terms are first.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-211">The main purpose of this field is to provide a user interface with a means to sort back-translations so the most frequent terms are first.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a7ad1-212">If the term being looked-up does not exist in the dictionary, the response is 200 (OK) but the `translations` list is an empty list.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-212">If the term being looked-up does not exist in the dictionary, the response is 200 (OK) but the `translations` list is an empty list.</span></span>

## <a name="examples"></a><span data-ttu-id="a7ad1-213">Examples</span><span class="sxs-lookup"><span data-stu-id="a7ad1-213">Examples</span></span>

<span data-ttu-id="a7ad1-214">This example shows how to lookup alternative translations in Spanish of the English term `fly` .</span><span class="sxs-lookup"><span data-stu-id="a7ad1-214">This example shows how to lookup alternative translations in Spanish of the English term `fly` .</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="a7ad1-215">curl</span><span class="sxs-lookup"><span data-stu-id="a7ad1-215">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/dictionary/lookup?api-version=3.0&from=en&to=es" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'fly'}]"
```

---

<span data-ttu-id="a7ad1-216">The response body (abbreviated for clarity) is:</span><span class="sxs-lookup"><span data-stu-id="a7ad1-216">The response body (abbreviated for clarity) is:</span></span>

```
[
    {
        "normalizedSource":"fly",
        "displaySource":"fly",
        "translations":[
            {
                "normalizedTarget":"volar",
                "displayTarget":"volar",
                "posTag":"VERB",
                "confidence":0.4081,
                "prefixWord":"",
                "backTranslations":[
                    {"normalizedText":"fly","displayText":"fly","numExamples":15,"frequencyCount":4637},
                    {"normalizedText":"flying","displayText":"flying","numExamples":15,"frequencyCount":1365},
                    {"normalizedText":"blow","displayText":"blow","numExamples":15,"frequencyCount":503},
                    {"normalizedText":"flight","displayText":"flight","numExamples":15,"frequencyCount":135}
                ]
            },
            {
                "normalizedTarget":"mosca",
                "displayTarget":"mosca",
                "posTag":"NOUN",
                "confidence":0.2668,
                "prefixWord":"",
                "backTranslations":[
                    {"normalizedText":"fly","displayText":"fly","numExamples":15,"frequencyCount":1697},
                    {"normalizedText":"flyweight","displayText":"flyweight","numExamples":0,"frequencyCount":48},
                    {"normalizedText":"flies","displayText":"flies","numExamples":9,"frequencyCount":34}
                ]
            },
            //
            // ...list abbreviated for documentation clarity
            //
        ]
    }
]
```

<span data-ttu-id="a7ad1-217">This example shows what happens when the term being looked up does not exist for the valid dictionary pair.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-217">This example shows what happens when the term being looked up does not exist for the valid dictionary pair.</span></span>

# <a name="curltabcurl"></a>[<span data-ttu-id="a7ad1-218">curl</span><span class="sxs-lookup"><span data-stu-id="a7ad1-218">curl</span></span>](#tab/curl)

```
curl -X POST "https://api.cognitive.microsofttranslator.com/dictionary/lookup?api-version=3.0&from=en&to=es" -H "X-ClientTraceId: 875030C7-5380-40B8-8A03-63DACCF69C11" -H "Ocp-Apim-Subscription-Key: <client-secret>" -H "Content-Type: application/json" -d "[{'Text':'fly123456'}]"
```

---

<span data-ttu-id="a7ad1-219">Since the term is not found in the dictionary, the response body includes an empty `translations` list.</span><span class="sxs-lookup"><span data-stu-id="a7ad1-219">Since the term is not found in the dictionary, the response body includes an empty `translations` list.</span></span>

```
[
    {
        "normalizedSource":"fly123456",
        "displaySource":"fly123456",
        "translations":[]
    }
]
```
