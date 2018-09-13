---
title: 'Quickstart: Extract printed text (OCR) - REST, PHP - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you extract printed text from an image using Computer Vision with PHP in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 83954b5463213d0360e0466af89204c205e43ec2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870325"
---
# <a name="quickstart-extract-printed-text-ocr---rest-php---computer-vision"></a><span data-ttu-id="8c20a-103">Quickstart: Extract printed text (OCR) - REST, PHP - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="8c20a-103">Quickstart: Extract printed text (OCR) - REST, PHP - Computer Vision</span></span>

<span data-ttu-id="8c20a-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="8c20a-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c20a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8c20a-105">Prerequisites</span></span>

<span data-ttu-id="8c20a-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="8c20a-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="ocr-request"></a><span data-ttu-id="8c20a-107">OCR request</span><span class="sxs-lookup"><span data-stu-id="8c20a-107">OCR request</span></span>

<span data-ttu-id="8c20a-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="8c20a-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

<span data-ttu-id="8c20a-109">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="8c20a-109">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="8c20a-110">Copy the following code into an editor.</span><span class="sxs-lookup"><span data-stu-id="8c20a-110">Copy the following code into an editor.</span></span>
1. <span data-ttu-id="8c20a-111">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="8c20a-111">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="8c20a-112">Change `uriBase` to use the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="8c20a-112">Change `uriBase` to use the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="8c20a-113">Optionally, set `imageUrl` to the image you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="8c20a-113">Optionally, set `imageUrl` to the image you want to analyze.</span></span>
1. <span data-ttu-id="8c20a-114">Save the file with a `.php` extension.</span><span class="sxs-lookup"><span data-stu-id="8c20a-114">Save the file with a `.php` extension.</span></span>
1. <span data-ttu-id="8c20a-115">Open the file in a browser window with PHP support.</span><span class="sxs-lookup"><span data-stu-id="8c20a-115">Open the file in a browser window with PHP support.</span></span>

<span data-ttu-id="8c20a-116">This sample uses the PHP5 [HTTP_Request2](http://pear.php.net/package/HTTP_Request2) package.</span><span class="sxs-lookup"><span data-stu-id="8c20a-116">This sample uses the PHP5 [HTTP_Request2](http://pear.php.net/package/HTTP_Request2) package.</span></span>

```php
<?php
<html>
<head>
    <title>OCR Sample</title>
</head>
<body>
<?php
// Replace <Subscription Key> with a valid subscription key.
$ocpApimSubscriptionKey = '<Subscription Key>';

// You must use the same location in your REST call as you used to obtain
// your subscription keys. For example, if you obtained your subscription keys
// from westus, replace "westcentralus" in the URL below with "westus".
$uriBase = 'https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/';

$imageUrl = 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/' .
    'Atomist_quote_from_Democritus.png/338px-Atomist_quote_from_Democritus.png';

require_once 'HTTP/Request2.php';

$request = new Http_Request2($uriBase . 'ocr');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',
    'Ocp-Apim-Subscription-Key' => $ocpApimSubscriptionKey
);
$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'language' => 'unk',
    'detectOrientation' => 'true'
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

## <a name="ocr-response"></a><span data-ttu-id="8c20a-117">OCR response</span><span class="sxs-lookup"><span data-stu-id="8c20a-117">OCR response</span></span>

<span data-ttu-id="8c20a-118">Upon success, the OCR results returned include text, bounding box for regions, lines, and words, for example:</span><span class="sxs-lookup"><span data-stu-id="8c20a-118">Upon success, the OCR results returned include text, bounding box for regions, lines, and words, for example:</span></span>

```json
{
    "language": "en",
    "orientation": "Up",
    "textAngle": 0,
    "regions": [
        {
            "boundingBox": "21,16,304,451",
            "lines": [
                {
                    "boundingBox": "28,16,288,41",
                    "words": [
                        {
                            "boundingBox": "28,16,288,41",
                            "text": "NOTHING"
                        }
                    ]
                },
                {
                    "boundingBox": "27,66,283,52",
                    "words": [
                        {
                            "boundingBox": "27,66,283,52",
                            "text": "EXISTS"
                        }
                    ]
                },
                {
                    "boundingBox": "27,128,292,49",
                    "words": [
                        {
                            "boundingBox": "27,128,292,49",
                            "text": "EXCEPT"
                        }
                    ]
                },
                {
                    "boundingBox": "24,188,292,54",
                    "words": [
                        {
                            "boundingBox": "24,188,292,54",
                            "text": "ATOMS"
                        }
                    ]
                },
                {
                    "boundingBox": "22,253,297,32",
                    "words": [
                        {
                            "boundingBox": "22,253,105,32",
                            "text": "AND"
                        },
                        {
                            "boundingBox": "144,253,175,32",
                            "text": "EMPTY"
                        }
                    ]
                },
                {
                    "boundingBox": "21,298,304,60",
                    "words": [
                        {
                            "boundingBox": "21,298,304,60",
                            "text": "SPACE."
                        }
                    ]
                },
                {
                    "boundingBox": "26,387,294,37",
                    "words": [
                        {
                            "boundingBox": "26,387,210,37",
                            "text": "Everything"
                        },
                        {
                            "boundingBox": "249,389,71,27",
                            "text": "else"
                        }
                    ]
                },
                {
                    "boundingBox": "127,431,198,36",
                    "words": [
                        {
                            "boundingBox": "127,431,31,29",
                            "text": "is"
                        },
                        {
                            "boundingBox": "172,431,153,36",
                            "text": "opinion."
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="8c20a-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c20a-119">Next steps</span></span>

<span data-ttu-id="8c20a-120">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span><span class="sxs-lookup"><span data-stu-id="8c20a-120">Explore the Computer Vision APIs used to analyze an image, detect celebrities and landmarks, create a thumbnail, and extract printed and handwritten text.</span></span> <span data-ttu-id="8c20a-121">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="8c20a-121">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8c20a-122">Explore Computer Vision APIs</span><span class="sxs-lookup"><span data-stu-id="8c20a-122">Explore Computer Vision APIs</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
