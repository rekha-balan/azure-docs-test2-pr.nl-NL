---
title: Introduction to Azure Advisor | Microsoft Docs
description: Use Azure Advisor to optimize your Azure deployments.
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
ms.openlocfilehash: a2eaad6926d9e0c73257246868ef914b0ca2a66d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548744"
---
# <a name="introduction-to-azure-advisor"></a><span data-ttu-id="93052-103">Introduction to Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="93052-103">Introduction to Azure Advisor</span></span>

<span data-ttu-id="93052-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span><span class="sxs-lookup"><span data-stu-id="93052-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="93052-105">What is Advisor?</span><span class="sxs-lookup"><span data-stu-id="93052-105">What is Advisor?</span></span>
<span data-ttu-id="93052-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span><span class="sxs-lookup"><span data-stu-id="93052-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span></span> <span data-ttu-id="93052-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="93052-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="93052-108">With Advisor, you can:</span><span class="sxs-lookup"><span data-stu-id="93052-108">With Advisor, you can:</span></span>
* <span data-ttu-id="93052-109">Get proactive, actionable, and personalized best practices recommendations.</span><span class="sxs-lookup"><span data-stu-id="93052-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="93052-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span><span class="sxs-lookup"><span data-stu-id="93052-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span></span>
* <span data-ttu-id="93052-111">Get recommendations with proposed actions inline.</span><span class="sxs-lookup"><span data-stu-id="93052-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="93052-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="93052-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="93052-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="93052-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="93052-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span><span class="sxs-lookup"><span data-stu-id="93052-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="93052-115">The recommendations are divided into four categories:</span><span class="sxs-lookup"><span data-stu-id="93052-115">The recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="93052-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span><span class="sxs-lookup"><span data-stu-id="93052-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="93052-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="93052-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="93052-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span><span class="sxs-lookup"><span data-stu-id="93052-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span></span> <span data-ttu-id="93052-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="93052-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="93052-120">**Performance**: To improve the speed of your applications.</span><span class="sxs-lookup"><span data-stu-id="93052-120">**Performance**: To improve the speed of your applications.</span></span> <span data-ttu-id="93052-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="93052-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="93052-122">**Cost**: To optimize and reduce your overall Azure spend.</span><span class="sxs-lookup"><span data-stu-id="93052-122">**Cost**: To optimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="93052-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="93052-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![Advisor recommendation types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="93052-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span><span class="sxs-lookup"><span data-stu-id="93052-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="93052-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span><span class="sxs-lookup"><span data-stu-id="93052-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="93052-127">This is a *one-time operation*.</span><span class="sxs-lookup"><span data-stu-id="93052-127">This is a *one-time operation*.</span></span> <span data-ttu-id="93052-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span><span class="sxs-lookup"><span data-stu-id="93052-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="93052-129">You can click a recommendation to learn more about it.</span><span class="sxs-lookup"><span data-stu-id="93052-129">You can click a recommendation to learn more about it.</span></span> <span data-ttu-id="93052-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span><span class="sxs-lookup"><span data-stu-id="93052-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="93052-131">Advisor offers recommendations with inline actions or documentation links.</span><span class="sxs-lookup"><span data-stu-id="93052-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="93052-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span><span class="sxs-lookup"><span data-stu-id="93052-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span></span> <span data-ttu-id="93052-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span><span class="sxs-lookup"><span data-stu-id="93052-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span></span> 

<span data-ttu-id="93052-134">Advisor updates recommendations hourly.</span><span class="sxs-lookup"><span data-stu-id="93052-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="93052-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span><span class="sxs-lookup"><span data-stu-id="93052-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="93052-136">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="93052-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="93052-137">How do I access Advisor?</span><span class="sxs-lookup"><span data-stu-id="93052-137">How do I access Advisor?</span></span>
<span data-ttu-id="93052-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="93052-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="93052-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="93052-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="93052-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span><span class="sxs-lookup"><span data-stu-id="93052-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="93052-141">You can also view Advisor recommendations through the virtual machine resource blade.</span><span class="sxs-lookup"><span data-stu-id="93052-141">You can also view Advisor recommendations through the virtual machine resource blade.</span></span> <span data-ttu-id="93052-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span><span class="sxs-lookup"><span data-stu-id="93052-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span></span> 

### <a name="what-permissions-do-i-need-to-access-advisor"></a><span data-ttu-id="93052-143">What permissions do I need to access Advisor?</span><span class="sxs-lookup"><span data-stu-id="93052-143">What permissions do I need to access Advisor?</span></span>

<span data-ttu-id="93052-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span><span class="sxs-lookup"><span data-stu-id="93052-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="93052-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span><span class="sxs-lookup"><span data-stu-id="93052-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="93052-146">This is a *one-time operation*.</span><span class="sxs-lookup"><span data-stu-id="93052-146">This is a *one-time operation*.</span></span> <span data-ttu-id="93052-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span><span class="sxs-lookup"><span data-stu-id="93052-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="93052-148">How often are Advisor recommendations updated?</span><span class="sxs-lookup"><span data-stu-id="93052-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="93052-149">Advisor recommendations are updated hourly.</span><span class="sxs-lookup"><span data-stu-id="93052-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="93052-150">What resources does Advisor provide recommendations for?</span><span class="sxs-lookup"><span data-stu-id="93052-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="93052-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="93052-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="93052-152">Can I snooze or dismiss a recommendation?</span><span class="sxs-lookup"><span data-stu-id="93052-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="93052-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span><span class="sxs-lookup"><span data-stu-id="93052-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span></span> <span data-ttu-id="93052-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span><span class="sxs-lookup"><span data-stu-id="93052-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93052-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="93052-155">Next steps</span></span>

<span data-ttu-id="93052-156">To learn more about Advisor recommendations, see:</span><span class="sxs-lookup"><span data-stu-id="93052-156">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="93052-157">Get started with Advisor</span><span class="sxs-lookup"><span data-stu-id="93052-157">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="93052-158">Advisor High Availability recommendations</span><span class="sxs-lookup"><span data-stu-id="93052-158">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="93052-159">Advisor Security recommendations</span><span class="sxs-lookup"><span data-stu-id="93052-159">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
* [<span data-ttu-id="93052-160">Advisor Performance recommendations</span><span class="sxs-lookup"><span data-stu-id="93052-160">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="93052-161">Advisor Cost recommendations</span><span class="sxs-lookup"><span data-stu-id="93052-161">Advisor Cost recommendations</span></span>](advisor-cost-recommendations.md)

