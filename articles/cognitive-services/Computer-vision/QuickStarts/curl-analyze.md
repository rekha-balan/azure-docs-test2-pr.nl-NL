---
title: 'Quickstart: Analyze a remote image - REST, cURL - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze a remote image using Computer Vision with cURL in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: e73cd116f004904a1f346a0b56d4172fe1aa7706
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871684"
---
# <a name="quickstart-analyze-a-remote-image---rest-curl---computer-vision"></a><span data-ttu-id="4eb73-103">Quickstart: Analyze a remote image - REST, cURL - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="4eb73-103">Quickstart: Analyze a remote image - REST, cURL - Computer Vision</span></span>

<span data-ttu-id="4eb73-104">In this quickstart, you analyze a remote image to extract visual features using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="4eb73-104">In this quickstart, you analyze a remote image to extract visual features using Computer Vision.</span></span> <span data-ttu-id="4eb73-105">To analyze a local image, see [Analyze a local image with cURL](curl-disk.md).</span><span class="sxs-lookup"><span data-stu-id="4eb73-105">To analyze a local image, see [Analyze a local image with cURL](curl-disk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4eb73-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4eb73-106">Prerequisites</span></span>

<span data-ttu-id="4eb73-107">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="4eb73-107">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="analyze-a-remote-image"></a><span data-ttu-id="4eb73-108">Analyze a remote image</span><span class="sxs-lookup"><span data-stu-id="4eb73-108">Analyze a remote image</span></span>

<span data-ttu-id="4eb73-109">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="4eb73-109">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="4eb73-110">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="4eb73-110">You can upload an image or specify an image URL and choose which features to return, including:</span></span>

* <span data-ttu-id="4eb73-111">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="4eb73-111">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="4eb73-112">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="4eb73-112">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="4eb73-113">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="4eb73-113">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="4eb73-114">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="4eb73-114">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="4eb73-115">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="4eb73-115">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="4eb73-116">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="4eb73-116">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span>
* <span data-ttu-id="4eb73-117">Does the image contain adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="4eb73-117">Does the image contain adult or sexually suggestive content?</span></span>

<span data-ttu-id="4eb73-118">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4eb73-118">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="4eb73-119">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="4eb73-119">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="4eb73-120">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="4eb73-120">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="4eb73-121">Change the Request URL (`https://westcentralus.api.cognitive.microsoft.com/vision/v2.0`) to use the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="4eb73-121">Change the Request URL (`https://westcentralus.api.cognitive.microsoft.com/vision/v2.0`) to use the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="4eb73-122">Optionally, change the image (`{\"url\":\"...`) to analyze.</span><span class="sxs-lookup"><span data-stu-id="4eb73-122">Optionally, change the image (`{\"url\":\"...`) to analyze.</span></span>
1. <span data-ttu-id="4eb73-123">Optionally, change the response language (`language=en`).</span><span class="sxs-lookup"><span data-stu-id="4eb73-123">Optionally, change the response language (`language=en`).</span></span>
1. <span data-ttu-id="4eb73-124">Open a command window on a computer with cURL installed.</span><span class="sxs-lookup"><span data-stu-id="4eb73-124">Open a command window on a computer with cURL installed.</span></span>
1. <span data-ttu-id="4eb73-125">Paste the code in the window and run the command.</span><span class="sxs-lookup"><span data-stu-id="4eb73-125">Paste the code in the window and run the command.</span></span>

>[!NOTE]
><span data-ttu-id="4eb73-126">You must use the same location in your REST call as you used to obtain your subscription keys.</span><span class="sxs-lookup"><span data-stu-id="4eb73-126">You must use the same location in your REST call as you used to obtain your subscription keys.</span></span> <span data-ttu-id="4eb73-127">For example, if you obtained your subscription keys from westus, replace "westcentralus" in the URL below with "westus".</span><span class="sxs-lookup"><span data-stu-id="4eb73-127">For example, if you obtained your subscription keys from westus, replace "westcentralus" in the URL below with "westus".</span></span>

## <a name="analyze-image-request"></a><span data-ttu-id="4eb73-128">Analyze Image request</span><span class="sxs-lookup"><span data-stu-id="4eb73-128">Analyze Image request</span></span>

```json
curl -H "Ocp-Apim-Subscription-Key: <Subscription Key>" -H "Content-Type: application/json" "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Description&details=Landmarks&language=en" -d "{\"url\":\"http://upload.wikimedia.org/wikipedia/commons/3/3c/Shaki_waterfall.jpg\"}"
```

## <a name="analyze-image-response"></a><span data-ttu-id="4eb73-129">Analyze Image response</span><span class="sxs-lookup"><span data-stu-id="4eb73-129">Analyze Image response</span></span>

<span data-ttu-id="4eb73-130">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="4eb73-130">A successful response is returned in JSON, for example:</span></span>

```json
{
  "categories": [
    {
      "name": "outdoor_water",
      "score": 0.9921875,
      "detail": {
        "landmarks": []
      }
    }
  ],
  "description": {
    "tags": [
      "nature",
      "water",
      "waterfall",
      "outdoor",
      "rock",
      "mountain",
      "rocky",
      "grass",
      "hill",
      "covered",
      "hillside",
      "standing",
      "side",
      "group",
      "walking",
      "white",
      "man",
      "large",
      "snow",
      "grazing",
      "forest",
      "slope",
      "herd",
      "river",
      "giraffe",
      "field"
    ],
    "captions": [
      {
        "text": "a large waterfall over a rocky cliff",
        "confidence": 0.916458423253597
      }
    ]
  },
  "requestId": "b6e33879-abb2-43a0-a96e-02cb5ae0b795",
  "metadata": {
    "height": 959,
    "width": 1280,
    "format": "Jpeg"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="4eb73-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="4eb73-131">Next steps</span></span>

<span data-ttu-id="4eb73-132">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="4eb73-132">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="4eb73-133">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="4eb73-133">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4eb73-134">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="4eb73-134">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
