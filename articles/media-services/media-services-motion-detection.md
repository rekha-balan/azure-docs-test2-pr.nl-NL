---
title: Detect Motions with Azure Media Analytics | Microsoft Docs
description: The Azure Media Motion Detector media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 10/10/2016
ms.author: milanga;juliako;
ms.openlocfilehash: b62793e5f77aa89f8b57fddc5b9c3d8806e05b35
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553327"
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="c52be-103">Detect Motions with Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="c52be-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="c52be-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c52be-104">Overview</span></span>
<span data-ttu-id="c52be-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span><span class="sxs-lookup"><span data-stu-id="c52be-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="c52be-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span><span class="sxs-lookup"><span data-stu-id="c52be-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="c52be-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span><span class="sxs-lookup"><span data-stu-id="c52be-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="c52be-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span><span class="sxs-lookup"><span data-stu-id="c52be-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="c52be-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span><span class="sxs-lookup"><span data-stu-id="c52be-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="c52be-110">The **Azure Media Motion Detector** MP is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="c52be-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="c52be-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="c52be-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="c52be-112">Motion Detector input files</span><span class="sxs-lookup"><span data-stu-id="c52be-112">Motion Detector input files</span></span>
<span data-ttu-id="c52be-113">Video files.</span><span class="sxs-lookup"><span data-stu-id="c52be-113">Video files.</span></span> <span data-ttu-id="c52be-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span><span class="sxs-lookup"><span data-stu-id="c52be-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="c52be-115">Task configuration (preset)</span><span class="sxs-lookup"><span data-stu-id="c52be-115">Task configuration (preset)</span></span>
<span data-ttu-id="c52be-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span><span class="sxs-lookup"><span data-stu-id="c52be-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="c52be-117">Parameters</span><span class="sxs-lookup"><span data-stu-id="c52be-117">Parameters</span></span>
<span data-ttu-id="c52be-118">You can use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="c52be-118">You can use the following parameters:</span></span>

| <span data-ttu-id="c52be-119">Name</span><span class="sxs-lookup"><span data-stu-id="c52be-119">Name</span></span> | <span data-ttu-id="c52be-120">Options</span><span class="sxs-lookup"><span data-stu-id="c52be-120">Options</span></span> | <span data-ttu-id="c52be-121">Description</span><span class="sxs-lookup"><span data-stu-id="c52be-121">Description</span></span> | <span data-ttu-id="c52be-122">Default</span><span class="sxs-lookup"><span data-stu-id="c52be-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c52be-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="c52be-123">sensitivityLevel</span></span> |<span data-ttu-id="c52be-124">String:'low', 'medium', 'high'</span><span class="sxs-lookup"><span data-stu-id="c52be-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="c52be-125">Sets the sensitivity level at which motions is reported.</span><span class="sxs-lookup"><span data-stu-id="c52be-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="c52be-126">Adjust this to adjust amount of false positives.</span><span class="sxs-lookup"><span data-stu-id="c52be-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="c52be-127">'medium'</span><span class="sxs-lookup"><span data-stu-id="c52be-127">'medium'</span></span> |
| <span data-ttu-id="c52be-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="c52be-128">frameSamplingValue</span></span> |<span data-ttu-id="c52be-129">Positive integer</span><span class="sxs-lookup"><span data-stu-id="c52be-129">Positive integer</span></span> |<span data-ttu-id="c52be-130">Sets the frequency at which algorithm runs.</span><span class="sxs-lookup"><span data-stu-id="c52be-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="c52be-131">1 equals every frame, 2 means every 2nd frame, and so on.</span><span class="sxs-lookup"><span data-stu-id="c52be-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="c52be-132">1</span><span class="sxs-lookup"><span data-stu-id="c52be-132">1</span></span> |
| <span data-ttu-id="c52be-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="c52be-133">detectLightChange</span></span> |<span data-ttu-id="c52be-134">Boolean:'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="c52be-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="c52be-135">Sets whether light changes are reported in the results</span><span class="sxs-lookup"><span data-stu-id="c52be-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="c52be-136">'False'</span><span class="sxs-lookup"><span data-stu-id="c52be-136">'False'</span></span> |
| <span data-ttu-id="c52be-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="c52be-137">mergeTimeThreshold</span></span> |<span data-ttu-id="c52be-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="c52be-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="c52be-139">Example: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="c52be-139">Example: 00:00:03</span></span> |<span data-ttu-id="c52be-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span><span class="sxs-lookup"><span data-stu-id="c52be-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="c52be-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="c52be-141">00:00:00</span></span> |
| <span data-ttu-id="c52be-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="c52be-142">detectionZones</span></span> |<span data-ttu-id="c52be-143">An array of detection zones:</span><span class="sxs-lookup"><span data-stu-id="c52be-143">An array of detection zones:</span></span><br/><span data-ttu-id="c52be-144">- Detection Zone is an array of 3 or more points</span><span class="sxs-lookup"><span data-stu-id="c52be-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="c52be-145">- Point is a x and y coordinate from 0 to 1.</span><span class="sxs-lookup"><span data-stu-id="c52be-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="c52be-146">Describes the list of polygonal detection zones to be used.</span><span class="sxs-lookup"><span data-stu-id="c52be-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="c52be-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span><span class="sxs-lookup"><span data-stu-id="c52be-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="c52be-148">Single zone which covers the entire frame.</span><span class="sxs-lookup"><span data-stu-id="c52be-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="c52be-149">JSON example</span><span class="sxs-lookup"><span data-stu-id="c52be-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="c52be-150">Motion Detector output files</span><span class="sxs-lookup"><span data-stu-id="c52be-150">Motion Detector output files</span></span>
<span data-ttu-id="c52be-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span><span class="sxs-lookup"><span data-stu-id="c52be-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="c52be-152">The file will contain information about the time and duration of motion detected in the video.</span><span class="sxs-lookup"><span data-stu-id="c52be-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="c52be-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span><span class="sxs-lookup"><span data-stu-id="c52be-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="c52be-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span><span class="sxs-lookup"><span data-stu-id="c52be-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="c52be-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span><span class="sxs-lookup"><span data-stu-id="c52be-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <a id="output_elements"></a><span data-ttu-id="c52be-156">Elements of the output JSON file</span><span class="sxs-lookup"><span data-stu-id="c52be-156">Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="c52be-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span><span class="sxs-lookup"><span data-stu-id="c52be-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="c52be-158">The following table describes elements of the output JSON file.</span><span class="sxs-lookup"><span data-stu-id="c52be-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="c52be-159">Element</span><span class="sxs-lookup"><span data-stu-id="c52be-159">Element</span></span> | <span data-ttu-id="c52be-160">Description</span><span class="sxs-lookup"><span data-stu-id="c52be-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c52be-161">Version</span><span class="sxs-lookup"><span data-stu-id="c52be-161">Version</span></span> |<span data-ttu-id="c52be-162">This refers to the version of the Video API.</span><span class="sxs-lookup"><span data-stu-id="c52be-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="c52be-163">The current version is 2.</span><span class="sxs-lookup"><span data-stu-id="c52be-163">The current version is 2.</span></span> |
| <span data-ttu-id="c52be-164">Timescale</span><span class="sxs-lookup"><span data-stu-id="c52be-164">Timescale</span></span> |<span data-ttu-id="c52be-165">"Ticks" per second of the video.</span><span class="sxs-lookup"><span data-stu-id="c52be-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="c52be-166">Offset</span><span class="sxs-lookup"><span data-stu-id="c52be-166">Offset</span></span> |<span data-ttu-id="c52be-167">The time offset for timestamps in "ticks".</span><span class="sxs-lookup"><span data-stu-id="c52be-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="c52be-168">In version 1.0 of Video APIs, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="c52be-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="c52be-169">In future scenarios we support, this value may change.</span><span class="sxs-lookup"><span data-stu-id="c52be-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="c52be-170">Framerate</span><span class="sxs-lookup"><span data-stu-id="c52be-170">Framerate</span></span> |<span data-ttu-id="c52be-171">Frames per second of the video.</span><span class="sxs-lookup"><span data-stu-id="c52be-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="c52be-172">Width, Height</span><span class="sxs-lookup"><span data-stu-id="c52be-172">Width, Height</span></span> |<span data-ttu-id="c52be-173">Refers to the width and height of the video in pixels.</span><span class="sxs-lookup"><span data-stu-id="c52be-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="c52be-174">Start</span><span class="sxs-lookup"><span data-stu-id="c52be-174">Start</span></span> |<span data-ttu-id="c52be-175">The start timestamp in "ticks".</span><span class="sxs-lookup"><span data-stu-id="c52be-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="c52be-176">Duration</span><span class="sxs-lookup"><span data-stu-id="c52be-176">Duration</span></span> |<span data-ttu-id="c52be-177">The length of the event, in "ticks".</span><span class="sxs-lookup"><span data-stu-id="c52be-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="c52be-178">Interval</span><span class="sxs-lookup"><span data-stu-id="c52be-178">Interval</span></span> |<span data-ttu-id="c52be-179">The interval of each entry in the event, in "ticks".</span><span class="sxs-lookup"><span data-stu-id="c52be-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="c52be-180">Events</span><span class="sxs-lookup"><span data-stu-id="c52be-180">Events</span></span> |<span data-ttu-id="c52be-181">Each event fragment contains the motion detected within that time duration.</span><span class="sxs-lookup"><span data-stu-id="c52be-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="c52be-182">Type</span><span class="sxs-lookup"><span data-stu-id="c52be-182">Type</span></span> |<span data-ttu-id="c52be-183">In the current version, this is always ‘2’ for generic motion.</span><span class="sxs-lookup"><span data-stu-id="c52be-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="c52be-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span><span class="sxs-lookup"><span data-stu-id="c52be-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="c52be-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="c52be-185">RegionID</span></span> |<span data-ttu-id="c52be-186">As explained above, this will always be 0 in this version.</span><span class="sxs-lookup"><span data-stu-id="c52be-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="c52be-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span><span class="sxs-lookup"><span data-stu-id="c52be-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="c52be-188">Regions</span><span class="sxs-lookup"><span data-stu-id="c52be-188">Regions</span></span> |<span data-ttu-id="c52be-189">Refers to the area in your video where you care about motion.</span><span class="sxs-lookup"><span data-stu-id="c52be-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="c52be-190">-"id" represents the region area – in this version there is only one, ID 0.</span><span class="sxs-lookup"><span data-stu-id="c52be-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="c52be-191">-"type" represents the shape of the region you care about for motion.</span><span class="sxs-lookup"><span data-stu-id="c52be-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="c52be-192">Currently, "rectangle" and "polygon" are supported.</span><span class="sxs-lookup"><span data-stu-id="c52be-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="c52be-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span><span class="sxs-lookup"><span data-stu-id="c52be-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="c52be-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="c52be-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="c52be-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="c52be-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="c52be-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span><span class="sxs-lookup"><span data-stu-id="c52be-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="c52be-197">If you specified "polygon", the region has dimensions in points.</span><span class="sxs-lookup"><span data-stu-id="c52be-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="c52be-198">Fragments</span><span class="sxs-lookup"><span data-stu-id="c52be-198">Fragments</span></span> |<span data-ttu-id="c52be-199">The metadata is chunked up into different segments called fragments.</span><span class="sxs-lookup"><span data-stu-id="c52be-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="c52be-200">Each fragment contains a start, duration, interval number, and event(s).</span><span class="sxs-lookup"><span data-stu-id="c52be-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="c52be-201">A fragment with no events means that no motion was detected during that start time and duration.</span><span class="sxs-lookup"><span data-stu-id="c52be-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="c52be-202">Brackets []</span><span class="sxs-lookup"><span data-stu-id="c52be-202">Brackets []</span></span> |<span data-ttu-id="c52be-203">Each bracket represents one interval in the event.</span><span class="sxs-lookup"><span data-stu-id="c52be-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="c52be-204">Empty brackets for that interval means that no motion was detected.</span><span class="sxs-lookup"><span data-stu-id="c52be-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="c52be-205">locations</span><span class="sxs-lookup"><span data-stu-id="c52be-205">locations</span></span> |<span data-ttu-id="c52be-206">This new entry under events lists the location where the motion occurred.</span><span class="sxs-lookup"><span data-stu-id="c52be-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="c52be-207">This is more specific than the detection zones.</span><span class="sxs-lookup"><span data-stu-id="c52be-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="c52be-208">The following is a JSON output example</span><span class="sxs-lookup"><span data-stu-id="c52be-208">The following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="c52be-209">Limitations</span><span class="sxs-lookup"><span data-stu-id="c52be-209">Limitations</span></span>
* <span data-ttu-id="c52be-210">The supported input video formats include MP4, MOV, and WMV.</span><span class="sxs-lookup"><span data-stu-id="c52be-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="c52be-211">Motion Detection is optimized for stationary background videos.</span><span class="sxs-lookup"><span data-stu-id="c52be-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="c52be-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span><span class="sxs-lookup"><span data-stu-id="c52be-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="c52be-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span><span class="sxs-lookup"><span data-stu-id="c52be-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="sample-code"></a><span data-ttu-id="c52be-214">Sample code</span><span class="sxs-lookup"><span data-stu-id="c52be-214">Sample code</span></span>
<span data-ttu-id="c52be-215">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="c52be-215">The following program shows how to:</span></span>

1. <span data-ttu-id="c52be-216">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="c52be-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="c52be-217">Creates a job with a video motion detection task based on a configuration file that contains the following json preset.</span><span class="sxs-lookup"><span data-stu-id="c52be-217">Creates a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="c52be-218">Downloads the output JSON files.</span><span class="sxs-lookup"><span data-stu-id="c52be-218">Downloads the output JSON files.</span></span> 
   
        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Threading.Tasks;
   
        namespace VideoMotionDetection
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
   
                    // Run the VideoMotionDetection job.
                    var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                                @"C:\supportFiles\VideoMotionDetection\config.json");
   
                    // Download the job output asset.
                    DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
                }
   
                static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
                {
                    // Create an asset and upload the input media file to storage.
                    IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                        "My Video Motion Detection Input Asset",
                        AssetCreationOptions.None);
   
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("My Video Motion Detection Job");
   
                    // Get a reference to Azure Media Motion Detector.
                    string MediaProcessorName = "Azure Media Motion Detector";
   
                    var processor = GetLatestMediaProcessorByName(MediaProcessorName);
   
                    // Read configuration from the specified file.
                    string configuration = File.ReadAllText(configurationFile);
   
                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                        processor,
                        configuration,
                        TaskOptions.None);
   
                    // Specify the input asset.
                    task.InputAssets.Add(asset);
   
                    // Add an output asset to contain the results of the job.
                    task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);
   
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="c52be-219">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="c52be-219">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c52be-220">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="c52be-220">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c52be-221">Related links</span><span class="sxs-lookup"><span data-stu-id="c52be-221">Related links</span></span>
[<span data-ttu-id="c52be-222">Azure Media Services Motion Detector blog</span><span class="sxs-lookup"><span data-stu-id="c52be-222">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="c52be-223">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="c52be-223">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c52be-224">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="c52be-224">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

