---
title: 'Quickstart: Analyze a remote image - REST, Node.js - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze an image using Computer Vision with Node.js in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 479da5fbbe0e6a5532b40da574e0e567febe7393
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868449"
---
# <a name="quickstart-analyze-a-remote-image---rest-nodejs---computer-vision"></a><span data-ttu-id="d6c84-103">Quickstart: Analyze a remote image - REST, Node.js - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="d6c84-103">Quickstart: Analyze a remote image - REST, Node.js - Computer Vision</span></span>

<span data-ttu-id="d6c84-104">In this quickstart, you analyze an image to extract visual features using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="d6c84-104">In this quickstart, you analyze an image to extract visual features using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6c84-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d6c84-105">Prerequisites</span></span>

<span data-ttu-id="d6c84-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="d6c84-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="analyze-image-request"></a><span data-ttu-id="d6c84-107">Analyze Image request</span><span class="sxs-lookup"><span data-stu-id="d6c84-107">Analyze Image request</span></span>

<span data-ttu-id="d6c84-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="d6c84-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="d6c84-109">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="d6c84-109">You can upload an image or specify an image URL and choose which features to return, including:</span></span>

* <span data-ttu-id="d6c84-110">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="d6c84-110">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="d6c84-111">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="d6c84-111">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="d6c84-112">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="d6c84-112">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="d6c84-113">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="d6c84-113">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="d6c84-114">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="d6c84-114">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="d6c84-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="d6c84-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span>
* <span data-ttu-id="d6c84-116">Does the image contain adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="d6c84-116">Does the image contain adult or sexually suggestive content?</span></span>

<span data-ttu-id="d6c84-117">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="d6c84-117">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="d6c84-118">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="d6c84-118">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="d6c84-119">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="d6c84-119">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="d6c84-120">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="d6c84-120">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="d6c84-121">Optionally, change the `imageUrl` value to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="d6c84-121">Optionally, change the `imageUrl` value to the image you want to analyze.</span></span>
1. <span data-ttu-id="d6c84-122">Optionally, change the response language (`'language': 'en'`).</span><span class="sxs-lookup"><span data-stu-id="d6c84-122">Optionally, change the response language (`'language': 'en'`).</span></span>
1. <span data-ttu-id="d6c84-123">Save the file with an `.js` extension.</span><span class="sxs-lookup"><span data-stu-id="d6c84-123">Save the file with an `.js` extension.</span></span>
1. <span data-ttu-id="d6c84-124">Open the Node.js command prompt and run the file, for example: `node myfile.js`.</span><span class="sxs-lookup"><span data-stu-id="d6c84-124">Open the Node.js command prompt and run the file, for example: `node myfile.js`.</span></span>

<span data-ttu-id="d6c84-125">This sample uses the npm [request](https://www.npmjs.com/package/request) package.</span><span class="sxs-lookup"><span data-stu-id="d6c84-125">This sample uses the npm [request](https://www.npmjs.com/package/request) package.</span></span>

```nodejs
'use strict';

const request = require('request');

// Replace <Subscription Key> with your valid subscription key.
const subscriptionKey = '<Subscription Key>';

// You must use the same location in your REST call as you used to get your
// subscription keys. For example, if you got your subscription keys from
// westus, replace "westcentralus" in the URL below with "westus".
const uriBase =
    'https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/analyze';

const imageUrl =
    'http://upload.wikimedia.org/wikipedia/commons/3/3c/Shaki_waterfall.jpg';

// Request parameters.
const params = {
    'visualFeatures': 'Categories,Description,Color',
    'details': '',
    'language': 'en'
};

const options = {
    uri: uriBase,
    qs: params,
    body: '{"url": ' + '"' + imageUrl + '"}',
    headers: {
        'Content-Type': 'application/json',
        'Ocp-Apim-Subscription-Key' : subscriptionKey
    }
};

request.post(options, (error, response, body) => {
  if (error) {
    console.log('Error: ', error);
    return;
  }
  let jsonResponse = JSON.stringify(JSON.parse(body), null, '  ');
  console.log('JSON Response\n');
  console.log(jsonResponse);
});
```

## <a name="analyze-image-response"></a><span data-ttu-id="d6c84-126">Analyze Image response</span><span class="sxs-lookup"><span data-stu-id="d6c84-126">Analyze Image response</span></span>

<span data-ttu-id="d6c84-127">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="d6c84-127">A successful response is returned in JSON, for example:</span></span>

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
  "color": {
    "dominantColorForeground": "Grey",
    "dominantColorBackground": "Green",
    "dominantColors": [
      "Grey",
      "Green"
    ],
    "accentColor": "4D5E2F",
    "isBwImg": false
  },
  "requestId": "81b4e400-e3c1-41f1-9020-e6871ad9f0ed",
  "metadata": {
    "height": 959,
    "width": 1280,
    "format": "Jpeg"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="d6c84-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6c84-128">Next steps</span></span>

<span data-ttu-id="d6c84-129">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="d6c84-129">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="d6c84-130">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="d6c84-130">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6c84-131">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="d6c84-131">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
