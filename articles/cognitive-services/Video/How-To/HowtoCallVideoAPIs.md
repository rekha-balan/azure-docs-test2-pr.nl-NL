---
title: Call Video APIs in Microsoft Cognitive Services | Microsoft Docs
description: Get guidance for calling Video APIs, with samples in C# using the Video API client library.
services: cognitive-services
author: CYokel
manager: ytkuo
ms.service: cognitive-services
ms.technology: video
ms.topic: article
ms.date: 01/20/2017
ms.author: chbryant
ms.openlocfilehash: c5c97c3f70dac65c8c3547bcb43688ef9fddda92
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563617"
---
# <a name="how-to-call-video-apis"></a><span data-ttu-id="34154-103">How to Call Video APIs</span><span class="sxs-lookup"><span data-stu-id="34154-103">How to Call Video APIs</span></span>


<span data-ttu-id="34154-104">The samples are written in C# using the Video API client library.</span><span class="sxs-lookup"><span data-stu-id="34154-104">The samples are written in C# using the Video API client library.</span></span>

## <a name="concepts"></a><span data-ttu-id="34154-105">Concepts</span><span class="sxs-lookup"><span data-stu-id="34154-105">Concepts</span></span> 
<span data-ttu-id="34154-106">If you are not familiar with any of the following concepts in this guide, please refer to the definitions in our [glossary](../Glossary.md) at any time.</span><span class="sxs-lookup"><span data-stu-id="34154-106">If you are not familiar with any of the following concepts in this guide, please refer to the definitions in our [glossary](../Glossary.md) at any time.</span></span>

* <span data-ttu-id="34154-107">Stabilization</span><span class="sxs-lookup"><span data-stu-id="34154-107">Stabilization</span></span>
* <span data-ttu-id="34154-108">Face Detection and Tracking</span><span class="sxs-lookup"><span data-stu-id="34154-108">Face Detection and Tracking</span></span>
* <span data-ttu-id="34154-109">Motion Detection</span><span class="sxs-lookup"><span data-stu-id="34154-109">Motion Detection</span></span>

## <a name="preparation"></a><span data-ttu-id="34154-110">Preparation</span><span class="sxs-lookup"><span data-stu-id="34154-110">Preparation</span></span> 
<span data-ttu-id="34154-111">In the below examples the following features are demonstrated:</span><span class="sxs-lookup"><span data-stu-id="34154-111">In the below examples the following features are demonstrated:</span></span>
* <span data-ttu-id="34154-112">Creating a stabilized video from a shaky video</span><span class="sxs-lookup"><span data-stu-id="34154-112">Creating a stabilized video from a shaky video</span></span>
* <span data-ttu-id="34154-113">Analyzing faces detected in a video and outputting the corresponding JSON</span><span class="sxs-lookup"><span data-stu-id="34154-113">Analyzing faces detected in a video and outputting the corresponding JSON</span></span>
* <span data-ttu-id="34154-114">Analyzing motion detected in a video and outputting the corresponding JSON</span><span class="sxs-lookup"><span data-stu-id="34154-114">Analyzing motion detected in a video and outputting the corresponding JSON</span></span>

<span data-ttu-id="34154-115">In order to implement these features, you will need a video with the below specified characteristics for each of the features you want to try.</span><span class="sxs-lookup"><span data-stu-id="34154-115">In order to implement these features, you will need a video with the below specified characteristics for each of the features you want to try.</span></span>
* <span data-ttu-id="34154-116">For stabilization: A video that is shaky or jittery.</span><span class="sxs-lookup"><span data-stu-id="34154-116">For stabilization: A video that is shaky or jittery.</span></span>
* <span data-ttu-id="34154-117">For face detection and tracking: A video where people's faces are facing the camera.</span><span class="sxs-lookup"><span data-stu-id="34154-117">For face detection and tracking: A video where people's faces are facing the camera.</span></span>
* <span data-ttu-id="34154-118">For motion detection: A video with a stationary background and some movement in the foreground.</span><span class="sxs-lookup"><span data-stu-id="34154-118">For motion detection: A video with a stationary background and some movement in the foreground.</span></span>

## <a name="step1"></a><span data-ttu-id="34154-119">Step 1: Authorize the API call</span><span class="sxs-lookup"><span data-stu-id="34154-119">Step 1: Authorize the API call</span></span> 
<span data-ttu-id="34154-120">Every call to the Video API requires a subscription key.</span><span class="sxs-lookup"><span data-stu-id="34154-120">Every call to the Video API requires a subscription key.</span></span> <span data-ttu-id="34154-121">This key needs to be either passed through a query string parameter or specified in the request header.</span><span class="sxs-lookup"><span data-stu-id="34154-121">This key needs to be either passed through a query string parameter or specified in the request header.</span></span> <span data-ttu-id="34154-122">To pass the subscription key through a query string, refer to the Video API request URL below as an example:</span><span class="sxs-lookup"><span data-stu-id="34154-122">To pass the subscription key through a query string, refer to the Video API request URL below as an example:</span></span>

```

https://westus.api.cognitive.microsoft.com/video/v1.0/stabilize&subscription-key=<Your subscription key>
  
```

<span data-ttu-id="34154-123">As an alternative, the subscription key can also be specified in the HTTP request header:</span><span class="sxs-lookup"><span data-stu-id="34154-123">As an alternative, the subscription key can also be specified in the HTTP request header:</span></span>
```

ocp-apim-subscription-key: <Your subscription key>
  
```

<span data-ttu-id="34154-124">When using a client library, the subscription key is passed in through the constructor of the VideoServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="34154-124">When using a client library, the subscription key is passed in through the constructor of the VideoServiceClient class.</span></span> <span data-ttu-id="34154-125">For example:</span><span class="sxs-lookup"><span data-stu-id="34154-125">For example:</span></span>

```

var videoServiceClient = new VideoServiceClient("Your subscription key");

```
 
<span data-ttu-id="34154-126">To obtain a subscription key, see [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="34154-126">To obtain a subscription key, see [Subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span>

## <a name="step2"></a><span data-ttu-id="34154-127">Step 2: Upload a video to the service and check the status</span><span class="sxs-lookup"><span data-stu-id="34154-127">Step 2: Upload a video to the service and check the status</span></span>

<span data-ttu-id="34154-128">The most basic way to perform any of the Video API calls is by uploading a video directly.</span><span class="sxs-lookup"><span data-stu-id="34154-128">The most basic way to perform any of the Video API calls is by uploading a video directly.</span></span> <span data-ttu-id="34154-129">This is done by sending a "POST" request with application/octet-stream content type together with the data read from a video file.</span><span class="sxs-lookup"><span data-stu-id="34154-129">This is done by sending a "POST" request with application/octet-stream content type together with the data read from a video file.</span></span> <span data-ttu-id="34154-130">The maximum size of the video is 100MB.</span><span class="sxs-lookup"><span data-stu-id="34154-130">The maximum size of the video is 100MB.</span></span>

<span data-ttu-id="34154-131">Using the client library, stabilization by means of uploading is done by passing in a stream object.</span><span class="sxs-lookup"><span data-stu-id="34154-131">Using the client library, stabilization by means of uploading is done by passing in a stream object.</span></span> <span data-ttu-id="34154-132">See the example below:</span><span class="sxs-lookup"><span data-stu-id="34154-132">See the example below:</span></span>

```

Operation videoOperation;
using (var fs = new FileStream(@"C:\Videos\Sample.mp4", FileMode.Open))
{
      videoOperation = await videoServiceClient.CreateOperationAsync(fs, OperationType.Stabilize);
}
  
```

<span data-ttu-id="34154-133">*Please note that the CreateOperationAsync method of VideoServiceClient is async. The calling method should be marked as async as well in order to use the await clause.*</span><span class="sxs-lookup"><span data-stu-id="34154-133">*Please note that the CreateOperationAsync method of VideoServiceClient is async. The calling method should be marked as async as well in order to use the await clause.*</span></span>

<span data-ttu-id="34154-134">If the video is already on the web and has a public URL, Video APIs can be accessed by providing the URL.</span><span class="sxs-lookup"><span data-stu-id="34154-134">If the video is already on the web and has a public URL, Video APIs can be accessed by providing the URL.</span></span> <span data-ttu-id="34154-135">In this example, the request body will be a JSON string which contains the URL.</span><span class="sxs-lookup"><span data-stu-id="34154-135">In this example, the request body will be a JSON string which contains the URL.</span></span>

<span data-ttu-id="34154-136">Using the client library, stabilization by means of an URL can easily be executed using another overload of the CreateOperationAsync method.</span><span class="sxs-lookup"><span data-stu-id="34154-136">Using the client library, stabilization by means of an URL can easily be executed using another overload of the CreateOperationAsync method.</span></span>


```

var videoUrl = "http://www.example.com/sample.mp4";
Operation videoOperation = await videoServiceClient.CreateOperationAsync(videoUrl, OperationType.Stabilize);

```

<span data-ttu-id="34154-137">This upload method will be the same for all the Video API calls.</span><span class="sxs-lookup"><span data-stu-id="34154-137">This upload method will be the same for all the Video API calls.</span></span> <span data-ttu-id="34154-138">The only difference will be the POST calls to the various APIs you want to execute (POST stabilize, trackFace, detectMotion).</span><span class="sxs-lookup"><span data-stu-id="34154-138">The only difference will be the POST calls to the various APIs you want to execute (POST stabilize, trackFace, detectMotion).</span></span>

<span data-ttu-id="34154-139">Once you have uploaded a video to the Video API call you want to execute, the next operation you will want to perform is to check its status.</span><span class="sxs-lookup"><span data-stu-id="34154-139">Once you have uploaded a video to the Video API call you want to execute, the next operation you will want to perform is to check its status.</span></span> <span data-ttu-id="34154-140">Because video files are usually larger and more diverse than other files, users can expect a long processing time at this step.</span><span class="sxs-lookup"><span data-stu-id="34154-140">Because video files are usually larger and more diverse than other files, users can expect a long processing time at this step.</span></span> <span data-ttu-id="34154-141">The time depends on the size and the length of the file.</span><span class="sxs-lookup"><span data-stu-id="34154-141">The time depends on the size and the length of the file.</span></span> 

<span data-ttu-id="34154-142">Using the client library, you can retrieve the operation status and result using the GetOperationResultAsync method.</span><span class="sxs-lookup"><span data-stu-id="34154-142">Using the client library, you can retrieve the operation status and result using the GetOperationResultAsync method.</span></span>


```

var operationResult = await videoServiceClient.GetOperationResultAsync(videoOperation);

```

<span data-ttu-id="34154-143">Typically, the client side should periodically retrieve the operation status until the status is shown as “Succeeded” or “Failed”.</span><span class="sxs-lookup"><span data-stu-id="34154-143">Typically, the client side should periodically retrieve the operation status until the status is shown as “Succeeded” or “Failed”.</span></span>


```

OperationResult operationResult;
while (true)
{
      operationResult = await videoServiceClient.GetOperationResultAsync(videoOperation);
      if (operationResult.Status == OperationStatus.Succeeded || operationResult.Status == OperationStatus.Failed)
      {
           break;
      }

      Task.Delay(30000).Wait();
}

```

<span data-ttu-id="34154-144">When the status of OperationResult is shown as “Succeeded”, depending on the video operation you created, the result can be retrieved in the following ways:</span><span class="sxs-lookup"><span data-stu-id="34154-144">When the status of OperationResult is shown as “Succeeded”, depending on the video operation you created, the result can be retrieved in the following ways:</span></span>  

<span data-ttu-id="34154-145">Video Operation</span><span class="sxs-lookup"><span data-stu-id="34154-145">Video Operation</span></span>  | <span data-ttu-id="34154-146">How to retrieve results?</span><span class="sxs-lookup"><span data-stu-id="34154-146">How to retrieve results?</span></span>  | <span data-ttu-id="34154-147">Sample code</span><span class="sxs-lookup"><span data-stu-id="34154-147">Sample code</span></span>  
---------|---------|---------
<span data-ttu-id="34154-148">Stabilization</span><span class="sxs-lookup"><span data-stu-id="34154-148">Stabilization</span></span>   |  <span data-ttu-id="34154-149">The result (as a video file) can be retrieved from the URL specified in the ResourceLocation field of the OperationResult instance.</span><span class="sxs-lookup"><span data-stu-id="34154-149">The result (as a video file) can be retrieved from the URL specified in the ResourceLocation field of the OperationResult instance.</span></span>  |  <span data-ttu-id="34154-150">var stabilziationResultUrl = operationResult.ResourceLocation;</span><span class="sxs-lookup"><span data-stu-id="34154-150">var stabilziationResultUrl = operationResult.ResourceLocation;</span></span>     
<span data-ttu-id="34154-151">Face Detection/Tracking and Motion Detection</span><span class="sxs-lookup"><span data-stu-id="34154-151">Face Detection/Tracking and Motion Detection</span></span>|<span data-ttu-id="34154-152">The result (as a JSON string) is available in the ProcessingResult field of OperationResult.</span><span class="sxs-lookup"><span data-stu-id="34154-152">The result (as a JSON string) is available in the ProcessingResult field of OperationResult.</span></span> |<span data-ttu-id="34154-153">var motionDetectionJsonString = operationResult.ProcessingResult;</span><span class="sxs-lookup"><span data-stu-id="34154-153">var motionDetectionJsonString = operationResult.ProcessingResult;</span></span>

## <a name="step3"></a><span data-ttu-id="34154-154">Step 3: Retrieving video output files for stabilization</span><span class="sxs-lookup"><span data-stu-id="34154-154">Step 3: Retrieving video output files for stabilization</span></span>  
     
<span data-ttu-id="34154-155">The output from the Stabilization Video API is stabilized in MP4 video format.</span><span class="sxs-lookup"><span data-stu-id="34154-155">The output from the Stabilization Video API is stabilized in MP4 video format.</span></span> <span data-ttu-id="34154-156">Once your video output is ready, as informed by the GetVideoOperationResultAsync method, you can download your video using the GetResultVideoAsync method.</span><span class="sxs-lookup"><span data-stu-id="34154-156">Once your video output is ready, as informed by the GetVideoOperationResultAsync method, you can download your video using the GetResultVideoAsync method.</span></span>

```

var videoStream = await videoServiceClient.GetResultVideoAsync(resultUrl);
using (var fileStream = File.Create(outputFile))
{
      videoStream.CopyTo(fileStream);
}

```

## <a name="step4"></a><span data-ttu-id="34154-157">Step 4: Retrieving and understanding the face detection and tracking JSON output</span><span class="sxs-lookup"><span data-stu-id="34154-157">Step 4: Retrieving and understanding the face detection and tracking JSON output</span></span>
<span data-ttu-id="34154-158">For the face detection and tracking operation, the output result contains the metadata from the faces within the given file in JSON format.</span><span class="sxs-lookup"><span data-stu-id="34154-158">For the face detection and tracking operation, the output result contains the metadata from the faces within the given file in JSON format.</span></span> 

<span data-ttu-id="34154-159">As explained in Step 2, the JSON output is available in the ProcessingResult field of OperationResult, when its status is shown as “Succeeded”.</span><span class="sxs-lookup"><span data-stu-id="34154-159">As explained in Step 2, the JSON output is available in the ProcessingResult field of OperationResult, when its status is shown as “Succeeded”.</span></span>

<span data-ttu-id="34154-160">The face detection and tracking JSON includes the following attributes:</span><span class="sxs-lookup"><span data-stu-id="34154-160">The face detection and tracking JSON includes the following attributes:</span></span>  


<span data-ttu-id="34154-161">Attribute</span><span class="sxs-lookup"><span data-stu-id="34154-161">Attribute</span></span>  |<span data-ttu-id="34154-162">Description</span><span class="sxs-lookup"><span data-stu-id="34154-162">Description</span></span>  
---------|---------
<span data-ttu-id="34154-163">Version</span><span class="sxs-lookup"><span data-stu-id="34154-163">Version</span></span>     |   <span data-ttu-id="34154-164">Refers to the version of the Video API JSON.</span><span class="sxs-lookup"><span data-stu-id="34154-164">Refers to the version of the Video API JSON.</span></span>      
<span data-ttu-id="34154-165">Timescale</span><span class="sxs-lookup"><span data-stu-id="34154-165">Timescale</span></span>    |   <span data-ttu-id="34154-166">“Ticks” per second of the video.</span><span class="sxs-lookup"><span data-stu-id="34154-166">“Ticks” per second of the video.</span></span>     
<span data-ttu-id="34154-167">Offset</span><span class="sxs-lookup"><span data-stu-id="34154-167">Offset</span></span>     |     <span data-ttu-id="34154-168">The time offset for timestamps.</span><span class="sxs-lookup"><span data-stu-id="34154-168">The time offset for timestamps.</span></span> <span data-ttu-id="34154-169">In version 1.0 of Video APIs, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="34154-169">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="34154-170">In future supported scenarios, this value may change.</span><span class="sxs-lookup"><span data-stu-id="34154-170">In future supported scenarios, this value may change.</span></span>    
<span data-ttu-id="34154-171">Framerate</span><span class="sxs-lookup"><span data-stu-id="34154-171">Framerate</span></span>    |   <span data-ttu-id="34154-172">Frames per second of the video.</span><span class="sxs-lookup"><span data-stu-id="34154-172">Frames per second of the video.</span></span>      
<span data-ttu-id="34154-173">Fragments</span><span class="sxs-lookup"><span data-stu-id="34154-173">Fragments</span></span>    |    <span data-ttu-id="34154-174">The metadata is cut up into different smaller pieces called fragments.</span><span class="sxs-lookup"><span data-stu-id="34154-174">The metadata is cut up into different smaller pieces called fragments.</span></span> <span data-ttu-id="34154-175">Each fragment contains a start, duration, interval number, and event(s).</span><span class="sxs-lookup"><span data-stu-id="34154-175">Each fragment contains a start, duration, interval number, and event(s).</span></span>     
<span data-ttu-id="34154-176">Start</span><span class="sxs-lookup"><span data-stu-id="34154-176">Start</span></span>    |    <span data-ttu-id="34154-177">The start time of the first event, in ticks.</span><span class="sxs-lookup"><span data-stu-id="34154-177">The start time of the first event, in ticks.</span></span>     
<span data-ttu-id="34154-178">Duration</span><span class="sxs-lookup"><span data-stu-id="34154-178">Duration</span></span>    |    <span data-ttu-id="34154-179">The length of the fragment, in ticks.</span><span class="sxs-lookup"><span data-stu-id="34154-179">The length of the fragment, in ticks.</span></span>     
<span data-ttu-id="34154-180">Interval</span><span class="sxs-lookup"><span data-stu-id="34154-180">Interval</span></span>     |     <span data-ttu-id="34154-181">The length of each event within the fragment, in ticks.</span><span class="sxs-lookup"><span data-stu-id="34154-181">The length of each event within the fragment, in ticks.</span></span>    
<span data-ttu-id="34154-182">Events</span><span class="sxs-lookup"><span data-stu-id="34154-182">Events</span></span>     |   <span data-ttu-id="34154-183">An array of events.</span><span class="sxs-lookup"><span data-stu-id="34154-183">An array of events.</span></span> <span data-ttu-id="34154-184">The outer array represents one interval of time.</span><span class="sxs-lookup"><span data-stu-id="34154-184">The outer array represents one interval of time.</span></span> <span data-ttu-id="34154-185">The inner array consists of 0 or more events that happened at that point in time.</span><span class="sxs-lookup"><span data-stu-id="34154-185">The inner array consists of 0 or more events that happened at that point in time.</span></span>      
<span data-ttu-id="34154-186">ID</span><span class="sxs-lookup"><span data-stu-id="34154-186">ID</span></span>    |   <span data-ttu-id="34154-187">Index of a face.</span><span class="sxs-lookup"><span data-stu-id="34154-187">Index of a face.</span></span> <span data-ttu-id="34154-188">A given individual should have the same ID throughout the overall video.</span><span class="sxs-lookup"><span data-stu-id="34154-188">A given individual should have the same ID throughout the overall video.</span></span> <span data-ttu-id="34154-189">Due to limitations in the detection algorithm (e.g. occlusion) this cannot be gauranteed.</span><span class="sxs-lookup"><span data-stu-id="34154-189">Due to limitations in the detection algorithm (e.g. occlusion) this cannot be gauranteed.</span></span>      
<span data-ttu-id="34154-190">X, Y</span><span class="sxs-lookup"><span data-stu-id="34154-190">X, Y</span></span>    |     <span data-ttu-id="34154-191">The upper left X and Y coordinates of the face bounding box in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="34154-191">The upper left X and Y coordinates of the face bounding box in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="34154-192">The X and Y coordinates are relative to the landscape orientation of a video.</span><span class="sxs-lookup"><span data-stu-id="34154-192">The X and Y coordinates are relative to the landscape orientation of a video.</span></span> <span data-ttu-id="34154-193">For example, if you have a portrait video, you will have to transpose the coordinates accordingly .</span><span class="sxs-lookup"><span data-stu-id="34154-193">For example, if you have a portrait video, you will have to transpose the coordinates accordingly .</span></span>   
<span data-ttu-id="34154-194">Width, Height</span><span class="sxs-lookup"><span data-stu-id="34154-194">Width, Height</span></span>    |    <span data-ttu-id="34154-195">The width and height of the face bounding box in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="34154-195">The width and height of the face bounding box in a normalized scale of 0.0 to 1.0.</span></span>     
<span data-ttu-id="34154-196">facesDetected</span><span class="sxs-lookup"><span data-stu-id="34154-196">facesDetected</span></span>    |    <span data-ttu-id="34154-197">Attribute is found at the end of the JSON results and summarizes the number of faces that the algorithm detected during the video.</span><span class="sxs-lookup"><span data-stu-id="34154-197">Attribute is found at the end of the JSON results and summarizes the number of faces that the algorithm detected during the video.</span></span> <span data-ttu-id="34154-198">Because the IDs can be reset if a face becomes undetected (e.g. face goes off screen, looks away), this number may not always equal the true number of faces in the video.</span><span class="sxs-lookup"><span data-stu-id="34154-198">Because the IDs can be reset if a face becomes undetected (e.g. face goes off screen, looks away), this number may not always equal the true number of faces in the video.</span></span> 

<span data-ttu-id="34154-199">The reason for formatting the JSON this way is to set up the APIs for future scenarios, where it will be important to retrieve metadata quickly and manage a large stream of results.</span><span class="sxs-lookup"><span data-stu-id="34154-199">The reason for formatting the JSON this way is to set up the APIs for future scenarios, where it will be important to retrieve metadata quickly and manage a large stream of results.</span></span> <span data-ttu-id="34154-200">This formatting is using both the techniques of fragmentation (allowing you to break up the metadata in time-based portions, where you can download only what you need), and segmentation (allowing you to break up the events if they get too large).</span><span class="sxs-lookup"><span data-stu-id="34154-200">This formatting is using both the techniques of fragmentation (allowing you to break up the metadata in time-based portions, where you can download only what you need), and segmentation (allowing you to break up the events if they get too large).</span></span> <span data-ttu-id="34154-201">Some simple calculations can help you transform the data.</span><span class="sxs-lookup"><span data-stu-id="34154-201">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="34154-202">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and a framerate of 29.97 (frames/sec), then:</span><span class="sxs-lookup"><span data-stu-id="34154-202">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and a framerate of 29.97 (frames/sec), then:</span></span>
* <span data-ttu-id="34154-203">Start/Timescale = 2.1 seconds</span><span class="sxs-lookup"><span data-stu-id="34154-203">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="34154-204">Seconds x (Framerate/Timescale) = 63 frames</span><span class="sxs-lookup"><span data-stu-id="34154-204">Seconds x (Framerate/Timescale) = 63 frames</span></span>

<span data-ttu-id="34154-205">Below is a simple example of extracting the JSON into a per frame format for face detection and tracking:</span><span class="sxs-lookup"><span data-stu-id="34154-205">Below is a simple example of extracting the JSON into a per frame format for face detection and tracking:</span></span>

```

var faceDetectionTrackingResultJsonString = operationResult.ProcessingResult;
var faceDetecionTracking = JsonConvert.DeserializeObject<FaceDetectionResult>(faceDetectionTrackingResultJsonString, settings);

```

## <a name="step5"></a><span data-ttu-id="34154-206">Step 5: Retrieving and understanding the motion detection JSON output</span><span class="sxs-lookup"><span data-stu-id="34154-206">Step 5: Retrieving and understanding the motion detection JSON output</span></span>  

<span data-ttu-id="34154-207">You retrieve the motion detection JSON results in exactly the same way as with the face detection and tracking method.</span><span class="sxs-lookup"><span data-stu-id="34154-207">You retrieve the motion detection JSON results in exactly the same way as with the face detection and tracking method.</span></span> <span data-ttu-id="34154-208">Please see Step 4 to learn how to retrieve the results.</span><span class="sxs-lookup"><span data-stu-id="34154-208">Please see Step 4 to learn how to retrieve the results.</span></span>

<span data-ttu-id="34154-209">The motion detection JSON has similar concepts as the face detection and tracking JSON.</span><span class="sxs-lookup"><span data-stu-id="34154-209">The motion detection JSON has similar concepts as the face detection and tracking JSON.</span></span> <span data-ttu-id="34154-210">Because the motion detection JSON only needs to record when motion happened and the duration of motion, there are a few differences.</span><span class="sxs-lookup"><span data-stu-id="34154-210">Because the motion detection JSON only needs to record when motion happened and the duration of motion, there are a few differences.</span></span>  

<span data-ttu-id="34154-211">Attribute</span><span class="sxs-lookup"><span data-stu-id="34154-211">Attribute</span></span>  |<span data-ttu-id="34154-212">Description</span><span class="sxs-lookup"><span data-stu-id="34154-212">Description</span></span>  
---------|---------
<span data-ttu-id="34154-213">Version</span><span class="sxs-lookup"><span data-stu-id="34154-213">Version</span></span>     |   <span data-ttu-id="34154-214">Refers to the version of the Video API JSON.</span><span class="sxs-lookup"><span data-stu-id="34154-214">Refers to the version of the Video API JSON.</span></span>      
<span data-ttu-id="34154-215">Timescale</span><span class="sxs-lookup"><span data-stu-id="34154-215">Timescale</span></span>     |    <span data-ttu-id="34154-216">“Ticks” per second of the video.</span><span class="sxs-lookup"><span data-stu-id="34154-216">“Ticks” per second of the video.</span></span>     
<span data-ttu-id="34154-217">Offset</span><span class="sxs-lookup"><span data-stu-id="34154-217">Offset</span></span>     |     <span data-ttu-id="34154-218">The time offset for timestamps.</span><span class="sxs-lookup"><span data-stu-id="34154-218">The time offset for timestamps.</span></span> <span data-ttu-id="34154-219">In version 1.0 of Video APIs, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="34154-219">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="34154-220">In future supported scenarios, this value may change.</span><span class="sxs-lookup"><span data-stu-id="34154-220">In future supported scenarios, this value may change.</span></span>    
<span data-ttu-id="34154-221">Framerate</span><span class="sxs-lookup"><span data-stu-id="34154-221">Framerate</span></span>     |   <span data-ttu-id="34154-222">Frames per second of the video.</span><span class="sxs-lookup"><span data-stu-id="34154-222">Frames per second of the video.</span></span>      
<span data-ttu-id="34154-223">Fragments</span><span class="sxs-lookup"><span data-stu-id="34154-223">Fragments</span></span>    |    <span data-ttu-id="34154-224">The metadata is cut up into smaller pieces called fragments.</span><span class="sxs-lookup"><span data-stu-id="34154-224">The metadata is cut up into smaller pieces called fragments.</span></span> <span data-ttu-id="34154-225">Each fragment contains a start, duration, interval number, and event(s).</span><span class="sxs-lookup"><span data-stu-id="34154-225">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="34154-226">A fragment with no events means that no motion was detected during that start time and duration.</span><span class="sxs-lookup"><span data-stu-id="34154-226">A fragment with no events means that no motion was detected during that start time and duration.</span></span>   
<span data-ttu-id="34154-227">Width, Height</span><span class="sxs-lookup"><span data-stu-id="34154-227">Width, Height</span></span>     |    <span data-ttu-id="34154-228">Refers to the width and height of the video in pixels.</span><span class="sxs-lookup"><span data-stu-id="34154-228">Refers to the width and height of the video in pixels.</span></span>     
<span data-ttu-id="34154-229">Regions</span><span class="sxs-lookup"><span data-stu-id="34154-229">Regions</span></span>    |    <span data-ttu-id="34154-230">Regions refer to the area(s) in your video where you care about motion.</span><span class="sxs-lookup"><span data-stu-id="34154-230">Regions refer to the area(s) in your video where you care about motion.</span></span>  <span data-ttu-id="34154-231">**1. ID** represents the region area.</span><span class="sxs-lookup"><span data-stu-id="34154-231">**1. ID** represents the region area.</span></span> <span data-ttu-id="34154-232">**2. TYPE** represents the shape of the region you are concerned about in regards to motion.</span><span class="sxs-lookup"><span data-stu-id="34154-232">**2. TYPE** represents the shape of the region you are concerned about in regards to motion.</span></span> <span data-ttu-id="34154-233">In this version, it is always a polygon.</span><span class="sxs-lookup"><span data-stu-id="34154-233">In this version, it is always a polygon.</span></span> <span data-ttu-id="34154-234">**3. The region** is defined by an array of polygon points, each point has X and Y coordinates in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="34154-234">**3. The region** is defined by an array of polygon points, each point has X and Y coordinates in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="34154-235">**4. The X and Y coordinates** are relative to the landscape orientation of a video.</span><span class="sxs-lookup"><span data-stu-id="34154-235">**4. The X and Y coordinates** are relative to the landscape orientation of a video.</span></span> <span data-ttu-id="34154-236">For example, if you have a portrait video, you will have to transpose the coordinates accordingly.</span><span class="sxs-lookup"><span data-stu-id="34154-236">For example, if you have a portrait video, you will have to transpose the coordinates accordingly.</span></span> 
<span data-ttu-id="34154-237">Start</span><span class="sxs-lookup"><span data-stu-id="34154-237">Start</span></span>     |     <span data-ttu-id="34154-238">The start time of the first event, in ticks.</span><span class="sxs-lookup"><span data-stu-id="34154-238">The start time of the first event, in ticks.</span></span>   
<span data-ttu-id="34154-239">Duration</span><span class="sxs-lookup"><span data-stu-id="34154-239">Duration</span></span>     |   <span data-ttu-id="34154-240">The length of the fragment, in ticks.</span><span class="sxs-lookup"><span data-stu-id="34154-240">The length of the fragment, in ticks.</span></span>      
<span data-ttu-id="34154-241">Interval</span><span class="sxs-lookup"><span data-stu-id="34154-241">Interval</span></span>    |   <span data-ttu-id="34154-242">The length of each event within the fragment, in ticks.</span><span class="sxs-lookup"><span data-stu-id="34154-242">The length of each event within the fragment, in ticks.</span></span>    
<span data-ttu-id="34154-243">Event</span><span class="sxs-lookup"><span data-stu-id="34154-243">Event</span></span>    |     <span data-ttu-id="34154-244">An of array of events.</span><span class="sxs-lookup"><span data-stu-id="34154-244">An of array of events.</span></span> <span data-ttu-id="34154-245">The outer array represents one interval of time.</span><span class="sxs-lookup"><span data-stu-id="34154-245">The outer array represents one interval of time.</span></span> <span data-ttu-id="34154-246">The inner array consists of 0 or more events that happened at that point in time.</span><span class="sxs-lookup"><span data-stu-id="34154-246">The inner array consists of 0 or more events that happened at that point in time.</span></span>  
<span data-ttu-id="34154-247">Type</span><span class="sxs-lookup"><span data-stu-id="34154-247">Type</span></span>    |    <span data-ttu-id="34154-248">In the current version, the integer 2 refers to when motion happened, integer 4 refers to when light changes happen.</span><span class="sxs-lookup"><span data-stu-id="34154-248">In the current version, the integer 2 refers to when motion happened, integer 4 refers to when light changes happen.</span></span>
<span data-ttu-id="34154-249">TypeName</span><span class="sxs-lookup"><span data-stu-id="34154-249">TypeName</span></span>    |    <span data-ttu-id="34154-250">Will be “motion” when Type is 2 and “light change” when Type is 4.</span><span class="sxs-lookup"><span data-stu-id="34154-250">Will be “motion” when Type is 2 and “light change” when Type is 4.</span></span> <span data-ttu-id="34154-251">(This is a string).</span><span class="sxs-lookup"><span data-stu-id="34154-251">(This is a string).</span></span>      
<span data-ttu-id="34154-252">Location</span><span class="sxs-lookup"><span data-stu-id="34154-252">Location</span></span>    |    <span data-ttu-id="34154-253">An array of motion locations indicating where motion happens.</span><span class="sxs-lookup"><span data-stu-id="34154-253">An array of motion locations indicating where motion happens.</span></span> <span data-ttu-id="34154-254">There will always be one location in this version.</span><span class="sxs-lookup"><span data-stu-id="34154-254">There will always be one location in this version.</span></span> <span data-ttu-id="34154-255">The motion location has dimensions in X, Y, Width, and Height.</span><span class="sxs-lookup"><span data-stu-id="34154-255">The motion location has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="34154-256">The X and Y coordinates represent the upper left hand X, Y coordinates of the location in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="34154-256">The X and Y coordinates represent the upper left hand X, Y coordinates of the location in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="34154-257">The width and height represent the size of the location in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="34154-257">The width and height represent the size of the location in a normalized scale of 0.0 to 1.0.</span></span> 

<span data-ttu-id="34154-258">Below is a simple example of extracting the JSON into a per frame motion detection result:</span><span class="sxs-lookup"><span data-stu-id="34154-258">Below is a simple example of extracting the JSON into a per frame motion detection result:</span></span>


```

var motionDetectionJsonString = operationResult.ProcessingResult;
var motionDetection = JsonConvert.DeserializeObject<MotionDetectionResult>(motionDetectionJsonString, settings);

```  

## <a name="summary"></a><span data-ttu-id="34154-259">Summary</span><span class="sxs-lookup"><span data-stu-id="34154-259">Summary</span></span>
<span data-ttu-id="34154-260">You have now learned about the functionalities of the Video API: how you can upload a video, check its status, retrieve a stabilized video, and retrieve face detection/tracking and motion detection metadata.</span><span class="sxs-lookup"><span data-stu-id="34154-260">You have now learned about the functionalities of the Video API: how you can upload a video, check its status, retrieve a stabilized video, and retrieve face detection/tracking and motion detection metadata.</span></span>

<span data-ttu-id="34154-261">For more information about API details, see the API reference guide “[Video API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/565d6516778daf15800928d5)”.</span><span class="sxs-lookup"><span data-stu-id="34154-261">For more information about API details, see the API reference guide “[Video API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/565d6516778daf15800928d5)”.</span></span>
 
---

 
