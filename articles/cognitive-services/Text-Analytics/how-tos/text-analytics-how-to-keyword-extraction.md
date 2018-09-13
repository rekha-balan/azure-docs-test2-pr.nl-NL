---
title: How-to key phrase extraction in Text Analytics REST API (Microsoft Cognitive Services on Azure) | Microsoft Docs
description: How to extract key phrases using the Text Analytics REST API in Microsoft Cognitive Services on Azure in this walkthrough tutorial.
services: cognitive-services
author: HeidiSteen
manager: cgronlun
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: article
ms.date: 3/07/2018
ms.author: heidist
ms.openlocfilehash: 78b100e737242fa9f56e50275ef2038d8895349e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871210"
---
# <a name="how-to-extract-key-phrases-in-text-analytics"></a><span data-ttu-id="7608b-103">How to extract key phrases in Text Analytics</span><span class="sxs-lookup"><span data-stu-id="7608b-103">How to extract key phrases in Text Analytics</span></span>

<span data-ttu-id="7608b-104">The [Key Phrase Extraction API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) evaluates unstructured text, and for each JSON document, returns a list of key phrases.</span><span class="sxs-lookup"><span data-stu-id="7608b-104">The [Key Phrase Extraction API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) evaluates unstructured text, and for each JSON document, returns a list of key phrases.</span></span> 

<span data-ttu-id="7608b-105">This capability is useful if you need to quickly identify the main points in a collection of documents.</span><span class="sxs-lookup"><span data-stu-id="7608b-105">This capability is useful if you need to quickly identify the main points in a collection of documents.</span></span> <span data-ttu-id="7608b-106">For example, given input text "The food was delicious and there were wonderful staff", the service returns the main talking points: "food" and "wonderful staff".</span><span class="sxs-lookup"><span data-stu-id="7608b-106">For example, given input text "The food was delicious and there were wonderful staff", the service returns the main talking points: "food" and "wonderful staff".</span></span>

<span data-ttu-id="7608b-107">Currently, Key Phrase Extraction supports English, German, Spanish, and Japanese.</span><span class="sxs-lookup"><span data-stu-id="7608b-107">Currently, Key Phrase Extraction supports English, German, Spanish, and Japanese.</span></span> <span data-ttu-id="7608b-108">Other languages are in preview.</span><span class="sxs-lookup"><span data-stu-id="7608b-108">Other languages are in preview.</span></span> <span data-ttu-id="7608b-109">For more information, see [Supported languages](../text-analytics-supported-languages.md).</span><span class="sxs-lookup"><span data-stu-id="7608b-109">For more information, see [Supported languages](../text-analytics-supported-languages.md).</span></span>

## <a name="preparation"></a><span data-ttu-id="7608b-110">Preparation</span><span class="sxs-lookup"><span data-stu-id="7608b-110">Preparation</span></span>

<span data-ttu-id="7608b-111">Key phrase extraction works best when you give it bigger chunks of text to work on.</span><span class="sxs-lookup"><span data-stu-id="7608b-111">Key phrase extraction works best when you give it bigger chunks of text to work on.</span></span> <span data-ttu-id="7608b-112">This is opposite from sentiment analysis, which performs better on smaller blocks of text.</span><span class="sxs-lookup"><span data-stu-id="7608b-112">This is opposite from sentiment analysis, which performs better on smaller blocks of text.</span></span> <span data-ttu-id="7608b-113">To get the best results from both operations, consider restructuring the inputs accordingly.</span><span class="sxs-lookup"><span data-stu-id="7608b-113">To get the best results from both operations, consider restructuring the inputs accordingly.</span></span>

<span data-ttu-id="7608b-114">You must have JSON documents in this format: id, text, language</span><span class="sxs-lookup"><span data-stu-id="7608b-114">You must have JSON documents in this format: id, text, language</span></span>

<span data-ttu-id="7608b-115">Document size must be under 5,000 characters per document, and you can have up to 1,000 items (IDs) per collection.</span><span class="sxs-lookup"><span data-stu-id="7608b-115">Document size must be under 5,000 characters per document, and you can have up to 1,000 items (IDs) per collection.</span></span> <span data-ttu-id="7608b-116">The collection is submitted in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="7608b-116">The collection is submitted in the body of the request.</span></span> <span data-ttu-id="7608b-117">The following example is an illustration of content you might submit for key phrase extraction.</span><span class="sxs-lookup"><span data-stu-id="7608b-117">The following example is an illustration of content you might submit for key phrase extraction.</span></span>

```
    {
        "documents": [
            {
                "language": "en",
                "id": "1",
                "text": "We love this trail and make the trip every year. The views are breathtaking and well worth the hike!"
            },
            {
                "language": "en",
                "id": "2",
                "text": "Poorly marked trails! I thought we were goners. Worst hike ever."
            },
            {
                "language": "en",
                "id": "3",
                "text": "Everyone in my family liked the trail but thought it was too challenging for the less athletic among us. Not necessarily recommended for small children."
            },
            {
                "language": "en",
                "id": "4",
                "text": "It was foggy so we missed the spectacular views, but the trail was ok. Worth checking out if you are in the area."
            },                
            {
                "language": "en",
                "id": "5",
                "text": "This is my favorite trail. It has beautiful views and many places to stop and rest"
            }
        ]
    }
```    
    
## <a name="step-1-structure-the-request"></a><span data-ttu-id="7608b-118">Step 1: Structure the request</span><span class="sxs-lookup"><span data-stu-id="7608b-118">Step 1: Structure the request</span></span>

<span data-ttu-id="7608b-119">Details on request definition can be found in [How to call the Text Analytics API](text-analytics-how-to-call-api.md).</span><span class="sxs-lookup"><span data-stu-id="7608b-119">Details on request definition can be found in [How to call the Text Analytics API](text-analytics-how-to-call-api.md).</span></span> <span data-ttu-id="7608b-120">The following points are restated for convenience:</span><span class="sxs-lookup"><span data-stu-id="7608b-120">The following points are restated for convenience:</span></span>

+ <span data-ttu-id="7608b-121">Create a **POST** request.</span><span class="sxs-lookup"><span data-stu-id="7608b-121">Create a **POST** request.</span></span> <span data-ttu-id="7608b-122">Review the API documentation for this request: [Key Phrases API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6)</span><span class="sxs-lookup"><span data-stu-id="7608b-122">Review the API documentation for this request: [Key Phrases API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6)</span></span>

+ <span data-ttu-id="7608b-123">Set the HTTP endpoint for key phrase extraction.</span><span class="sxs-lookup"><span data-stu-id="7608b-123">Set the HTTP endpoint for key phrase extraction.</span></span> <span data-ttu-id="7608b-124">It must include the `/keyphrases` resource: `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases`</span><span class="sxs-lookup"><span data-stu-id="7608b-124">It must include the `/keyphrases` resource: `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases`</span></span>

+ <span data-ttu-id="7608b-125">Set a request header to include the access key for Text Analytics operations.</span><span class="sxs-lookup"><span data-stu-id="7608b-125">Set a request header to include the access key for Text Analytics operations.</span></span> <span data-ttu-id="7608b-126">For more information, see [How to find endpoints and access keys](text-analytics-how-to-access-key.md).</span><span class="sxs-lookup"><span data-stu-id="7608b-126">For more information, see [How to find endpoints and access keys](text-analytics-how-to-access-key.md).</span></span>

+ <span data-ttu-id="7608b-127">In the request body, provide the JSON documents collection you prepared for this analysis</span><span class="sxs-lookup"><span data-stu-id="7608b-127">In the request body, provide the JSON documents collection you prepared for this analysis</span></span>

> [!Tip]
> <span data-ttu-id="7608b-128">Use [Postman](text-analytics-how-to-call-api.md) or open the **API testing console** in the [documentation](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) to structure a request and POST it to the service.</span><span class="sxs-lookup"><span data-stu-id="7608b-128">Use [Postman](text-analytics-how-to-call-api.md) or open the **API testing console** in the [documentation](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) to structure a request and POST it to the service.</span></span>

## <a name="step-2-post-the-request"></a><span data-ttu-id="7608b-129">Step 2: Post the request</span><span class="sxs-lookup"><span data-stu-id="7608b-129">Step 2: Post the request</span></span>

<span data-ttu-id="7608b-130">Analysis is performed upon receipt of the request.</span><span class="sxs-lookup"><span data-stu-id="7608b-130">Analysis is performed upon receipt of the request.</span></span> <span data-ttu-id="7608b-131">The service accepts up to 100 requests per minute.</span><span class="sxs-lookup"><span data-stu-id="7608b-131">The service accepts up to 100 requests per minute.</span></span> <span data-ttu-id="7608b-132">Each request can be a maximum of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="7608b-132">Each request can be a maximum of 1 MB.</span></span>

<span data-ttu-id="7608b-133">Recall that the service is stateless.</span><span class="sxs-lookup"><span data-stu-id="7608b-133">Recall that the service is stateless.</span></span> <span data-ttu-id="7608b-134">No data is stored in your account.</span><span class="sxs-lookup"><span data-stu-id="7608b-134">No data is stored in your account.</span></span> <span data-ttu-id="7608b-135">Results are returned immediately in the response.</span><span class="sxs-lookup"><span data-stu-id="7608b-135">Results are returned immediately in the response.</span></span>

## <a name="step-3-view-results"></a><span data-ttu-id="7608b-136">Step 3: View results</span><span class="sxs-lookup"><span data-stu-id="7608b-136">Step 3: View results</span></span>

<span data-ttu-id="7608b-137">All POST requests return a JSON formatted response with the IDs and detected properties.</span><span class="sxs-lookup"><span data-stu-id="7608b-137">All POST requests return a JSON formatted response with the IDs and detected properties.</span></span>

<span data-ttu-id="7608b-138">Output is returned immediately.</span><span class="sxs-lookup"><span data-stu-id="7608b-138">Output is returned immediately.</span></span> <span data-ttu-id="7608b-139">You can stream the results to an application that accepts JSON or save the output to a file on the local system, and then import it into an application that allows you to sort, search, and manipulate the data.</span><span class="sxs-lookup"><span data-stu-id="7608b-139">You can stream the results to an application that accepts JSON or save the output to a file on the local system, and then import it into an application that allows you to sort, search, and manipulate the data.</span></span>

<span data-ttu-id="7608b-140">An example of the output for key phrase extraction is shown next:</span><span class="sxs-lookup"><span data-stu-id="7608b-140">An example of the output for key phrase extraction is shown next:</span></span>

```
    "documents": [
        {
            "keyPhrases": [
                "year",
                "trail",
                "trip",
                "views"
            ],
            "id": "1"
        },
        {
            "keyPhrases": [
                "marked trails",
                "Worst hike",
                "goners"
            ],
            "id": "2"
        },
        {
            "keyPhrases": [
                "trail",
                "small children",
                "family"
            ],
            "id": "3"
        },
        {
            "keyPhrases": [
                "spectacular views",
                "trail",
                "area"
            ],
            "id": "4"
        },
        {
            "keyPhrases": [
                "places",
                "beautiful views",
                "favorite trail"
            ],
            "id": "5"
        }
```

<span data-ttu-id="7608b-141">As noted, the analyzer finds and discards non-essential words, and keeps single terms or phrases that appear to be the subject or object of a sentence.</span><span class="sxs-lookup"><span data-stu-id="7608b-141">As noted, the analyzer finds and discards non-essential words, and keeps single terms or phrases that appear to be the subject or object of a sentence.</span></span> 

## <a name="summary"></a><span data-ttu-id="7608b-142">Summary</span><span class="sxs-lookup"><span data-stu-id="7608b-142">Summary</span></span>

<span data-ttu-id="7608b-143">In this article, you learned concepts and workflow for key phrase extraction using Text Analytics in Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="7608b-143">In this article, you learned concepts and workflow for key phrase extraction using Text Analytics in Cognitive Services.</span></span> <span data-ttu-id="7608b-144">In summary:</span><span class="sxs-lookup"><span data-stu-id="7608b-144">In summary:</span></span>

+ <span data-ttu-id="7608b-145">[Key phrase extraction API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) is available for selected languages.</span><span class="sxs-lookup"><span data-stu-id="7608b-145">[Key phrase extraction API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6) is available for selected languages.</span></span>
+ <span data-ttu-id="7608b-146">JSON documents in the request body include an id, text, and language code.</span><span class="sxs-lookup"><span data-stu-id="7608b-146">JSON documents in the request body include an id, text, and language code.</span></span>
+ <span data-ttu-id="7608b-147">POST request is to a `/keyphrases` endpoint, using a personalized [access key and an endpoint](text-analytics-how-to-access-key.md) that is valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="7608b-147">POST request is to a `/keyphrases` endpoint, using a personalized [access key and an endpoint](text-analytics-how-to-access-key.md) that is valid for your subscription.</span></span>
+ <span data-ttu-id="7608b-148">Response output, which consists of key words and phrases for each document ID, can be streamed to any app that accepts JSON, including Excel and Power BI, to name a few.</span><span class="sxs-lookup"><span data-stu-id="7608b-148">Response output, which consists of key words and phrases for each document ID, can be streamed to any app that accepts JSON, including Excel and Power BI, to name a few.</span></span>

## <a name="see-also"></a><span data-ttu-id="7608b-149">See also</span><span class="sxs-lookup"><span data-stu-id="7608b-149">See also</span></span> 

 [<span data-ttu-id="7608b-150">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="7608b-150">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="7608b-151">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="7608b-151">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)</br>
 [<span data-ttu-id="7608b-152">Text Analytics product page</span><span class="sxs-lookup"><span data-stu-id="7608b-152">Text Analytics product page</span></span>](//go.microsoft.com/fwlink/?LinkID=759712) 

## <a name="next-steps"></a><span data-ttu-id="7608b-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="7608b-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7608b-154">Text Analytics API</span><span class="sxs-lookup"><span data-stu-id="7608b-154">Text Analytics API</span></span>](//westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6)
