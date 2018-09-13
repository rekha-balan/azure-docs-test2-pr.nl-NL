---
title: Face API Node.js quickstart | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you detect faces from an image using the Face API with Node.js in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: face-api
ms.topic: quickstart
ms.date: 06/08/2018
ms.author: nolachar
ms.openlocfilehash: 15e6db9c9d92e60f18bf2d7708403fd8b0b7a990
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856683"
---
# <a name="quickstart-detect-faces-in-an-image-using-nodejs"></a><span data-ttu-id="fe65d-103">Quickstart: Detect faces in an image using Node.js</span><span class="sxs-lookup"><span data-stu-id="fe65d-103">Quickstart: Detect faces in an image using Node.js</span></span>

<span data-ttu-id="fe65d-104">In this quickstart, you detect human faces in an image using the Face API.</span><span class="sxs-lookup"><span data-stu-id="fe65d-104">In this quickstart, you detect human faces in an image using the Face API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe65d-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fe65d-105">Prerequisites</span></span>

<span data-ttu-id="fe65d-106">You need a subscription key to run the sample.</span><span class="sxs-lookup"><span data-stu-id="fe65d-106">You need a subscription key to run the sample.</span></span> <span data-ttu-id="fe65d-107">You can get free trial subscription keys from [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=face-api).</span><span class="sxs-lookup"><span data-stu-id="fe65d-107">You can get free trial subscription keys from [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=face-api).</span></span>

## <a name="face---detect-request"></a><span data-ttu-id="fe65d-108">Face - Detect request</span><span class="sxs-lookup"><span data-stu-id="fe65d-108">Face - Detect request</span></span>

<span data-ttu-id="fe65d-109">Use the [Face - Detect](https://westcentralus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) method to detect faces in an image and return face attributes including:</span><span class="sxs-lookup"><span data-stu-id="fe65d-109">Use the [Face - Detect](https://westcentralus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) method to detect faces in an image and return face attributes including:</span></span>

* <span data-ttu-id="fe65d-110">Face ID: Unique ID used in several Face API scenarios.</span><span class="sxs-lookup"><span data-stu-id="fe65d-110">Face ID: Unique ID used in several Face API scenarios.</span></span>
* <span data-ttu-id="fe65d-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span><span class="sxs-lookup"><span data-stu-id="fe65d-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span></span>
* <span data-ttu-id="fe65d-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span><span class="sxs-lookup"><span data-stu-id="fe65d-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span></span>
* <span data-ttu-id="fe65d-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span><span class="sxs-lookup"><span data-stu-id="fe65d-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span></span>

<span data-ttu-id="fe65d-114">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="fe65d-114">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="fe65d-115">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="fe65d-115">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="fe65d-116">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="fe65d-116">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="fe65d-117">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="fe65d-117">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="fe65d-118">Optionally, set `imageUri` to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="fe65d-118">Optionally, set `imageUri` to the image you want to analyze.</span></span>
1. <span data-ttu-id="fe65d-119">Save the file with an `.js` extension.</span><span class="sxs-lookup"><span data-stu-id="fe65d-119">Save the file with an `.js` extension.</span></span>
1. <span data-ttu-id="fe65d-120">Open the Node.js command prompt and run the file, for example: `node myfile.js`.</span><span class="sxs-lookup"><span data-stu-id="fe65d-120">Open the Node.js command prompt and run the file, for example: `node myfile.js`.</span></span>

```nodejs
'use strict';

const request = require('request');

// Replace <Subscription Key> with your valid subscription key.
const subscriptionKey = '<Subscription Key>';

// You must use the same location in your REST call as you used to get your
// subscription keys. For example, if you got your subscription keys from
// westus, replace "westcentralus" in the URL below with "westus".
const uriBase = 'https://westcentralus.api.cognitive.microsoft.com/face/v1.0/detect';

const imageUrl =
    'https://upload.wikimedia.org/wikipedia/commons/3/37/Dagestani_man_and_woman.jpg';

// Request parameters.
const params = {
    'returnFaceId': 'true',
    'returnFaceLandmarks': 'false',
    'returnFaceAttributes': 'age,gender,headPose,smile,facialHair,glasses,' +
        'emotion,hair,makeup,occlusion,accessories,blur,exposure,noise'
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

## <a name="face---detect-response"></a><span data-ttu-id="fe65d-121">Face - Detect response</span><span class="sxs-lookup"><span data-stu-id="fe65d-121">Face - Detect response</span></span>

<span data-ttu-id="fe65d-122">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="fe65d-122">A successful response is returned in JSON, for example:</span></span>

```json
[
  {
    "faceId": "ae8952c1-7b5e-4a5a-a330-a6aa351262c9",
    "faceRectangle": {
      "top": 621,
      "left": 616,
      "width": 195,
      "height": 195
    },
    "faceAttributes": {
      "smile": 0,
      "headPose": {
        "pitch": 0,
        "roll": 6.8,
        "yaw": 3.7
      },
      "gender": "male",
      "age": 37,
      "facialHair": {
        "moustache": 0.4,
        "beard": 0.4,
        "sideburns": 0.1
      },
      "glasses": "NoGlasses",
      "emotion": {
        "anger": 0,
        "contempt": 0,
        "disgust": 0,
        "fear": 0,
        "happiness": 0,
        "neutral": 0.999,
        "sadness": 0.001,
        "surprise": 0
      },
      "blur": {
        "blurLevel": "high",
        "value": 0.89
      },
      "exposure": {
        "exposureLevel": "goodExposure",
        "value": 0.51
      },
      "noise": {
        "noiseLevel": "medium",
        "value": 0.59
      },
      "makeup": {
        "eyeMakeup": true,
        "lipMakeup": false
      },
      "accessories": [],
      "occlusion": {
        "foreheadOccluded": false,
        "eyeOccluded": false,
        "mouthOccluded": false
      },
      "hair": {
        "bald": 0.04,
        "invisible": false,
        "hairColor": [
          {
            "color": "black",
            "confidence": 0.98
          },
          {
            "color": "brown",
            "confidence": 0.87
          },
          {
            "color": "gray",
            "confidence": 0.85
          },
          {
            "color": "other",
            "confidence": 0.25
          },
          {
            "color": "blond",
            "confidence": 0.07
          },
          {
            "color": "red",
            "confidence": 0.02
          }
        ]
      }
    }
  },
  {
    "faceId": "b1bb3cbe-5a73-4f8d-96c8-836a5aca9415",
    "faceRectangle": {
      "top": 693,
      "left": 1503,
      "width": 180,
      "height": 180
    },
    "faceAttributes": {
      "smile": 0.003,
      "headPose": {
        "pitch": 0,
        "roll": 2,
        "yaw": -2.2
      },
      "gender": "female",
      "age": 56,
      "facialHair": {
        "moustache": 0,
        "beard": 0,
        "sideburns": 0
      },
      "glasses": "NoGlasses",
      "emotion": {
        "anger": 0,
        "contempt": 0.001,
        "disgust": 0,
        "fear": 0,
        "happiness": 0.003,
        "neutral": 0.984,
        "sadness": 0.011,
        "surprise": 0
      },
      "blur": {
        "blurLevel": "high",
        "value": 0.83
      },
      "exposure": {
        "exposureLevel": "goodExposure",
        "value": 0.41
      },
      "noise": {
        "noiseLevel": "high",
        "value": 0.76
      },
      "makeup": {
        "eyeMakeup": false,
        "lipMakeup": false
      },
      "accessories": [],
      "occlusion": {
        "foreheadOccluded": false,
        "eyeOccluded": false,
        "mouthOccluded": false
      },
      "hair": {
        "bald": 0.06,
        "invisible": false,
        "hairColor": [
          {
            "color": "black",
            "confidence": 0.99
          },
          {
            "color": "gray",
            "confidence": 0.89
          },
          {
            "color": "other",
            "confidence": 0.64
          },
          {
            "color": "brown",
            "confidence": 0.34
          },
          {
            "color": "blond",
            "confidence": 0.07
          },
          {
            "color": "red",
            "confidence": 0.03
          }
        ]
      }
    }
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="fe65d-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="fe65d-123">Next steps</span></span>

<span data-ttu-id="fe65d-124">Explore the Face APIs used to detect human faces in an image, demarcate the faces with rectangles, and return attributes such as age and gender.</span><span class="sxs-lookup"><span data-stu-id="fe65d-124">Explore the Face APIs used to detect human faces in an image, demarcate the faces with rectangles, and return attributes such as age and gender.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe65d-125">Face APIs</span><span class="sxs-lookup"><span data-stu-id="fe65d-125">Face APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236)
