---
title: Customizing Media Encoder Standard presets | Microsoft Docs
description: This topic shows how to perform advanced encoding by customizing Media Encoder Standard task presets. The topic shows how to use Media Services .NET SDK to create an encoding task and job. It also shows how to supply custom presets to the encoding job.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: juliako
ms.openlocfilehash: 2a344af8b5bb5002f400d7a0f87b52a0f73ae619
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549545"
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="0542b-105">Customizing Media Encoder Standard presets</span><span class="sxs-lookup"><span data-stu-id="0542b-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="0542b-106">Overview</span><span class="sxs-lookup"><span data-stu-id="0542b-106">Overview</span></span>

<span data-ttu-id="0542b-107">This topic shows how to perform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span><span class="sxs-lookup"><span data-stu-id="0542b-107">This topic shows how to perform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="0542b-108">The topic uses .NET to create an encoding task and a job that executes this task.</span><span class="sxs-lookup"><span data-stu-id="0542b-108">The topic uses .NET to create an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="0542b-109">In this topic you will see how to customize a preset by taking the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing the number of layers.</span><span class="sxs-lookup"><span data-stu-id="0542b-109">In this topic you will see how to customize a preset by taking the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing the number of layers.</span></span> <span data-ttu-id="0542b-110">The [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used to perform advanced encoding tasks.</span><span class="sxs-lookup"><span data-stu-id="0542b-110">The [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used to perform advanced encoding tasks.</span></span>

## <a id="customizing_presets"></a> <span data-ttu-id="0542b-111">Customizing a MES preset</span><span class="sxs-lookup"><span data-stu-id="0542b-111">Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="0542b-112">Original preset</span><span class="sxs-lookup"><span data-stu-id="0542b-112">Original preset</span></span>

<span data-ttu-id="0542b-113">Save the JSON defined in the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span><span class="sxs-lookup"><span data-stu-id="0542b-113">Save the JSON defined in the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span></span> <span data-ttu-id="0542b-114">For example, **CustomPreset_JSON.json**.</span><span class="sxs-lookup"><span data-stu-id="0542b-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="0542b-115">Customized preset</span><span class="sxs-lookup"><span data-stu-id="0542b-115">Customized preset</span></span>

<span data-ttu-id="0542b-116">Open the **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span><span class="sxs-lookup"><span data-stu-id="0542b-116">Open the **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

    
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
    

## <a id="encoding_with_dotnet"></a><span data-ttu-id="0542b-117">Encoding with Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0542b-117">Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="0542b-118">The following code example uses Media Services .NET SDK to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="0542b-118">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="0542b-119">Create an encoding job.</span><span class="sxs-lookup"><span data-stu-id="0542b-119">Create an encoding job.</span></span>
- <span data-ttu-id="0542b-120">Get a reference to the Media Encoder Standard encoder.</span><span class="sxs-lookup"><span data-stu-id="0542b-120">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="0542b-121">Load the custom JSON preset that you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="0542b-121">Load the custom JSON preset that you created in the previous section.</span></span> 
  
        // Load the JSON from the local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="0542b-122">Add an encoding task to the job.</span><span class="sxs-lookup"><span data-stu-id="0542b-122">Add an encoding task to the job.</span></span> 
- <span data-ttu-id="0542b-123">Specify the input asset to be encoded.</span><span class="sxs-lookup"><span data-stu-id="0542b-123">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="0542b-124">Create an output asset that will contain the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="0542b-124">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="0542b-125">Add an event handler to check the job progress.</span><span class="sxs-lookup"><span data-stu-id="0542b-125">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="0542b-126">Submit the job.</span><span class="sxs-lookup"><span data-stu-id="0542b-126">Submit the job.</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using System.Net;
        using System.Security.Cryptography;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using Newtonsoft.Json.Linq;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
        using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
        using System.Web;
        using System.Globalization;
  
        namespace CustomizeMESPresests
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
  
                private static readonly string _mediaFiles =
                    Path.GetFullPath(@"../..\Media");
  
                private static readonly string _singleMP4File =
                    Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");
  
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="0542b-127">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="0542b-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0542b-128">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="0542b-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="0542b-129">See Also</span><span class="sxs-lookup"><span data-stu-id="0542b-129">See Also</span></span>
[<span data-ttu-id="0542b-130">Media Services Encoding Overview</span><span class="sxs-lookup"><span data-stu-id="0542b-130">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

