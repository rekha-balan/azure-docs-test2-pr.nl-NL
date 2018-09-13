---
title: Use Azure Media Video Thumbnails to Create a Video Summarization | Microsoft Docs
description: Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from the source video. This is useful when you want to provide a quick overview of what to expect in a long video.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 7510c8ab4adadbd7d738ba0b8e2bbdddba8d1048
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552777"
---
# <a name="use-azure-media-video-thumbnails-to-create-a-video-summarization"></a><span data-ttu-id="634c1-104">Use Azure Media Video Thumbnails to Create a Video Summarization</span><span class="sxs-lookup"><span data-stu-id="634c1-104">Use Azure Media Video Thumbnails to Create a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="634c1-105">Overview</span><span class="sxs-lookup"><span data-stu-id="634c1-105">Overview</span></span>
<span data-ttu-id="634c1-106">The **Azure Media Video Thumbnails** media processor (MP) enables you to create a summary of a video that is useful to customers who just want to preview a summary of a long video.</span><span class="sxs-lookup"><span data-stu-id="634c1-106">The **Azure Media Video Thumbnails** media processor (MP) enables you to create a summary of a video that is useful to customers who just want to preview a summary of a long video.</span></span> <span data-ttu-id="634c1-107">For example, customers might want to see a short "summary video" when they hover over a thumbnail.</span><span class="sxs-lookup"><span data-stu-id="634c1-107">For example, customers might want to see a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="634c1-108">By tweaking the parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use the MP's powerful shot detection and concatenation technology to algorithmically generate a descriptive subclip.</span><span class="sxs-lookup"><span data-stu-id="634c1-108">By tweaking the parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use the MP's powerful shot detection and concatenation technology to algorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="634c1-109">The **Azure Media Video Thumbnail** MP is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="634c1-109">The **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="634c1-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how to use it with Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="634c1-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="634c1-111">Limitations</span><span class="sxs-lookup"><span data-stu-id="634c1-111">Limitations</span></span>

<span data-ttu-id="634c1-112">In some cases, if your video is not comprised of different scenes, the output will only be a single shot.</span><span class="sxs-lookup"><span data-stu-id="634c1-112">In some cases, if your video is not comprised of different scenes, the output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="634c1-113">Video summary example</span><span class="sxs-lookup"><span data-stu-id="634c1-113">Video summary example</span></span>
<span data-ttu-id="634c1-114">Here are some examples of what the Azure Media Video Thumbnails media processor can do:</span><span class="sxs-lookup"><span data-stu-id="634c1-114">Here are some examples of what the Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="634c1-115">Original video</span><span class="sxs-lookup"><span data-stu-id="634c1-115">Original video</span></span>
[<span data-ttu-id="634c1-116">Original video</span><span class="sxs-lookup"><span data-stu-id="634c1-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="634c1-117">Video thumbnail result</span><span class="sxs-lookup"><span data-stu-id="634c1-117">Video thumbnail result</span></span>
[<span data-ttu-id="634c1-118">Video thumbnail result</span><span class="sxs-lookup"><span data-stu-id="634c1-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="634c1-119">Task configuration (preset)</span><span class="sxs-lookup"><span data-stu-id="634c1-119">Task configuration (preset)</span></span>
<span data-ttu-id="634c1-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span><span class="sxs-lookup"><span data-stu-id="634c1-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="634c1-121">The above thumbnail sample was created with the following basic JSON configuration:</span><span class="sxs-lookup"><span data-stu-id="634c1-121">The above thumbnail sample was created with the following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="634c1-122">Currently, you can change the following parameters:</span><span class="sxs-lookup"><span data-stu-id="634c1-122">Currently, you can change the following parameters:</span></span>

| <span data-ttu-id="634c1-123">Param</span><span class="sxs-lookup"><span data-stu-id="634c1-123">Param</span></span> | <span data-ttu-id="634c1-124">Description</span><span class="sxs-lookup"><span data-stu-id="634c1-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="634c1-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="634c1-125">outputAudio</span></span> |<span data-ttu-id="634c1-126">Specifies whether or not the resultant video contains any audio.</span><span class="sxs-lookup"><span data-stu-id="634c1-126">Specifies whether or not the resultant video contains any audio.</span></span> <br/><span data-ttu-id="634c1-127">Allowed values are: True or False.</span><span class="sxs-lookup"><span data-stu-id="634c1-127">Allowed values are: True or False.</span></span> <span data-ttu-id="634c1-128">Default is True.</span><span class="sxs-lookup"><span data-stu-id="634c1-128">Default is True.</span></span> |
| <span data-ttu-id="634c1-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="634c1-129">fadeInFadeOut</span></span> |<span data-ttu-id="634c1-130">Specifies whether or not fade transitions are used between the separate motion thumbnails.</span><span class="sxs-lookup"><span data-stu-id="634c1-130">Specifies whether or not fade transitions are used between the separate motion thumbnails.</span></span>  <br/><span data-ttu-id="634c1-131">Allowed values are: True or False.</span><span class="sxs-lookup"><span data-stu-id="634c1-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="634c1-132">Default is True.</span><span class="sxs-lookup"><span data-stu-id="634c1-132">Default is True.</span></span> |
| <span data-ttu-id="634c1-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="634c1-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="634c1-134">Integer that specifies how long the entire resultant video shall be.</span><span class="sxs-lookup"><span data-stu-id="634c1-134">Integer that specifies how long the entire resultant video shall be.</span></span>  <span data-ttu-id="634c1-135">Default depends on original video duration.</span><span class="sxs-lookup"><span data-stu-id="634c1-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="634c1-136">The following table describes the default duration, when **maxMotionThumbnailInSecs** is not used.</span><span class="sxs-lookup"><span data-stu-id="634c1-136">The following table describes the default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="634c1-137">Video duration</span><span class="sxs-lookup"><span data-stu-id="634c1-137">Video duration</span></span> |<span data-ttu-id="634c1-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="634c1-138">d < 3 min</span></span> |<span data-ttu-id="634c1-139">3 min < d < 15 min</span><span class="sxs-lookup"><span data-stu-id="634c1-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="634c1-140">Thumbnail duration</span><span class="sxs-lookup"><span data-stu-id="634c1-140">Thumbnail duration</span></span> |<span data-ttu-id="634c1-141">15 sec (2-3 scenes)</span><span class="sxs-lookup"><span data-stu-id="634c1-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="634c1-142">30 sec (3-5 scenes)</span><span class="sxs-lookup"><span data-stu-id="634c1-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="634c1-143">The following JSON sets available parameters.</span><span class="sxs-lookup"><span data-stu-id="634c1-143">The following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="sample-code"></a><span data-ttu-id="634c1-144">Sample code</span><span class="sxs-lookup"><span data-stu-id="634c1-144">Sample code</span></span>
<span data-ttu-id="634c1-145">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="634c1-145">The following program shows how to:</span></span>

1. <span data-ttu-id="634c1-146">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="634c1-146">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="634c1-147">Creates a job with a video thumbnail task based on a configuration file that contains the following json preset.</span><span class="sxs-lookup"><span data-stu-id="634c1-147">Creates a job with a video thumbnail task based on a configuration file that contains the following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="634c1-148">Downloads the output files.</span><span class="sxs-lookup"><span data-stu-id="634c1-148">Downloads the output files.</span></span> 

### <a name="net-code"></a><span data-ttu-id="634c1-149">.NET code</span><span class="sxs-lookup"><span data-stu-id="634c1-149">.NET code</span></span>
    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
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


                // Run the thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference to Azure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

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

### <a name="video-thumbnail-output"></a><span data-ttu-id="634c1-150">Video thumbnail output</span><span class="sxs-lookup"><span data-stu-id="634c1-150">Video thumbnail output</span></span>
[<span data-ttu-id="634c1-151">Video thumbnail output</span><span class="sxs-lookup"><span data-stu-id="634c1-151">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="634c1-152">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="634c1-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="634c1-153">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="634c1-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="634c1-154">Related links</span><span class="sxs-lookup"><span data-stu-id="634c1-154">Related links</span></span>
[<span data-ttu-id="634c1-155">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="634c1-155">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="634c1-156">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="634c1-156">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

