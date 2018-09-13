---
title: 'Quickstart: Use the Bing Web Search SDK for Java'
description: Learn to use the Bing Web Search SDK for Java.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 08/22/2018
ms.author: erhopf
ms.openlocfilehash: cc7335b9f8b5596edef895ff5a42a1018b06a381
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868852"
---
# <a name="quickstart-use-the-bing-web-search-sdk-for-java"></a><span data-ttu-id="3cae1-103">Quickstart: Use the Bing Web Search SDK for Java</span><span class="sxs-lookup"><span data-stu-id="3cae1-103">Quickstart: Use the Bing Web Search SDK for Java</span></span>

<span data-ttu-id="3cae1-104">The Bing Web Search SDK makes it easy to integrate Bing Web Search into your Java application.</span><span class="sxs-lookup"><span data-stu-id="3cae1-104">The Bing Web Search SDK makes it easy to integrate Bing Web Search into your Java application.</span></span> <span data-ttu-id="3cae1-105">In this quickstart, you'll learn how to send a request, receive a JSON response, and filter and parse the results.</span><span class="sxs-lookup"><span data-stu-id="3cae1-105">In this quickstart, you'll learn how to send a request, receive a JSON response, and filter and parse the results.</span></span>

<span data-ttu-id="3cae1-106">Want to see the code right now?</span><span class="sxs-lookup"><span data-stu-id="3cae1-106">Want to see the code right now?</span></span> <span data-ttu-id="3cae1-107">The [Bing Web Search SDK for Java samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/) are available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="3cae1-107">The [Bing Web Search SDK for Java samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/) are available on GitHub.</span></span>

[!INCLUDE [bing-web-search-quickstart-signup](../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a><span data-ttu-id="3cae1-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3cae1-108">Prerequisites</span></span>

<span data-ttu-id="3cae1-109">Here are a few things that you'll need before running this quickstart:</span><span class="sxs-lookup"><span data-stu-id="3cae1-109">Here are a few things that you'll need before running this quickstart:</span></span>

* [<span data-ttu-id="3cae1-110">JDK 7 or 8</span><span class="sxs-lookup"><span data-stu-id="3cae1-110">JDK 7 or 8</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* <span data-ttu-id="3cae1-111">[Apache Maven](https://maven.apache.org/download.cgi) or your favorite build automation tool</span><span class="sxs-lookup"><span data-stu-id="3cae1-111">[Apache Maven](https://maven.apache.org/download.cgi) or your favorite build automation tool</span></span>
* <span data-ttu-id="3cae1-112">A subscription key</span><span class="sxs-lookup"><span data-stu-id="3cae1-112">A subscription key</span></span>

## <a name="create-a-project-and-configure-your-pom-file"></a><span data-ttu-id="3cae1-113">Create a project and configure your POM file</span><span class="sxs-lookup"><span data-stu-id="3cae1-113">Create a project and configure your POM file</span></span>

<span data-ttu-id="3cae1-114">Create a new Java project using Maven or your favorite build automation tool.</span><span class="sxs-lookup"><span data-stu-id="3cae1-114">Create a new Java project using Maven or your favorite build automation tool.</span></span> <span data-ttu-id="3cae1-115">Assuming that you're using Maven, add the following lines to your POM file.</span><span class="sxs-lookup"><span data-stu-id="3cae1-115">Assuming that you're using Maven, add the following lines to your POM file.</span></span> <span data-ttu-id="3cae1-116">Replace all instances of `mainClass` with your application.</span><span class="sxs-lookup"><span data-stu-id="3cae1-116">Replace all instances of `mainClass` with your application.</span></span>

```xml
<build>
    <plugins>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>1.4.0</version>
        <configuration>
          <!--Your comment
            Replace the mainClass with the path to your java application.
            It should begin with com and doesn't require the .java extension.
            For example: com.bingwebsearch.app.BingWebSearchSample. This maps to
            The following directory structure:
            src/main/java/com/bingwebsearch/app/BingWebSearchSample.java.
          -->
          <mainClass>com.path.to.your.app.APP_NAME</mainClass>
        </configuration>
      </plugin>
      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.0</version>
        <configuration>
          <source>1.7</source>
          <target>1.7</target>
        </configuration>
      </plugin>
      <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>attached</goal>
            </goals>
            <configuration>
              <descriptorRefs>
                <descriptorRef>jar-with-dependencies</descriptorRef>
              </descriptorRefs>
              <archive>
                <manifest>
                  <!--Your comment
                    Replace the mainClass with the path to your java application.
                    For example: com.bingwebsearch.app.BingWebSearchSample.java.
                    This maps to the following directory structure:
                    src/main/java/com/bingwebsearch/app/BingWebSearchSample.java.
                  -->
                  <mainClass>com.path.to.your.app.APP_NAME.java</mainClass>
                </manifest>
              </archive>
            </configuration>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.9.0</version>
    </dependency>
    <dependency>
      <groupId>commons-net</groupId>
      <artifactId>commons-net</artifactId>
      <version>3.3</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure.cognitiveservices</groupId>
      <artifactId>azure-cognitiveservices-websearch</artifactId>
      <version>1.0.1</version>
    </dependency>
  </dependencies>
```

## <a name="declare-dependencies"></a><span data-ttu-id="3cae1-117">Declare dependencies</span><span class="sxs-lookup"><span data-stu-id="3cae1-117">Declare dependencies</span></span>

<span data-ttu-id="3cae1-118">Open your project in your favorite IDE or editor and import these dependencies:</span><span class="sxs-lookup"><span data-stu-id="3cae1-118">Open your project in your favorite IDE or editor and import these dependencies:</span></span>

```java
import com.microsoft.azure.cognitiveservices.search.websearch.BingWebSearchAPI;
import com.microsoft.azure.cognitiveservices.search.websearch.BingWebSearchManager;
import com.microsoft.azure.cognitiveservices.search.websearch.models.ImageObject;
import com.microsoft.azure.cognitiveservices.search.websearch.models.NewsArticle;
import com.microsoft.azure.cognitiveservices.search.websearch.models.SearchResponse;
import com.microsoft.azure.cognitiveservices.search.websearch.models.VideoObject;
import com.microsoft.azure.cognitiveservices.search.websearch.models.WebPage;
```

<span data-ttu-id="3cae1-119">If you created the project with Maven, the package should already be declared.</span><span class="sxs-lookup"><span data-stu-id="3cae1-119">If you created the project with Maven, the package should already be declared.</span></span> <span data-ttu-id="3cae1-120">Otherwise, declare the package now.</span><span class="sxs-lookup"><span data-stu-id="3cae1-120">Otherwise, declare the package now.</span></span> <span data-ttu-id="3cae1-121">For example:</span><span class="sxs-lookup"><span data-stu-id="3cae1-121">For example:</span></span>

```java
package com.bingwebsearch.app
```

## <a name="declare-the-bingwebsearchsample-class"></a><span data-ttu-id="3cae1-122">Declare the BingWebSearchSample class</span><span class="sxs-lookup"><span data-stu-id="3cae1-122">Declare the BingWebSearchSample class</span></span>

<span data-ttu-id="3cae1-123">Declare the `BingWebSearchSample` class.</span><span class="sxs-lookup"><span data-stu-id="3cae1-123">Declare the `BingWebSearchSample` class.</span></span> <span data-ttu-id="3cae1-124">It will include most of our code including the `main` method.</span><span class="sxs-lookup"><span data-stu-id="3cae1-124">It will include most of our code including the `main` method.</span></span>  

```java
public class BingWebSearchSample {

// The code in the following sections goes here.

}
```

## <a name="construct-a-request"></a><span data-ttu-id="3cae1-125">Construct a request</span><span class="sxs-lookup"><span data-stu-id="3cae1-125">Construct a request</span></span>

<span data-ttu-id="3cae1-126">The `runSample` method, which lives in the `BingWebSearchSample` class, constructs the request.</span><span class="sxs-lookup"><span data-stu-id="3cae1-126">The `runSample` method, which lives in the `BingWebSearchSample` class, constructs the request.</span></span> <span data-ttu-id="3cae1-127">Copy this code into your application:</span><span class="sxs-lookup"><span data-stu-id="3cae1-127">Copy this code into your application:</span></span>

```java
public static boolean runSample(BingWebSearchAPI client) {
    /*
     * This function performs the search.
     *
     * @param client instance of the Bing Web Search API client
     * @return true if sample runs successfully
     */
    try {
        /*
         * Performs a search based on the .withQuery and prints the name and
         * url for the first web pages, image, news, and video result
         * included in the response.
         */
        System.out.println("Searched Web for \"Xbox\"");
        // Construct the request.
        SearchResponse webData = client.bingWebs().search()
            .withQuery("Xbox")
            .withMarket("en-us")
            .withCount(10)
            .execute();

// Code continues in the next section...
```

## <a name="handle-the-response"></a><span data-ttu-id="3cae1-128">Handle the response</span><span class="sxs-lookup"><span data-stu-id="3cae1-128">Handle the response</span></span>

<span data-ttu-id="3cae1-129">Next, let's add some code to parse the response and print the results.</span><span class="sxs-lookup"><span data-stu-id="3cae1-129">Next, let's add some code to parse the response and print the results.</span></span> <span data-ttu-id="3cae1-130">The `name` and `url` for the first web page, image, news article, and video are printed when included in the response object.</span><span class="sxs-lookup"><span data-stu-id="3cae1-130">The `name` and `url` for the first web page, image, news article, and video are printed when included in the response object.</span></span>

```java
/*
* WebPages
* If the search response contains web pages, the first result's name
* and url are printed.
*/
if (webData != null && webData.webPages() != null && webData.webPages().value() != null &&
        webData.webPages().value().size() > 0) {
    // find the first web page
    WebPage firstWebPagesResult = webData.webPages().value().get(0);

    if (firstWebPagesResult != null) {
        System.out.println(String.format("Webpage Results#%d", webData.webPages().value().size()));
        System.out.println(String.format("First web page name: %s ", firstWebPagesResult.name()));
        System.out.println(String.format("First web page URL: %s ", firstWebPagesResult.url()));
    } else {
        System.out.println("Couldn't find the first web result!");
    }
} else {
    System.out.println("Didn't find any web pages...");
}
/*
 * Images
 * If the search response contains images, the first result's name
 * and url are printed.
 */
if (webData != null && webData.images() != null && webData.images().value() != null &&
        webData.images().value().size() > 0) {
    // find the first image result
    ImageObject firstImageResult = webData.images().value().get(0);

    if (firstImageResult != null) {
        System.out.println(String.format("Image Results#%d", webData.images().value().size()));
        System.out.println(String.format("First Image result name: %s ", firstImageResult.name()));
        System.out.println(String.format("First Image result URL: %s ", firstImageResult.contentUrl()));
    } else {
        System.out.println("Couldn't find the first image result!");
    }
} else {
    System.out.println("Didn't find any images...");
}
/*
 * News
 * If the search response contains news articles, the first result's name
 * and url are printed.
 */
if (webData != null && webData.news() != null && webData.news().value() != null &&
        webData.news().value().size() > 0) {
    // find the first news result
    NewsArticle firstNewsResult = webData.news().value().get(0);
    if (firstNewsResult != null) {
        System.out.println(String.format("News Results#%d", webData.news().value().size()));
        System.out.println(String.format("First news result name: %s ", firstNewsResult.name()));
        System.out.println(String.format("First news result URL: %s ", firstNewsResult.url()));
    } else {
        System.out.println("Couldn't find the first news result!");
    }
} else {
    System.out.println("Didn't find any news articles...");
}

/*
 * Videos
 * If the search response contains videos, the first result's name
 * and url are printed.
 */
if (webData != null && webData.videos() != null && webData.videos().value() != null &&
        webData.videos().value().size() > 0) {
    // find the first video result
    VideoObject firstVideoResult = webData.videos().value().get(0);

    if (firstVideoResult != null) {
        System.out.println(String.format("Video Results#%s", webData.videos().value().size()));
        System.out.println(String.format("First Video result name: %s ", firstVideoResult.name()));
        System.out.println(String.format("First Video result URL: %s ", firstVideoResult.contentUrl()));
    } else {
        System.out.println("Couldn't find the first video result!");
    }
} else {
    System.out.println("Didn't find any videos...");
}
```

## <a name="declare-the-main-method"></a><span data-ttu-id="3cae1-131">Declare the main method</span><span class="sxs-lookup"><span data-stu-id="3cae1-131">Declare the main method</span></span>

<span data-ttu-id="3cae1-132">In this application, the main method includes code that instantiates the client, validates the `subscriptionKey`, and calls `runSample`.</span><span class="sxs-lookup"><span data-stu-id="3cae1-132">In this application, the main method includes code that instantiates the client, validates the `subscriptionKey`, and calls `runSample`.</span></span> <span data-ttu-id="3cae1-133">Make sure that you enter a valid subscription key for your Azure account before continuing.</span><span class="sxs-lookup"><span data-stu-id="3cae1-133">Make sure that you enter a valid subscription key for your Azure account before continuing.</span></span>

```java
public static void main(String[] args) {
    try {
        // Enter a valid subscription key for your account.
        final String subscriptionKey = "YOUR_SUBSCRIPTION_KEY";
        // Instantiate the client.
        BingWebSearchAPI client = BingWebSearchManager.authenticate(subscriptionKey);
        // Make a call to the Bing Web Search API.
        runSample(client);
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }
}
```

## <a name="run-the-program"></a><span data-ttu-id="3cae1-134">Run the program</span><span class="sxs-lookup"><span data-stu-id="3cae1-134">Run the program</span></span>

<span data-ttu-id="3cae1-135">The final step is to run your program!</span><span class="sxs-lookup"><span data-stu-id="3cae1-135">The final step is to run your program!</span></span>

```console
mvn compile exec:java
```

## <a name="clean-up-resources"></a><span data-ttu-id="3cae1-136">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="3cae1-136">Clean up resources</span></span>

<span data-ttu-id="3cae1-137">When you're done with this project, make sure to remove your subscription key from the program's code.</span><span class="sxs-lookup"><span data-stu-id="3cae1-137">When you're done with this project, make sure to remove your subscription key from the program's code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cae1-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="3cae1-138">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cae1-139">Cognitive Services Java SDK samples</span><span class="sxs-lookup"><span data-stu-id="3cae1-139">Cognitive Services Java SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingWebSearch)

## <a name="see-also"></a><span data-ttu-id="3cae1-140">See also</span><span class="sxs-lookup"><span data-stu-id="3cae1-140">See also</span></span>

* [<span data-ttu-id="3cae1-141">Azure Java SDK reference</span><span class="sxs-lookup"><span data-stu-id="3cae1-141">Azure Java SDK reference</span></span>](https://docs.microsoft.com/java/api/overview/azure/cognitiveservices/client/websearch)
