---
title: Improve performance by compressing files in Azure CDN | Microsoft Docs
description: Learn how to improve file transfer speed and increases page load performance by compressing your files in Azure CDN.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 8c49a2250af0648fa67781cb259d4deaa80ee279
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550323"
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="ff5c9-103">Improve performance by compressing files in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="ff5c9-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="ff5c9-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="ff5c9-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="ff5c9-106">There are two ways to enable compression:</span><span class="sxs-lookup"><span data-stu-id="ff5c9-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="ff5c9-107">You can enable compression on your origin server, in which case the CDN will pass through the compressed files and deliver compressed files to clients that request them.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-107">You can enable compression on your origin server, in which case the CDN will pass through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="ff5c9-108">You can enable compression directly on CDN edge servers, in which case the CDN will compress the files and serve it to end users, even if they are not compressed by the origin server.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-108">You can enable compression directly on CDN edge servers, in which case the CDN will compress the files and serve it to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff5c9-109">CDN configuration changes take some time to propagate through the network.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="ff5c9-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="ff5c9-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="ff5c9-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span><span class="sxs-lookup"><span data-stu-id="ff5c9-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="ff5c9-113">Enabling compression</span><span class="sxs-lookup"><span data-stu-id="ff5c9-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="ff5c9-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="ff5c9-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff5c9-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="ff5c9-116">Standard tier</span><span class="sxs-lookup"><span data-stu-id="ff5c9-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="ff5c9-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="ff5c9-118">From the CDN profile blade, click the CDN endpoint you wish to manage.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-118">From the CDN profile blade, click the CDN endpoint you wish to manage.</span></span>
   
    ![CDN profile blade endpoints](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="ff5c9-120">The CDN endpoint blade opens.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-120">The CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="ff5c9-121">Click the **Configure** button.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-121">Click the **Configure** button.</span></span>
   
    ![CDN profile blade manage button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="ff5c9-123">The CDN Configuration blade opens.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-123">The CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="ff5c9-124">Turn on **Compression**.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-124">Turn on **Compression**.</span></span>
   
    ![CDN compression options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="ff5c9-126">Use the default types, or modify the list by removing or adding file types.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ff5c9-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="ff5c9-128">After making your changes, click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="ff5c9-129">Premium tier</span><span class="sxs-lookup"><span data-stu-id="ff5c9-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="ff5c9-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="ff5c9-131">From the CDN profile blade, click the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-131">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN profile blade manage button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="ff5c9-133">The CDN management portal opens.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="ff5c9-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="ff5c9-135">Click on **Compression**.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-135">Click on **Compression**.</span></span>
   
    <span data-ttu-id="ff5c9-136">Compression options are displayed.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-136">Compression options are displayed.</span></span>
   
    ![File compression](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="ff5c9-138">Enable compression by clicking the **Compression Enabled** radio button.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-138">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="ff5c9-139">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-139">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ff5c9-140">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-140">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="ff5c9-141">After making your changes, click the **Update** button.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-141">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="ff5c9-142">Compression rules</span><span class="sxs-lookup"><span data-stu-id="ff5c9-142">Compression rules</span></span>
<span data-ttu-id="ff5c9-143">These tables describe Azure CDN compression behavior for every scenario.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-143">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff5c9-144">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-144">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="ff5c9-145">To be eligible for compression, a file must:</span><span class="sxs-lookup"><span data-stu-id="ff5c9-145">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="ff5c9-146">Be larger than 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-146">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="ff5c9-147">Be smaller than 1 MB.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-147">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="ff5c9-148">For **Azure CDN from Akamai**, all files are eligible for compression.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-148">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="ff5c9-149">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="ff5c9-149">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="ff5c9-150">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip**, **deflate**, or **bzip2** encoding.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-150">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip**, **deflate**, or **bzip2** encoding.</span></span>  <span data-ttu-id="ff5c9-151">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-151">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> <span data-ttu-id="ff5c9-152">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-152">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span>
> 
> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="ff5c9-153">Compression disabled or file is ineligible for compression</span><span class="sxs-lookup"><span data-stu-id="ff5c9-153">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="ff5c9-154">Client requested format (via Accept-Encoding header)</span><span class="sxs-lookup"><span data-stu-id="ff5c9-154">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="ff5c9-155">Cached file format</span><span class="sxs-lookup"><span data-stu-id="ff5c9-155">Cached file format</span></span> | <span data-ttu-id="ff5c9-156">CDN response to the client</span><span class="sxs-lookup"><span data-stu-id="ff5c9-156">CDN response to the client</span></span> | <span data-ttu-id="ff5c9-157">Notes</span><span class="sxs-lookup"><span data-stu-id="ff5c9-157">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ff5c9-158">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-158">Compressed</span></span> |<span data-ttu-id="ff5c9-159">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-159">Compressed</span></span> |<span data-ttu-id="ff5c9-160">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-160">Compressed</span></span> | |
| <span data-ttu-id="ff5c9-161">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-161">Compressed</span></span> |<span data-ttu-id="ff5c9-162">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-162">Uncompressed</span></span> |<span data-ttu-id="ff5c9-163">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-163">Uncompressed</span></span> | |
| <span data-ttu-id="ff5c9-164">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-164">Compressed</span></span> |<span data-ttu-id="ff5c9-165">Not cached</span><span class="sxs-lookup"><span data-stu-id="ff5c9-165">Not cached</span></span> |<span data-ttu-id="ff5c9-166">Compressed or Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-166">Compressed or Uncompressed</span></span> |<span data-ttu-id="ff5c9-167">Depends on origin response</span><span class="sxs-lookup"><span data-stu-id="ff5c9-167">Depends on origin response</span></span> |
| <span data-ttu-id="ff5c9-168">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-168">Uncompressed</span></span> |<span data-ttu-id="ff5c9-169">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-169">Compressed</span></span> |<span data-ttu-id="ff5c9-170">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-170">Uncompressed</span></span> | |
| <span data-ttu-id="ff5c9-171">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-171">Uncompressed</span></span> |<span data-ttu-id="ff5c9-172">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-172">Uncompressed</span></span> |<span data-ttu-id="ff5c9-173">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-173">Uncompressed</span></span> | |
| <span data-ttu-id="ff5c9-174">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-174">Uncompressed</span></span> |<span data-ttu-id="ff5c9-175">Not cached</span><span class="sxs-lookup"><span data-stu-id="ff5c9-175">Not cached</span></span> |<span data-ttu-id="ff5c9-176">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-176">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="ff5c9-177">Compression enabled and file is eligible for compression</span><span class="sxs-lookup"><span data-stu-id="ff5c9-177">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="ff5c9-178">Client requested format (via Accept-Encoding header)</span><span class="sxs-lookup"><span data-stu-id="ff5c9-178">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="ff5c9-179">Cached file format</span><span class="sxs-lookup"><span data-stu-id="ff5c9-179">Cached file format</span></span> | <span data-ttu-id="ff5c9-180">CDN response to the client</span><span class="sxs-lookup"><span data-stu-id="ff5c9-180">CDN response to the client</span></span> | <span data-ttu-id="ff5c9-181">Notes</span><span class="sxs-lookup"><span data-stu-id="ff5c9-181">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ff5c9-182">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-182">Compressed</span></span> |<span data-ttu-id="ff5c9-183">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-183">Compressed</span></span> |<span data-ttu-id="ff5c9-184">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-184">Compressed</span></span> |<span data-ttu-id="ff5c9-185">CDN transcodes between supported formats</span><span class="sxs-lookup"><span data-stu-id="ff5c9-185">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="ff5c9-186">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-186">Compressed</span></span> |<span data-ttu-id="ff5c9-187">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-187">Uncompressed</span></span> |<span data-ttu-id="ff5c9-188">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-188">Compressed</span></span> |<span data-ttu-id="ff5c9-189">CDN performs compression</span><span class="sxs-lookup"><span data-stu-id="ff5c9-189">CDN performs compression</span></span> |
| <span data-ttu-id="ff5c9-190">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-190">Compressed</span></span> |<span data-ttu-id="ff5c9-191">Not cached</span><span class="sxs-lookup"><span data-stu-id="ff5c9-191">Not cached</span></span> |<span data-ttu-id="ff5c9-192">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-192">Compressed</span></span> |<span data-ttu-id="ff5c9-193">CDN performs compression if origin returns uncompressed.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-193">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="ff5c9-194">**Azure CDN from Verizon** will pass the uncompressed file on the first request and then compress and cache the file for subsequent requests.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-194">**Azure CDN from Verizon** will pass the uncompressed file on the first request and then compress and cache the file for subsequent requests.</span></span>  <span data-ttu-id="ff5c9-195">Files with `Cache-Control: no-cache` header will never be compressed.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-195">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="ff5c9-196">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-196">Uncompressed</span></span> |<span data-ttu-id="ff5c9-197">Compressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-197">Compressed</span></span> |<span data-ttu-id="ff5c9-198">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-198">Uncompressed</span></span> |<span data-ttu-id="ff5c9-199">CDN performs decompression</span><span class="sxs-lookup"><span data-stu-id="ff5c9-199">CDN performs decompression</span></span> |
| <span data-ttu-id="ff5c9-200">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-200">Uncompressed</span></span> |<span data-ttu-id="ff5c9-201">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-201">Uncompressed</span></span> |<span data-ttu-id="ff5c9-202">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-202">Uncompressed</span></span> | |
| <span data-ttu-id="ff5c9-203">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-203">Uncompressed</span></span> |<span data-ttu-id="ff5c9-204">Not cached</span><span class="sxs-lookup"><span data-stu-id="ff5c9-204">Not cached</span></span> |<span data-ttu-id="ff5c9-205">Uncompressed</span><span class="sxs-lookup"><span data-stu-id="ff5c9-205">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="ff5c9-206">Media Services CDN Compression</span><span class="sxs-lookup"><span data-stu-id="ff5c9-206">Media Services CDN Compression</span></span>
<span data-ttu-id="ff5c9-207">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-207">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="ff5c9-208">You cannot enable/disable compression for the mentioned types using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ff5c9-208">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="ff5c9-209">See also</span><span class="sxs-lookup"><span data-stu-id="ff5c9-209">See also</span></span>
* [<span data-ttu-id="ff5c9-210">Troubleshooting CDN file compression</span><span class="sxs-lookup"><span data-stu-id="ff5c9-210">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    






