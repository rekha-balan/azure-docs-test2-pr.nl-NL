---
title: Call endpoint by using Java - Bing Custom Search - Microsoft Cognitive Services
description: This quickstart shows how to request search results from your custom search instance by using Java to call the Bing Custom Search endpoint.
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: conceptual
ms.date: 05/07/2018
ms.author: v-brapel
ms.openlocfilehash: 03d622e3c7a3315238f2bceedae529bbe06af299
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868485"
---
# <a name="call-bing-custom-search-endpoint-java"></a><span data-ttu-id="17a82-103">Call Bing Custom Search endpoint (Java)</span><span class="sxs-lookup"><span data-stu-id="17a82-103">Call Bing Custom Search endpoint (Java)</span></span>

<span data-ttu-id="17a82-104">This quickstart shows how to request search results from your custom search instance by using Java to call the Bing Custom Search endpoint.</span><span class="sxs-lookup"><span data-stu-id="17a82-104">This quickstart shows how to request search results from your custom search instance by using Java to call the Bing Custom Search endpoint.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="17a82-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="17a82-105">Prerequisites</span></span>
<span data-ttu-id="17a82-106">To complete this quickstart, you need:</span><span class="sxs-lookup"><span data-stu-id="17a82-106">To complete this quickstart, you need:</span></span>
- <span data-ttu-id="17a82-107">A custom search instance.</span><span class="sxs-lookup"><span data-stu-id="17a82-107">A custom search instance.</span></span> <span data-ttu-id="17a82-108">See [Create your first Bing Custom Search instance](quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="17a82-108">See [Create your first Bing Custom Search instance](quick-start.md).</span></span>

- <span data-ttu-id="17a82-109">[Java](https://www.java.com) installed.</span><span class="sxs-lookup"><span data-stu-id="17a82-109">[Java](https://www.java.com) installed.</span></span>

- <span data-ttu-id="17a82-110">A [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span><span class="sxs-lookup"><span data-stu-id="17a82-110">A [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span></span> <span data-ttu-id="17a82-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="17a82-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search) is sufficient for this quickstart.</span></span> <span data-ttu-id="17a82-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="17a82-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="run-the-code"></a><span data-ttu-id="17a82-113">Run the code</span><span class="sxs-lookup"><span data-stu-id="17a82-113">Run the code</span></span>

<span data-ttu-id="17a82-114">To call the Bing Custom Search endpoint, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="17a82-114">To call the Bing Custom Search endpoint, follow these steps:</span></span>

1. <span data-ttu-id="17a82-115">Using your Java IDE of choice create a package.</span><span class="sxs-lookup"><span data-stu-id="17a82-115">Using your Java IDE of choice create a package.</span></span>
2. <span data-ttu-id="17a82-116">Create the file CustomSrchJava.java and copy the following code to it.</span><span class="sxs-lookup"><span data-stu-id="17a82-116">Create the file CustomSrchJava.java and copy the following code to it.</span></span>
3. <span data-ttu-id="17a82-117">Replace **YOUR-SUBSCRIPTION-KEY** and **YOUR-CUSTOM-CONFIG-ID** with your key and configuration ID.</span><span class="sxs-lookup"><span data-stu-id="17a82-117">Replace **YOUR-SUBSCRIPTION-KEY** and **YOUR-CUSTOM-CONFIG-ID** with your key and configuration ID.</span></span>

    ``` Java
    import java.io.InputStream;
    import java.net.URL;
    import java.net.URLEncoder;
    import java.util.HashMap;
    import java.util.List;
    import java.util.Map;
    import java.util.Scanner;
    
    import javax.net.ssl.HttpsURLConnection;
    
    import com.google.gson.Gson;
    import com.google.gson.GsonBuilder;
    import com.google.gson.JsonObject;
    import com.google.gson.JsonParser;
    
    public class CustomSrchJava {       
        static String host = "https://api.cognitive.microsoft.com";
        static String path = "/bingcustomsearch/v7.0/search";
        static String subscriptionKey = "YOUR-SUBSCRIPTION-KEY"; 
        static String customConfigId = "YOUR-CUSTOM-CONFIG-ID";  
    
        static String searchTerm = "Microsoft";  // Replace with search term specific to your defined sources.
    
        public static SearchResults SearchImages (String searchQuery) throws Exception {
            // construct URL of search request (endpoint + query string)
            URL url = new URL(host + path + "?q=" +  URLEncoder.encode(searchTerm, "UTF-8") + "&CustomConfig=" + customConfigId);
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
4. <span data-ttu-id="17a82-118">Run the program.</span><span class="sxs-lookup"><span data-stu-id="17a82-118">Run the program.</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="17a82-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="17a82-119">Next steps</span></span>
- [<span data-ttu-id="17a82-120">Configure your hosted UI experience</span><span class="sxs-lookup"><span data-stu-id="17a82-120">Configure your hosted UI experience</span></span>](./hosted-ui.md)
- [<span data-ttu-id="17a82-121">Use decoration markers to highlight text</span><span class="sxs-lookup"><span data-stu-id="17a82-121">Use decoration markers to highlight text</span></span>](./hit-highlighting.md)
- [<span data-ttu-id="17a82-122">Page webpages</span><span class="sxs-lookup"><span data-stu-id="17a82-122">Page webpages</span></span>](./page-webpages.md)