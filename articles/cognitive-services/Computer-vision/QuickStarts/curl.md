---
title: Computer Vision API cURL quick starts | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Computer Vision API with cURL in Cognitive Services.
services: cognitive-services
author: JuliaNik
manager: ytkuo
ms.service: cognitive-services
ms.technology: computer-vision
ms.topic: article
ms.date: 02/06/2017
ms.author: juliakuz
ms.openlocfilehash: 1ff737a8fcab95a6e88816a31cb7260b86eba086
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563006"
---
# <a name="computer-vision-curl-quick-starts"></a><span data-ttu-id="c542d-103">Computer Vision cURL Quick Starts</span><span class="sxs-lookup"><span data-stu-id="c542d-103">Computer Vision cURL Quick Starts</span></span>
<span data-ttu-id="c542d-104">This article provides information and code samples to help you quickly get started using the Computer Vision API with cURL to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="c542d-104">This article provides information and code samples to help you quickly get started using the Computer Vision API with cURL to accomplish the following tasks:</span></span>
* [<span data-ttu-id="c542d-105">Analyze an image</span><span class="sxs-lookup"><span data-stu-id="c542d-105">Analyze an image</span></span>](#AnalyzeImage) 
* [<span data-ttu-id="c542d-106">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="c542d-106">Intelligently generate a thumbnail</span></span>](#GetThumbnail)
* [<span data-ttu-id="c542d-107">Detect and extract text from an Image</span><span class="sxs-lookup"><span data-stu-id="c542d-107">Detect and extract text from an Image</span></span>](#OCR)

<span data-ttu-id="c542d-108">Learn more about obtaining free Subscription Keys [here](../Vision-API-How-to-Topics/HowToSubscribe.md)</span><span class="sxs-lookup"><span data-stu-id="c542d-108">Learn more about obtaining free Subscription Keys [here](../Vision-API-How-to-Topics/HowToSubscribe.md)</span></span>

## <span data-ttu-id="c542d-109">Analyze an Image With Computer Vision API Using cURL <a name="AnalyzeImage"> </a></span><span class="sxs-lookup"><span data-stu-id="c542d-109">Analyze an Image With Computer Vision API Using cURL <a name="AnalyzeImage"> </a></span></span>
<span data-ttu-id="c542d-110">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="c542d-110">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) you can extract visual features based on image content.</span></span> <span data-ttu-id="c542d-111">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="c542d-111">You can upload an image or specify an image URL and choose which features to return, including:</span></span>
* <span data-ttu-id="c542d-112">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="c542d-112">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span> 
* <span data-ttu-id="c542d-113">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="c542d-113">A detailed list of tags related to the image content.</span></span> 
* <span data-ttu-id="c542d-114">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="c542d-114">A description of image content in a complete sentence.</span></span> 
* <span data-ttu-id="c542d-115">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="c542d-115">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="c542d-116">The ImageType (clipart or a line drawing)</span><span class="sxs-lookup"><span data-stu-id="c542d-116">The ImageType (clipart or a line drawing)</span></span>
* <span data-ttu-id="c542d-117">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="c542d-117">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="c542d-118">Whether the image contains pornographic or sexually suggestive content.</span><span class="sxs-lookup"><span data-stu-id="c542d-118">Whether the image contains pornographic or sexually suggestive content.</span></span> 

### <a name="analyze-an-image-curl-example-request"></a><span data-ttu-id="c542d-119">Analyze an Image curl Example Request</span><span class="sxs-lookup"><span data-stu-id="c542d-119">Analyze an Image curl Example Request</span></span>

```json

@ECHO OFF

curl -v -X POST "https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Categories&details={string}&language=en"
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {subscription key}"

--data-ascii "{body}" 

```
### <a name="analyze-an-image-response"></a><span data-ttu-id="c542d-120">Analyze an Image Response</span><span class="sxs-lookup"><span data-stu-id="c542d-120">Analyze an Image Response</span></span>
<span data-ttu-id="c542d-121">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="c542d-121">A successful response is returned in JSON.</span></span> <span data-ttu-id="c542d-122">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="c542d-122">Following is an example of a successful response:</span></span> 

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

## <span data-ttu-id="c542d-123">Get a Thumbnail with Computer Vision API Using curl <a name="GetThumbnail"> </a></span><span class="sxs-lookup"><span data-stu-id="c542d-123">Get a Thumbnail with Computer Vision API Using curl <a name="GetThumbnail"> </a></span></span>
<span data-ttu-id="c542d-124">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to  crop an image based on its region of interest (ROI) to the height and width you desire, even if the aspect ratio differs from the input image.</span><span class="sxs-lookup"><span data-stu-id="c542d-124">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to  crop an image based on its region of interest (ROI) to the height and width you desire, even if the aspect ratio differs from the input image.</span></span> 

### <a name="get-a-thumbnail-curl-example-request"></a><span data-ttu-id="c542d-125">Get a Thumbnail curl Example Request</span><span class="sxs-lookup"><span data-stu-id="c542d-125">Get a Thumbnail curl Example Request</span></span>

```JSON
@ECHO OFF

curl -v -X POST "https://westus.api.cognitive.microsoft.com/vision/v1.0/generateThumbnail?width={number}&height={number}&smartCropping=true"
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {subscription key}"

--data-ascii "{body}" 
```
### <a name="get-a-thumbnail-response"></a><span data-ttu-id="c542d-126">Get a Thumbnail Response</span><span class="sxs-lookup"><span data-stu-id="c542d-126">Get a Thumbnail Response</span></span>
<span data-ttu-id="c542d-127">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="c542d-127">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="c542d-128">If the request failed, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="c542d-128">If the request failed, the response contains an error code and a message to help determine what went wrong.</span></span>


## <span data-ttu-id="c542d-129">Optical Character Recognition (OCR) with Computer Vision API Using curl <a name="OCR"> </a></span><span class="sxs-lookup"><span data-stu-id="c542d-129">Optical Character Recognition (OCR) with Computer Vision API Using curl <a name="OCR"> </a></span></span>
<span data-ttu-id="c542d-130">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="c542d-130">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect text in an image and extract recognized characters into a machine-usable character stream.</span></span>

### <a name="ocr-curl-example-request"></a><span data-ttu-id="c542d-131">OCR curl Example Request</span><span class="sxs-lookup"><span data-stu-id="c542d-131">OCR curl Example Request</span></span>
```JSON
@ECHO OFF

curl -v -X POST "https://westus.api.cognitive.microsoft.com/vision/v1.0/ocr?language=unk&detectOrientation =true"
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {subscription key}"

--data-ascii "{body}" 
```

### <a name="ocr-example-response"></a><span data-ttu-id="c542d-132">OCR Example Response</span><span class="sxs-lookup"><span data-stu-id="c542d-132">OCR Example Response</span></span>
<span data-ttu-id="c542d-133">Upon success, the OCR results returned include text, bounding box for regions, lines and words.</span><span class="sxs-lookup"><span data-stu-id="c542d-133">Upon success, the OCR results returned include text, bounding box for regions, lines and words.</span></span> 

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
