---
title: Filters in Azure Log Analytics views | Microsoft Docs
description: A filter in a Log Analytics view allows users to filter the data in the view by the value of a particular property without modifying the view itself.  This article describes how to use a filter and add one to a custom view.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/22/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 0ad22562bd1f36bba7c0ab99fe504e82645033d3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966073"
---
# <a name="filters-in-log-analytics-views"></a>Filters in Log Analytics views
A **filter** in a [Log Analytics view](log-analytics-view-designer.md) allows users to filter the data in the view by the value of a particular property without modifying the view itself.  For example, you could allow users of your view to filter the view for data only from a particular computer or set of computers.  You can create multiple filters on a single view to allow users to filter by multiple properties.  This article describes how to use a filter and add one to a custom view.

## <a name="using-a-filter"></a>Using a filter
Click the data time range at the top of a view to open the drop down where you can change the data time range for the view.

![Filter example](media/log-analytics-view-designer/filters-example-time.png)

Click the **+** to add a filter using custom filters that are defined for the view. Either select a value for the filter from the dropdown or type in a value. Continue to add filters by clicking the **+**. 


![Filter example](media/log-analytics-view-designer/filters-example-custom.png)

If you remove all of the values for a filter, then that filter will no longer be applied.


## <a name="creating-a-filter"></a>Creating a filter

Create a filter from the **Filters** tab when [editing a view](log-analytics-view-designer.md).  The filter is global for the view and applies to all parts in the view.  

![Filter settings](media/log-analytics-view-designer/filters-settings.png)

The following table describes the settings for a filter.

| Setting | Description |
|:---|:---|
| Field Name | Name of the field used for filtering.  This must match the summarize field in **Query for Values**. |
| Query for Values | Query to run to populate filter dropdown for the user.  This must use either [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) or [distinct](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/distinct-operator) to provide unique values for a particular field, and it must match the **Field Name**.  You can use [sort](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/sort-operator) to sort the values that are displayed to the user. |
| Tag | Name for the field that's used in queries supporting the filter and is also displayed to the user. |

### <a name="examples"></a>Examples

The following table includes a few examples of common filters.  

| Field Name | Query for Values | Tag |
|:--|:--|:--|
| Computer   | Heartbeat &#124; distinct Computer &#124; sort by Computer asc | Computers |
| EventLevelName | Event &#124; distinct EventLevelName | Severity |
| SeverityLevel | Syslog &#124; distinct SeverityLevel | Severity |
| SvcChangeType | ConfigurationChange &#124; distinct svcChangeType | ChangeType |


## <a name="modify-view-queries"></a>Modify view queries

For a filter to have any effect, you must modify any queries in the view to filter on the selected values.  If you don't modify any queries in the view then any values the user selects will have no effect.

The syntax for using a filter value in a query is: 

    where ${filter name}  

For example, if your view has a query the returns events and uses a filter called Computers, you could use the following.

    Event | where ${Computers} | summarize count() by EventLevelName

If you added another filter called Severity, you could use the following query to use both filters.

    Event | where ${Computers} | where ${Severity} | summarize count() by EventLevelName

## <a name="next-steps"></a>Next steps
* Learn more about the [Visualization Parts](log-analytics-view-designer-parts.md) you can add to your custom view.