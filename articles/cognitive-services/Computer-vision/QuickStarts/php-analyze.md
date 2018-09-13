---
title: 'Quickstart: Analyze a remote image - REST, PHP - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze an image using Computer Vision with PHP in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 4865943fb5b903695f9d79b13624cbe8a94b8cd7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871095"
---
# <a name="quickstart-analyze-a-remote-image---rest-php---computer-vision"></a><span data-ttu-id="600f7-103">Quickstart: Analyze a remote image - REST, PHP - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="600f7-103">Quickstart: Analyze a remote image - REST, PHP - Computer Vision</span></span>

<span data-ttu-id="600f7-104">In this quickstart, you analyze an image to extract visual features using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="600f7-104">In this quickstart, you analyze an image to extract visual features using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="600f7-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="600f7-105">Prerequisites</span></span>

<span data-ttu-id="600f7-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="600f7-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="analyze-image-request"></a><span data-ttu-id="600f7-107">Analyze Image request</span><span class="sxs-lookup"><span data-stu-id="600f7-107">Analyze Image request</span></span>

<span data-ttu-id="600f7-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="600f7-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="600f7-109">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="600f7-109">You can upload an image or specify an image URL and choose which features to return, including:</span></span>

* <span data-ttu-id="600f7-110">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="600f7-110">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="600f7-111">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="600f7-111">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="600f7-112">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="600f7-112">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="600f7-113">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="600f7-113">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="600f7-114">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="600f7-114">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="600f7-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="600f7-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span>
* <span data-ttu-id="600f7-116">Does the image contain adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="600f7-116">Does the image contain adult or sexually suggestive content?</span></span>

<span data-ttu-id="600f7-117">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="600f7-117">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="600f7-118">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="600f7-118">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="600f7-119">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="600f7-119">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="600f7-120">Change `uriBase` to use the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="600f7-120">Change `uriBase` to use the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="600f7-121">Optionally, set `imageUrl` to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="600f7-121">Optionally, set `imageUrl` to the image you want to analyze.</span></span>
1. <span data-ttu-id="600f7-122">Optionally, change the response language (`'language' => 'en'`).</span><span class="sxs-lookup"><span data-stu-id="600f7-122">Optionally, change the response language (`'language' => 'en'`).</span></span>
1. <span data-ttu-id="600f7-123">Save the file with a `.php` extension.</span><span class="sxs-lookup"><span data-stu-id="600f7-123">Save the file with a `.php` extension.</span></span>
1. <span data-ttu-id="600f7-124">Open the file in a browser window with PHP support.</span><span class="sxs-lookup"><span data-stu-id="600f7-124">Open the file in a browser window with PHP support.</span></span>

<span data-ttu-id="600f7-125">This sample uses the PHP5 [HTTP_Request2](http://pear.php.net/package/HTTP_Request2) package.</span><span class="sxs-lookup"><span data-stu-id="600f7-125">This sample uses the PHP5 [HTTP_Request2](http://pear.php.net/package/HTTP_Request2) package.</span></span>

```php
<html>
<head>
    <title>Analyze Image Sample</title>
</head>
<body>
<?php
// Replace <Subscription Key> with a valid subscription key.
$ocpApimSubscriptionKey = '<Subscription Key>';

// You must use the same location in your REST call as you used to obtain
// your subscription keys. For example, if you obtained your subscription keys
// from westus, replace "westcentralus" in the URL below with "westus".
$uriBase = 'https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/';

$imageUrl = 'http://upload.wikimedia.org/wikipedia/commons/3/3c/Shaki_waterfall.jpg';

require_once 'HTTP/Request2.php';

$request = new Http_Request2($uriBase . '/analyze');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => $ocpApimSubscriptionKey
);
$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'visualFeatures' => 'Categories,Description',
    'details' => '',
    'language' => 'en'
);
$url->setQueryVariables($parameters);

$request->setMethod(HTTP_Request2::METHOD_POST);

// Request body parameters
$body = json_encode(array('url' => $imageUrl));

// Request body
$request->setBody($body);

try
{
    $response = $request->send();
    echo "<pre>" .
        json_encode(json_decode($response->getBody()), JSON_PRETTY_PRINT) . "</pre>";
}
catch (HttpException $ex)
{
    echo "<pre>" . $ex . "</pre>";
}
?>
</body>
</html>
```

## <a name="analyze-image-response"></a><span data-ttu-id="600f7-126">Analyze Image response</span><span class="sxs-lookup"><span data-stu-id="600f7-126">Analyze Image response</span></span>

<span data-ttu-id="600f7-127">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="600f7-127">A successful response is returned in JSON, for example:</span></span>

```json
{
  "categories": [
    {
      "name": "outdoor_water",
      "score": 0.9921875,
      "detail": {
        "landmarks": []
      }
    }
  ],
  "description": {
    "tags": [
      "nature",
      "water",
      "waterfall",
      "outdoor",
      "rock",
      "mountain",
      "rocky",
      "grass",
      "hill",
      "covered",
      "hillside",
      "standing",
      "side",
      "group",
      "walking",
      "white",
      "man",
      "large",
      "snow",
      "grazing",
      "forest",
      "slope",
      "herd",
      "river",
      "giraffe",
      "field"
    ],
    "captions": [
      {
        "text": "a large waterfall over a rocky cliff",
        "confidence": 0.916458423253597
      }
    ]
  },
  "requestId": "ebf5a1bc-3ba2-4c56-99b4-bbd20ba28705",
  "metadata": {
    "height": 959,
    "width": 1280,
    "format": "Jpeg"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="600f7-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="600f7-128">Next steps</span></span>

<span data-ttu-id="600f7-129">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="600f7-129">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="600f7-130">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="600f7-130">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="600f7-131">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="600f7-131">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
