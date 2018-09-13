---
title: 'Quickstart: Use C# to call the Bing Web Search API'
description: In this quickstart, you will learn how to make your first call to the Bing Web Search API using C# and receive a JSON response.
services: cognitive-services
author: erhopf
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 8/16/2018
ms.author: erhopf
ms.openlocfilehash: 9db551f89a3b7834119fe85a22e4cdc8d0402252
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856743"
---
# <a name="quickstart-use-c-to-call-the-bing-web-search-api"></a><span data-ttu-id="430ff-103">Quickstart: Use C# to call the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="430ff-103">Quickstart: Use C# to call the Bing Web Search API</span></span>  

<span data-ttu-id="430ff-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response.</span><span class="sxs-lookup"><span data-stu-id="430ff-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response.</span></span>  

[!INCLUDE [bing-web-search-quickstart-signup](../../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a><span data-ttu-id="430ff-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="430ff-105">Prerequisites</span></span>

<span data-ttu-id="430ff-106">Here are a few things that you'll need before running this quickstart:</span><span class="sxs-lookup"><span data-stu-id="430ff-106">Here are a few things that you'll need before running this quickstart:</span></span>

* <span data-ttu-id="430ff-107">Windows: [Visual Studio 2017](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="430ff-107">Windows: [Visual Studio 2017](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="430ff-108">Linux/macOS: [Mono](http://www.mono-project.com/)</span><span class="sxs-lookup"><span data-stu-id="430ff-108">Linux/macOS: [Mono](http://www.mono-project.com/)</span></span>  
* <span data-ttu-id="430ff-109">A subscription key</span><span class="sxs-lookup"><span data-stu-id="430ff-109">A subscription key</span></span>

<span data-ttu-id="430ff-110">This example program only uses .NET Core classes.</span><span class="sxs-lookup"><span data-stu-id="430ff-110">This example program only uses .NET Core classes.</span></span>

## <a name="create-a-project-and-declare-dependencies"></a><span data-ttu-id="430ff-111">Create a project and declare dependencies</span><span class="sxs-lookup"><span data-stu-id="430ff-111">Create a project and declare dependencies</span></span>

<span data-ttu-id="430ff-112">Create a new project in Visual Studio or Mono.</span><span class="sxs-lookup"><span data-stu-id="430ff-112">Create a new project in Visual Studio or Mono.</span></span> <span data-ttu-id="430ff-113">Then use this code to import required namespaces and types.</span><span class="sxs-lookup"><span data-stu-id="430ff-113">Then use this code to import required namespaces and types.</span></span>

```csharp
using System;
using System.Text;
using System.Net;
using System.IO;
using System.Collections.Generic;
```

## <a name="declare-a-namespace-and-class-for-your-program"></a><span data-ttu-id="430ff-114">Declare a namespace and class for your program</span><span class="sxs-lookup"><span data-stu-id="430ff-114">Declare a namespace and class for your program</span></span>

<span data-ttu-id="430ff-115">In this quickstart, we'll put most of the code in the `Program` class.</span><span class="sxs-lookup"><span data-stu-id="430ff-115">In this quickstart, we'll put most of the code in the `Program` class.</span></span> <span data-ttu-id="430ff-116">Start by creating the `BingSearchApiQuickstart` namespace and `Program` class in your project.</span><span class="sxs-lookup"><span data-stu-id="430ff-116">Start by creating the `BingSearchApiQuickstart` namespace and `Program` class in your project.</span></span>  

```csharp
namespace BingSearchApisQuickstart
{
    class Program
    {
        // The code in the following sections goes here.
    }
}
```

## <a name="define-variables"></a><span data-ttu-id="430ff-117">Define variables</span><span class="sxs-lookup"><span data-stu-id="430ff-117">Define variables</span></span>

<span data-ttu-id="430ff-118">A few variables must be set before we can continue.</span><span class="sxs-lookup"><span data-stu-id="430ff-118">A few variables must be set before we can continue.</span></span> <span data-ttu-id="430ff-119">Confirm that the `uriBase` is valid and replace the `accessKey` value with a valid subscription key from your Azure account.</span><span class="sxs-lookup"><span data-stu-id="430ff-119">Confirm that the `uriBase` is valid and replace the `accessKey` value with a valid subscription key from your Azure account.</span></span> <span data-ttu-id="430ff-120">Feel free to customize the search query by replacing the value for `searchTerm`.</span><span class="sxs-lookup"><span data-stu-id="430ff-120">Feel free to customize the search query by replacing the value for `searchTerm`.</span></span>

```csharp
// Enter a valid subscription key.
const string accessKey = "enter key here";
/*
 * If you encounter unexpected authorization errors, double-check this value
 * against the endpoint for your Bing Web search instance in your Azure
 * dashboard.
 */
const string uriBase = "https://api.cognitive.microsoft.com/bing/v7.0/search";
const string searchTerm = "Microsoft Cognitive Services";
```

## <a name="declare-the-main-method"></a><span data-ttu-id="430ff-121">Declare the Main method</span><span class="sxs-lookup"><span data-stu-id="430ff-121">Declare the Main method</span></span>

<span data-ttu-id="430ff-122">The `Main()` is required and it's the first method invoked when the program is started.</span><span class="sxs-lookup"><span data-stu-id="430ff-122">The `Main()` is required and it's the first method invoked when the program is started.</span></span> <span data-ttu-id="430ff-123">In this application, the main method  validates the `accessKey`, makes a request, and prints the response.</span><span class="sxs-lookup"><span data-stu-id="430ff-123">In this application, the main method  validates the `accessKey`, makes a request, and prints the response.</span></span>

<span data-ttu-id="430ff-124">Keep in mind that `main()` is dependent on methods that are created in the next few sections.</span><span class="sxs-lookup"><span data-stu-id="430ff-124">Keep in mind that `main()` is dependent on methods that are created in the next few sections.</span></span>

```csharp
static void Main()
{
    Console.OutputEncoding = System.Text.Encoding.UTF8;
    if (accessKey.Length == 32)
    {
        Console.WriteLine("Searching the Web for: " + searchTerm);
        SearchResult result = BingWebSearch(searchTerm);
        Console.WriteLine("\nRelevant HTTP Headers:\n");
        foreach (var header in result.relevantHeaders)
            Console.WriteLine(header.Key + ": " + header.Value);

        Console.WriteLine("\nJSON Response:\n");
        Console.WriteLine(JsonPrettyPrint(result.jsonResult));
    }
    else
    {
        Console.WriteLine("Invalid Bing Search API subscription key!");
        Console.WriteLine("Please paste yours into the source code.");
    }
    Console.Write("\nPress Enter to exit ");
    Console.ReadLine();
}
```

## <a name="create-a-struct-for-search-results"></a><span data-ttu-id="430ff-125">Create a struct for search results</span><span class="sxs-lookup"><span data-stu-id="430ff-125">Create a struct for search results</span></span>

<span data-ttu-id="430ff-126">This struct returns search results with relevant headers.</span><span class="sxs-lookup"><span data-stu-id="430ff-126">This struct returns search results with relevant headers.</span></span> <span data-ttu-id="430ff-127">It is called when making a request to the Bing Web Search API to create a result object.</span><span class="sxs-lookup"><span data-stu-id="430ff-127">It is called when making a request to the Bing Web Search API to create a result object.</span></span>

```csharp
// Returns search results with headers.
struct SearchResult
{
    public String jsonResult;
    public Dictionary<String, String> relevantHeaders;
}
```

## <a name="construct-a-request"></a><span data-ttu-id="430ff-128">Construct a request</span><span class="sxs-lookup"><span data-stu-id="430ff-128">Construct a request</span></span>

<span data-ttu-id="430ff-129">Use this code to construct the search query, perform the GET request, and handle the response.</span><span class="sxs-lookup"><span data-stu-id="430ff-129">Use this code to construct the search query, perform the GET request, and handle the response.</span></span>

```csharp
/// <summary>
/// Makes a request to the Bing Web Search API and returns data as a SearchResult.
/// </summary>
static SearchResult BingWebSearch(string searchQuery)
{
    // Construct the search request URI.
    var uriQuery = uriBase + "?q=" + Uri.EscapeDataString(searchQuery);

    // Perform request and get a response.
    WebRequest request = HttpWebRequest.Create(uriQuery);
    request.Headers["Ocp-Apim-Subscription-Key"] = accessKey;
    HttpWebResponse response = (HttpWebResponse)request.GetResponseAsync().Result;
    string json = new StreamReader(response.GetResponseStream()).ReadToEnd();

    // Create a result object.
    var searchResult = new SearchResult()
    {
        jsonResult = json,
        relevantHeaders = new Dictionary<String, String>()
    };

    // Extract Bing HTTP headers.
    foreach (String header in response.Headers)
    {
        if (header.StartsWith("BingAPIs-") || header.StartsWith("X-MSEdge-"))
            searchResult.relevantHeaders[header] = response.Headers[header];
    }
    return searchResult;
}
```

## <a name="format-the-response"></a><span data-ttu-id="430ff-130">Format the response</span><span class="sxs-lookup"><span data-stu-id="430ff-130">Format the response</span></span>

<span data-ttu-id="430ff-131">This method formats the JSON response, primarily indenting and adding line breaks.</span><span class="sxs-lookup"><span data-stu-id="430ff-131">This method formats the JSON response, primarily indenting and adding line breaks.</span></span>

```csharp
/// <summary>
/// Formats the JSON string by adding line breaks and indents.
/// </summary>
/// <param name="json">The raw JSON string.</param>
/// <returns>The formatted JSON string.</returns>
static string JsonPrettyPrint(string json)
{
    if (string.IsNullOrEmpty(json))
        return string.Empty;

    json = json.Replace(Environment.NewLine, "").Replace("\t", "");

    StringBuilder sb = new StringBuilder();
    bool quote = false;
    bool ignore = false;
    char last = ' ';
    int offset = 0;
    int indentLength = 2;

    foreach (char ch in json)
    {
        switch (ch)
        {
            case '"':
                if (!ignore) quote = !quote;
                break;
            case '\\':
                if (quote && last != '\\') ignore = true;
                break;
        }

        if (quote)
        {
            sb.Append(ch);
            if (last == '\\' && ignore) ignore = false;
        }
        else
        {
            switch (ch)
            {
                case '{':
                    case '[':
                        sb.Append(ch);
                        sb.Append(Environment.NewLine);
                        sb.Append(new string(' ', ++offset * indentLength));
                        break;
                    case ']':
                    case '}':
                        sb.Append(Environment.NewLine);
                        sb.Append(new string(' ', --offset * indentLength));
                        sb.Append(ch);
                        break;
                    case ',':
                        sb.Append(ch);
                        sb.Append(Environment.NewLine);
                        sb.Append(new string(' ', offset * indentLength));
                        break;
                    case ':':
                        sb.Append(ch);
                        sb.Append(' ');
                        break;
                    default:
                        if (quote || ch != ' ') sb.Append(ch);
                        break;
            }
        }
        last = ch;
    }
    return sb.ToString().Trim();
}
```

## <a name="put-it-all-together"></a><span data-ttu-id="430ff-132">Put it all together</span><span class="sxs-lookup"><span data-stu-id="430ff-132">Put it all together</span></span>

<span data-ttu-id="430ff-133">The last step is to run your code!</span><span class="sxs-lookup"><span data-stu-id="430ff-133">The last step is to run your code!</span></span> <span data-ttu-id="430ff-134">If you'd like to compare your code with ours, [sample code is available on GitHub](https://github.com/Azure-Samples/cognitive-services-REST-api-samples/blob/master/dotnet/Search/BingWebSearchv7.cs).</span><span class="sxs-lookup"><span data-stu-id="430ff-134">If you'd like to compare your code with ours, [sample code is available on GitHub](https://github.com/Azure-Samples/cognitive-services-REST-api-samples/blob/master/dotnet/Search/BingWebSearchv7.cs).</span></span>

## <a name="sample-response"></a><span data-ttu-id="430ff-135">Sample response</span><span class="sxs-lookup"><span data-stu-id="430ff-135">Sample response</span></span>

<span data-ttu-id="430ff-136">Responses from the Bing Web Search API are returned as JSON.</span><span class="sxs-lookup"><span data-stu-id="430ff-136">Responses from the Bing Web Search API are returned as JSON.</span></span> <span data-ttu-id="430ff-137">This sample response has been truncated to show a single result.</span><span class="sxs-lookup"><span data-stu-id="430ff-137">This sample response has been truncated to show a single result.</span></span>  

```json
{
  "_type": "SearchResponse",
  "queryContext": {
    "originalQuery": "Microsoft Cognitive Services"
  },
  "webPages": {
    "webSearchUrl": "https://www.bing.com/search?q=Microsoft+cognitive+services",
    "totalEstimatedMatches": 22300000,
    "value": [
      {
        "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.0",
        "name": "Microsoft Cognitive Services",
        "url": "https://www.microsoft.com/cognitive-services",
        "displayUrl": "https://www.microsoft.com/cognitive-services",
        "snippet": "Knock down barriers between you and your ideas. Enable natural and contextual interaction with tools that augment users' experiences via the power of machine-based AI. Plug them in and bring your ideas to life.",
        "deepLinks": [
          {
            "name": "Face API",
            "url": "https://azure.microsoft.com/services/cognitive-services/face/",
            "snippet": "Add facial recognition to your applications to detect, identify, and verify faces using a Face API from Microsoft Azure. ... Cognitive Services; Face API;"
          },
          {
            "name": "Text Analytics",
            "url": "https://azure.microsoft.com/services/cognitive-services/text-analytics/",
            "snippet": "Cognitive Services; Text Analytics API; Text Analytics API . Detect sentiment, ... you agree that Microsoft may store it and use it to improve Microsoft services, ..."
          },
          {
            "name": "Computer Vision API",
            "url": "https://azure.microsoft.com/services/cognitive-services/computer-vision/",
            "snippet": "Extract the data you need from images using optical character recognition and image analytics with Computer Vision APIs from Microsoft Azure."
          },
          {
            "name": "Emotion",
            "url": "https://www.microsoft.com/cognitive-services/en-us/emotion-api",
            "snippet": "Cognitive Services Emotion API - microsoft.com"
          },
          {
            "name": "Bing Speech API",
            "url": "https://azure.microsoft.com/services/cognitive-services/speech/",
            "snippet": "Add speech recognition to your applications, including text to speech, with a speech API from Microsoft Azure. ... Cognitive Services; Bing Speech API;"
          },
          {
            "name": "Get Started for Free",
            "url": "https://azure.microsoft.com/services/cognitive-services/",
            "snippet": "Add vision, speech, language, and knowledge capabilities to your applications using intelligence APIs and SDKs from Cognitive Services."
          }
        ]
      }
    ]
  },
  "relatedSearches": {
    "id": "https://api.cognitive.microsoft.com/api/v7/#RelatedSearches",
    "value": [
      {
        "text": "microsoft bot framework",
        "displayText": "microsoft bot framework",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+bot+framework"
      },
      {
        "text": "microsoft cognitive services youtube",
        "displayText": "microsoft cognitive services youtube",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+youtube"
      },
      {
        "text": "microsoft cognitive services search api",
        "displayText": "microsoft cognitive services search api",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+search+api"
      },
      {
        "text": "microsoft cognitive services news",
        "displayText": "microsoft cognitive services news",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+news"
      },
      {
        "text": "ms cognitive service",
        "displayText": "ms cognitive service",
        "webSearchUrl": "https://www.bing.com/search?q=ms+cognitive+service"
      },
      {
        "text": "microsoft cognitive services text analytics",
        "displayText": "microsoft cognitive services text analytics",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+text+analytics"
      },
      {
        "text": "microsoft cognitive services toolkit",
        "displayText": "microsoft cognitive services toolkit",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+toolkit"
      },
      {
        "text": "microsoft cognitive services api",
        "displayText": "microsoft cognitive services api",
        "webSearchUrl": "https://www.bing.com/search?q=microsoft+cognitive+services+api"
      }
    ]
  },
  "rankingResponse": {
    "mainline": {
      "items": [
        {
          "answerType": "WebPages",
          "resultIndex": 0,
          "value": {
            "id": "https://api.cognitive.microsoft.com/api/v7/#WebPages.0"
          }
        }
      ]
    },
    "sidebar": {
      "items": [
        {
          "answerType": "RelatedSearches",
          "value": {
            "id": "https://api.cognitive.microsoft.com/api/v7/#RelatedSearches"
          }
        }
      ]
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="430ff-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="430ff-138">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="430ff-139">Bing Web search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="430ff-139">Bing Web search single-page app tutorial</span></span>](../tutorial-bing-web-search-single-page-app.md)

[!INCLUDE [bing-web-search-quickstart-see-also](../../../../includes/bing-web-search-quickstart-see-also.md)]
