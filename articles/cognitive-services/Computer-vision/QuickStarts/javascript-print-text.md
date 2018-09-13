---
title: 'Quickstart: Extract printed text (OCR) - REST, JavaScript - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you extract printed text from an image using Computer Vision with JavaScript in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 877f206d325127ba625984bfb1821f15e1280e5e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968319"
---
# <a name="quickstart-extract-printed-text-ocr---rest-javascript---computer-vision"></a><span data-ttu-id="11cd0-103">Quickstart: Extract printed text (OCR) - REST, JavaScript - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="11cd0-103">Quickstart: Extract printed text (OCR) - REST, JavaScript - Computer Vision</span></span>

<span data-ttu-id="11cd0-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="11cd0-104">In this quickstart, you extract printed text, also known as optical character recognition (OCR), from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11cd0-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="11cd0-105">Prerequisites</span></span>

<span data-ttu-id="11cd0-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="11cd0-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="ocr-request"></a><span data-ttu-id="11cd0-107">OCR request</span><span class="sxs-lookup"><span data-stu-id="11cd0-107">OCR request</span></span>

<span data-ttu-id="11cd0-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span><span class="sxs-lookup"><span data-stu-id="11cd0-108">With the [OCR method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc), you can detect printed text in an image and extract recognized characters into a machine-usable character stream.</span></span>

<span data-ttu-id="11cd0-109">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="11cd0-109">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="11cd0-110">Copy the following and save it to a file such as `ocr.html`.</span><span class="sxs-lookup"><span data-stu-id="11cd0-110">Copy the following and save it to a file such as `ocr.html`.</span></span>
1. <span data-ttu-id="11cd0-111">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="11cd0-111">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="11cd0-112">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="11cd0-112">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="11cd0-113">Drag-and-drop the file into your browser.</span><span class="sxs-lookup"><span data-stu-id="11cd0-113">Drag-and-drop the file into your browser.</span></span>
1. <span data-ttu-id="11cd0-114">Click the `Read image` button.</span><span class="sxs-lookup"><span data-stu-id="11cd0-114">Click the `Read image` button.</span></span>

<span data-ttu-id="11cd0-115">This sample uses jQuery 1.9.0.</span><span class="sxs-lookup"><span data-stu-id="11cd0-115">This sample uses jQuery 1.9.0.</span></span> <span data-ttu-id="11cd0-116">For a sample that uses JavaScript without jQuery, see [Intelligently generate a thumbnail](javascript-thumb.md).</span><span class="sxs-lookup"><span data-stu-id="11cd0-116">For a sample that uses JavaScript without jQuery, see [Intelligently generate a thumbnail](javascript-thumb.md).</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <title>OCR Sample</title>
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
            "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/ocr";

        // Request parameters.
        var params = {
            "language": "unk",
            "detectOrientation": "true",
        };

        // Display the image.
        var sourceImageUrl = document.getElementById("inputImage").value;
        document.querySelector("#sourceImage").src = sourceImageUrl;

        // Perform the REST API call.
        $.ajax({
            url: uriBase + "?" + $.param(params),

            // Request headers.
            beforeSend: function(jqXHR){
                jqXHR.setRequestHeader("Content-Type","application/json");
                jqXHR.setRequestHeader("Ocp-Apim-Subscription-Key", subscriptionKey);
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
            var errorString = (errorThrown === "") ?
                "Error. " : errorThrown + " (" + jqXHR.status + "): ";
            errorString += (jqXHR.responseText === "") ? "" :
                (jQuery.parseJSON(jqXHR.responseText).message) ?
                    jQuery.parseJSON(jqXHR.responseText).message :
                    jQuery.parseJSON(jqXHR.responseText).error.message;
            alert(errorString);
        });
    };
</script>

<h1>Optical Character Recognition (OCR):</h1>
Enter the URL to an image of printed text, then
click the <strong>Read image</strong> button.
<br><br>
Image to read:
<input type="text" name="inputImage" id="inputImage" 
    value="https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/Atomist_quote_from_Democritus.png/338px-Atomist_quote_from_Democritus.png" />
<button onclick="processImage()">Read image</button>
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

## <a name="ocr-response"></a><span data-ttu-id="11cd0-117">OCR response</span><span class="sxs-lookup"><span data-stu-id="11cd0-117">OCR response</span></span>

<span data-ttu-id="11cd0-118">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="11cd0-118">A successful response is returned in JSON.</span></span> <span data-ttu-id="11cd0-119">The OCR results returned include text, bounding box for regions, lines, and words.</span><span class="sxs-lookup"><span data-stu-id="11cd0-119">The OCR results returned include text, bounding box for regions, lines, and words.</span></span>

<span data-ttu-id="11cd0-120">The program produces output similar to the following JSON:</span><span class="sxs-lookup"><span data-stu-id="11cd0-120">The program produces output similar to the following JSON:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="11cd0-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="11cd0-121">Next steps</span></span>

<span data-ttu-id="11cd0-122">Explore a JavaScript application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="11cd0-122">Explore a JavaScript application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="11cd0-123">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="11cd0-123">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="11cd0-124">Computer Vision API JavaScript Tutorial</span><span class="sxs-lookup"><span data-stu-id="11cd0-124">Computer Vision API JavaScript Tutorial</span></span>](../Tutorials/javascript-tutorial.md)
