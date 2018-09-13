---
title: Microsoft Azure Media Services scenarios and availability of features across datacenters | Microsoft Docs
description: This topic gives an overview of Microsoft Azure Media Services scenarios and availability of features and services across datacenters.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 8381cdfffd34ffa25d1b87be3a3aca3de69c2802
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871642"
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a><span data-ttu-id="6af1e-103">Scenarios and availability of Media Services features across datacenters</span><span class="sxs-lookup"><span data-stu-id="6af1e-103">Scenarios and availability of Media Services features across datacenters</span></span>

<span data-ttu-id="6af1e-104">Microsoft Azure Media Services (AMS) enables you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span><span class="sxs-lookup"><span data-stu-id="6af1e-104">Microsoft Azure Media Services (AMS) enables you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="6af1e-105">AMS operates in multiple datacenters around the world.</span><span class="sxs-lookup"><span data-stu-id="6af1e-105">AMS operates in multiple datacenters around the world.</span></span> <span data-ttu-id="6af1e-106">These datacenters are grouped in to geographic regions, giving you flexibility in choosing where to build your applications.</span><span class="sxs-lookup"><span data-stu-id="6af1e-106">These datacenters are grouped in to geographic regions, giving you flexibility in choosing where to build your applications.</span></span> <span data-ttu-id="6af1e-107">You can review the [list of regions and their locations](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="6af1e-107">You can review the [list of regions and their locations](https://azure.microsoft.com/regions/).</span></span> 

<span data-ttu-id="6af1e-108">This topic shows common scenarios for delivering your content [live](#live_scenarios) or [on-demand](#vod_scenarios).</span><span class="sxs-lookup"><span data-stu-id="6af1e-108">This topic shows common scenarios for delivering your content [live](#live_scenarios) or [on-demand](#vod_scenarios).</span></span> <span data-ttu-id="6af1e-109">The topic also provides details about availability of media features and services across datacenters.</span><span class="sxs-lookup"><span data-stu-id="6af1e-109">The topic also provides details about availability of media features and services across datacenters.</span></span>

## <a name="overview"></a><span data-ttu-id="6af1e-110">Overview</span><span class="sxs-lookup"><span data-stu-id="6af1e-110">Overview</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6af1e-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6af1e-111">Prerequisites</span></span>

<span data-ttu-id="6af1e-112">To start using Azure Media Services, you should have the following:</span><span class="sxs-lookup"><span data-stu-id="6af1e-112">To start using Azure Media Services, you should have the following:</span></span>

* <span data-ttu-id="6af1e-113">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="6af1e-113">An Azure account.</span></span> <span data-ttu-id="6af1e-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="6af1e-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6af1e-115">For details, see [Azure Free Trial](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6af1e-115">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="6af1e-116">An Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="6af1e-116">An Azure Media Services account.</span></span> <span data-ttu-id="6af1e-117">For more information, see [Create Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-117">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="6af1e-118">The streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="6af1e-118">The streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

    <span data-ttu-id="6af1e-119">When your AMS account is created, a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="6af1e-119">When your AMS account is created, a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="6af1e-120">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="6af1e-120">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint has to be in the **Running** state.</span></span>

### <a name="commonly-used-objects-when-developing-against-the-ams-odata-model"></a><span data-ttu-id="6af1e-121">Commonly used objects when developing against the AMS OData model</span><span class="sxs-lookup"><span data-stu-id="6af1e-121">Commonly used objects when developing against the AMS OData model</span></span>

<span data-ttu-id="6af1e-122">The following image shows some of the most commonly used objects when developing against the Media Services OData model.</span><span class="sxs-lookup"><span data-stu-id="6af1e-122">The following image shows some of the most commonly used objects when developing against the Media Services OData model.</span></span>

<span data-ttu-id="6af1e-123">Click the image to view it full size.</span><span class="sxs-lookup"><span data-stu-id="6af1e-123">Click the image to view it full size.</span></span>  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="6af1e-124">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="6af1e-124">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-the-clear-non-encrypted"></a><span data-ttu-id="6af1e-125">Protect content in storage and deliver streaming media in the clear (non-encrypted)</span><span class="sxs-lookup"><span data-stu-id="6af1e-125">Protect content in storage and deliver streaming media in the clear (non-encrypted)</span></span>

![VoD workflow](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. <span data-ttu-id="6af1e-127">Upload a high-quality media file into an asset.</span><span class="sxs-lookup"><span data-stu-id="6af1e-127">Upload a high-quality media file into an asset.</span></span>

    <span data-ttu-id="6af1e-128">It is recommended to apply storage encryption option to your asset in order to protect your content during upload and while at rest in storage.</span><span class="sxs-lookup"><span data-stu-id="6af1e-128">It is recommended to apply storage encryption option to your asset in order to protect your content during upload and while at rest in storage.</span></span>
2. <span data-ttu-id="6af1e-129">Encode to a set of adaptive bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="6af1e-129">Encode to a set of adaptive bitrate MP4 files.</span></span>

    <span data-ttu-id="6af1e-130">It is recommended to apply storage encryption option to the output asset in order to protect your content at rest.</span><span class="sxs-lookup"><span data-stu-id="6af1e-130">It is recommended to apply storage encryption option to the output asset in order to protect your content at rest.</span></span>
3. <span data-ttu-id="6af1e-131">Configure asset delivery policy (used by dynamic packaging).</span><span class="sxs-lookup"><span data-stu-id="6af1e-131">Configure asset delivery policy (used by dynamic packaging).</span></span>

    <span data-ttu-id="6af1e-132">If your asset is storage encrypted, you **must** configure asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="6af1e-132">If your asset is storage encrypted, you **must** configure asset delivery policy.</span></span>
4. <span data-ttu-id="6af1e-133">Publish the asset by creating an OnDemand locator.</span><span class="sxs-lookup"><span data-stu-id="6af1e-133">Publish the asset by creating an OnDemand locator.</span></span>
5. <span data-ttu-id="6af1e-134">Stream published content.</span><span class="sxs-lookup"><span data-stu-id="6af1e-134">Stream published content.</span></span>

<span data-ttu-id="6af1e-135">For information about availability in datacenters, see the [Availability](#availability) section.</span><span class="sxs-lookup"><span data-stu-id="6af1e-135">For information about availability in datacenters, see the [Availability](#availability) section.</span></span>

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a><span data-ttu-id="6af1e-136">Protect content in storage, deliver dynamically encrypted streaming media</span><span class="sxs-lookup"><span data-stu-id="6af1e-136">Protect content in storage, deliver dynamically encrypted streaming media</span></span>

![Protect with PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. <span data-ttu-id="6af1e-138">Upload a high-quality media file into an asset.</span><span class="sxs-lookup"><span data-stu-id="6af1e-138">Upload a high-quality media file into an asset.</span></span> <span data-ttu-id="6af1e-139">Apply storage encryption option to the asset.</span><span class="sxs-lookup"><span data-stu-id="6af1e-139">Apply storage encryption option to the asset.</span></span>
2. <span data-ttu-id="6af1e-140">Encode to a set of adaptive bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="6af1e-140">Encode to a set of adaptive bitrate MP4 files.</span></span> <span data-ttu-id="6af1e-141">Apply storage encryption option to the output asset.</span><span class="sxs-lookup"><span data-stu-id="6af1e-141">Apply storage encryption option to the output asset.</span></span>
3. <span data-ttu-id="6af1e-142">Create encryption content key for the asset you want to be dynamically encrypted during playback.</span><span class="sxs-lookup"><span data-stu-id="6af1e-142">Create encryption content key for the asset you want to be dynamically encrypted during playback.</span></span>
4. <span data-ttu-id="6af1e-143">Configure content key authorization policy.</span><span class="sxs-lookup"><span data-stu-id="6af1e-143">Configure content key authorization policy.</span></span>
5. <span data-ttu-id="6af1e-144">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span><span class="sxs-lookup"><span data-stu-id="6af1e-144">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
6. <span data-ttu-id="6af1e-145">Publish the asset by creating an OnDemand locator.</span><span class="sxs-lookup"><span data-stu-id="6af1e-145">Publish the asset by creating an OnDemand locator.</span></span>
7. <span data-ttu-id="6af1e-146">Stream published content.</span><span class="sxs-lookup"><span data-stu-id="6af1e-146">Stream published content.</span></span>

<span data-ttu-id="6af1e-147">For information about availability in datacenters, see the [Availability](#availability) section.</span><span class="sxs-lookup"><span data-stu-id="6af1e-147">For information about availability in datacenters, see the [Availability](#availability) section.</span></span>

## <a name="use-media-analytics-to-derive-actionable-insights-from-your-videos"></a><span data-ttu-id="6af1e-148">Use Media Analytics to derive actionable insights from your videos</span><span class="sxs-lookup"><span data-stu-id="6af1e-148">Use Media Analytics to derive actionable insights from your videos</span></span>

<span data-ttu-id="6af1e-149">Media Analytics is a collection of speech and vision components that make it easier for organizations and enterprises to derive actionable insights from their video files.</span><span class="sxs-lookup"><span data-stu-id="6af1e-149">Media Analytics is a collection of speech and vision components that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="6af1e-150">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-150">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

1. <span data-ttu-id="6af1e-151">Upload a high-quality media file into an asset.</span><span class="sxs-lookup"><span data-stu-id="6af1e-151">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="6af1e-152">Process your videos with one of the Media Analytics services described in the [Media Analytics overview](media-services-analytics-overview.md) section.</span><span class="sxs-lookup"><span data-stu-id="6af1e-152">Process your videos with one of the Media Analytics services described in the [Media Analytics overview](media-services-analytics-overview.md) section.</span></span>
3. <span data-ttu-id="6af1e-153">Media Analytics media processors produce MP4 files or JSON files.</span><span class="sxs-lookup"><span data-stu-id="6af1e-153">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="6af1e-154">If a media processor produced an MP4 file, you can progressively download the file.</span><span class="sxs-lookup"><span data-stu-id="6af1e-154">If a media processor produced an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="6af1e-155">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="6af1e-155">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span></span>

<span data-ttu-id="6af1e-156">For information about availability in datacenters, see the [Availability](#availability) section.</span><span class="sxs-lookup"><span data-stu-id="6af1e-156">For information about availability in datacenters, see the [Availability](#availability) section.</span></span>

## <a name="deliver-progressive-download"></a><span data-ttu-id="6af1e-157">Deliver progressive download</span><span class="sxs-lookup"><span data-stu-id="6af1e-157">Deliver progressive download</span></span>

1. <span data-ttu-id="6af1e-158">Upload a high-quality media file into an asset.</span><span class="sxs-lookup"><span data-stu-id="6af1e-158">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="6af1e-159">Encode to a single MP4 file.</span><span class="sxs-lookup"><span data-stu-id="6af1e-159">Encode to a single MP4 file.</span></span>
3. <span data-ttu-id="6af1e-160">Publish the asset by creating an OnDemand or SAS locator.</span><span class="sxs-lookup"><span data-stu-id="6af1e-160">Publish the asset by creating an OnDemand or SAS locator.</span></span>

    <span data-ttu-id="6af1e-161">If using SAS locator, the content is downloaded from the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="6af1e-161">If using SAS locator, the content is downloaded from the Azure blob storage.</span></span> <span data-ttu-id="6af1e-162">In this case, you do not need to have streaming endpoints in started state.</span><span class="sxs-lookup"><span data-stu-id="6af1e-162">In this case, you do not need to have streaming endpoints in started state.</span></span>
4. <span data-ttu-id="6af1e-163">Progressively download content.</span><span class="sxs-lookup"><span data-stu-id="6af1e-163">Progressively download content.</span></span>

## <a id="live_scenarios"></a><span data-ttu-id="6af1e-164">Delivering live-streaming events</span><span class="sxs-lookup"><span data-stu-id="6af1e-164">Delivering live-streaming events</span></span> 

1. <span data-ttu-id="6af1e-165">Ingest live content using various live streaming protocols (for example RTMP or Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="6af1e-165">Ingest live content using various live streaming protocols (for example RTMP or Smooth Streaming).</span></span>
2. <span data-ttu-id="6af1e-166">(optionally) Encode your stream into adaptive bitrate stream.</span><span class="sxs-lookup"><span data-stu-id="6af1e-166">(optionally) Encode your stream into adaptive bitrate stream.</span></span>
3. <span data-ttu-id="6af1e-167">Preview your live stream.</span><span class="sxs-lookup"><span data-stu-id="6af1e-167">Preview your live stream.</span></span>
4. <span data-ttu-id="6af1e-168">Deliver the content through common streaming protocols (for example, MPEG DASH, Smooth, HLS) directly to your customers, or to a Content Delivery Network (CDN) for further distribution.</span><span class="sxs-lookup"><span data-stu-id="6af1e-168">Deliver the content through common streaming protocols (for example, MPEG DASH, Smooth, HLS) directly to your customers, or to a Content Delivery Network (CDN) for further distribution.</span></span>

    <span data-ttu-id="6af1e-169">-or-</span><span class="sxs-lookup"><span data-stu-id="6af1e-169">-or-</span></span>

    <span data-ttu-id="6af1e-170">Record and store the ingested content in order to be streamed later (Video-on-Demand).</span><span class="sxs-lookup"><span data-stu-id="6af1e-170">Record and store the ingested content in order to be streamed later (Video-on-Demand).</span></span>

<span data-ttu-id="6af1e-171">When doing live streaming, you can choose one of the following routes:</span><span class="sxs-lookup"><span data-stu-id="6af1e-171">When doing live streaming, you can choose one of the following routes:</span></span>

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a><span data-ttu-id="6af1e-172">Working with channels that receive multi-bitrate live stream from on-premises encoders (pass-through)</span><span class="sxs-lookup"><span data-stu-id="6af1e-172">Working with channels that receive multi-bitrate live stream from on-premises encoders (pass-through)</span></span>

<span data-ttu-id="6af1e-173">The following diagram shows the major parts of the AMS platform that are involved in the **pass-through** workflow.</span><span class="sxs-lookup"><span data-stu-id="6af1e-173">The following diagram shows the major parts of the AMS platform that are involved in the **pass-through** workflow.</span></span>

![Live workflow](./media/scenarios-and-availability/media-services-live-streaming-current.png)

<span data-ttu-id="6af1e-175">For more information, see [Working with Channels that Receive Multi-bitrate Live Stream from On-premises Encoders](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-175">For more information, see [Working with Channels that Receive Multi-bitrate Live Stream from On-premises Encoders](media-services-live-streaming-with-onprem-encoders.md).</span></span>

### <a name="working-with-channels-that-are-enabled-to-perform-live-encoding-with-azure-media-services"></a><span data-ttu-id="6af1e-176">Working with channels that are enabled to perform live encoding with Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="6af1e-176">Working with channels that are enabled to perform live encoding with Azure Media Services</span></span>

<span data-ttu-id="6af1e-177">The following diagram shows the major parts of the AMS platform that are involved in Live Streaming workflow where a Channel is enabled to perform live encoding with Media Services.</span><span class="sxs-lookup"><span data-stu-id="6af1e-177">The following diagram shows the major parts of the AMS platform that are involved in Live Streaming workflow where a Channel is enabled to perform live encoding with Media Services.</span></span>

![Live workflow](./media/scenarios-and-availability/media-services-live-streaming-new.png)

<span data-ttu-id="6af1e-179">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-179">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="6af1e-180">For information about availability in datacenters, see the [Availability](#availability) section.</span><span class="sxs-lookup"><span data-stu-id="6af1e-180">For information about availability in datacenters, see the [Availability](#availability) section.</span></span>

## <a name="consuming-content"></a><span data-ttu-id="6af1e-181">Consuming content</span><span class="sxs-lookup"><span data-stu-id="6af1e-181">Consuming content</span></span>

<span data-ttu-id="6af1e-182">Azure Media Services provides the tools you need to create rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span><span class="sxs-lookup"><span data-stu-id="6af1e-182">Azure Media Services provides the tools you need to create rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="6af1e-183">The following topic provides links to SDKs and Player Frameworks that you can use to develop your own client applications that can consume streaming media from Media Services.</span><span class="sxs-lookup"><span data-stu-id="6af1e-183">The following topic provides links to SDKs and Player Frameworks that you can use to develop your own client applications that can consume streaming media from Media Services.</span></span> <span data-ttu-id="6af1e-184">For more information, see [Developing video payer applications](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="6af1e-184">For more information, see [Developing video payer applications](media-services-develop-video-players.md)</span></span>

## <a name="enabling-azure-cdn"></a><span data-ttu-id="6af1e-185">Enabling Azure CDN</span><span class="sxs-lookup"><span data-stu-id="6af1e-185">Enabling Azure CDN</span></span>

<span data-ttu-id="6af1e-186">Media Services supports integration with Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="6af1e-186">Media Services supports integration with Azure CDN.</span></span> <span data-ttu-id="6af1e-187">For information on how to enable Azure CDN, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-187">For information on how to enable Azure CDN, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>

## <a id="scaling"></a><span data-ttu-id="6af1e-188">Scaling a Media Services account</span><span class="sxs-lookup"><span data-stu-id="6af1e-188">Scaling a Media Services account</span></span>

<span data-ttu-id="6af1e-189">AMS customers can scale streaming endpoints, media processing, and storage in their AMS accounts.</span><span class="sxs-lookup"><span data-stu-id="6af1e-189">AMS customers can scale streaming endpoints, media processing, and storage in their AMS accounts.</span></span>

* <span data-ttu-id="6af1e-190">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="6af1e-190">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="6af1e-191">A **Standard** streaming endpoint is suitable for most streaming workloads.</span><span class="sxs-lookup"><span data-stu-id="6af1e-191">A **Standard** streaming endpoint is suitable for most streaming workloads.</span></span> <span data-ttu-id="6af1e-192">It includes the same features as a **Premium** streaming endpoints and scales outbound bandwidth automatically.</span><span class="sxs-lookup"><span data-stu-id="6af1e-192">It includes the same features as a **Premium** streaming endpoints and scales outbound bandwidth automatically.</span></span> 

    <span data-ttu-id="6af1e-193">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span><span class="sxs-lookup"><span data-stu-id="6af1e-193">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="6af1e-194">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span><span class="sxs-lookup"><span data-stu-id="6af1e-194">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="6af1e-195">The streaming endpoint can be scaled by adding SUs.</span><span class="sxs-lookup"><span data-stu-id="6af1e-195">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="6af1e-196">Each SU provides additional bandwidth capacity to the application.</span><span class="sxs-lookup"><span data-stu-id="6af1e-196">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="6af1e-197">For more information about scaling **Premium** streaming endpoints, see the [Scaling streaming endpoints](media-services-portal-scale-streaming-endpoints.md) topic.</span><span class="sxs-lookup"><span data-stu-id="6af1e-197">For more information about scaling **Premium** streaming endpoints, see the [Scaling streaming endpoints](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

* <span data-ttu-id="6af1e-198">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span><span class="sxs-lookup"><span data-stu-id="6af1e-198">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="6af1e-199">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span><span class="sxs-lookup"><span data-stu-id="6af1e-199">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="6af1e-200">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span><span class="sxs-lookup"><span data-stu-id="6af1e-200">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

    <span data-ttu-id="6af1e-201">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span><span class="sxs-lookup"><span data-stu-id="6af1e-201">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="6af1e-202">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span><span class="sxs-lookup"><span data-stu-id="6af1e-202">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6af1e-203">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="6af1e-203">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="6af1e-204">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span><span class="sxs-lookup"><span data-stu-id="6af1e-204">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

    <span data-ttu-id="6af1e-205">For more information see, [Scale media processing](media-services-portal-scale-media-processing.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-205">For more information see, [Scale media processing](media-services-portal-scale-media-processing.md).</span></span>
* <span data-ttu-id="6af1e-206">You can also scale your Media Services account by adding storage accounts to it.</span><span class="sxs-lookup"><span data-stu-id="6af1e-206">You can also scale your Media Services account by adding storage accounts to it.</span></span> <span data-ttu-id="6af1e-207">Each storage account is limited to 500 TB.</span><span class="sxs-lookup"><span data-stu-id="6af1e-207">Each storage account is limited to 500 TB.</span></span> <span data-ttu-id="6af1e-208">To expand your storage beyond the default limitations, you can choose to attach multiple storage accounts to a single Media Services account.</span><span class="sxs-lookup"><span data-stu-id="6af1e-208">To expand your storage beyond the default limitations, you can choose to attach multiple storage accounts to a single Media Services account.</span></span> <span data-ttu-id="6af1e-209">For more information, see [Manage storage accounts](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-209">For more information, see [Manage storage accounts](meda-services-managing-multiple-storage-accounts.md).</span></span>

##<a id="availability"></a> <span data-ttu-id="6af1e-210">Availability of Media Services features across datacenters</span><span class="sxs-lookup"><span data-stu-id="6af1e-210">Availability of Media Services features across datacenters</span></span>

<span data-ttu-id="6af1e-211">This section provides details about availability of Media Services features across datacenters.</span><span class="sxs-lookup"><span data-stu-id="6af1e-211">This section provides details about availability of Media Services features across datacenters.</span></span>

### <a name="ams-accounts"></a><span data-ttu-id="6af1e-212">AMS accounts</span><span class="sxs-lookup"><span data-stu-id="6af1e-212">AMS accounts</span></span>

#### <a name="availability"></a><span data-ttu-id="6af1e-213">Availability</span><span class="sxs-lookup"><span data-stu-id="6af1e-213">Availability</span></span>

<span data-ttu-id="6af1e-214">To determine if Media Services is available in a datacenter, browse to https://azure.microsoft.com/status/ and scroll to the MEDIA table.</span><span class="sxs-lookup"><span data-stu-id="6af1e-214">To determine if Media Services is available in a datacenter, browse to https://azure.microsoft.com/status/ and scroll to the MEDIA table.</span></span>

### <a name="streaming-endpoints"></a><span data-ttu-id="6af1e-215">Streaming endpoints</span><span class="sxs-lookup"><span data-stu-id="6af1e-215">Streaming endpoints</span></span> 

<span data-ttu-id="6af1e-216">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="6af1e-216">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="6af1e-217">For more information, see the [scaling](#scaling) section.</span><span class="sxs-lookup"><span data-stu-id="6af1e-217">For more information, see the [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="6af1e-218">Availability</span><span class="sxs-lookup"><span data-stu-id="6af1e-218">Availability</span></span>

|<span data-ttu-id="6af1e-219">Name</span><span class="sxs-lookup"><span data-stu-id="6af1e-219">Name</span></span>|<span data-ttu-id="6af1e-220">Status</span><span class="sxs-lookup"><span data-stu-id="6af1e-220">Status</span></span>|<span data-ttu-id="6af1e-221">Datacenters</span><span class="sxs-lookup"><span data-stu-id="6af1e-221">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="6af1e-222">Standard</span><span class="sxs-lookup"><span data-stu-id="6af1e-222">Standard</span></span>|<span data-ttu-id="6af1e-223">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-223">GA</span></span>|<span data-ttu-id="6af1e-224">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-224">All</span></span>|
|<span data-ttu-id="6af1e-225">Premium</span><span class="sxs-lookup"><span data-stu-id="6af1e-225">Premium</span></span>|<span data-ttu-id="6af1e-226">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-226">GA</span></span>|<span data-ttu-id="6af1e-227">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-227">All</span></span>|

### <a name="live-encoding"></a><span data-ttu-id="6af1e-228">Live encoding</span><span class="sxs-lookup"><span data-stu-id="6af1e-228">Live encoding</span></span>

#### <a name="availability"></a><span data-ttu-id="6af1e-229">Availability</span><span class="sxs-lookup"><span data-stu-id="6af1e-229">Availability</span></span>

<span data-ttu-id="6af1e-230">Available in all datacenters except: Germany, Brazil South, India West, India South, and India Central.</span><span class="sxs-lookup"><span data-stu-id="6af1e-230">Available in all datacenters except: Germany, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="encoding-media-processors"></a><span data-ttu-id="6af1e-231">Encoding media processors</span><span class="sxs-lookup"><span data-stu-id="6af1e-231">Encoding media processors</span></span>

<span data-ttu-id="6af1e-232">AMS offers two on-demand encoders **Media Encoder Standard** and **Media Encoder Premium Workflow**.</span><span class="sxs-lookup"><span data-stu-id="6af1e-232">AMS offers two on-demand encoders **Media Encoder Standard** and **Media Encoder Premium Workflow**.</span></span> <span data-ttu-id="6af1e-233">For more information, see [Overview and comparison of Azure on-demand media encoders](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-233">For more information, see [Overview and comparison of Azure on-demand media encoders](media-services-encode-asset.md).</span></span> 

#### <a name="availability"></a><span data-ttu-id="6af1e-234">Availability</span><span class="sxs-lookup"><span data-stu-id="6af1e-234">Availability</span></span>

|<span data-ttu-id="6af1e-235">Media processor name</span><span class="sxs-lookup"><span data-stu-id="6af1e-235">Media processor name</span></span>|<span data-ttu-id="6af1e-236">Status</span><span class="sxs-lookup"><span data-stu-id="6af1e-236">Status</span></span>|<span data-ttu-id="6af1e-237">Datacenters</span><span class="sxs-lookup"><span data-stu-id="6af1e-237">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="6af1e-238">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="6af1e-238">Media Encoder Standard</span></span>|<span data-ttu-id="6af1e-239">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-239">GA</span></span>|<span data-ttu-id="6af1e-240">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-240">All</span></span>|
|<span data-ttu-id="6af1e-241">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="6af1e-241">Media Encoder Premium Workflow</span></span>|<span data-ttu-id="6af1e-242">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-242">GA</span></span>|<span data-ttu-id="6af1e-243">All except China</span><span class="sxs-lookup"><span data-stu-id="6af1e-243">All except China</span></span>|

### <a name="analytics-media-processors"></a><span data-ttu-id="6af1e-244">Analytics media processors</span><span class="sxs-lookup"><span data-stu-id="6af1e-244">Analytics media processors</span></span>

<span data-ttu-id="6af1e-245">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span><span class="sxs-lookup"><span data-stu-id="6af1e-245">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="6af1e-246">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-246">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="6af1e-247">Availability</span><span class="sxs-lookup"><span data-stu-id="6af1e-247">Availability</span></span>

|<span data-ttu-id="6af1e-248">Media processor name</span><span class="sxs-lookup"><span data-stu-id="6af1e-248">Media processor name</span></span>|<span data-ttu-id="6af1e-249">Status</span><span class="sxs-lookup"><span data-stu-id="6af1e-249">Status</span></span>|<span data-ttu-id="6af1e-250">Datacenters</span><span class="sxs-lookup"><span data-stu-id="6af1e-250">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="6af1e-251">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="6af1e-251">Azure Media Face Detector</span></span>|<span data-ttu-id="6af1e-252">Preview</span><span class="sxs-lookup"><span data-stu-id="6af1e-252">Preview</span></span>|<span data-ttu-id="6af1e-253">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-253">All</span></span>|
|<span data-ttu-id="6af1e-254">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="6af1e-254">Azure Media Hyperlapse</span></span>|<span data-ttu-id="6af1e-255">Preview</span><span class="sxs-lookup"><span data-stu-id="6af1e-255">Preview</span></span>|<span data-ttu-id="6af1e-256">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-256">All</span></span>|
|<span data-ttu-id="6af1e-257">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="6af1e-257">Azure Media Indexer</span></span>|<span data-ttu-id="6af1e-258">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-258">GA</span></span>|<span data-ttu-id="6af1e-259">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-259">All</span></span>|
|<span data-ttu-id="6af1e-260">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="6af1e-260">Azure Media Motion Detector</span></span>|<span data-ttu-id="6af1e-261">Preview</span><span class="sxs-lookup"><span data-stu-id="6af1e-261">Preview</span></span>|<span data-ttu-id="6af1e-262">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-262">All</span></span>|
|<span data-ttu-id="6af1e-263">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="6af1e-263">Azure Media OCR</span></span>|<span data-ttu-id="6af1e-264">Preview</span><span class="sxs-lookup"><span data-stu-id="6af1e-264">Preview</span></span>|<span data-ttu-id="6af1e-265">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-265">All</span></span>|
|<span data-ttu-id="6af1e-266">Azure Media Redactor</span><span class="sxs-lookup"><span data-stu-id="6af1e-266">Azure Media Redactor</span></span>|<span data-ttu-id="6af1e-267">Preview</span><span class="sxs-lookup"><span data-stu-id="6af1e-267">Preview</span></span>|<span data-ttu-id="6af1e-268">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-268">All</span></span>|
|<span data-ttu-id="6af1e-269">Azure Media Stabilizer</span><span class="sxs-lookup"><span data-stu-id="6af1e-269">Azure Media Stabilizer</span></span>|<span data-ttu-id="6af1e-270">Preview</span><span class="sxs-lookup"><span data-stu-id="6af1e-270">Preview</span></span>|<span data-ttu-id="6af1e-271">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-271">All</span></span>|
|<span data-ttu-id="6af1e-272">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="6af1e-272">Azure Media Video Thumbnails</span></span>|<span data-ttu-id="6af1e-273">Preview</span><span class="sxs-lookup"><span data-stu-id="6af1e-273">Preview</span></span>|<span data-ttu-id="6af1e-274">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-274">All</span></span>|
|<span data-ttu-id="6af1e-275">Azure Media Indexer 2</span><span class="sxs-lookup"><span data-stu-id="6af1e-275">Azure Media Indexer 2</span></span>|<span data-ttu-id="6af1e-276">Preview</span><span class="sxs-lookup"><span data-stu-id="6af1e-276">Preview</span></span>|<span data-ttu-id="6af1e-277">All except China and Federal Government region</span><span class="sxs-lookup"><span data-stu-id="6af1e-277">All except China and Federal Government region</span></span>|

### <a name="protection"></a><span data-ttu-id="6af1e-278">Protection</span><span class="sxs-lookup"><span data-stu-id="6af1e-278">Protection</span></span>

<span data-ttu-id="6af1e-279">Microsoft Azure Media Services enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span><span class="sxs-lookup"><span data-stu-id="6af1e-279">Microsoft Azure Media Services enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="6af1e-280">For more information, see [Protecting AMS content](media-services-content-protection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6af1e-280">For more information, see [Protecting AMS content](media-services-content-protection-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="6af1e-281">Availability</span><span class="sxs-lookup"><span data-stu-id="6af1e-281">Availability</span></span>

|<span data-ttu-id="6af1e-282">Encryption</span><span class="sxs-lookup"><span data-stu-id="6af1e-282">Encryption</span></span>|<span data-ttu-id="6af1e-283">Status</span><span class="sxs-lookup"><span data-stu-id="6af1e-283">Status</span></span>|<span data-ttu-id="6af1e-284">Datacenters</span><span class="sxs-lookup"><span data-stu-id="6af1e-284">Datacenters</span></span>|
|---|---|---| 
|<span data-ttu-id="6af1e-285">Storage</span><span class="sxs-lookup"><span data-stu-id="6af1e-285">Storage</span></span>|<span data-ttu-id="6af1e-286">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-286">GA</span></span>|<span data-ttu-id="6af1e-287">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-287">All</span></span>|
|<span data-ttu-id="6af1e-288">AES-128 keys</span><span class="sxs-lookup"><span data-stu-id="6af1e-288">AES-128 keys</span></span>|<span data-ttu-id="6af1e-289">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-289">GA</span></span>|<span data-ttu-id="6af1e-290">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-290">All</span></span>|
|<span data-ttu-id="6af1e-291">Fairplay</span><span class="sxs-lookup"><span data-stu-id="6af1e-291">Fairplay</span></span>|<span data-ttu-id="6af1e-292">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-292">GA</span></span>|<span data-ttu-id="6af1e-293">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-293">All</span></span>|
|<span data-ttu-id="6af1e-294">PlayReady</span><span class="sxs-lookup"><span data-stu-id="6af1e-294">PlayReady</span></span>|<span data-ttu-id="6af1e-295">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-295">GA</span></span>|<span data-ttu-id="6af1e-296">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-296">All</span></span>|
|<span data-ttu-id="6af1e-297">Widevine</span><span class="sxs-lookup"><span data-stu-id="6af1e-297">Widevine</span></span>|<span data-ttu-id="6af1e-298">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-298">GA</span></span>|<span data-ttu-id="6af1e-299">All except Germany, Federal Government and China.</span><span class="sxs-lookup"><span data-stu-id="6af1e-299">All except Germany, Federal Government and China.</span></span>

### <a name="reserved-units-rus"></a><span data-ttu-id="6af1e-300">Reserved units (RUs)</span><span class="sxs-lookup"><span data-stu-id="6af1e-300">Reserved units (RUs)</span></span>

<span data-ttu-id="6af1e-301">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span><span class="sxs-lookup"><span data-stu-id="6af1e-301">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> 

<span data-ttu-id="6af1e-302">For more information, see the [scaling](#scaling) section.</span><span class="sxs-lookup"><span data-stu-id="6af1e-302">For more information, see the [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="6af1e-303">Availability</span><span class="sxs-lookup"><span data-stu-id="6af1e-303">Availability</span></span>

<span data-ttu-id="6af1e-304">Available in all datacenters.</span><span class="sxs-lookup"><span data-stu-id="6af1e-304">Available in all datacenters.</span></span>

### <a name="reserved-unit-ru-type"></a><span data-ttu-id="6af1e-305">Reserved unit (RU) type</span><span class="sxs-lookup"><span data-stu-id="6af1e-305">Reserved unit (RU) type</span></span>

<span data-ttu-id="6af1e-306">A Media Services account is associated with a Reserved unit type, which determines the speed with which your media processing tasks are processed.</span><span class="sxs-lookup"><span data-stu-id="6af1e-306">A Media Services account is associated with a Reserved unit type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="6af1e-307">You can pick between the following reserved unit types: S1, S2, or S3.</span><span class="sxs-lookup"><span data-stu-id="6af1e-307">You can pick between the following reserved unit types: S1, S2, or S3.</span></span>

<span data-ttu-id="6af1e-308">For more information, see the [scaling](#scaling) section.</span><span class="sxs-lookup"><span data-stu-id="6af1e-308">For more information, see the [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="6af1e-309">Availability</span><span class="sxs-lookup"><span data-stu-id="6af1e-309">Availability</span></span>

|<span data-ttu-id="6af1e-310">RU type name</span><span class="sxs-lookup"><span data-stu-id="6af1e-310">RU type name</span></span>|<span data-ttu-id="6af1e-311">Status</span><span class="sxs-lookup"><span data-stu-id="6af1e-311">Status</span></span>|<span data-ttu-id="6af1e-312">Datacenters</span><span class="sxs-lookup"><span data-stu-id="6af1e-312">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="6af1e-313">S1</span><span class="sxs-lookup"><span data-stu-id="6af1e-313">S1</span></span>|<span data-ttu-id="6af1e-314">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-314">GA</span></span>|<span data-ttu-id="6af1e-315">All</span><span class="sxs-lookup"><span data-stu-id="6af1e-315">All</span></span>|
|<span data-ttu-id="6af1e-316">S2</span><span class="sxs-lookup"><span data-stu-id="6af1e-316">S2</span></span>|<span data-ttu-id="6af1e-317">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-317">GA</span></span>|<span data-ttu-id="6af1e-318">All except Brazil South, and India West</span><span class="sxs-lookup"><span data-stu-id="6af1e-318">All except Brazil South, and India West</span></span>|
|<span data-ttu-id="6af1e-319">S3</span><span class="sxs-lookup"><span data-stu-id="6af1e-319">S3</span></span>|<span data-ttu-id="6af1e-320">GA</span><span class="sxs-lookup"><span data-stu-id="6af1e-320">GA</span></span>|<span data-ttu-id="6af1e-321">All except India West</span><span class="sxs-lookup"><span data-stu-id="6af1e-321">All except India West</span></span>|

## <a name="next-steps"></a><span data-ttu-id="6af1e-322">Next steps</span><span class="sxs-lookup"><span data-stu-id="6af1e-322">Next steps</span></span>

<span data-ttu-id="6af1e-323">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="6af1e-323">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6af1e-324">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="6af1e-324">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

