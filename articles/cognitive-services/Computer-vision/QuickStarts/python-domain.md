---
title: 'Quickstart: Use a domain model - REST, Python - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you use domain models to identify celebrities and landmarks in  an image using Computer Vision with Python in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: abe0040b7d6a045506d883957ad900fdda83ab97
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865534"
---
# <a name="quickstart-use-a-domain-model---rest-python---computer-vision"></a><span data-ttu-id="5e7fa-103">Quickstart: Use a domain model - REST, Python - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="5e7fa-103">Quickstart: Use a domain model - REST, Python - Computer Vision</span></span>

<span data-ttu-id="5e7fa-104">In this quickstart, you use domain models to identify celebrities and landmarks in an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-104">In this quickstart, you use domain models to identify celebrities and landmarks in an image using Computer Vision.</span></span>

<span data-ttu-id="5e7fa-105">You can run this quickstart in a step-by step fashion using a Jupyter notebook on [MyBinder](https://mybinder.org).</span><span class="sxs-lookup"><span data-stu-id="5e7fa-105">You can run this quickstart in a step-by step fashion using a Jupyter notebook on [MyBinder](https://mybinder.org).</span></span> <span data-ttu-id="5e7fa-106">To launch Binder, select the following button:</span><span class="sxs-lookup"><span data-stu-id="5e7fa-106">To launch Binder, select the following button:</span></span>

<span data-ttu-id="5e7fa-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=VisionAPI.ipynb)</span><span class="sxs-lookup"><span data-stu-id="5e7fa-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=VisionAPI.ipynb)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e7fa-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5e7fa-108">Prerequisites</span></span>

<span data-ttu-id="5e7fa-109">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="5e7fa-109">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="identify-celebrities-and-landmarks"></a><span data-ttu-id="5e7fa-110">Identify celebrities and landmarks</span><span class="sxs-lookup"><span data-stu-id="5e7fa-110">Identify celebrities and landmarks</span></span>

<span data-ttu-id="5e7fa-111">With the [Recognize Domain Specific Content method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e200), you can identify a specific set of objects in an image.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-111">With the [Recognize Domain Specific Content method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e200), you can identify a specific set of objects in an image.</span></span> <span data-ttu-id="5e7fa-112">The two domain-specific models that are currently available are _celebrities_ and _landmarks_.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-112">The two domain-specific models that are currently available are _celebrities_ and _landmarks_.</span></span>

<span data-ttu-id="5e7fa-113">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="5e7fa-113">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="5e7fa-114">Copy the following code to a new Python script file.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-114">Copy the following code to a new Python script file.</span></span>
1. <span data-ttu-id="5e7fa-115">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-115">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="5e7fa-116">Change the `vision_base_url` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-116">Change the `vision_base_url` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="5e7fa-117">Optionally, change the `image_url` value to another image.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-117">Optionally, change the `image_url` value to another image.</span></span>
1. <span data-ttu-id="5e7fa-118">Run the script.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-118">Run the script.</span></span>

<span data-ttu-id="5e7fa-119">The following code uses the Python `requests` library to call the Computer Vision Analyze Image API.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-119">The following code uses the Python `requests` library to call the Computer Vision Analyze Image API.</span></span> <span data-ttu-id="5e7fa-120">It returns the results as a JSON object.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-120">It returns the results as a JSON object.</span></span> <span data-ttu-id="5e7fa-121">The API key is passed in via the `headers` dictionary.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-121">The API key is passed in via the `headers` dictionary.</span></span> <span data-ttu-id="5e7fa-122">The model to use is passed in via the `params` dictionary.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-122">The model to use is passed in via the `params` dictionary.</span></span>

## <a name="landmark-identification"></a><span data-ttu-id="5e7fa-123">Landmark identification</span><span class="sxs-lookup"><span data-stu-id="5e7fa-123">Landmark identification</span></span>

### <a name="recognize-landmark-request"></a><span data-ttu-id="5e7fa-124">Recognize Landmark request</span><span class="sxs-lookup"><span data-stu-id="5e7fa-124">Recognize Landmark request</span></span>

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

landmark_analyze_url = vision_base_url + "models/landmarks/analyze"

# Set image_url to the URL of an image that you want to analyze.
image_url = "https://upload.wikimedia.org/wikipedia/commons/f/f6/" + \
    "Bunker_Hill_Monument_2005.jpg"

headers = {'Ocp-Apim-Subscription-Key': subscription_key}
params  = {'model': 'landmarks'}
data    = {'url': image_url}
response = requests.post(
    landmark_analyze_url, headers=headers, params=params, json=data)
response.raise_for_status()

# The 'analysis' object contains various fields that describe the image. The
# most relevant landmark for the image is obtained from the 'result' property.
analysis = response.json()
assert analysis["result"]["landmarks"] is not []
print(analysis)
landmark_name = analysis["result"]["landmarks"][0]["name"].capitalize()

# Display the image and overlay it with the landmark name.
image = Image.open(BytesIO(requests.get(image_url).content))
plt.imshow(image)
plt.axis("off")
_ = plt.title(landmark_name, size="x-large", y=-0.1)
```

### <a name="recognize-landmark-response"></a><span data-ttu-id="5e7fa-125">Recognize Landmark response</span><span class="sxs-lookup"><span data-stu-id="5e7fa-125">Recognize Landmark response</span></span>

<span data-ttu-id="5e7fa-126">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="5e7fa-126">A successful response is returned in JSON, for example:</span></span>

```json
{
  "result": {
    "landmarks": [
      {
        "name": "Bunker Hill Monument",
        "confidence": 0.9768505096435547
      }
    ]
  },
  "requestId": "659a10cd-44bb-44db-9147-a295b853b2b8",
  "metadata": {
    "height": 1600,
    "width": 1200,
    "format": "Jpeg"
  }
}
```

## <a name="celebrity-identification"></a><span data-ttu-id="5e7fa-127">Celebrity identification</span><span class="sxs-lookup"><span data-stu-id="5e7fa-127">Celebrity identification</span></span>

### <a name="recognize-celebrity-request"></a><span data-ttu-id="5e7fa-128">Recognize Celebrity request</span><span class="sxs-lookup"><span data-stu-id="5e7fa-128">Recognize Celebrity request</span></span>

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

vision_base_url = "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/"

celebrity_analyze_url = vision_base_url + "models/celebrities/analyze"

# Set image_url to the URL of an image that you want to analyze.
image_url = "https://upload.wikimedia.org/wikipedia/commons/d/d9/" + \
    "Bill_gates_portrait.jpg"

headers = {'Ocp-Apim-Subscription-Key': subscription_key}
params  = {'model': 'celebrities'}
data    = {'url': image_url}
response = requests.post(
    celebrity_analyze_url, headers=headers, params=params, json=data)
response.raise_for_status()

# The 'analysis' object contains various fields that describe the image. The
# most relevant celebrity for the image is obtained from the 'result' property.
analysis = response.json()
assert analysis["result"]["celebrities"] is not []
print(analysis)
celebrity_name = analysis["result"]["celebrities"][0]["name"].capitalize()

# Display the image and overlay it with the celebrity name.
image = Image.open(BytesIO(requests.get(image_url).content))
plt.imshow(image)
plt.axis("off")
_ = plt.title(celebrity_name, size="x-large", y=-0.1)
```

### <a name="recognize-celebrity-response"></a><span data-ttu-id="5e7fa-129">Recognize Celebrity response</span><span class="sxs-lookup"><span data-stu-id="5e7fa-129">Recognize Celebrity response</span></span>

<span data-ttu-id="5e7fa-130">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="5e7fa-130">A successful response is returned in JSON, for example:</span></span>

```json
{
  "result": {
    "celebrities": [
      {
        "faceRectangle": {
          "top": 123,
          "left": 156,
          "width": 187,
          "height": 187
        },
        "name": "Bill Gates",
        "confidence": 0.9993845224380493
      }
    ]
  },
  "requestId": "f14ec1d0-62d4-4296-9ceb-6b5776dc2020",
  "metadata": {
    "height": 521,
    "width": 550,
    "format": "Jpeg"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="5e7fa-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e7fa-131">Next steps</span></span>

<span data-ttu-id="5e7fa-132">Explore a Python application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="5e7fa-132">Explore a Python application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="5e7fa-133">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="5e7fa-133">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e7fa-134">Computer Vision API Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="5e7fa-134">Computer Vision API Python Tutorial</span></span>](../Tutorials/PythonTutorial.md)
