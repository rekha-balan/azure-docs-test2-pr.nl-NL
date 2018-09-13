---
title: Pre-load assets on an Azure CDN endpoint | Microsoft Docs
description: Learn how to pre-load cached content on an Azure CDN endpoint.
services: cdn
documentationcenter: ''
author: dksimpson
manager: akucer
editor: ''
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2018
ms.author: mazha
ms.openlocfilehash: bf3161d756759e4b278e48ad7a49615e4a73d17f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44780590"
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="3c42f-103">Pre-load assets on an Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="3c42f-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="3c42f-104">By default, assets are cached only when they're requested.</span><span class="sxs-lookup"><span data-stu-id="3c42f-104">By default, assets are cached only when they're requested.</span></span> <span data-ttu-id="3c42f-105">Because the edge servers have not yet cached the content and need to forward the request to the origin server, the first request from each region can take longer than subsequent requests.</span><span class="sxs-lookup"><span data-stu-id="3c42f-105">Because the edge servers have not yet cached the content and need to forward the request to the origin server, the first request from each region can take longer than subsequent requests.</span></span> <span data-ttu-id="3c42f-106">To avoid this first-hit latency, pre-load your assets.</span><span class="sxs-lookup"><span data-stu-id="3c42f-106">To avoid this first-hit latency, pre-load your assets.</span></span> <span data-ttu-id="3c42f-107">In addition to providing a better customer experience, pre-loading your cached assets can reduce network traffic on the origin server.</span><span class="sxs-lookup"><span data-stu-id="3c42f-107">In addition to providing a better customer experience, pre-loading your cached assets can reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="3c42f-108">Pre-loading assets is useful for large events or content that becomes simultaneously available to many users, such as a new movie release or a software update.</span><span class="sxs-lookup"><span data-stu-id="3c42f-108">Pre-loading assets is useful for large events or content that becomes simultaneously available to many users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="3c42f-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span><span class="sxs-lookup"><span data-stu-id="3c42f-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="to-pre-load-assets"></a><span data-ttu-id="3c42f-110">To pre-load assets</span><span class="sxs-lookup"><span data-stu-id="3c42f-110">To pre-load assets</span></span>
1. <span data-ttu-id="3c42f-111">In the [Azure portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span><span class="sxs-lookup"><span data-stu-id="3c42f-111">In the [Azure portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span> <span data-ttu-id="3c42f-112">The profile pane opens.</span><span class="sxs-lookup"><span data-stu-id="3c42f-112">The profile pane opens.</span></span>
    
2. <span data-ttu-id="3c42f-113">Click the endpoint in the list.</span><span class="sxs-lookup"><span data-stu-id="3c42f-113">Click the endpoint in the list.</span></span> <span data-ttu-id="3c42f-114">The endpoint pane opens.</span><span class="sxs-lookup"><span data-stu-id="3c42f-114">The endpoint pane opens.</span></span>
3. <span data-ttu-id="3c42f-115">From the CDN endpoint pane, select **Load**.</span><span class="sxs-lookup"><span data-stu-id="3c42f-115">From the CDN endpoint pane, select **Load**.</span></span>
   
    ![CDN endpoint pane](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="3c42f-117">The **Load** pane opens.</span><span class="sxs-lookup"><span data-stu-id="3c42f-117">The **Load** pane opens.</span></span>
   
    ![CDN load pane](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="3c42f-119">For **Content path**, enter the full path of each asset you wish to load (for example, `/pictures/kitten.png`).</span><span class="sxs-lookup"><span data-stu-id="3c42f-119">For **Content path**, enter the full path of each asset you wish to load (for example, `/pictures/kitten.png`).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="3c42f-120">After you start entering text, more **Content path** text boxes will appear to allow you to build a list of multiple assets.</span><span class="sxs-lookup"><span data-stu-id="3c42f-120">After you start entering text, more **Content path** text boxes will appear to allow you to build a list of multiple assets.</span></span> <span data-ttu-id="3c42f-121">To delete assets from the list, select the ellipsis (...) button, then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="3c42f-121">To delete assets from the list, select the ellipsis (...) button, then select **Delete**.</span></span>
   > 
   > <span data-ttu-id="3c42f-122">Each content path must be a relative URL that fits the following [regular expressions](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="3c42f-122">Each content path must be a relative URL that fits the following [regular expressions](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > - <span data-ttu-id="3c42f-123">Load a single file path: `^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$`</span><span class="sxs-lookup"><span data-stu-id="3c42f-123">Load a single file path: `^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$`</span></span>  
   > - <span data-ttu-id="3c42f-124">Load a single file with query string: `^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$`</span><span class="sxs-lookup"><span data-stu-id="3c42f-124">Load a single file with query string: `^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$`</span></span> 
   > 
   > <span data-ttu-id="3c42f-125">Because each asset must have its own path, there's no wildcard functionality for pre-loading assets.</span><span class="sxs-lookup"><span data-stu-id="3c42f-125">Because each asset must have its own path, there's no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Load button](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="3c42f-127">When you are finished entering content paths, select **Load**.</span><span class="sxs-lookup"><span data-stu-id="3c42f-127">When you are finished entering content paths, select **Load**.</span></span>
   

> [!NOTE]
> <span data-ttu-id="3c42f-128">There's a limit of 10 load requests per minute per CDN profile and 50 concurrent paths can be processed at one time.</span><span class="sxs-lookup"><span data-stu-id="3c42f-128">There's a limit of 10 load requests per minute per CDN profile and 50 concurrent paths can be processed at one time.</span></span> <span data-ttu-id="3c42f-129">Each path has a path-length limit of 1024 characters.</span><span class="sxs-lookup"><span data-stu-id="3c42f-129">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="3c42f-130">See also</span><span class="sxs-lookup"><span data-stu-id="3c42f-130">See also</span></span>
* [<span data-ttu-id="3c42f-131">Purge an Azure CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="3c42f-131">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="3c42f-132">Azure CDN REST API reference: Pre-load content on an endpoint</span><span class="sxs-lookup"><span data-stu-id="3c42f-132">Azure CDN REST API reference: Pre-load content on an endpoint</span></span>](https://docs.microsoft.com/rest/api/cdn/endpoints/loadcontent)
* [<span data-ttu-id="3c42f-133">Azure CDN REST API reference: Purge content from an endpoint</span><span class="sxs-lookup"><span data-stu-id="3c42f-133">Azure CDN REST API reference: Purge content from an endpoint</span></span>](https://docs.microsoft.com/rest/api/cdn/endpoints/purgecontent)

