---
title: How to page through the available images | Microsoft Docs
description: Shows how to page through all of the images that Bing can return.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 3C8423F8-41E0-4F89-86B6-697E840610A7
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: a74ee817e84be5bb563c5fdaf25afc1dc14732e5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966799"
---
# <a name="paging-results"></a><span data-ttu-id="d0e71-103">Paging results</span><span class="sxs-lookup"><span data-stu-id="d0e71-103">Paging results</span></span>

<span data-ttu-id="d0e71-104">When you call the Image Search API, Bing returns a list of results.</span><span class="sxs-lookup"><span data-stu-id="d0e71-104">When you call the Image Search API, Bing returns a list of results.</span></span> <span data-ttu-id="d0e71-105">The list is a subset of the total number of results that are relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="d0e71-105">The list is a subset of the total number of results that are relevant to the query.</span></span> <span data-ttu-id="d0e71-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#totalestimatedmatches) field.</span><span class="sxs-lookup"><span data-stu-id="d0e71-106">To get the estimated total number of available results, access the answer object's [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#totalestimatedmatches) field.</span></span>  
  
<span data-ttu-id="d0e71-107">The following example shows the `totalEstimatedMatches` field that an Images answer includes.</span><span class="sxs-lookup"><span data-stu-id="d0e71-107">The following example shows the `totalEstimatedMatches` field that an Images answer includes.</span></span>  
  
```json
{
    "_type" : "Images",
    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=73118C8...",
    "totalEstimatedMatches" : 838,
    "value" : [...]  
}  
```  
  
<span data-ttu-id="d0e71-108">To page through the available images, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#offset) query parameters.</span><span class="sxs-lookup"><span data-stu-id="d0e71-108">To page through the available images, use the [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#count) and [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#offset) query parameters.</span></span>  
  
<span data-ttu-id="d0e71-109">The `count` parameter specifies the number of results to return in the response.</span><span class="sxs-lookup"><span data-stu-id="d0e71-109">The `count` parameter specifies the number of results to return in the response.</span></span> <span data-ttu-id="d0e71-110">The maximum number of results that you may request in the response is 150.</span><span class="sxs-lookup"><span data-stu-id="d0e71-110">The maximum number of results that you may request in the response is 150.</span></span> <span data-ttu-id="d0e71-111">The default is 35.</span><span class="sxs-lookup"><span data-stu-id="d0e71-111">The default is 35.</span></span> <span data-ttu-id="d0e71-112">The actual number delivered may be less than requested.</span><span class="sxs-lookup"><span data-stu-id="d0e71-112">The actual number delivered may be less than requested.</span></span>

<span data-ttu-id="d0e71-113">The `offset` parameter specifies the number of results to skip.</span><span class="sxs-lookup"><span data-stu-id="d0e71-113">The `offset` parameter specifies the number of results to skip.</span></span> <span data-ttu-id="d0e71-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span><span class="sxs-lookup"><span data-stu-id="d0e71-114">The `offset` is zero-based and should be less than (`totalEstimatedMatches` - `count`).</span></span>  
  
<span data-ttu-id="d0e71-115">If you want to display 20 images per page, you would set `count` to 20 and `offset` to 0 to get the first page of results.</span><span class="sxs-lookup"><span data-stu-id="d0e71-115">If you want to display 20 images per page, you would set `count` to 20 and `offset` to 0 to get the first page of results.</span></span> <span data-ttu-id="d0e71-116">The following shows an example that requests 20 images beginning at offset 40.</span><span class="sxs-lookup"><span data-stu-id="d0e71-116">The following shows an example that requests 20 images beginning at offset 40.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies&count=20&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="d0e71-117">If the default `count` value works for your implementation, you only need to specify the `offset` query parameter.</span><span class="sxs-lookup"><span data-stu-id="d0e71-117">If the default `count` value works for your implementation, you only need to specify the `offset` query parameter.</span></span>  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  
  
<span data-ttu-id="d0e71-118">You might expect that if you page 35 images at a time, you would set the `offset` query parameter to 0 on your first request, and then increment `offset` by 35 on each subsequent request.</span><span class="sxs-lookup"><span data-stu-id="d0e71-118">You might expect that if you page 35 images at a time, you would set the `offset` query parameter to 0 on your first request, and then increment `offset` by 35 on each subsequent request.</span></span> <span data-ttu-id="d0e71-119">However, some of the results in the subsequent response may be duplicates of the previous response.</span><span class="sxs-lookup"><span data-stu-id="d0e71-119">However, some of the results in the subsequent response may be duplicates of the previous response.</span></span> <span data-ttu-id="d0e71-120">For example, the first two images in the response may be the same as the last two images from the previous response.</span><span class="sxs-lookup"><span data-stu-id="d0e71-120">For example, the first two images in the response may be the same as the last two images from the previous response.</span></span>

<span data-ttu-id="d0e71-121">To eliminate duplicate results, use the [nextOffset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#nextoffset) field of the `Images` object.</span><span class="sxs-lookup"><span data-stu-id="d0e71-121">To eliminate duplicate results, use the [nextOffset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#nextoffset) field of the `Images` object.</span></span> <span data-ttu-id="d0e71-122">The `nextOffset` field tells you the `offset` to use for your next request.</span><span class="sxs-lookup"><span data-stu-id="d0e71-122">The `nextOffset` field tells you the `offset` to use for your next request.</span></span> <span data-ttu-id="d0e71-123">For example, if you want to page 30 images at a time, you'd set `count` to 30 and `offset` to 0 in your first request.</span><span class="sxs-lookup"><span data-stu-id="d0e71-123">For example, if you want to page 30 images at a time, you'd set `count` to 30 and `offset` to 0 in your first request.</span></span> <span data-ttu-id="d0e71-124">In your next request, you'd set `count` to 30 and `offset` to the value of the previous response's `nextOffset`.</span><span class="sxs-lookup"><span data-stu-id="d0e71-124">In your next request, you'd set `count` to 30 and `offset` to the value of the previous response's `nextOffset`.</span></span> <span data-ttu-id="d0e71-125">To page backward, we suggest maintaining a stack of the previous offsets and popping the most recent.</span><span class="sxs-lookup"><span data-stu-id="d0e71-125">To page backward, we suggest maintaining a stack of the previous offsets and popping the most recent.</span></span>

> [!NOTE]
> <span data-ttu-id="d0e71-126">Paging applies only to image search (/images/search), and not to image insights or trending images (/images/trending).</span><span class="sxs-lookup"><span data-stu-id="d0e71-126">Paging applies only to image search (/images/search), and not to image insights or trending images (/images/trending).</span></span>