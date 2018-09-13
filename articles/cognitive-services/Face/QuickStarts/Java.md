---
title: Face API Java quickstart | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you detect faces from an image using the Face API with Java in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: face-api
ms.topic: quickstart
ms.date: 05/10/2018
ms.author: nolachar
ms.openlocfilehash: 5788b5f3a91397ad0cb497004b7776fa4ec5e645
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800506"
---
# <a name="quickstart-detect-faces-in-an-image-using-java"></a><span data-ttu-id="ea091-103">Quickstart: Detect faces in an image using Java</span><span class="sxs-lookup"><span data-stu-id="ea091-103">Quickstart: Detect faces in an image using Java</span></span>

<span data-ttu-id="ea091-104">In this quickstart, you detect human faces in an image using the Face API.</span><span class="sxs-lookup"><span data-stu-id="ea091-104">In this quickstart, you detect human faces in an image using the Face API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea091-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ea091-105">Prerequisites</span></span>

<span data-ttu-id="ea091-106">You need a subscription key to run the sample.</span><span class="sxs-lookup"><span data-stu-id="ea091-106">You need a subscription key to run the sample.</span></span> <span data-ttu-id="ea091-107">You can get free trial subscription keys from [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=face-api).</span><span class="sxs-lookup"><span data-stu-id="ea091-107">You can get free trial subscription keys from [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=face-api).</span></span>

## <a name="detect-faces-in-an-image"></a><span data-ttu-id="ea091-108">Detect faces in an image</span><span class="sxs-lookup"><span data-stu-id="ea091-108">Detect faces in an image</span></span>

<span data-ttu-id="ea091-109">Use the [Face - Detect](https://westcentralus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) method to detect faces in an image and return face attributes including:</span><span class="sxs-lookup"><span data-stu-id="ea091-109">Use the [Face - Detect](https://westcentralus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) method to detect faces in an image and return face attributes including:</span></span>

* <span data-ttu-id="ea091-110">Face ID: Unique ID used in several Face API scenarios.</span><span class="sxs-lookup"><span data-stu-id="ea091-110">Face ID: Unique ID used in several Face API scenarios.</span></span>
* <span data-ttu-id="ea091-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span><span class="sxs-lookup"><span data-stu-id="ea091-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span></span>
* <span data-ttu-id="ea091-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span><span class="sxs-lookup"><span data-stu-id="ea091-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span></span>
* <span data-ttu-id="ea091-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span><span class="sxs-lookup"><span data-stu-id="ea091-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span></span>

<span data-ttu-id="ea091-114">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="ea091-114">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="ea091-115">Create a new command-line app in your favorite Java IDE.</span><span class="sxs-lookup"><span data-stu-id="ea091-115">Create a new command-line app in your favorite Java IDE.</span></span>
2. <span data-ttu-id="ea091-116">Replace the Main class with the following code (keep any `package` statements).</span><span class="sxs-lookup"><span data-stu-id="ea091-116">Replace the Main class with the following code (keep any `package` statements).</span></span>
3. <span data-ttu-id="ea091-117">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="ea091-117">Replace `<Subscription Key>` with your valid subscription key.</span></span>
4. <span data-ttu-id="ea091-118">Change the `uriBase` value to use the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="ea091-118">Change the `uriBase` value to use the location where you obtained your subscription keys, if necessary.</span></span>
5. <span data-ttu-id="ea091-119">Download these global libraries from the Maven Repository to the `lib` directory in your project:</span><span class="sxs-lookup"><span data-stu-id="ea091-119">Download these global libraries from the Maven Repository to the `lib` directory in your project:</span></span>
   * `org.apache.httpcomponents:httpclient:4.2.4`
   * `org.json:json:20170516`
6. <span data-ttu-id="ea091-120">Run 'Main'.</span><span class="sxs-lookup"><span data-stu-id="ea091-120">Run 'Main'.</span></span>

### <a name="face---detect-request"></a><span data-ttu-id="ea091-121">Face - Detect request</span><span class="sxs-lookup"><span data-stu-id="ea091-121">Face - Detect request</span></span>

```java
// This sample uses Apache HttpComponents:
// http://hc.apache.org/httpcomponents-core-ga/httpcore/apidocs/
// https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/

import java.net.URI;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.util.EntityUtils;
import org.json.JSONArray;
import org.json.JSONObject;

public class Main
{
    // Replace <Subscription Key> with your valid subscription key.
    private static final String subscriptionKey = "<Subscription Key>";

    // NOTE: You must use the same region in your REST call as you used to
    // obtain your subscription keys. For example, if you obtained your
    // subscription keys from westus, replace "westcentralus" in the URL
    // below with "westus".
    //
    // Free trial subscription keys are generated in the westcentralus region. If you
    // use a free trial subscription key, you shouldn't need to change this region.
    private static final String uriBase =
        "https://westcentralus.api.cognitive.microsoft.com/face/v1.0/detect";

    private static final String imageWithFaces =
        "{\"url\":\"https://upload.wikimedia.org/wikipedia/commons/c/c3/RH_Louise_Lillian_Gish.jpg\"}";

    private static final String faceAttributes =
        "age,gender,headPose,smile,facialHair,glasses,emotion,hair,makeup,occlusion,accessories,blur,exposure,noise";

    public static void main(String[] args)
    {
        HttpClient httpclient = new DefaultHttpClient();

        try
        {
            URIBuilder builder = new URIBuilder(uriBase);

            // Request parameters. All of them are optional.
            builder.setParameter("returnFaceId", "true");
            builder.setParameter("returnFaceLandmarks", "false");
            builder.setParameter("returnFaceAttributes", faceAttributes);

            // Prepare the URI for the REST API call.
            URI uri = builder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKey);

            // Request body.
            StringEntity reqEntity = new StringEntity(imageWithFaces);
            request.setEntity(reqEntity);

            // Execute the REST API call and get the response entity.
            HttpResponse response = httpclient.execute(request);
            HttpEntity entity = response.getEntity();

            if (entity != null)
            {
                // Format and display the JSON response.
                System.out.println("REST Response:\n");

                String jsonString = EntityUtils.toString(entity).trim();
                if (jsonString.charAt(0) == '[') {
                    JSONArray jsonArray = new JSONArray(jsonString);
                    System.out.println(jsonArray.toString(2));
                }
                else if (jsonString.charAt(0) == '{') {
                    JSONObject jsonObject = new JSONObject(jsonString);
                    System.out.println(jsonObject.toString(2));
                } else {
                    System.out.println(jsonString);
                }
            }
        }
        catch (Exception e)
        {
            // Display error message.
            System.out.println(e.getMessage());
        }
    }
}
```

### <a name="face---detect-response"></a><span data-ttu-id="ea091-122">Face - Detect response</span><span class="sxs-lookup"><span data-stu-id="ea091-122">Face - Detect response</span></span>

<span data-ttu-id="ea091-123">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="ea091-123">A successful response is returned in JSON.</span></span>

```json
[{
  "faceRectangle": {
    "top": 131,
    "left": 177,
    "width": 162,
    "height": 162
  },
  "faceAttributes": {
    "makeup": {
      "eyeMakeup": true,
      "lipMakeup": true
    },
    "facialHair": {
      "sideburns": 0,
      "beard": 0,
      "moustache": 0
    },
    "gender": "female",
    "accessories": [],
    "blur": {
      "blurLevel": "low",
      "value": 0.06
    },
    "headPose": {
      "roll": 0.1,
      "pitch": 0,
      "yaw": -32.9
    },
    "smile": 0,
    "glasses": "NoGlasses",
    "hair": {
      "bald": 0,
      "invisible": false,
      "hairColor": [
        {
          "color": "brown",
          "confidence": 1
        },
        {
          "color": "black",
          "confidence": 0.87
        },
        {
          "color": "other",
          "confidence": 0.51
        },
        {
          "color": "blond",
          "confidence": 0.08
        },
        {
          "color": "red",
          "confidence": 0.08
        },
        {
          "color": "gray",
          "confidence": 0.02
        }
      ]
    },
    "emotion": {
      "contempt": 0,
      "surprise": 0.005,
      "happiness": 0,
      "neutral": 0.986,
      "sadness": 0.009,
      "disgust": 0,
      "anger": 0,
      "fear": 0
    },
    "exposure": {
      "value": 0.67,
      "exposureLevel": "goodExposure"
    },
    "occlusion": {
      "eyeOccluded": false,
      "mouthOccluded": false,
      "foreheadOccluded": false
    },
    "noise": {
      "noiseLevel": "low",
      "value": 0
    },
    "age": 22.9
  },
  "faceId": "49d55c17-e018-4a42-ba7b-8cbbdfae7c6f"
}]
```

## <a name="next-steps"></a><span data-ttu-id="ea091-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea091-124">Next steps</span></span>

<span data-ttu-id="ea091-125">Learn how to create an Android application that uses the Face service to detect faces in an image.</span><span class="sxs-lookup"><span data-stu-id="ea091-125">Learn how to create an Android application that uses the Face service to detect faces in an image.</span></span> <span data-ttu-id="ea091-126">The application displays the image with a frame drawn around each face.</span><span class="sxs-lookup"><span data-stu-id="ea091-126">The application displays the image with a frame drawn around each face.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ea091-127">Tutorial: Getting Started with Face API in Android</span><span class="sxs-lookup"><span data-stu-id="ea091-127">Tutorial: Getting Started with Face API in Android</span></span>](../Tutorials/FaceAPIinJavaForAndroidTutorial.md)
