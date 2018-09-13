---
title: Analyze Azure CDN usage patterns | Microsoft Docs
description: This article describes the different types of analysis reports available for Azure CDN products.
services: cdn
documentationcenter: ''
author: dksimpson
manager: akucer
editor: ''
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/05/2017
ms.author: rli; v-deasim
ms.openlocfilehash: 61fbe6e29df787048a9694138d3c9095f5cba76b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857023"
---
# <a name="analyze-azure-cdn-usage-patterns"></a><span data-ttu-id="f2dd4-103">Analyze Azure CDN usage patterns</span><span class="sxs-lookup"><span data-stu-id="f2dd4-103">Analyze Azure CDN usage patterns</span></span>

<span data-ttu-id="f2dd4-104">After you enable CDN for your application, you can monitor CDN usage, check the health of your delivery, and troubleshoot potential issues.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-104">After you enable CDN for your application, you can monitor CDN usage, check the health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="f2dd4-105">Azure CDN provides these capabilities in the following ways:</span><span class="sxs-lookup"><span data-stu-id="f2dd4-105">Azure CDN provides these capabilities in the following ways:</span></span> 

## <a name="core-analytics-via-azure-diagnostic-logs"></a><span data-ttu-id="f2dd4-106">Core analytics via Azure diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="f2dd4-106">Core analytics via Azure diagnostic logs</span></span>

<span data-ttu-id="f2dd4-107">Core analytics is available for CDN endpoints for all pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-107">Core analytics is available for CDN endpoints for all pricing tiers.</span></span> <span data-ttu-id="f2dd4-108">Azure diagnostics logs allow core analytics to be exported to Azure storage, event hubs, or Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-108">Azure diagnostics logs allow core analytics to be exported to Azure storage, event hubs, or Azure Log Analytics.</span></span> <span data-ttu-id="f2dd4-109">Azure Log Analytics offers a solution with graphs that are user-configurable and customizable.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-109">Azure Log Analytics offers a solution with graphs that are user-configurable and customizable.</span></span> <span data-ttu-id="f2dd4-110">For more information about Azure diagnostic logs, see [Azure diagnostic logs](cdn-azure-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd4-110">For more information about Azure diagnostic logs, see [Azure diagnostic logs](cdn-azure-diagnostic-logs.md).</span></span>

## <a name="verizon-core-reports"></a><span data-ttu-id="f2dd4-111">Verizon core reports</span><span class="sxs-lookup"><span data-stu-id="f2dd4-111">Verizon core reports</span></span>

<span data-ttu-id="f2dd4-112">As an Azure CDN user with an **Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon** profile, you can view Verizon core reports in the Verizon supplemental portal.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-112">As an Azure CDN user with an **Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon** profile, you can view Verizon core reports in the Verizon supplemental portal.</span></span> <span data-ttu-id="f2dd4-113">Verizon core reports is accessible via the **Manage** option from the Azure portal and offers a variety of graphs and views.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-113">Verizon core reports is accessible via the **Manage** option from the Azure portal and offers a variety of graphs and views.</span></span> <span data-ttu-id="f2dd4-114">For more information, see [Core Reports from Verizon](cdn-analyze-usage-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd4-114">For more information, see [Core Reports from Verizon](cdn-analyze-usage-patterns.md).</span></span>

## <a name="verizon-custom-reports"></a><span data-ttu-id="f2dd4-115">Verizon custom reports</span><span class="sxs-lookup"><span data-stu-id="f2dd4-115">Verizon custom reports</span></span>

<span data-ttu-id="f2dd4-116">As an Azure CDN user with an **Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon** profile, you can view Verizon custom reports in the Verizon supplemental portal.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-116">As an Azure CDN user with an **Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon** profile, you can view Verizon custom reports in the Verizon supplemental portal.</span></span> <span data-ttu-id="f2dd4-117">Verizon custom reports is accessible via the **Manage** option from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-117">Verizon custom reports is accessible via the **Manage** option from the Azure portal.</span></span> <span data-ttu-id="f2dd4-118">The Verizon custom reports page shows the number of hits or data transferred for each edge CName belonging to an Azure CDN profile.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-118">The Verizon custom reports page shows the number of hits or data transferred for each edge CName belonging to an Azure CDN profile.</span></span> <span data-ttu-id="f2dd4-119">The data can be grouped by HTTP response code or cache status over any period of time.</span><span class="sxs-lookup"><span data-stu-id="f2dd4-119">The data can be grouped by HTTP response code or cache status over any period of time.</span></span> <span data-ttu-id="f2dd4-120">For more information, see [Custom Reports from Verizon](cdn-verizon-custom-reports.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd4-120">For more information, see [Custom Reports from Verizon](cdn-verizon-custom-reports.md).</span></span>

## <a name="azure-cdn-premium-from-verizon-reports"></a><span data-ttu-id="f2dd4-121">Azure CDN Premium from Verizon reports</span><span class="sxs-lookup"><span data-stu-id="f2dd4-121">Azure CDN Premium from Verizon reports</span></span>

<span data-ttu-id="f2dd4-122">With **Azure CDN Premium from Verizon**, you can also access the following reports:</span><span class="sxs-lookup"><span data-stu-id="f2dd4-122">With **Azure CDN Premium from Verizon**, you can also access the following reports:</span></span>
   * [<span data-ttu-id="f2dd4-123">Advanced HTTP reports</span><span class="sxs-lookup"><span data-stu-id="f2dd4-123">Advanced HTTP reports</span></span>](cdn-advanced-http-reports.md)
   * [<span data-ttu-id="f2dd4-124">Real-time stats</span><span class="sxs-lookup"><span data-stu-id="f2dd4-124">Real-time stats</span></span>](cdn-real-time-stats.md)
   * [<span data-ttu-id="f2dd4-125">Edge node performance</span><span class="sxs-lookup"><span data-stu-id="f2dd4-125">Edge node performance</span></span>](cdn-edge-performance.md)

