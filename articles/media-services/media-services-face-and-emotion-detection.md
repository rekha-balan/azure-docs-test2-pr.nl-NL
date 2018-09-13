---
title: Detect Face and Emotion with Azure Media Analytics | Microsoft Docs
description: This topic demonstrates how to detect faces and emotions with Azure Media Analytics.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/17/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 5a604f3538a0749f7f951926f451cc91504255d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564535"
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="3c5b0-103">Detect Face and Emotion with Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="3c5b0-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="3c5b0-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3c5b0-104">Overview</span></span>
<span data-ttu-id="3c5b0-105">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-105">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="3c5b0-106">This service contains two features:</span><span class="sxs-lookup"><span data-stu-id="3c5b0-106">This service contains two features:</span></span> 

* <span data-ttu-id="3c5b0-107">**Face detection**</span><span class="sxs-lookup"><span data-stu-id="3c5b0-107">**Face detection**</span></span>
  
    <span data-ttu-id="3c5b0-108">Face detection finds and tracks human faces within a video.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="3c5b0-109">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-109">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="3c5b0-110">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-110">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3c5b0-111">This services does not perform facial recognition.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-111">This services does not perform facial recognition.</span></span> <span data-ttu-id="3c5b0-112">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-112">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="3c5b0-113">**Emotion detection**</span><span class="sxs-lookup"><span data-stu-id="3c5b0-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="3c5b0-114">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-114">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="3c5b0-115">The **Azure Media Face Detector** MP is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-115">The **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="3c5b0-116">This topic gives details about  **Azure Media Face Detector** and shows how to use it with Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-116">This topic gives details about  **Azure Media Face Detector** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="3c5b0-117">Face Detector input files</span><span class="sxs-lookup"><span data-stu-id="3c5b0-117">Face Detector input files</span></span>
<span data-ttu-id="3c5b0-118">Video files.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-118">Video files.</span></span> <span data-ttu-id="3c5b0-119">Currently, the following formats are supported: MP4, MOV, and WMV.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-119">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="3c5b0-120">Face Detector output files</span><span class="sxs-lookup"><span data-stu-id="3c5b0-120">Face Detector output files</span></span>
<span data-ttu-id="3c5b0-121">The face detection and tracking API provides high precision face location detection and tracking that can detect up to 64 human faces in a video.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-121">The face detection and tracking API provides high precision face location detection and tracking that can detect up to 64 human faces in a video.</span></span> <span data-ttu-id="3c5b0-122">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) might not be as accurate.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-122">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="3c5b0-123">The detected and tracked faces are returned with coordinates (left, top, width, and height) indicating the location of faces in the image in pixels, as well as a face ID number indicating the tracking of that individual.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-123">The detected and tracked faces are returned with coordinates (left, top, width, and height) indicating the location of faces in the image in pixels, as well as a face ID number indicating the tracking of that individual.</span></span> <span data-ttu-id="3c5b0-124">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-124">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span></span>

### <a id="output_elements"></a><span data-ttu-id="3c5b0-125">Elements of the output JSON file</span><span class="sxs-lookup"><span data-stu-id="3c5b0-125">Elements of the output JSON file</span></span>
<span data-ttu-id="3c5b0-126">For the face detection and tracking operation, the output result contains the metadata from the faces within the given file in JSON format.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-126">For the face detection and tracking operation, the output result contains the metadata from the faces within the given file in JSON format.</span></span>

<span data-ttu-id="3c5b0-127">The face detection and tracking JSON includes the following attributes:</span><span class="sxs-lookup"><span data-stu-id="3c5b0-127">The face detection and tracking JSON includes the following attributes:</span></span>

| <span data-ttu-id="3c5b0-128">Element</span><span class="sxs-lookup"><span data-stu-id="3c5b0-128">Element</span></span> | <span data-ttu-id="3c5b0-129">Description</span><span class="sxs-lookup"><span data-stu-id="3c5b0-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c5b0-130">Version</span><span class="sxs-lookup"><span data-stu-id="3c5b0-130">Version</span></span> |<span data-ttu-id="3c5b0-131">This refers to the version of the Video API.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-131">This refers to the version of the Video API.</span></span> |
| <span data-ttu-id="3c5b0-132">Timescale</span><span class="sxs-lookup"><span data-stu-id="3c5b0-132">Timescale</span></span> |<span data-ttu-id="3c5b0-133">"Ticks" per second of the video.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-133">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="3c5b0-134">Offset</span><span class="sxs-lookup"><span data-stu-id="3c5b0-134">Offset</span></span> |<span data-ttu-id="3c5b0-135">This is the time offset for timestamps.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-135">This is the time offset for timestamps.</span></span> <span data-ttu-id="3c5b0-136">In version 1.0 of Video APIs, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-136">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="3c5b0-137">In future scenarios we support, this value may change.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-137">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="3c5b0-138">Framerate</span><span class="sxs-lookup"><span data-stu-id="3c5b0-138">Framerate</span></span> |<span data-ttu-id="3c5b0-139">Frames per second of the video.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-139">Frames per second of the video.</span></span> |
| <span data-ttu-id="3c5b0-140">Fragments</span><span class="sxs-lookup"><span data-stu-id="3c5b0-140">Fragments</span></span> |<span data-ttu-id="3c5b0-141">The metadata is chunked up into different segments called fragments.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-141">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="3c5b0-142">Each fragment contains a start, duration, interval number, and event(s).</span><span class="sxs-lookup"><span data-stu-id="3c5b0-142">Each fragment contains a start, duration, interval number, and event(s).</span></span> |
| <span data-ttu-id="3c5b0-143">Start</span><span class="sxs-lookup"><span data-stu-id="3c5b0-143">Start</span></span> |<span data-ttu-id="3c5b0-144">The start time of the first event in ‘ticks’.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-144">The start time of the first event in ‘ticks’.</span></span> |
| <span data-ttu-id="3c5b0-145">Duration</span><span class="sxs-lookup"><span data-stu-id="3c5b0-145">Duration</span></span> |<span data-ttu-id="3c5b0-146">The length of the fragment, in “ticks”.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-146">The length of the fragment, in “ticks”.</span></span> |
| <span data-ttu-id="3c5b0-147">Interval</span><span class="sxs-lookup"><span data-stu-id="3c5b0-147">Interval</span></span> |<span data-ttu-id="3c5b0-148">The interval of each event entry within the fragment, in “ticks”.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-148">The interval of each event entry within the fragment, in “ticks”.</span></span> |
| <span data-ttu-id="3c5b0-149">Events</span><span class="sxs-lookup"><span data-stu-id="3c5b0-149">Events</span></span> |<span data-ttu-id="3c5b0-150">Each event contains the faces detected and tracked within that time duration.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-150">Each event contains the faces detected and tracked within that time duration.</span></span> <span data-ttu-id="3c5b0-151">It is an array of array of events.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-151">It is an array of array of events.</span></span> <span data-ttu-id="3c5b0-152">The outer array represents one interval of time.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-152">The outer array represents one interval of time.</span></span> <span data-ttu-id="3c5b0-153">The inner array consists of 0 or more events that happened at that point in time.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-153">The inner array consists of 0 or more events that happened at that point in time.</span></span> <span data-ttu-id="3c5b0-154">An empty bracket [] means no faces were detected.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-154">An empty bracket [] means no faces were detected.</span></span> |
| <span data-ttu-id="3c5b0-155">ID</span><span class="sxs-lookup"><span data-stu-id="3c5b0-155">ID</span></span> |<span data-ttu-id="3c5b0-156">The ID of the face that is being tracked.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-156">The ID of the face that is being tracked.</span></span> <span data-ttu-id="3c5b0-157">This number may inadvertently change if a face becomes undetected.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-157">This number may inadvertently change if a face becomes undetected.</span></span> <span data-ttu-id="3c5b0-158">A given individual should have the same ID throughout the overall video, but this cannot be guaranteed due to limitations in the detection algorithm (occlusion, etc.)</span><span class="sxs-lookup"><span data-stu-id="3c5b0-158">A given individual should have the same ID throughout the overall video, but this cannot be guaranteed due to limitations in the detection algorithm (occlusion, etc.)</span></span> |
| <span data-ttu-id="3c5b0-159">X, Y</span><span class="sxs-lookup"><span data-stu-id="3c5b0-159">X, Y</span></span> |<span data-ttu-id="3c5b0-160">The upper left X and Y coordinates of the face bounding box in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-160">The upper left X and Y coordinates of the face bounding box in a normalized scale of 0.0 to 1.0.</span></span> <br/><span data-ttu-id="3c5b0-161">-X and Y coordinates are relative to landscape always, so if you have a portrait video (or upside-down, in the case of iOS), you'll have to transpose the coordinates accordingly.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-161">-X and Y coordinates are relative to landscape always, so if you have a portrait video (or upside-down, in the case of iOS), you'll have to transpose the coordinates accordingly.</span></span> |
| <span data-ttu-id="3c5b0-162">Width, Height</span><span class="sxs-lookup"><span data-stu-id="3c5b0-162">Width, Height</span></span> |<span data-ttu-id="3c5b0-163">The width and height of the face bounding box in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-163">The width and height of the face bounding box in a normalized scale of 0.0 to 1.0.</span></span> |
| <span data-ttu-id="3c5b0-164">facesDetected</span><span class="sxs-lookup"><span data-stu-id="3c5b0-164">facesDetected</span></span> |<span data-ttu-id="3c5b0-165">This is found at the end of the JSON results and summarizes the number of faces that the algorithm detected during the video.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-165">This is found at the end of the JSON results and summarizes the number of faces that the algorithm detected during the video.</span></span> <span data-ttu-id="3c5b0-166">Because the IDs can be reset inadvertently if a face becomes undetected (e.g. face goes off screen, looks away), this number may not always equal the true number of faces in the video.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-166">Because the IDs can be reset inadvertently if a face becomes undetected (e.g. face goes off screen, looks away), this number may not always equal the true number of faces in the video.</span></span> |

<span data-ttu-id="3c5b0-167">Face Detector uses techniques of fragmentation (where the metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where the events are broken up in case they get too large).</span><span class="sxs-lookup"><span data-stu-id="3c5b0-167">Face Detector uses techniques of fragmentation (where the metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where the events are broken up in case they get too large).</span></span> <span data-ttu-id="3c5b0-168">Some simple calculations can help you transform the data.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-168">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="3c5b0-169">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span><span class="sxs-lookup"><span data-stu-id="3c5b0-169">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="3c5b0-170">Start/Timescale = 2.1 seconds</span><span class="sxs-lookup"><span data-stu-id="3c5b0-170">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="3c5b0-171">Seconds x Framerate = 63 frames</span><span class="sxs-lookup"><span data-stu-id="3c5b0-171">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="3c5b0-172">Face detection input and output example</span><span class="sxs-lookup"><span data-stu-id="3c5b0-172">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="3c5b0-173">Input video</span><span class="sxs-lookup"><span data-stu-id="3c5b0-173">Input video</span></span>
[<span data-ttu-id="3c5b0-174">Input Video</span><span class="sxs-lookup"><span data-stu-id="3c5b0-174">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="3c5b0-175">Task configuration (preset)</span><span class="sxs-lookup"><span data-stu-id="3c5b0-175">Task configuration (preset)</span></span>
<span data-ttu-id="3c5b0-176">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-176">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="3c5b0-177">The following configuration preset is just for face detection.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-177">The following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="3c5b0-178">Attribute descriptions</span><span class="sxs-lookup"><span data-stu-id="3c5b0-178">Attribute descriptions</span></span>
| <span data-ttu-id="3c5b0-179">Attribute name</span><span class="sxs-lookup"><span data-stu-id="3c5b0-179">Attribute name</span></span> | <span data-ttu-id="3c5b0-180">Description</span><span class="sxs-lookup"><span data-stu-id="3c5b0-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c5b0-181">Mode</span><span class="sxs-lookup"><span data-stu-id="3c5b0-181">Mode</span></span> |<span data-ttu-id="3c5b0-182">Fast - fast processing speed, but less accurate (default).</span><span class="sxs-lookup"><span data-stu-id="3c5b0-182">Fast - fast processing speed, but less accurate (default).</span></span>|


### <a name="json-output"></a><span data-ttu-id="3c5b0-183">JSON output</span><span class="sxs-lookup"><span data-stu-id="3c5b0-183">JSON output</span></span>
<span data-ttu-id="3c5b0-184">The following example of JSON output was truncated.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-184">The following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="3c5b0-185">Emotion detection input and output example</span><span class="sxs-lookup"><span data-stu-id="3c5b0-185">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="3c5b0-186">Input video</span><span class="sxs-lookup"><span data-stu-id="3c5b0-186">Input video</span></span>
[<span data-ttu-id="3c5b0-187">Input Video</span><span class="sxs-lookup"><span data-stu-id="3c5b0-187">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="3c5b0-188">Task configuration (preset)</span><span class="sxs-lookup"><span data-stu-id="3c5b0-188">Task configuration (preset)</span></span>
<span data-ttu-id="3c5b0-189">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-189">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="3c5b0-190">The following configuration preset specifies to create JSON based on the emotion detection.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-190">The following configuration preset specifies to create JSON based on the emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="3c5b0-191">Attribute descriptions</span><span class="sxs-lookup"><span data-stu-id="3c5b0-191">Attribute descriptions</span></span>
| <span data-ttu-id="3c5b0-192">Attribute name</span><span class="sxs-lookup"><span data-stu-id="3c5b0-192">Attribute name</span></span> | <span data-ttu-id="3c5b0-193">Description</span><span class="sxs-lookup"><span data-stu-id="3c5b0-193">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c5b0-194">Mode</span><span class="sxs-lookup"><span data-stu-id="3c5b0-194">Mode</span></span> |<span data-ttu-id="3c5b0-195">Faces: Only face detection.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-195">Faces: Only face detection.</span></span><br/><span data-ttu-id="3c5b0-196">PerFaceEmotion: Return emotion independently for each face detection.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-196">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="3c5b0-197">AggregateEmotion: Return average emotion values for all faces in frame.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-197">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="3c5b0-198">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="3c5b0-198">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="3c5b0-199">Use if AggregateEmotion mode selected.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-199">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="3c5b0-200">Specifies the length of video used to produce each aggregate result, in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-200">Specifies the length of video used to produce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="3c5b0-201">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="3c5b0-201">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="3c5b0-202">Use if AggregateEmotion mode selected.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-202">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="3c5b0-203">Specifies with what frequency to produce aggregate results.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-203">Specifies with what frequency to produce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="3c5b0-204">Aggregate defaults</span><span class="sxs-lookup"><span data-stu-id="3c5b0-204">Aggregate defaults</span></span>
<span data-ttu-id="3c5b0-205">Below are recommended values for the aggregate window and interval settings.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-205">Below are recommended values for the aggregate window and interval settings.</span></span> <span data-ttu-id="3c5b0-206">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-206">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="3c5b0-207">Defaults(s)</span><span class="sxs-lookup"><span data-stu-id="3c5b0-207">Defaults(s)</span></span> | <span data-ttu-id="3c5b0-208">Min(s)</span><span class="sxs-lookup"><span data-stu-id="3c5b0-208">Min(s)</span></span> | <span data-ttu-id="3c5b0-209">Max(s)</span><span class="sxs-lookup"><span data-stu-id="3c5b0-209">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="3c5b0-210">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="3c5b0-210">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="3c5b0-211">0.5</span><span class="sxs-lookup"><span data-stu-id="3c5b0-211">0.5</span></span> |<span data-ttu-id="3c5b0-212">2</span><span class="sxs-lookup"><span data-stu-id="3c5b0-212">2</span></span> |<span data-ttu-id="3c5b0-213">0.25</span><span class="sxs-lookup"><span data-stu-id="3c5b0-213">0.25</span></span>|
| <span data-ttu-id="3c5b0-214">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="3c5b0-214">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="3c5b0-215">0.5</span><span class="sxs-lookup"><span data-stu-id="3c5b0-215">0.5</span></span> |<span data-ttu-id="3c5b0-216">1</span><span class="sxs-lookup"><span data-stu-id="3c5b0-216">1</span></span> |<span data-ttu-id="3c5b0-217">0.25</span><span class="sxs-lookup"><span data-stu-id="3c5b0-217">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="3c5b0-218">JSON output</span><span class="sxs-lookup"><span data-stu-id="3c5b0-218">JSON output</span></span>
<span data-ttu-id="3c5b0-219">JSON output for aggregate emotion (truncated):</span><span class="sxs-lookup"><span data-stu-id="3c5b0-219">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,


## <a name="limitations"></a><span data-ttu-id="3c5b0-220">Limitations</span><span class="sxs-lookup"><span data-stu-id="3c5b0-220">Limitations</span></span>
* <span data-ttu-id="3c5b0-221">The supported input video formats include MP4, MOV, and WMV.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-221">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="3c5b0-222">The detectable face size range is 24x24 to 2048x2048 pixels.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-222">The detectable face size range is 24x24 to 2048x2048 pixels.</span></span> <span data-ttu-id="3c5b0-223">The faces out of this range will not be detected.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-223">The faces out of this range will not be detected.</span></span>
* <span data-ttu-id="3c5b0-224">For each video, the maximum number of faces returned is 64.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-224">For each video, the maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="3c5b0-225">Some faces may not be detected due to technical challenges; e.g. very large face angles (head-pose), and large occlusion.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-225">Some faces may not be detected due to technical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="3c5b0-226">Frontal and near-frontal faces have the best results.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-226">Frontal and near-frontal faces have the best results.</span></span>

## <a name="sample-code"></a><span data-ttu-id="3c5b0-227">Sample code</span><span class="sxs-lookup"><span data-stu-id="3c5b0-227">Sample code</span></span>
<span data-ttu-id="3c5b0-228">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="3c5b0-228">The following program shows how to:</span></span>

1. <span data-ttu-id="3c5b0-229">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-229">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="3c5b0-230">Create a job with a face detection task based on a configuration file that contains the following json preset.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-230">Create a job with a face detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="3c5b0-231">Download the output JSON files.</span><span class="sxs-lookup"><span data-stu-id="3c5b0-231">Download the output JSON files.</span></span> 
   
        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Threading.Tasks;
   
        namespace FaceDetection
        {
            class Program
            {
                // Read values from the App.config file.
                private static readonly string _mediaServicesAccountName =
                    ConfigurationManager.AppSettings["MediaServicesAccountName"];
                private static readonly string _mediaServicesAccountKey =
                    ConfigurationManager.AppSettings["MediaServicesAccountKey"];
   
                // Field for service context.
                private static CloudMediaContext _context = null;
                private static MediaServicesCredentials _cachedCredentials = null;
   
                static void Main(string[] args)
                {
   
                    // Create and cache the Media Services credentials in a static class variable.
                    _cachedCredentials = new MediaServicesCredentials(
                                    _mediaServicesAccountName,
                                    _mediaServicesAccountKey);
                    // Used the cached credentials to create CloudMediaContext.
                    _context = new CloudMediaContext(_cachedCredentials);
   
                    // Run the FaceDetection job.
                    var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                                @"C:\supportFiles\FaceDetection\config.json");
   
                    // Download the job output asset.
                    DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
                }
   
                static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
                {
                    // Create an asset and upload the input media file to storage.
                    IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                        "My Face Detection Input Asset",
                        AssetCreationOptions.None);
   
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("My Face Detection Job");
   
                    // Get a reference to Azure Media Face Detector.
                    string MediaProcessorName = "Azure Media Face Detector";
   
                    var processor = GetLatestMediaProcessorByName(MediaProcessorName);
   
                    // Read configuration from the specified file.
                    string configuration = File.ReadAllText(configurationFile);
   
                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("My Face Detection Task",
                        processor,
                        configuration,
                        TaskOptions.None);
   
                    // Specify the input asset.
                    task.InputAssets.Add(asset);
   
                    // Add an output asset to contain the results of the job.
                    task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);
   
                    // Use the following event handler to check job progress.  
                    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);
   
                    // Launch the job.
                    job.Submit();
   
                    // Check job execution and wait for job to finish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
   
                    progressJobTask.Wait();
   
                    // If job state is Error, the event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                        Console.WriteLine(string.Format("Error: {0}. {1}",
                                                        error.Code,
                                                        error.Message));
                        return null;
                    }
   
                    return job.OutputMediaAssets[0];
                }
   
                static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
                {
                    IAsset asset = _context.Assets.Create(assetName, options);
   
                    var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                    assetFile.Upload(filePath);
   
                    return asset;
                }
   
                static void DownloadAsset(IAsset asset, string outputDirectory)
                {
                    foreach (IAssetFile file in asset.AssetFiles)
                    {
                        file.Download(Path.Combine(outputDirectory, file.Name));
                    }
                }
   
                static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
                {
                    var processor = _context.MediaProcessors
                        .Where(p => p.Name == mediaProcessorName)
                        .ToList()
                        .OrderBy(p => new Version(p.Version))
                        .LastOrDefault();
   
                    if (processor == null)
                        throw new ArgumentException(string.Format("Unknown media processor",
                                                                   mediaProcessorName));
   
                    return processor;
                }
   
                static private void StateChanged(object sender, JobStateChangedEventArgs e)
                {
                    Console.WriteLine("Job state changed event:");
                    Console.WriteLine("  Previous state: " + e.PreviousState);
                    Console.WriteLine("  Current state: " + e.CurrentState);
   
                    switch (e.CurrentState)
                    {
                        case JobState.Finished:
                            Console.WriteLine();
                            Console.WriteLine("Job is finished.");
                            Console.WriteLine();
                            break;
                        case JobState.Canceling:
                        case JobState.Queued:
                        case JobState.Scheduled:
                        case JobState.Processing:
                            Console.WriteLine("Please wait...\n");
                            break;
                        case JobState.Canceled:
                        case JobState.Error:
                            // Cast sender as a job.
                            IJob job = (IJob)sender;
                            // Display or log error details as needed.
                            // LogJobStop(job.Id);
                            break;
                        default:
                            break;
                    }
                }
   
            }
        }

## <a name="media-services-learning-paths"></a><span data-ttu-id="3c5b0-232">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="3c5b0-232">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3c5b0-233">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="3c5b0-233">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="3c5b0-234">Related links</span><span class="sxs-lookup"><span data-stu-id="3c5b0-234">Related links</span></span>
[<span data-ttu-id="3c5b0-235">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="3c5b0-235">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="3c5b0-236">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="3c5b0-236">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

