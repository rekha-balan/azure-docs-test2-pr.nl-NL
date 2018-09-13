---
title: Filtering the web answers that Bing returns | Microsoft Docs
description: Shows how to use responseFilter to filter the answers that the Bing Web Search API returns.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 8B837DC2-70F1-41C7-9496-11EDFD1A888D
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 01/12/2017
ms.author: scottwhi
ms.openlocfilehash: 64095089e4c0841aa1f77165969221836c747738
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864949"
---
# <a name="filtering-the-answers-that-the-search-response-includes"></a><span data-ttu-id="39c30-103">Filtering the answers that the search response includes</span><span class="sxs-lookup"><span data-stu-id="39c30-103">Filtering the answers that the search response includes</span></span>  

<span data-ttu-id="39c30-104">When you query the web, Bing returns all content that it thinks is relevant to the search.</span><span class="sxs-lookup"><span data-stu-id="39c30-104">When you query the web, Bing returns all content that it thinks is relevant to the search.</span></span> <span data-ttu-id="39c30-105">For example, if the search query is "sailing+dinghies", the response might contain the following answers:</span><span class="sxs-lookup"><span data-stu-id="39c30-105">For example, if the search query is "sailing+dinghies", the response might contain the following answers:</span></span>

```json
{
    "_type" : "SearchResponse",
    "webPages" : {
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=3A43C...",
        "totalEstimatedMatches" : 262000,
        "value" : [...]
    },
    "images" : {
        "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#Images",
        "readLink" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=sail...",
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=3A43CA5CA6464E5D...",
        "isFamilyFriendly" : true,
        "value" : [...]
    },
    "rankingResponse" : {
        "mainline" : {
            "items" : [...]
        }
    }
}    
```

<span data-ttu-id="39c30-106">If you're interested in specific types of content such as images, videos, and news, you can request only those answers by using the [responseFilter](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#responsefilter) query parameter.</span><span class="sxs-lookup"><span data-stu-id="39c30-106">If you're interested in specific types of content such as images, videos, and news, you can request only those answers by using the [responseFilter](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#responsefilter) query parameter.</span></span> <span data-ttu-id="39c30-107">If Bing finds relevant content for the specified answers, Bing returns it.</span><span class="sxs-lookup"><span data-stu-id="39c30-107">If Bing finds relevant content for the specified answers, Bing returns it.</span></span> <span data-ttu-id="39c30-108">The response filter is a comma-delimited list of answers.</span><span class="sxs-lookup"><span data-stu-id="39c30-108">The response filter is a comma-delimited list of answers.</span></span> <span data-ttu-id="39c30-109">The following shows how to use `responseFilter` to request images, videos, and news of sailing dinghies.</span><span class="sxs-lookup"><span data-stu-id="39c30-109">The following shows how to use `responseFilter` to request images, videos, and news of sailing dinghies.</span></span> <span data-ttu-id="39c30-110">When you encode the query string, the commas change to %2C.</span><span class="sxs-lookup"><span data-stu-id="39c30-110">When you encode the query string, the commas change to %2C.</span></span>  

```  
GET https://api.cognitive.microsoft.com/bing/v7.0/search?q=sailing+dinghies&responseFilter=images%2Cvideos%2Cnews&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-Search-ClientIP: 999.999.999.999  
X-Search-Location:  47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="39c30-111">The following shows the response to the previous query.</span><span class="sxs-lookup"><span data-stu-id="39c30-111">The following shows the response to the previous query.</span></span> <span data-ttu-id="39c30-112">As you can see Bing didn't find relevant video and news results, so the response doesn't include them.</span><span class="sxs-lookup"><span data-stu-id="39c30-112">As you can see Bing didn't find relevant video and news results, so the response doesn't include them.</span></span>

```json
{
    "_type" : "SearchResponse",
    "images" : {
        "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#Images",
        "readLink" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=sail...",
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=3AD78B183C56456C...",
        "isFamilyFriendly" : true,
        "value" : [...]
    },
    "rankingResponse" : {
        "mainline" : {
            "items" : [{
                "answerType" : "Images",
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#Images"
                }
            }]
        }
    }
}
```

<span data-ttu-id="39c30-113">If you want to exclude specific types of content, such as images, from the response, you can exclude them with the hyphen (minus) prefix to the responseFilter value.</span><span class="sxs-lookup"><span data-stu-id="39c30-113">If you want to exclude specific types of content, such as images, from the response, you can exclude them with the hyphen (minus) prefix to the responseFilter value.</span></span> <span data-ttu-id="39c30-114">Separate excluded types with a comma:</span><span class="sxs-lookup"><span data-stu-id="39c30-114">Separate excluded types with a comma:</span></span> 

```
&responseFilter=-images,-videos
```

<span data-ttu-id="39c30-115">Although Bing did not return video and news results in the previous response, it does not mean that video and news content does not exist.</span><span class="sxs-lookup"><span data-stu-id="39c30-115">Although Bing did not return video and news results in the previous response, it does not mean that video and news content does not exist.</span></span> <span data-ttu-id="39c30-116">It simply means that the page didn't include them.</span><span class="sxs-lookup"><span data-stu-id="39c30-116">It simply means that the page didn't include them.</span></span> <span data-ttu-id="39c30-117">However, if you [page](./paging-webpages.md) through more results, the subsequent pages would likely include them.</span><span class="sxs-lookup"><span data-stu-id="39c30-117">However, if you [page](./paging-webpages.md) through more results, the subsequent pages would likely include them.</span></span> <span data-ttu-id="39c30-118">Also, if you call the [Video Search API](../bing-video-search/search-the-web.md) and [News Search API](../bing-news-search/search-the-web.md) endpoints directly, the response would likely contain results.</span><span class="sxs-lookup"><span data-stu-id="39c30-118">Also, if you call the [Video Search API](../bing-video-search/search-the-web.md) and [News Search API](../bing-news-search/search-the-web.md) endpoints directly, the response would likely contain results.</span></span> 

<span data-ttu-id="39c30-119">You are discouraged from using `responseFilter` to get results from a single API.</span><span class="sxs-lookup"><span data-stu-id="39c30-119">You are discouraged from using `responseFilter` to get results from a single API.</span></span> <span data-ttu-id="39c30-120">If you want content from a single Bing API, call that API directly.</span><span class="sxs-lookup"><span data-stu-id="39c30-120">If you want content from a single Bing API, call that API directly.</span></span> <span data-ttu-id="39c30-121">For example, to receive only images, send a request to the Image Search API endpoint, `https://api.cognitive.microsoft.com/bing/v7.0/images/search` or one of the other [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#endpoints) endpoints.</span><span class="sxs-lookup"><span data-stu-id="39c30-121">For example, to receive only images, send a request to the Image Search API endpoint, `https://api.cognitive.microsoft.com/bing/v7.0/images/search` or one of the other [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#endpoints) endpoints.</span></span> <span data-ttu-id="39c30-122">Calling the single API is important not only for performance reasons but because the content-specific APIs offer richer results.</span><span class="sxs-lookup"><span data-stu-id="39c30-122">Calling the single API is important not only for performance reasons but because the content-specific APIs offer richer results.</span></span> <span data-ttu-id="39c30-123">For example, you can use filters that are not available to the Web Search API to filter the results.</span><span class="sxs-lookup"><span data-stu-id="39c30-123">For example, you can use filters that are not available to the Web Search API to filter the results.</span></span>  
  
<span data-ttu-id="39c30-124">To get search results from a specific domain, include the `site:` query operator in the query string.</span><span class="sxs-lookup"><span data-stu-id="39c30-124">To get search results from a specific domain, include the `site:` query operator in the query string.</span></span>  

```
https://api.cognitive.microsoft.com/bing/v7.0/search?q=sailing+dinghies+site:contososailing.com&mkt=en-us
```

> [!NOTE] 
> <span data-ttu-id="39c30-125">Depending on the query, if you use the `site:` query operator, there is the chance that the response may contain adult content regardless of the [safeSearch](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#safesearch) setting.</span><span class="sxs-lookup"><span data-stu-id="39c30-125">Depending on the query, if you use the `site:` query operator, there is the chance that the response may contain adult content regardless of the [safeSearch](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#safesearch) setting.</span></span> <span data-ttu-id="39c30-126">You should use `site:` only if you are aware of the content on the site and your scenario supports the possibility of adult content.</span><span class="sxs-lookup"><span data-stu-id="39c30-126">You should use `site:` only if you are aware of the content on the site and your scenario supports the possibility of adult content.</span></span> 
  
## <a name="limiting-the-number-of-answers-in-the-response"></a><span data-ttu-id="39c30-127">Limiting the number of answers in the response</span><span class="sxs-lookup"><span data-stu-id="39c30-127">Limiting the number of answers in the response</span></span>

<span data-ttu-id="39c30-128">Bing includes answers in the response based on ranking.</span><span class="sxs-lookup"><span data-stu-id="39c30-128">Bing includes answers in the response based on ranking.</span></span> <span data-ttu-id="39c30-129">For example, if you query *sailing+dinghies*, Bing returns `webpages`, `images`, `videos`, and `relatedSearches`.</span><span class="sxs-lookup"><span data-stu-id="39c30-129">For example, if you query *sailing+dinghies*, Bing returns `webpages`, `images`, `videos`, and `relatedSearches`.</span></span>

```json
{
    "_type" : "SearchResponse",
    "queryContext" : {
        "originalQuery" : "sailing dinghies"
    },
    "webPages" : {...},
    "images" : {...},
    "relatedSearches" : {...},
    "videos" : {...},
    "rankingResponse" : {...}
}
```

<span data-ttu-id="39c30-130">To limit the number of answers that Bing returns to the top two answers (webpages and images), set the [answerCount](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#answercount) query parameter to 2.</span><span class="sxs-lookup"><span data-stu-id="39c30-130">To limit the number of answers that Bing returns to the top two answers (webpages and images), set the [answerCount](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#answercount) query parameter to 2.</span></span> 

```  
GET https://api.cognitive.microsoft.com/bing/v7.0/search?q=sailing+dinghies&answerCount=2&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-Search-ClientIP: 999.999.999.999  
X-Search-Location:  47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="39c30-131">The response includes only `webPages` and `images`.</span><span class="sxs-lookup"><span data-stu-id="39c30-131">The response includes only `webPages` and `images`.</span></span>

```json
{
    "_type" : "SearchResponse",
    "queryContext" : {
        "originalQuery" : "sailing dinghies"
    },
    "webPages" : {...},
    "images" : {...},
    "rankingResponse" : {...}
}
```

<span data-ttu-id="39c30-132">If you add the `responseFilter` query parameter to the previous query and set it to webpages and news, the response contains only webpages because news is not ranked.</span><span class="sxs-lookup"><span data-stu-id="39c30-132">If you add the `responseFilter` query parameter to the previous query and set it to webpages and news, the response contains only webpages because news is not ranked.</span></span>

```json
{
    "_type" : "SearchResponse",
    "queryContext" : {
        "originalQuery" : "sailing dinghies"
    },
    "webPages" : {...},
    "rankingResponse" : {...}
}
```

## <a name="promoting-answers-that-are-not-ranked"></a><span data-ttu-id="39c30-133">Promoting answers that are not ranked</span><span class="sxs-lookup"><span data-stu-id="39c30-133">Promoting answers that are not ranked</span></span>

<span data-ttu-id="39c30-134">If the top ranked answers that Bing returns for a query are webpages, images, videos, and relatedSearches, the response would include those answers.</span><span class="sxs-lookup"><span data-stu-id="39c30-134">If the top ranked answers that Bing returns for a query are webpages, images, videos, and relatedSearches, the response would include those answers.</span></span> <span data-ttu-id="39c30-135">If you set [answerCount](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#answercount) to two (2), Bing returns the top two ranked answers: webpages and images.</span><span class="sxs-lookup"><span data-stu-id="39c30-135">If you set [answerCount](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#answercount) to two (2), Bing returns the top two ranked answers: webpages and images.</span></span> <span data-ttu-id="39c30-136">If you want Bing to include images and videos in the response, specify the [promote](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#promote) query parameter and set it to images and videos.</span><span class="sxs-lookup"><span data-stu-id="39c30-136">If you want Bing to include images and videos in the response, specify the [promote](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#promote) query parameter and set it to images and videos.</span></span> 

```  
GET https://api.cognitive.microsoft.com/bing/v7.0/search?q=sailing+dinghies&answerCount=2&promote=images%2Cvideos&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-Search-ClientIP: 999.999.999.999  
X-Search-Location:  47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```  

<span data-ttu-id="39c30-137">The following is the response to the above request.</span><span class="sxs-lookup"><span data-stu-id="39c30-137">The following is the response to the above request.</span></span> <span data-ttu-id="39c30-138">Bing returns the top two answers, webpages and images, and promotes videos into the answer.</span><span class="sxs-lookup"><span data-stu-id="39c30-138">Bing returns the top two answers, webpages and images, and promotes videos into the answer.</span></span>

```json
{
    "_type" : "SearchResponse",
    "queryContext" : {
        "originalQuery" : "sailiing dinghies"
    },
    "webPages" : {...},
    "images" : {...},
    "videos" : {...},
    "rankingResponse" : {...}
}
```

<span data-ttu-id="39c30-139">If you set `promote` to news, the response doesn't include the news answer because it is not a ranked answer&mdash;you can promote only ranked answers.</span><span class="sxs-lookup"><span data-stu-id="39c30-139">If you set `promote` to news, the response doesn't include the news answer because it is not a ranked answer&mdash;you can promote only ranked answers.</span></span>

<span data-ttu-id="39c30-140">The answers that you want to promote do not count against the `answerCount` limit.</span><span class="sxs-lookup"><span data-stu-id="39c30-140">The answers that you want to promote do not count against the `answerCount` limit.</span></span> <span data-ttu-id="39c30-141">For example, if the ranked answers are news, images, and videos, and you set `answerCount` to 1 and `promote` to news, the response contains news and images.</span><span class="sxs-lookup"><span data-stu-id="39c30-141">For example, if the ranked answers are news, images, and videos, and you set `answerCount` to 1 and `promote` to news, the response contains news and images.</span></span> <span data-ttu-id="39c30-142">Or, if the ranked answers are videos, images, and news, the response contains videos and news.</span><span class="sxs-lookup"><span data-stu-id="39c30-142">Or, if the ranked answers are videos, images, and news, the response contains videos and news.</span></span>

<span data-ttu-id="39c30-143">You may use `promote` only if you specify the `answerCount` query parameter.</span><span class="sxs-lookup"><span data-stu-id="39c30-143">You may use `promote` only if you specify the `answerCount` query parameter.</span></span>
