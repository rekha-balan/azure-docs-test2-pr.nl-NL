---
title: Troubleshooting file compression in Azure CDN | Microsoft Docs
description: Troubleshoot issues with Azure CDN file compression.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 14d50cb7cac77af75dd4b7293812154d1f24e47c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44790525"
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="6ea60-103">Troubleshooting CDN file compression</span><span class="sxs-lookup"><span data-stu-id="6ea60-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="6ea60-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="6ea60-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="6ea60-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="6ea60-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="6ea60-106">Alternatively, you can also file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="6ea60-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="6ea60-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="6ea60-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="6ea60-108">Symptom</span><span class="sxs-lookup"><span data-stu-id="6ea60-108">Symptom</span></span>
<span data-ttu-id="6ea60-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span><span class="sxs-lookup"><span data-stu-id="6ea60-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="6ea60-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="6ea60-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="6ea60-111">Check the HTTP response headers returned with your cached CDN content.</span><span class="sxs-lookup"><span data-stu-id="6ea60-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="6ea60-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span><span class="sxs-lookup"><span data-stu-id="6ea60-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Content-Encoding header](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="6ea60-114">Cause</span><span class="sxs-lookup"><span data-stu-id="6ea60-114">Cause</span></span>
<span data-ttu-id="6ea60-115">There are several possible causes, including:</span><span class="sxs-lookup"><span data-stu-id="6ea60-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="6ea60-116">The requested content is not eligible for compression.</span><span class="sxs-lookup"><span data-stu-id="6ea60-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="6ea60-117">Compression is not enabled for the requested file type.</span><span class="sxs-lookup"><span data-stu-id="6ea60-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="6ea60-118">The HTTP request did not include a header requesting a valid compression type.</span><span class="sxs-lookup"><span data-stu-id="6ea60-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="6ea60-119">Troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="6ea60-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="6ea60-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span><span class="sxs-lookup"><span data-stu-id="6ea60-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="6ea60-121">Usually, changes are applied within 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="6ea60-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="6ea60-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span><span class="sxs-lookup"><span data-stu-id="6ea60-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="6ea60-123">Verify the request</span><span class="sxs-lookup"><span data-stu-id="6ea60-123">Verify the request</span></span>
<span data-ttu-id="6ea60-124">First, we should do a quick sanity check on the request.</span><span class="sxs-lookup"><span data-stu-id="6ea60-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="6ea60-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span><span class="sxs-lookup"><span data-stu-id="6ea60-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="6ea60-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span><span class="sxs-lookup"><span data-stu-id="6ea60-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="6ea60-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span><span class="sxs-lookup"><span data-stu-id="6ea60-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea60-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span><span class="sxs-lookup"><span data-stu-id="6ea60-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN request headers](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profiles"></a><span data-ttu-id="6ea60-130">Verify compression settings (standard CDN profiles)</span><span class="sxs-lookup"><span data-stu-id="6ea60-130">Verify compression settings (standard CDN profiles)</span></span>
> [!NOTE]
> <span data-ttu-id="6ea60-131">This step applies only if your CDN profile is an **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Verizon**, or **Azure CDN Standard from Akamai** profile.</span><span class="sxs-lookup"><span data-stu-id="6ea60-131">This step applies only if your CDN profile is an **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Verizon**, or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="6ea60-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span><span class="sxs-lookup"><span data-stu-id="6ea60-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="6ea60-133">Verify compression is enabled.</span><span class="sxs-lookup"><span data-stu-id="6ea60-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="6ea60-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span><span class="sxs-lookup"><span data-stu-id="6ea60-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN compression settings](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profiles"></a><span data-ttu-id="6ea60-136">Verify compression settings (Premium CDN profiles)</span><span class="sxs-lookup"><span data-stu-id="6ea60-136">Verify compression settings (Premium CDN profiles)</span></span>
> [!NOTE]
> <span data-ttu-id="6ea60-137">This step applies only if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span><span class="sxs-lookup"><span data-stu-id="6ea60-137">This step applies only if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="6ea60-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="6ea60-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="6ea60-139">The supplemental portal will open.</span><span class="sxs-lookup"><span data-stu-id="6ea60-139">The supplemental portal will open.</span></span>  <span data-ttu-id="6ea60-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span><span class="sxs-lookup"><span data-stu-id="6ea60-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="6ea60-141">Click **Compression**.</span><span class="sxs-lookup"><span data-stu-id="6ea60-141">Click **Compression**.</span></span> 

* <span data-ttu-id="6ea60-142">Verify compression is enabled.</span><span class="sxs-lookup"><span data-stu-id="6ea60-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="6ea60-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span><span class="sxs-lookup"><span data-stu-id="6ea60-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="6ea60-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span><span class="sxs-lookup"><span data-stu-id="6ea60-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN premium compression settings](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached-verizon-cdn-profiles"></a><span data-ttu-id="6ea60-146">Verify the content is cached (Verizon CDN profiles)</span><span class="sxs-lookup"><span data-stu-id="6ea60-146">Verify the content is cached (Verizon CDN profiles)</span></span>
> [!NOTE]
> <span data-ttu-id="6ea60-147">This step applies only if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon** profile.</span><span class="sxs-lookup"><span data-stu-id="6ea60-147">This step applies only if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="6ea60-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span><span class="sxs-lookup"><span data-stu-id="6ea60-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="6ea60-149">Check the **Server** response header.</span><span class="sxs-lookup"><span data-stu-id="6ea60-149">Check the **Server** response header.</span></span>  <span data-ttu-id="6ea60-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span><span class="sxs-lookup"><span data-stu-id="6ea60-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="6ea60-151">Check the **X-Cache** response header.</span><span class="sxs-lookup"><span data-stu-id="6ea60-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="6ea60-152">The header should read **HIT**.</span><span class="sxs-lookup"><span data-stu-id="6ea60-152">The header should read **HIT**.</span></span>  

![CDN response headers](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements-verizon-cdn-profiles"></a><span data-ttu-id="6ea60-154">Verify the file meets the size requirements (Verizon CDN profiles)</span><span class="sxs-lookup"><span data-stu-id="6ea60-154">Verify the file meets the size requirements (Verizon CDN profiles)</span></span>
> [!NOTE]
> <span data-ttu-id="6ea60-155">This step applies only if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon** profile.</span><span class="sxs-lookup"><span data-stu-id="6ea60-155">This step applies only if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="6ea60-156">To be eligible for compression, a file must meet the following size requirements:</span><span class="sxs-lookup"><span data-stu-id="6ea60-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="6ea60-157">Larger than 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="6ea60-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="6ea60-158">Smaller than 1 MB.</span><span class="sxs-lookup"><span data-stu-id="6ea60-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="6ea60-159">Check the request at the origin server for a **Via** header</span><span class="sxs-lookup"><span data-stu-id="6ea60-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="6ea60-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span><span class="sxs-lookup"><span data-stu-id="6ea60-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="6ea60-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span><span class="sxs-lookup"><span data-stu-id="6ea60-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="6ea60-162">To override this behavior, perform the following:</span><span class="sxs-lookup"><span data-stu-id="6ea60-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="6ea60-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="6ea60-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="6ea60-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="6ea60-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

