---
title: 'Quickstart: Request and filter images using the SDK using C#'
description: In this quickstart, you request and filter the images returned by Bing Image Search, using C#.
titleSuffix: Azure cognitive services setup Image search SDK C# console application
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 01/29/2018
ms.author: v-gedod
ms.openlocfilehash: 81375019e53b49b531fde1f81fbcb9a061cc5562
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866811"
---
# <a name="quickstart-request-and-filter-images-using-the-sdk-and-c"></a><span data-ttu-id="fc6c5-103">Quickstart: Request and filter images using the SDK and C#</span><span class="sxs-lookup"><span data-stu-id="fc6c5-103">Quickstart: Request and filter images using the SDK and C#</span></span>

<span data-ttu-id="fc6c5-104">The Bing Image Search SDK contains the functionality of the REST API for image requests and parsing results.</span><span class="sxs-lookup"><span data-stu-id="fc6c5-104">The Bing Image Search SDK contains the functionality of the REST API for image requests and parsing results.</span></span> 

<span data-ttu-id="fc6c5-105">The [source code for C# Bing Image Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingImageSearch) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="fc6c5-105">The [source code for C# Bing Image Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingImageSearch) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="fc6c5-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="fc6c5-106">Application dependencies</span></span>

<span data-ttu-id="fc6c5-107">To set up a console application using the Bing Image Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fc6c5-107">To set up a console application using the Bing Image Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span></span>  <span data-ttu-id="fc6c5-108">Add the `Microsoft.Azure.CognitiveServices.Search.ImageSearch` package.</span><span class="sxs-lookup"><span data-stu-id="fc6c5-108">Add the `Microsoft.Azure.CognitiveServices.Search.ImageSearch` package.</span></span>

<span data-ttu-id="fc6c5-109">Installing the [NuGet Image Search package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.ImageSearch/1.2.0) also installs dependencies, including:</span><span class="sxs-lookup"><span data-stu-id="fc6c5-109">Installing the [NuGet Image Search package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.ImageSearch/1.2.0) also installs dependencies, including:</span></span>
* <span data-ttu-id="fc6c5-110">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="fc6c5-110">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="fc6c5-111">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="fc6c5-111">Microsoft.Rest.ClientRuntime.Azure</span></span>
* <span data-ttu-id="fc6c5-112">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="fc6c5-112">Newtonsoft.Json</span></span>

## <a name="image-search-client"></a><span data-ttu-id="fc6c5-113">Image Search client</span><span class="sxs-lookup"><span data-stu-id="fc6c5-113">Image Search client</span></span>
<span data-ttu-id="fc6c5-114">To create an instance of the `ImageSearchAPI` client, add using directives:</span><span class="sxs-lookup"><span data-stu-id="fc6c5-114">To create an instance of the `ImageSearchAPI` client, add using directives:</span></span>
```
using Microsoft.Azure.CognitiveServices.Search.ImageSearch;
using Microsoft.Azure.CognitiveServices.Search.ImageSearch.Models;

```
<span data-ttu-id="fc6c5-115">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="fc6c5-115">Then, instantiate the client:</span></span>
```
var client = new ImageSearchAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));


```
<span data-ttu-id="fc6c5-116">Use the client to search with a query text:</span><span class="sxs-lookup"><span data-stu-id="fc6c5-116">Use the client to search with a query text:</span></span>
```
// Search for "Yosemite National Park"
var imageResults = client.Images.SearchAsync(query: "Canadian Rockies").Result;
Console.WriteLine("Search images for query \"canadian rockies\"");

```
<span data-ttu-id="fc6c5-117">Parse the image results returned by the previous query:</span><span class="sxs-lookup"><span data-stu-id="fc6c5-117">Parse the image results returned by the previous query:</span></span>

```
if (imageResults.Value.Count > 0)
{
    var firstImageResult = imageResults.Value.First();

    Console.WriteLine($"\r\nImage result count: {imageResults.Value.Count}");
    Console.WriteLine($"First image insights token: {firstImageResult.ImageInsightsToken}");
    Console.WriteLine($"First image thumbnail url: {firstImageResult.ThumbnailUrl}");
    Console.WriteLine($"First image content url: {firstImageResult.ContentUrl}");
}
else
{
    Console.WriteLine("Couldn't find image results!");
}

Console.WriteLine($"\r\nImage result total estimated matches: {imageResults.TotalEstimatedMatches}");

```

## <a name="complete-console-application"></a><span data-ttu-id="fc6c5-118">Complete console application</span><span class="sxs-lookup"><span data-stu-id="fc6c5-118">Complete console application</span></span>

<span data-ttu-id="fc6c5-119">The following console application executes the previously defined query "Canadian Rockies" to search for results then print first image insights token, thumbnail url, and image content url:</span><span class="sxs-lookup"><span data-stu-id="fc6c5-119">The following console application executes the previously defined query "Canadian Rockies" to search for results then print first image insights token, thumbnail url, and image content url:</span></span>

```
using System;
using System.Collections.Generic;
using Microsoft.Azure.CognitiveServices.Search.ImageSearch;
using Microsoft.Azure.CognitiveServices.Search.ImageSearch.Models;
using System.Linq;

namespace ImageSrchSDK
{
    class Program
    {
        static void Main(string[] args)
        {
            var client = new ImageSearchAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));
            ImageResults(client);
            ImageDetail(client);
            ImageTrending(client);
            ImageSearchWithFilters(client);

            Console.WriteLine("Any key to exit...");
            Console.ReadKey();
        }

        // Searches for results on query (Canadian Rockies) and prints first image insights token, thumbnail url, and image content url.
        static void ImageResults(ImageSearchAPI client)
        {
            try
            {
                var imageResults = client.Images.SearchAsync(query: "canadian rockies").Result;
                Console.WriteLine("Search images for query \"canadian rockies\"");

                if (imageResults == null)
                {
                    Console.WriteLine("No image result data.");
                }
                else
                {
                    // Image results
                    if (imageResults.Value.Count > 0)
                    {
                        var firstImageResult = imageResults.Value.First();

                        Console.WriteLine($"\r\nImage result count: {imageResults.Value.Count}");
                        Console.WriteLine($"First image insights token: {firstImageResult.ImageInsightsToken}");
                        Console.WriteLine($"First image thumbnail url: {firstImageResult.ThumbnailUrl}");
                        Console.WriteLine($"First image content url: {firstImageResult.ContentUrl}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find image results!");
                    }

                    Console.WriteLine($"\r\nImage result total estimated matches: {imageResults.TotalEstimatedMatches}");
                    Console.WriteLine($"Image result next offset: {imageResults.NextOffset}");

                    // Pivot suggestions
                    if (imageResults.PivotSuggestions.Count > 0)
                    {
                        var firstPivot = imageResults.PivotSuggestions.First();

                        Console.WriteLine($"\r\nPivot suggestion count: {imageResults.PivotSuggestions.Count}");
                        Console.WriteLine($"First pivot: {firstPivot.Pivot}");

                        if (firstPivot.Suggestions.Count > 0)
                        {
                            var firstSuggestion = firstPivot.Suggestions.First();

                            Console.WriteLine($"\r\nSuggestion count: {firstPivot.Suggestions.Count}");
                            Console.WriteLine($"First suggestion text: {firstSuggestion.Text}");
                            Console.WriteLine($"First suggestion web search url: {firstSuggestion.WebSearchUrl}");
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find suggestions!");
                        }
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find pivot suggestions!");
                    }

                    // Query expansions
                    if (imageResults.QueryExpansions.Count > 0)
                    {
                        var firstQueryExpansion = imageResults.QueryExpansions.First();

                        Console.WriteLine($"\r\nQuery expansion count: {imageResults.QueryExpansions.Count}");
                        Console.WriteLine($"First query expansion text: {firstQueryExpansion.Text}");
                        Console.WriteLine($"First query expansion search link: {firstQueryExpansion.SearchLink}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find query expansions!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("\r\nEncountered exception. " + ex.Message);
            }
        }
    }
}

```

## <a name="search-options"></a><span data-ttu-id="fc6c5-120">Search options</span><span class="sxs-lookup"><span data-stu-id="fc6c5-120">Search options</span></span>

<span data-ttu-id="fc6c5-121">The Bing search samples demonstrate various features of the SDK.</span><span class="sxs-lookup"><span data-stu-id="fc6c5-121">The Bing search samples demonstrate various features of the SDK.</span></span>  <span data-ttu-id="fc6c5-122">Add the following functions to the previously defined `ImageSrchSDK` class.</span><span class="sxs-lookup"><span data-stu-id="fc6c5-122">Add the following functions to the previously defined `ImageSrchSDK` class.</span></span>

### <a name="search-using-a-filter"></a><span data-ttu-id="fc6c5-123">Search using a filter</span><span class="sxs-lookup"><span data-stu-id="fc6c5-123">Search using a filter</span></span>

<span data-ttu-id="fc6c5-124">Search images for "studio ghibli", filtered for animated gifs and wide aspect, then verify number of results and print out insightsToken, thumbnail url, and url of first result.</span><span class="sxs-lookup"><span data-stu-id="fc6c5-124">Search images for "studio ghibli", filtered for animated gifs and wide aspect, then verify number of results and print out insightsToken, thumbnail url, and url of first result.</span></span>

```
        public static void ImageSearchWithFilters(ImageSearchAPI client)
        {
            try
            {
                var imageResults = client.Images.SearchAsync(query: "studio ghibli", imageType: ImageType.AnimatedGif, aspect: ImageAspect.Wide).Result;
                Console.WriteLine("Search images for \"studio ghibli\" results that are animated gifs and wide aspect");

                if (imageResults == null)
                {
                    Console.WriteLine("Didn't see any image result data.");
                }
                else
                {
                    // First image result
                    if (imageResults.Value.Count > 0)
                    {
                        var firstImageResult = imageResults.Value.First();

                        Console.WriteLine($"\r\nImage result count: {imageResults.Value.Count}");
                        Console.WriteLine($"First image insightsToken: {firstImageResult.ImageInsightsToken}");
                        Console.WriteLine($"First image thumbnail url: {firstImageResult.ThumbnailUrl}");
                        Console.WriteLine($"First image web search url: {firstImageResult.WebSearchUrl}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find image results!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }

        }

```

### <a name="trending-images"></a><span data-ttu-id="fc6c5-125">Trending images</span><span class="sxs-lookup"><span data-stu-id="fc6c5-125">Trending images</span></span>

<span data-ttu-id="fc6c5-126">Search for trending images, and then verify categories and tiles.</span><span class="sxs-lookup"><span data-stu-id="fc6c5-126">Search for trending images, and then verify categories and tiles.</span></span>

```
        public static void ImageTrending(ImageSearchAPI client)
        {
            try
            {
                var trendingResults = client.Images.TrendingAsync().Result;
                Console.WriteLine("Search trending images");

                if (trendingResults == null)
                {
                    Console.WriteLine("Didn't see any trending image data.");
                }
                else
                {
                    // Categories
                    if (trendingResults.Categories?.Count > 0)
                    {
                        var firstCategory = trendingResults.Categories[0];
                        Console.WriteLine($"\r\nCategory count: {trendingResults.Categories.Count}");
                        Console.WriteLine($"First category title: {firstCategory.Title}");

                        // Tiles
                        if (firstCategory.Tiles?.Count > 0)
                        {
                            var firstTile = firstCategory.Tiles[0];
                            Console.WriteLine($"\r\nTile count: {firstCategory.Tiles.Count}");
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

### <a name="image-details"></a><span data-ttu-id="fc6c5-127">Image details</span><span class="sxs-lookup"><span data-stu-id="fc6c5-127">Image details</span></span>

<span data-ttu-id="fc6c5-128">Search images for "Degas", and then search for image details of the first image.</span><span class="sxs-lookup"><span data-stu-id="fc6c5-128">Search images for "Degas", and then search for image details of the first image.</span></span>
```
        public static void ImageDetail(ImageSearchAPI client)
        {

            try
            {
                var imageResults = client.Images.SearchAsync(query: "degas").Result;

                var firstImage = imageResults?.Value?.FirstOrDefault();

                if (firstImage != null)
                {
                    var modules = new List<string>() { ImageInsightModule.All };
                    var imageDetail = client.Images.DetailsAsync(query: "degas", insightsToken: firstImage.ImageInsightsToken, modules: modules).Result;
                    Console.WriteLine($"\r\nSearch detail for image insightsToken={firstImage.ImageInsightsToken}");

                    if (imageDetail != null)
                    {
                        // Insights token
                        Console.WriteLine($"Expected image insights token: {imageDetail.ImageInsightsToken}");

                        // Best representative query
                        if (imageDetail.BestRepresentativeQuery != null)
                        {
                            Console.WriteLine($"\r\nBest representative query text: {imageDetail.BestRepresentativeQuery.Text}");
                            Console.WriteLine($"Best representative query web search url: {imageDetail.BestRepresentativeQuery.WebSearchUrl}");
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find best representative query!");
                        }

                        // Caption 
                        if (imageDetail.ImageCaption != null)
                        {
                            Console.WriteLine($"\r\nImage caption: {imageDetail.ImageCaption.Caption}");
                            Console.WriteLine($"Image caption data source url: {imageDetail.ImageCaption.DataSourceUrl}");
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find image caption!");
                        }

                        // Pages including the image
                        if (imageDetail.PagesIncluding?.Value?.Count > 0)
                        {
                            var firstPage = imageDetail.PagesIncluding.Value[0];
                            Console.WriteLine($"\r\nPages including count: {imageDetail.PagesIncluding.Value.Count}");
                            Console.WriteLine($"First page content url: {firstPage.ContentUrl}");
                            Console.WriteLine($"First page name: {firstPage.Name}");
                            Console.WriteLine($"First page date published: {firstPage.DatePublished}");
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find any pages including this image!");
                        }

                        // Related searches 
                        if (imageDetail.RelatedSearches?.Value?.Count > 0)
                        {
                            var firstRelatedSearch = imageDetail.RelatedSearches.Value[0];
                            Console.WriteLine($"\r\nRelated searches count: {imageDetail.RelatedSearches.Value.Count}");
                            Console.WriteLine($"First related search text: {firstRelatedSearch.Text}");
                            Console.WriteLine($"First related search web search url: {firstRelatedSearch.WebSearchUrl}");
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find any related searches!");
                        }

                        // Visually similar images
                        if (imageDetail.VisuallySimilarImages?.Value?.Count > 0)
                        {
                            var firstVisuallySimilarImage = imageDetail.VisuallySimilarImages.Value[0];
                            Console.WriteLine($"\r\nVisually similar images count: {imageDetail.RelatedSearches.Value.Count}");
                            Console.WriteLine($"First visually similar image name: {firstVisuallySimilarImage.Name}");
                            Console.WriteLine($"First visually similar image content url: {firstVisuallySimilarImage.ContentUrl}");
                            Console.WriteLine($"First visually similar image size: {firstVisuallySimilarImage.ContentSize}");
                        }
                        else
                        {
                            Console.WriteLine("Couldn't find any related searches!");
                        }

                        // Image tags
                        if (imageDetail.ImageTags?.Value?.Count > 0)
                        {
                            var firstTag = imageDetail.ImageTags.Value[0];
                            Console.WriteLine($"\r\nImage tags count: {imageDetail.ImageTags.Value.Count}");
                            Console.WriteLine($"First tag name: {firstTag.Name}");
                        }
                        else
                        {
                            Console.WriteLine("\r\nCouldn't find any related searches!");
                        }
                    }
                    else
                    {
                        Console.WriteLine("\r\nCouldn't find detail about the image!");
                    }
                }
                else
                {
                    Console.WriteLine("\r\nCouldn't find image results!");
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("\r\nEncountered exception. " + ex.Message);
            }
        }

```

## <a name="next-steps"></a><span data-ttu-id="fc6c5-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc6c5-129">Next steps</span></span>

[<span data-ttu-id="fc6c5-130">Cognitive services .NET SDK samples</span><span class="sxs-lookup"><span data-stu-id="fc6c5-130">Cognitive services .NET SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)