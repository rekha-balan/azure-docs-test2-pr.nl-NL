---
title: How-to use Entity Linking in Text Analytics REST API (Microsoft Cognitive Services on Azure) | Microsoft Docs
description: Learn how to identify and resolve entities using the Text Analytics REST API in Microsoft Cognitive Services on Azure in this walkthrough tutorial.
services: cognitive-services
author: ashmaka
manager: cgronlun
ms.service: cognitive-services
ms.technology: text-analytics
ms.topic: article
ms.date: 5/02/2018
ms.author: ashmaka
ms.openlocfilehash: 55bec1a0223b70749a97a30e2da92ef15128038c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869137"
---
# <a name="how-to-identify-linked-entities-in-text-analytics-preview"></a><span data-ttu-id="9b656-103">How to identify linked entities in Text Analytics (Preview)</span><span class="sxs-lookup"><span data-stu-id="9b656-103">How to identify linked entities in Text Analytics (Preview)</span></span>

<span data-ttu-id="9b656-104">The [Entity Linking API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634) takes unstructured text, and for each JSON document, returns a list of disambiguated entities with links to more information on the web (Wikipedia and Bing).</span><span class="sxs-lookup"><span data-stu-id="9b656-104">The [Entity Linking API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634) takes unstructured text, and for each JSON document, returns a list of disambiguated entities with links to more information on the web (Wikipedia and Bing).</span></span> 

## <a name="entity-linking-vs-named-entity-recognition"></a><span data-ttu-id="9b656-105">Entity Linking vs. Named Entity Recognition</span><span class="sxs-lookup"><span data-stu-id="9b656-105">Entity Linking vs. Named Entity Recognition</span></span>

<span data-ttu-id="9b656-106">In natural language processing, the concepts of entity linking and named entity recognition (NER) can easily be confused.</span><span class="sxs-lookup"><span data-stu-id="9b656-106">In natural language processing, the concepts of entity linking and named entity recognition (NER) can easily be confused.</span></span> <span data-ttu-id="9b656-107">In the preview version of Text Analytics' `entities` endpoint, only entity linking is supported.</span><span class="sxs-lookup"><span data-stu-id="9b656-107">In the preview version of Text Analytics' `entities` endpoint, only entity linking is supported.</span></span>

<span data-ttu-id="9b656-108">Entity linking is the ability to identify and disambiguate the identity of an entity found in text (e.g. determining whether the "Mars" is being used as the planet or as the Roman god of war).</span><span class="sxs-lookup"><span data-stu-id="9b656-108">Entity linking is the ability to identify and disambiguate the identity of an entity found in text (e.g. determining whether the "Mars" is being used as the planet or as the Roman god of war).</span></span> <span data-ttu-id="9b656-109">This process requires the presence of a knowledge base to which recognized entities are linked - Wikipedia is used as the knowledge base for the `entities` endpoint Text Analytics.</span><span class="sxs-lookup"><span data-stu-id="9b656-109">This process requires the presence of a knowledge base to which recognized entities are linked - Wikipedia is used as the knowledge base for the `entities` endpoint Text Analytics.</span></span>

### <a name="language-support"></a><span data-ttu-id="9b656-110">Language support</span><span class="sxs-lookup"><span data-stu-id="9b656-110">Language support</span></span>

<span data-ttu-id="9b656-111">Using entity linking in various languages requires using a corresponding knowledge base in each language.</span><span class="sxs-lookup"><span data-stu-id="9b656-111">Using entity linking in various languages requires using a corresponding knowledge base in each language.</span></span> <span data-ttu-id="9b656-112">For entity linking in Text Analytics, this means each language that is supported by the `entities` endpoint will link to the corresponding Wikipedia corpus in that language.</span><span class="sxs-lookup"><span data-stu-id="9b656-112">For entity linking in Text Analytics, this means each language that is supported by the `entities` endpoint will link to the corresponding Wikipedia corpus in that language.</span></span> <span data-ttu-id="9b656-113">Since the size of corpora varies between languages, it is expected that the entity linking functionality's recall will also vary.</span><span class="sxs-lookup"><span data-stu-id="9b656-113">Since the size of corpora varies between languages, it is expected that the entity linking functionality's recall will also vary.</span></span>


## <a name="preparation"></a><span data-ttu-id="9b656-114">Preparation</span><span class="sxs-lookup"><span data-stu-id="9b656-114">Preparation</span></span>

<span data-ttu-id="9b656-115">You must have JSON documents in this format: id, text, language</span><span class="sxs-lookup"><span data-stu-id="9b656-115">You must have JSON documents in this format: id, text, language</span></span>

<span data-ttu-id="9b656-116">For currently supported languages, please see [this list](../text-analytics-supported-languages.md).</span><span class="sxs-lookup"><span data-stu-id="9b656-116">For currently supported languages, please see [this list](../text-analytics-supported-languages.md).</span></span>

<span data-ttu-id="9b656-117">Document size must be under 5,000 characters per document, and you can have up to 1,000 items (IDs) per collection.</span><span class="sxs-lookup"><span data-stu-id="9b656-117">Document size must be under 5,000 characters per document, and you can have up to 1,000 items (IDs) per collection.</span></span> <span data-ttu-id="9b656-118">The collection is submitted in the body of the request.</span><span class="sxs-lookup"><span data-stu-id="9b656-118">The collection is submitted in the body of the request.</span></span> <span data-ttu-id="9b656-119">The following example is an illustration of content you might submit to the entity linking end.</span><span class="sxs-lookup"><span data-stu-id="9b656-119">The following example is an illustration of content you might submit to the entity linking end.</span></span>

```
{"documents": [{"id": "1",
                "language": "en",
                "text": "I really enjoy the new XBox One S. It has a clean look, it has 4K/HDR resolution and it is affordable."
                },
               {"id": "2",
                "language": "en",
                "text": "The Seattle Seahawks won the Super Bowl in 2014."
                }
               ]
}
```    
    
## <a name="step-1-structure-the-request"></a><span data-ttu-id="9b656-120">Step 1: Structure the request</span><span class="sxs-lookup"><span data-stu-id="9b656-120">Step 1: Structure the request</span></span>

<span data-ttu-id="9b656-121">Details on request definition can be found in [How to call the Text Analytics API](text-analytics-how-to-call-api.md).</span><span class="sxs-lookup"><span data-stu-id="9b656-121">Details on request definition can be found in [How to call the Text Analytics API](text-analytics-how-to-call-api.md).</span></span> <span data-ttu-id="9b656-122">The following points are restated for convenience:</span><span class="sxs-lookup"><span data-stu-id="9b656-122">The following points are restated for convenience:</span></span>

+ <span data-ttu-id="9b656-123">Create a **POST** request.</span><span class="sxs-lookup"><span data-stu-id="9b656-123">Create a **POST** request.</span></span> <span data-ttu-id="9b656-124">Review the API documentation for this request: [Entity Linking API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634)</span><span class="sxs-lookup"><span data-stu-id="9b656-124">Review the API documentation for this request: [Entity Linking API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634)</span></span>

+ <span data-ttu-id="9b656-125">Set the HTTP endpoint for key phrase extraction.</span><span class="sxs-lookup"><span data-stu-id="9b656-125">Set the HTTP endpoint for key phrase extraction.</span></span> <span data-ttu-id="9b656-126">It must include the `/entities` resource: `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/entities`</span><span class="sxs-lookup"><span data-stu-id="9b656-126">It must include the `/entities` resource: `https://westus.api.cognitive.microsoft.com/text/analytics/v2.0/entities`</span></span>

+ <span data-ttu-id="9b656-127">Set a request header to include the access key for Text Analytics operations.</span><span class="sxs-lookup"><span data-stu-id="9b656-127">Set a request header to include the access key for Text Analytics operations.</span></span> <span data-ttu-id="9b656-128">For more information, see [How to find endpoints and access keys](text-analytics-how-to-access-key.md).</span><span class="sxs-lookup"><span data-stu-id="9b656-128">For more information, see [How to find endpoints and access keys](text-analytics-how-to-access-key.md).</span></span>

+ <span data-ttu-id="9b656-129">In the request body, provide the JSON documents collection you prepared for this analysis</span><span class="sxs-lookup"><span data-stu-id="9b656-129">In the request body, provide the JSON documents collection you prepared for this analysis</span></span>

> [!Tip]
> <span data-ttu-id="9b656-130">Use [Postman](text-analytics-how-to-call-api.md) or open the **API testing console** in the [documentation](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634) to structure a request and POST it to the service.</span><span class="sxs-lookup"><span data-stu-id="9b656-130">Use [Postman](text-analytics-how-to-call-api.md) or open the **API testing console** in the [documentation](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634) to structure a request and POST it to the service.</span></span>

## <a name="step-2-post-the-request"></a><span data-ttu-id="9b656-131">Step 2: Post the request</span><span class="sxs-lookup"><span data-stu-id="9b656-131">Step 2: Post the request</span></span>

<span data-ttu-id="9b656-132">Analysis is performed upon receipt of the request.</span><span class="sxs-lookup"><span data-stu-id="9b656-132">Analysis is performed upon receipt of the request.</span></span> <span data-ttu-id="9b656-133">The service accepts up to 100 requests per minute.</span><span class="sxs-lookup"><span data-stu-id="9b656-133">The service accepts up to 100 requests per minute.</span></span> <span data-ttu-id="9b656-134">Each request can be a maximum of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="9b656-134">Each request can be a maximum of 1 MB.</span></span>

<span data-ttu-id="9b656-135">Recall that the service is stateless.</span><span class="sxs-lookup"><span data-stu-id="9b656-135">Recall that the service is stateless.</span></span> <span data-ttu-id="9b656-136">No data is stored in your account.</span><span class="sxs-lookup"><span data-stu-id="9b656-136">No data is stored in your account.</span></span> <span data-ttu-id="9b656-137">Results are returned immediately in the response.</span><span class="sxs-lookup"><span data-stu-id="9b656-137">Results are returned immediately in the response.</span></span>

## <a name="step-3-view-results"></a><span data-ttu-id="9b656-138">Step 3: View results</span><span class="sxs-lookup"><span data-stu-id="9b656-138">Step 3: View results</span></span>

<span data-ttu-id="9b656-139">All POST requests return a JSON formatted response with the IDs and detected properties.</span><span class="sxs-lookup"><span data-stu-id="9b656-139">All POST requests return a JSON formatted response with the IDs and detected properties.</span></span>

<span data-ttu-id="9b656-140">Output is returned immediately.</span><span class="sxs-lookup"><span data-stu-id="9b656-140">Output is returned immediately.</span></span> <span data-ttu-id="9b656-141">You can stream the results to an application that accepts JSON or save the output to a file on the local system, and then import it into an application that allows you to sort, search, and manipulate the data.</span><span class="sxs-lookup"><span data-stu-id="9b656-141">You can stream the results to an application that accepts JSON or save the output to a file on the local system, and then import it into an application that allows you to sort, search, and manipulate the data.</span></span>

<span data-ttu-id="9b656-142">An example of the output for entity linking is shown next:</span><span class="sxs-lookup"><span data-stu-id="9b656-142">An example of the output for entity linking is shown next:</span></span>

```
{
    "documents": [
        {
            "id": "1",
            "entities": [
                {
                    "name": "Xbox One",
                    "matches": [
                        {
                            "text": "XBox One",
                            "offset": 23,
                            "length": 8
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Xbox One",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Xbox_One",
                    "bingId": "446bb4df-4999-4243-84c0-74e0f6c60e75"
                },
                {
                    "name": "Ultra-high-definition television",
                    "matches": [
                        {
                            "text": "4K",
                            "offset": 63,
                            "length": 2
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "Ultra-high-definition television",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/Ultra-high-definition_television",
                    "bingId": "7ee02026-b6ec-878b-f4de-f0bc7b0ab8c4"
                }
            ]
        },
        {
            "id": "2",
            "entities": [
                {
                    "name": "2013 Seattle Seahawks season",
                    "matches": [
                        {
                            "text": "Seattle Seahawks",
                            "offset": 4,
                            "length": 16
                        }
                    ],
                    "wikipediaLanguage": "en",
                    "wikipediaId": "2013 Seattle Seahawks season",
                    "wikipediaUrl": "https://en.wikipedia.org/wiki/2013_Seattle_Seahawks_season",
                    "bingId": "eb637865-4722-4eca-be9e-0ac0c376d361"
                }
            ]
        }
    ],
    "errors": []
}
```

<span data-ttu-id="9b656-143">When available, the response includes the Wikipedia ID, Wikipedia URL, and Bing ID for each detected entity.</span><span class="sxs-lookup"><span data-stu-id="9b656-143">When available, the response includes the Wikipedia ID, Wikipedia URL, and Bing ID for each detected entity.</span></span> <span data-ttu-id="9b656-144">These can be used to further enhance your application with information regarding the linked entity.</span><span class="sxs-lookup"><span data-stu-id="9b656-144">These can be used to further enhance your application with information regarding the linked entity.</span></span>


## <a name="summary"></a><span data-ttu-id="9b656-145">Summary</span><span class="sxs-lookup"><span data-stu-id="9b656-145">Summary</span></span>

<span data-ttu-id="9b656-146">In this article, you learned concepts and workflow for entity linking using Text Analytics in Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="9b656-146">In this article, you learned concepts and workflow for entity linking using Text Analytics in Cognitive Services.</span></span> <span data-ttu-id="9b656-147">In summary:</span><span class="sxs-lookup"><span data-stu-id="9b656-147">In summary:</span></span>

+ <span data-ttu-id="9b656-148">[Entity Linking API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634) is available for selected languages.</span><span class="sxs-lookup"><span data-stu-id="9b656-148">[Entity Linking API](https://westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/5ac4251d5b4ccd1554da7634) is available for selected languages.</span></span>
+ <span data-ttu-id="9b656-149">JSON documents in the request body include an id, text, and language code.</span><span class="sxs-lookup"><span data-stu-id="9b656-149">JSON documents in the request body include an id, text, and language code.</span></span>
+ <span data-ttu-id="9b656-150">POST request is to a `/entities` endpoint, using a personalized [access key and an endpoint](text-analytics-how-to-access-key.md) that is valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="9b656-150">POST request is to a `/entities` endpoint, using a personalized [access key and an endpoint](text-analytics-how-to-access-key.md) that is valid for your subscription.</span></span>
+ <span data-ttu-id="9b656-151">Response output, which consists of linked entities (including confidence scores, offsets, and web links, for each document ID) can be used in any application</span><span class="sxs-lookup"><span data-stu-id="9b656-151">Response output, which consists of linked entities (including confidence scores, offsets, and web links, for each document ID) can be used in any application</span></span>

## <a name="see-also"></a><span data-ttu-id="9b656-152">See also</span><span class="sxs-lookup"><span data-stu-id="9b656-152">See also</span></span> 

 [<span data-ttu-id="9b656-153">Text Analytics overview</span><span class="sxs-lookup"><span data-stu-id="9b656-153">Text Analytics overview</span></span>](../overview.md)  
 [<span data-ttu-id="9b656-154">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="9b656-154">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)</br>
 [<span data-ttu-id="9b656-155">Text Analytics product page</span><span class="sxs-lookup"><span data-stu-id="9b656-155">Text Analytics product page</span></span>](//go.microsoft.com/fwlink/?LinkID=759712) 

## <a name="next-steps"></a><span data-ttu-id="9b656-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b656-156">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9b656-157">Text Analytics API</span><span class="sxs-lookup"><span data-stu-id="9b656-157">Text Analytics API</span></span>](//westus.dev.cognitive.microsoft.com/docs/services/TextAnalytics.V2.0/operations/56f30ceeeda5650db055a3c6)
