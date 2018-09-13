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
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Create a custom dashboard for use in Log Analytics
This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.

![Example Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-example-dash.png)

All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App. See the following pages for more information about the apps.

* [OMS mobile app from the Microsoft Store](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [OMS mobile app from Apple iTunes](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobile dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>How do I create my dashboard?
To begin, go to the OMS Overview page. You'll see the **My Dashboard** tile on the left. Click it to drill down into your dashboard.

![Overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>Adding a tile
In dashboards, tiles are powered by your saved log searches. OMS comes with many pre-made saved log searches, so you can begin right away. Use the following steps that outline how to begin.

In the My Dashboard view, simply click **Customize** to enter customize mode.

![Pictorial](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 The panel that opens on the right side of the page shows all of your workspace's saved log searches. To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.

![Add Tiles 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

When you click the **plus** symbol, a new tile appears in the My Dashboard view.

![Add Tiles 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>Edit a tile
In the My Dashboard view, simply click  **Customize** to enter customize mode. Click the tile you want to edit. The right panel changes to edit, and gives a selection of options:

![Edit Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Edit Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>Tile visualizations
There are three kinds of tile visualizations to choose from:

| chart type | what it does |
| --- | --- |
| ![Bar Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not. |
| ![metric](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-metric.png) |Displays your total log search result hits as a number in a tile. Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached. |
| ![line](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-line.png) |Displays a timeline of your saved log search result hits with values as a line chart. |

### <a name="threshold"></a>Threshold
You can create a threshold on a tile using the Metric visualization. Select on to create a threshold value on the tile. Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.

## <a name="organizing-the-dashboard"></a>Organizing the dashboard
To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode. Click and drag the tile you want to move, and move it to where you want your tile to be.

![Organize your Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>Remove a tile
To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode. Select the tile you want to remove, then on the right panel select **Remove Tile**.

![Remove a Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>Next steps
* Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.













