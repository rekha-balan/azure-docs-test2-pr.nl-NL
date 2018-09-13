---
title: How to page through the available news articles | Microsoft Docs
description: Shows how to page through all of the news articles that Bing can return.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: EA388F72-FA43-493B-967C-9560B3243C62
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 2c90d468536f0864d7deac073667e29e9a54692f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855986"
---
# <a name="paging-news"></a><span data-ttu-id="8bb5c-103">Paging news</span><span class="sxs-lookup"><span data-stu-id="8bb5c-103">Paging news</span></span>

<span data-ttu-id="8bb5c-104">When you call the News Search API, Bing returns a list of results.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-104">When you call the News Search API, Bing returns a list of results.</span></span> <span data-ttu-id="8bb5c-105">The list is a subset of the total number of results that may be relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-105">The list is a subset of the total number of results that may be relevant to the query.</span></span> <span data-ttu-id="8bb5c-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#news-totalmatches) field.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#news-totalmatches) field.</span></span>  
  
<span data-ttu-id="8bb5c-107">The following example shows the `totalEstimatedMatches` field that a News answer includes.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-107">The following example shows the `totalEstimatedMatches` field that a News answer includes.</span></span>  
  
```  
{  
    "_type" : "News",  
    "readLink" : "https:\/\/api.cognitive.microsoft.com\/bing\/v7\/news\/search?q=sailing+dinghies",  
    "totalEstimatedMatches" : 88400,  
    "value" : [...]  
}  
```  
  
<span data-ttu-id="8bb5c-108">To page through the available articles, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#offset) query parameters.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-108">To page through the available articles, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#offset) query parameters.</span></span>  
  
<span data-ttu-id="8bb5c-109">The `count` parameter specifies the number of results to return in the response.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-109">The `count` parameter specifies the number of results to return in the response.</span></span> <span data-ttu-id="8bb5c-110">The maximum number of results that you may request in the response is 100.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-110">The maximum number of results that you may request in the response is 100.</span></span> <span data-ttu-id="8bb5c-111">The default is 10.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-111">The default is 10.</span></span> <span data-ttu-id="8bb5c-112">The actual number delivered may be less than requested.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-112">The actual number delivered may be less than requested.</span></span>

<span data-ttu-id="8bb5c-113">The `offset` parameter specifies the number of results to skip.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-113">The `offset` parameter specifies the number of results to skip.</span></span> <span data-ttu-id="8bb5c-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span><span class="sxs-lookup"><span data-stu-id="8bb5c-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span></span>  

<span data-ttu-id="8bb5c-115">If you want to display 20 articles per page, you would set `count` to 20 and `offset` to 0 to get the first page of results.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-115">If you want to display 20 articles per page, you would set `count` to 20 and `offset` to 0 to get the first page of results.</span></span> <span data-ttu-id="8bb5c-116">For each subsequent page, you would increment `offset` by 20 (for example, 20, 40).</span><span class="sxs-lookup"><span data-stu-id="8bb5c-116">For each subsequent page, you would increment `offset` by 20 (for example, 20, 40).</span></span>  
  
<span data-ttu-id="8bb5c-117">The following shows an example that requests 20 news articles beginning at offset 40.</span><span class="sxs-lookup"><span data-stu-id="8bb5c-117">The following shows an example that requests 20 news articles beginning at offset 40.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/news/search?q=sailing+dinghies&count=20&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  
  
<span data-ttu-id="8bb5c-118">If the default `count` value works for your implementation, specify only the `offset` query parameter as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8bb5c-118">If the default `count` value works for your implementation, specify only the `offset` query parameter as shown in the following example:</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/news/search?q=sailing+dinghies&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  
  
> [!NOTE]
> <span data-ttu-id="8bb5c-119">Paging applies only to news search (/news/search), and not to trending topics (/news/trendingtopics) or news categories (/news).</span><span class="sxs-lookup"><span data-stu-id="8bb5c-119">Paging applies only to news search (/news/search), and not to trending topics (/news/trendingtopics) or news categories (/news).</span></span>