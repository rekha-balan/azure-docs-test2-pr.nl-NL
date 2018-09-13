---
title: 'Quickstart: Generate a thumbnail - REST, JavaScript - Computer Vision'
titleSuffix: Azure Cognitive Services
description: In this quickstart, you generate a thumbnail from an image using Computer Vision with JavaScript in Cognitive Services.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 0ea799f883f790c536df6c90a47fad74f400e7a9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867740"
---
# <a name="quickstart-generate-a-thumbnail---rest-javascript---computer-vision"></a><span data-ttu-id="7f09f-103">Quickstart: Generate a thumbnail - REST, JavaScript - Computer Vision</span><span class="sxs-lookup"><span data-stu-id="7f09f-103">Quickstart: Generate a thumbnail - REST, JavaScript - Computer Vision</span></span>

<span data-ttu-id="7f09f-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span><span class="sxs-lookup"><span data-stu-id="7f09f-104">In this quickstart, you generate a thumbnail from an image using Computer Vision.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f09f-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7f09f-105">Prerequisites</span></span>

<span data-ttu-id="7f09f-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span><span class="sxs-lookup"><span data-stu-id="7f09f-106">To use Computer Vision, you need a subscription key; see [Obtaining Subscription Keys](../Vision-API-How-to-Topics/HowToSubscribe.md).</span></span>

## <a name="get-thumbnail-request"></a><span data-ttu-id="7f09f-107">Get Thumbnail request</span><span class="sxs-lookup"><span data-stu-id="7f09f-107">Get Thumbnail request</span></span>

<span data-ttu-id="7f09f-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span><span class="sxs-lookup"><span data-stu-id="7f09f-108">With the [Get Thumbnail method](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb), you can generate a thumbnail of an image.</span></span> <span data-ttu-id="7f09f-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span><span class="sxs-lookup"><span data-stu-id="7f09f-109">You specify the height and width, which can differ from the aspect ratio of the input image.</span></span> <span data-ttu-id="7f09f-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span><span class="sxs-lookup"><span data-stu-id="7f09f-110">Computer Vision uses smart cropping to intelligently identify the region of interest and generate cropping coordinates based on that region.</span></span>

<span data-ttu-id="7f09f-111">To run the sample, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f09f-111">To run the sample, do the following steps:</span></span>

1. <span data-ttu-id="7f09f-112">Copy the following and save it to a file such as `thumbnail.html`.</span><span class="sxs-lookup"><span data-stu-id="7f09f-112">Copy the following and save it to a file such as `thumbnail.html`.</span></span>
1. <span data-ttu-id="7f09f-113">Replace `<Subscription Key>` with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="7f09f-113">Replace `<Subscription Key>` with your valid subscription key.</span></span>
1. <span data-ttu-id="7f09f-114">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span><span class="sxs-lookup"><span data-stu-id="7f09f-114">Change the `uriBase` value to the location where you obtained your subscription keys, if necessary.</span></span>
1. <span data-ttu-id="7f09f-115">Drag-and-drop the file into your browser.</span><span class="sxs-lookup"><span data-stu-id="7f09f-115">Drag-and-drop the file into your browser.</span></span>
1. <span data-ttu-id="7f09f-116">Click the `Generate thumbnail` button.</span><span class="sxs-lookup"><span data-stu-id="7f09f-116">Click the `Generate thumbnail` button.</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <title>Thumbnail Sample</title>
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
            "https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail";

        // Request parameters.
        var params = "?width=100&height=150&smartCropping=true";

        // Display the source image.
        var sourceImageUrl = document.getElementById("inputImage").value;
        document.querySelector("#sourceImage").src = sourceImageUrl;

        // Prepare the REST API call:

        // Create the HTTP Request object.
        var xhr = new XMLHttpRequest();

        // Identify the request as a POST, with the URL and parameters.
        xhr.open("POST", uriBase + params);

        // Add the request headers.
        xhr.setRequestHeader("Content-Type","application/json");
        xhr.setRequestHeader("Ocp-Apim-Subscription-Key", subscriptionKey);

        // Set the response type to "blob" for the thumbnail image data.
        xhr.responseType = "blob";

        // Process the result of the REST API call.
        xhr.onreadystatechange = function(e) {
            if(xhr.readyState === XMLHttpRequest.DONE) {

                // Thumbnail successfully created.
                if (xhr.status === 200) {
                    // Show response headers.
                    var s = JSON.stringify(xhr.getAllResponseHeaders(), null, 2);
                    document.getElementById("responseTextArea").value =
                        JSON.stringify(xhr.getAllResponseHeaders(), null, 2);

                    // Show thumbnail image.
                    var urlCreator = window.URL || window.webkitURL;
                    var imageUrl = urlCreator.createObjectURL(this.response);
                    document.querySelector("#thumbnailImage").src = imageUrl;
                } else {
                    // Display the error message. The error message is the response
                    // body as a JSON string. The code in this code block extracts
                    // the JSON string from the blob response.
                    var reader = new FileReader();

                    // This event fires after the blob has been read.
                    reader.addEventListener('loadend', (e) => {
                        document.getElementById("responseTextArea").value =
                            JSON.stringify(JSON.parse(e.srcElement.result), null, 2);
                    });

                    // Start reading the blob as text.
                    reader.readAsText(xhr.response);
                }
            }
        }

        // Make the REST API call.
        xhr.send('{"url": ' + '"' + sourceImageUrl + '"}');
    };
</script>

<h1>Generate thumbnail image:</h1>
Enter the URL to an image to use in creating a thumbnail image,
then click the <strong>Generate thumbnail</strong> button.
<br><br>
Image for thumbnail:
<input type="text" name="inputImage" id="inputImage"
    value="https://upload.wikimedia.org/wikipedia/commons/thumb/5/56/Shorkie_Poo_Puppy.jpg/1280px-Shorkie_Poo_Puppy.jpg" />
<button onclick="processImage()">Generate thumbnail</button>
<br><br>
<div id="wrapper" style="width:1160px; display:table;">
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
    <div id="thumbnailDiv" style="width:140px; display:table-cell;">
        Thumbnail:
        <br><br>
        <img id="thumbnailImage" />
    </div>
</div>
</body>
</html>
```

## <a name="get-thumbnail-response"></a><span data-ttu-id="7f09f-117">Get Thumbnail response</span><span class="sxs-lookup"><span data-stu-id="7f09f-117">Get Thumbnail response</span></span>

<span data-ttu-id="7f09f-118">A successful response contains the thumbnail image binary.</span><span class="sxs-lookup"><span data-stu-id="7f09f-118">A successful response contains the thumbnail image binary.</span></span> <span data-ttu-id="7f09f-119">If the request fails, the response contains an error code and a message to help determine what went wrong.</span><span class="sxs-lookup"><span data-stu-id="7f09f-119">If the request fails, the response contains an error code and a message to help determine what went wrong.</span></span> <span data-ttu-id="7f09f-120">The following text is an example of a successful response.</span><span class="sxs-lookup"><span data-stu-id="7f09f-120">The following text is an example of a successful response.</span></span>

```text
Response:

"Content-Type: image/jpeg\r\n"
```

## <a name="next-steps"></a><span data-ttu-id="7f09f-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f09f-121">Next steps</span></span>

<span data-ttu-id="7f09f-122">Explore a JavaScript application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="7f09f-122">Explore a JavaScript application that uses Computer Vision to perform optical character recognition (OCR); create smart-cropped thumbnails; plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="7f09f-123">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span><span class="sxs-lookup"><span data-stu-id="7f09f-123">To rapidly experiment with the Computer Vision APIs, try the [Open API testing console](https://westcentralus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa/console).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f09f-124">Computer Vision API JavaScript Tutorial</span><span class="sxs-lookup"><span data-stu-id="7f09f-124">Computer Vision API JavaScript Tutorial</span></span>](../Tutorials/javascript-tutorial.md)
