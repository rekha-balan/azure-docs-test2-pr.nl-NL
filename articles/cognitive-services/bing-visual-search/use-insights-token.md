---
title: Using insights token with Bing Visual Search API | Microsoft Docs
titleSuffix: Bing Web Search APIs - Cognitive Services
description: Shows how to use an image's insight token with Visual Search API to get insights about an image.
services: cognitive-services
author: swhite-msft
manager: rosh
ms.service: cognitive-services
ms.technology: bing-visual-search
ms.topic: article
ms.date: 5/16/2018
ms.author: scottwhi
ms.openlocfilehash: 569ae89a712d14fb36989e756f99725dce398c0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865629"
---
# <a name="using-an-insights-token-to-get-insights-about-an-image"></a><span data-ttu-id="3b130-103">Using an insights token to get insights about an image</span><span class="sxs-lookup"><span data-stu-id="3b130-103">Using an insights token to get insights about an image</span></span>

<span data-ttu-id="3b130-104">Bing Visual Search API returns information about an image that you provide.</span><span class="sxs-lookup"><span data-stu-id="3b130-104">Bing Visual Search API returns information about an image that you provide.</span></span> <span data-ttu-id="3b130-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span><span class="sxs-lookup"><span data-stu-id="3b130-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span></span> <span data-ttu-id="3b130-106">For information about these options, see [What is Bing Visual Search API?](overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b130-106">For information about these options, see [What is Bing Visual Search API?](overview.md).</span></span> <span data-ttu-id="3b130-107">This article demonstrates using an insights token.</span><span class="sxs-lookup"><span data-stu-id="3b130-107">This article demonstrates using an insights token.</span></span> <span data-ttu-id="3b130-108">For examples that demonstrate uploading an image to get insights, see the quickstarts ([C#](quickstarts\csharp.md) | [Java](quickstarts\java.md) | [Node.js](quickstarts\nodejs.md) | [Python](quickstarts\python.md)).</span><span class="sxs-lookup"><span data-stu-id="3b130-108">For examples that demonstrate uploading an image to get insights, see the quickstarts ([C#](quickstarts\csharp.md) | [Java](quickstarts\java.md) | [Node.js](quickstarts\nodejs.md) | [Python](quickstarts\python.md)).</span></span>


<span data-ttu-id="3b130-109">If you send Visual Search an image token or URL, the following shows the form data you must include in the body of the POST.</span><span class="sxs-lookup"><span data-stu-id="3b130-109">If you send Visual Search an image token or URL, the following shows the form data you must include in the body of the POST.</span></span> <span data-ttu-id="3b130-110">The form data must include the Content-Disposition header and its `name` parameter must be set to "knowledgeRequest".</span><span class="sxs-lookup"><span data-stu-id="3b130-110">The form data must include the Content-Disposition header and its `name` parameter must be set to "knowledgeRequest".</span></span> <span data-ttu-id="3b130-111">For details about the `imageInfo` object, see [The request](#the-request).</span><span class="sxs-lookup"><span data-stu-id="3b130-111">For details about the `imageInfo` object, see [The request](#the-request).</span></span>

```json
{
    "imageInfo" : {
        "url" : "",
        "imageInsightsToken" : "",
        "cropArea" : {
            "top" : 0.1,
            "left" : 0.5,
            "right" : 0.9,
            "bottom" : 0.9
        }
    },
    "knowledgeRequest" : {
      "filters" : {
        "site" : ""
      }
    }
}
```

<span data-ttu-id="3b130-112">The examples in this article show how to use the insights token.</span><span class="sxs-lookup"><span data-stu-id="3b130-112">The examples in this article show how to use the insights token.</span></span> <span data-ttu-id="3b130-113">You get the insights token from an Image object in an /images/search API response.</span><span class="sxs-lookup"><span data-stu-id="3b130-113">You get the insights token from an Image object in an /images/search API response.</span></span> <span data-ttu-id="3b130-114">For information about getting the insights token, see [Bing Image Search API](../Bing-Image-Search/overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b130-114">For information about getting the insights token, see [Bing Image Search API](../Bing-Image-Search/overview.md).</span></span>

```
--boundary_1234-abcd
Content-Disposition: form-data; name="knowledgeRequest"

{
    "imageInfo" : {
        "imageInsightsToken" : "ccid_tmaGQ2eU*mid_D12339146CFEDF3D40...",
    }
}

--boundary_1234-abcd--
```


<span data-ttu-id="3b130-115">For examples that use the insights token, see [C#](#using-csharp) | [Java](#using-java) | [Node.js](#using-nodejs) | [Python](#using-python).</span><span class="sxs-lookup"><span data-stu-id="3b130-115">For examples that use the insights token, see [C#](#using-csharp) | [Java](#using-java) | [Node.js](#using-nodejs) | [Python](#using-python).</span></span>

<a name="using-csharp" />

## <a name="using-c"></a><span data-ttu-id="3b130-116">Using C#</span><span class="sxs-lookup"><span data-stu-id="3b130-116">Using C#</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3b130-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b130-117">Prerequisites</span></span>

<span data-ttu-id="3b130-118">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to get this code running on Windows.</span><span class="sxs-lookup"><span data-stu-id="3b130-118">You will need [Visual Studio 2017](https://www.visualstudio.com/downloads/) to get this code running on Windows.</span></span> <span data-ttu-id="3b130-119">(The free Community Edition will work.)</span><span class="sxs-lookup"><span data-stu-id="3b130-119">(The free Community Edition will work.)</span></span>

<span data-ttu-id="3b130-120">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span><span class="sxs-lookup"><span data-stu-id="3b130-120">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="3b130-121">Running the application</span><span class="sxs-lookup"><span data-stu-id="3b130-121">Running the application</span></span>

<span data-ttu-id="3b130-122">To run this application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="3b130-122">To run this application, follow these steps:</span></span>

1. <span data-ttu-id="3b130-123">Create a new Console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b130-123">Create a new Console solution in Visual Studio.</span></span>
1. <span data-ttu-id="3b130-124">Replace the contents of `Program.cs` with the code shown in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="3b130-124">Replace the contents of `Program.cs` with the code shown in this quickstart.</span></span>
2. <span data-ttu-id="3b130-125">Replace the `accessKey` value with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="3b130-125">Replace the `accessKey` value with your subscription key.</span></span>
2. <span data-ttu-id="3b130-126">Replace the `insightsToken` value with an insights token from an /images/search response.</span><span class="sxs-lookup"><span data-stu-id="3b130-126">Replace the `insightsToken` value with an insights token from an /images/search response.</span></span>
3. <span data-ttu-id="3b130-127">Run the program.</span><span class="sxs-lookup"><span data-stu-id="3b130-127">Run the program.</span></span>

```csharp
using System;
using System.Text;
using System.Net;
using System.IO;
using System.Collections.Generic;
using System.Net.Http;
using System.Threading.Tasks;
using System.Threading;

namespace VisualSearchInsightsToken
{

    class Program
    {
        // Replace the accessKey string value with your valid subscription key.
        const string accessKey = "<yoursubscriptionkeygoeshere>";

        const string uriBase = "https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch";

        // Update with an insights token from an image object that the /images/search API endpoint returns.
        static string insightsToken = @"ccid_tmaGQ2eU*mid_D12339146CFEDF3D409CC7A66D2C98D0D71904D4*simid_608022145667564759*thid_OIP.tmaGQ2eUI1yq3yll!_jn9kwHaFZ";

        static string BoundaryTemplate = "batch_{0}";

        static void Main(string[] args)
        {
            try { 
                Console.WriteLine("Getting image insights using insights token: " + insightsToken);

                var knowledgeRequest = "{\"imageInfo\" : {\"imageInsightsToken\" : \"" + insightsToken + "\"}}";
                var boundary = string.Format(BoundaryTemplate, Guid.NewGuid());

                var json = BingVisualSearch(knowledgeRequest, boundary, uriBase, accessKey);

                Console.WriteLine("\nJSON Response:\n");
                Console.WriteLine(JsonPrettyPrint(json));

                Console.Write("\nPress Enter to exit ");
                Console.ReadLine();
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
            }

        }


        /// <summary>
        /// Calls the Bing visual search endpoint and returns the JSON response with insights.
        /// </summary>
        static string BingVisualSearch(string knowledgeRequest, string boundary, string uri, string subscriptionKey)
        {
            var requestMessage = new HttpRequestMessage(HttpMethod.Post, uri);
            requestMessage.Headers.Add("Ocp-Apim-Subscription-Key", accessKey);

            var content = new MultipartFormDataContent(boundary);
            content.Add(new StringContent(knowledgeRequest, Encoding.UTF8, "application/json"), "knowledgeRequest");
            requestMessage.Content = content;

            var httpClient = new HttpClient();

            Task<HttpResponseMessage> httpRequest = httpClient.SendAsync(requestMessage, HttpCompletionOption.ResponseContentRead, CancellationToken.None);
            HttpResponseMessage httpResponse = httpRequest.Result;
            HttpStatusCode statusCode = httpResponse.StatusCode;
            HttpContent responseContent = httpResponse.Content;

            string json = null;

            if (responseContent != null)
            {
                Task<String> stringContentsTask = responseContent.ReadAsStringAsync();
                json = stringContentsTask.Result;
            }


            return json;
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

<a name="using-java" />

## <a name="using-java"></a><span data-ttu-id="3b130-128">Using Java</span><span class="sxs-lookup"><span data-stu-id="3b130-128">Using Java</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3b130-129">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b130-129">Prerequisites</span></span>

<span data-ttu-id="3b130-130">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="3b130-130">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="3b130-131">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span><span class="sxs-lookup"><span data-stu-id="3b130-131">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span></span>

<span data-ttu-id="3b130-132">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span><span class="sxs-lookup"><span data-stu-id="3b130-132">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="3b130-133">Running the application</span><span class="sxs-lookup"><span data-stu-id="3b130-133">Running the application</span></span>

<span data-ttu-id="3b130-134">To run this application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="3b130-134">To run this application, follow these steps:</span></span>

1. <span data-ttu-id="3b130-135">Download or install the [gson library](https://github.com/google/gson).</span><span class="sxs-lookup"><span data-stu-id="3b130-135">Download or install the [gson library](https://github.com/google/gson).</span></span> <span data-ttu-id="3b130-136">You may also obtain it via Maven.</span><span class="sxs-lookup"><span data-stu-id="3b130-136">You may also obtain it via Maven.</span></span>
2. <span data-ttu-id="3b130-137">Create a new Java project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="3b130-137">Create a new Java project in your favorite IDE or editor.</span></span>
3. <span data-ttu-id="3b130-138">Add the provided code in a file named `VisualSearch.java`.</span><span class="sxs-lookup"><span data-stu-id="3b130-138">Add the provided code in a file named `VisualSearch.java`.</span></span>
4. <span data-ttu-id="3b130-139">Replace the `subscriptionKey` value with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="3b130-139">Replace the `subscriptionKey` value with your subscription key.</span></span>
5. <span data-ttu-id="3b130-140">Run the program.</span><span class="sxs-lookup"><span data-stu-id="3b130-140">Run the program.</span></span>

```java
package insightstoken;

import java.util.*;
import java.io.*;



/*
 * Gson: https://github.com/google/gson
 * Maven info:
 *     groupId: com.google.code.gson
 *     artifactId: gson
 *     version: 2.8.2
 *
 * Once you have compiled or downloaded gson-2.8.2.jar, assuming you have placed it in the
 * same folder as this file (BingImageSearch.java), you can compile and run this program at
 * the command line as follows.
 *
 * javac BingImageSearch.java -classpath .;gson-2.8.2.jar -encoding UTF-8
 * java -cp .;gson-2.8.2.jar BingImageSearch
 */

import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

// http://hc.apache.org/downloads.cgi (HttpComponents Downloads) HttpClient 4.5.5

import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.ContentType;
import org.apache.http.entity.mime.MultipartEntityBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClientBuilder;


public class InsightsToken {

    
    static String endpoint = "https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch";
    static String subscriptionKey = "<yoursubscriptionkeygoeshere>";

    // To get an insights, call the /images/search endpoint. Get the token from
    // the imageInsightsToken field in the Image object.
    static String insightsToken = "ccid_tmaGQ2eU*mid_D12339146CFEDF3D409CC7A66D2C98D0D71904D4*simid_608022145667564759*thid_OIP.tmaGQ2eUI1yq3yll!_jn9kwHaFZ";

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        CloseableHttpClient httpClient = HttpClientBuilder.create().build();
        
        String knowledgeRequest = "{\"imageInfo\" : {\"imageInsightsToken\" : \"" + insightsToken + "\"}}";

        try {
            HttpEntity entity = MultipartEntityBuilder
                .create()
                .addTextBody("knowledgeRequest", knowledgeRequest, ContentType.create("application/json"))
                .build();

            HttpPost httpPost = new HttpPost(endpoint);
            httpPost.setHeader("Ocp-Apim-Subscription-Key", subscriptionKey);
            httpPost.setEntity(entity);
            HttpResponse response = httpClient.execute(httpPost);

            InputStream stream = response.getEntity().getContent();
            String json = new Scanner(stream).useDelimiter("\\A").next();

            System.out.println("\nJSON Response:\n");
            System.out.println(prettify(json));
        }
        catch (IOException e)
        {
            e.printStackTrace(System.out);
            System.exit(1);
        }
        catch (Exception e) {
            e.printStackTrace(System.out);
            System.exit(1);
        }
    }
    
    // pretty-printer for JSON; uses GSON parser to parse and re-serialize
    public static String prettify(String json_text) {
        JsonParser parser = new JsonParser();
        JsonObject json = parser.parse(json_text).getAsJsonObject();
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        return gson.toJson(json);
    }

    
}
```


<a name="using-nodejs" />

## <a name="using-nodejs"></a><span data-ttu-id="3b130-141">Using Node.js</span><span class="sxs-lookup"><span data-stu-id="3b130-141">Using Node.js</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3b130-142">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b130-142">Prerequisites</span></span>

<span data-ttu-id="3b130-143">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="3b130-143">You need [Node.js 6](https://nodejs.org/en/download/) to run this code.</span></span>

<span data-ttu-id="3b130-144">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span><span class="sxs-lookup"><span data-stu-id="3b130-144">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="3b130-145">Running the application</span><span class="sxs-lookup"><span data-stu-id="3b130-145">Running the application</span></span>

<span data-ttu-id="3b130-146">To run this application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="3b130-146">To run this application, follow these steps:</span></span>

1. <span data-ttu-id="3b130-147">Create a folder for your project (or use your favorite IDE or editor).</span><span class="sxs-lookup"><span data-stu-id="3b130-147">Create a folder for your project (or use your favorite IDE or editor).</span></span>
2. <span data-ttu-id="3b130-148">From a command prompt or terminal, navigate to the folder you just created.</span><span class="sxs-lookup"><span data-stu-id="3b130-148">From a command prompt or terminal, navigate to the folder you just created.</span></span>
3. <span data-ttu-id="3b130-149">Install the request modules:</span><span class="sxs-lookup"><span data-stu-id="3b130-149">Install the request modules:</span></span>  
  ```  
  npm install request  
  ```  
3. <span data-ttu-id="3b130-150">Install the form-data modules:</span><span class="sxs-lookup"><span data-stu-id="3b130-150">Install the form-data modules:</span></span>  
  ```  
  npm install form-data  
  ```  
4. <span data-ttu-id="3b130-151">Create a file named GetVisualInsights.js and add the following code to it.</span><span class="sxs-lookup"><span data-stu-id="3b130-151">Create a file named GetVisualInsights.js and add the following code to it.</span></span>
5. <span data-ttu-id="3b130-152">Replace the `subscriptionKey` value with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="3b130-152">Replace the `subscriptionKey` value with your subscription key.</span></span>
7. <span data-ttu-id="3b130-153">Run the program.</span><span class="sxs-lookup"><span data-stu-id="3b130-153">Run the program.</span></span>  
  ```
  node GetVisualInsights.js
  ```

```javascript
var request = require('request');
var FormData = require('form-data');

var baseUri = 'https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch';
var subscriptionKey = '<yoursubscriptionkeygoeshere>';

// To get an insights, call the /images/search endpoint. Get the token from
// the imageInsightsToken field in the Image object.
var insightsToken = "ccid_tmaGQ2eU*mid_D12339146CFEDF3D409CC7A66D2C98D0D71904D4*simid_608022145667564759*thid_OIP.tmaGQ2eUI1yq3yll!_jn9kwHaFZ";

var knowledgeRequest = {
    "imageInfo" : {
        "imageInsightsToken" : insightsToken
    }
};

var form = new FormData();
form.append('knowledgeRequest', JSON.stringify(knowledgeRequest));

form.getLength(function(err, length){
  if (err) {
    return requestCallback(err);
  }

  var r = request.post(baseUri, requestCallback);
  r._form = form; 
  r.setHeader('Ocp-Apim-Subscription-Key', subscriptionKey);
});

function requestCallback(err, res, body) {
    console.log(JSON.stringify(JSON.parse(body), null, '  '))
}
```


<a name="using-python" />

## <a name="using-python"></a><span data-ttu-id="3b130-154">Using Python</span><span class="sxs-lookup"><span data-stu-id="3b130-154">Using Python</span></span>


### <a name="prerequisites"></a><span data-ttu-id="3b130-155">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3b130-155">Prerequisites</span></span>

<span data-ttu-id="3b130-156">You need [Python 3](https://www.python.org/) to run this code.</span><span class="sxs-lookup"><span data-stu-id="3b130-156">You need [Python 3](https://www.python.org/) to run this code.</span></span>

<span data-ttu-id="3b130-157">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span><span class="sxs-lookup"><span data-stu-id="3b130-157">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span></span>

## <a name="running-the-walkthrough"></a><span data-ttu-id="3b130-158">Running the walkthrough</span><span class="sxs-lookup"><span data-stu-id="3b130-158">Running the walkthrough</span></span>

<span data-ttu-id="3b130-159">To run this application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="3b130-159">To run this application, follow these steps:</span></span>

1. <span data-ttu-id="3b130-160">Create a new Python project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="3b130-160">Create a new Python project in your favorite IDE or editor.</span></span>
2. <span data-ttu-id="3b130-161">Create a file named visualsearch.py and add the code shown in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="3b130-161">Create a file named visualsearch.py and add the code shown in this quickstart.</span></span>
3. <span data-ttu-id="3b130-162">Replace the `SUBSCRIPTION_KEY` value with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="3b130-162">Replace the `SUBSCRIPTION_KEY` value with your subscription key.</span></span>
4. <span data-ttu-id="3b130-163">Run the program.</span><span class="sxs-lookup"><span data-stu-id="3b130-163">Run the program.</span></span>


```python
"""Bing Visual Search example"""

# Download and install Python at https://www.python.org/
# Run the following in a command console window
# pip3 install requests

import requests, json

BASE_URI = 'https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch'

SUBSCRIPTION_KEY = '<yoursubscriptionkeygoeshere>'

HEADERS = {'Ocp-Apim-Subscription-Key': SUBSCRIPTION_KEY}

# To get an insights, call the /images/search endpoint. Get the token from
# the imageInsightsToken field in the Image object.
insightsToken = 'ccid_tmaGQ2eU*mid_D12339146CFEDF3D409CC7A66D2C98D0D71904D4*simid_608022145667564759*thid_OIP.tmaGQ2eUI1yq3yll!_jn9kwHaFZ'

formData = '{"imageInfo":{"imageInsightsToken":"' + insightsToken + '"}}'


file = {'knowledgeRequest' : (None, formData)}

def main():
    
    try:
        response = requests.post(BASE_URI, headers=HEADERS, files=file)
        response.raise_for_status()
        print_json(response.json())

    except Exception as ex:
        raise ex


def print_json(obj):
    """Print the object as json"""
    print(json.dumps(obj, sort_keys=True, indent=2, separators=(',', ': ')))



# Main execution
if __name__ == '__main__':
    main()
```

## <a name="next-steps"></a><span data-ttu-id="3b130-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b130-164">Next steps</span></span>

[<span data-ttu-id="3b130-165">Bing Visual Search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="3b130-165">Bing Visual Search single-page app tutorial</span></span>](tutorial-bing-visual-search-single-page-app.md)  
[<span data-ttu-id="3b130-166">Bing Visual Search overview</span><span class="sxs-lookup"><span data-stu-id="3b130-166">Bing Visual Search overview</span></span>](overview.md)  
[<span data-ttu-id="3b130-167">Try it</span><span class="sxs-lookup"><span data-stu-id="3b130-167">Try it</span></span>](https://aka.ms/bingvisualsearchtryforfree)  
[<span data-ttu-id="3b130-168">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="3b130-168">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-visual-search-api)  
[<span data-ttu-id="3b130-169">Bing Visual Search API reference</span><span class="sxs-lookup"><span data-stu-id="3b130-169">Bing Visual Search API reference</span></span>](https://aka.ms/bingvisualsearchreferencedoc)
