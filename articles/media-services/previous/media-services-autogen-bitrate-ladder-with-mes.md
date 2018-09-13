---
title: Use Azure Media Encoder Standard to auto-generate a bitrate ladder | Microsoft Docs
description: This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder based on the input resolution and bitrate. The input resolution and bitrate will never be exceeded. For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2017
ms.author: juliako
ms.openlocfilehash: 80f76f413ec2c267ba8fb93514480e168563f470
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855990"
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a><span data-ttu-id="1a13a-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span><span class="sxs-lookup"><span data-stu-id="1a13a-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="1a13a-106">Overview</span><span class="sxs-lookup"><span data-stu-id="1a13a-106">Overview</span></span>

<span data-ttu-id="1a13a-107">This article shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span><span class="sxs-lookup"><span data-stu-id="1a13a-107">This article shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span></span> <span data-ttu-id="1a13a-108">The auto-generated preset will never exceed the input resolution and bitrate.</span><span class="sxs-lookup"><span data-stu-id="1a13a-108">The auto-generated preset will never exceed the input resolution and bitrate.</span></span> <span data-ttu-id="1a13a-109">For example, if the input is 720p at 3 Mbps, output remains 720p at best, and will start at rates lower than 3 Mbps.</span><span class="sxs-lookup"><span data-stu-id="1a13a-109">For example, if the input is 720p at 3 Mbps, output remains 720p at best, and will start at rates lower than 3 Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="1a13a-110">Encoding for Streaming Only</span><span class="sxs-lookup"><span data-stu-id="1a13a-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="1a13a-111">If your intent is to encode your source video only for streaming, then you should use the "Adaptive Streaming" preset when creating an encoding task.</span><span class="sxs-lookup"><span data-stu-id="1a13a-111">If your intent is to encode your source video only for streaming, then you should use the "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="1a13a-112">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span><span class="sxs-lookup"><span data-stu-id="1a13a-112">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="1a13a-113">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span><span class="sxs-lookup"><span data-stu-id="1a13a-113">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span></span> <span data-ttu-id="1a13a-114">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="1a13a-114">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the end of this article.</span></span> <span data-ttu-id="1a13a-115">The output Asset contains MP4 files where audio and video is not interleaved.</span><span class="sxs-lookup"><span data-stu-id="1a13a-115">The output Asset contains MP4 files where audio and video is not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="1a13a-116">Encoding for Streaming and Progressive Download</span><span class="sxs-lookup"><span data-stu-id="1a13a-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="1a13a-117">If your intent is to encode your source video for streaming as well as to produce MP4 files for progressive download, then you should use the "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span><span class="sxs-lookup"><span data-stu-id="1a13a-117">If your intent is to encode your source video for streaming as well as to produce MP4 files for progressive download, then you should use the "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="1a13a-118">When using the **Content Adaptive Multiple Bitrate MP4** preset, the MES encoder applies the same encoding logic as above, but now the output asset will contain MP4 files where audio and video is interleaved.</span><span class="sxs-lookup"><span data-stu-id="1a13a-118">When using the **Content Adaptive Multiple Bitrate MP4** preset, the MES encoder applies the same encoding logic as above, but now the output asset will contain MP4 files where audio and video is interleaved.</span></span> <span data-ttu-id="1a13a-119">You can use one of these MP4 files (for example, the highest bitrate version) as a progressive download file.</span><span class="sxs-lookup"><span data-stu-id="1a13a-119">You can use one of these MP4 files (for example, the highest bitrate version) as a progressive download file.</span></span>

## <a id="encoding_with_dotnet"></a><span data-ttu-id="1a13a-120">Encoding with Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1a13a-120">Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="1a13a-121">The following code example uses Media Services .NET SDK to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="1a13a-121">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="1a13a-122">Create an encoding job.</span><span class="sxs-lookup"><span data-stu-id="1a13a-122">Create an encoding job.</span></span>
- <span data-ttu-id="1a13a-123">Get a reference to the Media Encoder Standard encoder.</span><span class="sxs-lookup"><span data-stu-id="1a13a-123">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="1a13a-124">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span><span class="sxs-lookup"><span data-stu-id="1a13a-124">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="1a13a-125">Create an output asset that contains the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="1a13a-125">Create an output asset that contains the encoded asset.</span></span>
- <span data-ttu-id="1a13a-126">Add an event handler to check the job progress.</span><span class="sxs-lookup"><span data-stu-id="1a13a-126">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="1a13a-127">Submit the job.</span><span class="sxs-lookup"><span data-stu-id="1a13a-127">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="1a13a-128">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="1a13a-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="1a13a-129">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1a13a-129">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="1a13a-130">Example</span><span class="sxs-lookup"><span data-stu-id="1a13a-130">Example</span></span>

```
using System;
using System.Configuration;
using System.Linq;
using Microsoft.WindowsAzure.MediaServices.Client;
using System.Threading;

namespace AdaptiveStreamingMESPresest
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
```

## <a id="output"></a><span data-ttu-id="1a13a-131">Output</span><span class="sxs-lookup"><span data-stu-id="1a13a-131">Output</span></span>

<span data-ttu-id="1a13a-132">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span><span class="sxs-lookup"><span data-stu-id="1a13a-132">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="1a13a-133">Example 1</span><span class="sxs-lookup"><span data-stu-id="1a13a-133">Example 1</span></span>
<span data-ttu-id="1a13a-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span><span class="sxs-lookup"><span data-stu-id="1a13a-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="1a13a-135">Layer</span><span class="sxs-lookup"><span data-stu-id="1a13a-135">Layer</span></span>|<span data-ttu-id="1a13a-136">Height</span><span class="sxs-lookup"><span data-stu-id="1a13a-136">Height</span></span>|<span data-ttu-id="1a13a-137">Width</span><span class="sxs-lookup"><span data-stu-id="1a13a-137">Width</span></span>|<span data-ttu-id="1a13a-138">Bitrate(kbps)</span><span class="sxs-lookup"><span data-stu-id="1a13a-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="1a13a-139">1</span><span class="sxs-lookup"><span data-stu-id="1a13a-139">1</span></span>|<span data-ttu-id="1a13a-140">1080</span><span class="sxs-lookup"><span data-stu-id="1a13a-140">1080</span></span>|<span data-ttu-id="1a13a-141">1920</span><span class="sxs-lookup"><span data-stu-id="1a13a-141">1920</span></span>|<span data-ttu-id="1a13a-142">6780</span><span class="sxs-lookup"><span data-stu-id="1a13a-142">6780</span></span>|
|<span data-ttu-id="1a13a-143">2</span><span class="sxs-lookup"><span data-stu-id="1a13a-143">2</span></span>|<span data-ttu-id="1a13a-144">720</span><span class="sxs-lookup"><span data-stu-id="1a13a-144">720</span></span>|<span data-ttu-id="1a13a-145">1280</span><span class="sxs-lookup"><span data-stu-id="1a13a-145">1280</span></span>|<span data-ttu-id="1a13a-146">3520</span><span class="sxs-lookup"><span data-stu-id="1a13a-146">3520</span></span>|
|<span data-ttu-id="1a13a-147">3</span><span class="sxs-lookup"><span data-stu-id="1a13a-147">3</span></span>|<span data-ttu-id="1a13a-148">540</span><span class="sxs-lookup"><span data-stu-id="1a13a-148">540</span></span>|<span data-ttu-id="1a13a-149">960</span><span class="sxs-lookup"><span data-stu-id="1a13a-149">960</span></span>|<span data-ttu-id="1a13a-150">2210</span><span class="sxs-lookup"><span data-stu-id="1a13a-150">2210</span></span>|
|<span data-ttu-id="1a13a-151">4</span><span class="sxs-lookup"><span data-stu-id="1a13a-151">4</span></span>|<span data-ttu-id="1a13a-152">360</span><span class="sxs-lookup"><span data-stu-id="1a13a-152">360</span></span>|<span data-ttu-id="1a13a-153">640</span><span class="sxs-lookup"><span data-stu-id="1a13a-153">640</span></span>|<span data-ttu-id="1a13a-154">1150</span><span class="sxs-lookup"><span data-stu-id="1a13a-154">1150</span></span>|
|<span data-ttu-id="1a13a-155">5</span><span class="sxs-lookup"><span data-stu-id="1a13a-155">5</span></span>|<span data-ttu-id="1a13a-156">270</span><span class="sxs-lookup"><span data-stu-id="1a13a-156">270</span></span>|<span data-ttu-id="1a13a-157">480</span><span class="sxs-lookup"><span data-stu-id="1a13a-157">480</span></span>|<span data-ttu-id="1a13a-158">720</span><span class="sxs-lookup"><span data-stu-id="1a13a-158">720</span></span>|
|<span data-ttu-id="1a13a-159">6</span><span class="sxs-lookup"><span data-stu-id="1a13a-159">6</span></span>|<span data-ttu-id="1a13a-160">180</span><span class="sxs-lookup"><span data-stu-id="1a13a-160">180</span></span>|<span data-ttu-id="1a13a-161">320</span><span class="sxs-lookup"><span data-stu-id="1a13a-161">320</span></span>|<span data-ttu-id="1a13a-162">380</span><span class="sxs-lookup"><span data-stu-id="1a13a-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="1a13a-163">Example 2</span><span class="sxs-lookup"><span data-stu-id="1a13a-163">Example 2</span></span>
<span data-ttu-id="1a13a-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span><span class="sxs-lookup"><span data-stu-id="1a13a-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="1a13a-165">Layer</span><span class="sxs-lookup"><span data-stu-id="1a13a-165">Layer</span></span>|<span data-ttu-id="1a13a-166">Height</span><span class="sxs-lookup"><span data-stu-id="1a13a-166">Height</span></span>|<span data-ttu-id="1a13a-167">Width</span><span class="sxs-lookup"><span data-stu-id="1a13a-167">Width</span></span>|<span data-ttu-id="1a13a-168">Bitrate(kbps)</span><span class="sxs-lookup"><span data-stu-id="1a13a-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="1a13a-169">1</span><span class="sxs-lookup"><span data-stu-id="1a13a-169">1</span></span>|<span data-ttu-id="1a13a-170">720</span><span class="sxs-lookup"><span data-stu-id="1a13a-170">720</span></span>|<span data-ttu-id="1a13a-171">1280</span><span class="sxs-lookup"><span data-stu-id="1a13a-171">1280</span></span>|<span data-ttu-id="1a13a-172">2940</span><span class="sxs-lookup"><span data-stu-id="1a13a-172">2940</span></span>|
|<span data-ttu-id="1a13a-173">2</span><span class="sxs-lookup"><span data-stu-id="1a13a-173">2</span></span>|<span data-ttu-id="1a13a-174">540</span><span class="sxs-lookup"><span data-stu-id="1a13a-174">540</span></span>|<span data-ttu-id="1a13a-175">960</span><span class="sxs-lookup"><span data-stu-id="1a13a-175">960</span></span>|<span data-ttu-id="1a13a-176">1850</span><span class="sxs-lookup"><span data-stu-id="1a13a-176">1850</span></span>|
|<span data-ttu-id="1a13a-177">3</span><span class="sxs-lookup"><span data-stu-id="1a13a-177">3</span></span>|<span data-ttu-id="1a13a-178">360</span><span class="sxs-lookup"><span data-stu-id="1a13a-178">360</span></span>|<span data-ttu-id="1a13a-179">640</span><span class="sxs-lookup"><span data-stu-id="1a13a-179">640</span></span>|<span data-ttu-id="1a13a-180">960</span><span class="sxs-lookup"><span data-stu-id="1a13a-180">960</span></span>|
|<span data-ttu-id="1a13a-181">4</span><span class="sxs-lookup"><span data-stu-id="1a13a-181">4</span></span>|<span data-ttu-id="1a13a-182">270</span><span class="sxs-lookup"><span data-stu-id="1a13a-182">270</span></span>|<span data-ttu-id="1a13a-183">480</span><span class="sxs-lookup"><span data-stu-id="1a13a-183">480</span></span>|<span data-ttu-id="1a13a-184">600</span><span class="sxs-lookup"><span data-stu-id="1a13a-184">600</span></span>|
|<span data-ttu-id="1a13a-185">5</span><span class="sxs-lookup"><span data-stu-id="1a13a-185">5</span></span>|<span data-ttu-id="1a13a-186">180</span><span class="sxs-lookup"><span data-stu-id="1a13a-186">180</span></span>|<span data-ttu-id="1a13a-187">320</span><span class="sxs-lookup"><span data-stu-id="1a13a-187">320</span></span>|<span data-ttu-id="1a13a-188">320</span><span class="sxs-lookup"><span data-stu-id="1a13a-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="1a13a-189">Example 3</span><span class="sxs-lookup"><span data-stu-id="1a13a-189">Example 3</span></span>
<span data-ttu-id="1a13a-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span><span class="sxs-lookup"><span data-stu-id="1a13a-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="1a13a-191">Layer</span><span class="sxs-lookup"><span data-stu-id="1a13a-191">Layer</span></span>|<span data-ttu-id="1a13a-192">Height</span><span class="sxs-lookup"><span data-stu-id="1a13a-192">Height</span></span>|<span data-ttu-id="1a13a-193">Width</span><span class="sxs-lookup"><span data-stu-id="1a13a-193">Width</span></span>|<span data-ttu-id="1a13a-194">Bitrate(kbps)</span><span class="sxs-lookup"><span data-stu-id="1a13a-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="1a13a-195">1</span><span class="sxs-lookup"><span data-stu-id="1a13a-195">1</span></span>|<span data-ttu-id="1a13a-196">360</span><span class="sxs-lookup"><span data-stu-id="1a13a-196">360</span></span>|<span data-ttu-id="1a13a-197">640</span><span class="sxs-lookup"><span data-stu-id="1a13a-197">640</span></span>|<span data-ttu-id="1a13a-198">700</span><span class="sxs-lookup"><span data-stu-id="1a13a-198">700</span></span>|
|<span data-ttu-id="1a13a-199">2</span><span class="sxs-lookup"><span data-stu-id="1a13a-199">2</span></span>|<span data-ttu-id="1a13a-200">270</span><span class="sxs-lookup"><span data-stu-id="1a13a-200">270</span></span>|<span data-ttu-id="1a13a-201">480</span><span class="sxs-lookup"><span data-stu-id="1a13a-201">480</span></span>|<span data-ttu-id="1a13a-202">440</span><span class="sxs-lookup"><span data-stu-id="1a13a-202">440</span></span>|
|<span data-ttu-id="1a13a-203">3</span><span class="sxs-lookup"><span data-stu-id="1a13a-203">3</span></span>|<span data-ttu-id="1a13a-204">180</span><span class="sxs-lookup"><span data-stu-id="1a13a-204">180</span></span>|<span data-ttu-id="1a13a-205">320</span><span class="sxs-lookup"><span data-stu-id="1a13a-205">320</span></span>|<span data-ttu-id="1a13a-206">230</span><span class="sxs-lookup"><span data-stu-id="1a13a-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="1a13a-207">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="1a13a-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1a13a-208">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="1a13a-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1a13a-209">See Also</span><span class="sxs-lookup"><span data-stu-id="1a13a-209">See Also</span></span>
[<span data-ttu-id="1a13a-210">Media Services Encoding Overview</span><span class="sxs-lookup"><span data-stu-id="1a13a-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

