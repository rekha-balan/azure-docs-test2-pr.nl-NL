---
title: 'Quickstart: Extract printed text (OCR) - REST, Node.js - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you extract printed text from an image using Computer Vision with Node.js in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 540f3ae05fa7049ee5330d613c1c0352e25db57e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870433"
---
# <a name="quickstart-extract-printed-text-ocr---rest-nodejs---computer-vision"></a><span data-ttu-id="97851-103">Quickstart: Extract printed text (OCR) - REST, Node.js - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="97851-103">Quickstart: Extract printed text (OCR) - REST, Node.js - Computer Vision</span></span>

<span data-ttu-id="97851-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="97851-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97851-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="97851-105">Prerequisites</span></span>

<span data-ttu-id="97851-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="97851-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="ocr-request"></a><span data-ttu-id="97851-107">OCR request</span><span class="sxs-lookup"><span data-stu-id="97851-107">OCR request</span></span>

<span data-ttu-id="97851-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="97851-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

<span data-ttu-id="97851-109">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="97851-109">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="97851-110">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="97851-110">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="97851-111">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="97851-111">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="97851-112">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="97851-112">Change the `uriBase` value to the location where you got your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="97851-113">Optionally, change the `imageUrl` value to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="97851-113">Optionally, change the `imageUrl` value to the image you want to analyze.</span></span>
1. <span data-ttu-id="97851-114">Save the file with an `.js` extension.</span><span class="sxs-lookup"><span data-stu-id="97851-114">Save the file with an `.js` extension.</span></span>
1. <span data-ttu-id="97851-115">Open the Node.js command prompt and run the file, for example: `node myfile.js`.</span><span class="sxs-lookup"><span data-stu-id="97851-115">Open the Node.js command prompt and run the file, for example: `node myfile.js`.</span></span>

<span data-ttu-id="97851-116">This sample uses the npm [request](https://www.npmjs.com/package/request) package.</span><span class="sxs-lookup"><span data-stu-id="97851-116">This sample uses the npm [request](https://www.npmjs.com/package/request) package.</span></span>

```nodejs
'use strict';

const request = require('request');

// Replace <Subscription Key> with your valid subscription key.
const subscriptionKey = '<Subscription Key>';

// You must use the same location in your REST call as you used to get your
// subscription keys. For example, if you got your subscription keys from
// westus, replace "westcentralus" in the URL below with "westus".
const uriBase =
    'https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/ocr';

const imageUrl = 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/' +
    'Atomist_quote_from_Democritus.png/338px-Atomist_quote_from_Democritus.png';

// Request parameters.
const params = {
    'language': 'unk',
    'detectOrientation': 'true',
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

## <a name="ocr-response"></a><span data-ttu-id="97851-117">OCR response</span><span class="sxs-lookup"><span data-stu-id="97851-117">OCR response</span></span>

<span data-ttu-id="97851-118">Upon success, the OCR results returned include text, bounding box for regions, lines, and words, for example:</span><span class="sxs-lookup"><span data-stu-id="97851-118">Upon success, the OCR results returned include text, bounding box for regions, lines, and words, for example:</span></span>

```json
{
  "language": "en",
  "orientation": "Up",
  "textAngle": 0,
  "regions": [
    {
      "boundingBox": "21,16,304,451",
      "lines": [
        {
          "boundingBox": "28,16,288,41",
          "words": [
            {
              "boundingBox": "28,16,288,41",
              "text": "NOTHING"
            }
          ]
        },
        {
          "boundingBox": "27,66,283,52",
          "words": [
            {
              "boundingBox": "27,66,283,52",
              "text": "EXISTS"
            }
          ]
        },
        {
          "boundingBox": "27,128,292,49",
          "words": [
            {
              "boundingBox": "27,128,292,49",
              "text": "EXCEPT"
            }
          ]
        },
        {
          "boundingBox": "24,188,292,54",
          "words": [
            {
              "boundingBox": "24,188,292,54",
              "text": "ATOMS"
            }
          ]
        },
        {
          "boundingBox": "22,253,297,32",
          "words": [
            {
              "boundingBox": "22,253,105,32",
              "text": "AND"
            },
            {
              "boundingBox": "144,253,175,32",
              "text": "EMPTY"
            }
          ]
        },
        {
          "boundingBox": "21,298,304,60",
          "words": [
            {
              "boundingBox": "21,298,304,60",
              "text": "SPACE."
            }
          ]
        },
        {
          "boundingBox": "26,387,294,37",
          "words": [
            {
              "boundingBox": "26,387,210,37",
              "text": "Everything"
            },
            {
              "boundingBox": "249,389,71,27",
              "text": "else"
            }
          ]
        },
        {
          "boundingBox": "127,431,198,36",
          "words": [
            {
              "boundingBox": "127,431,31,29",
              "text": "is"
            },
            {
              "boundingBox": "172,431,153,36",
              "text": "opinion."
            }
          ]
        }
      ]
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="97851-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="97851-119">Next steps</span></span>

<span data-ttu-id="97851-120">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="97851-120">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="97851-121">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="97851-121">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="97851-122">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="97851-122">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
