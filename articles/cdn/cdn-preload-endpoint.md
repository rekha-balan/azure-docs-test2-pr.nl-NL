---
title: Pre-load assets on an Azure CDN endpoint | Microsoft Docs
description: Learn how to pre-load cached content on an Azure CDN endpoint.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f449e2434b23f274ca6a59d24667724bac8a7846
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555166"
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="030d0-103">Pre-load assets on an Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="030d0-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="030d0-104">By default, assets are first cached as they are requested.</span><span class="sxs-lookup"><span data-stu-id="030d0-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="030d0-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span><span class="sxs-lookup"><span data-stu-id="030d0-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span></span> <span data-ttu-id="030d0-106">Pre-loading content avoids this first hit latency.</span><span class="sxs-lookup"><span data-stu-id="030d0-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="030d0-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span><span class="sxs-lookup"><span data-stu-id="030d0-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="030d0-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span><span class="sxs-lookup"><span data-stu-id="030d0-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="030d0-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span><span class="sxs-lookup"><span data-stu-id="030d0-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="030d0-110">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="030d0-110">Walkthrough</span></span>
1. <span data-ttu-id="030d0-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span><span class="sxs-lookup"><span data-stu-id="030d0-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span>  <span data-ttu-id="030d0-112">The profile blade opens.</span><span class="sxs-lookup"><span data-stu-id="030d0-112">The profile blade opens.</span></span>
2. <span data-ttu-id="030d0-113">Click the endpoint in the list.</span><span class="sxs-lookup"><span data-stu-id="030d0-113">Click the endpoint in the list.</span></span>  <span data-ttu-id="030d0-114">The endpoint blade opens.</span><span class="sxs-lookup"><span data-stu-id="030d0-114">The endpoint blade opens.</span></span>
3. <span data-ttu-id="030d0-115">From the CDN endpoint blade, click the load button.</span><span class="sxs-lookup"><span data-stu-id="030d0-115">From the CDN endpoint blade, click the load button.</span></span>
   
    ![CDN endpoint blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="030d0-117">The Load blade opens.</span><span class="sxs-lookup"><span data-stu-id="030d0-117">The Load blade opens.</span></span>
   
    ![CDN load blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="030d0-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span><span class="sxs-lookup"><span data-stu-id="030d0-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="030d0-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span><span class="sxs-lookup"><span data-stu-id="030d0-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="030d0-121">You can delete assets from the list by clicking the ellipsis (...) button.</span><span class="sxs-lookup"><span data-stu-id="030d0-121">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="030d0-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="030d0-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="030d0-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="030d0-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="030d0-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="030d0-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="030d0-125">Each asset must have its own path.</span><span class="sxs-lookup"><span data-stu-id="030d0-125">Each asset must have its own path.</span></span>  <span data-ttu-id="030d0-126">There is no wildcard functionality for pre-loading assets.</span><span class="sxs-lookup"><span data-stu-id="030d0-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Load button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="030d0-128">Click the **Load** button.</span><span class="sxs-lookup"><span data-stu-id="030d0-128">Click the **Load** button.</span></span>
   
    ![Load button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="030d0-130">There is a limitation of 10 load requests per minute per CDN profile.</span><span class="sxs-lookup"><span data-stu-id="030d0-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="030d0-131">See also</span><span class="sxs-lookup"><span data-stu-id="030d0-131">See also</span></span>
* [<span data-ttu-id="030d0-132">Purge an Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="030d0-132">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="030d0-133">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span><span class="sxs-lookup"><span data-stu-id="030d0-133">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)





