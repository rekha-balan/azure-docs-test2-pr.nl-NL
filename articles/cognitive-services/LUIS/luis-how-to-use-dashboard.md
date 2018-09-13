---
title: Application dashboard for LUIS apps | Microsoft Docs
description: Learn about the application dashboard, a visualized reporting tool that enables you to monitor your apps at a single glance.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/01/2018
ms.author: diberry
ms.openlocfilehash: 518227d9f4165a08fafefa357de255d97c710f61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871464"
---
# <a name="application-dashboard"></a><span data-ttu-id="8b36e-103">Application Dashboard</span><span class="sxs-lookup"><span data-stu-id="8b36e-103">Application Dashboard</span></span>
<span data-ttu-id="8b36e-104">The app dashboard enables you to monitor your app at a single glance.</span><span class="sxs-lookup"><span data-stu-id="8b36e-104">The app dashboard enables you to monitor your app at a single glance.</span></span> <span data-ttu-id="8b36e-105">The **Dashboard** displays when you open an app by clicking the application name on **My Apps** page then select **Dashboard** from top panel.</span><span class="sxs-lookup"><span data-stu-id="8b36e-105">The **Dashboard** displays when you open an app by clicking the application name on **My Apps** page then select **Dashboard** from top panel.</span></span> 

> [!CAUTION]
> <span data-ttu-id="8b36e-106">If you want the most up-to-date metrics for LUIS, you need to:</span><span class="sxs-lookup"><span data-stu-id="8b36e-106">If you want the most up-to-date metrics for LUIS, you need to:</span></span>
> * <span data-ttu-id="8b36e-107">Use a LUIS [endpoint key](luis-how-to-azure-subscription.md) created in Azure</span><span class="sxs-lookup"><span data-stu-id="8b36e-107">Use a LUIS [endpoint key](luis-how-to-azure-subscription.md) created in Azure</span></span>
> * <span data-ttu-id="8b36e-108">Use LUIS endpoint key for all endpoint requests including LUIS [API](https://aka.ms/luis-endpoint-apis) and bot</span><span class="sxs-lookup"><span data-stu-id="8b36e-108">Use LUIS endpoint key for all endpoint requests including LUIS [API](https://aka.ms/luis-endpoint-apis) and bot</span></span>
> * <span data-ttu-id="8b36e-109">Use different endpoint key for each LUIS app.</span><span class="sxs-lookup"><span data-stu-id="8b36e-109">Use different endpoint key for each LUIS app.</span></span> <span data-ttu-id="8b36e-110">Do not use a single endpoint key for all apps.</span><span class="sxs-lookup"><span data-stu-id="8b36e-110">Do not use a single endpoint key for all apps.</span></span> <span data-ttu-id="8b36e-111">The endpoint key is tracked at the key level, not at the app level.</span><span class="sxs-lookup"><span data-stu-id="8b36e-111">The endpoint key is tracked at the key level, not at the app level.</span></span>  

<span data-ttu-id="8b36e-112">The **Dashboard** page gives you an overview of the LUIS app including the current model state as well as [endpoint](luis-glossary.md#endpoint) usage over time.</span><span class="sxs-lookup"><span data-stu-id="8b36e-112">The **Dashboard** page gives you an overview of the LUIS app including the current model state as well as [endpoint](luis-glossary.md#endpoint) usage over time.</span></span> <!--The following image shows the **Dashboard** page.-->

<!-- TBD: Get a working screen shot
![The Dashboard](./media/luis-how-to-use-dashboard/dashboard.png)
-->

<!-- TBD: IS THIS STILL TRUE?
At the top of the **Dashboard** page, a contextual notification bar constantly displays notifications to update you on the required or recommended actions appropriate for the current state of your app. It also provides useful tips and alerts as needed. A detailed description of the data reported on the **Dashboard** page follows.
-->
  
## <a name="app-status"></a><span data-ttu-id="8b36e-113">App status</span><span class="sxs-lookup"><span data-stu-id="8b36e-113">App status</span></span>
<span data-ttu-id="8b36e-114">The dashboard displays the application's training and publishing status, including the date and time when the app was last trained and published.</span><span class="sxs-lookup"><span data-stu-id="8b36e-114">The dashboard displays the application's training and publishing status, including the date and time when the app was last trained and published.</span></span>  

![Dashboard - App Status](./media/luis-how-to-use-dashboard/app-state.png)

## <a name="model-data-statistics"></a><span data-ttu-id="8b36e-116">Model data statistics</span><span class="sxs-lookup"><span data-stu-id="8b36e-116">Model data statistics</span></span>
<span data-ttu-id="8b36e-117">The dashboard displays the total numbers of intents, entities, and labeled utterances existing in the app.</span><span class="sxs-lookup"><span data-stu-id="8b36e-117">The dashboard displays the total numbers of intents, entities, and labeled utterances existing in the app.</span></span> 

![App Data Statistics](./media/luis-how-to-use-dashboard/app-model-count.png)

## <a name="endpoint-hits"></a><span data-ttu-id="8b36e-119">Endpoint hits</span><span class="sxs-lookup"><span data-stu-id="8b36e-119">Endpoint hits</span></span>
<span data-ttu-id="8b36e-120">The dashboard displays the total endpoint hits that the LUIS app receives and enables you to display hits within a period that you specify.</span><span class="sxs-lookup"><span data-stu-id="8b36e-120">The dashboard displays the total endpoint hits that the LUIS app receives and enables you to display hits within a period that you specify.</span></span> <span data-ttu-id="8b36e-121">The total number of hits displayed is the sum of endpoint hits that use an [Endpoint key](./luis-concept-keys.md#endpoint-key) and endpoint hits that use an [Authoring key](./luis-concept-keys.md#authoring-key).</span><span class="sxs-lookup"><span data-stu-id="8b36e-121">The total number of hits displayed is the sum of endpoint hits that use an [Endpoint key](./luis-concept-keys.md#endpoint-key) and endpoint hits that use an [Authoring key](./luis-concept-keys.md#authoring-key).</span></span>

<span data-ttu-id="8b36e-122"><!-- TBD: this image is old but I don't have a new one based on usage -->
![Endpoint Hits](./media/luis-how-to-use-dashboard/dashboard-endpointhits.png)</span><span class="sxs-lookup"><span data-stu-id="8b36e-122"><!-- TBD: this image is old but I don't have a new one based on usage -->
![Endpoint Hits](./media/luis-how-to-use-dashboard/dashboard-endpointhits.png)</span></span>

> [!NOTE] 
> <span data-ttu-id="8b36e-123">The most current endpoint hit count is in the Azure portal on the LUIS service overview.</span><span class="sxs-lookup"><span data-stu-id="8b36e-123">The most current endpoint hit count is in the Azure portal on the LUIS service overview.</span></span> 
 
### <a name="total-endpoint-hits"></a><span data-ttu-id="8b36e-124">Total endpoint hits</span><span class="sxs-lookup"><span data-stu-id="8b36e-124">Total endpoint hits</span></span>
<span data-ttu-id="8b36e-125">The total number of endpoint hits received to your app since app creation up to the current date.</span><span class="sxs-lookup"><span data-stu-id="8b36e-125">The total number of endpoint hits received to your app since app creation up to the current date.</span></span>

### <a name="endpoint-hits-per-period"></a><span data-ttu-id="8b36e-126">Endpoint hits per period</span><span class="sxs-lookup"><span data-stu-id="8b36e-126">Endpoint hits per period</span></span>
<span data-ttu-id="8b36e-127">The number of hits received within a past period, displayed per day.</span><span class="sxs-lookup"><span data-stu-id="8b36e-127">The number of hits received within a past period, displayed per day.</span></span> <span data-ttu-id="8b36e-128">The points between the start and end dates represent the days falling in this period.</span><span class="sxs-lookup"><span data-stu-id="8b36e-128">The points between the start and end dates represent the days falling in this period.</span></span> <span data-ttu-id="8b36e-129">Hover your mouse pointer over each point to see the hits count in each day within the period.</span><span class="sxs-lookup"><span data-stu-id="8b36e-129">Hover your mouse pointer over each point to see the hits count in each day within the period.</span></span> 

<span data-ttu-id="8b36e-130">To select a period to view on the chart:</span><span class="sxs-lookup"><span data-stu-id="8b36e-130">To select a period to view on the chart:</span></span>
 
1. <span data-ttu-id="8b36e-131">Click **Additional Settings** ![Additional Settings button](./media/luis-how-to-use-dashboard/Dashboard-Settings-btn.png) to access the periods list.</span><span class="sxs-lookup"><span data-stu-id="8b36e-131">Click **Additional Settings** ![Additional Settings button](./media/luis-how-to-use-dashboard/Dashboard-Settings-btn.png) to access the periods list.</span></span> <span data-ttu-id="8b36e-132">You can select periods ranging from one week up to one year.</span><span class="sxs-lookup"><span data-stu-id="8b36e-132">You can select periods ranging from one week up to one year.</span></span> 

    ![Endpoint Hits per Period](./media/luis-how-to-use-dashboard/timerange.png)

2. <span data-ttu-id="8b36e-134">Select a period from the list and then click the back arrow</span><span class="sxs-lookup"><span data-stu-id="8b36e-134">Select a period from the list and then click the back arrow</span></span> ![Back Arrow](./media/luis-how-to-use-dashboard/Dashboard-backArrow.png) <span data-ttu-id="8b36e-136">to display the chart.</span><span class="sxs-lookup"><span data-stu-id="8b36e-136">to display the chart.</span></span>

### <a name="key-usage"></a><span data-ttu-id="8b36e-137">Key usage</span><span class="sxs-lookup"><span data-stu-id="8b36e-137">Key usage</span></span>
<span data-ttu-id="8b36e-138">The number of hits consumed from the application's endpoint key.</span><span class="sxs-lookup"><span data-stu-id="8b36e-138">The number of hits consumed from the application's endpoint key.</span></span> <span data-ttu-id="8b36e-139">For more information about endpoint keys, see [Keys in LUIS](luis-concept-keys.md).</span><span class="sxs-lookup"><span data-stu-id="8b36e-139">For more information about endpoint keys, see [Keys in LUIS](luis-concept-keys.md).</span></span> 
  
## <a name="intent-breakdown"></a><span data-ttu-id="8b36e-140">Intent breakdown</span><span class="sxs-lookup"><span data-stu-id="8b36e-140">Intent breakdown</span></span>
<span data-ttu-id="8b36e-141">The **Intent Breakdown** displays a breakdown of intents based on labeled utterances or endpoint hits.</span><span class="sxs-lookup"><span data-stu-id="8b36e-141">The **Intent Breakdown** displays a breakdown of intents based on labeled utterances or endpoint hits.</span></span> <span data-ttu-id="8b36e-142">This summary graph shows the relative importance of each intent in the app.</span><span class="sxs-lookup"><span data-stu-id="8b36e-142">This summary graph shows the relative importance of each intent in the app.</span></span> <span data-ttu-id="8b36e-143">When you hover your mouse pointer over a slice, you see the intent name and the percentage it represents of the total count of labeled utterances/endpoint hits.</span><span class="sxs-lookup"><span data-stu-id="8b36e-143">When you hover your mouse pointer over a slice, you see the intent name and the percentage it represents of the total count of labeled utterances/endpoint hits.</span></span> 

![Intent Breakdown](./media/luis-how-to-use-dashboard/intent-breakdown.png)

<span data-ttu-id="8b36e-145">To control whether the breakdown is based on labeled utterances or endpoint hits:</span><span class="sxs-lookup"><span data-stu-id="8b36e-145">To control whether the breakdown is based on labeled utterances or endpoint hits:</span></span>

1. <span data-ttu-id="8b36e-146">Click **Additional Settings** ![Additional Settings button](./media/luis-how-to-use-dashboard/Dashboard-Settings-btn.png) to access the list as in the following image:</span><span class="sxs-lookup"><span data-stu-id="8b36e-146">Click **Additional Settings** ![Additional Settings button](./media/luis-how-to-use-dashboard/Dashboard-Settings-btn.png) to access the list as in the following image:</span></span>

    ![Intent Breakdown List](./media/luis-how-to-use-dashboard/intent-breakdown-based-on.png)
2. <span data-ttu-id="8b36e-148">Select a value from the list and then click the back arrow</span><span class="sxs-lookup"><span data-stu-id="8b36e-148">Select a value from the list and then click the back arrow</span></span> ![Back Arrow](./media/luis-how-to-use-dashboard/Dashboard-backArrow.png) <span data-ttu-id="8b36e-150">to display the chart.</span><span class="sxs-lookup"><span data-stu-id="8b36e-150">to display the chart.</span></span>

## <a name="entity-breakdown"></a><span data-ttu-id="8b36e-151">Entity breakdown</span><span class="sxs-lookup"><span data-stu-id="8b36e-151">Entity breakdown</span></span>
<span data-ttu-id="8b36e-152">The dashboard displays a breakdown of entities based on labeled utterances or endpoint hits.</span><span class="sxs-lookup"><span data-stu-id="8b36e-152">The dashboard displays a breakdown of entities based on labeled utterances or endpoint hits.</span></span> <span data-ttu-id="8b36e-153">This summary graph shows the relative importance of each entity in the app.</span><span class="sxs-lookup"><span data-stu-id="8b36e-153">This summary graph shows the relative importance of each entity in the app.</span></span> <span data-ttu-id="8b36e-154">When you hover your mouse pointer over a slice, you see the entity name and the percentage in labeled utterances/endpoint hits.</span><span class="sxs-lookup"><span data-stu-id="8b36e-154">When you hover your mouse pointer over a slice, you see the entity name and the percentage in labeled utterances/endpoint hits.</span></span> 

![Entity Breakdown](./media/luis-how-to-use-dashboard/entity-breakdown.png)

<span data-ttu-id="8b36e-156">To control whether the breakdown is based on labeled utterances or endpoint hits:</span><span class="sxs-lookup"><span data-stu-id="8b36e-156">To control whether the breakdown is based on labeled utterances or endpoint hits:</span></span>

1. <span data-ttu-id="8b36e-157">Click **Additional Settings** ![Additional Settings button](./media/luis-how-to-use-dashboard/Dashboard-Settings-btn.png) to access the list as in the following image:</span><span class="sxs-lookup"><span data-stu-id="8b36e-157">Click **Additional Settings** ![Additional Settings button](./media/luis-how-to-use-dashboard/Dashboard-Settings-btn.png) to access the list as in the following image:</span></span>

    ![Entity Breakdown List](./media/luis-how-to-use-dashboard/entity-breakdown-based-on.png)
2. <span data-ttu-id="8b36e-159">Select a value from the list and then click the back arrow</span><span class="sxs-lookup"><span data-stu-id="8b36e-159">Select a value from the list and then click the back arrow</span></span> ![Back Arrow](./media/luis-how-to-use-dashboard/Dashboard-backArrow.png) <span data-ttu-id="8b36e-161">to display the chart accordingly.</span><span class="sxs-lookup"><span data-stu-id="8b36e-161">to display the chart accordingly.</span></span>
