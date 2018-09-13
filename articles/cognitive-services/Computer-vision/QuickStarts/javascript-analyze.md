---
title: 'Quickstart: Analyze a remote image - REST, JavaScript - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you analyze an image using Computer Vision with JavaScript in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 9fa9d55aca1c368b734ea74a4eee193ffa0dc4f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869500"
---
# <a name="quickstart-analyze-a-remote-image---rest-javascript---computer-vision"></a><span data-ttu-id="88fc7-103">Quickstart: Analyze a remote image - REST, JavaScript - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="88fc7-103">Quickstart: Analyze a remote image - REST, JavaScript - Computer Vision</span></span>

<span data-ttu-id="88fc7-104">In this quickstart, you analyze an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="88fc7-104">In this quickstart, you analyze an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88fc7-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="88fc7-105">Prerequisites</span></span>

<span data-ttu-id="88fc7-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="88fc7-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="analyze-image-request"></a><span data-ttu-id="88fc7-107">Analyze Image request</span><span class="sxs-lookup"><span data-stu-id="88fc7-107">Analyze Image request</span></span>

<span data-ttu-id="88fc7-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span><span class="sxs-lookup"><span data-stu-id="88fc7-108">With the [Analyze Image method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa), you can extract visual features based on image content.</span></span> <span data-ttu-id="88fc7-109">You can upload an image or specify an image URL and choose which features to return, including:</span><span class="sxs-lookup"><span data-stu-id="88fc7-109">You can upload an image or specify an image URL and choose which features to return, including:</span></span>

* <span data-ttu-id="88fc7-110">A detailed list of tags related to the image content.</span><span class="sxs-lookup"><span data-stu-id="88fc7-110">A detailed list of tags related to the image content.</span></span>
* <span data-ttu-id="88fc7-111">A description of image content in a complete sentence.</span><span class="sxs-lookup"><span data-stu-id="88fc7-111">A description of image content in a complete sentence.</span></span>
* <span data-ttu-id="88fc7-112">The coordinates, gender, and age of any faces contained in the image.</span><span class="sxs-lookup"><span data-stu-id="88fc7-112">The coordinates, gender, and age of any faces contained in the image.</span></span>
* <span data-ttu-id="88fc7-113">The ImageType (clip art or a line drawing).</span><span class="sxs-lookup"><span data-stu-id="88fc7-113">The ImageType (clip art or a line drawing).</span></span>
* <span data-ttu-id="88fc7-114">The dominant color, the accent color, or whether an image is black & white.</span><span class="sxs-lookup"><span data-stu-id="88fc7-114">The dominant color, the accent color, or whether an image is black & white.</span></span>
* <span data-ttu-id="88fc7-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span><span class="sxs-lookup"><span data-stu-id="88fc7-115">The category defined in this [taxonomy](../Category-Taxonomy.md).</span></span>
* <span data-ttu-id="88fc7-116">Does the image contain adult or sexually suggestive content?</span><span class="sxs-lookup"><span data-stu-id="88fc7-116">Does the image contain adult or sexually suggestive content?</span></span>

<span data-ttu-id="88fc7-117">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="88fc7-117">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="88fc7-118">Copy the following and save it to a file such as `analyze.html`.</span><span class="sxs-lookup"><span data-stu-id="88fc7-118">Copy the following and save it to a file such as `analyze.html`.</span></span>
1. <span data-ttu-id="88fc7-119">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="88fc7-119">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="88fc7-120">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="88fc7-120">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="88fc7-121">Drag-and-drop the file into your browser.</span><span class="sxs-lookup"><span data-stu-id="88fc7-121">Drag-and-drop the file into your browser.</span></span>
1. <span data-ttu-id="88fc7-122">Click the `Analyze image` button.</span><span class="sxs-lookup"><span data-stu-id="88fc7-122">Click the `Analyze image` button.</span></span>

<span data-ttu-id="88fc7-123">This sample uses jQuery 1.9.0.</span><span class="sxs-lookup"><span data-stu-id="88fc7-123">This sample uses jQuery 1.9.0.</span></span> <span data-ttu-id="88fc7-124">For a sample that uses JavaScript without jQuery, see [Intelligently generate a thumbnail](javascript-thumb.md).</span><span class="sxs-lookup"><span data-stu-id="88fc7-124">For a sample that uses JavaScript without jQuery, see [Intelligently generate a thumbnail](javascript-thumb.md).</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <title>Analyze Sample</title>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>
</head>
<body>

<script type="text/javascript">
    function processImage() {
        // **********************************************
        // *** Update or verify the following values. ***
        // **********************************************

        // Replace <Subscription Key> with your valid subscription key.
        var subscriptionKey = "<Subscription Key>";

        // You must use the same region in your REST call as you used to get your
        // subscription keys. For example, if you got your subscription keys from
        // westus, replace "westcentralus" in the URI below with "westus".
        //
        // Free trial subscription keys are generated in the westcentralus region.
        // If you use a free trial subscription key, you shouldn't need to change
        // this region.
        var uriBase =
            "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/analyze";

        // Request parameters.
        var params = {
            "visualFeatures": "Categories,Description,Color",
            "details": "",
            "language": "en",
        };

        // Display the image.
        var sourceImageUrl = document.getElementById("inputImage").value;
        document.querySelector("#sourceImage").src = sourceImageUrl;

        // Make the REST API call.
        $.ajax({
            url: uriBase + "?" + $.param(params),

            // Request headers.
            beforeSend: function(xhrObj){
                xhrObj.setRequestHeader("Content-Type","application/json");
                xhrObj.setRequestHeader(
                    "Ocp-Apim-Subscription-Key", subscriptionKey);
            },

            type: "POST",

            // Request body.
            data: '{"url": ' + '"' + sourceImageUrl + '"}',
        })

        .done(function(data) {
            // Show formatted JSON on webpage.
            $("#responseTextArea").val(JSON.stringify(data, null, 2));
        })

        .fail(function(jqXHR, textStatus, errorThrown) {
            // Display error message.
            var errorString = (errorThrown === "") ? "Error. " :
                errorThrown + " (" + jqXHR.status + "): ";
            errorString += (jqXHR.responseText === "") ? "" :
                jQuery.parseJSON(jqXHR.responseText).message;
            alert(errorString);
        });
    };
</script>

<h1>Analyze image:</h1>
Enter the URL to an image, then click the <strong>Analyze image</strong> button.
<br><br>
Image to analyze:
<input type="text" name="inputImage" id="inputImage"
    value="http://upload.wikimedia.org/wikipedia/commons/3/3c/Shaki_waterfall.jpg" />
<button onclick="processImage()">Analyze image</button>
<br><br>
<div id="wrapper" style="width:1020px; display:table;">
    <div id="jsonOutput" style="width:600px; display:table-cell;">
        Response:
        <br><br>
        <textarea id="responseTextArea" class="UIInput"
                  style="width:580px; height:400px;"></textarea>
    </div>
    <div id="imageDiv" style="width:420px; display:table-cell;">
        Source image:
        <br><br>
        <img id="sourceImage" width="400" />
    </div>
</div>
</body>
</html>
```

## <a name="analyze-image-response"></a><span data-ttu-id="88fc7-125">Analyze Image response</span><span class="sxs-lookup"><span data-stu-id="88fc7-125">Analyze Image response</span></span>

<span data-ttu-id="88fc7-126">A successful response is returned in JSON, for example:</span><span class="sxs-lookup"><span data-stu-id="88fc7-126">A successful response is returned in JSON, for example:</span></span>

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
  "color": {
    "dominantColorForeground": "Grey",
    "dominantColorBackground": "Green",
    "dominantColors": [
      "Grey",
      "Green"
    ],
    "accentColor": "4D5E2F",
    "isBwImg": false
  },
  "requestId": "73ef10ce-a4ea-43c6-aee7-70325777e4b3",
  "metadata": {
    "height": 959,
    "width": 1280,
    "format": "Jpeg"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="88fc7-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="88fc7-127">Next steps</span></span>

<span data-ttu-id="88fc7-128">Explore a JavaScript application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="88fc7-128">Explore a JavaScript application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="88fc7-129">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="88fc7-129">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="88fc7-130">Computer Vision API JavaScript Tutorial</span><span class="sxs-lookup"><span data-stu-id="88fc7-130">Computer Vision API JavaScript Tutorial</span></span>](../Tutorials/javascript-tutorial.md)
