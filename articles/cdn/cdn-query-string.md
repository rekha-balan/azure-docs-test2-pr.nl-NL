---
title: Control Azure CDN caching behavior with query strings - standard tier | Microsoft Docs
description: Azure CDN query string caching controls how files are cached when a web request contains a query string. This article describes query string caching in Azure CDN standard products.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2018
ms.author: v-deasim
ms.openlocfilehash: aa553dfc04a755be1169fa117ec66dd10ea75b54
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44813994"
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---standard-tier"></a><span data-ttu-id="0da48-104">Control Azure CDN caching behavior with query strings - standard tier</span><span class="sxs-lookup"><span data-stu-id="0da48-104">Control Azure CDN caching behavior with query strings - standard tier</span></span>
> [!div class="op_single_selector"]
> * [Standard tier](cdn-query-string.md)
> * [Premium tier](cdn-query-string-premium.md)
> 

## <a name="overview"></a><span data-ttu-id="0da48-107">Overview</span><span class="sxs-lookup"><span data-stu-id="0da48-107">Overview</span></span>
<span data-ttu-id="0da48-108">With Azure Content Delivery Network (CDN), you can control how files are cached for a web request that contains a query string.</span><span class="sxs-lookup"><span data-stu-id="0da48-108">With Azure Content Delivery Network (CDN), you can control how files are cached for a web request that contains a query string.</span></span> <span data-ttu-id="0da48-109">In a web request with a query string, the query string is that portion of the request that occurs after a question mark (?).</span><span class="sxs-lookup"><span data-stu-id="0da48-109">In a web request with a query string, the query string is that portion of the request that occurs after a question mark (?).</span></span> <span data-ttu-id="0da48-110">A query string can contain one or more key-value pairs, in which the field name and its value are separated by an equals sign (=).</span><span class="sxs-lookup"><span data-stu-id="0da48-110">A query string can contain one or more key-value pairs, in which the field name and its value are separated by an equals sign (=).</span></span> <span data-ttu-id="0da48-111">Each key-value pair is separated by an ampersand (&).</span><span class="sxs-lookup"><span data-stu-id="0da48-111">Each key-value pair is separated by an ampersand (&).</span></span> <span data-ttu-id="0da48-112">For example, http:\//www.contoso.com/content.mov?field1=value1&field2=value2.</span><span class="sxs-lookup"><span data-stu-id="0da48-112">For example, http:\//www.contoso.com/content.mov?field1=value1&field2=value2.</span></span> <span data-ttu-id="0da48-113">If there is more than one key-value pair in a query string of a request, their order does not matter.</span><span class="sxs-lookup"><span data-stu-id="0da48-113">If there is more than one key-value pair in a query string of a request, their order does not matter.</span></span> 

> [!IMPORTANT]
> The Azure CDN standard and premium products provide the same query string caching functionality, but the user interface is different. This article describes the interface for **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**. For query string caching with **Azure CDN Premium from Verizon**, see [Control Azure CDN caching behavior with query strings - premium tier](cdn-query-string-premium.md).

<span data-ttu-id="0da48-117">Three query string modes are available:</span><span class="sxs-lookup"><span data-stu-id="0da48-117">Three query string modes are available:</span></span>

- <span data-ttu-id="0da48-118">**Ignore query strings**: Default mode.</span><span class="sxs-lookup"><span data-stu-id="0da48-118">**Ignore query strings**: Default mode.</span></span> <span data-ttu-id="0da48-119">In this mode, the CDN point-of-presence (POP) node passes the query strings from the requestor to the origin server on the first request and caches the asset.</span><span class="sxs-lookup"><span data-stu-id="0da48-119">In this mode, the CDN point-of-presence (POP) node passes the query strings from the requestor to the origin server on the first request and caches the asset.</span></span> <span data-ttu-id="0da48-120">All subsequent requests for the asset that are served from the POP ignore the query strings until the cached asset expires.</span><span class="sxs-lookup"><span data-stu-id="0da48-120">All subsequent requests for the asset that are served from the POP ignore the query strings until the cached asset expires.</span></span>

- <span data-ttu-id="0da48-121">**Bypass caching for query strings**: In this mode, requests with query strings are not cached at the CDN POP node.</span><span class="sxs-lookup"><span data-stu-id="0da48-121">**Bypass caching for query strings**: In this mode, requests with query strings are not cached at the CDN POP node.</span></span> <span data-ttu-id="0da48-122">The POP node retrieves the asset directly from the origin server and passes it to the requestor with each request.</span><span class="sxs-lookup"><span data-stu-id="0da48-122">The POP node retrieves the asset directly from the origin server and passes it to the requestor with each request.</span></span>

- <span data-ttu-id="0da48-123">**Cache every unique URL**: In this mode, each request with a unique URL, including the query string, is treated as a unique asset with its own cache.</span><span class="sxs-lookup"><span data-stu-id="0da48-123">**Cache every unique URL**: In this mode, each request with a unique URL, including the query string, is treated as a unique asset with its own cache.</span></span> <span data-ttu-id="0da48-124">For example, the response from the origin server for a request for example.ashx?q=test1 is cached at the POP node and returned for subsequent caches with the same query string.</span><span class="sxs-lookup"><span data-stu-id="0da48-124">For example, the response from the origin server for a request for example.ashx?q=test1 is cached at the POP node and returned for subsequent caches with the same query string.</span></span> <span data-ttu-id="0da48-125">A request for example.ashx?q=test2 is cached as a separate asset with its own time-to-live setting.</span><span class="sxs-lookup"><span data-stu-id="0da48-125">A request for example.ashx?q=test2 is cached as a separate asset with its own time-to-live setting.</span></span>
   
    >[!IMPORTANT] 
    > Do not use this mode when the query string contains parameters that will change with every request, such as a session ID or a user name, because it will result in a low cache-hit ratio.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="0da48-127">Changing query string caching settings for standard CDN profiles</span><span class="sxs-lookup"><span data-stu-id="0da48-127">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="0da48-128">Open a CDN profile, then select the CDN endpoint you want to manage.</span><span class="sxs-lookup"><span data-stu-id="0da48-128">Open a CDN profile, then select the CDN endpoint you want to manage.</span></span>
   
   ![CDN profile endpoints](./media/cdn-query-string/cdn-endpoints.png)
   
2. <span data-ttu-id="0da48-130">In the left pane under Settings, click **Caching rules**.</span><span class="sxs-lookup"><span data-stu-id="0da48-130">In the left pane under Settings, click **Caching rules**.</span></span>
   
    ![CDN Caching rules button](./media/cdn-query-string/cdn-caching-rules-btn.png)
   
3. <span data-ttu-id="0da48-132">In the **Query string caching behavior** list, select a query string mode, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0da48-132">In the **Query string caching behavior** list, select a query string mode, then click **Save**.</span></span>
   
   ![CDN query string caching options](./media/cdn-query-string/cdn-query-string.png)

> [!IMPORTANT]
> Because it takes time for the registration to propagate through Azure CDN, cache string settings changes might not be immediately visible:
> - For **Azure CDN Standard from Microsoft** profiles, propagation usually completes in 10 minutes. 
> - For **Azure CDN Standard from Akamai** profiles, propagation usually completes within one minute. 
> - For **Azure CDN Standard from Verizon** and **Azure CDN Premium from Verizon** profiles, propagation usually completes in 10 minutes. 



