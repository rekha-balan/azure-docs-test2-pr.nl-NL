---
title: Create a custom dashboard in Azure Log Analytics | Microsoft Docs
description: This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 047c2b251eae6a560ba724b31b7116dab7bf881e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556718"
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="6bd1a-103">Create a custom dashboard for use in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6bd1a-103">Create a custom dashboard for use in Log Analytics</span></span>
<span data-ttu-id="6bd1a-104">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-104">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span></span>

![Example Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="6bd1a-106">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-106">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span></span> <span data-ttu-id="6bd1a-107">See the following pages for more information about the apps.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-107">See the following pages for more information about the apps.</span></span>

* [<span data-ttu-id="6bd1a-108">OMS mobile app from the Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="6bd1a-108">OMS mobile app from the Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="6bd1a-109">OMS mobile app from Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="6bd1a-109">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobile dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="6bd1a-111">How do I create my dashboard?</span><span class="sxs-lookup"><span data-stu-id="6bd1a-111">How do I create my dashboard?</span></span>
<span data-ttu-id="6bd1a-112">To begin, go to the OMS Overview page.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-112">To begin, go to the OMS Overview page.</span></span> <span data-ttu-id="6bd1a-113">You'll see the **My Dashboard** tile on the left.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-113">You'll see the **My Dashboard** tile on the left.</span></span> <span data-ttu-id="6bd1a-114">Click it to drill down into your dashboard.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-114">Click it to drill down into your dashboard.</span></span>

![Overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="6bd1a-116">Adding a tile</span><span class="sxs-lookup"><span data-stu-id="6bd1a-116">Adding a tile</span></span>
<span data-ttu-id="6bd1a-117">In dashboards, tiles are powered by your saved log searches.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-117">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="6bd1a-118">OMS comes with many pre-made saved log searches, so you can begin right away.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-118">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="6bd1a-119">Use the following steps that outline how to begin.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-119">Use the following steps that outline how to begin.</span></span>

<span data-ttu-id="6bd1a-120">In the My Dashboard view, simply click **Customize** to enter customize mode.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-120">In the My Dashboard view, simply click **Customize** to enter customize mode.</span></span>

![Pictorial](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="6bd1a-122">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-122">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="6bd1a-123">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-123">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span></span>

![Add Tiles 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="6bd1a-125">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-125">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span></span>

![Add Tiles 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="6bd1a-127">Edit a tile</span><span class="sxs-lookup"><span data-stu-id="6bd1a-127">Edit a tile</span></span>
<span data-ttu-id="6bd1a-128">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-128">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span></span> <span data-ttu-id="6bd1a-129">Click the tile you want to edit.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-129">Click the tile you want to edit.</span></span> <span data-ttu-id="6bd1a-130">The right panel changes to edit, and gives a selection of options:</span><span class="sxs-lookup"><span data-stu-id="6bd1a-130">The right panel changes to edit, and gives a selection of options:</span></span>

![Edit Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Edit Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="6bd1a-133">Tile visualizations</span><span class="sxs-lookup"><span data-stu-id="6bd1a-133">Tile visualizations</span></span>
<span data-ttu-id="6bd1a-134">There are three kinds of tile visualizations to choose from:</span><span class="sxs-lookup"><span data-stu-id="6bd1a-134">There are three kinds of tile visualizations to choose from:</span></span>

| <span data-ttu-id="6bd1a-135">chart type</span><span class="sxs-lookup"><span data-stu-id="6bd1a-135">chart type</span></span> | <span data-ttu-id="6bd1a-136">what it does</span><span class="sxs-lookup"><span data-stu-id="6bd1a-136">what it does</span></span> |
| --- | --- |
| ![Bar Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="6bd1a-138">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-138">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![metric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="6bd1a-140">Displays your total log search result hits as a number in a tile.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-140">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="6bd1a-141">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-141">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span></span> |
| ![line](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="6bd1a-143">Displays a timeline of your saved log search result hits with values as a line chart.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-143">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="6bd1a-144">Threshold</span><span class="sxs-lookup"><span data-stu-id="6bd1a-144">Threshold</span></span>
<span data-ttu-id="6bd1a-145">You can create a threshold on a tile using the Metric visualization.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-145">You can create a threshold on a tile using the Metric visualization.</span></span> <span data-ttu-id="6bd1a-146">Select on to create a threshold value on the tile.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-146">Select on to create a threshold value on the tile.</span></span> <span data-ttu-id="6bd1a-147">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-147">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span></span>

## <a name="organizing-the-dashboard"></a><span data-ttu-id="6bd1a-148">Organizing the dashboard</span><span class="sxs-lookup"><span data-stu-id="6bd1a-148">Organizing the dashboard</span></span>
<span data-ttu-id="6bd1a-149">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-149">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="6bd1a-150">Click and drag the tile you want to move, and move it to where you want your tile to be.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-150">Click and drag the tile you want to move, and move it to where you want your tile to be.</span></span>

![Organize your Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="6bd1a-152">Remove a tile</span><span class="sxs-lookup"><span data-stu-id="6bd1a-152">Remove a tile</span></span>
<span data-ttu-id="6bd1a-153">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-153">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="6bd1a-154">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-154">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span></span>

![Remove a Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="6bd1a-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="6bd1a-156">Next steps</span></span>
* <span data-ttu-id="6bd1a-157">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span><span class="sxs-lookup"><span data-stu-id="6bd1a-157">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span></span>













