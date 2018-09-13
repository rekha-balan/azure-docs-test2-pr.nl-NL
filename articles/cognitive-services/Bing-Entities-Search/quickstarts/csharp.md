---
title: C# Quickstart for Azure Cognitive Services, Bing Entity Search API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Entity Search API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 11/28/2017
ms.author: v-jaswel
ms.openlocfilehash: 928cddf5017890bddd25b9da3584d230cc44483a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865571"
---
# <a name="quickstart-for-microsoft-bing-entity-search-api-with-c"></a><span data-ttu-id="7a436-103">Quickstart for Microsoft Bing Entity Search API with C#</span><span class="sxs-lookup"><span data-stu-id="7a436-103">Quickstart for Microsoft Bing Entity Search API with C#</span></span> 
<a name="HOLTop"></a>

<span data-ttu-id="7a436-104">This article shows you how to use the [Bing Entity Search](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web) API with C#.</span><span class="sxs-lookup"><span data-stu-id="7a436-104">This article shows you how to use the [Bing Entity Search](https://docs.microsoft.com/azure/cognitive-services/bing-entities-search/search-the-web) API with C#.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a436-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a436-105">Prerequisites</span></span>

<span data-ttu-id="7a436-106">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span><span class="sxs-lookup"><span data-stu-id="7a436-106">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to run this code on Windows.</span></span> <span data-ttu-id="7a436-107">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="7a436-107">(The free Community Edition will work.)</span></span>

<span data-ttu-id="7a436-108">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Entity Search API**.</span><span class="sxs-lookup"><span data-stu-id="7a436-108">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Entity Search API**.</span></span> <span data-ttu-id="7a436-109">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-entity-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="7a436-109">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-entity-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="7a436-110">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="7a436-110">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="search-entities"></a><span data-ttu-id="7a436-111">Search entities</span><span class="sxs-lookup"><span data-stu-id="7a436-111">Search entities</span></span>

<span data-ttu-id="7a436-112">To run this application, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="7a436-112">To run this application, follow these steps.</span></span>

1. <span data-ttu-id="7a436-113">Create a new C# project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="7a436-113">Create a new C# project in your favorite IDE.</span></span>
2. <span data-ttu-id="7a436-114">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="7a436-114">Add the code provided below.</span></span>
3. <span data-ttu-id="7a436-115">Replace the `key` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="7a436-115">Replace the `key` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="7a436-116">Run the program.</span><span class="sxs-lookup"><span data-stu-id="7a436-116">Run the program.</span></span>

```csharp
using System;
using System.Net.Http;
using System.Text;

namespace EntitySearchSample
{
    class Program
    {
        static string host = "https://api.cognitive.microsoft.com";
        static string path = "/bing/v7.0/entities";

        static string market = "en-US";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string query = "italian restaurant near me";

        async static void Search()
        {
            HttpClient client = new HttpClient();
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", key);

            string uri = host + path + "?mkt=" + market + "&q=" + System.Net.WebUtility.UrlEncode(query);

            HttpResponseMessage response = await client.GetAsync(uri);

            string contentString = await response.Content.ReadAsStringAsync();
            Console.WriteLine(JsonPrettyPrint(contentString));
        }

        static void Main(string[] args)
        {
            Search();
            Console.ReadLine();
        }


        static string JsonPrettyPrint(string json)
        {
            if (string.IsNullOrEmpty(json))
                return string.Empty;

            json = json.Replace(Environment.NewLine, "").Replace("\t", "");

            StringBuilder sb = new StringBuilder();
            bool quote = false;
            bool ignore = false;
            int offset = 0;
            int indentLength = 3;

            foreach (char ch in json)
            {
                switch (ch)
                {
                    case '"':
                        if (!ignore) quote = !quote;
                        break;
                    case '\'':
                        if (quote) ignore = !ignore;
                        break;
                }

                if (quote)
                    sb.Append(ch);
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
                            if (ch != ' ') sb.Append(ch);
                            break;
                    }
                }
            }

            return sb.ToString().Trim();
        }

    }
}
```

<span data-ttu-id="7a436-117">**Response**</span><span class="sxs-lookup"><span data-stu-id="7a436-117">**Response**</span></span>

<span data-ttu-id="7a436-118">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7a436-118">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "_type": "SearchResponse",
  "queryContext": {
    "originalQuery": "italian restaurant near me",
    "askUserForLocation": true
  },
  "places": {
    "value": [
      {
        "_type": "LocalBusiness",
        "webSearchUrl": "https://www.bing.com/search?q=sinful+bakery&filters=local...",
        "name": "Liberty's Delightful Sinful Bakery & Cafe",
        "url": "https://www.contoso.com/",
        "entityPresentationInfo": {
          "entityScenario": "ListItem",
          "entityTypeHints": [
            "Place",
            "LocalBusiness"
          ]
        },
        "address": {
          "addressLocality": "Seattle",
          "addressRegion": "WA",
          "postalCode": "98112",
          "addressCountry": "US",
          "neighborhood": "Madison Park"
        },
        "telephone": "(800) 555-1212"
      },

      . . .
      {
        "_type": "Restaurant",
        "webSearchUrl": "https://www.bing.com/search?q=Pickles+and+Preserves...",
        "name": "Munson's Pickles and Preserves Farm",
        "url": "http://www.princi.com/",
        "entityPresentationInfo": {
          "entityScenario": "ListItem",
          "entityTypeHints": [
            "Place",
            "LocalBusiness",
            "Restaurant"
          ]
        },
        "address": {
          "addressLocality": "Seattle",
          "addressRegion": "WA",
          "postalCode": "98101",
          "addressCountry": "US",
          "neighborhood": "Capitol Hill"
        },
        "telephone": "(800) 555-1212"
      },
      
      . . .
    ]
  }
}
```

[<span data-ttu-id="7a436-119">Back to top</span><span class="sxs-lookup"><span data-stu-id="7a436-119">Back to top</span></span>](#HOLTop)

## <a name="next-steps"></a><span data-ttu-id="7a436-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a436-120">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="7a436-121">[Bing Entity Search tutorial](../tutorial-bing-entities-search-single-page-app.md)
> [Bing Entity Search overview](../search-the-web.md )
> [API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)</span><span class="sxs-lookup"><span data-stu-id="7a436-121">[Bing Entity Search tutorial](../tutorial-bing-entities-search-single-page-app.md)
[Bing Entity Search overview](../search-the-web.md )
[API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)</span></span>
