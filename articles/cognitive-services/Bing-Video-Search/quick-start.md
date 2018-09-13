---
title: Video Search API quick start | Microsoft Docs
description: Shows how to get started using the Bing Video Search API.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 7E59692A-83A8-4F4C-B122-1F0EDC8E5C86
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 0bd0f067d64cac3ebac342ebadcfcc010a47af7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869755"
---
# <a name="your-first-video-search-query"></a><span data-ttu-id="39c00-103">Your first video search query</span><span class="sxs-lookup"><span data-stu-id="39c00-103">Your first video search query</span></span>

<span data-ttu-id="39c00-104">Before you can make your first call, you need to get a Bing Search Cognitive Services subscription key.</span><span class="sxs-lookup"><span data-stu-id="39c00-104">Before you can make your first call, you need to get a Bing Search Cognitive Services subscription key.</span></span> <span data-ttu-id="39c00-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-video-search-api).</span><span class="sxs-lookup"><span data-stu-id="39c00-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-video-search-api).</span></span>

<span data-ttu-id="39c00-106">To get Video search results, you'd send a GET request to the following endpoint:</span><span class="sxs-lookup"><span data-stu-id="39c00-106">To get Video search results, you'd send a GET request to the following endpoint:</span></span>  
  
```
https://api.cognitive.microsoft.com/bing/v7.0/videos/search
```
   
<span data-ttu-id="39c00-107">The request must use the HTTPS protocol.</span><span class="sxs-lookup"><span data-stu-id="39c00-107">The request must use the HTTPS protocol.</span></span>

<span data-ttu-id="39c00-108">We recommend that all requests originate from a server.</span><span class="sxs-lookup"><span data-stu-id="39c00-108">We recommend that all requests originate from a server.</span></span> <span data-ttu-id="39c00-109">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span><span class="sxs-lookup"><span data-stu-id="39c00-109">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span></span> <span data-ttu-id="39c00-110">Also, making calls from a server provides a single upgrade point for future versions of the API.</span><span class="sxs-lookup"><span data-stu-id="39c00-110">Also, making calls from a server provides a single upgrade point for future versions of the API.</span></span>

  
<span data-ttu-id="39c00-111">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query) query parameter, which contains the user's search term.</span><span class="sxs-lookup"><span data-stu-id="39c00-111">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query) query parameter, which contains the user's search term.</span></span> <span data-ttu-id="39c00-112">Although it's optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span><span class="sxs-lookup"><span data-stu-id="39c00-112">Although it's optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span></span> <span data-ttu-id="39c00-113">For a list of optional query parameters such as `pricing`, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query-parameters).</span><span class="sxs-lookup"><span data-stu-id="39c00-113">For a list of optional query parameters such as `pricing`, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query-parameters).</span></span> <span data-ttu-id="39c00-114">All query parameter values must be URL encoded.</span><span class="sxs-lookup"><span data-stu-id="39c00-114">All query parameter values must be URL encoded.</span></span>  
  
<span data-ttu-id="39c00-115">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#subscriptionkey) header.</span><span class="sxs-lookup"><span data-stu-id="39c00-115">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#subscriptionkey) header.</span></span> <span data-ttu-id="39c00-116">Although optional, you are encouraged to also specify the following headers:</span><span class="sxs-lookup"><span data-stu-id="39c00-116">Although optional, you are encouraged to also specify the following headers:</span></span>  
  
-   [<span data-ttu-id="39c00-117">User-Agent</span><span class="sxs-lookup"><span data-stu-id="39c00-117">User-Agent</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#useragent)  
-   [<span data-ttu-id="39c00-118">X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="39c00-118">X-MSEdge-ClientID</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#clientid)  
-   [<span data-ttu-id="39c00-119">X-Search-ClientIP</span><span class="sxs-lookup"><span data-stu-id="39c00-119">X-Search-ClientIP</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#clientip)  
-   [<span data-ttu-id="39c00-120">X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="39c00-120">X-Search-Location</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#location)  

<span data-ttu-id="39c00-121">The client IP and location headers are important for returning location aware content.</span><span class="sxs-lookup"><span data-stu-id="39c00-121">The client IP and location headers are important for returning location aware content.</span></span>  

<span data-ttu-id="39c00-122">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#headers).</span><span class="sxs-lookup"><span data-stu-id="39c00-122">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#headers).</span></span>


## <a name="the-request"></a><span data-ttu-id="39c00-123">The request</span><span class="sxs-lookup"><span data-stu-id="39c00-123">The request</span></span>

<span data-ttu-id="39c00-124">The following shows a search request that includes all the suggested query parameters and headers.</span><span class="sxs-lookup"><span data-stu-id="39c00-124">The following shows a search request that includes all the suggested query parameters and headers.</span></span> <span data-ttu-id="39c00-125">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span><span class="sxs-lookup"><span data-stu-id="39c00-125">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span></span> <span data-ttu-id="39c00-126">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span><span class="sxs-lookup"><span data-stu-id="39c00-126">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span></span> 
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/search?q=sailing+dinghies&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-Search-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="39c00-127">The following shows the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="39c00-127">The following shows the response to the previous request.</span></span> <span data-ttu-id="39c00-128">The example also shows the Bing-specific response headers.</span><span class="sxs-lookup"><span data-stu-id="39c00-128">The example also shows the Bing-specific response headers.</span></span>

```
BingAPIs-TraceId: 76DD2C2549B94F9FB55B4BD6FEB6AC
X-MSEdge-ClientID: 1C3352B306E669780D58D607B96869
BingAPIs-Market: en-US

{
    "_type" : "Videos",
    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=81EF7545D5694...",
    "totalEstimatedMatches" : 1000,
    "value" : [
        {
            "name" : "How to sail - What to Wear for Dinghy Sailing",
            "description" : "An informative video on what to wear when...",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=81EF7545D56...",
            "thumbnailUrl" : "https:\/\/tse4.mm.bing.net\/th?id=OVP.DYWCvh...",
            "datePublished" : "2014-03-04T11:51:53",
            "publisher" : [
                {
                    "name" : "Fabrikam"
                }
            ],
            "creator" : {
                "name" : "Marcus Appel"
            },
            "contentUrl" : "https:\/\/www.fabrikam.com\/watch?v=vzmPjHZ--g",
            "hostPageUrl" : "https:\/\/www.bing.com\/cr?IG=81EF7545D56944...",
            "encodingFormat" : "h264",
            "hostPageDisplayUrl" : "https:\/\/www.fabrikam.com\/watch?v=vzmPjBZ--g",
            "width" : 1280,
            "height" : 720,
            "duration" : "PT2M47S",
            "motionThumbnailUrl" : "https:\/\/tse3.mm.bing.net\/th?id=OM.Y6...",
            "embedHtml" : "<iframe width=\"1280\" height=\"720\" src=\"https:...><\/iframe>",
            "allowHttpsEmbed" : true,
            "viewCount" : 8743,
            "thumbnail" : {
                "width" : 300,
                "height" : 168
            },
            "videoId" : "6DB795E11A6E3CBAAD636DB795E11E3CBAAD63",
            "allowMobileEmbed" : true,
            "isSuperfresh" : false
        },
        . . .
    ],
    "nextOffset" : 0,
    "pivotSuggestions" : [
        {
            "pivot" : "sailing",
            "suggestions" : []
        },
        {
            "pivot" : "dinghies",
            "suggestions" : [
                {
                    "text" : "Sailing Cruising",
                    "displayText" : "Cruising",
                    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=81EF754...",
                    "searchLink" : "https:\/\/api.cognitive.microsoft.com...",
                    "thumbnail" : {
                        "thumbnailUrl" : "https:\/\/tse4.mm.bing.net\/th?q=Sailing..."
                    }
                },
                . . .
            ]
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="39c00-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="39c00-129">Next steps</span></span>

<span data-ttu-id="39c00-130">Try out the API.</span><span class="sxs-lookup"><span data-stu-id="39c00-130">Try out the API.</span></span> <span data-ttu-id="39c00-131">Go to [Video Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56b43f3ccf5ff8098cef3809/operations/58113fe5e31dac0a1ce6b0a8).</span><span class="sxs-lookup"><span data-stu-id="39c00-131">Go to [Video Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56b43f3ccf5ff8098cef3809/operations/58113fe5e31dac0a1ce6b0a8).</span></span> 

<span data-ttu-id="39c00-132">For details about consuming the response objects, see [Searching the Web for Videos](./search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="39c00-132">For details about consuming the response objects, see [Searching the Web for Videos](./search-the-web.md).</span></span>

<span data-ttu-id="39c00-133">For details about getting insights about a video such as related searches, see [Video Insights](./video-insights.md).</span><span class="sxs-lookup"><span data-stu-id="39c00-133">For details about getting insights about a video such as related searches, see [Video Insights](./video-insights.md).</span></span>  
  
<span data-ttu-id="39c00-134">For details about videos that are trending on social media, see [Trending Videos](./trending-videos.md).</span><span class="sxs-lookup"><span data-stu-id="39c00-134">For details about videos that are trending on social media, see [Trending Videos](./trending-videos.md).</span></span>  
