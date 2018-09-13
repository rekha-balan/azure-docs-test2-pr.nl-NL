---
title: Licensing Microsoft® Smooth Streaming Client Porting Kit
description: Learn about how to licensing the Microsoft® Smooth Streaming Client Porting Kit.
services: media-services
documentationcenter: ''
author: xpouyat
manager: erikre
editor: ''
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: xpouyat
ms.openlocfilehash: 859eaa02a26000ef96028d802362f603482b5f0e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660567"
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="104b3-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="104b3-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="104b3-104">Overview</span><span class="sxs-lookup"><span data-stu-id="104b3-104">Overview</span></span>
<span data-ttu-id="104b3-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive streaming content in Smooth Streaming format.</span><span class="sxs-lookup"><span data-stu-id="104b3-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="104b3-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span><span class="sxs-lookup"><span data-stu-id="104b3-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span></span> 

<span data-ttu-id="104b3-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span><span class="sxs-lookup"><span data-stu-id="104b3-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="104b3-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span><span class="sxs-lookup"><span data-stu-id="104b3-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="104b3-110">Description</span><span class="sxs-lookup"><span data-stu-id="104b3-110">Description</span></span>
<span data-ttu-id="104b3-111">SSPK is licensed on terms that offer excellent business value.</span><span class="sxs-lookup"><span data-stu-id="104b3-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="104b3-112">SSPK license provides the industry with:</span><span class="sxs-lookup"><span data-stu-id="104b3-112">SSPK license provides the industry with:</span></span>

* <span data-ttu-id="104b3-113">Smooth Streaming Porting Kit source in C++</span><span class="sxs-lookup"><span data-stu-id="104b3-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="104b3-114">implements Smooth Streaming Client functionality</span><span class="sxs-lookup"><span data-stu-id="104b3-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="104b3-115">adds format parsing, heuristics, buffering logic, etc.</span><span class="sxs-lookup"><span data-stu-id="104b3-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="104b3-116">Player application APIs</span><span class="sxs-lookup"><span data-stu-id="104b3-116">Player application APIs</span></span> 
  * <span data-ttu-id="104b3-117">programming interfaces for interaction with a media player application</span><span class="sxs-lookup"><span data-stu-id="104b3-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="104b3-118">Platform Abstraction Layer (PAL) Interface</span><span class="sxs-lookup"><span data-stu-id="104b3-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="104b3-119">programming interfaces for interaction with the operating system (threads, sockets)</span><span class="sxs-lookup"><span data-stu-id="104b3-119">programming interfaces for interaction with the operating system (threads, sockets)</span></span>
* <span data-ttu-id="104b3-120">Hardware Abstraction Layer (HAL) Interface</span><span class="sxs-lookup"><span data-stu-id="104b3-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="104b3-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span><span class="sxs-lookup"><span data-stu-id="104b3-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="104b3-122">Digital Rights Management (DRM) Interface</span><span class="sxs-lookup"><span data-stu-id="104b3-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="104b3-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span><span class="sxs-lookup"><span data-stu-id="104b3-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="104b3-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span><span class="sxs-lookup"><span data-stu-id="104b3-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="104b3-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="104b3-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="104b3-126">Implementation samples</span><span class="sxs-lookup"><span data-stu-id="104b3-126">Implementation samples</span></span> 
  * <span data-ttu-id="104b3-127">sample PAL implementation for Linux</span><span class="sxs-lookup"><span data-stu-id="104b3-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="104b3-128">sample HAL implementation for GStreamer</span><span class="sxs-lookup"><span data-stu-id="104b3-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="104b3-129">Licensing Options</span><span class="sxs-lookup"><span data-stu-id="104b3-129">Licensing Options</span></span>
<span data-ttu-id="104b3-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span><span class="sxs-lookup"><span data-stu-id="104b3-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span></span>

* <span data-ttu-id="104b3-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span><span class="sxs-lookup"><span data-stu-id="104b3-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="104b3-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span><span class="sxs-lookup"><span data-stu-id="104b3-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="104b3-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span><span class="sxs-lookup"><span data-stu-id="104b3-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="104b3-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span><span class="sxs-lookup"><span data-stu-id="104b3-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="104b3-135">Fee structure</span><span class="sxs-lookup"><span data-stu-id="104b3-135">Fee structure</span></span>
<span data-ttu-id="104b3-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="104b3-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="104b3-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span><span class="sxs-lookup"><span data-stu-id="104b3-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="104b3-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span><span class="sxs-lookup"><span data-stu-id="104b3-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="104b3-139">Fee structure</span><span class="sxs-lookup"><span data-stu-id="104b3-139">Fee structure</span></span>
<span data-ttu-id="104b3-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span><span class="sxs-lookup"><span data-stu-id="104b3-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="104b3-141">$0.10 per device implementation shipped</span><span class="sxs-lookup"><span data-stu-id="104b3-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="104b3-142">The royalty is capped at $50,000 each year</span><span class="sxs-lookup"><span data-stu-id="104b3-142">The royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="104b3-143">No royalty for first 10,000 device implementations each year</span><span class="sxs-lookup"><span data-stu-id="104b3-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="104b3-144">Licensing Procedure and SSPK access</span><span class="sxs-lookup"><span data-stu-id="104b3-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="104b3-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span><span class="sxs-lookup"><span data-stu-id="104b3-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="104b3-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span><span class="sxs-lookup"><span data-stu-id="104b3-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span></span>

<span data-ttu-id="104b3-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="104b3-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="104b3-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span><span class="sxs-lookup"><span data-stu-id="104b3-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="104b3-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="104b3-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="104b3-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="104b3-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="104b3-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="104b3-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="104b3-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="104b3-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-153">Alticast Corporation</span></span>
* <span data-ttu-id="104b3-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="104b3-155">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-155">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="104b3-156">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-156">Cavium, Inc.</span></span>
* <span data-ttu-id="104b3-157">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-157">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="104b3-158">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-158">Enseo, Inc.</span></span>
* <span data-ttu-id="104b3-159">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="104b3-159">Fluendo S.A.</span></span>
* <span data-ttu-id="104b3-160">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-160">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="104b3-161">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="104b3-161">Infomir GMBH</span></span>
* <span data-ttu-id="104b3-162">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-162">Irdeto USA Inc.</span></span>
* <span data-ttu-id="104b3-163">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="104b3-163">iWEDIA S.A.</span></span> 
* <span data-ttu-id="104b3-164">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="104b3-164">Liberty Global Services BV</span></span>
* <span data-ttu-id="104b3-165">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-165">MediaTek Inc.</span></span>
* <span data-ttu-id="104b3-166">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="104b3-166">MStar Co, Ltd</span></span>
* <span data-ttu-id="104b3-167">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-167">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="104b3-168">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-168">OpenTV, Inc.</span></span>
* <span data-ttu-id="104b3-169">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="104b3-169">Saffron Digital Limited</span></span>
* <span data-ttu-id="104b3-170">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="104b3-170">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="104b3-171">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="104b3-171">SoftAtHome</span></span>
* <span data-ttu-id="104b3-172">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-172">Sony Corporation</span></span>
* <span data-ttu-id="104b3-173">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-173">Tatung Technology Inc.</span></span>
* <span data-ttu-id="104b3-174">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-174">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="104b3-175">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="104b3-175">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="104b3-176">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-176">VisualOn, Inc.</span></span>
* <span data-ttu-id="104b3-177">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-177">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="104b3-178">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span><span class="sxs-lookup"><span data-stu-id="104b3-178">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="104b3-179">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="104b3-179">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="104b3-180">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="104b3-180">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="104b3-181">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-181">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="104b3-182">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-182">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="104b3-183">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-183">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="104b3-184">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-184">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="104b3-185">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="104b3-185">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="104b3-186">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="104b3-186">VE TİC.</span></span> <span data-ttu-id="104b3-187">A.Ş</span><span class="sxs-lookup"><span data-stu-id="104b3-187">A.Ş</span></span>
* <span data-ttu-id="104b3-188">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="104b3-188">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="104b3-189">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="104b3-189">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="104b3-190">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-190">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="104b3-191">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-191">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="104b3-192">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-192">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="104b3-193">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-193">Enseo, Inc.</span></span>
* <span data-ttu-id="104b3-194">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="104b3-194">Filmflex Movies Limited</span></span>
* <span data-ttu-id="104b3-195">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="104b3-195">Fluendo S.A.</span></span>
* <span data-ttu-id="104b3-196">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="104b3-196">Gibson Innovations Limited</span></span>
* <span data-ttu-id="104b3-197">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="104b3-197">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="104b3-198">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-198">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="104b3-199">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="104b3-199">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="104b3-200">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-200">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="104b3-201">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="104b3-201">Infomir GMBH</span></span>
* <span data-ttu-id="104b3-202">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-202">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="104b3-203">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-203">KDDI Corporation</span></span>
* <span data-ttu-id="104b3-204">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-204">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="104b3-205">Orange SA</span><span class="sxs-lookup"><span data-stu-id="104b3-205">Orange SA</span></span>
* <span data-ttu-id="104b3-206">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="104b3-206">Saffron Digital Limited</span></span>
* <span data-ttu-id="104b3-207">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="104b3-207">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="104b3-208">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="104b3-208">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="104b3-209">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="104b3-209">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="104b3-210">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="104b3-210">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="104b3-211">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-211">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="104b3-212">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="104b3-212">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="104b3-213">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="104b3-213">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="104b3-214">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="104b3-214">SmarDTV S.A.</span></span>
* <span data-ttu-id="104b3-215">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="104b3-215">SoftAtHome</span></span>
* <span data-ttu-id="104b3-216">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-216">Sony Corporation</span></span>
* <span data-ttu-id="104b3-217">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="104b3-217">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="104b3-218">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="104b3-218">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="104b3-219">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="104b3-219">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="104b3-220">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-220">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="104b3-221">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="104b3-221">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="104b3-222">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="104b3-222">VIZIO, Inc.</span></span>
* <span data-ttu-id="104b3-223">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-223">Wistron Corporation</span></span>
* <span data-ttu-id="104b3-224">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="104b3-224">ZTE Corporation</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="104b3-225">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="104b3-225">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="104b3-226">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="104b3-226">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


