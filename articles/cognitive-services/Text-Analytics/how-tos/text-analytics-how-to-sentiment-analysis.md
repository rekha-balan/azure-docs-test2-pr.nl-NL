---
title: How-to sentiment analysis in Text Analytics REST API (Microsoft Cognitive Services on Azure) | Microsoft Docs
description: How to detect sentiment  using the Text Analytics REST API in Microsoft Cognitive Services on Azure in this walkthrough tutorial.
services: cognitive-services
author: HeidiSteen
manager: cgronlun
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: article
ms.date: 12/11/2017
ms.author: heidist
ms.openlocfilehash: 7ffd8bbe47409b459fdd308cd8d670d32f56649b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868717"
---
# <a name="how-to-detect-sentiment-in-text-analytics"></a><span data-ttu-id="040e3-103">How to detect sentiment in Text Analytics</span><span class="sxs-lookup"><span data-stu-id="040e3-103">How to detect sentiment in Text Analytics</span></span>

<span data-ttu-id="040e3-104">The [Sentiment Analysis API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9) evaluates text input and returns a sentiment score for each document, ranging from 0 (negative) to 1 (positive).</span><span class="sxs-lookup"><span data-stu-id="040e3-104">The [Sentiment Analysis API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9) evaluates text input and returns a sentiment score for each document, ranging from 0 (negative) to 1 (positive).</span></span>

<span data-ttu-id="040e3-105">This capability is useful for detecting positive and negative sentiment in social media, customer reviews, and discussion forums.</span><span class="sxs-lookup"><span data-stu-id="040e3-105">This capability is useful for detecting positive and negative sentiment in social media, customer reviews, and discussion forums.</span></span> <span data-ttu-id="040e3-106">Content is provided by you; models and training data are provided by the service.</span><span class="sxs-lookup"><span data-stu-id="040e3-106">Content is provided by you; models and training data are provided by the service.</span></span>

<span data-ttu-id="040e3-107">Currently, Sentiment Analysis supports English, German, Spanish, and French.</span><span class="sxs-lookup"><span data-stu-id="040e3-107">Currently, Sentiment Analysis supports English, German, Spanish, and French.</span></span> <span data-ttu-id="040e3-108">Other languages are in preview.</span><span class="sxs-lookup"><span data-stu-id="040e3-108">Other languages are in preview.</span></span> <span data-ttu-id="040e3-109">For more information, see [Supported languages](../text-analytics-supported-languages.md).</span><span class="sxs-lookup"><span data-stu-id="040e3-109">For more information, see [Supported languages](../text-analytics-supported-languages.md).</span></span>

## <a name="concepts"></a><span data-ttu-id="040e3-110">Concepts</span><span class="sxs-lookup"><span data-stu-id="040e3-110">Concepts</span></span>

<span data-ttu-id="040e3-111">Text Analytics uses a machine learning classification algorithm to generate a sentiment score between 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="040e3-111">Text Analytics uses a machine learning classification algorithm to generate a sentiment score between 0 and 1.</span></span> <span data-ttu-id="040e3-112">Scores closer to 1 indicate positive sentiment, while scores closer to 0 indicate negative sentiment.</span><span class="sxs-lookup"><span data-stu-id="040e3-112">Scores closer to 1 indicate positive sentiment, while scores closer to 0 indicate negative sentiment.</span></span> <span data-ttu-id="040e3-113">The model is pretrained with an extensive body of text with sentiment associations.</span><span class="sxs-lookup"><span data-stu-id="040e3-113">The model is pretrained with an extensive body of text with sentiment associations.</span></span> <span data-ttu-id="040e3-114">Currently, it is not possible to provide your own training data.</span><span class="sxs-lookup"><span data-stu-id="040e3-114">Currently, it is not possible to provide your own training data.</span></span> <span data-ttu-id="040e3-115">The model uses a combination of techniques during text analysis, including text processing, part-of-speech analysis, word placement, and word associations.</span><span class="sxs-lookup"><span data-stu-id="040e3-115">The model uses a combination of techniques during text analysis, including text processing, part-of-speech analysis, word placement, and word associations.</span></span> <span data-ttu-id="040e3-116">For more information about the algorithm, see [Introducing Text Analytics](https://blogs.technet.microsoft.com/machinelearning/2015/04/08/introducing-text-analytics-in-the-azure-ml-marketplace/).</span><span class="sxs-lookup"><span data-stu-id="040e3-116">For more information about the algorithm, see [Introducing Text Analytics](https://blogs.technet.microsoft.com/machinelearning/2015/04/08/introducing-text-analytics-in-the-azure-ml-marketplace/).</span></span>

<span data-ttu-id="040e3-117">Sentiment analysis is performed on the entire document, as opposed to extracting sentiment for a particular entity in the text.</span><span class="sxs-lookup"><span data-stu-id="040e3-117">Sentiment analysis is performed on the entire document, as opposed to extracting sentiment for a particular entity in the text.</span></span> <span data-ttu-id="040e3-118">In practice, there is a tendency for scoring accuracy to improve when documents contain one or two sentences rather than a large block of text.</span><span class="sxs-lookup"><span data-stu-id="040e3-118">In practice, there is a tendency for scoring accuracy to improve when documents contain one or two sentences rather than a large block of text.</span></span> <span data-ttu-id="040e3-119">During an objectivity assessment phase, the model determines whether a document as a whole is objective or contains sentiment.</span><span class="sxs-lookup"><span data-stu-id="040e3-119">During an objectivity assessment phase, the model determines whether a document as a whole is objective or contains sentiment.</span></span> <span data-ttu-id="040e3-120">A document that is mostly objective does not progress to the sentiment detection phrase, resulting in a .50 score, with no further processing.</span><span class="sxs-lookup"><span data-stu-id="040e3-120">A document that is mostly objective does not progress to the sentiment detection phrase, resulting in a .50 score, with no further processing.</span></span> <span data-ttu-id="040e3-121">For documents continuing in the pipeline, the next phase generates a score above or below .50, depending on the degree of sentiment detected in the document.</span><span class="sxs-lookup"><span data-stu-id="040e3-121">For documents continuing in the pipeline, the next phase generates a score above or below .50, depending on the degree of sentiment detected in the document.</span></span>

## <a name="preparation"></a><span data-ttu-id="040e3-122">Preparation</span><span class="sxs-lookup"><span data-stu-id="040e3-122">Preparation</span></span>

<span data-ttu-id="040e3-123">Sentiment analysis produces a higher quality result when you give it smaller chunks of text to work on.</span><span class="sxs-lookup"><span data-stu-id="040e3-123">Sentiment analysis produces a higher quality result when you give it smaller chunks of text to work on.</span></span> <span data-ttu-id="040e3-124">This is opposite from key phrase extraction, which performs better on larger blocks of text.</span><span class="sxs-lookup"><span data-stu-id="040e3-124">This is opposite from key phrase extraction, which performs better on larger blocks of text.</span></span> <span data-ttu-id="040e3-125">To get the best results from both operations, consider restructuring the inputs accordingly.</span><span class="sxs-lookup"><span data-stu-id="040e3-125">To get the best results from both operations, consider restructuring the inputs accordingly.</span></span>

<span data-ttu-id="040e3-126">You must have JSON documents in this format: id, text, language</span><span class="sxs-lookup"><span data-stu-id="040e3-126">You must have JSON documents in this format: id, text, language</span></span>

<span data-ttu-id="040e3-127">Document size must be under 5,000 characters per document, and you can have up to 1,000 items (IDs) per collection.</span><span class="sxs-lookup"><span data-stu-id="040e3-127">Document size must be under 5,000 characters per document, and you can have up to 1,000 items (IDs) per collection.</span></span> <span data-ttu-id="040e3-128">The collection is submitted in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="040e3-128">The collection is submitted in the body of the request.</span></span> <span data-ttu-id="040e3-129">The following is an example of content you might submit for sentiment analysis.</span><span class="sxs-lookup"><span data-stu-id="040e3-129">The following is an example of content you might submit for sentiment analysis.</span></span>

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

## <a name="step-1-structure-the-request"></a><span data-ttu-id="040e3-130">Step 1: Structure the request</span><span class="sxs-lookup"><span data-stu-id="040e3-130">Step 1: Structure the request</span></span>

<span data-ttu-id="040e3-131">Details on request definition can be found in [How to call the Text Analytics API](text-analytics-how-to-call-api.md).</span><span class="sxs-lookup"><span data-stu-id="040e3-131">Details on request definition can be found in [How to call the Text Analytics API](text-analytics-how-to-call-api.md).</span></span> <span data-ttu-id="040e3-132">The following points are restated for convenience:</span><span class="sxs-lookup"><span data-stu-id="040e3-132">The following points are restated for convenience:</span></span>

+ <span data-ttu-id="040e3-133">Create a **POST** request.</span><span class="sxs-lookup"><span data-stu-id="040e3-133">Create a **POST** request.</span></span> <span data-ttu-id="040e3-134">Review the API documentation for this request: [Sentiment Analysis API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9)</span><span class="sxs-lookup"><span data-stu-id="040e3-134">Review the API documentation for this request: [Sentiment Analysis API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9)</span></span>

+ <span data-ttu-id="040e3-135">Set the HTTP endpoint for key phrase extraction.</span><span class="sxs-lookup"><span data-stu-id="040e3-135">Set the HTTP endpoint for key phrase extraction.</span></span> <span data-ttu-id="040e3-136">It must include the `/sentiment` resource: `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/sentiment`</span><span class="sxs-lookup"><span data-stu-id="040e3-136">It must include the `/sentiment` resource: `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/sentiment`</span></span>

+ <span data-ttu-id="040e3-137">Set a request header to include the access key for Text Analytics operations.</span><span class="sxs-lookup"><span data-stu-id="040e3-137">Set a request header to include the access key for Text Analytics operations.</span></span> <span data-ttu-id="040e3-138">For more information, see [How to find endpoints and access keys](text-analytics-how-to-access-key.md).</span><span class="sxs-lookup"><span data-stu-id="040e3-138">For more information, see [How to find endpoints and access keys](text-analytics-how-to-access-key.md).</span></span>

+ <span data-ttu-id="040e3-139">In the request body, provide the JSON documents collection you prepared for this analysis.</span><span class="sxs-lookup"><span data-stu-id="040e3-139">In the request body, provide the JSON documents collection you prepared for this analysis.</span></span>

> [!Tip]
> <span data-ttu-id="040e3-140">Use [Postman](text-analytics-how-to-call-api.md) or open the **API testing console** in the [documentation](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9) to structure the request and POST it to the service.</span><span class="sxs-lookup"><span data-stu-id="040e3-140">Use [Postman](text-analytics-how-to-call-api.md) or open the **API testing console** in the [documentation](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9) to structure the request and POST it to the service.</span></span>

## <a name="step-2-post-the-request"></a><span data-ttu-id="040e3-141">Step 2: Post the request</span><span class="sxs-lookup"><span data-stu-id="040e3-141">Step 2: Post the request</span></span>

<span data-ttu-id="040e3-142">Analysis is performed upon receipt of the request.</span><span class="sxs-lookup"><span data-stu-id="040e3-142">Analysis is performed upon receipt of the request.</span></span> <span data-ttu-id="040e3-143">The service accepts up to 100 requests per minute.</span><span class="sxs-lookup"><span data-stu-id="040e3-143">The service accepts up to 100 requests per minute.</span></span> <span data-ttu-id="040e3-144">Each request can be a maximum of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="040e3-144">Each request can be a maximum of 1 MB.</span></span>

<span data-ttu-id="040e3-145">Recall that the service is stateless.</span><span class="sxs-lookup"><span data-stu-id="040e3-145">Recall that the service is stateless.</span></span> <span data-ttu-id="040e3-146">No data is stored in your account.</span><span class="sxs-lookup"><span data-stu-id="040e3-146">No data is stored in your account.</span></span> <span data-ttu-id="040e3-147">Results are returned immediately in the response.</span><span class="sxs-lookup"><span data-stu-id="040e3-147">Results are returned immediately in the response.</span></span>


## <a name="step-3-view-results"></a><span data-ttu-id="040e3-148">Step 3: View results</span><span class="sxs-lookup"><span data-stu-id="040e3-148">Step 3: View results</span></span>

<span data-ttu-id="040e3-149">The sentiment analyzer classifies text as predominantly positive or negative, assigning a score in the range of 0 to 1.</span><span class="sxs-lookup"><span data-stu-id="040e3-149">The sentiment analyzer classifies text as predominantly positive or negative, assigning a score in the range of 0 to 1.</span></span> <span data-ttu-id="040e3-150">Values close to 0.5 are neutral or indeterminate.</span><span class="sxs-lookup"><span data-stu-id="040e3-150">Values close to 0.5 are neutral or indeterminate.</span></span> <span data-ttu-id="040e3-151">A score of 0.5 indicates neutrality.</span><span class="sxs-lookup"><span data-stu-id="040e3-151">A score of 0.5 indicates neutrality.</span></span> <span data-ttu-id="040e3-152">When a string cannot be analyzed for sentiment or has no sentiment, the score is always 0.5 exactly.</span><span class="sxs-lookup"><span data-stu-id="040e3-152">When a string cannot be analyzed for sentiment or has no sentiment, the score is always 0.5 exactly.</span></span> <span data-ttu-id="040e3-153">For example, if you pass in a Spanish string with an English language code, the score is 0.5.</span><span class="sxs-lookup"><span data-stu-id="040e3-153">For example, if you pass in a Spanish string with an English language code, the score is 0.5.</span></span>

<span data-ttu-id="040e3-154">Output is returned immediately.</span><span class="sxs-lookup"><span data-stu-id="040e3-154">Output is returned immediately.</span></span> <span data-ttu-id="040e3-155">You can stream the results to an application that accepts JSON or save the output to a file on the local system, and then import it into an application that allows you to sort, search, and manipulate the data.</span><span class="sxs-lookup"><span data-stu-id="040e3-155">You can stream the results to an application that accepts JSON or save the output to a file on the local system, and then import it into an application that allows you to sort, search, and manipulate the data.</span></span>

<span data-ttu-id="040e3-156">The following example shows the response for the document collection in this article.</span><span class="sxs-lookup"><span data-stu-id="040e3-156">The following example shows the response for the document collection in this article.</span></span>

```
{
    "documents": [
        {
            "score": 0.9999237060546875,
            "id": "1"
        },
        {
            "score": 0.0000540316104888916,
            "id": "2"
        },
        {
            "score": 0.99990355968475342,
            "id": "3"
        },
        {
            "score": 0.980544924736023,
            "id": "4"
        },
        {
            "score": 0.99996328353881836,
            "id": "5"
        }
    ],
    "errors": []
}
```

## <a name="summary"></a><span data-ttu-id="040e3-157">Summary</span><span class="sxs-lookup"><span data-stu-id="040e3-157">Summary</span></span>

<span data-ttu-id="040e3-158">In this article, you learned concepts and workflow for sentiment analysis using Text Analytics in Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="040e3-158">In this article, you learned concepts and workflow for sentiment analysis using Text Analytics in Cognitive Services.</span></span> <span data-ttu-id="040e3-159">In summary:</span><span class="sxs-lookup"><span data-stu-id="040e3-159">In summary:</span></span>

+ <span data-ttu-id="040e3-160">[Sentiment analysis API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9) is available for selected languages.</span><span class="sxs-lookup"><span data-stu-id="040e3-160">[Sentiment analysis API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c9) is available for selected languages.</span></span>
+ <span data-ttu-id="040e3-161">JSON documents in the request body include an id, text, and language code.</span><span class="sxs-lookup"><span data-stu-id="040e3-161">JSON documents in the request body include an id, text, and language code.</span></span>
+ <span data-ttu-id="040e3-162">POST request is to a `/sentiment` endpoint, using a personalized [access key and an endpoint](text-analytics-how-to-access-key.md) that is valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="040e3-162">POST request is to a `/sentiment` endpoint, using a personalized [access key and an endpoint](text-analytics-how-to-access-key.md) that is valid for your subscription.</span></span>
+ <span data-ttu-id="040e3-163">Response output, which consists of a sentiment score for each document ID, can be streamed to any app that accepts JSON, including Excel and Power BI, to name a few.</span><span class="sxs-lookup"><span data-stu-id="040e3-163">Response output, which consists of a sentiment score for each document ID, can be streamed to any app that accepts JSON, including Excel and Power BI, to name a few.</span></span>

## <a name="see-also"></a><span data-ttu-id="040e3-164">See also</span><span class="sxs-lookup"><span data-stu-id="040e3-164">See also</span></span> 

 [<span data-ttu-id="040e3-165">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="040e3-165">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="040e3-166">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="040e3-166">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)</br>
 [<span data-ttu-id="040e3-167">Text Analytics product page</span><span class="sxs-lookup"><span data-stu-id="040e3-167">Text Analytics product page</span></span>](//go.microsoft.com/fwlink/?LinkID=759712) 

## <a name="next-steps"></a><span data-ttu-id="040e3-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="040e3-168">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="040e3-169">Extract key phrases</span><span class="sxs-lookup"><span data-stu-id="040e3-169">Extract key phrases</span></span>](text-analytics-how-to-keyword-extraction.md)
