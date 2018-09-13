---
title: Perform advanced encoding by customizing MES presets | Microsoft Docs
description: This topic shows how to perform advanced encoding by customizing Media Encoder Standard task presets.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: 7776ac35f1a8a30c959286a9e31beb666f5fc799
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555809"
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="03edd-103">Perform advanced encoding by customizing MES presets</span><span class="sxs-lookup"><span data-stu-id="03edd-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="03edd-104">Overview</span><span class="sxs-lookup"><span data-stu-id="03edd-104">Overview</span></span>

<span data-ttu-id="03edd-105">This topic shows how to customize Media Encoder Standard presets.</span><span class="sxs-lookup"><span data-stu-id="03edd-105">This topic shows how to customize Media Encoder Standard presets.</span></span> <span data-ttu-id="03edd-106">The [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how to use .NET to create an encoding task and a job that executes this task.</span><span class="sxs-lookup"><span data-stu-id="03edd-106">The [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how to use .NET to create an encoding task and a job that executes this task.</span></span> <span data-ttu-id="03edd-107">Once you customize a preset, supply the custom presets to the encoding task.</span><span class="sxs-lookup"><span data-stu-id="03edd-107">Once you customize a preset, supply the custom presets to the encoding task.</span></span> 

<span data-ttu-id="03edd-108">In this topic, the custom presets that perform the following encoding tasks are demonstrated.</span><span class="sxs-lookup"><span data-stu-id="03edd-108">In this topic, the custom presets that perform the following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="03edd-109">Support for relative sizes</span><span class="sxs-lookup"><span data-stu-id="03edd-109">Support for relative sizes</span></span>

<span data-ttu-id="03edd-110">When generating thumbnails, you do not need to always specify output width and height in pixels.</span><span class="sxs-lookup"><span data-stu-id="03edd-110">When generating thumbnails, you do not need to always specify output width and height in pixels.</span></span> <span data-ttu-id="03edd-111">You can specify them in percentages, in the range [1%, …, 100%].</span><span class="sxs-lookup"><span data-stu-id="03edd-111">You can specify them in percentages, in the range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="03edd-112">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-112">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="03edd-113">XML preset</span><span class="sxs-lookup"><span data-stu-id="03edd-113">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a><span data-ttu-id="03edd-114">Generate thumbnails</span><span class="sxs-lookup"><span data-stu-id="03edd-114">Generate thumbnails</span></span>

<span data-ttu-id="03edd-115">This section shows how to customize a preset that generates thumbnails.</span><span class="sxs-lookup"><span data-stu-id="03edd-115">This section shows how to customize a preset that generates thumbnails.</span></span> <span data-ttu-id="03edd-116">The preset defined below contains information on how you want to encode your file as well as information needed to generate thumbnails.</span><span class="sxs-lookup"><span data-stu-id="03edd-116">The preset defined below contains information on how you want to encode your file as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="03edd-117">You can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span><span class="sxs-lookup"><span data-stu-id="03edd-117">You can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="03edd-118">The **SceneChangeDetection** setting in the following preset can only be set to true if you are encoding to a single  bitrate video.</span><span class="sxs-lookup"><span data-stu-id="03edd-118">The **SceneChangeDetection** setting in the following preset can only be set to true if you are encoding to a single  bitrate video.</span></span> <span data-ttu-id="03edd-119">If you are encoding to a multi-bitrate video and set **SceneChangeDetection** to true, the encoder returns an error.</span><span class="sxs-lookup"><span data-stu-id="03edd-119">If you are encoding to a multi-bitrate video and set **SceneChangeDetection** to true, the encoder returns an error.</span></span>  
>
>

<span data-ttu-id="03edd-120">For information about schema, see [this](media-services-mes-schema.md) topic.</span><span class="sxs-lookup"><span data-stu-id="03edd-120">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="03edd-121">Make sure to review the [Considerations](#considerations) section.</span><span class="sxs-lookup"><span data-stu-id="03edd-121">Make sure to review the [Considerations](#considerations) section.</span></span>

### <a id="json"></a><span data-ttu-id="03edd-122">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-122">JSON preset</span></span>
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
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
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
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a id="xml"></a><span data-ttu-id="03edd-123">XML preset</span><span class="sxs-lookup"><span data-stu-id="03edd-123">XML preset</span></span>
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
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="03edd-124">Considerations</span><span class="sxs-lookup"><span data-stu-id="03edd-124">Considerations</span></span>

<span data-ttu-id="03edd-125">The following considerations apply:</span><span class="sxs-lookup"><span data-stu-id="03edd-125">The following considerations apply:</span></span>

* <span data-ttu-id="03edd-126">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span><span class="sxs-lookup"><span data-stu-id="03edd-126">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="03edd-127">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span><span class="sxs-lookup"><span data-stu-id="03edd-127">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="03edd-128">Frame Number if they are non-negative integers, for example "Start": "120",</span><span class="sxs-lookup"><span data-stu-id="03edd-128">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="03edd-129">Relative to source duration if expressed as %-suffixed, for example "Start": "15%", OR</span><span class="sxs-lookup"><span data-stu-id="03edd-129">Relative to source duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="03edd-130">Timestamp if expressed as HH:MM:SS…</span><span class="sxs-lookup"><span data-stu-id="03edd-130">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="03edd-131">format, for example "Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="03edd-131">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="03edd-132">You can mix and match notations as you please.</span><span class="sxs-lookup"><span data-stu-id="03edd-132">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="03edd-133">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span><span class="sxs-lookup"><span data-stu-id="03edd-133">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="03edd-134">Defaults: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="03edd-134">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="03edd-135">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="03edd-135">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="03edd-136">When present, MES matches JpgVideo to JpgFormat and so on.</span><span class="sxs-lookup"><span data-stu-id="03edd-136">When present, MES matches JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="03edd-137">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span><span class="sxs-lookup"><span data-stu-id="03edd-137">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a id="trim_video"></a><span data-ttu-id="03edd-138">Trim a video (clipping)</span><span class="sxs-lookup"><span data-stu-id="03edd-138">Trim a video (clipping)</span></span>
<span data-ttu-id="03edd-139">This section talks about modifying the encoder presets to clip or trim the input video where the input is a so-called mezzanine file or on-demand file.</span><span class="sxs-lookup"><span data-stu-id="03edd-139">This section talks about modifying the encoder presets to clip or trim the input video where the input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="03edd-140">The encoder can also be used to clip or trim an asset, which is captured or archived from a live stream – the details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="03edd-140">The encoder can also be used to clip or trim an asset, which is captured or archived from a live stream – the details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="03edd-141">To trim your videos, you can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and modify the **Sources** element (as shown below).</span><span class="sxs-lookup"><span data-stu-id="03edd-141">To trim your videos, you can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and modify the **Sources** element (as shown below).</span></span> <span data-ttu-id="03edd-142">The value of StartTime needs to match the absolute timestamps of the input video.</span><span class="sxs-lookup"><span data-stu-id="03edd-142">The value of StartTime needs to match the absolute timestamps of the input video.</span></span> <span data-ttu-id="03edd-143">For example, if the first frame of the input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span><span class="sxs-lookup"><span data-stu-id="03edd-143">For example, if the first frame of the input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="03edd-144">In the example below, we assume that the input video has a starting timestamp of zero.</span><span class="sxs-lookup"><span data-stu-id="03edd-144">In the example below, we assume that the input video has a starting timestamp of zero.</span></span> <span data-ttu-id="03edd-145">**Sources** should be placed at the beginning of the preset.</span><span class="sxs-lookup"><span data-stu-id="03edd-145">**Sources** should be placed at the beginning of the preset.</span></span>

### <a id="json"></a><span data-ttu-id="03edd-146">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-146">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
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

### <a name="xml-preset"></a><span data-ttu-id="03edd-147">XML preset</span><span class="sxs-lookup"><span data-stu-id="03edd-147">XML preset</span></span>
<span data-ttu-id="03edd-148">To trim your videos, you can take any of the MES presets documented [here](media-services-mes-presets-overview.md) and modify the **Sources** element (as shown below).</span><span class="sxs-lookup"><span data-stu-id="03edd-148">To trim your videos, you can take any of the MES presets documented [here](media-services-mes-presets-overview.md) and modify the **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
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
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <a id="overlay"></a><span data-ttu-id="03edd-149">Create an overlay</span><span class="sxs-lookup"><span data-stu-id="03edd-149">Create an overlay</span></span>

<span data-ttu-id="03edd-150">The Media Encoder Standard allows you to overlay an image onto an existing video.</span><span class="sxs-lookup"><span data-stu-id="03edd-150">The Media Encoder Standard allows you to overlay an image onto an existing video.</span></span> <span data-ttu-id="03edd-151">Currently, the following formats are supported: png, jpg, gif, and bmp.</span><span class="sxs-lookup"><span data-stu-id="03edd-151">Currently, the following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="03edd-152">The preset defined below is a basic example  of a video overlay.</span><span class="sxs-lookup"><span data-stu-id="03edd-152">The preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="03edd-153">In addition to defining a preset file, you also have to let Media Services know which file in the asset is the overlay image and which file is the source video onto which you want to overlay the image.</span><span class="sxs-lookup"><span data-stu-id="03edd-153">In addition to defining a preset file, you also have to let Media Services know which file in the asset is the overlay image and which file is the source video onto which you want to overlay the image.</span></span> <span data-ttu-id="03edd-154">The video file has to be the **primary** file.</span><span class="sxs-lookup"><span data-stu-id="03edd-154">The video file has to be the **primary** file.</span></span>

<span data-ttu-id="03edd-155">If you are using .NET, add the following two functions to the .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span><span class="sxs-lookup"><span data-stu-id="03edd-155">If you are using .NET, add the following two functions to the .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="03edd-156">The **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets the mp4 file to be the primary file in the asset.</span><span class="sxs-lookup"><span data-stu-id="03edd-156">The **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets the mp4 file to be the primary file in the asset.</span></span> <span data-ttu-id="03edd-157">The **EncodeWithOverlay** function uses the custom preset file that was passed to it (for example, the preset that follows) to create the encoding task.</span><span class="sxs-lookup"><span data-stu-id="03edd-157">The **EncodeWithOverlay** function uses the custom preset file that was passed to it (for example, the preset that follows) to create the encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // The following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify the input assets to be encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset to contain the results of the job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="03edd-158">Current limitations:</span><span class="sxs-lookup"><span data-stu-id="03edd-158">Current limitations:</span></span>
>
> <span data-ttu-id="03edd-159">The overlay opacity setting is not supported.</span><span class="sxs-lookup"><span data-stu-id="03edd-159">The overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="03edd-160">Your source video file and the overlay image file have to be in the same asset, and the video file needs to be set as the primary file in this asset.</span><span class="sxs-lookup"><span data-stu-id="03edd-160">Your source video file and the overlay image file have to be in the same asset, and the video file needs to be set as the primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="03edd-161">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-161">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="03edd-162">XML preset</span><span class="sxs-lookup"><span data-stu-id="03edd-162">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <a id="silent_audio"></a><span data-ttu-id="03edd-163">Insert a silent audio track when input has no audio</span><span class="sxs-lookup"><span data-stu-id="03edd-163">Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="03edd-164">By default, if you send an input to the encoder that contains only video, and no audio, then the output asset contains files that contain only video data.</span><span class="sxs-lookup"><span data-stu-id="03edd-164">By default, if you send an input to the encoder that contains only video, and no audio, then the output asset contains files that contain only video data.</span></span> <span data-ttu-id="03edd-165">Some players may not be able to handle such output streams.</span><span class="sxs-lookup"><span data-stu-id="03edd-165">Some players may not be able to handle such output streams.</span></span> <span data-ttu-id="03edd-166">You can use this setting to force the encoder to add a silent audio track to the output in that scenario.</span><span class="sxs-lookup"><span data-stu-id="03edd-166">You can use this setting to force the encoder to add a silent audio track to the output in that scenario.</span></span>

<span data-ttu-id="03edd-167">To force the encoder to produce an asset that contains a silent audio track when input has no audio, specify the "InsertSilenceIfNoAudio" value.</span><span class="sxs-lookup"><span data-stu-id="03edd-167">To force the encoder to produce an asset that contains a silent audio track when input has no audio, specify the "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="03edd-168">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span><span class="sxs-lookup"><span data-stu-id="03edd-168">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="03edd-169">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-169">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="03edd-170">XML preset</span><span class="sxs-lookup"><span data-stu-id="03edd-170">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a><span data-ttu-id="03edd-171">Disable auto de-interlacing</span><span class="sxs-lookup"><span data-stu-id="03edd-171">Disable auto de-interlacing</span></span>
<span data-ttu-id="03edd-172">Customers don’t need to do anything if they like the interlace contents to be automatically de-interlaced.</span><span class="sxs-lookup"><span data-stu-id="03edd-172">Customers don’t need to do anything if they like the interlace contents to be automatically de-interlaced.</span></span> <span data-ttu-id="03edd-173">When the auto de-interlacing is on (default) the MES does the auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span><span class="sxs-lookup"><span data-stu-id="03edd-173">When the auto de-interlacing is on (default) the MES does the auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="03edd-174">You can turn the auto de-interlacing off.</span><span class="sxs-lookup"><span data-stu-id="03edd-174">You can turn the auto de-interlacing off.</span></span> <span data-ttu-id="03edd-175">This option is not recommended.</span><span class="sxs-lookup"><span data-stu-id="03edd-175">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="03edd-176">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-176">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="03edd-177">XML preset</span><span class="sxs-lookup"><span data-stu-id="03edd-177">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a><span data-ttu-id="03edd-178">Audio-only presets</span><span class="sxs-lookup"><span data-stu-id="03edd-178">Audio-only presets</span></span>
<span data-ttu-id="03edd-179">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span><span class="sxs-lookup"><span data-stu-id="03edd-179">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="03edd-180">AAC Audio</span><span class="sxs-lookup"><span data-stu-id="03edd-180">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
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
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="03edd-181">AAC Good Quality Audio</span><span class="sxs-lookup"><span data-stu-id="03edd-181">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="concatenate"></a><span data-ttu-id="03edd-182">Concatenate two or more video files</span><span class="sxs-lookup"><span data-stu-id="03edd-182">Concatenate two or more video files</span></span>

<span data-ttu-id="03edd-183">The following example illustrates how you can generate a preset to concatenate two or more video files.</span><span class="sxs-lookup"><span data-stu-id="03edd-183">The following example illustrates how you can generate a preset to concatenate two or more video files.</span></span> <span data-ttu-id="03edd-184">The most common scenario is when you want to add a header or a trailer to the main video.</span><span class="sxs-lookup"><span data-stu-id="03edd-184">The most common scenario is when you want to add a header or a trailer to the main video.</span></span> <span data-ttu-id="03edd-185">The intended use is when the video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span><span class="sxs-lookup"><span data-stu-id="03edd-185">The intended use is when the video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="03edd-186">You should take care not to mix videos of different frame rates, or with different number of audio tracks.</span><span class="sxs-lookup"><span data-stu-id="03edd-186">You should take care not to mix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="03edd-187">The current design of the concatenation feature expects that the input video clips are consistent in terms of resolution, frame rate etc.</span><span class="sxs-lookup"><span data-stu-id="03edd-187">The current design of the concatenation feature expects that the input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="03edd-188">Requirements and considerations</span><span class="sxs-lookup"><span data-stu-id="03edd-188">Requirements and considerations</span></span>

* <span data-ttu-id="03edd-189">Input videos should only have one audio track.</span><span class="sxs-lookup"><span data-stu-id="03edd-189">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="03edd-190">Input videos should all have the same frame rate.</span><span class="sxs-lookup"><span data-stu-id="03edd-190">Input videos should all have the same frame rate.</span></span>
* <span data-ttu-id="03edd-191">You must upload your videos into separate assets and set the videos as the primary file in each asset.</span><span class="sxs-lookup"><span data-stu-id="03edd-191">You must upload your videos into separate assets and set the videos as the primary file in each asset.</span></span>
* <span data-ttu-id="03edd-192">You need to know the duration of your videos.</span><span class="sxs-lookup"><span data-stu-id="03edd-192">You need to know the duration of your videos.</span></span>
* <span data-ttu-id="03edd-193">The preset examples below assumes that all the input videos start with a timestamp of zero.</span><span class="sxs-lookup"><span data-stu-id="03edd-193">The preset examples below assumes that all the input videos start with a timestamp of zero.</span></span> <span data-ttu-id="03edd-194">You need to modify the StartTime values if the videos have different starting timestamp, as is typically the case with live archives.</span><span class="sxs-lookup"><span data-stu-id="03edd-194">You need to modify the StartTime values if the videos have different starting timestamp, as is typically the case with live archives.</span></span>
* <span data-ttu-id="03edd-195">The JSON preset makes explicit references to the AssetID values of the input assets.</span><span class="sxs-lookup"><span data-stu-id="03edd-195">The JSON preset makes explicit references to the AssetID values of the input assets.</span></span>
* <span data-ttu-id="03edd-196">The sample code assumes that the JSON preset has been saved to a local file, such as "C:\supportFiles\preset.json".</span><span class="sxs-lookup"><span data-stu-id="03edd-196">The sample code assumes that the JSON preset has been saved to a local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="03edd-197">It also assumes that two assets have been created by uploading two video files, and that you know the resultant AssetID values.</span><span class="sxs-lookup"><span data-stu-id="03edd-197">It also assumes that two assets have been created by uploading two video files, and that you know the resultant AssetID values.</span></span>
* <span data-ttu-id="03edd-198">The code snippet and JSON preset shows an example of concatenating two video files.</span><span class="sxs-lookup"><span data-stu-id="03edd-198">The code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="03edd-199">You can extend it to more than two videos by:</span><span class="sxs-lookup"><span data-stu-id="03edd-199">You can extend it to more than two videos by:</span></span>

  1. <span data-ttu-id="03edd-200">Calling task.InputAssets.Add() repeatedly to add more videos, in order.</span><span class="sxs-lookup"><span data-stu-id="03edd-200">Calling task.InputAssets.Add() repeatedly to add more videos, in order.</span></span>
  2. <span data-ttu-id="03edd-201">Making corresponding edits to the "Sources" element in the JSON, by adding more entries, in the same order.</span><span class="sxs-lookup"><span data-stu-id="03edd-201">Making corresponding edits to the "Sources" element in the JSON, by adding more entries, in the same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="03edd-202">.NET code</span><span class="sxs-lookup"><span data-stu-id="03edd-202">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass to it the name of the
    // processor to use for the specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load the XML (or JSON) from the local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify the input videos to be concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset to contain the results of the job.
    // This output is specified as AssetCreationOptions.None, which
    // means the output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="03edd-203">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-203">JSON preset</span></span>

<span data-ttu-id="03edd-204">Update your custom preset with ids of the assets that you want to concatenate, and with the appropriate time segment for each video.</span><span class="sxs-lookup"><span data-stu-id="03edd-204">Update your custom preset with ids of the assets that you want to concatenate, and with the appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
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
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="crop"></a><span data-ttu-id="03edd-205">Crop videos with Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="03edd-205">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="03edd-206">See the [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span><span class="sxs-lookup"><span data-stu-id="03edd-206">See the [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <a id="no_video"></a><span data-ttu-id="03edd-207">Insert a video track when input has no video</span><span class="sxs-lookup"><span data-stu-id="03edd-207">Insert a video track when input has no video</span></span>
<span data-ttu-id="03edd-208">By default, if you send an input to the encoder that contains only audio, and no video, then the output asset contains files that contain only audio data.</span><span class="sxs-lookup"><span data-stu-id="03edd-208">By default, if you send an input to the encoder that contains only audio, and no video, then the output asset contains files that contain only audio data.</span></span> <span data-ttu-id="03edd-209">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able to handle such streams.</span><span class="sxs-lookup"><span data-stu-id="03edd-209">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able to handle such streams.</span></span> <span data-ttu-id="03edd-210">You can use this setting to force the encoder to add a monochrome video track to the output in that scenario.</span><span class="sxs-lookup"><span data-stu-id="03edd-210">You can use this setting to force the encoder to add a monochrome video track to the output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="03edd-211">Forcing the encoder to insert an output video track increases the size of the output Asset, and thereby the cost incurred for the encoding Task.</span><span class="sxs-lookup"><span data-stu-id="03edd-211">Forcing the encoder to insert an output video track increases the size of the output Asset, and thereby the cost incurred for the encoding Task.</span></span> <span data-ttu-id="03edd-212">You should run tests to verify that this resultant increase has only a modest impact on your monthly charges.</span><span class="sxs-lookup"><span data-stu-id="03edd-212">You should run tests to verify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>
>

### <a name="inserting-video-at-only-the-lowest-bitrate"></a><span data-ttu-id="03edd-213">Inserting video at only the lowest bitrate</span><span class="sxs-lookup"><span data-stu-id="03edd-213">Inserting video at only the lowest bitrate</span></span>
<span data-ttu-id="03edd-214">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span><span class="sxs-lookup"><span data-stu-id="03edd-214">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="03edd-215">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at just the lowest bitrate, as opposed to inserting video at every output bitrate.</span><span class="sxs-lookup"><span data-stu-id="03edd-215">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at just the lowest bitrate, as opposed to inserting video at every output bitrate.</span></span> <span data-ttu-id="03edd-216">To achieve this, you need to specify the "InsertBlackIfNoVideoBottomLayerOnly" flag.</span><span class="sxs-lookup"><span data-stu-id="03edd-216">To achieve this, you need to specify the "InsertBlackIfNoVideoBottomLayerOnly" flag.</span></span>

<span data-ttu-id="03edd-217">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span><span class="sxs-lookup"><span data-stu-id="03edd-217">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="03edd-218">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-218">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="03edd-219">XML preset</span><span class="sxs-lookup"><span data-stu-id="03edd-219">XML preset</span></span>
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <StretchMode>AutoSize</StretchMode>
    <Condition>InsertBlackIfNoVideoBottomLayerOnly</Condition>

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="03edd-220">Inserting video at all output bitrates</span><span class="sxs-lookup"><span data-stu-id="03edd-220">Inserting video at all output bitrates</span></span>
<span data-ttu-id="03edd-221">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span><span class="sxs-lookup"><span data-stu-id="03edd-221">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="03edd-222">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at all the output bitrates.</span><span class="sxs-lookup"><span data-stu-id="03edd-222">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at all the output bitrates.</span></span> <span data-ttu-id="03edd-223">This ensures that your output Assets are all homogenous with respect to number of video tracks and audio tracks.</span><span class="sxs-lookup"><span data-stu-id="03edd-223">This ensures that your output Assets are all homogenous with respect to number of video tracks and audio tracks.</span></span> <span data-ttu-id="03edd-224">To achieve this, you need to specify the "InsertBlackIfNoVideo" flag.</span><span class="sxs-lookup"><span data-stu-id="03edd-224">To achieve this, you need to specify the "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="03edd-225">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span><span class="sxs-lookup"><span data-stu-id="03edd-225">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="03edd-226">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-226">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="03edd-227">XML preset</span><span class="sxs-lookup"><span data-stu-id="03edd-227">XML preset</span></span>
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <StretchMode>AutoSize</StretchMode>
    <Condition>InsertBlackIfNoVideo</Condition>

## <a id="rotate_video"></a><span data-ttu-id="03edd-228">Rotate a video</span><span class="sxs-lookup"><span data-stu-id="03edd-228">Rotate a video</span></span>
<span data-ttu-id="03edd-229">The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span><span class="sxs-lookup"><span data-stu-id="03edd-229">The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="03edd-230">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming video file and compensate for it.</span><span class="sxs-lookup"><span data-stu-id="03edd-230">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming video file and compensate for it.</span></span> <span data-ttu-id="03edd-231">Include the following **Sources** element to one of the presets defined in [this](media-services-mes-presets-overview.md) section:</span><span class="sxs-lookup"><span data-stu-id="03edd-231">Include the following **Sources** element to one of the presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="03edd-232">JSON preset</span><span class="sxs-lookup"><span data-stu-id="03edd-232">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="03edd-233">XML preset</span><span class="sxs-lookup"><span data-stu-id="03edd-233">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="03edd-234">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how the encoder interprets the Width and Height settings in the preset, when rotation compensation is triggered.</span><span class="sxs-lookup"><span data-stu-id="03edd-234">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how the encoder interprets the Width and Height settings in the preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="03edd-235">You can use the value "0" to indicate to the encoder to ignore rotation metadata, if present, in the input video.</span><span class="sxs-lookup"><span data-stu-id="03edd-235">You can use the value "0" to indicate to the encoder to ignore rotation metadata, if present, in the input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="03edd-236">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="03edd-236">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="03edd-237">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="03edd-237">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="03edd-238">See Also</span><span class="sxs-lookup"><span data-stu-id="03edd-238">See Also</span></span>
[<span data-ttu-id="03edd-239">Media Services Encoding Overview</span><span class="sxs-lookup"><span data-stu-id="03edd-239">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
