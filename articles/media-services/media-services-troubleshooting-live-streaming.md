---
title: Troubleshooting guide for live streaming | Microsoft Docs
description: This topic gives suggestions on how to troubleshoot live streaming problems.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/12/2016
ms.author: juliako
ms.openlocfilehash: fe66d144006073fe9241f5e1360a0587dfb25204
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548787"
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="090fd-103">Troubleshooting guide for live streaming</span><span class="sxs-lookup"><span data-stu-id="090fd-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="090fd-104">This topic gives suggestions on how to troubleshoot some live streaming problems.</span><span class="sxs-lookup"><span data-stu-id="090fd-104">This topic gives suggestions on how to troubleshoot some live streaming problems.</span></span>

## <a name="issues-related-to-on-premises-encoders"></a><span data-ttu-id="090fd-105">Issues related to on-premises encoders</span><span class="sxs-lookup"><span data-stu-id="090fd-105">Issues related to on-premises encoders</span></span>
<span data-ttu-id="090fd-106">This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.</span><span class="sxs-lookup"><span data-stu-id="090fd-106">This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-to-see-logs"></a><span data-ttu-id="090fd-107">Problem: Would like to see logs</span><span class="sxs-lookup"><span data-stu-id="090fd-107">Problem: Would like to see logs</span></span>
* <span data-ttu-id="090fd-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span><span class="sxs-lookup"><span data-stu-id="090fd-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="090fd-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="090fd-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="090fd-110">**Elemental Live**: You can find has links to logs on the management portal.</span><span class="sxs-lookup"><span data-stu-id="090fd-110">**Elemental Live**: You can find has links to logs on the management portal.</span></span> <span data-ttu-id="090fd-111">Click on **Stats**, then **Logs**.</span><span class="sxs-lookup"><span data-stu-id="090fd-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="090fd-112">On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session.</span><span class="sxs-lookup"><span data-stu-id="090fd-112">On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session.</span></span> 
  * <span data-ttu-id="090fd-113">**Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.</span><span class="sxs-lookup"><span data-stu-id="090fd-113">**Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="090fd-114">Problem: There is no option for outputting a progressive stream</span><span class="sxs-lookup"><span data-stu-id="090fd-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="090fd-115">**Potential issue**: The encoder being used doesn't automatically deinterlace.</span><span class="sxs-lookup"><span data-stu-id="090fd-115">**Potential issue**: The encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="090fd-116">**Troubleshooting steps**: Look for a de-interlacing option within the encoder interface.</span><span class="sxs-lookup"><span data-stu-id="090fd-116">**Troubleshooting steps**: Look for a de-interlacing option within the encoder interface.</span></span> <span data-ttu-id="090fd-117">Once de-interlacing is enabled, check again for progressive output settings.</span><span class="sxs-lookup"><span data-stu-id="090fd-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a><span data-ttu-id="090fd-118">Problem: Tried several encoder output settings and still unable to connect.</span><span class="sxs-lookup"><span data-stu-id="090fd-118">Problem: Tried several encoder output settings and still unable to connect.</span></span>
* <span data-ttu-id="090fd-119">**Potential issue**: Azure encoding channel was not properly reset.</span><span class="sxs-lookup"><span data-stu-id="090fd-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="090fd-120">**Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel.</span><span class="sxs-lookup"><span data-stu-id="090fd-120">**Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel.</span></span> <span data-ttu-id="090fd-121">Once running again, try connecting your encoder with the new settings.</span><span class="sxs-lookup"><span data-stu-id="090fd-121">Once running again, try connecting your encoder with the new settings.</span></span> <span data-ttu-id="090fd-122">If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span><span class="sxs-lookup"><span data-stu-id="090fd-122">If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="090fd-123">**Potential issue**: The GOP size or key frame settings are not optimal.</span><span class="sxs-lookup"><span data-stu-id="090fd-123">**Potential issue**: The GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="090fd-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span><span class="sxs-lookup"><span data-stu-id="090fd-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="090fd-125">Some encoders calculate this setting in number of frames, while others use seconds.</span><span class="sxs-lookup"><span data-stu-id="090fd-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="090fd-126">For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.</span><span class="sxs-lookup"><span data-stu-id="090fd-126">For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.</span></span>  
* <span data-ttu-id="090fd-127">**Potential issue**: Closed ports are blocking the stream.</span><span class="sxs-lookup"><span data-stu-id="090fd-127">**Potential issue**: Closed ports are blocking the stream.</span></span> 
  
    <span data-ttu-id="090fd-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open.</span><span class="sxs-lookup"><span data-stu-id="090fd-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="090fd-129">When using RTP streaming, confirm that outbound port 2010 is open.</span><span class="sxs-lookup"><span data-stu-id="090fd-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a><span data-ttu-id="090fd-130">Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.</span><span class="sxs-lookup"><span data-stu-id="090fd-130">Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.</span></span>
* <span data-ttu-id="090fd-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.</span><span class="sxs-lookup"><span data-stu-id="090fd-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.</span></span>  
  
    <span data-ttu-id="090fd-132">**Troubleshooting steps**: To find the IP address, open a command prompt on any computer.</span><span class="sxs-lookup"><span data-stu-id="090fd-132">**Troubleshooting steps**: To find the IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="090fd-133">To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.</span><span class="sxs-lookup"><span data-stu-id="090fd-133">To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.</span></span>  
  
    <span data-ttu-id="090fd-134">Once the command prompt is open, type "Ping [AMS Host Name]".</span><span class="sxs-lookup"><span data-stu-id="090fd-134">Once the command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="090fd-135">The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example:</span><span class="sxs-lookup"><span data-stu-id="090fd-135">The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example:</span></span> 
  
    <span data-ttu-id="090fd-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="090fd-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="090fd-138">If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="090fd-138">If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="090fd-139">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="090fd-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="090fd-140">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="090fd-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


