---
title: Learn about encoders recommended by Azure Media Services | Microsoft Docs
description: Learn about encoders recommended by media services
services: media-services
keywords: encoding;encoders;media
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: d0c5536d2339470eac058250cc14e1f250b86d90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968739"
---
# <a name="recommended-on-premises-encoders"></a><span data-ttu-id="622f6-104">Recommended on-premises encoders</span><span class="sxs-lookup"><span data-stu-id="622f6-104">Recommended on-premises encoders</span></span>
<span data-ttu-id="622f6-105">When live streaming with Azure Media Services, you can specify how you want your channel to receive the input stream.</span><span class="sxs-lookup"><span data-stu-id="622f6-105">When live streaming with Azure Media Services, you can specify how you want your channel to receive the input stream.</span></span> <span data-ttu-id="622f6-106">If you choose to use an on-prem encoder with a live encoding channel, your encoder should push a high-quality single-bitrate stream as output.</span><span class="sxs-lookup"><span data-stu-id="622f6-106">If you choose to use an on-prem encoder with a live encoding channel, your encoder should push a high-quality single-bitrate stream as output.</span></span> <span data-ttu-id="622f6-107">If you choose to use an on-prem encoder with a pass through channel, your encoder should push a multi-bitrate stream as output with all desired output qualities.</span><span class="sxs-lookup"><span data-stu-id="622f6-107">If you choose to use an on-prem encoder with a pass through channel, your encoder should push a multi-bitrate stream as output with all desired output qualities.</span></span> <span data-ttu-id="622f6-108">For more information, see [Live streaming with on-prem encoders](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="622f6-108">For more information, see [Live streaming with on-prem encoders](media-services-live-streaming-with-onprem-encoders.md).</span></span>

<span data-ttu-id="622f6-109">Azure Media Services recommends using one of following live encoders that have RTMP as output:</span><span class="sxs-lookup"><span data-stu-id="622f6-109">Azure Media Services recommends using one of following live encoders that have RTMP as output:</span></span>
- <span data-ttu-id="622f6-110">Adobe Flash Media Live Encoder 3.2</span><span class="sxs-lookup"><span data-stu-id="622f6-110">Adobe Flash Media Live Encoder 3.2</span></span>
- <span data-ttu-id="622f6-111">Haivision Makito X HEVC</span><span class="sxs-lookup"><span data-stu-id="622f6-111">Haivision Makito X HEVC</span></span>
- <span data-ttu-id="622f6-112">Telestream Wirecast 8.1</span><span class="sxs-lookup"><span data-stu-id="622f6-112">Telestream Wirecast 8.1</span></span>
- <span data-ttu-id="622f6-113">Teradek Slice 756</span><span class="sxs-lookup"><span data-stu-id="622f6-113">Teradek Slice 756</span></span>
- <span data-ttu-id="622f6-114">TriCaster 8000</span><span class="sxs-lookup"><span data-stu-id="622f6-114">TriCaster 8000</span></span>
- <span data-ttu-id="622f6-115">Tricaster Mini HD-4</span><span class="sxs-lookup"><span data-stu-id="622f6-115">Tricaster Mini HD-4</span></span>

<span data-ttu-id="622f6-116">Azure Media Services recommends using one of the following live encoders that have multi-bitrate Smooth Streaming as output:</span><span class="sxs-lookup"><span data-stu-id="622f6-116">Azure Media Services recommends using one of the following live encoders that have multi-bitrate Smooth Streaming as output:</span></span>
- <span data-ttu-id="622f6-117">Ateme TITAN Live</span><span class="sxs-lookup"><span data-stu-id="622f6-117">Ateme TITAN Live</span></span>
- <span data-ttu-id="622f6-118">Cisco Digital Media Encoder 2200</span><span class="sxs-lookup"><span data-stu-id="622f6-118">Cisco Digital Media Encoder 2200</span></span>
- <span data-ttu-id="622f6-119">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="622f6-119">Elemental Live</span></span>
- <span data-ttu-id="622f6-120">Envivio 4Caster C4 Gen III</span><span class="sxs-lookup"><span data-stu-id="622f6-120">Envivio 4Caster C4 Gen III</span></span>
- <span data-ttu-id="622f6-121">Imagine Communications Selenio MCP3</span><span class="sxs-lookup"><span data-stu-id="622f6-121">Imagine Communications Selenio MCP3</span></span>
- <span data-ttu-id="622f6-122">Media Excel Hero Live</span><span class="sxs-lookup"><span data-stu-id="622f6-122">Media Excel Hero Live</span></span>

> [!NOTE]
> <span data-ttu-id="622f6-123">A live encoder can send a single-bitrate stream to a pass through channel, but this configuration is not recommended because it does not allow for adaptive bitrate streaming to the client.</span><span class="sxs-lookup"><span data-stu-id="622f6-123">A live encoder can send a single-bitrate stream to a pass through channel, but this configuration is not recommended because it does not allow for adaptive bitrate streaming to the client.</span></span>

## <a name="how-to-become-an-on-prem-encoder-partner"></a><span data-ttu-id="622f6-124">How to become an on-prem encoder partner</span><span class="sxs-lookup"><span data-stu-id="622f6-124">How to become an on-prem encoder partner</span></span>
<span data-ttu-id="622f6-125">As an Azure Media Services on-prem encoder partner, Media Services promotes your product by recommending your encoder to enterprise customers.</span><span class="sxs-lookup"><span data-stu-id="622f6-125">As an Azure Media Services on-prem encoder partner, Media Services promotes your product by recommending your encoder to enterprise customers.</span></span> <span data-ttu-id="622f6-126">To become an on-prem encoder partner, you must verify compatibility of your on-prem encoder with Media Services.</span><span class="sxs-lookup"><span data-stu-id="622f6-126">To become an on-prem encoder partner, you must verify compatibility of your on-prem encoder with Media Services.</span></span> <span data-ttu-id="622f6-127">To do so, complete the following verifications:</span><span class="sxs-lookup"><span data-stu-id="622f6-127">To do so, complete the following verifications:</span></span>

<span data-ttu-id="622f6-128">Pass through channel verification</span><span class="sxs-lookup"><span data-stu-id="622f6-128">Pass through channel verification</span></span>
1. <span data-ttu-id="622f6-129">Create or visit your Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="622f6-129">Create or visit your Azure Media Services account</span></span>
2. <span data-ttu-id="622f6-130">Create and start a **pass-through** channel</span><span class="sxs-lookup"><span data-stu-id="622f6-130">Create and start a **pass-through** channel</span></span>
3. <span data-ttu-id="622f6-131">Configure your encoder to push a multi-bitrate live stream.</span><span class="sxs-lookup"><span data-stu-id="622f6-131">Configure your encoder to push a multi-bitrate live stream.</span></span>
4. <span data-ttu-id="622f6-132">Create a published live event</span><span class="sxs-lookup"><span data-stu-id="622f6-132">Create a published live event</span></span>
5. <span data-ttu-id="622f6-133">Run your live encoder for approximately 10 minutes</span><span class="sxs-lookup"><span data-stu-id="622f6-133">Run your live encoder for approximately 10 minutes</span></span>
6. <span data-ttu-id="622f6-134">Stop the live event</span><span class="sxs-lookup"><span data-stu-id="622f6-134">Stop the live event</span></span>
7. <span data-ttu-id="622f6-135">Record the Asset ID, published streaming URL for the live archive, and the settings and version used from your live encoder</span><span class="sxs-lookup"><span data-stu-id="622f6-135">Record the Asset ID, published streaming URL for the live archive, and the settings and version used from your live encoder</span></span>
8. <span data-ttu-id="622f6-136">Reset the channel state after creating each sample</span><span class="sxs-lookup"><span data-stu-id="622f6-136">Reset the channel state after creating each sample</span></span>
9. <span data-ttu-id="622f6-137">Repeat steps 3 through 8 for all configurations supported by your encoder (with and without ad signaling/captions/different encoding speeds)</span><span class="sxs-lookup"><span data-stu-id="622f6-137">Repeat steps 3 through 8 for all configurations supported by your encoder (with and without ad signaling/captions/different encoding speeds)</span></span>

<span data-ttu-id="622f6-138">Live encoding channel verification</span><span class="sxs-lookup"><span data-stu-id="622f6-138">Live encoding channel verification</span></span>
1. <span data-ttu-id="622f6-139">Create or visit your Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="622f6-139">Create or visit your Azure Media Services account</span></span>
2. <span data-ttu-id="622f6-140">Create and start a **live encoding** channel</span><span class="sxs-lookup"><span data-stu-id="622f6-140">Create and start a **live encoding** channel</span></span>
3. <span data-ttu-id="622f6-141">Configure your encoder to push a single-bitrate live stream.</span><span class="sxs-lookup"><span data-stu-id="622f6-141">Configure your encoder to push a single-bitrate live stream.</span></span>
4. <span data-ttu-id="622f6-142">Create a published live event</span><span class="sxs-lookup"><span data-stu-id="622f6-142">Create a published live event</span></span>
5. <span data-ttu-id="622f6-143">Run your live encoder for approximately 10 minutes</span><span class="sxs-lookup"><span data-stu-id="622f6-143">Run your live encoder for approximately 10 minutes</span></span>
6. <span data-ttu-id="622f6-144">Stop the live event</span><span class="sxs-lookup"><span data-stu-id="622f6-144">Stop the live event</span></span>
7. <span data-ttu-id="622f6-145">Record the Asset ID, published streaming URL for the live archive, and the settings and version used from your live encoder</span><span class="sxs-lookup"><span data-stu-id="622f6-145">Record the Asset ID, published streaming URL for the live archive, and the settings and version used from your live encoder</span></span>
8. <span data-ttu-id="622f6-146">Reset the channel state after creating each sample</span><span class="sxs-lookup"><span data-stu-id="622f6-146">Reset the channel state after creating each sample</span></span>
9. <span data-ttu-id="622f6-147">Repeat steps 3 through 8 for all configurations supported by your encoder (with and without ad signaling/captions/various encoding speeds)</span><span class="sxs-lookup"><span data-stu-id="622f6-147">Repeat steps 3 through 8 for all configurations supported by your encoder (with and without ad signaling/captions/various encoding speeds)</span></span>

<span data-ttu-id="622f6-148">Longevity verification</span><span class="sxs-lookup"><span data-stu-id="622f6-148">Longevity verification</span></span>
1. <span data-ttu-id="622f6-149">Create or visit your Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="622f6-149">Create or visit your Azure Media Services account</span></span>
2. <span data-ttu-id="622f6-150">Create and start a **pass-through** channel</span><span class="sxs-lookup"><span data-stu-id="622f6-150">Create and start a **pass-through** channel</span></span>
3. <span data-ttu-id="622f6-151">Configure your encoder to push a multi-bitrate live stream.</span><span class="sxs-lookup"><span data-stu-id="622f6-151">Configure your encoder to push a multi-bitrate live stream.</span></span>
4. <span data-ttu-id="622f6-152">Create a published live event</span><span class="sxs-lookup"><span data-stu-id="622f6-152">Create a published live event</span></span>
5. <span data-ttu-id="622f6-153">Run your live encoder for one week or longer</span><span class="sxs-lookup"><span data-stu-id="622f6-153">Run your live encoder for one week or longer</span></span>
6. <span data-ttu-id="622f6-154">Stop the live event</span><span class="sxs-lookup"><span data-stu-id="622f6-154">Stop the live event</span></span>
7. <span data-ttu-id="622f6-155">Record the Asset ID, published streaming URL for the live archive, and the settings and version used from your live encoder</span><span class="sxs-lookup"><span data-stu-id="622f6-155">Record the Asset ID, published streaming URL for the live archive, and the settings and version used from your live encoder</span></span>

<span data-ttu-id="622f6-156">Lastly, send your recorded settings and live archive parameters to Media Services by emailing amsstreaming@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="622f6-156">Lastly, send your recorded settings and live archive parameters to Media Services by emailing amsstreaming@microsoft.com.</span></span> <span data-ttu-id="622f6-157">Upon receipt, Media Services performs verification tests on the samples from your live encoder.</span><span class="sxs-lookup"><span data-stu-id="622f6-157">Upon receipt, Media Services performs verification tests on the samples from your live encoder.</span></span> <span data-ttu-id="622f6-158">You can contact the Media Services with any questions regarding this process.</span><span class="sxs-lookup"><span data-stu-id="622f6-158">You can contact the Media Services with any questions regarding this process.</span></span>