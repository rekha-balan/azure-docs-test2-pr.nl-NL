---
title: Managing partner solutions in Azure Security Center | Microsoft Docs
description: This document walks you through how Azure Security Center lets you monitor at a glance the health status of your partner solutions integrated with your Azure subscription.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 74b495e0365823d839ce47bd390601f930cca240
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549269"
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="8d827-103">Monitoring partner solutions with Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8d827-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="8d827-104">This document walks you through how to monitor the health status of your partner solutions in Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="8d827-104">This document walks you through how to monitor the health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="8d827-105">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="8d827-105">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="8d827-106">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="8d827-106">This is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="8d827-107">Monitoring partner solutions</span><span class="sxs-lookup"><span data-stu-id="8d827-107">Monitoring partner solutions</span></span>
<span data-ttu-id="8d827-108">The **Partner solutions** tile on the **Security Center** blade lets you monitor at a glance the health status of your partner solutions integrated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8d827-108">The **Partner solutions** tile on the **Security Center** blade lets you monitor at a glance the health status of your partner solutions integrated with your Azure subscription.</span></span>

![Partner solutions tile][1]

<span data-ttu-id="8d827-110">The **Partner solutions** tile displays the number of partner solutions and a status summary for those solutions.</span><span class="sxs-lookup"><span data-stu-id="8d827-110">The **Partner solutions** tile displays the number of partner solutions and a status summary for those solutions.</span></span>

<span data-ttu-id="8d827-111">The **STATUS** of a partner solution can be:</span><span class="sxs-lookup"><span data-stu-id="8d827-111">The **STATUS** of a partner solution can be:</span></span>

* <span data-ttu-id="8d827-112">Protected (green) - there is no health issue.</span><span class="sxs-lookup"><span data-stu-id="8d827-112">Protected (green) - there is no health issue.</span></span>
* <span data-ttu-id="8d827-113">Unhealthy (red) - there is a health issue that requires immediate attention.</span><span class="sxs-lookup"><span data-stu-id="8d827-113">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
* <span data-ttu-id="8d827-114">Stopped reporting (orange) - the solution has stopped reporting its health.</span><span class="sxs-lookup"><span data-stu-id="8d827-114">Stopped reporting (orange) - the solution has stopped reporting its health.</span></span>
* <span data-ttu-id="8d827-115">Unknown protection status (orange) - the health of the solution is unknown at this time due to a failed process of adding a new resource to the existing solution.</span><span class="sxs-lookup"><span data-stu-id="8d827-115">Unknown protection status (orange) - the health of the solution is unknown at this time due to a failed process of adding a new resource to the existing solution.</span></span>
* <span data-ttu-id="8d827-116">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has just been connected and is still deploying.</span><span class="sxs-lookup"><span data-stu-id="8d827-116">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has just been connected and is still deploying.</span></span>

<span data-ttu-id="8d827-117">If there are no solutions integrated with your subscription the tile will state that there are no solutions.</span><span class="sxs-lookup"><span data-stu-id="8d827-117">If there are no solutions integrated with your subscription the tile will state that there are no solutions.</span></span> <span data-ttu-id="8d827-118">Selecting the **Partner solutions** tile will enable you to open the **Recommendations** blade to deploy partner security solutions.</span><span class="sxs-lookup"><span data-stu-id="8d827-118">Selecting the **Partner solutions** tile will enable you to open the **Recommendations** blade to deploy partner security solutions.</span></span>

![No partner solutions][2]

<span data-ttu-id="8d827-120">To view the health of your partner solutions:</span><span class="sxs-lookup"><span data-stu-id="8d827-120">To view the health of your partner solutions:</span></span>

1. <span data-ttu-id="8d827-121">Select the **Partner solutions** tile.</span><span class="sxs-lookup"><span data-stu-id="8d827-121">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="8d827-122">A blade opens displaying a list of your partner solutions connected to Security Center.</span><span class="sxs-lookup"><span data-stu-id="8d827-122">A blade opens displaying a list of your partner solutions connected to Security Center.</span></span>

   ![Partner solutions][3]
2. <span data-ttu-id="8d827-124">Select a partner solution.</span><span class="sxs-lookup"><span data-stu-id="8d827-124">Select a partner solution.</span></span> <span data-ttu-id="8d827-125">In this example, lets select the **F5-WAF2** solution.</span><span class="sxs-lookup"><span data-stu-id="8d827-125">In this example, lets select the **F5-WAF2** solution.</span></span>  <span data-ttu-id="8d827-126">A blade opens showing you the status of the partner solution and the solution's associated resources.</span><span class="sxs-lookup"><span data-stu-id="8d827-126">A blade opens showing you the status of the partner solution and the solution's associated resources.</span></span> <span data-ttu-id="8d827-127">Select **Solution console** to open the partner management experience for this solution.</span><span class="sxs-lookup"><span data-stu-id="8d827-127">Select **Solution console** to open the partner management experience for this solution.</span></span>

   ![Partner solution detail][4]
3. <span data-ttu-id="8d827-129">Go back to the **F5-WAF2** blade and select **Link app**.</span><span class="sxs-lookup"><span data-stu-id="8d827-129">Go back to the **F5-WAF2** blade and select **Link app**.</span></span> <span data-ttu-id="8d827-130">The **Link Applications** blade opens.</span><span class="sxs-lookup"><span data-stu-id="8d827-130">The **Link Applications** blade opens.</span></span> <span data-ttu-id="8d827-131">Here you can connect resources to the partner solution.</span><span class="sxs-lookup"><span data-stu-id="8d827-131">Here you can connect resources to the partner solution.</span></span>

   ![Link resources to partner solution][5]

## <a name="see-also"></a><span data-ttu-id="8d827-133">See also</span><span class="sxs-lookup"><span data-stu-id="8d827-133">See also</span></span>
<span data-ttu-id="8d827-134">In this document, you were introduced to the **Partner Solutions** tile in Security Center.</span><span class="sxs-lookup"><span data-stu-id="8d827-134">In this document, you were introduced to the **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="8d827-135">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="8d827-135">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="8d827-136">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="8d827-136">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8d827-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="8d827-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="8d827-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="8d827-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="8d827-139">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="8d827-139">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="8d827-140">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="8d827-140">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="8d827-141">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="8d827-141">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/partner-solutions-tile.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/no-partner-solutions-to-display.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/partner-solutions.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/partner-solutions-detail.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/link-applications.png





