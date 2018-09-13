---
title: Search the web for trending videos | Microsoft Docs
description: Shows how to use the Bing Video Search API to search the web for trending videos.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 897A28A3-0980-484E-814F-FFE1D5C885E6
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 8db7fcf77042631260b4b165bd3d44053827f3ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855843"
---
# <a name="get-trending-videos"></a><span data-ttu-id="9a1cc-103">Get trending videos</span><span class="sxs-lookup"><span data-stu-id="9a1cc-103">Get trending videos</span></span>  

<span data-ttu-id="9a1cc-104">To get today's trending videos, send the following GET request:</span><span class="sxs-lookup"><span data-stu-id="9a1cc-104">To get today's trending videos, send the following GET request:</span></span>  
  
```
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/trending?mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE  
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; Touch; NOKIA; Lumia 822)  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```

<span data-ttu-id="9a1cc-105">The following markets support trending videos.</span><span class="sxs-lookup"><span data-stu-id="9a1cc-105">The following markets support trending videos.</span></span>  
 
-   <span data-ttu-id="9a1cc-106">en-AU (English, Australia)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-106">en-AU (English, Australia)</span></span>  
-   <span data-ttu-id="9a1cc-107">en-CA (English, Canada)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-107">en-CA (English, Canada)</span></span>  
-   <span data-ttu-id="9a1cc-108">en-GB (English, Great Britain)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-108">en-GB (English, Great Britain)</span></span>  
-   <span data-ttu-id="9a1cc-109">en-ID (English, Indonesia)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-109">en-ID (English, Indonesia)</span></span>  
-   <span data-ttu-id="9a1cc-110">en-IE (English, Ireland)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-110">en-IE (English, Ireland)</span></span>  
-   <span data-ttu-id="9a1cc-111">en-IN (English, India)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-111">en-IN (English, India)</span></span>  
-   <span data-ttu-id="9a1cc-112">en-NZ (English, New Zealand)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-112">en-NZ (English, New Zealand)</span></span>  
-   <span data-ttu-id="9a1cc-113">en-PH (English, Philippines)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-113">en-PH (English, Philippines)</span></span>  
-   <span data-ttu-id="9a1cc-114">en-SG (English, Singapore)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-114">en-SG (English, Singapore)</span></span>  
-   <span data-ttu-id="9a1cc-115">en-US (English, United States)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-115">en-US (English, United States)</span></span>  
-   <span data-ttu-id="9a1cc-116">en-WW (English, Worldwide aggregate code)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-116">en-WW (English, Worldwide aggregate code)</span></span>  
-   <span data-ttu-id="9a1cc-117">en-ZA (English, South Africa)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-117">en-ZA (English, South Africa)</span></span>  
-   <span data-ttu-id="9a1cc-118">zh-CN (Chinese, China)</span><span class="sxs-lookup"><span data-stu-id="9a1cc-118">zh-CN (Chinese, China)</span></span>

  
<span data-ttu-id="9a1cc-119">The following example shows a response that contains trending videos.</span><span class="sxs-lookup"><span data-stu-id="9a1cc-119">The following example shows a response that contains trending videos.</span></span>  

```  
{  
    "_type" : "TrendingVideos",  
    "bannerTiles" : [
        {  
            "query" : {  
                "text" : "Hello - Smith",  
                "displayText" : "Hello - Smith",  
                "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=3E8F5..."
            },  
            "image" : {  
                "description" : "Image from: contosowallpapers.com",  
                "thumbnailUrl" : "https:\/\/tse4.mm.bing.net\/th?id=RsA%2fdPlTmx4zS...",  
                "headLine" : "\"Hello\" is a song by...",  
                "contentUrl" : "http:\/\/www.contosowallpapers.com\/wp-content..."  
            }  
        },  
        . . .  
    ],  
    "categories" : [
        {  
            "title" : "Music videos",  
            "subcategories" : [
                {  
                    "tiles" : [
                        {  
                            "query" : {  
                                "text" : "Song Title - Artist Name",  
                                "displayText" : "Song Title - Artist Name",  
                                "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=3E8F5..."
                            },  
                            "image" : {  
                                "description" : "Image from: contoso.com",  
                                "thumbnailUrl" : "https:\/\/tse2.mm.bing.net\/th?id=...",  
                                "contentUrl" : "http:\/\/images6.contoso.com\/image..."  
                            }  
                        },  
                        . . .  
                    ],
                    "title" : "Top "  
                },
                {
                    "tiles" : [...],
                    "title" : "Trending"
                },
                . . .
            ],  
        },
        {
            "title" : "Viral videos",
            "subcategories" : [
                {
                    "tiles" : [...],
                    "title" : "Trending"
                },
                . . .
            ],  
        },
        . . .  
    ]  
}  
  
```  
<span data-ttu-id="9a1cc-120">The response contains a list of videos by category and subcategory.</span><span class="sxs-lookup"><span data-stu-id="9a1cc-120">The response contains a list of videos by category and subcategory.</span></span> <span data-ttu-id="9a1cc-121">For example, if the list of categories contained a Music Videos category and one of its subcategories was Top, you could create a Top Music Videos category in your user experience.</span><span class="sxs-lookup"><span data-stu-id="9a1cc-121">For example, if the list of categories contained a Music Videos category and one of its subcategories was Top, you could create a Top Music Videos category in your user experience.</span></span> <span data-ttu-id="9a1cc-122">You could then use the `thumbnailUrl`, `displayText`, and `webSearchUrl` fields to create a clickable tile under each category (for example, Top Music Videos).</span><span class="sxs-lookup"><span data-stu-id="9a1cc-122">You could then use the `thumbnailUrl`, `displayText`, and `webSearchUrl` fields to create a clickable tile under each category (for example, Top Music Videos).</span></span> <span data-ttu-id="9a1cc-123">When the user clicks the tile, they're taken to Bing's video browser where the video is played.</span><span class="sxs-lookup"><span data-stu-id="9a1cc-123">When the user clicks the tile, they're taken to Bing's video browser where the video is played.</span></span>

<span data-ttu-id="9a1cc-124">The response also contains banner videos, which are the most popular trending videos.</span><span class="sxs-lookup"><span data-stu-id="9a1cc-124">The response also contains banner videos, which are the most popular trending videos.</span></span> <span data-ttu-id="9a1cc-125">The banner videos may come from one or more of the categories.</span><span class="sxs-lookup"><span data-stu-id="9a1cc-125">The banner videos may come from one or more of the categories.</span></span>  
  
