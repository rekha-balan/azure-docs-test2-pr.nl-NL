---
title: Face API Python tutorial | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Learn how to use the Face API with the Python SDK to detect human faces in an image in Cognitive Services.
services: cognitive-services
author: SteveMSFT
manager: corncar
ms.service: cognitive-services
ms.component: face-api
ms.topic: article
ms.date: 03/01/2018
ms.author: sbowles
ms.openlocfilehash: 90d74d8df2ed59e6f3313ef7c620284d1022a667
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808267"
---
# <a name="getting-started-with-face-api-in-python-tutorial"></a><span data-ttu-id="2a467-103">Getting Started with Face API in Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="2a467-103">Getting Started with Face API in Python Tutorial</span></span>

<span data-ttu-id="2a467-104">In this tutorial, you will learn to invoke the Face API via the Python SDK to detect human faces in an image.</span><span class="sxs-lookup"><span data-stu-id="2a467-104">In this tutorial, you will learn to invoke the Face API via the Python SDK to detect human faces in an image.</span></span>

## <a name="prerequisites"></a> <span data-ttu-id="2a467-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2a467-105">Prerequisites</span></span>

<span data-ttu-id="2a467-106">To use the tutorial, you will need to do the following:</span><span class="sxs-lookup"><span data-stu-id="2a467-106">To use the tutorial, you will need to do the following:</span></span>

- <span data-ttu-id="2a467-107">Install either Python 2.7+ or Python 3.5+.</span><span class="sxs-lookup"><span data-stu-id="2a467-107">Install either Python 2.7+ or Python 3.5+.</span></span>
- <span data-ttu-id="2a467-108">Install pip.</span><span class="sxs-lookup"><span data-stu-id="2a467-108">Install pip.</span></span>
- <span data-ttu-id="2a467-109">Install the Python SDK for the Face API as follows:</span><span class="sxs-lookup"><span data-stu-id="2a467-109">Install the Python SDK for the Face API as follows:</span></span>

```bash
pip install cognitive_face
```

- <span data-ttu-id="2a467-110">Obtain a [subscription key](https://azure.microsoft.com/try/cognitive-services/) for Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="2a467-110">Obtain a [subscription key](https://azure.microsoft.com/try/cognitive-services/) for Microsoft Cognitive Services.</span></span> <span data-ttu-id="2a467-111">You can use either your primary or your secondary key in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a467-111">You can use either your primary or your secondary key in this tutorial.</span></span> <span data-ttu-id="2a467-112">(Note that to use any Face API, you must have a valid subscription key.)</span><span class="sxs-lookup"><span data-stu-id="2a467-112">(Note that to use any Face API, you must have a valid subscription key.)</span></span>

## <a name="sdk-example"></a> <span data-ttu-id="2a467-113">Detect a Face in an Image</span><span class="sxs-lookup"><span data-stu-id="2a467-113">Detect a Face in an Image</span></span>

```python
import cognitive_face as CF

KEY = '<Subscription Key>'  # Replace with a valid subscription key (keeping the quotes in place).
CF.Key.set(KEY)

BASE_URL = 'https://westus.api.cognitive.microsoft.com/face/v1.0/'  # Replace with your regional Base URL
CF.BaseUrl.set(BASE_URL)

# You can use this example JPG or replace the URL below with your own URL to a JPEG image.
img_url = 'https://raw.githubusercontent.com/Microsoft/Cognitive-Face-Windows/master/Data/detection1.jpg'
faces = CF.face.detect(img_url)
print(faces)
```

<span data-ttu-id="2a467-114">Below is an example result.</span><span class="sxs-lookup"><span data-stu-id="2a467-114">Below is an example result.</span></span> <span data-ttu-id="2a467-115">It's a `list` of detected faces.</span><span class="sxs-lookup"><span data-stu-id="2a467-115">It's a `list` of detected faces.</span></span> <span data-ttu-id="2a467-116">Each item in the list is a `dict` instance where `faceId` is a unique ID for the detected face and `faceRectangle` describes the position of the detected face.</span><span class="sxs-lookup"><span data-stu-id="2a467-116">Each item in the list is a `dict` instance where `faceId` is a unique ID for the detected face and `faceRectangle` describes the position of the detected face.</span></span> <span data-ttu-id="2a467-117">A face ID expires in 24 hours.</span><span class="sxs-lookup"><span data-stu-id="2a467-117">A face ID expires in 24 hours.</span></span>

```python
[{u'faceId': u'68a0f8cf-9dba-4a25-afb3-f9cdf57cca51', u'faceRectangle': {u'width': 89, u'top': 66, u'height': 89, u'left': 446}}]
```

## <a name="draw-rectangles-around-the-faces"></a><span data-ttu-id="2a467-118">Draw rectangles around the faces</span><span class="sxs-lookup"><span data-stu-id="2a467-118">Draw rectangles around the faces</span></span>

<span data-ttu-id="2a467-119">Using the json coordinates that you received from the previous command, you can draw rectangles on the image to visually represent each face.</span><span class="sxs-lookup"><span data-stu-id="2a467-119">Using the json coordinates that you received from the previous command, you can draw rectangles on the image to visually represent each face.</span></span> <span data-ttu-id="2a467-120">You will need to `pip install Pillow` to use the `PIL` imaging module.</span><span class="sxs-lookup"><span data-stu-id="2a467-120">You will need to `pip install Pillow` to use the `PIL` imaging module.</span></span>  <span data-ttu-id="2a467-121">At the top of the file, add the following:</span><span class="sxs-lookup"><span data-stu-id="2a467-121">At the top of the file, add the following:</span></span>

```python
import requests
from io import BytesIO
from PIL import Image, ImageDraw
```

<span data-ttu-id="2a467-122">Then, after `print(faces)`, include the following in your script:</span><span class="sxs-lookup"><span data-stu-id="2a467-122">Then, after `print(faces)`, include the following in your script:</span></span>

```python
#Convert width height to a point in a rectangle
def getRectangle(faceDictionary):
    rect = faceDictionary['faceRectangle']
    left = rect['left']
    top = rect['top']
    bottom = left + rect['height']
    right = top + rect['width']
    return ((left, top), (bottom, right))

#Download the image from the url
response = requests.get(img_url)
img = Image.open(BytesIO(response.content))

#For each face returned use the face rectangle and draw a red box.
draw = ImageDraw.Draw(img)
for face in faces:
    draw.rectangle(getRectangle(face), outline='red')

#Display the image in the users default image browser.
img.show()
```

## <a name='further'></a> <span data-ttu-id="2a467-123">Further Exploration</span><span class="sxs-lookup"><span data-stu-id="2a467-123">Further Exploration</span></span>

<span data-ttu-id="2a467-124">To help you further explore the Face API, this tutorial provides a GUI sample.</span><span class="sxs-lookup"><span data-stu-id="2a467-124">To help you further explore the Face API, this tutorial provides a GUI sample.</span></span> <span data-ttu-id="2a467-125">To run it, first install [wxPython](https://wxpython.org/pages/downloads/) then run the commands below.</span><span class="sxs-lookup"><span data-stu-id="2a467-125">To run it, first install [wxPython](https://wxpython.org/pages/downloads/) then run the commands below.</span></span>

```bash
git clone https://github.com/Microsoft/Cognitive-Face-Python.git
cd Cognitive-Face-Python
python sample
```

## <a name="summary"></a> <span data-ttu-id="2a467-126">Summary</span><span class="sxs-lookup"><span data-stu-id="2a467-126">Summary</span></span>

<span data-ttu-id="2a467-127">In this tutorial, you have learned the basic process for using the Face API via invoking the Python SDK.</span><span class="sxs-lookup"><span data-stu-id="2a467-127">In this tutorial, you have learned the basic process for using the Face API via invoking the Python SDK.</span></span> <span data-ttu-id="2a467-128">For more information on API details, please refer to the How-To and [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="2a467-128">For more information on API details, please refer to the How-To and [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

## <a name="related"></a> <span data-ttu-id="2a467-129">Related Topics</span><span class="sxs-lookup"><span data-stu-id="2a467-129">Related Topics</span></span>

- [<span data-ttu-id="2a467-130">Getting Started with Face API in CSharp</span><span class="sxs-lookup"><span data-stu-id="2a467-130">Getting Started with Face API in CSharp</span></span>](FaceAPIinCSharpTutorial.md)
- [<span data-ttu-id="2a467-131">Getting Started with Face API in Java for Android</span><span class="sxs-lookup"><span data-stu-id="2a467-131">Getting Started with Face API in Java for Android</span></span>](FaceAPIinJavaForAndroidTutorial.md)
