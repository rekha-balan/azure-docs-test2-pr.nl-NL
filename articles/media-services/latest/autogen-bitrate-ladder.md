---
title: Use the Standard Encoder in Azure Media Services to encode videos using an auto-generated bitrate ladder | Microsoft Docs
description: This topic shows how to use the Standard Encoder in Media Services to encode an input video with an auto-generated bitrate ladder, based on the input resolution and bitrate. The input resolution and bitrate will never be exceeded. For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/19/2018
ms.author: juliako
ms.openlocfilehash: 6e447c04f4a94f2fb534ecb0605595a90816431e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867000"
---
#  <a name="encode-with-an-auto-generated-bitrate-ladder"></a><span data-ttu-id="48d93-105">Encode with an auto-generated bitrate ladder</span><span class="sxs-lookup"><span data-stu-id="48d93-105">Encode with an auto-generated bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="48d93-106">Overview</span><span class="sxs-lookup"><span data-stu-id="48d93-106">Overview</span></span>

<span data-ttu-id="48d93-107">This article explains how to use the Standard Encoder in Media Services to encode an input video into an auto-generated bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span><span class="sxs-lookup"><span data-stu-id="48d93-107">This article explains how to use the Standard Encoder in Media Services to encode an input video into an auto-generated bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span></span> <span data-ttu-id="48d93-108">This built-in encoder setting, or preset, will never exceed the input resolution and bitrate.</span><span class="sxs-lookup"><span data-stu-id="48d93-108">This built-in encoder setting, or preset, will never exceed the input resolution and bitrate.</span></span> <span data-ttu-id="48d93-109">For example, if the input is 720p at 3 Mbps, output remains 720p at best, and will start at rates lower than 3 Mbps.</span><span class="sxs-lookup"><span data-stu-id="48d93-109">For example, if the input is 720p at 3 Mbps, output remains 720p at best, and will start at rates lower than 3 Mbps.</span></span>

### <a name="encoding-for-streaming"></a><span data-ttu-id="48d93-110">Encoding for streaming</span><span class="sxs-lookup"><span data-stu-id="48d93-110">Encoding for streaming</span></span>

<span data-ttu-id="48d93-111">When you use the **AdaptiveStreaming** preset in **Transform**, you get an output that is suitable for delivery via streaming protocols like HLS and DASH.</span><span class="sxs-lookup"><span data-stu-id="48d93-111">When you use the **AdaptiveStreaming** preset in **Transform**, you get an output that is suitable for delivery via streaming protocols like HLS and DASH.</span></span> <span data-ttu-id="48d93-112">When using this preset, the service intelligently determines how many video layers to generate and at what bitrate and resolution.</span><span class="sxs-lookup"><span data-stu-id="48d93-112">When using this preset, the service intelligently determines how many video layers to generate and at what bitrate and resolution.</span></span> <span data-ttu-id="48d93-113">The output content contains MP4 files where AAC-encoded audio and H.264-encoded video is not interleaved.</span><span class="sxs-lookup"><span data-stu-id="48d93-113">The output content contains MP4 files where AAC-encoded audio and H.264-encoded video is not interleaved.</span></span>

<span data-ttu-id="48d93-114">To see an example of how this preset is used, see [Stream a file](stream-files-dotnet-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="48d93-114">To see an example of how this preset is used, see [Stream a file](stream-files-dotnet-quickstart.md).</span></span>

## <a name="output"></a><span data-ttu-id="48d93-115">Output</span><span class="sxs-lookup"><span data-stu-id="48d93-115">Output</span></span>

<span data-ttu-id="48d93-116">This section shows three examples of the output video layers produced by the Media Services encoder as a result of encoding with the **AdaptiveStreaming** preset.</span><span class="sxs-lookup"><span data-stu-id="48d93-116">This section shows three examples of the output video layers produced by the Media Services encoder as a result of encoding with the **AdaptiveStreaming** preset.</span></span> <span data-ttu-id="48d93-117">In all cases, the output contains an audio-only MP4 file with stereo audio encoded at 128 kbps.</span><span class="sxs-lookup"><span data-stu-id="48d93-117">In all cases, the output contains an audio-only MP4 file with stereo audio encoded at 128 kbps.</span></span>

### <a name="example-1"></a><span data-ttu-id="48d93-118">Example 1</span><span class="sxs-lookup"><span data-stu-id="48d93-118">Example 1</span></span>
<span data-ttu-id="48d93-119">Source with height "1080" and framerate "29.970" produces 6 video layers:</span><span class="sxs-lookup"><span data-stu-id="48d93-119">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="48d93-120">Layer</span><span class="sxs-lookup"><span data-stu-id="48d93-120">Layer</span></span>|<span data-ttu-id="48d93-121">Height</span><span class="sxs-lookup"><span data-stu-id="48d93-121">Height</span></span>|<span data-ttu-id="48d93-122">Width</span><span class="sxs-lookup"><span data-stu-id="48d93-122">Width</span></span>|<span data-ttu-id="48d93-123">Bitrate (kbps)</span><span class="sxs-lookup"><span data-stu-id="48d93-123">Bitrate (kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="48d93-124">1</span><span class="sxs-lookup"><span data-stu-id="48d93-124">1</span></span>|<span data-ttu-id="48d93-125">1080</span><span class="sxs-lookup"><span data-stu-id="48d93-125">1080</span></span>|<span data-ttu-id="48d93-126">1920</span><span class="sxs-lookup"><span data-stu-id="48d93-126">1920</span></span>|<span data-ttu-id="48d93-127">6780</span><span class="sxs-lookup"><span data-stu-id="48d93-127">6780</span></span>|
|<span data-ttu-id="48d93-128">2</span><span class="sxs-lookup"><span data-stu-id="48d93-128">2</span></span>|<span data-ttu-id="48d93-129">720</span><span class="sxs-lookup"><span data-stu-id="48d93-129">720</span></span>|<span data-ttu-id="48d93-130">1280</span><span class="sxs-lookup"><span data-stu-id="48d93-130">1280</span></span>|<span data-ttu-id="48d93-131">3520</span><span class="sxs-lookup"><span data-stu-id="48d93-131">3520</span></span>|
|<span data-ttu-id="48d93-132">3</span><span class="sxs-lookup"><span data-stu-id="48d93-132">3</span></span>|<span data-ttu-id="48d93-133">540</span><span class="sxs-lookup"><span data-stu-id="48d93-133">540</span></span>|<span data-ttu-id="48d93-134">960</span><span class="sxs-lookup"><span data-stu-id="48d93-134">960</span></span>|<span data-ttu-id="48d93-135">2210</span><span class="sxs-lookup"><span data-stu-id="48d93-135">2210</span></span>|
|<span data-ttu-id="48d93-136">4</span><span class="sxs-lookup"><span data-stu-id="48d93-136">4</span></span>|<span data-ttu-id="48d93-137">360</span><span class="sxs-lookup"><span data-stu-id="48d93-137">360</span></span>|<span data-ttu-id="48d93-138">640</span><span class="sxs-lookup"><span data-stu-id="48d93-138">640</span></span>|<span data-ttu-id="48d93-139">1150</span><span class="sxs-lookup"><span data-stu-id="48d93-139">1150</span></span>|
|<span data-ttu-id="48d93-140">5</span><span class="sxs-lookup"><span data-stu-id="48d93-140">5</span></span>|<span data-ttu-id="48d93-141">270</span><span class="sxs-lookup"><span data-stu-id="48d93-141">270</span></span>|<span data-ttu-id="48d93-142">480</span><span class="sxs-lookup"><span data-stu-id="48d93-142">480</span></span>|<span data-ttu-id="48d93-143">720</span><span class="sxs-lookup"><span data-stu-id="48d93-143">720</span></span>|
|<span data-ttu-id="48d93-144">6</span><span class="sxs-lookup"><span data-stu-id="48d93-144">6</span></span>|<span data-ttu-id="48d93-145">180</span><span class="sxs-lookup"><span data-stu-id="48d93-145">180</span></span>|<span data-ttu-id="48d93-146">320</span><span class="sxs-lookup"><span data-stu-id="48d93-146">320</span></span>|<span data-ttu-id="48d93-147">380</span><span class="sxs-lookup"><span data-stu-id="48d93-147">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="48d93-148">Example 2</span><span class="sxs-lookup"><span data-stu-id="48d93-148">Example 2</span></span>
<span data-ttu-id="48d93-149">Source with height "720" and framerate "23.970" produces 5 video layers:</span><span class="sxs-lookup"><span data-stu-id="48d93-149">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="48d93-150">Layer</span><span class="sxs-lookup"><span data-stu-id="48d93-150">Layer</span></span>|<span data-ttu-id="48d93-151">Height</span><span class="sxs-lookup"><span data-stu-id="48d93-151">Height</span></span>|<span data-ttu-id="48d93-152">Width</span><span class="sxs-lookup"><span data-stu-id="48d93-152">Width</span></span>|<span data-ttu-id="48d93-153">Bitrate (kbps)</span><span class="sxs-lookup"><span data-stu-id="48d93-153">Bitrate (kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="48d93-154">1</span><span class="sxs-lookup"><span data-stu-id="48d93-154">1</span></span>|<span data-ttu-id="48d93-155">720</span><span class="sxs-lookup"><span data-stu-id="48d93-155">720</span></span>|<span data-ttu-id="48d93-156">1280</span><span class="sxs-lookup"><span data-stu-id="48d93-156">1280</span></span>|<span data-ttu-id="48d93-157">2940</span><span class="sxs-lookup"><span data-stu-id="48d93-157">2940</span></span>|
|<span data-ttu-id="48d93-158">2</span><span class="sxs-lookup"><span data-stu-id="48d93-158">2</span></span>|<span data-ttu-id="48d93-159">540</span><span class="sxs-lookup"><span data-stu-id="48d93-159">540</span></span>|<span data-ttu-id="48d93-160">960</span><span class="sxs-lookup"><span data-stu-id="48d93-160">960</span></span>|<span data-ttu-id="48d93-161">1850</span><span class="sxs-lookup"><span data-stu-id="48d93-161">1850</span></span>|
|<span data-ttu-id="48d93-162">3</span><span class="sxs-lookup"><span data-stu-id="48d93-162">3</span></span>|<span data-ttu-id="48d93-163">360</span><span class="sxs-lookup"><span data-stu-id="48d93-163">360</span></span>|<span data-ttu-id="48d93-164">640</span><span class="sxs-lookup"><span data-stu-id="48d93-164">640</span></span>|<span data-ttu-id="48d93-165">960</span><span class="sxs-lookup"><span data-stu-id="48d93-165">960</span></span>|
|<span data-ttu-id="48d93-166">4</span><span class="sxs-lookup"><span data-stu-id="48d93-166">4</span></span>|<span data-ttu-id="48d93-167">270</span><span class="sxs-lookup"><span data-stu-id="48d93-167">270</span></span>|<span data-ttu-id="48d93-168">480</span><span class="sxs-lookup"><span data-stu-id="48d93-168">480</span></span>|<span data-ttu-id="48d93-169">600</span><span class="sxs-lookup"><span data-stu-id="48d93-169">600</span></span>|
|<span data-ttu-id="48d93-170">5</span><span class="sxs-lookup"><span data-stu-id="48d93-170">5</span></span>|<span data-ttu-id="48d93-171">180</span><span class="sxs-lookup"><span data-stu-id="48d93-171">180</span></span>|<span data-ttu-id="48d93-172">320</span><span class="sxs-lookup"><span data-stu-id="48d93-172">320</span></span>|<span data-ttu-id="48d93-173">320</span><span class="sxs-lookup"><span data-stu-id="48d93-173">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="48d93-174">Example 3</span><span class="sxs-lookup"><span data-stu-id="48d93-174">Example 3</span></span>
<span data-ttu-id="48d93-175">Source with height "360" and framerate "29.970" produces 3 video layers:</span><span class="sxs-lookup"><span data-stu-id="48d93-175">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="48d93-176">Layer</span><span class="sxs-lookup"><span data-stu-id="48d93-176">Layer</span></span>|<span data-ttu-id="48d93-177">Height</span><span class="sxs-lookup"><span data-stu-id="48d93-177">Height</span></span>|<span data-ttu-id="48d93-178">Width</span><span class="sxs-lookup"><span data-stu-id="48d93-178">Width</span></span>|<span data-ttu-id="48d93-179">Bitrate (kbps)</span><span class="sxs-lookup"><span data-stu-id="48d93-179">Bitrate (kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="48d93-180">1</span><span class="sxs-lookup"><span data-stu-id="48d93-180">1</span></span>|<span data-ttu-id="48d93-181">360</span><span class="sxs-lookup"><span data-stu-id="48d93-181">360</span></span>|<span data-ttu-id="48d93-182">640</span><span class="sxs-lookup"><span data-stu-id="48d93-182">640</span></span>|<span data-ttu-id="48d93-183">700</span><span class="sxs-lookup"><span data-stu-id="48d93-183">700</span></span>|
|<span data-ttu-id="48d93-184">2</span><span class="sxs-lookup"><span data-stu-id="48d93-184">2</span></span>|<span data-ttu-id="48d93-185">270</span><span class="sxs-lookup"><span data-stu-id="48d93-185">270</span></span>|<span data-ttu-id="48d93-186">480</span><span class="sxs-lookup"><span data-stu-id="48d93-186">480</span></span>|<span data-ttu-id="48d93-187">440</span><span class="sxs-lookup"><span data-stu-id="48d93-187">440</span></span>|
|<span data-ttu-id="48d93-188">3</span><span class="sxs-lookup"><span data-stu-id="48d93-188">3</span></span>|<span data-ttu-id="48d93-189">180</span><span class="sxs-lookup"><span data-stu-id="48d93-189">180</span></span>|<span data-ttu-id="48d93-190">320</span><span class="sxs-lookup"><span data-stu-id="48d93-190">320</span></span>|<span data-ttu-id="48d93-191">230</span><span class="sxs-lookup"><span data-stu-id="48d93-191">230</span></span>|

## <a name="next-steps"></a><span data-ttu-id="48d93-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="48d93-192">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="48d93-193">Stream a file</span><span class="sxs-lookup"><span data-stu-id="48d93-193">Stream a file</span></span>](stream-files-dotnet-quickstart.md)
