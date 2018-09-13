---
title: Computer Vision API JavaScript quick starts | Microsoft Docs
description: Get information and code samples to help you quickly get started using JavaScript and the Computer Vision API in Cognitive Services.
services: cognitive-services
author: JuliaNik
manager: ytkuo
ms.service: cognitive-services
ms.technology: computer-vision
ms.topic: article
ms.date: 02/06/2017
ms.author: juliakuz
ms.openlocfilehash: e05776f4b5914d829981a7550045ad6b3b9e88c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540911"
---
# <a name="computer-vision-javascript-quick-starts"></a><span data-ttu-id="dfdd7-103">Computer Vision JavaScript Quick Starts</span><span class="sxs-lookup"><span data-stu-id="dfdd7-103">Computer Vision JavaScript Quick Starts</span></span>
<span data-ttu-id="dfdd7-104">This article provides information and code samples to help you quickly get started using JavaScript and the Computer Vision API to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="dfdd7-104">This article provides information and code samples to help you quickly get started using JavaScript and the Computer Vision API to accomplish the following tasks:</span></span> 
* [<span data-ttu-id="dfdd7-105">Analyze an image</span><span class="sxs-lookup"><span data-stu-id="dfdd7-105">Analyze an image</span></span>](#AnalyzeImage) 
* [<span data-ttu-id="dfdd7-106">Use a Domain-Specific Model</span><span class="sxs-lookup"><span data-stu-id="dfdd7-106">Use a Domain-Specific Model</span></span>](#DomainSpecificModel)
* [<span data-ttu-id="dfdd7-107">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="dfdd7-107">Intelligently generate a thumbnail</span></span>](#GetThumbnail)
* [<span data-ttu-id="dfdd7-108">Detect and extract text from an Image</span><span class="sxs-lookup"><span data-stu-id="dfdd7-108">Detect and extract text from an Image</span></span>](#OCR)

<span data-ttu-id="dfdd7-109">Learn more about obtaining free Subscription Keys [here](../Vision-API-How-to-Topics/HowToSubscribe.md)</span><span class="sxs-lookup"><span data-stu-id="dfdd7-109">Learn more about obtaining free Subscription Keys [here](../Vision-API-How-to-Topics/HowToSubscribe.md)</span></span>

## <span data-ttu-id="dfdd7-110">Analyze an Image With Computer Vision API Using JavaScript <a name="AnalyzeImage"> </a></span><span class="sxs-lookup"><span data-stu-id="dfdd7-110">Analyze an Image With Computer Vision API Using JavaScript <a name="AnalyzeImage"> </a></span></span>
<span data-ttu-id="dfdd7-111">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-111">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa) you can extract visual features based on image content.</span></span> <span data-ttu-id="dfdd7-112">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="dfdd7-112">You can upload an image or specify an image URL and choose which features to return, including:</span></span>
* <span data-ttu-id="dfdd7-113">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="dfdd7-113">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span> 
* <span data-ttu-id="dfdd7-114">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-114">A detailed list of tags related to the image content.</span></span> 
* <span data-ttu-id="dfdd7-115">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-115">A description of image content in a complete sentence.</span></span> 
* <span data-ttu-id="dfdd7-116">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-116">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="dfdd7-117">The ImageType (clipart or a line drawing)</span><span class="sxs-lookup"><span data-stu-id="dfdd7-117">The ImageType (clipart or a line drawing)</span></span>
* <span data-ttu-id="dfdd7-118">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-118">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="dfdd7-119">Whether the image contains pornographic or sexually suggestive content.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-119">Whether the image contains pornographic or sexually suggestive content.</span></span> 

### <a name="analyze-an-image-javascript-example-request"></a><span data-ttu-id="dfdd7-120">Analyze an Image JavaScript Example Request</span><span class="sxs-lookup"><span data-stu-id="dfdd7-120">Analyze an Image JavaScript Example Request</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <title>JSSample</title>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>
</head>
<body>

<script type="text/javascript">
    $(function() {
        var params = {
            // Request parameters
            "visualFeatures": "Categories",
            "details": "{string}",
            "language": "en",
        };
      
        $.ajax({
            url: "https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze?" + $.param(params),
            beforeSend: function(xhrObj){
                // Request headers
                xhrObj.setRequestHeader("Content-Type","application/json");
                xhrObj.setRequestHeader("Ocp-Apim-Subscription-Key","{subscription key}");
            },
            type: "POST",
            // Request body
            data: "{body}",
        })
        .done(function(data) {
            alert("success");
        })
        .fail(function() {
            alert("error");
        });
    });
</script>
</body>
</html>
```
### <a name="analyze-an-image-response"></a><span data-ttu-id="dfdd7-121">Analyze an Image Response</span><span class="sxs-lookup"><span data-stu-id="dfdd7-121">Analyze an Image Response</span></span>
<span data-ttu-id="dfdd7-122">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-122">A successful response is returned in JSON.</span></span> <span data-ttu-id="dfdd7-123">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="dfdd7-123">Following is an example of a successful response:</span></span> 

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

## <span data-ttu-id="dfdd7-124">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span><span class="sxs-lookup"><span data-stu-id="dfdd7-124">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span></span>
<span data-ttu-id="dfdd7-125">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-125">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span></span> <span data-ttu-id="dfdd7-126">The two domain-specific models that are currently available are celebrities and landmarks.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-126">The two domain-specific models that are currently available are celebrities and landmarks.</span></span> <span data-ttu-id="dfdd7-127">The following example identifies a landmark in an image.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-127">The following example identifies a landmark in an image.</span></span>

### <a name="landmark-javascript-example-request"></a><span data-ttu-id="dfdd7-128">Landmark JavaScript Example Request</span><span class="sxs-lookup"><span data-stu-id="dfdd7-128">Landmark JavaScript Example Request</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript Sample</title>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>
</head>
<body>

<script type="text/javascript">
    $(function() {
        var params = {
            // Request parameters
            "model": "landmarks", // Use "model": "celebrities" to use the Celebrities model.
        };

        $.ajax({
            // Change "landmarks" to "celebrities" in the url to use the Celebrities model.
            url: "https://westus.api.cognitive.microsoft.com/vision/v1.0/models/landmarks/analyze?" + $.param(params),

            beforeSend: function(xhrObj){
                // Request headers
                xhrObj.setRequestHeader("Content-Type", "application/json");
    
                // Replace the "Ocp-Apim-Subscription-Key" value with a valid subscription key.
                xhrObj.setRequestHeader("Ocp-Apim-Subscription-Key", "13hc77781f7e4b19b5fcdd72a8df7156");
            },

            type: "POST",

            // Request body
            data: '{"url": "https://upload.wikimedia.org/wikipedia/commons/2/23/Space_Needle_2011-07-04.jpg"}',
        })
        
        .done(function(data) {
            $("#responseTextArea").val(JSON.stringify(data, null, 2));
        })
        
        .fail(function(jqXHR, textStatus, errorThrown) {
            var errorString = (errorThrown === "") ? "Error. " : errorThrown + " (" + jqXHR.status + "): ";
            errorString += (jqXHR.responseText === "") ? "" : jQuery.parseJSON(jqXHR.responseText).message;
            alert(errorString);
        });
    });
</script>
REST response:
<br><br>
<textarea id="responseTextArea" class="UIInput" cols="120" rows="32"></textarea>
</body>
</html>
```

### <a name="landmark-example-response"></a><span data-ttu-id="dfdd7-129">Landmark Example Response</span><span class="sxs-lookup"><span data-stu-id="dfdd7-129">Landmark Example Response</span></span>
<span data-ttu-id="dfdd7-130">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-130">A successful response is returned in JSON.</span></span> <span data-ttu-id="dfdd7-131">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="dfdd7-131">Following is an example of a successful response:</span></span>  

```json
{
  "requestId": "e0970003-1cb7-4ac6-b0d4-f36a1914bf4e",
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

## <span data-ttu-id="dfdd7-132">Get a Thumbnail with Computer Vision API Using JavaScript <a name="GetThumbnail"> </a></span><span class="sxs-lookup"><span data-stu-id="dfdd7-132">Get a Thumbnail with Computer Vision API Using JavaScript <a name="GetThumbnail"> </a></span></span>
<span data-ttu-id="dfdd7-133">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to  crop an image based on its region of interest (ROI) to the height and width you desire, even if the aspect ratio differs from the input image.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-133">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to  crop an image based on its region of interest (ROI) to the height and width you desire, even if the aspect ratio differs from the input image.</span></span> 

### <a name="get-a-thumbnail-javascript-example-request"></a><span data-ttu-id="dfdd7-134">Get a Thumbnail JavaScript Example Request</span><span class="sxs-lookup"><span data-stu-id="dfdd7-134">Get a Thumbnail JavaScript Example Request</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <title>JSSample</title>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>
</head>
<body>

<script type="text/javascript">
    $(function() {
        var params = {
            // Request parameters
            "width": "{number}",
            "height": "{number}",
            "smartCropping": "true",
        };
      
        $.ajax({
            url: "https://westus.api.cognitive.microsoft.com/vision/v1.0/generateThumbnail?" + $.param(params),
            beforeSend: function(xhrObj){
                // Request headers
                xhrObj.setRequestHeader("Content-Type","application/json");
                xhrObj.setRequestHeader("Ocp-Apim-Subscription-Key","{subscription key}");
            },
            type: "POST",
            // Request body
            data: "{body}",
        })
        .done(function(data) {
            alert("success");
        })
        .fail(function() {
            alert("error");
        });
    });
</script>
</body>
</html>
```
### <a name="get-a-thumbnail-response"></a><span data-ttu-id="dfdd7-135">Get a Thumbnail Response</span><span class="sxs-lookup"><span data-stu-id="dfdd7-135">Get a Thumbnail Response</span></span>
<span data-ttu-id="dfdd7-136">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-136">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="dfdd7-137">If the request failed, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-137">If the request failed, the response contains an error code and a message to help determine what went wrong.</span></span>


## <span data-ttu-id="dfdd7-138">Optical Character Recognition (OCR) with Computer Vision API Using JavaScript<a name="OCR"> </a></span><span class="sxs-lookup"><span data-stu-id="dfdd7-138">Optical Character Recognition (OCR) with Computer Vision API Using JavaScript<a name="OCR"> </a></span></span>
<span data-ttu-id="dfdd7-139">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-139">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect text in an image and extract recognized characters into a machine-usable character stream.</span></span>

### <a name="ocr-javascript-example-request"></a><span data-ttu-id="dfdd7-140">OCR JavaScript Example Request</span><span class="sxs-lookup"><span data-stu-id="dfdd7-140">OCR JavaScript Example Request</span></span>
```html
<!DOCTYPE html>
<html>
<head>
    <title>JSSample</title>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>
</head>
<body>

<script type="text/javascript">
    $(function() {
        var params = {
            // Request parameters
            "language": "unk",
            "detectOrientation ": "true",
        };
      
        $.ajax({
            url: "https://westus.api.cognitive.microsoft.com/vision/v1.0/ocr?" + $.param(params),
            beforeSend: function(xhrObj){
                // Request headers
                xhrObj.setRequestHeader("Content-Type","application/json");
                xhrObj.setRequestHeader("Ocp-Apim-Subscription-Key","{subscription key}");
            },
            type: "POST",
            // Request body
            data: "{body}",
        })
        .done(function(data) {
            alert("success");
        })
        .fail(function() {
            alert("error");
        });
    });
</script>
</body>
</html>

```

### <a name="ocr-example-response"></a><span data-ttu-id="dfdd7-141">OCR Example Response</span><span class="sxs-lookup"><span data-stu-id="dfdd7-141">OCR Example Response</span></span>
<span data-ttu-id="dfdd7-142">Upon success, the OCR results returned include text, bounding box for regions, lines and words.</span><span class="sxs-lookup"><span data-stu-id="dfdd7-142">Upon success, the OCR results returned include text, bounding box for regions, lines and words.</span></span> 

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

