---
title: Bing News Search SDK Java quickstart | Microsoft Docs
description: Learn how to set up the Bing News Search SDK console application.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: article
ms.date: 02/16/2018
ms.author: v-gedod
ms.openlocfilehash: a6d4baf307fa3edcc0886d32204f2872fe310ce2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866198"
---
# <a name="bing-news-search-sdk-java-quickstart"></a><span data-ttu-id="0ff8e-103">Bing News Search SDK Java quickstart</span><span class="sxs-lookup"><span data-stu-id="0ff8e-103">Bing News Search SDK Java quickstart</span></span>

<span data-ttu-id="0ff8e-104">The Bing News Search SDK provides the REST API functionality for news queries and parsing results.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-104">The Bing News Search SDK provides the REST API functionality for news queries and parsing results.</span></span> 

<span data-ttu-id="0ff8e-105">The [source code for Java Bing News Search SDK samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingNewsSearch) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-105">The [source code for Java Bing News Search SDK samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingNewsSearch) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="0ff8e-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="0ff8e-106">Application dependencies</span></span>
<span data-ttu-id="0ff8e-107">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under **Search**.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-107">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under **Search**.</span></span> <span data-ttu-id="0ff8e-108">Install the Bing News Search SDK dependencies by using Maven, Gradle, or another dependency management system.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-108">Install the Bing News Search SDK dependencies by using Maven, Gradle, or another dependency management system.</span></span> <span data-ttu-id="0ff8e-109">The Maven POM file requires the declaration:</span><span class="sxs-lookup"><span data-stu-id="0ff8e-109">The Maven POM file requires the declaration:</span></span>
```
  <dependencies>
    <dependency>
        <groupId>com.microsoft.azure.cognitiveservices</groupId>
        <artifactId>azure-cognitiveservices-newssearch</artifactId>
        <version>0.0.1-beta-SNAPSHOT</version>
    </dependency>
  </dependencies>
```
## <a name="news-search-client"></a><span data-ttu-id="0ff8e-110">News Search client</span><span class="sxs-lookup"><span data-stu-id="0ff8e-110">News Search client</span></span>
<span data-ttu-id="0ff8e-111">Add imports to the class implementation.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-111">Add imports to the class implementation.</span></span>
```
import com.microsoft.azure.cognitiveservices.newssearch.*;
import com.microsoft.azure.cognitiveservices.newssearch.implementation.NewsInner;
import com.microsoft.azure.cognitiveservices.newssearch.implementation.NewsSearchAPIImpl;
import com.microsoft.azure.cognitiveservices.newssearch.implementation.TrendingTopicsInner;
import com.microsoft.rest.credentials.ServiceClientCredentials;
import okhttp3.Interceptor;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import java.io.IOException;
```
<span data-ttu-id="0ff8e-112">Implement the **NewsSearchAPIImpl** client, which requires an instance of the **ServiceClientCredentials** class.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-112">Implement the **NewsSearchAPIImpl** client, which requires an instance of the **ServiceClientCredentials** class.</span></span>
```
public static NewsSearchAPIImpl getClient(final String subscriptionKey) {
    return new NewsSearchAPIImpl("https://api.cognitive.microsoft.com/bing/v7.0/",
            new ServiceClientCredentials() {
                @Override
                public void applyCredentialsFilter(OkHttpClient.Builder builder) {
                    builder.addNetworkInterceptor(
                            new Interceptor() {
                                @Override
                                public Response intercept(Chain chain) throws IOException {
                                    Request request = null;
                                    Request original = chain.request();
                                    // Request customization: add request headers.
                                    Request.Builder requestBuilder = original.newBuilder()
                                            .addHeader("Ocp-Apim-Subscription-Key", subscriptionKey);
                                    request = requestBuilder.build();
                                    return chain.proceed(request);
                                }
                            });
                }
            });
}


```
<span data-ttu-id="0ff8e-113">Search for news with the single query "Quantum Computing."</span><span class="sxs-lookup"><span data-stu-id="0ff8e-113">Search for news with the single query "Quantum Computing."</span></span> <span data-ttu-id="0ff8e-114">Filter the search with the *market* and *count* parameters.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-114">Filter the search with the *market* and *count* parameters.</span></span> <span data-ttu-id="0ff8e-115">Verify the number of results.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-115">Verify the number of results.</span></span> <span data-ttu-id="0ff8e-116">Print information about the first news result: name, URL, publication date, description, provider name, and total number of estimated matches.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-116">Print information about the first news result: name, URL, publication date, description, provider name, and total number of estimated matches.</span></span>
```
public static void newsSearch(String subscriptionKey)
{
    NewsSearchAPIImpl client = getClient(subscriptionKey);

    try
    {
        NewsInner newsResults = client.searchs().list("Quantum  Computing", null, null, null,
                null, null, 100, null, "en-us",
                null, null, null, null, null,
                null, null);

        System.out.println("\r\nSearch news for query \"Quantum  Computing\" with market and count");

        if (newsResults == null)
        {
            System.out.println("Didn't see any news result data..");
        }
        else
        {
            if (newsResults.value().size() > 0)
            {
                NewsArticle firstNewsResult = newsResults.value().get(0);

                System.out.println(String.format("TotalEstimatedMatches value: %d", newsResults.totalEstimatedMatches()));
                System.out.println(String.format("News result count: %d", newsResults.value().size()));
                System.out.println(String.format("First news name: %s", firstNewsResult.name()));
                System.out.println(String.format("First news url: %s", firstNewsResult.url()));
                System.out.println(String.format("First news description: %s", firstNewsResult.description()));
                System.out.println(String.format("First news published time: %s", firstNewsResult.datePublished()));
                System.out.println(String.format("First news provider: %s", firstNewsResult.provider().get(0).name()));
            }
            else
            {
                System.out.println("Couldn't find news results!");
            }
        }
    }

    catch (Exception ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }
}

```
<span data-ttu-id="0ff8e-117">Search for recent news about "Artificial Intelligence."</span><span class="sxs-lookup"><span data-stu-id="0ff8e-117">Search for recent news about "Artificial Intelligence."</span></span> <span data-ttu-id="0ff8e-118">Filter the search with the *freshness* and *sortBy* parameters.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-118">Filter the search with the *freshness* and *sortBy* parameters.</span></span> <span data-ttu-id="0ff8e-119">Verify the number of results.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-119">Verify the number of results.</span></span> <span data-ttu-id="0ff8e-120">Print information about the first news result: name, URL, publication date, description, provider name, and total number of estimated matches.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-120">Print information about the first news result: name, URL, publication date, description, provider name, and total number of estimated matches.</span></span>
```
/**
 * Search recent news for (Artificial Intelligence) with the freshness and sortBy parameters.
 * Verify the number of results. Print the totalEstimatedMatches, name, url, description,
 * published time, and provider name for the first news result.
 * @param subscriptionKey cognitive services subscription key
 */
public static void newsSearchWithFilters(String subscriptionKey)
{
    NewsSearchAPIImpl client = getClient(subscriptionKey);

    try
    {
        NewsInner newsResults = client.searchs().list("Artificial Intelligence", null, null, null, null, null,
                    null, Freshness.WEEK, "en-us", null, null, null,
                    null, "Date", null, null);
        System.out.println("\r\nSearch most recent news for query \"Artificial Intelligence\" with freshness and sortBy");

        if (newsResults == null)
        {
            System.out.println("Didn't see any news result data..");
        }
        else
        {
            if (newsResults.value().size() > 0)
            {
                NewsArticle firstNewsResult = newsResults.value().get(0);

                System.out.println(String.format("TotalEstimatedMatches value: %d", newsResults.totalEstimatedMatches()));
                System.out.println(String.format("News result count: %d", newsResults.value().size()));
                System.out.println(String.format("First news name: %s", firstNewsResult.name()));
                System.out.println(String.format("First news url: %s", firstNewsResult.url()));
                System.out.println(String.format("First news description: %s", firstNewsResult.description()));
                System.out.println(String.format("First news published time: %s", firstNewsResult.datePublished()));
                System.out.println(String.format("First news provider: %s", firstNewsResult.provider().get(0).name()));
            }
            else
            {
                System.out.println("Couldn't find news results!");
            }
        }
    }

    catch (Exception ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }
}

```
<span data-ttu-id="0ff8e-121">Search the news **category** for *movie and TV entertainment* topics and use the *safe search* feature.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-121">Search the news **category** for *movie and TV entertainment* topics and use the *safe search* feature.</span></span> <span data-ttu-id="0ff8e-122">Verify the number of results.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-122">Verify the number of results.</span></span> <span data-ttu-id="0ff8e-123">Print the category, name, URL, description, publication date, and provider name for the first news result.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-123">Print the category, name, URL, description, publication date, and provider name for the first news result.</span></span>
```
/**
 * Search the news category for (movie and TV entertainment) with safe search. Verify the number of results. 
 * Print the category, name, url, description, published time, and provider name for the first news result.
 * @param subscriptionKey cognitive services subscription key
 */
public static void newsCategory(String subscriptionKey)
{
    NewsSearchAPIImpl client = getClient(subscriptionKey);

    try
    {
        NewsInner newsResults = client.categorys().list(null, null, null, null, null, "Entertainment_MovieAndTV",
                null, null, "en-us", null, null, SafeSearch.STRICT,
                null, null, null);
        System.out.println("\r\nSearch category news for movie and TV entertainment with safe search");

        if (newsResults == null)
        {
            System.out.println("Didn't see any news result data..");
        }
        else
        {
            if (newsResults.value().size() > 0)
            {
                NewsArticle firstNewsResult = newsResults.value().get(0);

                System.out.println(String.format("News result count: %d", newsResults.value().size()));
                //System.out.println(String.format("First news category: %d", firstNewsResult.category()));
                System.out.println(String.format("First news name: %s", firstNewsResult.name()));
                System.out.println(String.format("First news url: %s", firstNewsResult.url()));
                System.out.println(String.format("First news description: %s", firstNewsResult.description()));
                System.out.println(String.format("First news published time: %s", firstNewsResult.datePublished()));
                System.out.println(String.format("First news provider: %s", firstNewsResult.provider().get(0).name()));
            }
            else
            {
                System.out.println("Couldn't find news results!");
            }
        }
    }

    catch (Exception ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage()
        );
    }
}

```
<span data-ttu-id="0ff8e-124">Search for trending news topics.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-124">Search for trending news topics.</span></span> <span data-ttu-id="0ff8e-125">Verify the number of results.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-125">Verify the number of results.</span></span> <span data-ttu-id="0ff8e-126">Print the name, query text, web search URL, and news search URL for the first news result.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-126">Print the name, query text, web search URL, and news search URL for the first news result.</span></span>
```
public static void trendingTopics(String subscriptionKey)
{
    NewsSearchAPIImpl client = getClient(subscriptionKey);

    try
    {
        TrendingTopicsInner trendingTopics = client.trendings().list(null, null, null, null, null, null,
                "en-us", null, null, null, null, null, null, null);
        System.out.println("\r\nSearch news trending topics in Bing");

        if (trendingTopics == null)
        {
            System.out.println("Didn't see any news trending topics..");
        }
        else
        {
            if (trendingTopics.value().size() > 0)
            {
                NewsTopic firstTopic = trendingTopics.value().get(0);

                System.out.println(String.format("Trending topics count: %s", trendingTopics.value().size()));
                System.out.println(String.format("First topic name: %s", firstTopic.name()));
                System.out.println(String.format("First topic query: %s", firstTopic.query().text()));
                System.out.println(String.format("First topic image url: %s", firstTopic.image().url()));
                System.out.println(String.format("First topic webSearchUrl: %s", firstTopic.webSearchUrl()));
                System.out.println(String.format("First topic newsSearchUrl: %s", firstTopic.newsSearchUrl()));
            }
            else
            {
                System.out.println("Couldn't find news trending topics!");
            }
        }
    }

    catch (Exception ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }
}
```
<span data-ttu-id="0ff8e-127">Add the methods described in this article to a class with a main function for executing the code.</span><span class="sxs-lookup"><span data-stu-id="0ff8e-127">Add the methods described in this article to a class with a main function for executing the code.</span></span>
```
package javaNewsSDK;
import com.microsoft.azure.cognitiveservices.newssearch.*;

public class NewsSearchSDK {
    

    public static void main(String[] args) {
        String subscriptionKey = "YOUR-SUBSCRIPTION-KEY";
        NewsSearchSDK.newsSearch("YOUR-SUBSCRIPTION-KEY");
        NewsSearchSDK.newsSearchWithFilters("YOUR-SUBSCRIPTION-KEY");
        NewsSearchSDK.newsCategory("YOUR-SUBSCRIPTION-KEY");
        NewsSearchSDK.trendingTopics("YOUR-SUBSCRIPTION-KEY");
    }

    // Include the methods described in this article.
}
```
## <a name="next-steps"></a><span data-ttu-id="0ff8e-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ff8e-128">Next steps</span></span>

[<span data-ttu-id="0ff8e-129">Cognitive Services Java SDK samples</span><span class="sxs-lookup"><span data-stu-id="0ff8e-129">Cognitive Services Java SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)


