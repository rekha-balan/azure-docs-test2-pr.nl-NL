---
title: Detect Motions with Azure Media Analytics | Microsoft Docs
description: The Azure Media Motion Detector media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/09/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 8488b968fe2ab823479d70a98ba86be97b28f67d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870066"
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="00078-103">Detect Motions with Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="00078-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="00078-104">Overview</span><span class="sxs-lookup"><span data-stu-id="00078-104">Overview</span></span>
<span data-ttu-id="00078-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span><span class="sxs-lookup"><span data-stu-id="00078-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="00078-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span><span class="sxs-lookup"><span data-stu-id="00078-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="00078-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span><span class="sxs-lookup"><span data-stu-id="00078-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="00078-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span><span class="sxs-lookup"><span data-stu-id="00078-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="00078-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from long surveillance videos.</span><span class="sxs-lookup"><span data-stu-id="00078-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from long surveillance videos.</span></span>

<span data-ttu-id="00078-110">The **Azure Media Motion Detector** MP is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="00078-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="00078-111">This article gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="00078-111">This article gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="00078-112">Motion Detector input files</span><span class="sxs-lookup"><span data-stu-id="00078-112">Motion Detector input files</span></span>
<span data-ttu-id="00078-113">Video files.</span><span class="sxs-lookup"><span data-stu-id="00078-113">Video files.</span></span> <span data-ttu-id="00078-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span><span class="sxs-lookup"><span data-stu-id="00078-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="00078-115">Task configuration (preset)</span><span class="sxs-lookup"><span data-stu-id="00078-115">Task configuration (preset)</span></span>
<span data-ttu-id="00078-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span><span class="sxs-lookup"><span data-stu-id="00078-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="00078-117">Parameters</span><span class="sxs-lookup"><span data-stu-id="00078-117">Parameters</span></span>
<span data-ttu-id="00078-118">You can use the following parameters:</span><span class="sxs-lookup"><span data-stu-id="00078-118">You can use the following parameters:</span></span>

| <span data-ttu-id="00078-119">Name</span><span class="sxs-lookup"><span data-stu-id="00078-119">Name</span></span> | <span data-ttu-id="00078-120">Options</span><span class="sxs-lookup"><span data-stu-id="00078-120">Options</span></span> | <span data-ttu-id="00078-121">Description</span><span class="sxs-lookup"><span data-stu-id="00078-121">Description</span></span> | <span data-ttu-id="00078-122">Default</span><span class="sxs-lookup"><span data-stu-id="00078-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00078-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="00078-123">sensitivityLevel</span></span> |<span data-ttu-id="00078-124">String:'low', 'medium', 'high'</span><span class="sxs-lookup"><span data-stu-id="00078-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="00078-125">Sets the sensitivity level at which motions are reported.</span><span class="sxs-lookup"><span data-stu-id="00078-125">Sets the sensitivity level at which motions are reported.</span></span> <span data-ttu-id="00078-126">Adjust this to adjust number of false positives.</span><span class="sxs-lookup"><span data-stu-id="00078-126">Adjust this to adjust number of false positives.</span></span> |<span data-ttu-id="00078-127">'medium'</span><span class="sxs-lookup"><span data-stu-id="00078-127">'medium'</span></span> |
| <span data-ttu-id="00078-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="00078-128">frameSamplingValue</span></span> |<span data-ttu-id="00078-129">Positive integer</span><span class="sxs-lookup"><span data-stu-id="00078-129">Positive integer</span></span> |<span data-ttu-id="00078-130">Sets the frequency at which algorithm runs.</span><span class="sxs-lookup"><span data-stu-id="00078-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="00078-131">1 equals every frame, 2 means every second frame, and so on.</span><span class="sxs-lookup"><span data-stu-id="00078-131">1 equals every frame, 2 means every second frame, and so on.</span></span> |<span data-ttu-id="00078-132">1</span><span class="sxs-lookup"><span data-stu-id="00078-132">1</span></span> |
| <span data-ttu-id="00078-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="00078-133">detectLightChange</span></span> |<span data-ttu-id="00078-134">Boolean:'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="00078-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="00078-135">Sets whether light changes are reported in the results</span><span class="sxs-lookup"><span data-stu-id="00078-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="00078-136">'False'</span><span class="sxs-lookup"><span data-stu-id="00078-136">'False'</span></span> |
| <span data-ttu-id="00078-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="00078-137">mergeTimeThreshold</span></span> |<span data-ttu-id="00078-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="00078-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="00078-139">Example: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="00078-139">Example: 00:00:03</span></span> |<span data-ttu-id="00078-140">Specifies the time window between motion events where 2 events are be combined and reported as 1.</span><span class="sxs-lookup"><span data-stu-id="00078-140">Specifies the time window between motion events where 2 events are be combined and reported as 1.</span></span> |<span data-ttu-id="00078-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="00078-141">00:00:00</span></span> |
| <span data-ttu-id="00078-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="00078-142">detectionZones</span></span> |<span data-ttu-id="00078-143">An array of detection zones:</span><span class="sxs-lookup"><span data-stu-id="00078-143">An array of detection zones:</span></span><br/><span data-ttu-id="00078-144">- Detection Zone is an array of 3 or more points</span><span class="sxs-lookup"><span data-stu-id="00078-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="00078-145">- Point is an x and y coordinate from 0 to 1.</span><span class="sxs-lookup"><span data-stu-id="00078-145">- Point is an x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="00078-146">Describes the list of polygonal detection zones to be used.</span><span class="sxs-lookup"><span data-stu-id="00078-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="00078-147">Results are reported with the zones as an ID, with the first one being 'id':0</span><span class="sxs-lookup"><span data-stu-id="00078-147">Results are reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="00078-148">Single zone, which covers the entire frame.</span><span class="sxs-lookup"><span data-stu-id="00078-148">Single zone, which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="00078-149">JSON example</span><span class="sxs-lookup"><span data-stu-id="00078-149">JSON example</span></span>

```json
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
```

## <a name="motion-detector-output-files"></a><span data-ttu-id="00078-150">Motion Detector output files</span><span class="sxs-lookup"><span data-stu-id="00078-150">Motion Detector output files</span></span>
<span data-ttu-id="00078-151">A motion detection job returns a JSON file in the output asset, which describes the motion alerts, and their categories, within the video.</span><span class="sxs-lookup"><span data-stu-id="00078-151">A motion detection job returns a JSON file in the output asset, which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="00078-152">The file contains information about the time and duration of motion detected in the video.</span><span class="sxs-lookup"><span data-stu-id="00078-152">The file contains information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="00078-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (for example, a surveillance video).</span><span class="sxs-lookup"><span data-stu-id="00078-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (for example, a surveillance video).</span></span> <span data-ttu-id="00078-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span><span class="sxs-lookup"><span data-stu-id="00078-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="00078-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span><span class="sxs-lookup"><span data-stu-id="00078-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <a id="output_elements"></a><span data-ttu-id="00078-156">Elements of the output JSON file</span><span class="sxs-lookup"><span data-stu-id="00078-156">Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="00078-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span><span class="sxs-lookup"><span data-stu-id="00078-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="00078-158">The following table describes elements of the output JSON file.</span><span class="sxs-lookup"><span data-stu-id="00078-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="00078-159">Element</span><span class="sxs-lookup"><span data-stu-id="00078-159">Element</span></span> | <span data-ttu-id="00078-160">Description</span><span class="sxs-lookup"><span data-stu-id="00078-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="00078-161">Version</span><span class="sxs-lookup"><span data-stu-id="00078-161">Version</span></span> |<span data-ttu-id="00078-162">This refers to the version of the Video API.</span><span class="sxs-lookup"><span data-stu-id="00078-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="00078-163">The current version is 2.</span><span class="sxs-lookup"><span data-stu-id="00078-163">The current version is 2.</span></span> |
| <span data-ttu-id="00078-164">Timescale</span><span class="sxs-lookup"><span data-stu-id="00078-164">Timescale</span></span> |<span data-ttu-id="00078-165">"Ticks" per second of the video.</span><span class="sxs-lookup"><span data-stu-id="00078-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="00078-166">Offset</span><span class="sxs-lookup"><span data-stu-id="00078-166">Offset</span></span> |<span data-ttu-id="00078-167">The time offset for timestamps in "ticks."</span><span class="sxs-lookup"><span data-stu-id="00078-167">The time offset for timestamps in "ticks."</span></span> <span data-ttu-id="00078-168">In version 1.0 of Video APIs, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="00078-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="00078-169">In future scenarios we support, this value may change.</span><span class="sxs-lookup"><span data-stu-id="00078-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="00078-170">Framerate</span><span class="sxs-lookup"><span data-stu-id="00078-170">Framerate</span></span> |<span data-ttu-id="00078-171">Frames per second of the video.</span><span class="sxs-lookup"><span data-stu-id="00078-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="00078-172">Width, Height</span><span class="sxs-lookup"><span data-stu-id="00078-172">Width, Height</span></span> |<span data-ttu-id="00078-173">Refers to the width and height of the video in pixels.</span><span class="sxs-lookup"><span data-stu-id="00078-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="00078-174">Start</span><span class="sxs-lookup"><span data-stu-id="00078-174">Start</span></span> |<span data-ttu-id="00078-175">The start timestamp in "ticks".</span><span class="sxs-lookup"><span data-stu-id="00078-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="00078-176">Duration</span><span class="sxs-lookup"><span data-stu-id="00078-176">Duration</span></span> |<span data-ttu-id="00078-177">The length of the event, in "ticks".</span><span class="sxs-lookup"><span data-stu-id="00078-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="00078-178">Interval</span><span class="sxs-lookup"><span data-stu-id="00078-178">Interval</span></span> |<span data-ttu-id="00078-179">The interval of each entry in the event, in "ticks".</span><span class="sxs-lookup"><span data-stu-id="00078-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="00078-180">Events</span><span class="sxs-lookup"><span data-stu-id="00078-180">Events</span></span> |<span data-ttu-id="00078-181">Each event fragment contains the motion detected within that time duration.</span><span class="sxs-lookup"><span data-stu-id="00078-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="00078-182">Type</span><span class="sxs-lookup"><span data-stu-id="00078-182">Type</span></span> |<span data-ttu-id="00078-183">In the current version, this is always ‘2’ for generic motion.</span><span class="sxs-lookup"><span data-stu-id="00078-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="00078-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span><span class="sxs-lookup"><span data-stu-id="00078-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="00078-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="00078-185">RegionID</span></span> |<span data-ttu-id="00078-186">As explained above, this will always be 0 in this version.</span><span class="sxs-lookup"><span data-stu-id="00078-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="00078-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span><span class="sxs-lookup"><span data-stu-id="00078-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="00078-188">Regions</span><span class="sxs-lookup"><span data-stu-id="00078-188">Regions</span></span> |<span data-ttu-id="00078-189">Refers to the area in your video where you care about motion.</span><span class="sxs-lookup"><span data-stu-id="00078-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="00078-190">-"id" represents the region area – in this version there is only one, ID 0.</span><span class="sxs-lookup"><span data-stu-id="00078-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="00078-191">-"type" represents the shape of the region you care about for motion.</span><span class="sxs-lookup"><span data-stu-id="00078-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="00078-192">Currently, "rectangle" and "polygon" are supported.</span><span class="sxs-lookup"><span data-stu-id="00078-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="00078-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span><span class="sxs-lookup"><span data-stu-id="00078-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="00078-194">The X and Y coordinates represent the upper left-hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="00078-194">The X and Y coordinates represent the upper left-hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="00078-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span><span class="sxs-lookup"><span data-stu-id="00078-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="00078-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span><span class="sxs-lookup"><span data-stu-id="00078-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="00078-197">If you specified "polygon", the region has dimensions in points.</span><span class="sxs-lookup"><span data-stu-id="00078-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="00078-198">Fragments</span><span class="sxs-lookup"><span data-stu-id="00078-198">Fragments</span></span> |<span data-ttu-id="00078-199">The metadata is chunked up into different segments called fragments.</span><span class="sxs-lookup"><span data-stu-id="00078-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="00078-200">Each fragment contains a start, duration, interval number, and event(s).</span><span class="sxs-lookup"><span data-stu-id="00078-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="00078-201">A fragment with no events means that no motion was detected during that start time and duration.</span><span class="sxs-lookup"><span data-stu-id="00078-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="00078-202">Brackets []</span><span class="sxs-lookup"><span data-stu-id="00078-202">Brackets []</span></span> |<span data-ttu-id="00078-203">Each bracket represents one interval in the event.</span><span class="sxs-lookup"><span data-stu-id="00078-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="00078-204">Empty brackets for that interval means that no motion was detected.</span><span class="sxs-lookup"><span data-stu-id="00078-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="00078-205">locations</span><span class="sxs-lookup"><span data-stu-id="00078-205">locations</span></span> |<span data-ttu-id="00078-206">This new entry under events lists the location where the motion occurred.</span><span class="sxs-lookup"><span data-stu-id="00078-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="00078-207">This is more specific than the detection zones.</span><span class="sxs-lookup"><span data-stu-id="00078-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="00078-208">The following JSON example shows the output:</span><span class="sxs-lookup"><span data-stu-id="00078-208">The following JSON example shows the output:</span></span>

```json
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
```

## <a name="limitations"></a><span data-ttu-id="00078-209">Limitations</span><span class="sxs-lookup"><span data-stu-id="00078-209">Limitations</span></span>
* <span data-ttu-id="00078-210">The supported input video formats include MP4, MOV, and WMV.</span><span class="sxs-lookup"><span data-stu-id="00078-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="00078-211">Motion Detection is optimized for stationary background videos.</span><span class="sxs-lookup"><span data-stu-id="00078-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="00078-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span><span class="sxs-lookup"><span data-stu-id="00078-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="00078-213">Some motion may not be detected due to technical challenges; for example, night vision videos, semi-transparent objects, and small objects.</span><span class="sxs-lookup"><span data-stu-id="00078-213">Some motion may not be detected due to technical challenges; for example, night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="00078-214">.NET sample code</span><span class="sxs-lookup"><span data-stu-id="00078-214">.NET sample code</span></span>

<span data-ttu-id="00078-215">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="00078-215">The following program shows how to:</span></span>

1. <span data-ttu-id="00078-216">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="00078-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="00078-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset:</span><span class="sxs-lookup"><span data-stu-id="00078-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset:</span></span> 
   
    ```json
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
    ```

3. <span data-ttu-id="00078-218">Download the output JSON files.</span><span class="sxs-lookup"><span data-stu-id="00078-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="00078-219">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="00078-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="00078-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="00078-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="00078-221">Example</span><span class="sxs-lookup"><span data-stu-id="00078-221">Example</span></span>

```csharp

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
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AMSAADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];
        private static readonly string _AMSClientId =
            ConfigurationManager.AppSettings["AMSClientId"];
        private static readonly string _AMSClientSecret =
            ConfigurationManager.AppSettings["AMSClientSecret"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            AzureAdTokenCredentials tokenCredentials =
                new AzureAdTokenCredentials(_AADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

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
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="00078-222">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="00078-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="00078-223">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="00078-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="00078-224">Related links</span><span class="sxs-lookup"><span data-stu-id="00078-224">Related links</span></span>
[<span data-ttu-id="00078-225">Azure Media Services Motion Detector blog</span><span class="sxs-lookup"><span data-stu-id="00078-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="00078-226">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="00078-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="00078-227">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="00078-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

