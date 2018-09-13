---
title: 'Quickstart: Use the Bing Web Search SDK for C#'
description: Learn to use the Bing Web Search SDK for C#.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 08/16/2018
ms.author: erhopf
ms.openlocfilehash: ed958f4a691b878cfa7ff9766a0fb72857cce5db
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868297"
---
# <a name="quickstart-use-the-bing-web-search-sdk-for-c"></a><span data-ttu-id="09176-103">Quickstart: Use the Bing Web Search SDK for C#</span><span class="sxs-lookup"><span data-stu-id="09176-103">Quickstart: Use the Bing Web Search SDK for C#</span></span>

<span data-ttu-id="09176-104">The Bing Web Search SDK makes it easy to integrate Bing Web Search into your C# application.</span><span class="sxs-lookup"><span data-stu-id="09176-104">The Bing Web Search SDK makes it easy to integrate Bing Web Search into your C# application.</span></span> <span data-ttu-id="09176-105">In this quickstart, you'll learn how to instantiate a client, send a request, and print the response.</span><span class="sxs-lookup"><span data-stu-id="09176-105">In this quickstart, you'll learn how to instantiate a client, send a request, and print the response.</span></span>

<span data-ttu-id="09176-106">Want to see the code right now?</span><span class="sxs-lookup"><span data-stu-id="09176-106">Want to see the code right now?</span></span> <span data-ttu-id="09176-107">The [Bing Web Search SDK for C# samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/) are available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="09176-107">The [Bing Web Search SDK for C# samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/) are available on GitHub.</span></span>

[!INCLUDE [bing-web-search-quickstart-signup](../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a><span data-ttu-id="09176-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="09176-108">Prerequisites</span></span>

<span data-ttu-id="09176-109">Here are a few things that you'll need before running this quickstart:</span><span class="sxs-lookup"><span data-stu-id="09176-109">Here are a few things that you'll need before running this quickstart:</span></span>

* <span data-ttu-id="09176-110">[Visual Studio](https://visualstudio.microsoft.com/downloads/) or</span><span class="sxs-lookup"><span data-stu-id="09176-110">[Visual Studio](https://visualstudio.microsoft.com/downloads/) or</span></span>
* [<span data-ttu-id="09176-111">Visual Studio Code 2017</span><span class="sxs-lookup"><span data-stu-id="09176-111">Visual Studio Code 2017</span></span>](https://code.visualstudio.com/download)
  * [<span data-ttu-id="09176-112">C# for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="09176-112">C# for Visual Studio Code</span></span>](https://visualstudio.microsoft.com/downloads/)
  * [<span data-ttu-id="09176-113">NuGet Package Manager</span><span class="sxs-lookup"><span data-stu-id="09176-113">NuGet Package Manager</span></span>](https://github.com/jmrog/vscode-nuget-package-manager)
* [<span data-ttu-id="09176-114">.Net Core SDK</span><span class="sxs-lookup"><span data-stu-id="09176-114">.Net Core SDK</span></span>](https://www.microsoft.com/net/download)

## <a name="create-a-project-and-install-dependencies"></a><span data-ttu-id="09176-115">Create a project and install dependencies</span><span class="sxs-lookup"><span data-stu-id="09176-115">Create a project and install dependencies</span></span>

<span data-ttu-id="09176-116">The first step is to create a new console project.</span><span class="sxs-lookup"><span data-stu-id="09176-116">The first step is to create a new console project.</span></span> <span data-ttu-id="09176-117">If you need help setting up a console project, see [Hello World -- Your First Program (C# Programming Guide)](https://docs.microsoft.com/dotnet/csharp/programming-guide/inside-a-program/hello-world-your-first-program).</span><span class="sxs-lookup"><span data-stu-id="09176-117">If you need help setting up a console project, see [Hello World -- Your First Program (C# Programming Guide)](https://docs.microsoft.com/dotnet/csharp/programming-guide/inside-a-program/hello-world-your-first-program).</span></span> <span data-ttu-id="09176-118">To use the Bing Web Search SDK in your application, you'll need to install `Microsoft.Azure.CognitiveServices.Search.WebSearch` using the NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="09176-118">To use the Bing Web Search SDK in your application, you'll need to install `Microsoft.Azure.CognitiveServices.Search.WebSearch` using the NuGet Package Manager.</span></span>

<span data-ttu-id="09176-119">The [Web Search SDK package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.WebSearch/1.2.0) also installs:</span><span class="sxs-lookup"><span data-stu-id="09176-119">The [Web Search SDK package](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.WebSearch/1.2.0) also installs:</span></span>

* <span data-ttu-id="09176-120">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="09176-120">Microsoft.Rest.ClientRuntime</span></span>
* <span data-ttu-id="09176-121">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="09176-121">Microsoft.Rest.ClientRuntime.Azure</span></span>
* <span data-ttu-id="09176-122">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="09176-122">Newtonsoft.Json</span></span>

## <a name="declare-dependencies"></a><span data-ttu-id="09176-123">Declare dependencies</span><span class="sxs-lookup"><span data-stu-id="09176-123">Declare dependencies</span></span>

<span data-ttu-id="09176-124">Open your project in Visual Studio or Visual Studio Code and import these dependencies:</span><span class="sxs-lookup"><span data-stu-id="09176-124">Open your project in Visual Studio or Visual Studio Code and import these dependencies:</span></span>

```csharp
using System;
using System.Collections.Generic;
using Microsoft.Azure.CognitiveServices.Search.WebSearch;
using Microsoft.Azure.CognitiveServices.Search.WebSearch.Models;
using System.Linq;
```

## <a name="create-project-scaffolding"></a><span data-ttu-id="09176-125">Create project scaffolding</span><span class="sxs-lookup"><span data-stu-id="09176-125">Create project scaffolding</span></span>

<span data-ttu-id="09176-126">When you created your new console project, a namespace and class for your application should have been created.</span><span class="sxs-lookup"><span data-stu-id="09176-126">When you created your new console project, a namespace and class for your application should have been created.</span></span> <span data-ttu-id="09176-127">Your program should look like this:</span><span class="sxs-lookup"><span data-stu-id="09176-127">Your program should look like this:</span></span>

```csharp
namespace WebSearchSDK
{
    class YOUR_PROGRAM
    {

        // The code in the following sections goes here.

    }
}
```

<span data-ttu-id="09176-128">In the following sections, we'll build our sample application within this class.</span><span class="sxs-lookup"><span data-stu-id="09176-128">In the following sections, we'll build our sample application within this class.</span></span>

## <a name="construct-a-request"></a><span data-ttu-id="09176-129">Construct a request</span><span class="sxs-lookup"><span data-stu-id="09176-129">Construct a request</span></span>

<span data-ttu-id="09176-130">This code constructs the search query.</span><span class="sxs-lookup"><span data-stu-id="09176-130">This code constructs the search query.</span></span>

```csharp
public static void WebResults(WebSearchAPI client)
{
    try
    {
        var webData = client.Web.Search(query: "Yosemite National Park");
        Console.WriteLine("Searching for \"Yosemite National Park\"");

        // Code for handling responses is provided in the next section...

    }
    catch (Exception ex)
    {
        Console.WriteLine("Encountered exception. " + ex.Message);
    }
}
```

## <a name="handle-the-response"></a><span data-ttu-id="09176-131">Handle the response</span><span class="sxs-lookup"><span data-stu-id="09176-131">Handle the response</span></span>

<span data-ttu-id="09176-132">Next, let's add some code to parse the response and print the results.</span><span class="sxs-lookup"><span data-stu-id="09176-132">Next, let's add some code to parse the response and print the results.</span></span> <span data-ttu-id="09176-133">The `name` and `url` for the first web page, image, news article, and video are printed if present in the response object.</span><span class="sxs-lookup"><span data-stu-id="09176-133">The `name` and `url` for the first web page, image, news article, and video are printed if present in the response object.</span></span>

```csharp
if (webData?.WebPages?.Value?.Count > 0)
{
    // find the first web page
    var firstWebPagesResult = webData.WebPages.Value.FirstOrDefault();

    if (firstWebPagesResult != null)
    {
        Console.WriteLine("Webpage Results # {0}", webData.WebPages.Value.Count);
        Console.WriteLine("First web page name: {0} ", firstWebPagesResult.Name);
        Console.WriteLine("First web page URL: {0} ", firstWebPagesResult.Url);
    }
    else
    {
        Console.WriteLine("Didn't find any web pages...");
    }
}
else
{
    Console.WriteLine("Didn't find any web pages...");
}

/*
 * Images
 * If the search response contains images, the first result's name
 * and url are printed.
 */
if (webData?.Images?.Value?.Count > 0)
{
    // find the first image result
    var firstImageResult = webData.Images.Value.FirstOrDefault();

    if (firstImageResult != null)
    {
        Console.WriteLine("Image Results # {0}", webData.Images.Value.Count);
        Console.WriteLine("First Image result name: {0} ", firstImageResult.Name);
        Console.WriteLine("First Image result URL: {0} ", firstImageResult.ContentUrl);
    }
    else
    {
        Console.WriteLine("Didn't find any images...");
    }
}
else
{
    Console.WriteLine("Didn't find any images...");
}

/*
 * News
 * If the search response contains news articles, the first result's name
 * and url are printed.
 */
if (webData?.News?.Value?.Count > 0)
{
    // find the first news result
    var firstNewsResult = webData.News.Value.FirstOrDefault();

    if (firstNewsResult != null)
    {
        Console.WriteLine("\r\nNews Results # {0}", webData.News.Value.Count);
        Console.WriteLine("First news result name: {0} ", firstNewsResult.Name);
        Console.WriteLine("First news result URL: {0} ", firstNewsResult.Url);
    }
    else
    {
        Console.WriteLine("Didn't find any news articles...");
    }
}
else
{
    Console.WriteLine("Didn't find any news articles...");
}

/*
 * Videos
 * If the search response contains videos, the first result's name
 * and url are printed.
 */
if (webData?.Videos?.Value?.Count > 0)
{
    // find the first video result
    var firstVideoResult = webData.Videos.Value.FirstOrDefault();

    if (firstVideoResult != null)
    {
        Console.WriteLine("\r\nVideo Results # {0}", webData.Videos.Value.Count);
        Console.WriteLine("First Video result name: {0} ", firstVideoResult.Name);
        Console.WriteLine("First Video result URL: {0} ", firstVideoResult.ContentUrl);
    }
    else
    {
        Console.WriteLine("Didn't find any videos...");
    }
}
else
{
    Console.WriteLine("Didn't find any videos...");
}
```

## <a name="declare-the-main-method"></a><span data-ttu-id="09176-134">Declare the main method</span><span class="sxs-lookup"><span data-stu-id="09176-134">Declare the main method</span></span>

<span data-ttu-id="09176-135">In this application, the main method includes code that instantiates the client, validates the `subscriptionKey`, and calls `WebResults`.</span><span class="sxs-lookup"><span data-stu-id="09176-135">In this application, the main method includes code that instantiates the client, validates the `subscriptionKey`, and calls `WebResults`.</span></span> <span data-ttu-id="09176-136">Make sure that you enter a valid subscription key for your Azure account before continuing.</span><span class="sxs-lookup"><span data-stu-id="09176-136">Make sure that you enter a valid subscription key for your Azure account before continuing.</span></span>

```csharp
static void Main(string[] args)
{
    var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR_SUBSCRIPTION_KEY"));

    WebResults(client);

    Console.WriteLine("Press any key to exit...");
    Console.ReadKey();
}
```

## <a name="run-the-application"></a><span data-ttu-id="09176-137">Run the application</span><span class="sxs-lookup"><span data-stu-id="09176-137">Run the application</span></span>

<span data-ttu-id="09176-138">Let's run the application!</span><span class="sxs-lookup"><span data-stu-id="09176-138">Let's run the application!</span></span>

```console
dotnet run
```

## <a name="define-functions-and-filter-results"></a><span data-ttu-id="09176-139">Define functions and filter results</span><span class="sxs-lookup"><span data-stu-id="09176-139">Define functions and filter results</span></span>

<span data-ttu-id="09176-140">Now that you've made your first call to the Bing Web Search API, let's look at a few functions that highlight SDK functionality for refining queries and filtering results.</span><span class="sxs-lookup"><span data-stu-id="09176-140">Now that you've made your first call to the Bing Web Search API, let's look at a few functions that highlight SDK functionality for refining queries and filtering results.</span></span> <span data-ttu-id="09176-141">Each function can be added to your C# application created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="09176-141">Each function can be added to your C# application created in the previous section.</span></span>

### <a name="limit-the-number-of-results-returned-by-bing"></a><span data-ttu-id="09176-142">Limit the number of results returned by Bing</span><span class="sxs-lookup"><span data-stu-id="09176-142">Limit the number of results returned by Bing</span></span>

<span data-ttu-id="09176-143">This sample uses the `count` and `offset` parameters to limit the number of results returned for "Best restaurants in Seattle".</span><span class="sxs-lookup"><span data-stu-id="09176-143">This sample uses the `count` and `offset` parameters to limit the number of results returned for "Best restaurants in Seattle".</span></span> <span data-ttu-id="09176-144">The `name` and `URL` for the first result are printed.</span><span class="sxs-lookup"><span data-stu-id="09176-144">The `name` and `URL` for the first result are printed.</span></span>

1. <span data-ttu-id="09176-145">Add this code to your console project:</span><span class="sxs-lookup"><span data-stu-id="09176-145">Add this code to your console project:</span></span>
    ```csharp
    public static void WebResultsWithCountAndOffset(WebSearchAPI client)
    {
        try
        {
            var webData = client.Web.SearchAsync(query: "Best restaurants in Seattle", offset: 10, count: 20).Result;
            Console.WriteLine("\r\nSearching for \" Best restaurants in Seattle \"");

            if (webData?.WebPages?.Value?.Count > 0)
            {
                var firstWebPagesResult = webData.WebPages.Value.FirstOrDefault();

                if (firstWebPagesResult != null)
                {
                    Console.WriteLine("Web Results #{0}", webData.WebPages.Value.Count);
                    Console.WriteLine("First web page name: {0} ", firstWebPagesResult.Name);
                    Console.WriteLine("First web page URL: {0} ", firstWebPagesResult.Url);
                }
                else
                {
                    Console.WriteLine("Couldn't find first web result!");
                }
            }
            else
            {
                Console.WriteLine("Didn't see any Web data..");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("Encountered exception. " + ex.Message);
        }
    }
    ```
2. <span data-ttu-id="09176-146">Add `WebResultsWithCountAndOffset` to `main`:</span><span class="sxs-lookup"><span data-stu-id="09176-146">Add `WebResultsWithCountAndOffset` to `main`:</span></span>
    ```csharp
    static void Main(string[] args)
    {
        var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR_SUBSCRIPTION_KEY"));

        WebResults(client);
        // Search with count and offset...
        WebResultsWithCountAndOffset(client);  

        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
    ```
3. <span data-ttu-id="09176-147">Run the application.</span><span class="sxs-lookup"><span data-stu-id="09176-147">Run the application.</span></span>

### <a name="filter-for-news"></a><span data-ttu-id="09176-148">Filter for news</span><span class="sxs-lookup"><span data-stu-id="09176-148">Filter for news</span></span>

<span data-ttu-id="09176-149">This sample uses the `response_filter` parameter to filter search results.</span><span class="sxs-lookup"><span data-stu-id="09176-149">This sample uses the `response_filter` parameter to filter search results.</span></span> <span data-ttu-id="09176-150">The search results returned are limited to news articles for "Microsoft".</span><span class="sxs-lookup"><span data-stu-id="09176-150">The search results returned are limited to news articles for "Microsoft".</span></span> <span data-ttu-id="09176-151">The `name` and `URL` for the first result are printed.</span><span class="sxs-lookup"><span data-stu-id="09176-151">The `name` and `URL` for the first result are printed.</span></span>

1. <span data-ttu-id="09176-152">Add this code to your console project:</span><span class="sxs-lookup"><span data-stu-id="09176-152">Add this code to your console project:</span></span>
    ```csharp
    public static void WebSearchWithResponseFilter(WebSearchAPI client)
    {
        try
        {
            IList<string> responseFilterstrings = new List<string>() { "news" };
            var webData = client.Web.SearchAsync(query: "Microsoft", responseFilter: responseFilterstrings).Result;
            Console.WriteLine("\r\nSearching for \" Microsoft \" with response filter \"news\"");

            if (webData?.News?.Value?.Count > 0)
            {
                var firstNewsResult = webData.News.Value.FirstOrDefault();

                if (firstNewsResult != null)
                {
                    Console.WriteLine("News Results #{0}", webData.News.Value.Count);
                    Console.WriteLine("First news result name: {0} ", firstNewsResult.Name);
                    Console.WriteLine("First news result URL: {0} ", firstNewsResult.Url);
                }
                else
                {
                    Console.WriteLine("Couldn't find first News results!");
                }
            }
            else
            {
                Console.WriteLine("Didn't see any News data..");
            }

        }
        catch (Exception ex)
        {
            Console.WriteLine("Encountered exception. " + ex.Message);
        }
    }
    ```
2. <span data-ttu-id="09176-153">Add `WebResultsWithCountAndOffset` to `main`:</span><span class="sxs-lookup"><span data-stu-id="09176-153">Add `WebResultsWithCountAndOffset` to `main`:</span></span>
    ```csharp
    static void Main(string[] args)
    {
        var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR_SUBSCRIPTION_KEY"));

        WebResults(client);
        // Search with count and offset...
        WebResultsWithCountAndOffset(client);  
        // Search with news filter...
        WebSearchWithResponseFilter(client);

        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
    ```
3. <span data-ttu-id="09176-154">Run the application.</span><span class="sxs-lookup"><span data-stu-id="09176-154">Run the application.</span></span>

### <a name="use-safe-search-answer-count-and-the-promote-filter"></a><span data-ttu-id="09176-155">Use safe search, answer count, and the promote filter</span><span class="sxs-lookup"><span data-stu-id="09176-155">Use safe search, answer count, and the promote filter</span></span>

<span data-ttu-id="09176-156">This sample uses the `answer_count`, `promote`, and `safe_search` parameters to filter search results for "Music Videos".</span><span class="sxs-lookup"><span data-stu-id="09176-156">This sample uses the `answer_count`, `promote`, and `safe_search` parameters to filter search results for "Music Videos".</span></span> <span data-ttu-id="09176-157">The `name` and `URL` for the first result are displayed.</span><span class="sxs-lookup"><span data-stu-id="09176-157">The `name` and `URL` for the first result are displayed.</span></span>

1. <span data-ttu-id="09176-158">Add this code to your console project:</span><span class="sxs-lookup"><span data-stu-id="09176-158">Add this code to your console project:</span></span>
    ```csharp
    public static void WebSearchWithAnswerCountPromoteAndSafeSearch(WebSearchAPI client)
    {
        try
        {
            IList<string> promoteAnswertypeStrings = new List<string>() { "videos" };
            var webData = client.Web.SearchAsync(query: "Music Videos", answerCount: 2, promote: promoteAnswertypeStrings, safeSearch: SafeSearch.Strict).Result;
            Console.WriteLine("\r\nSearching for \"Music Videos\"");

            if (webData?.Videos?.Value?.Count > 0)
            {
                var firstVideosResult = webData.Videos.Value.FirstOrDefault();

                if (firstVideosResult != null)
                {
                    Console.WriteLine("Video Results # {0}", webData.Videos.Value.Count);
                    Console.WriteLine("First Video result name: {0} ", firstVideosResult.Name);
                    Console.WriteLine("First Video result URL: {0} ", firstVideosResult.ContentUrl);
                }
                else
                {
                    Console.WriteLine("Couldn't find videos results!");
                }
            }
            else
            {
                Console.WriteLine("Didn't see any data..");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("Encountered exception. " + ex.Message);
        }
    }
    ```
2. <span data-ttu-id="09176-159">Add `WebResultsWithCountAndOffset` to `main`:</span><span class="sxs-lookup"><span data-stu-id="09176-159">Add `WebResultsWithCountAndOffset` to `main`:</span></span>
    ```csharp
    static void Main(string[] args)
    {
        var client = new WebSearchAPI(new ApiKeyServiceClientCredentials("YOUR_SUBSCRIPTION_KEY"));

        WebResults(client);
        // Search with count and offset...
        WebResultsWithCountAndOffset(client);  
        // Search with news filter...
        WebSearchWithResponseFilter(client);
        // Search with answer count, promote, and safe search
        WebSearchWithAnswerCountPromoteAndSafeSearch(client);

        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
    ```
3. <span data-ttu-id="09176-160">Run the application.</span><span class="sxs-lookup"><span data-stu-id="09176-160">Run the application.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="09176-161">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="09176-161">Clean up resources</span></span>

<span data-ttu-id="09176-162">When you're done with this project, make sure to remove your subscription key from the application's code.</span><span class="sxs-lookup"><span data-stu-id="09176-162">When you're done with this project, make sure to remove your subscription key from the application's code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09176-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="09176-163">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09176-164">Cognitive Services Node.js SDK samples</span><span class="sxs-lookup"><span data-stu-id="09176-164">Cognitive Services Node.js SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/)
