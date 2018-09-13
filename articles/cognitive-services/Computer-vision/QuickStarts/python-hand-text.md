---
title: 'Quickstart: Extract handwritten text - REST, Python - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you extract handwritten text from an image using Computer Vision with Python in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: f53ad0aae06d85cb38690d1cac1dfe702797402a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868078"
---
# <a name="quickstart-extract-handwritten-text---rest-python---computer-vision"></a><span data-ttu-id="bfa98-103">Quickstart: Extract handwritten text - REST, Python - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="bfa98-103">Quickstart: Extract handwritten text - REST, Python - Computer Vision</span></span>

<span data-ttu-id="bfa98-104">In this quickstart, you extract handwritten text from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="bfa98-104">In this quickstart, you extract handwritten text from an image using Computer Vision.</span></span>

<span data-ttu-id="bfa98-105">You can run this quickstart in a step-by step fashion using a Jupyter notebook on [MyBinder](https://mybinder.org).</span><span class="sxs-lookup"><span data-stu-id="bfa98-105">You can run this quickstart in a step-by step fashion using a Jupyter notebook on [MyBinder](https://mybinder.org).</span></span> <span data-ttu-id="bfa98-106">To launch Binder, select the following button:</span><span class="sxs-lookup"><span data-stu-id="bfa98-106">To launch Binder, select the following button:</span></span>

<span data-ttu-id="bfa98-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=VisionAPI.ipynb)</span><span class="sxs-lookup"><span data-stu-id="bfa98-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=VisionAPI.ipynb)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfa98-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bfa98-108">Prerequisites</span></span>

<span data-ttu-id="bfa98-109">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="bfa98-109">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="extract-handwritten-text"></a><span data-ttu-id="bfa98-110">Extract handwritten text</span><span class="sxs-lookup"><span data-stu-id="bfa98-110">Extract handwritten text</span></span>

<span data-ttu-id="bfa98-111">With the [Recognize Text](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) and the [Get Recognize Text Operation Result methods](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2cf1154055056008f201), you can detect handwritten text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="bfa98-111">With the [Recognize Text](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) and the [Get Recognize Text Operation Result methods](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2cf1154055056008f201), you can detect handwritten text in an image and extract recognized characters into a machine-usable character stream.</span></span>

<span data-ttu-id="bfa98-112">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bfa98-112">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="bfa98-113">Copy the following code to a new Python script file.</span><span class="sxs-lookup"><span data-stu-id="bfa98-113">Copy the following code to a new Python script file.</span></span>
1. <span data-ttu-id="bfa98-114">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="bfa98-114">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="bfa98-115">Change the `vision_base_url` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="bfa98-115">Change the `vision_base_url` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="bfa98-116">Optionally, change the `image_url` value to another image.</span><span class="sxs-lookup"><span data-stu-id="bfa98-116">Optionally, change the `image_url` value to another image.</span></span>
1. <span data-ttu-id="bfa98-117">Run the script.</span><span class="sxs-lookup"><span data-stu-id="bfa98-117">Run the script.</span></span>

<span data-ttu-id="bfa98-118">The following code uses the Python `requests` library to call the Computer Vision Analyze Image API.</span><span class="sxs-lookup"><span data-stu-id="bfa98-118">The following code uses the Python `requests` library to call the Computer Vision Analyze Image API.</span></span> <span data-ttu-id="bfa98-119">It returns the results as a JSON object.</span><span class="sxs-lookup"><span data-stu-id="bfa98-119">It returns the results as a JSON object.</span></span> <span data-ttu-id="bfa98-120">The API key is passed in via the `headers` dictionary.</span><span class="sxs-lookup"><span data-stu-id="bfa98-120">The API key is passed in via the `headers` dictionary.</span></span>

## <a name="recognize-text-request"></a><span data-ttu-id="bfa98-121">Recognize Text request</span><span class="sxs-lookup"><span data-stu-id="bfa98-121">Recognize Text request</span></span>

```python
import requests
import time
# If you are using a Jupyter notebook, uncomment the following line.
#%matplotlib inline
import matplotlib.pyplot as plt
from matplotlib.patches import Polygon
from PIL import Image
from io import BytesIO

# Replace <Subscription Key> with your valid subscription key.
subscription_key = "<Subscription Key>"
assert subscription_key

# You must use the same region in your REST call as you used to get your
# subscription keys. For example, if you got your subscription keys from
# westus, replace "westcentralus" in the URI below with "westus".
#
# Free trial subscription keys are generated in the westcentralus region.
# If you use a free trial subscription key, you shouldn't need to change
# this region.
vision_base_url = "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/"

text_recognition_url = vision_base_url + "recognizeText"

# Set image_url to the URL of an image that you want to analyze.
image_url = "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/" + \
    "Cursive_Writing_on_Notebook_paper.jpg/800px-Cursive_Writing_on_Notebook_paper.jpg"

headers = {'Ocp-Apim-Subscription-Key': subscription_key}
# Note: The request parameter changed for APIv2.
# For APIv1, it is 'handwriting': 'true'.
params  = {'mode': 'Handwritten'}
data    = {'url': image_url}
response = requests.post(
    text_recognition_url, headers=headers, params=params, json=data)
response.raise_for_status()

# Extracting handwritten text requires two API calls: One call to submit the
# image for processing, the other to retrieve the text found in the image.

# Holds the URI used to retrieve the recognized text.
operation_url = response.headers["Operation-Location"]

# The recognized text isn't immediately available, so poll to wait for completion.
analysis = {}
poll = True
while (poll):
    response_final = requests.get(
        response.headers["Operation-Location"], headers=headers)
    analysis = response_final.json()
    time.sleep(1)
    if ("recognitionResult" in analysis):
        poll= False 
    if ("status" in analysis and analysis['status'] == 'Failed'):
        poll= False

polygons=[]
if ("recognitionResult" in analysis):
    # Extract the recognized text, with bounding boxes.
    polygons = [(line["boundingBox"], line["text"])
        for line in analysis["recognitionResult"]["lines"]]

# Display the image and overlay it with the extracted text.
plt.figure(figsize=(15, 15))
image = Image.open(BytesIO(requests.get(image_url).content))
ax = plt.imshow(image)
for polygon in polygons:
    vertices = [(polygon[0][i], polygon[0][i+1])
        for i in range(0, len(polygon[0]), 2)]
    text     = polygon[1]
    patch    = Polygon(vertices, closed=True, fill=False, linewidth=2, color='y')
    ax.axes.add_patch(patch)
    plt.text(vertices[0][0], vertices[0][1], text, fontsize=20, va="top")
_ = plt.axis("off")
```

## <a name="recognize-text-response"></a><span data-ttu-id="bfa98-122">Recognize Text response</span><span class="sxs-lookup"><span data-stu-id="bfa98-122">Recognize Text response</span></span>

<span data-ttu-id="bfa98-123">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="bfa98-123">A successful response is returned in JSON, for example:</span></span>

```json
{
  "status": "Succeeded",
  "recognitionResult": {
    "lines": [
      {
        "boundingBox": [
          2,
          52,
          65,
          46,
          69,
          89,
          7,
          95
        ],
        "text": "dog",
        "words": [
          {
            "boundingBox": [
              0,
              59,
              63,
              43,
              77,
              86,
              3,
              102
            ],
            "text": "dog"
          }
        ]
      },
      {
        "boundingBox": [
          6,
          2,
          771,
          13,
          770,
          75,
          5,
          64
        ],
        "text": "The quick brown fox jumps over the lazy",
        "words": [
          {
            "boundingBox": [
              0,
              4,
              92,
              5,
              77,
              71,
              0,
              71
            ],
            "text": "The"
          },
          {
            "boundingBox": [
              74,
              4,
              189,
              5,
              174,
              72,
              60,
              71
            ],
            "text": "quick"
          },
          {
            "boundingBox": [
              176,
              5,
              321,
              6,
              306,
              73,
              161,
              72
            ],
            "text": "brown"
          },
          {
            "boundingBox": [
              308,
              6,
              387,
              6,
              372,
              73,
              293,
              73
            ],
            "text": "fox"
          },
          {
            "boundingBox": [
              382,
              6,
              506,
              7,
              491,
              74,
              368,
              73
            ],
            "text": "jumps"
          },
          {
            "boundingBox": [
              492,
              7,
              607,
              8,
              592,
              75,
              478,
              74
            ],
            "text": "over"
          },
          {
            "boundingBox": [
              589,
              8,
              673,
              8,
              658,
              75,
              575,
              75
            ],
            "text": "the"
          },
          {
            "boundingBox": [
              660,
              8,
              783,
              9,
              768,
              76,
              645,
              75
            ],
            "text": "lazy"
          }
        ]
      },
      {
        "boundingBox": [
          2,
          84,
          783,
          96,
          782,
          154,
          1,
          148
        ],
        "text": "Pack my box with five dozen liquor jugs",
        "words": [
          {
            "boundingBox": [
              0,
              86,
              94,
              87,
              72,
              151,
              0,
              149
            ],
            "text": "Pack"
          },
          {
            "boundingBox": [
              76,
              87,
              164,
              88,
              142,
              152,
              54,
              150
            ],
            "text": "my"
          },
          {
            "boundingBox": [
              155,
              88,
              243,
              89,
              222,
              152,
              134,
              151
            ],
            "text": "box"
          },
          {
            "boundingBox": [
              226,
              89,
              344,
              90,
              323,
              154,
              204,
              152
            ],
            "text": "with"
          },
          {
            "boundingBox": [
              336,
              90,
              432,
              91,
              411,
              154,
              314,
              154
            ],
            "text": "five"
          },
          {
            "boundingBox": [
              419,
              91,
              538,
              92,
              516,
              154,
              398,
              154
            ],
            "text": "dozen"
          },
          {
            "boundingBox": [
              547,
              92,
              701,
              94,
              679,
              154,
              525,
              154
            ],
            "text": "liquor"
          },
          {
            "boundingBox": [
              696,
              94,
              800,
              95,
              780,
              154,
              675,
              154
            ],
            "text": "jugs"
          }
        ]
      }
    ]
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="bfa98-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfa98-124">Next steps</span></span>

<span data-ttu-id="bfa98-125">Explore a Python application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="bfa98-125">Explore a Python application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="bfa98-126">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="bfa98-126">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfa98-127">Computer Vision API Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="bfa98-127">Computer Vision API Python Tutorial</span></span>](../Tutorials/PythonTutorial.md)
