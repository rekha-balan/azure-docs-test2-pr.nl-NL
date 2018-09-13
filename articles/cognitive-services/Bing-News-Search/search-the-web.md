---
title: What is Bing News Search? | Microsoft Docs
description: Shows how to use the Bing News Search API to search the web for news.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 4B35B035-34FB-403A-9F52-6470AF726FB6
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: overview
ms.date: 06/21/2016
ms.author: scottwhi
ms.openlocfilehash: 977b2e10c8a2ceccc5a6ffb3f396e6721afe1816
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869221"
---
# <a name="what-is-bing-news-search"></a><span data-ttu-id="19937-104">What is Bing News Search?</span><span class="sxs-lookup"><span data-stu-id="19937-104">What is Bing News Search?</span></span>

<span data-ttu-id="19937-105">The Bing News Search API provides a similar (but not exact) experience to [Bing News](https://www.bing.com/news).</span><span class="sxs-lookup"><span data-stu-id="19937-105">The Bing News Search API provides a similar (but not exact) experience to [Bing News](https://www.bing.com/news).</span></span> <span data-ttu-id="19937-106">The Bing News Search API lets you send a search query to Bing and get back a list of relevant news articles.</span><span class="sxs-lookup"><span data-stu-id="19937-106">The Bing News Search API lets you send a search query to Bing and get back a list of relevant news articles.</span></span>

<span data-ttu-id="19937-107">If you're building a news-only search results page to find news that's relevant to the user's search query, call this API instead of calling the more general [Bing Web Search API](../bing-web-search/search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="19937-107">If you're building a news-only search results page to find news that's relevant to the user's search query, call this API instead of calling the more general [Bing Web Search API](../bing-web-search/search-the-web.md).</span></span> <span data-ttu-id="19937-108">If you want news and other types of content such as webpages, images, and videos, then call the Bing Web Search API.</span><span class="sxs-lookup"><span data-stu-id="19937-108">If you want news and other types of content such as webpages, images, and videos, then call the Bing Web Search API.</span></span>

## <a name="suggesting--using-search-terms"></a><span data-ttu-id="19937-109">Suggesting & using search terms</span><span class="sxs-lookup"><span data-stu-id="19937-109">Suggesting & using search terms</span></span>

<span data-ttu-id="19937-110">If you provide a search box where the user enters their search term, use the [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span><span class="sxs-lookup"><span data-stu-id="19937-110">If you provide a search box where the user enters their search term, use the [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span></span> <span data-ttu-id="19937-111">The API returns suggested query strings based on partial search terms as the user types.</span><span class="sxs-lookup"><span data-stu-id="19937-111">The API returns suggested query strings based on partial search terms as the user types.</span></span>

<span data-ttu-id="19937-112">After the user enters their search term, URL encode it before setting the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#query) query parameter.</span><span class="sxs-lookup"><span data-stu-id="19937-112">After the user enters their search term, URL encode it before setting the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#query) query parameter.</span></span> <span data-ttu-id="19937-113">For example, if the user enters *sailing dinghies*, set `q` to `sailing+dinghies` or `sailing%20dinghies`.</span><span class="sxs-lookup"><span data-stu-id="19937-113">For example, if the user enters *sailing dinghies*, set `q` to `sailing+dinghies` or `sailing%20dinghies`.</span></span>

## <a name="getting-general-news"></a><span data-ttu-id="19937-114">Getting general news</span><span class="sxs-lookup"><span data-stu-id="19937-114">Getting general news</span></span>

<span data-ttu-id="19937-115">To get general news articles related to the user's search term from the web, send the following GET request:</span><span class="sxs-lookup"><span data-stu-id="19937-115">To get general news articles related to the user's search term from the web, send the following GET request:</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/news/search?q=sailing+dinghies&mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)
X-Search-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

<span data-ttu-id="19937-116">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span><span class="sxs-lookup"><span data-stu-id="19937-116">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span></span> <span data-ttu-id="19937-117">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span><span class="sxs-lookup"><span data-stu-id="19937-117">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span></span>

<span data-ttu-id="19937-118">To get news from a specific domain, use the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator.</span><span class="sxs-lookup"><span data-stu-id="19937-118">To get news from a specific domain, use the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator.</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/news/search?q=sailing+dinghies+site:contososailing.com&mkt=en-us HTTP/1.1
```

<span data-ttu-id="19937-119">The following shows the response to the previous query.</span><span class="sxs-lookup"><span data-stu-id="19937-119">The following shows the response to the previous query.</span></span> <span data-ttu-id="19937-120">You must display each news article in the order provided in the response.</span><span class="sxs-lookup"><span data-stu-id="19937-120">You must display each news article in the order provided in the response.</span></span> <span data-ttu-id="19937-121">If the article has clustered articles, you should indicate that related articles exist and display them if the user requests to see them.</span><span class="sxs-lookup"><span data-stu-id="19937-121">If the article has clustered articles, you should indicate that related articles exist and display them if the user requests to see them.</span></span>

```json
{
    "_type" : "News",
    "readLink" : "https:\/\/api.cognitive.microsoft.com\/bing\/v5\/news\/search?q=sailing+dinghies",
    "totalEstimatedMatches" : 88400,
    "value" : [{
        "name" : "Sailing Vies for Four Trophies",
        "url" : "http:\/\/www.bing.com\/cr?IG=CCE2F06CA750455891FE99A72...",
        "image" : {
            "thumbnail" : {
                "contentUrl" : "https:\/\/www.bing.com\/th?id=ON.9C23AA5...",
                "width" : 650,
                "height" : 341
            }
        },
        "description" : "College Rankings, presented by Zim...",
        "provider" : [{
            "_type" : "Organization",
            "name" : "contoso.com"
        }],
        "datePublished" : "2017-04-14T15:28:00"
    },

    ...

    {
        "name" : "Fabrikam Sailing Club to host Mirror Dinghy...",
        "url" : "http:\/\/www.bing.com\/cr?IG=CCE2F06CA750455891F...",
        "image" : {
            "thumbnail" : {
                "contentUrl" : "https:\/\/www.bing.com\/th?id=ON.36...",
                "width" : 448,
                "height" : 300
            }
        },
        "description" : "The sailing club that trained Olympian Ben...",
        "provider" : [{
            "_type" : "Organization",
            "name" : "Contoso"
        }],
        "datePublished" : "2017-04-04T11:02:00",
        "category" : "Sports"
    }]
}
```

<span data-ttu-id="19937-122">The [news](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v5-reference#news) answer lists the news articles that Bing thought were relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="19937-122">The [news](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v5-reference#news) answer lists the news articles that Bing thought were relevant to the query.</span></span> <span data-ttu-id="19937-123">The `totalEstimatedMatches` field contains an estimate of the number of articles available to view.</span><span class="sxs-lookup"><span data-stu-id="19937-123">The `totalEstimatedMatches` field contains an estimate of the number of articles available to view.</span></span> <span data-ttu-id="19937-124">For information about paging through the articles, see [Paging News](./paging-news.md).</span><span class="sxs-lookup"><span data-stu-id="19937-124">For information about paging through the articles, see [Paging News](./paging-news.md).</span></span>

<span data-ttu-id="19937-125">Each [news article](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v5-reference#newsarticle) in the list includes the article's name, description, and URL to the article on the host's website.</span><span class="sxs-lookup"><span data-stu-id="19937-125">Each [news article](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v5-reference#newsarticle) in the list includes the article's name, description, and URL to the article on the host's website.</span></span> <span data-ttu-id="19937-126">If the article contains an image, the object includes a thumbnail of the image.</span><span class="sxs-lookup"><span data-stu-id="19937-126">If the article contains an image, the object includes a thumbnail of the image.</span></span> <span data-ttu-id="19937-127">Use `name` and `url` to create a hyperlink that takes the user to the news article on the host's site.</span><span class="sxs-lookup"><span data-stu-id="19937-127">Use `name` and `url` to create a hyperlink that takes the user to the news article on the host's site.</span></span> <span data-ttu-id="19937-128">If the article includes an image, also make the image clickable using `url`.</span><span class="sxs-lookup"><span data-stu-id="19937-128">If the article includes an image, also make the image clickable using `url`.</span></span> <span data-ttu-id="19937-129">Be sure to use `provider` to attribute the article.</span><span class="sxs-lookup"><span data-stu-id="19937-129">Be sure to use `provider` to attribute the article.</span></span>

<span data-ttu-id="19937-130">If Bing can determine the category of news article, the article includes the `category` field.</span><span class="sxs-lookup"><span data-stu-id="19937-130">If Bing can determine the category of news article, the article includes the `category` field.</span></span>

## <a name="getting-todays-top-news"></a><span data-ttu-id="19937-131">Getting today's top news</span><span class="sxs-lookup"><span data-stu-id="19937-131">Getting today's top news</span></span>

<span data-ttu-id="19937-132">To get today's top news articles, you'd make the same request as getting general news except that you'd leave `q` unset.</span><span class="sxs-lookup"><span data-stu-id="19937-132">To get today's top news articles, you'd make the same request as getting general news except that you'd leave `q` unset.</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/news/search?q=&mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)
X-Search-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

<span data-ttu-id="19937-133">The response for getting top news is almost the same as getting general news.</span><span class="sxs-lookup"><span data-stu-id="19937-133">The response for getting top news is almost the same as getting general news.</span></span> <span data-ttu-id="19937-134">However, the `news` answer doesn't include the `totalEstimatedMatches` field because there's a set number of results.</span><span class="sxs-lookup"><span data-stu-id="19937-134">However, the `news` answer doesn't include the `totalEstimatedMatches` field because there's a set number of results.</span></span> <span data-ttu-id="19937-135">The number of top news articles may vary depending on the news cycle.</span><span class="sxs-lookup"><span data-stu-id="19937-135">The number of top news articles may vary depending on the news cycle.</span></span> <span data-ttu-id="19937-136">Be sure to use `provider` to attribute the article.</span><span class="sxs-lookup"><span data-stu-id="19937-136">Be sure to use `provider` to attribute the article.</span></span>

## <a name="getting-news-by-category"></a><span data-ttu-id="19937-137">Getting news by category</span><span class="sxs-lookup"><span data-stu-id="19937-137">Getting news by category</span></span>

<span data-ttu-id="19937-138">To get news articles by category, such as the top sports or entertainment articles, send the following GET request to Bing:</span><span class="sxs-lookup"><span data-stu-id="19937-138">To get news articles by category, such as the top sports or entertainment articles, send the following GET request to Bing:</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/news?category=sports&mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)
X-Search-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

<span data-ttu-id="19937-139">Use the [category](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#category) query parameter to specify the category of articles to get.</span><span class="sxs-lookup"><span data-stu-id="19937-139">Use the [category](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#category) query parameter to specify the category of articles to get.</span></span> <span data-ttu-id="19937-140">For a list of possible news categories that you may specify, see [News Categories by Market](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#news-categories-by-market).</span><span class="sxs-lookup"><span data-stu-id="19937-140">For a list of possible news categories that you may specify, see [News Categories by Market](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#news-categories-by-market).</span></span>

<span data-ttu-id="19937-141">The response for getting news by category is almost the same as getting general news.</span><span class="sxs-lookup"><span data-stu-id="19937-141">The response for getting news by category is almost the same as getting general news.</span></span> <span data-ttu-id="19937-142">However, the articles are all from the specified category.</span><span class="sxs-lookup"><span data-stu-id="19937-142">However, the articles are all from the specified category.</span></span>

## <a name="getting-headline-news"></a><span data-ttu-id="19937-143">Getting headline news</span><span class="sxs-lookup"><span data-stu-id="19937-143">Getting headline news</span></span>

<span data-ttu-id="19937-144">To request headline news articles and get articles from all news categories, send the following GET request to Bing:</span><span class="sxs-lookup"><span data-stu-id="19937-144">To request headline news articles and get articles from all news categories, send the following GET request to Bing:</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/news?mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)
X-MSEdge-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

<span data-ttu-id="19937-145">Do not include the [category](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#category) query parameter.</span><span class="sxs-lookup"><span data-stu-id="19937-145">Do not include the [category](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#category) query parameter.</span></span>

<span data-ttu-id="19937-146">The response for getting headline news is the same as getting today's top news.</span><span class="sxs-lookup"><span data-stu-id="19937-146">The response for getting headline news is the same as getting today's top news.</span></span> <span data-ttu-id="19937-147">If the article is a headline article, its `headline` field is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="19937-147">If the article is a headline article, its `headline` field is set to **true**.</span></span>

<span data-ttu-id="19937-148">By default, the response includes up to 12 headline articles.</span><span class="sxs-lookup"><span data-stu-id="19937-148">By default, the response includes up to 12 headline articles.</span></span> <span data-ttu-id="19937-149">To change the number of headline articles to return, specify the [headlineCount](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#headlinecount) query parameter.</span><span class="sxs-lookup"><span data-stu-id="19937-149">To change the number of headline articles to return, specify the [headlineCount](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#headlinecount) query parameter.</span></span> <span data-ttu-id="19937-150">The response also includes up to four non-headline articles per news category.</span><span class="sxs-lookup"><span data-stu-id="19937-150">The response also includes up to four non-headline articles per news category.</span></span>

<span data-ttu-id="19937-151">The response counts clusters as one article.</span><span class="sxs-lookup"><span data-stu-id="19937-151">The response counts clusters as one article.</span></span> <span data-ttu-id="19937-152">Because a cluster may have several articles, the response may include more than 12 headline articles and more than four non-headline articles per category.</span><span class="sxs-lookup"><span data-stu-id="19937-152">Because a cluster may have several articles, the response may include more than 12 headline articles and more than four non-headline articles per category.</span></span>

## <a name="getting-trending-news"></a><span data-ttu-id="19937-153">Getting trending news</span><span class="sxs-lookup"><span data-stu-id="19937-153">Getting trending news</span></span>

<span data-ttu-id="19937-154">To get news topics that are trending on social networks, send the following GET request to Bing:</span><span class="sxs-lookup"><span data-stu-id="19937-154">To get news topics that are trending on social networks, send the following GET request to Bing:</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/news/trendingtopics?mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)
X-Search-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
X-MSAPI-UserState: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

> [!NOTE]
> <span data-ttu-id="19937-155">Trending Topics is available only in the en-US and zh-CN markets.</span><span class="sxs-lookup"><span data-stu-id="19937-155">Trending Topics is available only in the en-US and zh-CN markets.</span></span>

<span data-ttu-id="19937-156">The following JSON is the response to the preceding request.</span><span class="sxs-lookup"><span data-stu-id="19937-156">The following JSON is the response to the preceding request.</span></span> <span data-ttu-id="19937-157">Each trending news article includes a related image, breaking news flag, and a URL to the Bing search results for the article.</span><span class="sxs-lookup"><span data-stu-id="19937-157">Each trending news article includes a related image, breaking news flag, and a URL to the Bing search results for the article.</span></span> <span data-ttu-id="19937-158">Use the URL in the `webSearchUrl` field to take the user to the Bing search results page.</span><span class="sxs-lookup"><span data-stu-id="19937-158">Use the URL in the `webSearchUrl` field to take the user to the Bing search results page.</span></span> <span data-ttu-id="19937-159">Or, use the query text to call the [Web Search API](../bing-web-search/search-the-web.md) to display the results yourself.</span><span class="sxs-lookup"><span data-stu-id="19937-159">Or, use the query text to call the [Web Search API](../bing-web-search/search-the-web.md) to display the results yourself.</span></span>

```json
{
    "_type" : "TrendingTopics",
    "value" : [{
        "name" : "Canada pot measure",
        "image" : {
            "url" : "https:\/\/www.bing.com\/th?id=OPN.RTNews_hHD...",
            "provider" : [{
                "_type" : "Organization",
                "name" : "Contoso Images"
            }]
        },
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=070292D8CEDD...",
        "isBreakingNews" : false,
        "query" : {
            "text" : "Canada marijuana"
        }
    },
    {
        "name" : "Down on Vegas move",
        "image" : {
            "url" : "https:\/\/www.bing.com\/th?id=OPN.RTNews_Bfbmg8h...",
            "provider" : [{
                "_type" : "Organization",
                "name" : "Contoso"
            }]
        },
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=070292D8CEDD...",
        "isBreakingNews" : false,
        "query" : {
            "text" : "Marcus Appel Las Vegas"
        }
    },

    ...

    ]
}
```

## <a name="getting-related-news"></a><span data-ttu-id="19937-160">Getting related news</span><span class="sxs-lookup"><span data-stu-id="19937-160">Getting related news</span></span>

<span data-ttu-id="19937-161">If there are other articles that are related to a news article, the news article may include the [clusteredArticles](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#newsarticle-clusteredarticles) field.</span><span class="sxs-lookup"><span data-stu-id="19937-161">If there are other articles that are related to a news article, the news article may include the [clusteredArticles](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#newsarticle-clusteredarticles) field.</span></span> <span data-ttu-id="19937-162">The following shows an article with clustered articles.</span><span class="sxs-lookup"><span data-stu-id="19937-162">The following shows an article with clustered articles.</span></span>

```json
    {
        "name" : "Playoffs 2017: Betting lines, point spreads...",
        "url" : "http:\/\/www.bing.com\/cr?IG=4B7056CEC271408997D115...",
        "image" : {
            "thumbnail" : {
                "contentUrl" : "https:\/\/www.bing.com\/th?id=ON.D7B1...",
                "width" : 700,
                "height" : 393
            }
        },
        "description" : "April 14, 2017 3:37pm EDT April 14, 2017 3:34pm...",
        "provider" : [{
            "_type" : "Organization",
            "name" : "Contoso"
        }],
        "datePublished" : "2017-04-14T19:43:00",
        "category" : "Sports",
        "clusteredArticles" : [{
            "name" : "Playoffs 2017: Betting odds, favorites to win...",
            "url" : "http:\/\/www.bing.com\/cr?IG=4B7056CEC271408997D1159E...",
            "description" : "April 14, 2017 3:30pm EDT April 14, 2017 3:27pm...",
            "provider" : [{
                "_type" : "Organization",
                "name" : "Contoso"
            }],
            "datePublished" : "2017-04-14T19:37:00",
            "category" : "Sports"
        }]
    },
```

## <a name="throttling-requests"></a><span data-ttu-id="19937-163">Throttling requests</span><span class="sxs-lookup"><span data-stu-id="19937-163">Throttling requests</span></span>

[!INCLUDE [cognitive-services-bing-throttling-requests](../../../includes/cognitive-services-bing-throttling-requests.md)]

## <a name="next-steps"></a><span data-ttu-id="19937-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="19937-164">Next steps</span></span>

<span data-ttu-id="19937-165">To get started quickly with your first request, see [Making Your First Request](./quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="19937-165">To get started quickly with your first request, see [Making Your First Request](./quickstart.md).</span></span>

<span data-ttu-id="19937-166">Familiarize yourself with the [Bing News Search API v7] (https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference) reference.</span><span class="sxs-lookup"><span data-stu-id="19937-166">Familiarize yourself with the [Bing News Search API v7] (https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference) reference.</span></span> <span data-ttu-id="19937-167">The reference contains the list of endpoints, headers, and query parameters that you'd use to request search results.</span><span class="sxs-lookup"><span data-stu-id="19937-167">The reference contains the list of endpoints, headers, and query parameters that you'd use to request search results.</span></span> <span data-ttu-id="19937-168">It also includes definitions of the response objects.</span><span class="sxs-lookup"><span data-stu-id="19937-168">It also includes definitions of the response objects.</span></span>

<span data-ttu-id="19937-169">To improve your search box user experience, see [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md).</span><span class="sxs-lookup"><span data-stu-id="19937-169">To improve your search box user experience, see [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md).</span></span> <span data-ttu-id="19937-170">As the user enters their query term, you can call this API to get relevant query terms that were used by others.</span><span class="sxs-lookup"><span data-stu-id="19937-170">As the user enters their query term, you can call this API to get relevant query terms that were used by others.</span></span>

<span data-ttu-id="19937-171">Be sure to read [Bing Use and Display Requirements](./useanddisplayrequirements.md) so you don't break any of the rules about using the search results.</span><span class="sxs-lookup"><span data-stu-id="19937-171">Be sure to read [Bing Use and Display Requirements](./useanddisplayrequirements.md) so you don't break any of the rules about using the search results.</span></span>