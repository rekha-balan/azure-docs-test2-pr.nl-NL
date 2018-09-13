---
title: 'Quickstart: Generate a thumbnail - REST, Ruby - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you generate a thumbnail from an image using Computer Vision with Ruby in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 531bab4b6450d5da22fb390008bc55f01a686d07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969170"
---
# <a name="quickstart-generate-a-thumbnail---rest-ruby---computer-vision"></a><span data-ttu-id="47248-103">Quickstart: Generate a thumbnail - REST, Ruby - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="47248-103">Quickstart: Generate a thumbnail - REST, Ruby - Computer Vision</span></span>

<span data-ttu-id="47248-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="47248-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47248-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="47248-105">Prerequisites</span></span>

<span data-ttu-id="47248-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="47248-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="get-thumbnail-request"></a><span data-ttu-id="47248-107">Get Thumbnail request</span><span class="sxs-lookup"><span data-stu-id="47248-107">Get Thumbnail request</span></span>

<span data-ttu-id="47248-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span><span class="sxs-lookup"><span data-stu-id="47248-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span></span> <span data-ttu-id="47248-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="47248-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span></span> <span data-ttu-id="47248-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span><span class="sxs-lookup"><span data-stu-id="47248-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span></span>

<span data-ttu-id="47248-111">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="47248-111">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="47248-112">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="47248-112">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="47248-113">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="47248-113">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="47248-114">Change the `uri` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="47248-114">Change the `uri` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="47248-115">Optionally, change the image (`{\"url\":\"...`) to analyze.</span><span class="sxs-lookup"><span data-stu-id="47248-115">Optionally, change the image (`{\"url\":\"...`) to analyze.</span></span>
1. <span data-ttu-id="47248-116">Save the file with an `.rb` extension.</span><span class="sxs-lookup"><span data-stu-id="47248-116">Save the file with an `.rb` extension.</span></span>
1. <span data-ttu-id="47248-117">Open the Ruby Command Prompt and run the file, for example: `ruby myfile.rb`.</span><span class="sxs-lookup"><span data-stu-id="47248-117">Open the Ruby Command Prompt and run the file, for example: `ruby myfile.rb`.</span></span>

```ruby
require 'net/http'

# You must use the same location in your REST call as you used to get your
# subscription keys. For example, if you got your subscription keys from westus,
# replace "westcentralus" in the URL below with "westus".
uri = URI('https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail')
uri.query = URI.encode_www_form({
    # Request parameters
    'width' => '100',
    'height' => '100',
    'smartCropping' => 'true'
})

request = Net::HTTP::Post.new(uri.request_uri)

# Request headers
# Replace <Subscription Key> with your valid subscription key.
request['Ocp-Apim-Subscription-Key'] = '<Subscription Key>'
request['Content-Type'] = 'application/json'

request.body =
    "{\"url\": \"https://upload.wikimedia.org/wikipedia/commons/thumb/5/56/" +
    "Shorkie_Poo_Puppy.jpg/1280px-Shorkie_Poo_Puppy.jpg\"}"

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request(request)
end

#puts response.body
```

## <a name="get-thumbnail-response"></a><span data-ttu-id="47248-118">Get Thumbnail response</span><span class="sxs-lookup"><span data-stu-id="47248-118">Get Thumbnail response</span></span>

<span data-ttu-id="47248-119">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="47248-119">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="47248-120">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="47248-120">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47248-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="47248-121">Next steps</span></span>

<span data-ttu-id="47248-122">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="47248-122">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="47248-123">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="47248-123">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47248-124">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="47248-124">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
