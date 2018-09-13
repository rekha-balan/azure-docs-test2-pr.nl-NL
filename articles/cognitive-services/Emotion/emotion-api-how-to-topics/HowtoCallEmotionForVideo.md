---
title: Call the Emotion API for Video | Microsoft Docs
description: Learn how to call the Emotion API for Video in Cognitive Services.
services: cognitive-services
author: anrothMSFT
manager: corncar
ms.service: cognitive-services
ms.component: emotion-api
ms.topic: article
ms.date: 02/06/2017
ms.author: anroth
ms.openlocfilehash: 0875013b2061a84e3e23ae90c1106382672fdca6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818784"
---
# <a name="how-to-call-emotion-api-for-video"></a><span data-ttu-id="a2209-103">How to Call Emotion API for Video</span><span class="sxs-lookup"><span data-stu-id="a2209-103">How to Call Emotion API for Video</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2209-104">Video API Preview will end on October 30th, 2017.</span><span class="sxs-lookup"><span data-stu-id="a2209-104">Video API Preview will end on October 30th, 2017.</span></span> <span data-ttu-id="a2209-105">Try the new [Video Indexer API Preview](https://azure.microsoft.com/services/cognitive-services/video-indexer/) to easily extract insights from videos and to enhance content discovery experiences, such as search results, by detecting spoken words, faces, characters, and emotions.</span><span class="sxs-lookup"><span data-stu-id="a2209-105">Try the new [Video Indexer API Preview](https://azure.microsoft.com/services/cognitive-services/video-indexer/) to easily extract insights from videos and to enhance content discovery experiences, such as search results, by detecting spoken words, faces, characters, and emotions.</span></span> <span data-ttu-id="a2209-106">[Learn more](https://docs.microsoft.com/azure/cognitive-services/video-indexer/video-indexer-overview).</span><span class="sxs-lookup"><span data-stu-id="a2209-106">[Learn more](https://docs.microsoft.com/azure/cognitive-services/video-indexer/video-indexer-overview).</span></span>

<span data-ttu-id="a2209-107">This guide demonstrates how to call Emotion API for Video.</span><span class="sxs-lookup"><span data-stu-id="a2209-107">This guide demonstrates how to call Emotion API for Video.</span></span> <span data-ttu-id="a2209-108">The samples are written in C# using the Emotion API for Video client library.</span><span class="sxs-lookup"><span data-stu-id="a2209-108">The samples are written in C# using the Emotion API for Video client library.</span></span>

### <span data-ttu-id="a2209-109"><a name="Prep">Preparation</a></span><span class="sxs-lookup"><span data-stu-id="a2209-109"><a name="Prep">Preparation</a></span></span> 
<span data-ttu-id="a2209-110">In order to use the Emotion API for Video, you will need a video that includes people, preferably video where the people are facing the camera.</span><span class="sxs-lookup"><span data-stu-id="a2209-110">In order to use the Emotion API for Video, you will need a video that includes people, preferably video where the people are facing the camera.</span></span>

### <span data-ttu-id="a2209-111"><a name="Step1">Step 1: Authorize the API call</a></span><span class="sxs-lookup"><span data-stu-id="a2209-111"><a name="Step1">Step 1: Authorize the API call</a></span></span> 
<span data-ttu-id="a2209-112">Every call to the Emotion API for Video requires a subscription key.</span><span class="sxs-lookup"><span data-stu-id="a2209-112">Every call to the Emotion API for Video requires a subscription key.</span></span> <span data-ttu-id="a2209-113">This key needs to be either passed through a query string parameter or specified in the request header.</span><span class="sxs-lookup"><span data-stu-id="a2209-113">This key needs to be either passed through a query string parameter or specified in the request header.</span></span> <span data-ttu-id="a2209-114">To pass the subscription key through a query string, refer to the request URL below for the Emotion API for Video as an example:</span><span class="sxs-lookup"><span data-stu-id="a2209-114">To pass the subscription key through a query string, refer to the request URL below for the Emotion API for Video as an example:</span></span>

```
https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognizeInVideo&subscription-key=<Your subscription key>
```

<span data-ttu-id="a2209-115">As an alternative, the subscription key can also be specified in the HTTP request header:</span><span class="sxs-lookup"><span data-stu-id="a2209-115">As an alternative, the subscription key can also be specified in the HTTP request header:</span></span>

```
ocp-apim-subscription-key: <Your subscription key>
```

<span data-ttu-id="a2209-116">When using a client library, the subscription key is passed in through the constructor of the VideoServiceClient class.</span><span class="sxs-lookup"><span data-stu-id="a2209-116">When using a client library, the subscription key is passed in through the constructor of the VideoServiceClient class.</span></span> <span data-ttu-id="a2209-117">For example:</span><span class="sxs-lookup"><span data-stu-id="a2209-117">For example:</span></span>

```
var emotionServiceClient = new emotionServiceClient("Your subscription key");
```
<span data-ttu-id="a2209-118">To obtain a subscription key, see [Subscriptions] (https://azure.microsoft.com/try/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="a2209-118">To obtain a subscription key, see [Subscriptions] (https://azure.microsoft.com/try/cognitive-services/).</span></span> 

### <span data-ttu-id="a2209-119"><a name="Step2">Step 2: Upload a video to the service and check the status</a></span><span class="sxs-lookup"><span data-stu-id="a2209-119"><a name="Step2">Step 2: Upload a video to the service and check the status</a></span></span>
<span data-ttu-id="a2209-120">The most basic way to perform any of the Emotion API for Video calls is by uploading a video directly.</span><span class="sxs-lookup"><span data-stu-id="a2209-120">The most basic way to perform any of the Emotion API for Video calls is by uploading a video directly.</span></span> <span data-ttu-id="a2209-121">This is done by sending a "POST" request with application/octet-stream content type together with the data read from a video file.</span><span class="sxs-lookup"><span data-stu-id="a2209-121">This is done by sending a "POST" request with application/octet-stream content type together with the data read from a video file.</span></span> <span data-ttu-id="a2209-122">The maximum size of the video is 100MB.</span><span class="sxs-lookup"><span data-stu-id="a2209-122">The maximum size of the video is 100MB.</span></span>

<span data-ttu-id="a2209-123">Using the client library, stabilization by means of uploading is done by passing in a stream object.</span><span class="sxs-lookup"><span data-stu-id="a2209-123">Using the client library, stabilization by means of uploading is done by passing in a stream object.</span></span> <span data-ttu-id="a2209-124">See the example below:</span><span class="sxs-lookup"><span data-stu-id="a2209-124">See the example below:</span></span>

```
Operation videoOperation;
using (var fs = new FileStream(@"C:\Videos\Sample.mp4", FileMode.Open))
{
      videoOperation = await videoServiceClient.CreateOperationAsync(fs, OperationType.recognizeInVideo);
}
```

<span data-ttu-id="a2209-125">Please note that the CreateOperationAsync method of VideoServiceClient is async.</span><span class="sxs-lookup"><span data-stu-id="a2209-125">Please note that the CreateOperationAsync method of VideoServiceClient is async.</span></span> <span data-ttu-id="a2209-126">The calling method should be marked as async as well in order to use the await clause.</span><span class="sxs-lookup"><span data-stu-id="a2209-126">The calling method should be marked as async as well in order to use the await clause.</span></span>
<span data-ttu-id="a2209-127">If the video is already on the web and has a public URL, Emotion API for Video can be accessed by providing the URL.</span><span class="sxs-lookup"><span data-stu-id="a2209-127">If the video is already on the web and has a public URL, Emotion API for Video can be accessed by providing the URL.</span></span> <span data-ttu-id="a2209-128">In this example, the request body will be a JSON string which contains the URL.</span><span class="sxs-lookup"><span data-stu-id="a2209-128">In this example, the request body will be a JSON string which contains the URL.</span></span>

<span data-ttu-id="a2209-129">Using the client library, stabilization by means of an URL can easily be executed using another overload of the CreateOperationAsync method.</span><span class="sxs-lookup"><span data-stu-id="a2209-129">Using the client library, stabilization by means of an URL can easily be executed using another overload of the CreateOperationAsync method.</span></span>


```
var videoUrl = "http://www.example.com/sample.mp4";
Operation videoOperation = await videoServiceClient.CreateOperationAsync(videoUrl, OperationType. recognizeInVideo);

```

<span data-ttu-id="a2209-130">This upload method will be the same for all the Emotion API for Video calls.</span><span class="sxs-lookup"><span data-stu-id="a2209-130">This upload method will be the same for all the Emotion API for Video calls.</span></span> 

<span data-ttu-id="a2209-131">Once you have uploaded a video, the next operation you will want to perform is to check its status.</span><span class="sxs-lookup"><span data-stu-id="a2209-131">Once you have uploaded a video, the next operation you will want to perform is to check its status.</span></span> <span data-ttu-id="a2209-132">Because video files are usually larger and more diverse than other files, users can expect a long processing time at this step.</span><span class="sxs-lookup"><span data-stu-id="a2209-132">Because video files are usually larger and more diverse than other files, users can expect a long processing time at this step.</span></span> <span data-ttu-id="a2209-133">The time depends on the size and the length of the file.</span><span class="sxs-lookup"><span data-stu-id="a2209-133">The time depends on the size and the length of the file.</span></span>

<span data-ttu-id="a2209-134">Using the client library, you can retrieve the operation status and result using the GetOperationResultAsync method.</span><span class="sxs-lookup"><span data-stu-id="a2209-134">Using the client library, you can retrieve the operation status and result using the GetOperationResultAsync method.</span></span>


```
var operationResult = await videoServiceClient.GetOperationResultAsync(videoOperation);

```
<span data-ttu-id="a2209-135">Typically, the client side should periodically retrieve the operation status until the status is shown as “Succeeded” or “Failed”.</span><span class="sxs-lookup"><span data-stu-id="a2209-135">Typically, the client side should periodically retrieve the operation status until the status is shown as “Succeeded” or “Failed”.</span></span>

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

<span data-ttu-id="a2209-136">When the status of VideoOperationResult is shown as “Succeeded” the result can be retrieved by casting the VideoOperationResult to a VideoOperationInfoResult<VideoAggregateRecognitionResult> and accessing the ProcessingResult field.</span><span class="sxs-lookup"><span data-stu-id="a2209-136">When the status of VideoOperationResult is shown as “Succeeded” the result can be retrieved by casting the VideoOperationResult to a VideoOperationInfoResult<VideoAggregateRecognitionResult> and accessing the ProcessingResult field.</span></span>

```
var emotionRecognitionJsonString = ((VideoOperationInfoResult<VideoAggregateRecognitionResult>)operationResult).ProcessingResult;
```

### <span data-ttu-id="a2209-137"><a name="Step3">Step 3: Retrieving and understanding the emotion recognition and tracking JSON output</a></span><span class="sxs-lookup"><span data-stu-id="a2209-137"><a name="Step3">Step 3: Retrieving and understanding the emotion recognition and tracking JSON output</a></span></span>

<span data-ttu-id="a2209-138">The output result contains the metadata from the faces within the given file in JSON format.</span><span class="sxs-lookup"><span data-stu-id="a2209-138">The output result contains the metadata from the faces within the given file in JSON format.</span></span>

<span data-ttu-id="a2209-139">As explained in Step 2, the JSON output is available in the ProcessingResult field of OperationResult, when its status is shown as “Succeeded”.</span><span class="sxs-lookup"><span data-stu-id="a2209-139">As explained in Step 2, the JSON output is available in the ProcessingResult field of OperationResult, when its status is shown as “Succeeded”.</span></span>

<span data-ttu-id="a2209-140">The face detection and tracking JSON includes the following attributes:</span><span class="sxs-lookup"><span data-stu-id="a2209-140">The face detection and tracking JSON includes the following attributes:</span></span>

<span data-ttu-id="a2209-141">Attribute</span><span class="sxs-lookup"><span data-stu-id="a2209-141">Attribute</span></span> | <span data-ttu-id="a2209-142">Description</span><span class="sxs-lookup"><span data-stu-id="a2209-142">Description</span></span>
-------------|-------------
<span data-ttu-id="a2209-143">Version</span><span class="sxs-lookup"><span data-stu-id="a2209-143">Version</span></span> | <span data-ttu-id="a2209-144">Refers to the version of the Emotion API for Video JSON.</span><span class="sxs-lookup"><span data-stu-id="a2209-144">Refers to the version of the Emotion API for Video JSON.</span></span>
<span data-ttu-id="a2209-145">Timescale</span><span class="sxs-lookup"><span data-stu-id="a2209-145">Timescale</span></span> | <span data-ttu-id="a2209-146">“Ticks” per second of the video.</span><span class="sxs-lookup"><span data-stu-id="a2209-146">“Ticks” per second of the video.</span></span>
<span data-ttu-id="a2209-147">Offset</span><span class="sxs-lookup"><span data-stu-id="a2209-147">Offset</span></span>  |<span data-ttu-id="a2209-148">The time offset for timestamps.</span><span class="sxs-lookup"><span data-stu-id="a2209-148">The time offset for timestamps.</span></span> <span data-ttu-id="a2209-149">In version 1.0 of Emotion API for Videos, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="a2209-149">In version 1.0 of Emotion API for Videos, this will always be 0.</span></span> <span data-ttu-id="a2209-150">In future supported scenarios, this value may change.</span><span class="sxs-lookup"><span data-stu-id="a2209-150">In future supported scenarios, this value may change.</span></span>
<span data-ttu-id="a2209-151">Framerate</span><span class="sxs-lookup"><span data-stu-id="a2209-151">Framerate</span></span> | <span data-ttu-id="a2209-152">Frames per second of the video.</span><span class="sxs-lookup"><span data-stu-id="a2209-152">Frames per second of the video.</span></span>
<span data-ttu-id="a2209-153">Fragments</span><span class="sxs-lookup"><span data-stu-id="a2209-153">Fragments</span></span>   | <span data-ttu-id="a2209-154">The metadata is cut up into different smaller pieces called fragments.</span><span class="sxs-lookup"><span data-stu-id="a2209-154">The metadata is cut up into different smaller pieces called fragments.</span></span> <span data-ttu-id="a2209-155">Each fragment contains a start, duration, interval number, and event(s).</span><span class="sxs-lookup"><span data-stu-id="a2209-155">Each fragment contains a start, duration, interval number, and event(s).</span></span>
<span data-ttu-id="a2209-156">Start</span><span class="sxs-lookup"><span data-stu-id="a2209-156">Start</span></span>   | <span data-ttu-id="a2209-157">The start time of the first event, in ticks.</span><span class="sxs-lookup"><span data-stu-id="a2209-157">The start time of the first event, in ticks.</span></span>
<span data-ttu-id="a2209-158">Duration</span><span class="sxs-lookup"><span data-stu-id="a2209-158">Duration</span></span> |  <span data-ttu-id="a2209-159">The length of the fragment, in ticks.</span><span class="sxs-lookup"><span data-stu-id="a2209-159">The length of the fragment, in ticks.</span></span>
<span data-ttu-id="a2209-160">Interval</span><span class="sxs-lookup"><span data-stu-id="a2209-160">Interval</span></span> |  <span data-ttu-id="a2209-161">The length of each event within the fragment, in ticks.</span><span class="sxs-lookup"><span data-stu-id="a2209-161">The length of each event within the fragment, in ticks.</span></span>
<span data-ttu-id="a2209-162">Events</span><span class="sxs-lookup"><span data-stu-id="a2209-162">Events</span></span>  | <span data-ttu-id="a2209-163">An array of events.</span><span class="sxs-lookup"><span data-stu-id="a2209-163">An array of events.</span></span> <span data-ttu-id="a2209-164">The outer array represents one interval of time.</span><span class="sxs-lookup"><span data-stu-id="a2209-164">The outer array represents one interval of time.</span></span> <span data-ttu-id="a2209-165">The inner array consists of 0 or more events that happened at that point in time.</span><span class="sxs-lookup"><span data-stu-id="a2209-165">The inner array consists of 0 or more events that happened at that point in time.</span></span>
<span data-ttu-id="a2209-166">windowFaceDistribution</span><span class="sxs-lookup"><span data-stu-id="a2209-166">windowFaceDistribution</span></span> |    <span data-ttu-id="a2209-167">Percent faces to have a particular emotion during the event.</span><span class="sxs-lookup"><span data-stu-id="a2209-167">Percent faces to have a particular emotion during the event.</span></span>
<span data-ttu-id="a2209-168">windowMeanScores</span><span class="sxs-lookup"><span data-stu-id="a2209-168">windowMeanScores</span></span> |  <span data-ttu-id="a2209-169">Mean scores for each emotion of the faces in the image.</span><span class="sxs-lookup"><span data-stu-id="a2209-169">Mean scores for each emotion of the faces in the image.</span></span>

<span data-ttu-id="a2209-170">The reason for formatting the JSON this way is to set up the APIs for future scenarios, where it will be important to retrieve metadata quickly and manage a large stream of results.</span><span class="sxs-lookup"><span data-stu-id="a2209-170">The reason for formatting the JSON this way is to set up the APIs for future scenarios, where it will be important to retrieve metadata quickly and manage a large stream of results.</span></span> <span data-ttu-id="a2209-171">This formatting is using both the techniques of fragmentation (allowing you to break up the metadata in time-based portions, where you can download only what you need), and segmentation (allowing you to break up the events if they get too large).</span><span class="sxs-lookup"><span data-stu-id="a2209-171">This formatting is using both the techniques of fragmentation (allowing you to break up the metadata in time-based portions, where you can download only what you need), and segmentation (allowing you to break up the events if they get too large).</span></span> <span data-ttu-id="a2209-172">Some simple calculations can help you transform the data.</span><span class="sxs-lookup"><span data-stu-id="a2209-172">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="a2209-173">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and a framerate of 29.97 (frames/sec), then:</span><span class="sxs-lookup"><span data-stu-id="a2209-173">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and a framerate of 29.97 (frames/sec), then:</span></span>

*   <span data-ttu-id="a2209-174">Start/Timescale = 2.1 seconds</span><span class="sxs-lookup"><span data-stu-id="a2209-174">Start/Timescale = 2.1 seconds</span></span>
*   <span data-ttu-id="a2209-175">Seconds x (Framerate/Timescale) = 63 frames</span><span class="sxs-lookup"><span data-stu-id="a2209-175">Seconds x (Framerate/Timescale) = 63 frames</span></span>

<span data-ttu-id="a2209-176">Below is a simple example of extracting the JSON into a per frame format for face detection and tracking:</span><span class="sxs-lookup"><span data-stu-id="a2209-176">Below is a simple example of extracting the JSON into a per frame format for face detection and tracking:</span></span>

```
var emotionRecognitionTrackingResultJsonString = operationResult.ProcessingResult;
var emotionRecognitionTracking = JsonConvert.DeserializeObject<EmotionRecognitionResult>(emotionRecognitionTrackingResultJsonString, settings);
```
<span data-ttu-id="a2209-177">Because emotions are smoothed over time, if you ever build a visualization to overlay your results on top the original video, subtract 250 milliseconds from the provided timestamps.</span><span class="sxs-lookup"><span data-stu-id="a2209-177">Because emotions are smoothed over time, if you ever build a visualization to overlay your results on top the original video, subtract 250 milliseconds from the provided timestamps.</span></span>

### <span data-ttu-id="a2209-178"><a name="Summary">Summary</a></span><span class="sxs-lookup"><span data-stu-id="a2209-178"><a name="Summary">Summary</a></span></span>
<span data-ttu-id="a2209-179">In this guide you have learned about the functionalities of the Emotion API for Video: how you can upload a video, check its status, retrieve emotion recognition metadata.</span><span class="sxs-lookup"><span data-stu-id="a2209-179">In this guide you have learned about the functionalities of the Emotion API for Video: how you can upload a video, check its status, retrieve emotion recognition metadata.</span></span>

<span data-ttu-id="a2209-180">For more information about API details, see the API reference guide “[Emotion API for Video Reference](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89/operations/56f8d40e1984551ec0a0984e)”.</span><span class="sxs-lookup"><span data-stu-id="a2209-180">For more information about API details, see the API reference guide “[Emotion API for Video Reference](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89/operations/56f8d40e1984551ec0a0984e)”.</span></span>
