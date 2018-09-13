---
title: News search SDK C# quickstart | Microsoft Docs
description: Setup for News search SDK console application.
titleSuffix: Azure cognitive services News search SDK C# quickstart
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: article
ms.date: 01/30/2018
ms.author: v-gedod
ms.openlocfilehash: e803fd579c6b71b8b1754546446715795a12087a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865129"
---
# <a name="news-search-sdk-c-quickstart"></a><span data-ttu-id="81d8b-103">News Search SDK C# quickstart</span><span class="sxs-lookup"><span data-stu-id="81d8b-103">News Search SDK C# quickstart</span></span>

<span data-ttu-id="81d8b-104">The Bing News Search SDK contains the functionality of the REST API for news queries and parsing results.</span><span class="sxs-lookup"><span data-stu-id="81d8b-104">The Bing News Search SDK contains the functionality of the REST API for news queries and parsing results.</span></span> 

<span data-ttu-id="81d8b-105">The [source code for C# Bing News Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingNewsSearch) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="81d8b-105">The [source code for C# Bing News Search SDK samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7/BingNewsSearch) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="81d8b-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="81d8b-106">Application dependencies</span></span>

<span data-ttu-id="81d8b-107">To set up a console application using the Bing News Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81d8b-107">To set up a console application using the Bing News Search SDK, browse to the `Manage NuGet Packages` option from the Solution Explorer in Visual Studio.</span></span>  <span data-ttu-id="81d8b-108">Add the `Microsoft.Azure.CognitiveServices.Search.NewsSearch` package.</span><span class="sxs-lookup"><span data-stu-id="81d8b-108">Add the `Microsoft.Azure.CognitiveServices.Search.NewsSearch` package.</span></span>

<span data-ttu-id="81d8b-109">Installing the [NuGet News Search SDK package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.NewsSearch/1.2.0) also installs dependencies, including:</span><span class="sxs-lookup"><span data-stu-id="81d8b-109">Installing the [NuGet News Search SDK package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.NewsSearch/1.2.0) also installs dependencies, including:</span></span>
* <span data-ttu-id="81d8b-110">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="81d8b-110">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="81d8b-111">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="81d8b-111">Microsoft.Rest.ClientRuntime.Azure</span></span>
* <span data-ttu-id="81d8b-112">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="81d8b-112">Newtonsoft.Json</span></span>

## <a name="news-search-client"></a><span data-ttu-id="81d8b-113">News Search client</span><span class="sxs-lookup"><span data-stu-id="81d8b-113">News Search client</span></span>
<span data-ttu-id="81d8b-114">To create an instance of the `NewsSearchAPI` client, add using directive:</span><span class="sxs-lookup"><span data-stu-id="81d8b-114">To create an instance of the `NewsSearchAPI` client, add using directive:</span></span>
```
using Microsoft.Azure.CognitiveServices.Search.NewsSearch;

```
<span data-ttu-id="81d8b-115">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="81d8b-115">Then, instantiate the client:</span></span>
```
var client = new NewsSearchAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));


```
<span data-ttu-id="81d8b-116">Use the client to search with a query text:</span><span class="sxs-lookup"><span data-stu-id="81d8b-116">Use the client to search with a query text:</span></span>
```
var newsResults = client.News.SearchAsync(query: "Quantum  Computing", market: "en-us", count: 10).Result;
Console.WriteLine("Search news for query \"Quantum  Computing\" with market and count");

```
<span data-ttu-id="81d8b-117">Parse the news returned in the results of the previous query:</span><span class="sxs-lookup"><span data-stu-id="81d8b-117">Parse the news returned in the results of the previous query:</span></span>
```
if (newsResults.Value.Count > 0)
{
    var firstNewsResult = newsResults.Value.First();

    Console.WriteLine($"TotalEstimatedMatches value: {newsResults.TotalEstimatedMatches}");
    Console.WriteLine($"News result count: {newsResults.Value.Count}");
    Console.WriteLine($"First news name: {firstNewsResult.Name}");
    Console.WriteLine($"First news url: {firstNewsResult.Url}");
    Console.WriteLine($"First news description: {firstNewsResult.Description}");
    Console.WriteLine($"First news published time: {firstNewsResult.DatePublished}");
    Console.WriteLine($"First news provider: {firstNewsResult.Provider.First().Name}");
}

else
{
    Console.WriteLine("Couldn't find news results!");
}

```
## <a name="complete-console-application"></a><span data-ttu-id="81d8b-118">Complete console application</span><span class="sxs-lookup"><span data-stu-id="81d8b-118">Complete console application</span></span>

<span data-ttu-id="81d8b-119">The following console application executes the previously defined query and searches news for "Quantum  Computing".</span><span class="sxs-lookup"><span data-stu-id="81d8b-119">The following console application executes the previously defined query and searches news for "Quantum  Computing".</span></span> <span data-ttu-id="81d8b-120">The request includes `market` and `count` parameters.</span><span class="sxs-lookup"><span data-stu-id="81d8b-120">The request includes `market` and `count` parameters.</span></span> <span data-ttu-id="81d8b-121">The code verifies the number of results and prints out `totalEstimatedMatches`, `name`, `url`, `description`, `published time` and `name` of `provider` for the first news result.</span><span class="sxs-lookup"><span data-stu-id="81d8b-121">The code verifies the number of results and prints out `totalEstimatedMatches`, `name`, `url`, `description`, `published time` and `name` of `provider` for the first news result.</span></span>

```
using System;
using System.Linq;
using Microsoft.Azure.CognitiveServices.Search.NewsSearch;

namespace NewsSrchSDK
{
    class Program
    {
        static void Main(string[] args)
        {
            var client = new NewsSearchAPI(new ApiKeyServiceClientCredentials("YOUR-ACCESS-KEY"));

            try
            {
                var newsResults = client.News.SearchAsync(query: "Quantum  Computing", market: "en-us", count: 10).Result;
                Console.WriteLine("Search news for query \"Quantum  Computing\" with market and count");

                if (newsResults == null)
                {
                    Console.WriteLine("Didn't see any news result data..");
                }
                else
                {
                    if (newsResults.Value.Count > 0)
                    {
                        var firstNewsResult = newsResults.Value.First();

                        Console.WriteLine($"TotalEstimatedMatches value: {newsResults.TotalEstimatedMatches}");
                        Console.WriteLine($"News result count: {newsResults.Value.Count}");
                        Console.WriteLine($"First news name: {firstNewsResult.Name}");
                        Console.WriteLine($"First news url: {firstNewsResult.Url}");
                        Console.WriteLine($"First news description: {firstNewsResult.Description}");
                        Console.WriteLine($"First news published time: {firstNewsResult.DatePublished}");
                        Console.WriteLine($"First news provider: {firstNewsResult.Provider.First().Name}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find news results!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }

            // Include these methods to run queries explained under headings following.
            // NewsSearchWithFilters(client);
            // NewsCategory(client);
            // TrendingTopics(client);

            Console.WriteLine("Any key to exit...");
            Console.ReadKey();
        }

    }
}

```
## <a name="recent-news-freshness-and-sortby-parameters"></a><span data-ttu-id="81d8b-122">Recent news, freshness and sortBy parameters</span><span class="sxs-lookup"><span data-stu-id="81d8b-122">Recent news, freshness and sortBy parameters</span></span>
<span data-ttu-id="81d8b-123">The following code searches most recent news for "Artificial Intelligence" with `freshness` and `sortBy` parameters.</span><span class="sxs-lookup"><span data-stu-id="81d8b-123">The following code searches most recent news for "Artificial Intelligence" with `freshness` and `sortBy` parameters.</span></span> <span data-ttu-id="81d8b-124">It verifies the number of results and prints out `totalEstimatedMatches`, `name`, `url`, `description`, `published time`, and `name` of provider of the first news result.</span><span class="sxs-lookup"><span data-stu-id="81d8b-124">It verifies the number of results and prints out `totalEstimatedMatches`, `name`, `url`, `description`, `published time`, and `name` of provider of the first news result.</span></span>
```
        public static void NewsSearchWithFilters(NewsSearchAPI client)
        {
            try
            {
                var newsResults = client.News.SearchAsync(query: "Artificial Intelligence", market: "en-us", freshness: "Week", sortBy: "Date").Result;
                Console.WriteLine("Search most recent news for query \"Artificial Intelligence\" with freshness and sortBy");

                if (newsResults == null)
                {
                    Console.WriteLine("Didn't see any news result data..");
                }
                else
                {
                    if (newsResults.Value.Count > 0)
                    {
                        var firstNewsResult = newsResults.Value.First();

                        Console.WriteLine($"\r\nTotalEstimatedMatches value: {newsResults.TotalEstimatedMatches}");
                        Console.WriteLine($"News result count: {newsResults.Value.Count}");
                        Console.WriteLine($"First news name: {firstNewsResult.Name}");
                        Console.WriteLine($"First news url: {firstNewsResult.Url}");
                        Console.WriteLine($"First news description: {firstNewsResult.Description}");
                        Console.WriteLine($"First news published time: {firstNewsResult.DatePublished}");
                        Console.WriteLine($"First news provider: {firstNewsResult.Provider.First().Name}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find news results!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }
        }

```

## <a name="category-news-safe-search"></a><span data-ttu-id="81d8b-125">Category news, safe search</span><span class="sxs-lookup"><span data-stu-id="81d8b-125">Category news, safe search</span></span>
<span data-ttu-id="81d8b-126">The following code searches category news for movie and TV entertainment with safe search.</span><span class="sxs-lookup"><span data-stu-id="81d8b-126">The following code searches category news for movie and TV entertainment with safe search.</span></span>  <span data-ttu-id="81d8b-127">It verifies the number of results and prints out `category`, `name`, `url`, `description`, `published time`, and `name` of provider of the first news result.</span><span class="sxs-lookup"><span data-stu-id="81d8b-127">It verifies the number of results and prints out `category`, `name`, `url`, `description`, `published time`, and `name` of provider of the first news result.</span></span>
```
        public static void NewsCategory(NewsSearchAPI client)
        {
            try
            {
                var newsResults = client.News.CategoryAsync(category: "Entertainment_MovieAndTV", market: "en-us", safeSearch: "strict").Result;
                Console.WriteLine("Search category news for movie and TV entertainment with safe search");

                if (newsResults == null)
                {
                    Console.WriteLine("Didn't see any news result data..");
                }
                else
                {
                    if (newsResults.Value.Count > 0)
                    {
                        var firstNewsResult = newsResults.Value.First();

                        Console.WriteLine($"\r\nNews result count: {newsResults.Value.Count}");
                        Console.WriteLine($"First news category: {firstNewsResult.Category}");
                        Console.WriteLine($"First news name: {firstNewsResult.Name}");
                        Console.WriteLine($"First news url: {firstNewsResult.Url}");
                        Console.WriteLine($"First news description: {firstNewsResult.Description}");
                        Console.WriteLine($"First news published time: {firstNewsResult.DatePublished}");
                        Console.WriteLine($"First news provider: {firstNewsResult.Provider.First().Name}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find news results!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }
        }

```
## <a name="trending-topics"></a><span data-ttu-id="81d8b-128">Trending topics</span><span class="sxs-lookup"><span data-stu-id="81d8b-128">Trending topics</span></span>
<span data-ttu-id="81d8b-129">The following code searches news trending topics in Bing.</span><span class="sxs-lookup"><span data-stu-id="81d8b-129">The following code searches news trending topics in Bing.</span></span> <span data-ttu-id="81d8b-130">It verifies the number of results and prints out `name`, `text of query`, `webSearchUrl`, `newsSearchUrl`, and `image.Url` of the first news result.</span><span class="sxs-lookup"><span data-stu-id="81d8b-130">It verifies the number of results and prints out `name`, `text of query`, `webSearchUrl`, `newsSearchUrl`, and `image.Url` of the first news result.</span></span>
```
        public static void TrendingTopics(NewsSearchAPI client)
        {
            try
            {
                var trendingTopics = client.News.TrendingAsync(market: "en-us").Result;
                Console.WriteLine("Search news trending topics in Bing");

                if (trendingTopics == null)
                {
                    Console.WriteLine("Didn't see any news trending topics..");
                }
                else
                {
                    if (trendingTopics.Value.Count > 0)
                    {
                        var firstTopic = trendingTopics.Value.First();

                        Console.WriteLine($"\r\nTrending topics count: {trendingTopics.Value.Count}");
                        Console.WriteLine($"First topic name: {firstTopic.Name}");
                        Console.WriteLine($"First topic query: {firstTopic.Query.Text}");
                        Console.WriteLine($"First topic image url: {firstTopic.Image.Url}");
                        Console.WriteLine($"First topic webSearchUrl: {firstTopic.WebSearchUrl}");
                        Console.WriteLine($"First topic newsSearchUrl: {firstTopic.NewsSearchUrl}");
                    }
                    else
                    {
                        Console.WriteLine("Couldn't find news trending topics!");
                    }
                }
            }

            catch (Exception ex)
            {
                Console.WriteLine("Encountered exception. " + ex.Message);
            }
        }

```

## <a name="next-steps"></a><span data-ttu-id="81d8b-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="81d8b-131">Next steps</span></span>

[<span data-ttu-id="81d8b-132">Cognitive services .NET SDK samples</span><span class="sxs-lookup"><span data-stu-id="81d8b-132">Cognitive services .NET SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)