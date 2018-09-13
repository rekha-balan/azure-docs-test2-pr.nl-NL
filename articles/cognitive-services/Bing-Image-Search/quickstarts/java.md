---
title: 'Quickstart: Send search queries using the REST API for the Bing Image Search API and Java'
description: In this quickstart, you send search queries to the Bing Search API to get a list of relevant images using Java.
services: cognitive-services
documentationcenter: ''
author: v-jerkin
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 9/21/2017
ms.author: v-jerkin
ms.openlocfilehash: 3d779bae099bde5b015ee8316906ace77c0ad3bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869381"
---
# <a name="quickstart-send-search-queries-using-the-rest-api-and-java"></a><span data-ttu-id="400b2-103">Quickstart: Send search queries using the REST API and Java</span><span class="sxs-lookup"><span data-stu-id="400b2-103">Quickstart: Send search queries using the REST API and Java</span></span>

<span data-ttu-id="400b2-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span><span class="sxs-lookup"><span data-stu-id="400b2-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span></span>

<span data-ttu-id="400b2-105">This article includes a simple console application that performs a Bing Image Search API query and displays the returned raw search results, which are in JSON format.</span><span class="sxs-lookup"><span data-stu-id="400b2-105">This article includes a simple console application that performs a Bing Image Search API query and displays the returned raw search results, which are in JSON format.</span></span> <span data-ttu-id="400b2-106">While this application is written in Java, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="400b2-106">While this application is written in Java, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="400b2-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="400b2-107">Prerequisites</span></span>

<span data-ttu-id="400b2-108">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="400b2-108">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="400b2-109">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span><span class="sxs-lookup"><span data-stu-id="400b2-109">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span></span>

[!INCLUDE [cognitive-services-bing-image-search-signup-requirements](../../../../includes/cognitive-services-bing-image-search-signup-requirements.md)]

## <a name="running-the-application"></a><span data-ttu-id="400b2-110">Running the application</span><span class="sxs-lookup"><span data-stu-id="400b2-110">Running the application</span></span>

<span data-ttu-id="400b2-111">To run this application, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="400b2-111">To run this application, follow these steps.</span></span>

1. <span data-ttu-id="400b2-112">Download or install the [gson library](https://github.com/google/gson).</span><span class="sxs-lookup"><span data-stu-id="400b2-112">Download or install the [gson library](https://github.com/google/gson).</span></span> <span data-ttu-id="400b2-113">You may also obtain it via Maven.</span><span class="sxs-lookup"><span data-stu-id="400b2-113">You may also obtain it via Maven.</span></span>
2. <span data-ttu-id="400b2-114">Create a new Java project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="400b2-114">Create a new Java project in your favorite IDE or editor.</span></span>
3. <span data-ttu-id="400b2-115">Add the provided code in a file named `BingImageSearch.java`.</span><span class="sxs-lookup"><span data-stu-id="400b2-115">Add the provided code in a file named `BingImageSearch.java`.</span></span>
4. <span data-ttu-id="400b2-116">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="400b2-116">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
5. <span data-ttu-id="400b2-117">Run the program.</span><span class="sxs-lookup"><span data-stu-id="400b2-117">Run the program.</span></span>

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
 * same folder as this file (BingImageSearch.java), you can compile and run this program at
 * the command line as follows.
 *
 * javac BingImageSearch.java -classpath .;gson-2.8.1.jar -encoding UTF-8
 * java -cp .;gson-2.8.1.jar BingImageSearch
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

public class BingImageSearch {

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
    static String path = "/bing/v7.0/images/search";

    static String searchTerm = "puppies";

    public static SearchResults SearchImages (String searchQuery) throws Exception {
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
        if (subscriptionKey.length() != 32) {
            System.out.println("Invalid Bing Search API subscription key!");
            System.out.println("Please paste yours into the source code.");
            System.exit(1);
        }

        try {
            System.out.println("Searching the Web for: " + searchTerm);

            SearchResults result = SearchImages(searchTerm);

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

## <a name="json-response"></a><span data-ttu-id="400b2-118">JSON response</span><span class="sxs-lookup"><span data-stu-id="400b2-118">JSON response</span></span>

<span data-ttu-id="400b2-119">A sample response follows.</span><span class="sxs-lookup"><span data-stu-id="400b2-119">A sample response follows.</span></span> <span data-ttu-id="400b2-120">To limit the length of the JSON, only a single result is shown, and other parts of the response have been truncated.</span><span class="sxs-lookup"><span data-stu-id="400b2-120">To limit the length of the JSON, only a single result is shown, and other parts of the response have been truncated.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="400b2-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="400b2-121">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="400b2-122">Bing Image Search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="400b2-122">Bing Image Search single-page app tutorial</span></span>](../tutorial-bing-image-search-single-page-app.md)

## <a name="see-also"></a><span data-ttu-id="400b2-123">See also</span><span class="sxs-lookup"><span data-stu-id="400b2-123">See also</span></span> 

[<span data-ttu-id="400b2-124">Bing Image Search overview</span><span class="sxs-lookup"><span data-stu-id="400b2-124">Bing Image Search overview</span></span>](../overview.md)  
[<span data-ttu-id="400b2-125">Try it</span><span class="sxs-lookup"><span data-stu-id="400b2-125">Try it</span></span>](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/)  
[<span data-ttu-id="400b2-126">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="400b2-126">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api)  
[<span data-ttu-id="400b2-127">Bing Image Search API reference</span><span class="sxs-lookup"><span data-stu-id="400b2-127">Bing Image Search API reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)
