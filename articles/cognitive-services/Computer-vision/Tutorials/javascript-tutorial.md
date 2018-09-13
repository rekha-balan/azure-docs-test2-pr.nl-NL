---
title: Computer Vision API JavaScript tutorial | Microsoft Docs
description: Explore a basic JavaScript app that uses the Computer Vision API in Microsoft Cognitive Services. Perform OCR, create thumbnails, and work with visual features in an image.
services: cognitive-services
author: KellyDF
manager: corncar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: article
ms.date: 09/19/2017
ms.author: kefre
ms.openlocfilehash: 89bdc0524e07c1cb6a1473e0a52791fe20271e06
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868928"
---
# <a name="computer-vision-api-javascript-tutorial"></a><span data-ttu-id="0c203-104">Computer Vision API JavaScript tutorial</span><span class="sxs-lookup"><span data-stu-id="0c203-104">Computer Vision API JavaScript tutorial</span></span>

<span data-ttu-id="0c203-105">This tutorial shows the features of the Microsoft Cognitive Services Computer Vision REST API.</span><span class="sxs-lookup"><span data-stu-id="0c203-105">This tutorial shows the features of the Microsoft Cognitive Services Computer Vision REST API.</span></span>

<span data-ttu-id="0c203-106">Explore a JavaScript application that uses the Computer Vision REST API to perform optical character recognition (OCR), create smart-cropped thumbnails, plus detect, categorize, tag, and describe visual features, including faces, in an image.</span><span class="sxs-lookup"><span data-stu-id="0c203-106">Explore a JavaScript application that uses the Computer Vision REST API to perform optical character recognition (OCR), create smart-cropped thumbnails, plus detect, categorize, tag, and describe visual features, including faces, in an image.</span></span> <span data-ttu-id="0c203-107">This example lets you submit an image URL for analysis or processing.</span><span class="sxs-lookup"><span data-stu-id="0c203-107">This example lets you submit an image URL for analysis or processing.</span></span> <span data-ttu-id="0c203-108">You can use this open source example as a template for building your own app in JavaScript to use the Computer Vision REST API.</span><span class="sxs-lookup"><span data-stu-id="0c203-108">You can use this open source example as a template for building your own app in JavaScript to use the Computer Vision REST API.</span></span>

<span data-ttu-id="0c203-109">The JavaScript form application has already been written, but has no Computer Vision functionality.</span><span class="sxs-lookup"><span data-stu-id="0c203-109">The JavaScript form application has already been written, but has no Computer Vision functionality.</span></span> <span data-ttu-id="0c203-110">In this tutorial, you add the code specific to the Computer Vision REST API to complete the application's functionality.</span><span class="sxs-lookup"><span data-stu-id="0c203-110">In this tutorial, you add the code specific to the Computer Vision REST API to complete the application's functionality.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c203-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0c203-111">Prerequisites</span></span>

### <a name="platform-requirements"></a><span data-ttu-id="0c203-112">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="0c203-112">Platform requirements</span></span>

<span data-ttu-id="0c203-113">This tutorial has been developed using a simple text editor.</span><span class="sxs-lookup"><span data-stu-id="0c203-113">This tutorial has been developed using a simple text editor.</span></span>

### <a name="subscribe-to-computer-vision-api-and-get-a-subscription-key"></a><span data-ttu-id="0c203-114">Subscribe to Computer Vision API and get a subscription key</span><span class="sxs-lookup"><span data-stu-id="0c203-114">Subscribe to Computer Vision API and get a subscription key</span></span> 

<span data-ttu-id="0c203-115">Before creating the example, you must subscribe to Computer Vision API which is part of the Microsoft Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="0c203-115">Before creating the example, you must subscribe to Computer Vision API which is part of the Microsoft Cognitive Services.</span></span> <span data-ttu-id="0c203-116">For subscription and key management details, see [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="0c203-116">For subscription and key management details, see [Subscriptions](https://azure.microsoft.com/try/cognitive-services/).</span></span> <span data-ttu-id="0c203-117">Both the primary and secondary keys are valid to use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0c203-117">Both the primary and secondary keys are valid to use in this tutorial.</span></span> 

## <a name="download-the-tutorial-project"></a><span data-ttu-id="0c203-118">Download the tutorial project</span><span class="sxs-lookup"><span data-stu-id="0c203-118">Download the tutorial project</span></span>

<span data-ttu-id="0c203-119">Clone the [Cognitive Services JavaScript Computer Vision Tutorial](https://github.com/Azure-Samples/cognitive-services-javascript-computer-vision-tutorial), or download the .zip file and extract it to an empty directory.</span><span class="sxs-lookup"><span data-stu-id="0c203-119">Clone the [Cognitive Services JavaScript Computer Vision Tutorial](https://github.com/Azure-Samples/cognitive-services-javascript-computer-vision-tutorial), or download the .zip file and extract it to an empty directory.</span></span>

<span data-ttu-id="0c203-120">If you would prefer to use the finished tutorial with all tutorial code added, you can use the files in the **Completed** folder.</span><span class="sxs-lookup"><span data-stu-id="0c203-120">If you would prefer to use the finished tutorial with all tutorial code added, you can use the files in the **Completed** folder.</span></span>

## <a name="add-the-tutorial-code"></a><span data-ttu-id="0c203-121">Add the tutorial code</span><span class="sxs-lookup"><span data-stu-id="0c203-121">Add the tutorial code</span></span>

<span data-ttu-id="0c203-122">The JavaScript application is set up with six .html files, one for each feature.</span><span class="sxs-lookup"><span data-stu-id="0c203-122">The JavaScript application is set up with six .html files, one for each feature.</span></span> <span data-ttu-id="0c203-123">Each file demonstrates a different function of Computer Vision (analyze, OCR, etc).</span><span class="sxs-lookup"><span data-stu-id="0c203-123">Each file demonstrates a different function of Computer Vision (analyze, OCR, etc).</span></span> <span data-ttu-id="0c203-124">The six tutorial sections do not have interdependencies, so you can add the tutorial code to one file, all six files, or only a couple of files.</span><span class="sxs-lookup"><span data-stu-id="0c203-124">The six tutorial sections do not have interdependencies, so you can add the tutorial code to one file, all six files, or only a couple of files.</span></span> <span data-ttu-id="0c203-125">And you can add the tutorial code to the files in any order.</span><span class="sxs-lookup"><span data-stu-id="0c203-125">And you can add the tutorial code to the files in any order.</span></span>

<span data-ttu-id="0c203-126">Let's get started.</span><span class="sxs-lookup"><span data-stu-id="0c203-126">Let's get started.</span></span>

## <a name="analyze-an-image"></a><span data-ttu-id="0c203-127">Analyze an image</span><span class="sxs-lookup"><span data-stu-id="0c203-127">Analyze an image</span></span>

<span data-ttu-id="0c203-128">The Analyze feature of Computer Vision analyzes an image for more than 2,000 recognizable objects, living beings, scenery, and actions.</span><span class="sxs-lookup"><span data-stu-id="0c203-128">The Analyze feature of Computer Vision analyzes an image for more than 2,000 recognizable objects, living beings, scenery, and actions.</span></span> <span data-ttu-id="0c203-129">Once the analysis is complete, Analyze returns a JSON object that describes the image with descriptive tags, color analysis, captions, and more.</span><span class="sxs-lookup"><span data-stu-id="0c203-129">Once the analysis is complete, Analyze returns a JSON object that describes the image with descriptive tags, color analysis, captions, and more.</span></span>

<span data-ttu-id="0c203-130">To complete the Analyze feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c203-130">To complete the Analyze feature of the tutorial application, perform the following steps:</span></span>

### <a name="analyze-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="0c203-131">Analyze step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="0c203-131">Analyze step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="0c203-132">Open the **analyze.html** file in a text editor and locate the **analyzeButtonClick** function near the bottom of the file.</span><span class="sxs-lookup"><span data-stu-id="0c203-132">Open the **analyze.html** file in a text editor and locate the **analyzeButtonClick** function near the bottom of the file.</span></span>

<span data-ttu-id="0c203-133">The **analyzeButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **AnalyzeImage** function to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="0c203-133">The **analyzeButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **AnalyzeImage** function to analyze the image.</span></span>

<span data-ttu-id="0c203-134">Copy and paste the following code into the **analyzeButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-134">Copy and paste the following code into the **analyzeButtonClick** function.</span></span>

```javascript
function analyzeButtonClick() {

    // Clear the display fields.
    $("#sourceImage").attr("src", "#");
    $("#responseTextArea").val("");
    $("#captionSpan").text("");
    
    // Display the image.
    var sourceImageUrl = $("#inputImage").val();
    $("#sourceImage").attr("src", sourceImageUrl);
    
    AnalyzeImage(sourceImageUrl, $("#responseTextArea"), $("#captionSpan"));
}
```

### <a name="analyze-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="0c203-135">Analyze step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="0c203-135">Analyze step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="0c203-136">The **AnalyzeImage** function wraps the REST API call to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="0c203-136">The **AnalyzeImage** function wraps the REST API call to analyze an image.</span></span> <span data-ttu-id="0c203-137">Upon a successful return, the formatted JSON analysis will be displayed in the specified textarea, and the caption will be displayed in the specified span.</span><span class="sxs-lookup"><span data-stu-id="0c203-137">Upon a successful return, the formatted JSON analysis will be displayed in the specified textarea, and the caption will be displayed in the specified span.</span></span>

<span data-ttu-id="0c203-138">Copy and paste the **AnalyzeImage** function code to just underneath the **analyzeButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-138">Copy and paste the **AnalyzeImage** function code to just underneath the **analyzeButtonClick** function.</span></span>

```javascript
/* Analyze the image at the specified URL by using Microsoft Cognitive Services Analyze Image API.
 * @param {string} sourceImageUrl - The URL to the image to analyze.
 * @param {<textarea> element} responseTextArea - The text area to display the JSON string returned
 *                             from the REST API call, or to display the error message if there was 
 *                             an error.
 * @param {<span> element} captionSpan - The span to display the image caption.
 */
function AnalyzeImage(sourceImageUrl, responseTextArea, captionSpan) {
    // Request parameters.
    var params = {
        "visualFeatures": "Categories,Description,Color",
        "details": "",
        "language": "en",
    };
    
    // Perform the REST API call.
    $.ajax({
        url: common.uriBasePreRegion + 
             $("#subscriptionRegionSelect").val() + 
             common.uriBasePostRegion + 
             common.uriBaseAnalyze +
             "?" + 
             $.param(params),
                    
        // Request headers.
        beforeSend: function(jqXHR){
            jqXHR.setRequestHeader("Content-Type","application/json");
            jqXHR.setRequestHeader("Ocp-Apim-Subscription-Key", 
                encodeURIComponent($("#subscriptionKeyInput").val()));
        },
        
        type: "POST",
        
        // Request body.
        data: '{"url": ' + '"' + sourceImageUrl + '"}',
    })
    
    .done(function(data) {
        // Show formatted JSON on webpage.
        responseTextArea.val(JSON.stringify(data, null, 2));
        
        // Extract and display the caption and confidence from the first caption in the description object.
        if (data.description && data.description.captions) {
            var caption = data.description.captions[0];
            
            if (caption.text && caption.confidence) {
                captionSpan.text("Caption: " + caption.text +
                    " (confidence: " + caption.confidence + ").");
            }
        }
    })
    
    .fail(function(jqXHR, textStatus, errorThrown) {
        // Prepare the error string.
        var errorString = (errorThrown === "") ? "Error. " : errorThrown + " (" + jqXHR.status + "): ";
        errorString += (jqXHR.responseText === "") ? "" : (jQuery.parseJSON(jqXHR.responseText).message) ? 
            jQuery.parseJSON(jqXHR.responseText).message : jQuery.parseJSON(jqXHR.responseText).error.message;
        
        // Put the error JSON in the response textarea.
        responseTextArea.val(JSON.stringify(jqXHR, null, 2));
        
        // Show the error message.
        alert(errorString);
    });
}
```

### <a name="analyze-step-3-run-the-application"></a><span data-ttu-id="0c203-139">Analyze step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="0c203-139">Analyze step 3: Run the application</span></span>

<span data-ttu-id="0c203-140">Save the **analyze.html** file and open it in a Web browser.</span><span class="sxs-lookup"><span data-stu-id="0c203-140">Save the **analyze.html** file and open it in a Web browser.</span></span> <span data-ttu-id="0c203-141">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="0c203-141">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="0c203-142">Enter a URL to an image to analyze, then click the **Analyze Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="0c203-142">Enter a URL to an image to analyze, then click the **Analyze Image** button to analyze an image and see the result.</span></span>

## <a name="recognize-a-landmark"></a><span data-ttu-id="0c203-143">Recognize a landmark</span><span class="sxs-lookup"><span data-stu-id="0c203-143">Recognize a landmark</span></span>

<span data-ttu-id="0c203-144">The Landmark feature of Computer Vision analyzes an image for natural and artificial landmarks, such as mountains or famous buildings.</span><span class="sxs-lookup"><span data-stu-id="0c203-144">The Landmark feature of Computer Vision analyzes an image for natural and artificial landmarks, such as mountains or famous buildings.</span></span> <span data-ttu-id="0c203-145">Once the analysis is complete, Landmark returns a JSON object that identifies the landmarks found in the image.</span><span class="sxs-lookup"><span data-stu-id="0c203-145">Once the analysis is complete, Landmark returns a JSON object that identifies the landmarks found in the image.</span></span>

<span data-ttu-id="0c203-146">To complete the Landmark feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c203-146">To complete the Landmark feature of the tutorial application, perform the following steps:</span></span>

### <a name="landmark-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="0c203-147">Landmark step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="0c203-147">Landmark step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="0c203-148">Open the **landmark.html** file in a text editor and locate the **landmarkButtonClick** function near the bottom of the file.</span><span class="sxs-lookup"><span data-stu-id="0c203-148">Open the **landmark.html** file in a text editor and locate the **landmarkButtonClick** function near the bottom of the file.</span></span>

<span data-ttu-id="0c203-149">The **landmarkButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **IdentifyLandmarks** function to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="0c203-149">The **landmarkButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **IdentifyLandmarks** function to analyze the image.</span></span>

<span data-ttu-id="0c203-150">Copy and paste the following code into the **landmarkButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-150">Copy and paste the following code into the **landmarkButtonClick** function.</span></span>

```javascript
function landmarkButtonClick() {

    // Clear the display fields.
    $("#sourceImage").attr("src", "#");
    $("#responseTextArea").val("");
    $("#captionSpan").text("");
    
    // Display the image.
    var sourceImageUrl = $("#inputImage").val();
    $("#sourceImage").attr("src", sourceImageUrl);
    
    IdentifyLandmarks(sourceImageUrl, $("#responseTextArea"), $("#captionSpan"));
}
```

### <a name="landmark-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="0c203-151">Landmark step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="0c203-151">Landmark step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="0c203-152">The **IdentifyLandmarks** function wraps the REST API call to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="0c203-152">The **IdentifyLandmarks** function wraps the REST API call to analyze an image.</span></span> <span data-ttu-id="0c203-153">Upon a successful return, the formatted JSON analysis will be displayed in the specified textarea, and the caption will be displayed in the specified span.</span><span class="sxs-lookup"><span data-stu-id="0c203-153">Upon a successful return, the formatted JSON analysis will be displayed in the specified textarea, and the caption will be displayed in the specified span.</span></span>

<span data-ttu-id="0c203-154">Copy and paste the **IdentifyLandmarks** function code to just underneath the **landmarkButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-154">Copy and paste the **IdentifyLandmarks** function code to just underneath the **landmarkButtonClick** function.</span></span>

```javascript
/* Identify landmarks in the image at the specified URL by using Microsoft Cognitive Services 
 * Landmarks API.
 * @param {string} sourceImageUrl - The URL to the image to analyze for landmarks.
 * @param {<textarea> element} responseTextArea - The text area to display the JSON string returned
 *                             from the REST API call, or to display the error message if there was 
 *                             an error.
 * @param {<span> element} captionSpan - The span to display the image caption.
 */
function IdentifyLandmarks(sourceImageUrl, responseTextArea, captionSpan) {
    // Request parameters.
    var params = {
        "model": "landmarks"
    };
    
    // Perform the REST API call.
    $.ajax({
        url: common.uriBasePreRegion + 
             $("#subscriptionRegionSelect").val() + 
             common.uriBasePostRegion + 
             common.uriBaseLandmark +
             "?" + 
             $.param(params),
                    
        // Request headers.
        beforeSend: function(jqXHR){
            jqXHR.setRequestHeader("Content-Type","application/json");
            jqXHR.setRequestHeader("Ocp-Apim-Subscription-Key", 
                encodeURIComponent($("#subscriptionKeyInput").val()));
        },
        
        type: "POST",
        
        // Request body.
        data: '{"url": ' + '"' + sourceImageUrl + '"}',
    })
    
    .done(function(data) {
        // Show formatted JSON on webpage.
        responseTextArea.val(JSON.stringify(data, null, 2));
        
        // Extract and display the caption and confidence from the first caption in the description object.
        if (data.result && data.result.landmarks) {
            var landmark = data.result.landmarks[0];
            
            if (landmark.name && landmark.confidence) {
                captionSpan.text("Landmark: " + landmark.name +
                    " (confidence: " + landmark.confidence + ").");
            }
        }
    })
    
    .fail(function(jqXHR, textStatus, errorThrown) {
        // Prepare the error string.
        var errorString = (errorThrown === "") ? "Error. " : errorThrown + " (" + jqXHR.status + "): ";
        errorString += (jqXHR.responseText === "") ? "" : (jQuery.parseJSON(jqXHR.responseText).message) ? 
            jQuery.parseJSON(jqXHR.responseText).message : jQuery.parseJSON(jqXHR.responseText).error.message;
        
        // Put the error JSON in the response textarea.
        responseTextArea.val(JSON.stringify(jqXHR, null, 2));
        
        // Show the error message.
        alert(errorString);
    });
}
```

### <a name="landmark-step-3-run-the-application"></a><span data-ttu-id="0c203-155">Landmark step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="0c203-155">Landmark step 3: Run the application</span></span>

<span data-ttu-id="0c203-156">Save the **landmark.html** file and open it in a Web browser.</span><span class="sxs-lookup"><span data-stu-id="0c203-156">Save the **landmark.html** file and open it in a Web browser.</span></span> <span data-ttu-id="0c203-157">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="0c203-157">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="0c203-158">Enter a URL to an image to analyze, then click the **Analyze Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="0c203-158">Enter a URL to an image to analyze, then click the **Analyze Image** button to analyze an image and see the result.</span></span>

## <a name="recognize-celebrities"></a><span data-ttu-id="0c203-159">Recognize celebrities</span><span class="sxs-lookup"><span data-stu-id="0c203-159">Recognize celebrities</span></span>

<span data-ttu-id="0c203-160">The Celebrities feature of Computer Vision analyzes an image for famous people.</span><span class="sxs-lookup"><span data-stu-id="0c203-160">The Celebrities feature of Computer Vision analyzes an image for famous people.</span></span> <span data-ttu-id="0c203-161">Once the analysis is complete, Celebrities returns a JSON object that identifies the Celebrities found in the image.</span><span class="sxs-lookup"><span data-stu-id="0c203-161">Once the analysis is complete, Celebrities returns a JSON object that identifies the Celebrities found in the image.</span></span>

<span data-ttu-id="0c203-162">To complete the Celebrities feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c203-162">To complete the Celebrities feature of the tutorial application, perform the following steps:</span></span>

### <a name="celebrities-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="0c203-163">Celebrities step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="0c203-163">Celebrities step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="0c203-164">Open the **celebrities.html** file in a text editor and locate the **celebritiesButtonClick** function near the bottom of the file.</span><span class="sxs-lookup"><span data-stu-id="0c203-164">Open the **celebrities.html** file in a text editor and locate the **celebritiesButtonClick** function near the bottom of the file.</span></span>

<span data-ttu-id="0c203-165">The **celebritiesButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **IdentifyCelebrities** function to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="0c203-165">The **celebritiesButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **IdentifyCelebrities** function to analyze the image.</span></span>

<span data-ttu-id="0c203-166">Copy and paste the following code into the **celebritiesButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-166">Copy and paste the following code into the **celebritiesButtonClick** function.</span></span>

```javascript
function celebritiesButtonClick() {

    // Clear the display fields.
    $("#sourceImage").attr("src", "#");
    $("#responseTextArea").val("");
    $("#captionSpan").text("");
    
    // Display the image.
    var sourceImageUrl = $("#inputImage").val();
    $("#sourceImage").attr("src", sourceImageUrl);
    
    IdentifyCelebrities(sourceImageUrl, $("#responseTextArea"), $("#captionSpan"));
}
```

### <a name="celebrities-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="0c203-167">Celebrities step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="0c203-167">Celebrities step 2: Add the wrapper for the REST API call</span></span>

```javascript
/* Identify celebrities in the image at the specified URL by using Microsoft Cognitive Services 
 * Celebrities API.
 * @param {string} sourceImageUrl - The URL to the image to analyze for celebrities.
 * @param {<textarea> element} responseTextArea - The text area to display the JSON string returned
 *                             from the REST API call, or to display the error message if there was 
 *                             an error.
 * @param {<span> element} captionSpan - The span to display the image caption.
 */
function IdentifyCelebrities(sourceImageUrl, responseTextArea, captionSpan) {
    // Request parameters.
    var params = {
        "model": "celebrities"
    };
    
    // Perform the REST API call.
    $.ajax({
        url: common.uriBasePreRegion + 
             $("#subscriptionRegionSelect").val() + 
             common.uriBasePostRegion + 
             common.uriBaseCelebrities +
             "?" + 
             $.param(params),
                    
        // Request headers.
        beforeSend: function(jqXHR){
            jqXHR.setRequestHeader("Content-Type","application/json");
            jqXHR.setRequestHeader("Ocp-Apim-Subscription-Key", 
                encodeURIComponent($("#subscriptionKeyInput").val()));
        },
        
        type: "POST",
        
        // Request body.
        data: '{"url": ' + '"' + sourceImageUrl + '"}',
    })
    
    .done(function(data) {
        // Show formatted JSON on webpage.
        responseTextArea.val(JSON.stringify(data, null, 2));
        
        // Extract and display the caption and confidence from the first caption in the description object.
        if (data.result && data.result.celebrities) {
            var celebrity = data.result.celebrities[0];
            
            if (celebrity.name && celebrity.confidence) {
                captionSpan.text("Celebrity name: " + celebrity.name +
                    " (confidence: " + celebrity.confidence + ").");
            }
        }
    })
    
    .fail(function(jqXHR, textStatus, errorThrown) {
        // Prepare the error string.
        var errorString = (errorThrown === "") ? "Error. " : errorThrown + " (" + jqXHR.status + "): ";
        errorString += (jqXHR.responseText === "") ? "" : (jQuery.parseJSON(jqXHR.responseText).message) ? 
            jQuery.parseJSON(jqXHR.responseText).message : jQuery.parseJSON(jqXHR.responseText).error.message;
        
        // Put the error JSON in the response textarea.
        responseTextArea.val(JSON.stringify(jqXHR, null, 2));
        
        // Show the error message.
        alert(errorString);
    });
}
```

### <a name="celebrities-step-3-run-the-application"></a><span data-ttu-id="0c203-168">Celebrities step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="0c203-168">Celebrities step 3: Run the application</span></span>

<span data-ttu-id="0c203-169">Save the **celebrities.html** file and open it in a Web browser.</span><span class="sxs-lookup"><span data-stu-id="0c203-169">Save the **celebrities.html** file and open it in a Web browser.</span></span> <span data-ttu-id="0c203-170">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="0c203-170">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="0c203-171">Enter a URL to an image to analyze, then click the **Analyze Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="0c203-171">Enter a URL to an image to analyze, then click the **Analyze Image** button to analyze an image and see the result.</span></span>

## <a name="intelligently-generate-a-thumbnail"></a><span data-ttu-id="0c203-172">Intelligently generate a thumbnail</span><span class="sxs-lookup"><span data-stu-id="0c203-172">Intelligently generate a thumbnail</span></span>

<span data-ttu-id="0c203-173">The Thumbnail feature of Computer Vision generates a thumbnail from an image.</span><span class="sxs-lookup"><span data-stu-id="0c203-173">The Thumbnail feature of Computer Vision generates a thumbnail from an image.</span></span> <span data-ttu-id="0c203-174">By using the **Smart Crop** feature, the Thumbnail feature will identify the area of interest in an image and center the thumbnail on this area, to generate more aesthetically pleasing thumbnail images.</span><span class="sxs-lookup"><span data-stu-id="0c203-174">By using the **Smart Crop** feature, the Thumbnail feature will identify the area of interest in an image and center the thumbnail on this area, to generate more aesthetically pleasing thumbnail images.</span></span>

<span data-ttu-id="0c203-175">To complete the Thumbnail feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c203-175">To complete the Thumbnail feature of the tutorial application, perform the following steps:</span></span>

### <a name="thumbnail-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="0c203-176">Thumbnail step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="0c203-176">Thumbnail step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="0c203-177">Open the **thumbnail.html** file in a text editor and locate the **thumbnailButtonClick** function near the bottom of the file.</span><span class="sxs-lookup"><span data-stu-id="0c203-177">Open the **thumbnail.html** file in a text editor and locate the **thumbnailButtonClick** function near the bottom of the file.</span></span>

<span data-ttu-id="0c203-178">The **thumbnailButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **getThumbnail** function twice to create two thumbnails, one smart cropped and one without smart crop.</span><span class="sxs-lookup"><span data-stu-id="0c203-178">The **thumbnailButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **getThumbnail** function twice to create two thumbnails, one smart cropped and one without smart crop.</span></span>

<span data-ttu-id="0c203-179">Copy and paste the following code into the **thumbnailButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-179">Copy and paste the following code into the **thumbnailButtonClick** function.</span></span>

```javascript
function thumbnailButtonClick() {

    // Clear the display fields.
    document.getElementById("sourceImage").src = "#";
    document.getElementById("thumbnailImageSmartCrop").src = "#";
    document.getElementById("thumbnailImageNonSmartCrop").src = "#";
    document.getElementById("responseTextArea").value = "";
    document.getElementById("captionSpan").text = "";
    
    // Display the image.
    var sourceImageUrl = document.getElementById("inputImage").value;
    document.getElementById("sourceImage").src = sourceImageUrl;
    
    // Get a smart cropped thumbnail.
    getThumbnail (sourceImageUrl, true, document.getElementById("thumbnailImageSmartCrop"), 
        document.getElementById("responseTextArea"));
    
    // Get a non-smart-cropped thumbnail.
    getThumbnail (sourceImageUrl, false, document.getElementById("thumbnailImageNonSmartCrop"),
        document.getElementById("responseTextArea"));
}
```

### <a name="thumbnail-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="0c203-180">Thumbnail step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="0c203-180">Thumbnail step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="0c203-181">The **getThumbnail** function wraps the REST API call to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="0c203-181">The **getThumbnail** function wraps the REST API call to analyze an image.</span></span> <span data-ttu-id="0c203-182">Upon a successful return, the thumbnail will be displayed in the specified img element.</span><span class="sxs-lookup"><span data-stu-id="0c203-182">Upon a successful return, the thumbnail will be displayed in the specified img element.</span></span>

<span data-ttu-id="0c203-183">Copy and paste the following **getThumbnail** function to just underneath the **thumbnailButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-183">Copy and paste the following **getThumbnail** function to just underneath the **thumbnailButtonClick** function.</span></span>

```javascript
/* Get a thumbnail of the image at the specified URL by using Microsoft Cognitive Services
 * Thumbnail API.
 * @param {string} sourceImageUrl URL to image.
 * @param {boolean} smartCropping Set to true to use the smart cropping feature which crops to the
 *                                more interesting area of an image; false to crop for the center
 *                                of the image.
 * @param {<img> element} imageElement The img element in the DOM which will display the thumnail image.
 * @param {<textarea> element} responseTextArea - The text area to display the Response Headers returned
 *                             from the REST API call, or to display the error message if there was 
 *                             an error.
 */
function getThumbnail (sourceImageUrl, smartCropping, imageElement, responseTextArea) {
    // Create the HTTP Request object.
    var xhr = new XMLHttpRequest();
    
    // Request parameters.
    var params = "width=100&height=150&smartCropping=" + smartCropping.toString();

    // Build the full URI.
    var fullUri = common.uriBasePreRegion + 
                  document.getElementById("subscriptionRegionSelect").value + 
                  common.uriBasePostRegion + 
                  common.uriBaseThumbnail +
                  "?" + 
                  params;
    
    // Identify the request as a POST, with the URI and parameters.
    xhr.open("POST", fullUri);
    
    // Add the request headers.
    xhr.setRequestHeader("Content-Type","application/json");
    xhr.setRequestHeader("Ocp-Apim-Subscription-Key", 
        encodeURIComponent(document.getElementById("subscriptionKeyInput").value));
    
    // Set the response type to "blob" for the thumbnail image data.
    xhr.responseType = "blob";
    
    // Process the result of the REST API call.
    xhr.onreadystatechange = function(e) {
        if(xhr.readyState === XMLHttpRequest.DONE) {
            
            // Thumbnail successfully created.
            if (xhr.status === 200) {
                // Show response headers.
                var s = JSON.stringify(xhr.getAllResponseHeaders(), null, 2);
                responseTextArea.value = JSON.stringify(xhr.getAllResponseHeaders(), null, 2);
                
                // Show thumbnail image.
                var urlCreator = window.URL || window.webkitURL;
                var imageUrl = urlCreator.createObjectURL(this.response);
                imageElement.src = imageUrl;
            } else {
                // Display the error message. The error message is the response body as a JSON string. 
                // The code in this code block extracts the JSON string from the blob response.
                var reader = new FileReader();
                
                // This event fires after the blob has been read.
                reader.addEventListener('loadend', (e) => {
                    responseTextArea.value = JSON.stringify(JSON.parse(e.srcElement.result), null, 2);
                });
                
                // Start reading the blob as text.
                reader.readAsText(xhr.response);
            }
        }
    }
    
    // Execute the REST API call.
    xhr.send('{"url": ' + '"' + sourceImageUrl + '"}');
}
```

### <a name="thumbnail-step-3-run-the-application"></a><span data-ttu-id="0c203-184">Thumbnail step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="0c203-184">Thumbnail step 3: Run the application</span></span>

<span data-ttu-id="0c203-185">Save the **thumbnail.html** file and open it in a Web browser.</span><span class="sxs-lookup"><span data-stu-id="0c203-185">Save the **thumbnail.html** file and open it in a Web browser.</span></span> <span data-ttu-id="0c203-186">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="0c203-186">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="0c203-187">Enter a URL to an image to analyze, then click the **Generate Thumbnails** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="0c203-187">Enter a URL to an image to analyze, then click the **Generate Thumbnails** button to analyze an image and see the result.</span></span>

## <a name="read-printed-text-ocr"></a><span data-ttu-id="0c203-188">Read printed text (OCR)</span><span class="sxs-lookup"><span data-stu-id="0c203-188">Read printed text (OCR)</span></span>

<span data-ttu-id="0c203-189">The Optical Character Recognition (OCR) feature of Computer Vision analyzes an image of printed text.</span><span class="sxs-lookup"><span data-stu-id="0c203-189">The Optical Character Recognition (OCR) feature of Computer Vision analyzes an image of printed text.</span></span> <span data-ttu-id="0c203-190">After the analysis is complete, OCR returns a JSON object that contains the text and the location of the text in the image.</span><span class="sxs-lookup"><span data-stu-id="0c203-190">After the analysis is complete, OCR returns a JSON object that contains the text and the location of the text in the image.</span></span>

<span data-ttu-id="0c203-191">To complete the OCR feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c203-191">To complete the OCR feature of the tutorial application, perform the following steps:</span></span>

### <a name="ocr-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="0c203-192">OCR step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="0c203-192">OCR step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="0c203-193">Open the **ocr.html** file in a text editor and locate the **ocrButtonClick** function near the bottom of the file.</span><span class="sxs-lookup"><span data-stu-id="0c203-193">Open the **ocr.html** file in a text editor and locate the **ocrButtonClick** function near the bottom of the file.</span></span>

<span data-ttu-id="0c203-194">The **ocrButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **ReadOcrImage** function to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="0c203-194">The **ocrButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **ReadOcrImage** function to analyze the image.</span></span>

<span data-ttu-id="0c203-195">Copy and paste the following code into the **ocrButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-195">Copy and paste the following code into the **ocrButtonClick** function.</span></span>

```javascript
function ocrButtonClick() {

    // Clear the display fields.
    $("#sourceImage").attr("src", "#");
    $("#responseTextArea").val("");
    $("#captionSpan").text("");
    
    // Display the image.
    var sourceImageUrl = $("#inputImage").val();
    $("#sourceImage").attr("src", sourceImageUrl);
    
    ReadOcrImage(sourceImageUrl, $("#responseTextArea"));
}
```

### <a name="ocr-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="0c203-196">OCR step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="0c203-196">OCR step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="0c203-197">The **ReadOcrImage** function wraps the REST API call to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="0c203-197">The **ReadOcrImage** function wraps the REST API call to analyze an image.</span></span> <span data-ttu-id="0c203-198">Upon a successful return, the formatted JSON describing the text and the location of the text will be displayed in the specified textarea.</span><span class="sxs-lookup"><span data-stu-id="0c203-198">Upon a successful return, the formatted JSON describing the text and the location of the text will be displayed in the specified textarea.</span></span>

<span data-ttu-id="0c203-199">Copy and paste the following **ReadOcrImage** function to just underneath the **ocrButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-199">Copy and paste the following **ReadOcrImage** function to just underneath the **ocrButtonClick** function.</span></span>

```javascript
/* Recognize and read printed text in an image at the specified URL by using Microsoft Cognitive 
 * Services OCR API.
 * @param {string} sourceImageUrl - The URL to the image to analyze for printed text.
 * @param {<textarea> element} responseTextArea - The text area to display the JSON string returned
 *                             from the REST API call, or to display the error message if there was 
 *                             an error.
 */
function ReadOcrImage(sourceImageUrl, responseTextArea) {
    // Request parameters.
    var params = {
        "language": "unk",
        "detectOrientation ": "true",
    };

    // Perform the REST API call.
    $.ajax({
        url: common.uriBasePreRegion + 
             $("#subscriptionRegionSelect").val() + 
             common.uriBasePostRegion + 
             common.uriBaseOcr +
             "?" + 
             $.param(params),
        
        // Request headers.
        beforeSend: function(jqXHR){
            jqXHR.setRequestHeader("Content-Type","application/json");
            jqXHR.setRequestHeader("Ocp-Apim-Subscription-Key", 
                encodeURIComponent($("#subscriptionKeyInput").val()));
        },
        
        type: "POST",
        
        // Request body.
        data: '{"url": ' + '"' + sourceImageUrl + '"}',
    })
    
    .done(function(data) {
        // Show formatted JSON on webpage.
        responseTextArea.val(JSON.stringify(data, null, 2));
    })
    
    .fail(function(jqXHR, textStatus, errorThrown) {
        // Put the JSON description into the text area.
        responseTextArea.val(JSON.stringify(jqXHR, null, 2));
        
        // Display error message.
        var errorString = (errorThrown === "") ? "Error. " : errorThrown + " (" + jqXHR.status + "): ";
        errorString += (jqXHR.responseText === "") ? "" : (jQuery.parseJSON(jqXHR.responseText).message) ? 
            jQuery.parseJSON(jqXHR.responseText).message : jQuery.parseJSON(jqXHR.responseText).error.message;
        alert(errorString);
    });
}
```

### <a name="ocr-step-3-run-the-application"></a><span data-ttu-id="0c203-200">OCR step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="0c203-200">OCR step 3: Run the application</span></span>

<span data-ttu-id="0c203-201">Save the **ocr.html** file and open it in a Web browser.</span><span class="sxs-lookup"><span data-stu-id="0c203-201">Save the **ocr.html** file and open it in a Web browser.</span></span> <span data-ttu-id="0c203-202">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="0c203-202">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="0c203-203">Enter a URL to an image of text to read, then click the **Read Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="0c203-203">Enter a URL to an image of text to read, then click the **Read Image** button to analyze an image and see the result.</span></span>

## <a name="read-handwritten-text-handwriting-recognition"></a><span data-ttu-id="0c203-204">Read handwritten text (Handwriting Recognition)</span><span class="sxs-lookup"><span data-stu-id="0c203-204">Read handwritten text (Handwriting Recognition)</span></span>

<span data-ttu-id="0c203-205">The Handwriting Recognition feature of Computer Vision analyzes an image of handwritten text.</span><span class="sxs-lookup"><span data-stu-id="0c203-205">The Handwriting Recognition feature of Computer Vision analyzes an image of handwritten text.</span></span> <span data-ttu-id="0c203-206">After the analysis is complete, Handwriting Recognition returns a JSON object that contains the text and the location of the text in the image.</span><span class="sxs-lookup"><span data-stu-id="0c203-206">After the analysis is complete, Handwriting Recognition returns a JSON object that contains the text and the location of the text in the image.</span></span>

<span data-ttu-id="0c203-207">To complete the Handwriting Recognition feature of the tutorial application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c203-207">To complete the Handwriting Recognition feature of the tutorial application, perform the following steps:</span></span>

### <a name="handwriting-recognition-step-1-add-the-event-handler-code-for-the-form-button"></a><span data-ttu-id="0c203-208">Handwriting Recognition step 1: Add the event handler code for the form button</span><span class="sxs-lookup"><span data-stu-id="0c203-208">Handwriting Recognition step 1: Add the event handler code for the form button</span></span>

<span data-ttu-id="0c203-209">Open the **handwriting.html** file in a text editor and locate the **handwritingButtonClick** function near the bottom of the file.</span><span class="sxs-lookup"><span data-stu-id="0c203-209">Open the **handwriting.html** file in a text editor and locate the **handwritingButtonClick** function near the bottom of the file.</span></span>

<span data-ttu-id="0c203-210">The **handwritingButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **HandwritingImage** function to analyze the image.</span><span class="sxs-lookup"><span data-stu-id="0c203-210">The **handwritingButtonClick** event handler function clears the form, displays the image specified in the URL, then calls the **HandwritingImage** function to analyze the image.</span></span>

<span data-ttu-id="0c203-211">Copy and paste the following code into the **handwritingButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-211">Copy and paste the following code into the **handwritingButtonClick** function.</span></span>

```javascript
function handwritingButtonClick() {

    // Clear the display fields.
    $("#sourceImage").attr("src", "#");
    $("#responseTextArea").val("");
    
    // Display the image.
    var sourceImageUrl = $("#inputImage").val();
    $("#sourceImage").attr("src", sourceImageUrl);
    
    ReadHandwrittenImage(sourceImageUrl, $("#responseTextArea"));
}
```

### <a name="handwriting-recognition-step-2-add-the-wrapper-for-the-rest-api-call"></a><span data-ttu-id="0c203-212">Handwriting Recognition step 2: Add the wrapper for the REST API call</span><span class="sxs-lookup"><span data-stu-id="0c203-212">Handwriting Recognition step 2: Add the wrapper for the REST API call</span></span>

<span data-ttu-id="0c203-213">The **ReadHandwrittenImage** function wraps the two REST API calls needed to analyze an image.</span><span class="sxs-lookup"><span data-stu-id="0c203-213">The **ReadHandwrittenImage** function wraps the two REST API calls needed to analyze an image.</span></span> <span data-ttu-id="0c203-214">Because Handwriting Recognition is a time consuming process, a two step process is used.</span><span class="sxs-lookup"><span data-stu-id="0c203-214">Because Handwriting Recognition is a time consuming process, a two step process is used.</span></span> <span data-ttu-id="0c203-215">The first call submits the image for processing; the second call retrieves the detected text when the processing is complete.</span><span class="sxs-lookup"><span data-stu-id="0c203-215">The first call submits the image for processing; the second call retrieves the detected text when the processing is complete.</span></span>

<span data-ttu-id="0c203-216">After the text is retrieved, the formatted JSON describing the text and the location of the text will be displayed in the specified textarea.</span><span class="sxs-lookup"><span data-stu-id="0c203-216">After the text is retrieved, the formatted JSON describing the text and the location of the text will be displayed in the specified textarea.</span></span>

<span data-ttu-id="0c203-217">Copy and paste the following **ReadHandwrittenImage** function to just underneath the **handwritingButtonClick** function.</span><span class="sxs-lookup"><span data-stu-id="0c203-217">Copy and paste the following **ReadHandwrittenImage** function to just underneath the **handwritingButtonClick** function.</span></span>

```javascript
/* Recognize and read text from an image of handwriting at the specified URL by using Microsoft 
 * Cognitive Services Recognize Handwritten Text API.
 * @param {string} sourceImageUrl - The URL to the image to analyze for handwriting.
 * @param {<textarea> element} responseTextArea - The text area to display the JSON string returned
 *                             from the REST API call, or to display the error message if there was 
 *                             an error.
 */
function ReadHandwrittenImage(sourceImageUrl, responseTextArea) {
    // Request parameters.
    var params = {
        "handwriting": "true",
    };

    // This operation requrires two REST API calls. One to submit the image for processing,
    // the other to retrieve the text found in the image. 
    //
    // Perform the first REST API call to submit the image for processing.
    $.ajax({
        url: common.uriBasePreRegion + 
             $("#subscriptionRegionSelect").val() + 
             common.uriBasePostRegion + 
             common.uriBaseHandwriting +
             "?" + 
             $.param(params),
        
        // Request headers.
        beforeSend: function(jqXHR){
            jqXHR.setRequestHeader("Content-Type","application/json");
            jqXHR.setRequestHeader("Ocp-Apim-Subscription-Key", 
                encodeURIComponent($("#subscriptionKeyInput").val()));
        },
        
        type: "POST",
        
        // Request body.
        data: '{"url": ' + '"' + sourceImageUrl + '"}',
    })
    
    .done(function(data, textStatus, jqXHR) {
        // Show progress.
        responseTextArea.val("Handwritten image submitted.");
        
        // Note: The response may not be immediately available. Handwriting Recognition is an
        // async operation that can take a variable amount of time depending on the length
        // of the text you want to recognize. You may need to wait or retry this GET operation.
        //
        // Try once per second for up to ten seconds to receive the result.
        var tries = 10;
        var waitTime = 100;
        var taskCompleted = false;
        
        var timeoutID = setInterval(function () { 
            // Limit the number of calls.
            if (--tries <= 0) {
                window.clearTimeout(timeoutID);
                responseTextArea.val("The response was not available in the time allowed.");
                return;
            }

            // The "Operation-Location" in the response contains the URI to retrieve the recognized text.
            var operationLocation = jqXHR.getResponseHeader("Operation-Location");
            
            // Perform the second REST API call and get the response.
            $.ajax({
                url: operationLocation,
                
                // Request headers.
                beforeSend: function(jqXHR){
                    jqXHR.setRequestHeader("Content-Type","application/json");
                    jqXHR.setRequestHeader("Ocp-Apim-Subscription-Key",
                        encodeURIComponent($("#subscriptionKeyInput").val()));
                },
                
                type: "GET",
            })
            
            .done(function(data) {
                // If the result is not yet available, return.
                if (data.status && (data.status === "NotStarted" || data.status === "Running")) {
                    return;
                }
                
                // Show formatted JSON on webpage.
                responseTextArea.val(JSON.stringify(data, null, 2));
                
                // Indicate the task is complete and clear the timer.
                taskCompleted = true;
                window.clearTimeout(timeoutID);
            })
            
            .fail(function(jqXHR, textStatus, errorThrown) {
                // Indicate the task is complete and clear the timer.
                taskCompleted = true;
                window.clearTimeout(timeoutID);
                
                // Display error message.
                var errorString = (errorThrown === "") ? "Error. " : errorThrown + " (" + jqXHR.status + "): ";
                errorString += (jqXHR.responseText === "") ? "" : (jQuery.parseJSON(jqXHR.responseText).message) ? 
                    jQuery.parseJSON(jqXHR.responseText).message : jQuery.parseJSON(jqXHR.responseText).error.message;
                alert(errorString);
            });
        }, waitTime);
    })
    
    .fail(function(jqXHR, textStatus, errorThrown) {
        // Put the JSON description into the text area.
        responseTextArea.val(JSON.stringify(jqXHR, null, 2));
        
        // Display error message.
        var errorString = (errorThrown === "") ? "Error. " : errorThrown + " (" + jqXHR.status + "): ";
        errorString += (jqXHR.responseText === "") ? "" : (jQuery.parseJSON(jqXHR.responseText).message) ? 
            jQuery.parseJSON(jqXHR.responseText).message : jQuery.parseJSON(jqXHR.responseText).error.message;
        alert(errorString);
    });
}
```

### <a name="handwriting-recognition-step-3-run-the-application"></a><span data-ttu-id="0c203-218">Handwriting Recognition step 3: Run the application</span><span class="sxs-lookup"><span data-stu-id="0c203-218">Handwriting Recognition step 3: Run the application</span></span>

<span data-ttu-id="0c203-219">Save the **handwriting.html** file and open it in a Web browser.</span><span class="sxs-lookup"><span data-stu-id="0c203-219">Save the **handwriting.html** file and open it in a Web browser.</span></span> <span data-ttu-id="0c203-220">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span><span class="sxs-lookup"><span data-stu-id="0c203-220">Put your subscription key into the **Subscription Key** field and verify that you are using the correct region in **Subscription Region**.</span></span> <span data-ttu-id="0c203-221">Enter a URL to an image of text to read, then click the **Read Image** button to analyze an image and see the result.</span><span class="sxs-lookup"><span data-stu-id="0c203-221">Enter a URL to an image of text to read, then click the **Read Image** button to analyze an image and see the result.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c203-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c203-222">Next steps</span></span>

- [<span data-ttu-id="0c203-223">Computer Vision API C&#35; Tutorial</span><span class="sxs-lookup"><span data-stu-id="0c203-223">Computer Vision API C&#35; Tutorial</span></span>](CSharpTutorial.md)
- [<span data-ttu-id="0c203-224">Computer Vision API Python Tutorial</span><span class="sxs-lookup"><span data-stu-id="0c203-224">Computer Vision API Python Tutorial</span></span>](PythonTutorial.md)
