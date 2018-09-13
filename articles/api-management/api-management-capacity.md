---
title: Capacity of an Azure API Management instance | Microsoft Docs
description: This article explains what the capacity metric is and how to make informed decisions whether to scale an Azure API Management instance.
services: api-management
documentationcenter: ''
author: mikebudzynski
manager: anneta
editor: ''
ms.service: api-management
ms.workload: integration
ms.topic: article
ms.date: 06/18/2018
ms.author: apimpm
ms.openlocfilehash: 4983854a14a6efe9214692dc677dedeada73933b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868316"
---
# <a name="capacity-of-an-azure-api-management-instance"></a><span data-ttu-id="2aaf2-103">Capacity of an Azure API Management instance</span><span class="sxs-lookup"><span data-stu-id="2aaf2-103">Capacity of an Azure API Management instance</span></span>

<span data-ttu-id="2aaf2-104">**Capacity** is the single, most important [Azure Monitor metric](api-management-howto-use-azure-monitor.md#view-metrics-of-your-apis) for making informed decisions whether to scale an API Management instance to accommodate more load.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-104">**Capacity** is the single, most important [Azure Monitor metric](api-management-howto-use-azure-monitor.md#view-metrics-of-your-apis) for making informed decisions whether to scale an API Management instance to accommodate more load.</span></span> <span data-ttu-id="2aaf2-105">Its construction is complex and imposes certain behavior.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-105">Its construction is complex and imposes certain behavior.</span></span>

<span data-ttu-id="2aaf2-106">This article explains what the **capacity** is and how it behaves.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-106">This article explains what the **capacity** is and how it behaves.</span></span> <span data-ttu-id="2aaf2-107">It shows how to access **capacity** metrics in the Azure portal and suggests when to consider scaling or upgrading your API Management instance.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-107">It shows how to access **capacity** metrics in the Azure portal and suggests when to consider scaling or upgrading your API Management instance.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2aaf2-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2aaf2-108">Prerequisites</span></span>

<span data-ttu-id="2aaf2-109">To follow the steps from this article, you must have:</span><span class="sxs-lookup"><span data-stu-id="2aaf2-109">To follow the steps from this article, you must have:</span></span>

+ <span data-ttu-id="2aaf2-110">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-110">An active Azure subscription.</span></span>

    [!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

+ <span data-ttu-id="2aaf2-111">An APIM instance.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-111">An APIM instance.</span></span> <span data-ttu-id="2aaf2-112">For more information, see [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="2aaf2-112">For more information, see [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>

## <a name="what-is-capacity"></a><span data-ttu-id="2aaf2-113">What is capacity</span><span class="sxs-lookup"><span data-stu-id="2aaf2-113">What is capacity</span></span>

![Capacity metric](./media/api-management-capacity/capacity-ingredients.png)

<span data-ttu-id="2aaf2-115">**Capacity** is an indicator of load on an APIM instance.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-115">**Capacity** is an indicator of load on an APIM instance.</span></span> <span data-ttu-id="2aaf2-116">It reflects resources usage (CPU, memory) and network queue lengths.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-116">It reflects resources usage (CPU, memory) and network queue lengths.</span></span> <span data-ttu-id="2aaf2-117">CPU and memory usage reveals resources consumption by:</span><span class="sxs-lookup"><span data-stu-id="2aaf2-117">CPU and memory usage reveals resources consumption by:</span></span>

+ <span data-ttu-id="2aaf2-118">APIM services, such as management actions or request processing, which can include forwarding requests or running a policy</span><span class="sxs-lookup"><span data-stu-id="2aaf2-118">APIM services, such as management actions or request processing, which can include forwarding requests or running a policy</span></span>
+ <span data-ttu-id="2aaf2-119">selected operating system processes, including processes that involve cost of SSL handshakes on new connections.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-119">selected operating system processes, including processes that involve cost of SSL handshakes on new connections.</span></span>

<span data-ttu-id="2aaf2-120">Total **capacity** is an average of its own values from every unit of an API Management instance.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-120">Total **capacity** is an average of its own values from every unit of an API Management instance.</span></span>

## <a name="capacity-metric-behavior"></a><span data-ttu-id="2aaf2-121">Capacity metric behavior</span><span class="sxs-lookup"><span data-stu-id="2aaf2-121">Capacity metric behavior</span></span>

<span data-ttu-id="2aaf2-122">Because of its construction, in real life **capacity** can be impacted by many variables, for example:</span><span class="sxs-lookup"><span data-stu-id="2aaf2-122">Because of its construction, in real life **capacity** can be impacted by many variables, for example:</span></span>

+ <span data-ttu-id="2aaf2-123">connection patterns (new connection on a request vs reusing the existing connection)</span><span class="sxs-lookup"><span data-stu-id="2aaf2-123">connection patterns (new connection on a request vs reusing the existing connection)</span></span>
+ <span data-ttu-id="2aaf2-124">size of a request and response</span><span class="sxs-lookup"><span data-stu-id="2aaf2-124">size of a request and response</span></span>
+ <span data-ttu-id="2aaf2-125">policies configured on each API or number of clients sending requests.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-125">policies configured on each API or number of clients sending requests.</span></span>

<span data-ttu-id="2aaf2-126">The more complex operations on the requests are, the higher the **capacity** consumption will be.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-126">The more complex operations on the requests are, the higher the **capacity** consumption will be.</span></span> <span data-ttu-id="2aaf2-127">For example, complex transformation policies consume much more CPU than a simple request forwarding.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-127">For example, complex transformation policies consume much more CPU than a simple request forwarding.</span></span> <span data-ttu-id="2aaf2-128">Slow backend service responses will increase it too.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-128">Slow backend service responses will increase it too.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2aaf2-129">**Capacity** is not a direct measure of the number of requests being processed.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-129">**Capacity** is not a direct measure of the number of requests being processed.</span></span>

![Capacity metric spikes](./media/api-management-capacity/capacity-spikes.png)

<span data-ttu-id="2aaf2-131">**Capacity** can also spike intermittently or be greater than zero even if there are no requests being processed.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-131">**Capacity** can also spike intermittently or be greater than zero even if there are no requests being processed.</span></span> <span data-ttu-id="2aaf2-132">It happens because of system- or platform-specific actions and should not be taken into consideration when deciding whether to scale an instance.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-132">It happens because of system- or platform-specific actions and should not be taken into consideration when deciding whether to scale an instance.</span></span>
  
## <a name="use-the-azure-portal-to-examine-capacity"></a><span data-ttu-id="2aaf2-133">Use the Azure Portal to examine capacity</span><span class="sxs-lookup"><span data-stu-id="2aaf2-133">Use the Azure Portal to examine capacity</span></span>
  
![Capacity metric](./media/api-management-capacity/capacity-metric.png)  

1. <span data-ttu-id="2aaf2-135">Navigate to your APIM instance in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2aaf2-135">Navigate to your APIM instance in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2aaf2-136">Select **Metrics (preview)**.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-136">Select **Metrics (preview)**.</span></span>
3. <span data-ttu-id="2aaf2-137">From the purple section, select **Capacity** metric from available metrics and leave the default **Avg** aggregation.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-137">From the purple section, select **Capacity** metric from available metrics and leave the default **Avg** aggregation.</span></span>

    > [!TIP]
    > <span data-ttu-id="2aaf2-138">You should always look at a **capacity** metric breakdown per location to avoid wrong interpretations.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-138">You should always look at a **capacity** metric breakdown per location to avoid wrong interpretations.</span></span>

4. <span data-ttu-id="2aaf2-139">From the green section, select **Location** for splitting the metric by dimension.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-139">From the green section, select **Location** for splitting the metric by dimension.</span></span>
5. <span data-ttu-id="2aaf2-140">Pick a desired timeframe from the top bar of the section.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-140">Pick a desired timeframe from the top bar of the section.</span></span>

    <span data-ttu-id="2aaf2-141">You can set a metric alert to let you know when something unexpected is happening.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-141">You can set a metric alert to let you know when something unexpected is happening.</span></span> <span data-ttu-id="2aaf2-142">For example, get notifications when your APIM instance has been exceededing its expected peak capacity for over 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-142">For example, get notifications when your APIM instance has been exceededing its expected peak capacity for over 20 minutes.</span></span>

    >[!TIP]
    > <span data-ttu-id="2aaf2-143">You can configure alerts to let you know when your service is running low on capacity or use Azure Monitor autoscaling functionality to automatically add an Azure API Management unit.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-143">You can configure alerts to let you know when your service is running low on capacity or use Azure Monitor autoscaling functionality to automatically add an Azure API Management unit.</span></span> <span data-ttu-id="2aaf2-144">Scaling operation can take around 30 minutes, so you should plan your rules accordingly.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-144">Scaling operation can take around 30 minutes, so you should plan your rules accordingly.</span></span>  
    > <span data-ttu-id="2aaf2-145">Only scaling the master location is allowed.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-145">Only scaling the master location is allowed.</span></span>

## <a name="use-capacity-for-scaling-decisions"></a><span data-ttu-id="2aaf2-146">Use capacity for scaling decisions</span><span class="sxs-lookup"><span data-stu-id="2aaf2-146">Use capacity for scaling decisions</span></span>

<span data-ttu-id="2aaf2-147">**Capacity** is the metric for making decisions whether to scale an API Management instance to accommodate more load.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-147">**Capacity** is the metric for making decisions whether to scale an API Management instance to accommodate more load.</span></span> <span data-ttu-id="2aaf2-148">Consider:</span><span class="sxs-lookup"><span data-stu-id="2aaf2-148">Consider:</span></span>

+ <span data-ttu-id="2aaf2-149">Looking at a long-term trend and average.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-149">Looking at a long-term trend and average.</span></span>
+ <span data-ttu-id="2aaf2-150">Ignoring sudden spikes that are most likely not related to any increase in load (see "Capacity metric behavior" section for explanation).</span><span class="sxs-lookup"><span data-stu-id="2aaf2-150">Ignoring sudden spikes that are most likely not related to any increase in load (see "Capacity metric behavior" section for explanation).</span></span>
+ <span data-ttu-id="2aaf2-151">Upgrading or scaling your instance, when **capacity**'s value exceeds 60% or 70% for a longer period of time (for example 30 minutes).</span><span class="sxs-lookup"><span data-stu-id="2aaf2-151">Upgrading or scaling your instance, when **capacity**'s value exceeds 60% or 70% for a longer period of time (for example 30 minutes).</span></span> <span data-ttu-id="2aaf2-152">Different values may work better for your service or scenario.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-152">Different values may work better for your service or scenario.</span></span>

>[!TIP]  
> <span data-ttu-id="2aaf2-153">If you are able to estimate your traffic beforehand, test your APIM instance on workloads you expect.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-153">If you are able to estimate your traffic beforehand, test your APIM instance on workloads you expect.</span></span> <span data-ttu-id="2aaf2-154">You can increase the request load on your tenant gradually and monitor what value of the capacity metric corresponds to your peak load.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-154">You can increase the request load on your tenant gradually and monitor what value of the capacity metric corresponds to your peak load.</span></span> <span data-ttu-id="2aaf2-155">Follow the steps from the previous section to use Azure portal to understand how much capacity is used at any given time.</span><span class="sxs-lookup"><span data-stu-id="2aaf2-155">Follow the steps from the previous section to use Azure portal to understand how much capacity is used at any given time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aaf2-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="2aaf2-156">Next steps</span></span>

[<span data-ttu-id="2aaf2-157">How to scale or upgrade an Azure API Management service instance</span><span class="sxs-lookup"><span data-stu-id="2aaf2-157">How to scale or upgrade an Azure API Management service instance</span></span>](upgrade-and-scale.md)