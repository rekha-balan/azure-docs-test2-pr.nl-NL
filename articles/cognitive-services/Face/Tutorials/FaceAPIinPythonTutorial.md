---
title: Face API Python tutorial | Microsoft Docs
description: Learn how to use the Face API with the Python SDK to detect human faces in an image in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 02/24/2017
ms.author: anroth
ms.openlocfilehash: c8f47c62d86c8066d02813d387065d9dadf087b8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661278"
---
# <a name="getting-started-with-face-api-in-python-tutorial"></a><span data-ttu-id="7d6a2-103">Getting Started with Face API in Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="7d6a2-103">Getting Started with Face API in Python Tutorial</span></span>

<span data-ttu-id="7d6a2-104">In this tutorial, you will learn to invoke the Face API via the Python SDK to detect human faces in an image.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-104">In this tutorial, you will learn to invoke the Face API via the Python SDK to detect human faces in an image.</span></span>

## <a name="prerequisites"></a> <span data-ttu-id="7d6a2-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7d6a2-105">Prerequisites</span></span>

<span data-ttu-id="7d6a2-106">To use the tutorial, you will need to do the following:</span><span class="sxs-lookup"><span data-stu-id="7d6a2-106">To use the tutorial, you will need to do the following:</span></span>

- <span data-ttu-id="7d6a2-107">Install either Python 2.7+ or Python 3.5+.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-107">Install either Python 2.7+ or Python 3.5+.</span></span>
- <span data-ttu-id="7d6a2-108">Install pip.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-108">Install pip.</span></span>
- <span data-ttu-id="7d6a2-109">Install the Python SDK for the Face API as follows:</span><span class="sxs-lookup"><span data-stu-id="7d6a2-109">Install the Python SDK for the Face API as follows:</span></span>

```bash
pip install cognitive_face
```

- <span data-ttu-id="7d6a2-110">Obtain a [subscription key](https://www.microsoft.com/cognitive-services/en-us/sign-up) for Microsoft Cognitive Services (formerly Project Oxford).</span><span class="sxs-lookup"><span data-stu-id="7d6a2-110">Obtain a [subscription key](https://www.microsoft.com/cognitive-services/en-us/sign-up) for Microsoft Cognitive Services (formerly Project Oxford).</span></span> <span data-ttu-id="7d6a2-111">You can use either your primary or your secondary key in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-111">You can use either your primary or your secondary key in this tutorial.</span></span> <span data-ttu-id="7d6a2-112">(Note that to use any Face API, you must have a valid subscription key.)</span><span class="sxs-lookup"><span data-stu-id="7d6a2-112">(Note that to use any Face API, you must have a valid subscription key.)</span></span>

## <a name="sdk-example"></a> <span data-ttu-id="7d6a2-113">Detect a Face in an Image</span><span class="sxs-lookup"><span data-stu-id="7d6a2-113">Detect a Face in an Image</span></span>

```python
import cognitive_face as CF

KEY = 'subscription key'  # Replace with a valid subscription key (keeping the quotes in place).
CF.Key.set(KEY)

# You can use this example JPG or replace the URL below with your own URL to a JPEG image.
img_url = 'https://raw.githubusercontent.com/Microsoft/Cognitive-Face-Windows/master/Data/detection1.jpg'
result = CF.face.detect(img_url)
print result
```

<span data-ttu-id="7d6a2-114">Below is an example result.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-114">Below is an example result.</span></span> <span data-ttu-id="7d6a2-115">It's a `list` of detected faces.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-115">It's a `list` of detected faces.</span></span> <span data-ttu-id="7d6a2-116">Each item in the list is a `dict` instance where `faceId` is a unique ID for the detected face and `faceRectangle` describes the postion of the detected face.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-116">Each item in the list is a `dict` instance where `faceId` is a unique ID for the detected face and `faceRectangle` describes the postion of the detected face.</span></span> <span data-ttu-id="7d6a2-117">A face ID expires in 24 hours.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-117">A face ID expires in 24 hours.</span></span>

```python
[{u'faceId': u'68a0f8cf-9dba-4a25-afb3-f9cdf57cca51', u'faceRectangle': {u'width': 89, u'top': 66, u'height': 89, u'left': 446}}]
```

## <a name='further'></a> <span data-ttu-id="7d6a2-118">Further Exploration</span><span class="sxs-lookup"><span data-stu-id="7d6a2-118">Further Exploration</span></span>

<span data-ttu-id="7d6a2-119">To help you further explore the Face API, this tutorial provides a GUI sample.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-119">To help you further explore the Face API, this tutorial provides a GUI sample.</span></span> <span data-ttu-id="7d6a2-120">To run it, first install [wxPython](https://wxpython.org/) then run the commands below.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-120">To run it, first install [wxPython](https://wxpython.org/) then run the commands below.</span></span>

```bash
git clone https://github.com/Microsoft/Cognitive-Face-Python.git
cd Cognitive-Face-Python
python sample
```

## <a name="summary"></a> <span data-ttu-id="7d6a2-121">Summary</span><span class="sxs-lookup"><span data-stu-id="7d6a2-121">Summary</span></span>

<span data-ttu-id="7d6a2-122">In this tutorial, you have learned the basic process for using the Face API via invoking the Python SDK.</span><span class="sxs-lookup"><span data-stu-id="7d6a2-122">In this tutorial, you have learned the basic process for using the Face API via invoking the Python SDK.</span></span> <span data-ttu-id="7d6a2-123">For more information on API details, please refer to the How-To and [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span><span class="sxs-lookup"><span data-stu-id="7d6a2-123">For more information on API details, please refer to the How-To and [API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).</span></span>

## <a name="related"></a> <span data-ttu-id="7d6a2-124">Related Topics</span><span class="sxs-lookup"><span data-stu-id="7d6a2-124">Related Topics</span></span>

- [<span data-ttu-id="7d6a2-125">Getting Started with Face API in CSharp</span><span class="sxs-lookup"><span data-stu-id="7d6a2-125">Getting Started with Face API in CSharp</span></span>](FaceAPIinCSharpTutorial.md)
- [<span data-ttu-id="7d6a2-126">Getting Started with Face API in Java for Android</span><span class="sxs-lookup"><span data-stu-id="7d6a2-126">Getting Started with Face API in Java for Android</span></span>](FaceAPIinJavaForAndroidTutorial.md)
