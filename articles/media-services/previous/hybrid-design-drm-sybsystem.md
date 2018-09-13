---
title: Hybrid design of DRM subsystem(s) using Azure Media Services | Microsoft Docs
description: This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.
services: media-services
documentationcenter: ''
author: willzhan
manager: cfowler
editor: ''
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 1584dab96d1cd772bf04620c68dbe1f133304a1c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866349"
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="3c817-103">Hybrid design of DRM subsystem(s)</span><span class="sxs-lookup"><span data-stu-id="3c817-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="3c817-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="3c817-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="3c817-105">Overview</span><span class="sxs-lookup"><span data-stu-id="3c817-105">Overview</span></span>

<span data-ttu-id="3c817-106">Azure Media Services provides support for the following three DRM system:</span><span class="sxs-lookup"><span data-stu-id="3c817-106">Azure Media Services provides support for the following three DRM system:</span></span>

* <span data-ttu-id="3c817-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="3c817-107">PlayReady</span></span>
* <span data-ttu-id="3c817-108">Widevine (Modular)</span><span class="sxs-lookup"><span data-stu-id="3c817-108">Widevine (Modular)</span></span>
* <span data-ttu-id="3c817-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="3c817-109">FairPlay</span></span>

<span data-ttu-id="3c817-110">The DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span><span class="sxs-lookup"><span data-stu-id="3c817-110">The DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="3c817-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see the document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="3c817-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see the document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="3c817-112">Although we offer complete support for three DRM systems, sometimes customers need to use various parts of their own infrastructure/subsystems in addition to Azure Media Services to build a hybrid DRM subsystem.</span><span class="sxs-lookup"><span data-stu-id="3c817-112">Although we offer complete support for three DRM systems, sometimes customers need to use various parts of their own infrastructure/subsystems in addition to Azure Media Services to build a hybrid DRM subsystem.</span></span>

<span data-ttu-id="3c817-113">Below are some common questions asked by customers:</span><span class="sxs-lookup"><span data-stu-id="3c817-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="3c817-114">"Can I use my own DRM license servers?"</span><span class="sxs-lookup"><span data-stu-id="3c817-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="3c817-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span><span class="sxs-lookup"><span data-stu-id="3c817-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="3c817-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span><span class="sxs-lookup"><span data-stu-id="3c817-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-the-ams-drm-platform"></a><span data-ttu-id="3c817-117">Modularity of the AMS DRM platform</span><span class="sxs-lookup"><span data-stu-id="3c817-117">Modularity of the AMS DRM platform</span></span>

<span data-ttu-id="3c817-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span><span class="sxs-lookup"><span data-stu-id="3c817-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="3c817-119">You can use Azure Media Services with any of the following different combinations described in the table below (an explanation of the notation used in the table follows).</span><span class="sxs-lookup"><span data-stu-id="3c817-119">You can use Azure Media Services with any of the following different combinations described in the table below (an explanation of the notation used in the table follows).</span></span> 

|<span data-ttu-id="3c817-120">**Content hosting & origin**</span><span class="sxs-lookup"><span data-stu-id="3c817-120">**Content hosting & origin**</span></span>|<span data-ttu-id="3c817-121">**Content encryption**</span><span class="sxs-lookup"><span data-stu-id="3c817-121">**Content encryption**</span></span>|<span data-ttu-id="3c817-122">**DRM license delivery**</span><span class="sxs-lookup"><span data-stu-id="3c817-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="3c817-123">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-123">AMS</span></span>|<span data-ttu-id="3c817-124">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-124">AMS</span></span>|<span data-ttu-id="3c817-125">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-125">AMS</span></span>|
|<span data-ttu-id="3c817-126">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-126">AMS</span></span>|<span data-ttu-id="3c817-127">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-127">AMS</span></span>|<span data-ttu-id="3c817-128">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-128">Third-party</span></span>|
|<span data-ttu-id="3c817-129">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-129">AMS</span></span>|<span data-ttu-id="3c817-130">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-130">Third-party</span></span>|<span data-ttu-id="3c817-131">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-131">AMS</span></span>|
|<span data-ttu-id="3c817-132">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-132">AMS</span></span>|<span data-ttu-id="3c817-133">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-133">Third-party</span></span>|<span data-ttu-id="3c817-134">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-134">Third-party</span></span>|
|<span data-ttu-id="3c817-135">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-135">Third-party</span></span>|<span data-ttu-id="3c817-136">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-136">Third-party</span></span>|<span data-ttu-id="3c817-137">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="3c817-138">Content hosting & origin</span><span class="sxs-lookup"><span data-stu-id="3c817-138">Content hosting & origin</span></span>

* <span data-ttu-id="3c817-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span><span class="sxs-lookup"><span data-stu-id="3c817-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="3c817-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span><span class="sxs-lookup"><span data-stu-id="3c817-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="3c817-141">Content encryption</span><span class="sxs-lookup"><span data-stu-id="3c817-141">Content encryption</span></span>

* <span data-ttu-id="3c817-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span><span class="sxs-lookup"><span data-stu-id="3c817-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="3c817-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span><span class="sxs-lookup"><span data-stu-id="3c817-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="3c817-144">DRM license delivery</span><span class="sxs-lookup"><span data-stu-id="3c817-144">DRM license delivery</span></span>

* <span data-ttu-id="3c817-145">AMS: DRM license is delivered by AMS license delivery service.</span><span class="sxs-lookup"><span data-stu-id="3c817-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="3c817-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span><span class="sxs-lookup"><span data-stu-id="3c817-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="3c817-147">Configure based on your hybrid scenario</span><span class="sxs-lookup"><span data-stu-id="3c817-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="3c817-148">Content key</span><span class="sxs-lookup"><span data-stu-id="3c817-148">Content key</span></span>

<span data-ttu-id="3c817-149">Through configuration of a content key, you can control the following attributes of both AMS dynamic encryption and AMS license delivery service:</span><span class="sxs-lookup"><span data-stu-id="3c817-149">Through configuration of a content key, you can control the following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="3c817-150">The content key used for dynamic DRM encryption.</span><span class="sxs-lookup"><span data-stu-id="3c817-150">The content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="3c817-151">DRM license content to be delivered by license delivery services: rights, content key and restrictions.</span><span class="sxs-lookup"><span data-stu-id="3c817-151">DRM license content to be delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="3c817-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span><span class="sxs-lookup"><span data-stu-id="3c817-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="3c817-153">If **token** type of **content key authorization policy restriction is used**, the **content key authorization policy restriction** must be met before a license is issued.</span><span class="sxs-lookup"><span data-stu-id="3c817-153">If **token** type of **content key authorization policy restriction is used**, the **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="3c817-154">Asset delivery policy</span><span class="sxs-lookup"><span data-stu-id="3c817-154">Asset delivery policy</span></span>

<span data-ttu-id="3c817-155">Through configuration of an asset delivery policy, you can control the following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span><span class="sxs-lookup"><span data-stu-id="3c817-155">Through configuration of an asset delivery policy, you can control the following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="3c817-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span><span class="sxs-lookup"><span data-stu-id="3c817-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="3c817-157">The default/embedded license delivery URLs for each of the involved DRMs.</span><span class="sxs-lookup"><span data-stu-id="3c817-157">The default/embedded license delivery URLs for each of the involved DRMs.</span></span>
* <span data-ttu-id="3c817-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span><span class="sxs-lookup"><span data-stu-id="3c817-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="3c817-159">Scenarios and samples</span><span class="sxs-lookup"><span data-stu-id="3c817-159">Scenarios and samples</span></span>

<span data-ttu-id="3c817-160">Based on the explanations in the previous section, the following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (the samples mentioned in the last column follow the table):</span><span class="sxs-lookup"><span data-stu-id="3c817-160">Based on the explanations in the previous section, the following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (the samples mentioned in the last column follow the table):</span></span>

|<span data-ttu-id="3c817-161">**Content hosting & origin**</span><span class="sxs-lookup"><span data-stu-id="3c817-161">**Content hosting & origin**</span></span>|<span data-ttu-id="3c817-162">**DRM encryption**</span><span class="sxs-lookup"><span data-stu-id="3c817-162">**DRM encryption**</span></span>|<span data-ttu-id="3c817-163">**DRM license delivery**</span><span class="sxs-lookup"><span data-stu-id="3c817-163">**DRM license delivery**</span></span>|<span data-ttu-id="3c817-164">**Configure content key**</span><span class="sxs-lookup"><span data-stu-id="3c817-164">**Configure content key**</span></span>|<span data-ttu-id="3c817-165">**Configure asset delivery policy**</span><span class="sxs-lookup"><span data-stu-id="3c817-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="3c817-166">**Sample**</span><span class="sxs-lookup"><span data-stu-id="3c817-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="3c817-167">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-167">AMS</span></span>|<span data-ttu-id="3c817-168">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-168">AMS</span></span>|<span data-ttu-id="3c817-169">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-169">AMS</span></span>|<span data-ttu-id="3c817-170">Yes</span><span class="sxs-lookup"><span data-stu-id="3c817-170">Yes</span></span>|<span data-ttu-id="3c817-171">Yes</span><span class="sxs-lookup"><span data-stu-id="3c817-171">Yes</span></span>|<span data-ttu-id="3c817-172">Sample 1</span><span class="sxs-lookup"><span data-stu-id="3c817-172">Sample 1</span></span>|
|<span data-ttu-id="3c817-173">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-173">AMS</span></span>|<span data-ttu-id="3c817-174">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-174">AMS</span></span>|<span data-ttu-id="3c817-175">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-175">Third-party</span></span>|<span data-ttu-id="3c817-176">Yes</span><span class="sxs-lookup"><span data-stu-id="3c817-176">Yes</span></span>|<span data-ttu-id="3c817-177">Yes</span><span class="sxs-lookup"><span data-stu-id="3c817-177">Yes</span></span>|<span data-ttu-id="3c817-178">Sample 2</span><span class="sxs-lookup"><span data-stu-id="3c817-178">Sample 2</span></span>|
|<span data-ttu-id="3c817-179">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-179">AMS</span></span>|<span data-ttu-id="3c817-180">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-180">Third-party</span></span>|<span data-ttu-id="3c817-181">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-181">AMS</span></span>|<span data-ttu-id="3c817-182">Yes</span><span class="sxs-lookup"><span data-stu-id="3c817-182">Yes</span></span>|<span data-ttu-id="3c817-183">No</span><span class="sxs-lookup"><span data-stu-id="3c817-183">No</span></span>|<span data-ttu-id="3c817-184">Sample 3</span><span class="sxs-lookup"><span data-stu-id="3c817-184">Sample 3</span></span>|
|<span data-ttu-id="3c817-185">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-185">AMS</span></span>|<span data-ttu-id="3c817-186">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-186">Third-party</span></span>|<span data-ttu-id="3c817-187">Outside</span><span class="sxs-lookup"><span data-stu-id="3c817-187">Outside</span></span>|<span data-ttu-id="3c817-188">No</span><span class="sxs-lookup"><span data-stu-id="3c817-188">No</span></span>|<span data-ttu-id="3c817-189">No</span><span class="sxs-lookup"><span data-stu-id="3c817-189">No</span></span>|<span data-ttu-id="3c817-190">Sample 4</span><span class="sxs-lookup"><span data-stu-id="3c817-190">Sample 4</span></span>|
|<span data-ttu-id="3c817-191">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-191">Third-party</span></span>|<span data-ttu-id="3c817-192">Third-party</span><span class="sxs-lookup"><span data-stu-id="3c817-192">Third-party</span></span>|<span data-ttu-id="3c817-193">AMS</span><span class="sxs-lookup"><span data-stu-id="3c817-193">AMS</span></span>|<span data-ttu-id="3c817-194">Yes</span><span class="sxs-lookup"><span data-stu-id="3c817-194">Yes</span></span>|<span data-ttu-id="3c817-195">No</span><span class="sxs-lookup"><span data-stu-id="3c817-195">No</span></span>|    

<span data-ttu-id="3c817-196">In the samples, PlayReady protection works for both DASH and smooth streaming.</span><span class="sxs-lookup"><span data-stu-id="3c817-196">In the samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="3c817-197">The video URLs below are smooth streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="3c817-197">The video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="3c817-198">To get the corresponding DASH URLs, just append "(format=mpd-time-csf)".</span><span class="sxs-lookup"><span data-stu-id="3c817-198">To get the corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="3c817-199">You could use the [azure media test player](http://aka.ms/amtest) to test in a browser.</span><span class="sxs-lookup"><span data-stu-id="3c817-199">You could use the [azure media test player](http://aka.ms/amtest) to test in a browser.</span></span> <span data-ttu-id="3c817-200">It allows you to configure which streaming protocol to use, under which tech.</span><span class="sxs-lookup"><span data-stu-id="3c817-200">It allows you to configure which streaming protocol to use, under which tech.</span></span> <span data-ttu-id="3c817-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span><span class="sxs-lookup"><span data-stu-id="3c817-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="3c817-202">For more information, see [details about the test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span><span class="sxs-lookup"><span data-stu-id="3c817-202">For more information, see [details about the test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="3c817-203">Sample 1</span><span class="sxs-lookup"><span data-stu-id="3c817-203">Sample 1</span></span>

* <span data-ttu-id="3c817-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="3c817-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="3c817-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="3c817-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="3c817-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="3c817-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="3c817-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="3c817-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="3c817-208">Sample 2</span><span class="sxs-lookup"><span data-stu-id="3c817-208">Sample 2</span></span>

* <span data-ttu-id="3c817-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="3c817-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="3c817-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="3c817-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="3c817-211">Sample 3</span><span class="sxs-lookup"><span data-stu-id="3c817-211">Sample 3</span></span>

* <span data-ttu-id="3c817-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="3c817-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="3c817-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="3c817-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="3c817-214">Sample 4</span><span class="sxs-lookup"><span data-stu-id="3c817-214">Sample 4</span></span>

* <span data-ttu-id="3c817-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="3c817-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="3c817-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="3c817-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="3c817-217">Summary</span><span class="sxs-lookup"><span data-stu-id="3c817-217">Summary</span></span>

<span data-ttu-id="3c817-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span><span class="sxs-lookup"><span data-stu-id="3c817-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c817-219">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c817-219">Next steps</span></span>
<span data-ttu-id="3c817-220">View Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="3c817-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3c817-221">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="3c817-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

