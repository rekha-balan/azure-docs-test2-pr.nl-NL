---
title: Emotion API PHP quick start | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Emotion API with PHP in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 01/30/2017
ms.author: anroth
ms.openlocfilehash: 381c77c06127b96f74bc2903fa1f2afb5a388a2a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549873"
---
# <a name="emotion-api-php-quick-start"></a><span data-ttu-id="7b4a7-103">Emotion API PHP Quick Start</span><span class="sxs-lookup"><span data-stu-id="7b4a7-103">Emotion API PHP Quick Start</span></span>
<span data-ttu-id="7b4a7-104">This article provides information and code samples to help you quickly get started using PHP and the [Emotion API Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) to recognize the emotions expressed by one or more people in an image.</span><span class="sxs-lookup"><span data-stu-id="7b4a7-104">This article provides information and code samples to help you quickly get started using PHP and the [Emotion API Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) to recognize the emotions expressed by one or more people in an image.</span></span> 

## <a name="prerequisite"></a><span data-ttu-id="7b4a7-105">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="7b4a7-105">Prerequisite</span></span>
* <span data-ttu-id="7b4a7-106">Get your free Subscription Key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span><span class="sxs-lookup"><span data-stu-id="7b4a7-106">Get your free Subscription Key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span></span>

## <a name="recognize-emotions-php-example-request"></a><span data-ttu-id="7b4a7-107">Recognize Emotions PHP Example Request</span><span class="sxs-lookup"><span data-stu-id="7b4a7-107">Recognize Emotions PHP Example Request</span></span>

```PHP
<?php
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
require_once 'HTTP/Request2.php';

$request = new Http_Request2('https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognize');
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

## <a name="recognize-emotions-sample-response"></a><span data-ttu-id="7b4a7-108">Recognize Emotions Sample Response</span><span class="sxs-lookup"><span data-stu-id="7b4a7-108">Recognize Emotions Sample Response</span></span>
<span data-ttu-id="7b4a7-109">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span><span class="sxs-lookup"><span data-stu-id="7b4a7-109">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span></span> <span data-ttu-id="7b4a7-110">An empty response indicates that no faces were detected.</span><span class="sxs-lookup"><span data-stu-id="7b4a7-110">An empty response indicates that no faces were detected.</span></span> <span data-ttu-id="7b4a7-111">An emotion entry contains the following fields:</span><span class="sxs-lookup"><span data-stu-id="7b4a7-111">An emotion entry contains the following fields:</span></span>
* <span data-ttu-id="7b4a7-112">faceRectangle - Rectangle location of face in the image.</span><span class="sxs-lookup"><span data-stu-id="7b4a7-112">faceRectangle - Rectangle location of face in the image.</span></span>
* <span data-ttu-id="7b4a7-113">scores - Emotion scores for each face in the image.</span><span class="sxs-lookup"><span data-stu-id="7b4a7-113">scores - Emotion scores for each face in the image.</span></span> 

```json
application/json 
[
  {
    "faceRectangle": {
      "left": 68,
      "top": 97,
      "width": 64,
      "height": 97
    },
    "scores": {
      "anger": 0.00300731952,
      "contempt": 5.14648448E-08,
      "disgust": 9.180124E-06,
      "fear": 0.0001912825,
      "happiness": 0.9875571,
      "neutral": 0.0009861537,
      "sadness": 1.889955E-05,
      "surprise": 0.008229999
    }
  }
]

