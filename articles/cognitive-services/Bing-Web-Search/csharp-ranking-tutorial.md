---
title: Using rank to display search results | Microsoft Docs
description: Shows how to use the Bing RankingResponse answer to display search results in rank order.
services: cognitive-services
author: bradumbaugh
manager: bking
ms.assetid: 2575A80C-FC74-4631-AE5D-8101CF2591D3
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 05/08/2017
ms.author: brumbaug
ms.openlocfilehash: 0dd3a2057e73adda3224e7cebe7c492572f94105
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864360"
---
# <a name="build-a-console-app-search-client-in-c"></a><span data-ttu-id="f0b7e-103">Build a console app search client in C#</span><span class="sxs-lookup"><span data-stu-id="f0b7e-103">Build a console app search client in C#</span></span>

<span data-ttu-id="f0b7e-104">This tutorial shows how to build a simple .NET Core console app that allows users to query the Bing Web Search API and display ranked results.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-104">This tutorial shows how to build a simple .NET Core console app that allows users to query the Bing Web Search API and display ranked results.</span></span>

<span data-ttu-id="f0b7e-105">This tutorial shows how to:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-105">This tutorial shows how to:</span></span>

- <span data-ttu-id="f0b7e-106">Make a simple query to the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="f0b7e-106">Make a simple query to the Bing Web Search API</span></span>
- <span data-ttu-id="f0b7e-107">Display query results in ranked order</span><span class="sxs-lookup"><span data-stu-id="f0b7e-107">Display query results in ranked order</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0b7e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f0b7e-108">Prerequisites</span></span>

<span data-ttu-id="f0b7e-109">To follow along with the tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-109">To follow along with the tutorial, you need:</span></span>

- <span data-ttu-id="f0b7e-110">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-110">Visual Studio.</span></span> <span data-ttu-id="f0b7e-111">If you don't have it, [download and install the free Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f0b7e-111">If you don't have it, [download and install the free Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="f0b7e-112">A subscription key for the Bing Web Search API.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-112">A subscription key for the Bing Web Search API.</span></span> <span data-ttu-id="f0b7e-113">If you don't have one, [sign up for a free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api).</span><span class="sxs-lookup"><span data-stu-id="f0b7e-113">If you don't have one, [sign up for a free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api).</span></span>

## <a name="create-a-new-console-app-project"></a><span data-ttu-id="f0b7e-114">Create a new Console App project</span><span class="sxs-lookup"><span data-stu-id="f0b7e-114">Create a new Console App project</span></span>

<span data-ttu-id="f0b7e-115">In Visual Studio, create a project with `Ctrl`+`Shift`+`N`.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-115">In Visual Studio, create a project with `Ctrl`+`Shift`+`N`.</span></span>

<span data-ttu-id="f0b7e-116">In the **New Project** dialog, click **Visual C# > Windows Classic Desktop > Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-116">In the **New Project** dialog, click **Visual C# > Windows Classic Desktop > Console App (.NET Framework)**.</span></span>

<span data-ttu-id="f0b7e-117">Name the application **MyConsoleSearchApp**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-117">Name the application **MyConsoleSearchApp**, and then click **OK**.</span></span>

## <a name="add-the-jsonnet-nuget-package-to-the-project"></a><span data-ttu-id="f0b7e-118">Add the JSON.net Nuget package to the project</span><span class="sxs-lookup"><span data-stu-id="f0b7e-118">Add the JSON.net Nuget package to the project</span></span>

<span data-ttu-id="f0b7e-119">JSON.net allows you to work with the JSON responses returned by the API.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-119">JSON.net allows you to work with the JSON responses returned by the API.</span></span> <span data-ttu-id="f0b7e-120">Add its NuGet package to your project:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-120">Add its NuGet package to your project:</span></span>

- <span data-ttu-id="f0b7e-121">In **Solution Explorer** right-click on the project and select **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-121">In **Solution Explorer** right-click on the project and select **Manage NuGet Packages...**.</span></span> 
- <span data-ttu-id="f0b7e-122">On the  **Browse** tab, search for `Newtonsoft.Json`.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-122">On the  **Browse** tab, search for `Newtonsoft.Json`.</span></span> <span data-ttu-id="f0b7e-123">Select the latest version, and then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-123">Select the latest version, and then click **Install**.</span></span> 
- <span data-ttu-id="f0b7e-124">Click the **OK** button on the **Review Changes** window.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-124">Click the **OK** button on the **Review Changes** window.</span></span>
- <span data-ttu-id="f0b7e-125">Close the Visual Studio tab titled **NuGet: MyConsoleSearchApp**.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-125">Close the Visual Studio tab titled **NuGet: MyConsoleSearchApp**.</span></span>

## <a name="add-a-reference-to-systemweb"></a><span data-ttu-id="f0b7e-126">Add a reference to System.Web</span><span class="sxs-lookup"><span data-stu-id="f0b7e-126">Add a reference to System.Web</span></span>

<span data-ttu-id="f0b7e-127">This tutorial relies on the `System.Web` assembly.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-127">This tutorial relies on the `System.Web` assembly.</span></span> <span data-ttu-id="f0b7e-128">Add a reference to this assembly to your project:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-128">Add a reference to this assembly to your project:</span></span>

- <span data-ttu-id="f0b7e-129">In **Solution Explorer**, right-click on **References** and select **Add Reference...**</span><span class="sxs-lookup"><span data-stu-id="f0b7e-129">In **Solution Explorer**, right-click on **References** and select **Add Reference...**</span></span>
- <span data-ttu-id="f0b7e-130">Select **Assemblies > Framework**, then scroll down and check **System.Web**</span><span class="sxs-lookup"><span data-stu-id="f0b7e-130">Select **Assemblies > Framework**, then scroll down and check **System.Web**</span></span>
- <span data-ttu-id="f0b7e-131">Select **OK**</span><span class="sxs-lookup"><span data-stu-id="f0b7e-131">Select **OK**</span></span>

## <a name="add-some-necessary-using-statements"></a><span data-ttu-id="f0b7e-132">Add some necessary using statements</span><span class="sxs-lookup"><span data-stu-id="f0b7e-132">Add some necessary using statements</span></span>

<span data-ttu-id="f0b7e-133">The code in this tutorial requires three additional using statements.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-133">The code in this tutorial requires three additional using statements.</span></span> <span data-ttu-id="f0b7e-134">Add these statements below the existing `using` statements at the top of **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-134">Add these statements below the existing `using` statements at the top of **Program.cs**:</span></span> 

```csharp
using System.Web;
using System.Net.Http;
```

## <a name="ask-the-user-for-a-query"></a><span data-ttu-id="f0b7e-135">Ask the user for a query</span><span class="sxs-lookup"><span data-stu-id="f0b7e-135">Ask the user for a query</span></span>

<span data-ttu-id="f0b7e-136">In **Solution Explorer**, open **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-136">In **Solution Explorer**, open **Program.cs**.</span></span> <span data-ttu-id="f0b7e-137">Update the `Main()` method:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-137">Update the `Main()` method:</span></span>

```csharp
static void Main()
{
    // Get the user's query
    Console.Write("Enter Bing query: ");
    string userQuery = Console.ReadLine();
    Console.WriteLine();

    // Run the query and display the results
    RunQueryAndDisplayResults(userQuery);

    // Prevent the console window from closing immediately
    Console.WriteLine("\nHit ENTER to exit...");
    Console.ReadLine();
}
```

<span data-ttu-id="f0b7e-138">This method:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-138">This method:</span></span>

- <span data-ttu-id="f0b7e-139">Asks the user for a query</span><span class="sxs-lookup"><span data-stu-id="f0b7e-139">Asks the user for a query</span></span>
- <span data-ttu-id="f0b7e-140">Calls `RunQueryAndDisplayResults(userQuery)` to execute the query and display the results</span><span class="sxs-lookup"><span data-stu-id="f0b7e-140">Calls `RunQueryAndDisplayResults(userQuery)` to execute the query and display the results</span></span>
- <span data-ttu-id="f0b7e-141">Waits for user input in order to prevent the console window from immediately closing.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-141">Waits for user input in order to prevent the console window from immediately closing.</span></span>

## <a name="search-for-query-results-using-the-bing-web-search-api"></a><span data-ttu-id="f0b7e-142">Search for query results using the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="f0b7e-142">Search for query results using the Bing Web Search API</span></span>

<span data-ttu-id="f0b7e-143">Next, add a method that queries the API and displays the results:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-143">Next, add a method that queries the API and displays the results:</span></span>

```csharp
static void RunQueryAndDisplayResults(string userQuery)
{
    try
    {
        // Create a query
        var client = new HttpClient();
        client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "<YOUR_SUBSCRIPTION_KEY_GOES_HERE>");
        var queryString = HttpUtility.ParseQueryString(string.Empty);
        queryString["q"] = userQuery;
        var query = "https://api.cognitive.microsoft.com/bing/v7.0/search?" + queryString;

        // Run the query
        HttpResponseMessage httpResponseMessage = client.GetAsync(query).Result;

        // Deserialize the response content
        var responseContentString = httpResponseMessage.Content.ReadAsStringAsync().Result;
        Newtonsoft.Json.Linq.JObject responseObjects = Newtonsoft.Json.Linq.JObject.Parse(responseContentString);

        // Handle success and error codes
        if (httpResponseMessage.IsSuccessStatusCode)
        {
            DisplayAllRankedResults(responseObjects);
        }
        else
        {
            Console.WriteLine($"HTTP error status code: {httpResponseMessage.StatusCode.ToString()}");
        }
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }
}
```

<span data-ttu-id="f0b7e-144">This method:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-144">This method:</span></span>

- <span data-ttu-id="f0b7e-145">Creates an `HttpClient` to query the Web Search API</span><span class="sxs-lookup"><span data-stu-id="f0b7e-145">Creates an `HttpClient` to query the Web Search API</span></span>
- <span data-ttu-id="f0b7e-146">Sets the `Ocp-Apim-Subscription-Key` HTTP header, which Bing uses to authenticate the request</span><span class="sxs-lookup"><span data-stu-id="f0b7e-146">Sets the `Ocp-Apim-Subscription-Key` HTTP header, which Bing uses to authenticate the request</span></span>
- <span data-ttu-id="f0b7e-147">Executes the request and uses JSON.net to deserialize the results</span><span class="sxs-lookup"><span data-stu-id="f0b7e-147">Executes the request and uses JSON.net to deserialize the results</span></span>
- <span data-ttu-id="f0b7e-148">Calls `DisplayAllRankedResults(responseObjects)` to display all results in ranked order</span><span class="sxs-lookup"><span data-stu-id="f0b7e-148">Calls `DisplayAllRankedResults(responseObjects)` to display all results in ranked order</span></span>

<span data-ttu-id="f0b7e-149">Make sure to set the value of `Ocp-Apim-Subscription-Key` to your subscription key.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-149">Make sure to set the value of `Ocp-Apim-Subscription-Key` to your subscription key.</span></span>

## <a name="display-ranked-results"></a><span data-ttu-id="f0b7e-150">Display ranked results</span><span class="sxs-lookup"><span data-stu-id="f0b7e-150">Display ranked results</span></span>

<span data-ttu-id="f0b7e-151">Before showing how to display the results in ranked order, take a look at a sample web search response:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-151">Before showing how to display the results in ranked order, take a look at a sample web search response:</span></span> 

```json
{
    "_type" : "SearchResponse",
    "webPages" : {
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346...",
        "totalEstimatedMatches" : 982000,
        "value" : [{
            "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.0",
            "name" : "Contoso Sailing Club - Seattle",
            "url" : "https:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FE...",
            "displayUrl" : "https:\/\/contososailingsea...",
            "snippet" : "Come sail with Contoso in Seattle...",
            "dateLastCrawled" : "2017-04-07T02:25:00"
        },
        {
            "id" : "https:\/\/api.cognitive.microsoft.com\/api\/7\/#WebPages.6",
            "name" : "Contoso Sailing Lessons - Official Site",
            "url" : "http:\/\/www.bing.com\/cr?IG=70BE289346ED4594874FE...",
            "displayUrl" : "https:\/\/www.constososailinglessonsseat...",
            "snippet" : "Contoso sailing lessons in Seattle...",
            "dateLastCrawled" : "2017-04-09T14:30:00"
        },

        ...
        
        ],
        "someResultsRemoved" : true
    },
    "relatedSearches" : {
        "id" : "https:\/\/api.cognitive.microsoft.com\/api\/7\/#RelatedSearches",
        "value" : [{
            "text" : "sailing lessons",
            "displayText" : "sailing lessons",
            "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=70BE289346E..."
        }

        ...
        
        ]
    },
    "rankingResponse" : {
        "mainline" : {
            "items" : [{
                "answerType" : "WebPages",
                "resultIndex" : 0,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.0"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 1,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.1"
                }
            }

            ...

            ]
        },
        "sidebar" : {
            "items" : [{
                "answerType" : "RelatedSearches",
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#RelatedSearches"
                }
            }]
        }
    }
}
```

<span data-ttu-id="f0b7e-152">The `rankingResponse` JSON object ([documentation](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse)) describes the appropriate display order for search results.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-152">The `rankingResponse` JSON object ([documentation](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse)) describes the appropriate display order for search results.</span></span> <span data-ttu-id="f0b7e-153">It includes one or more of the following, prioritized groups:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-153">It includes one or more of the following, prioritized groups:</span></span> 

- <span data-ttu-id="f0b7e-154">`pole`: The search results to get the most visible treatment (for example, displayed above the mainline and sidebar).</span><span class="sxs-lookup"><span data-stu-id="f0b7e-154">`pole`: The search results to get the most visible treatment (for example, displayed above the mainline and sidebar).</span></span>
- <span data-ttu-id="f0b7e-155">`mainline`: The search results to display in the mainline.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-155">`mainline`: The search results to display in the mainline.</span></span>
- <span data-ttu-id="f0b7e-156">`sidebar`: The search results to display in the sidebar.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-156">`sidebar`: The search results to display in the sidebar.</span></span> <span data-ttu-id="f0b7e-157">If there is no sidebar, display the results below the mainline.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-157">If there is no sidebar, display the results below the mainline.</span></span>

<span data-ttu-id="f0b7e-158">The ranking response JSON may include one or more of the groups.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-158">The ranking response JSON may include one or more of the groups.</span></span>

<span data-ttu-id="f0b7e-159">In **Program.cs**, add the following method to display results in properly ranked order:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-159">In **Program.cs**, add the following method to display results in properly ranked order:</span></span>

```csharp
static void DisplayAllRankedResults(Newtonsoft.Json.Linq.JObject responseObjects)
{
    string[] rankingGroups = new string[] { "pole", "mainline", "sidebar" };

    // Loop through the ranking groups in priority order
    foreach (string rankingName in rankingGroups)
    {
        Newtonsoft.Json.Linq.JToken rankingResponseItems = responseObjects.SelectToken($"rankingResponse.{rankingName}.items");
        if (rankingResponseItems != null)
        {
            foreach (Newtonsoft.Json.Linq.JObject rankingResponseItem in rankingResponseItems)
            {
                Newtonsoft.Json.Linq.JToken resultIndex;
                rankingResponseItem.TryGetValue("resultIndex", out resultIndex);
                var answerType = rankingResponseItem.Value<string>("answerType");
                switch (answerType)
                {
                    case "WebPages":
                        DisplaySpecificResults(resultIndex, responseObjects.SelectToken("webPages.value"), "WebPage", "name", "url", "displayUrl", "snippet");
                        break;
                    case "News":
                        DisplaySpecificResults(resultIndex, responseObjects.SelectToken("news.value"), "News", "name", "url", "description");
                        break;
                    case "Images":
                        DisplaySpecificResults(resultIndex, responseObjects.SelectToken("images.value"), "Image", "thumbnailUrl");
                        break;
                    case "Videos":
                        DisplaySpecificResults(resultIndex, responseObjects.SelectToken("videos.value"), "Video", "embedHtml");
                        break;
                    case "RelatedSearches":
                        DisplaySpecificResults(resultIndex, responseObjects.SelectToken("relatedSearches.value"), "RelatedSearch", "displayText", "webSearchUrl");
                        break;
                }
            }
        }
    }
}
```

<span data-ttu-id="f0b7e-160">This method:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-160">This method:</span></span>

- <span data-ttu-id="f0b7e-161">Loops over the `rankingResponse` groups that the response contains</span><span class="sxs-lookup"><span data-stu-id="f0b7e-161">Loops over the `rankingResponse` groups that the response contains</span></span>
- <span data-ttu-id="f0b7e-162">Displays the items in each group by calling `DisplaySpecificResults(...)`</span><span class="sxs-lookup"><span data-stu-id="f0b7e-162">Displays the items in each group by calling `DisplaySpecificResults(...)`</span></span> 

<span data-ttu-id="f0b7e-163">In **Program.cs**, add the following two methods:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-163">In **Program.cs**, add the following two methods:</span></span>

```csharp
static void DisplaySpecificResults(Newtonsoft.Json.Linq.JToken resultIndex, Newtonsoft.Json.Linq.JToken items, string title, params string[] fields)
{
    if (resultIndex == null)
    {
        foreach (Newtonsoft.Json.Linq.JToken item in items)
        {
            DisplayItem(item, title, fields);
        }
    }
    else
    {
        DisplayItem(items.ElementAt((int)resultIndex), title, fields);
    }
}

static void DisplayItem(Newtonsoft.Json.Linq.JToken item, string title, string[] fields)
{
    Console.WriteLine($"{title}: ");
    foreach( string field in fields )
    {
        Console.WriteLine($"- {field}: {item[field]}");
    }
    Console.WriteLine();
}
```

<span data-ttu-id="f0b7e-164">These methods work together to output the search results to the console.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-164">These methods work together to output the search results to the console.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="f0b7e-165">Run the application</span><span class="sxs-lookup"><span data-stu-id="f0b7e-165">Run the application</span></span>

<span data-ttu-id="f0b7e-166">Run the application.</span><span class="sxs-lookup"><span data-stu-id="f0b7e-166">Run the application.</span></span> <span data-ttu-id="f0b7e-167">The output should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f0b7e-167">The output should look similar to the following:</span></span>

```
Enter Bing query: sailing lessons seattle

WebPage:
- name: Contoso Sailing Club - Seattle
- url: https://www.bing.com/cr?IG=70BE289346ED4594874FE...
- displayUrl: https://contososailingsea....
- snippet: Come sail with Contoso in Seattle...

WebPage:
- name: Contoso Sailing Lessons Seattle - Official Site
- url: http://www.bing.com/cr?IG=70BE289346ED4594874FE...
- displayUrl: https://www.constososailinglessonsseat...
- snippet: Contoso sailing lessons in Seattle...

...
```

## <a name="next-steps"></a><span data-ttu-id="f0b7e-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="f0b7e-168">Next steps</span></span>

<span data-ttu-id="f0b7e-169">Read more about [using ranking to display results](rank-results.md).</span><span class="sxs-lookup"><span data-stu-id="f0b7e-169">Read more about [using ranking to display results](rank-results.md).</span></span>
