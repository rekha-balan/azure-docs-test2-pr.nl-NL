---
title: How to page through Bing Web Search API results | Microsoft Docs
description: Learn how to page through Bing Web Search API results.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 26CA595B-0866-43E8-93A2-F2B5E09D1F3B
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 08/20/2018
ms.author: erhopf
ms.openlocfilehash: cd03b3af08746674dd2ba2d4af593e19e066efca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966132"
---
# <a name="how-to-page-through-bing-web-search-api-results"></a><span data-ttu-id="550f3-103">How to page through Bing Web Search API results</span><span class="sxs-lookup"><span data-stu-id="550f3-103">How to page through Bing Web Search API results</span></span>

<span data-ttu-id="550f3-104">When you call the Web Search API, Bing returns a list of results.</span><span class="sxs-lookup"><span data-stu-id="550f3-104">When you call the Web Search API, Bing returns a list of results.</span></span> <span data-ttu-id="550f3-105">The list is a subset of the total number of results that may be relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="550f3-105">The list is a subset of the total number of results that may be relevant to the query.</span></span> <span data-ttu-id="550f3-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#totalestimatedmatches) field.</span><span class="sxs-lookup"><span data-stu-id="550f3-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#totalestimatedmatches) field.</span></span>  
  
<span data-ttu-id="550f3-107">The following example shows the `totalEstimatedMatches` field that a Web answer includes.</span><span class="sxs-lookup"><span data-stu-id="550f3-107">The following example shows the `totalEstimatedMatches` field that a Web answer includes.</span></span>  
  
```
{
    "_type" : "SearchResponse",
    "webPages" : {
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=3A43CA...",
        "totalEstimatedMatches" : 262000,
        "value" : [...]
    }
}  
```
  
<span data-ttu-id="550f3-108">To page through the available webpages, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#offset) query parameters.</span><span class="sxs-lookup"><span data-stu-id="550f3-108">To page through the available webpages, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#offset) query parameters.</span></span>  
  
<span data-ttu-id="550f3-109">The `count` parameter specifies the number of results to return in the response.</span><span class="sxs-lookup"><span data-stu-id="550f3-109">The `count` parameter specifies the number of results to return in the response.</span></span> <span data-ttu-id="550f3-110">The maximum number of results that you may request in the response is 50.</span><span class="sxs-lookup"><span data-stu-id="550f3-110">The maximum number of results that you may request in the response is 50.</span></span> <span data-ttu-id="550f3-111">The default is 10.</span><span class="sxs-lookup"><span data-stu-id="550f3-111">The default is 10.</span></span> <span data-ttu-id="550f3-112">The actual number delivered may be less than requested.</span><span class="sxs-lookup"><span data-stu-id="550f3-112">The actual number delivered may be less than requested.</span></span>

<span data-ttu-id="550f3-113">The `offset` parameter specifies the number of results to skip.</span><span class="sxs-lookup"><span data-stu-id="550f3-113">The `offset` parameter specifies the number of results to skip.</span></span> <span data-ttu-id="550f3-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span><span class="sxs-lookup"><span data-stu-id="550f3-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span></span>  
  
<span data-ttu-id="550f3-115">If you want to display 15 webpages per page, you would set `count` to 15 and `offset` to 0 to get the first page of results.</span><span class="sxs-lookup"><span data-stu-id="550f3-115">If you want to display 15 webpages per page, you would set `count` to 15 and `offset` to 0 to get the first page of results.</span></span> <span data-ttu-id="550f3-116">For each subsequent page, you would increment `offset` by 15 (for example, 15, 30).</span><span class="sxs-lookup"><span data-stu-id="550f3-116">For each subsequent page, you would increment `offset` by 15 (for example, 15, 30).</span></span>  
  
<span data-ttu-id="550f3-117">The following example requests 15 webpages beginning at offset 45.</span><span class="sxs-lookup"><span data-stu-id="550f3-117">The following example requests 15 webpages beginning at offset 45.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/search?q=sailing+dinghies&count=15&offset=45&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```

<span data-ttu-id="550f3-118">If the default `count` value works for your implementation, you only need to specify the `offset` query parameter.</span><span class="sxs-lookup"><span data-stu-id="550f3-118">If the default `count` value works for your implementation, you only need to specify the `offset` query parameter.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/search?q=sailing+dinghies&offset=45&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```

<span data-ttu-id="550f3-119">The Web Search API returns results that include webpages and may include images, videos, and news.</span><span class="sxs-lookup"><span data-stu-id="550f3-119">The Web Search API returns results that include webpages and may include images, videos, and news.</span></span> <span data-ttu-id="550f3-120">When you page the search results, you are paging the [WebAnswer](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#webanswer) answer and not the other answers such as images or news.</span><span class="sxs-lookup"><span data-stu-id="550f3-120">When you page the search results, you are paging the [WebAnswer](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#webanswer) answer and not the other answers such as images or news.</span></span> <span data-ttu-id="550f3-121">For example, if you set `count` to 50, you get back 50 webpage results, but the response may include results for the other answers as well.</span><span class="sxs-lookup"><span data-stu-id="550f3-121">For example, if you set `count` to 50, you get back 50 webpage results, but the response may include results for the other answers as well.</span></span> <span data-ttu-id="550f3-122">For example, the response may include 15 images and 4 news articles.</span><span class="sxs-lookup"><span data-stu-id="550f3-122">For example, the response may include 15 images and 4 news articles.</span></span> <span data-ttu-id="550f3-123">It is also possible that the results may include news on the first page but not the second page, or vice versa.</span><span class="sxs-lookup"><span data-stu-id="550f3-123">It is also possible that the results may include news on the first page but not the second page, or vice versa.</span></span>   
    
<span data-ttu-id="550f3-124">If you specify the `responseFilter` query parameter and do not include Webpages in the filter list, don't use the `count` and `offset` parameters.</span><span class="sxs-lookup"><span data-stu-id="550f3-124">If you specify the `responseFilter` query parameter and do not include Webpages in the filter list, don't use the `count` and `offset` parameters.</span></span>  
