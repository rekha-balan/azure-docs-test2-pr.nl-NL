---
title: 'Bing Custom Search: Page through available webpages | Microsoft Docs'
description: Shows how to page through all of the webpages that Bing can return.
services: cognitive-services
author: brapel
manager: ehansen
ms.assetid: 26CA595B-0866-43E8-93A2-F2B5E09D1F3B
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: article
ms.date: 09/28/2017
ms.author: v-brapel
ms.openlocfilehash: f2f545a5a9195fc65515ea716f277723600cbb78
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867442"
---
# <a name="paging-webpages"></a><span data-ttu-id="43e6c-103">Paging webpages</span><span class="sxs-lookup"><span data-stu-id="43e6c-103">Paging webpages</span></span> 

<span data-ttu-id="43e6c-104">When you call the Custom Search API, Bing returns a list of results.</span><span class="sxs-lookup"><span data-stu-id="43e6c-104">When you call the Custom Search API, Bing returns a list of results.</span></span> <span data-ttu-id="43e6c-105">The list is a subset of the total number of results that may be relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="43e6c-105">The list is a subset of the total number of results that may be relevant to the query.</span></span> <span data-ttu-id="43e6c-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#totalestimatedmatches) field.</span><span class="sxs-lookup"><span data-stu-id="43e6c-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#totalestimatedmatches) field.</span></span>  
  
<span data-ttu-id="43e6c-107">The following example shows the `totalEstimatedMatches` field that a Web answer includes.</span><span class="sxs-lookup"><span data-stu-id="43e6c-107">The following example shows the `totalEstimatedMatches` field that a Web answer includes.</span></span>  
  
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
  
<span data-ttu-id="43e6c-108">To page through the available webpages, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#offset) query parameters.</span><span class="sxs-lookup"><span data-stu-id="43e6c-108">To page through the available webpages, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#offset) query parameters.</span></span>  
  
<span data-ttu-id="43e6c-109">The `count` parameter specifies the number of results to return in the response.</span><span class="sxs-lookup"><span data-stu-id="43e6c-109">The `count` parameter specifies the number of results to return in the response.</span></span> <span data-ttu-id="43e6c-110">The maximum number of results that you may request in the response is 50.</span><span class="sxs-lookup"><span data-stu-id="43e6c-110">The maximum number of results that you may request in the response is 50.</span></span> <span data-ttu-id="43e6c-111">The default is 10.</span><span class="sxs-lookup"><span data-stu-id="43e6c-111">The default is 10.</span></span> <span data-ttu-id="43e6c-112">The actual number delivered may be less than requested.</span><span class="sxs-lookup"><span data-stu-id="43e6c-112">The actual number delivered may be less than requested.</span></span>

<span data-ttu-id="43e6c-113">The `offset` parameter specifies the number of results to skip.</span><span class="sxs-lookup"><span data-stu-id="43e6c-113">The `offset` parameter specifies the number of results to skip.</span></span> <span data-ttu-id="43e6c-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span><span class="sxs-lookup"><span data-stu-id="43e6c-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span></span>  
  
<span data-ttu-id="43e6c-115">If you want to display 15 webpages per page, you would set `count` to 15 and `offset` to 0 to get the first page of results.</span><span class="sxs-lookup"><span data-stu-id="43e6c-115">If you want to display 15 webpages per page, you would set `count` to 15 and `offset` to 0 to get the first page of results.</span></span> <span data-ttu-id="43e6c-116">For each subsequent page, you would increment `offset` by 15 (for example, 15, 30).</span><span class="sxs-lookup"><span data-stu-id="43e6c-116">For each subsequent page, you would increment `offset` by 15 (for example, 15, 30).</span></span>  
  
<span data-ttu-id="43e6c-117">The following shows an example that requests 15 webpages beginning at offset 45.</span><span class="sxs-lookup"><span data-stu-id="43e6c-117">The following shows an example that requests 15 webpages beginning at offset 45.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/search?q=sailing+dinghies&count=15&offset=45&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: <subscription ID>
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="43e6c-118">If the default `count` value works for your implementation, you only need to specify the `offset` query parameter.</span><span class="sxs-lookup"><span data-stu-id="43e6c-118">If the default `count` value works for your implementation, you only need to specify the `offset` query parameter.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/search?q=sailing+dinghies&offset=45&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: <subscription ID>  
Host: api.cognitive.microsoft.com  
```  

