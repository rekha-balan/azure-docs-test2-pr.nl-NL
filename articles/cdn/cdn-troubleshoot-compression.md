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
ms.openlocfilehash: b9b3d97318383ec0ae417c524141d6d8ad39d846
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551943"
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="57580-103">Troubleshooting CDN file compression</span><span class="sxs-lookup"><span data-stu-id="57580-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="57580-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="57580-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="57580-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="57580-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="57580-106">Alternatively, you can also file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="57580-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="57580-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="57580-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="57580-108">Symptom</span><span class="sxs-lookup"><span data-stu-id="57580-108">Symptom</span></span>
<span data-ttu-id="57580-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span><span class="sxs-lookup"><span data-stu-id="57580-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="57580-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="57580-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="57580-111">Check the HTTP response headers returned with your cached CDN content.</span><span class="sxs-lookup"><span data-stu-id="57580-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="57580-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span><span class="sxs-lookup"><span data-stu-id="57580-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Content-Encoding header](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="57580-114">Cause</span><span class="sxs-lookup"><span data-stu-id="57580-114">Cause</span></span>
<span data-ttu-id="57580-115">There are several possible causes, including:</span><span class="sxs-lookup"><span data-stu-id="57580-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="57580-116">The requested content is not eligible for compression.</span><span class="sxs-lookup"><span data-stu-id="57580-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="57580-117">Compression is not enabled for the requested file type.</span><span class="sxs-lookup"><span data-stu-id="57580-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="57580-118">The HTTP request did not include a header requesting a valid compression type.</span><span class="sxs-lookup"><span data-stu-id="57580-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="57580-119">Troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="57580-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="57580-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span><span class="sxs-lookup"><span data-stu-id="57580-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="57580-121">Usually, changes are applied within 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="57580-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="57580-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span><span class="sxs-lookup"><span data-stu-id="57580-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="57580-123">Verify the request</span><span class="sxs-lookup"><span data-stu-id="57580-123">Verify the request</span></span>
<span data-ttu-id="57580-124">First, we should do a quick sanity check on the request.</span><span class="sxs-lookup"><span data-stu-id="57580-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="57580-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span><span class="sxs-lookup"><span data-stu-id="57580-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="57580-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span><span class="sxs-lookup"><span data-stu-id="57580-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="57580-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span><span class="sxs-lookup"><span data-stu-id="57580-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="57580-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span><span class="sxs-lookup"><span data-stu-id="57580-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN request headers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="57580-130">Verify compression settings (Standard CDN profile)</span><span class="sxs-lookup"><span data-stu-id="57580-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="57580-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span><span class="sxs-lookup"><span data-stu-id="57580-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="57580-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span><span class="sxs-lookup"><span data-stu-id="57580-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="57580-133">Verify compression is enabled.</span><span class="sxs-lookup"><span data-stu-id="57580-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="57580-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span><span class="sxs-lookup"><span data-stu-id="57580-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN compression settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="57580-136">Verify compression settings (Premium CDN profile)</span><span class="sxs-lookup"><span data-stu-id="57580-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="57580-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span><span class="sxs-lookup"><span data-stu-id="57580-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="57580-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="57580-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="57580-139">The supplemental portal will open.</span><span class="sxs-lookup"><span data-stu-id="57580-139">The supplemental portal will open.</span></span>  <span data-ttu-id="57580-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span><span class="sxs-lookup"><span data-stu-id="57580-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="57580-141">Click **Compression**.</span><span class="sxs-lookup"><span data-stu-id="57580-141">Click **Compression**.</span></span> 

* <span data-ttu-id="57580-142">Verify compression is enabled.</span><span class="sxs-lookup"><span data-stu-id="57580-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="57580-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span><span class="sxs-lookup"><span data-stu-id="57580-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="57580-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span><span class="sxs-lookup"><span data-stu-id="57580-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN premium compression settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="57580-146">Verify the content is cached</span><span class="sxs-lookup"><span data-stu-id="57580-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="57580-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span><span class="sxs-lookup"><span data-stu-id="57580-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="57580-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span><span class="sxs-lookup"><span data-stu-id="57580-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="57580-149">Check the **Server** response header.</span><span class="sxs-lookup"><span data-stu-id="57580-149">Check the **Server** response header.</span></span>  <span data-ttu-id="57580-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span><span class="sxs-lookup"><span data-stu-id="57580-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="57580-151">Check the **X-Cache** response header.</span><span class="sxs-lookup"><span data-stu-id="57580-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="57580-152">The header should read **HIT**.</span><span class="sxs-lookup"><span data-stu-id="57580-152">The header should read **HIT**.</span></span>  

![CDN response headers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="57580-154">Verify the file meets the size requirements</span><span class="sxs-lookup"><span data-stu-id="57580-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="57580-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span><span class="sxs-lookup"><span data-stu-id="57580-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="57580-156">To be eligible for compression, a file must meet the following size requirements:</span><span class="sxs-lookup"><span data-stu-id="57580-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="57580-157">Larger than 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="57580-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="57580-158">Smaller than 1 MB.</span><span class="sxs-lookup"><span data-stu-id="57580-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="57580-159">Check the request at the origin server for a **Via** header</span><span class="sxs-lookup"><span data-stu-id="57580-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="57580-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span><span class="sxs-lookup"><span data-stu-id="57580-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="57580-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span><span class="sxs-lookup"><span data-stu-id="57580-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="57580-162">To override this behavior, perform the following:</span><span class="sxs-lookup"><span data-stu-id="57580-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="57580-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="57580-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="57580-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="57580-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>






