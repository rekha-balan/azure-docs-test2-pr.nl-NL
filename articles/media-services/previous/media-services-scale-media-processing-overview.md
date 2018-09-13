---
title: Scaling Media Processing overview | Microsoft Docs
description: This topic is an overview of scaling Media Processing with Azure Media Services.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2018
ms.author: juliako
ms.openlocfilehash: 81fab8903c0101d0e4aae8a392f05129651cd762
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867945"
---
# <a name="scaling-media-processing-overview"></a>Scaling Media Processing overview
This page gives an overview of how and why to scale media processing. 

## <a name="overview"></a>Overview
A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed. You can pick between the following reserved unit types: **S1**, **S2**, or **S3**. For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type. For more information, see the [Reserved Unit Types](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

In addition to specifying the reserved unit type, you can specify to provision your account with reserved units. The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account. For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed. The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes. If an account does not have any reserved units provisioned, then tasks will be picked up sequentially. In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.

## <a name="choosing-between-different-reserved-unit-types"></a>Choosing between different reserved unit types
The following table helps you make decision when choosing between different encoding speeds. It also provides a few benchmark cases and provides SAS URLs that you can use to download videos on which you can perform your own tests:

| Scenarios | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Intended use case |Single bitrate encoding. <br/>Files at SD or below resolutions, not time sensitive, low cost. |Single bitrate and multiple bitrate encoding.<br/>Normal usage for both SD and HD encoding. |Single bitrate and multiple bitrate encoding.<br/>Full HD and 4K resolution videos. Time sensitive, faster turnaround encoding. |
| Benchmark |Encoding to a single bitrate MP4 file, at the same resolution, takes approximately 11 minutes. |Encoding with "H264 Single Bitrate 720p" preset takes approximately 5 minutes.<br/><br/>Encoding with "H264 Multiple Bitrate 720p" preset takes approximately 11.5 minutes. |Encoding with "H264 Single Bitrate 1080p" preset takes approximately 2.7 minutes.<br/><br/>Encoding with "H264 Multiple Bitrate 1080p" preset takes approximately 5.7 minutes. |


## <a name="considerations"></a>Considerations
> [!IMPORTANT]
> Review considerations described in this section.  
> 
> 

* For the Audio Analysis and Video Analysis jobs that are triggered by Media Services v3 or Video Indexer, S3 unit type is highly recommended.
* If using the shared pool, that is, without any reserved units, then your encode tasks have the same performance as with S1 RUs. However, there is no upper bound to the time your Tasks can spend in queued state, and at any given time, at most only one Task will be running.

## <a name="billing"></a>Billing

You are charged based on actual minutes of usage of Media Reserved Units. For a detailed explanation, see the FAQ section of the [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/) page.   

## <a name="quotas-and-limitations"></a>Quotas and limitations
For information about quotas and limitations and how to open a support ticket, see [Quotas and limitations](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Next step
Achieve the scaling media processing task with one of these technologies: 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 

> [!NOTE]
> To get the latest version of Java SDK and get started developing with Java, see [Get started with the Java client SDK for Media Services](https://docs.microsoft.com/azure/media-services/media-services-java-how-to-use). <br/>
> To download the latest PHP SDK for Media Services, look for version 0.5.7 of the Microsoft/WindowAzure package in the [Packagist repository](https://packagist.org/packages/microsoft/windowsazure#v0.5.7).  

## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

