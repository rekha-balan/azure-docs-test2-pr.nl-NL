---
title: 'Quickstart: Use Java to call the Bing Web Search API'
description: In this quickstart, you will learn how to make your first call to the Bing Web Search API using Java and receive a JSON response.
services: cognitive-services
author: erhopf
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 8/16/2018
ms.author: erhopf
ms.openlocfilehash: 8d3e01aef8efdf1503ad7056220e0cba9fb38ed3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869380"
---
# <a name="quickstart-use-java-to-call-the-bing-web-search-api"></a><span data-ttu-id="cab8b-103">Quickstart: Use Java to call the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="cab8b-103">Quickstart: Use Java to call the Bing Web Search API</span></span>  

<span data-ttu-id="cab8b-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response.</span><span class="sxs-lookup"><span data-stu-id="cab8b-104">Use this quickstart to make your first call to the Bing Web Search API and receive a JSON response.</span></span>  

[!INCLUDE [bing-web-search-quickstart-signup](../../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a><span data-ttu-id="cab8b-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cab8b-105">Prerequisites</span></span>

<span data-ttu-id="cab8b-106">Here are a few things that you'll need before running this quickstart:</span><span class="sxs-lookup"><span data-stu-id="cab8b-106">Here are a few things that you'll need before running this quickstart:</span></span>

* [<span data-ttu-id="cab8b-107">JDK 7 or 8</span><span class="sxs-lookup"><span data-stu-id="cab8b-107">JDK 7 or 8</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="cab8b-108">Gson library</span><span class="sxs-lookup"><span data-stu-id="cab8b-108">Gson library</span></span>](https://github.com/google/gson)
* <span data-ttu-id="cab8b-109">A subscription key</span><span class="sxs-lookup"><span data-stu-id="cab8b-109">A subscription key</span></span>

## <a name="create-a-project-and-import-dependencies"></a><span data-ttu-id="cab8b-110">Create a project and import dependencies</span><span class="sxs-lookup"><span data-stu-id="cab8b-110">Create a project and import dependencies</span></span>

<span data-ttu-id="cab8b-111">Create a new Java project in your favorite IDE or editor and import the following libraries.</span><span class="sxs-lookup"><span data-stu-id="cab8b-111">Create a new Java project in your favorite IDE or editor and import the following libraries.</span></span> <span data-ttu-id="cab8b-112">Gson is required to convert Java Objects into JSON.</span><span class="sxs-lookup"><span data-stu-id="cab8b-112">Gson is required to convert Java Objects into JSON.</span></span>

```java
import java.net.*;
import java.util.*;
import java.io.*;
import javax.net.ssl.HttpsURLConnection;
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
```

### <a name="declare-gson-in-the-maven-pom-file"></a><span data-ttu-id="cab8b-113">Declare Gson in the Maven POM file</span><span class="sxs-lookup"><span data-stu-id="cab8b-113">Declare Gson in the Maven POM file</span></span>

<span data-ttu-id="cab8b-114">If you're using Maven, declare Gson in the `POM.xml`.</span><span class="sxs-lookup"><span data-stu-id="cab8b-114">If you're using Maven, declare Gson in the `POM.xml`.</span></span> <span data-ttu-id="cab8b-115">Skip this step if you've installed Gson locally.</span><span class="sxs-lookup"><span data-stu-id="cab8b-115">Skip this step if you've installed Gson locally.</span></span>

```xml
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.1</version>
</dependency>
```

## <a name="declare-the-bingwebsearch-class"></a><span data-ttu-id="cab8b-116">Declare the BingWebSearch class</span><span class="sxs-lookup"><span data-stu-id="cab8b-116">Declare the BingWebSearch class</span></span>

<span data-ttu-id="cab8b-117">Declare the `BingWebSearch` class.</span><span class="sxs-lookup"><span data-stu-id="cab8b-117">Declare the `BingWebSearch` class.</span></span> <span data-ttu-id="cab8b-118">It will include most of the code we review in this quickstart including the `main` method.</span><span class="sxs-lookup"><span data-stu-id="cab8b-118">It will include most of the code we review in this quickstart including the `main` method.</span></span>  

```java
public class BingWebSearch {

// The code in the following sections goes here.

}
```

## <a name="define-variables"></a><span data-ttu-id="cab8b-119">Define variables</span><span class="sxs-lookup"><span data-stu-id="cab8b-119">Define variables</span></span>

<span data-ttu-id="cab8b-120">This code sets the `subscriptionKey`, `host`, `path`, and `searchTerm`.</span><span class="sxs-lookup"><span data-stu-id="cab8b-120">This code sets the `subscriptionKey`, `host`, `path`, and `searchTerm`.</span></span> <span data-ttu-id="cab8b-121">Confirm that the endpoint is correct and replace the `subscriptionKey` value with a valid subscription key from your Azure account.</span><span class="sxs-lookup"><span data-stu-id="cab8b-121">Confirm that the endpoint is correct and replace the `subscriptionKey` value with a valid subscription key from your Azure account.</span></span> <span data-ttu-id="cab8b-122">Feel free to customize the search query by replacing the value for `searchTerm`.</span><span class="sxs-lookup"><span data-stu-id="cab8b-122">Feel free to customize the search query by replacing the value for `searchTerm`.</span></span>

```java
// Enter a valid subscription key.
static String subscriptionKey = "enter key here";

/*
 * If you encounter unexpected authorization errors, double-check these values
 * against the endpoint for your Bing Web search instance in your Azure
 * dashboard.
 */
static String host = "https://api.cognitive.microsoft.com";
static String path = "/bing/v7.0/search";
static String searchTerm = "Microsoft Cognitive Services";
```

## <a name="construct-a-request"></a><span data-ttu-id="cab8b-123">Construct a request</span><span class="sxs-lookup"><span data-stu-id="cab8b-123">Construct a request</span></span>

<span data-ttu-id="cab8b-124">This method, which lives in the `BingWebSearch` class, constructs the `url`, receives and parses the response, and extracts Bing-related HTTP headers.</span><span class="sxs-lookup"><span data-stu-id="cab8b-124">This method, which lives in the `BingWebSearch` class, constructs the `url`, receives and parses the response, and extracts Bing-related HTTP headers.</span></span>  

```java
public static SearchResults SearchWeb (String searchQuery) throws Exception {
    // Construct the URL.
    URL url = new URL(host + path + "?q=" +  URLEncoder.encode(searchQuery, "UTF-8"));

    // Open the connection.
    HttpsURLConnection connection = (HttpsURLConnection)url.openConnection();
    connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);

    // Receive the JSON response body.
    InputStream stream = connection.getInputStream();
    String response = new Scanner(stream).useDelimiter("\\A").next();

    // Construct the result object.
    SearchResults results = new SearchResults(new HashMap<String, String>(), response);

    // Extract Bing-related HTTP headers.
    Map<String, List<String>> headers = connection.getHeaderFields();
    for (String header : headers.keySet()) {
        if (header == null) continue;      // may have null key
        if (header.startsWith("BingAPIs-") || header.startsWith("X-MSEdge-")){
            results.relevantHeaders.put(header, headers.get(header).get(0));
        }
    }
    stream.close();
    return results;
}
```

## <a name="handle-the-response"></a><span data-ttu-id="cab8b-125">Handle the response</span><span class="sxs-lookup"><span data-stu-id="cab8b-125">Handle the response</span></span>

<span data-ttu-id="cab8b-126">Use Gson to parse and reserialize the response.</span><span class="sxs-lookup"><span data-stu-id="cab8b-126">Use Gson to parse and reserialize the response.</span></span>

```java
public static String prettify(String json_text) {
    JsonParser parser = new JsonParser();
    JsonObject json = parser.parse(json_text).getAsJsonObject();
    Gson gson = new GsonBuilder().setPrettyPrinting().create();
    return gson.toJson(json);
}
```

## <a name="declare-the-main-method"></a><span data-ttu-id="cab8b-127">Declare the main method</span><span class="sxs-lookup"><span data-stu-id="cab8b-127">Declare the main method</span></span>

<span data-ttu-id="cab8b-128">This method is required and is the first method invoked when the program is started.</span><span class="sxs-lookup"><span data-stu-id="cab8b-128">This method is required and is the first method invoked when the program is started.</span></span> <span data-ttu-id="cab8b-129">In this application, it includes code that validates the `subscriptionKey`, makes a request, and prints the JSON response.</span><span class="sxs-lookup"><span data-stu-id="cab8b-129">In this application, it includes code that validates the `subscriptionKey`, makes a request, and prints the JSON response.</span></span>

```java
public static void main (String[] args) {
    // Confirm the subscriptionKey is valid.
    if (subscriptionKey.length() != 32) {
        System.out.println("Invalid Bing Search API subscription key!");
        System.out.println("Please paste yours into the source code.");
        System.exit(1);
    }

    // Call the SearchWeb method and print the response.
    try {
        System.out.println("Searching the Web for: " + searchTerm);
        SearchResults result = SearchWeb(searchTerm);
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
```

## <a name="create-a-container-class-for-search-results"></a><span data-ttu-id="cab8b-130">Create a container class for search results</span><span class="sxs-lookup"><span data-stu-id="cab8b-130">Create a container class for search results</span></span>

<span data-ttu-id="cab8b-131">The `SearchResults` container class is outside of the `BingWebSearch` class.</span><span class="sxs-lookup"><span data-stu-id="cab8b-131">The `SearchResults` container class is outside of the `BingWebSearch` class.</span></span> <span data-ttu-id="cab8b-132">It includes relevant headers and JSON data for the response.</span><span class="sxs-lookup"><span data-stu-id="cab8b-132">It includes relevant headers and JSON data for the response.</span></span>

```java
class SearchResults{
    HashMap<String, String> relevantHeaders;
    String jsonResponse;
    SearchResults(HashMap<String, String> headers, String json) {
        relevantHeaders = headers;
        jsonResponse = json;
    }
}
```

## <a name="put-it-all-together"></a><span data-ttu-id="cab8b-133">Put it all together</span><span class="sxs-lookup"><span data-stu-id="cab8b-133">Put it all together</span></span>

<span data-ttu-id="cab8b-134">The last step is to compile your code and run it!</span><span class="sxs-lookup"><span data-stu-id="cab8b-134">The last step is to compile your code and run it!</span></span> <span data-ttu-id="cab8b-135">Here are the commands:</span><span class="sxs-lookup"><span data-stu-id="cab8b-135">Here are the commands:</span></span>

```powershell
javac BingWebSearch.java -classpath ./gson-2.8.1.jar -encoding UTF-8
java -cp ./gson-2.8.1.jar BingWebSearch
```

<span data-ttu-id="cab8b-136">If you'd like to compare your code with ours, [sample code is available on GitHub](https://github.com/Azure-Samples/cognitive-services-REST-api-samples/blob/master/java/Search/BingWebSearchv7.java).</span><span class="sxs-lookup"><span data-stu-id="cab8b-136">If you'd like to compare your code with ours, [sample code is available on GitHub](https://github.com/Azure-Samples/cognitive-services-REST-api-samples/blob/master/java/Search/BingWebSearchv7.java).</span></span>

## <a name="sample-response"></a><span data-ttu-id="cab8b-137">Sample response</span><span class="sxs-lookup"><span data-stu-id="cab8b-137">Sample response</span></span>

<span data-ttu-id="cab8b-138">Responses from the Bing Web Search API are returned as JSON.</span><span class="sxs-lookup"><span data-stu-id="cab8b-138">Responses from the Bing Web Search API are returned as JSON.</span></span> <span data-ttu-id="cab8b-139">This sample response has been truncated to show a single result.</span><span class="sxs-lookup"><span data-stu-id="cab8b-139">This sample response has been truncated to show a single result.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cab8b-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="cab8b-140">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cab8b-141">Bing Web search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="cab8b-141">Bing Web search single-page app tutorial</span></span>](../tutorial-bing-web-search-single-page-app.md)

[!INCLUDE [bing-web-search-quickstart-see-also](../../../../includes/bing-web-search-quickstart-see-also.md)]  
