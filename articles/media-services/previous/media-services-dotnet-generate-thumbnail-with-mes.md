---
title: How to generate thumbnails using Media Encoder Standard with .NET
description: This topic shows how to use .NET to encode an asset and generate thumbnails at the same time using Media Encoder Standard.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 08332865a60baa0dd87b16809994065ddfed3055
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857157"
---
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="194fa-103">How to generate thumbnails using Media Encoder Standard with .NET</span><span class="sxs-lookup"><span data-stu-id="194fa-103">How to generate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="194fa-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span><span class="sxs-lookup"><span data-stu-id="194fa-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="194fa-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span><span class="sxs-lookup"><span data-stu-id="194fa-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="194fa-106">This article provides a few sample XML and JSON thumbnail presets for such scenarios.</span><span class="sxs-lookup"><span data-stu-id="194fa-106">This article provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="194fa-107">At the end of the article, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span><span class="sxs-lookup"><span data-stu-id="194fa-107">At the end of the article, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span></span>

<span data-ttu-id="194fa-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="194fa-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="194fa-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span><span class="sxs-lookup"><span data-stu-id="194fa-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>
    
## <a name="example-of-a-single-png-file-preset"></a><span data-ttu-id="194fa-110">Example of a "single PNG file" preset</span><span class="sxs-lookup"><span data-stu-id="194fa-110">Example of a "single PNG file" preset</span></span>

<span data-ttu-id="194fa-111">The following JSON and XML preset can be used to produce a single output PNG file from the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span><span class="sxs-lookup"><span data-stu-id="194fa-111">The following JSON and XML preset can be used to produce a single output PNG file from the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="194fa-112">Note that the output image dimensions have been set to 100%, meaning these match the dimensions of the input video.</span><span class="sxs-lookup"><span data-stu-id="194fa-112">Note that the output image dimensions have been set to 100%, meaning these match the dimensions of the input video.</span></span> <span data-ttu-id="194fa-113">Note also how the “Format” setting in "Outputs" is required to match the use of "PngLayers" in the “Codecs” section.</span><span class="sxs-lookup"><span data-stu-id="194fa-113">Note also how the “Format” setting in "Outputs" is required to match the use of "PngLayers" in the “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="194fa-114">JSON preset</span><span class="sxs-lookup"><span data-stu-id="194fa-114">JSON preset</span></span>

```json
    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
```
    
### <a name="xml-preset"></a><span data-ttu-id="194fa-115">XML preset</span><span class="sxs-lookup"><span data-stu-id="194fa-115">XML preset</span></span>

```xml
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>
```

## <a name="example-of-a-series-of-jpeg-images-preset"></a><span data-ttu-id="194fa-116">Example of a "series of JPEG images" preset</span><span class="sxs-lookup"><span data-stu-id="194fa-116">Example of a "series of JPEG images" preset</span></span>

<span data-ttu-id="194fa-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span><span class="sxs-lookup"><span data-stu-id="194fa-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="194fa-118">JSON preset</span><span class="sxs-lookup"><span data-stu-id="194fa-118">JSON preset</span></span>

```json
    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "10%",
          "Range": "96%",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
```

### <a name="xml-preset"></a><span data-ttu-id="194fa-119">XML preset</span><span class="sxs-lookup"><span data-stu-id="194fa-119">XML preset</span></span>
    
```xml
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>
```

## <a name="example-of-a-one-image-at-a-specific-timestamp-preset"></a><span data-ttu-id="194fa-120">Example of a "one image at a specific timestamp" preset</span><span class="sxs-lookup"><span data-stu-id="194fa-120">Example of a "one image at a specific timestamp" preset</span></span>

<span data-ttu-id="194fa-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30-second mark of the input video.</span><span class="sxs-lookup"><span data-stu-id="194fa-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30-second mark of the input video.</span></span> <span data-ttu-id="194fa-122">This preset expects the input video to be more than 30 seconds in duration (else the job fails).</span><span class="sxs-lookup"><span data-stu-id="194fa-122">This preset expects the input video to be more than 30 seconds in duration (else the job fails).</span></span>

### <a name="json-preset"></a><span data-ttu-id="194fa-123">JSON preset</span><span class="sxs-lookup"><span data-stu-id="194fa-123">JSON preset</span></span>

```json
    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
```

### <a name="xml-preset"></a><span data-ttu-id="194fa-124">XML preset</span><span class="sxs-lookup"><span data-stu-id="194fa-124">XML preset</span></span>
```xml
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:01" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>
```

## <a name="example-of-a-thumbnails-at-different-resolutions-preset"></a><span data-ttu-id="194fa-125">Example of a "thumbnails at different resolutions" preset</span><span class="sxs-lookup"><span data-stu-id="194fa-125">Example of a "thumbnails at different resolutions" preset</span></span>

<span data-ttu-id="194fa-126">The following preset can be used to generate thumbnails at different resolutions in one task.</span><span class="sxs-lookup"><span data-stu-id="194fa-126">The following preset can be used to generate thumbnails at different resolutions in one task.</span></span> <span data-ttu-id="194fa-127">In the example, at positions 5%, 15%, …, 95% of the input timeline, the encoder generates two images – one at 100% of the input video resolution and the other at 50%.</span><span class="sxs-lookup"><span data-stu-id="194fa-127">In the example, at positions 5%, 15%, …, 95% of the input timeline, the encoder generates two images – one at 100% of the input video resolution and the other at 50%.</span></span>

<span data-ttu-id="194fa-128">Note the use of {Resolution} macro in the FileName; it indicates to the encoder to use the width and height that you specified in the Encoding section of the preset while generating the file name of the output images.</span><span class="sxs-lookup"><span data-stu-id="194fa-128">Note the use of {Resolution} macro in the FileName; it indicates to the encoder to use the width and height that you specified in the Encoding section of the preset while generating the file name of the output images.</span></span> <span data-ttu-id="194fa-129">This also helps you distinguish between the different images easily</span><span class="sxs-lookup"><span data-stu-id="194fa-129">This also helps you distinguish between the different images easily</span></span>

### <a name="json-preset"></a><span data-ttu-id="194fa-130">JSON preset</span><span class="sxs-lookup"><span data-stu-id="194fa-130">JSON preset</span></span>

```json
    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
        {
          "Quality": 90,
          "Type": "JpgLayer",
          "Width": "100%",
          "Height": "100%"
        },
        {
          "Quality": 90,
          "Type": "JpgLayer",
          "Width": "50%",
          "Height": "50%"
        }

          ],
          "Start": "5%",
          "Step": "10%",
          "Range": "96%",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Resolution}_{Index}{Extension}",
          "Format": {
        "Type": "JpgFormat"
          }
        }
      ]
    }
```

### <a name="xml-preset"></a><span data-ttu-id="194fa-131">XML preset</span><span class="sxs-lookup"><span data-stu-id="194fa-131">XML preset</span></span>
```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
    <Encoding>
    <JpgImage Start="5%" Step="10%" Range="96%"><JpgImage Start="00:00:01" Step="00:00:15">
      <JpgLayers>
       <JpgLayer>
        <Width>100%</Width>
        <Height>100%</Height>
        <Quality>90</Quality>
       </JpgLayer>
       <JpgLayer>
        <Width>50%</Width>
        <Height>50%</Height>
        <Quality>90</Quality>
       </JpgLayer>
      </JpgLayers>
    </JpgImage>
    </Encoding>
    <Outputs>
      <Output FileName="{Basename}_{Resolution}_{Index}{Extension}">
        <JpgFormat/>
      </Output>
    </Outputs>
    </Preset>
```

## <a name="example-of-generating-a-thumbnail-while-encoding"></a><span data-ttu-id="194fa-132">Example of generating a thumbnail while encoding</span><span class="sxs-lookup"><span data-stu-id="194fa-132">Example of generating a thumbnail while encoding</span></span>

<span data-ttu-id="194fa-133">While all of the above examples have discussed how you can submit an encoding task that only produces images, you can also combine video/audio encoding with thumbnail generation.</span><span class="sxs-lookup"><span data-stu-id="194fa-133">While all of the above examples have discussed how you can submit an encoding task that only produces images, you can also combine video/audio encoding with thumbnail generation.</span></span> <span data-ttu-id="194fa-134">The following JSON and XML preset tell **Media Encoder Standard** to generate a thumbnail during encoding.</span><span class="sxs-lookup"><span data-stu-id="194fa-134">The following JSON and XML preset tell **Media Encoder Standard** to generate a thumbnail during encoding.</span></span>

### <a id="json"></a><span data-ttu-id="194fa-135">JSON preset</span><span class="sxs-lookup"><span data-stu-id="194fa-135">JSON preset</span></span>
<span data-ttu-id="194fa-136">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) article.</span><span class="sxs-lookup"><span data-stu-id="194fa-136">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) article.</span></span>

```json
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }
```

### <a id="xml"></a><span data-ttu-id="194fa-137">XML preset</span><span class="sxs-lookup"><span data-stu-id="194fa-137">XML preset</span></span>
<span data-ttu-id="194fa-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) article.</span><span class="sxs-lookup"><span data-stu-id="194fa-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) article.</span></span>

```csharp
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>   
```

## <a id="code_sample"></a><span data-ttu-id="194fa-139">Encode video and generate thumbnail with .NET</span><span class="sxs-lookup"><span data-stu-id="194fa-139">Encode video and generate thumbnail with .NET</span></span>

<span data-ttu-id="194fa-140">The following code example uses Media Services .NET SDK to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="194fa-140">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="194fa-141">Create an encoding job.</span><span class="sxs-lookup"><span data-stu-id="194fa-141">Create an encoding job.</span></span>
* <span data-ttu-id="194fa-142">Get a reference to the Media Encoder Standard encoder.</span><span class="sxs-lookup"><span data-stu-id="194fa-142">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="194fa-143">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span><span class="sxs-lookup"><span data-stu-id="194fa-143">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="194fa-144">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span><span class="sxs-lookup"><span data-stu-id="194fa-144">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span></span>
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="194fa-145">Add a single encoding task to the job.</span><span class="sxs-lookup"><span data-stu-id="194fa-145">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="194fa-146">Specify the input asset to be encoded.</span><span class="sxs-lookup"><span data-stu-id="194fa-146">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="194fa-147">Create an output asset that contains the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="194fa-147">Create an output asset that contains the encoded asset.</span></span>
* <span data-ttu-id="194fa-148">Add an event handler to check the job progress.</span><span class="sxs-lookup"><span data-stu-id="194fa-148">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="194fa-149">Submit the job.</span><span class="sxs-lookup"><span data-stu-id="194fa-149">Submit the job.</span></span>

<span data-ttu-id="194fa-150">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) article for directions on how to set up your dev environment.</span><span class="sxs-lookup"><span data-stu-id="194fa-150">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) article for directions on how to set up your dev environment.</span></span>

```csharp
using System;
using System.Configuration;
using System.IO;
using System.Linq;
using Microsoft.WindowsAzure.MediaServices.Client;
using System.Threading;

namespace EncodeAndGenerateThumbnails
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

            // Encode and generate the thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Thumbnail Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard Thumbnail task",
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

## <a name="considerations"></a><span data-ttu-id="194fa-151">Considerations</span><span class="sxs-lookup"><span data-stu-id="194fa-151">Considerations</span></span>
<span data-ttu-id="194fa-152">The following considerations apply:</span><span class="sxs-lookup"><span data-stu-id="194fa-152">The following considerations apply:</span></span>

* <span data-ttu-id="194fa-153">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span><span class="sxs-lookup"><span data-stu-id="194fa-153">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="194fa-154">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span><span class="sxs-lookup"><span data-stu-id="194fa-154">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="194fa-155">Frame Number if they are non-negative integers, for example "Start": "120",</span><span class="sxs-lookup"><span data-stu-id="194fa-155">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="194fa-156">Relative to source duration if expressed as %-suffixed, for example "Start": "15%", OR</span><span class="sxs-lookup"><span data-stu-id="194fa-156">Relative to source duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="194fa-157">Timestamp if expressed as HH:MM:SS…</span><span class="sxs-lookup"><span data-stu-id="194fa-157">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="194fa-158">format.</span><span class="sxs-lookup"><span data-stu-id="194fa-158">format.</span></span> <span data-ttu-id="194fa-159">For example "Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="194fa-159">For example "Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="194fa-160">You can mix and match notations as you please.</span><span class="sxs-lookup"><span data-stu-id="194fa-160">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="194fa-161">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span><span class="sxs-lookup"><span data-stu-id="194fa-161">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="194fa-162">Defaults: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="194fa-162">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="194fa-163">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="194fa-163">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="194fa-164">When present, MES matches JpgVideo to JpgFormat and so on.</span><span class="sxs-lookup"><span data-stu-id="194fa-164">When present, MES matches JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="194fa-165">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span><span class="sxs-lookup"><span data-stu-id="194fa-165">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="194fa-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="194fa-166">Next steps</span></span>

<span data-ttu-id="194fa-167">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span><span class="sxs-lookup"><span data-stu-id="194fa-167">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="194fa-168">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="194fa-168">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="194fa-169">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="194fa-169">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="194fa-170">See Also</span><span class="sxs-lookup"><span data-stu-id="194fa-170">See Also</span></span>
[<span data-ttu-id="194fa-171">Media Services Encoding Overview</span><span class="sxs-lookup"><span data-stu-id="194fa-171">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

