---
title: H264 Single Bitrate 16x9 SD Audio 5.1 | Microsoft Docs
description: The topic gives an overview of the **H264 Single Bitrate 16x9 SD Audio 5.1** task preset.
author: Juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: d57cd39f-60e8-4248-a21d-c5b9f096b0ce
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: juliako
ms.openlocfilehash: 8ca2eb740a2b2b1ef60fdb6037c619fb378b2575
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552232"
---
# <a name="h264-single-bitrate-16x9-sd-audio-51"></a><span data-ttu-id="9d7a6-103">H264 Single Bitrate 16x9 SD Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="9d7a6-103">H264 Single Bitrate 16x9 SD Audio 5.1</span></span>
<span data-ttu-id="9d7a6-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span><span class="sxs-lookup"><span data-stu-id="9d7a6-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="9d7a6-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span><span class="sxs-lookup"><span data-stu-id="9d7a6-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="9d7a6-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span><span class="sxs-lookup"><span data-stu-id="9d7a6-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="9d7a6-107">You would then pass the custom preset to the encoder.</span><span class="sxs-lookup"><span data-stu-id="9d7a6-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="9d7a6-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d7a6-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="9d7a6-109">This topic shows the `H264 Single Bitrate 16x9 SD Audio 5.1` preset in XML and JSON format.</span><span class="sxs-lookup"><span data-stu-id="9d7a6-109">This topic shows the `H264 Single Bitrate 16x9 SD Audio 5.1` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="9d7a6-110">This preset produces a single MP4 file with a bitrate of 2200 kbps, and AAC 5.1 audio.</span><span class="sxs-lookup"><span data-stu-id="9d7a6-110">This preset produces a single MP4 file with a bitrate of 2200 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="9d7a6-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span><span class="sxs-lookup"><span data-stu-id="9d7a6-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="9d7a6-112">For explanations of what each element means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9d7a6-112">For explanations of what each element means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
 <span data-ttu-id="9d7a6-113">XML</span><span class="sxs-lookup"><span data-stu-id="9d7a6-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>2200</Bitrate>  
          <Width>848</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>2200</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="9d7a6-114">JSON</span><span class="sxs-lookup"><span data-stu-id="9d7a6-114">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 2200,  
          "MaxBitrate": 2200,  
          "BufferWindow": "00:00:05",  
          "Width": 848,  
          "Height": 480,  
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
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
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