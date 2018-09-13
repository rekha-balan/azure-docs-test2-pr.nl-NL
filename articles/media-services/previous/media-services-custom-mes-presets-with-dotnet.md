---
title: Customizing Media Encoder Standard presets | Microsoft Docs
description: This topic shows how to perform advanced encoding by customizing Media Encoder Standard task presets. The topic shows how to use Media Services .NET SDK to create an encoding task and job. It also shows how to supply custom presets to the encoding job.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 4bdfdb5bd5362d5a8039ca31d498d122843df2a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867269"
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="34bab-105">Customizing Media Encoder Standard presets</span><span class="sxs-lookup"><span data-stu-id="34bab-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="34bab-106">Overview</span><span class="sxs-lookup"><span data-stu-id="34bab-106">Overview</span></span>

<span data-ttu-id="34bab-107">This article shows how to perform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span><span class="sxs-lookup"><span data-stu-id="34bab-107">This article shows how to perform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="34bab-108">The article uses .NET to create an encoding task and a job that executes this task.</span><span class="sxs-lookup"><span data-stu-id="34bab-108">The article uses .NET to create an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="34bab-109">This article shows you how to customize a preset by taking the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing the number of layers.</span><span class="sxs-lookup"><span data-stu-id="34bab-109">This article shows you how to customize a preset by taking the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing the number of layers.</span></span> <span data-ttu-id="34bab-110">The [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) article demonstrates custom presets that can be used to perform advanced encoding tasks.</span><span class="sxs-lookup"><span data-stu-id="34bab-110">The [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) article demonstrates custom presets that can be used to perform advanced encoding tasks.</span></span>

## <a id="customizing_presets"></a> <span data-ttu-id="34bab-111">Customizing a MES preset</span><span class="sxs-lookup"><span data-stu-id="34bab-111">Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="34bab-112">Original preset</span><span class="sxs-lookup"><span data-stu-id="34bab-112">Original preset</span></span>

<span data-ttu-id="34bab-113">Save the JSON defined in the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) article in some file with .json extension.</span><span class="sxs-lookup"><span data-stu-id="34bab-113">Save the JSON defined in the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) article in some file with .json extension.</span></span> <span data-ttu-id="34bab-114">For example, **CustomPreset_JSON.json**.</span><span class="sxs-lookup"><span data-stu-id="34bab-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="34bab-115">Customized preset</span><span class="sxs-lookup"><span data-stu-id="34bab-115">Customized preset</span></span>

<span data-ttu-id="34bab-116">Open the **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span><span class="sxs-lookup"><span data-stu-id="34bab-116">Open the **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

```json 
    {  
      "Version": 1.0,  
      "Codecs": [  
        {  
          "KeyFrameInterval": "00:00:02",  
          "H264Layers": [  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 1000,  
              "MaxBitrate": 1000,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 650,  
              "MaxBitrate": 650,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 400,  
              "MaxBitrate": 400,  
              "BufferWindow": "00:00:05",  
              "Width": 320,  
              "Height": 180,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            }  
          ],  
          "Type": "H264Video"  
        },  
        {  
          "Profile": "AACLC",  
          "Channels": 2,  
          "SamplingRate": 48000,  
          "Bitrate": 128,  
          "Type": "AACAudio"  
        }  
      ],  
      "Outputs": [  
        {  
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
          "Format": {  
            "Type": "MP4Format"  
          }  
        }  
      ]  
    }  
```

## <a id="encoding_with_dotnet"></a><span data-ttu-id="34bab-117">Encoding with Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="34bab-117">Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="34bab-118">The following code example uses Media Services .NET SDK to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="34bab-118">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="34bab-119">Create an encoding job.</span><span class="sxs-lookup"><span data-stu-id="34bab-119">Create an encoding job.</span></span>
- <span data-ttu-id="34bab-120">Get a reference to the Media Encoder Standard encoder.</span><span class="sxs-lookup"><span data-stu-id="34bab-120">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="34bab-121">Load the custom JSON preset that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="34bab-121">Load the custom JSON preset that you created in the previous section.</span></span> 
  
        // Load the JSON from the local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="34bab-122">Add an encoding task to the job.</span><span class="sxs-lookup"><span data-stu-id="34bab-122">Add an encoding task to the job.</span></span> 
- <span data-ttu-id="34bab-123">Specify the input asset to be encoded.</span><span class="sxs-lookup"><span data-stu-id="34bab-123">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="34bab-124">Create an output asset that contains the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="34bab-124">Create an output asset that contains the encoded asset.</span></span>
- <span data-ttu-id="34bab-125">Add an event handler to check the job progress.</span><span class="sxs-lookup"><span data-stu-id="34bab-125">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="34bab-126">Submit the job.</span><span class="sxs-lookup"><span data-stu-id="34bab-126">Submit the job.</span></span>
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="34bab-127">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="34bab-127">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="34bab-128">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="34bab-128">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="34bab-129">Example</span><span class="sxs-lookup"><span data-stu-id="34bab-129">Example</span></span>   

```csharp
using System;
using System.Configuration;
using System.IO;
using System.Linq;
using Microsoft.WindowsAzure.MediaServices.Client;
using System.Threading;

namespace CustomizeMESPresests
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

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

            // Encode and generate the output using custom presets.
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

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="34bab-130">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="34bab-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="34bab-131">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="34bab-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="34bab-132">See Also</span><span class="sxs-lookup"><span data-stu-id="34bab-132">See Also</span></span>
[<span data-ttu-id="34bab-133">Media Services Encoding Overview</span><span class="sxs-lookup"><span data-stu-id="34bab-133">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

