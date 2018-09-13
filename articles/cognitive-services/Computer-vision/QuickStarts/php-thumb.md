---
title: 'Quickstart: Generate a thumbnail - REST, PHP - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you generate a thumbnail from an image using Computer Vision with PHP in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: dc2d5c4e5a1a9a098ad8b70b6b7a280c4dd02299
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969466"
---
# <a name="quickstart-generate-a-thumbnail---rest-php---computer-vision"></a><span data-ttu-id="ddeac-103">Quickstart: Generate a thumbnail - REST, PHP - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="ddeac-103">Quickstart: Generate a thumbnail - REST, PHP - Computer Vision</span></span>

<span data-ttu-id="ddeac-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="ddeac-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddeac-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ddeac-105">Prerequisites</span></span>

<span data-ttu-id="ddeac-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="ddeac-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="get-thumbnail-request"></a><span data-ttu-id="ddeac-107">Get Thumbnail request</span><span class="sxs-lookup"><span data-stu-id="ddeac-107">Get Thumbnail request</span></span>

<span data-ttu-id="ddeac-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span><span class="sxs-lookup"><span data-stu-id="ddeac-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span></span> <span data-ttu-id="ddeac-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="ddeac-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span></span> <span data-ttu-id="ddeac-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span><span class="sxs-lookup"><span data-stu-id="ddeac-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span></span>

<span data-ttu-id="ddeac-111">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="ddeac-111">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="ddeac-112">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="ddeac-112">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="ddeac-113">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="ddeac-113">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="ddeac-114">Change `uriBase` to use the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="ddeac-114">Change `uriBase` to use the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="ddeac-115">Optionally, set `imageUrl` to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="ddeac-115">Optionally, set `imageUrl` to the image you want to analyze.</span></span>
1. <span data-ttu-id="ddeac-116">Save the file with a `.php` extension.</span><span class="sxs-lookup"><span data-stu-id="ddeac-116">Save the file with a `.php` extension.</span></span>
1. <span data-ttu-id="ddeac-117">Open the file in a browser window with PHP support.</span><span class="sxs-lookup"><span data-stu-id="ddeac-117">Open the file in a browser window with PHP support.</span></span>

<span data-ttu-id="ddeac-118">This sample uses the PHP5 [HTTP_Request2](http://pear.php.net/package/HTTP_Request2) package.</span><span class="sxs-lookup"><span data-stu-id="ddeac-118">This sample uses the PHP5 [HTTP_Request2](http://pear.php.net/package/HTTP_Request2) package.</span></span>

```php
<html>
<head>
    <title>Get Thumbnail Sample</title>
</head>
<body>
<?php
// Replace <Subscription Key> with a valid subscription key.
$ocpApimSubscriptionKey = '<Subscription Key>';

// You must use the same location in your REST call as you used to obtain
// your subscription keys. For example, if you obtained your subscription keys
// from westus, replace "westcentralus" in the URL below with "westus".
$uriBase = 'https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/';

$imageUrl =
    'https://upload.wikimedia.org/wikipedia/commons/9/94/Bloodhound_Puppy.jpg';

require_once 'HTTP/Request2.php';

$request = new Http_Request2($uriBase . 'generateThumbnail');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => $ocpApimSubscriptionKey
);
$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'width' => '100',  // Width of the thumbnail.
    'height' => '100', // Height of the thumbnail.
    'smartCropping' => 'true',
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

## <a name="get-thumbnail-response"></a><span data-ttu-id="ddeac-119">Get Thumbnail response</span><span class="sxs-lookup"><span data-stu-id="ddeac-119">Get Thumbnail response</span></span>

<span data-ttu-id="ddeac-120">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="ddeac-120">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="ddeac-121">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="ddeac-121">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddeac-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="ddeac-122">Next steps</span></span>

<span data-ttu-id="ddeac-123">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="ddeac-123">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="ddeac-124">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="ddeac-124">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ddeac-125">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="ddeac-125">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
