---
title: Get started with Azure Advisor | Microsoft Docs
description: Get started with Azure Advisor.
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: 8e2718b4144b5e77806a65b10fd623ec2594ee49
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671647"
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="3679a-103">Get started with Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="3679a-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="3679a-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span><span class="sxs-lookup"><span data-stu-id="3679a-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="3679a-105">Get Advisor recommendations</span><span class="sxs-lookup"><span data-stu-id="3679a-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="3679a-106">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3679a-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="3679a-107">In the left pane, click **More services**.</span><span class="sxs-lookup"><span data-stu-id="3679a-107">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="3679a-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="3679a-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="3679a-109">The Advisor dashboard is displayed.</span><span class="sxs-lookup"><span data-stu-id="3679a-109">The Advisor dashboard is displayed.</span></span>

   ![Access Azure Advisor using the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="3679a-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span><span class="sxs-lookup"><span data-stu-id="3679a-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span></span>  
<span data-ttu-id="3679a-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span><span class="sxs-lookup"><span data-stu-id="3679a-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="3679a-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span><span class="sxs-lookup"><span data-stu-id="3679a-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="3679a-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span><span class="sxs-lookup"><span data-stu-id="3679a-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="3679a-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span><span class="sxs-lookup"><span data-stu-id="3679a-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="3679a-116">This is a *one-time operation*.</span><span class="sxs-lookup"><span data-stu-id="3679a-116">This is a *one-time operation*.</span></span> <span data-ttu-id="3679a-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span><span class="sxs-lookup"><span data-stu-id="3679a-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Azure Advisor dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="3679a-119">Get Advisor recommendation details, and implement a solution</span><span class="sxs-lookup"><span data-stu-id="3679a-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="3679a-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span><span class="sxs-lookup"><span data-stu-id="3679a-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span></span> 

1. <span data-ttu-id="3679a-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="3679a-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3679a-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span><span class="sxs-lookup"><span data-stu-id="3679a-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="3679a-123">In the list of recommendations, click a recommendation that you want to review in detail.</span><span class="sxs-lookup"><span data-stu-id="3679a-123">In the list of recommendations, click a recommendation that you want to review in detail.</span></span>  
<span data-ttu-id="3679a-124">The **Recommendation** blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="3679a-124">The **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="3679a-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span><span class="sxs-lookup"><span data-stu-id="3679a-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![The Advisor Recommendation blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="3679a-127">Search for Advisor recommendations</span><span class="sxs-lookup"><span data-stu-id="3679a-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="3679a-128">You can search for recommendations for a particular subscription or resource group.</span><span class="sxs-lookup"><span data-stu-id="3679a-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="3679a-129">You can also search for recommendations by status.</span><span class="sxs-lookup"><span data-stu-id="3679a-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="3679a-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="3679a-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3679a-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span><span class="sxs-lookup"><span data-stu-id="3679a-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="3679a-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span><span class="sxs-lookup"><span data-stu-id="3679a-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Advisor search-filter criteria](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="3679a-134">Snooze or dismiss Advisor recommendations</span><span class="sxs-lookup"><span data-stu-id="3679a-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="3679a-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="3679a-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="3679a-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span><span class="sxs-lookup"><span data-stu-id="3679a-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="3679a-137">On the **Recommendation** blade, click **Snooze**.</span><span class="sxs-lookup"><span data-stu-id="3679a-137">On the **Recommendation** blade, click **Snooze**.</span></span>  

   ![Advisor recommendation action example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="3679a-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span><span class="sxs-lookup"><span data-stu-id="3679a-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3679a-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="3679a-140">Next steps</span></span>

<span data-ttu-id="3679a-141">To learn more about Advisor, see:</span><span class="sxs-lookup"><span data-stu-id="3679a-141">To learn more about Advisor, see:</span></span>
* [<span data-ttu-id="3679a-142">Introduction to Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="3679a-142">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="3679a-143">Advisor High Availability recommendations</span><span class="sxs-lookup"><span data-stu-id="3679a-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="3679a-144">Advisor Security recommendations</span><span class="sxs-lookup"><span data-stu-id="3679a-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="3679a-145">Advisor Performance recommendations</span><span class="sxs-lookup"><span data-stu-id="3679a-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="3679a-146">Advisor Cost recommendations</span><span class="sxs-lookup"><span data-stu-id="3679a-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)





