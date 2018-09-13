---
title: Manage Azure endpoint subscription | Microsoft Docs
description: In this article, you create a metered endpoint key for your LUIS account to provide unlimited traffic to your endpoint following a payment plan.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/21/2018
ms.author: diberry
ms.openlocfilehash: 0b735499ae589e44c2ce5076fce38ec47ddd69c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867137"
---
# <a name="manage-azure-endpoint-subscription-keys"></a><span data-ttu-id="c37b6-103">Manage Azure endpoint subscription keys</span><span class="sxs-lookup"><span data-stu-id="c37b6-103">Manage Azure endpoint subscription keys</span></span>

<span data-ttu-id="c37b6-104">For testing and prototype only, use the free (F0) tier.</span><span class="sxs-lookup"><span data-stu-id="c37b6-104">For testing and prototype only, use the free (F0) tier.</span></span> <span data-ttu-id="c37b6-105">For production systems, use a [paid](https://aka.ms/luis-price-tier) tier.</span><span class="sxs-lookup"><span data-stu-id="c37b6-105">For production systems, use a [paid](https://aka.ms/luis-price-tier) tier.</span></span> 

> [!NOTE]
> <span data-ttu-id="c37b6-106">Do not use the [authoring key](luis-concept-keys.md#authoring-key) for endpoint queries in production.</span><span class="sxs-lookup"><span data-stu-id="c37b6-106">Do not use the [authoring key](luis-concept-keys.md#authoring-key) for endpoint queries in production.</span></span>

<a name="create-luis-service"></a>
## <a name="create-luis-endpoint-key"></a><span data-ttu-id="c37b6-107">Create LUIS endpoint key</span><span class="sxs-lookup"><span data-stu-id="c37b6-107">Create LUIS endpoint key</span></span>

1. <span data-ttu-id="c37b6-108">Sign in to **[Microsoft Azure](https://ms.portal.azure.com/)**</span><span class="sxs-lookup"><span data-stu-id="c37b6-108">Sign in to **[Microsoft Azure](https://ms.portal.azure.com/)**</span></span> 
2. <span data-ttu-id="c37b6-109">Click the green **+** sign in the upper left-hand panel and search for “LUIS” in the marketplace, then click on **Language Understanding** and follow the **create experience** to create a LUIS subscription account.</span><span class="sxs-lookup"><span data-stu-id="c37b6-109">Click the green **+** sign in the upper left-hand panel and search for “LUIS” in the marketplace, then click on **Language Understanding** and follow the **create experience** to create a LUIS subscription account.</span></span> 

    ![Azure Search](./media/luis-azure-subscription/azure-search.png) 

3. <span data-ttu-id="c37b6-111">Configure the subscription with settings including account name, pricing tiers, etc.</span><span class="sxs-lookup"><span data-stu-id="c37b6-111">Configure the subscription with settings including account name, pricing tiers, etc.</span></span> 

    ![Azure API Choice](./media/luis-azure-subscription/azure-api-choice.png) 

4. <span data-ttu-id="c37b6-113">Once you create the LUIS service, you can view the access keys generated in **Resource Management->Keys**.</span><span class="sxs-lookup"><span data-stu-id="c37b6-113">Once you create the LUIS service, you can view the access keys generated in **Resource Management->Keys**.</span></span>  

    ![Azure Keys](./media/luis-azure-subscription/azure-keys.png)

    > [!Note] 
    > * <span data-ttu-id="c37b6-115">Log into your region's [LUIS](luis-reference-regions.md) website and [add the new LUIS endpoint key](luis-how-to-manage-keys.md#assign-endpoint-key).</span><span class="sxs-lookup"><span data-stu-id="c37b6-115">Log into your region's [LUIS](luis-reference-regions.md) website and [add the new LUIS endpoint key](luis-how-to-manage-keys.md#assign-endpoint-key).</span></span> 
    > * <span data-ttu-id="c37b6-116">You need to remember the name of the Azure service you created in order to select it on the region's [LUIS](luis-reference-regions.md) publish page.</span><span class="sxs-lookup"><span data-stu-id="c37b6-116">You need to remember the name of the Azure service you created in order to select it on the region's [LUIS](luis-reference-regions.md) publish page.</span></span>  

## <a name="change-luis-pricing-tier"></a><span data-ttu-id="c37b6-117">Change LUIS pricing tier</span><span class="sxs-lookup"><span data-stu-id="c37b6-117">Change LUIS pricing tier</span></span>

1.  <span data-ttu-id="c37b6-118">In [Azure](https://portal.azure.com), find your LUIS subscription.</span><span class="sxs-lookup"><span data-stu-id="c37b6-118">In [Azure](https://portal.azure.com), find your LUIS subscription.</span></span> <span data-ttu-id="c37b6-119">Click the LUIS subscription.</span><span class="sxs-lookup"><span data-stu-id="c37b6-119">Click the LUIS subscription.</span></span>
    <span data-ttu-id="c37b6-120">![Find your LUIS subscription](./media/luis-usage-tiers/find.png)</span><span class="sxs-lookup"><span data-stu-id="c37b6-120">![Find your LUIS subscription](./media/luis-usage-tiers/find.png)</span></span>
2.  <span data-ttu-id="c37b6-121">Click **Pricing tier** in order to see the available pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="c37b6-121">Click **Pricing tier** in order to see the available pricing tiers.</span></span> 
    <span data-ttu-id="c37b6-122">![View pricing tiers](./media/luis-usage-tiers/subscription.png)</span><span class="sxs-lookup"><span data-stu-id="c37b6-122">![View pricing tiers](./media/luis-usage-tiers/subscription.png)</span></span>
3.  <span data-ttu-id="c37b6-123">Click the pricing tier and click **Select** to save your change.</span><span class="sxs-lookup"><span data-stu-id="c37b6-123">Click the pricing tier and click **Select** to save your change.</span></span> 
    <span data-ttu-id="c37b6-124">![Change your LUIS payment tier](./media/luis-usage-tiers/plans.png)</span><span class="sxs-lookup"><span data-stu-id="c37b6-124">![Change your LUIS payment tier](./media/luis-usage-tiers/plans.png)</span></span>
4.  <span data-ttu-id="c37b6-125">When the pricing change is complete, a pop-up window verifies the new pricing tier.</span><span class="sxs-lookup"><span data-stu-id="c37b6-125">When the pricing change is complete, a pop-up window verifies the new pricing tier.</span></span> 
    <span data-ttu-id="c37b6-126">![Verify your LUIS payment tier](./media/luis-usage-tiers/updated.png)</span><span class="sxs-lookup"><span data-stu-id="c37b6-126">![Verify your LUIS payment tier](./media/luis-usage-tiers/updated.png)</span></span>
5. <span data-ttu-id="c37b6-127">Remember to [assign this endpoint key](luis-how-to-manage-keys.md#assign-endpoint-key) on the **Publish** page and use it in all endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="c37b6-127">Remember to [assign this endpoint key](luis-how-to-manage-keys.md#assign-endpoint-key) on the **Publish** page and use it in all endpoint queries.</span></span> 

## <a name="exceed-pricing-tier-usage"></a><span data-ttu-id="c37b6-128">Exceed pricing tier usage</span><span class="sxs-lookup"><span data-stu-id="c37b6-128">Exceed pricing tier usage</span></span>
<span data-ttu-id="c37b6-129">Each tier allows endpoint requests to your LUIS account at a specific rate.</span><span class="sxs-lookup"><span data-stu-id="c37b6-129">Each tier allows endpoint requests to your LUIS account at a specific rate.</span></span> <span data-ttu-id="c37b6-130">If the rate of requests is higher than the allowed rate of your metered account per minute or per month, requests receive an HTTP error of "429: Too Many Requests."</span><span class="sxs-lookup"><span data-stu-id="c37b6-130">If the rate of requests is higher than the allowed rate of your metered account per minute or per month, requests receive an HTTP error of "429: Too Many Requests."</span></span>

<span data-ttu-id="c37b6-131">Each tier allows accumulative requests per month.</span><span class="sxs-lookup"><span data-stu-id="c37b6-131">Each tier allows accumulative requests per month.</span></span> <span data-ttu-id="c37b6-132">If the total requests are higher than the allowed rate, requests receive an HTTP error of "403: forbidden".</span><span class="sxs-lookup"><span data-stu-id="c37b6-132">If the total requests are higher than the allowed rate, requests receive an HTTP error of "403: forbidden".</span></span>  

## <a name="viewing-summary-usage"></a><span data-ttu-id="c37b6-133">Viewing summary usage</span><span class="sxs-lookup"><span data-stu-id="c37b6-133">Viewing summary usage</span></span>
<span data-ttu-id="c37b6-134">You can view LUIS usage information in Azure.</span><span class="sxs-lookup"><span data-stu-id="c37b6-134">You can view LUIS usage information in Azure.</span></span> <span data-ttu-id="c37b6-135">The **Overview** page shows recent summary information including calls and errors.</span><span class="sxs-lookup"><span data-stu-id="c37b6-135">The **Overview** page shows recent summary information including calls and errors.</span></span> <span data-ttu-id="c37b6-136">If you make a LUIS endpoint request, then immediately watch the **Overview page**, allow up to five minutes for the usage to show up.</span><span class="sxs-lookup"><span data-stu-id="c37b6-136">If you make a LUIS endpoint request, then immediately watch the **Overview page**, allow up to five minutes for the usage to show up.</span></span>

![Viewing summary usage](./media/luis-usage-tiers/overview.png)

## <a name="customizing-usage-charts"></a><span data-ttu-id="c37b6-138">Customizing usage charts</span><span class="sxs-lookup"><span data-stu-id="c37b6-138">Customizing usage charts</span></span>
<span data-ttu-id="c37b6-139">Metrics provides a more detailed view into the data.</span><span class="sxs-lookup"><span data-stu-id="c37b6-139">Metrics provides a more detailed view into the data.</span></span>

![Default metrics](./media/luis-usage-tiers/metrics-default.png)

<span data-ttu-id="c37b6-141">You can configure your metrics charts for time period and metric type.</span><span class="sxs-lookup"><span data-stu-id="c37b6-141">You can configure your metrics charts for time period and metric type.</span></span> 

![Custom metrics](./media/luis-usage-tiers/metrics-custom.png)

## <a name="total-transactions-threshold-alert"></a><span data-ttu-id="c37b6-143">Total transactions threshold alert</span><span class="sxs-lookup"><span data-stu-id="c37b6-143">Total transactions threshold alert</span></span>
<span data-ttu-id="c37b6-144">If you would like to know when you have reached a certain transaction threshold, for example 10,000 transactions, you can create an alert.</span><span class="sxs-lookup"><span data-stu-id="c37b6-144">If you would like to know when you have reached a certain transaction threshold, for example 10,000 transactions, you can create an alert.</span></span> 

![Default alerts](./media/luis-usage-tiers/alert-default.png)

<span data-ttu-id="c37b6-146">Add a metric alert for the **total calls** metric for a certain time period.</span><span class="sxs-lookup"><span data-stu-id="c37b6-146">Add a metric alert for the **total calls** metric for a certain time period.</span></span> <span data-ttu-id="c37b6-147">Add email addresses of all people that should receive the alert.</span><span class="sxs-lookup"><span data-stu-id="c37b6-147">Add email addresses of all people that should receive the alert.</span></span> <span data-ttu-id="c37b6-148">Add webhooks for all systems that should receive the alert.</span><span class="sxs-lookup"><span data-stu-id="c37b6-148">Add webhooks for all systems that should receive the alert.</span></span> <span data-ttu-id="c37b6-149">You can also run a logic app when the alert is triggered.</span><span class="sxs-lookup"><span data-stu-id="c37b6-149">You can also run a logic app when the alert is triggered.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c37b6-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="c37b6-150">Next steps</span></span>

<span data-ttu-id="c37b6-151">Learn how to use [versions](luis-how-to-manage-versions.md) to manage changes to your LUIS app.</span><span class="sxs-lookup"><span data-stu-id="c37b6-151">Learn how to use [versions](luis-how-to-manage-versions.md) to manage changes to your LUIS app.</span></span>