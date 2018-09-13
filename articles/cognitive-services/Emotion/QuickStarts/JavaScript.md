---
title: Emotion API JavaScript quick start | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Emotion API with JavaScript in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 01/30/2017
ms.author: anroth
ms.openlocfilehash: 7b12b1b7066481855151abdc931ce62f94eb3b4e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662695"
---
# <a name="emotion-api-javascript-quick-start"></a><span data-ttu-id="c124c-103">Emotion API JavaScript Quick Start</span><span class="sxs-lookup"><span data-stu-id="c124c-103">Emotion API JavaScript Quick Start</span></span>
<span data-ttu-id="c124c-104">This article provides information and code samples to help you quickly get started using the [Emotion API Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) with JavaScript to recognize the emotions expressed by one or more people in an image.</span><span class="sxs-lookup"><span data-stu-id="c124c-104">This article provides information and code samples to help you quickly get started using the [Emotion API Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) with JavaScript to recognize the emotions expressed by one or more people in an image.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="c124c-105">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="c124c-105">Prerequisite</span></span>
* <span data-ttu-id="c124c-106">Get your free Subscription Key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span><span class="sxs-lookup"><span data-stu-id="c124c-106">Get your free Subscription Key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span></span>

## <a name="recognize-emotions-javascript-example-request"></a><span data-ttu-id="c124c-107">Recognize Emotions JavaScript Example Request</span><span class="sxs-lookup"><span data-stu-id="c124c-107">Recognize Emotions JavaScript Example Request</span></span>

```JavaScript
<!DOCTYPE html>
<html>
<head>
    <title>JSSample</title>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>
</head>
<body>

<script type="text/javascript">
    $(function() {
        var params = {
            // Request parameters
        };
      
        $.ajax({
            url: "https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognize?" + $.param(params),
            beforeSend: function(xhrObj){
                // Request headers
                xhrObj.setRequestHeader("Content-Type","application/json");
                xhrObj.setRequestHeader("Ocp-Apim-Subscription-Key","{subscription key}");
            },
            type: "POST",
            // Request body
            data: "{body}",
        })
        .done(function(data) {
            alert("success");
        })
        .fail(function() {
            alert("error");
        });
    });
</script>
</body>
</html>
```

## <a name="recognize-emotions-sample-response"></a><span data-ttu-id="c124c-108">Recognize Emotions Sample Response</span><span class="sxs-lookup"><span data-stu-id="c124c-108">Recognize Emotions Sample Response</span></span>
<span data-ttu-id="c124c-109">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span><span class="sxs-lookup"><span data-stu-id="c124c-109">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span></span> <span data-ttu-id="c124c-110">An empty response indicates that no faces were detected.</span><span class="sxs-lookup"><span data-stu-id="c124c-110">An empty response indicates that no faces were detected.</span></span> <span data-ttu-id="c124c-111">An emotion entry contains the following fields:</span><span class="sxs-lookup"><span data-stu-id="c124c-111">An emotion entry contains the following fields:</span></span>
* <span data-ttu-id="c124c-112">faceRectangle - Rectangle location of face in the image.</span><span class="sxs-lookup"><span data-stu-id="c124c-112">faceRectangle - Rectangle location of face in the image.</span></span>
* <span data-ttu-id="c124c-113">scores - Emotion scores for each face in the image.</span><span class="sxs-lookup"><span data-stu-id="c124c-113">scores - Emotion scores for each face in the image.</span></span> 

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
