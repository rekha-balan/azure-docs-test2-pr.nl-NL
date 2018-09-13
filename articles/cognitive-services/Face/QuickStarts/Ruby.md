---
title: Face API Ruby quick start | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Face API with Ruby in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 03/21/2017
ms.author: anroth
ms.openlocfilehash: 73994a1774289d4242074032716ba3e65aec4ff3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563160"
---
# <a name="face-api-ruby-quick-starts"></a><span data-ttu-id="c7585-103">Face API Ruby Quick Starts</span><span class="sxs-lookup"><span data-stu-id="c7585-103">Face API Ruby Quick Starts</span></span>
<span data-ttu-id="c7585-104">This article provides information and code samples to help you quickly get started using the Face API with Ruby to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="c7585-104">This article provides information and code samples to help you quickly get started using the Face API with Ruby to accomplish the following tasks:</span></span> 
* [<span data-ttu-id="c7585-105">Detect Faces in Images</span><span class="sxs-lookup"><span data-stu-id="c7585-105">Detect Faces in Images</span></span>](#Detect) 
* [<span data-ttu-id="c7585-106">Identify Faces in Images</span><span class="sxs-lookup"><span data-stu-id="c7585-106">Identify Faces in Images</span></span>](#Identify)

<span data-ttu-id="c7585-107">Learn more about obtaining free Subscription Keys [here](../../Computer-vision/Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="c7585-107">Learn more about obtaining free Subscription Keys [here](../../Computer-vision/Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <span data-ttu-id="c7585-108">Detect Faces in Images With Face API Using Ruby <a name="Detect"> </a></span><span class="sxs-lookup"><span data-stu-id="c7585-108">Detect Faces in Images With Face API Using Ruby <a name="Detect"> </a></span></span>
<span data-ttu-id="c7585-109">Use the [Face - Detect method](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) to detect faces in an image and return face attributes including:</span><span class="sxs-lookup"><span data-stu-id="c7585-109">Use the [Face - Detect method](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) to detect faces in an image and return face attributes including:</span></span>
* <span data-ttu-id="c7585-110">Face ID: Unique ID used in a number of Face API scenarios.</span><span class="sxs-lookup"><span data-stu-id="c7585-110">Face ID: Unique ID used in a number of Face API scenarios.</span></span> 
* <span data-ttu-id="c7585-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span><span class="sxs-lookup"><span data-stu-id="c7585-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span></span>
* <span data-ttu-id="c7585-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span><span class="sxs-lookup"><span data-stu-id="c7585-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span></span>
* <span data-ttu-id="c7585-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span><span class="sxs-lookup"><span data-stu-id="c7585-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span></span> 

#### <a name="face-detect-ruby-example-request"></a><span data-ttu-id="c7585-114">Face Detect Ruby Example Request</span><span class="sxs-lookup"><span data-stu-id="c7585-114">Face Detect Ruby Example Request</span></span>

```Ruby 
require 'net/http'

uri = URI('https://westus.api.cognitive.microsoft.com/face/v1.0/detect')
uri.query = URI.encode_www_form({
    # Request parameters
    'returnFaceId' => 'true',
    'returnFaceLandmarks' => 'false',
    'returnFaceAttributes' => '{string}'
})

request = Net::HTTP::Post.new(uri.request_uri)
# Request headers
request['Content-Type'] = 'application/json'
# Request headers
request['Ocp-Apim-Subscription-Key'] = '{subscription key}'
# Request body
request.body = "{body}"

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request(request)
end

puts response.body
```

#### <a name="face---detect-response"></a><span data-ttu-id="c7585-115">Face - Detect Response</span><span class="sxs-lookup"><span data-stu-id="c7585-115">Face - Detect Response</span></span>
<span data-ttu-id="c7585-116">A successful response will be returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="c7585-116">A successful response will be returned in JSON.</span></span> <span data-ttu-id="c7585-117">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="c7585-117">Following is an example of a successful response:</span></span> 

```json
[
    {
        "faceId": "c5c24a82-6845-4031-9d5d-978df9175426",
        "faceRectangle": {
            "width": 78,
            "height": 78,
            "left": 394,
            "top": 54
        },
        "faceLandmarks": {
            "pupilLeft": {
                "x": 412.7,
                "y": 78.4 
            },
            "pupilRight": {
                "x": 446.8,
                "y": 74.2 
            },
            "noseTip": {
                "x": 437.7,
                "y": 92.4 
            },
            "mouthLeft": {
                "x": 417.8,
                "y": 114.4 
            },
            "mouthRight": {
                "x": 451.3,
                "y": 109.3 
            },
            "eyebrowLeftOuter": {
                "x": 397.9,
                "y": 78.5 
            },
            "eyebrowLeftInner": {
                "x": 425.4,
                "y": 70.5 
            },
            "eyeLeftOuter": {
                "x": 406.7,
                "y": 80.6 
            },
            "eyeLeftTop": {
                "x": 412.2,
                "y": 76.2 
            },
            "eyeLeftBottom": {
                "x": 413.0,
                "y": 80.1 
            },
            "eyeLeftInner": {
                "x": 418.9,
                "y": 78.0 
            },
            "eyebrowRightInner": {
                "x": 4.8,
                "y": 69.7 
            },
            "eyebrowRightOuter": {
                "x": 5.5,
                "y": 68.5 
            },
            "eyeRightInner": {
                "x": 441.5,
                "y": 75.0 
            },
            "eyeRightTop": {
                "x": 446.4,
                "y": 71.7 
            },
            "eyeRightBottom": {
                "x": 447.0,
                "y": 75.3 
            },
            "eyeRightOuter": {
                "x": 451.7,
                "y": 73.4 
            },
            "noseRootLeft": {
                "x": 428.0,
                "y": 77.1 
            },
            "noseRootRight": {
                "x": 435.8,
                "y": 75.6 
            },
            "noseLeftAlarTop": {
                "x": 428.3,
                "y": 89.7 
            },
            "noseRightAlarTop": {
                "x": 442.2,
                "y": 87.0 
            },
            "noseLeftAlarOutTip": {
                "x": 424.3,
                "y": 96.4 
            },
            "noseRightAlarOutTip": {
                "x": 446.6,
                "y": 92.5 
            },
            "upperLipTop": {
                "x": 437.6,
                "y": 105.9 
            },
            "upperLipBottom": {
                "x": 437.6,
                "y": 108.2 
            },
            "underLipTop": {
                "x": 436.8,
                "y": 111.4 
            },
            "underLipBottom": {
                "x": 437.3,
                "y": 114.5 
            }
        },
        "faceAttributes": {
            "age": 71.0,
            "gender": "male",
            "smile": 0.88,
            "facialHair": {
                "mustache": 0.8,
                "beard": 0.1,
                "sideburns": 0.02
            },
            "glasses": "sunglasses",
            "headPose": {
                "roll": 2.1,
                "yaw": 3,
                "pitch": 0
            }
        }
    }
]
```

## <span data-ttu-id="c7585-118">Identify Faces in Images With Face API Using Ruby <a name="Identify"> </a></span><span class="sxs-lookup"><span data-stu-id="c7585-118">Identify Faces in Images With Face API Using Ruby <a name="Identify"> </a></span></span>
<span data-ttu-id="c7585-119">Use the [Face - Identify method](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239) identify people based on a detected face and people database (defined as a person group) which needs to be created in advance and can be edited over time</span><span class="sxs-lookup"><span data-stu-id="c7585-119">Use the [Face - Identify method](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239) identify people based on a detected face and people database (defined as a person group) which needs to be created in advance and can be edited over time</span></span>

#### <a name="face---identify-ruby-example-request"></a><span data-ttu-id="c7585-120">Face - Identify Ruby Example Request</span><span class="sxs-lookup"><span data-stu-id="c7585-120">Face - Identify Ruby Example Request</span></span>
```ruby
require 'net/http'

uri = URI('https://westus.api.cognitive.microsoft.com/face/v1.0/identify')
uri.query = URI.encode_www_form({
})

request = Net::HTTP::Post.new(uri.request_uri)
# Request headers
request['Content-Type'] = 'application/json'
# Request headers
request['Ocp-Apim-Subscription-Key'] = '{subscription key}'
# Request body
request.body = "{body}"

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request(request)
end

puts response.body
 
```

#### <a name="face---identify-response"></a><span data-ttu-id="c7585-121">Face - Identify Response</span><span class="sxs-lookup"><span data-stu-id="c7585-121">Face - Identify Response</span></span>
<span data-ttu-id="c7585-122">A successful response will be returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="c7585-122">A successful response will be returned in JSON.</span></span> <span data-ttu-id="c7585-123">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="c7585-123">Following is an example of a successful response:</span></span> 
```json
[
    {
        "faceId":"c5c24a82-6845-4031-9d5d-978df9175426",
        "candidates":[
            {
                "personId":"25985303-c537-4467-b41d-bdb45cd95ca1",
                "confidence":0.92
            }
        ]
    },
    {
        "faceId":"65d083d4-9447-47d1-af30-b626144bf0fb",
        "candidates":[
            {
                "personId":"2ae4935b-9659-44c3-977f-61fac20d0538",
                "confidence":0.89
            }
        ]
    }
]
```
