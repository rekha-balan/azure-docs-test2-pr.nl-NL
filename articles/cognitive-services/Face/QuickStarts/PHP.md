---
title: Face API PHP quick start | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Face API with PHP in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: face
ms.topic: article
ms.date: 03/21/2017
ms.author: anroth
ms.openlocfilehash: dfa6bada6da5a51c23e1156358aa8ffb0fc94196
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660543"
---
# <a name="face-api-php-quick-starts"></a>Face API PHP Quick Starts
This article provides information and code samples to help you quickly get started using the Face API with PHP to accomplish the following tasks: 
* [Detect Faces in Images](#Detect) 
* [Identify Faces in Images](#Identify)

Learn more about obtaining free Subscription Keys [here](../../Computer-vision/Vision-API-How-to-Topics/HowToSubscribe.md).

## Detect Faces in Images With Face API Using PHP <a name="Detect"> </a>
Use the [Face - Detect method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) to detect faces in an image and return face attributes including:
* Face ID: Unique ID used in a number of Face API scenarios. 
* Face Rectangle: The left, top, width, and height indicating the location of the face in the image.
* Landmarks: An array of 27-point face landmarks pointing to the important positions of face components.
* Facial attributes including age, gender, smile intensity, head pose, and facial hair. 

#### <a name="face-detect-php-example-request"></a>Face Detect PHP Example Request
 
```php
<?php
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
require_once 'HTTP/Request2.php';

$request = new Http_Request2('https://westus.api.cognitive.microsoft.com/face/v1.0/detect');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => '{subscription key}',
);

$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'returnFaceId' => 'true',
    'returnFaceLandmarks' => 'false',
    'returnFaceAttributes' => '{string}',
);

$url->setQueryVariables($parameters);

$request->setMethod(HTTP_Request2::METHOD_POST);

// Request body
$request->setBody("{body}");

try
{
    $response = $request->send();
    echo $response->getBody();
}
catch (HttpException $ex)
{
    echo $ex;
}

?>  

```
#### <a name="face---detect-response"></a>Face - Detect Response
A successful response will be returned in JSON. Following is an example of a successful response: 

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
## Identify Faces in Images With Face API Using PHP <a name="Identify"> </a>
Use the [Face - Identify method](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239) identify people based on a detected face and people database (defined as a person group) which needs to be created in advance and can be edited over time

#### <a name="face---identify-php-example-request"></a>Face - Identify PHP Example Request
```php
<?php
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
require_once 'HTTP/Request2.php';

$request = new Http_Request2('https://westus.api.cognitive.microsoft.com/face/v1.0/identify');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => '{subscription key}',
);

$request->setHeader($headers);

$parameters = array(
    // Request parameters
);

$url->setQueryVariables($parameters);

$request->setMethod(HTTP_Request2::METHOD_POST);

// Request body
$request->setBody("{body}");

try
{
    $response = $request->send();
    echo $response->getBody();
}
catch (HttpException $ex)
{
    echo $ex;
}

?>

```
#### <a name="face---identify-response"></a>Face - Identify Response
A successful response will be returned in JSON. Following is an example of a successful response: 
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

