---
title: Optimize Azure CDN for the type of content delivery
description: Optimize Azure CDN for the type of content delivery
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2018
ms.author: v-deasim
ms.openlocfilehash: be41678b56fdb57c29d65b6b2a17eccd55e85c74
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966016"
---
# <a name="optimize-azure-cdn-for-the-type-of-content-delivery"></a><span data-ttu-id="9c531-103">Optimize Azure CDN for the type of content delivery</span><span class="sxs-lookup"><span data-stu-id="9c531-103">Optimize Azure CDN for the type of content delivery</span></span>

<span data-ttu-id="9c531-104">When you deliver content to a large global audience, it's critical to ensure the optimized delivery of your content.</span><span class="sxs-lookup"><span data-stu-id="9c531-104">When you deliver content to a large global audience, it's critical to ensure the optimized delivery of your content.</span></span> <span data-ttu-id="9c531-105">[Azure Content Delivery Network (CDN)](cdn-overview.md) can optimize the delivery experience based on the type of content you have.</span><span class="sxs-lookup"><span data-stu-id="9c531-105">[Azure Content Delivery Network (CDN)](cdn-overview.md) can optimize the delivery experience based on the type of content you have.</span></span> <span data-ttu-id="9c531-106">The content can be a website, a live stream, a video, or a large file for download.</span><span class="sxs-lookup"><span data-stu-id="9c531-106">The content can be a website, a live stream, a video, or a large file for download.</span></span> <span data-ttu-id="9c531-107">When you create a CDN endpoint, you specify a scenario in the **Optimized for** option.</span><span class="sxs-lookup"><span data-stu-id="9c531-107">When you create a CDN endpoint, you specify a scenario in the **Optimized for** option.</span></span> <span data-ttu-id="9c531-108">Your choice determines which optimization is applied to the content delivered from the CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="9c531-108">Your choice determines which optimization is applied to the content delivered from the CDN endpoint.</span></span>

<span data-ttu-id="9c531-109">Optimization choices are designed to use best-practice behaviors to improve content delivery performance and better origin offload.</span><span class="sxs-lookup"><span data-stu-id="9c531-109">Optimization choices are designed to use best-practice behaviors to improve content delivery performance and better origin offload.</span></span> <span data-ttu-id="9c531-110">Your scenario choices affect performance by modifying configurations for partial caching, object chunking, and the origin failure retry policy.</span><span class="sxs-lookup"><span data-stu-id="9c531-110">Your scenario choices affect performance by modifying configurations for partial caching, object chunking, and the origin failure retry policy.</span></span> 

<span data-ttu-id="9c531-111">This article provides an overview of various optimization features and when you should use them.</span><span class="sxs-lookup"><span data-stu-id="9c531-111">This article provides an overview of various optimization features and when you should use them.</span></span> <span data-ttu-id="9c531-112">For more information on features and limitations, see the respective articles on each individual optimization type.</span><span class="sxs-lookup"><span data-stu-id="9c531-112">For more information on features and limitations, see the respective articles on each individual optimization type.</span></span>

> [!NOTE]
> <span data-ttu-id="9c531-113">When you create a CDN endpoint, the **Optimized for** options can vary based on the type of profile the endpoint is created in.</span><span class="sxs-lookup"><span data-stu-id="9c531-113">When you create a CDN endpoint, the **Optimized for** options can vary based on the type of profile the endpoint is created in.</span></span> <span data-ttu-id="9c531-114">Azure CDN providers apply enhancement in different ways, depending on the scenario.</span><span class="sxs-lookup"><span data-stu-id="9c531-114">Azure CDN providers apply enhancement in different ways, depending on the scenario.</span></span> 

## <a name="provider-options"></a><span data-ttu-id="9c531-115">Provider options</span><span class="sxs-lookup"><span data-stu-id="9c531-115">Provider options</span></span>

<span data-ttu-id="9c531-116">**Azure CDN Standard from Microsoft** profiles supports the following optimizations:</span><span class="sxs-lookup"><span data-stu-id="9c531-116">**Azure CDN Standard from Microsoft** profiles supports the following optimizations:</span></span>

* <span data-ttu-id="9c531-117">[General web delivery](#general-web-delivery).</span><span class="sxs-lookup"><span data-stu-id="9c531-117">[General web delivery](#general-web-delivery).</span></span> <span data-ttu-id="9c531-118">This optimization is also used for media streaming and large file download.</span><span class="sxs-lookup"><span data-stu-id="9c531-118">This optimization is also used for media streaming and large file download.</span></span>


<span data-ttu-id="9c531-119">**Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles support the following optimizations:</span><span class="sxs-lookup"><span data-stu-id="9c531-119">**Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles support the following optimizations:</span></span>

* <span data-ttu-id="9c531-120">[General web delivery](#general-web-delivery).</span><span class="sxs-lookup"><span data-stu-id="9c531-120">[General web delivery](#general-web-delivery).</span></span> <span data-ttu-id="9c531-121">This optimization is also used for media streaming and large file download.</span><span class="sxs-lookup"><span data-stu-id="9c531-121">This optimization is also used for media streaming and large file download.</span></span>

* [<span data-ttu-id="9c531-122">Dynamic site acceleration</span><span class="sxs-lookup"><span data-stu-id="9c531-122">Dynamic site acceleration</span></span>](#dynamic-site-acceleration) 


<span data-ttu-id="9c531-123">**Azure CDN Standard from Akamai** profiles support the following optimizations:</span><span class="sxs-lookup"><span data-stu-id="9c531-123">**Azure CDN Standard from Akamai** profiles support the following optimizations:</span></span>

* [<span data-ttu-id="9c531-124">General web delivery</span><span class="sxs-lookup"><span data-stu-id="9c531-124">General web delivery</span></span>](#general-web-delivery) 

* [<span data-ttu-id="9c531-125">General media streaming</span><span class="sxs-lookup"><span data-stu-id="9c531-125">General media streaming</span></span>](#general-media-streaming)

* [<span data-ttu-id="9c531-126">Video-on-demand media streaming</span><span class="sxs-lookup"><span data-stu-id="9c531-126">Video-on-demand media streaming</span></span>](#video-on-demand-media-streaming)

* [<span data-ttu-id="9c531-127">Large file download</span><span class="sxs-lookup"><span data-stu-id="9c531-127">Large file download</span></span>](#large-file-download)

* [<span data-ttu-id="9c531-128">Dynamic site acceleration</span><span class="sxs-lookup"><span data-stu-id="9c531-128">Dynamic site acceleration</span></span>](#dynamic-site-acceleration) 

<span data-ttu-id="9c531-129">Microsoft recommends that you test performance variations between different providers to select the optimal provider for your delivery.</span><span class="sxs-lookup"><span data-stu-id="9c531-129">Microsoft recommends that you test performance variations between different providers to select the optimal provider for your delivery.</span></span>

## <a name="select-and-configure-optimization-types"></a><span data-ttu-id="9c531-130">Select and configure optimization types</span><span class="sxs-lookup"><span data-stu-id="9c531-130">Select and configure optimization types</span></span>

<span data-ttu-id="9c531-131">When you create a CDN endpoint, select an optimization type that best matches the scenario and type of content that you want the endpoint to deliver.</span><span class="sxs-lookup"><span data-stu-id="9c531-131">When you create a CDN endpoint, select an optimization type that best matches the scenario and type of content that you want the endpoint to deliver.</span></span> <span data-ttu-id="9c531-132">**General web delivery** is the default selection.</span><span class="sxs-lookup"><span data-stu-id="9c531-132">**General web delivery** is the default selection.</span></span> <span data-ttu-id="9c531-133">For existing **Azure CDN Standard from Akamai** endpoints only, you can update the optimization option at any time.</span><span class="sxs-lookup"><span data-stu-id="9c531-133">For existing **Azure CDN Standard from Akamai** endpoints only, you can update the optimization option at any time.</span></span> <span data-ttu-id="9c531-134">This change doesn't interrupt delivery from Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="9c531-134">This change doesn't interrupt delivery from Azure CDN.</span></span> 

1. <span data-ttu-id="9c531-135">In an **Azure CDN Standard from Akamai** profile, select an endpoint.</span><span class="sxs-lookup"><span data-stu-id="9c531-135">In an **Azure CDN Standard from Akamai** profile, select an endpoint.</span></span>

    ![<span data-ttu-id="9c531-136">Endpoint selection</span><span class="sxs-lookup"><span data-stu-id="9c531-136">Endpoint selection</span></span> ](./media/cdn-optimization-overview/01_Akamai.png)

2. <span data-ttu-id="9c531-137">Under SETTINGS, select **Optimization**.</span><span class="sxs-lookup"><span data-stu-id="9c531-137">Under SETTINGS, select **Optimization**.</span></span> <span data-ttu-id="9c531-138">Then, select a type from the **Optimized for** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="9c531-138">Then, select a type from the **Optimized for** drop-down list.</span></span>

    ![Optimization and type selection](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a><span data-ttu-id="9c531-140">Optimization for specific scenarios</span><span class="sxs-lookup"><span data-stu-id="9c531-140">Optimization for specific scenarios</span></span>

<span data-ttu-id="9c531-141">You can optimize the CDN endpoint for one of these scenarios.</span><span class="sxs-lookup"><span data-stu-id="9c531-141">You can optimize the CDN endpoint for one of these scenarios.</span></span> 

### <a name="general-web-delivery"></a><span data-ttu-id="9c531-142">General web delivery</span><span class="sxs-lookup"><span data-stu-id="9c531-142">General web delivery</span></span>

<span data-ttu-id="9c531-143">General web delivery is the most common optimization option.</span><span class="sxs-lookup"><span data-stu-id="9c531-143">General web delivery is the most common optimization option.</span></span> <span data-ttu-id="9c531-144">It's designed for general web content optimization, such as webpages and web applications.</span><span class="sxs-lookup"><span data-stu-id="9c531-144">It's designed for general web content optimization, such as webpages and web applications.</span></span> <span data-ttu-id="9c531-145">This optimization also can be used for file and video downloads.</span><span class="sxs-lookup"><span data-stu-id="9c531-145">This optimization also can be used for file and video downloads.</span></span>

<span data-ttu-id="9c531-146">A typical website contains static and dynamic content.</span><span class="sxs-lookup"><span data-stu-id="9c531-146">A typical website contains static and dynamic content.</span></span> <span data-ttu-id="9c531-147">Static content includes images, JavaScript libraries, and style sheets that can be cached and delivered to different users.</span><span class="sxs-lookup"><span data-stu-id="9c531-147">Static content includes images, JavaScript libraries, and style sheets that can be cached and delivered to different users.</span></span> <span data-ttu-id="9c531-148">Dynamic content is personalized for an individual user, such as news items that are tailored to a user profile.</span><span class="sxs-lookup"><span data-stu-id="9c531-148">Dynamic content is personalized for an individual user, such as news items that are tailored to a user profile.</span></span> <span data-ttu-id="9c531-149">Dynamic content, such as shopping cart contents, isn't cached because it's unique to each user.</span><span class="sxs-lookup"><span data-stu-id="9c531-149">Dynamic content, such as shopping cart contents, isn't cached because it's unique to each user.</span></span> <span data-ttu-id="9c531-150">General web delivery can optimize your entire website.</span><span class="sxs-lookup"><span data-stu-id="9c531-150">General web delivery can optimize your entire website.</span></span> 

> [!NOTE]
> <span data-ttu-id="9c531-151">If you are using an **Azure CDN Standard from Akamai** profile, select this optimization type if your average file size is smaller than 10 MB.</span><span class="sxs-lookup"><span data-stu-id="9c531-151">If you are using an **Azure CDN Standard from Akamai** profile, select this optimization type if your average file size is smaller than 10 MB.</span></span> <span data-ttu-id="9c531-152">Othewise, if your average file size is larger than 10 MB, select **Large file download** from the **Optimized for** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="9c531-152">Othewise, if your average file size is larger than 10 MB, select **Large file download** from the **Optimized for** drop-down list.</span></span>

### <a name="general-media-streaming"></a><span data-ttu-id="9c531-153">General media streaming</span><span class="sxs-lookup"><span data-stu-id="9c531-153">General media streaming</span></span>

<span data-ttu-id="9c531-154">If you need to use the endpoint for live streaming and video-on-demand streaming, select the general media streaming optimization type.</span><span class="sxs-lookup"><span data-stu-id="9c531-154">If you need to use the endpoint for live streaming and video-on-demand streaming, select the general media streaming optimization type.</span></span>

<span data-ttu-id="9c531-155">Media streaming is time-sensitive, because packets that arrive late on the client, such as frequent buffering of video content, can cause a degraded viewing experience.</span><span class="sxs-lookup"><span data-stu-id="9c531-155">Media streaming is time-sensitive, because packets that arrive late on the client, such as frequent buffering of video content, can cause a degraded viewing experience.</span></span> <span data-ttu-id="9c531-156">Media streaming optimization reduces the latency of media content delivery and provides a smooth streaming experience for users.</span><span class="sxs-lookup"><span data-stu-id="9c531-156">Media streaming optimization reduces the latency of media content delivery and provides a smooth streaming experience for users.</span></span> 

<span data-ttu-id="9c531-157">This scenario is common for Azure media service customers.</span><span class="sxs-lookup"><span data-stu-id="9c531-157">This scenario is common for Azure media service customers.</span></span> <span data-ttu-id="9c531-158">When you use Azure media services, you get a single streaming endpoint that can be used for both live and on-demand streaming.</span><span class="sxs-lookup"><span data-stu-id="9c531-158">When you use Azure media services, you get a single streaming endpoint that can be used for both live and on-demand streaming.</span></span> <span data-ttu-id="9c531-159">With this scenario, customers don't need to switch to another endpoint when they change from live to on-demand streaming.</span><span class="sxs-lookup"><span data-stu-id="9c531-159">With this scenario, customers don't need to switch to another endpoint when they change from live to on-demand streaming.</span></span> <span data-ttu-id="9c531-160">General media streaming optimization supports this type of scenario.</span><span class="sxs-lookup"><span data-stu-id="9c531-160">General media streaming optimization supports this type of scenario.</span></span>

<span data-ttu-id="9c531-161">For **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Verizon**, and **Azure CDN Premium from Verizon**, use the general web delivery optimization type to deliver general streaming media content.</span><span class="sxs-lookup"><span data-stu-id="9c531-161">For **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Verizon**, and **Azure CDN Premium from Verizon**, use the general web delivery optimization type to deliver general streaming media content.</span></span>

<span data-ttu-id="9c531-162">For more information about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span><span class="sxs-lookup"><span data-stu-id="9c531-162">For more information about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

### <a name="video-on-demand-media-streaming"></a><span data-ttu-id="9c531-163">Video-on-demand media streaming</span><span class="sxs-lookup"><span data-stu-id="9c531-163">Video-on-demand media streaming</span></span>

<span data-ttu-id="9c531-164">Video-on-demand media streaming optimization improves video-on-demand streaming content.</span><span class="sxs-lookup"><span data-stu-id="9c531-164">Video-on-demand media streaming optimization improves video-on-demand streaming content.</span></span> <span data-ttu-id="9c531-165">If you use an endpoint for video-on-demand streaming, use this option.</span><span class="sxs-lookup"><span data-stu-id="9c531-165">If you use an endpoint for video-on-demand streaming, use this option.</span></span>

<span data-ttu-id="9c531-166">For **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Verizon**, and **Azure CDN Premium from Verizon** profiles, use the general web delivery optimization type to deliver video-on-demand streaming media content.</span><span class="sxs-lookup"><span data-stu-id="9c531-166">For **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Verizon**, and **Azure CDN Premium from Verizon** profiles, use the general web delivery optimization type to deliver video-on-demand streaming media content.</span></span>

<span data-ttu-id="9c531-167">For more information about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span><span class="sxs-lookup"><span data-stu-id="9c531-167">For more information about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9c531-168">If the CDN endpoint primarily serves video-on-demand content, use this optimization type.</span><span class="sxs-lookup"><span data-stu-id="9c531-168">If the CDN endpoint primarily serves video-on-demand content, use this optimization type.</span></span> <span data-ttu-id="9c531-169">The major difference between this optimization type and the general media streaming optimization type is the connection retry time-out. The time-out is much shorter to work with live streaming scenarios.</span><span class="sxs-lookup"><span data-stu-id="9c531-169">The major difference between this optimization type and the general media streaming optimization type is the connection retry time-out. The time-out is much shorter to work with live streaming scenarios.</span></span>
>

### <a name="large-file-download"></a><span data-ttu-id="9c531-170">Large file download</span><span class="sxs-lookup"><span data-stu-id="9c531-170">Large file download</span></span>

<span data-ttu-id="9c531-171">For **Azure CDN Standard from Akamai** profiles, large file downloads are optimized for content larger than 10 MB.</span><span class="sxs-lookup"><span data-stu-id="9c531-171">For **Azure CDN Standard from Akamai** profiles, large file downloads are optimized for content larger than 10 MB.</span></span> <span data-ttu-id="9c531-172">If your average file size is smaller than 10 MB, use general web delivery.</span><span class="sxs-lookup"><span data-stu-id="9c531-172">If your average file size is smaller than 10 MB, use general web delivery.</span></span> <span data-ttu-id="9c531-173">If your average files sizes are consistently larger than 10 MB, it might be more efficient to create a separate endpoint for large files.</span><span class="sxs-lookup"><span data-stu-id="9c531-173">If your average files sizes are consistently larger than 10 MB, it might be more efficient to create a separate endpoint for large files.</span></span> <span data-ttu-id="9c531-174">For example, firmware or software updates typically are large files.</span><span class="sxs-lookup"><span data-stu-id="9c531-174">For example, firmware or software updates typically are large files.</span></span> <span data-ttu-id="9c531-175">To deliver files larger than 1.8 GB, the large file download optimization is required.</span><span class="sxs-lookup"><span data-stu-id="9c531-175">To deliver files larger than 1.8 GB, the large file download optimization is required.</span></span>

<span data-ttu-id="9c531-176">For **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Verizon**, and **Azure CDN Premium from Verizon** profiles, use the general web delivery optimization type to deliver large file download content.</span><span class="sxs-lookup"><span data-stu-id="9c531-176">For **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Verizon**, and **Azure CDN Premium from Verizon** profiles, use the general web delivery optimization type to deliver large file download content.</span></span> <span data-ttu-id="9c531-177">There is no limitation on file download size.</span><span class="sxs-lookup"><span data-stu-id="9c531-177">There is no limitation on file download size.</span></span>

<span data-ttu-id="9c531-178">For more information about large file optimization, see [Large file optimization](cdn-large-file-optimization.md).</span><span class="sxs-lookup"><span data-stu-id="9c531-178">For more information about large file optimization, see [Large file optimization](cdn-large-file-optimization.md).</span></span>

### <a name="dynamic-site-acceleration"></a><span data-ttu-id="9c531-179">Dynamic site acceleration</span><span class="sxs-lookup"><span data-stu-id="9c531-179">Dynamic site acceleration</span></span>

 <span data-ttu-id="9c531-180">Dynamic site acceleration (DSA) is available for **Azure CDN Standard from Akamai**, **Azure CDN Standard from Verizon**, and **Azure CDN Premium from Verizon** profiles.</span><span class="sxs-lookup"><span data-stu-id="9c531-180">Dynamic site acceleration (DSA) is available for **Azure CDN Standard from Akamai**, **Azure CDN Standard from Verizon**, and **Azure CDN Premium from Verizon** profiles.</span></span> <span data-ttu-id="9c531-181">This optimization involves an additional fee to use; for more information, see [Content Delivery Network pricing](https://azure.microsoft.com/pricing/details/cdn/).</span><span class="sxs-lookup"><span data-stu-id="9c531-181">This optimization involves an additional fee to use; for more information, see [Content Delivery Network pricing](https://azure.microsoft.com/pricing/details/cdn/).</span></span>

<span data-ttu-id="9c531-182">DSA includes various techniques that benefit the latency and performance of dynamic content.</span><span class="sxs-lookup"><span data-stu-id="9c531-182">DSA includes various techniques that benefit the latency and performance of dynamic content.</span></span> <span data-ttu-id="9c531-183">Techniques include route and network optimization, TCP optimization, and more.</span><span class="sxs-lookup"><span data-stu-id="9c531-183">Techniques include route and network optimization, TCP optimization, and more.</span></span> 

<span data-ttu-id="9c531-184">You can use this optimization to accelerate a web app that includes numerous responses that aren't cacheable.</span><span class="sxs-lookup"><span data-stu-id="9c531-184">You can use this optimization to accelerate a web app that includes numerous responses that aren't cacheable.</span></span> <span data-ttu-id="9c531-185">Examples are search results, checkout transactions, or real-time data.</span><span class="sxs-lookup"><span data-stu-id="9c531-185">Examples are search results, checkout transactions, or real-time data.</span></span> <span data-ttu-id="9c531-186">You can continue to use core Azure CDN caching capabilities for static data.</span><span class="sxs-lookup"><span data-stu-id="9c531-186">You can continue to use core Azure CDN caching capabilities for static data.</span></span> 

<span data-ttu-id="9c531-187">For more information about dynamic site acceleration, see [Dynamic site acceleration](cdn-dynamic-site-acceleration.md).</span><span class="sxs-lookup"><span data-stu-id="9c531-187">For more information about dynamic site acceleration, see [Dynamic site acceleration](cdn-dynamic-site-acceleration.md).</span></span>



