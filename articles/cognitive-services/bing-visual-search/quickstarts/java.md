---
title: Java Quickstart for Bing Visual Search API | Microsoft Docs
titleSuffix: Bing Web Search APIs - Cognitive Services
description: Shows how to upload an image to Bing Visual Search API and get back insights about the image.
services: cognitive-services
author: swhite-msft
manager: rosh
ms.service: cognitive-services
ms.technology: bing-visual-search
ms.topic: article
ms.date: 5/16/2018
ms.author: scottwhi
ms.openlocfilehash: 41e0855b126ca6e54d0a487a88fe59a0be6f72f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871493"
---
# <a name="your-first-bing-visual-search-query-in-java"></a><span data-ttu-id="bbb77-103">Your first Bing Visual Search query in Java</span><span class="sxs-lookup"><span data-stu-id="bbb77-103">Your first Bing Visual Search query in Java</span></span>

<span data-ttu-id="bbb77-104">Bing Visual Search API returns information about an image that you provide.</span><span class="sxs-lookup"><span data-stu-id="bbb77-104">Bing Visual Search API returns information about an image that you provide.</span></span> <span data-ttu-id="bbb77-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span><span class="sxs-lookup"><span data-stu-id="bbb77-105">You can provide the image by using the URL of the image, an insights token, or by uploading an image.</span></span> <span data-ttu-id="bbb77-106">For information about these options, see [What is Bing Visual Search API?](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="bbb77-106">For information about these options, see [What is Bing Visual Search API?](../overview.md)</span></span> <span data-ttu-id="bbb77-107">This article demonstrates uploading an image.</span><span class="sxs-lookup"><span data-stu-id="bbb77-107">This article demonstrates uploading an image.</span></span> <span data-ttu-id="bbb77-108">Uploading an image could be useful in mobile scenarios where you take a picture of a well-known landmark and get back information about it.</span><span class="sxs-lookup"><span data-stu-id="bbb77-108">Uploading an image could be useful in mobile scenarios where you take a picture of a well-known landmark and get back information about it.</span></span> <span data-ttu-id="bbb77-109">For example, the insights could include trivia about the landmark.</span><span class="sxs-lookup"><span data-stu-id="bbb77-109">For example, the insights could include trivia about the landmark.</span></span> 

<span data-ttu-id="bbb77-110">If you upload a local image, the following shows the form data you must include in the body of the POST.</span><span class="sxs-lookup"><span data-stu-id="bbb77-110">If you upload a local image, the following shows the form data you must include in the body of the POST.</span></span> <span data-ttu-id="bbb77-111">The form data must include the Content-Disposition header.</span><span class="sxs-lookup"><span data-stu-id="bbb77-111">The form data must include the Content-Disposition header.</span></span> <span data-ttu-id="bbb77-112">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span><span class="sxs-lookup"><span data-stu-id="bbb77-112">Its `name` parameter must be set to "image" and the `filename` parameter may be set to any string.</span></span> <span data-ttu-id="bbb77-113">The contents of the form is the binary of the image.</span><span class="sxs-lookup"><span data-stu-id="bbb77-113">The contents of the form is the binary of the image.</span></span> <span data-ttu-id="bbb77-114">The maximum image size you may upload is 1 MB.</span><span class="sxs-lookup"><span data-stu-id="bbb77-114">The maximum image size you may upload is 1 MB.</span></span> 

```
--boundary_1234-abcd
Content-Disposition: form-data; name="image"; filename="myimagefile.jpg"

ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...

--boundary_1234-abcd--
```

<span data-ttu-id="bbb77-115">This article includes a simple console application that sends a Bing Visual Search API request and displays the JSON search results.</span><span class="sxs-lookup"><span data-stu-id="bbb77-115">This article includes a simple console application that sends a Bing Visual Search API request and displays the JSON search results.</span></span> <span data-ttu-id="bbb77-116">While this application is written in Java, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span><span class="sxs-lookup"><span data-stu-id="bbb77-116">While this application is written in Java, the API is a RESTful Web service compatible with any programming language that can make HTTP requests and parse JSON.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="bbb77-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bbb77-117">Prerequisites</span></span>

<span data-ttu-id="bbb77-118">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span><span class="sxs-lookup"><span data-stu-id="bbb77-118">You will need [JDK 7 or 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to compile and run this code.</span></span> <span data-ttu-id="bbb77-119">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span><span class="sxs-lookup"><span data-stu-id="bbb77-119">You may use a Java IDE if you have a favorite, but a text editor will suffice.</span></span>

<span data-ttu-id="bbb77-120">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span><span class="sxs-lookup"><span data-stu-id="bbb77-120">For this quickstart, you may use a [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) subscription key or a paid subscription key.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="bbb77-121">Running the application</span><span class="sxs-lookup"><span data-stu-id="bbb77-121">Running the application</span></span>

<span data-ttu-id="bbb77-122">The following shows how to upload the image using MultipartEntityBuilder in Java.</span><span class="sxs-lookup"><span data-stu-id="bbb77-122">The following shows how to upload the image using MultipartEntityBuilder in Java.</span></span>

<span data-ttu-id="bbb77-123">To run this application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="bbb77-123">To run this application, follow these steps:</span></span>

1. <span data-ttu-id="bbb77-124">Download or install the [gson library](https://github.com/google/gson).</span><span class="sxs-lookup"><span data-stu-id="bbb77-124">Download or install the [gson library](https://github.com/google/gson).</span></span> <span data-ttu-id="bbb77-125">You may also obtain it via Maven.</span><span class="sxs-lookup"><span data-stu-id="bbb77-125">You may also obtain it via Maven.</span></span>
2. <span data-ttu-id="bbb77-126">Create a new Java project in your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="bbb77-126">Create a new Java project in your favorite IDE or editor.</span></span>
3. <span data-ttu-id="bbb77-127">Add the provided code in a file named `VisualSearch.java`.</span><span class="sxs-lookup"><span data-stu-id="bbb77-127">Add the provided code in a file named `VisualSearch.java`.</span></span>
4. <span data-ttu-id="bbb77-128">Replace the `subscriptionKey` value with your subscription key.</span><span class="sxs-lookup"><span data-stu-id="bbb77-128">Replace the `subscriptionKey` value with your subscription key.</span></span>
4. <span data-ttu-id="bbb77-129">Replace the `imagePath` value with the path of the image to upload.</span><span class="sxs-lookup"><span data-stu-id="bbb77-129">Replace the `imagePath` value with the path of the image to upload.</span></span>
5. <span data-ttu-id="bbb77-130">Run the program.</span><span class="sxs-lookup"><span data-stu-id="bbb77-130">Run the program.</span></span>


```java
package uploadimage;

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


public class UploadImage2 {

    static String endpoint = "https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch";
    static String subscriptionKey = "<yoursubscriptionkeygoeshere";
    static String imagePath = "<pathtoyourimagetouploadgoeshere>";

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        
        CloseableHttpClient httpClient = HttpClientBuilder.create().build();
        
        try {
            HttpEntity entity = MultipartEntityBuilder
                .create()
                .addBinaryBody("image", new File(imagePath))
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

## <a name="next-steps"></a><span data-ttu-id="bbb77-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="bbb77-131">Next steps</span></span>

[<span data-ttu-id="bbb77-132">Get insights about an image using an insights token</span><span class="sxs-lookup"><span data-stu-id="bbb77-132">Get insights about an image using an insights token</span></span>](../use-insights-token.md)  
<span data-ttu-id="bbb77-133">[Bing Visual Search image upload tutorial](../tutorial-visual-search-image-upload.md)
[Bing Visual Search single-page app tutorial](../tutorial-bing-visual-search-single-page-app.md)</span><span class="sxs-lookup"><span data-stu-id="bbb77-133">[Bing Visual Search image upload tutorial](../tutorial-visual-search-image-upload.md)
[Bing Visual Search single-page app tutorial](../tutorial-bing-visual-search-single-page-app.md)</span></span>  
[<span data-ttu-id="bbb77-134">Bing Visual Search overview</span><span class="sxs-lookup"><span data-stu-id="bbb77-134">Bing Visual Search overview</span></span>](../overview.md)  
[<span data-ttu-id="bbb77-135">Try it</span><span class="sxs-lookup"><span data-stu-id="bbb77-135">Try it</span></span>](https://aka.ms/bingvisualsearchtryforfree)  
[<span data-ttu-id="bbb77-136">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="bbb77-136">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-visual-search-api)  
[<span data-ttu-id="bbb77-137">Bing Visual Search API reference</span><span class="sxs-lookup"><span data-stu-id="bbb77-137">Bing Visual Search API reference</span></span>](https://aka.ms/bingvisualsearchreferencedoc)

