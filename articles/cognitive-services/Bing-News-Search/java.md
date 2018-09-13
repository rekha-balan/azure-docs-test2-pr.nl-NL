---
title: Java Quickstart for Azure Cognitive Services, Bing News Search API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing News Search API in Microsoft Cognitive Services on Azure.
services: cognitive-services
documentationcenter: ''
author: v-jerkin
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: article
ms.date: 9/21/2017
ms.author: v-jerkin
ms.openlocfilehash: 15d0f6490a517466036d3caba1058cfefa551321
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866797"
---
# <a name="quickstart-for-bing-news-search-api-with-java"></a><span data-ttu-id="8afab-103">Quickstart for Bing News Search API with Java</span><span class="sxs-lookup"><span data-stu-id="8afab-103">Quickstart for Bing News Search API with Java</span></span>

<span data-ttu-id="8afab-104">This article shows you how use the Bing Search API, part of Microsoft Cognitive Services on Azure.</span><span class="sxs-lookup"><span data-stu-id="8afab-104">This article shows you how use the Bing Search API, part of Microsoft Cognitive Services on Azure.</span></span> <span data-ttu-id="8afab-105">While this article employs Java, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="8afab-105">While this article employs Java, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

<span data-ttu-id="8afab-106">The example code is written to run under Java 7 as a console application.</span><span class="sxs-lookup"><span data-stu-id="8afab-106">The example code is written to run under Java 7 as a console application.</span></span>

<span data-ttu-id="8afab-107">Refer to the [API reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference) for technical details about the APIs.</span><span class="sxs-lookup"><span data-stu-id="8afab-107">Refer to the [API reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference) for technical details about the APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8afab-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8afab-108">Prerequisites</span></span>

<span data-ttu-id="8afab-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span><span class="sxs-lookup"><span data-stu-id="8afab-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span></span> <span data-ttu-id="8afab-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="8afab-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="8afab-111">You will need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="8afab-111">You will need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="bing-news-search"></a><span data-ttu-id="8afab-112">Bing News search</span><span class="sxs-lookup"><span data-stu-id="8afab-112">Bing News search</span></span>

<span data-ttu-id="8afab-113">The [Bing News Search API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference) returns news results from the Bing search engine.</span><span class="sxs-lookup"><span data-stu-id="8afab-113">The [Bing News Search API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference) returns news results from the Bing search engine.</span></span>

1. <span data-ttu-id="8afab-114">Download or install the [gson library](https://github.com/google/gson).</span><span class="sxs-lookup"><span data-stu-id="8afab-114">Download or install the [gson library](https://github.com/google/gson).</span></span>
2. <span data-ttu-id="8afab-115">Create a new Java project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="8afab-115">Create a new Java project in your favorite IDE or editor.</span></span>
3. <span data-ttu-id="8afab-116">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="8afab-116">Add the code provided below.</span></span>
4. <span data-ttu-id="8afab-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="8afab-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
5. <span data-ttu-id="8afab-118">Run the program.</span><span class="sxs-lookup"><span data-stu-id="8afab-118">Run the program.</span></span>

```java
import java.net.*;
import java.util.*;
import java.io.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *     groupId: com.google.code.gson
 *     artifactId: gson
 *     version: 2.8.1
 *
 * Once you have compiled or downloaded gson-2.8.1.jar, assuming you have placed it in the
 * same folder as this file (BingNewsSearch.java), you can compile and run this program at
 * the command line as follows.
 *
 * javac BingNewsSearch.java -classpath .;gson-2.8.1.jar -encoding UTF-8
 * java -cp .;gson-2.8.1.jar BingNewsSearch
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

public class BingNewsSearch {

// ***********************************************
// *** Update or verify the following values. ***
// **********************************************

    // Replace the subscriptionKey string value with your valid subscription key.
    static String subscriptionKey = "enter key here";

    // Verify the endpoint URI.  At this writing, only one endpoint is used for Bing
    // search APIs.  In the future, regional endpoints may be available.  If you
    // encounter unexpected authorization errors, double-check this value against
    // the endpoint for your Bing Web search instance in your Azure dashboard.
    static String host = "https://api.cognitive.microsoft.com";
    static String path = "/bing/v7.0/news/search";

    static String searchTerm = "Microsoft";

    public static SearchResults SearchNews (String searchQuery) throws Exception {
        // construct URL of search request (endpoint + query string)
        URL url = new URL(host + path + "?q=" +  URLEncoder.encode(searchQuery, "UTF-8"));
        HttpsURLConnection connection = (HttpsURLConnection)url.openConnection();
        connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);

        // receive JSON body
        InputStream stream = connection.getInputStream();
        String response = new Scanner(stream).useDelimiter("\\A").next();

        // construct result object for return
        SearchResults results = new SearchResults(new HashMap<String, String>(), response);

        // extract Bing-related HTTP headers
        Map<String, List<String>> headers = connection.getHeaderFields();
        for (String header : headers.keySet()) {
            if (header == null) continue;      // may have null key
            if (header.startsWith("BingAPIs-") || header.startsWith("X-MSEdge-")) {
                results.relevantHeaders.put(header, headers.get(header).get(0));
            }
        }

        stream.close();
        return results;
    }

    // pretty-printer for JSON; uses GSON parser to parse and re-serialize
    public static String prettify(String json_text) {
        JsonParser parser = new JsonParser();
        JsonObject json = parser.parse(json_text).getAsJsonObject();
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

    public static void main (String[] args) {
        try {
            System.out.println("Searching the Web for: " + searchTerm);

            SearchResults result = SearchNews(searchTerm);

            System.out.println("\nRelevant HTTP Headers:\n");
            for (String header : result.relevantHeaders.keySet())
                System.out.println(header + ": " + result.relevantHeaders.get(header));

            System.out.println("\nJSON Response:\n");
            System.out.println(prettify(result.jsonResponse));
        }
        catch (Exception e) {
            e.printStackTrace(System.out);
            System.exit(1);
        }
    }
}

// Container class for search results encapsulates relevant headers and JSON data
class SearchResults{
    HashMap<String, String> relevantHeaders;
    String jsonResponse;
    SearchResults(HashMap<String, String> headers, String json) {
        relevantHeaders = headers;
        jsonResponse = json;
    }
}
```

<span data-ttu-id="8afab-119">**Response**</span><span class="sxs-lookup"><span data-stu-id="8afab-119">**Response**</span></span>

<span data-ttu-id="8afab-120">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8afab-120">A successful response is returned in JSON, as shown in the following example:</span></span>

```json
{
   "_type": "News",
   "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/news\/search?q=Microsoft",
   "totalEstimatedMatches": 36,
   "sort": [
      {
         "name": "Best match",
         "id": "relevance",
         "isSelected": true,
         "url": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/news\/search?q=Microsoft"
      },
      {
         "name": "Most recent",
         "id": "date",
         "isSelected": false,
         "url": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/news\/search?q=Microsoft&sortby=date"
      }
   ],
   "value": [
      {
         "name": "Microsoft to open flagship London brick-and-mortar retail store",
         "url": "http:\/\/www.contoso.com\/article\/microsoft-to-open-flagshi...",
         "image": {
            "thumbnail": {
               "contentUrl": "https:\/\/www.bing.com\/th?id=ON.F9E4A49EC010417...",
               "width": 220,
               "height": 146
            }
         },
         "description": "After years of rumors about Microsoft opening a brick-and-mortar...", 
         "about": [
           {
             "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entiti...", 
             "name": "Microsoft"
           }, 
           {
             "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entit...", 
             "name": "London"
           }
         ], 
         "provider": [
           {
             "_type": "Organization", 
             "name": "Contoso"
           }
         ], 
          "datePublished": "2017-09-21T21:16:00.0000000Z", 
          "category": "ScienceAndTechnology"
      }, 

      . . .
      
      {
         "name": "Microsoft adds Availability Zones to its Azure cloud platform",
         "url": "https:\/\/contoso.com\/2017\/09\/21\/microsoft-adds-availability...",
         "image": {
            "thumbnail": {
               "contentUrl": "https:\/\/www.bing.com\/th?id=ON.0AE7595B9720...",
               "width": 700,
               "height": 466
            }
         },
         "description": "Microsoft has begun adding Availability Zones to its...",
         "about": [
            {
               "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entities\/a093e9b...",
               "name": "Microsoft"
            },
            {
               "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entities\/cf3abf7d-e379-...",
               "name": "Windows Azure"
            },
            {
               "readLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/entities\/9cdd061c-1fae-d0...",
               "name": "Cloud"
            }
         ],
         "provider": [
            {
               "_type": "Organization",
               "name": "Contoso"
            }
         ],
         "datePublished": "2017-09-21T09:01:00.0000000Z",
         "category": "ScienceAndTechnology"
      }
   ]
}
```


## <a name="next-steps"></a><span data-ttu-id="8afab-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="8afab-121">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="8afab-122">[Paging news](paging-news.md)
> [Using decoration markers to highlight text](hit-highlighting.md)
> [Searching the web for news](search-the-web.md) </span><span class="sxs-lookup"><span data-stu-id="8afab-122">[Paging news](paging-news.md)
> [Using decoration markers to highlight text](hit-highlighting.md)
[Searching the web for news](search-the-web.md) </span></span>  
[<span data-ttu-id="8afab-123">Try it</span><span class="sxs-lookup"><span data-stu-id="8afab-123">Try it</span></span>](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/)

