---
title: Indexing Media Files with Azure Media Indexer 2 Preview | Microsoft Docs
description: Azure Media Indexer enables you to make content of your media files searchable and to generate a full-text transcript for closed captioning and keywords. This topic shows how to use Media Indexer 2 Preview.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/07/2016
ms.author: adsolank;juliako;
ms.openlocfilehash: 902e872b224b267c989f741345efdd8ef3fa8ce3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556095"
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a><span data-ttu-id="26c2c-104">Indexing Media Files with Azure Media Indexer 2 Preview</span><span class="sxs-lookup"><span data-stu-id="26c2c-104">Indexing Media Files with Azure Media Indexer 2 Preview</span></span>
## <a name="overview"></a><span data-ttu-id="26c2c-105">Overview</span><span class="sxs-lookup"><span data-stu-id="26c2c-105">Overview</span></span>
<span data-ttu-id="26c2c-106">The **Azure Media Indexer 2 Preview** media processor (MP) enables you to make media files and content searchable, as well as generate closed captioning tracks.</span><span class="sxs-lookup"><span data-stu-id="26c2c-106">The **Azure Media Indexer 2 Preview** media processor (MP) enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="26c2c-107">Compared to the previous version of [Azure Media Indexer](media-services-index-content.md), **Azure Media Indexer 2 Preview** performs faster indexing and offers broader language support.</span><span class="sxs-lookup"><span data-stu-id="26c2c-107">Compared to the previous version of [Azure Media Indexer](media-services-index-content.md), **Azure Media Indexer 2 Preview** performs faster indexing and offers broader language support.</span></span> <span data-ttu-id="26c2c-108">Supported languages include English, Spanish, French, German, Italian, Chinese (Mandarin, Simplified), Portuguese, Arabic, and Japanese.</span><span class="sxs-lookup"><span data-stu-id="26c2c-108">Supported languages include English, Spanish, French, German, Italian, Chinese (Mandarin, Simplified), Portuguese, Arabic, and Japanese.</span></span>

<span data-ttu-id="26c2c-109">The **Azure Media Indexer 2 Preview** MP is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="26c2c-109">The **Azure Media Indexer 2 Preview** MP is currently in Preview.</span></span>

<span data-ttu-id="26c2c-110">This topic shows how to create indexing jobs with **Azure Media Indexer 2 Preview**.</span><span class="sxs-lookup"><span data-stu-id="26c2c-110">This topic shows how to create indexing jobs with **Azure Media Indexer 2 Preview**.</span></span>

> [!NOTE]
> <span data-ttu-id="26c2c-111">The following considerations apply:</span><span class="sxs-lookup"><span data-stu-id="26c2c-111">The following considerations apply:</span></span>
> 
> <span data-ttu-id="26c2c-112">Indexer 2 is not supported in Azure China and Azure Government.</span><span class="sxs-lookup"><span data-stu-id="26c2c-112">Indexer 2 is not supported in Azure China and Azure Government.</span></span>
> 
> <span data-ttu-id="26c2c-113">When indexing content, make sure to use media files that have very clear speech (without background music, noise, effects, or microphone hiss).</span><span class="sxs-lookup"><span data-stu-id="26c2c-113">When indexing content, make sure to use media files that have very clear speech (without background music, noise, effects, or microphone hiss).</span></span> <span data-ttu-id="26c2c-114">Some examples of appropriate content are: recorded meetings, lectures or presentations.</span><span class="sxs-lookup"><span data-stu-id="26c2c-114">Some examples of appropriate content are: recorded meetings, lectures or presentations.</span></span> <span data-ttu-id="26c2c-115">The following content might not be suitable for indexing: movies, TV shows, anything with mixed audio and sound effects, poorly recorded content with background noise (hiss).</span><span class="sxs-lookup"><span data-stu-id="26c2c-115">The following content might not be suitable for indexing: movies, TV shows, anything with mixed audio and sound effects, poorly recorded content with background noise (hiss).</span></span>
> 
> 

<span data-ttu-id="26c2c-116">This topic gives details about  **Azure Media Indexer 2 Preview** and shows how to use it with Media Services SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="26c2c-116">This topic gives details about  **Azure Media Indexer 2 Preview** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="input-and-output-files"></a><span data-ttu-id="26c2c-117">Input and output files</span><span class="sxs-lookup"><span data-stu-id="26c2c-117">Input and output files</span></span>
### <a name="input-files"></a><span data-ttu-id="26c2c-118">Input files</span><span class="sxs-lookup"><span data-stu-id="26c2c-118">Input files</span></span>
<span data-ttu-id="26c2c-119">Audio or video files</span><span class="sxs-lookup"><span data-stu-id="26c2c-119">Audio or video files</span></span>

### <a name="output-files"></a><span data-ttu-id="26c2c-120">Output files</span><span class="sxs-lookup"><span data-stu-id="26c2c-120">Output files</span></span>
<span data-ttu-id="26c2c-121">An indexing job can generate closed caption files in the following formats:</span><span class="sxs-lookup"><span data-stu-id="26c2c-121">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="26c2c-122">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="26c2c-122">**SAMI**</span></span>
* <span data-ttu-id="26c2c-123">**TTML**</span><span class="sxs-lookup"><span data-stu-id="26c2c-123">**TTML**</span></span>
* <span data-ttu-id="26c2c-124">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="26c2c-124">**WebVTT**</span></span>

<span data-ttu-id="26c2c-125">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span><span class="sxs-lookup"><span data-stu-id="26c2c-125">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="26c2c-126">Task configuration (preset)</span><span class="sxs-lookup"><span data-stu-id="26c2c-126">Task configuration (preset)</span></span>
<span data-ttu-id="26c2c-127">When creating an indexing task with **Azure Media Indexer 2 Preview**, you must specify a configuration preset.</span><span class="sxs-lookup"><span data-stu-id="26c2c-127">When creating an indexing task with **Azure Media Indexer 2 Preview**, you must specify a configuration preset.</span></span>

<span data-ttu-id="26c2c-128">The following JSON sets available parameters.</span><span class="sxs-lookup"><span data-stu-id="26c2c-128">The following JSON sets available parameters.</span></span>

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a><span data-ttu-id="26c2c-129">Supported languages</span><span class="sxs-lookup"><span data-stu-id="26c2c-129">Supported languages</span></span>
<span data-ttu-id="26c2c-130">Azure Media Indexer 2 Preview supports speech-to-text for the following languages (when specifying the language name in the task configuration, use 4-character code in brackets as shown below):</span><span class="sxs-lookup"><span data-stu-id="26c2c-130">Azure Media Indexer 2 Preview supports speech-to-text for the following languages (when specifying the language name in the task configuration, use 4-character code in brackets as shown below):</span></span>

* <span data-ttu-id="26c2c-131">English [EnUs]</span><span class="sxs-lookup"><span data-stu-id="26c2c-131">English [EnUs]</span></span>
* <span data-ttu-id="26c2c-132">Spanish [EsEs]</span><span class="sxs-lookup"><span data-stu-id="26c2c-132">Spanish [EsEs]</span></span>
* <span data-ttu-id="26c2c-133">Chinese (Mandarin, Simplified) [ZhCn]</span><span class="sxs-lookup"><span data-stu-id="26c2c-133">Chinese (Mandarin, Simplified) [ZhCn]</span></span>
* <span data-ttu-id="26c2c-134">French [FrFr]</span><span class="sxs-lookup"><span data-stu-id="26c2c-134">French [FrFr]</span></span>
* <span data-ttu-id="26c2c-135">German [DeDe]</span><span class="sxs-lookup"><span data-stu-id="26c2c-135">German [DeDe]</span></span>
* <span data-ttu-id="26c2c-136">Italian [ItIt]</span><span class="sxs-lookup"><span data-stu-id="26c2c-136">Italian [ItIt]</span></span>
* <span data-ttu-id="26c2c-137">Portuguese  [PtBr]</span><span class="sxs-lookup"><span data-stu-id="26c2c-137">Portuguese  [PtBr]</span></span>
* <span data-ttu-id="26c2c-138">Arabic (Egyptian) [ArEg]</span><span class="sxs-lookup"><span data-stu-id="26c2c-138">Arabic (Egyptian) [ArEg]</span></span>
* <span data-ttu-id="26c2c-139">Japanese [JaJp]</span><span class="sxs-lookup"><span data-stu-id="26c2c-139">Japanese [JaJp]</span></span>

## <a name="sample-code"></a><span data-ttu-id="26c2c-140">Sample code</span><span class="sxs-lookup"><span data-stu-id="26c2c-140">Sample code</span></span>

<span data-ttu-id="26c2c-141">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="26c2c-141">The following program shows how to:</span></span>

1. <span data-ttu-id="26c2c-142">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="26c2c-142">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="26c2c-143">Creates a job with an indexing task based on a configuration file that contains the following json preset.</span><span class="sxs-lookup"><span data-stu-id="26c2c-143">Creates a job with an indexing task based on a configuration file that contains the following json preset.</span></span>
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. <span data-ttu-id="26c2c-144">Downloads the output files.</span><span class="sxs-lookup"><span data-stu-id="26c2c-144">Downloads the output files.</span></span> 
   
        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Threading.Tasks;
   
        namespace IndexContent
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
   
                    // Run indexing job.
                    var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                                @"C:\supportFiles\Indexer\config.json");
   
                    // Download the job output asset.
                    DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
                }
   
                static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
                {
                    // Create an asset and upload the input media file to storage.
                    IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                        "My Indexing Input Asset",
                        AssetCreationOptions.None);
   
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("My Indexing Job");
   
                    // Get a reference to Azure Media Indexer 2 Preview.
                    string MediaProcessorName = "Azure Media Indexer 2 Preview";
   
                    var processor = GetLatestMediaProcessorByName(MediaProcessorName);
   
                    // Read configuration from the specified file.
                    string configuration = File.ReadAllText(configurationFile);
   
                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("My Indexing Task",
                        processor,
                        configuration,
                        TaskOptions.None);
   
                    // Specify the input asset to be indexed.
                    task.InputAssets.Add(asset);
   
                    // Add an output asset to contain the results of the job.
                    task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);
   
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="26c2c-145">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="26c2c-145">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="26c2c-146">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="26c2c-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="26c2c-147">Related links</span><span class="sxs-lookup"><span data-stu-id="26c2c-147">Related links</span></span>
[<span data-ttu-id="26c2c-148">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="26c2c-148">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="26c2c-149">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="26c2c-149">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

