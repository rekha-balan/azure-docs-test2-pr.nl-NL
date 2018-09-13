---
title: Video Search SDK Python quickstart | Microsoft Docs
description: Setup for Video Search SDK console application.
titleSuffix: Azure Video Search SDK Python quickstart
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 02/15/2018
ms.author: v-gedod
ms.openlocfilehash: 1c4769a6ca3391fa595cc078651beff330bbfd60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966804"
---
# <a name="video-search-sdk-python-quickstart"></a><span data-ttu-id="715d7-103">Video Search SDK Python quickstart</span><span class="sxs-lookup"><span data-stu-id="715d7-103">Video Search SDK Python quickstart</span></span>

<span data-ttu-id="715d7-104">The Bing Image Search SDK contains the functionality of the REST API for web queries and parsing results.</span><span class="sxs-lookup"><span data-stu-id="715d7-104">The Bing Image Search SDK contains the functionality of the REST API for web queries and parsing results.</span></span>

<span data-ttu-id="715d7-105">The [source code for Python Bing Video Search SDK samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/blob/master/samples/search/video_search_samples.py) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="715d7-105">The [source code for Python Bing Video Search SDK samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/blob/master/samples/search/video_search_samples.py) is available on Git Hub.</span></span>


## <a name="application-dependencies"></a><span data-ttu-id="715d7-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="715d7-106">Application dependencies</span></span>
<span data-ttu-id="715d7-107">If you don't already have it, install Python.</span><span class="sxs-lookup"><span data-stu-id="715d7-107">If you don't already have it, install Python.</span></span> <span data-ttu-id="715d7-108">The SDK is compatible with Python 2.7, 3.3, 3.4, 3.5 and 3.6.</span><span class="sxs-lookup"><span data-stu-id="715d7-108">The SDK is compatible with Python 2.7, 3.3, 3.4, 3.5 and 3.6.</span></span>

<span data-ttu-id="715d7-109">The general recommendation for Python development is to use a [virtual environment](https://docs.python.org/3/tutorial/venv.html).</span><span class="sxs-lookup"><span data-stu-id="715d7-109">The general recommendation for Python development is to use a [virtual environment](https://docs.python.org/3/tutorial/venv.html).</span></span> <span data-ttu-id="715d7-110">Install and initialize the virtual environment with the [venv module](https://pypi.python.org/pypi/virtualenv).</span><span class="sxs-lookup"><span data-stu-id="715d7-110">Install and initialize the virtual environment with the [venv module](https://pypi.python.org/pypi/virtualenv).</span></span> <span data-ttu-id="715d7-111">Install virtualenv for Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="715d7-111">Install virtualenv for Python 2.7.</span></span>
```
python -m venv mytestenv
```
<span data-ttu-id="715d7-112">Install Bing Videos Search SDK dependencies:</span><span class="sxs-lookup"><span data-stu-id="715d7-112">Install Bing Videos Search SDK dependencies:</span></span>
```
cd mytestenv
python -m pip install azure-cognitiveservices-search-videosearch
```
## <a name="video-search-client"></a><span data-ttu-id="715d7-113">Video Search client</span><span class="sxs-lookup"><span data-stu-id="715d7-113">Video Search client</span></span>
<span data-ttu-id="715d7-114">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span><span class="sxs-lookup"><span data-stu-id="715d7-114">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span></span> <span data-ttu-id="715d7-115">Add imports:</span><span class="sxs-lookup"><span data-stu-id="715d7-115">Add imports:</span></span>
```
subscription_key = "YOUR-SUBSCRIPTION-KEY"
```
<span data-ttu-id="715d7-116">Create an instance of the `CognitiveServicesCredentials`, and instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="715d7-116">Create an instance of the `CognitiveServicesCredentials`, and instantiate the client:</span></span>
```
client = VideoSearchAPI(CognitiveServicesCredentials(subscription_key))
```
<span data-ttu-id="715d7-117">Search videos for (SwiftKey), then verify number of results.</span><span class="sxs-lookup"><span data-stu-id="715d7-117">Search videos for (SwiftKey), then verify number of results.</span></span> <span data-ttu-id="715d7-118">Print out `ID`, `name` and `URL` of first video result.</span><span class="sxs-lookup"><span data-stu-id="715d7-118">Print out `ID`, `name` and `URL` of first video result.</span></span>
```
client = VideoSearchAPI(CognitiveServicesCredentials(subscription_key))

try:
    video_result = client.videos.search(query="SwiftKey")
    print("Search videos for query \"SwiftKey\"")

    if video_result.value:
        first_video_result = video_result.value[0]
        print("Video result count: {}".format(len(video_result.value)))
        print("First video id: {}".format(first_video_result.video_id))
        print("First video name: {}".format(first_video_result.name))
        print("First video url: {}".format(first_video_result.content_url))
    else:
        print("Didn't see any video result data..")

except Exception as err:
    print("Encountered exception. {}".format(err))

```
<span data-ttu-id="715d7-119">Search videos for (Bellevue Trailer) that is free, short, and 1080p resolution.</span><span class="sxs-lookup"><span data-stu-id="715d7-119">Search videos for (Bellevue Trailer) that is free, short, and 1080p resolution.</span></span> <span data-ttu-id="715d7-120">Verify number of results, and print out `ID`, `name` and `URL` of first video result.</span><span class="sxs-lookup"><span data-stu-id="715d7-120">Verify number of results, and print out `ID`, `name` and `URL` of first video result.</span></span>
```
def video_search_with_filtering(subscription_key):

    client = VideoSearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        video_result = client.videos.search(
            query="Bellevue Trailer",
            pricing=VideoPricing.free,  # Can use the str "free" too
            length=VideoLength.short,   # Can use the str "short" too
            resolution=VideoResolution.hd1080p  # Can use the str "hd1080p" too
        )
        print("Search videos for query \"Bellevue Trailer\" that is free, short and 1080p resolution")

        if video_result.value:
            first_video_result = video_result.value[0]
            print("Video result count: {}".format(len(video_result.value)))
            print("First video id: {}".format(first_video_result.video_id))
            print("First video name: {}".format(first_video_result.name))
            print("First video url: {}".format(first_video_result.content_url))
        else:
            print("Didn't see any video result data..")

    except Exception as err:
        print("Encountered exception. {}".format(err))

```

<span data-ttu-id="715d7-121">Get trending results.</span><span class="sxs-lookup"><span data-stu-id="715d7-121">Get trending results.</span></span> <span data-ttu-id="715d7-122">Verify banner tiles and categories:</span><span class="sxs-lookup"><span data-stu-id="715d7-122">Verify banner tiles and categories:</span></span>
```
def video_trending(subscription_key):

    client = VideoSearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        trending_result = client.videos.trending()
        print("Search trending video")

        # Banner tiles
        if trending_result.banner_tiles:
            first_banner_tile = trending_result.banner_tiles[0]
            print("Banner tile count: {}".format(len(trending_result.banner_tiles)))
            print("First banner tile text: {}".format(first_banner_tile.query.text))
            print("First banner tile url: {}".format(first_banner_tile.query.web_search_url))
        else:
            print("Couldn't find banner tiles!")

        # Categorires
        if trending_result.categories:
            first_category = trending_result.categories[0]
            print("Category count: {}".format(len(trending_result.categories)))
            print("First category title: {}".format(first_category.title))
            if first_category.subcategories:
                first_subcategory = first_category.subcategories[0]
                print("Subcategory count: {}".format(len(first_category.subcategories)))
                print("First subcategory title: {}".format(first_subcategory.title))
                if first_subcategory.tiles:
                    first_tile = first_subcategory.tiles[0]
                    print("Subcategory tile count: {}".format(len(first_subcategory.tiles)))
                    print("First tile text: {}".format(first_tile.query.text))
                    print("First tile url: {}".format(first_tile.query.web_search_url))
                else:
                    print("Couldn't find subcategory tiles!")
            else:
                print("Couldn't find subcategories!")
        else:
            print("Couldn't find categories!")

    except Exception as err:
        print("Encountered exception. {}".format(err))

```
<span data-ttu-id="715d7-123">Search videos for (Bellevue Trailer), and then search for detailed information of the first video.</span><span class="sxs-lookup"><span data-stu-id="715d7-123">Search videos for (Bellevue Trailer), and then search for detailed information of the first video.</span></span>
```
def video_detail(subscription_key):

    client = VideoSearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        video_result = client.videos.search(query="Bellevue Trailer")
        first_video_result = video_result.value[0]

        video_details = client.videos.details(
            query="Bellevue Trailer",
            id=first_video_result.video_id,
            modules=[VideoInsightModule.all]  # Can use ["all"] too
        )
        print("Search detail for video id={}, name={}".format(
            first_video_result.video_id,
            first_video_result.name
        ))

        if video_details.video_result:
            print("Expected Video id: {}".format(video_details.video_result.video_id))
            print("Expected Video name: {}".format(video_details.video_result.name))
            print("Expected Video url: {}".format(video_details.video_result.content_url))
        else:
            print("Couldn't find expected video")

        if video_details.related_videos.value:
            first_related_video = video_details.related_videos.value[0]
            print("Related video count: {}".format(len(video_details.related_videos.value)))
            print("First related video id: {}".format(first_related_video.video_id))
            print("First related video name: {}".format(first_related_video.name))
            print("First related video content url: {}".format(first_related_video.content_url))
        else:
            print("Couldn't find any related video!")

    except Exception as err:
        print("Encountered exception. {}".format(err))

```
## <a name="next-steps"></a><span data-ttu-id="715d7-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="715d7-124">Next steps</span></span>

[<span data-ttu-id="715d7-125">Cognitive Services Python SDK samples</span><span class="sxs-lookup"><span data-stu-id="715d7-125">Cognitive Services Python SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)

