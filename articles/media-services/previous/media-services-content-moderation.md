---
title: Use Azure Media Content Moderator to detect possible adult and racy content | Microsoft Docs
description: Video moderation helps detect potential adult and racy content in videos.
services: media-services
documentationcenter: ''
author: sanjeev3
manager: mikemcca
editor: ''
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/06/2018
ms.author: sajagtap
ms.openlocfilehash: e44308f38a138c0e186e41fc8310f8b480cd4e09
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857043"
---
# <a name="use-azure-media-content-moderator-to-detect-possible-adult-and-racy-content"></a><span data-ttu-id="047eb-103">Use Azure Media Content Moderator to detect possible adult and racy content</span><span class="sxs-lookup"><span data-stu-id="047eb-103">Use Azure Media Content Moderator to detect possible adult and racy content</span></span>

## <a name="overview"></a><span data-ttu-id="047eb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="047eb-104">Overview</span></span>
<span data-ttu-id="047eb-105">The **Azure Media Content Moderator** media processor (MP) enables you to use machine-assisted moderation for your videos.</span><span class="sxs-lookup"><span data-stu-id="047eb-105">The **Azure Media Content Moderator** media processor (MP) enables you to use machine-assisted moderation for your videos.</span></span> <span data-ttu-id="047eb-106">For example, you might want to detect possible adult and racy content in videos and review the flagged content by your human moderation teams.</span><span class="sxs-lookup"><span data-stu-id="047eb-106">For example, you might want to detect possible adult and racy content in videos and review the flagged content by your human moderation teams.</span></span>

<span data-ttu-id="047eb-107">The **Azure Media Content Moderator** MP is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="047eb-107">The **Azure Media Content Moderator** MP is currently in Preview.</span></span>

<span data-ttu-id="047eb-108">This article gives details about  **Azure Media Content Moderator** and shows how to use it with Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="047eb-108">This article gives details about  **Azure Media Content Moderator** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="content-moderator-input-files"></a><span data-ttu-id="047eb-109">Content Moderator input files</span><span class="sxs-lookup"><span data-stu-id="047eb-109">Content Moderator input files</span></span>
<span data-ttu-id="047eb-110">Video files.</span><span class="sxs-lookup"><span data-stu-id="047eb-110">Video files.</span></span> <span data-ttu-id="047eb-111">Currently, the following formats are supported: MP4, MOV, and WMV.</span><span class="sxs-lookup"><span data-stu-id="047eb-111">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="content-moderator-output-files"></a><span data-ttu-id="047eb-112">Content Moderator output files</span><span class="sxs-lookup"><span data-stu-id="047eb-112">Content Moderator output files</span></span>
<span data-ttu-id="047eb-113">The moderated output in the JSON format includes auto-detected shots and keyframes.</span><span class="sxs-lookup"><span data-stu-id="047eb-113">The moderated output in the JSON format includes auto-detected shots and keyframes.</span></span> <span data-ttu-id="047eb-114">The keyframes are returned with confidence scores for possible adult or racy content.</span><span class="sxs-lookup"><span data-stu-id="047eb-114">The keyframes are returned with confidence scores for possible adult or racy content.</span></span> <span data-ttu-id="047eb-115">They also include a boolean flag indicating whether a review is recommended.</span><span class="sxs-lookup"><span data-stu-id="047eb-115">They also include a boolean flag indicating whether a review is recommended.</span></span> <span data-ttu-id="047eb-116">The review recommendation flag is assigned values based on the internal thresholds for adult and racy scores.</span><span class="sxs-lookup"><span data-stu-id="047eb-116">The review recommendation flag is assigned values based on the internal thresholds for adult and racy scores.</span></span>

## <a name="elements-of-the-output-json-file"></a><span data-ttu-id="047eb-117">Elements of the output JSON file</span><span class="sxs-lookup"><span data-stu-id="047eb-117">Elements of the output JSON file</span></span>

<span data-ttu-id="047eb-118">The job produces a JSON output file that contains metadata about detected shots and keyframes and whether they contain adult or racy content.</span><span class="sxs-lookup"><span data-stu-id="047eb-118">The job produces a JSON output file that contains metadata about detected shots and keyframes and whether they contain adult or racy content.</span></span>

<span data-ttu-id="047eb-119">The output JSON includes the following elements:</span><span class="sxs-lookup"><span data-stu-id="047eb-119">The output JSON includes the following elements:</span></span>

### <a name="root-json-elements"></a><span data-ttu-id="047eb-120">Root JSON elements</span><span class="sxs-lookup"><span data-stu-id="047eb-120">Root JSON elements</span></span>

| <span data-ttu-id="047eb-121">Element</span><span class="sxs-lookup"><span data-stu-id="047eb-121">Element</span></span> | <span data-ttu-id="047eb-122">Description</span><span class="sxs-lookup"><span data-stu-id="047eb-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="047eb-123">version</span><span class="sxs-lookup"><span data-stu-id="047eb-123">version</span></span> |<span data-ttu-id="047eb-124">The version of Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="047eb-124">The version of Content Moderator.</span></span> |
| <span data-ttu-id="047eb-125">timescale</span><span class="sxs-lookup"><span data-stu-id="047eb-125">timescale</span></span> |<span data-ttu-id="047eb-126">"Ticks" per second of the video.</span><span class="sxs-lookup"><span data-stu-id="047eb-126">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="047eb-127">offset</span><span class="sxs-lookup"><span data-stu-id="047eb-127">offset</span></span> |<span data-ttu-id="047eb-128">The time offset for timestamps.</span><span class="sxs-lookup"><span data-stu-id="047eb-128">The time offset for timestamps.</span></span> <span data-ttu-id="047eb-129">In version 1.0 of Video APIs, this value  will always be 0.</span><span class="sxs-lookup"><span data-stu-id="047eb-129">In version 1.0 of Video APIs, this value  will always be 0.</span></span> <span data-ttu-id="047eb-130">This value may change in the future.</span><span class="sxs-lookup"><span data-stu-id="047eb-130">This value may change in the future.</span></span> |
| <span data-ttu-id="047eb-131">framerate</span><span class="sxs-lookup"><span data-stu-id="047eb-131">framerate</span></span> |<span data-ttu-id="047eb-132">Frames per second of the video.</span><span class="sxs-lookup"><span data-stu-id="047eb-132">Frames per second of the video.</span></span> |
| <span data-ttu-id="047eb-133">width</span><span class="sxs-lookup"><span data-stu-id="047eb-133">width</span></span> |<span data-ttu-id="047eb-134">The width of the output video frame, in pixels.</span><span class="sxs-lookup"><span data-stu-id="047eb-134">The width of the output video frame, in pixels.</span></span>|
| <span data-ttu-id="047eb-135">height</span><span class="sxs-lookup"><span data-stu-id="047eb-135">height</span></span> |<span data-ttu-id="047eb-136">The height of the output video frame, in pixels.</span><span class="sxs-lookup"><span data-stu-id="047eb-136">The height of the output video frame, in pixels.</span></span>|
| <span data-ttu-id="047eb-137">totalDuration</span><span class="sxs-lookup"><span data-stu-id="047eb-137">totalDuration</span></span> |<span data-ttu-id="047eb-138">The duration of the input video, in "ticks."</span><span class="sxs-lookup"><span data-stu-id="047eb-138">The duration of the input video, in "ticks."</span></span> |
| [<span data-ttu-id="047eb-139">fragments</span><span class="sxs-lookup"><span data-stu-id="047eb-139">fragments</span></span>](#fragments-json-elements) |<span data-ttu-id="047eb-140">The metadata is chunked up into different segments called fragments.</span><span class="sxs-lookup"><span data-stu-id="047eb-140">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="047eb-141">Each fragment is an auto-detected shot with a start, duration, interval number, and event(s).</span><span class="sxs-lookup"><span data-stu-id="047eb-141">Each fragment is an auto-detected shot with a start, duration, interval number, and event(s).</span></span> |

### <a name="fragments-json-elements"></a><span data-ttu-id="047eb-142">Fragments JSON elements</span><span class="sxs-lookup"><span data-stu-id="047eb-142">Fragments JSON elements</span></span>

|<span data-ttu-id="047eb-143">Element</span><span class="sxs-lookup"><span data-stu-id="047eb-143">Element</span></span>|<span data-ttu-id="047eb-144">Description</span><span class="sxs-lookup"><span data-stu-id="047eb-144">Description</span></span>|
|---|---|
| <span data-ttu-id="047eb-145">start</span><span class="sxs-lookup"><span data-stu-id="047eb-145">start</span></span> |<span data-ttu-id="047eb-146">The start time of the first event in "ticks."</span><span class="sxs-lookup"><span data-stu-id="047eb-146">The start time of the first event in "ticks."</span></span> |
| <span data-ttu-id="047eb-147">duration</span><span class="sxs-lookup"><span data-stu-id="047eb-147">duration</span></span> |<span data-ttu-id="047eb-148">The length of the fragment, in “ticks.”</span><span class="sxs-lookup"><span data-stu-id="047eb-148">The length of the fragment, in “ticks.”</span></span> |
| <span data-ttu-id="047eb-149">interval</span><span class="sxs-lookup"><span data-stu-id="047eb-149">interval</span></span> |<span data-ttu-id="047eb-150">The interval of each event entry within the fragment, in “ticks.”</span><span class="sxs-lookup"><span data-stu-id="047eb-150">The interval of each event entry within the fragment, in “ticks.”</span></span> |
| [<span data-ttu-id="047eb-151">events</span><span class="sxs-lookup"><span data-stu-id="047eb-151">events</span></span>](#events-json-elements) |<span data-ttu-id="047eb-152">Each event represents a clip and each clip contains keyframes detected and tracked within that time duration.</span><span class="sxs-lookup"><span data-stu-id="047eb-152">Each event represents a clip and each clip contains keyframes detected and tracked within that time duration.</span></span> <span data-ttu-id="047eb-153">It is an array of events.</span><span class="sxs-lookup"><span data-stu-id="047eb-153">It is an array of events.</span></span> <span data-ttu-id="047eb-154">The outer array represents one interval of time.</span><span class="sxs-lookup"><span data-stu-id="047eb-154">The outer array represents one interval of time.</span></span> <span data-ttu-id="047eb-155">The inner array consists of 0 or more events that happened at that point in time.</span><span class="sxs-lookup"><span data-stu-id="047eb-155">The inner array consists of 0 or more events that happened at that point in time.</span></span>|

### <a name="events-json-elements"></a><span data-ttu-id="047eb-156">Events JSON elements</span><span class="sxs-lookup"><span data-stu-id="047eb-156">Events JSON elements</span></span>

|<span data-ttu-id="047eb-157">Element</span><span class="sxs-lookup"><span data-stu-id="047eb-157">Element</span></span>|<span data-ttu-id="047eb-158">Description</span><span class="sxs-lookup"><span data-stu-id="047eb-158">Description</span></span>|
|---|---|
| <span data-ttu-id="047eb-159">reviewRecommended</span><span class="sxs-lookup"><span data-stu-id="047eb-159">reviewRecommended</span></span> | <span data-ttu-id="047eb-160">`true` or `false` depending on whether the **adultScore** or **racyScore** exceed the internal thresholds.</span><span class="sxs-lookup"><span data-stu-id="047eb-160">`true` or `false` depending on whether the **adultScore** or **racyScore** exceed the internal thresholds.</span></span> |
| <span data-ttu-id="047eb-161">adultScore</span><span class="sxs-lookup"><span data-stu-id="047eb-161">adultScore</span></span> | <span data-ttu-id="047eb-162">Confidence score for possible adult content, on a scale of 0.00 to 0.99.</span><span class="sxs-lookup"><span data-stu-id="047eb-162">Confidence score for possible adult content, on a scale of 0.00 to 0.99.</span></span> |
| <span data-ttu-id="047eb-163">racyScore</span><span class="sxs-lookup"><span data-stu-id="047eb-163">racyScore</span></span> | <span data-ttu-id="047eb-164">Confidence score for possible racy content, on a scale of 0.00 to 0.99.</span><span class="sxs-lookup"><span data-stu-id="047eb-164">Confidence score for possible racy content, on a scale of 0.00 to 0.99.</span></span> |
| <span data-ttu-id="047eb-165">index</span><span class="sxs-lookup"><span data-stu-id="047eb-165">index</span></span> | <span data-ttu-id="047eb-166">index of the frame on a scale from the first frame index to the last frame index.</span><span class="sxs-lookup"><span data-stu-id="047eb-166">index of the frame on a scale from the first frame index to the last frame index.</span></span> |
| <span data-ttu-id="047eb-167">timestamp</span><span class="sxs-lookup"><span data-stu-id="047eb-167">timestamp</span></span> | <span data-ttu-id="047eb-168">The location of the frame in "ticks."</span><span class="sxs-lookup"><span data-stu-id="047eb-168">The location of the frame in "ticks."</span></span> |
| <span data-ttu-id="047eb-169">shotIndex</span><span class="sxs-lookup"><span data-stu-id="047eb-169">shotIndex</span></span> | <span data-ttu-id="047eb-170">The index of the parent shot.</span><span class="sxs-lookup"><span data-stu-id="047eb-170">The index of the parent shot.</span></span> |


## <a name="content-moderation-quickstart-and-sample-output"></a><span data-ttu-id="047eb-171">Content Moderation quickstart and sample output</span><span class="sxs-lookup"><span data-stu-id="047eb-171">Content Moderation quickstart and sample output</span></span>

### <a name="task-configuration-preset"></a><span data-ttu-id="047eb-172">Task configuration (preset)</span><span class="sxs-lookup"><span data-stu-id="047eb-172">Task configuration (preset)</span></span>
<span data-ttu-id="047eb-173">When creating a task with **Azure Media Content Moderator**, you must specify a configuration preset.</span><span class="sxs-lookup"><span data-stu-id="047eb-173">When creating a task with **Azure Media Content Moderator**, you must specify a configuration preset.</span></span> <span data-ttu-id="047eb-174">The following configuration preset is just for content moderation.</span><span class="sxs-lookup"><span data-stu-id="047eb-174">The following configuration preset is just for content moderation.</span></span>

    {
      "version":"2.0"
    }

### <a name="net-code-sample"></a><span data-ttu-id="047eb-175">.NET code sample</span><span class="sxs-lookup"><span data-stu-id="047eb-175">.NET code sample</span></span>

<span data-ttu-id="047eb-176">The following .NET code sample uses the Media Services .NET SDK to run a Content Moderator job.</span><span class="sxs-lookup"><span data-stu-id="047eb-176">The following .NET code sample uses the Media Services .NET SDK to run a Content Moderator job.</span></span> <span data-ttu-id="047eb-177">It takes a media services Asset as the input that contains the video to be moderated.</span><span class="sxs-lookup"><span data-stu-id="047eb-177">It takes a media services Asset as the input that contains the video to be moderated.</span></span>
<span data-ttu-id="047eb-178">See the [Content Moderator video quickstart](../../cognitive-services/Content-Moderator/video-moderation-api.md) for the full source code and the Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="047eb-178">See the [Content Moderator video quickstart](../../cognitive-services/Content-Moderator/video-moderation-api.md) for the full source code and the Visual Studio project.</span></span>


```csharp
    /// <summary>
    /// Run the Content Moderator job on the designated Asset from local file or blob storage
    /// </summary>
    /// <param name="asset"></param>
    static void RunContentModeratorJob(IAsset asset)
    {
        // Grab the presets
        string configuration = File.ReadAllText(CONTENT_MODERATOR_PRESET_FILE);

        // grab instance of Azure Media Content Moderator MP
        IMediaProcessor mp = _context.MediaProcessors.GetLatestMediaProcessorByName(MEDIA_PROCESSOR);

        // create Job with Content Moderator task
        IJob job = _context.Jobs.Create(String.Format("Content Moderator {0}",
                asset.AssetFiles.First() + "_" + Guid.NewGuid()));

        ITask contentModeratorTask = job.Tasks.AddNew("Adult and racy classifier task",
                mp, configuration,
                TaskOptions.None);
        contentModeratorTask.InputAssets.Add(asset);
        contentModeratorTask.OutputAssets.AddNew("Adult and racy classifier output",
            AssetCreationOptions.None);

        job.Submit();


        // Create progress printing and querying tasks
        Task progressPrintTask = new Task(() =>
        {
            IJob jobQuery = null;
            do
            {
                var progressContext = _context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                    .First();
                    Console.WriteLine(string.Format("{0}\t{1}",
                    DateTime.Now,
                    jobQuery.State));
                    Thread.Sleep(10000);
             }
             while (jobQuery.State != JobState.Finished &&
             jobQuery.State != JobState.Error &&
             jobQuery.State != JobState.Canceled);
        });
        progressPrintTask.Start();

        Task progressJobTask = job.GetExecutionProgressTask(
        CancellationToken.None);
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
        }

        DownloadAsset(job.OutputMediaAssets.First(), OUTPUT_FOLDER);
    }

For the full source code and the Visual Studio project, check out the [Content Moderator video quickstart](../../cognitive-services/Content-Moderator/video-moderation-api.md).

### JSON output

The following example of a Content Moderator JSON output was truncated.

> [!NOTE]
> Location of a keyframe in seconds = timestamp/timescale

    {
    "version": 2,
    "timescale": 90000,
    "offset": 0,
    "framerate": 50,
    "width": 1280,
    "height": 720,
    "totalDuration": 18696321,
    "fragments": [
    {
      "start": 0,
      "duration": 18000
    },
    {
      "start": 18000,
      "duration": 3600,
      "interval": 3600,
      "events": [
        [
          {
            "reviewRecommended": false,
            "adultScore": 0.00001,
            "racyScore": 0.03077,
            "index": 5,
            "timestamp": 18000,
            "shotIndex": 0
          }
        ]
      ]
    },
    {
      "start": 18386372,
      "duration": 119149,
      "interval": 119149,
      "events": [
        [
          {
            "reviewRecommended": true,
            "adultScore": 0.00000,
            "racyScore": 0.91902,
            "index": 5085,
            "timestamp": 18386372,
            "shotIndex": 62
          }
        ]
      ]
    }
    ]
    }
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="047eb-179">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="047eb-179">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="047eb-180">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="047eb-180">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="047eb-181">Related links</span><span class="sxs-lookup"><span data-stu-id="047eb-181">Related links</span></span>
[<span data-ttu-id="047eb-182">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="047eb-182">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="047eb-183">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="047eb-183">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

## <a name="next-steps"></a><span data-ttu-id="047eb-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="047eb-184">Next steps</span></span>

<span data-ttu-id="047eb-185">Learn more about Content Moderator's [video moderation and review solution](../../cognitive-services/Content-Moderator/video-moderation-human-review.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-185">Learn more about Content Moderator's [video moderation and review solution](../../cognitive-services/Content-Moderator/video-moderation-human-review.md).</span></span>

<span data-ttu-id="047eb-186">Get the full source code and the Visual Studio project from the [video moderation quickstart](../../cognitive-services/Content-Moderator/video-moderation-api.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-186">Get the full source code and the Visual Studio project from the [video moderation quickstart](../../cognitive-services/Content-Moderator/video-moderation-api.md).</span></span> 

<span data-ttu-id="047eb-187">Learn how to generate [video reviews](../../cognitive-services/Content-Moderator/video-reviews-quickstart-dotnet.md) from your moderated output, and [moderate transcripts](../../cognitive-services/Content-Moderator/video-transcript-reviews-quickstart-dotnet.md) in .NET.</span><span class="sxs-lookup"><span data-stu-id="047eb-187">Learn how to generate [video reviews](../../cognitive-services/Content-Moderator/video-reviews-quickstart-dotnet.md) from your moderated output, and [moderate transcripts](../../cognitive-services/Content-Moderator/video-transcript-reviews-quickstart-dotnet.md) in .NET.</span></span>

<span data-ttu-id="047eb-188">Check out the detailed .NET [video moderation and review tutorial](../../cognitive-services/Content-Moderator/video-transcript-moderation-review-tutorial-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-188">Check out the detailed .NET [video moderation and review tutorial](../../cognitive-services/Content-Moderator/video-transcript-moderation-review-tutorial-dotnet.md).</span></span> 
