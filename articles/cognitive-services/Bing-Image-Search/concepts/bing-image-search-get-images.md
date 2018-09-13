---
title: Get images from the web with the Bing Image Search API | Microsoft Docs
description: Use the Bing Image Search API to search for and get relevant images from the web.
services: cognitive-services
author: aahill
manager: cgronlun
ms.assetid: AB1B9898-C94A-4B59-91A1-8623C94BA3D4
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: conceptual
ms.date: 8/8/2018
ms.author: aahi
ms.openlocfilehash: 720318ab2be53c59c47e3399b1be5a55487840b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870965"
---
# <a name="get-images-from-the-web-with-the-bing-image-search-api"></a><span data-ttu-id="6b501-103">Get images from the web with the Bing Image Search API</span><span class="sxs-lookup"><span data-stu-id="6b501-103">Get images from the web with the Bing Image Search API</span></span>

<span data-ttu-id="6b501-104">When you use the Bing Image Search REST API, you can get images from the web that are related to your search term by sending the following GET request:</span><span class="sxs-lookup"><span data-stu-id="6b501-104">When you use the Bing Image Search REST API, you can get images from the web that are related to your search term by sending the following GET request:</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies&mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
X-MSEdge-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

> [!IMPORTANT]
> * <span data-ttu-id="6b501-105">All requests must be made from a server, and not from a client.</span><span class="sxs-lookup"><span data-stu-id="6b501-105">All requests must be made from a server, and not from a client.</span></span>
> * <span data-ttu-id="6b501-106">If it's your first time calling any of the Bing search APIs, don't include the client ID header.</span><span class="sxs-lookup"><span data-stu-id="6b501-106">If it's your first time calling any of the Bing search APIs, don't include the client ID header.</span></span> <span data-ttu-id="6b501-107">Only include the client ID if you've previously called a Bing API that returned a client ID for the user and device combination.</span><span class="sxs-lookup"><span data-stu-id="6b501-107">Only include the client ID if you've previously called a Bing API that returned a client ID for the user and device combination.</span></span>
> * <span data-ttu-id="6b501-108">Images must be displayed in the order provided in the response.</span><span class="sxs-lookup"><span data-stu-id="6b501-108">Images must be displayed in the order provided in the response.</span></span>

## <a name="get-images-from-a-specific-web-domain"></a><span data-ttu-id="6b501-109">Get images from a specific web domain</span><span class="sxs-lookup"><span data-stu-id="6b501-109">Get images from a specific web domain</span></span>

<span data-ttu-id="6b501-110">To get images from a specific domain, use the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator.</span><span class="sxs-lookup"><span data-stu-id="6b501-110">To get images from a specific domain, use the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator.</span></span>

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies+site:contososailing.com&mkt=en-us HTTP/1.1
```

> [!NOTE]
> <span data-ttu-id="6b501-111">Responses to queries using the `site:` operator might include adult content regardless of the [safeSearch](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#safesearch) setting.</span><span class="sxs-lookup"><span data-stu-id="6b501-111">Responses to queries using the `site:` operator might include adult content regardless of the [safeSearch](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#safesearch) setting.</span></span> <span data-ttu-id="6b501-112">Only use `site:` if you're aware of the content on the domain.</span><span class="sxs-lookup"><span data-stu-id="6b501-112">Only use `site:` if you're aware of the content on the domain.</span></span>

<span data-ttu-id="6b501-113">The following example shows how to get small images from ContosoSailing.com that Bing has discovered in the past week.</span><span class="sxs-lookup"><span data-stu-id="6b501-113">The following example shows how to get small images from ContosoSailing.com that Bing has discovered in the past week.</span></span>  

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies+site:contososailing.com&size=small&freshness=week&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```

## <a name="filter-images"></a><span data-ttu-id="6b501-114">Filter images</span><span class="sxs-lookup"><span data-stu-id="6b501-114">Filter images</span></span>

 <span data-ttu-id="6b501-115">By default, the Image Search API returns all images that are relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="6b501-115">By default, the Image Search API returns all images that are relevant to the query.</span></span> <span data-ttu-id="6b501-116">If you want to filter the images that Bing returns (for example, to return only images with a transparent background or specific size), use the following query parameters:</span><span class="sxs-lookup"><span data-stu-id="6b501-116">If you want to filter the images that Bing returns (for example, to return only images with a transparent background or specific size), use the following query parameters:</span></span>

* <span data-ttu-id="6b501-117">[aspect](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#aspect)—Filter images by aspect ratio (for example, standard or wide screen images).</span><span class="sxs-lookup"><span data-stu-id="6b501-117">[aspect](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#aspect)—Filter images by aspect ratio (for example, standard or wide screen images).</span></span>
* <span data-ttu-id="6b501-118">[color](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#color)—Filter images by dominant color or black and white.</span><span class="sxs-lookup"><span data-stu-id="6b501-118">[color](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#color)—Filter images by dominant color or black and white.</span></span>
* <span data-ttu-id="6b501-119">[freshness](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#freshness)—Filter images by age (for example, images discovered by Bing in the past week).</span><span class="sxs-lookup"><span data-stu-id="6b501-119">[freshness](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#freshness)—Filter images by age (for example, images discovered by Bing in the past week).</span></span>
* <span data-ttu-id="6b501-120">[height](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#height), [width](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#width)—Filter images by width and height.</span><span class="sxs-lookup"><span data-stu-id="6b501-120">[height](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#height), [width](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#width)—Filter images by width and height.</span></span>
* <span data-ttu-id="6b501-121">[imageContent](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imagecontent)—Filter images by content (for example, images that show only a person's face).</span><span class="sxs-lookup"><span data-stu-id="6b501-121">[imageContent](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imagecontent)—Filter images by content (for example, images that show only a person's face).</span></span>
* <span data-ttu-id="6b501-122">[imageType](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imagetype)—Filter images by type (for example, clip art, animated GIFs, or transparent backgrounds).</span><span class="sxs-lookup"><span data-stu-id="6b501-122">[imageType](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#imagetype)—Filter images by type (for example, clip art, animated GIFs, or transparent backgrounds).</span></span>
* <span data-ttu-id="6b501-123">[license](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#license)—Filter images by the type of license associated with the site.</span><span class="sxs-lookup"><span data-stu-id="6b501-123">[license](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#license)—Filter images by the type of license associated with the site.</span></span>
* <span data-ttu-id="6b501-124">[size](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#size)—Filter images by size, such as small images up to 200x200 pixels.</span><span class="sxs-lookup"><span data-stu-id="6b501-124">[size](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#size)—Filter images by size, such as small images up to 200x200 pixels.</span></span>

<span data-ttu-id="6b501-125">To get images from a specific domain, use the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator.</span><span class="sxs-lookup"><span data-stu-id="6b501-125">To get images from a specific domain, use the [site:](http://msdn.microsoft.com/library/ff795613.aspx) query operator.</span></span>

 > [!NOTE]
 > <span data-ttu-id="6b501-126">Responses to queries using the `site:` operator might include adult content regardless of the [safeSearch](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#safesearch) setting.</span><span class="sxs-lookup"><span data-stu-id="6b501-126">Responses to queries using the `site:` operator might include adult content regardless of the [safeSearch](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#safesearch) setting.</span></span> <span data-ttu-id="6b501-127">Only use `site:` if you're aware of the content on the domain.</span><span class="sxs-lookup"><span data-stu-id="6b501-127">Only use `site:` if you're aware of the content on the domain.</span></span>

<span data-ttu-id="6b501-128">The following example shows how to get small images from ContosoSailing.com that Bing discovered in the past week.</span><span class="sxs-lookup"><span data-stu-id="6b501-128">The following example shows how to get small images from ContosoSailing.com that Bing discovered in the past week.</span></span>  

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies+site:contososailing.com&size=small&freshness=week&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```

## <a name="bing-image-search-response-format"></a><span data-ttu-id="6b501-129">Bing Image Search response format</span><span class="sxs-lookup"><span data-stu-id="6b501-129">Bing Image Search response format</span></span>

<span data-ttu-id="6b501-130">The response message from Bing contains an [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) answer that contains a list of images that Cognitive Services determined to be relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="6b501-130">The response message from Bing contains an [Images](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#images) answer that contains a list of images that Cognitive Services determined to be relevant to the query.</span></span> <span data-ttu-id="6b501-131">Each [Image](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image) object in the list includes the following information about the image: the URL, its size, its dimensions, its encoding format, a URL to a thumbnail of the image, and the thumbnail's dimensions.</span><span class="sxs-lookup"><span data-stu-id="6b501-131">Each [Image](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image) object in the list includes the following information about the image: the URL, its size, its dimensions, its encoding format, a URL to a thumbnail of the image, and the thumbnail's dimensions.</span></span>

```json
{
    "name": "Rich Passage Sailing Dinghy",
    "webSearchUrl": "https:\/\/www.bing.com\/cr?IG=73118C8B4E3...",
    "thumbnailUrl": "https:\/\/tse1.mm.bing.net\/th?id=OIP.GNarK7m...",
    "datePublished": "2011-10-29T11:26:00",
    "contentUrl": "http:\/\/www.bing.com\/cr?IG=73118C8B4E3D4C3...",
    "hostPageUrl": "http:\/\/www.bing.com\/cr?IG=73118C8B4E3D4C3687...",
    "contentSize": "79239 B",
    "encodingFormat": "jpeg",
    "hostPageDisplayUrl": "en.contoso.org\/wiki\/File:Rich_Passage...",
    "width": 526,
    "height": 688,
    "thumbnail": {
        "width": 229,
        "height": 300
    },
    "imageInsightsToken": "ccid_GNarK7ma*mid_CCF85447ADA6...",
    "insightsSourcesSummary": {
        "shoppingSourcesCount": 0,
        "recipeSourcesCount": 0
    },
    "imageId": "CCF85447ADA6FFF9E96E7DF0B796F7A86E34593",
    "accentColor": "376094"
},
```

<span data-ttu-id="6b501-132">When you call the Bing Image Search API, Bing returns a list of results.</span><span class="sxs-lookup"><span data-stu-id="6b501-132">When you call the Bing Image Search API, Bing returns a list of results.</span></span> <span data-ttu-id="6b501-133">The list is a subset of the total number of results that are relevant to the query.</span><span class="sxs-lookup"><span data-stu-id="6b501-133">The list is a subset of the total number of results that are relevant to the query.</span></span> <span data-ttu-id="6b501-134">The response's `totalEstimatedMatches` field contains an estimate of the number of images that are available to view.</span><span class="sxs-lookup"><span data-stu-id="6b501-134">The response's `totalEstimatedMatches` field contains an estimate of the number of images that are available to view.</span></span> <span data-ttu-id="6b501-135">For details about how to page through the rest of the images, see [Paging Images](../paging-images.md).</span><span class="sxs-lookup"><span data-stu-id="6b501-135">For details about how to page through the rest of the images, see [Paging Images](../paging-images.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b501-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b501-136">Next steps</span></span>

<span data-ttu-id="6b501-137">If you haven't tried the Bing Image Search API before, try a [quickstart](../quickstarts/csharp.md).</span><span class="sxs-lookup"><span data-stu-id="6b501-137">If you haven't tried the Bing Image Search API before, try a [quickstart](../quickstarts/csharp.md).</span></span> <span data-ttu-id="6b501-138">If you're looking for something more complex, try the tutorial to create a [single-page web app](../tutorial-bing-image-search-single-page-app.md).</span><span class="sxs-lookup"><span data-stu-id="6b501-138">If you're looking for something more complex, try the tutorial to create a [single-page web app](../tutorial-bing-image-search-single-page-app.md).</span></span>
