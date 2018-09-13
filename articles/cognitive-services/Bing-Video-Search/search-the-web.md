---
title: What is Bing Video Search? | Microsoft Docs
description: Shows how to use the Bing Video Search API to search the web for videos.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 4A76718B-E32C-419F-98DF-19E877643378
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: overview
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 9de59f0289e41a1d8164bf1d9aaf4c20cd661058
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869529"
---
# <a name="what-is-bing-video-search"></a><span data-ttu-id="c6fab-104">What is Bing Video Search?</span><span class="sxs-lookup"><span data-stu-id="c6fab-104">What is Bing Video Search?</span></span>

<span data-ttu-id="c6fab-105">The Bing Video Search API provides a similar (but not exact) experience to [Bing Videos](https://www.bing.com/videos).</span><span class="sxs-lookup"><span data-stu-id="c6fab-105">The Bing Video Search API provides a similar (but not exact) experience to [Bing Videos](https://www.bing.com/videos).</span></span> <span data-ttu-id="c6fab-106">The Bing Video Search API lets you send a search query to Bing and get back a list of relevant videos.</span><span class="sxs-lookup"><span data-stu-id="c6fab-106">The Bing Video Search API lets you send a search query to Bing and get back a list of relevant videos.</span></span>

<span data-ttu-id="c6fab-107">If you're building a videos-only search results page to find videos that are relevant to the user's search query, call this API instead of calling the more general [Bing Web Search API](../bing-web-search/search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="c6fab-107">If you're building a videos-only search results page to find videos that are relevant to the user's search query, call this API instead of calling the more general [Bing Web Search API](../bing-web-search/search-the-web.md).</span></span> <span data-ttu-id="c6fab-108">If you want videos and other types of content such as webpages, news, and images, then call the Bing Web Search API.</span><span class="sxs-lookup"><span data-stu-id="c6fab-108">If you want videos and other types of content such as webpages, news, and images, then call the Bing Web Search API.</span></span>

## <a name="suggesting--using-search-terms"></a><span data-ttu-id="c6fab-109">Suggesting & using search terms</span><span class="sxs-lookup"><span data-stu-id="c6fab-109">Suggesting & using search terms</span></span>

<span data-ttu-id="c6fab-110">If you provide a search box where the user enters their search term, use the [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span><span class="sxs-lookup"><span data-stu-id="c6fab-110">If you provide a search box where the user enters their search term, use the [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span></span> <span data-ttu-id="c6fab-111">The API returns suggested query strings based on partial search terms as the user types.</span><span class="sxs-lookup"><span data-stu-id="c6fab-111">The API returns suggested query strings based on partial search terms as the user types.</span></span>

<span data-ttu-id="c6fab-112">After the user enters their search term, URL encode it before setting the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query) query parameter.</span><span class="sxs-lookup"><span data-stu-id="c6fab-112">After the user enters their search term, URL encode it before setting the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query) query parameter.</span></span> <span data-ttu-id="c6fab-113">For example, if the user enters *sailing dinghies*, set `q` to `sailing+dinghies` or `sailing%20dinghies`.</span><span class="sxs-lookup"><span data-stu-id="c6fab-113">For example, if the user enters *sailing dinghies*, set `q` to `sailing+dinghies` or `sailing%20dinghies`.</span></span>

## <a name="getting-videos"></a><span data-ttu-id="c6fab-114">Getting videos</span><span class="sxs-lookup"><span data-stu-id="c6fab-114">Getting videos</span></span>

<span data-ttu-id="c6fab-115">To get videos related to the user's search term from the web, send the following GET request:</span><span class="sxs-lookup"><span data-stu-id="c6fab-115">To get videos related to the user's search term from the web, send the following GET request:</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/search?q=sailing+dinghies&mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)
X-Search-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

<span data-ttu-id="c6fab-116">All requests must be made from a server.</span><span class="sxs-lookup"><span data-stu-id="c6fab-116">All requests must be made from a server.</span></span>

<span data-ttu-id="c6fab-117">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span><span class="sxs-lookup"><span data-stu-id="c6fab-117">If it's your first time calling any of the Bing APIs, don't include the client ID header.</span></span> <span data-ttu-id="c6fab-118">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span><span class="sxs-lookup"><span data-stu-id="c6fab-118">Only include the client ID if you've previously called a Bing API and Bing returned a client ID for the user and device combination.</span></span>

<span data-ttu-id="c6fab-119">To get videos from a specific domain, use the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator.</span><span class="sxs-lookup"><span data-stu-id="c6fab-119">To get videos from a specific domain, use the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator.</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/search?q=sailing+dinghies+site:contososailing.com&mkt=en-us HTTP/1.1
```

<span data-ttu-id="c6fab-120">The response contains a [Videos](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos) answer that contains a list of videos that Bing thought were relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="c6fab-120">The response contains a [Videos](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos) answer that contains a list of videos that Bing thought were relevant to the query.</span></span> <span data-ttu-id="c6fab-121">Each [Video](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video) object in the list includes the URL of the video, its duration, its dimensions, and its encoding format among other attributes.</span><span class="sxs-lookup"><span data-stu-id="c6fab-121">Each [Video](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video) object in the list includes the URL of the video, its duration, its dimensions, and its encoding format among other attributes.</span></span> <span data-ttu-id="c6fab-122">The video object also includes the URL of a thumbnail of the video and the thumbnail's dimensions.</span><span class="sxs-lookup"><span data-stu-id="c6fab-122">The video object also includes the URL of a thumbnail of the video and the thumbnail's dimensions.</span></span>

```json
{
    "_type" : "Videos",
    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=81EF7545...",
    "totalEstimatedMatches" : 1000,
    "value" : [
        {
            "name" : "How to sail - What to Wear for Dinghy Sailing",
            "description" : "An informative video on what to wear when...",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=81EF7...",
            "thumbnailUrl" : "https:\/\/tse4.mm.bing.net\/th?id=OVP.DYW...",
            "datePublished" : "2014-03-04T11:51:53",
            "publisher" : [
                {
                    "name" : "Fabrikam"
                }
            ],
            "creator" : 
            {
                "name" : "Marcus Appel"
            },
            "contentUrl" : "https:\/\/www.fabrikam.com\/watch?v=vzmPjZ--g",
            "hostPageUrl" : "https:\/\/www.bing.com\/cr?IG=81EF7545D569...",
            "encodingFormat" : "h264",
            "hostPageDisplayUrl" : "https:\/\/www.fabrikam.com\/watch?v=vzmPjZ--g",
            "width" : 1280,
            "height" : 720,
            "duration" : "PT2M47S",
            "motionThumbnailUrl" : "https:\/\/tse3.mm.bing.net\/th?id=OM.Y62...",
            "embedHtml" : "<iframe width=\"1280\" height=\"720\" src=\"https:...><\/iframe>",
            "allowHttpsEmbed" : true,
            "viewCount" : 8743,
            "thumbnail" : 
            {
                "width" : 300,
                "height" : 168
            },
            "videoId" : "6DB795E11A6E3CBAAD636DB795E113CBAAD63",
            "allowMobileEmbed" : true,
            "isSuperfresh" : false
        },
        ...
    ],
    "queryExpansions" : [...],
    "nextOffsetAddCount" : 0,
    "pivotSuggestions" : [...]
}
```

<span data-ttu-id="c6fab-123">You could display a collage of all the video thumbnails or you could display a subset of the thumbnails.</span><span class="sxs-lookup"><span data-stu-id="c6fab-123">You could display a collage of all the video thumbnails or you could display a subset of the thumbnails.</span></span> <span data-ttu-id="c6fab-124">If you display a subset, provide the user an option to view the remaining videos.</span><span class="sxs-lookup"><span data-stu-id="c6fab-124">If you display a subset, provide the user an option to view the remaining videos.</span></span> <span data-ttu-id="c6fab-125">You must display the videos in the order provided in the response.</span><span class="sxs-lookup"><span data-stu-id="c6fab-125">You must display the videos in the order provided in the response.</span></span> <span data-ttu-id="c6fab-126">For information about resizing the thumbnail, see [Resizing and Cropping Thumbnails](./resize-and-crop-thumbnails.md).</span><span class="sxs-lookup"><span data-stu-id="c6fab-126">For information about resizing the thumbnail, see [Resizing and Cropping Thumbnails](./resize-and-crop-thumbnails.md).</span></span> 

<span data-ttu-id="c6fab-127">As the user hovers over the thumbnail you can use [motionThumbnailUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-motionthumbnailurl) to play a thumbnail version of the video.</span><span class="sxs-lookup"><span data-stu-id="c6fab-127">As the user hovers over the thumbnail you can use [motionThumbnailUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-motionthumbnailurl) to play a thumbnail version of the video.</span></span> <span data-ttu-id="c6fab-128">Be sure to attribute the motion thumbnail when you display it.</span><span class="sxs-lookup"><span data-stu-id="c6fab-128">Be sure to attribute the motion thumbnail when you display it.</span></span>

<!-- Removing until the images can be sanitized.
![Motion thumbnail of a video](../bing-web-search/media/cognitive-services-bing-web-api/bing-web-video-motion-thumbnail.PNG)
-->

<span data-ttu-id="c6fab-129">If the user clicks the thumbnail, the following are the video viewing options:</span><span class="sxs-lookup"><span data-stu-id="c6fab-129">If the user clicks the thumbnail, the following are the video viewing options:</span></span>

- <span data-ttu-id="c6fab-130">Use [hostPageUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-hostpageurl) to view the video on the host website (for example, YouTube)</span><span class="sxs-lookup"><span data-stu-id="c6fab-130">Use [hostPageUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-hostpageurl) to view the video on the host website (for example, YouTube)</span></span>
- <span data-ttu-id="c6fab-131">Use [webSearchUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-websearchurl) to view the video in the Bing video browser</span><span class="sxs-lookup"><span data-stu-id="c6fab-131">Use [webSearchUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-websearchurl) to view the video in the Bing video browser</span></span>
- <span data-ttu-id="c6fab-132">Use [embdedHtml](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-embedhtml) to embed the video in your own experience</span><span class="sxs-lookup"><span data-stu-id="c6fab-132">Use [embdedHtml](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-embedhtml) to embed the video in your own experience</span></span> 

<span data-ttu-id="c6fab-133">Be sure to use the publisher and creator to attribute the video when you play it.</span><span class="sxs-lookup"><span data-stu-id="c6fab-133">Be sure to use the publisher and creator to attribute the video when you play it.</span></span>

<span data-ttu-id="c6fab-134">For details about using [videoId](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-videoid) to get insights about the video, see [Video Insights](./video-insights.md).</span><span class="sxs-lookup"><span data-stu-id="c6fab-134">For details about using [videoId](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video-videoid) to get insights about the video, see [Video Insights](./video-insights.md).</span></span>

## <a name="filtering-videos"></a><span data-ttu-id="c6fab-135">Filtering videos</span><span class="sxs-lookup"><span data-stu-id="c6fab-135">Filtering videos</span></span>

<span data-ttu-id="c6fab-136">By default, the Video Search API returns all videos that are relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="c6fab-136">By default, the Video Search API returns all videos that are relevant to the query.</span></span> <span data-ttu-id="c6fab-137">If you only want free videos or videos less than five minutes in length, you'd use the following filter query parameters:</span><span class="sxs-lookup"><span data-stu-id="c6fab-137">If you only want free videos or videos less than five minutes in length, you'd use the following filter query parameters:</span></span>

- <span data-ttu-id="c6fab-138">[pricing](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#pricing)&mdash;Filter videos by pricing (for example, videos that are free or that you have to pay for)</span><span class="sxs-lookup"><span data-stu-id="c6fab-138">[pricing](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#pricing)&mdash;Filter videos by pricing (for example, videos that are free or that you have to pay for)</span></span>
- <span data-ttu-id="c6fab-139">[resolution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#resolution)&mdash;Filter videos by resolution (for example, videos with a 720p or higher resolution)</span><span class="sxs-lookup"><span data-stu-id="c6fab-139">[resolution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#resolution)&mdash;Filter videos by resolution (for example, videos with a 720p or higher resolution)</span></span>
- <span data-ttu-id="c6fab-140">[videoLength](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videolength)&mdash;Filter videos by video length (for example, videos that are less than five minutes in length)</span><span class="sxs-lookup"><span data-stu-id="c6fab-140">[videoLength](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videolength)&mdash;Filter videos by video length (for example, videos that are less than five minutes in length)</span></span>
- <span data-ttu-id="c6fab-141">[freshness](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#freshness)&mdash;Filter videos by age (for example, videos discovered by Bing in the past week)</span><span class="sxs-lookup"><span data-stu-id="c6fab-141">[freshness](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#freshness)&mdash;Filter videos by age (for example, videos discovered by Bing in the past week)</span></span>

<span data-ttu-id="c6fab-142">To get videos from a specific domain, include the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator in the query string.</span><span class="sxs-lookup"><span data-stu-id="c6fab-142">To get videos from a specific domain, include the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator in the query string.</span></span>

> [!NOTE]
> <span data-ttu-id="c6fab-143">Depending on the query, if you use the `site:` query operator, there is the chance that the response contains adult content regardless of the [safeSearch](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#safesearch) setting.</span><span class="sxs-lookup"><span data-stu-id="c6fab-143">Depending on the query, if you use the `site:` query operator, there is the chance that the response contains adult content regardless of the [safeSearch](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#safesearch) setting.</span></span> <span data-ttu-id="c6fab-144">You should use `site:` only if you are aware of the content on the site and your scenario supports the possibility of adult content.</span><span class="sxs-lookup"><span data-stu-id="c6fab-144">You should use `site:` only if you are aware of the content on the site and your scenario supports the possibility of adult content.</span></span>

<span data-ttu-id="c6fab-145">The following example shows how to get free videos from ContosoSailing.com that have a resolution of 720p or better and that Bing has discovered in the past month.</span><span class="sxs-lookup"><span data-stu-id="c6fab-145">The following example shows how to get free videos from ContosoSailing.com that have a resolution of 720p or better and that Bing has discovered in the past month.</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/search?q=sailing+dinghies+site:contososailing.com&pricing=free&freshness=month&resolution=720p&mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)
X-MSEdge-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

## <a name="expanding-the-query"></a><span data-ttu-id="c6fab-146">Expanding the query</span><span class="sxs-lookup"><span data-stu-id="c6fab-146">Expanding the query</span></span>

<span data-ttu-id="c6fab-147">If Bing can expand the query to narrow the original search, the [Videos](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos) object contains the `queryExpansions` field.</span><span class="sxs-lookup"><span data-stu-id="c6fab-147">If Bing can expand the query to narrow the original search, the [Videos](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos) object contains the `queryExpansions` field.</span></span> <span data-ttu-id="c6fab-148">For example, if the query was *Cleaning Gutters*, the expanded queries might be: Gutter Cleaning **Tools**, Cleaning Gutters **From the Ground**, Gutter Cleaning **Machine**, and **Easy** Gutter Cleaning.</span><span class="sxs-lookup"><span data-stu-id="c6fab-148">For example, if the query was *Cleaning Gutters*, the expanded queries might be: Gutter Cleaning **Tools**, Cleaning Gutters **From the Ground**, Gutter Cleaning **Machine**, and **Easy** Gutter Cleaning.</span></span>

<span data-ttu-id="c6fab-149">The following example shows the expanded queries for *Cleaning Gutters*.</span><span class="sxs-lookup"><span data-stu-id="c6fab-149">The following example shows the expanded queries for *Cleaning Gutters*.</span></span>

```json
{
    "_type" : "Videos",
    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=B52FBC5...",
    "totalEstimatedMatches" : 1000,
    "value" : [...],
    "nextOffsetAddCount" : 4,
    "queryExpansions" : [
        {
            "text" : "Gutter Cleaning Tools",
            "displayText" : "Tools",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=B52FB....",
            "searchLink" : "https:\/\/api.cognitive.microsoft.com\/api\/v5...",
            "thumbnail" : {
                "thumbnailUrl" : "https:\/\/tse4.mm.bing.net\/th?q=Gutter..."
            }
        },
        ...
    ]
    "pivotSuggestions" : [...],
}
```

<span data-ttu-id="c6fab-150">The `queryExpansions` field contains a list of [Query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query_obj) objects.</span><span class="sxs-lookup"><span data-stu-id="c6fab-150">The `queryExpansions` field contains a list of [Query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query_obj) objects.</span></span> <span data-ttu-id="c6fab-151">The `text` field contains the expanded query and the `displayText` field contains the expansion term.</span><span class="sxs-lookup"><span data-stu-id="c6fab-151">The `text` field contains the expanded query and the `displayText` field contains the expansion term.</span></span> <span data-ttu-id="c6fab-152">You can use the text and thumbnail fields to display the expanded query strings to the user in case the expanded query string is really what they're looking for.</span><span class="sxs-lookup"><span data-stu-id="c6fab-152">You can use the text and thumbnail fields to display the expanded query strings to the user in case the expanded query string is really what they're looking for.</span></span> <span data-ttu-id="c6fab-153">Make the thumbnail and text clickable using the `webSearchUrl` URL or `searchLink` URL.</span><span class="sxs-lookup"><span data-stu-id="c6fab-153">Make the thumbnail and text clickable using the `webSearchUrl` URL or `searchLink` URL.</span></span> <span data-ttu-id="c6fab-154">Use `webSearchUrl` to send the user to the Bing search results, or `searchLink` if you provide your own results page.</span><span class="sxs-lookup"><span data-stu-id="c6fab-154">Use `webSearchUrl` to send the user to the Bing search results, or `searchLink` if you provide your own results page.</span></span>

## <a name="pivoting-the-query"></a><span data-ttu-id="c6fab-155">Pivoting the query</span><span class="sxs-lookup"><span data-stu-id="c6fab-155">Pivoting the query</span></span>

<span data-ttu-id="c6fab-156">If Bing can segment the original search query, the [Videos](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos) object contains the `pivotSuggestions` field.</span><span class="sxs-lookup"><span data-stu-id="c6fab-156">If Bing can segment the original search query, the [Videos](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos) object contains the `pivotSuggestions` field.</span></span> <span data-ttu-id="c6fab-157">For example, if the original query was *Cleaning Gutters*, Bing might segment the query into *Cleaning* and *Gutters*.</span><span class="sxs-lookup"><span data-stu-id="c6fab-157">For example, if the original query was *Cleaning Gutters*, Bing might segment the query into *Cleaning* and *Gutters*.</span></span>

<span data-ttu-id="c6fab-158">The following example shows the pivot suggestions for *Cleaning Gutters*.</span><span class="sxs-lookup"><span data-stu-id="c6fab-158">The following example shows the pivot suggestions for *Cleaning Gutters*.</span></span>

```json
{
    "_type" : "Videos",
    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=B52FBC...",
    "totalEstimatedMatches" : 1000,
    "value" : [...],
    "nextOffsetAddCount" : 0,
    "queryExpansions" : [...],
    "pivotSuggestions" : [
        {
            "pivot" : "cleaning",
            "suggestions" : [
                {
                    "text" : "Gutter Repair",
                    "displayText" : "Repair",
                    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=B52...",
                    "searchLink" : "https:\/\/api.cognitive.microsoft.com\/api\/v5\/videos...",
                    "thumbnail" : {
                        "thumbnailUrl" : "https:\/\/tse3.mm.bing.net\/th?q=Gutter..."
                    }
                },
                ...
            ]
        },
        {
            "pivot" : "gutters",
            "suggestions" : [
                {
                    "text" : "Window Cleaning",
                    "displayText" : "Window",
                    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=B52FBC59...",
                    "searchLink" : "https:\/\/api.cognitive.microsoft.com\/api\/v5...",
                    "thumbnail" : {
                        "thumbnailUrl" : "https:\/\/tse2.mm.bing.net\/th?q=Window..."
                    }
                },
                ...
            ]
        }
    ]
}
```

<span data-ttu-id="c6fab-159">For each pivot, the response contains a list of [Query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query_obj) objects that contain suggested queries.</span><span class="sxs-lookup"><span data-stu-id="c6fab-159">For each pivot, the response contains a list of [Query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#query_obj) objects that contain suggested queries.</span></span> <span data-ttu-id="c6fab-160">The `text` field contains the suggested query and the `displayText` field contains the term that replaces the pivot in the original query.</span><span class="sxs-lookup"><span data-stu-id="c6fab-160">The `text` field contains the suggested query and the `displayText` field contains the term that replaces the pivot in the original query.</span></span> <span data-ttu-id="c6fab-161">For example, Window Cleaning.</span><span class="sxs-lookup"><span data-stu-id="c6fab-161">For example, Window Cleaning.</span></span>

<span data-ttu-id="c6fab-162">You can use the `text` and `thumbnail` fields to display the expanded query strings to the user in case the expanded query string is really what they're looking for.</span><span class="sxs-lookup"><span data-stu-id="c6fab-162">You can use the `text` and `thumbnail` fields to display the expanded query strings to the user in case the expanded query string is really what they're looking for.</span></span> <span data-ttu-id="c6fab-163">Make the thumbnail and text clickable using the `webSearchUrl` URL or `searchLink` URL.</span><span class="sxs-lookup"><span data-stu-id="c6fab-163">Make the thumbnail and text clickable using the `webSearchUrl` URL or `searchLink` URL.</span></span> <span data-ttu-id="c6fab-164">Use `webSearchUrl` to send the user to the Bing search results, or `searchLink` if you provide your own results page.</span><span class="sxs-lookup"><span data-stu-id="c6fab-164">Use `webSearchUrl` to send the user to the Bing search results, or `searchLink` if you provide your own results page.</span></span>

## <a name="throttling-requests"></a><span data-ttu-id="c6fab-165">Throttling requests</span><span class="sxs-lookup"><span data-stu-id="c6fab-165">Throttling requests</span></span>

[!INCLUDE [cognitive-services-bing-throttling-requests](../../../includes/cognitive-services-bing-throttling-requests.md)]

## <a name="next-steps"></a><span data-ttu-id="c6fab-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="c6fab-166">Next steps</span></span>

<span data-ttu-id="c6fab-167">To get started quickly with your first request, see [Making Your First Request](./quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="c6fab-167">To get started quickly with your first request, see [Making Your First Request](./quick-start.md).</span></span>

<span data-ttu-id="c6fab-168">To get your subscription key, see [Subscription Keys](https://azure.microsoft.com/try/cognitive-services/?api=bing-video-search-api).</span><span class="sxs-lookup"><span data-stu-id="c6fab-168">To get your subscription key, see [Subscription Keys](https://azure.microsoft.com/try/cognitive-services/?api=bing-video-search-api).</span></span>

<span data-ttu-id="c6fab-169">Familiarize yourself with the [Bing Video Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) reference.</span><span class="sxs-lookup"><span data-stu-id="c6fab-169">Familiarize yourself with the [Bing Video Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) reference.</span></span> <span data-ttu-id="c6fab-170">The reference contains the list of endpoints, headers, and query parameters that you'd use to request search results.</span><span class="sxs-lookup"><span data-stu-id="c6fab-170">The reference contains the list of endpoints, headers, and query parameters that you'd use to request search results.</span></span> <span data-ttu-id="c6fab-171">It also includes definitions of the response objects.</span><span class="sxs-lookup"><span data-stu-id="c6fab-171">It also includes definitions of the response objects.</span></span> 

<span data-ttu-id="c6fab-172">To improve your search box user experience, see [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md).</span><span class="sxs-lookup"><span data-stu-id="c6fab-172">To improve your search box user experience, see [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md).</span></span> <span data-ttu-id="c6fab-173">As the user enters their query term, you can call this API to get relevant query terms that were used by others.</span><span class="sxs-lookup"><span data-stu-id="c6fab-173">As the user enters their query term, you can call this API to get relevant query terms that were used by others.</span></span>

<span data-ttu-id="c6fab-174">Be sure to read [Bing Use and Display Requirements](./useanddisplayrequirements.md) so you don't break any of the rules about using the search results.</span><span class="sxs-lookup"><span data-stu-id="c6fab-174">Be sure to read [Bing Use and Display Requirements](./useanddisplayrequirements.md) so you don't break any of the rules about using the search results.</span></span>

<span data-ttu-id="c6fab-175">When you call the Video Search API, Bing returns a list of results.</span><span class="sxs-lookup"><span data-stu-id="c6fab-175">When you call the Video Search API, Bing returns a list of results.</span></span> <span data-ttu-id="c6fab-176">The list is a subset of the total number of results that are relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="c6fab-176">The list is a subset of the total number of results that are relevant to the query.</span></span> <span data-ttu-id="c6fab-177">The response's `totalEstimatedMatches` field contains an estimate of the number of videos that are available to view.</span><span class="sxs-lookup"><span data-stu-id="c6fab-177">The response's `totalEstimatedMatches` field contains an estimate of the number of videos that are available to view.</span></span> <span data-ttu-id="c6fab-178">For details about how you'd page through the remaining videos, see [Paging Videos](./paging-videos.md).</span><span class="sxs-lookup"><span data-stu-id="c6fab-178">For details about how you'd page through the remaining videos, see [Paging Videos](./paging-videos.md).</span></span>

<span data-ttu-id="c6fab-179">For details about getting insights about a video, see [Video Insights](./video-insights.md).</span><span class="sxs-lookup"><span data-stu-id="c6fab-179">For details about getting insights about a video, see [Video Insights](./video-insights.md).</span></span>

<span data-ttu-id="c6fab-180">For details about getting trending videos, see [Trending Videos](./trending-videos.md).</span><span class="sxs-lookup"><span data-stu-id="c6fab-180">For details about getting trending videos, see [Trending Videos](./trending-videos.md).</span></span>