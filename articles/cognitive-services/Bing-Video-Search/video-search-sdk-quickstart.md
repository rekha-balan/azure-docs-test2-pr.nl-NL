---
title: Video search SDK C# quickstart | Microsoft Docs
description: Setup for Video search SDK console application.
titleSuffix: Azure cognitive services setup News search SDK C# console application
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 01/29/2018
ms.author: v-gedod
ms.openlocfilehash: f53e2d0f0052ccfabb6d750556cb532f069c9121
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966308"
---
# <a name="video-search-sdk-c-quickstart"></a><span data-ttu-id="e8e13-103">Video Search SDK C# quickstart</span><span class="sxs-lookup"><span data-stu-id="e8e13-103">Video Search SDK C# quickstart</span></span>

<span data-ttu-id="e8e13-104">The Bing Video Search SDK contains the functionality of the REST API for web requests and parsing results.</span><span class="sxs-lookup"><span data-stu-id="e8e13-104">The Bing Video Search SDK contains the functionality of the REST API for web requests and parsing results.</span></span>

<span data-ttu-id="e8e13-105">The [source code for C# Bing Video Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingVideoSearch) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="e8e13-105">The [source code for C# Bing Video Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingVideoSearch) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="e8e13-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="e8e13-106">Application dependencies</span></span>

<span data-ttu-id="e8e13-107">To set up a console application using the Bing Video Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8e13-107">To set up a console application using the Bing Video Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span></span>  <span data-ttu-id="e8e13-108">Add the `Microsoft.Azure.CognitiveServices.Search.VideoSearch` package.</span><span class="sxs-lookup"><span data-stu-id="e8e13-108">Add the `Microsoft.Azure.CognitiveServices.Search.VideoSearch` package.</span></span>

<span data-ttu-id="e8e13-109">Installing the [[NuGet Video Search SDK package]](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.VideoSearch/1.2.0) also installs dependencies, including:</span><span class="sxs-lookup"><span data-stu-id="e8e13-109">Installing the [[NuGet Video Search SDK package]](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.VideoSearch/1.2.0) also installs dependencies, including:</span></span>
* <span data-ttu-id="e8e13-110">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="e8e13-110">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="e8e13-111">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="e8e13-111">Microsoft.Rest.ClientRuntime.Azure</span></span>
* <span data-ttu-id="e8e13-112">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="e8e13-112">Newtonsoft.Json</span></span>


## <a name="video-search-client"></a><span data-ttu-id="e8e13-113">Video Search client</span><span class="sxs-lookup"><span data-stu-id="e8e13-113">Video Search client</span></span>
<span data-ttu-id="e8e13-114">To create an instance of the `VideoSearchAPI` client, add using directives:</span><span class="sxs-lookup"><span data-stu-id="e8e13-114">To create an instance of the `VideoSearchAPI` client, add using directives:</span></span>
```
using Microsoft.Azure.CognitiveServices.Search.VideoSearch;
using Microsoft.Azure.CognitiveServices.Search.VideoSearch.Models;

```
<span data-ttu-id="e8e13-115">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="e8e13-115">Then, instantiate the client:</span></span>
```
var client = new VideoSearchAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));


```
<span data-ttu-id="e8e13-116">Use the client to search with a query text "SwiftKey" for videos.</span><span class="sxs-lookup"><span data-stu-id="e8e13-116">Use the client to search with a query text "SwiftKey" for videos.</span></span>
```
var videoResults = client.Videos.SearchAsync(query: "SwiftKey").Result;
Console.WriteLine("Search videos for query \"SwiftKey\"");

```

<span data-ttu-id="e8e13-117">Parse the results, then verify number of results and print out ID, name, and url of first video result.</span><span class="sxs-lookup"><span data-stu-id="e8e13-117">Parse the results, then verify number of results and print out ID, name, and url of first video result.</span></span>
```
if (videoResults == null)
{
    Console.WriteLine("Didn't see any video result data..");
}
else
{
    if (videoResults.Value.Count > 0)
    {
        var firstVideoResult = videoResults.Value.First();

        Console.WriteLine($"\r\nVideo result count: {videoResults.Value.Count}");
        Console.WriteLine($"First video id: {firstVideoResult.VideoId}");
        Console.WriteLine($"First video name: {firstVideoResult.Name}");
        Console.WriteLine($"First video url: {firstVideoResult.ContentUrl}");
    }
    else
    {
        Console.WriteLine("Couldn't find video results!");
    }
}

```
## <a name="complete-console-application"></a><span data-ttu-id="e8e13-118">Complete console application</span><span class="sxs-lookup"><span data-stu-id="e8e13-118">Complete console application</span></span>

<span data-ttu-id="e8e13-119">The following console application executes the previously defined query and parses results.</span><span class="sxs-lookup"><span data-stu-id="e8e13-119">The following console application executes the previously defined query and parses results.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.Azure.CognitiveServices.Search.VideoSearch;
using Microsoft.Azure.CognitiveServices.Search.VideoSearch.Models;

namespace VideoSrchSDK
{
    class Program
    {
        static void Main(string[] args)
        {
            var client = new VideoSearchAPI(new ApiKeyServiceClientCredentials("19aa718a79d6444daaa415981d9f54ad"));

            try
            {
                var videoResults = client.Videos.SearchAsync(query: "SwiftKey").Result;
                Console.WriteLine("Search videos for query \"SwiftKey\"");

                if (videoResults == null)
                {
                    Console.WriteLine("Didn't see any video result data..");
                }
                else
                {
                    if (videoResults.Value.Count > 0)
                    {
                        var firstVideoResult = videoResults.Value.First();

                        Console.WriteLine($"\r\nVideo result count: {videoResults.Value.Count}");
                        Console.WriteLine($"First video id: {firstVideoResult.VideoId}");
                        Console.WriteLine($"First video name: {firstVideoResult.Name}");
                        Console.WriteLine($"First video url: {firstVideoResult.ContentUrl}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find video results!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }

            // Include these calls to use queries defined under the following headings.
            //VideoSearchWithFilters(client);
            //VideoDetail(client);
            //VideoTrending(client);


            Console.WriteLine("Any key to exit...");
            Console.ReadKey();

        }

```
## <a name="url-parameters"></a><span data-ttu-id="e8e13-120">URL parameters</span><span class="sxs-lookup"><span data-stu-id="e8e13-120">URL parameters</span></span>

<span data-ttu-id="e8e13-121">Search on query text "Bellevue Trailer" for videos that are unchanged, short, and 1080p resolution.</span><span class="sxs-lookup"><span data-stu-id="e8e13-121">Search on query text "Bellevue Trailer" for videos that are unchanged, short, and 1080p resolution.</span></span>  <span data-ttu-id="e8e13-122">Verify the number of results, and print out ID, name, and url of first video result.</span><span class="sxs-lookup"><span data-stu-id="e8e13-122">Verify the number of results, and print out ID, name, and url of first video result.</span></span>

```
        public static void VideoSearchWithFilters(VideoSearchAPI client)
        {
            try
            {
                var videoResults = client.Videos.SearchAsync(query: "Bellevue Trailer", pricing: VideoPricing.Free, length: VideoLength.Short, resolution: VideoResolution.HD1080p).Result;
                Console.WriteLine("Search videos for query \"Bellevue Trailer\" that is free, short and 1080p resolution");

                if (videoResults == null)
                {
                    Console.WriteLine("Didn't see any video result data..");
                }
                else
                {
                    if (videoResults.Value.Count > 0)
                    {
                        var firstVideoResult = videoResults.Value.First();

                        Console.WriteLine($"\r\nVideo result count: {videoResults.Value.Count}");
                        Console.WriteLine($"First video id: {firstVideoResult.VideoId}");
                        Console.WriteLine($"First video name: {firstVideoResult.Name}");
                        Console.WriteLine($"First video url: {firstVideoResult.ContentUrl}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find video results!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }

        }


```
## <a name="trending-videos"></a><span data-ttu-id="e8e13-123">Trending videos</span><span class="sxs-lookup"><span data-stu-id="e8e13-123">Trending videos</span></span>
<span data-ttu-id="e8e13-124">Search for trending videos, then verify banner tiles and categories.</span><span class="sxs-lookup"><span data-stu-id="e8e13-124">Search for trending videos, then verify banner tiles and categories.</span></span>
```
        public static void VideoTrending(VideoSearchAPI client)
        {
            try
            {
                var trendingResults = client.Videos.TrendingAsync().Result;
                Console.WriteLine("Search trending videos");

                if (trendingResults == null)
                {
                    Console.WriteLine("Didn't see any trending video data..");
                }
                else
                {
                    // Banner Tiles
                    if (trendingResults.BannerTiles?.Count > 0)
                    {
                        var firstBannerTile = trendingResults.BannerTiles[0];
                        Console.WriteLine($"\r\nBanner tile count: {trendingResults.BannerTiles.Count}");
                        Console.WriteLine($"First banner tile text: {firstBannerTile.Query.Text}");
                        Console.WriteLine($"First banner tile url: {firstBannerTile.Query.WebSearchUrl}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find banner tiles!");
                    }

                    // Categories
                    if (trendingResults.Categories?.Count > 0)
                    {
                        var firstCategory = trendingResults.Categories[0];
                        Console.WriteLine($"Category count: {trendingResults.Categories.Count}");
                        Console.WriteLine($"First category title: {firstCategory.Title}");

                        if (firstCategory.Subcategories?.Count > 0)
                        {
                            var firstSubCategory = firstCategory.Subcategories[0];
                            Console.WriteLine($"SubCategory count: {firstCategory.Subcategories.Count}");
                            Console.WriteLine($"First sub category title: {firstSubCategory.Title}");

                            if (firstSubCategory.Tiles?.Count > 0)
                            {
                                var firstTile = firstSubCategory.Tiles[0];
                                Console.WriteLine($"Tile count: {firstSubCategory.Tiles.Count}");
                                Console.WriteLine($"First tile text: {firstTile.Query.Text}");
                                Console.WriteLine($"First tile url: {firstTile.Query.WebSearchUrl}");
                            }
                            else
                            {
                                Console.WriteLine("Couldn't find tiles!");
                            }
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find subcategories!");
                        }
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find categories!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }

        }


```
## <a name="details"></a><span data-ttu-id="e8e13-125">Details</span><span class="sxs-lookup"><span data-stu-id="e8e13-125">Details</span></span>
<span data-ttu-id="e8e13-126">Search videos for "Bellevue Trailer", and then search for detailed information of the first video.</span><span class="sxs-lookup"><span data-stu-id="e8e13-126">Search videos for "Bellevue Trailer", and then search for detailed information of the first video.</span></span>
```
        public static void VideoDetail(VideoSearchAPI client)
        {
            try
            {
                var videoResults = client.Videos.SearchAsync(query: "Bellevue Trailer").Result;

                var firstVideo = videoResults?.Value?.FirstOrDefault();

                if (firstVideo != null)
                {
                    var modules = new List<VideoInsightModule?>() { VideoInsightModule.All };
                    var videoDetail = client.Videos.DetailsAsync(query: "Bellevue Trailer", id: firstVideo.VideoId, modules: modules).Result;
                    Console.WriteLine($"Search detail for video id={firstVideo.VideoId}, name={firstVideo.Name}");

                    if (videoDetail != null)
                    {
                        if (videoDetail.VideoResult != null)
                        {
                            Console.WriteLine($"\r\nExpected video id: {videoDetail.VideoResult.VideoId}");
                            Console.WriteLine($"Expected video name: {videoDetail.VideoResult.Name}");
                            Console.WriteLine($"Expected video url: {videoDetail.VideoResult.ContentUrl}");
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find expected video!");
                        }

                        if (videoDetail?.RelatedVideos?.Value?.Count > 0)
                        {
                            var firstRelatedVideo = videoDetail.RelatedVideos.Value[0];
                            Console.WriteLine($"Related video count: {videoDetail.RelatedVideos.Value.Count}");
                            Console.WriteLine($"First related video id: {firstRelatedVideo.VideoId}");
                            Console.WriteLine($"First related video name: {firstRelatedVideo.Name}");
                            Console.WriteLine($"First related video url: {firstRelatedVideo.ContentUrl}");
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find any related video!");
                        }
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find detail about the video!");
                    }
                }
                else
                {
                    Console.WriteLine("Couldn't find video results!");
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }
        }
    }

```

## <a name="next-steps"></a><span data-ttu-id="e8e13-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8e13-127">Next steps</span></span>

[<span data-ttu-id="e8e13-128">Cognitive services .NET SDK samples</span><span class="sxs-lookup"><span data-stu-id="e8e13-128">Cognitive services .NET SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)