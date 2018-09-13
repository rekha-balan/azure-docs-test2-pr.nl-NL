---
title: Bing Web Search API responses | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Learn about answer types and responses provided by the Bing Web Search API.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 8/13/2018
ms.author: erhopf
ms.openlocfilehash: 13e9792f3d5765047dabb4cdef59e85a47a69aba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857070"
---
# <a name="bing-web-search-responses"></a><span data-ttu-id="1c4c7-103">Bing Web Search responses</span><span class="sxs-lookup"><span data-stu-id="1c4c7-103">Bing Web Search responses</span></span>  

<span data-ttu-id="1c4c7-104">When you send Bing Web Search a search request, it returns a [`SearchResponse`](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#searchresponse) object in the response body.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-104">When you send Bing Web Search a search request, it returns a [`SearchResponse`](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#searchresponse) object in the response body.</span></span> <span data-ttu-id="1c4c7-105">The object includes a field for each answer that Bing determined was relevant to query.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-105">The object includes a field for each answer that Bing determined was relevant to query.</span></span> <span data-ttu-id="1c4c7-106">This example illustrates a response object if Bing returned all answers:</span><span class="sxs-lookup"><span data-stu-id="1c4c7-106">This example illustrates a response object if Bing returned all answers:</span></span>

```json
{
    "_type": "SearchResponse",
    "queryContext": {...},
    "webPages": {...},
    "images": {...},
    "relatedSearches": {...},
    "videos": {...},
    "news": {...},
    "spellSuggestion": {...},
    "computation": {...},
    "timeZone": {...},
    "rankingResponse": {...}
}, ...
```

<span data-ttu-id="1c4c7-107">Typically, Bing Web Search returns a subset of the answers.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-107">Typically, Bing Web Search returns a subset of the answers.</span></span> <span data-ttu-id="1c4c7-108">For example, if the query term was *sailing dinghies*, the response might include `webPages`, `images`, and `rankingResponse`.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-108">For example, if the query term was *sailing dinghies*, the response might include `webPages`, `images`, and `rankingResponse`.</span></span> <span data-ttu-id="1c4c7-109">Unless you've used [responseFilter](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#responsefilter) to filter out webpages, the response always includes the `webpages` and `rankingResponse` answers.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-109">Unless you've used [responseFilter](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#responsefilter) to filter out webpages, the response always includes the `webpages` and `rankingResponse` answers.</span></span>

## <a name="webpages-answer"></a><span data-ttu-id="1c4c7-110">Webpages answer</span><span class="sxs-lookup"><span data-stu-id="1c4c7-110">Webpages answer</span></span>

<span data-ttu-id="1c4c7-111">The [webPages](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#webanswer) answer contains a list of links to webpages that Bing Web Search determined were relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-111">The [webPages](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#webanswer) answer contains a list of links to webpages that Bing Web Search determined were relevant to the query.</span></span> <span data-ttu-id="1c4c7-112">Each [web page](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#webpage) in the list includes the page's name, url, display URL, short description of the content and the date Bing found the content.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-112">Each [web page](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#webpage) in the list includes the page's name, url, display URL, short description of the content and the date Bing found the content.</span></span>

```json
{
    "id": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.0",
    "name": "Dinghy sailing",
    "url": "https:\/\/www.bing.com\/cr?IG=3A43CA5...",
    "displayUrl": "https:\/\/en.contoso.com\/wiki\/Dinghy_sailing",
    "snippet": "Dinghy sailing is the activity of sailing small boats...",
    "dateLastCrawled": "2017-04-05T16:25:00"
}, ...
```

<span data-ttu-id="1c4c7-113">Use `name` and `url` to create a hyperlink that takes the user to the webpage.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-113">Use `name` and `url` to create a hyperlink that takes the user to the webpage.</span></span>

<!-- Remove until this can be replaced with a sanitized version.
The following shows an example of how you might display the webpage in a search results page.

![Rendered webpage example](./media/cognitive-services-bing-web-api/bing-rendered-webpage-example.PNG)
-->

## <a name="images-answer"></a><span data-ttu-id="1c4c7-114">Images answer</span><span class="sxs-lookup"><span data-stu-id="1c4c7-114">Images answer</span></span>

<span data-ttu-id="1c4c7-115">The [images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) answer contains a list of images that Bing thought were relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-115">The [images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) answer contains a list of images that Bing thought were relevant to the query.</span></span> <span data-ttu-id="1c4c7-116">Each [image](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image) in the list includes the URL of the image, its size, its dimensions, and its encoding format.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-116">Each [image](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image) in the list includes the URL of the image, its size, its dimensions, and its encoding format.</span></span> <span data-ttu-id="1c4c7-117">The image object also includes the URL of a thumbnail of the image and the thumbnail's dimensions.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-117">The image object also includes the URL of a thumbnail of the image and the thumbnail's dimensions.</span></span>

```json
{
    "name": "Rich Passage Sailing Dinghy",
    "webSearchUrl": "https:\/\/www.bing.com\/cr?IG=3A43CA5CA64...",
    "thumbnailUrl": "https:\/\/tse1.mm.bing.net\/th?id=OIP....",
    "datePublished": "2011-10-29T11:26:00",
    "contentUrl": "http:\/\/upload.contoso.com\/sailing\/...",
    "hostPageUrl": "http:\/\/www.bing.com\/cr?IG=3A43CA5CA6464....",
    "contentSize": "79239 B",
    "encodingFormat": "jpeg",
    "hostPageDisplayUrl": "http:\/\/en.contoso.com\/wiki\/File...",
    "width": 526,
    "height": 688,
    "thumbnail": {
        "width": 229,
        "height": 300
    },
    "insightsSourcesSummary": {
        "shoppingSourcesCount": 0,
        "recipeSourcesCount": 0
    }
}, ...
```

<span data-ttu-id="1c4c7-118">Depending on the user's device, you'd typically display a subset of the thumbnails with an option for the user to view the remaining images.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-118">Depending on the user's device, you'd typically display a subset of the thumbnails with an option for the user to view the remaining images.</span></span>

<!-- Remove until this can be replaced with a sanitized version.
![List of thumbnail images](./media/cognitive-services-bing-web-api/bing-web-image-thumbnails.PNG)
-->

<span data-ttu-id="1c4c7-119">You can also expand the thumbnail as the user hovers the cursor over it.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-119">You can also expand the thumbnail as the user hovers the cursor over it.</span></span> <span data-ttu-id="1c4c7-120">Be sure to attribute the image if you expand it.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-120">Be sure to attribute the image if you expand it.</span></span> <span data-ttu-id="1c4c7-121">For example, by extracting the host from `hostPageDisplayUrl` and displaying it below the image.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-121">For example, by extracting the host from `hostPageDisplayUrl` and displaying it below the image.</span></span> <span data-ttu-id="1c4c7-122">For information about resizing the thumbnail, see [Resizing and Cropping Thumbnails](./resize-and-crop-thumbnails.md).</span><span class="sxs-lookup"><span data-stu-id="1c4c7-122">For information about resizing the thumbnail, see [Resizing and Cropping Thumbnails](./resize-and-crop-thumbnails.md).</span></span>

<!-- Remove until this can be replaced with a sanitized version.
![Expanded view of thumbnail image](./media/cognitive-services-bing-web-api/bing-web-image-thumbnail-expansion.PNG)
-->

<span data-ttu-id="1c4c7-123">If the user clicks the thumbnail, use `webSearchUrl` to take the user to Bing's search results page for images, which contains a collage of the images.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-123">If the user clicks the thumbnail, use `webSearchUrl` to take the user to Bing's search results page for images, which contains a collage of the images.</span></span>

<span data-ttu-id="1c4c7-124">For details about the image answer and images, see [Image Search API](../bing-image-search/search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="1c4c7-124">For details about the image answer and images, see [Image Search API](../bing-image-search/search-the-web.md).</span></span>

## <a name="related-searches-answer"></a><span data-ttu-id="1c4c7-125">Related searches answer</span><span class="sxs-lookup"><span data-stu-id="1c4c7-125">Related searches answer</span></span>

<span data-ttu-id="1c4c7-126">The [relatedSearches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#searchresponse-relatedsearches) answer contains a list of the most popular related queries made by other users.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-126">The [relatedSearches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#searchresponse-relatedsearches) answer contains a list of the most popular related queries made by other users.</span></span> <span data-ttu-id="1c4c7-127">Each [query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#query_obj) in the list includes a query string (`text`), a query string with hit highlighting characters (`displayText`), and a URL (`webSearchUrl`) to Bing's search results page for that query.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-127">Each [query](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#query_obj) in the list includes a query string (`text`), a query string with hit highlighting characters (`displayText`), and a URL (`webSearchUrl`) to Bing's search results page for that query.</span></span>

```json
{
    "text": "dinghy racing teams",
    "displayText": "dinghy racing teams",
    "webSearchUrl": "https:\/\/www.bing.com\/cr?IG=96C4CF214A0..."
}, ...
```

<span data-ttu-id="1c4c7-128">Use the `displayText` query string and the `webSearchUrl` URL to create a hyperlink that takes the user to the Bing search results page for the related query.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-128">Use the `displayText` query string and the `webSearchUrl` URL to create a hyperlink that takes the user to the Bing search results page for the related query.</span></span> <span data-ttu-id="1c4c7-129">You could also use the `text` query string in your own Web Search API query and display the results yourself.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-129">You could also use the `text` query string in your own Web Search API query and display the results yourself.</span></span>

<span data-ttu-id="1c4c7-130">For information about how to handle the highlighting markers in `displayText`, see [Hit Highlighting](./hit-highlighting.md).</span><span class="sxs-lookup"><span data-stu-id="1c4c7-130">For information about how to handle the highlighting markers in `displayText`, see [Hit Highlighting](./hit-highlighting.md).</span></span>

<span data-ttu-id="1c4c7-131">The following shows an example of the related queries usage in Bing.com.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-131">The following shows an example of the related queries usage in Bing.com.</span></span>

![Related searches example on Bing](./media/cognitive-services-bing-web-api/bing-web-rendered-relatedsearches.GIF)

## <a name="videos-answer"></a><span data-ttu-id="1c4c7-133">Videos answer</span><span class="sxs-lookup"><span data-stu-id="1c4c7-133">Videos answer</span></span>

<span data-ttu-id="1c4c7-134">The [videos](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos) answer contains a list of videos that Bing thought were relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-134">The [videos](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos) answer contains a list of videos that Bing thought were relevant to the query.</span></span> <span data-ttu-id="1c4c7-135">Each [video](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video) in the list includes the URL of the video, its duration, its dimensions, and its encoding format.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-135">Each [video](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#video) in the list includes the URL of the video, its duration, its dimensions, and its encoding format.</span></span> <span data-ttu-id="1c4c7-136">The video object also includes the URL of a thumbnail of the video and the thumbnail's dimensions.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-136">The video object also includes the URL of a thumbnail of the video and the thumbnail's dimensions.</span></span>

```json
{
    "name": "Sailing dinghy",
    "description": "Northwind Traders is a 12 foot gunter rigged...",
    "webSearchUrl": "https:\/\/www.bing.com\/cr?IG=1CAE739681D84...",
    "thumbnailUrl": "https:\/\/tse2.mm.bing.net\/th?id=OVP.wsKiL...",
    "datePublished": "2013-11-06T01:56:28",
    "publisher": [{
        "name": "Fabrikam"
    }],
    "contentUrl": "https:\/\/www.fabrikam.com\/watch?v=MrVBWZpJjX",
    "hostPageUrl": "https:\/\/www.bing.com\/cr?IG=1CAE739681D8400DB...",
    "encodingFormat": "mp4",
    "hostPageDisplayUrl": "https:\/\/www.fabrikam.com\/watch?v=MrBWZpJjXo",
    "width": 1280,
    "height": 720,
    "duration": "PT3M47S",
    "motionThumbnailUrl": "https:\/\/tse2.mm.bing.net\/th?id=OM.oa...",
    "embedHtml": "<iframe width=\"1280\" height=\"720\" src=\"http:\/\/www....><\/iframe>",
    "allowHttpsEmbed": true,
    "viewCount": 19089,
    "thumbnail": {
        "width": 300,
        "height": 168
    },
    "allowMobileEmbed": true,
    "isSuperfresh": false
}, ...
```

<span data-ttu-id="1c4c7-137">Depending on the user's device, you'd typically display a subset of the videos with an option for the user to view the remaining videos.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-137">Depending on the user's device, you'd typically display a subset of the videos with an option for the user to view the remaining videos.</span></span> <span data-ttu-id="1c4c7-138">You'd display a thumbnail of the video with the video's length, description (name), and attribution (publisher).</span><span class="sxs-lookup"><span data-stu-id="1c4c7-138">You'd display a thumbnail of the video with the video's length, description (name), and attribution (publisher).</span></span>

<!-- Remove until this can be replaced with a sanitized version.
![List of video thumbnails](./media/cognitive-services-bing-web-api/bing-web-video-thumbnails.PNG)
-->

<span data-ttu-id="1c4c7-139">As the user hovers over the thumbnail you can use `motionThumbnailUrl` to play a thumbnail version of the video.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-139">As the user hovers over the thumbnail you can use `motionThumbnailUrl` to play a thumbnail version of the video.</span></span> <span data-ttu-id="1c4c7-140">Be sure to attribute the motion thumbnail when you display it.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-140">Be sure to attribute the motion thumbnail when you display it.</span></span>

<!-- Remove until this can be replaced with a sanitized version.
![Motion thumbnail of a video](./media/cognitive-services-bing-web-api/bing-web-video-motion-thumbnail.PNG)
-->

<span data-ttu-id="1c4c7-141">If the user clicks the thumbnail, the following are the video viewing options:</span><span class="sxs-lookup"><span data-stu-id="1c4c7-141">If the user clicks the thumbnail, the following are the video viewing options:</span></span>

- <span data-ttu-id="1c4c7-142">Use `hostPageUrl` to view the video on the host website (for example, YouTube)</span><span class="sxs-lookup"><span data-stu-id="1c4c7-142">Use `hostPageUrl` to view the video on the host website (for example, YouTube)</span></span>
- <span data-ttu-id="1c4c7-143">Use `webSearchUrl` to view the video in the Bing video browser</span><span class="sxs-lookup"><span data-stu-id="1c4c7-143">Use `webSearchUrl` to view the video in the Bing video browser</span></span>
- <span data-ttu-id="1c4c7-144">Use `embedHtml` to embed the video in your own experience</span><span class="sxs-lookup"><span data-stu-id="1c4c7-144">Use `embedHtml` to embed the video in your own experience</span></span>

<span data-ttu-id="1c4c7-145">For details about the video answer and videos, see [Video Search API](../bing-video-search/search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="1c4c7-145">For details about the video answer and videos, see [Video Search API](../bing-video-search/search-the-web.md).</span></span>

## <a name="news-answer"></a><span data-ttu-id="1c4c7-146">News answer</span><span class="sxs-lookup"><span data-stu-id="1c4c7-146">News answer</span></span>

<span data-ttu-id="1c4c7-147">The [news](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#news) answer contains a list of news articles that Bing thought were relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-147">The [news](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#news) answer contains a list of news articles that Bing thought were relevant to the query.</span></span> <span data-ttu-id="1c4c7-148">Each [news article](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#newsarticle) in the list includes the article's name, description, and URL to the article on the host's website.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-148">Each [news article](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference#newsarticle) in the list includes the article's name, description, and URL to the article on the host's website.</span></span> <span data-ttu-id="1c4c7-149">If the article contains an image, the object includes a thumbnail of the image.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-149">If the article contains an image, the object includes a thumbnail of the image.</span></span>

```json
{
    "name": "WC Sailing Qualifies for America Trophy with...",
    "url": "http:\/\/www.bing.com\/cr?IG=3445EEF15DAF4FFFBF7...",
    "image": {
        "contentUrl": "http:\/\/www.contoso.com\/sports\/sail...",
        "thumbnail": {
            "contentUrl": "https:\/\/www.bing.com\/th?id=ON.1...",
            "width": 400,
            "height": 272
        }
    },
    "description": "The WC sailing team qualified for a...",
    "provider": [{
        "_type": "Organization",
        "name": "contoso.com"
    }],
    "datePublished": "2017-04-16T21:56:00"
}, ...
```

<span data-ttu-id="1c4c7-150">Depending on the user's device, you'd display a subset of the news articles with an option for the user to view the remaining articles.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-150">Depending on the user's device, you'd display a subset of the news articles with an option for the user to view the remaining articles.</span></span> <span data-ttu-id="1c4c7-151">Use `name` and `url` to create a hyperlink that takes the user to the news article on the host's site.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-151">Use `name` and `url` to create a hyperlink that takes the user to the news article on the host's site.</span></span> <span data-ttu-id="1c4c7-152">If the article includes an image, make the image clickable using `url`.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-152">If the article includes an image, make the image clickable using `url`.</span></span> <span data-ttu-id="1c4c7-153">Be sure to use `provider` to attribute the article.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-153">Be sure to use `provider` to attribute the article.</span></span>

<!-- Remove until this can be replaced with a sanitized version.
The following shows an example of how you might display articles in a search results page.

![List of news articles](./media/cognitive-services-bing-web-api/bing-web-news-list.PNG)
-->

<span data-ttu-id="1c4c7-154">For details about the news answer and news articles, see [News Search API](../bing-news-search/search-the-web.md).</span><span class="sxs-lookup"><span data-stu-id="1c4c7-154">For details about the news answer and news articles, see [News Search API](../bing-news-search/search-the-web.md).</span></span>

## <a name="computation-answer"></a><span data-ttu-id="1c4c7-155">Computation answer</span><span class="sxs-lookup"><span data-stu-id="1c4c7-155">Computation answer</span></span>

<span data-ttu-id="1c4c7-156">If the user enters a mathematical expression or a unit conversion query, the response may contain a [Computation](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#computation) answer.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-156">If the user enters a mathematical expression or a unit conversion query, the response may contain a [Computation](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#computation) answer.</span></span> <span data-ttu-id="1c4c7-157">The `computation` answer contains the normalized expression and its result.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-157">The `computation` answer contains the normalized expression and its result.</span></span>

<span data-ttu-id="1c4c7-158">A unit conversion query is a query that converts one unit to another.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-158">A unit conversion query is a query that converts one unit to another.</span></span> <span data-ttu-id="1c4c7-159">For example, *How many feet in 10 meters?* or *How many tablespoons in a 1/4 cup?*</span><span class="sxs-lookup"><span data-stu-id="1c4c7-159">For example, *How many feet in 10 meters?* or *How many tablespoons in a 1/4 cup?*</span></span>

<span data-ttu-id="1c4c7-160">The following shows the `computation` answer for *How many feet in 10 meters?*</span><span class="sxs-lookup"><span data-stu-id="1c4c7-160">The following shows the `computation` answer for *How many feet in 10 meters?*</span></span>

```json
"computation": {
    "id": "https:\/\/www.bing.com\/api\/v7\/#Computation",
    "expression": "10 meters",
    "value": "32.808399 feet"
}, ...
```

<span data-ttu-id="1c4c7-161">The following shows examples of mathematical queries and their corresponding `computation` answers.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-161">The following shows examples of mathematical queries and their corresponding `computation` answers.</span></span>

```
Query: (5+3)(10/2)+8
Encoded query: %285%2B3%29%2810%2F2%29%2B8
```

```json
"computation": {
    "id": "https:\/\/www.bing.com\/api\/v7\/#Computation",
    "expression": "((5+3)*(10\/2))+8",
    "value": "48"
}
```

```
Query: sqrt(4^2+8^2)
Encoded query: sqrt%284^2%2B8^2%29
```

```json
"computation": {
    "id": "https:\/\/www.bing.com\/api\/v7\/#Computation",
    "expression": "sqrt((4^2)+(8^2))",
    "value": "8.94427191"
}
```

```
Query: 30 6/8 - 18 8/16
Encoded query: 30%206%2F8%20-%2018%208%2F16
```

```json
"computation": {
    "id": "https:\/\/www.bing.com\/api\/v7\/#WolframAlpha",
    "expression": "30 6\/8-18 8\/16",
    "value": "12.25"
}
```

```
Query: 8^2+11^2-2*8*11*cos(37)
Encoded query: 8^2%2B11^2-2*8*11*cos%2837%29
```

```json
"computation": {
        "id": "https:\/\/www.bing.com\/api\/v7\/#Computation",
        "expression": "(8^2)+(11^2)-(2*8*11*cos(37))",
        "value": "44.4401502"
}
```

<span data-ttu-id="1c4c7-162">A mathematical expression may contain the following symbols:</span><span class="sxs-lookup"><span data-stu-id="1c4c7-162">A mathematical expression may contain the following symbols:</span></span>

|<span data-ttu-id="1c4c7-163">Symbol</span><span class="sxs-lookup"><span data-stu-id="1c4c7-163">Symbol</span></span>|<span data-ttu-id="1c4c7-164">Description</span><span class="sxs-lookup"><span data-stu-id="1c4c7-164">Description</span></span>|
|------------|-----------------|
|+|<span data-ttu-id="1c4c7-165">Addition</span><span class="sxs-lookup"><span data-stu-id="1c4c7-165">Addition</span></span>|
|-|<span data-ttu-id="1c4c7-166">Subtraction</span><span class="sxs-lookup"><span data-stu-id="1c4c7-166">Subtraction</span></span>|
|/|<span data-ttu-id="1c4c7-167">Division</span><span class="sxs-lookup"><span data-stu-id="1c4c7-167">Division</span></span>|
|*|<span data-ttu-id="1c4c7-168">Multiplication</span><span class="sxs-lookup"><span data-stu-id="1c4c7-168">Multiplication</span></span>|
|^|<span data-ttu-id="1c4c7-169">Power</span><span class="sxs-lookup"><span data-stu-id="1c4c7-169">Power</span></span>|
|<span data-ttu-id="1c4c7-170">!</span><span class="sxs-lookup"><span data-stu-id="1c4c7-170">!</span></span>|<span data-ttu-id="1c4c7-171">Factorial</span><span class="sxs-lookup"><span data-stu-id="1c4c7-171">Factorial</span></span>|
|<span data-ttu-id="1c4c7-172">.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-172">.</span></span>|<span data-ttu-id="1c4c7-173">Decimal</span><span class="sxs-lookup"><span data-stu-id="1c4c7-173">Decimal</span></span>|
|<span data-ttu-id="1c4c7-174">()</span><span class="sxs-lookup"><span data-stu-id="1c4c7-174">()</span></span>|<span data-ttu-id="1c4c7-175">Precedence grouping</span><span class="sxs-lookup"><span data-stu-id="1c4c7-175">Precedence grouping</span></span>|
|<span data-ttu-id="1c4c7-176">[]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-176">[]</span></span>|<span data-ttu-id="1c4c7-177">Function</span><span class="sxs-lookup"><span data-stu-id="1c4c7-177">Function</span></span>|

<span data-ttu-id="1c4c7-178">A mathematical expression may contain the following constants:</span><span class="sxs-lookup"><span data-stu-id="1c4c7-178">A mathematical expression may contain the following constants:</span></span>

|<span data-ttu-id="1c4c7-179">Symbol</span><span class="sxs-lookup"><span data-stu-id="1c4c7-179">Symbol</span></span>|<span data-ttu-id="1c4c7-180">Description</span><span class="sxs-lookup"><span data-stu-id="1c4c7-180">Description</span></span>|
|------------|-----------------|
|<span data-ttu-id="1c4c7-181">Pi</span><span class="sxs-lookup"><span data-stu-id="1c4c7-181">Pi</span></span>|<span data-ttu-id="1c4c7-182">3.14159...</span><span class="sxs-lookup"><span data-stu-id="1c4c7-182">3.14159...</span></span>|
|<span data-ttu-id="1c4c7-183">Degree</span><span class="sxs-lookup"><span data-stu-id="1c4c7-183">Degree</span></span>|<span data-ttu-id="1c4c7-184">Degree</span><span class="sxs-lookup"><span data-stu-id="1c4c7-184">Degree</span></span>|
|<span data-ttu-id="1c4c7-185">i</span><span class="sxs-lookup"><span data-stu-id="1c4c7-185">i</span></span>|<span data-ttu-id="1c4c7-186">Imaginary number</span><span class="sxs-lookup"><span data-stu-id="1c4c7-186">Imaginary number</span></span>|
|<span data-ttu-id="1c4c7-187">e</span><span class="sxs-lookup"><span data-stu-id="1c4c7-187">e</span></span>|<span data-ttu-id="1c4c7-188">e, 2.71828...</span><span class="sxs-lookup"><span data-stu-id="1c4c7-188">e, 2.71828...</span></span>|
|<span data-ttu-id="1c4c7-189">GoldenRatio</span><span class="sxs-lookup"><span data-stu-id="1c4c7-189">GoldenRatio</span></span>|<span data-ttu-id="1c4c7-190">Golden ratio, 1.61803...</span><span class="sxs-lookup"><span data-stu-id="1c4c7-190">Golden ratio, 1.61803...</span></span>|

<span data-ttu-id="1c4c7-191">A mathematical expression may contain the following functions:</span><span class="sxs-lookup"><span data-stu-id="1c4c7-191">A mathematical expression may contain the following functions:</span></span>

|<span data-ttu-id="1c4c7-192">Symbol</span><span class="sxs-lookup"><span data-stu-id="1c4c7-192">Symbol</span></span>|<span data-ttu-id="1c4c7-193">Description</span><span class="sxs-lookup"><span data-stu-id="1c4c7-193">Description</span></span>|
|------------|-----------------|
|<span data-ttu-id="1c4c7-194">Sqrt</span><span class="sxs-lookup"><span data-stu-id="1c4c7-194">Sqrt</span></span>|<span data-ttu-id="1c4c7-195">Square root</span><span class="sxs-lookup"><span data-stu-id="1c4c7-195">Square root</span></span>|
|<span data-ttu-id="1c4c7-196">Sin[x], Cos[x], Tan[x]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-196">Sin[x], Cos[x], Tan[x]</span></span><br /><span data-ttu-id="1c4c7-197">Csc[x], Sec[x], Cot[x]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-197">Csc[x], Sec[x], Cot[x]</span></span>|<span data-ttu-id="1c4c7-198">Trigonometric functions (with arguments in radians)</span><span class="sxs-lookup"><span data-stu-id="1c4c7-198">Trigonometric functions (with arguments in radians)</span></span>|
|<span data-ttu-id="1c4c7-199">ArcSin[x], ArcCos[x], ArcTan[x]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-199">ArcSin[x], ArcCos[x], ArcTan[x]</span></span><br /><span data-ttu-id="1c4c7-200">ArcCsc[x], ArcSec[x], ArcCot[x]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-200">ArcCsc[x], ArcSec[x], ArcCot[x]</span></span>|<span data-ttu-id="1c4c7-201">Inverse trigonometric functions (giving results in radians)</span><span class="sxs-lookup"><span data-stu-id="1c4c7-201">Inverse trigonometric functions (giving results in radians)</span></span>|
|<span data-ttu-id="1c4c7-202">Exp[x], E^x</span><span class="sxs-lookup"><span data-stu-id="1c4c7-202">Exp[x], E^x</span></span>|<span data-ttu-id="1c4c7-203">Exponential function</span><span class="sxs-lookup"><span data-stu-id="1c4c7-203">Exponential function</span></span>|
|<span data-ttu-id="1c4c7-204">Log[x]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-204">Log[x]</span></span>|<span data-ttu-id="1c4c7-205">Natural logarithm</span><span class="sxs-lookup"><span data-stu-id="1c4c7-205">Natural logarithm</span></span>|
|<span data-ttu-id="1c4c7-206">Sinh[x], Cosh[x], Tanh[x]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-206">Sinh[x], Cosh[x], Tanh[x]</span></span><br /><span data-ttu-id="1c4c7-207">Csch[x], Sech[x], Coth[x]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-207">Csch[x], Sech[x], Coth[x]</span></span>|<span data-ttu-id="1c4c7-208">Hyperbolic functions</span><span class="sxs-lookup"><span data-stu-id="1c4c7-208">Hyperbolic functions</span></span>|
|<span data-ttu-id="1c4c7-209">ArcSinh[x], ArcCosh[x], ArcTanh[x]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-209">ArcSinh[x], ArcCosh[x], ArcTanh[x]</span></span><br /><span data-ttu-id="1c4c7-210">ArcCsch[x], ArcSech[x], ArcCoth[x]</span><span class="sxs-lookup"><span data-stu-id="1c4c7-210">ArcCsch[x], ArcSech[x], ArcCoth[x]</span></span>|<span data-ttu-id="1c4c7-211">Inverse hyperbolic functions</span><span class="sxs-lookup"><span data-stu-id="1c4c7-211">Inverse hyperbolic functions</span></span>|

<span data-ttu-id="1c4c7-212">Mathematical expressions that contain variables (for example, 4x+6=18, where x is the variable) are not supported.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-212">Mathematical expressions that contain variables (for example, 4x+6=18, where x is the variable) are not supported.</span></span>

## <a name="timezone-answer"></a><span data-ttu-id="1c4c7-213">TimeZone answer</span><span class="sxs-lookup"><span data-stu-id="1c4c7-213">TimeZone answer</span></span>

<span data-ttu-id="1c4c7-214">If the user enters a time or date query, the response may contain a [TimeZone](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#timezone) answer.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-214">If the user enters a time or date query, the response may contain a [TimeZone](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#timezone) answer.</span></span> <span data-ttu-id="1c4c7-215">This answer supports implicit or explicit queries.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-215">This answer supports implicit or explicit queries.</span></span> <span data-ttu-id="1c4c7-216">An implicit query, such as *What time is it?*, returns the local time based on the user's location.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-216">An implicit query, such as *What time is it?*, returns the local time based on the user's location.</span></span> <span data-ttu-id="1c4c7-217">An explicit query, such as *What time is it in Seattle?*, returns the local time for Seattle, WA.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-217">An explicit query, such as *What time is it in Seattle?*, returns the local time for Seattle, WA.</span></span>

<span data-ttu-id="1c4c7-218">The `timeZone` answer provides the name of the location, the current UTC date and time at the specified location, and the UTC offset.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-218">The `timeZone` answer provides the name of the location, the current UTC date and time at the specified location, and the UTC offset.</span></span> <span data-ttu-id="1c4c7-219">If the boundary of the location is within multiple time zones, the answer contains the current UTC date and time of all time zones within the boundary.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-219">If the boundary of the location is within multiple time zones, the answer contains the current UTC date and time of all time zones within the boundary.</span></span> <span data-ttu-id="1c4c7-220">For example, because Florida State falls within two time zones, the answer contains the local date and time of both time zones.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-220">For example, because Florida State falls within two time zones, the answer contains the local date and time of both time zones.</span></span>  

<span data-ttu-id="1c4c7-221">If the query requests the time of a state or country, Bing determines the primary city within the location's geographical boundary and returns it in the `primaryCityTime` field.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-221">If the query requests the time of a state or country, Bing determines the primary city within the location's geographical boundary and returns it in the `primaryCityTime` field.</span></span> <span data-ttu-id="1c4c7-222">If the boundary contains multiple time zones, the remaining time zones are returned in the `otherCityTimes` field.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-222">If the boundary contains multiple time zones, the remaining time zones are returned in the `otherCityTimes` field.</span></span>

<span data-ttu-id="1c4c7-223">The following shows example queries that return the `timeZone` answer.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-223">The following shows example queries that return the `timeZone` answer.</span></span>

```
Query: What time is it?

"timeZone": {
    "id": "https:\/\/www.bing.com\/api\/v7\/#TimeZone",
    "primaryCityTime": {
        "location": "Redmond, Washington, United States",
        "time": "2015-10-27T08:38:12.1189231Z",
        "utcOffset": "UTC-7"
    }
}

Query: What time is it in the Pacific time zone?

"timeZone": {
    "id": "https:\/\/www.bing.com\/api\/v7\/#TimeZone",
    "primaryCityTime": {
        "location": "Pacific Time Zone",
        "time": "2015-10-23T12:33:19.0728146Z",
        "utcOffset": "UTC-7"
    }
}

Query: Time in Florida?

"timeZone": {
        "id": "https:\/\/www.bing.com\/api\/v7\/#TimeZone",
        "primaryCityTime": {
            "location": "Tallahassee, Florida, United States",
            "time": "2015-10-23T13:04:56.6774389Z",
            "utcOffset": "UTC-4"
        },
        "otherCityTimes": [{
            "location": "Pensacola",
            "time": "2015-10-23T12:04:56.6664294Z",
            "utcOffset": "UTC-5"
        }]
}

Query: What time is it in the U.S.

"timeZone": {
    "id": "https:\/\/www.bing.com\/api\/v7\/#TimeZone",
    "primaryCityTime": {
        "location": "Washington, D.C., United States",
        "time": "2015-10-23T15:27:59.8892745Z",
        "utcOffset": "UTC-4"
    },
    "otherCityTimes": [{
        "location": "Honolulu",
        "time": "2015-10-23T09:27:59.8892745Z",
        "utcOffset": "UTC-10"
    },
    {
        "location": "Anchorage",
        "time": "2015-10-23T11:27:59.8892745Z",
        "utcOffset": "UTC-8"
    },
    {
        "location": "Phoenix",
        "time": "2015-10-23T12:27:59.8892745Z",
        "utcOffset": "UTC-7"
    },
    {
        "location": "Los Angeles",
        "time": "2015-10-23T12:27:59.8942788Z",
        "utcOffset": "UTC-7"
    },
    {
        "location": "Denver",
        "time": "2015-10-23T13:27:59.8812681Z",
        "utcOffset": "UTC-6"
    },
    {
        "location": "Chicago",
        "time": "2015-10-23T14:27:59.8892745Z",
        "utcOffset": "UTC-5"
    }]
}
```

## <a name="spellsuggestion-answer"></a><span data-ttu-id="1c4c7-224">SpellSuggestion answer</span><span class="sxs-lookup"><span data-stu-id="1c4c7-224">SpellSuggestion answer</span></span>

<span data-ttu-id="1c4c7-225">If Bing determines that the user may have intended to search for something different, the response includes a [SpellSuggestions](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#spellsuggestions) object.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-225">If Bing determines that the user may have intended to search for something different, the response includes a [SpellSuggestions](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#spellsuggestions) object.</span></span> <span data-ttu-id="1c4c7-226">For example, if the user searches for *carlos pen*, Bing may determine that the user likely intended to search for Carlos Pena instead (based on past searches by others of *carlos pen*).</span><span class="sxs-lookup"><span data-stu-id="1c4c7-226">For example, if the user searches for *carlos pen*, Bing may determine that the user likely intended to search for Carlos Pena instead (based on past searches by others of *carlos pen*).</span></span> <span data-ttu-id="1c4c7-227">The following shows an example spell response.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-227">The following shows an example spell response.</span></span>

```json
"spellSuggestions": {
    "id": "https:\/\/www.bing.com\/api\/v7\/#SpellSuggestions",
    "value": [{
        "text": "carlos pena",
        "displayText": "carlos pena"
    }]
}, ...
```

<span data-ttu-id="1c4c7-228">The following shows how Bing uses the spelling suggestion.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-228">The following shows how Bing uses the spelling suggestion.</span></span>

![Bing spelling suggestion example](./media/cognitive-services-bing-web-api/bing-web-spellingsuggestion.GIF)  

## <a name="next-steps"></a><span data-ttu-id="1c4c7-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c4c7-230">Next steps</span></span>  

* <span data-ttu-id="1c4c7-231">Review [request throttling](throttling-requests.md) documentation.</span><span class="sxs-lookup"><span data-stu-id="1c4c7-231">Review [request throttling](throttling-requests.md) documentation.</span></span>  

## <a name="see-also"></a><span data-ttu-id="1c4c7-232">See also</span><span class="sxs-lookup"><span data-stu-id="1c4c7-232">See also</span></span>  

* [<span data-ttu-id="1c4c7-233">Bing Web Search API reference</span><span class="sxs-lookup"><span data-stu-id="1c4c7-233">Bing Web Search API reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference)
