---
title: Images Search API quick start | Microsoft Docs
description: Shows how to get started using the Bing Images Search API.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: BE2B2F8C-20B5-4E0B-AEC8-EAD505BA4C85
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 9e211cf5acd17ab80948d0b7161bdd2a9220c4a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865536"
---
# <a name="your-first-images-search-query"></a><span data-ttu-id="b56f2-103">Your first images search query</span><span class="sxs-lookup"><span data-stu-id="b56f2-103">Your first images search query</span></span>

<span data-ttu-id="b56f2-104">Before you can make your first call, you need to get a Bing Search Cognitive Services subscription key.</span><span class="sxs-lookup"><span data-stu-id="b56f2-104">Before you can make your first call, you need to get a Bing Search Cognitive Services subscription key.</span></span> <span data-ttu-id="b56f2-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api).</span><span class="sxs-lookup"><span data-stu-id="b56f2-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api).</span></span>

<span data-ttu-id="b56f2-106">To get Image search results, you'd send a GET request to the following endpoint:</span><span class="sxs-lookup"><span data-stu-id="b56f2-106">To get Image search results, you'd send a GET request to the following endpoint:</span></span>  
  
```
https://api.cognitive.microsoft.com/bing/v7.0/images/search
```
  
<span data-ttu-id="b56f2-107">The request must use the HTTPS protocol.</span><span class="sxs-lookup"><span data-stu-id="b56f2-107">The request must use the HTTPS protocol.</span></span>

<span data-ttu-id="b56f2-108">We recommend that all requests originate from a server.</span><span class="sxs-lookup"><span data-stu-id="b56f2-108">We recommend that all requests originate from a server.</span></span> <span data-ttu-id="b56f2-109">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span><span class="sxs-lookup"><span data-stu-id="b56f2-109">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span></span> <span data-ttu-id="b56f2-110">Also, making calls from a server provides a single upgrade point for future versions of the API.</span><span class="sxs-lookup"><span data-stu-id="b56f2-110">Also, making calls from a server provides a single upgrade point for future versions of the API.</span></span>

<span data-ttu-id="b56f2-111">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query) query parameter, which contains the user's search term.</span><span class="sxs-lookup"><span data-stu-id="b56f2-111">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query) query parameter, which contains the user's search term.</span></span> <span data-ttu-id="b56f2-112">Although it's optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span><span class="sxs-lookup"><span data-stu-id="b56f2-112">Although it's optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span></span> <span data-ttu-id="b56f2-113">For a list of optional query parameters such as `freshness` and `size`, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query-parameters).</span><span class="sxs-lookup"><span data-stu-id="b56f2-113">For a list of optional query parameters such as `freshness` and `size`, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#query-parameters).</span></span> <span data-ttu-id="b56f2-114">All query parameter values must be URL encoded.</span><span class="sxs-lookup"><span data-stu-id="b56f2-114">All query parameter values must be URL encoded.</span></span>  
  
<span data-ttu-id="b56f2-115">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#subscriptionkey) header.</span><span class="sxs-lookup"><span data-stu-id="b56f2-115">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#subscriptionkey) header.</span></span> <span data-ttu-id="b56f2-116">Although optional, you are encouraged to also specify the following headers:</span><span class="sxs-lookup"><span data-stu-id="b56f2-116">Although optional, you are encouraged to also specify the following headers:</span></span>  
  
-   [<span data-ttu-id="b56f2-117">User-Agent</span><span class="sxs-lookup"><span data-stu-id="b56f2-117">User-Agent</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#useragent)  
-   [<span data-ttu-id="b56f2-118">X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="b56f2-118">X-MSEdge-ClientID</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#clientid)  
-   [<span data-ttu-id="b56f2-119">X-Search-ClientIP</span><span class="sxs-lookup"><span data-stu-id="b56f2-119">X-Search-ClientIP</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#clientip)  
-   [<span data-ttu-id="b56f2-120">X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="b56f2-120">X-Search-Location</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#location)  

<span data-ttu-id="b56f2-121">The client IP and location headers are important for returning location aware content.</span><span class="sxs-lookup"><span data-stu-id="b56f2-121">The client IP and location headers are important for returning location aware content.</span></span>  

<span data-ttu-id="b56f2-122">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#headers).</span><span class="sxs-lookup"><span data-stu-id="b56f2-122">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#headers).</span></span>

## <a name="the-request"></a><span data-ttu-id="b56f2-123">The request</span><span class="sxs-lookup"><span data-stu-id="b56f2-123">The request</span></span>

<span data-ttu-id="b56f2-124">The following shows a search request that includes all the suggested query parameters and headers.</span><span class="sxs-lookup"><span data-stu-id="b56f2-124">The following shows a search request that includes all the suggested query parameters and headers.</span></span> <span data-ttu-id="b56f2-125">If it's is your first time calling any of the Bing APIs, don't include the client ID header.</span><span class="sxs-lookup"><span data-stu-id="b56f2-125">If it's is your first time calling any of the Bing APIs, don't include the client ID header.</span></span> <span data-ttu-id="b56f2-126">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span><span class="sxs-lookup"><span data-stu-id="b56f2-126">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span></span> 
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="b56f2-127">The following shows the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="b56f2-127">The following shows the response to the previous request.</span></span>

```json
{
    "_type" : "Images",
    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=73118C8B4E3...",
    "totalEstimatedMatches" : 838,
    "value" : [
        {
            "name" : "File:Rich Passage Minto Sailing Dinghy.jpg - Wikipedia",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=73118C8B4E3...",
            "thumbnailUrl" : "https:\/\/tse1.mm.bing.net\/th?id=OIP.GNarK7m...",
            "datePublished" : "2011-10-29T11:26:00",
            "contentUrl" : "http:\/\/www.bing.com\/cr?IG=73118C8B4E3D4C3...",
            "hostPageUrl" : "http:\/\/www.bing.com\/cr?IG=73118C8B4E3D4C3687...",
            "contentSize" : "79239 B",
            "encodingFormat" : "jpeg",
            "hostPageDisplayUrl" : "en.wikipedia.org\/wiki\/File:Rich_Passage...",
            "width" : 526,
            "height" : 688,
            "thumbnail" : {
                "width" : 229,
                "height" : 300
            },
            "imageInsightsToken" : "ccid_GNarK7ma*mid_CCF85447ADA6...",
            "insightsSourcesSummary" : {
                "shoppingSourcesCount" : 0,
                "recipeSourcesCount" : 0
            },
            "imageId" : "CCF85447ADA6FFF9E96E7DF0B796F7A86E34593",
            "accentColor" : "376094"
        },
        . . .
    ],
    "queryExpansions" : [
        {
            "text" : "Small Sailing Dinghies",
            "displayText" : "Small",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=73118C8B4...",
            "searchLink" : "https:\/\/api.cognitive.microsoft.com\/api...",
            "thumbnail" : {
                "thumbnailUrl" : "https:\/\/tse2.mm.bing.net\/th?q=..."
            }
        },
        . . .
    ],
    "nextOffset" : 10,
    "pivotSuggestions" : [
        {
            "pivot" : "sailing",
            "suggestions" : []
        },
        {
            "pivot" : "dinghies",
            "suggestions" : [
                {
                    "text" : "Sailing Tender",
                    "displayText" : "Tender",
                    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=73118...",
                    "searchLink" : "https:\/\/api.cognitive.microsoft.com\/api...",
                    "thumbnail" : {
                        "thumbnailUrl" : "https:\/\/tse2.mm.bing.net\/th?q=..."
                    }
                },
                . . .
            ]
        }
    ],
    "displayShoppingSourcesBadges" : false,
    "displayRecipeSourcesBadges" : true
}
```

## <a name="next-steps"></a><span data-ttu-id="b56f2-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="b56f2-128">Next steps</span></span>

<span data-ttu-id="b56f2-129">Try out the API.</span><span class="sxs-lookup"><span data-stu-id="b56f2-129">Try out the API.</span></span> <span data-ttu-id="b56f2-130">Go to [Image Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/8336afba49a84475ba401758c0dbf749/operations/571fab09dbe2d933e891028f).</span><span class="sxs-lookup"><span data-stu-id="b56f2-130">Go to [Image Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/8336afba49a84475ba401758c0dbf749/operations/571fab09dbe2d933e891028f).</span></span> 

<span data-ttu-id="b56f2-131">For details about consuming the response objects, see [Searching the Web](./search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="b56f2-131">For details about consuming the response objects, see [Searching the Web](./search-the-web.md).</span></span>

<span data-ttu-id="b56f2-132">For details about getting insights about an image such as web pages that include the image or people that were recognized in the image, see [Image Insights](./image-insights.md).</span><span class="sxs-lookup"><span data-stu-id="b56f2-132">For details about getting insights about an image such as web pages that include the image or people that were recognized in the image, see [Image Insights](./image-insights.md).</span></span>  
  
<span data-ttu-id="b56f2-133">For details about images that are trending on social media, see [Trending Images](./trending-images.md).</span><span class="sxs-lookup"><span data-stu-id="b56f2-133">For details about images that are trending on social media, see [Trending Images](./trending-images.md).</span></span>  
