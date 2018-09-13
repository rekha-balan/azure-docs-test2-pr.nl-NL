---
title: How to page through the available videos | Microsoft Docs
description: Shows how to page through all of the videos that Bing can return.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 910A485F-BCF3-42B9-958D-DD48BDEDA965
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 00476825eb3fc1008c3f2172b591d8b7a2f35884
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866809"
---
# <a name="paging-videos"></a><span data-ttu-id="13b03-103">Paging videos</span><span class="sxs-lookup"><span data-stu-id="13b03-103">Paging videos</span></span>

<span data-ttu-id="13b03-104">When you call the Video Search API, Bing returns a list of results.</span><span class="sxs-lookup"><span data-stu-id="13b03-104">When you call the Video Search API, Bing returns a list of results.</span></span> <span data-ttu-id="13b03-105">The list is a subset of the total number of results that are relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="13b03-105">The list is a subset of the total number of results that are relevant to the query.</span></span> <span data-ttu-id="13b03-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos-totalestimatedmatches) field.</span><span class="sxs-lookup"><span data-stu-id="13b03-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos-totalestimatedmatches) field.</span></span>  
  
<span data-ttu-id="13b03-107">The following example shows the `totalEstimatedMatches` field that a Video answer includes.</span><span class="sxs-lookup"><span data-stu-id="13b03-107">The following example shows the `totalEstimatedMatches` field that a Video answer includes.</span></span>  
  
```  
{
    "_type" : "Videos",
    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=81EF7545D56...",
    "totalEstimatedMatches" : 1000,
    "value" : [...]
}  
```  
  
<span data-ttu-id="13b03-108">To page through the available videos, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#offset) query parameters.</span><span class="sxs-lookup"><span data-stu-id="13b03-108">To page through the available videos, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#offset) query parameters.</span></span>  
  
<span data-ttu-id="13b03-109">The `count` parameter specifies the number of results to return in the response.</span><span class="sxs-lookup"><span data-stu-id="13b03-109">The `count` parameter specifies the number of results to return in the response.</span></span> <span data-ttu-id="13b03-110">The maximum number of results that you may request in the response is 105.</span><span class="sxs-lookup"><span data-stu-id="13b03-110">The maximum number of results that you may request in the response is 105.</span></span> <span data-ttu-id="13b03-111">The default is 35.</span><span class="sxs-lookup"><span data-stu-id="13b03-111">The default is 35.</span></span> <span data-ttu-id="13b03-112">The actual number delivered may be less than requested.</span><span class="sxs-lookup"><span data-stu-id="13b03-112">The actual number delivered may be less than requested.</span></span>

<span data-ttu-id="13b03-113">The `offset` parameter specifies the number of results to skip.</span><span class="sxs-lookup"><span data-stu-id="13b03-113">The `offset` parameter specifies the number of results to skip.</span></span> <span data-ttu-id="13b03-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span><span class="sxs-lookup"><span data-stu-id="13b03-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span></span>  
  
<span data-ttu-id="13b03-115">If you want to display 20 videos per page, you would set `count` to 20 and `offset` to 0 to get the first page of results.</span><span class="sxs-lookup"><span data-stu-id="13b03-115">If you want to display 20 videos per page, you would set `count` to 20 and `offset` to 0 to get the first page of results.</span></span> <span data-ttu-id="13b03-116">For each subsequent page, you would increment `offset` by 20 (for example, 20, 40).</span><span class="sxs-lookup"><span data-stu-id="13b03-116">For each subsequent page, you would increment `offset` by 20 (for example, 20, 40).</span></span>  

<span data-ttu-id="13b03-117">The following shows an example that requests 20 videos beginning at offset 40.</span><span class="sxs-lookup"><span data-stu-id="13b03-117">The following shows an example that requests 20 videos beginning at offset 40.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/search?q=sailing+dinghies&count=20&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="13b03-118">If the default `count` value works for your implementation, you only need to specify the `offset` query parameter.</span><span class="sxs-lookup"><span data-stu-id="13b03-118">If the default `count` value works for your implementation, you only need to specify the `offset` query parameter.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/search?q=sailing+dinghies&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="13b03-119">Typically, if you page 35 videos at a time, you would set the `offset` query parameter to 0 on your first request, and then increment `offset` by 35 on each subsequent request.</span><span class="sxs-lookup"><span data-stu-id="13b03-119">Typically, if you page 35 videos at a time, you would set the `offset` query parameter to 0 on your first request, and then increment `offset` by 35 on each subsequent request.</span></span> <span data-ttu-id="13b03-120">However, some of the results in the subsequent response may be duplicates of the previous response.</span><span class="sxs-lookup"><span data-stu-id="13b03-120">However, some of the results in the subsequent response may be duplicates of the previous response.</span></span> <span data-ttu-id="13b03-121">For example, the first two videos in the response may be the same as the last two videos from the previous response.</span><span class="sxs-lookup"><span data-stu-id="13b03-121">For example, the first two videos in the response may be the same as the last two videos from the previous response.</span></span>

<span data-ttu-id="13b03-122">To eliminate duplicate results, use the [nextOffset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos-nextoffset) field of the `Videos` object.</span><span class="sxs-lookup"><span data-stu-id="13b03-122">To eliminate duplicate results, use the [nextOffset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos-nextoffset) field of the `Videos` object.</span></span>

<span data-ttu-id="13b03-123">For example, if you want to page 30 videos at a time, you'd set `count` to 30 and `offset` to 0 in your first request.</span><span class="sxs-lookup"><span data-stu-id="13b03-123">For example, if you want to page 30 videos at a time, you'd set `count` to 30 and `offset` to 0 in your first request.</span></span> <span data-ttu-id="13b03-124">In your next request, you'd set the `offset` query parameter to the `nextOffset` value.</span><span class="sxs-lookup"><span data-stu-id="13b03-124">In your next request, you'd set the `offset` query parameter to the `nextOffset` value.</span></span>


> [!NOTE]
> <span data-ttu-id="13b03-125">Paging applies only to videos search (/videos/search), and not to video insights (/videos/details) or trending videos (/videos/trending).</span><span class="sxs-lookup"><span data-stu-id="13b03-125">Paging applies only to videos search (/videos/search), and not to video insights (/videos/details) or trending videos (/videos/trending).</span></span>