---
title: Call the Emotion API for Video | Microsoft Docs
description: Learn how to call the Emotion API for Video in Cognitive Services.
services: cognitive-services
author: v-royhar
manager: yutkuo
ms.service: cognitive-services
ms.technology: emotion
ms.topic: article
ms.date: 02/06/2017
ms.author: anroth
ms.openlocfilehash: 87e0dd559591001466e492ae05bfcf1f136f6431
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563170"
---
# <a name="how-to-call-emotion-api-for-video"></a><span data-ttu-id="9b08b-103">How to Call Emotion API for Video</span><span class="sxs-lookup"><span data-stu-id="9b08b-103">How to Call Emotion API for Video</span></span>

<span data-ttu-id="9b08b-104">This guide demonstrates how to call Emotion API for Video.</span><span class="sxs-lookup"><span data-stu-id="9b08b-104">This guide demonstrates how to call Emotion API for Video.</span></span> <span data-ttu-id="9b08b-105">The samples are written in C# using the Emotion API for Video client library.</span><span class="sxs-lookup"><span data-stu-id="9b08b-105">The samples are written in C# using the Emotion API for Video client library.</span></span>

### <span data-ttu-id="9b08b-106"><a name="Prep">Preparation</a></span><span class="sxs-lookup"><span data-stu-id="9b08b-106"><a name="Prep">Preparation</a></span></span> 
<span data-ttu-id="9b08b-107">In order to use the Emotion API for Video, you will need a video that includes people, preferably video where the people are facing the camera.</span><span class="sxs-lookup"><span data-stu-id="9b08b-107">In order to use the Emotion API for Video, you will need a video that includes people, preferably video where the people are facing the camera.</span></span>

### <span data-ttu-id="9b08b-108"><a name="Step1">Step 1: Authorize the API call</a></span><span class="sxs-lookup"><span data-stu-id="9b08b-108"><a name="Step1">Step 1: Authorize the API call</a></span></span> 
<span data-ttu-id="9b08b-109">Every call to the Emotion API for Video requires a subscription key.</span><span class="sxs-lookup"><span data-stu-id="9b08b-109">Every call to the Emotion API for Video requires a subscription key.</span></span> <span data-ttu-id="9b08b-110">This key needs to be either passed through a query string parameter or specified in the request header.</span><span class="sxs-lookup"><span data-stu-id="9b08b-110">This key needs to be either passed through a query string parameter or specified in the request header.</span></span> <span data-ttu-id="9b08b-111">To pass the subscription key through a query string, refer to the request URL below for the Emotion API for Video as an example:</span><span class="sxs-lookup"><span data-stu-id="9b08b-111">To pass the subscription key through a query string, refer to the request URL below for the Emotion API for Video as an example:</span></span>

```
https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognizeInVideo&subscription-key=<Your subscription key>
```

<span data-ttu-id="9b08b-112">As an alternative, the subscription key can also be specified in the HTTP request header:</span><span class="sxs-lookup"><span data-stu-id="9b08b-112">As an alternative, the subscription key can also be specified in the HTTP request header:</span></span>

```
ocp-apim-subscription-key: <Your subscription key>
```

<span data-ttu-id="9b08b-113">When using a client library, the subscription key is passed in through the constructor of the VideoServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="9b08b-113">When using a client library, the subscription key is passed in through the constructor of the VideoServiceClient class.</span></span> <span data-ttu-id="9b08b-114">For example:</span><span class="sxs-lookup"><span data-stu-id="9b08b-114">For example:</span></span>

```
var emotionServiceClient = new emotionServiceClient("Your subscription key");
```
<span data-ttu-id="9b08b-115">To obtain a subscription key, see [Subscriptions] (https://www.microsoft.com/cognitive-services/en-us/sign-up).</span><span class="sxs-lookup"><span data-stu-id="9b08b-115">To obtain a subscription key, see [Subscriptions] (https://www.microsoft.com/cognitive-services/en-us/sign-up).</span></span> 

### <span data-ttu-id="9b08b-116"><a name="Step2">Step 2: Upload a video to the service and check the status</a></span><span class="sxs-lookup"><span data-stu-id="9b08b-116"><a name="Step2">Step 2: Upload a video to the service and check the status</a></span></span>
<span data-ttu-id="9b08b-117">The most basic way to perform any of the Emotion API for Video calls is by uploading a video directly.</span><span class="sxs-lookup"><span data-stu-id="9b08b-117">The most basic way to perform any of the Emotion API for Video calls is by uploading a video directly.</span></span> <span data-ttu-id="9b08b-118">This is done by sending a "POST" request with application/octet-stream content type together with the data read from a video file.</span><span class="sxs-lookup"><span data-stu-id="9b08b-118">This is done by sending a "POST" request with application/octet-stream content type together with the data read from a video file.</span></span> <span data-ttu-id="9b08b-119">The maximum size of the video is 100MB.</span><span class="sxs-lookup"><span data-stu-id="9b08b-119">The maximum size of the video is 100MB.</span></span>

<span data-ttu-id="9b08b-120">Using the client library, stabilization by means of uploading is done by passing in a stream object.</span><span class="sxs-lookup"><span data-stu-id="9b08b-120">Using the client library, stabilization by means of uploading is done by passing in a stream object.</span></span> <span data-ttu-id="9b08b-121">See the example below:</span><span class="sxs-lookup"><span data-stu-id="9b08b-121">See the example below:</span></span>

```
Operation videoOperation;
using (var fs = new FileStream(@"C:\Videos\Sample.mp4", FileMode.Open))
{
      videoOperation = await videoServiceClient.CreateOperationAsync(fs, OperationType.recognizeInVideo);
}
```

<span data-ttu-id="9b08b-122">Please note that the CreateOperationAsync method of VideoServiceClient is async.</span><span class="sxs-lookup"><span data-stu-id="9b08b-122">Please note that the CreateOperationAsync method of VideoServiceClient is async.</span></span> <span data-ttu-id="9b08b-123">The calling method should be marked as async as well in order to use the await clause.</span><span class="sxs-lookup"><span data-stu-id="9b08b-123">The calling method should be marked as async as well in order to use the await clause.</span></span>
<span data-ttu-id="9b08b-124">If the video is already on the web and has a public URL, Emotion API for Video can be accessed by providing the URL.</span><span class="sxs-lookup"><span data-stu-id="9b08b-124">If the video is already on the web and has a public URL, Emotion API for Video can be accessed by providing the URL.</span></span> <span data-ttu-id="9b08b-125">In this example, the request body will be a JSON string which contains the URL.</span><span class="sxs-lookup"><span data-stu-id="9b08b-125">In this example, the request body will be a JSON string which contains the URL.</span></span>

<span data-ttu-id="9b08b-126">Using the client library, stabilization by means of an URL can easily be executed using another overload of the CreateOperationAsync method.</span><span class="sxs-lookup"><span data-stu-id="9b08b-126">Using the client library, stabilization by means of an URL can easily be executed using another overload of the CreateOperationAsync method.</span></span>


```
var videoUrl = "http://www.example.com/sample.mp4";
Operation videoOperation = await videoServiceClient.CreateOperationAsync(videoUrl, OperationType. recognizeInVideo);

```

<span data-ttu-id="9b08b-127">This upload method will be the same for all the Emotion API for Video calls.</span><span class="sxs-lookup"><span data-stu-id="9b08b-127">This upload method will be the same for all the Emotion API for Video calls.</span></span> 

<span data-ttu-id="9b08b-128">Once you have uploaded a video, the next operation you will want to perform is to check its status.</span><span class="sxs-lookup"><span data-stu-id="9b08b-128">Once you have uploaded a video, the next operation you will want to perform is to check its status.</span></span> <span data-ttu-id="9b08b-129">Because video files are usually larger and more diverse than other files, users can expect a long processing time at this step.</span><span class="sxs-lookup"><span data-stu-id="9b08b-129">Because video files are usually larger and more diverse than other files, users can expect a long processing time at this step.</span></span> <span data-ttu-id="9b08b-130">The time depends on the size and the length of the file.</span><span class="sxs-lookup"><span data-stu-id="9b08b-130">The time depends on the size and the length of the file.</span></span>

<span data-ttu-id="9b08b-131">Using the client library, you can retrieve the operation status and result using the GetOperationResultAsync method.</span><span class="sxs-lookup"><span data-stu-id="9b08b-131">Using the client library, you can retrieve the operation status and result using the GetOperationResultAsync method.</span></span>


```
var operationResult = await videoServiceClient.GetOperationResultAsync(videoOperation);

```
<span data-ttu-id="9b08b-132">Typically, the client side should periodically retrieve the operation status until the status is shown as “Succeeded” or “Failed”.</span><span class="sxs-lookup"><span data-stu-id="9b08b-132">Typically, the client side should periodically retrieve the operation status until the status is shown as “Succeeded” or “Failed”.</span></span>

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

<span data-ttu-id="9b08b-133">When the status of VideoOperationResult is shown as “Succeeded” the result can be retrieved by casting the VideoOperationResult to a VideoOperationInfoResult<VideoAggregateRecognitionResult> and accessing the ProcessingResult field.</span><span class="sxs-lookup"><span data-stu-id="9b08b-133">When the status of VideoOperationResult is shown as “Succeeded” the result can be retrieved by casting the VideoOperationResult to a VideoOperationInfoResult<VideoAggregateRecognitionResult> and accessing the ProcessingResult field.</span></span>

```
var emotionRecognitionJsonString = ((VideoOperationInfoResult<VideoAggregateRecognitionResult>)operationResult).ProcessingResult;
```

### <span data-ttu-id="9b08b-134"><a name="Step3">Step 3: Retrieving and understanding the emotion recognition and tracking JSON output</a></span><span class="sxs-lookup"><span data-stu-id="9b08b-134"><a name="Step3">Step 3: Retrieving and understanding the emotion recognition and tracking JSON output</a></span></span>

<span data-ttu-id="9b08b-135">The output result contains the metadata from the faces within the given file in JSON format.</span><span class="sxs-lookup"><span data-stu-id="9b08b-135">The output result contains the metadata from the faces within the given file in JSON format.</span></span>

<span data-ttu-id="9b08b-136">As explained in Step 2, the JSON output is available in the ProcessingResult field of OperationResult, when its status is shown as “Succeeded”.</span><span class="sxs-lookup"><span data-stu-id="9b08b-136">As explained in Step 2, the JSON output is available in the ProcessingResult field of OperationResult, when its status is shown as “Succeeded”.</span></span>

<span data-ttu-id="9b08b-137">The face detection and tracking JSON includes the following attributes:</span><span class="sxs-lookup"><span data-stu-id="9b08b-137">The face detection and tracking JSON includes the following attributes:</span></span>

<span data-ttu-id="9b08b-138">Attribute</span><span class="sxs-lookup"><span data-stu-id="9b08b-138">Attribute</span></span> | <span data-ttu-id="9b08b-139">Description</span><span class="sxs-lookup"><span data-stu-id="9b08b-139">Description</span></span>
-------------|-------------
<span data-ttu-id="9b08b-140">Version</span><span class="sxs-lookup"><span data-stu-id="9b08b-140">Version</span></span> | <span data-ttu-id="9b08b-141">Refers to the version of the Emotion API for Video JSON.</span><span class="sxs-lookup"><span data-stu-id="9b08b-141">Refers to the version of the Emotion API for Video JSON.</span></span>
<span data-ttu-id="9b08b-142">Timescale</span><span class="sxs-lookup"><span data-stu-id="9b08b-142">Timescale</span></span> | <span data-ttu-id="9b08b-143">“Ticks” per second of the video.</span><span class="sxs-lookup"><span data-stu-id="9b08b-143">“Ticks” per second of the video.</span></span>
<span data-ttu-id="9b08b-144">Offset</span><span class="sxs-lookup"><span data-stu-id="9b08b-144">Offset</span></span>  |<span data-ttu-id="9b08b-145">The time offset for timestamps.</span><span class="sxs-lookup"><span data-stu-id="9b08b-145">The time offset for timestamps.</span></span> <span data-ttu-id="9b08b-146">In version 1.0 of Emotion API for Videos, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="9b08b-146">In version 1.0 of Emotion API for Videos, this will always be 0.</span></span> <span data-ttu-id="9b08b-147">In future supported scenarios, this value may change.</span><span class="sxs-lookup"><span data-stu-id="9b08b-147">In future supported scenarios, this value may change.</span></span>
<span data-ttu-id="9b08b-148">Framerate</span><span class="sxs-lookup"><span data-stu-id="9b08b-148">Framerate</span></span> | <span data-ttu-id="9b08b-149">Frames per second of the video.</span><span class="sxs-lookup"><span data-stu-id="9b08b-149">Frames per second of the video.</span></span>
<span data-ttu-id="9b08b-150">Fragments</span><span class="sxs-lookup"><span data-stu-id="9b08b-150">Fragments</span></span>   | <span data-ttu-id="9b08b-151">The metadata is cut up into different smaller pieces called fragments.</span><span class="sxs-lookup"><span data-stu-id="9b08b-151">The metadata is cut up into different smaller pieces called fragments.</span></span> <span data-ttu-id="9b08b-152">Each fragment contains a start, duration, interval number, and event(s).</span><span class="sxs-lookup"><span data-stu-id="9b08b-152">Each fragment contains a start, duration, interval number, and event(s).</span></span>
<span data-ttu-id="9b08b-153">Start</span><span class="sxs-lookup"><span data-stu-id="9b08b-153">Start</span></span>   | <span data-ttu-id="9b08b-154">The start time of the first event, in ticks.</span><span class="sxs-lookup"><span data-stu-id="9b08b-154">The start time of the first event, in ticks.</span></span>
<span data-ttu-id="9b08b-155">Duration</span><span class="sxs-lookup"><span data-stu-id="9b08b-155">Duration</span></span> |  <span data-ttu-id="9b08b-156">The length of the fragment, in ticks.</span><span class="sxs-lookup"><span data-stu-id="9b08b-156">The length of the fragment, in ticks.</span></span>
<span data-ttu-id="9b08b-157">Interval</span><span class="sxs-lookup"><span data-stu-id="9b08b-157">Interval</span></span> |  <span data-ttu-id="9b08b-158">The length of each event within the fragment, in ticks.</span><span class="sxs-lookup"><span data-stu-id="9b08b-158">The length of each event within the fragment, in ticks.</span></span>
<span data-ttu-id="9b08b-159">Events</span><span class="sxs-lookup"><span data-stu-id="9b08b-159">Events</span></span>  | <span data-ttu-id="9b08b-160">An array of events.</span><span class="sxs-lookup"><span data-stu-id="9b08b-160">An array of events.</span></span> <span data-ttu-id="9b08b-161">The outer array represents one interval of time.</span><span class="sxs-lookup"><span data-stu-id="9b08b-161">The outer array represents one interval of time.</span></span> <span data-ttu-id="9b08b-162">The inner array consists of 0 or more events that happened at that point in time.</span><span class="sxs-lookup"><span data-stu-id="9b08b-162">The inner array consists of 0 or more events that happened at that point in time.</span></span>
<span data-ttu-id="9b08b-163">windowFaceDistribution</span><span class="sxs-lookup"><span data-stu-id="9b08b-163">windowFaceDistribution</span></span> |    <span data-ttu-id="9b08b-164">Percent faces to have a particular emotion during the event.</span><span class="sxs-lookup"><span data-stu-id="9b08b-164">Percent faces to have a particular emotion during the event.</span></span>
<span data-ttu-id="9b08b-165">windowMeanScores</span><span class="sxs-lookup"><span data-stu-id="9b08b-165">windowMeanScores</span></span> |  <span data-ttu-id="9b08b-166">Mean scores for each emotion of the faces in the image.</span><span class="sxs-lookup"><span data-stu-id="9b08b-166">Mean scores for each emotion of the faces in the image.</span></span>

<span data-ttu-id="9b08b-167">The reason for formatting the JSON this way is to set up the APIs for future scenarios, where it will be important to retrieve metadata quickly and manage a large stream of results.</span><span class="sxs-lookup"><span data-stu-id="9b08b-167">The reason for formatting the JSON this way is to set up the APIs for future scenarios, where it will be important to retrieve metadata quickly and manage a large stream of results.</span></span> <span data-ttu-id="9b08b-168">This formatting is using both the techniques of fragmentation (allowing you to break up the metadata in time-based portions, where you can download only what you need), and segmentation (allowing you to break up the events if they get too large).</span><span class="sxs-lookup"><span data-stu-id="9b08b-168">This formatting is using both the techniques of fragmentation (allowing you to break up the metadata in time-based portions, where you can download only what you need), and segmentation (allowing you to break up the events if they get too large).</span></span> <span data-ttu-id="9b08b-169">Some simple calculations can help you transform the data.</span><span class="sxs-lookup"><span data-stu-id="9b08b-169">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="9b08b-170">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and a framerate of 29.97 (frames/sec), then:</span><span class="sxs-lookup"><span data-stu-id="9b08b-170">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and a framerate of 29.97 (frames/sec), then:</span></span>

*   <span data-ttu-id="9b08b-171">Start/Timescale = 2.1 seconds</span><span class="sxs-lookup"><span data-stu-id="9b08b-171">Start/Timescale = 2.1 seconds</span></span>
*   <span data-ttu-id="9b08b-172">Seconds x (Framerate/Timescale) = 63 frames</span><span class="sxs-lookup"><span data-stu-id="9b08b-172">Seconds x (Framerate/Timescale) = 63 frames</span></span>

<span data-ttu-id="9b08b-173">Below is a simple example of extracting the JSON into a per frame format for face detection and tracking:</span><span class="sxs-lookup"><span data-stu-id="9b08b-173">Below is a simple example of extracting the JSON into a per frame format for face detection and tracking:</span></span>

```
var emotionRecognitionTrackingResultJsonString = operationResult.ProcessingResult;
var emotionRecognitionTracking = JsonConvert.DeserializeObject<EmotionRecognitionResult>(emotionRecognitionTrackingResultJsonString, settings);
```
<span data-ttu-id="9b08b-174">Because emotions are smoothed over time, if you ever build a visualization to overlay your results on top the original video, subtract 250 milliseconds from the provided timestamps.</span><span class="sxs-lookup"><span data-stu-id="9b08b-174">Because emotions are smoothed over time, if you ever build a visualization to overlay your results on top the original video, subtract 250 milliseconds from the provided timestamps.</span></span>

### <span data-ttu-id="9b08b-175"><a name="Summary">Summary</a></span><span class="sxs-lookup"><span data-stu-id="9b08b-175"><a name="Summary">Summary</a></span></span>
<span data-ttu-id="9b08b-176">In this guide you have learned about the functionalities of the Emotion API for Video: how you can upload a video, check its status, retrieve emotion recognition metadata.</span><span class="sxs-lookup"><span data-stu-id="9b08b-176">In this guide you have learned about the functionalities of the Emotion API for Video: how you can upload a video, check its status, retrieve emotion recognition metadata.</span></span>

<span data-ttu-id="9b08b-177">For more information about API details, see the API reference guide “[Emotion API for Video Reference](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89/operations/56f8d40e1984551ec0a0984e)”.</span><span class="sxs-lookup"><span data-stu-id="9b08b-177">For more information about API details, see the API reference guide “[Emotion API for Video Reference](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89/operations/56f8d40e1984551ec0a0984e)”.</span></span>
