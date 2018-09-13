---
title: Digitize text with Azure Media Analytics OCR | Microsoft Docs
description: Azure Media Analytics OCR (optical character recognition) enables you to convert text content in video files into editable, searchable digital text.  This allows you to automate the extraction of meaningful metadata from the video signal of your media.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 4a7a31b4e0069d2c94a4f109248d7b02c0b03faa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865460"
---
# <a name="use-azure-media-analytics-to-convert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="b2221-104">Use Azure Media Analytics to convert text content in video files into digital text</span><span class="sxs-lookup"><span data-stu-id="b2221-104">Use Azure Media Analytics to convert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="b2221-105">Overview</span><span class="sxs-lookup"><span data-stu-id="b2221-105">Overview</span></span>
<span data-ttu-id="b2221-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span><span class="sxs-lookup"><span data-stu-id="b2221-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="b2221-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span><span class="sxs-lookup"><span data-stu-id="b2221-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="b2221-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span><span class="sxs-lookup"><span data-stu-id="b2221-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span></span>

<span data-ttu-id="b2221-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span><span class="sxs-lookup"><span data-stu-id="b2221-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span></span> <span data-ttu-id="b2221-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span><span class="sxs-lookup"><span data-stu-id="b2221-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="b2221-111">The Azure OCR Media Processor is optimized for digital text.</span><span class="sxs-lookup"><span data-stu-id="b2221-111">The Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="b2221-112">The **Azure Media OCR** media processor is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="b2221-112">The **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="b2221-113">This article gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="b2221-113">This article gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span></span> <span data-ttu-id="b2221-114">For more information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="b2221-114">For more information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="b2221-115">OCR input files</span><span class="sxs-lookup"><span data-stu-id="b2221-115">OCR input files</span></span>
<span data-ttu-id="b2221-116">Video files.</span><span class="sxs-lookup"><span data-stu-id="b2221-116">Video files.</span></span> <span data-ttu-id="b2221-117">Currently, the following formats are supported: MP4, MOV, and WMV.</span><span class="sxs-lookup"><span data-stu-id="b2221-117">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="b2221-118">Task configuration</span><span class="sxs-lookup"><span data-stu-id="b2221-118">Task configuration</span></span>
<span data-ttu-id="b2221-119">Task configuration (preset).</span><span class="sxs-lookup"><span data-stu-id="b2221-119">Task configuration (preset).</span></span> <span data-ttu-id="b2221-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span><span class="sxs-lookup"><span data-stu-id="b2221-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="b2221-121">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span><span class="sxs-lookup"><span data-stu-id="b2221-121">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="b2221-122">Attribute descriptions</span><span class="sxs-lookup"><span data-stu-id="b2221-122">Attribute descriptions</span></span>
| <span data-ttu-id="b2221-123">Attribute name</span><span class="sxs-lookup"><span data-stu-id="b2221-123">Attribute name</span></span> | <span data-ttu-id="b2221-124">Description</span><span class="sxs-lookup"><span data-stu-id="b2221-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="b2221-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="b2221-125">AdvancedOutput</span></span>| <span data-ttu-id="b2221-126">If you set AdvancedOutput to true, the JSON output will contain positional data for every single word (in addition to phrases and regions).</span><span class="sxs-lookup"><span data-stu-id="b2221-126">If you set AdvancedOutput to true, the JSON output will contain positional data for every single word (in addition to phrases and regions).</span></span> <span data-ttu-id="b2221-127">If you do not want to see these details, set the flag to false.</span><span class="sxs-lookup"><span data-stu-id="b2221-127">If you do not want to see these details, set the flag to false.</span></span> <span data-ttu-id="b2221-128">The default value is false.</span><span class="sxs-lookup"><span data-stu-id="b2221-128">The default value is false.</span></span> <span data-ttu-id="b2221-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="b2221-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="b2221-130">Language</span><span class="sxs-lookup"><span data-stu-id="b2221-130">Language</span></span> |<span data-ttu-id="b2221-131">(optional) describes the language of text for which to look.</span><span class="sxs-lookup"><span data-stu-id="b2221-131">(optional) describes the language of text for which to look.</span></span> <span data-ttu-id="b2221-132">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span><span class="sxs-lookup"><span data-stu-id="b2221-132">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="b2221-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="b2221-133">TextOrientation</span></span> |<span data-ttu-id="b2221-134">(optional) describes the orientation of text for which to look.</span><span class="sxs-lookup"><span data-stu-id="b2221-134">(optional) describes the orientation of text for which to look.</span></span>  <span data-ttu-id="b2221-135">"Left" means that the top of all letters are pointed towards the left.</span><span class="sxs-lookup"><span data-stu-id="b2221-135">"Left" means that the top of all letters are pointed towards the left.</span></span>  <span data-ttu-id="b2221-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span><span class="sxs-lookup"><span data-stu-id="b2221-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="b2221-137">One of the following: AutoDetect (default), Up, Right, Down, Left.</span><span class="sxs-lookup"><span data-stu-id="b2221-137">One of the following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="b2221-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="b2221-138">TimeInterval</span></span> |<span data-ttu-id="b2221-139">(optional) describes the sampling rate.</span><span class="sxs-lookup"><span data-stu-id="b2221-139">(optional) describes the sampling rate.</span></span>  <span data-ttu-id="b2221-140">Default is every 1/2 second.</span><span class="sxs-lookup"><span data-stu-id="b2221-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="b2221-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="b2221-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="b2221-142">XML format – W3C XSD duration primitive (default PT0.5)</span><span class="sxs-lookup"><span data-stu-id="b2221-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="b2221-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="b2221-143">DetectRegions</span></span> |<span data-ttu-id="b2221-144">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span><span class="sxs-lookup"><span data-stu-id="b2221-144">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span></span><br/><span data-ttu-id="b2221-145">A DetectRegion object is made of the following four integer values:</span><span class="sxs-lookup"><span data-stu-id="b2221-145">A DetectRegion object is made of the following four integer values:</span></span><br/><span data-ttu-id="b2221-146">Left – pixels from the left-margin</span><span class="sxs-lookup"><span data-stu-id="b2221-146">Left – pixels from the left-margin</span></span><br/><span data-ttu-id="b2221-147">Top – pixels from the top-margin</span><span class="sxs-lookup"><span data-stu-id="b2221-147">Top – pixels from the top-margin</span></span><br/><span data-ttu-id="b2221-148">Width – width of the region in pixels</span><span class="sxs-lookup"><span data-stu-id="b2221-148">Width – width of the region in pixels</span></span><br/><span data-ttu-id="b2221-149">Height – height of the region in pixels</span><span class="sxs-lookup"><span data-stu-id="b2221-149">Height – height of the region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="b2221-150">JSON preset example</span><span class="sxs-lookup"><span data-stu-id="b2221-150">JSON preset example</span></span>

```json
    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
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
```

#### <a name="xml-preset-example"></a><span data-ttu-id="b2221-151">XML preset example</span><span class="sxs-lookup"><span data-stu-id="b2221-151">XML preset example</span></span>

```xml
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
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
```

## <a name="ocr-output-files"></a><span data-ttu-id="b2221-152">OCR output files</span><span class="sxs-lookup"><span data-stu-id="b2221-152">OCR output files</span></span>
<span data-ttu-id="b2221-153">The output of the OCR media processor is a JSON file.</span><span class="sxs-lookup"><span data-stu-id="b2221-153">The output of the OCR media processor is a JSON file.</span></span>

### <a name="elements-of-the-output-json-file"></a><span data-ttu-id="b2221-154">Elements of the output JSON file</span><span class="sxs-lookup"><span data-stu-id="b2221-154">Elements of the output JSON file</span></span>
<span data-ttu-id="b2221-155">The Video OCR output provides time-segmented data on the characters found in your video.</span><span class="sxs-lookup"><span data-stu-id="b2221-155">The Video OCR output provides time-segmented data on the characters found in your video.</span></span>  <span data-ttu-id="b2221-156">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span><span class="sxs-lookup"><span data-stu-id="b2221-156">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span></span> 

<span data-ttu-id="b2221-157">The output contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="b2221-157">The output contains the following attributes:</span></span>

| <span data-ttu-id="b2221-158">Element</span><span class="sxs-lookup"><span data-stu-id="b2221-158">Element</span></span> | <span data-ttu-id="b2221-159">Description</span><span class="sxs-lookup"><span data-stu-id="b2221-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b2221-160">Timescale</span><span class="sxs-lookup"><span data-stu-id="b2221-160">Timescale</span></span> |<span data-ttu-id="b2221-161">"ticks" per second of the video</span><span class="sxs-lookup"><span data-stu-id="b2221-161">"ticks" per second of the video</span></span> |
| <span data-ttu-id="b2221-162">Offset</span><span class="sxs-lookup"><span data-stu-id="b2221-162">Offset</span></span> |<span data-ttu-id="b2221-163">time offset for timestamps.</span><span class="sxs-lookup"><span data-stu-id="b2221-163">time offset for timestamps.</span></span> <span data-ttu-id="b2221-164">In version 1.0 of Video APIs, this will always be 0.</span><span class="sxs-lookup"><span data-stu-id="b2221-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="b2221-165">Framerate</span><span class="sxs-lookup"><span data-stu-id="b2221-165">Framerate</span></span> |<span data-ttu-id="b2221-166">Frames per second of the video</span><span class="sxs-lookup"><span data-stu-id="b2221-166">Frames per second of the video</span></span> |
| <span data-ttu-id="b2221-167">width</span><span class="sxs-lookup"><span data-stu-id="b2221-167">width</span></span> |<span data-ttu-id="b2221-168">width of the video in pixels</span><span class="sxs-lookup"><span data-stu-id="b2221-168">width of the video in pixels</span></span> |
| <span data-ttu-id="b2221-169">height</span><span class="sxs-lookup"><span data-stu-id="b2221-169">height</span></span> |<span data-ttu-id="b2221-170">height of the video in pixels</span><span class="sxs-lookup"><span data-stu-id="b2221-170">height of the video in pixels</span></span> |
| <span data-ttu-id="b2221-171">Fragments</span><span class="sxs-lookup"><span data-stu-id="b2221-171">Fragments</span></span> |<span data-ttu-id="b2221-172">array of time-based chunks of video into which the metadata is chunked</span><span class="sxs-lookup"><span data-stu-id="b2221-172">array of time-based chunks of video into which the metadata is chunked</span></span> |
| <span data-ttu-id="b2221-173">start</span><span class="sxs-lookup"><span data-stu-id="b2221-173">start</span></span> |<span data-ttu-id="b2221-174">start time of a fragment in "ticks"</span><span class="sxs-lookup"><span data-stu-id="b2221-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="b2221-175">duration</span><span class="sxs-lookup"><span data-stu-id="b2221-175">duration</span></span> |<span data-ttu-id="b2221-176">length of a fragment in "ticks"</span><span class="sxs-lookup"><span data-stu-id="b2221-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="b2221-177">interval</span><span class="sxs-lookup"><span data-stu-id="b2221-177">interval</span></span> |<span data-ttu-id="b2221-178">interval of each event within the given fragment</span><span class="sxs-lookup"><span data-stu-id="b2221-178">interval of each event within the given fragment</span></span> |
| <span data-ttu-id="b2221-179">events</span><span class="sxs-lookup"><span data-stu-id="b2221-179">events</span></span> |<span data-ttu-id="b2221-180">array containing regions</span><span class="sxs-lookup"><span data-stu-id="b2221-180">array containing regions</span></span> |
| <span data-ttu-id="b2221-181">region</span><span class="sxs-lookup"><span data-stu-id="b2221-181">region</span></span> |<span data-ttu-id="b2221-182">object representing detected words or phrases</span><span class="sxs-lookup"><span data-stu-id="b2221-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="b2221-183">language</span><span class="sxs-lookup"><span data-stu-id="b2221-183">language</span></span> |<span data-ttu-id="b2221-184">language of the text detected within a region</span><span class="sxs-lookup"><span data-stu-id="b2221-184">language of the text detected within a region</span></span> |
| <span data-ttu-id="b2221-185">orientation</span><span class="sxs-lookup"><span data-stu-id="b2221-185">orientation</span></span> |<span data-ttu-id="b2221-186">orientation of the text detected within a region</span><span class="sxs-lookup"><span data-stu-id="b2221-186">orientation of the text detected within a region</span></span> |
| <span data-ttu-id="b2221-187">lines</span><span class="sxs-lookup"><span data-stu-id="b2221-187">lines</span></span> |<span data-ttu-id="b2221-188">array of lines of text detected within a region</span><span class="sxs-lookup"><span data-stu-id="b2221-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="b2221-189">text</span><span class="sxs-lookup"><span data-stu-id="b2221-189">text</span></span> |<span data-ttu-id="b2221-190">the actual text</span><span class="sxs-lookup"><span data-stu-id="b2221-190">the actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="b2221-191">JSON output example</span><span class="sxs-lookup"><span data-stu-id="b2221-191">JSON output example</span></span>
<span data-ttu-id="b2221-192">The following output example contains the general video information and several video fragments.</span><span class="sxs-lookup"><span data-stu-id="b2221-192">The following output example contains the general video information and several video fragments.</span></span> <span data-ttu-id="b2221-193">In every video fragment, it contains every region, which is detected by OCR MP with the language and its text orientation.</span><span class="sxs-lookup"><span data-stu-id="b2221-193">In every video fragment, it contains every region, which is detected by OCR MP with the language and its text orientation.</span></span> <span data-ttu-id="b2221-194">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position, and confidence) in this line.</span><span class="sxs-lookup"><span data-stu-id="b2221-194">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position, and confidence) in this line.</span></span> <span data-ttu-id="b2221-195">The following is an example, and I put some comments inline.</span><span class="sxs-lookup"><span data-stu-id="b2221-195">The following is an example, and I put some comments inline.</span></span>

```json
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
```

## <a name="net-sample-code"></a><span data-ttu-id="b2221-196">.NET sample code</span><span class="sxs-lookup"><span data-stu-id="b2221-196">.NET sample code</span></span>

<span data-ttu-id="b2221-197">The following program shows how to:</span><span class="sxs-lookup"><span data-stu-id="b2221-197">The following program shows how to:</span></span>

1. <span data-ttu-id="b2221-198">Create an asset and upload a media file into the asset.</span><span class="sxs-lookup"><span data-stu-id="b2221-198">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="b2221-199">Create a job with an OCR configuration/preset file.</span><span class="sxs-lookup"><span data-stu-id="b2221-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="b2221-200">Download the output JSON files.</span><span class="sxs-lookup"><span data-stu-id="b2221-200">Download the output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b2221-201">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="b2221-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="b2221-202">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b2221-202">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="b2221-203">Example</span><span class="sxs-lookup"><span data-stu-id="b2221-203">Example</span></span>

```csharp
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
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="b2221-204">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="b2221-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b2221-205">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="b2221-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="b2221-206">Related links</span><span class="sxs-lookup"><span data-stu-id="b2221-206">Related links</span></span>
[<span data-ttu-id="b2221-207">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="b2221-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

