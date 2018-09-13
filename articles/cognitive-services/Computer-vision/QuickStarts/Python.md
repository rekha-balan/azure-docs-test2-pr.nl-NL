---
title: Computer Vision API Python quick start | Microsoft Docs
description: Get information and code samples to help you quickly get started using Python and the Computer Vision API in Microsoft Cognitive Services.
services: cognitive-services
author: JuliaNik
manager: ytkuo
ms.service: cognitive-services
ms.technology: computer-vision
ms.topic: article
ms.date: 02/22/2017
ms.author: juliakuz
ms.openlocfilehash: a8da78baf8f0d5dafcec2dc7ae2ab31855e3dac0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562997"
---
# <a name="computer-vision-python-quick-starts"></a><span data-ttu-id="b678b-103">Computer Vision Python Quick Starts</span><span class="sxs-lookup"><span data-stu-id="b678b-103">Computer Vision Python Quick Starts</span></span>
<span data-ttu-id="b678b-104">This article provides information and code samples to help you quickly get started using the Computer Vision API with Python to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="b678b-104">This article provides information and code samples to help you quickly get started using the Computer Vision API with Python to accomplish the following tasks:</span></span>
* [<span data-ttu-id="b678b-105">Analyze an image</span><span class="sxs-lookup"><span data-stu-id="b678b-105">Analyze an image</span></span>](#AnalyzeImage)
* [<span data-ttu-id="b678b-106">Use a Domain-Specific Model</span><span class="sxs-lookup"><span data-stu-id="b678b-106">Use a Domain-Specific Model</span></span>](#DomainSpecificModel)
* [<span data-ttu-id="b678b-107">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="b678b-107">Intelligently generate a thumbnail</span></span>](#GetThumbnail)
* [<span data-ttu-id="b678b-108">Detect and extract printed text from an image</span><span class="sxs-lookup"><span data-stu-id="b678b-108">Detect and extract printed text from an image</span></span>](#OCR)
* [<span data-ttu-id="b678b-109">Detect and extract handwritten text from an image</span><span class="sxs-lookup"><span data-stu-id="b678b-109">Detect and extract handwritten text from an image</span></span>](#RecognizeText)

<span data-ttu-id="b678b-110">To use the Computer Vision API, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="b678b-110">To use the Computer Vision API, you need a subscription key.</span></span> <span data-ttu-id="b678b-111">You can get free subscription keys [here](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/vision-api-how-to-topics/HowToSubscribe).</span><span class="sxs-lookup"><span data-stu-id="b678b-111">You can get free subscription keys [here](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/vision-api-how-to-topics/HowToSubscribe).</span></span>

## <span data-ttu-id="b678b-112">Analyze an Image With Computer Vision API Using Python <a name="AnalyzeImage"> </a></span><span class="sxs-lookup"><span data-stu-id="b678b-112">Analyze an Image With Computer Vision API Using Python <a name="AnalyzeImage"> </a></span></span>
<span data-ttu-id="b678b-113">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="b678b-113">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="b678b-114">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="b678b-114">You can upload an image or specify an image URL and choose which features to return, including:</span></span>
* <span data-ttu-id="b678b-115">The category defined in this [taxonomy](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/Category-Taxonomy).</span><span class="sxs-lookup"><span data-stu-id="b678b-115">The category defined in this [taxonomy](https://www.microsoft.com/cognitive-services/en-us/Computer-Vision-API/documentation/Category-Taxonomy).</span></span>
* <span data-ttu-id="b678b-116">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="b678b-116">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="b678b-117">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="b678b-117">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="b678b-118">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="b678b-118">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="b678b-119">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="b678b-119">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="b678b-120">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="b678b-120">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="b678b-121">Does the image contains adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="b678b-121">Does the image contains adult or sexually suggestive content?</span></span>

### <a name="analyze-an-image-python-example-request"></a><span data-ttu-id="b678b-122">Analyze an Image Python Example Request</span><span class="sxs-lookup"><span data-stu-id="b678b-122">Analyze an Image Python Example Request</span></span>

```Python
########### Python 2.7 #############
import httplib, urllib, base64

headers = {
    # Request headers. Replace the key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

params = urllib.urlencode({
    # Request parameters. All of them are optional.
    'visualFeatures': 'Categories',
    'details': 'Celebrities',
    'language': 'en',
})

# Replace the three dots below with the URL of a JPEG image of a celebrity.
body = "{'url':'...'}"

try:
    conn = httplib.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/vision/v1.0/analyze?%s" % params, body, headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))

####################################

########### Python 3.2 #############
import http.client, urllib.request, urllib.parse, urllib.error, base64

headers = {
    # Request headers. Replace the key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

params = urllib.parse.urlencode({
    # Request parameters. All of them are optional.
    'visualFeatures': 'Categories',
    'details': 'Celebrities',
    'language': 'en',
})

# Replace the three dots below with the URL of a JPEG image of a celebrity.
body = "{'url':'...'}"

try:
    conn = http.client.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/vision/v1.0/analyze?%s" % params, body, headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))
####################################

```

### <a name="analyze-an-image-response"></a><span data-ttu-id="b678b-123">Analyze an Image Response</span><span class="sxs-lookup"><span data-stu-id="b678b-123">Analyze an Image Response</span></span>
<span data-ttu-id="b678b-124">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="b678b-124">A successful response is returned in JSON.</span></span> <span data-ttu-id="b678b-125">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="b678b-125">Following is an example of a successful response:</span></span>

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

## <span data-ttu-id="b678b-126">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span><span class="sxs-lookup"><span data-stu-id="b678b-126">Use a Domain-Specific Model <a name="DomainSpecificModel"> </a></span></span>
<span data-ttu-id="b678b-127">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span><span class="sxs-lookup"><span data-stu-id="b678b-127">The Domain-Specific Model is a model trained to identify a specific set of objects in an image.</span></span> <span data-ttu-id="b678b-128">The two domain-specific models that are currently available are celebrities and landmarks.</span><span class="sxs-lookup"><span data-stu-id="b678b-128">The two domain-specific models that are currently available are celebrities and landmarks.</span></span> <span data-ttu-id="b678b-129">The following example identifies a landmark in an image.</span><span class="sxs-lookup"><span data-stu-id="b678b-129">The following example identifies a landmark in an image.</span></span>

### <a name="landmark-python-example-request"></a><span data-ttu-id="b678b-130">Landmark Python Example Request</span><span class="sxs-lookup"><span data-stu-id="b678b-130">Landmark Python Example Request</span></span>

```Python
########### Python 2.7 #############
import httplib, urllib, base64, json

headers = {
    # Request headers. Replace the key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

params = urllib.urlencode({
    # Request parameters. Use "model": "celebrities" to use the Celebrity model.
    'model': 'landmarks',
})

# The URL of a JEPG image containing text.
body = "{'url':'https://upload.wikimedia.org/wikipedia/commons/2/23/Space_Needle_2011-07-04.jpg'}"

try:
    conn = httplib.HTTPSConnection('westus.api.cognitive.microsoft.com')
    # Change "landmarks" to "celebrities" in the url to use the Celebrity model.
    conn.request("POST", "/vision/v1.0/models/landmarks/analyze?%s" % params, body, headers)
    response = conn.getresponse()
    data = response.read()
    # 'data' contains the JSON data. The following formats the JSON data for display.
    parsed = json.loads(data)
    print ("REST Response:")
    print (json.dumps(parsed, sort_keys=True, indent=2))
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))

####################################

########### Python 3.2 #############
import http.client, urllib.request, urllib.parse, urllib.error, base64, json

headers = {
    # Request headers. Replace the key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

params = urllib.parse.urlencode({
    # Request parameters. Use "model": "celebrities" to use the Celebrity model.
    'model': 'landmarks',
})

# The URL of a JEPG image containing text.
body = "{'url':'https://upload.wikimedia.org/wikipedia/commons/2/23/Space_Needle_2011-07-04.jpg'}"

try:
    conn = http.client.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/vision/v1.0/models/landmarks/analyze?%s" % params, body, headers)
    response = conn.getresponse()
    data = response.read()
    # 'data' contains the JSON data. The following formats the JSON data for display.
    encoding = response.headers.get_content_charset()
    parsed = json.loads(data.decode(encoding))
    print ("REST Response:")
    print (json.dumps(parsed, sort_keys=True, indent=2))
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))

####################################
```

### <a name="landmark-example-response"></a><span data-ttu-id="b678b-131">Landmark Example Response</span><span class="sxs-lookup"><span data-stu-id="b678b-131">Landmark Example Response</span></span>
<span data-ttu-id="b678b-132">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="b678b-132">A successful response is returned in JSON.</span></span> <span data-ttu-id="b678b-133">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="b678b-133">Following is an example of a successful response:</span></span>  

```json
{
  "metadata": {
    "format": "Jpeg",
    "height": 4132,
    "width": 2096
  },
  "requestId": "d08a914a-0fbb-4695-9a2e-c93791865436",
  "result": {
    "landmarks": [
      {
        "confidence": 0.9998178,
        "name": "Space Needle"
      }
    ]
  }
}
```

## <span data-ttu-id="b678b-134">Get a Thumbnail with Computer Vision API Using Python <a name="GetThumbnail"> </a></span><span class="sxs-lookup"><span data-stu-id="b678b-134">Get a Thumbnail with Computer Vision API Using Python <a name="GetThumbnail"> </a></span></span>
<span data-ttu-id="b678b-135">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to crop an image based on its region of interest (ROI) to the height and width you desire.</span><span class="sxs-lookup"><span data-stu-id="b678b-135">Use the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fb) to crop an image based on its region of interest (ROI) to the height and width you desire.</span></span> <span data-ttu-id="b678b-136">The aspect ratio you set for the thumbnail can be different from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="b678b-136">The aspect ratio you set for the thumbnail can be different from the aspect ratio of the input image.</span></span>

### <a name="get-a-thumbnail-python-example-request"></a><span data-ttu-id="b678b-137">Get a Thumbnail Python Example Request</span><span class="sxs-lookup"><span data-stu-id="b678b-137">Get a Thumbnail Python Example Request</span></span>

```Python
########### Python 2.7 #############
import httplib, urllib, base64

headers = {
    # Request headers. Replace the key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

params = urllib.urlencode({
    # Request parameters. The smartCropping flag is optional.
    'width': '150',
    'height': '100',
    'smartCropping': 'true',
})

# Replace the three dots below with the URL of the JPEG image for which you want a thumbnail.
body = "{'url':'...'}"

try:
    conn = httplib.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/vision/v1.0/generateThumbnail?%s" % params, body, headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))

####################################

########### Python 3.2 #############
import http.client, urllib.request, urllib.parse, urllib.error, base64

headers = {
    # Request headers. Replace the key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

params = urllib.parse.urlencode({
    # Request parameters. The smartCropping flag is optional.
    'width': '150',
    'height': '100',
    'smartCropping': 'true',
})

# Replace the three dots below with the URL of the JPEG image for which you want a thumbnail.
body = "{'url':'...'}"

try:
    conn = http.client.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/vision/v1.0/generateThumbnail?%s" % params, body, headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))
####################################
```

### <a name="get-a-thumbnail-response"></a><span data-ttu-id="b678b-138">Get a Thumbnail Response</span><span class="sxs-lookup"><span data-stu-id="b678b-138">Get a Thumbnail Response</span></span>
<span data-ttu-id="b678b-139">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="b678b-139">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="b678b-140">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="b678b-140">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span>


## <span data-ttu-id="b678b-141">Optical Character Recognition (OCR) with Computer Vision API Using Python <a name="OCR"> </a></span><span class="sxs-lookup"><span data-stu-id="b678b-141">Optical Character Recognition (OCR) with Computer Vision API Using Python <a name="OCR"> </a></span></span>
<span data-ttu-id="b678b-142">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="b678b-142">Use the [Optical Character Recognition (OCR) method](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fc) to detect text in an image and extract recognized characters into a machine-usable character stream.</span></span>

### <a name="ocr-python-example-request"></a><span data-ttu-id="b678b-143">OCR Python Example Request</span><span class="sxs-lookup"><span data-stu-id="b678b-143">OCR Python Example Request</span></span>
```Python
########### Python 2.7 #############
import httplib, urllib, base64

headers = {
    # Request headers. Replace the key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

params = urllib.urlencode({
    # Request parameters. The language setting "unk" means automatically detect the language.
    'language': 'unk',
    'detectOrientation ': 'true',
})

# Replace the three dots below with the URL of a JPEG image containing text.
body = "{'url':'...'}"

try:
    conn = httplib.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/vision/v1.0/ocr?%s" % params, body, headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))

####################################

########### Python 3.2 #############
import http.client, urllib.request, urllib.parse, urllib.error, base64

headers = {
    # Request headers. Replace the key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

params = urllib.parse.urlencode({
    # Request parameters. The language setting "unk" means automatically detect the language.
    'language': 'unk',
    'detectOrientation ': 'true',
})

# Replace the three dots below with the URL of a JPEG image containing text.
body = "{'url':'...'}"

try:
    conn = http.client.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/vision/v1.0/ocr?%s" % params, body, headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))
####################################

```

### <a name="ocr-example-response"></a><span data-ttu-id="b678b-144">OCR Example Response</span><span class="sxs-lookup"><span data-stu-id="b678b-144">OCR Example Response</span></span>
<span data-ttu-id="b678b-145">Upon success, the OCR results include the text from the image.</span><span class="sxs-lookup"><span data-stu-id="b678b-145">Upon success, the OCR results include the text from the image.</span></span> <span data-ttu-id="b678b-146">They also include bounding boxes for regions, lines, and words.</span><span class="sxs-lookup"><span data-stu-id="b678b-146">They also include bounding boxes for regions, lines, and words.</span></span>

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

## <span data-ttu-id="b678b-147">Text recognition with Computer Vision API Using Python <a name="RecognizeText"> </a></span><span class="sxs-lookup"><span data-stu-id="b678b-147">Text recognition with Computer Vision API Using Python <a name="RecognizeText"> </a></span></span>
<span data-ttu-id="b678b-148">Use the [RecognizeText method](https://ocr.portal.azure-api.net/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200) to detect handwritten or printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="b678b-148">Use the [RecognizeText method](https://ocr.portal.azure-api.net/docs/services/56f91f2d778daf23d8ec6739/operations/587f2c6a154055056008f200) to detect handwritten or printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

### <a name="handwriting-recognition-python-example"></a><span data-ttu-id="b678b-149">Handwriting Recognition Python Example</span><span class="sxs-lookup"><span data-stu-id="b678b-149">Handwriting Recognition Python Example</span></span>

```Python
########### Python 2.7 #############
import httplib, urllib, base64, time

headers = {
    # Request headers - replace this example key with your valid subscription key.
    # Another valid content type is "application/octet-stream".
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

# Replace the three dots below with the URL of a JPEG image containing text.
body = "{'url':'...'}"

serviceUrl = 'westus.api.cognitive.microsoft.com'

# For printed text, set "handwriting" to false.
params = urllib.urlencode({'handwriting' : 'true'})


try:
    conn = httplib.HTTPSConnection(serviceUrl)
    conn.request("POST", "/vision/v1.0/RecognizeText?%s" % params, body, headers)
    response = conn.getresponse()

    # This is the URI where you can get the text recognition operation result.
    operationLocation = response.getheader('Operation-Location')
    print "Operation-Location:", operationLocation

    parsedLocation = operationLocation.split(serviceUrl)
    answerURL = parsedLocation[1]
    print "AnswerURL:", answerURL

    # Note: The response may not be immediately available. Handwriting recognition is an
    # async operation that can take a variable amount of time depending on the length
    # of the text you want to recognize. You may need to wait or retry this GET operation.

    time.sleep(10)
    conn = httplib.HTTPSConnection(serviceUrl)
    conn.request("GET", answerURL, '', headers)
    response = conn.getresponse()
    print response.status, response.reason
    print response.read()
except Exception as e:
    print e

####################################

########### Python 3.2 #############
import http.client, urllib.request, urllib.parse, urllib.error, base64, requests, time

requestHeaders = {
    # Request headers - replace this example key with your valid subscription key.
    # Another valid content type is "application/octet-stream".
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

# Replace the three dots below with the URL of a JPEG image containing text.
body = {'url':'...'}

serviceUrl = 'https://westus.api.cognitive.microsoft.com/vision/v1.0/RecognizeText'

# For printed text, set "handwriting" to false.
params = {'handwriting' : 'true'}


try:
    response = requests.request('post', serviceUrl, json=body, data=None, headers=requestHeaders, params=params)
    print(response.status_code)

    # This is the URI where you can get the text recognition operation result.
    operationLocation = response.headers['Operation-Location']

    # Note: The response may not be immediately available. Handwriting recognition is an
    # async operation that can take a variable amount of time depending on the length
    # of the text you want to recognize. You may need to wait or retry this GET operation.

    time.sleep(10)
    response = requests.request('get', operationLocation, json=None, data=None, headers=requestHeaders, params=None)
    data = response.json()
    print(data)
except Exception as e:
    print(e)

####################################

```