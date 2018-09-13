---
title: Get .gif images - Microsoft Cognitive Services | Microsoft Docs
description: How to use the Bing Image Search API to get more information about .gif images.
services: cognitive-services
author: MikeDodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 04/24/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: 10e922b0cd15868bfe8f09b3846c76a368052e69
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867870"
---
# <a name="search-for-gif-images"></a><span data-ttu-id="1bd91-103">Search for .gif images</span><span class="sxs-lookup"><span data-stu-id="1bd91-103">Search for .gif images</span></span>
<span data-ttu-id="1bd91-104">The Bing Image Search API enables you to also search across the entire Web for the most relevant .gif images.</span><span class="sxs-lookup"><span data-stu-id="1bd91-104">The Bing Image Search API enables you to also search across the entire Web for the most relevant .gif images.</span></span>  <span data-ttu-id="1bd91-105">Developers can integrate engaging gifs in various conversation scenarios.</span><span class="sxs-lookup"><span data-stu-id="1bd91-105">Developers can integrate engaging gifs in various conversation scenarios.</span></span> 

<span data-ttu-id="1bd91-106">The following URL is a query for animated .gif images.</span><span class="sxs-lookup"><span data-stu-id="1bd91-106">The following URL is a query for animated .gif images.</span></span>
````
https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=interesting&imageType=AnimatedGif&mkt=en-us
````
<span data-ttu-id="1bd91-107">The [q](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#query) parameter specifies the search terms.</span><span class="sxs-lookup"><span data-stu-id="1bd91-107">The [q](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#query) parameter specifies the search terms.</span></span>  <span data-ttu-id="1bd91-108">The previous query also specifies `animatedGif` using the [imageType](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#imagetype) filter parameter.</span><span class="sxs-lookup"><span data-stu-id="1bd91-108">The previous query also specifies `animatedGif` using the [imageType](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#imagetype) filter parameter.</span></span>

<span data-ttu-id="1bd91-109">To see examples of results, use the following URL to search bing.com.</span><span class="sxs-lookup"><span data-stu-id="1bd91-109">To see examples of results, use the following URL to search bing.com.</span></span>
````
https://www.bing.com/images/search?q=interesting&qft=%20filterui%3Aphoto-animatedgif 

````
## <a name="query-parameters"></a><span data-ttu-id="1bd91-110">Query parameters</span><span class="sxs-lookup"><span data-stu-id="1bd91-110">Query parameters</span></span>

<span data-ttu-id="1bd91-111">For more information about query parameters and options, see the [Image Search API reference](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#query-parameters).</span><span class="sxs-lookup"><span data-stu-id="1bd91-111">For more information about query parameters and options, see the [Image Search API reference](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#query-parameters).</span></span> <span data-ttu-id="1bd91-112">An example follows under the heading [Example search for animated gif using Java](#gifExample).</span><span class="sxs-lookup"><span data-stu-id="1bd91-112">An example follows under the heading [Example search for animated gif using Java](#gifExample).</span></span>

## <a name="tips-and-suggestions"></a><span data-ttu-id="1bd91-113">Tips and suggestions</span><span class="sxs-lookup"><span data-stu-id="1bd91-113">Tips and suggestions</span></span>

- <span data-ttu-id="1bd91-114">You can specify [maxFileSize](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#maxfilesize) and [minFileSize](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#minfilesize) parameters.</span><span class="sxs-lookup"><span data-stu-id="1bd91-114">You can specify [maxFileSize](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#maxfilesize) and [minFileSize](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#minfilesize) parameters.</span></span> <span data-ttu-id="1bd91-115">We recommend setting the maxFileSize=2000000 as majority of gifs in our index are under 2MB.</span><span class="sxs-lookup"><span data-stu-id="1bd91-115">We recommend setting the maxFileSize=2000000 as majority of gifs in our index are under 2MB.</span></span>  <span data-ttu-id="1bd91-116">This also helps to control the data size if bandwidth is a concern, such as in mobile cellular scenarios.</span><span class="sxs-lookup"><span data-stu-id="1bd91-116">This also helps to control the data size if bandwidth is a concern, such as in mobile cellular scenarios.</span></span>
- <span data-ttu-id="1bd91-117">To help improve perceived performance, load the thumbnail first before loading the source url.</span><span class="sxs-lookup"><span data-stu-id="1bd91-117">To help improve perceived performance, load the thumbnail first before loading the source url.</span></span>  
- <span data-ttu-id="1bd91-118">For first-run or landing page experience where you don't have a user query yet, try using our trending gif searches to help from the [trending images API](trending-images.md).</span><span class="sxs-lookup"><span data-stu-id="1bd91-118">For first-run or landing page experience where you don't have a user query yet, try using our trending gif searches to help from the [trending images API](trending-images.md).</span></span>
- <span data-ttu-id="1bd91-119">There are three settings for the [safeSearch](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#safesearch) parameter.</span><span class="sxs-lookup"><span data-stu-id="1bd91-119">There are three settings for the [safeSearch](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#safesearch) parameter.</span></span>  <span data-ttu-id="1bd91-120">The `strict` option blocks adult content.</span><span class="sxs-lookup"><span data-stu-id="1bd91-120">The `strict` option blocks adult content.</span></span> 
- <span data-ttu-id="1bd91-121">See [mkt](supported-countries-markets.md) for full list of languages and locations supported.</span><span class="sxs-lookup"><span data-stu-id="1bd91-121">See [mkt](supported-countries-markets.md) for full list of languages and locations supported.</span></span>
- <span data-ttu-id="1bd91-122">*AnimatedGifHttps* only returns animated gif images that are from an https address.</span><span class="sxs-lookup"><span data-stu-id="1bd91-122">*AnimatedGifHttps* only returns animated gif images that are from an https address.</span></span> <span data-ttu-id="1bd91-123">For security, many applications require connection to external web links over https.</span><span class="sxs-lookup"><span data-stu-id="1bd91-123">For security, many applications require connection to external web links over https.</span></span> <span data-ttu-id="1bd91-124">For example, the Apple App Store requires connection to web services over HTTPS, which encrypts user data secure while in transit.</span><span class="sxs-lookup"><span data-stu-id="1bd91-124">For example, the Apple App Store requires connection to web services over HTTPS, which encrypts user data secure while in transit.</span></span>

<a name="gifExample" />
## <a name="example-search-for-animated-gif-using-java"></a><span data-ttu-id="1bd91-125">Example search for animated gif using Java</span><span class="sxs-lookup"><span data-stu-id="1bd91-125">Example search for animated gif using Java</span></span>

<span data-ttu-id="1bd91-126">The following URL searches for animated .gif images: `q=interesting`</span><span class="sxs-lookup"><span data-stu-id="1bd91-126">The following URL searches for animated .gif images: `q=interesting`</span></span>
````
https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=interesting&imageType=AnimatedGif&mkt=en-us

````
<span data-ttu-id="1bd91-127">As shown in the following example, the URL query requires [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#headers) header.</span><span class="sxs-lookup"><span data-stu-id="1bd91-127">As shown in the following example, the URL query requires [Ocp-Apim-Subscription-Key](https://docs.microsoft.com/en-us/rest/api/cognitiveservices/bing-images-api-v7-reference#headers) header.</span></span>

<span data-ttu-id="1bd91-128">The following Java example builds and sends the request.</span><span class="sxs-lookup"><span data-stu-id="1bd91-128">The following Java example builds and sends the request.</span></span>

````
package gifSearch;
import java.net.*;
import java.util.*;
import java.io.*;
import javax.net.ssl.HttpsURLConnection;

import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

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
 * javac GIFsearch.java -classpath .;gson-2.8.1.jar -encoding UTF-8
 * java -cp .;gson-2.8.1.jar GIFsearch
 */


public class GIFsearch {

    // Replace the subscriptionKey string value with your valid subscription key.
    static String subscriptionKey = "YOUR-ACCESS-KEY";

    static String host = "https://api.cognitive.microsoft.com";
    static String path = "/bing/v7.0/images/search";

    static String searchTerm = "interesting";

    public static SearchResults SearchImages (String searchQuery) throws Exception {
        // construct URL of search request (endpoint + query string)
        URL url = new URL(host + path + "?q=" +  URLEncoder.encode(searchQuery, "UTF-8") + "&imageType=AnimatedGif&mkt=en-us");
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

//Container class for search results encapsulates relevant headers and JSON data
class SearchResults{
 HashMap<String, String> relevantHeaders;
 String jsonResponse;
 SearchResults(HashMap<String, String> headers, String json) {
     relevantHeaders = headers;
     jsonResponse = json;
 }
}

````

## <a name="results"></a><span data-ttu-id="1bd91-129">Results</span><span class="sxs-lookup"><span data-stu-id="1bd91-129">Results</span></span>
<span data-ttu-id="1bd91-130">The code gets the following results as JSON objects:</span><span class="sxs-lookup"><span data-stu-id="1bd91-130">The code gets the following results as JSON objects:</span></span>

```json
    {
      "webSearchUrl": "https://www.bing.com/images/search?view\u003ddetai...",
      "name": "Very Interesting GIF - Thats Very Interesting - ...",
      "thumbnailUrl": "https://tse1.mm.bing.net/th?id\u003dOIP.yJX6Vz345JPK...",
      "datePublished": "2017-03-12T01:35:00.0000000Z",
      "contentUrl": "https://media.contoso.co/images/c895fa573df8e493ca8d0dec7d93b/raw",
      "hostPageUrl": "https://www.contoso.co/view/thats-very-interesting-christi...",
      "contentSize": "1295633 B",
      "encodingFormat": "animatedgif",
      "hostPageDisplayUrl": "https://www.contoso.co/view/thats-very-christian...",
      "width": 440,
      "height": 186,
      "thumbnail": {
        "width": 474,
        "height": 200
      },
      "imageInsightsToken": "ccid_yJX6Vz34*mid_9FF0FFA42AADA1357F042443D2103B40EA...",
      "insightsMetadata": {
        "recipeSourcesCount": 0,
        "bestRepresentativeQuery": {
          "text": "That\u0027s Very Interesting",
          "displayText": "That\u0027s Very Interesting",
          "webSearchUrl": "https://www.bing.com/images/search?q\u003dThat..."
        },
        "pagesIncludingCount": 19,
        "availableSizesCount": 2
      },
      "imageId": "9FF0FFA42AADA1357F042443D21030EAAA225F",
      "accentColor": "62452D"
    },

```

## <a name="next-steps"></a><span data-ttu-id="1bd91-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="1bd91-131">Next steps</span></span>
- [<span data-ttu-id="1bd91-132">C# quickstart</span><span class="sxs-lookup"><span data-stu-id="1bd91-132">C# quickstart</span></span>](quickstarts/csharp.md)
- [<span data-ttu-id="1bd91-133">Tutorial Image Search single-page application</span><span class="sxs-lookup"><span data-stu-id="1bd91-133">Tutorial Image Search single-page application</span></span>](tutorial-bing-image-search-single-page-app.md)