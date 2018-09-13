---
title: Create an Azure Media Services encoding task that generates fMP4 chunks | Microsoft Docs
description: This topic shows how to create an encoding task that generates fMP4 chunks. When this task is used with the Media Encoder Standard or Media Encoder Premium Workflow encoder, the output asset will contain fMP4 chunks instead of ISO MP4 files.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: b7029ac5-eadd-4a2f-8111-1fc460828981
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: juliako
ms.openlocfilehash: 9b373d3174592d26b74896eda712ff7cae1f787e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671357"
---
#  <a name="create-an-encoding-task-that-generates-fmp4-chunks"></a><span data-ttu-id="11337-104">Create an encoding task that generates fMP4 chunks</span><span class="sxs-lookup"><span data-stu-id="11337-104">Create an encoding task that generates fMP4 chunks</span></span>

## <a name="overview"></a><span data-ttu-id="11337-105">Overview</span><span class="sxs-lookup"><span data-stu-id="11337-105">Overview</span></span>

<span data-ttu-id="11337-106">This topic shows how to create an encoding task that generates fragmented MP4 (fMP4) chunks instead of ISO MP4 files.</span><span class="sxs-lookup"><span data-stu-id="11337-106">This topic shows how to create an encoding task that generates fragmented MP4 (fMP4) chunks instead of ISO MP4 files.</span></span> <span data-ttu-id="11337-107">To generate fMP4 chunks, use the **Media Encoder Standard** or **Media Encoder Premium Workflow** encoder to create an encoding task and also specify **AssetFormatOption.AdaptiveStreaming** option, as shown in this code snippet:</span><span class="sxs-lookup"><span data-stu-id="11337-107">To generate fMP4 chunks, use the **Media Encoder Standard** or **Media Encoder Premium Workflow** encoder to create an encoding task and also specify **AssetFormatOption.AdaptiveStreaming** option, as shown in this code snippet:</span></span>  
    
    task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks", 
            options: AssetCreationOptions.None, 
            formatOption: AssetFormatOption.AdaptiveStreaming);


## <a id="encoding_with_dotnet"></a><span data-ttu-id="11337-108">Encoding with Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="11337-108">Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="11337-109">The following code example uses Media Services .NET SDK to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="11337-109">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="11337-110">Create an encoding job.</span><span class="sxs-lookup"><span data-stu-id="11337-110">Create an encoding job.</span></span>
- <span data-ttu-id="11337-111">Get a reference to the **Media Encoder Standard** encoder.</span><span class="sxs-lookup"><span data-stu-id="11337-111">Get a reference to the **Media Encoder Standard** encoder.</span></span>
- <span data-ttu-id="11337-112">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span><span class="sxs-lookup"><span data-stu-id="11337-112">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="11337-113">Create an output asset that will contain fMP4 chunks and an .ism file.</span><span class="sxs-lookup"><span data-stu-id="11337-113">Create an output asset that will contain fMP4 chunks and an .ism file.</span></span>
- <span data-ttu-id="11337-114">Add an event handler to check the job progress.</span><span class="sxs-lookup"><span data-stu-id="11337-114">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="11337-115">Submit the job.</span><span class="sxs-lookup"><span data-stu-id="11337-115">Submit the job.</span></span>

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace AdaptiveStreaming
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
                // It is also specified to use AssetFormatOption.AdaptiveStreaming, 
                // which means the output asset will contain fMP4 chunks.

                task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks",
                    options: AssetCreationOptions.None,
                    formatOption: AssetFormatOption.AdaptiveStreaming);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="11337-116">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="11337-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="11337-117">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="11337-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="11337-118">See Also</span><span class="sxs-lookup"><span data-stu-id="11337-118">See Also</span></span>
[<span data-ttu-id="11337-119">Media Services Encoding Overview</span><span class="sxs-lookup"><span data-stu-id="11337-119">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

