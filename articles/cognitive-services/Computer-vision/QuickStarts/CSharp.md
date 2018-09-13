---
title: Computer Vision API C# quick starts | Microsoft Docs
description: Get information and code samples to help you quickly get started using C# and the Computer Vision API in Cognitive Services.
services: cognitive-services
author: JuliaNik
manager: ytkuo
ms.service: cognitive-services
ms.technology: computer-vision
ms.topic: article
ms.date: 02/20/2017
ms.author: juliakuz
ms.openlocfilehash: 8ac89b716f07c1f2a7463a872900fcd36c8a84bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554265"
---
# <a name="computer-vision-c-quick-starts"></a><span data-ttu-id="a2596-103">Computer Vision C# Quick Starts</span><span class="sxs-lookup"><span data-stu-id="a2596-103">Computer Vision C# Quick Starts</span></span>
<span data-ttu-id="a2596-104">This article provides information and code samples to help you quickly get started using the Computer Vision API with C# to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="a2596-104">This article provides information and code samples to help you quickly get started using the Computer Vision API with C# to accomplish the following tasks:</span></span>
* [<span data-ttu-id="a2596-105">Analyze an image</span><span class="sxs-lookup"><span data-stu-id="a2596-105">Analyze an image</span></span>](#AnalyzeImage)
* [<span data-ttu-id="a2596-106">Use a Domain-Specific Model</span><span class="sxs-lookup"><span data-stu-id="a2596-106">Use a Domain-Specific Model</span></span>](#DomainSpecificModel)
* [<span data-ttu-id="a2596-107">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="a2596-107">Intelligently generate a thumbnail</span></span>](#GetThumbnail)
* [<span data-ttu-id="a2596-108">Detect and extract printed text from an image</span><span class="sxs-lookup"><span data-stu-id="a2596-108">Detect and extract printed text from an image</span></span>](#OCR)
* [<span data-ttu-id="a2596-109">Detect and extract handwritten text from an image</span><span class="sxs-lookup"><span data-stu-id="a2596-109">Detect and extract handwritten text from an image</span></span>](#RecognizeText)

## <a name="prerequisites"></a><span data-ttu-id="a2596-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a2596-110">Prerequisites</span></span>
* <span data-ttu-id="a2596-111">Get the Microsoft Computer Vision API Windows SDK [here](https://github.com/Microsoft/Cognitive-vision-windows).</span><span class="sxs-lookup"><span data-stu-id="a2596-111">Get the Microsoft Computer Vision API Windows SDK [here](https://github.com/Microsoft/Cognitive-vision-windows).</span></span>
* <span data-ttu-id="a2596-112">To use the Computer Vision API, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="a2596-112">To use the Computer Vision API, you need a subscription key.</span></span> <span data-ttu-id="a2596-113">You can get free subscription keys [here](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/vision-api-how-to-topics/HowToSubscribe).</span><span class="sxs-lookup"><span data-stu-id="a2596-113">You can get free subscription keys [here](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/vision-api-how-to-topics/HowToSubscribe).</span></span>

## <span data-ttu-id="a2596-114">Analyze an Image With Computer Vision API Using C# <a name="AnalyzeImage"> </a></span><span class="sxs-lookup"><span data-stu-id="a2596-114">Analyze an Image With Computer Vision API Using C# <a name="AnalyzeImage"> </a></span></span>
<span data-ttu-id="a2596-115">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="a2596-115">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="a2596-116">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="a2596-116">You can upload an image or specify an image URL and choose which features to return, including:</span></span>
* <span data-ttu-id="a2596-117">The category defined in this [taxonomy](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/Category-Taxonomy).</span><span class="sxs-lookup"><span data-stu-id="a2596-117">The category defined in this [taxonomy](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/Category-Taxonomy).</span></span>
* <span data-ttu-id="a2596-118">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="a2596-118">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="a2596-119">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="a2596-119">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="a2596-120">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="a2596-120">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="a2596-121">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="a2596-121">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="a2596-122">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="a2596-122">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="a2596-123">Does the image contains adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="a2596-123">Does the image contains adult or sexually suggestive content?</span></span>

### <a name="analyze-an-image-c-example-request"></a><span data-ttu-id="a2596-124">Analyze an Image C# Example Request</span><span class="sxs-lookup"><span data-stu-id="a2596-124">Analyze an Image C# Example Request</span></span>

```c#
using System;
using System.IO;
using System.Net.Http;
using System.Net.Http.Headers;

namespace CSHttpClientSample
{
    static class Program
    {
        static void Main()
        {
            Console.Write("Enter image file path: ");
            string imageFilePath = Console.ReadLine();

            MakeAnalysisRequest(imageFilePath);

            Console.WriteLine("\n\n\nHit ENTER to exit...");
            Console.ReadLine();
        }

        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }

        static async void MakeAnalysisRequest(string imageFilePath)
        {
            var client = new HttpClient();

            // Request headers - replace this example key with your valid subscription key.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request parameters. A third optional parameter is "details".
            string requestParameters = "visualFeatures=Categories&language=en";
            string uri = "https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze?" + requestParameters;
            Console.WriteLine(uri);

            HttpResponseMessage response;

            // Request body. Try this sample with a locally stored JPEG image.
            byte[] byteData = GetImageAsByteArray(imageFilePath);

            using (var content = new ByteArrayContent(byteData))
            {
                // This example uses content type "application/octet-stream".
                // The other content types you can use are "application/json" and "multipart/form-data".
                content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
                response = await client.PostAsync(uri, content);
            }
        }
    }
}
```
### <a name="analyze-an-image-response"></a><span data-ttu-id="a2596-125">Analyze an Image Response</span><span class="sxs-lookup"><span data-stu-id="a2596-125">Analyze an Image Response</span></span>
<span data-ttu-id="a2596-126">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="a2596-126">A successful response is returned in JSON.</span></span> <span data-ttu-id="a2596-127">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="a2596-127">Following is an example of a successful response:</span></span>

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
    ]
  },
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

## <span data-ttu-id="a2596-128">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span><span class="sxs-lookup"><span data-stu-id="a2596-128">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span></span>
<span data-ttu-id="a2596-129">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span><span class="sxs-lookup"><span data-stu-id="a2596-129">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span></span> <span data-ttu-id="a2596-130">The two domain-specific models that are currently available are celebrities and landmarks.</span><span class="sxs-lookup"><span data-stu-id="a2596-130">The two domain-specific models that are currently available are celebrities and landmarks.</span></span> <span data-ttu-id="a2596-131">The following example identifies a landmark in an image.</span><span class="sxs-lookup"><span data-stu-id="a2596-131">The following example identifies a landmark in an image.</span></span>

### <a name="landmark-c-example-request"></a><span data-ttu-id="a2596-132">Landmark C# Example Request</span><span class="sxs-lookup"><span data-stu-id="a2596-132">Landmark C# Example Request</span></span>

```c#
using System;
using System.IO;
using System.Net.Http;
using System.Net.Http.Headers;

namespace CSHttpClientSample
{
    static class Program
    {
        static void Main()
        {
            Console.Write("Enter image file path: ");
            string imageFilePath = Console.ReadLine();

            MakeAnalysisRequest(imageFilePath);

            Console.WriteLine("\n\nHit ENTER to exit...\n");
            Console.ReadLine();
        }

        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }

        static async void MakeAnalysisRequest(string imageFilePath)
        {
            var client = new HttpClient();

            // Request headers. Replace the second parameter with a valid subscription key.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request parameters. Change "landmarks" to "celebrities" on requestParameters and uri to use the Celebrities model.
            string requestParameters = "model=landmarks";
            string uri = "https://westus.api.cognitive.microsoft.com/vision/v1.0/models/landmarks/analyze?" + requestParameters;
            Console.WriteLine(uri);

            HttpResponseMessage response;

            // Request body. Try this sample with a locally stored JPEG image.
            byte[] byteData = GetImageAsByteArray(imageFilePath);

            using (var content = new ByteArrayContent(byteData))
            {
                // This example uses content type "application/octet-stream".
                // The other content types you can use are "application/json" and "multipart/form-data".
                content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
                response = await client.PostAsync(uri, content);
                string contentString = await response.Content.ReadAsStringAsync();
                Console.WriteLine("Response:\n");
                Console.WriteLine(contentString);
            }
        }
    }
}
```

### <a name="landmark-example-response"></a><span data-ttu-id="a2596-133">Landmark Example Response</span><span class="sxs-lookup"><span data-stu-id="a2596-133">Landmark Example Response</span></span>
<span data-ttu-id="a2596-134">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="a2596-134">A successful response is returned in JSON.</span></span> <span data-ttu-id="a2596-135">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="a2596-135">Following is an example of a successful response:</span></span>  

```json
{
  "requestId": "b15f13a4-77d9-4fab-a701-7ad65bcdcaed",
  "metadata": {
    "width": 1024,
    "height": 680,
    "format": "Jpeg"
  },
  "result": {
    "landmarks": [
      {
        "name": "Space Needle",
        "confidence": 0.9448209
      }
    ]
  }
}
```

## <span data-ttu-id="a2596-136">Get a Thumbnail with Computer Vision API Using C# <a name="GetThumbnail"> </a></span><span class="sxs-lookup"><span data-stu-id="a2596-136">Get a Thumbnail with Computer Vision API Using C# <a name="GetThumbnail"> </a></span></span>
<span data-ttu-id="a2596-137">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to crop an image based on its region of interest (ROI) to the height and width you desire.</span><span class="sxs-lookup"><span data-stu-id="a2596-137">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to crop an image based on its region of interest (ROI) to the height and width you desire.</span></span> <span data-ttu-id="a2596-138">You can even pick an aspect ratio that differs from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="a2596-138">You can even pick an aspect ratio that differs from the aspect ratio of the input image.</span></span>

### <a name="get-a-thumbnail-c-example-request"></a><span data-ttu-id="a2596-139">Get a Thumbnail C# Example Request</span><span class="sxs-lookup"><span data-stu-id="a2596-139">Get a Thumbnail C# Example Request</span></span>

```c#
using System;
using System.IO;
using System.Net.Http;
using System.Net.Http.Headers;

namespace CSHttpClientSample
{
    static class Program
    {
        static void Main()
        {
            Console.Write("Enter image file path: ");
            string imageFilePath = Console.ReadLine();

            MakeThumbNailRequest(imageFilePath);

            Console.WriteLine("\n\n\nHit ENTER to exit...");
            Console.ReadLine();
        }

        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }

        static async void MakeThumbNailRequest(string imageFilePath)
        {
            var client = new HttpClient();

            // Request headers - replace this example key with your valid subscription key.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request parameters and URI.
            string requestParameters = "width=200&height=150&smartCropping=true";
            string uri = "https://westus.api.cognitive.microsoft.com/vision/v1.0/generateThumbnail?" + requestParameters;

            HttpResponseMessage response;

            // Request body. Try this sample with a locally stored JPEG image.
            byte[] byteData = GetImageAsByteArray(imageFilePath);

            using (var content = new ByteArrayContent(byteData))
            {
                // This example uses content type "application/octet-stream".
                // The other content types you can use are "application/json" and "multipart/form-data".
                content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
                response = await client.PostAsync(uri, content);
            }
        }
    }
}
```
### <a name="get-a-thumbnail-response"></a><span data-ttu-id="a2596-140">Get a Thumbnail Response</span><span class="sxs-lookup"><span data-stu-id="a2596-140">Get a Thumbnail Response</span></span>
<span data-ttu-id="a2596-141">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="a2596-141">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="a2596-142">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="a2596-142">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span>


## <span data-ttu-id="a2596-143">Optical Character Recognition (OCR) with Computer Vision API Using C#<a name="OCR"> </a></span><span class="sxs-lookup"><span data-stu-id="a2596-143">Optical Character Recognition (OCR) with Computer Vision API Using C#<a name="OCR"> </a></span></span>
<span data-ttu-id="a2596-144">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="a2596-144">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

### <a name="ocr-c-example-request"></a><span data-ttu-id="a2596-145">OCR C# Example Request</span><span class="sxs-lookup"><span data-stu-id="a2596-145">OCR C# Example Request</span></span>
```C#
using System;
using System.IO;
using System.Net.Http;
using System.Net.Http.Headers;

namespace CSHttpClientSample
{
    static class Program
    {
        static void Main()
        {
            Console.Write("Enter image file path: ");
            string imageFilePath = Console.ReadLine();

            MakeOCRRequest(imageFilePath);

            Console.WriteLine("\n\n\nHit ENTER to exit...");
            Console.ReadLine();
        }

        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }

        static async void MakeOCRRequest(string imageFilePath)
        {
            var client = new HttpClient();

            // Request headers - replace this example key with your valid subscription key.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request parameters and URI
            string requestParameters = "language=unk&detectOrientation =true";
            string uri = "https://westus.api.cognitive.microsoft.com/vision/v1.0/ocr?" + requestParameters;

            HttpResponseMessage response;

            // Request body. Try this sample with a locally stored JPEG image.
            byte[] byteData = GetImageAsByteArray(imageFilePath);

            using (var content = new ByteArrayContent(byteData))
            {
                // This example uses content type "application/octet-stream".
                // The other content types you can use are "application/json" and "multipart/form-data".
                content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
                response = await client.PostAsync(uri, content);
            }
        }
    }
}
```

### <a name="ocr-example-response"></a><span data-ttu-id="a2596-146">OCR Example Response</span><span class="sxs-lookup"><span data-stu-id="a2596-146">OCR Example Response</span></span>
<span data-ttu-id="a2596-147">Upon success, the OCR results returned include text, bounding box for regions, lines, and words.</span><span class="sxs-lookup"><span data-stu-id="a2596-147">Upon success, the OCR results returned include text, bounding box for regions, lines, and words.</span></span>

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
## <span data-ttu-id="a2596-148">Text Recognition with Computer Vision API Using C# <a name="RecognizeText"> </a></span><span class="sxs-lookup"><span data-stu-id="a2596-148">Text Recognition with Computer Vision API Using C# <a name="RecognizeText"> </a></span></span>
<span data-ttu-id="a2596-149">Use the [RecognizeText method](https://ocr.portal.azure-api.net/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200) to detect handwritten or printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="a2596-149">Use the [RecognizeText method](https://ocr.portal.azure-api.net/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200) to detect handwritten or printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

### <a name="handwriting-recognition-c-example"></a><span data-ttu-id="a2596-150">Handwriting Recognition C# Example</span><span class="sxs-lookup"><span data-stu-id="a2596-150">Handwriting Recognition C# Example</span></span>
```c#
using System;
using System.IO;
using System.Collections;
using System.Collections.Generic;
using System.Net.Http;
using System.Net.Http.Headers;

namespace CSHttpClientSample
{
    static class Program
    {
        static void Main()
        {
            Console.Write("Enter image file path: ");
            string imageFilePath = Console.ReadLine();

            ReadHandwrittenText(imageFilePath);

            Console.WriteLine("\n\n\nHit ENTER to exit...");
            Console.ReadLine();
        }

        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }

        static async void ReadHandwrittenText(string imageFilePath)
        {
            var client = new HttpClient();

            // Request headers - replace this example key with your valid subscription key.
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");

            // Request parameters and URI. Set "handwriting" to false for printed text.
            string requestParameter = "handwriting=true";
            string uri = "https://westus.api.cognitive.microsoft.com/vision/v1.0/recognizeText?" + requestParameter;

            HttpResponseMessage response = null;
            IEnumerable<string> responseValues = null;
            string operationLocation = null;

            // Request body. Try this sample with a locally stored JPEG image.
            byte[] byteData = GetImageAsByteArray(imageFilePath);
            var content = new ByteArrayContent(byteData);

            // This example uses content type "application/octet-stream".
            // You can also use "application/json" and specify an image URL.
            content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");

            try {
                response = await client.PostAsync(uri, content);
                responseValues = response.Headers.GetValues("Operation-Location");
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
            }

            foreach (var value in responseValues)
            {
                // This value is the URI where you can get the text recognition operation result.
                operationLocation = value;
                Console.WriteLine(operationLocation);
                break;
            }

            try
            {
                // Note: The response may not be immediately available. Handwriting recognition is an
                // async operation that can take a variable amount of time depending on the length
                // of the text you want to recognize. You may need to wait or retry this operation.
                response = await client.GetAsync(operationLocation);

                // And now you can see the response in in JSON:
                Console.WriteLine(await response.Content.ReadAsStringAsync());
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
            }
        }
    }
}
```