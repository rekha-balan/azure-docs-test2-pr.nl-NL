---
title: Indexing Media Files with Azure Media Indexer 2 Preview | Microsoft Docs
description: Azure Media Indexer enables you to make content of your media files searchable and to generate a full-text transcript for closed captioning and keywords. This topic shows how to use Media Indexer 2 Preview.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/09/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ae06f397fd0ed3f1a1b5ebbdc418abc02789fe91
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966336"
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a><span data-ttu-id="128e2-104">Indexing Media Files with Azure Media Indexer 2 Preview</span><span class="sxs-lookup"><span data-stu-id="128e2-104">Indexing Media Files with Azure Media Indexer 2 Preview</span></span>
## <a name="overview"></a><span data-ttu-id="128e2-105">Overview</span><span class="sxs-lookup"><span data-stu-id="128e2-105">Overview</span></span>
<span data-ttu-id="128e2-106">The **Azure Media Indexer 2 Preview** media processor (MP) enables you to make media files and content searchable, as well as generate closed captioning tracks.</span><span class="sxs-lookup"><span data-stu-id="128e2-106">The **Azure Media Indexer 2 Preview** media processor (MP) enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="128e2-107">Compared to the previous version of [Azure Media Indexer](media-services-index-content.md), **Azure Media Indexer 2 Preview** performs faster indexing and offers broader language support.</span><span class="sxs-lookup"><span data-stu-id="128e2-107">Compared to the previous version of [Azure Media Indexer](media-services-index-content.md), **Azure Media Indexer 2 Preview** performs faster indexing and offers broader language support.</span></span> <span data-ttu-id="128e2-108">Supported languages include English, Spanish, French, German, Italian, Chinese (Mandarin, Simplified), Portuguese, Arabic, Russian, and Japanese.</span><span class="sxs-lookup"><span data-stu-id="128e2-108">Supported languages include English, Spanish, French, German, Italian, Chinese (Mandarin, Simplified), Portuguese, Arabic, Russian, and Japanese.</span></span>

<span data-ttu-id="128e2-109">The **Azure Media Indexer 2 Preview** MP is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="128e2-109">The **Azure Media Indexer 2 Preview** MP is currently in Preview.</span></span>

<span data-ttu-id="128e2-110">This article shows how to create indexing jobs with **Azure Media Indexer 2 Preview**.</span><span class="sxs-lookup"><span data-stu-id="128e2-110">This article shows how to create indexing jobs with **Azure Media Indexer 2 Preview**.</span></span>

> [!NOTE]
> <span data-ttu-id="128e2-111">The following considerations apply:</span><span class="sxs-lookup"><span data-stu-id="128e2-111">The following considerations apply:</span></span>
> 
> <span data-ttu-id="128e2-112">Indexer 2 is not supported in Azure China and Azure Government.</span><span class="sxs-lookup"><span data-stu-id="128e2-112">Indexer 2 is not supported in Azure China and Azure Government.</span></span>
> 
> <span data-ttu-id="128e2-113">When indexing content, make sure to use media files that have very clear speech (without background music, noise, effects, or microphone hiss).</span><span class="sxs-lookup"><span data-stu-id="128e2-113">When indexing content, make sure to use media files that have very clear speech (without background music, noise, effects, or microphone hiss).</span></span> <span data-ttu-id="128e2-114">Some examples of appropriate content are: recorded meetings, lectures, or presentations.</span><span class="sxs-lookup"><span data-stu-id="128e2-114">Some examples of appropriate content are: recorded meetings, lectures, or presentations.</span></span> <span data-ttu-id="128e2-115">The following content might not be suitable for indexing: movies, TV shows, anything with mixed audio and sound effects, poorly recorded content with background noise (hiss).</span><span class="sxs-lookup"><span data-stu-id="128e2-115">The following content might not be suitable for indexing: movies, TV shows, anything with mixed audio and sound effects, poorly recorded content with background noise (hiss).</span></span>
> 
> 

<span data-ttu-id="128e2-116">This article gives details about  **Azure Media Indexer 2 Preview** and shows how to use it with Media Services SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="128e2-116">This article gives details about  **Azure Media Indexer 2 Preview** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="input-and-output-files"></a><span data-ttu-id="128e2-117">Input and output files</span><span class="sxs-lookup"><span data-stu-id="128e2-117">Input and output files</span></span>
### <a name="input-files"></a><span data-ttu-id="128e2-118">Input files</span><span class="sxs-lookup"><span data-stu-id="128e2-118">Input files</span></span>
<span data-ttu-id="128e2-119">Audio or video files</span><span class="sxs-lookup"><span data-stu-id="128e2-119">Audio or video files</span></span>

### <a name="output-files"></a><span data-ttu-id="128e2-120">Output files</span><span class="sxs-lookup"><span data-stu-id="128e2-120">Output files</span></span>
<span data-ttu-id="128e2-121">An indexing job can generate closed caption files in the following formats:</span><span class="sxs-lookup"><span data-stu-id="128e2-121">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="128e2-122">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="128e2-122">**SAMI**</span></span>
* <span data-ttu-id="128e2-123">**TTML**</span><span class="sxs-lookup"><span data-stu-id="128e2-123">**TTML**</span></span>
* <span data-ttu-id="128e2-124">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="128e2-124">**WebVTT**</span></span>

<span data-ttu-id="128e2-125">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span><span class="sxs-lookup"><span data-stu-id="128e2-125">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="128e2-126">Task configuration (preset)</span><span class="sxs-lookup"><span data-stu-id="128e2-126">Task configuration (preset)</span></span>
<span data-ttu-id="128e2-127">When creating an indexing task with **Azure Media Indexer 2 Preview**, you must specify a configuration preset.</span><span class="sxs-lookup"><span data-stu-id="128e2-127">When creating an indexing task with **Azure Media Indexer 2 Preview**, you must specify a configuration preset.</span></span>

<span data-ttu-id="128e2-128">The following JSON sets available parameters.</span><span class="sxs-lookup"><span data-stu-id="128e2-128">The following JSON sets available parameters.</span></span>

```json
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
```

## <a name="supported-languages"></a><span data-ttu-id="128e2-129">Supported languages</span><span class="sxs-lookup"><span data-stu-id="128e2-129">Supported languages</span></span>
<span data-ttu-id="128e2-130">Azure Media Indexer 2 Preview supports speech-to-text for the following languages (when specifying the language name in the task configuration, use 4-character code in brackets as shown below):</span><span class="sxs-lookup"><span data-stu-id="128e2-130">Azure Media Indexer 2 Preview supports speech-to-text for the following languages (when specifying the language name in the task configuration, use 4-character code in brackets as shown below):</span></span>

* <span data-ttu-id="128e2-131">English [EnUs]</span><span class="sxs-lookup"><span data-stu-id="128e2-131">English [EnUs]</span></span>
* <span data-ttu-id="128e2-132">Spanish [EsEs]</span><span class="sxs-lookup"><span data-stu-id="128e2-132">Spanish [EsEs]</span></span>
* <span data-ttu-id="128e2-133">Chinese (Mandarin, Simplified) [ZhCn]</span><span class="sxs-lookup"><span data-stu-id="128e2-133">Chinese (Mandarin, Simplified) [ZhCn]</span></span>
* <span data-ttu-id="128e2-134">French [FrFr]</span><span class="sxs-lookup"><span data-stu-id="128e2-134">French [FrFr]</span></span>
* <span data-ttu-id="128e2-135">German [DeDe]</span><span class="sxs-lookup"><span data-stu-id="128e2-135">German [DeDe]</span></span>
* <span data-ttu-id="128e2-136">Italian [ItIt]</span><span class="sxs-lookup"><span data-stu-id="128e2-136">Italian [ItIt]</span></span>
* <span data-ttu-id="128e2-137">Portuguese  [PtBr]</span><span class="sxs-lookup"><span data-stu-id="128e2-137">Portuguese  [PtBr]</span></span>
* <span data-ttu-id="128e2-138">Arabic (Egyptian) [ArEg]</span><span class="sxs-lookup"><span data-stu-id="128e2-138">Arabic (Egyptian) [ArEg]</span></span>
* <span data-ttu-id="128e2-139">Japanese [JaJp]</span><span class="sxs-lookup"><span data-stu-id="128e2-139">Japanese [JaJp]</span></span>
* <span data-ttu-id="128e2-140">Russian [RuRu]</span><span class="sxs-lookup"><span data-stu-id="128e2-140">Russian [RuRu]</span></span>
* <span data-ttu-id="128e2-141">British English [EnGb]</span><span class="sxs-lookup"><span data-stu-id="128e2-141">British English [EnGb]</span></span>
* <span data-ttu-id="128e2-142">Mexican Spanish [EsMx]</span><span class="sxs-lookup"><span data-stu-id="128e2-142">Mexican Spanish [EsMx]</span></span> 

## <a name="supported-file-types"></a><span data-ttu-id="128e2-143">Supported file types</span><span class="sxs-lookup"><span data-stu-id="128e2-143">Supported file types</span></span>

<span data-ttu-id="128e2-144">For information about supported files types, see the [supported codecs/formats](media-services-media-encoder-standard-formats.md#input-containerfile-formats) section.</span><span class="sxs-lookup"><span data-stu-id="128e2-144">For information about supported files types, see the [supported codecs/formats](media-services-media-encoder-standard-formats.md#input-containerfile-formats) section.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="128e2-145">.NET sample code</span><span class="sxs-lookup"><span data-stu-id="128e2-145">.NET sample code</span></span>

<span data-ttu-id="128e2-146">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="128e2-146">The following program shows how to:</span></span>

1. <span data-ttu-id="128e2-147">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="128e2-147">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="128e2-148">Create a job with an indexing task based on a configuration file that contains the following json preset:</span><span class="sxs-lookup"><span data-stu-id="128e2-148">Create a job with an indexing task based on a configuration file that contains the following json preset:</span></span>

    ```json
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
    ```
    
3. <span data-ttu-id="128e2-149">Download the output files.</span><span class="sxs-lookup"><span data-stu-id="128e2-149">Download the output files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="128e2-150">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="128e2-150">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="128e2-151">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="128e2-151">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="128e2-152">Example</span><span class="sxs-lookup"><span data-stu-id="128e2-152">Example</span></span>

```csharp
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
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="128e2-153">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="128e2-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="128e2-154">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="128e2-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="128e2-155">Related links</span><span class="sxs-lookup"><span data-stu-id="128e2-155">Related links</span></span>
[<span data-ttu-id="128e2-156">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="128e2-156">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="128e2-157">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="128e2-157">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

