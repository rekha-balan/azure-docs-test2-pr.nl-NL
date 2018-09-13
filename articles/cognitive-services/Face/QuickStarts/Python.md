---
title: Face API Python quick start | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Face API with Python in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 03/21/2017
ms.author: anroth
ms.openlocfilehash: bf0cadb283fc6e3ebc91b33f25f662be07652107
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552482"
---
# <a name="face-api-python-quick-starts"></a><span data-ttu-id="93767-103">Face API Python Quick Starts</span><span class="sxs-lookup"><span data-stu-id="93767-103">Face API Python Quick Starts</span></span>
<span data-ttu-id="93767-104">This article provides information and code samples to help you quickly get started using the Face API with Python to accomplish the following tasks:</span><span class="sxs-lookup"><span data-stu-id="93767-104">This article provides information and code samples to help you quickly get started using the Face API with Python to accomplish the following tasks:</span></span> 
* [<span data-ttu-id="93767-105">Detect Faces in Images</span><span class="sxs-lookup"><span data-stu-id="93767-105">Detect Faces in Images</span></span>](#Detect) 
* [<span data-ttu-id="93767-106">Create a Person Group</span><span class="sxs-lookup"><span data-stu-id="93767-106">Create a Person Group</span></span>](#Create)

<span data-ttu-id="93767-107">Learn more about obtaining free Subscription Keys [here](../../Computer-vision/Vision-API-How-to-Topics/HowToSubscribe.md)</span><span class="sxs-lookup"><span data-stu-id="93767-107">Learn more about obtaining free Subscription Keys [here](../../Computer-vision/Vision-API-How-to-Topics/HowToSubscribe.md)</span></span>

## <span data-ttu-id="93767-108">Detect Faces in Images With Face API Using Python <a name="Detect"> </a></span><span class="sxs-lookup"><span data-stu-id="93767-108">Detect Faces in Images With Face API Using Python <a name="Detect"> </a></span></span>
<span data-ttu-id="93767-109">Use the [Face - Detect method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) to detect faces in an image and return face attributes including:</span><span class="sxs-lookup"><span data-stu-id="93767-109">Use the [Face - Detect method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) to detect faces in an image and return face attributes including:</span></span>
* <span data-ttu-id="93767-110">Face ID: Unique ID used in a number of Face API scenarios.</span><span class="sxs-lookup"><span data-stu-id="93767-110">Face ID: Unique ID used in a number of Face API scenarios.</span></span> 
* <span data-ttu-id="93767-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span><span class="sxs-lookup"><span data-stu-id="93767-111">Face Rectangle: The left, top, width, and height indicating the location of the face in the image.</span></span>
* <span data-ttu-id="93767-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span><span class="sxs-lookup"><span data-stu-id="93767-112">Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.</span></span>
* <span data-ttu-id="93767-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span><span class="sxs-lookup"><span data-stu-id="93767-113">Facial attributes including age, gender, smile intensity, head pose, and facial hair.</span></span> 

#### <a name="face-detect-python-example-request"></a><span data-ttu-id="93767-114">Face Detect Python Example Request</span><span class="sxs-lookup"><span data-stu-id="93767-114">Face Detect Python Example Request</span></span>

```python
########### Python 2.7 #############
import httplib, urllib, base64

headers = {
    # Request headers
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '{subscription key}',
}

params = urllib.urlencode({
    # Request parameters
    'returnFaceId': 'true',
    'returnFaceLandmarks': 'false',
    'returnFaceAttributes': '{string}',
})

try:
    conn = httplib.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/face/v1.0/detect?%s" % params, "{body}", headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))

####################################

########### Python 3.2 #############
import http.client, urllib.request, urllib.parse, urllib.error, base64

headers = {
    # Request headers
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '{subscription key}',
}

params = urllib.parse.urlencode({
    # Request parameters
    'returnFaceId': 'true',
    'returnFaceLandmarks': 'false',
    'returnFaceAttributes': '{string}',
})

try:
    conn = http.client.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/face/v1.0/detect?%s" % params, "{body}", headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))

####################################    

```
#### <a name="face---detect-response"></a><span data-ttu-id="93767-115">Face - Detect Response</span><span class="sxs-lookup"><span data-stu-id="93767-115">Face - Detect Response</span></span>
<span data-ttu-id="93767-116">A successful response will be returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="93767-116">A successful response will be returned in JSON.</span></span> <span data-ttu-id="93767-117">Following is an example of a successful response:</span><span class="sxs-lookup"><span data-stu-id="93767-117">Following is an example of a successful response:</span></span> 

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
## <span data-ttu-id="93767-118">Create a Person Group With Face API Using Python <a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="93767-118">Create a Person Group With Face API Using Python <a name="Create"> </a></span></span>
<span data-ttu-id="93767-119">Use the [Person Group - Create a Person Group method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) to create a new person group with specified personGroupId, name, and user-provided userData.</span><span class="sxs-lookup"><span data-stu-id="93767-119">Use the [Person Group - Create a Person Group method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244) to create a new person group with specified personGroupId, name, and user-provided userData.</span></span> <span data-ttu-id="93767-120">A person group is one of the most important parameters for the Face - Identify API.</span><span class="sxs-lookup"><span data-stu-id="93767-120">A person group is one of the most important parameters for the Face - Identify API.</span></span> <span data-ttu-id="93767-121">The Identify API searches for persons' faces in a specified person group.</span><span class="sxs-lookup"><span data-stu-id="93767-121">The Identify API searches for persons' faces in a specified person group.</span></span> 

#### <a name="person-group---create-a-person-group-example"></a><span data-ttu-id="93767-122">Person Group - Create a Person Group Example</span><span class="sxs-lookup"><span data-stu-id="93767-122">Person Group - Create a Person Group Example</span></span>
```python
########### Python 2.7 #############
import httplib, urllib, base64

headers = {
    # Request headers. Replace the placeholder key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

# Replace 'examplegroupid' with an ID you haven't used for creating a group before.
# The valid characters for the ID include numbers, English letters in lower case, '-' and '_'. 
# The maximum length of the ID is 64.
personGroupId = 'examplegroupid'

# The userData field is optional. The size limit for it is 16KB.
body = "{ 'name':'group1', 'userData':'user-provided data attached to the person group' }"

try:
    conn = httplib.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("POST", "/face/v1.0/persongroups/%s" % personGroupId, body, headers)
    response = conn.getresponse()

    # 'OK' indicates success. 'Conflict' means a group with this ID already exists.
    # If you get 'Conflict', change the value of personGroupId above and try again.
    # If you get 'Access Denied', verify the validity of the subscription key above and try again.
    print(response.reason)

    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))
####################################

########### Python 3.2 #############
import http.client, urllib.request, urllib.parse, urllib.error, base64, sys

headers = {
    # Request headers. Replace the placeholder key below with your subscription key.
    'Content-Type': 'application/json',
    'Ocp-Apim-Subscription-Key': '13hc77781f7e4b19b5fcdd72a8df7156',
}

# Replace 'examplegroupid' with an ID you haven't used for creating a group before.
# The valid characters for the ID include numbers, English letters in lower case, '-' and '_'. 
# The maximum length of the ID is 64.
personGroupId = 'examplegroupid'

# The userData field is optional. The size limit for it is 16KB.
body = "{ 'name':'group1', 'userData':'user-provided data attached to the person group' }"

try:
    conn = http.client.HTTPSConnection('westus.api.cognitive.microsoft.com')
    conn.request("PUT", "/face/v1.0/persongroups/%s" % personGroupId, body, headers)
    response = conn.getresponse()

    # 'OK' indicates success. 'Conflict' means a group with this ID already exists.
    # If you get 'Conflict', change the value of personGroupId above and try again.
    # If you get 'Access Denied', verify the validity of the subscription key above and try again.
    print(response.reason)

    conn.close()
except Exception as e:
    print(e.args)
####################################
