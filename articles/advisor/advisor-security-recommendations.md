---
title: Azure Advisor Security Recommendations | Microsoft Docs
description: Use Azure Advisor to help improve the security of your Azure deployments.
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
ms.openlocfilehash: 986b1563b923ae340e86b62f31696bbc2b8c54c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672371"
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="211a0-103">Advisor Security recommendations</span><span class="sxs-lookup"><span data-stu-id="211a0-103">Advisor Security recommendations</span></span>

<span data-ttu-id="211a0-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="211a0-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="211a0-105">It integrates with Azure Security Center to bring you security recommendations.</span><span class="sxs-lookup"><span data-stu-id="211a0-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="211a0-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span><span class="sxs-lookup"><span data-stu-id="211a0-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![The Advisor Security button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="211a0-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="211a0-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="211a0-109">It periodically analyzes the security state of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="211a0-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="211a0-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span><span class="sxs-lookup"><span data-stu-id="211a0-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="211a0-111">The recommendations guide you through the process of configuring the controls you need.</span><span class="sxs-lookup"><span data-stu-id="211a0-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![The Advisor Security tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="211a0-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="211a0-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="211a0-114">How to access Security recommendations in Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="211a0-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="211a0-115">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="211a0-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="211a0-116">In the left pane, click **More services**.</span><span class="sxs-lookup"><span data-stu-id="211a0-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="211a0-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="211a0-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="211a0-118">The Advisor dashboard is displayed.</span><span class="sxs-lookup"><span data-stu-id="211a0-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="211a0-119">On the Advisor dashboard, click the **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="211a0-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="211a0-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span><span class="sxs-lookup"><span data-stu-id="211a0-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="211a0-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span><span class="sxs-lookup"><span data-stu-id="211a0-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="211a0-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span><span class="sxs-lookup"><span data-stu-id="211a0-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="211a0-123">This is a *one-time operation*.</span><span class="sxs-lookup"><span data-stu-id="211a0-123">This is a *one-time operation*.</span></span> <span data-ttu-id="211a0-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span><span class="sxs-lookup"><span data-stu-id="211a0-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="211a0-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="211a0-125">Next steps</span></span>

<span data-ttu-id="211a0-126">To learn more about Advisor recommendations, see:</span><span class="sxs-lookup"><span data-stu-id="211a0-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="211a0-127">Introduction to Advisor</span><span class="sxs-lookup"><span data-stu-id="211a0-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="211a0-128">Get started with Advisor</span><span class="sxs-lookup"><span data-stu-id="211a0-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="211a0-129">Advisor Cost recommendations</span><span class="sxs-lookup"><span data-stu-id="211a0-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="211a0-130">Advisor Performance recommendations</span><span class="sxs-lookup"><span data-stu-id="211a0-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="211a0-131">Advisor High Availability recommendations</span><span class="sxs-lookup"><span data-stu-id="211a0-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 


