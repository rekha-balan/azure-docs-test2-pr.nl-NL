---
title: Entities Search API quick start | Microsoft Docs
description: Shows how to get started using the Bing Entities Search API.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: B206A254-B7E9-49FF-AFD5-87B1E4D6D30B
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 07/06/2017
ms.author: scottwhi
ms.openlocfilehash: 12031d2447920c7e2d6180f35cf4fb29aa1b6150
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869668"
---
# <a name="making-your-first-entities-request"></a><span data-ttu-id="99571-103">Making your first entities request</span><span class="sxs-lookup"><span data-stu-id="99571-103">Making your first entities request</span></span>

<span data-ttu-id="99571-104">The Entity Search API sends a search query to Bing and gets results that include entities and places.</span><span class="sxs-lookup"><span data-stu-id="99571-104">The Entity Search API sends a search query to Bing and gets results that include entities and places.</span></span> <span data-ttu-id="99571-105">Place results include restaurants, hotel, or other local businesses.</span><span class="sxs-lookup"><span data-stu-id="99571-105">Place results include restaurants, hotel, or other local businesses.</span></span> <span data-ttu-id="99571-106">For places, the query can specify the name of the local business or it can ask for a list (for example, restaurants near me).</span><span class="sxs-lookup"><span data-stu-id="99571-106">For places, the query can specify the name of the local business or it can ask for a list (for example, restaurants near me).</span></span> <span data-ttu-id="99571-107">Entity results include persons, places, or things.</span><span class="sxs-lookup"><span data-stu-id="99571-107">Entity results include persons, places, or things.</span></span> <span data-ttu-id="99571-108">Place in this context is tourist attractions, states, countries, etc.</span><span class="sxs-lookup"><span data-stu-id="99571-108">Place in this context is tourist attractions, states, countries, etc.</span></span> 

## <a name="first-steps"></a><span data-ttu-id="99571-109">First steps</span><span class="sxs-lookup"><span data-stu-id="99571-109">First steps</span></span>

<span data-ttu-id="99571-110">Before you can make your first call, you need to get a Cognitive Services subscription key.</span><span class="sxs-lookup"><span data-stu-id="99571-110">Before you can make your first call, you need to get a Cognitive Services subscription key.</span></span> <span data-ttu-id="99571-111">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-entities-search-api).</span><span class="sxs-lookup"><span data-stu-id="99571-111">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-entities-search-api).</span></span> <span data-ttu-id="99571-112">(If the Entities Search API isn't visible at the top, click the **Search** tab and scroll down until you see it.)</span><span class="sxs-lookup"><span data-stu-id="99571-112">(If the Entities Search API isn't visible at the top, click the **Search** tab and scroll down until you see it.)</span></span>

## <a name="the-endpoint"></a><span data-ttu-id="99571-113">The endpoint</span><span class="sxs-lookup"><span data-stu-id="99571-113">The endpoint</span></span>

<span data-ttu-id="99571-114">To get entity and place search results, send a GET request to the following endpoint:</span><span class="sxs-lookup"><span data-stu-id="99571-114">To get entity and place search results, send a GET request to the following endpoint:</span></span>  
  
```
https://api.cognitive.microsoft.com/bing/v7.0/entities
```

<span data-ttu-id="99571-115">The request must use the HTTPS protocol.</span><span class="sxs-lookup"><span data-stu-id="99571-115">The request must use the HTTPS protocol.</span></span>

<span data-ttu-id="99571-116">We recommend that all requests originate from a server.</span><span class="sxs-lookup"><span data-stu-id="99571-116">We recommend that all requests originate from a server.</span></span> <span data-ttu-id="99571-117">Distributing the key as part of a client application provides more opportunity for a malicious third party to access it.</span><span class="sxs-lookup"><span data-stu-id="99571-117">Distributing the key as part of a client application provides more opportunity for a malicious third party to access it.</span></span> <span data-ttu-id="99571-118">Also, making calls from a server provides a single upgrade point for future versions of the API.</span><span class="sxs-lookup"><span data-stu-id="99571-118">Also, making calls from a server provides a single upgrade point for future versions of the API.</span></span>

## <a name="specifying-query-parameters-and-headers"></a><span data-ttu-id="99571-119">Specifying query parameters and headers</span><span class="sxs-lookup"><span data-stu-id="99571-119">Specifying query parameters and headers</span></span>

<span data-ttu-id="99571-120">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#query) query parameter, which contains the user's search term.</span><span class="sxs-lookup"><span data-stu-id="99571-120">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#query) query parameter, which contains the user's search term.</span></span> <span data-ttu-id="99571-121">The request must also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span><span class="sxs-lookup"><span data-stu-id="99571-121">The request must also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span></span> <span data-ttu-id="99571-122">For a list of optional query parameters, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#query-parameters).</span><span class="sxs-lookup"><span data-stu-id="99571-122">For a list of optional query parameters, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#query-parameters).</span></span> <span data-ttu-id="99571-123">URL encode all query parameters.</span><span class="sxs-lookup"><span data-stu-id="99571-123">URL encode all query parameters.</span></span>  
  
<span data-ttu-id="99571-124">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#subscriptionkey) header.</span><span class="sxs-lookup"><span data-stu-id="99571-124">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#subscriptionkey) header.</span></span> <span data-ttu-id="99571-125">Although optional, you are encouraged to also specify the following headers:</span><span class="sxs-lookup"><span data-stu-id="99571-125">Although optional, you are encouraged to also specify the following headers:</span></span>  
  
-   [<span data-ttu-id="99571-126">User-Agent</span><span class="sxs-lookup"><span data-stu-id="99571-126">User-Agent</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#useragent)  
-   [<span data-ttu-id="99571-127">X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="99571-127">X-MSEdge-ClientID</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#clientid)  
-   [<span data-ttu-id="99571-128">X-MSEdge-ClientIP</span><span class="sxs-lookup"><span data-stu-id="99571-128">X-MSEdge-ClientIP</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#clientip)  
-   [<span data-ttu-id="99571-129">X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="99571-129">X-Search-Location</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#location)  

<span data-ttu-id="99571-130">The client IP and location headers are important for returning location aware content.</span><span class="sxs-lookup"><span data-stu-id="99571-130">The client IP and location headers are important for returning location aware content.</span></span>  

<span data-ttu-id="99571-131">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#headers).</span><span class="sxs-lookup"><span data-stu-id="99571-131">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#headers).</span></span>

## <a name="the-request"></a><span data-ttu-id="99571-132">The request</span><span class="sxs-lookup"><span data-stu-id="99571-132">The request</span></span>

<span data-ttu-id="99571-133">The following shows an entities request that includes all the suggested query parameters and headers.</span><span class="sxs-lookup"><span data-stu-id="99571-133">The following shows an entities request that includes all the suggested query parameters and headers.</span></span> 

```  
GET https://api.cognitive.microsoft.com/bing/v7.0/entities?q=mount+rainier&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-Search-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="99571-134">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span><span class="sxs-lookup"><span data-stu-id="99571-134">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span></span> <span data-ttu-id="99571-135">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span><span class="sxs-lookup"><span data-stu-id="99571-135">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span></span>

## <a name="the-response"></a><span data-ttu-id="99571-136">The response</span><span class="sxs-lookup"><span data-stu-id="99571-136">The response</span></span>

<span data-ttu-id="99571-137">The following shows the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="99571-137">The following shows the response to the previous request.</span></span> <span data-ttu-id="99571-138">The example also shows the Bing-specific response headers.</span><span class="sxs-lookup"><span data-stu-id="99571-138">The example also shows the Bing-specific response headers.</span></span> <span data-ttu-id="99571-139">For information about the response object, see [SearchResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#searchresponse).</span><span class="sxs-lookup"><span data-stu-id="99571-139">For information about the response object, see [SearchResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#searchresponse).</span></span>

```
BingAPIs-TraceId: 76DD2C2549B94F9FB55B4BD6FEB6AC
X-MSEdge-ClientID: 1C3352B306E669780D58D607B96869
BingAPIs-Market: en-US

{
    "_type" : "SearchResponse",
    "queryContext" : {
        "originalQuery" : "mount rainier"
    },
    "entities" : {
        "queryScenario" : "DominantEntity",
        "value" : [{
            "contractualRules" : [{
                "_type" : "ContractualRules\/LicenseAttribution",
                "targetPropertyName" : "description",
                "mustBeCloseToContent" : true,
                "license" : {
                    "name" : "CC-BY-SA",
                    "url" : "http:\/\/creativecommons.org\/licenses\/by-sa\/3.0\/"
                },
                "licenseNotice" : "Text under CC-BY-SA license"
            },
            {
                "_type" : "ContractualRules\/LinkAttribution",
                "targetPropertyName" : "description",
                "mustBeCloseToContent" : true,
                "text" : "en.wikipedia.org",
                "url" : "http:\/\/en.wikipedia.org\/wiki\/Mount_Rainier"
            },
            {
                "_type" : "ContractualRules\/MediaAttribution",
                "targetPropertyName" : "image",
                "mustBeCloseToContent" : true,
                "url" : "http:\/\/en.wikipedia.org\/wiki\/Mount_Rainier"
            }],
            "webSearchUrl" : "https:\/\/www.bing.com\/search?q=Mount%20Rainier...",
            "name" : "Mount Rainier",
            "image" : {
                "name" : "Mount Rainier",
                "thumbnailUrl" : "https:\/\/www.bing.com\/th?id=A21890c0e1f...",
                "provider" : [{
                    "_type" : "Organization",
                    "url" : "http:\/\/en.wikipedia.org\/wiki\/Mount_Rainier"
                }],
                "hostPageUrl" : "http:\/\/upload.wikimedia.org\/wikipedia...",
                "width" : 110,
                "height" : 110
            },
            "description" : "Mount Rainier, Mount Tacoma, or Mount Tahoma is the highest...",
            "entityPresentationInfo" : {
                "entityScenario" : "DominantEntity",
                "entityTypeHints" : ["Attraction"],
                "entityTypeDisplayHint" : "Mountain"
            },
            "bingId" : "9ae3e6ca-81ea-6fa1-ffa0-42e1d78906"
        }]
    }
}
```



## <a name="next-steps"></a><span data-ttu-id="99571-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="99571-140">Next steps</span></span>

<span data-ttu-id="99571-141">Try out the API.</span><span class="sxs-lookup"><span data-stu-id="99571-141">Try out the API.</span></span> <span data-ttu-id="99571-142">Go to [Entities Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/7a3fb374be374859a823b79fd938cc65/).</span><span class="sxs-lookup"><span data-stu-id="99571-142">Go to [Entities Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/7a3fb374be374859a823b79fd938cc65/).</span></span> 

<span data-ttu-id="99571-143">For details about consuming the response objects, see [Searching the Web for entities and places](./search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="99571-143">For details about consuming the response objects, see [Searching the Web for entities and places](./search-the-web.md).</span></span>

<span data-ttu-id="99571-144">Be sure to read [Bing Use and Display Requirements](./use-display-requirements.md) so you don't break any of the rules about using the search results.</span><span class="sxs-lookup"><span data-stu-id="99571-144">Be sure to read [Bing Use and Display Requirements](./use-display-requirements.md) so you don't break any of the rules about using the search results.</span></span>
