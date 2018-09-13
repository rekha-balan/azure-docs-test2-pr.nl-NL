---
title: Web Search API quick start | Microsoft Docs
description: Shows how to get started using the Bing Web Search API.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 27B4B51A-D017-44C8-8E4E-9684DC553886
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 0b8c4678a518985a4be3ee426a85b0a85dd2365d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867877"
---
# <a name="your-first-bing-search-query"></a><span data-ttu-id="4b161-103">Your first Bing search query</span><span class="sxs-lookup"><span data-stu-id="4b161-103">Your first Bing search query</span></span>

<span data-ttu-id="4b161-104">Before you can make your first call, you need to get a Cognitive Services subscription key.</span><span class="sxs-lookup"><span data-stu-id="4b161-104">Before you can make your first call, you need to get a Cognitive Services subscription key.</span></span> <span data-ttu-id="4b161-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api).</span><span class="sxs-lookup"><span data-stu-id="4b161-105">To get a key, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api).</span></span>

<span data-ttu-id="4b161-106">To get Web search results, you'd send a GET request to the following endpoint:</span><span class="sxs-lookup"><span data-stu-id="4b161-106">To get Web search results, you'd send a GET request to the following endpoint:</span></span>  
  
```
https://api.cognitive.microsoft.com/bing/v7.0/search
```  

<span data-ttu-id="4b161-107">The request must use the HTTPS protocol.</span><span class="sxs-lookup"><span data-stu-id="4b161-107">The request must use the HTTPS protocol.</span></span>

<span data-ttu-id="4b161-108">We recommend that all requests originate from a server.</span><span class="sxs-lookup"><span data-stu-id="4b161-108">We recommend that all requests originate from a server.</span></span> <span data-ttu-id="4b161-109">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span><span class="sxs-lookup"><span data-stu-id="4b161-109">Distributing the key as part of a client application provides more opportunity for a malicious third-party to access it.</span></span> <span data-ttu-id="4b161-110">Also, making calls from a server provides a single upgrade point for future versions of the API.</span><span class="sxs-lookup"><span data-stu-id="4b161-110">Also, making calls from a server provides a single upgrade point for future versions of the API.</span></span>  
  
<span data-ttu-id="4b161-111">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#query) query parameter, which contains the user's search term.</span><span class="sxs-lookup"><span data-stu-id="4b161-111">The request must specify the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#query) query parameter, which contains the user's search term.</span></span> <span data-ttu-id="4b161-112">Although it's optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span><span class="sxs-lookup"><span data-stu-id="4b161-112">Although it's optional, the request should also specify the [mkt](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#mkt) query parameter, which identifies the market where you want the results to come from.</span></span> <span data-ttu-id="4b161-113">For a list of optional query parameters such as `responseFilter` and `textDecorations`, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#query-parameters).</span><span class="sxs-lookup"><span data-stu-id="4b161-113">For a list of optional query parameters such as `responseFilter` and `textDecorations`, see [Query Parameters](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#query-parameters).</span></span> <span data-ttu-id="4b161-114">All query parameter values must be URL encoded.</span><span class="sxs-lookup"><span data-stu-id="4b161-114">All query parameter values must be URL encoded.</span></span>  
  
<span data-ttu-id="4b161-115">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#subscriptionkey) header.</span><span class="sxs-lookup"><span data-stu-id="4b161-115">The request must specify the [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#subscriptionkey) header.</span></span> <span data-ttu-id="4b161-116">Although optional, you are encouraged to also specify the following headers:</span><span class="sxs-lookup"><span data-stu-id="4b161-116">Although optional, you are encouraged to also specify the following headers:</span></span>  
  
-   [<span data-ttu-id="4b161-117">User-Agent</span><span class="sxs-lookup"><span data-stu-id="4b161-117">User-Agent</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#useragent)  
-   [<span data-ttu-id="4b161-118">X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="4b161-118">X-MSEdge-ClientID</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#clientid)  
-   [<span data-ttu-id="4b161-119">X-Search-ClientIP</span><span class="sxs-lookup"><span data-stu-id="4b161-119">X-Search-ClientIP</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#clientip)  
-   [<span data-ttu-id="4b161-120">X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="4b161-120">X-Search-Location</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#location)  

<span data-ttu-id="4b161-121">The client IP and location headers are important for returning location aware content.</span><span class="sxs-lookup"><span data-stu-id="4b161-121">The client IP and location headers are important for returning location aware content.</span></span> <span data-ttu-id="4b161-122">For example, if the user's query is *sailing+lessons*, they're probably interested in lessons located nearby their location.</span><span class="sxs-lookup"><span data-stu-id="4b161-122">For example, if the user's query is *sailing+lessons*, they're probably interested in lessons located nearby their location.</span></span> <span data-ttu-id="4b161-123">If you want the results to contain lessons that are available near the user's location, you need to include the location header and optionally, the client IP header.</span><span class="sxs-lookup"><span data-stu-id="4b161-123">If you want the results to contain lessons that are available near the user's location, you need to include the location header and optionally, the client IP header.</span></span> <span data-ttu-id="4b161-124">It's less important if the query term explicitly mentions a location (for example, sailing+lessons+florida+keys).</span><span class="sxs-lookup"><span data-stu-id="4b161-124">It's less important if the query term explicitly mentions a location (for example, sailing+lessons+florida+keys).</span></span> 

<span data-ttu-id="4b161-125">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#headers).</span><span class="sxs-lookup"><span data-stu-id="4b161-125">For a list of all request and response headers, see [Headers](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#headers).</span></span>

## <a name="the-request"></a><span data-ttu-id="4b161-126">The request</span><span class="sxs-lookup"><span data-stu-id="4b161-126">The request</span></span>

<span data-ttu-id="4b161-127">The following shows a search request that includes all the suggested query parameters and headers.</span><span class="sxs-lookup"><span data-stu-id="4b161-127">The following shows a search request that includes all the suggested query parameters and headers.</span></span> <span data-ttu-id="4b161-128">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span><span class="sxs-lookup"><span data-stu-id="4b161-128">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span></span> <span data-ttu-id="4b161-129">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span><span class="sxs-lookup"><span data-stu-id="4b161-129">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span></span> 
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/search?q=sailing+lessons+seattle&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="4b161-130">The following shows the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="4b161-130">The following shows the response to the previous request.</span></span> <span data-ttu-id="4b161-131">The example also shows the Bing-specific response headers.</span><span class="sxs-lookup"><span data-stu-id="4b161-131">The example also shows the Bing-specific response headers.</span></span>

```
BingAPIs-TraceId: 76DD2C2549B94F9FB55B4BD6FEB6AC
X-MSEdge-ClientID: 1C3352B306E669780D58D607B96869
BingAPIs-Market: en-US

{
    "_type" : "SearchResponse",
    "webPages" : {
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346...",
        "totalEstimatedMatches" : 982000,
        "value" : [{
            "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.0",
            "name" : "Seattle Sailing Club | Lessons, Membership & More",
            "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FE...",
            "displayUrl" : "https:\/\/seattlesailing.com",
            "snippet" : "Sailing is fun! Seattle Sailing Club makes it accessible and affordable...",
            "deepLinks" : [{
                "name" : "Learn to Sail",
                "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FEFDAD..."
            },
            {
                "name" : "Fleet",
                "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FEFDAD38...",
                "snippet" : "The Seattle Sailing Club is nothing without our fleet of excellent..."
            },
            {
                "name" : "Sailing Lessons",
                "url" : "http:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FEFDAD38...",
                "snippet" : "Sailing Lessons. Taking the first step into the sailing community..."
            },
            {
                "name" : "Membership",
                "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FEFDAD3...",
                "snippet" : "Seattle sailboat rental for less than the cost of moorage!"
            },
            {
                "name" : "Hours – Directions",
                "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874...",
                "snippet" : "Contact the Seattle Sailing Club by phone or email..."
            },
            {
                "name" : "Overnight Cruising",
                "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FEFDAD...",
                "snippet" : "Overnight Cruising. Setting sail for a multi-day adventure..."
            }],
            "dateLastCrawled" : "2017-04-07T02:25:00"
        },
        {
            "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.1",
            "name" : "Best Sailing lessons in Seattle, WA - yelp.com",
            "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FEFDAD38AA...",
            "displayUrl" : "https:\/\/www.yelp.com\/search?find_desc=sailing+lessons&find_loc...",
            "snippet" : "Reviews on Sailing lessons in Seattle, WA - Seattle Sailing...",
            "dateLastCrawled" : "2017-04-01T10:49:00"
        },
        {
            "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.2",
            "name" : "Seattle Sailing with Windworks Sailing Club - Sailing ...",
            "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FEFDAD3...",
            "displayUrl" : "https:\/\/www.windworkssailing.com",
            "snippet" : "Seattle sailing club for sailing lessons, sailboat charters...",
            "dateLastCrawled" : "2017-04-09T03:33:00"
        },
        {
            "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.3",
            "name" : "Sailing Lessons in Downtown Seattle - SheSails Seattle",
            "url" : "http:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FEFDAD38...",
            "displayUrl" : "shesailsseattle.com",
            "snippet" : "SheSails Seattle is sailing lessons and sailboat charters in a fun...",
            "dateLastCrawled" : "2017-04-05T07:15:00"
        },
        {
            "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.4",
            "name" : "Seattle Sailing Club - 19 Photos & 27 Reviews - Boating ...",
            "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FE...",
            "displayUrl" : "https:\/\/www.yelp.com\/biz\/seattle-sailing-club-seattle",
            "snippet" : "27 reviews of Seattle Sailing Club \"Love the Seattle Sailing...",
            "dateLastCrawled" : "2017-04-08T14:40:00"
        },
        {
            "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.5",
            "name" : "Puget Sound Sailing - Seattle and Tacoma - PUGET SOUND ...",
            "url" : "http:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FEFDA...",
            "displayUrl" : "www.pugetsoundsailing.com",
            "snippet" : "Puget Sound Sailing Institute is an American Sailing Association...",
            "dateLastCrawled" : "2017-04-09T01:39:00"
        },
        {
            "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.6",
            "name" : "Seattle Yacht Club - Official Site",
            "url" : "http:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FE...",
            "displayUrl" : "www.seattleyachtclub.org",
            "snippet" : "Seattle Yacht Club Awarded Joe Prosser Trophy for Excellence...",
            "dateLastCrawled" : "2017-04-09T14:30:00"
        }],
        "someResultsRemoved" : true
    },
    "relatedSearches" : {
        "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#RelatedSearches",
        "value" : [{
            "text" : "sailing lessons",
            "displayText" : "sailing lessons",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346E..."
        },
        {
            "text" : "sailing schools seattle",
            "displayText" : "sailing schools seattle",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4..."
        },
        {
            "text" : "seattle boating lessons",
            "displayText" : "seattle boating lessons",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4..."
        },
        {
            "text" : "adult sailing lessons seattle",
            "displayText" : "adult sailing lessons seattle",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED..."
        },
        {
            "text" : "seattle sailing club",
            "displayText" : "seattle sailing club",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED459..."
        },
        {
            "text" : "seattle sailing club lessons",
            "displayText" : "seattle sailing club lessons",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289..."
        },
        {
            "text" : "sailing in seattle area",
            "displayText" : "sailing in seattle area",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED45948..."
        },
        {
            "text" : "seattle sailing lessons lake union",
            "displayText" : "seattle sailing lessons lake union",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED459..."
        }]
    },
    "rankingResponse" : {
        "mainline" : {
            "items" : [{
                "answerType" : "WebPages",
                "resultIndex" : 0,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.0"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 1,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.1"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 2,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.2"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 3,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.3"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 4,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.4"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 5,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.5"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 6,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.6"
                }
            }]
        },
        "sidebar" : {
            "items" : [{
                "answerType" : "RelatedSearches",
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#RelatedSearches"
                }
            }]
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="4b161-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b161-132">Next steps</span></span>

<span data-ttu-id="4b161-133">Try out the API.</span><span class="sxs-lookup"><span data-stu-id="4b161-133">Try out the API.</span></span> <span data-ttu-id="4b161-134">Go to [Web Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56b43eeccf5ff8098cef3807/operations/56b4447dcf5ff8098cef380d).</span><span class="sxs-lookup"><span data-stu-id="4b161-134">Go to [Web Search API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56b43eeccf5ff8098cef3807/operations/56b4447dcf5ff8098cef380d).</span></span> 

<span data-ttu-id="4b161-135">For details about consuming the response objects, see [Searching the Web](./search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="4b161-135">For details about consuming the response objects, see [Searching the Web](./search-the-web.md).</span></span>