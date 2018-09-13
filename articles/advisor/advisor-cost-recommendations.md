---
title: Azure Advisor Cost recommendations | Microsoft Docs
description: Use Azure Advisor to optimize the cost of your Azure deployments.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 81eb993bb9cfd959acb91fe1f8f9c9fb452e868d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670471"
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="e6437-103">Advisor Cost recommendations</span><span class="sxs-lookup"><span data-stu-id="e6437-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="e6437-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span><span class="sxs-lookup"><span data-stu-id="e6437-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="e6437-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span><span class="sxs-lookup"><span data-stu-id="e6437-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

![Advisor Cost tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="e6437-107">Optimize virtual machine spend by resizing underutilized instances</span><span class="sxs-lookup"><span data-stu-id="e6437-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="e6437-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="e6437-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="e6437-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span><span class="sxs-lookup"><span data-stu-id="e6437-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="e6437-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span><span class="sxs-lookup"><span data-stu-id="e6437-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="e6437-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span><span class="sxs-lookup"><span data-stu-id="e6437-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>  

![Advisor cost recommendations for resizing virtual machines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-to-manage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="e6437-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span><span class="sxs-lookup"><span data-stu-id="e6437-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="e6437-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span><span class="sxs-lookup"><span data-stu-id="e6437-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="e6437-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span><span class="sxs-lookup"><span data-stu-id="e6437-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="e6437-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="e6437-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Advisor cost recommendations for elastic database pools](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="e6437-118">How to access cost recommendations in Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="e6437-118">How to access cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="e6437-119">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6437-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e6437-120">In the left pane, click **More services**.</span><span class="sxs-lookup"><span data-stu-id="e6437-120">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="e6437-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="e6437-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="e6437-122">The Advisor dashboard is displayed.</span><span class="sxs-lookup"><span data-stu-id="e6437-122">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="e6437-123">On the Advisor dashboard, click the **Cost** tab.</span><span class="sxs-lookup"><span data-stu-id="e6437-123">On the Advisor dashboard, click the **Cost** tab.</span></span>

5. <span data-ttu-id="e6437-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span><span class="sxs-lookup"><span data-stu-id="e6437-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="e6437-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span><span class="sxs-lookup"><span data-stu-id="e6437-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="e6437-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span><span class="sxs-lookup"><span data-stu-id="e6437-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="e6437-127">This is a *one-time operation*.</span><span class="sxs-lookup"><span data-stu-id="e6437-127">This is a *one-time operation*.</span></span> <span data-ttu-id="e6437-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span><span class="sxs-lookup"><span data-stu-id="e6437-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6437-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6437-129">Next steps</span></span>

<span data-ttu-id="e6437-130">To learn more about Advisor recommendations, see:</span><span class="sxs-lookup"><span data-stu-id="e6437-130">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="e6437-131">Introduction to Advisor</span><span class="sxs-lookup"><span data-stu-id="e6437-131">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="e6437-132">Get Started</span><span class="sxs-lookup"><span data-stu-id="e6437-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="e6437-133">Advisor Performance recommendations</span><span class="sxs-lookup"><span data-stu-id="e6437-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="e6437-134">Advisor High Availability recommendations</span><span class="sxs-lookup"><span data-stu-id="e6437-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="e6437-135">Advisor Security recommendations</span><span class="sxs-lookup"><span data-stu-id="e6437-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)



