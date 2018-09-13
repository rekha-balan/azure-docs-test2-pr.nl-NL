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
# <a name="filters-in-log-analytics-views"></a><span data-ttu-id="6a396-104">Filters in Log Analytics views</span><span class="sxs-lookup"><span data-stu-id="6a396-104">Filters in Log Analytics views</span></span>
<span data-ttu-id="6a396-105">A **filter** in a [Log Analytics view](log-analytics-view-designer.md) allows users to filter the data in the view by the value of a particular property without modifying the view itself.</span><span class="sxs-lookup"><span data-stu-id="6a396-105">A **filter** in a [Log Analytics view](log-analytics-view-designer.md) allows users to filter the data in the view by the value of a particular property without modifying the view itself.</span></span>  <span data-ttu-id="6a396-106">For example, you could allow users of your view to filter the view for data only from a particular computer or set of computers.</span><span class="sxs-lookup"><span data-stu-id="6a396-106">For example, you could allow users of your view to filter the view for data only from a particular computer or set of computers.</span></span>  <span data-ttu-id="6a396-107">You can create multiple filters on a single view to allow users to filter by multiple properties.</span><span class="sxs-lookup"><span data-stu-id="6a396-107">You can create multiple filters on a single view to allow users to filter by multiple properties.</span></span>  <span data-ttu-id="6a396-108">This article describes how to use a filter and add one to a custom view.</span><span class="sxs-lookup"><span data-stu-id="6a396-108">This article describes how to use a filter and add one to a custom view.</span></span>

## <a name="using-a-filter"></a><span data-ttu-id="6a396-109">Using a filter</span><span class="sxs-lookup"><span data-stu-id="6a396-109">Using a filter</span></span>
<span data-ttu-id="6a396-110">Click the data time range at the top of a view to open the drop down where you can change the data time range for the view.</span><span class="sxs-lookup"><span data-stu-id="6a396-110">Click the data time range at the top of a view to open the drop down where you can change the data time range for the view.</span></span>

![Filter example](media/log-analytics-view-designer/filters-example-time.png)

<span data-ttu-id="6a396-112">Click the **+** to add a filter using custom filters that are defined for the view.</span><span class="sxs-lookup"><span data-stu-id="6a396-112">Click the **+** to add a filter using custom filters that are defined for the view.</span></span> <span data-ttu-id="6a396-113">Either select a value for the filter from the dropdown or type in a value.</span><span class="sxs-lookup"><span data-stu-id="6a396-113">Either select a value for the filter from the dropdown or type in a value.</span></span> <span data-ttu-id="6a396-114">Continue to add filters by clicking the **+**.</span><span class="sxs-lookup"><span data-stu-id="6a396-114">Continue to add filters by clicking the **+**.</span></span> 


![Filter example](media/log-analytics-view-designer/filters-example-custom.png)

<span data-ttu-id="6a396-116">If you remove all of the values for a filter, then that filter will no longer be applied.</span><span class="sxs-lookup"><span data-stu-id="6a396-116">If you remove all of the values for a filter, then that filter will no longer be applied.</span></span>


## <a name="creating-a-filter"></a><span data-ttu-id="6a396-117">Creating a filter</span><span class="sxs-lookup"><span data-stu-id="6a396-117">Creating a filter</span></span>

<span data-ttu-id="6a396-118">Create a filter from the **Filters** tab when [editing a view](log-analytics-view-designer.md).</span><span class="sxs-lookup"><span data-stu-id="6a396-118">Create a filter from the **Filters** tab when [editing a view](log-analytics-view-designer.md).</span></span>  <span data-ttu-id="6a396-119">The filter is global for the view and applies to all parts in the view.</span><span class="sxs-lookup"><span data-stu-id="6a396-119">The filter is global for the view and applies to all parts in the view.</span></span>  

![Filter settings](media/log-analytics-view-designer/filters-settings.png)

<span data-ttu-id="6a396-121">The following table describes the settings for a filter.</span><span class="sxs-lookup"><span data-stu-id="6a396-121">The following table describes the settings for a filter.</span></span>

| <span data-ttu-id="6a396-122">Setting</span><span class="sxs-lookup"><span data-stu-id="6a396-122">Setting</span></span> | <span data-ttu-id="6a396-123">Description</span><span class="sxs-lookup"><span data-stu-id="6a396-123">Description</span></span> |
|:---|:---|
| <span data-ttu-id="6a396-124">Field Name</span><span class="sxs-lookup"><span data-stu-id="6a396-124">Field Name</span></span> | <span data-ttu-id="6a396-125">Name of the field used for filtering.</span><span class="sxs-lookup"><span data-stu-id="6a396-125">Name of the field used for filtering.</span></span>  <span data-ttu-id="6a396-126">This must match the summarize field in **Query for Values**.</span><span class="sxs-lookup"><span data-stu-id="6a396-126">This must match the summarize field in **Query for Values**.</span></span> |
| <span data-ttu-id="6a396-127">Query for Values</span><span class="sxs-lookup"><span data-stu-id="6a396-127">Query for Values</span></span> | <span data-ttu-id="6a396-128">Query to run to populate filter dropdown for the user.</span><span class="sxs-lookup"><span data-stu-id="6a396-128">Query to run to populate filter dropdown for the user.</span></span>  <span data-ttu-id="6a396-129">This must use either [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) or [distinct](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/distinct-operator) to provide unique values for a particular field, and it must match the **Field Name**.</span><span class="sxs-lookup"><span data-stu-id="6a396-129">This must use either [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) or [distinct](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/distinct-operator) to provide unique values for a particular field, and it must match the **Field Name**.</span></span>  <span data-ttu-id="6a396-130">You can use [sort](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/sort-operator) to sort the values that are displayed to the user.</span><span class="sxs-lookup"><span data-stu-id="6a396-130">You can use [sort](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/sort-operator) to sort the values that are displayed to the user.</span></span> |
| <span data-ttu-id="6a396-131">Tag</span><span class="sxs-lookup"><span data-stu-id="6a396-131">Tag</span></span> | <span data-ttu-id="6a396-132">Name for the field that's used in queries supporting the filter and is also displayed to the user.</span><span class="sxs-lookup"><span data-stu-id="6a396-132">Name for the field that's used in queries supporting the filter and is also displayed to the user.</span></span> |

### <a name="examples"></a><span data-ttu-id="6a396-133">Examples</span><span class="sxs-lookup"><span data-stu-id="6a396-133">Examples</span></span>

<span data-ttu-id="6a396-134">The following table includes a few examples of common filters.</span><span class="sxs-lookup"><span data-stu-id="6a396-134">The following table includes a few examples of common filters.</span></span>  

| <span data-ttu-id="6a396-135">Field Name</span><span class="sxs-lookup"><span data-stu-id="6a396-135">Field Name</span></span> | <span data-ttu-id="6a396-136">Query for Values</span><span class="sxs-lookup"><span data-stu-id="6a396-136">Query for Values</span></span> | <span data-ttu-id="6a396-137">Tag</span><span class="sxs-lookup"><span data-stu-id="6a396-137">Tag</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6a396-138">Computer</span><span class="sxs-lookup"><span data-stu-id="6a396-138">Computer</span></span>   | <span data-ttu-id="6a396-139">Heartbeat &#124; distinct Computer &#124; sort by Computer asc</span><span class="sxs-lookup"><span data-stu-id="6a396-139">Heartbeat &#124; distinct Computer &#124; sort by Computer asc</span></span> | <span data-ttu-id="6a396-140">Computers</span><span class="sxs-lookup"><span data-stu-id="6a396-140">Computers</span></span> |
| <span data-ttu-id="6a396-141">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="6a396-141">EventLevelName</span></span> | <span data-ttu-id="6a396-142">Event &#124; distinct EventLevelName</span><span class="sxs-lookup"><span data-stu-id="6a396-142">Event &#124; distinct EventLevelName</span></span> | <span data-ttu-id="6a396-143">Severity</span><span class="sxs-lookup"><span data-stu-id="6a396-143">Severity</span></span> |
| <span data-ttu-id="6a396-144">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="6a396-144">SeverityLevel</span></span> | <span data-ttu-id="6a396-145">Syslog &#124; distinct SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="6a396-145">Syslog &#124; distinct SeverityLevel</span></span> | <span data-ttu-id="6a396-146">Severity</span><span class="sxs-lookup"><span data-stu-id="6a396-146">Severity</span></span> |
| <span data-ttu-id="6a396-147">SvcChangeType</span><span class="sxs-lookup"><span data-stu-id="6a396-147">SvcChangeType</span></span> | <span data-ttu-id="6a396-148">ConfigurationChange &#124; distinct svcChangeType</span><span class="sxs-lookup"><span data-stu-id="6a396-148">ConfigurationChange &#124; distinct svcChangeType</span></span> | <span data-ttu-id="6a396-149">ChangeType</span><span class="sxs-lookup"><span data-stu-id="6a396-149">ChangeType</span></span> |


## <a name="modify-view-queries"></a><span data-ttu-id="6a396-150">Modify view queries</span><span class="sxs-lookup"><span data-stu-id="6a396-150">Modify view queries</span></span>

<span data-ttu-id="6a396-151">For a filter to have any effect, you must modify any queries in the view to filter on the selected values.</span><span class="sxs-lookup"><span data-stu-id="6a396-151">For a filter to have any effect, you must modify any queries in the view to filter on the selected values.</span></span>  <span data-ttu-id="6a396-152">If you don't modify any queries in the view then any values the user selects will have no effect.</span><span class="sxs-lookup"><span data-stu-id="6a396-152">If you don't modify any queries in the view then any values the user selects will have no effect.</span></span>

<span data-ttu-id="6a396-153">The syntax for using a filter value in a query is:</span><span class="sxs-lookup"><span data-stu-id="6a396-153">The syntax for using a filter value in a query is:</span></span> 

    where ${filter name}  

<span data-ttu-id="6a396-154">For example, if your view has a query the returns events and uses a filter called Computers, you could use the following.</span><span class="sxs-lookup"><span data-stu-id="6a396-154">For example, if your view has a query the returns events and uses a filter called Computers, you could use the following.</span></span>

    Event | where ${Computers} | summarize count() by EventLevelName

<span data-ttu-id="6a396-155">If you added another filter called Severity, you could use the following query to use both filters.</span><span class="sxs-lookup"><span data-stu-id="6a396-155">If you added another filter called Severity, you could use the following query to use both filters.</span></span>

    Event | where ${Computers} | where ${Severity} | summarize count() by EventLevelName

## <a name="next-steps"></a><span data-ttu-id="6a396-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a396-156">Next steps</span></span>
* <span data-ttu-id="6a396-157">Learn more about the [Visualization Parts](log-analytics-view-designer-parts.md) you can add to your custom view.</span><span class="sxs-lookup"><span data-stu-id="6a396-157">Learn more about the [Visualization Parts](log-analytics-view-designer-parts.md) you can add to your custom view.</span></span>