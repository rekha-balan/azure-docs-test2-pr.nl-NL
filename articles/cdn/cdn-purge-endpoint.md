---
title: Purge an Azure CDN endpoint | Microsoft Docs
description: Learn how to purge all cached content from an Azure CDN endpoint.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5991a4c7783c5ad49c529d74205e040fd24ce0d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552462"
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="9fe75-103">Purge an Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="9fe75-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="9fe75-104">Overview</span><span class="sxs-lookup"><span data-stu-id="9fe75-104">Overview</span></span>
<span data-ttu-id="9fe75-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span><span class="sxs-lookup"><span data-stu-id="9fe75-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="9fe75-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span><span class="sxs-lookup"><span data-stu-id="9fe75-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="9fe75-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span><span class="sxs-lookup"><span data-stu-id="9fe75-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="9fe75-108">CDN will immediately retrieve the new assets for the next client requests.</span><span class="sxs-lookup"><span data-stu-id="9fe75-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="9fe75-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span><span class="sxs-lookup"><span data-stu-id="9fe75-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="9fe75-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span><span class="sxs-lookup"><span data-stu-id="9fe75-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="9fe75-111">Note that purging only clears the cached content on the CDN edge servers.</span><span class="sxs-lookup"><span data-stu-id="9fe75-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="9fe75-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span><span class="sxs-lookup"><span data-stu-id="9fe75-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="9fe75-113">It's important to remember this when you set a file's time-to-live.</span><span class="sxs-lookup"><span data-stu-id="9fe75-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="9fe75-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="9fe75-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="9fe75-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span><span class="sxs-lookup"><span data-stu-id="9fe75-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="9fe75-116">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="9fe75-116">Walkthrough</span></span>
1. <span data-ttu-id="9fe75-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span><span class="sxs-lookup"><span data-stu-id="9fe75-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="9fe75-118">From the CDN profile blade, click the purge button.</span><span class="sxs-lookup"><span data-stu-id="9fe75-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![CDN profile blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="9fe75-120">The Purge blade opens.</span><span class="sxs-lookup"><span data-stu-id="9fe75-120">The Purge blade opens.</span></span>
   
    ![CDN purge blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="9fe75-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span><span class="sxs-lookup"><span data-stu-id="9fe75-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![Purge form](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="9fe75-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span><span class="sxs-lookup"><span data-stu-id="9fe75-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="9fe75-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span><span class="sxs-lookup"><span data-stu-id="9fe75-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="9fe75-126">Select what assets you wish to purge from the edge nodes.</span><span class="sxs-lookup"><span data-stu-id="9fe75-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="9fe75-127">If you wish to clear all assets, click the **Purge all** checkbox.</span><span class="sxs-lookup"><span data-stu-id="9fe75-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="9fe75-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span><span class="sxs-lookup"><span data-stu-id="9fe75-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="9fe75-129">Below formats are supported in the path.</span><span class="sxs-lookup"><span data-stu-id="9fe75-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="9fe75-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="9fe75-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="9fe75-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span><span class="sxs-lookup"><span data-stu-id="9fe75-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="9fe75-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="9fe75-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="9fe75-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span><span class="sxs-lookup"><span data-stu-id="9fe75-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="9fe75-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span><span class="sxs-lookup"><span data-stu-id="9fe75-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="9fe75-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fe75-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="9fe75-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span><span class="sxs-lookup"><span data-stu-id="9fe75-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="9fe75-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="9fe75-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="9fe75-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="9fe75-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="9fe75-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="9fe75-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="9fe75-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span><span class="sxs-lookup"><span data-stu-id="9fe75-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="9fe75-141">You can delete assets from the list by clicking the ellipsis (...) button.</span><span class="sxs-lookup"><span data-stu-id="9fe75-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="9fe75-142">Click the **Purge** button.</span><span class="sxs-lookup"><span data-stu-id="9fe75-142">Click the **Purge** button.</span></span>
   
    ![Purge button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="9fe75-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span><span class="sxs-lookup"><span data-stu-id="9fe75-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="9fe75-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span><span class="sxs-lookup"><span data-stu-id="9fe75-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="9fe75-146">See also</span><span class="sxs-lookup"><span data-stu-id="9fe75-146">See also</span></span>
* [<span data-ttu-id="9fe75-147">Pre-load assets on an Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="9fe75-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="9fe75-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span><span class="sxs-lookup"><span data-stu-id="9fe75-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)





