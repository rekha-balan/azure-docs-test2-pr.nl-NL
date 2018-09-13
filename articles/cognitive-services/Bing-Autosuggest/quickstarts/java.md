---
title: Quickstart for Bing Autosuggest API with Java | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Autosuggest API in Azure Cognitive Services.
services: cognitive-services
documentationcenter: ''
author: v-jaswel
ms.service: cognitive-services
ms.component: bing-autosuggest
ms.topic: article
ms.date: 09/14/2017
ms.author: v-jaswel
ms.openlocfilehash: c3a6b7119521772dbb60f3702c84e9bbd94217c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865989"
---
# <a name="quickstart-for-bing-autosuggest-api-with-java"></a><span data-ttu-id="bab0d-103">Quickstart for Bing Autosuggest API with Java</span><span class="sxs-lookup"><span data-stu-id="bab0d-103">Quickstart for Bing Autosuggest API with Java</span></span>
<a name="HOLTop"></a>

<span data-ttu-id="bab0d-104">This article shows you how to use the [Bing Autosuggest API](https://azure.microsoft.com/services/cognitive-services/autosuggest/) with Java.</span><span class="sxs-lookup"><span data-stu-id="bab0d-104">This article shows you how to use the [Bing Autosuggest API](https://azure.microsoft.com/services/cognitive-services/autosuggest/) with Java.</span></span> <span data-ttu-id="bab0d-105">The Bing Autosuggest API returns a list of suggested queries based on the partial query string the user enters in the search box.</span><span class="sxs-lookup"><span data-stu-id="bab0d-105">The Bing Autosuggest API returns a list of suggested queries based on the partial query string the user enters in the search box.</span></span> <span data-ttu-id="bab0d-106">Typically, you would call this API each time the user types a new character in the search box, and then display the suggestions in the search box's drop down list.</span><span class="sxs-lookup"><span data-stu-id="bab0d-106">Typically, you would call this API each time the user types a new character in the search box, and then display the suggestions in the search box's drop down list.</span></span> <span data-ttu-id="bab0d-107">This article shows how to send a request that returns the suggested query strings for *sail*.</span><span class="sxs-lookup"><span data-stu-id="bab0d-107">This article shows how to send a request that returns the suggested query strings for *sail*.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bab0d-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bab0d-108">Prerequisites</span></span>

<span data-ttu-id="bab0d-109">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="bab0d-109">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="bab0d-110">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span><span class="sxs-lookup"><span data-stu-id="bab0d-110">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span></span>

<span data-ttu-id="bab0d-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Autosuggest API v7**.</span><span class="sxs-lookup"><span data-stu-id="bab0d-111">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Autosuggest API v7**.</span></span> <span data-ttu-id="bab0d-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#search) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="bab0d-112">The [free trial](https://azure.microsoft.com/try/cognitive-services/#search) is sufficient for this quickstart.</span></span> <span data-ttu-id="bab0d-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="bab0d-113">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="get-autosuggest-results"></a><span data-ttu-id="bab0d-114">Get Autosuggest results</span><span class="sxs-lookup"><span data-stu-id="bab0d-114">Get Autosuggest results</span></span>

1. <span data-ttu-id="bab0d-115">Create a new Java project in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="bab0d-115">Create a new Java project in your favorite IDE.</span></span>
2. <span data-ttu-id="bab0d-116">Add the code provided below.</span><span class="sxs-lookup"><span data-stu-id="bab0d-116">Add the code provided below.</span></span>
3. <span data-ttu-id="bab0d-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span><span class="sxs-lookup"><span data-stu-id="bab0d-117">Replace the `subscriptionKey` value with an access key valid for your subscription.</span></span>
4. <span data-ttu-id="bab0d-118">Run the program.</span><span class="sxs-lookup"><span data-stu-id="bab0d-118">Run the program.</span></span>

```java
import java.io.*;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *     groupId: com.google.code.gson
 *     artifactId: gson
 *     version: 2.8.1
 *
 * Once you have compiled or downloaded gson-2.8.1.jar, assuming you have placed it in the
 * same folder as this file (Autosuggest.java), you can compile and run this program at
 * the command line as follows.
 *
 * javac Autosuggest.java -classpath .;gson-2.8.1.jar -encoding UTF-8
 * java -cp .;gson-2.8.1.jar Autosuggest
 */
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

public class Autosuggest {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
  static String subscriptionKey = "enter key here";

  static String host = "https://api.cognitive.microsoft.com";
  static String path = "/bing/v7.0/Suggestions";

  static String mkt = "en-US";
  static String query = "sail";

  public static String get_suggestions () throws Exception {
        String encoded_query = URLEncoder.encode (query, "UTF-8");
        String params = "?mkt=" + mkt + "&q=" + encoded_query;
    URL url = new URL (host + path + params);

    HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
    connection.setRequestMethod("GET");
    connection.setRequestProperty("Ocp-Apim-Subscription-Key", subscriptionKey);
    connection.setDoOutput(true);

    StringBuilder response = new StringBuilder ();
    BufferedReader in = new BufferedReader(
    new InputStreamReader(connection.getInputStream()));
    String line;
    while ((line = in.readLine()) != null) {
      response.append(line);
    }
    in.close();

    return response.toString();
    }

  public static String prettify (String json_text) {
    JsonParser parser = new JsonParser();
    JsonObject json = parser.parse(json_text).getAsJsonObject();
    Gson gson = new GsonBuilder().setPrettyPrinting().create();
    return gson.toJson(json);
  }

  public static void main(String[] args) {
    try {
      String response = get_suggestions ();
      System.out.println (prettify (response));
    }
    catch (Exception e) {
      System.out.println (e);
    }
  }
}
```

### <a name="response"></a><span data-ttu-id="bab0d-119">Response</span><span class="sxs-lookup"><span data-stu-id="bab0d-119">Response</span></span>

<span data-ttu-id="bab0d-120">A successful response is returned in JSON, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="bab0d-120">A successful response is returned in JSON, as shown in the following example:</span></span> 

```json
{
  "_type": "Suggestions",
  "queryContext": {
    "originalQuery": "sail"
  },
  "suggestionGroups": [
    {
      "name": "Web",
      "searchSuggestions": [
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dgvtP9TS9NwhajSapY2Se6y1eCbP2fq_GiP2n-cxi6OY\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailrite%26FORM%3dUSBAPI\u0026p\u003dDevEx,5003.1",
          "displayText": "sailrite",
          "query": "sailrite",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dBTS0G6AakxntIl9rmbDXtk1n6rQpsZZ99aQ7ClE7dTY\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsail%2bsand%2bpoint%26FORM%3dUSBAPI\u0026p\u003dDevEx,5004.1",
          "displayText": "sail sand point",
          "query": "sail sand point",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dc0QOA_j6swCZJy9FxqOwke2KslJE7ZRmMooGClAuCpY\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailboats%2bfor%2bsale%26FORM%3dUSBAPI\u0026p\u003dDevEx,5005.1",
          "displayText": "sailboats for sale",
          "query": "sailboats for sale",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dmnMdREUH20SepmHQH1zlh9Hy_w7jpOlZFm3KG2R_BoA\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailing%2banarchy%26FORM%3dUSBAPI\u0026p\u003dDevEx,5006.1",
          "displayText": "sailing anarchy",
          "query": "sailing anarchy",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dWLFO-B1GG5qtBGnoU1Bizz02YKkg5fgAQtHwhXn4z8I\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailpoint%26FORM%3dUSBAPI\u0026p\u003dDevEx,5007.1",
          "displayText": "sailpoint",
          "query": "sailpoint",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003dquBMwmKlGwqC5wAU0K7n416plhWcR8zQCi7r-Fw9Y0w\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailflow%26FORM%3dUSBAPI\u0026p\u003dDevEx,5008.1",
          "displayText": "sailflow",
          "query": "sailflow",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003d0udadFl0gCTKCp0QmzQTXS3_y08iO8FpwsoKPHPS6kw\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailboatdata%26FORM%3dUSBAPI\u0026p\u003dDevEx,5009.1",
          "displayText": "sailboatdata",
          "query": "sailboatdata",
          "searchKind": "WebSearch"
        },
        {
          "url": "https://www.bing.com/cr?IG\u003d2ACC4FE8B02F4AACB9182A6502B0E556\u0026CID\u003d1D546424A4CB64AF2D386F26A5CD6583\u0026rd\u003d1\u0026h\u003deSSt0MRSbl2V0RFPSuVd-gC7fGOT4717pz55EBUgPec\u0026v\u003d1\u0026r\u003dhttps%3a%2f%2fwww.bing.com%2fsearch%3fq%3dsailor%2b2025%26FORM%3dUSBAPI\u0026p\u003dDevEx,5010.1",
          "displayText": "sailor 2025",
          "query": "sailor 2025",
          "searchKind": "WebSearch"
        }
      ]
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="bab0d-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="bab0d-121">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bab0d-122">Bing Autosuggest tutorial</span><span class="sxs-lookup"><span data-stu-id="bab0d-122">Bing Autosuggest tutorial</span></span>](../tutorials/autosuggest.md)

## <a name="see-also"></a><span data-ttu-id="bab0d-123">See also</span><span class="sxs-lookup"><span data-stu-id="bab0d-123">See also</span></span>

- [<span data-ttu-id="bab0d-124">What is Bing Autosuggest?</span><span class="sxs-lookup"><span data-stu-id="bab0d-124">What is Bing Autosuggest?</span></span>](../get-suggested-search-terms.md)
- [<span data-ttu-id="bab0d-125">Bing Autosuggest API v7 reference</span><span class="sxs-lookup"><span data-stu-id="bab0d-125">Bing Autosuggest API v7 reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference)