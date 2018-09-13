---
<span data-ttu-id="2ad8c-101">title: Emotion API Ruby quick start | Microsoft Docs description: Get information and code samples to help you quickly get started using the Emotion API with Ruby in Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="2ad8c-101">title: Emotion API Ruby quick start | Microsoft Docs description: Get information and code samples to help you quickly get started using the Emotion API with Ruby in Cognitive Services.</span></span>
<span data-ttu-id="2ad8c-102">services: cognitive-services author: v-royhar manager: yutkuo</span><span class="sxs-lookup"><span data-stu-id="2ad8c-102">services: cognitive-services author: v-royhar manager: yutkuo</span></span>

<span data-ttu-id="2ad8c-103">ms.service: cognitive-services ms.technology: emotion ms.topic: article ms.date:01/30/2017 ms.author: anroth</span><span class="sxs-lookup"><span data-stu-id="2ad8c-103">ms.service: cognitive-services ms.technology: emotion ms.topic: article ms.date:01/30/2017 ms.author: anroth</span></span>
---

# <a name="emotion-api-ruby-quick-start"></a><span data-ttu-id="2ad8c-104">Emotion API Ruby Quick Start</span><span class="sxs-lookup"><span data-stu-id="2ad8c-104">Emotion API Ruby Quick Start</span></span>
<span data-ttu-id="2ad8c-105">This article provides information and code samples to help you quickly get started using the [Emotion API Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) with Ruby to recognize the emotions expressed by one or more people in an image.</span><span class="sxs-lookup"><span data-stu-id="2ad8c-105">This article provides information and code samples to help you quickly get started using the [Emotion API Recognize method](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) with Ruby to recognize the emotions expressed by one or more people in an image.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="2ad8c-106">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="2ad8c-106">Prerequisite</span></span>
* <span data-ttu-id="2ad8c-107">Get your free Subscription Key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span><span class="sxs-lookup"><span data-stu-id="2ad8c-107">Get your free Subscription Key [here](https://www.microsoft.com/cognitive-services/en-us/sign-up)</span></span>

## <a name="recognize-emotions-ruby-example-request"></a><span data-ttu-id="2ad8c-108">Recognize Emotions Ruby Example Request</span><span class="sxs-lookup"><span data-stu-id="2ad8c-108">Recognize Emotions Ruby Example Request</span></span>

```Ruby
require 'net/http'

uri = URI('https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognize')
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

## <a name="recognize-emotions-sample-response"></a><span data-ttu-id="2ad8c-109">Recognize Emotions Sample Response</span><span class="sxs-lookup"><span data-stu-id="2ad8c-109">Recognize Emotions Sample Response</span></span>
<span data-ttu-id="2ad8c-110">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span><span class="sxs-lookup"><span data-stu-id="2ad8c-110">A successful call returns an array of face entries and their associated emotion scores, ranked by face rectangle size in descending order.</span></span> <span data-ttu-id="2ad8c-111">An empty response indicates that no faces were detected.</span><span class="sxs-lookup"><span data-stu-id="2ad8c-111">An empty response indicates that no faces were detected.</span></span> <span data-ttu-id="2ad8c-112">An emotion entry contains the following fields:</span><span class="sxs-lookup"><span data-stu-id="2ad8c-112">An emotion entry contains the following fields:</span></span>
* <span data-ttu-id="2ad8c-113">faceRectangle - Rectangle location of face in the image.</span><span class="sxs-lookup"><span data-stu-id="2ad8c-113">faceRectangle - Rectangle location of face in the image.</span></span>
* <span data-ttu-id="2ad8c-114">scores - Emotion scores for each face in the image.</span><span class="sxs-lookup"><span data-stu-id="2ad8c-114">scores - Emotion scores for each face in the image.</span></span> 

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
