---
title: How-to language detection in Text Analytics REST API (Microsoft Cognitive Services on Azure) | Microsoft Docs
description: How to detect language using the Text Analytics REST API in Microsoft Cognitive Services on Azure in this walkthrough tutorial.
services: cognitive-services
author: HeidiSteen
manager: cgronlun
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: article
ms.date: 3/07/2018
ms.author: heidist
ms.openlocfilehash: f8e2d9a36533c298addcf42d3cb2061e9c2d1ac7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867996"
---
# <a name="how-to-detect-language-in-text-analytics"></a><span data-ttu-id="25e8b-103">How to detect language in Text Analytics</span><span class="sxs-lookup"><span data-stu-id="25e8b-103">How to detect language in Text Analytics</span></span>

<span data-ttu-id="25e8b-104">The [Language Detection API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7) evaluates text input and for each document and returns language identifiers with a score indicating the strength of the analysis.</span><span class="sxs-lookup"><span data-stu-id="25e8b-104">The [Language Detection API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7) evaluates text input and for each document and returns language identifiers with a score indicating the strength of the analysis.</span></span> <span data-ttu-id="25e8b-105">Text Analytics recognizes up to 120 languages.</span><span class="sxs-lookup"><span data-stu-id="25e8b-105">Text Analytics recognizes up to 120 languages.</span></span>

<span data-ttu-id="25e8b-106">This capability is useful for content stores that collect arbitrary text, where language is unknown.</span><span class="sxs-lookup"><span data-stu-id="25e8b-106">This capability is useful for content stores that collect arbitrary text, where language is unknown.</span></span> <span data-ttu-id="25e8b-107">You can parse the results of this analysis to determine which language is used in the input document.</span><span class="sxs-lookup"><span data-stu-id="25e8b-107">You can parse the results of this analysis to determine which language is used in the input document.</span></span> <span data-ttu-id="25e8b-108">The response also returns a score which reflects the confidence of the model (a value between 0 and 1).</span><span class="sxs-lookup"><span data-stu-id="25e8b-108">The response also returns a score which reflects the confidence of the model (a value between 0 and 1).</span></span>

## <a name="preparation"></a><span data-ttu-id="25e8b-109">Preparation</span><span class="sxs-lookup"><span data-stu-id="25e8b-109">Preparation</span></span>

<span data-ttu-id="25e8b-110">You must have JSON documents in this format: id, text</span><span class="sxs-lookup"><span data-stu-id="25e8b-110">You must have JSON documents in this format: id, text</span></span>

<span data-ttu-id="25e8b-111">Document size must be under 5,000 characters per document, and you can have up to 1,000 items (IDs) per collection.</span><span class="sxs-lookup"><span data-stu-id="25e8b-111">Document size must be under 5,000 characters per document, and you can have up to 1,000 items (IDs) per collection.</span></span> <span data-ttu-id="25e8b-112">The collection is submitted in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="25e8b-112">The collection is submitted in the body of the request.</span></span> <span data-ttu-id="25e8b-113">The following is an example of content you might submit for language detection.</span><span class="sxs-lookup"><span data-stu-id="25e8b-113">The following is an example of content you might submit for language detection.</span></span>

   ```
    {
        "documents": [
            {
                "id": "1",
                "text": "This document is in English."
            },
            {
                "id": "2",
                "text": "Este documento está en inglés."
            },
            {
                "id": "3",
                "text": "Ce document est en anglais."
            },
            {
                "id": "4",
                "text": "本文件为英文"
            },                
            {
                "id": "5",
                "text": "Этот документ находится на английском языке."
            }
        ]
    }
```

## <a name="step-1-structure-the-request"></a><span data-ttu-id="25e8b-114">Step 1: Structure the request</span><span class="sxs-lookup"><span data-stu-id="25e8b-114">Step 1: Structure the request</span></span>

<span data-ttu-id="25e8b-115">Details on request definition can be found in [How to call the Text Analytics API](text-analytics-how-to-call-api.md).</span><span class="sxs-lookup"><span data-stu-id="25e8b-115">Details on request definition can be found in [How to call the Text Analytics API](text-analytics-how-to-call-api.md).</span></span> <span data-ttu-id="25e8b-116">The following points are restated for convenience:</span><span class="sxs-lookup"><span data-stu-id="25e8b-116">The following points are restated for convenience:</span></span>

+ <span data-ttu-id="25e8b-117">Create a **POST** request.</span><span class="sxs-lookup"><span data-stu-id="25e8b-117">Create a **POST** request.</span></span> <span data-ttu-id="25e8b-118">Review the API documentation for this request: [Language Detection API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7)</span><span class="sxs-lookup"><span data-stu-id="25e8b-118">Review the API documentation for this request: [Language Detection API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7)</span></span>

+ <span data-ttu-id="25e8b-119">Set the HTTP endpoint for language detection.</span><span class="sxs-lookup"><span data-stu-id="25e8b-119">Set the HTTP endpoint for language detection.</span></span> <span data-ttu-id="25e8b-120">It must include the `/languages` resource: `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/languages`</span><span class="sxs-lookup"><span data-stu-id="25e8b-120">It must include the `/languages` resource: `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/languages`</span></span>

+ <span data-ttu-id="25e8b-121">Set a request header to include the access key for Text Analytics operations.</span><span class="sxs-lookup"><span data-stu-id="25e8b-121">Set a request header to include the access key for Text Analytics operations.</span></span> <span data-ttu-id="25e8b-122">For more information, see [How to find endpoints and access keys](text-analytics-how-to-access-key.md).</span><span class="sxs-lookup"><span data-stu-id="25e8b-122">For more information, see [How to find endpoints and access keys](text-analytics-how-to-access-key.md).</span></span>

+ <span data-ttu-id="25e8b-123">In the request body, provide the JSON documents collection you prepared for this analysis</span><span class="sxs-lookup"><span data-stu-id="25e8b-123">In the request body, provide the JSON documents collection you prepared for this analysis</span></span>

> [!Tip]
> <span data-ttu-id="25e8b-124">Use [Postman](text-analytics-how-to-call-api.md) or open the **API testing console** in the [documentation](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7) to structure a request and POST it to the service.</span><span class="sxs-lookup"><span data-stu-id="25e8b-124">Use [Postman](text-analytics-how-to-call-api.md) or open the **API testing console** in the [documentation](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7) to structure a request and POST it to the service.</span></span>

## <a name="step-2-post-the-request"></a><span data-ttu-id="25e8b-125">Step 2: Post the request</span><span class="sxs-lookup"><span data-stu-id="25e8b-125">Step 2: Post the request</span></span>

<span data-ttu-id="25e8b-126">Analysis is performed upon receipt of the request.</span><span class="sxs-lookup"><span data-stu-id="25e8b-126">Analysis is performed upon receipt of the request.</span></span> <span data-ttu-id="25e8b-127">The service accepts up to 100 requests per minute.</span><span class="sxs-lookup"><span data-stu-id="25e8b-127">The service accepts up to 100 requests per minute.</span></span> <span data-ttu-id="25e8b-128">Each request can be a maximum of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="25e8b-128">Each request can be a maximum of 1 MB.</span></span>

<span data-ttu-id="25e8b-129">Recall that the service is stateless.</span><span class="sxs-lookup"><span data-stu-id="25e8b-129">Recall that the service is stateless.</span></span> <span data-ttu-id="25e8b-130">No data is stored in your account.</span><span class="sxs-lookup"><span data-stu-id="25e8b-130">No data is stored in your account.</span></span> <span data-ttu-id="25e8b-131">Results are returned immediately in the response.</span><span class="sxs-lookup"><span data-stu-id="25e8b-131">Results are returned immediately in the response.</span></span>


## <a name="step-3-view-results"></a><span data-ttu-id="25e8b-132">Step 3: View results</span><span class="sxs-lookup"><span data-stu-id="25e8b-132">Step 3: View results</span></span>

<span data-ttu-id="25e8b-133">All POST requests return a JSON formatted response with the IDs and detected properties.</span><span class="sxs-lookup"><span data-stu-id="25e8b-133">All POST requests return a JSON formatted response with the IDs and detected properties.</span></span>

<span data-ttu-id="25e8b-134">Output is returned immediately.</span><span class="sxs-lookup"><span data-stu-id="25e8b-134">Output is returned immediately.</span></span> <span data-ttu-id="25e8b-135">You can stream the results to an application that accepts JSON or save the output to a file on the local system, and then import it into an application that allows you to sort, search, and manipulate the data.</span><span class="sxs-lookup"><span data-stu-id="25e8b-135">You can stream the results to an application that accepts JSON or save the output to a file on the local system, and then import it into an application that allows you to sort, search, and manipulate the data.</span></span>

<span data-ttu-id="25e8b-136">Results for the example request should look like the following JSON.</span><span class="sxs-lookup"><span data-stu-id="25e8b-136">Results for the example request should look like the following JSON.</span></span> <span data-ttu-id="25e8b-137">Notice that it is one document with multiple items.</span><span class="sxs-lookup"><span data-stu-id="25e8b-137">Notice that it is one document with multiple items.</span></span> <span data-ttu-id="25e8b-138">Output is in English.</span><span class="sxs-lookup"><span data-stu-id="25e8b-138">Output is in English.</span></span> <span data-ttu-id="25e8b-139">Language identifiers include a friendly name and a language code in [ISO 639-1](https://www.iso.org/standard/22109.html) format.</span><span class="sxs-lookup"><span data-stu-id="25e8b-139">Language identifiers include a friendly name and a language code in [ISO 639-1](https://www.iso.org/standard/22109.html) format.</span></span>

<span data-ttu-id="25e8b-140">A positive score of 1.0 expresses the highest possible confidence level of the analysis.</span><span class="sxs-lookup"><span data-stu-id="25e8b-140">A positive score of 1.0 expresses the highest possible confidence level of the analysis.</span></span>



```
{
    "documents": [
        {
            "id": "1",
            "detectedLanguages": [
                {
                    "name": "English",
                    "iso6391Name": "en",
                    "score": 1
                }
            ]
        },
        {
            "id": "2",
            "detectedLanguages": [
                {
                    "name": "Spanish",
                    "iso6391Name": "es",
                    "score": 1
                }
            ]
        },
        {
            "id": "3",
            "detectedLanguages": [
                {
                    "name": "French",
                    "iso6391Name": "fr",
                    "score": 1
                }
            ]
        },
        {
            "id": "4",
            "detectedLanguages": [
                {
                    "name": "Chinese_Simplified",
                    "iso6391Name": "zh_chs",
                    "score": 1
                }
            ]
        },
        {
            "id": "5",
            "detectedLanguages": [
                {
                    "name": "Russian",
                    "iso6391Name": "ru",
                    "score": 1
                }
            ]
        }
    ],
```

### <a name="ambiguous-content"></a><span data-ttu-id="25e8b-141">Ambiguous content</span><span class="sxs-lookup"><span data-stu-id="25e8b-141">Ambiguous content</span></span>

<span data-ttu-id="25e8b-142">If the analyzer cannot parse the input (for example, assume you submitted a text block consisting solely of Arabic numerals), it returns `(Unknown)`.</span><span class="sxs-lookup"><span data-stu-id="25e8b-142">If the analyzer cannot parse the input (for example, assume you submitted a text block consisting solely of Arabic numerals), it returns `(Unknown)`.</span></span>

```
    {
      "id": "5",
      "detectedLanguages": [
        {
          "name": "(Unknown)",
          "iso6391Name": "(Unknown)",
          "score": "NaN"
        }
      ]
```
### <a name="mixed-language-content"></a><span data-ttu-id="25e8b-143">Mixed language content</span><span class="sxs-lookup"><span data-stu-id="25e8b-143">Mixed language content</span></span>

<span data-ttu-id="25e8b-144">Mixed language content within the same document returns the language with the largest representation in the content, but with a lower positive rating, reflecting the marginal strength of that assessment.</span><span class="sxs-lookup"><span data-stu-id="25e8b-144">Mixed language content within the same document returns the language with the largest representation in the content, but with a lower positive rating, reflecting the marginal strength of that assessment.</span></span> <span data-ttu-id="25e8b-145">In the following example, input is a blend of English, Spanish, and French.</span><span class="sxs-lookup"><span data-stu-id="25e8b-145">In the following example, input is a blend of English, Spanish, and French.</span></span> <span data-ttu-id="25e8b-146">The analyzer counts characters in each segment to determine the predominant language.</span><span class="sxs-lookup"><span data-stu-id="25e8b-146">The analyzer counts characters in each segment to determine the predominant language.</span></span>

<span data-ttu-id="25e8b-147">**Input**</span><span class="sxs-lookup"><span data-stu-id="25e8b-147">**Input**</span></span>

```
{
  "documents": [
    {
      "id": "1",
      "text": "Hello, I would like to take a class at your University. ¿Se ofrecen clases en español? Es mi primera lengua y más fácil para escribir. Que diriez-vous des cours en français?"
    }
  ]
}
```

<span data-ttu-id="25e8b-148">**Output**</span><span class="sxs-lookup"><span data-stu-id="25e8b-148">**Output**</span></span>

<span data-ttu-id="25e8b-149">Resulting output consists of the predominant language, with a score of less than 1.0, indicating a weaker level of confidence.</span><span class="sxs-lookup"><span data-stu-id="25e8b-149">Resulting output consists of the predominant language, with a score of less than 1.0, indicating a weaker level of confidence.</span></span>

```
{
  "documents": [
    {
      "id": "1",
      "detectedLanguages": [
        {
          "name": "Spanish",
          "iso6391Name": "es",
          "score": 0.9375
        }
      ]
    }
  ],
  "errors": []
}
```

## <a name="summary"></a><span data-ttu-id="25e8b-150">Summary</span><span class="sxs-lookup"><span data-stu-id="25e8b-150">Summary</span></span>

<span data-ttu-id="25e8b-151">In this article, you learned concepts and workflow for language detection using Text Analytics in Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="25e8b-151">In this article, you learned concepts and workflow for language detection using Text Analytics in Cognitive Services.</span></span> <span data-ttu-id="25e8b-152">The following are a quick reminder of the main points previously explained and demonstrated:</span><span class="sxs-lookup"><span data-stu-id="25e8b-152">The following are a quick reminder of the main points previously explained and demonstrated:</span></span>

+ <span data-ttu-id="25e8b-153">[Language detection API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7) is available for 120 languages.</span><span class="sxs-lookup"><span data-stu-id="25e8b-153">[Language detection API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c7) is available for 120 languages.</span></span>
+ <span data-ttu-id="25e8b-154">JSON documents in the request body include an id and text.</span><span class="sxs-lookup"><span data-stu-id="25e8b-154">JSON documents in the request body include an id and text.</span></span>
+ <span data-ttu-id="25e8b-155">POST request is to a `/languages` endpoint, using a personalized [access key and an endpoint](text-analytics-how-to-access-key.md) that is valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="25e8b-155">POST request is to a `/languages` endpoint, using a personalized [access key and an endpoint](text-analytics-how-to-access-key.md) that is valid for your subscription.</span></span>
+ <span data-ttu-id="25e8b-156">Response output, which consists of language identifiers for each document ID, can be streamed to any app that accepts JSON, including Excel and Power BI, to name a few.</span><span class="sxs-lookup"><span data-stu-id="25e8b-156">Response output, which consists of language identifiers for each document ID, can be streamed to any app that accepts JSON, including Excel and Power BI, to name a few.</span></span>

## <a name="see-also"></a><span data-ttu-id="25e8b-157">See also</span><span class="sxs-lookup"><span data-stu-id="25e8b-157">See also</span></span> 

 [<span data-ttu-id="25e8b-158">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="25e8b-158">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="25e8b-159">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="25e8b-159">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)</br>
 [<span data-ttu-id="25e8b-160">Text Analytics product page</span><span class="sxs-lookup"><span data-stu-id="25e8b-160">Text Analytics product page</span></span>](//go.microsoft.com/fwlink/?LinkID=759712) 

## <a name="next-steps"></a><span data-ttu-id="25e8b-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="25e8b-161">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="25e8b-162">Analyze sentiment</span><span class="sxs-lookup"><span data-stu-id="25e8b-162">Analyze sentiment</span></span>](text-analytics-how-to-sentiment-analysis.md)
