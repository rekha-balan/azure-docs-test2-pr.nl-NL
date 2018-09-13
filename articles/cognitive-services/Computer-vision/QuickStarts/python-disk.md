---
title: 'Quickstart: Analyze a local image - REST, Python - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze a local image using Computer Vision with Python in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 1b980ab922d609d7d25cb6134407360f7a323aeb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968691"
---
# <a name="quickstart-analyze-a-local-image---rest-python---computer-vision"></a><span data-ttu-id="e8192-103">Quickstart: Analyze a local image - REST, Python - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="e8192-103">Quickstart: Analyze a local image - REST, Python - Computer Vision</span></span>

<span data-ttu-id="e8192-104">In this quickstart, you analyze a local image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="e8192-104">In this quickstart, you analyze a local image using Computer Vision.</span></span> <span data-ttu-id="e8192-105">To analyze a remote image, see [Analyze a remote image with Python](python-analyze.md).</span><span class="sxs-lookup"><span data-stu-id="e8192-105">To analyze a remote image, see [Analyze a remote image with Python](python-analyze.md).</span></span>

<span data-ttu-id="e8192-106">You can run this quickstart in a step-by step fashion using a Jupyter notebook on [MyBinder](https://mybinder.org).</span><span class="sxs-lookup"><span data-stu-id="e8192-106">You can run this quickstart in a step-by step fashion using a Jupyter notebook on [MyBinder](https://mybinder.org).</span></span> <span data-ttu-id="e8192-107">To launch Binder, select the following button:</span><span class="sxs-lookup"><span data-stu-id="e8192-107">To launch Binder, select the following button:</span></span>

<span data-ttu-id="e8192-108">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=VisionAPI.ipynb)</span><span class="sxs-lookup"><span data-stu-id="e8192-108">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=VisionAPI.ipynb)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8192-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e8192-109">Prerequisites</span></span>

<span data-ttu-id="e8192-110">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="e8192-110">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="analyze-a-local-image"></a><span data-ttu-id="e8192-111">Analyze a local image</span><span class="sxs-lookup"><span data-stu-id="e8192-111">Analyze a local image</span></span>

<span data-ttu-id="e8192-112">This sample is similar to [Analyze a remote image with Python](python-analyze.md) except the image to analyze is read locally from disk.</span><span class="sxs-lookup"><span data-stu-id="e8192-112">This sample is similar to [Analyze a remote image with Python](python-analyze.md) except the image to analyze is read locally from disk.</span></span> <span data-ttu-id="e8192-113">Two changes are required:</span><span class="sxs-lookup"><span data-stu-id="e8192-113">Two changes are required:</span></span>

- <span data-ttu-id="e8192-114">Add a `{"Content-Type": "application/octet-stream"}` header to the request.</span><span class="sxs-lookup"><span data-stu-id="e8192-114">Add a `{"Content-Type": "application/octet-stream"}` header to the request.</span></span>
- <span data-ttu-id="e8192-115">Add the image data (byte array) to the body of the request.</span><span class="sxs-lookup"><span data-stu-id="e8192-115">Add the image data (byte array) to the body of the request.</span></span>

<span data-ttu-id="e8192-116">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="e8192-116">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="e8192-117">Copy the following code to a new Python script file.</span><span class="sxs-lookup"><span data-stu-id="e8192-117">Copy the following code to a new Python script file.</span></span>
1. <span data-ttu-id="e8192-118">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="e8192-118">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="e8192-119">Change the `vision_base_url` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="e8192-119">Change the `vision_base_url` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="e8192-120">Change the `image_path` value to the path of a local image.</span><span class="sxs-lookup"><span data-stu-id="e8192-120">Change the `image_path` value to the path of a local image.</span></span>
1. <span data-ttu-id="e8192-121">Run the script.</span><span class="sxs-lookup"><span data-stu-id="e8192-121">Run the script.</span></span>

<span data-ttu-id="e8192-122">The following code uses the Python `requests` library to call the Computer Vision Analyze Image API.</span><span class="sxs-lookup"><span data-stu-id="e8192-122">The following code uses the Python `requests` library to call the Computer Vision Analyze Image API.</span></span> <span data-ttu-id="e8192-123">It returns the results as a JSON object.</span><span class="sxs-lookup"><span data-stu-id="e8192-123">It returns the results as a JSON object.</span></span> <span data-ttu-id="e8192-124">The API key is passed in via the `headers` dictionary.</span><span class="sxs-lookup"><span data-stu-id="e8192-124">The API key is passed in via the `headers` dictionary.</span></span> <span data-ttu-id="e8192-125">The types of features to recognize is passed in via the `params` dictionary.</span><span class="sxs-lookup"><span data-stu-id="e8192-125">The types of features to recognize is passed in via the `params` dictionary.</span></span> <span data-ttu-id="e8192-126">The binary image data is passed in via the `data` parameter to `requests.post`.</span><span class="sxs-lookup"><span data-stu-id="e8192-126">The binary image data is passed in via the `data` parameter to `requests.post`.</span></span>

## <a name="analyze-image-request"></a><span data-ttu-id="e8192-127">Analyze Image request</span><span class="sxs-lookup"><span data-stu-id="e8192-127">Analyze Image request</span></span>

```python
import requests
# If you are using a Jupyter notebook, uncomment the following line.
#%matplotlib inline
import matplotlib.pyplot as plt
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

analyze_url = vision_base_url + "analyze"

# Set image_path to the local path of an image that you want to analyze.
image_path = "C:/Documents/ImageToAnalyze.jpg"

# Read the image into a byte array
image_data = open(image_path, "rb").read()
headers    = {'Ocp-Apim-Subscription-Key': subscription_key,
              'Content-Type': 'application/octet-stream'}
params     = {'visualFeatures': 'Categories,Description,Color'}
response = requests.post(
    analyze_url, headers=headers, params=params, data=image_data)
response.raise_for_status()

# The 'analysis' object contains various fields that describe the image. The most
# relevant caption for the image is obtained from the 'description' property.
analysis = response.json()
print(analysis)
image_caption = analysis["description"]["captions"][0]["text"].capitalize()

# Display the image and overlay it with the caption.
image = Image.open(BytesIO(image_data))
plt.imshow(image)
plt.axis("off")
_ = plt.title(image_caption, size="x-large", y=-0.1)
```

## <a name="analyze-image-response"></a><span data-ttu-id="e8192-128">Analyze Image response</span><span class="sxs-lookup"><span data-stu-id="e8192-128">Analyze Image response</span></span>

<span data-ttu-id="e8192-129">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="e8192-129">A successful response is returned in JSON, for example:</span></span>

```json
{
  "categories": [
    {
      "name": "outdoor_",
      "score": 0.00390625,
      "detail": {
        "landmarks": []
      }
    },
    {
      "name": "outdoor_street",
      "score": 0.33984375,
      "detail": {
        "landmarks": []
      }
    }
  ],
  "description": {
    "tags": [
      "building",
      "outdoor",
      "street",
      "city",
      "people",
      "busy",
      "table",
      "walking",
      "traffic",
      "filled",
      "large",
      "many",
      "group",
      "night",
      "light",
      "crowded",
      "bunch",
      "standing",
      "man",
      "sign",
      "crowd",
      "umbrella",
      "riding",
      "tall",
      "woman",
      "bus"
    ],
    "captions": [
      {
        "text": "a group of people on a city street at night",
        "confidence": 0.9122243847383961
      }
    ]
  },
  "color": {
    "dominantColorForeground": "Brown",
    "dominantColorBackground": "Brown",
    "dominantColors": [
      "Brown"
    ],
    "accentColor": "B54316",
    "isBwImg": false
  },
  "requestId": "c11894eb-de3e-451b-9257-7c8b168073d1",
  "metadata": {
    "height": 600,
    "width": 450,
    "format": "Jpeg"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="e8192-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8192-130">Next steps</span></span>

<span data-ttu-id="e8192-131">Explore a Python application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="e8192-131">Explore a Python application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="e8192-132">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="e8192-132">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e8192-133">Computer Vision API Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="e8192-133">Computer Vision API Python Tutorial</span></span>](../Tutorials/PythonTutorial.md)
