---
title: Migrate pricing tiers of endpoints from Custom Speech Service on Azure | Microsoft Docs
description: Learn how to migrate deployments from tiers S0 and S1 to S2 of Custom Speech Service endpoints in Cognitive Services.
services: cognitive-services
author: PanosPeriorellis
manager: onano
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 07/05/2017
ms.author: panosper
ms.openlocfilehash: 6d92459deb3464cd97c215cbf9a8320628b6da80
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966305"
---
# <a name="migrate-deployments-to-the-new-pricing-model"></a><span data-ttu-id="c7520-103">Migrate deployments to the new pricing model</span><span class="sxs-lookup"><span data-stu-id="c7520-103">Migrate deployments to the new pricing model</span></span>
<span data-ttu-id="c7520-104">As of July 2017, Custom Speech Service offers a [new pricing model](https://azure.microsoft.com/pricing/details/cognitive-services/custom-speech-service/).</span><span class="sxs-lookup"><span data-stu-id="c7520-104">As of July 2017, Custom Speech Service offers a [new pricing model](https://azure.microsoft.com/pricing/details/cognitive-services/custom-speech-service/).</span></span> <span data-ttu-id="c7520-105">The new model is *easier to understand*, *simpler to calculate costs*, and *more flexible* in terms of scaling.</span><span class="sxs-lookup"><span data-stu-id="c7520-105">The new model is *easier to understand*, *simpler to calculate costs*, and *more flexible* in terms of scaling.</span></span> <span data-ttu-id="c7520-106">For scaling, Microsoft has introduced the concept of a scale unit.</span><span class="sxs-lookup"><span data-stu-id="c7520-106">For scaling, Microsoft has introduced the concept of a scale unit.</span></span> <span data-ttu-id="c7520-107">Each scale unit can handle five concurrent requests.</span><span class="sxs-lookup"><span data-stu-id="c7520-107">Each scale unit can handle five concurrent requests.</span></span> <span data-ttu-id="c7520-108">The scaling for concurrent requests in the old model was set at 5 concurrent requests for tier S0, and it was set at 12 concurrent requests for tier S1.</span><span class="sxs-lookup"><span data-stu-id="c7520-108">The scaling for concurrent requests in the old model was set at 5 concurrent requests for tier S0, and it was set at 12 concurrent requests for tier S1.</span></span> <span data-ttu-id="c7520-109">We have opened these limits to offer you greater flexibility with your use-case requirements.</span><span class="sxs-lookup"><span data-stu-id="c7520-109">We have opened these limits to offer you greater flexibility with your use-case requirements.</span></span>

<span data-ttu-id="c7520-110">If you run an old S0 or S1 tier, we recommend that you migrate your existing deployments to the new S2 tier.</span><span class="sxs-lookup"><span data-stu-id="c7520-110">If you run an old S0 or S1 tier, we recommend that you migrate your existing deployments to the new S2 tier.</span></span> <span data-ttu-id="c7520-111">The new S2 tier covers both the S0 and S1 tiers.</span><span class="sxs-lookup"><span data-stu-id="c7520-111">The new S2 tier covers both the S0 and S1 tiers.</span></span> <span data-ttu-id="c7520-112">You can see the available options in the following figure:</span><span class="sxs-lookup"><span data-stu-id="c7520-112">You can see the available options in the following figure:</span></span>

![The "Choose your pricing tier" page](../../../media/cognitive-services/custom-speech-service/custom-speech-pricing-tier.png)

<span data-ttu-id="c7520-114">Microsoft handles the migration in a semi-automated way.</span><span class="sxs-lookup"><span data-stu-id="c7520-114">Microsoft handles the migration in a semi-automated way.</span></span> <span data-ttu-id="c7520-115">First, you trigger the migration by selecting the new pricing tier.</span><span class="sxs-lookup"><span data-stu-id="c7520-115">First, you trigger the migration by selecting the new pricing tier.</span></span> <span data-ttu-id="c7520-116">Then, we migrate your deployment automatically.</span><span class="sxs-lookup"><span data-stu-id="c7520-116">Then, we migrate your deployment automatically.</span></span>

<span data-ttu-id="c7520-117">The mapping from the old tiers to scale units is shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="c7520-117">The mapping from the old tiers to scale units is shown in the following table:</span></span>

| <span data-ttu-id="c7520-118">Tier</span><span class="sxs-lookup"><span data-stu-id="c7520-118">Tier</span></span> | <span data-ttu-id="c7520-119">Concurrent requests (old model)</span><span class="sxs-lookup"><span data-stu-id="c7520-119">Concurrent requests (old model)</span></span> | <span data-ttu-id="c7520-120">Migration</span><span class="sxs-lookup"><span data-stu-id="c7520-120">Migration</span></span> | <span data-ttu-id="c7520-121">Concurrent requests</span><span class="sxs-lookup"><span data-stu-id="c7520-121">Concurrent requests</span></span> |
|----- | ----- | ---- | ---- |
| <span data-ttu-id="c7520-122">S0</span><span class="sxs-lookup"><span data-stu-id="c7520-122">S0</span></span> |  <span data-ttu-id="c7520-123">5</span><span class="sxs-lookup"><span data-stu-id="c7520-123">5</span></span>   |   <span data-ttu-id="c7520-124">=> **S2** with 1 scale unit</span><span class="sxs-lookup"><span data-stu-id="c7520-124">=> **S2** with 1 scale unit</span></span> |   <span data-ttu-id="c7520-125">5</span><span class="sxs-lookup"><span data-stu-id="c7520-125">5</span></span> |
| <span data-ttu-id="c7520-126">S1</span><span class="sxs-lookup"><span data-stu-id="c7520-126">S1</span></span> |  <span data-ttu-id="c7520-127">12</span><span class="sxs-lookup"><span data-stu-id="c7520-127">12</span></span>  |   <span data-ttu-id="c7520-128">=> **S2** with 3 scale units</span><span class="sxs-lookup"><span data-stu-id="c7520-128">=> **S2** with 3 scale units</span></span> |  <span data-ttu-id="c7520-129">15</span><span class="sxs-lookup"><span data-stu-id="c7520-129">15</span></span> |

<span data-ttu-id="c7520-130">To migrate to the new tier, do the following:</span><span class="sxs-lookup"><span data-stu-id="c7520-130">To migrate to the new tier, do the following:</span></span>

## <a name="step-1-check-your-existing-deployment"></a><span data-ttu-id="c7520-131">Step 1: Check your existing deployment</span><span class="sxs-lookup"><span data-stu-id="c7520-131">Step 1: Check your existing deployment</span></span>
<span data-ttu-id="c7520-132">Go to the [Custom Speech Service portal](http://cris.ai), and check your existing deployments.</span><span class="sxs-lookup"><span data-stu-id="c7520-132">Go to the [Custom Speech Service portal](http://cris.ai), and check your existing deployments.</span></span> <span data-ttu-id="c7520-133">In our example, there are two deployments.</span><span class="sxs-lookup"><span data-stu-id="c7520-133">In our example, there are two deployments.</span></span> <span data-ttu-id="c7520-134">One deployment runs on an S0 tier, and the other deployment runs on an S1 tier.</span><span class="sxs-lookup"><span data-stu-id="c7520-134">One deployment runs on an S0 tier, and the other deployment runs on an S1 tier.</span></span> <span data-ttu-id="c7520-135">The deployments are shown in the **Deployment Options** column of the following table:</span><span class="sxs-lookup"><span data-stu-id="c7520-135">The deployments are shown in the **Deployment Options** column of the following table:</span></span>

![The Deployments page](../../../media/cognitive-services/custom-speech-service/custom-speech-deployments.png)

## <a name="step-2-select-your-new-pricing-tier-in-the-azure-portal"></a><span data-ttu-id="c7520-137">Step 2: Select your new pricing tier in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c7520-137">Step 2: Select your new pricing tier in the Azure portal</span></span>
1. <span data-ttu-id="c7520-138">Open a new browser tab, and sign in to the [Azure portal](http://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c7520-138">Open a new browser tab, and sign in to the [Azure portal](http://ms.portal.azure.com/).</span></span> 

2. <span data-ttu-id="c7520-139">In the **Cognitive Services** pane, in the **Subscriptions** list, select your custom speech subscription.</span><span class="sxs-lookup"><span data-stu-id="c7520-139">In the **Cognitive Services** pane, in the **Subscriptions** list, select your custom speech subscription.</span></span> 

3. <span data-ttu-id="c7520-140">In the pane for your subscription, select **Pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="c7520-140">In the pane for your subscription, select **Pricing tier**.</span></span>

    ![The "Pricing tier" link](../../../media/cognitive-services/custom-speech-service/custom-speech-update-tier.png)

4. <span data-ttu-id="c7520-142">On the **Choose your pricing tier** page, select **S2 Standard**.</span><span class="sxs-lookup"><span data-stu-id="c7520-142">On the **Choose your pricing tier** page, select **S2 Standard**.</span></span> <span data-ttu-id="c7520-143">This pricing tier is the new, simplified, and more flexible pricing tier.</span><span class="sxs-lookup"><span data-stu-id="c7520-143">This pricing tier is the new, simplified, and more flexible pricing tier.</span></span>

5. <span data-ttu-id="c7520-144">Select the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="c7520-144">Select the **Select** button.</span></span>

    ![The "Choose your pricing tier" page](../../../media/cognitive-services/custom-speech-service/custom-speech-update-pricing.png)

## <a name="step-3-check-the-migration-status-in-the-custom-speech-service-portal"></a><span data-ttu-id="c7520-146">Step 3: Check the migration status in the Custom Speech Service portal</span><span class="sxs-lookup"><span data-stu-id="c7520-146">Step 3: Check the migration status in the Custom Speech Service portal</span></span>
<span data-ttu-id="c7520-147">Return to the Custom Speech Service portal, and check your deployments.</span><span class="sxs-lookup"><span data-stu-id="c7520-147">Return to the Custom Speech Service portal, and check your deployments.</span></span> <span data-ttu-id="c7520-148">(If your browser window is still open, refresh it.)</span><span class="sxs-lookup"><span data-stu-id="c7520-148">(If your browser window is still open, refresh it.)</span></span> 

<span data-ttu-id="c7520-149">The status of the related deployment should have switched to *Processing*.</span><span class="sxs-lookup"><span data-stu-id="c7520-149">The status of the related deployment should have switched to *Processing*.</span></span> <span data-ttu-id="c7520-150">You can also validate the migration by checking the **Deployment Options** column.</span><span class="sxs-lookup"><span data-stu-id="c7520-150">You can also validate the migration by checking the **Deployment Options** column.</span></span> <span data-ttu-id="c7520-151">There you can now find information about scale units and logging.</span><span class="sxs-lookup"><span data-stu-id="c7520-151">There you can now find information about scale units and logging.</span></span> <span data-ttu-id="c7520-152">The scale units should reflect your previous pricing tier.</span><span class="sxs-lookup"><span data-stu-id="c7520-152">The scale units should reflect your previous pricing tier.</span></span> <span data-ttu-id="c7520-153">The logging should also be turned on, as shown in the table:</span><span class="sxs-lookup"><span data-stu-id="c7520-153">The logging should also be turned on, as shown in the table:</span></span>

![The Deployment Options column](../../../media/cognitive-services/custom-speech-service/custom-speech-deployments-new.png)


> [!NOTE]
> <span data-ttu-id="c7520-155">If you have any problems during the migration, contact us.</span><span class="sxs-lookup"><span data-stu-id="c7520-155">If you have any problems during the migration, contact us.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="c7520-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7520-156">Next steps</span></span>
<span data-ttu-id="c7520-157">For more tutorials, see:</span><span class="sxs-lookup"><span data-stu-id="c7520-157">For more tutorials, see:</span></span>
* [<span data-ttu-id="c7520-158">Create a custom acoustic model</span><span class="sxs-lookup"><span data-stu-id="c7520-158">Create a custom acoustic model</span></span>](cognitive-services-custom-speech-create-acoustic-model.md)
* [<span data-ttu-id="c7520-159">Create a custom language model</span><span class="sxs-lookup"><span data-stu-id="c7520-159">Create a custom language model</span></span>](cognitive-services-custom-speech-create-language-model.md)
* [<span data-ttu-id="c7520-160">Create a custom speech-to-text endpoint</span><span class="sxs-lookup"><span data-stu-id="c7520-160">Create a custom speech-to-text endpoint</span></span>](cognitive-services-custom-speech-create-endpoint.md)
