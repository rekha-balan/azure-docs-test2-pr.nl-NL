---
title: Ruby Quickstart for Azure Cognitive Services, Bing Video Search API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Video Search API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jerkin
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 9/21/2017
ms.author: v-jerkin
ms.openlocfilehash: d621944415ec376f11a45ea96c331138ec4d6cdb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871093"
---
# <a name="quickstart-for-bing-video-search-api-with-ruby"></a><span data-ttu-id="919a2-103">Quickstart for Bing Video Search API with Ruby</span><span class="sxs-lookup"><span data-stu-id="919a2-103">Quickstart for Bing Video Search API with Ruby</span></span>

<span data-ttu-id="919a2-104">This article shows you how use the Bing Video Search API, part of Microsoft Cognitive Services on Azure.</span><span class="sxs-lookup"><span data-stu-id="919a2-104">This article shows you how use the Bing Video Search API, part of Microsoft Cognitive Services on Azure.</span></span> <span data-ttu-id="919a2-105">While this article employs Ruby, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="919a2-105">While this article employs Ruby, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

<span data-ttu-id="919a2-106">The example code was written to run under Ruby 2.4.</span><span class="sxs-lookup"><span data-stu-id="919a2-106">The example code was written to run under Ruby 2.4.</span></span>

<span data-ttu-id="919a2-107">Refer to the [API reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) for technical details about the APIs.</span><span class="sxs-lookup"><span data-stu-id="919a2-107">Refer to the [API reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) for technical details about the APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="919a2-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="919a2-108">Prerequisites</span></span>

<span data-ttu-id="919a2-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span><span class="sxs-lookup"><span data-stu-id="919a2-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span></span> <span data-ttu-id="919a2-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="919a2-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="919a2-111">You will need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="919a2-111">You will need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="bing-video-search"></a><span data-ttu-id="919a2-112">Bing video search</span><span class="sxs-lookup"><span data-stu-id="919a2-112">Bing video search</span></span>

<span data-ttu-id="919a2-113">The [Bing Video Search API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) returns video results from the Bing search engine.</span><span class="sxs-lookup"><span data-stu-id="919a2-113">The [Bing Video Search API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) returns video results from the Bing search engine.</span></span>

1. <span data-ttu-id="919a2-114">Create a new Ruby project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="919a2-114">Create a new Ruby project in your favorite IDE or editor.</span></span>
2. <span data-ttu-id="919a2-115">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="919a2-115">Add the code provided below.</span></span>
3. <span data-ttu-id="919a2-116">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="919a2-116">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="919a2-117">Run the program.</span><span class="sxs-lookup"><span data-stu-id="919a2-117">Run the program.</span></span>

```ruby
require 'net/https'
require 'uri'
require 'json'

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the accessKey string value with your valid access key.
accessKey = "enter key here"

# Verify the endpoint URI.  At this writing, only one endpoint is used for Bing
# search APIs.  In the future, regional endpoints may be available.  If you
# encounter unexpected authorization errors, double-check this value against
# the endpoint for your Bing Search instance in your Azure dashboard.

uri  = "https://api.cognitive.microsoft.com"
path = "/bing/v7.0/videos/search"

term = "kittens"

uri = URI(uri + path + "?q=" + URI.escape(term))

puts "Searching videos for: " + term

request = Net::HTTP::Get.new(uri)
request['Ocp-Apim-Subscription-Key'] = accessKey

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request(request)
end

puts "\nRelevant Headers:\n\n"
response.each_header do |key, value|
    # header names are coerced to lowercase
    if key.start_with?("bingapis-") or key.start_with?("x-msedge-") then
        puts key + ": " + value
    end
end

puts "\nJSON Response:\n\n"
puts JSON::pretty_generate(JSON(response.body))
```

<span data-ttu-id="919a2-118">**Response**</span><span class="sxs-lookup"><span data-stu-id="919a2-118">**Response**</span></span>

<span data-ttu-id="919a2-119">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="919a2-119">A successful response is returned in JSON, as shown in the following example:</span></span>

```json
{
    "_type": "Videos",
    "instrumentation": {},
    "readLink": "https://api.cognitive.microsoft.com/api/v7/videos/search?q=kittens",
    "webSearchUrl": "https://www.bing.com/videos/search?q=kittens",
    "totalEstimatedMatches": 1000,
    "value": [
        {
            "webSearchUrl": "https://www.bing.com/videos/search?q=kittens&view=...",
            "name": "Top 10 cute kitten videos compilation",
            "description": "HELP HOMELESS ANIMALS AND WIN A PRIZE BY CHOOSING...",
            "thumbnailUrl": "https://tse4.mm.bing.net/th?id=OVP.n1aE_Oikl4MtzBb...",
            "datePublished": "2014-11-12T22:47:36.0000000",
            "publisher": [
                {
                    "name": "Fabrikam"
                }
            ],
            "creator": {
                "name": "Marcus Appel"
            },
            "isAccessibleForFree": true,
            "contentUrl": "https://www.fabrikam.com/watch?v=8HVWitAW-Qg",
            "hostPageUrl": "https://www.fabrikam.com/watch?v=8HVWitAW-Qg",
            "encodingFormat": "h264",
            "hostPageDisplayUrl": "https://www.fabrikam.com/watch?v=8HVWitAW-Qg",
            "width": 480,
            "height": 360,
            "duration": "PT3M52S",
            "motionThumbnailUrl": "https://tse4.mm.bing.net/th?id=OM.j4QyJAENJphdZQ_1501386166&pid=Api",
            "embedHtml": "<iframe width=\"1280\" height=\"720\" src=\"https://www.fabrikam.com/embed/8HVWitAW-Qg?autoplay=1\" frameborder=\"0\" allowfullscreen></iframe>",
            "allowHttpsEmbed": true,
            "viewCount": 7513633,
            "thumbnail": {
                "width": 300,
                "height": 168
            },
            "videoId": "655D98260D012432848F6558260D012432848F",
            "allowMobileEmbed": true,
            "isSuperfresh": false
        },
        . . .
    ],
    "nextOffset": 36,
    "queryExpansions": [
        {
            "text": "Kittens Meowing",
            "displayText": "Meowing",
            "webSearchUrl": "https://www.bing.com/videos/search?q=Kittens+Meowing...",
            "searchLink": "https://api.cognitive.microsoft.com/api/v7/videos/search...",
            "thumbnail": {
                "thumbnailUrl": "https://tse3.mm.bing.net/th?q=Kittens+Meowing&pid..."
            }
        },
        {
            "text": "Funny Kittens",
            "displayText": "Funny",
            "webSearchUrl": "https://www.bing.com/videos/search?q=Funny+Kittens...",
            "searchLink": "https://api.cognitive.microsoft.com/api/v7/videos/search...",
            "thumbnail": {
                "thumbnailUrl": "https://tse3.mm.bing.net/th?q=Funny+Kittens&..."
            }
        },
        . . .
    ],
    "pivotSuggestions": [
        {
            "pivot": "kittens",
            "suggestions": [
                {
                    "text": "Cat",
                    "displayText": "Cat",
                    "webSearchUrl": "https://www.bing.com/videos/search?q=Cat...",
                    "searchLink": "https://api.cognitive.microsoft.com/api/v7/videos/search?...",
                    "thumbnail": {
                        "thumbnailUrl": "https://tse3.mm.bing.net/th?q=Cat&pid=Api..."
                    }
                },
                {
                    "text": "Feral Cat",
                    "displayText": "Feral Cat",
                    "webSearchUrl": "https://www.bing.com/videos/search?q=Feral+Cat...",
                    "searchLink": "https://api.cognitive.microsoft.com/api/v7/videos/search...",
                    "thumbnail": {
                        "thumbnailUrl": "https://tse3.mm.bing.net/th?q=Feral+Cat&pid=Api&..."
                    }
                }
            ]
        }
    ],
    "relatedSearches": [
        {
            "text": "Kittens Being Born",
            "displayText": "Kittens Being Born",
            "webSearchUrl": "https://www.bing.com/videos/search?q=Kittens+Being+Born...",
            "searchLink": "https://api.cognitive.microsoft.com/api/v7/videos/search?...",
            "thumbnail": {
                "thumbnailUrl": "https://tse1.mm.bing.net/th?q=Kittens+Being+Born&pid=..."
            }
        },
        . . .
    ]
}
```


## <a name="next-steps"></a><span data-ttu-id="919a2-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="919a2-120">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="919a2-121">[Paging videos](paging-videos.md)
> [Resizing and cropping thumbnail images](resize-and-crop-thumbnails.md)</span><span class="sxs-lookup"><span data-stu-id="919a2-121">[Paging videos](paging-videos.md)
[Resizing and cropping thumbnail images](resize-and-crop-thumbnails.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="919a2-122">See also</span><span class="sxs-lookup"><span data-stu-id="919a2-122">See also</span></span> 

 <span data-ttu-id="919a2-123">[Searching the web for videos](search-the-web.md) [Try it](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/)</span><span class="sxs-lookup"><span data-stu-id="919a2-123">[Searching the web for videos](search-the-web.md) [Try it](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/)</span></span>