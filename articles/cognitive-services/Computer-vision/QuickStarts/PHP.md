---
title: Computer Vision API PHP quick starts | Microsoft Docs
description: Get information and code samples to help you quickly get started using PHP and the Computer Vision API in Cognitive Services.
services: cognitive-services
author: JuliaNik
manager: ytkuo
ms.service: cognitive-services
ms.technology: computer-vision
ms.topic: article
ms.date: 02/06/2017
ms.author: juliakuz
ms.openlocfilehash: ea50384e00aa86fa8f399d91f7910889797b71af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660558"
---
# <a name="computer-vision-php-quick-starts"></a><span data-ttu-id="33a40-103">Computer Vision PHP Quick Starts</span><span class="sxs-lookup"><span data-stu-id="33a40-103">Computer Vision PHP Quick Starts</span></span>
<span data-ttu-id="33a40-104">This article provides information and code samples to help you quickly get started using PHP and the Computer Vision API to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="33a40-104">This article provides information and code samples to help you quickly get started using PHP and the Computer Vision API to accomplish the following tasks:</span></span> 
* [<span data-ttu-id="33a40-105">Analyze an image</span><span class="sxs-lookup"><span data-stu-id="33a40-105">Analyze an image</span></span>](#AnalyzeImage) 
* [<span data-ttu-id="33a40-106">Use a Domain-Specific Model</span><span class="sxs-lookup"><span data-stu-id="33a40-106">Use a Domain-Specific Model</span></span>](#DomainSpecificModel)
* [<span data-ttu-id="33a40-107">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="33a40-107">Intelligently generate a thumbnail</span></span>](#GetThumbnail)
* [<span data-ttu-id="33a40-108">Detect and extract text from an Image</span><span class="sxs-lookup"><span data-stu-id="33a40-108">Detect and extract text from an Image</span></span>](#OCR)

<span data-ttu-id="33a40-109">Learn more about obtaining free Subscription Keys [here](../Vision-API-How-to-Topics/HowToSubscribe.md)</span><span class="sxs-lookup"><span data-stu-id="33a40-109">Learn more about obtaining free Subscription Keys [here](../Vision-API-How-to-Topics/HowToSubscribe.md)</span></span>

## <span data-ttu-id="33a40-110">Analyze an Image With Computer Vision API Using PHP <a name="AnalyzeImage"> </a></span><span class="sxs-lookup"><span data-stu-id="33a40-110">Analyze an Image With Computer Vision API Using PHP <a name="AnalyzeImage"> </a></span></span>
<span data-ttu-id="33a40-111">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="33a40-111">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) you can extract visual features based on image content.</span></span> <span data-ttu-id="33a40-112">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="33a40-112">You can upload an image or specify an image URL and choose which features to return, including:</span></span>
* <span data-ttu-id="33a40-113">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="33a40-113">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span> 
* <span data-ttu-id="33a40-114">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="33a40-114">A detailed list of tags related to the image content.</span></span> 
* <span data-ttu-id="33a40-115">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="33a40-115">A description of image content in a complete sentence.</span></span> 
* <span data-ttu-id="33a40-116">The coordinates, gender and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="33a40-116">The coordinates, gender and age of any faces contained in the image.</span></span>
* <span data-ttu-id="33a40-117">The ImageType (clipart or a line drawing)</span><span class="sxs-lookup"><span data-stu-id="33a40-117">The ImageType (clipart or a line drawing)</span></span>
* <span data-ttu-id="33a40-118">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="33a40-118">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="33a40-119">Whether the image contains pornographic or sexually suggestive content.</span><span class="sxs-lookup"><span data-stu-id="33a40-119">Whether the image contains pornographic or sexually suggestive content.</span></span> 

### <a name="analyze-an-image-php-example-request"></a><span data-ttu-id="33a40-120">Analyze an Image PHP Example Request</span><span class="sxs-lookup"><span data-stu-id="33a40-120">Analyze an Image PHP Example Request</span></span>

```PHP
<?php
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
require_once 'HTTP/Request2.php';

$request = new Http_Request2('https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => '{subscription key}',
);

$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'visualFeatures' => 'Categories',
    'details' => '{string}',
    'language' => 'en',
);

$url->setQueryVariables($parameters);

$request->setMethod(HTTP_Request2::METHOD_POST);

// Request body
$request->setBody("{body}");

try
{
    $response = $request->send();
    echo $response->getBody();
}
catch (HttpException $ex)
{
    echo $ex;
}

?>

```

### <a name="analyze-an-image-response"></a><span data-ttu-id="33a40-121">Analyze an Image Response</span><span class="sxs-lookup"><span data-stu-id="33a40-121">Analyze an Image Response</span></span>
<span data-ttu-id="33a40-122">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="33a40-122">A successful response is returned in JSON.</span></span> <span data-ttu-id="33a40-123">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="33a40-123">Following is an example of a successful response:</span></span> 

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

## <span data-ttu-id="33a40-124">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span><span class="sxs-lookup"><span data-stu-id="33a40-124">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span></span>
<span data-ttu-id="33a40-125">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span><span class="sxs-lookup"><span data-stu-id="33a40-125">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span></span> <span data-ttu-id="33a40-126">The two domain-specific models that are currently available are celebrities and landmarks.</span><span class="sxs-lookup"><span data-stu-id="33a40-126">The two domain-specific models that are currently available are celebrities and landmarks.</span></span> <span data-ttu-id="33a40-127">The following example identifies a landmark in an image.</span><span class="sxs-lookup"><span data-stu-id="33a40-127">The following example identifies a landmark in an image.</span></span>

### <a name="landmark-php-example-request"></a><span data-ttu-id="33a40-128">Landmark PHP Example Request</span><span class="sxs-lookup"><span data-stu-id="33a40-128">Landmark PHP Example Request</span></span>

```PHP
<html>
<head>
    <title>PHP Sample</title>
</head>
<body>
<?php
// This sample uses PEAR (https://pear.php.net/package/HTTP_Request2/download)
require_once 'HTTP/Request2.php';

// Change "landmarks" to "celebrities" in the url to use the Celebrities model.
$request = new Http_Request2('https://westus.api.cognitive.microsoft.com/vision/v1.0/models/landmarks/analyze');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => '13hc77781f7e4b19b5fcdd72a8df7156',
);

$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'model' => 'landmarks',   // Use 'model' => 'celebrities' to use the Celebrities model.
);

$url->setQueryVariables($parameters);

$request->setMethod(HTTP_Request2::METHOD_POST);

// Request body
$body = json_encode(array(
    // Request body parameters
    'url' => 'https://upload.wikimedia.org/wikipedia/commons/2/23/Space_Needle_2011-07-04.jpg',
));
$request->setBody($body);

try
{
    $response = $request->send();
    echo "<pre>" . json_encode(json_decode($response->getBody()), JSON_PRETTY_PRINT) . "</pre>";
}
catch (HttpException $ex)
{
    echo "<pre>" . $ex . "</pre>";
}
?>
</body>
</html>
```

### <a name="landmark-example-response"></a><span data-ttu-id="33a40-129">Landmark Example Response</span><span class="sxs-lookup"><span data-stu-id="33a40-129">Landmark Example Response</span></span>
<span data-ttu-id="33a40-130">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="33a40-130">A successful response is returned in JSON.</span></span> <span data-ttu-id="33a40-131">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="33a40-131">Following is an example of a successful response:</span></span>  

```json
{
    "requestId": "0663b074-8eb3-4fab-a72e-4c31a49bd22e",
    "metadata": {
        "width": 2096,
        "height": 4132,
        "format": "Jpeg"
    },
    "result": {
        "landmarks": [
            {
                "name": "Space Needle",
                "confidence": 0.9998178
            }
        ]
    }
}
```

## <span data-ttu-id="33a40-132">Get a Thumbnail with Computer Vision API Using PHP <a name="GetThumbnail"> </a></span><span class="sxs-lookup"><span data-stu-id="33a40-132">Get a Thumbnail with Computer Vision API Using PHP <a name="GetThumbnail"> </a></span></span>
<span data-ttu-id="33a40-133">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to  crop an image based on its region of interest (ROI) to the height and width you desire, even if the aspect ratio differs from the input image.</span><span class="sxs-lookup"><span data-stu-id="33a40-133">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to  crop an image based on its region of interest (ROI) to the height and width you desire, even if the aspect ratio differs from the input image.</span></span> 

### <a name="get-a-thumbnail-php-example-request"></a><span data-ttu-id="33a40-134">Get a Thumbnail PHP Example Request</span><span class="sxs-lookup"><span data-stu-id="33a40-134">Get a Thumbnail PHP Example Request</span></span>

```PHP
<?php
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
require_once 'HTTP/Request2.php';

$request = new Http_Request2('https://westus.api.cognitive.microsoft.com/vision/v1.0/generateThumbnail');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => '{subscription key}',
);

$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'width' => '{number}',
    'height' => '{number}',
    'smartCropping' => 'true',
);

$url->setQueryVariables($parameters);

$request->setMethod(HTTP_Request2::METHOD_POST);

// Request body
$request->setBody("{body}");

try
{
    $response = $request->send();
    echo $response->getBody();
}
catch (HttpException $ex)
{
    echo $ex;
}

?>
```

### <a name="get-a-thumbnail-response"></a><span data-ttu-id="33a40-135">Get a Thumbnail Response</span><span class="sxs-lookup"><span data-stu-id="33a40-135">Get a Thumbnail Response</span></span>
<span data-ttu-id="33a40-136">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="33a40-136">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="33a40-137">If the request failed, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="33a40-137">If the request failed, the response contains an error code and a message to help determine what went wrong.</span></span>


## <span data-ttu-id="33a40-138">Optical Character Recognition (OCR) with Computer Vision API Using PHP <a name="OCR"> </a></span><span class="sxs-lookup"><span data-stu-id="33a40-138">Optical Character Recognition (OCR) with Computer Vision API Using PHP <a name="OCR"> </a></span></span>
<span data-ttu-id="33a40-139">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="33a40-139">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect text in an image and extract recognized characters into a machine-usable character stream.</span></span>

### <a name="ocr-php-example-request"></a><span data-ttu-id="33a40-140">OCR PHP Example Request</span><span class="sxs-lookup"><span data-stu-id="33a40-140">OCR PHP Example Request</span></span>
```PHP
<?php
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
require_once 'HTTP/Request2.php';

$request = new Http_Request2('https://westus.api.cognitive.microsoft.com/vision/v1.0/ocr');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => '{subscription key}',
);

$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'language' => 'unk',
    'detectOrientation ' => 'true',
);

$url->setQueryVariables($parameters);

$request->setMethod(HTTP_Request2::METHOD_POST);

// Request body
$request->setBody("{body}");

try
{
    $response = $request->send();
    echo $response->getBody();
}
catch (HttpException $ex)
{
    echo $ex;
}

?>
```

### <a name="ocr-example-response"></a><span data-ttu-id="33a40-141">OCR Example Response</span><span class="sxs-lookup"><span data-stu-id="33a40-141">OCR Example Response</span></span>
<span data-ttu-id="33a40-142">Upon success, the OCR results are returned include include text, bounding box for regions, lines and words.</span><span class="sxs-lookup"><span data-stu-id="33a40-142">Upon success, the OCR results are returned include include text, bounding box for regions, lines and words.</span></span> 

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
