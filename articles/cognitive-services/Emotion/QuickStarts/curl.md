---
title: Emotion API cURL quick start | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Emotion API with cURL in Cognitive Services.
services: cognitive-services
author: anrothMSFT
manager: corncar
ms.service: cognitive-services
ms.component: emotion-api
ms.topic: article
ms.date: 05/23/2017
ms.author: anroth
ms.openlocfilehash: a7ca2cac718797462bb4dc889b3f1361b252435e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825461"
---
# <a name="emotion-api-curl-quick-start"></a><span data-ttu-id="bdaed-103">Emotion API cURL Quick Start</span><span class="sxs-lookup"><span data-stu-id="bdaed-103">Emotion API cURL Quick Start</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bdaed-104">Video API Preview will end on October 30th, 2017.</span><span class="sxs-lookup"><span data-stu-id="bdaed-104">Video API Preview will end on October 30th, 2017.</span></span> <span data-ttu-id="bdaed-105">Try the new [Video Indexer API Preview](https://azure.microsoft.com/services/cognitive-services/video-indexer/) to easily extract insights from videos and to enhance content discovery experiences, such as search results, by detecting spoken words, faces, characters, and emotions.</span><span class="sxs-lookup"><span data-stu-id="bdaed-105">Try the new [Video Indexer API Preview](https://azure.microsoft.com/services/cognitive-services/video-indexer/) to easily extract insights from videos and to enhance content discovery experiences, such as search results, by detecting spoken words, faces, characters, and emotions.</span></span> <span data-ttu-id="bdaed-106">[Learn more](https://docs.microsoft.com/azure/cognitive-services/video-indexer/video-indexer-overview).</span><span class="sxs-lookup"><span data-stu-id="bdaed-106">[Learn more](https://docs.microsoft.com/azure/cognitive-services/video-indexer/video-indexer-overview).</span></span>

<span data-ttu-id="bdaed-107">This article provides information and code samples to help you quickly get started using the [Emotion API Recognize method](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) with cURL to recognize the emotions expressed by one or more people in an image.</span><span class="sxs-lookup"><span data-stu-id="bdaed-107">This article provides information and code samples to help you quickly get started using the [Emotion API Recognize method](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) with cURL to recognize the emotions expressed by one or more people in an image.</span></span> 

## <a name="prerequisite"></a><span data-ttu-id="bdaed-108">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="bdaed-108">Prerequisite</span></span>
* <span data-ttu-id="bdaed-109">Get your free Subscription Key [here](https://azure.microsoft.com/try/cognitive-services/)</span><span class="sxs-lookup"><span data-stu-id="bdaed-109">Get your free Subscription Key [here](https://azure.microsoft.com/try/cognitive-services/)</span></span>

## <a name="recognize-emotions-curl-example-request"></a><span data-ttu-id="bdaed-110">Recognize Emotions cURL Example Request</span><span class="sxs-lookup"><span data-stu-id="bdaed-110">Recognize Emotions cURL Example Request</span></span>

> [!NOTE]
> <span data-ttu-id="bdaed-111">You must use the same location in your REST call as you used to obtain your subscription keys.</span><span class="sxs-lookup"><span data-stu-id="bdaed-111">You must use the same location in your REST call as you used to obtain your subscription keys.</span></span> <span data-ttu-id="bdaed-112">For example, if you obtained your subscription keys from westcentralus, replace "westus" in the URL below with "westcentralus".</span><span class="sxs-lookup"><span data-stu-id="bdaed-112">For example, if you obtained your subscription keys from westcentralus, replace "westus" in the URL below with "westcentralus".</span></span>

```json
@ECHO OFF

curl -v -X POST "https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognize"
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {subscription key}"

--data-ascii "{body}" 
```

## <a name="recognize-emotions-sample-response"></a><span data-ttu-id="bdaed-113">Recognize Emotions Sample Response</span><span class="sxs-lookup"><span data-stu-id="bdaed-113">Recognize Emotions Sample Response</span></span>
<span data-ttu-id="bdaed-114">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span><span class="sxs-lookup"><span data-stu-id="bdaed-114">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span></span> <span data-ttu-id="bdaed-115">An empty response indicates that no faces were detected.</span><span class="sxs-lookup"><span data-stu-id="bdaed-115">An empty response indicates that no faces were detected.</span></span> <span data-ttu-id="bdaed-116">An emotion entry contains the following fields:</span><span class="sxs-lookup"><span data-stu-id="bdaed-116">An emotion entry contains the following fields:</span></span>
* <span data-ttu-id="bdaed-117">faceRectangle - Rectangle location of face in the image.</span><span class="sxs-lookup"><span data-stu-id="bdaed-117">faceRectangle - Rectangle location of face in the image.</span></span>
* <span data-ttu-id="bdaed-118">scores - Emotion scores for each face in the image.</span><span class="sxs-lookup"><span data-stu-id="bdaed-118">scores - Emotion scores for each face in the image.</span></span> 

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

