---
title: 'Quickstart: Send search queries using the REST API for the Bing Image Search API using C#'
description: In this quickstart, you send search queries to the Bing Search API to get a list of relevant images using C#.
services: cognitive-services
documentationcenter: ''
author: aahill
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 8/9/2018
ms.author: aahi
ms.openlocfilehash: 7a5ef36f02d82ee17698af9c647f043792280fbc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857573"
---
# <a name="quickstart-send-search-queries-using-the-rest-api-and-c"></a><span data-ttu-id="d340e-103">Quickstart: Send search queries using the REST API and C#</span><span class="sxs-lookup"><span data-stu-id="d340e-103">Quickstart: Send search queries using the REST API and C#</span></span>

<span data-ttu-id="d340e-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span><span class="sxs-lookup"><span data-stu-id="d340e-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span></span>

<span data-ttu-id="d340e-105">This article includes a simple console application that performs a Bing Image Search API query and displays the returned raw search results, which are in JSON format.</span><span class="sxs-lookup"><span data-stu-id="d340e-105">This article includes a simple console application that performs a Bing Image Search API query and displays the returned raw search results, which are in JSON format.</span></span> <span data-ttu-id="d340e-106">While this application is written in C#, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="d340e-106">While this application is written in C#, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

<span data-ttu-id="d340e-107">The example program uses .NET Core classes only and runs on Windows using the .NET CLR or on Linux or macOS using [Mono](http://www.mono-project.com/).</span><span class="sxs-lookup"><span data-stu-id="d340e-107">The example program uses .NET Core classes only and runs on Windows using the .NET CLR or on Linux or macOS using [Mono](http://www.mono-project.com/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d340e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d340e-108">Prerequisites</span></span>

<span data-ttu-id="d340e-109">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to get this code running on Windows.</span><span class="sxs-lookup"><span data-stu-id="d340e-109">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to get this code running on Windows.</span></span> <span data-ttu-id="d340e-110">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="d340e-110">(The free Community Edition will work.)</span></span>

[!INCLUDE [cognitive-services-bing-image-search-signup-requirements](../../../../includes/cognitive-services-bing-image-search-signup-requirements.md)]

## <a name="running-the-application"></a><span data-ttu-id="d340e-111">Running the application</span><span class="sxs-lookup"><span data-stu-id="d340e-111">Running the application</span></span>

<span data-ttu-id="d340e-112">To run this application, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="d340e-112">To run this application, follow these steps.</span></span>

1. <span data-ttu-id="d340e-113">Create a new Console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d340e-113">Create a new Console solution in Visual Studio.</span></span>
2. <span data-ttu-id="d340e-114">Replace `Program.cs` with the provided code.</span><span class="sxs-lookup"><span data-stu-id="d340e-114">Replace `Program.cs` with the provided code.</span></span>
3. <span data-ttu-id="d340e-115">Replace the `accessKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="d340e-115">Replace the `accessKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="d340e-116">Run the program.</span><span class="sxs-lookup"><span data-stu-id="d340e-116">Run the program.</span></span>

```csharp
using System;
using System.Text;
using System.Net;
using System.IO;
using System.Collections.Generic;

namespace BingSearchApisQuickstart
{

    class Program
    {
        // **********************************************
        // *** Update or verify the following values. ***
        // **********************************************

        // Replace the accessKey string value with your valid access key.
        const string accessKey = "enter key here";

        // Verify the endpoint URI.  At this writing, only one endpoint is used for Bing
        // search APIs.  In the future, regional endpoints may be available.  If you
        // encounter unexpected authorization errors, double-check this value against
        // the endpoint for your Bing search instance in your Azure dashboard.
        const string uriBase = "https://api.cognitive.microsoft.com/bing/v7.0/images/search";

        const string searchTerm = "puppies";

        // Used to return image search results including relevant headers
        struct SearchResult
        {
            public String jsonResult;
            public Dictionary<String, String> relevantHeaders;
        }

        static void Main()
        {
            Console.OutputEncoding = System.Text.Encoding.UTF8;

            if (accessKey.Length == 32)
            {
                Console.WriteLine("Searching images for: " + searchTerm);

                SearchResult result = BingImageSearch(searchTerm);

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

        /// <summary>
        /// Performs a Bing Image search and return the results as a SearchResult.
        /// </summary>
        static SearchResult BingImageSearch(string searchQuery)
        {
            // Construct the URI of the search request
            var uriQuery = uriBase + "?q=" + Uri.EscapeDataString(searchQuery);

            // Perform the Web request and get the response
            WebRequest request = HttpWebRequest.Create(uriQuery);
            request.Headers["Ocp-Apim-Subscription-Key"] = accessKey;
            HttpWebResponse response = (HttpWebResponse)request.GetResponseAsync().Result;
            string json = new StreamReader(response.GetResponseStream()).ReadToEnd();

            // Create result object for return
            var searchResult = new SearchResult()
            {
                jsonResult = json,
                relevantHeaders = new Dictionary<String, String>()
            };

            // Extract Bing HTTP headers
            foreach (String header in response.Headers)
            {
                if (header.StartsWith("BingAPIs-") || header.StartsWith("X-MSEdge-"))
                    searchResult.relevantHeaders[header] = response.Headers[header];
            }

            return searchResult;
        }

        /// <summary>
        /// Formats the given JSON string by adding line breaks and indents.
        /// </summary>
        /// <param name="json">The raw JSON string to format.</param>
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
                        case '}':
                        case ']':
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
    }
}
```

## <a name="json-response"></a><span data-ttu-id="d340e-117">JSON response</span><span class="sxs-lookup"><span data-stu-id="d340e-117">JSON response</span></span>

<span data-ttu-id="d340e-118">A sample response follows.</span><span class="sxs-lookup"><span data-stu-id="d340e-118">A sample response follows.</span></span> <span data-ttu-id="d340e-119">To limit the length of the JSON, only a single result is shown, and other parts of the response have been truncated.</span><span class="sxs-lookup"><span data-stu-id="d340e-119">To limit the length of the JSON, only a single result is shown, and other parts of the response have been truncated.</span></span> 

```json
{
  "_type": "Images",
  "instrumentation": {},
  "readLink": "https://api.cognitive.microsoft.com/api/v7/images/search?q=puppies",
  "webSearchUrl": "https://www.bing.com/images/search?q=puppies&FORM=OIIARP",
  "totalEstimatedMatches": 955,
  "nextOffset": 1,
  "value": [
    {
      "webSearchUrl": "https://www.bing.com/images/search?view=detailv...",
      "name": "So cute - Puppies Wallpaper",
      "thumbnailUrl": "https://tse3.mm.bing.net/th?id=OIP.jHrihoDNkXGS1t...",
      "datePublished": "2014-02-01T21:55:00.0000000Z",
      "contentUrl": "http://images4.contoso.com/image/photos/14700000/So-cute-puppies...",
      "hostPageUrl": "http://www.contoso.com/clubs/puppies/images/14749028/...",
      "contentSize": "394455 B",
      "encodingFormat": "jpeg",
      "hostPageDisplayUrl": "www.contoso.com/clubs/puppies/images/14749...",
      "width": 1600,
      "height": 1200,
      "thumbnail": {
        "width": 300,
        "height": 225
      },
      "imageInsightsToken": "ccid_jHrihoDN*mid_F68CC526226E163FD1EA659747AD...",
      "insightsMetadata": {
        "recipeSourcesCount": 0
      },
      "imageId": "F68CC526226E163FD1EA659747ADCB8F9FA36",
      "accentColor": "8D613E"
    }
  ],
  "queryExpansions": [
    {
      "text": "Shih Tzu Puppies",
      "displayText": "Shih Tzu",
      "webSearchUrl": "https://www.bing.com/images/search?q=Shih+Tzu+Puppies...",
      "searchLink": "https://api.cognitive.microsoft.com/api/v7/images/search?q=Shih...",
      "thumbnail": {
        "thumbnailUrl": "https://tse2.mm.bing.net/th?q=Shih+Tzu+Puppies&pid=Api..."
      }
    }
  ],
  "pivotSuggestions": [
    {
      "pivot": "puppies",
      "suggestions": [
        {
          "text": "Dog",
          "displayText": "Dog",
          "webSearchUrl": "https://www.bing.com/images/search?q=Dog&tq=%7b%22pq%...",
          "searchLink": "https://api.cognitive.microsoft.com/api/v7/images/search?q=Dog...",
          "thumbnail": {
            "thumbnailUrl": "https://tse1.mm.bing.net/th?q=Dog&pid=Api&mkt=en-US..."
          }
        }
      ]
    }
  ],
  "similarTerms": [
    {
      "text": "cute",
      "displayText": "cute",
      "webSearchUrl": "https://www.bing.com/images/search?q=cute&FORM=...",
      "thumbnail": {
        "url": "https://tse2.mm.bing.net/th?q=cute&pid=Api&mkt=en-US..."
      }
    }
  ],
  "relatedSearches": [
    {
      "text": "Cute Puppies",
      "displayText": "Cute Puppies",
      "webSearchUrl": "https://www.bing.com/images/search?q=Cute+Puppies",
      "searchLink": "https://api.cognitive.microsoft.com/api/v7/images/sear...",
      "thumbnail": {
        "thumbnailUrl": "https://tse4.mm.bing.net/th?q=Cute+Puppies&pid=..."
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="d340e-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="d340e-120">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d340e-121">Bing Image Search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="d340e-121">Bing Image Search single-page app tutorial</span></span>](../tutorial-bing-image-search-single-page-app.md)

## <a name="see-also"></a><span data-ttu-id="d340e-122">See also</span><span class="sxs-lookup"><span data-stu-id="d340e-122">See also</span></span> 

[<span data-ttu-id="d340e-123">Bing Image Search overview</span><span class="sxs-lookup"><span data-stu-id="d340e-123">Bing Image Search overview</span></span>](../overview.md)  
[<span data-ttu-id="d340e-124">Try it</span><span class="sxs-lookup"><span data-stu-id="d340e-124">Try it</span></span>](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/)  
[<span data-ttu-id="d340e-125">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="d340e-125">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api)  
[<span data-ttu-id="d340e-126">Bing Image Search API reference</span><span class="sxs-lookup"><span data-stu-id="d340e-126">Bing Image Search API reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)
