---
title: 'Quickstart: Use a domain model - REST, PHP - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you use a domain model to identify landmarks in  an image using Computer Vision with PHP in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 5c13daa5802852916e9ae4d1e694ddcef888bbb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855742"
---
# <a name="quickstart-use-a-domain-model---rest-php---computer-vision"></a><span data-ttu-id="317a0-103">Quickstart: Use a domain model - REST, PHP - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="317a0-103">Quickstart: Use a domain model - REST, PHP - Computer Vision</span></span>

<span data-ttu-id="317a0-104">In this quickstart, you use a domain model to identify landmarks or celebrities in an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="317a0-104">In this quickstart, you use a domain model to identify landmarks or celebrities in an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="317a0-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="317a0-105">Prerequisites</span></span>

<span data-ttu-id="317a0-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="317a0-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="recognize-landmark-request"></a><span data-ttu-id="317a0-107">Recognize Landmark request</span><span class="sxs-lookup"><span data-stu-id="317a0-107">Recognize Landmark request</span></span>

<span data-ttu-id="317a0-108">With the [Recognize Domain Specific Content method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e200), you can identify a specific set of objects in an image.</span><span class="sxs-lookup"><span data-stu-id="317a0-108">With the [Recognize Domain Specific Content method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e200), you can identify a specific set of objects in an image.</span></span> <span data-ttu-id="317a0-109">The two domain-specific models that are currently available are _celebrities_ and _landmarks_.</span><span class="sxs-lookup"><span data-stu-id="317a0-109">The two domain-specific models that are currently available are _celebrities_ and _landmarks_.</span></span>

<span data-ttu-id="317a0-110">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="317a0-110">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="317a0-111">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="317a0-111">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="317a0-112">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="317a0-112">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="317a0-113">Change `uriBase` to use the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="317a0-113">Change `uriBase` to use the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="317a0-114">Optionally, set `imageUrl` to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="317a0-114">Optionally, set `imageUrl` to the image you want to analyze.</span></span>
1. <span data-ttu-id="317a0-115">Optionally, set `domain` to `celebrities` to use the Celebrities model.</span><span class="sxs-lookup"><span data-stu-id="317a0-115">Optionally, set `domain` to `celebrities` to use the Celebrities model.</span></span>
1. <span data-ttu-id="317a0-116">Save the file with a `.php` extension.</span><span class="sxs-lookup"><span data-stu-id="317a0-116">Save the file with a `.php` extension.</span></span>
1. <span data-ttu-id="317a0-117">Open the file in a browser window with PHP support.</span><span class="sxs-lookup"><span data-stu-id="317a0-117">Open the file in a browser window with PHP support.</span></span>

<span data-ttu-id="317a0-118">The following example identifies a landmark in an image.</span><span class="sxs-lookup"><span data-stu-id="317a0-118">The following example identifies a landmark in an image.</span></span>

<span data-ttu-id="317a0-119">This sample uses the PHP5 [HTTP_Request2](http://pear.php.net/package/HTTP_Request2) package.</span><span class="sxs-lookup"><span data-stu-id="317a0-119">This sample uses the PHP5 [HTTP_Request2](http://pear.php.net/package/HTTP_Request2) package.</span></span>

```php
<html>
<head>
    <title>Analyze Domain Model Sample</title>
</head>
<body>
<?php
// Replace <Subscription Key> with a valid subscription key.
$ocpApimSubscriptionKey = '<Subscription Key>';

// You must use the same location in your REST call as you used to obtain
// your subscription keys. For example, if you obtained your subscription keys
// from westus, replace "westcentralus" in the URL below with "westus".
$uriBase = 'https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/';

// Change 'landmarks' to 'celebrities' to use the Celebrities model.
$domain = 'landmarks';

$imageUrl =
    'https://upload.wikimedia.org/wikipedia/commons/2/23/Space_Needle_2011-07-04.jpg';

require_once 'HTTP/Request2.php';

$request = new Http_Request2($uriBase . 'models/' . $domain . '/analyze');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => $ocpApimSubscriptionKey
);
$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'model' => $domain
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

## <a name="recognize-landmark-response"></a><span data-ttu-id="317a0-120">Recognize Landmark response</span><span class="sxs-lookup"><span data-stu-id="317a0-120">Recognize Landmark response</span></span>

<span data-ttu-id="317a0-121">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="317a0-121">A successful response is returned in JSON, for example:</span></span>

```json
{
    "result": {
        "landmarks": [
            {
                "name": "Space Needle",
                "confidence": 0.9998177886009216
            }
        ]
    },
    "requestId": "4d26587b-b2b9-408d-a70c-1f8121d84b0d",
    "metadata": {
        "height": 4132,
        "width": 2096,
        "format": "Jpeg"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="317a0-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="317a0-122">Next steps</span></span>

<span data-ttu-id="317a0-123">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="317a0-123">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="317a0-124">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="317a0-124">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="317a0-125">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="317a0-125">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
