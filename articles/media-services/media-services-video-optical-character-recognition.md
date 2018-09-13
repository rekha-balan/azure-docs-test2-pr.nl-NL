---
title: Digitize text with Azure Media Analytics OCR | Microsoft Docs
description: Azure Media Analytics OCR (optical character recognition) enables you to convert text content in video files into editable, searchable digital text.  This allows you to automate the extraction of meaningful metadata from the video signal of your media.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: juliako
ms.openlocfilehash: af446adcd1238017f53d82f1f3ea5c8c23808fe7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563862"
---
# <a name="use-azure-media-analytics-to-convert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="613c0-104">Use Azure Media Analytics to convert text content in video files into digital text</span><span class="sxs-lookup"><span data-stu-id="613c0-104">Use Azure Media Analytics to convert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="613c0-105">Overview</span><span class="sxs-lookup"><span data-stu-id="613c0-105">Overview</span></span>
<span data-ttu-id="613c0-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span><span class="sxs-lookup"><span data-stu-id="613c0-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="613c0-107">This Azure Media Processor detects text content in you video files and generates text files for your use.</span><span class="sxs-lookup"><span data-stu-id="613c0-107">This Azure Media Processor detects text content in you video files and generates text files for your use.</span></span> <span data-ttu-id="613c0-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span><span class="sxs-lookup"><span data-stu-id="613c0-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span></span>

<span data-ttu-id="613c0-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span><span class="sxs-lookup"><span data-stu-id="613c0-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span></span> <span data-ttu-id="613c0-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.The Azure OCR Media Processor is optimized for digital text.</span><span class="sxs-lookup"><span data-stu-id="613c0-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.The Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="613c0-111">The **Azure Media OCR** media processor is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="613c0-111">The **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="613c0-112">This topic gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="613c0-112">This topic gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span></span> <span data-ttu-id="613c0-113">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="613c0-113">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="613c0-114">OCR input files</span><span class="sxs-lookup"><span data-stu-id="613c0-114">OCR input files</span></span>
<span data-ttu-id="613c0-115">Video files.</span><span class="sxs-lookup"><span data-stu-id="613c0-115">Video files.</span></span> <span data-ttu-id="613c0-116">Currently, the following formats are supported: MP4, MOV, and WMV.</span><span class="sxs-lookup"><span data-stu-id="613c0-116">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="613c0-117">Task configuration</span><span class="sxs-lookup"><span data-stu-id="613c0-117">Task configuration</span></span>
<span data-ttu-id="613c0-118">Task configuration (preset).</span><span class="sxs-lookup"><span data-stu-id="613c0-118">Task configuration (preset).</span></span> <span data-ttu-id="613c0-119">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span><span class="sxs-lookup"><span data-stu-id="613c0-119">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="613c0-120">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span><span class="sxs-lookup"><span data-stu-id="613c0-120">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="613c0-121">Attribute descriptions</span><span class="sxs-lookup"><span data-stu-id="613c0-121">Attribute descriptions</span></span>
| <span data-ttu-id="613c0-122">Attribute name</span><span class="sxs-lookup"><span data-stu-id="613c0-122">Attribute name</span></span> | <span data-ttu-id="613c0-123">Description</span><span class="sxs-lookup"><span data-stu-id="613c0-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="613c0-124">Language</span><span class="sxs-lookup"><span data-stu-id="613c0-124">Language</span></span> |<span data-ttu-id="613c0-125">(optional) describes the language of text for which to look.</span><span class="sxs-lookup"><span data-stu-id="613c0-125">(optional) describes the language of text for which to look.</span></span> <span data-ttu-id="613c0-126">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span><span class="sxs-lookup"><span data-stu-id="613c0-126">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="613c0-127">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="613c0-127">TextOrientation</span></span> |<span data-ttu-id="613c0-128">(optional) describes the orientation of text for which to look.</span><span class="sxs-lookup"><span data-stu-id="613c0-128">(optional) describes the orientation of text for which to look.</span></span>  <span data-ttu-id="613c0-129">"Left" means that the top of all letters are pointed towards the left.</span><span class="sxs-lookup"><span data-stu-id="613c0-129">"Left" means that the top of all letters are pointed towards the left.</span></span>  <span data-ttu-id="613c0-130">Default text (like that which can be found in a book) can be called "Up" oriented.</span><span class="sxs-lookup"><span data-stu-id="613c0-130">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="613c0-131">One of the following: AutoDetect (default), Up, Right, Down, Left.</span><span class="sxs-lookup"><span data-stu-id="613c0-131">One of the following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="613c0-132">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="613c0-132">TimeInterval</span></span> |<span data-ttu-id="613c0-133">(optional) describes the sampling rate.</span><span class="sxs-lookup"><span data-stu-id="613c0-133">(optional) describes the sampling rate.</span></span>  <span data-ttu-id="613c0-134">Default is every 1/2 second.</span><span class="sxs-lookup"><span data-stu-id="613c0-134">Default is every 1/2 second.</span></span><br/><span data-ttu-id="613c0-135">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="613c0-135">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="613c0-136">XML format – W3C XSD duration primitive (default PT0.5)</span><span class="sxs-lookup"><span data-stu-id="613c0-136">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="613c0-137">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="613c0-137">DetectRegions</span></span> |<span data-ttu-id="613c0-138">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span><span class="sxs-lookup"><span data-stu-id="613c0-138">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span></span><br/><span data-ttu-id="613c0-139">A DetectRegion object is made of the following four integer values:</span><span class="sxs-lookup"><span data-stu-id="613c0-139">A DetectRegion object is made of the following four integer values:</span></span><br/><span data-ttu-id="613c0-140">Left – pixels from the left-margin</span><span class="sxs-lookup"><span data-stu-id="613c0-140">Left – pixels from the left-margin</span></span><br/><span data-ttu-id="613c0-141">Top – pixels from the top-margin</span><span class="sxs-lookup"><span data-stu-id="613c0-141">Top – pixels from the top-margin</span></span><br/><span data-ttu-id="613c0-142">Width – width of the region in pixels</span><span class="sxs-lookup"><span data-stu-id="613c0-142">Width – width of the region in pixels</span></span><br/><span data-ttu-id="613c0-143">Height – height of the region in pixels</span><span class="sxs-lookup"><span data-stu-id="613c0-143">Height – height of the region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="613c0-144">JSON preset example</span><span class="sxs-lookup"><span data-stu-id="613c0-144">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="613c0-145">XML preset example</span><span class="sxs-lookup"><span data-stu-id="613c0-145">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="613c0-146">OCR output files</span><span class="sxs-lookup"><span data-stu-id="613c0-146">OCR output files</span></span>
<span data-ttu-id="613c0-147">The output of the OCR media processor is a JSON file.</span><span class="sxs-lookup"><span data-stu-id="613c0-147">The output of the OCR media processor is a JSON file.</span></span>

### <a name="elements-of-the-output-json-file"></a><span data-ttu-id="613c0-148">Elements of the output JSON file</span><span class="sxs-lookup"><span data-stu-id="613c0-148">Elements of the output JSON file</span></span>
<span data-ttu-id="613c0-149">The Video OCR output provides time-segmented data on the characters found in your video.</span><span class="sxs-lookup"><span data-stu-id="613c0-149">The Video OCR output provides time-segmented data on the characters found in your video.</span></span>  <span data-ttu-id="613c0-150">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span><span class="sxs-lookup"><span data-stu-id="613c0-150">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span></span> 

<span data-ttu-id="613c0-151">The output contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="613c0-151">The output contains the following attributes:</span></span>

| <span data-ttu-id="613c0-152">Element</span><span class="sxs-lookup"><span data-stu-id="613c0-152">Element</span></span> | <span data-ttu-id="613c0-153">Description</span><span class="sxs-lookup"><span data-stu-id="613c0-153">Description</span></span> |
| --- | --- |
| <span data-ttu-id="613c0-154">Timescale</span><span class="sxs-lookup"><span data-stu-id="613c0-154">Timescale</span></span> |<span data-ttu-id="613c0-155">"ticks" per second of the video</span><span class="sxs-lookup"><span data-stu-id="613c0-155">"ticks" per second of the video</span></span> |
| <span data-ttu-id="613c0-156">Offset</span><span class="sxs-lookup"><span data-stu-id="613c0-156">Offset</span></span> |<span data-ttu-id="613c0-157">time offset for timestamps.</span><span class="sxs-lookup"><span data-stu-id="613c0-157">time offset for timestamps.</span></span> <span data-ttu-id="613c0-158">In version 1.0 of Video APIs, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="613c0-158">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="613c0-159">Framerate</span><span class="sxs-lookup"><span data-stu-id="613c0-159">Framerate</span></span> |<span data-ttu-id="613c0-160">Frames per second of the video</span><span class="sxs-lookup"><span data-stu-id="613c0-160">Frames per second of the video</span></span> |
| <span data-ttu-id="613c0-161">width</span><span class="sxs-lookup"><span data-stu-id="613c0-161">width</span></span> |<span data-ttu-id="613c0-162">width of the video in pixels</span><span class="sxs-lookup"><span data-stu-id="613c0-162">width of the video in pixels</span></span> |
| <span data-ttu-id="613c0-163">height</span><span class="sxs-lookup"><span data-stu-id="613c0-163">height</span></span> |<span data-ttu-id="613c0-164">height of the video in pixels</span><span class="sxs-lookup"><span data-stu-id="613c0-164">height of the video in pixels</span></span> |
| <span data-ttu-id="613c0-165">Fragments</span><span class="sxs-lookup"><span data-stu-id="613c0-165">Fragments</span></span> |<span data-ttu-id="613c0-166">array of time-based chunks of video into which the metadata is chunked</span><span class="sxs-lookup"><span data-stu-id="613c0-166">array of time-based chunks of video into which the metadata is chunked</span></span> |
| <span data-ttu-id="613c0-167">start</span><span class="sxs-lookup"><span data-stu-id="613c0-167">start</span></span> |<span data-ttu-id="613c0-168">start time of a fragment in "ticks"</span><span class="sxs-lookup"><span data-stu-id="613c0-168">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="613c0-169">duration</span><span class="sxs-lookup"><span data-stu-id="613c0-169">duration</span></span> |<span data-ttu-id="613c0-170">length of a fragment in "ticks"</span><span class="sxs-lookup"><span data-stu-id="613c0-170">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="613c0-171">interval</span><span class="sxs-lookup"><span data-stu-id="613c0-171">interval</span></span> |<span data-ttu-id="613c0-172">interval of each event within the given fragment</span><span class="sxs-lookup"><span data-stu-id="613c0-172">interval of each event within the given fragment</span></span> |
| <span data-ttu-id="613c0-173">events</span><span class="sxs-lookup"><span data-stu-id="613c0-173">events</span></span> |<span data-ttu-id="613c0-174">array containing regions</span><span class="sxs-lookup"><span data-stu-id="613c0-174">array containing regions</span></span> |
| <span data-ttu-id="613c0-175">region</span><span class="sxs-lookup"><span data-stu-id="613c0-175">region</span></span> |<span data-ttu-id="613c0-176">object representing detected words or phrases</span><span class="sxs-lookup"><span data-stu-id="613c0-176">object representing detected words or phrases</span></span> |
| <span data-ttu-id="613c0-177">language</span><span class="sxs-lookup"><span data-stu-id="613c0-177">language</span></span> |<span data-ttu-id="613c0-178">language of the text detected within a region</span><span class="sxs-lookup"><span data-stu-id="613c0-178">language of the text detected within a region</span></span> |
| <span data-ttu-id="613c0-179">orientation</span><span class="sxs-lookup"><span data-stu-id="613c0-179">orientation</span></span> |<span data-ttu-id="613c0-180">orientation of the text detected within a region</span><span class="sxs-lookup"><span data-stu-id="613c0-180">orientation of the text detected within a region</span></span> |
| <span data-ttu-id="613c0-181">lines</span><span class="sxs-lookup"><span data-stu-id="613c0-181">lines</span></span> |<span data-ttu-id="613c0-182">array of lines of text detected within a region</span><span class="sxs-lookup"><span data-stu-id="613c0-182">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="613c0-183">text</span><span class="sxs-lookup"><span data-stu-id="613c0-183">text</span></span> |<span data-ttu-id="613c0-184">the actual text</span><span class="sxs-lookup"><span data-stu-id="613c0-184">the actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="613c0-185">JSON output example</span><span class="sxs-lookup"><span data-stu-id="613c0-185">JSON output example</span></span>
<span data-ttu-id="613c0-186">The following output example contains the general video information and several video fragments.</span><span class="sxs-lookup"><span data-stu-id="613c0-186">The following output example contains the general video information and several video fragments.</span></span> <span data-ttu-id="613c0-187">In every video fragment, it contains every region which is detected by OCR MP with the language and the its text orientation.</span><span class="sxs-lookup"><span data-stu-id="613c0-187">In every video fragment, it contains every region which is detected by OCR MP with the language and the its text orientation.</span></span> <span data-ttu-id="613c0-188">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position and confidence) in this line.</span><span class="sxs-lookup"><span data-stu-id="613c0-188">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="613c0-189">The following is an example, and I put some comments inline.</span><span class="sxs-lookup"><span data-stu-id="613c0-189">The following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // the time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // the detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including the text and the position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="sample-code"></a><span data-ttu-id="613c0-190">Sample code</span><span class="sxs-lookup"><span data-stu-id="613c0-190">Sample code</span></span>
<span data-ttu-id="613c0-191">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="613c0-191">The following program shows how to:</span></span>

1. <span data-ttu-id="613c0-192">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="613c0-192">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="613c0-193">Creates a job with a OCR configuration/preset file.</span><span class="sxs-lookup"><span data-stu-id="613c0-193">Creates a job with a OCR configuration/preset file.</span></span>
3. <span data-ttu-id="613c0-194">Downloads the output JSON files.</span><span class="sxs-lookup"><span data-stu-id="613c0-194">Downloads the output JSON files.</span></span> 
   
        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Threading.Tasks;
   
        namespace OCR
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
   
                    // Run the OCR job.
                    var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                                @"C:\supportFiles\OCR\config.json");
   
                    // Download the job output asset.
                    DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
                }
   
                static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
                {
                    // Create an asset and upload the input media file to storage.
                    IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                        "My OCR Input Asset",
                        AssetCreationOptions.None);
   
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("My OCR Job");
   
                    // Get a reference to Azure Media OCR.
                    string MediaProcessorName = "Azure Media OCR";
   
                    var processor = GetLatestMediaProcessorByName(MediaProcessorName);
   
                    // Read configuration from the specified file.
                    string configuration = File.ReadAllText(configurationFile);
   
                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("My OCR Task",
                        processor,
                        configuration,
                        TaskOptions.None);
   
                    // Specify the input asset.
                    task.InputAssets.Add(asset);
   
                    // Add an output asset to contain the results of the job.
                    task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);
   
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="613c0-195">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="613c0-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="613c0-196">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="613c0-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="613c0-197">Related links</span><span class="sxs-lookup"><span data-stu-id="613c0-197">Related links</span></span>
[<span data-ttu-id="613c0-198">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="613c0-198">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

