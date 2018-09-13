---
title: Computer Vision API Java quick starts | Microsoft Docs
description: Get information and code samples to help you quickly get started using Java and the Computer Vision API in Cognitive Services.
services: cognitive-services
author: JuliaNik
manager: ytkuo
ms.service: cognitive-services
ms.technology: computer-vision
ms.topic: article
ms.date: 03/27/2017
ms.author: juliakuz
ms.openlocfilehash: 72051ec3195b7f72658088a33264af236272eccf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552877"
---
# <a name="computer-vision-java-quick-starts"></a><span data-ttu-id="00f4b-103">Computer Vision Java Quick Starts</span><span class="sxs-lookup"><span data-stu-id="00f4b-103">Computer Vision Java Quick Starts</span></span>
<span data-ttu-id="00f4b-104">This article provides information and code samples to help you quickly get started using Java and the Computer Vision API to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="00f4b-104">This article provides information and code samples to help you quickly get started using Java and the Computer Vision API to accomplish the following tasks:</span></span>
* [<span data-ttu-id="00f4b-105">Analyze an image</span><span class="sxs-lookup"><span data-stu-id="00f4b-105">Analyze an image</span></span>](#AnalyzeImage)
* [<span data-ttu-id="00f4b-106">Use a Domain-Specific Model</span><span class="sxs-lookup"><span data-stu-id="00f4b-106">Use a Domain-Specific Model</span></span>](#DomainSpecificModel)
* [<span data-ttu-id="00f4b-107">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="00f4b-107">Intelligently generate a thumbnail</span></span>](#GetThumbnail)
* [<span data-ttu-id="00f4b-108">Detect and extract printed text from an image</span><span class="sxs-lookup"><span data-stu-id="00f4b-108">Detect and extract printed text from an image</span></span>](#OCR)
* [<span data-ttu-id="00f4b-109">Detect and extract handwritten text from an image</span><span class="sxs-lookup"><span data-stu-id="00f4b-109">Detect and extract handwritten text from an image</span></span>](#RecognizeText)

## <a name="prerequisites"></a><span data-ttu-id="00f4b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="00f4b-110">Prerequisites</span></span>
* <span data-ttu-id="00f4b-111">Get the Microsoft Computer Vision Android SDK [here](https://github.com/Microsoft/Cognitive-vision-android).</span><span class="sxs-lookup"><span data-stu-id="00f4b-111">Get the Microsoft Computer Vision Android SDK [here](https://github.com/Microsoft/Cognitive-vision-android).</span></span>
* <span data-ttu-id="00f4b-112">To use the Computer Vision API, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="00f4b-112">To use the Computer Vision API, you need a subscription key.</span></span> <span data-ttu-id="00f4b-113">You can get free subscription keys [here](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/vision-api-how-to-topics/HowToSubscribe).</span><span class="sxs-lookup"><span data-stu-id="00f4b-113">You can get free subscription keys [here](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/vision-api-how-to-topics/HowToSubscribe).</span></span>

## <span data-ttu-id="00f4b-114">Analyze an Image With Computer Vision API Using Java <a name="AnalyzeImage"> </a></span><span class="sxs-lookup"><span data-stu-id="00f4b-114">Analyze an Image With Computer Vision API Using Java <a name="AnalyzeImage"> </a></span></span>
<span data-ttu-id="00f4b-115">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="00f4b-115">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="00f4b-116">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="00f4b-116">You can upload an image or specify an image URL and choose which features to return, including:</span></span>
* <span data-ttu-id="00f4b-117">The category defined in this [taxonomy](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/Category-Taxonomy).</span><span class="sxs-lookup"><span data-stu-id="00f4b-117">The category defined in this [taxonomy](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/Category-Taxonomy).</span></span>
* <span data-ttu-id="00f4b-118">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="00f4b-118">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="00f4b-119">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="00f4b-119">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="00f4b-120">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="00f4b-120">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="00f4b-121">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="00f4b-121">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="00f4b-122">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="00f4b-122">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="00f4b-123">Does the image contains adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="00f4b-123">Does the image contains adult or sexually suggestive content?</span></span>

### <a name="analyze-an-image-java-example-request"></a><span data-ttu-id="00f4b-124">Analyze an Image Java Example Request</span><span class="sxs-lookup"><span data-stu-id="00f4b-124">Analyze an Image Java Example Request</span></span>

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
        HttpClient httpclient = new DefaultHttpClient();

        try
        {
            URIBuilder builder = new URIBuilder("https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze");

            builder.setParameter("visualFeatures", "Categories");
            builder.setParameter("details", "Celebrities");
            builder.setParameter("language", "en");

            URI uri = builder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers - replace this example key with your valid subscription key.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request body. Replace the example URL with the URL for the JPEG image of a celebrity.
            StringEntity reqEntity = new StringEntity("{\"url\":\"http://example.com/images/test.jpg\"}");
            request.setEntity(reqEntity);

            HttpResponse response = httpclient.execute(request);
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
### <a name="analyze-an-image-response"></a><span data-ttu-id="00f4b-125">Analyze an Image Response</span><span class="sxs-lookup"><span data-stu-id="00f4b-125">Analyze an Image Response</span></span>
<span data-ttu-id="00f4b-126">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="00f4b-126">A successful response is returned in JSON.</span></span> <span data-ttu-id="00f4b-127">The following example shows a successful response:</span><span class="sxs-lookup"><span data-stu-id="00f4b-127">The following example shows a successful response:</span></span>

```json
{
  "categories": [
    {
      "name": "abstract_",
      "score": 0.00390625
    },
    {
      "name": "people_",
      "score": 0.83984375,
      "detail": {
        "celebrities": [
          {
            "name": "Satya Nadella",
            "faceRectangle": {
              "left": 597,
              "top": 162,
              "width": 248,
              "height": 248
            },
            "confidence": 0.999028444
          }
        ]
      }
    }
  ],
  "adult": {
    "isAdultContent": false,
    "isRacyContent": false,
    "adultScore": 0.0934349000453949,
    "racyScore": 0.068613491952419281
  },
  "tags": [
    {
      "name": "person",
      "confidence": 0.98979085683822632
    },
    {
      "name": "man",
      "confidence": 0.94493889808654785
    },
    {
      "name": "outdoor",
      "confidence": 0.938492476940155
    },
    {
      "name": "window",
      "confidence": 0.89513939619064331
    }
  ],
  "description": {
    "tags": [
      "person",
      "man",
      "outdoor",
      "window",
      "glasses"
    ],
    "captions": [
      {
        "text": "Satya Nadella sitting on a bench",
        "confidence": 0.48293603002174407
      }
    ]  },
  "requestId": "0dbec5ad-a3d3-4f7e-96b4-dfd57efe967d",
  "metadata": {
    "width": 1500,
    "height": 1000,
    "format": "Jpeg"
  },
  "faces": [
    {
      "age": 44,
      "gender": "Male",
      "faceRectangle": {
        "left": 593,
        "top": 160,
        "width": 250,
        "height": 250
      }
    }
  ],
  "color": {
    "dominantColorForeground": "Brown",
    "dominantColorBackground": "Brown",
    "dominantColors": [
      "Brown",
      "Black"
    ],
    "accentColor": "873B59",
    "isBWImg": false
  },
  "imageType": {
    "clipArtType": 0,
    "lineDrawingType": 0
  }
}

```

## <span data-ttu-id="00f4b-128">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span><span class="sxs-lookup"><span data-stu-id="00f4b-128">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span></span>
<span data-ttu-id="00f4b-129">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span><span class="sxs-lookup"><span data-stu-id="00f4b-129">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span></span> <span data-ttu-id="00f4b-130">The two domain-specific models that are currently available are celebrities and landmarks.</span><span class="sxs-lookup"><span data-stu-id="00f4b-130">The two domain-specific models that are currently available are celebrities and landmarks.</span></span> <span data-ttu-id="00f4b-131">The following example identifies a landmark in an image.</span><span class="sxs-lookup"><span data-stu-id="00f4b-131">The following example identifies a landmark in an image.</span></span>

### <a name="landmark-java-example-request"></a><span data-ttu-id="00f4b-132">Landmark Java Example Request</span><span class="sxs-lookup"><span data-stu-id="00f4b-132">Landmark Java Example Request</span></span>

```Java
// This sample uses the Apache HTTP client (org.apache.httpcomponents:httpclient:4.2.4)
// and org.json (org.json:20160810).

import java.net.URI;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.util.EntityUtils;
import org.json.JSONObject;

public class Main
{
    public static void main(String[] args)
    {
        HttpClient httpClient = new DefaultHttpClient();

        try
        {
            // Change "landmarks" to "celebrities" in the url to use the Celebrities model.
            URIBuilder uriBuilder = new URIBuilder("https://westus.api.cognitive.microsoft.com/vision/v1.0/models/landmarks/analyze");

            // Change "landmarks" to "celebrities" to use the Celebrities model.
            uriBuilder.setParameter("model", "landmarks");

            URI uri = uriBuilder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers. Replace the example key below with your valid subscription key.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request body. Replace the example URL with the URL of a JPEG image containing text.
            StringEntity requestEntity = new StringEntity("{\"url\":\"https://upload.wikimedia.org/wikipedia/commons/2/23/Space_Needle_2011-07-04.jpg\"}");
            request.setEntity(requestEntity);

            HttpResponse response = httpClient.execute(request);
            HttpEntity entity = response.getEntity();

            if (entity != null)
            {
                // Output the JSON response
                String jsonString = EntityUtils.toString(entity);
                JSONObject json = new JSONObject(jsonString);
                System.out.println("REST Response:");
                System.out.println(json.toString(2));
            }
        }
        catch (Exception e)
        {
            System.out.println(e.getMessage());
        }
    }
}
```

### <a name="landmark-example-response"></a><span data-ttu-id="00f4b-133">Landmark Example Response</span><span class="sxs-lookup"><span data-stu-id="00f4b-133">Landmark Example Response</span></span>
<span data-ttu-id="00f4b-134">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="00f4b-134">A successful response is returned in JSON.</span></span> <span data-ttu-id="00f4b-135">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="00f4b-135">Following is an example of a successful response:</span></span>  

```json
REST Response:
{
  "result": {"landmarks": [{
    "confidence": 0.9998178,
    "name": "Space Needle"
  }]},
  "metadata": {
    "width": 2096,
    "format": "Jpeg",
    "height": 4132
  },
  "requestId": "7d0d00da-ac37-44ba-ad77-050e11a5ee05"
}
```

## <span data-ttu-id="00f4b-136">Get a Thumbnail with Computer Vision API Using Java <a name="GetThumbnail"> </a></span><span class="sxs-lookup"><span data-stu-id="00f4b-136">Get a Thumbnail with Computer Vision API Using Java <a name="GetThumbnail"> </a></span></span>
<span data-ttu-id="00f4b-137">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to crop an image based on its region of interest (ROI) to the height and width you desire.</span><span class="sxs-lookup"><span data-stu-id="00f4b-137">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to crop an image based on its region of interest (ROI) to the height and width you desire.</span></span> <span data-ttu-id="00f4b-138">The aspect ratio you set for the thumbnail can be different from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="00f4b-138">The aspect ratio you set for the thumbnail can be different from the aspect ratio of the input image.</span></span>

### <a name="get-a-thumbnail-java-example-request"></a><span data-ttu-id="00f4b-139">Get a Thumbnail Java Example Request</span><span class="sxs-lookup"><span data-stu-id="00f4b-139">Get a Thumbnail Java Example Request</span></span>

```Java
// // This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
import java.awt.*;
import javax.swing.*;
import java.net.URI;
import java.io.InputStream;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.DefaultHttpClient;

public class Main
{
    public static void main(String[] args)
    {
        HttpClient httpClient = new DefaultHttpClient();

        try
        {
            URIBuilder uriBuilder = new URIBuilder("https://westus.api.cognitive.microsoft.com/vision/v1.0/generateThumbnail");

            uriBuilder.setParameter("width", "100");
            uriBuilder.setParameter("height", "150");
            uriBuilder.setParameter("smartCropping", "true");

            URI uri = uriBuilder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers - replace this example key with your valid subscription key.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request body. Replace the example URL with the URL for the JPEG image of a person.
            StringEntity requestEntity = new StringEntity("{\"url\":\"http://example.com/images/test.jpg\"}");
            request.setEntity(requestEntity);

            HttpResponse response = httpClient.execute(request);
            System.out.println(response);

            // Display the thumbnail.
            HttpEntity httpEntity = response.getEntity();
            displayImage(httpEntity.getContent());
        }
        catch (Exception e)
        {
            System.out.println(e.getMessage());
        }
    }

    private static void displayImage(InputStream inputStream)
    {
        try {
            BufferedImage bufferedImage = ImageIO.read(inputStream);

            ImageIcon imageIcon = new ImageIcon(bufferedImage);

            JLabel jLabel = new JLabel();
            jLabel.setIcon(imageIcon);

            JFrame jFrame = new JFrame();
            jFrame.setLayout(new FlowLayout());
            jFrame.setSize(100, 150);

            jFrame.add(jLabel);
            jFrame.setVisible(true);
            jFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        }
        catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```

### <a name="get-a-thumbnail-response"></a><span data-ttu-id="00f4b-140">Get a Thumbnail Response</span><span class="sxs-lookup"><span data-stu-id="00f4b-140">Get a Thumbnail Response</span></span>
<span data-ttu-id="00f4b-141">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="00f4b-141">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="00f4b-142">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="00f4b-142">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span>


## <span data-ttu-id="00f4b-143">Optical Character Recognition (OCR) with Computer Vision API Using Java<a name="OCR"> </a></span><span class="sxs-lookup"><span data-stu-id="00f4b-143">Optical Character Recognition (OCR) with Computer Vision API Using Java<a name="OCR"> </a></span></span>
<span data-ttu-id="00f4b-144">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="00f4b-144">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

### <a name="ocr-java-example-request"></a><span data-ttu-id="00f4b-145">OCR Java Example Request</span><span class="sxs-lookup"><span data-stu-id="00f4b-145">OCR Java Example Request</span></span>
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
            URIBuilder uriBuilder = new URIBuilder("https://westus.api.cognitive.microsoft.com/vision/v1.0/ocr");

            uriBuilder.setParameter("language", "unk");
            uriBuilder.setParameter("detectOrientation ", "true");

            URI uri = uriBuilder.build();
            HttpPost request = new HttpPost(uri);

            // Request headers - replace this example key with your valid subscription key.
            request.setHeader("Content-Type", "application/json");
            request.setHeader("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request body. Replace the example URL with the URL of a JPEG image containing text.
            StringEntity requestEntity = new StringEntity("{\"url\":\"http://example.com/images/test.jpg\"}");
            request.setEntity(requestEntity);

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

### <a name="ocr-example-response"></a><span data-ttu-id="00f4b-146">OCR Example Response</span><span class="sxs-lookup"><span data-stu-id="00f4b-146">OCR Example Response</span></span>
<span data-ttu-id="00f4b-147">Upon success, the OCR results returned include the detected text and bounding boxes for regions, lines, and words.</span><span class="sxs-lookup"><span data-stu-id="00f4b-147">Upon success, the OCR results returned include the detected text and bounding boxes for regions, lines, and words.</span></span>

```json
{
  "language": "en",
  "textAngle": -2.0000000000000338,
  "orientation": "Up",
  "regions": [
    {
      "boundingBox": "462,379,497,258",
      "lines": [
        {
          "boundingBox": "462,379,497,74",
          "words": [
            {
              "boundingBox": "462,379,41,73",
              "text": "A"
            },
            {
              "boundingBox": "523,379,153,73",
              "text": "GOAL"
            },
            {
              "boundingBox": "694,379,265,74",
              "text": "WITHOUT"
            }
          ]
        },
        {
          "boundingBox": "565,471,289,74",
          "words": [
            {
              "boundingBox": "565,471,41,73",
              "text": "A"
            },
            {
              "boundingBox": "626,471,150,73",
              "text": "PLAN"
            },
            {
              "boundingBox": "801,472,53,73",
              "text": "IS"
            }
          ]
        },
        {
          "boundingBox": "519,563,375,74",
          "words": [
            {
              "boundingBox": "519,563,149,74",
              "text": "JUST"
            },
            {
              "boundingBox": "683,564,41,72",
              "text": "A"
            },
            {
              "boundingBox": "741,564,153,73",
              "text": "WISH"
            }
          ]
        }
      ]
    }
  ]
}

```

## <span data-ttu-id="00f4b-148">Text Recognition with Computer Vision API Using Java<a name="RecognizeText"> </a></span><span class="sxs-lookup"><span data-stu-id="00f4b-148">Text Recognition with Computer Vision API Using Java<a name="RecognizeText"> </a></span></span>
<span data-ttu-id="00f4b-149">Use the [RecognizeText method](https://ocr.portal.azure-api.net/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200) to detect handwritten or printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="00f4b-149">Use the [RecognizeText method](https://ocr.portal.azure-api.net/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200) to detect handwritten or printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

### <a name="handwriting-recognition-java-example"></a><span data-ttu-id="00f4b-150">Handwriting Recognition Java Example</span><span class="sxs-lookup"><span data-stu-id="00f4b-150">Handwriting Recognition Java Example</span></span>
```Java
// // This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
import java.net.URI;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.util.EntityUtils;
import org.apache.http.Header;


public class Main
{
    public static void main(String[] args)
    {
        HttpClient textClient = new DefaultHttpClient();
        HttpClient resultClient = new DefaultHttpClient();

        // Replace this example key with your valid subscription key.
        String subscriptionKey = "13hc77781f7e4b19b5fcdd72a8df7156";

        try
        {
            // For printed text, set "handwriting" to false.
            URI uri = new URI("https://westus.api.cognitive.microsoft.com/vision/v1.0/recognizeText?handwriting=true");
            HttpPost textRequest = new HttpPost(uri);

            // Request headers. Another valid content type is "application/octet-stream".
            textRequest.setHeader("Content-Type", "application/json");
            textRequest.setHeader("Ocp-Apim-Subscription-Key", subscriptionKey);

            // Request body. Replace the example URL with the URL of a JPEG image containing handwriting.
            StringEntity requestEntity = new StringEntity("{\"url\":\"http://example.com/images/test.jpg\"}");
            textRequest.setEntity(requestEntity);

            HttpResponse textResponse = textClient.execute(textRequest);
            String operationLocation = null;

            Header[] responseHeaders = textResponse.getAllHeaders();
            for(Header header : responseHeaders) {
                if(header.getName().equals("Operation-Location"))
                {
                    // This string is the URI where you can get the text recognition operation result.
                    operationLocation = header.getValue();
                    break;
                }
            }

            System.out.println(operationLocation);

            HttpGet resultRequest = new HttpGet(operationLocation);
            resultRequest.setHeader("Ocp-Apim-Subscription-Key", subscriptionKey);

            // Note: The response may not be immediately available. Handwriting recognition is an
            // async operation that can take a variable amount of time depending on the length
            // of the text you want to recognize. You may need to wait or retry this operation.
            HttpResponse resultResponse = resultClient.execute(resultRequest);
            System.out.print("Text recognition result response: ");
            System.out.println(resultResponse);
        }
        catch (Exception e)
        {
            System.out.println(e.getMessage());
        }
    }
}
```