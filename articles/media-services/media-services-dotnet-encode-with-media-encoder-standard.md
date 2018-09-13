---
title: Encode an asset with Media Encoder Standard using .NET | Microsoft Docs
description: This topic shows how to use .NET to encode an asset using Media Encoder Strandard.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 9acb23c679e4a8279c944a384d142b1cccf0f4d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661331"
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="cec25-103">Encode an asset with Media Encoder Standard using .NET</span><span class="sxs-lookup"><span data-stu-id="cec25-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="cec25-104">Encoding jobs are one of the most common processing operations in Media Services.</span><span class="sxs-lookup"><span data-stu-id="cec25-104">Encoding jobs are one of the most common processing operations in Media Services.</span></span> <span data-ttu-id="cec25-105">You create encoding jobs to convert media files from one encoding to another.</span><span class="sxs-lookup"><span data-stu-id="cec25-105">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="cec25-106">When you encode, you can use the Media Services built-in Media Encoder.</span><span class="sxs-lookup"><span data-stu-id="cec25-106">When you encode, you can use the Media Services built-in Media Encoder.</span></span> <span data-ttu-id="cec25-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cec25-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through the Azure Marketplace.</span></span> 

<span data-ttu-id="cec25-108">This topic shows how to use .NET to encode your assets with Media Encoder Standard (MES).</span><span class="sxs-lookup"><span data-stu-id="cec25-108">This topic shows how to use .NET to encode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="cec25-109">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cec25-109">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="cec25-110">It is recommended to always encode your mezzanine files into an adaptive bitrate MP4 set and then convert the set to the desired format using the [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cec25-110">It is recommended to always encode your mezzanine files into an adaptive bitrate MP4 set and then convert the set to the desired format using the [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="cec25-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="cec25-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="cec25-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="cec25-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cec25-113">MES produces an output file with a name that contains the first 32 characters of the input file name.</span><span class="sxs-lookup"><span data-stu-id="cec25-113">MES produces an output file with a name that contains the first 32 characters of the input file name.</span></span> <span data-ttu-id="cec25-114">The name is based on what is specified in the preset file.</span><span class="sxs-lookup"><span data-stu-id="cec25-114">The name is based on what is specified in the preset file.</span></span> <span data-ttu-id="cec25-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span><span class="sxs-lookup"><span data-stu-id="cec25-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="cec25-116">{Basename} is replaced by the first 32 characters of the input file name.</span><span class="sxs-lookup"><span data-stu-id="cec25-116">{Basename} is replaced by the first 32 characters of the input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="cec25-117">MES Formats</span><span class="sxs-lookup"><span data-stu-id="cec25-117">MES Formats</span></span>
[<span data-ttu-id="cec25-118">Formats and codecs</span><span class="sxs-lookup"><span data-stu-id="cec25-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="cec25-119">MES Presets</span><span class="sxs-lookup"><span data-stu-id="cec25-119">MES Presets</span></span>
<span data-ttu-id="cec25-120">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cec25-120">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="cec25-121">Input and output metadata</span><span class="sxs-lookup"><span data-stu-id="cec25-121">Input and output metadata</span></span>
<span data-ttu-id="cec25-122">When you encode an input asset (or assets) using MES, you get an output asset at the successful completion of that encode task.</span><span class="sxs-lookup"><span data-stu-id="cec25-122">When you encode an input asset (or assets) using MES, you get an output asset at the successful completion of that encode task.</span></span> <span data-ttu-id="cec25-123">The output asset contains video, audio, thumbnails, manifest, etc. based on the encoding preset you use.</span><span class="sxs-lookup"><span data-stu-id="cec25-123">The output asset contains video, audio, thumbnails, manifest, etc. based on the encoding preset you use.</span></span>

<span data-ttu-id="cec25-124">The output asset also contains a file with metadata about the input asset.</span><span class="sxs-lookup"><span data-stu-id="cec25-124">The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="cec25-125">The name of the metadata XML file has the following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is the AssetId value of the input asset.</span><span class="sxs-lookup"><span data-stu-id="cec25-125">The name of the metadata XML file has the following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is the AssetId value of the input asset.</span></span> <span data-ttu-id="cec25-126">The schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="cec25-126">The schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="cec25-127">The output asset also contains a file with metadata about the output asset.</span><span class="sxs-lookup"><span data-stu-id="cec25-127">The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="cec25-128">The name of the metadata XML file has the following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="cec25-128">The name of the metadata XML file has the following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="cec25-129">The schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="cec25-129">The schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="cec25-130">If you want to examine either of the two metadata files, you can create a SAS locator and download the file to your local computer.</span><span class="sxs-lookup"><span data-stu-id="cec25-130">If you want to examine either of the two metadata files, you can create a SAS locator and download the file to your local computer.</span></span> <span data-ttu-id="cec25-131">You can find an example on how to create a SAS locator and download a file Using the Media Services .NET SDK Extensions.</span><span class="sxs-lookup"><span data-stu-id="cec25-131">You can find an example on how to create a SAS locator and download a file Using the Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="cec25-132">Download sample</span><span class="sxs-lookup"><span data-stu-id="cec25-132">Download sample</span></span>
<span data-ttu-id="cec25-133">You can get and run a sample that shows how to encode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="cec25-133">You can get and run a sample that shows how to encode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="example"></a><span data-ttu-id="cec25-134">Example</span><span class="sxs-lookup"><span data-stu-id="cec25-134">Example</span></span>
<span data-ttu-id="cec25-135">The following code example uses Media Services .NET SDK to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="cec25-135">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="cec25-136">Create an encoding job.</span><span class="sxs-lookup"><span data-stu-id="cec25-136">Create an encoding job.</span></span>
* <span data-ttu-id="cec25-137">Get a reference to the Media Encoder Standard encoder.</span><span class="sxs-lookup"><span data-stu-id="cec25-137">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="cec25-138">Specify to use the [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span><span class="sxs-lookup"><span data-stu-id="cec25-138">Specify to use the [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="cec25-139">Add a single encoding task to the job.</span><span class="sxs-lookup"><span data-stu-id="cec25-139">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="cec25-140">Specify the input asset to be encoded.</span><span class="sxs-lookup"><span data-stu-id="cec25-140">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="cec25-141">Create an output asset that will contain the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="cec25-141">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="cec25-142">Add an event handler to check the job progress.</span><span class="sxs-lookup"><span data-stu-id="cec25-142">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="cec25-143">Submit the job.</span><span class="sxs-lookup"><span data-stu-id="cec25-143">Submit the job.</span></span>
  
        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
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
                    break;
                default:
                    break;
            }
        }


        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }


## <a name="media-services-learning-paths"></a><span data-ttu-id="cec25-144">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="cec25-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cec25-145">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="cec25-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="cec25-146">See Also</span><span class="sxs-lookup"><span data-stu-id="cec25-146">See Also</span></span>
<span data-ttu-id="cec25-147">[How to generate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="cec25-147">[How to generate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

