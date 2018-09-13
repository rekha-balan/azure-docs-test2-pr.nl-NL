---
title: Licensing Microsoft® Smooth Streaming Client Porting Kit
description: Learn about how to licensing the Microsoft® Smooth Streaming Client Porting Kit.
services: media-services
documentationcenter: ''
author: xpouyat
manager: cfowler
editor: ''
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: b4472f522571e0056ce6b28d67a69b0dcabba8a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868299"
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="8c11c-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="8c11c-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="8c11c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="8c11c-104">Overview</span></span>
<span data-ttu-id="8c11c-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive content in Smooth Streaming format.</span><span class="sxs-lookup"><span data-stu-id="8c11c-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive content in Smooth Streaming format.</span></span> <span data-ttu-id="8c11c-106">SSPK is a device and platform-independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span><span class="sxs-lookup"><span data-stu-id="8c11c-106">SSPK is a device and platform-independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span></span> 

<span data-ttu-id="8c11c-107">Included below is a high-level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span><span class="sxs-lookup"><span data-stu-id="8c11c-107">Included below is a high-level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="8c11c-108">This content is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span><span class="sxs-lookup"><span data-stu-id="8c11c-108">This content is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="8c11c-110">Description</span><span class="sxs-lookup"><span data-stu-id="8c11c-110">Description</span></span>
<span data-ttu-id="8c11c-111">SSPK is licensed on terms that offer excellent business value.</span><span class="sxs-lookup"><span data-stu-id="8c11c-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="8c11c-112">SSPK license provides the industry with:</span><span class="sxs-lookup"><span data-stu-id="8c11c-112">SSPK license provides the industry with:</span></span>

* <span data-ttu-id="8c11c-113">Smooth Streaming Porting Kit source in C++</span><span class="sxs-lookup"><span data-stu-id="8c11c-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="8c11c-114">implements Smooth Streaming Client functionality</span><span class="sxs-lookup"><span data-stu-id="8c11c-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="8c11c-115">adds format parsing, heuristics, buffering logic, etc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="8c11c-116">Player application APIs</span><span class="sxs-lookup"><span data-stu-id="8c11c-116">Player application APIs</span></span> 
  * <span data-ttu-id="8c11c-117">programming interfaces for interaction with a media player application</span><span class="sxs-lookup"><span data-stu-id="8c11c-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="8c11c-118">Platform Abstraction Layer (PAL) Interface</span><span class="sxs-lookup"><span data-stu-id="8c11c-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="8c11c-119">programming interfaces for interaction with the operating system (threads, sockets)</span><span class="sxs-lookup"><span data-stu-id="8c11c-119">programming interfaces for interaction with the operating system (threads, sockets)</span></span>
* <span data-ttu-id="8c11c-120">Hardware Abstraction Layer (HAL) Interface</span><span class="sxs-lookup"><span data-stu-id="8c11c-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="8c11c-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span><span class="sxs-lookup"><span data-stu-id="8c11c-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="8c11c-122">Digital Rights Management (DRM) Interface</span><span class="sxs-lookup"><span data-stu-id="8c11c-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="8c11c-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span><span class="sxs-lookup"><span data-stu-id="8c11c-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="8c11c-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span><span class="sxs-lookup"><span data-stu-id="8c11c-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="8c11c-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="8c11c-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="8c11c-126">Implementation samples</span><span class="sxs-lookup"><span data-stu-id="8c11c-126">Implementation samples</span></span> 
  * <span data-ttu-id="8c11c-127">sample PAL implementation for Linux</span><span class="sxs-lookup"><span data-stu-id="8c11c-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="8c11c-128">sample HAL implementation for GStreamer</span><span class="sxs-lookup"><span data-stu-id="8c11c-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="8c11c-129">Licensing Options</span><span class="sxs-lookup"><span data-stu-id="8c11c-129">Licensing Options</span></span>
<span data-ttu-id="8c11c-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span><span class="sxs-lookup"><span data-stu-id="8c11c-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span></span>

* <span data-ttu-id="8c11c-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span><span class="sxs-lookup"><span data-stu-id="8c11c-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="8c11c-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span><span class="sxs-lookup"><span data-stu-id="8c11c-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="8c11c-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span><span class="sxs-lookup"><span data-stu-id="8c11c-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="8c11c-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span><span class="sxs-lookup"><span data-stu-id="8c11c-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="8c11c-135">Fee structure</span><span class="sxs-lookup"><span data-stu-id="8c11c-135">Fee structure</span></span>
<span data-ttu-id="8c11c-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="8c11c-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="8c11c-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span><span class="sxs-lookup"><span data-stu-id="8c11c-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="8c11c-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span><span class="sxs-lookup"><span data-stu-id="8c11c-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="8c11c-139">Fee structure</span><span class="sxs-lookup"><span data-stu-id="8c11c-139">Fee structure</span></span>
<span data-ttu-id="8c11c-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span><span class="sxs-lookup"><span data-stu-id="8c11c-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="8c11c-141">$0.10 per device implementation shipped</span><span class="sxs-lookup"><span data-stu-id="8c11c-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="8c11c-142">The royalty is capped at $50,000 each year</span><span class="sxs-lookup"><span data-stu-id="8c11c-142">The royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="8c11c-143">No royalty for first 10,000 device implementations each year</span><span class="sxs-lookup"><span data-stu-id="8c11c-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="8c11c-144">Licensing Procedure and SSPK access</span><span class="sxs-lookup"><span data-stu-id="8c11c-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="8c11c-145">Email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span><span class="sxs-lookup"><span data-stu-id="8c11c-145">Email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="8c11c-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span><span class="sxs-lookup"><span data-stu-id="8c11c-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span></span>

<span data-ttu-id="8c11c-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8c11c-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="8c11c-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span><span class="sxs-lookup"><span data-stu-id="8c11c-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="8c11c-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="8c11c-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="8c11c-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="8c11c-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="8c11c-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="8c11c-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="8c11c-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="8c11c-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-153">Alticast Corporation</span></span>
* <span data-ttu-id="8c11c-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="8c11c-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="8c11c-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-157">Cavium, Inc.</span></span>
* <span data-ttu-id="8c11c-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="8c11c-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-159">Enseo, Inc.</span></span>
* <span data-ttu-id="8c11c-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="8c11c-160">Fluendo S.A.</span></span>
* <span data-ttu-id="8c11c-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="8c11c-162">Infomir GMBH</span></span>
* <span data-ttu-id="8c11c-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="8c11c-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="8c11c-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="8c11c-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="8c11c-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="8c11c-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-166">MediaTek Inc.</span></span>
* <span data-ttu-id="8c11c-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="8c11c-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="8c11c-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="8c11c-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="8c11c-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="8c11c-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="8c11c-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="8c11c-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="8c11c-172">SoftAtHome</span></span>
* <span data-ttu-id="8c11c-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-173">Sony Corporation</span></span>
* <span data-ttu-id="8c11c-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="8c11c-175">TCL Technology Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-175">TCL Technology Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="8c11c-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="8c11c-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="8c11c-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="8c11c-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="8c11c-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span><span class="sxs-lookup"><span data-stu-id="8c11c-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="8c11c-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="8c11c-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="8c11c-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="8c11c-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="8c11c-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="8c11c-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="8c11c-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="8c11c-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="8c11c-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="8c11c-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="8c11c-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="8c11c-189">VE TİC.</span></span> <span data-ttu-id="8c11c-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="8c11c-190">A.Ş</span></span>
* <span data-ttu-id="8c11c-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="8c11c-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="8c11c-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="8c11c-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="8c11c-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="8c11c-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="8c11c-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="8c11c-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-196">Enseo, Inc.</span></span>
* <span data-ttu-id="8c11c-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="8c11c-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="8c11c-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="8c11c-198">Fluendo S.A.</span></span>
* <span data-ttu-id="8c11c-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="8c11c-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="8c11c-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="8c11c-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="8c11c-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="8c11c-203">Homecast Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="8c11c-203">Homecast Co., Ltd</span></span>
* <span data-ttu-id="8c11c-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="8c11c-205">Infomir GMBH</span></span>
* <span data-ttu-id="8c11c-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-207">KDDI Corporation</span></span>
* <span data-ttu-id="8c11c-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="8c11c-209">Orange SA</span></span>
* <span data-ttu-id="8c11c-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="8c11c-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="8c11c-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="8c11c-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="8c11c-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="8c11c-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="8c11c-213">Shenzhen Jiuzhou Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="8c11c-213">Shenzhen Jiuzhou Electric Co., Ltd</span></span>
* <span data-ttu-id="8c11c-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="8c11c-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="8c11c-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="8c11c-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="8c11c-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="8c11c-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="8c11c-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="8c11c-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="8c11c-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="8c11c-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="8c11c-219">SoftAtHome</span></span>
* <span data-ttu-id="8c11c-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-220">Sony Corporation</span></span>
* <span data-ttu-id="8c11c-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="8c11c-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="8c11c-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="8c11c-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="8c11c-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="8c11c-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="8c11c-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="8c11c-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="8c11c-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="8c11c-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="8c11c-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="8c11c-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="8c11c-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-228">Wistron Corporation</span></span>
* <span data-ttu-id="8c11c-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="8c11c-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="8c11c-230">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="8c11c-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8c11c-231">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="8c11c-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

