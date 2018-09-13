---
title: 'Quickstart: Extract printed text (OCR) - REST, Ruby - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you extract printed text from an image using Computer Vision with Ruby in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: fc3ca062ed2fb77d09fa8d3c87f4b7278c7b19cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857878"
---
# <a name="quickstart-extract-printed-text-ocr---rest-ruby---computer-vision"></a><span data-ttu-id="9813e-103">Quickstart: Extract printed text (OCR) - REST, Ruby - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="9813e-103">Quickstart: Extract printed text (OCR) - REST, Ruby - Computer Vision</span></span>

<span data-ttu-id="9813e-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="9813e-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9813e-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9813e-105">Prerequisites</span></span>

<span data-ttu-id="9813e-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="9813e-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="ocr-request"></a><span data-ttu-id="9813e-107">OCR request</span><span class="sxs-lookup"><span data-stu-id="9813e-107">OCR request</span></span>

<span data-ttu-id="9813e-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="9813e-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

<span data-ttu-id="9813e-109">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="9813e-109">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="9813e-110">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="9813e-110">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="9813e-111">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="9813e-111">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="9813e-112">Change the `uri` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="9813e-112">Change the `uri` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="9813e-113">Optionally, change the image (`{\"url\":\"...`) to analyze.</span><span class="sxs-lookup"><span data-stu-id="9813e-113">Optionally, change the image (`{\"url\":\"...`) to analyze.</span></span>
1. <span data-ttu-id="9813e-114">Save the file with an `.rb` extension.</span><span class="sxs-lookup"><span data-stu-id="9813e-114">Save the file with an `.rb` extension.</span></span>
1. <span data-ttu-id="9813e-115">Open the Ruby Command Prompt and run the file, for example: `ruby myfile.rb`.</span><span class="sxs-lookup"><span data-stu-id="9813e-115">Open the Ruby Command Prompt and run the file, for example: `ruby myfile.rb`.</span></span>

```ruby
require 'net/http'

# You must use the same location in your REST call as you used to get your
# subscription keys. For example, if you got your subscription keys from westus,
# replace "westcentralus" in the URL below with "westus".
uri = URI('https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/ocr')
uri.query = URI.encode_www_form({
    # Request parameters
    'language' => 'unk',
    'detectOrientation' => 'true'
})

request = Net::HTTP::Post.new(uri.request_uri)

# Request headers
# Replace <Subscription Key> with your valid subscription key.
request['Ocp-Apim-Subscription-Key'] = '<Subscription Key>'
request['Content-Type'] = 'application/json'

request.body =
    "{\"url\": \"https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/" +
    "Atomist_quote_from_Democritus.png/338px-Atomist_quote_from_Democritus.png\"}"

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request(request)
end

puts response.body
```

## <a name="ocr-response"></a><span data-ttu-id="9813e-116">OCR response</span><span class="sxs-lookup"><span data-stu-id="9813e-116">OCR response</span></span>

<span data-ttu-id="9813e-117">Upon success, the OCR results returned include text, bounding box for regions, lines, and words, for example:</span><span class="sxs-lookup"><span data-stu-id="9813e-117">Upon success, the OCR results returned include text, bounding box for regions, lines, and words, for example:</span></span>

```json
{
  "language": "en",
  "textAngle": -2.0000000000000338,
  "orientation": "Up",
  "regions": [
    {
      "boundingBox": "462,379,497,258",
      "lines": [
        {
          "boundingBox": "462,379,497,74",
          "words": [
            {
              "boundingBox": "462,379,41,73",
              "text": "A"
            },
            {
              "boundingBox": "523,379,153,73",
              "text": "GOAL"
            },
            {
              "boundingBox": "694,379,265,74",
              "text": "WITHOUT"
            }
          ]
        },
        {
          "boundingBox": "565,471,289,74",
          "words": [
            {
              "boundingBox": "565,471,41,73",
              "text": "A"
            },
            {
              "boundingBox": "626,471,150,73",
              "text": "PLAN"
            },
            {
              "boundingBox": "801,472,53,73",
              "text": "IS"
            }
          ]
        },
        {
          "boundingBox": "519,563,375,74",
          "words": [
            {
              "boundingBox": "519,563,149,74",
              "text": "JUST"
            },
            {
              "boundingBox": "683,564,41,72",
              "text": "A"
            },
            {
              "boundingBox": "741,564,153,73",
              "text": "WISH"
            }
          ]
        }
      ]
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="9813e-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="9813e-118">Next steps</span></span>

<span data-ttu-id="9813e-119">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="9813e-119">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="9813e-120">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="9813e-120">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9813e-121">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="9813e-121">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
