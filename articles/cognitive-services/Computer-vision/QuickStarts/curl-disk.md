---
title: 'Quickstart: Analyze a local image - REST, cURL - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze a local image using Computer Vision with cURL in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 941a46524ab4904029af771740cbdb534dec1cb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968201"
---
# <a name="quickstart-analyze-a-local-image---rest-curl---computer-vision"></a><span data-ttu-id="899ff-103">Quickstart: Analyze a local image - REST, cURL - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="899ff-103">Quickstart: Analyze a local image - REST, cURL - Computer Vision</span></span>

<span data-ttu-id="899ff-104">In this quickstart, you analyze a local image to extract visual features using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="899ff-104">In this quickstart, you analyze a local image to extract visual features using Computer Vision.</span></span> <span data-ttu-id="899ff-105">To analyze a remote image, see [Analyze a remote image with cURL](curl-analyze.md).</span><span class="sxs-lookup"><span data-stu-id="899ff-105">To analyze a remote image, see [Analyze a remote image with cURL](curl-analyze.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="899ff-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="899ff-106">Prerequisites</span></span>

<span data-ttu-id="899ff-107">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="899ff-107">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="analyze-a-local-image"></a><span data-ttu-id="899ff-108">Analyze a local image</span><span class="sxs-lookup"><span data-stu-id="899ff-108">Analyze a local image</span></span>

<span data-ttu-id="899ff-109">This sample is similar to [Analyze a remote image with cURL](curl-analyze.md) except the image to analyze is read locally from disk.</span><span class="sxs-lookup"><span data-stu-id="899ff-109">This sample is similar to [Analyze a remote image with cURL](curl-analyze.md) except the image to analyze is read locally from disk.</span></span> <span data-ttu-id="899ff-110">Three changes are required:</span><span class="sxs-lookup"><span data-stu-id="899ff-110">Three changes are required:</span></span>

- <span data-ttu-id="899ff-111">Change the Content-Type to `"Content-Type: application/octet-stream"`.</span><span class="sxs-lookup"><span data-stu-id="899ff-111">Change the Content-Type to `"Content-Type: application/octet-stream"`.</span></span>
- <span data-ttu-id="899ff-112">Change the `-d` switch to `--data-binary`.</span><span class="sxs-lookup"><span data-stu-id="899ff-112">Change the `-d` switch to `--data-binary`.</span></span>
- <span data-ttu-id="899ff-113">Specify the image to analyze using the following syntax: `@C:/Pictures/ImageToAnalyze.jpg`.</span><span class="sxs-lookup"><span data-stu-id="899ff-113">Specify the image to analyze using the following syntax: `@C:/Pictures/ImageToAnalyze.jpg`.</span></span>

<span data-ttu-id="899ff-114">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="899ff-114">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="899ff-115">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="899ff-115">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="899ff-116">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="899ff-116">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="899ff-117">Change the Request URL (`https://westcentralus.api.cognitive.microsoft.com/vision/v2.0`) to use the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="899ff-117">Change the Request URL (`https://westcentralus.api.cognitive.microsoft.com/vision/v2.0`) to use the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="899ff-118">Replace `<Image To Analyze>` with the local image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="899ff-118">Replace `<Image To Analyze>` with the local image you want to analyze.</span></span>
1. <span data-ttu-id="899ff-119">Optionally, change the response language (`language=en`).</span><span class="sxs-lookup"><span data-stu-id="899ff-119">Optionally, change the response language (`language=en`).</span></span>
1. <span data-ttu-id="899ff-120">Open a command window on a computer with cURL installed.</span><span class="sxs-lookup"><span data-stu-id="899ff-120">Open a command window on a computer with cURL installed.</span></span>
1. <span data-ttu-id="899ff-121">Paste the code in the window and run the command.</span><span class="sxs-lookup"><span data-stu-id="899ff-121">Paste the code in the window and run the command.</span></span>

>[!NOTE]
><span data-ttu-id="899ff-122">You must use the same location in your REST call as you used to obtain your subscription keys.</span><span class="sxs-lookup"><span data-stu-id="899ff-122">You must use the same location in your REST call as you used to obtain your subscription keys.</span></span> <span data-ttu-id="899ff-123">For example, if you obtained your subscription keys from westus, replace "westcentralus" in the URL below with "westus".</span><span class="sxs-lookup"><span data-stu-id="899ff-123">For example, if you obtained your subscription keys from westus, replace "westcentralus" in the URL below with "westus".</span></span>

```json
curl -H "Ocp-Apim-Subscription-Key: <Subscription Key>" -H "Content-Type: application/octet-stream" "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Description&details=Landmarks&language=en" --data-binary <Image To Analyze>
```

## <a name="analyze-image-response"></a><span data-ttu-id="899ff-124">Analyze Image response</span><span class="sxs-lookup"><span data-stu-id="899ff-124">Analyze Image response</span></span>

<span data-ttu-id="899ff-125">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="899ff-125">A successful response is returned in JSON, for example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="899ff-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="899ff-126">Next steps</span></span>

<span data-ttu-id="899ff-127">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="899ff-127">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="899ff-128">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="899ff-128">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="899ff-129">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="899ff-129">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
