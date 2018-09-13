---
title: Emotion API Java for Android quick start | Microsoft Docs
description: Get information and a code sample to help you quickly get started using the Emotion API with Java for Android in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 03/02/2017
ms.author: anroth
ms.openlocfilehash: c5d38d881624e956b897cbc993f8a4622de3e324
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550707"
---
# <a name="emotion-api-java-for-android-quick-start"></a><span data-ttu-id="31cc6-103">Emotion API Java for Android Quick Start</span><span class="sxs-lookup"><span data-stu-id="31cc6-103">Emotion API Java for Android Quick Start</span></span>
<span data-ttu-id="31cc6-104">This article provides information and a code sample to help you quickly get started with the [Emotion Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) in the Emotion API Android client library.</span><span class="sxs-lookup"><span data-stu-id="31cc6-104">This article provides information and a code sample to help you quickly get started with the [Emotion Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) in the Emotion API Android client library.</span></span> <span data-ttu-id="31cc6-105">The sample demonstrates how you can use Java to recognize the emotions expressed by people.</span><span class="sxs-lookup"><span data-stu-id="31cc6-105">The sample demonstrates how you can use Java to recognize the emotions expressed by people.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="31cc6-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31cc6-106">Prerequisites</span></span>
* <span data-ttu-id="31cc6-107">Get the Emotion API Java for Android SDK [here](https://github.com/Microsoft/Cognitive-emotion-android)</span><span class="sxs-lookup"><span data-stu-id="31cc6-107">Get the Emotion API Java for Android SDK [here](https://github.com/Microsoft/Cognitive-emotion-android)</span></span>
* <span data-ttu-id="31cc6-108">Get your free subscription key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span><span class="sxs-lookup"><span data-stu-id="31cc6-108">Get your free subscription key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span></span>

## <a name="recognize-emotions-java-for-android-example-request"></a><span data-ttu-id="31cc6-109">Recognize Emotions Java for Android Example Request</span><span class="sxs-lookup"><span data-stu-id="31cc6-109">Recognize Emotions Java for Android Example Request</span></span>

```Java
// // This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
import java.net.URI;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.util.EntityUtils;

public class Main
{
    public static void main(String[] args)
    {
        HttpClient httpClient = new DefaultHttpClient();

        try
        {
            URIBuilder uriBuilder = new URIBuilder("https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognize");

            URI uri = uriBuilder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers. Replace the example key below with your valid subscription key.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request body. Replace the example URL below with the URL of the image you want to analyze.
            StringEntity reqEntity = new StringEntity("{ \"url\": \"http://example.com/images/test.jpg\" }");
            request.setEntity(reqEntity);

            HttpResponse response = httpClient.execute(request);
            HttpEntity entity = response.getEntity();

            if (entity != null)
            {
                System.out.println(EntityUtils.toString(entity));
            }
        }
        catch (Exception e)
        {
            System.out.println(e.getMessage());
        }
    }
}
```

## <a name="recognize-emotions-sample-response"></a><span data-ttu-id="31cc6-110">Recognize Emotions Sample Response</span><span class="sxs-lookup"><span data-stu-id="31cc6-110">Recognize Emotions Sample Response</span></span>
<span data-ttu-id="31cc6-111">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span><span class="sxs-lookup"><span data-stu-id="31cc6-111">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span></span> <span data-ttu-id="31cc6-112">An empty response indicates that no faces were detected.</span><span class="sxs-lookup"><span data-stu-id="31cc6-112">An empty response indicates that no faces were detected.</span></span> <span data-ttu-id="31cc6-113">An emotion entry contains the following fields:</span><span class="sxs-lookup"><span data-stu-id="31cc6-113">An emotion entry contains the following fields:</span></span>
* <span data-ttu-id="31cc6-114">faceRectangle - Rectangle location of face in the image.</span><span class="sxs-lookup"><span data-stu-id="31cc6-114">faceRectangle - Rectangle location of face in the image.</span></span>
* <span data-ttu-id="31cc6-115">scores - Emotion scores for each face in the image.</span><span class="sxs-lookup"><span data-stu-id="31cc6-115">scores - Emotion scores for each face in the image.</span></span> 

```json
application/json 
[
  {
    "faceRectangle": {
      "left": 68,
      "top": 97,
      "width": 64,
      "height": 97
    },
    "scores": {
      "anger": 0.00300731952,
      "contempt": 5.14648448E-08,
      "disgust": 9.180124E-06,
      "fear": 0.0001912825,
      "happiness": 0.9875571,
      "neutral": 0.0009861537,
      "sadness": 1.889955E-05,
      "surprise": 0.008229999
    }
  }
]
