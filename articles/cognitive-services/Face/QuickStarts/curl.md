---
title: Face API cURL quickstart | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: In this quickstart, you detect faces from an image using the Face API with cURL in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: face-api
ms.topic: quickstart
ms.date: 05/10/2018
ms.author: nolachar
ms.openlocfilehash: 70c73d947679c8866ce67f4eb0678c11fd059a6c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830804"
---
# <a name="quickstart-detect-faces-in-an-image-using-curl"></a><span data-ttu-id="6c28e-103">Quickstart: Detect faces in an image using cURL</span><span class="sxs-lookup"><span data-stu-id="6c28e-103">Quickstart: Detect faces in an image using cURL</span></span>

<span data-ttu-id="6c28e-104">In this quickstart, you detect faces in an image using Face API.</span><span class="sxs-lookup"><span data-stu-id="6c28e-104">In this quickstart, you detect faces in an image using Face API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c28e-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c28e-105">Prerequisites</span></span>

<span data-ttu-id="6c28e-106">You need a subscription key to run the sample.</span><span class="sxs-lookup"><span data-stu-id="6c28e-106">You need a subscription key to run the sample.</span></span> <span data-ttu-id="6c28e-107">You can get free trial subscription keys from [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=face-api).</span><span class="sxs-lookup"><span data-stu-id="6c28e-107">You can get free trial subscription keys from [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=face-api).</span></span>

## <a name="detect-faces-in-an-image"></a><span data-ttu-id="6c28e-108">Detect faces in an image</span><span class="sxs-lookup"><span data-stu-id="6c28e-108">Detect faces in an image</span></span>

<span data-ttu-id="6c28e-109">Use the [Face - Detect](https://westcentralus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) method to detect faces in an image and return face attributes including:</span><span class="sxs-lookup"><span data-stu-id="6c28e-109">Use the [Face - Detect](https://westcentralus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) method to detect faces in an image and return face attributes including:</span></span>

* <span data-ttu-id="6c28e-110">Face ID: Unique ID used in several Face API scenarios.</span><span class="sxs-lookup"><span data-stu-id="6c28e-110">Face ID: Unique ID used in several Face API scenarios.</span></span>
* <span data-ttu-id="6c28e-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span><span class="sxs-lookup"><span data-stu-id="6c28e-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span></span>
* <span data-ttu-id="6c28e-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span><span class="sxs-lookup"><span data-stu-id="6c28e-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span></span>
* <span data-ttu-id="6c28e-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span><span class="sxs-lookup"><span data-stu-id="6c28e-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span></span>

<span data-ttu-id="6c28e-114">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c28e-114">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="6c28e-115">Open a Command Prompt.</span><span class="sxs-lookup"><span data-stu-id="6c28e-115">Open a Command Prompt.</span></span>
2. <span data-ttu-id="6c28e-116">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="6c28e-116">Replace `<Subscription Key>` with your valid subscription key.</span></span>
3. <span data-ttu-id="6c28e-117">Change the URL (`https://westcentralus.api.cognitive.microsoft.com/face/v1.0/detect`) to use the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="6c28e-117">Change the URL (`https://westcentralus.api.cognitive.microsoft.com/face/v1.0/detect`) to use the location where you obtained your subscription keys, if necessary.</span></span>
4. <span data-ttu-id="6c28e-118">Optionally, change the image (`"{\"url\":...`) to analyze.</span><span class="sxs-lookup"><span data-stu-id="6c28e-118">Optionally, change the image (`"{\"url\":...`) to analyze.</span></span>
5. <span data-ttu-id="6c28e-119">Paste the code in the command window.</span><span class="sxs-lookup"><span data-stu-id="6c28e-119">Paste the code in the command window.</span></span>
6. <span data-ttu-id="6c28e-120">Run the command.</span><span class="sxs-lookup"><span data-stu-id="6c28e-120">Run the command.</span></span>

### <a name="face---detect-request"></a><span data-ttu-id="6c28e-121">Face - Detect request</span><span class="sxs-lookup"><span data-stu-id="6c28e-121">Face - Detect request</span></span>

> [!NOTE]
> <span data-ttu-id="6c28e-122">You must use the same location in your REST call as you used to obtain your subscription keys.</span><span class="sxs-lookup"><span data-stu-id="6c28e-122">You must use the same location in your REST call as you used to obtain your subscription keys.</span></span> <span data-ttu-id="6c28e-123">For example, if you obtained your subscription keys from westus, replace "westcentralus" in the following URL with "westus".</span><span class="sxs-lookup"><span data-stu-id="6c28e-123">For example, if you obtained your subscription keys from westus, replace "westcentralus" in the following URL with "westus".</span></span>

```shell
curl -H "Ocp-Apim-Subscription-Key: <Subscription Key>" "https://westcentralus.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=true&returnFaceLandmarks=false&returnFaceAttributes=age,gender,headPose,smile,facialHair,glasses,emotion,hair,makeup,occlusion,accessories,blur,exposure,noise" -H "Content-Type: application/json" --data-ascii "{\"url\":\"https://upload.wikimedia.org/wikipedia/commons/c/c3/RH_Louise_Lillian_Gish.jpg\"}"
```

### <a name="face---detect-response"></a><span data-ttu-id="6c28e-124">Face - Detect response</span><span class="sxs-lookup"><span data-stu-id="6c28e-124">Face - Detect response</span></span>

<span data-ttu-id="6c28e-125">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="6c28e-125">A successful response is returned in JSON.</span></span>

```json
[
  {
    "faceId": "49d55c17-e018-4a42-ba7b-8cbbdfae7c6f",
    "faceRectangle": {
      "top": 131,
      "left": 177,
      "width": 162,
      "height": 162
    },
    "faceAttributes": {
      "smile": 0,
      "headPose": {
        "pitch": 0,
        "roll": 0.1,
        "yaw": -32.9
      },
      "gender": "female",
      "age": 22.9,
      "facialHair": {
        "moustache": 0,
        "beard": 0,
        "sideburns": 0
      },
      "glasses": "NoGlasses",
      "emotion": {
        "anger": 0,
        "contempt": 0,
        "disgust": 0,
        "fear": 0,
        "happiness": 0,
        "neutral": 0.986,
        "sadness": 0.009,
        "surprise": 0.005
      },
      "blur": {
        "blurLevel": "low",
        "value": 0.06
      },
      "exposure": {
        "exposureLevel": "goodExposure",
        "value": 0.67
      },
      "noise": {
        "noiseLevel": "low",
        "value": 0
      },
      "makeup": {
        "eyeMakeup": true,
        "lipMakeup": true
      },
      "accessories": [],
      "occlusion": {
        "foreheadOccluded": false,
        "eyeOccluded": false,
        "mouthOccluded": false
      },
      "hair": {
        "bald": 0,
        "invisible": false,
        "hairColor": [
          {
            "color": "brown",
            "confidence": 1
          },
          {
            "color": "black",
            "confidence": 0.87
          },
          {
            "color": "other",
            "confidence": 0.51
          },
          {
            "color": "blond",
            "confidence": 0.08
          },
          {
            "color": "red",
            "confidence": 0.08
          },
          {
            "color": "gray",
            "confidence": 0.02
          }
        ]
      }
    }
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="6c28e-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c28e-126">Next steps</span></span>

<span data-ttu-id="6c28e-127">Explore the Face APIs used to detect human faces in an image, demarcate the faces with rectangles, and return attributes such as age and gender.</span><span class="sxs-lookup"><span data-stu-id="6c28e-127">Explore the Face APIs used to detect human faces in an image, demarcate the faces with rectangles, and return attributes such as age and gender.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6c28e-128">Face APIs</span><span class="sxs-lookup"><span data-stu-id="6c28e-128">Face APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236)
