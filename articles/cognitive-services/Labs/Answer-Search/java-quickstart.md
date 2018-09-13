---
title: Project Answer Search Java quick start - Microsoft Cognitive Services | Microsoft Docs
description: Start using Project Answer Search in Java.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.technology: project-answer-search
ms.topic: article
ms.date: 04/13/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: 4e1f606e1564981589e638e0e51a8b42633ca7b0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857670"
---
# <a name="project-answer-search-query-in-java"></a><span data-ttu-id="7a6c4-103">Project Answer Search query in Java</span><span class="sxs-lookup"><span data-stu-id="7a6c4-103">Project Answer Search query in Java</span></span>
<span data-ttu-id="7a6c4-104">This article uses Java to demonstrate the Bing Answer Search API, part of Microsoft Cognitive Services on Azure.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-104">This article uses Java to demonstrate the Bing Answer Search API, part of Microsoft Cognitive Services on Azure.</span></span> <span data-ttu-id="7a6c4-105">The API is a REST Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-105">The API is a REST Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span>
 
<span data-ttu-id="7a6c4-106">The example code uses Java with minimal external dependencies.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-106">The example code uses Java with minimal external dependencies.</span></span>  <span data-ttu-id="7a6c4-107">You can also run it on Linux or Mac OS X using Mono.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-107">You can also run it on Linux or Mac OS X using Mono.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a6c4-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a6c4-108">Prerequisites</span></span>

<span data-ttu-id="7a6c4-109">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span><span class="sxs-lookup"><span data-stu-id="7a6c4-109">Get an access key for the free trial [Cognitive Services Labs](https://aka.ms/answersearchsubscription)</span></span>

## <a name="request"></a><span data-ttu-id="7a6c4-110">Request</span><span class="sxs-lookup"><span data-stu-id="7a6c4-110">Request</span></span> 

<span data-ttu-id="7a6c4-111">The following code creates a `WebRequest`, sets the access key header, and adds a query string for "Gibraltar".</span><span class="sxs-lookup"><span data-stu-id="7a6c4-111">The following code creates a `WebRequest`, sets the access key header, and adds a query string for "Gibraltar".</span></span>  <span data-ttu-id="7a6c4-112">It then sends the request and assigns the response to a string to contain the JSON text.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-112">It then sends the request and assigns the response to a string to contain the JSON text.</span></span>

````
    static String host = "https://api.labs.cognitive.microsoft.com";
    static String path = "/answerSearch/v7.0/search";

    // construct URL of search request (endpoint + query string)

    URL url = new URL(host + path + "?q=" +  URLEncoder.encode(searchQuery, "UTF-8") + &mkt=en-us");
    HttpsURLConnection connection = (HttpsURLConnection)url.openConnection();
    connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);

    // receive JSON body
    InputStream stream = connection.getInputStream();
    String response = new Scanner(stream).useDelimiter("\\A").next();

    // construct result object for return
    SearchResults results = new SearchResults(new HashMap<String, String>(), response);
````

## <a name="complete-code"></a><span data-ttu-id="7a6c4-113">Complete code</span><span class="sxs-lookup"><span data-stu-id="7a6c4-113">Complete code</span></span>

<span data-ttu-id="7a6c4-114">The Bing Answer Search API returns results from the Bing search engine.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-114">The Bing Answer Search API returns results from the Bing search engine.</span></span>
1. <span data-ttu-id="7a6c4-115">Download or install the gson library.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-115">Download or install the gson library.</span></span>
2. <span data-ttu-id="7a6c4-116">Create a new Java project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-116">Create a new Java project in your favorite IDE or editor.</span></span>
3. <span data-ttu-id="7a6c4-117">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-117">Add the code provided below.</span></span>
4. <span data-ttu-id="7a6c4-118">Replace the subscriptionKey value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-118">Replace the subscriptionKey value with an access key valid for your subscription.</span></span>
5. <span data-ttu-id="7a6c4-119">Run the program.</span><span class="sxs-lookup"><span data-stu-id="7a6c4-119">Run the program.</span></span>

````
package knowledgeAPI;
import java.io.InputStream;
import java.net.*;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

import javax.net.ssl.HttpsURLConnection;

import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

public class KnowledgeSrch {

        // Replace the subscriptionKey string value with your valid subscription key.
        static String subscriptionKey = "YOUR-ACCESS-KEY";

        static String host = "https://api.labs.cognitive.microsoft.com";
        static String path = "/answerSearch/v7.0/search";

        static String searchTerm = "Gibraltar";

        public static SearchResults SearchKnowledge (String searchQuery) throws Exception {

            URL url = new URL(host + path + "?q=" +  URLEncoder.encode(searchQuery, "UTF-8") + "&mkt=en-us");
            
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

                SearchResults result = SearchKnowledge(searchTerm);

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

````

## <a name="next-steps"></a><span data-ttu-id="7a6c4-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a6c4-120">Next steps</span></span>
- [<span data-ttu-id="7a6c4-121">C# quickstart</span><span class="sxs-lookup"><span data-stu-id="7a6c4-121">C# quickstart</span></span>](c-sharp-quickstart.md)
- [<span data-ttu-id="7a6c4-122">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="7a6c4-122">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="7a6c4-123">Node quickstart</span><span class="sxs-lookup"><span data-stu-id="7a6c4-123">Node quickstart</span></span>](node-quickstart.md)