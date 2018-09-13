---
title: Hyperlapse Media Files with Azure Media Hyperlapse  | Microsoft Docs
description: Azure Media Hyperlapse creates smooth time-lapsed videos from first-person or action-camera content. This topic shows how to use Media Indexer.
services: media-services
documentationcenter: ''
author: asolanki
manager: johndeu
editor: ''
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 02f634c2af04b6b372642ab0e6a17a5d29f16450
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553958"
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="b07f6-104">Hyperlapse Media Files with Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="b07f6-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="b07f6-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span><span class="sxs-lookup"><span data-stu-id="b07f6-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="b07f6-106">The cloud-based sibling to [Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes the massive scale of the Azure Media Services Media Processing platform to horizontally scale and parallelize bulk Hyperlapse processing.</span><span class="sxs-lookup"><span data-stu-id="b07f6-106">The cloud-based sibling to [Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes the massive scale of the Azure Media Services Media Processing platform to horizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b07f6-107">Microsoft Hyperlapse is designed to work best on first-person content with a moving camera.</span><span class="sxs-lookup"><span data-stu-id="b07f6-107">Microsoft Hyperlapse is designed to work best on first-person content with a moving camera.</span></span>  <span data-ttu-id="b07f6-108">Although still-camera footage can still work, the performance and quality of the Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span><span class="sxs-lookup"><span data-stu-id="b07f6-108">Although still-camera footage can still work, the performance and quality of the Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="b07f6-109">To learn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out the [introductory blog post](http://aka.ms/azurehyperlapseblog) from the public preview.</span><span class="sxs-lookup"><span data-stu-id="b07f6-109">To learn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out the [introductory blog post](http://aka.ms/azurehyperlapseblog) from the public preview.</span></span>
> 
> 

<span data-ttu-id="b07f6-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and to what speed (e.g. first 10,000 frames at 2x).</span><span class="sxs-lookup"><span data-stu-id="b07f6-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and to what speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="b07f6-111">The output is a stabilized and time-lapsed rendition of the input video.</span><span class="sxs-lookup"><span data-stu-id="b07f6-111">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

<span data-ttu-id="b07f6-112">For the latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="b07f6-112">For the latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="b07f6-113">Hyperlapse an asset</span><span class="sxs-lookup"><span data-stu-id="b07f6-113">Hyperlapse an asset</span></span>
<span data-ttu-id="b07f6-114">First you will need to upload your desired input file to Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b07f6-114">First you will need to upload your desired input file to Azure Media Services.</span></span>  <span data-ttu-id="b07f6-115">To learn more about the concepts involved with uploading and managing content, read the [content management article](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b07f6-115">To learn more about the concepts involved with uploading and managing content, read the [content management article](media-services-portal-vod-get-started.md).</span></span>

### <a id="configuration"></a><span data-ttu-id="b07f6-116">Configuration Preset for Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="b07f6-116">Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="b07f6-117">Once your content is in your Media Services account, you will need to construct your configuration preset.</span><span class="sxs-lookup"><span data-stu-id="b07f6-117">Once your content is in your Media Services account, you will need to construct your configuration preset.</span></span>  <span data-ttu-id="b07f6-118">The following table explains the user-specified fields:</span><span class="sxs-lookup"><span data-stu-id="b07f6-118">The following table explains the user-specified fields:</span></span>

| <span data-ttu-id="b07f6-119">Field</span><span class="sxs-lookup"><span data-stu-id="b07f6-119">Field</span></span> | <span data-ttu-id="b07f6-120">Description</span><span class="sxs-lookup"><span data-stu-id="b07f6-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b07f6-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="b07f6-121">StartFrame</span></span> |<span data-ttu-id="b07f6-122">The frame upon which the Microsoft Hyperlapse processing should begin.</span><span class="sxs-lookup"><span data-stu-id="b07f6-122">The frame upon which the Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="b07f6-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="b07f6-123">NumFrames</span></span> |<span data-ttu-id="b07f6-124">The number of frames to process</span><span class="sxs-lookup"><span data-stu-id="b07f6-124">The number of frames to process</span></span> |
| <span data-ttu-id="b07f6-125">Speed</span><span class="sxs-lookup"><span data-stu-id="b07f6-125">Speed</span></span> |<span data-ttu-id="b07f6-126">The factor with which to speed up the input video.</span><span class="sxs-lookup"><span data-stu-id="b07f6-126">The factor with which to speed up the input video.</span></span> |

<span data-ttu-id="b07f6-127">The following is an example of a conformant configuration file in XML and JSON:</span><span class="sxs-lookup"><span data-stu-id="b07f6-127">The following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="b07f6-128">**XML preset:**</span><span class="sxs-lookup"><span data-stu-id="b07f6-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="b07f6-129">**JSON preset:**</span><span class="sxs-lookup"><span data-stu-id="b07f6-129">**JSON preset:**</span></span>

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <a id="sample_code"></a> <span data-ttu-id="b07f6-130">Microsoft Hyperlapse with the AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b07f6-130">Microsoft Hyperlapse with the AMS .NET SDK</span></span>
<span data-ttu-id="b07f6-131">The following method uploads a media file as an asset and creates a job with the Azure Media Hyperlapse Media Processor.</span><span class="sxs-lookup"><span data-stu-id="b07f6-131">The following method uploads a media file as an asset and creates a job with the Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="b07f6-132">You should already have a CloudMediaContext in scope with the name "context" for this code to work.</span><span class="sxs-lookup"><span data-stu-id="b07f6-132">You should already have a CloudMediaContext in scope with the name "context" for this code to work.</span></span>  <span data-ttu-id="b07f6-133">To learn more about this, read the [content management article](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b07f6-133">To learn more about this, read the [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="b07f6-134">The string argument "hyperConfig" is expected to be a conformant configuration preset in either JSON or XML as described above.</span><span class="sxs-lookup"><span data-stu-id="b07f6-134">The string argument "hyperConfig" is expected to be a conformant configuration preset in either JSON or XML as described above.</span></span>
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
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
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <a id="file_types"></a><span data-ttu-id="b07f6-135">Supported File types</span><span class="sxs-lookup"><span data-stu-id="b07f6-135">Supported File types</span></span>
* <span data-ttu-id="b07f6-136">MP4</span><span class="sxs-lookup"><span data-stu-id="b07f6-136">MP4</span></span>
* <span data-ttu-id="b07f6-137">MOV</span><span class="sxs-lookup"><span data-stu-id="b07f6-137">MOV</span></span>
* <span data-ttu-id="b07f6-138">WMV</span><span class="sxs-lookup"><span data-stu-id="b07f6-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b07f6-139">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="b07f6-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b07f6-140">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="b07f6-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="b07f6-141">Related links</span><span class="sxs-lookup"><span data-stu-id="b07f6-141">Related links</span></span>
[<span data-ttu-id="b07f6-142">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="b07f6-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="b07f6-143">Azure Media Analytics demos</span><span class="sxs-lookup"><span data-stu-id="b07f6-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

