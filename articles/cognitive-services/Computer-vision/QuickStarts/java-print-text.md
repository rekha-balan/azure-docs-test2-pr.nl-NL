---
title: 'Quickstart: Extract printed text (OCR) - REST, Java - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you extract printed text from an image using Computer Vision with Java in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 4fcdf6254fc3623f89dd44b3c5537e78255b6a33
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864933"
---
# <a name="quickstart-extract-printed-text-ocr---rest-java---computer-vision"></a><span data-ttu-id="5940b-103">Quickstart: Extract printed text (OCR) - REST, Java - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="5940b-103">Quickstart: Extract printed text (OCR) - REST, Java - Computer Vision</span></span>

<span data-ttu-id="5940b-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="5940b-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5940b-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5940b-105">Prerequisites</span></span>

<span data-ttu-id="5940b-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="5940b-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="ocr-request"></a><span data-ttu-id="5940b-107">OCR request</span><span class="sxs-lookup"><span data-stu-id="5940b-107">OCR request</span></span>

<span data-ttu-id="5940b-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="5940b-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

<span data-ttu-id="5940b-109">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="5940b-109">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="5940b-110">Create a new command-line app.</span><span class="sxs-lookup"><span data-stu-id="5940b-110">Create a new command-line app.</span></span>
1. <span data-ttu-id="5940b-111">Replace the Main class with the following code (keep any `package` statements).</span><span class="sxs-lookup"><span data-stu-id="5940b-111">Replace the Main class with the following code (keep any `package` statements).</span></span>
1. <span data-ttu-id="5940b-112">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="5940b-112">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="5940b-113">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="5940b-113">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="5940b-114">Optionally, change the `imageToAnalyze` value to another image.</span><span class="sxs-lookup"><span data-stu-id="5940b-114">Optionally, change the `imageToAnalyze` value to another image.</span></span>
1. <span data-ttu-id="5940b-115">Download these libraries from the Maven Repository to the `lib` directory in your project:</span><span class="sxs-lookup"><span data-stu-id="5940b-115">Download these libraries from the Maven Repository to the `lib` directory in your project:</span></span>
   * `org.apache.httpcomponents:httpclient:4.5.5`
   * `org.apache.httpcomponents:httpcore:4.4.9`
   * `org.json:json:20180130`
1. <span data-ttu-id="5940b-116">Run 'Main'.</span><span class="sxs-lookup"><span data-stu-id="5940b-116">Run 'Main'.</span></span>

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
            "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/ocr";

    private static final String imageToAnalyze =
        "https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/" +
            "Atomist_quote_from_Democritus.png/338px-Atomist_quote_from_Democritus.png";

    public static void main(String[] args) {
        CloseableHttpClient httpClient = HttpClientBuilder.create().build();

        try {
            URIBuilder uriBuilder = new URIBuilder(uriBase);

            uriBuilder.setParameter("language", "unk");
            uriBuilder.setParameter("detectOrientation", "true");

            // Request parameters.
            URI uri = uriBuilder.build();
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

## <a name="ocr-response"></a><span data-ttu-id="5940b-117">OCR response</span><span class="sxs-lookup"><span data-stu-id="5940b-117">OCR response</span></span>

<span data-ttu-id="5940b-118">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="5940b-118">A successful response is returned in JSON.</span></span> <span data-ttu-id="5940b-119">The OCR results include the detected text and bounding boxes for regions, lines, and words.</span><span class="sxs-lookup"><span data-stu-id="5940b-119">The OCR results include the detected text and bounding boxes for regions, lines, and words.</span></span>

<span data-ttu-id="5940b-120">The program should produce output similar to the following JSON:</span><span class="sxs-lookup"><span data-stu-id="5940b-120">The program should produce output similar to the following JSON:</span></span>

```json
REST Response:

{
  "orientation": "Up",
  "regions": [{
    "boundingBox": "21,16,304,451",
    "lines": [
      {
        "boundingBox": "28,16,288,41",
        "words": [{
          "boundingBox": "28,16,288,41",
          "text": "NOTHING"
        }]
      },
      {
        "boundingBox": "27,66,283,52",
        "words": [{
          "boundingBox": "27,66,283,52",
          "text": "EXISTS"
        }]
      },
      {
        "boundingBox": "27,128,292,49",
        "words": [{
          "boundingBox": "27,128,292,49",
          "text": "EXCEPT"
        }]
      },
      {
        "boundingBox": "24,188,292,54",
        "words": [{
          "boundingBox": "24,188,292,54",
          "text": "ATOMS"
        }]
      },
      {
        "boundingBox": "22,253,297,32",
        "words": [
          {
            "boundingBox": "22,253,105,32",
            "text": "AND"
          },
          {
            "boundingBox": "144,253,175,32",
            "text": "EMPTY"
          }
        ]
      },
      {
        "boundingBox": "21,298,304,60",
        "words": [{
          "boundingBox": "21,298,304,60",
          "text": "SPACE."
        }]
      },
      {
        "boundingBox": "26,387,294,37",
        "words": [
          {
            "boundingBox": "26,387,210,37",
            "text": "Everything"
          },
          {
            "boundingBox": "249,389,71,27",
            "text": "else"
          }
        ]
      },
      {
        "boundingBox": "127,431,198,36",
        "words": [
          {
            "boundingBox": "127,431,31,29",
            "text": "is"
          },
          {
            "boundingBox": "172,431,153,36",
            "text": "opinion."
          }
        ]
      }
    ]
  }],
  "textAngle": 0,
  "language": "en"
}
```

## <a name="next-steps"></a><span data-ttu-id="5940b-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="5940b-121">Next steps</span></span>

<span data-ttu-id="5940b-122">Explore a Java Swing application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="5940b-122">Explore a Java Swing application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="5940b-123">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="5940b-123">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5940b-124">Computer Vision API Java Tutorial</span><span class="sxs-lookup"><span data-stu-id="5940b-124">Computer Vision API Java Tutorial</span></span>](../Tutorials/java-tutorial.md)
