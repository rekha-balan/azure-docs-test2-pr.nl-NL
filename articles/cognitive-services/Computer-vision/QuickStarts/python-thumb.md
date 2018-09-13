---
title: 'Quickstart: Generate a thumbnail - REST, Python - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you generate a thumbnail from an image using Computer Vision with Python in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: a558ceb078a81879cd0043e5d573a1f4bd580a25
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856592"
---
# <a name="quickstart-generate-a-thumbnail---rest-python---computer-vision"></a><span data-ttu-id="04d5f-103">Quickstart: Generate a thumbnail - REST, Python - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="04d5f-103">Quickstart: Generate a thumbnail - REST, Python - Computer Vision</span></span>

<span data-ttu-id="04d5f-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="04d5f-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span></span>

<span data-ttu-id="04d5f-105">You can run this quickstart in a step-by step fashion using a Jupyter notebook on [MyBinder](https://mybinder.org).</span><span class="sxs-lookup"><span data-stu-id="04d5f-105">You can run this quickstart in a step-by step fashion using a Jupyter notebook on [MyBinder](https://mybinder.org).</span></span> <span data-ttu-id="04d5f-106">To launch Binder, select the following button:</span><span class="sxs-lookup"><span data-stu-id="04d5f-106">To launch Binder, select the following button:</span></span>

<span data-ttu-id="04d5f-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=VisionAPI.ipynb)</span><span class="sxs-lookup"><span data-stu-id="04d5f-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=VisionAPI.ipynb)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04d5f-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04d5f-108">Prerequisites</span></span>

<span data-ttu-id="04d5f-109">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="04d5f-109">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="intelligently-generate-a-thumbnail"></a><span data-ttu-id="04d5f-110">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="04d5f-110">Intelligently generate a thumbnail</span></span>

<span data-ttu-id="04d5f-111">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span><span class="sxs-lookup"><span data-stu-id="04d5f-111">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span></span> <span data-ttu-id="04d5f-112">You specify the height and width, which can differ from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="04d5f-112">You specify the height and width, which can differ from the aspect ratio of the input image.</span></span> <span data-ttu-id="04d5f-113">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span><span class="sxs-lookup"><span data-stu-id="04d5f-113">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span></span>

<span data-ttu-id="04d5f-114">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="04d5f-114">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="04d5f-115">Copy the following code to a new Python script file.</span><span class="sxs-lookup"><span data-stu-id="04d5f-115">Copy the following code to a new Python script file.</span></span>
1. <span data-ttu-id="04d5f-116">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="04d5f-116">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="04d5f-117">Change the `vision_base_url` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="04d5f-117">Change the `vision_base_url` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="04d5f-118">Optionally, change the `image_url` value to another image.</span><span class="sxs-lookup"><span data-stu-id="04d5f-118">Optionally, change the `image_url` value to another image.</span></span>
1. <span data-ttu-id="04d5f-119">Run the script.</span><span class="sxs-lookup"><span data-stu-id="04d5f-119">Run the script.</span></span>

<span data-ttu-id="04d5f-120">The following code uses the Python `requests` library to call the Computer Vision Analyze Image API.</span><span class="sxs-lookup"><span data-stu-id="04d5f-120">The following code uses the Python `requests` library to call the Computer Vision Analyze Image API.</span></span> <span data-ttu-id="04d5f-121">The API key is passed in via the `headers` dictionary.</span><span class="sxs-lookup"><span data-stu-id="04d5f-121">The API key is passed in via the `headers` dictionary.</span></span> <span data-ttu-id="04d5f-122">The size of the thumbnail is passed in via the `params` dictionary.</span><span class="sxs-lookup"><span data-stu-id="04d5f-122">The size of the thumbnail is passed in via the `params` dictionary.</span></span> <span data-ttu-id="04d5f-123">The thumbnail is returned as a byte array in the response.</span><span class="sxs-lookup"><span data-stu-id="04d5f-123">The thumbnail is returned as a byte array in the response.</span></span>

## <a name="get-thumbnail-request"></a><span data-ttu-id="04d5f-124">Get Thumbnail request</span><span class="sxs-lookup"><span data-stu-id="04d5f-124">Get Thumbnail request</span></span>

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

thumbnail_url = vision_base_url + "generateThumbnail"

# Set image_url to the URL of an image that you want to analyze.
image_url = "https://upload.wikimedia.org/wikipedia/commons/9/94/Bloodhound_Puppy.jpg"

headers = {'Ocp-Apim-Subscription-Key': subscription_key}
params  = {'width': '50', 'height': '50', 'smartCropping': 'true'}
data    = {'url': image_url}
response = requests.post(thumbnail_url, headers=headers, params=params, json=data)
response.raise_for_status()

thumbnail = Image.open(BytesIO(response.content))

# Display the thumbnail.
plt.imshow(thumbnail)
plt.axis("off")

# Verify the thumbnail size.
print("Thumbnail is {0}-by-{1}".format(*thumbnail.size))
```

## <a name="next-steps"></a><span data-ttu-id="04d5f-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="04d5f-125">Next steps</span></span>

<span data-ttu-id="04d5f-126">Explore a Python application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="04d5f-126">Explore a Python application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="04d5f-127">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="04d5f-127">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04d5f-128">Computer Vision API Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="04d5f-128">Computer Vision API Python Tutorial</span></span>](../Tutorials/PythonTutorial.md)
