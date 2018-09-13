---
title: Use Azure Media Encoder Standard to auto-generate a bitrate ladder | Microsoft Docs
description: This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder based on the input resolution and bitrate. The input resolution and bitrate will never be exceeded. For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: juliako
ms.openlocfilehash: 244413be8b094605883445bb3cbf675b538b704e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540792"
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a><span data-ttu-id="0deb2-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span><span class="sxs-lookup"><span data-stu-id="0deb2-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="0deb2-106">Overview</span><span class="sxs-lookup"><span data-stu-id="0deb2-106">Overview</span></span>

<span data-ttu-id="0deb2-107">This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span><span class="sxs-lookup"><span data-stu-id="0deb2-107">This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span></span> <span data-ttu-id="0deb2-108">The auto-generated preset will never exceed the input resolution and bitrate.</span><span class="sxs-lookup"><span data-stu-id="0deb2-108">The auto-generated preset will never exceed the input resolution and bitrate.</span></span> <span data-ttu-id="0deb2-109">For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span><span class="sxs-lookup"><span data-stu-id="0deb2-109">For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

<span data-ttu-id="0deb2-110">To use this feature, you need to specify the **Adaptive Streaming** preset when creating an encoding task.</span><span class="sxs-lookup"><span data-stu-id="0deb2-110">To use this feature, you need to specify the **Adaptive Streaming** preset when creating an encoding task.</span></span> <span data-ttu-id="0deb2-111">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span><span class="sxs-lookup"><span data-stu-id="0deb2-111">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="0deb2-112">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span><span class="sxs-lookup"><span data-stu-id="0deb2-112">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span></span> <span data-ttu-id="0deb2-113">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the [end](#output) of this topic.</span><span class="sxs-lookup"><span data-stu-id="0deb2-113">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the [end](#output) of this topic.</span></span>

## <a id="encoding_with_dotnet"></a><span data-ttu-id="0deb2-114">Encoding with Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0deb2-114">Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="0deb2-115">The following code example uses Media Services .NET SDK to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="0deb2-115">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="0deb2-116">Create an encoding job.</span><span class="sxs-lookup"><span data-stu-id="0deb2-116">Create an encoding job.</span></span>
- <span data-ttu-id="0deb2-117">Get a reference to the Media Encoder Standard encoder.</span><span class="sxs-lookup"><span data-stu-id="0deb2-117">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="0deb2-118">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span><span class="sxs-lookup"><span data-stu-id="0deb2-118">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="0deb2-119">Create an output asset that will contain the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="0deb2-119">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="0deb2-120">Add an event handler to check the job progress.</span><span class="sxs-lookup"><span data-stu-id="0deb2-120">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="0deb2-121">Submit the job.</span><span class="sxs-lookup"><span data-stu-id="0deb2-121">Submit the job.</span></span>

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace AdaptiveStreamingMESPresest
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
                // Used the chached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Get an uploaded asset.
                var asset = _context.Assets.FirstOrDefault();

                // Encode and generate the output using the "Adaptive Streaming" preset.
                EncodeToAdaptiveBitrateMP4Set(asset);

                Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
                // Declare a new job.
                IJob job = _context.Jobs.Create("Media Encoder Standard Job");

                // Get a media processor reference, and pass to it the name of the 
                // processor to use for the specific task.
                IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                // Create a task
                ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
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

            }

        }

## <a id="output"></a><span data-ttu-id="0deb2-122">Output</span><span class="sxs-lookup"><span data-stu-id="0deb2-122">Output</span></span>

<span data-ttu-id="0deb2-123">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span><span class="sxs-lookup"><span data-stu-id="0deb2-123">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="0deb2-124">Example 1</span><span class="sxs-lookup"><span data-stu-id="0deb2-124">Example 1</span></span>
<span data-ttu-id="0deb2-125">Source with height "1080" and framerate "29.970" procuces 6 video layers:</span><span class="sxs-lookup"><span data-stu-id="0deb2-125">Source with height "1080" and framerate "29.970" procuces 6 video layers:</span></span>

|<span data-ttu-id="0deb2-126">Layer</span><span class="sxs-lookup"><span data-stu-id="0deb2-126">Layer</span></span>|<span data-ttu-id="0deb2-127">Height</span><span class="sxs-lookup"><span data-stu-id="0deb2-127">Height</span></span>|<span data-ttu-id="0deb2-128">Width</span><span class="sxs-lookup"><span data-stu-id="0deb2-128">Width</span></span>|<span data-ttu-id="0deb2-129">Bitrate(kbps)</span><span class="sxs-lookup"><span data-stu-id="0deb2-129">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="0deb2-130">1</span><span class="sxs-lookup"><span data-stu-id="0deb2-130">1</span></span>|<span data-ttu-id="0deb2-131">1080</span><span class="sxs-lookup"><span data-stu-id="0deb2-131">1080</span></span>|<span data-ttu-id="0deb2-132">1920</span><span class="sxs-lookup"><span data-stu-id="0deb2-132">1920</span></span>|<span data-ttu-id="0deb2-133">6780</span><span class="sxs-lookup"><span data-stu-id="0deb2-133">6780</span></span>|
|<span data-ttu-id="0deb2-134">2</span><span class="sxs-lookup"><span data-stu-id="0deb2-134">2</span></span>|<span data-ttu-id="0deb2-135">720</span><span class="sxs-lookup"><span data-stu-id="0deb2-135">720</span></span>|<span data-ttu-id="0deb2-136">1280</span><span class="sxs-lookup"><span data-stu-id="0deb2-136">1280</span></span>|<span data-ttu-id="0deb2-137">3520</span><span class="sxs-lookup"><span data-stu-id="0deb2-137">3520</span></span>|
|<span data-ttu-id="0deb2-138">3</span><span class="sxs-lookup"><span data-stu-id="0deb2-138">3</span></span>|<span data-ttu-id="0deb2-139">540</span><span class="sxs-lookup"><span data-stu-id="0deb2-139">540</span></span>|<span data-ttu-id="0deb2-140">960</span><span class="sxs-lookup"><span data-stu-id="0deb2-140">960</span></span>|<span data-ttu-id="0deb2-141">2210</span><span class="sxs-lookup"><span data-stu-id="0deb2-141">2210</span></span>|
|<span data-ttu-id="0deb2-142">4</span><span class="sxs-lookup"><span data-stu-id="0deb2-142">4</span></span>|<span data-ttu-id="0deb2-143">360</span><span class="sxs-lookup"><span data-stu-id="0deb2-143">360</span></span>|<span data-ttu-id="0deb2-144">640</span><span class="sxs-lookup"><span data-stu-id="0deb2-144">640</span></span>|<span data-ttu-id="0deb2-145">1150</span><span class="sxs-lookup"><span data-stu-id="0deb2-145">1150</span></span>|
|<span data-ttu-id="0deb2-146">5</span><span class="sxs-lookup"><span data-stu-id="0deb2-146">5</span></span>|<span data-ttu-id="0deb2-147">270</span><span class="sxs-lookup"><span data-stu-id="0deb2-147">270</span></span>|<span data-ttu-id="0deb2-148">480</span><span class="sxs-lookup"><span data-stu-id="0deb2-148">480</span></span>|<span data-ttu-id="0deb2-149">720</span><span class="sxs-lookup"><span data-stu-id="0deb2-149">720</span></span>|
|<span data-ttu-id="0deb2-150">6</span><span class="sxs-lookup"><span data-stu-id="0deb2-150">6</span></span>|<span data-ttu-id="0deb2-151">180</span><span class="sxs-lookup"><span data-stu-id="0deb2-151">180</span></span>|<span data-ttu-id="0deb2-152">320</span><span class="sxs-lookup"><span data-stu-id="0deb2-152">320</span></span>|<span data-ttu-id="0deb2-153">380</span><span class="sxs-lookup"><span data-stu-id="0deb2-153">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="0deb2-154">Example 2</span><span class="sxs-lookup"><span data-stu-id="0deb2-154">Example 2</span></span>
<span data-ttu-id="0deb2-155">Source with height "720" and framerate "23.970" procuces 5 video layers:</span><span class="sxs-lookup"><span data-stu-id="0deb2-155">Source with height "720" and framerate "23.970" procuces 5 video layers:</span></span>

|<span data-ttu-id="0deb2-156">Layer</span><span class="sxs-lookup"><span data-stu-id="0deb2-156">Layer</span></span>|<span data-ttu-id="0deb2-157">Height</span><span class="sxs-lookup"><span data-stu-id="0deb2-157">Height</span></span>|<span data-ttu-id="0deb2-158">Width</span><span class="sxs-lookup"><span data-stu-id="0deb2-158">Width</span></span>|<span data-ttu-id="0deb2-159">Bitrate(kbps)</span><span class="sxs-lookup"><span data-stu-id="0deb2-159">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="0deb2-160">1</span><span class="sxs-lookup"><span data-stu-id="0deb2-160">1</span></span>|<span data-ttu-id="0deb2-161">720</span><span class="sxs-lookup"><span data-stu-id="0deb2-161">720</span></span>|<span data-ttu-id="0deb2-162">1280</span><span class="sxs-lookup"><span data-stu-id="0deb2-162">1280</span></span>|<span data-ttu-id="0deb2-163">2940</span><span class="sxs-lookup"><span data-stu-id="0deb2-163">2940</span></span>|
|<span data-ttu-id="0deb2-164">2</span><span class="sxs-lookup"><span data-stu-id="0deb2-164">2</span></span>|<span data-ttu-id="0deb2-165">540</span><span class="sxs-lookup"><span data-stu-id="0deb2-165">540</span></span>|<span data-ttu-id="0deb2-166">960</span><span class="sxs-lookup"><span data-stu-id="0deb2-166">960</span></span>|<span data-ttu-id="0deb2-167">1850</span><span class="sxs-lookup"><span data-stu-id="0deb2-167">1850</span></span>|
|<span data-ttu-id="0deb2-168">3</span><span class="sxs-lookup"><span data-stu-id="0deb2-168">3</span></span>|<span data-ttu-id="0deb2-169">360</span><span class="sxs-lookup"><span data-stu-id="0deb2-169">360</span></span>|<span data-ttu-id="0deb2-170">640</span><span class="sxs-lookup"><span data-stu-id="0deb2-170">640</span></span>|<span data-ttu-id="0deb2-171">960</span><span class="sxs-lookup"><span data-stu-id="0deb2-171">960</span></span>|
|<span data-ttu-id="0deb2-172">4</span><span class="sxs-lookup"><span data-stu-id="0deb2-172">4</span></span>|<span data-ttu-id="0deb2-173">270</span><span class="sxs-lookup"><span data-stu-id="0deb2-173">270</span></span>|<span data-ttu-id="0deb2-174">480</span><span class="sxs-lookup"><span data-stu-id="0deb2-174">480</span></span>|<span data-ttu-id="0deb2-175">600</span><span class="sxs-lookup"><span data-stu-id="0deb2-175">600</span></span>|
|<span data-ttu-id="0deb2-176">5</span><span class="sxs-lookup"><span data-stu-id="0deb2-176">5</span></span>|<span data-ttu-id="0deb2-177">180</span><span class="sxs-lookup"><span data-stu-id="0deb2-177">180</span></span>|<span data-ttu-id="0deb2-178">320</span><span class="sxs-lookup"><span data-stu-id="0deb2-178">320</span></span>|<span data-ttu-id="0deb2-179">320</span><span class="sxs-lookup"><span data-stu-id="0deb2-179">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="0deb2-180">Example 3</span><span class="sxs-lookup"><span data-stu-id="0deb2-180">Example 3</span></span>
<span data-ttu-id="0deb2-181">Source with height "360" and framerate "29.970" procuces 3 video layers:</span><span class="sxs-lookup"><span data-stu-id="0deb2-181">Source with height "360" and framerate "29.970" procuces 3 video layers:</span></span>

|<span data-ttu-id="0deb2-182">Layer</span><span class="sxs-lookup"><span data-stu-id="0deb2-182">Layer</span></span>|<span data-ttu-id="0deb2-183">Height</span><span class="sxs-lookup"><span data-stu-id="0deb2-183">Height</span></span>|<span data-ttu-id="0deb2-184">Width</span><span class="sxs-lookup"><span data-stu-id="0deb2-184">Width</span></span>|<span data-ttu-id="0deb2-185">Bitrate(kbps)</span><span class="sxs-lookup"><span data-stu-id="0deb2-185">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="0deb2-186">1</span><span class="sxs-lookup"><span data-stu-id="0deb2-186">1</span></span>|<span data-ttu-id="0deb2-187">360</span><span class="sxs-lookup"><span data-stu-id="0deb2-187">360</span></span>|<span data-ttu-id="0deb2-188">640</span><span class="sxs-lookup"><span data-stu-id="0deb2-188">640</span></span>|<span data-ttu-id="0deb2-189">700</span><span class="sxs-lookup"><span data-stu-id="0deb2-189">700</span></span>|
|<span data-ttu-id="0deb2-190">2</span><span class="sxs-lookup"><span data-stu-id="0deb2-190">2</span></span>|<span data-ttu-id="0deb2-191">270</span><span class="sxs-lookup"><span data-stu-id="0deb2-191">270</span></span>|<span data-ttu-id="0deb2-192">480</span><span class="sxs-lookup"><span data-stu-id="0deb2-192">480</span></span>|<span data-ttu-id="0deb2-193">440</span><span class="sxs-lookup"><span data-stu-id="0deb2-193">440</span></span>|
|<span data-ttu-id="0deb2-194">3</span><span class="sxs-lookup"><span data-stu-id="0deb2-194">3</span></span>|<span data-ttu-id="0deb2-195">180</span><span class="sxs-lookup"><span data-stu-id="0deb2-195">180</span></span>|<span data-ttu-id="0deb2-196">320</span><span class="sxs-lookup"><span data-stu-id="0deb2-196">320</span></span>|<span data-ttu-id="0deb2-197">230</span><span class="sxs-lookup"><span data-stu-id="0deb2-197">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="0deb2-198">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="0deb2-198">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0deb2-199">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="0deb2-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="0deb2-200">See Also</span><span class="sxs-lookup"><span data-stu-id="0deb2-200">See Also</span></span>
[<span data-ttu-id="0deb2-201">Media Services Encoding Overview</span><span class="sxs-lookup"><span data-stu-id="0deb2-201">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

