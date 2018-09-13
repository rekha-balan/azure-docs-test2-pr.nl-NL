---
title: Migrate an Azure CDN profile from Verizon Standard to Verizon Premium | Microsoft Docs
description: Learn about the details of migrating a profile from Verizon Standard to Verizon Premium.
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
ms.date: 06/21/2018
ms.author: v-deasim
ms.custom: ''
ms.openlocfilehash: 074dbb094e7ae2cd1f1719016928bd7348da3949
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866673"
---
# <a name="migrate-an-azure-cdn-profile-from-standard-verizon-to-premium-verizon"></a><span data-ttu-id="d48cb-103">Migrate an Azure CDN profile from Standard Verizon to Premium Verizon</span><span class="sxs-lookup"><span data-stu-id="d48cb-103">Migrate an Azure CDN profile from Standard Verizon to Premium Verizon</span></span>

<span data-ttu-id="d48cb-104">When you create an Azure Content Delivery Network (CDN) profile to manage your endpoints, Azure CDN offers four different products for you to choose from.</span><span class="sxs-lookup"><span data-stu-id="d48cb-104">When you create an Azure Content Delivery Network (CDN) profile to manage your endpoints, Azure CDN offers four different products for you to choose from.</span></span> <span data-ttu-id="d48cb-105">For information about the different products and their available features, see [Compare Azure CDN product features](cdn-features.md).</span><span class="sxs-lookup"><span data-stu-id="d48cb-105">For information about the different products and their available features, see [Compare Azure CDN product features](cdn-features.md).</span></span>

<span data-ttu-id="d48cb-106">If you've create an **Azure CDN Standard from Verizon** profile and are using it to manage your CDN endpoints, you have the option to upgrade it to an **Azure CDN Premium from Verizon** profile.</span><span class="sxs-lookup"><span data-stu-id="d48cb-106">If you've create an **Azure CDN Standard from Verizon** profile and are using it to manage your CDN endpoints, you have the option to upgrade it to an **Azure CDN Premium from Verizon** profile.</span></span> <span data-ttu-id="d48cb-107">When you upgrade, your CDN endpoints and all of your data will be preserved.</span><span class="sxs-lookup"><span data-stu-id="d48cb-107">When you upgrade, your CDN endpoints and all of your data will be preserved.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d48cb-108">Once you've upgraded to an **Azure CDN Premium from Verizon** profile, you cannot later convert it back to an **Azure CDN Standard from Verizon** profile.</span><span class="sxs-lookup"><span data-stu-id="d48cb-108">Once you've upgraded to an **Azure CDN Premium from Verizon** profile, you cannot later convert it back to an **Azure CDN Standard from Verizon** profile.</span></span>
> 

<span data-ttu-id="d48cb-109">To upgrade an **Azure CDN Standard from Verizon** profile, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="d48cb-109">To upgrade an **Azure CDN Standard from Verizon** profile, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="profile-comparison"></a><span data-ttu-id="d48cb-110">Profile comparison</span><span class="sxs-lookup"><span data-stu-id="d48cb-110">Profile comparison</span></span>
<span data-ttu-id="d48cb-111">**Azure CDN Premium from Verizon** profiles have the following key differences from **Azure CDN Standard from Verizon** profiles:</span><span class="sxs-lookup"><span data-stu-id="d48cb-111">**Azure CDN Premium from Verizon** profiles have the following key differences from **Azure CDN Standard from Verizon** profiles:</span></span>
- <span data-ttu-id="d48cb-112">For certain Azure CDN features such as [compression](cdn-improve-performance.md), [caching rules](cdn-caching-rules.md), and [geo filtering](cdn-restrict-access-by-country.md), you cannot use the Azure CDN interface, you must use the Verizon portal via the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="d48cb-112">For certain Azure CDN features such as [compression](cdn-improve-performance.md), [caching rules](cdn-caching-rules.md), and [geo filtering](cdn-restrict-access-by-country.md), you cannot use the Azure CDN interface, you must use the Verizon portal via the **Manage** button.</span></span>
- <span data-ttu-id="d48cb-113">API: Unlike with Standard Verizon, you cannot use the API to control those features that are accessed from the Premium Verizon portal.</span><span class="sxs-lookup"><span data-stu-id="d48cb-113">API: Unlike with Standard Verizon, you cannot use the API to control those features that are accessed from the Premium Verizon portal.</span></span> <span data-ttu-id="d48cb-114">However, you can use the API to control other common features, such as creating/deleting an endpoint, purging/loading cached assets, and enabling/disabling a custom domain.</span><span class="sxs-lookup"><span data-stu-id="d48cb-114">However, you can use the API to control other common features, such as creating/deleting an endpoint, purging/loading cached assets, and enabling/disabling a custom domain.</span></span>
- <span data-ttu-id="d48cb-115">Pricing: Premium Verizon has a different pricing structure for data transfers  than Standard Verizon.</span><span class="sxs-lookup"><span data-stu-id="d48cb-115">Pricing: Premium Verizon has a different pricing structure for data transfers  than Standard Verizon.</span></span> <span data-ttu-id="d48cb-116">For more information, see [Content Delivery Network pricing](https://azure.microsoft.com/pricing/details/cdn/).</span><span class="sxs-lookup"><span data-stu-id="d48cb-116">For more information, see [Content Delivery Network pricing](https://azure.microsoft.com/pricing/details/cdn/).</span></span>

<span data-ttu-id="d48cb-117">**Azure CDN Premium from Verizon** profiles have the following additional features:</span><span class="sxs-lookup"><span data-stu-id="d48cb-117">**Azure CDN Premium from Verizon** profiles have the following additional features:</span></span>
- <span data-ttu-id="d48cb-118">[Token authentication](cdn-token-auth.md): Allows users to obtain and use a token to fetch secure resources.</span><span class="sxs-lookup"><span data-stu-id="d48cb-118">[Token authentication](cdn-token-auth.md): Allows users to obtain and use a token to fetch secure resources.</span></span>
- <span data-ttu-id="d48cb-119">[Rules engine](cdn-rules-engine.md): Enables you to customize how HTTP requests are handled.</span><span class="sxs-lookup"><span data-stu-id="d48cb-119">[Rules engine](cdn-rules-engine.md): Enables you to customize how HTTP requests are handled.</span></span>
- <span data-ttu-id="d48cb-120">Advanced analytics tools:</span><span class="sxs-lookup"><span data-stu-id="d48cb-120">Advanced analytics tools:</span></span>
   - [<span data-ttu-id="d48cb-121">Detailed HTTP analytics</span><span class="sxs-lookup"><span data-stu-id="d48cb-121">Detailed HTTP analytics</span></span>](cdn-advanced-http-reports.md)
   - [<span data-ttu-id="d48cb-122">Edge performance analytics</span><span class="sxs-lookup"><span data-stu-id="d48cb-122">Edge performance analytics</span></span>](cdn-edge-performance.md)
   - [<span data-ttu-id="d48cb-123">Real-time analytics</span><span class="sxs-lookup"><span data-stu-id="d48cb-123">Real-time analytics</span></span>](cdn-real-time-alerts.md)


## <a name="next-steps"></a><span data-ttu-id="d48cb-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="d48cb-124">Next steps</span></span>
<span data-ttu-id="d48cb-125">To learn more about the rules engine, see [Azure CDN rules engine reference](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d48cb-125">To learn more about the rules engine, see [Azure CDN rules engine reference](cdn-rules-engine-reference.md).</span></span>

