---
title: H264 Single Bitrate High Quality SD for Android | Microsoft Docs
description: The topic gives an overview of the **H264 Single Bitrate High Quality SD for Android** task preset.
author: Juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 4a190f24-ec6a-47e7-8bca-6294e064b15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: juliako
ms.openlocfilehash: 09c6c4f8552cb8dd9b987d5e2e6d3175d4780025
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562833"
---
# <a name="h264-single-bitrate-high-quality-sd-for-android"></a><span data-ttu-id="d8e38-103">H264 Single Bitrate High Quality SD for Android</span><span class="sxs-lookup"><span data-stu-id="d8e38-103">H264 Single Bitrate High Quality SD for Android</span></span>
<span data-ttu-id="d8e38-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span><span class="sxs-lookup"><span data-stu-id="d8e38-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="d8e38-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span><span class="sxs-lookup"><span data-stu-id="d8e38-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="d8e38-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span><span class="sxs-lookup"><span data-stu-id="d8e38-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="d8e38-107">You would then pass the custom preset to the encoder.</span><span class="sxs-lookup"><span data-stu-id="d8e38-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="d8e38-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8e38-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="d8e38-109">This topic shows the `H264 Single Bitrate High Quality SD for Android` preset in XML and JSON format.</span><span class="sxs-lookup"><span data-stu-id="d8e38-109">This topic shows the `H264 Single Bitrate High Quality SD for Android` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="d8e38-110">This preset produces a single MP4 file with a bitrate of 500 kbps, and stereo AAC audio.</span><span class="sxs-lookup"><span data-stu-id="d8e38-110">This preset produces a single MP4 file with a bitrate of 500 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="d8e38-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span><span class="sxs-lookup"><span data-stu-id="d8e38-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="d8e38-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span><span class="sxs-lookup"><span data-stu-id="d8e38-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="d8e38-113">XML</span><span class="sxs-lookup"><span data-stu-id="d8e38-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:05</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>500</Bitrate>  
          <Width>480</Width>  
          <Height>360</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Baseline</Profile>  
          <Level>3</Level>  
          <BFrames>0</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>false</AdaptiveBFrame>  
          <EntropyMode>Cavlc</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>500</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
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
```  
  
 <span data-ttu-id="d8e38-114">JSON</span><span class="sxs-lookup"><span data-stu-id="d8e38-114">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:05",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Baseline",  
          "Level": "3",  
          "Bitrate": 500,  
          "MaxBitrate": 500,  
          "BufferWindow": "00:00:05",  
          "Width": 480,  
          "Height": 360,  
          "ReferenceFrames": 3,  
          "EntropyMode": "Cavlc",  
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