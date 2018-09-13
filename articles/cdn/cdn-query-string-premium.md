---
title: Control Azure CDN caching behavior with query strings - Premium | Microsoft Docs
description: Azure CDN query string caching controls how files are to be cached when they contain query strings.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0aedccc30b644d2fbe4d16bfefb42ad971c6a506
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562985"
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="1a345-103">Control Azure CDN caching behavior with query strings - Premium</span><span class="sxs-lookup"><span data-stu-id="1a345-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [Azure CDN Premium from Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="1a345-106">Overview</span><span class="sxs-lookup"><span data-stu-id="1a345-106">Overview</span></span>
<span data-ttu-id="1a345-107">Query string caching controls how files are to be cached when they contain query strings.</span><span class="sxs-lookup"><span data-stu-id="1a345-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.  This document describes the interface for **Azure CDN Premium from Verizon**.  For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).
> 
> 

<span data-ttu-id="1a345-111">Three modes are available:</span><span class="sxs-lookup"><span data-stu-id="1a345-111">Three modes are available:</span></span>

* <span data-ttu-id="1a345-112">**standard-cache**:  This is the default mode.</span><span class="sxs-lookup"><span data-stu-id="1a345-112">**standard-cache**:  This is the default mode.</span></span>  <span data-ttu-id="1a345-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span><span class="sxs-lookup"><span data-stu-id="1a345-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="1a345-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span><span class="sxs-lookup"><span data-stu-id="1a345-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="1a345-115">**no-cache**:  In this mode, requests with query strings are not cached at the CDN edge node.</span><span class="sxs-lookup"><span data-stu-id="1a345-115">**no-cache**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="1a345-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span><span class="sxs-lookup"><span data-stu-id="1a345-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="1a345-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span><span class="sxs-lookup"><span data-stu-id="1a345-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="1a345-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span><span class="sxs-lookup"><span data-stu-id="1a345-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="1a345-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span><span class="sxs-lookup"><span data-stu-id="1a345-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="1a345-120">Changing query string caching settings for premium CDN profiles</span><span class="sxs-lookup"><span data-stu-id="1a345-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="1a345-121">From the CDN profile blade, click the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="1a345-121">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN profile blade manage button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="1a345-123">The CDN management portal opens.</span><span class="sxs-lookup"><span data-stu-id="1a345-123">The CDN management portal opens.</span></span>
2. <span data-ttu-id="1a345-124">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span><span class="sxs-lookup"><span data-stu-id="1a345-124">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="1a345-125">Click on **Query-String Caching**.</span><span class="sxs-lookup"><span data-stu-id="1a345-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="1a345-126">Query string caching options are displayed.</span><span class="sxs-lookup"><span data-stu-id="1a345-126">Query string caching options are displayed.</span></span>
   
    ![CDN query string caching options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="1a345-128">After making your selection, click the **Update** button.</span><span class="sxs-lookup"><span data-stu-id="1a345-128">After making your selection, click the **Update** button.</span></span>

> [!IMPORTANT]
> The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.  For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.
> 
> 



