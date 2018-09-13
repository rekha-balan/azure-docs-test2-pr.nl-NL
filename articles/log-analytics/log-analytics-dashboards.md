---
title: Create a custom dashboard in Azure Log Analytics | Microsoft Docs
description: This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/08/2017
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 34a398d0669d31736094b70b3bf961316b926f2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800441"
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="96080-103">Create a custom dashboard for use in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="96080-103">Create a custom dashboard for use in Log Analytics</span></span>

<span data-ttu-id="96080-104">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span><span class="sxs-lookup"><span data-stu-id="96080-104">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span></span>

>[!NOTE]
> <span data-ttu-id="96080-105">You can no longer edit your existing **My Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="96080-105">You can no longer edit your existing **My Dashboard**.</span></span> <span data-ttu-id="96080-106">This feature is in the process of being deprecated.</span><span class="sxs-lookup"><span data-stu-id="96080-106">This feature is in the process of being deprecated.</span></span>

![Example Dashboard](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="96080-108">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span><span class="sxs-lookup"><span data-stu-id="96080-108">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span></span> <span data-ttu-id="96080-109">See the following pages for more information about the apps.</span><span class="sxs-lookup"><span data-stu-id="96080-109">See the following pages for more information about the apps.</span></span>

* [<span data-ttu-id="96080-110">OMS mobile app from the Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="96080-110">OMS mobile app from the Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="96080-111">OMS mobile app from Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="96080-111">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobile dashboard](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="96080-113">How do I create my dashboard?</span><span class="sxs-lookup"><span data-stu-id="96080-113">How do I create my dashboard?</span></span>
<span data-ttu-id="96080-114">To begin, go to the OMS Overview page.</span><span class="sxs-lookup"><span data-stu-id="96080-114">To begin, go to the OMS Overview page.</span></span> <span data-ttu-id="96080-115">You'll see the **My Dashboard** tile on the left.</span><span class="sxs-lookup"><span data-stu-id="96080-115">You'll see the **My Dashboard** tile on the left.</span></span> <span data-ttu-id="96080-116">Click it to drill down into your dashboard.</span><span class="sxs-lookup"><span data-stu-id="96080-116">Click it to drill down into your dashboard.</span></span>

![Overview](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="96080-118">Adding a tile</span><span class="sxs-lookup"><span data-stu-id="96080-118">Adding a tile</span></span>
<span data-ttu-id="96080-119">In dashboards, tiles are powered by your saved log searches.</span><span class="sxs-lookup"><span data-stu-id="96080-119">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="96080-120">OMS comes with many pre-made saved log searches, so you can begin right away.</span><span class="sxs-lookup"><span data-stu-id="96080-120">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="96080-121">Use the following steps that outline how to begin.</span><span class="sxs-lookup"><span data-stu-id="96080-121">Use the following steps that outline how to begin.</span></span>

<span data-ttu-id="96080-122">In the My Dashboard view, simply click **Customize** to enter customize mode.</span><span class="sxs-lookup"><span data-stu-id="96080-122">In the My Dashboard view, simply click **Customize** to enter customize mode.</span></span>

![Pictorial](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="96080-124">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span><span class="sxs-lookup"><span data-stu-id="96080-124">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="96080-125">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span><span class="sxs-lookup"><span data-stu-id="96080-125">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span></span>

![Add Tiles 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="96080-127">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span><span class="sxs-lookup"><span data-stu-id="96080-127">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span></span>

![Add Tiles 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="96080-129">Edit a tile</span><span class="sxs-lookup"><span data-stu-id="96080-129">Edit a tile</span></span>
<span data-ttu-id="96080-130">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span><span class="sxs-lookup"><span data-stu-id="96080-130">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span></span> <span data-ttu-id="96080-131">Click the tile you want to edit.</span><span class="sxs-lookup"><span data-stu-id="96080-131">Click the tile you want to edit.</span></span> <span data-ttu-id="96080-132">The right panel changes to edit, and gives a selection of options:</span><span class="sxs-lookup"><span data-stu-id="96080-132">The right panel changes to edit, and gives a selection of options:</span></span>

![Edit Tile](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Edit Tile](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="96080-135">Tile visualizations</span><span class="sxs-lookup"><span data-stu-id="96080-135">Tile visualizations</span></span>
<span data-ttu-id="96080-136">There are three kinds of tile visualizations to choose from:</span><span class="sxs-lookup"><span data-stu-id="96080-136">There are three kinds of tile visualizations to choose from:</span></span>

| <span data-ttu-id="96080-137">chart type</span><span class="sxs-lookup"><span data-stu-id="96080-137">chart type</span></span> | <span data-ttu-id="96080-138">what it does</span><span class="sxs-lookup"><span data-stu-id="96080-138">what it does</span></span> |
| --- | --- |
| ![Bar Chart](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="96080-140">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span><span class="sxs-lookup"><span data-stu-id="96080-140">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![metric](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="96080-142">Displays your total log search result hits as a number in a tile.</span><span class="sxs-lookup"><span data-stu-id="96080-142">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="96080-143">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span><span class="sxs-lookup"><span data-stu-id="96080-143">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="96080-145">Displays a timeline of your saved log search result hits with values as a line chart.</span><span class="sxs-lookup"><span data-stu-id="96080-145">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="96080-146">Threshold</span><span class="sxs-lookup"><span data-stu-id="96080-146">Threshold</span></span>
<span data-ttu-id="96080-147">You can create a threshold on a tile using the Metric visualization.</span><span class="sxs-lookup"><span data-stu-id="96080-147">You can create a threshold on a tile using the Metric visualization.</span></span> <span data-ttu-id="96080-148">Select on to create a threshold value on the tile.</span><span class="sxs-lookup"><span data-stu-id="96080-148">Select on to create a threshold value on the tile.</span></span> <span data-ttu-id="96080-149">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span><span class="sxs-lookup"><span data-stu-id="96080-149">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span></span>

## <a name="organizing-the-dashboard"></a><span data-ttu-id="96080-150">Organizing the dashboard</span><span class="sxs-lookup"><span data-stu-id="96080-150">Organizing the dashboard</span></span>
<span data-ttu-id="96080-151">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span><span class="sxs-lookup"><span data-stu-id="96080-151">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="96080-152">Click and drag the tile you want to move, and move it to where you want your tile to be.</span><span class="sxs-lookup"><span data-stu-id="96080-152">Click and drag the tile you want to move, and move it to where you want your tile to be.</span></span>

![Organize your Dashboard](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="96080-154">Remove a tile</span><span class="sxs-lookup"><span data-stu-id="96080-154">Remove a tile</span></span>
<span data-ttu-id="96080-155">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span><span class="sxs-lookup"><span data-stu-id="96080-155">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="96080-156">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span><span class="sxs-lookup"><span data-stu-id="96080-156">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span></span>

![Remove a Tile](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="96080-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="96080-158">Next steps</span></span>
* <span data-ttu-id="96080-159">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span><span class="sxs-lookup"><span data-stu-id="96080-159">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span></span>
