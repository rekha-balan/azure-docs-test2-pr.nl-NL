---
title: 'Quickstart: Analyze a remote image - REST, Java - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze an image using Computer Vision with Java in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 675efa80bd32fa841713f7aecd249bd6d457d9a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858108"
---
# <a name="quickstart-analyze-a-remote-image---rest-java---computer-vision"></a><span data-ttu-id="d1e24-103">Quickstart: Analyze a remote image - REST, Java - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="d1e24-103">Quickstart: Analyze a remote image - REST, Java - Computer Vision</span></span>

<span data-ttu-id="d1e24-104">In this quickstart, you analyze an image to extract visual features using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="d1e24-104">In this quickstart, you analyze an image to extract visual features using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1e24-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d1e24-105">Prerequisites</span></span>

<span data-ttu-id="d1e24-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="d1e24-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="analyze-image-request"></a><span data-ttu-id="d1e24-107">Analyze Image request</span><span class="sxs-lookup"><span data-stu-id="d1e24-107">Analyze Image request</span></span>

<span data-ttu-id="d1e24-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="d1e24-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="d1e24-109">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="d1e24-109">You can upload an image or specify an image URL and choose which features to return, including:</span></span>

* <span data-ttu-id="d1e24-110">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="d1e24-110">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="d1e24-111">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="d1e24-111">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="d1e24-112">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="d1e24-112">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="d1e24-113">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="d1e24-113">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="d1e24-114">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="d1e24-114">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="d1e24-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="d1e24-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span>
* <span data-ttu-id="d1e24-116">Does the image contain adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="d1e24-116">Does the image contain adult or sexually suggestive content?</span></span>

<span data-ttu-id="d1e24-117">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="d1e24-117">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="d1e24-118">Create a new command-line app.</span><span class="sxs-lookup"><span data-stu-id="d1e24-118">Create a new command-line app.</span></span>
1. <span data-ttu-id="d1e24-119">Replace the Main class with the following code (keep any `package` statements).</span><span class="sxs-lookup"><span data-stu-id="d1e24-119">Replace the Main class with the following code (keep any `package` statements).</span></span>
1. <span data-ttu-id="d1e24-120">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="d1e24-120">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="d1e24-121">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="d1e24-121">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="d1e24-122">Optionally, change the `imageToAnalyze` value to another image.</span><span class="sxs-lookup"><span data-stu-id="d1e24-122">Optionally, change the `imageToAnalyze` value to another image.</span></span>
1. <span data-ttu-id="d1e24-123">Download these libraries from the Maven Repository to the `lib` directory in your project:</span><span class="sxs-lookup"><span data-stu-id="d1e24-123">Download these libraries from the Maven Repository to the `lib` directory in your project:</span></span>
   * `org.apache.httpcomponents:httpclient:4.5.5`
   * `org.apache.httpcomponents:httpcore:4.4.9`
   * `org.json:json:20180130`
1. <span data-ttu-id="d1e24-124">Run 'Main'.</span><span class="sxs-lookup"><span data-stu-id="d1e24-124">Run 'Main'.</span></span>

```java
// This sample uses the following libraries:
//  - Apache HTTP client (org.apache.httpcomponents:httpclient:4.5.5)
//  - Apache HTTP core (org.apache.httpcomponents:httpccore:4.4.9)
//  - JSON library (org.json:json:20180130).

import java.net.URI;

import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClientBuilder;
import org.apache.http.util.EntityUtils;
import org.json.JSONObject;

public class Main {
    // **********************************************
    // *** Update or verify the following values. ***
    // **********************************************

    // Replace <Subscription Key> with your valid subscription key.
    private static final String subscriptionKey = "<Subscription Key>";

    // You must use the same region in your REST call as you used to get your
    // subscription keys. For example, if you got your subscription keys from
    // westus, replace "westcentralus" in the URI below with "westus".
    //
    // Free trial subscription keys are generated in the westcentralus region. If you
    // use a free trial subscription key, you shouldn't need to change this region.
    private static final String uriBase =
            "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/analyze";

    private static final String imageToAnalyze =
            "https://upload.wikimedia.org/wikipedia/commons/" +
                    "1/12/Broadway_and_Times_Square_by_night.jpg";

    public static void main(String[] args) {
        CloseableHttpClient httpClient = HttpClientBuilder.create().build();

        try {
            URIBuilder builder = new URIBuilder(uriBase);

            // Request parameters. All of them are optional.
            builder.setParameter("visualFeatures", "Categories,Description,Color");
            builder.setParameter("language", "en");

            // Prepare the URI for the REST API call.
            URI uri = builder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKey);

            // Request body.
            StringEntity requestEntity =
                    new StringEntity("{\"url\":\"" + imageToAnalyze + "\"}");
            request.setEntity(requestEntity);

            // Make the REST API call and get the response entity.
            HttpResponse response = httpClient.execute(request);
            HttpEntity entity = response.getEntity();

            if (entity != null) {
                // Format and display the JSON response.
                String jsonString = EntityUtils.toString(entity);
                JSONObject json = new JSONObject(jsonString);
                System.out.println("REST Response:\n");
                System.out.println(json.toString(2));
            }
        } catch (Exception e) {
            // Display error message.
            System.out.println(e.getMessage());
        }
    }
}
```

## <a name="analyze-image-response"></a><span data-ttu-id="d1e24-125">Analyze Image response</span><span class="sxs-lookup"><span data-stu-id="d1e24-125">Analyze Image response</span></span>

<span data-ttu-id="d1e24-126">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="d1e24-126">A successful response is returned in JSON, for example:</span></span>

```json
REST Response:

{
  "metadata": {
    "width": 1826,
    "format": "Jpeg",
    "height": 2436
  },
  "color": {
    "dominantColorForeground": "Brown",
    "isBWImg": false,
    "accentColor": "B74314",
    "dominantColorBackground": "Brown",
    "dominantColors": ["Brown"]
  },
  "requestId": "bbffe1a1-4fa3-4a6b-a4d5-a4964c58a811",
  "description": {
    "captions": [{
      "confidence": 0.8241405091548035,
      "text": "a group of people on a city street filled with traffic at night"
    }],
    "tags": [
      "outdoor",
      "building",
      "street",
      "city",
      "busy",
      "people",
      "filled",
      "traffic",
      "many",
      "table",
      "car",
      "group",
      "walking",
      "bunch",
      "crowded",
      "large",
      "night",
      "light",
      "standing",
      "man",
      "tall",
      "umbrella",
      "riding",
      "sign",
      "crowd"
    ]
  },
  "categories": [{
    "score": 0.625,
    "name": "outdoor_street"
  }]
}
```

## <a name="next-steps"></a><span data-ttu-id="d1e24-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1e24-127">Next steps</span></span>

<span data-ttu-id="d1e24-128">Explore a Java Swing application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="d1e24-128">Explore a Java Swing application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="d1e24-129">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="d1e24-129">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1e24-130">Computer Vision API Java Tutorial</span><span class="sxs-lookup"><span data-stu-id="d1e24-130">Computer Vision API Java Tutorial</span></span>](../Tutorials/java-tutorial.md)
