---
title: Azure Monitor Resource Group Insights | Microsoft Docs
description: Understand the health and performance of your distributed applications and services at the Resource Group level with Azure Monitor
services: azure-monitor
author: NumberByColors
manager: carmonm
ms.service: azure-monitor
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 08/29/2018
ms.reviewer: mbullwin
ms.author: daviste
ms.openlocfilehash: 723006d37ed0570e32790a0bb70a3dce5a87ade8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857161"
---
# <a name="monitor-resource-groups-with-azure-monitor-preview"></a><span data-ttu-id="a80eb-103">Monitor resource groups with Azure Monitor (preview)</span><span class="sxs-lookup"><span data-stu-id="a80eb-103">Monitor resource groups with Azure Monitor (preview)</span></span>

<span data-ttu-id="a80eb-104">Modern applications are often complex and highly distributed with many discrete parts working together to deliver a service.</span><span class="sxs-lookup"><span data-stu-id="a80eb-104">Modern applications are often complex and highly distributed with many discrete parts working together to deliver a service.</span></span> <span data-ttu-id="a80eb-105">Recognizing this complexity, Azure Monitor provides monitoring insights for resource groups.</span><span class="sxs-lookup"><span data-stu-id="a80eb-105">Recognizing this complexity, Azure Monitor provides monitoring insights for resource groups.</span></span> <span data-ttu-id="a80eb-106">This makes it easy to triage and diagnose any problems your individual resources encounter, while offering context as to the health and performance of the resource group&mdash;and your application&mdash;as a whole.</span><span class="sxs-lookup"><span data-stu-id="a80eb-106">This makes it easy to triage and diagnose any problems your individual resources encounter, while offering context as to the health and performance of the resource group&mdash;and your application&mdash;as a whole.</span></span>

## <a name="access-insights-for-resource-groups"></a><span data-ttu-id="a80eb-107">Access insights for resource groups</span><span class="sxs-lookup"><span data-stu-id="a80eb-107">Access insights for resource groups</span></span>

1. <span data-ttu-id="a80eb-108">Select **Resource groups**  from the left-side navigation bar.</span><span class="sxs-lookup"><span data-stu-id="a80eb-108">Select **Resource groups**  from the left-side navigation bar.</span></span>
2. <span data-ttu-id="a80eb-109">Pick one of your resource groups that you want to explore.</span><span class="sxs-lookup"><span data-stu-id="a80eb-109">Pick one of your resource groups that you want to explore.</span></span> <span data-ttu-id="a80eb-110">(If you have a large number of resource groups filtering by subscription can sometimes be helpful.)</span><span class="sxs-lookup"><span data-stu-id="a80eb-110">(If you have a large number of resource groups filtering by subscription can sometimes be helpful.)</span></span>
3. <span data-ttu-id="a80eb-111">To access insights for a resource group, click **Insights** in the left-side menu of any resource group.</span><span class="sxs-lookup"><span data-stu-id="a80eb-111">To access insights for a resource group, click **Insights** in the left-side menu of any resource group.</span></span>

![Screenshot of resource group insights overview page](.\media\resource-group-insights\0001-overview.png)

## <a name="resources-with-active-alerts-and-health-issues"></a><span data-ttu-id="a80eb-113">Resources with active alerts and health issues</span><span class="sxs-lookup"><span data-stu-id="a80eb-113">Resources with active alerts and health issues</span></span>

<span data-ttu-id="a80eb-114">The overview page shows how many alerts have been fired and are still active, along with the current Azure Resource Health of each resource.</span><span class="sxs-lookup"><span data-stu-id="a80eb-114">The overview page shows how many alerts have been fired and are still active, along with the current Azure Resource Health of each resource.</span></span> <span data-ttu-id="a80eb-115">Together, this information can help you quickly spot any resources that are experiencing issues.</span><span class="sxs-lookup"><span data-stu-id="a80eb-115">Together, this information can help you quickly spot any resources that are experiencing issues.</span></span> <span data-ttu-id="a80eb-116">Alerts help you detect issues in your code and how you've configured your infrastructure.</span><span class="sxs-lookup"><span data-stu-id="a80eb-116">Alerts help you detect issues in your code and how you've configured your infrastructure.</span></span> <span data-ttu-id="a80eb-117">Azure Resource Health surfaces issue with the Azure platform itself, that aren't specific to your individual applications.</span><span class="sxs-lookup"><span data-stu-id="a80eb-117">Azure Resource Health surfaces issue with the Azure platform itself, that aren't specific to your individual applications.</span></span>

![Screenshot of Azure Resource Health pane](.\media\resource-group-insights\0002-overview.png)

### <a name="azure-resource-health"></a><span data-ttu-id="a80eb-119">Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="a80eb-119">Azure Resource Health</span></span>

<span data-ttu-id="a80eb-120">To display Azure Resource Health, check the **Show Azure Resource Health** box above the table.</span><span class="sxs-lookup"><span data-stu-id="a80eb-120">To display Azure Resource Health, check the **Show Azure Resource Health** box above the table.</span></span> <span data-ttu-id="a80eb-121">This column is hidden by default to help the page load quickly.</span><span class="sxs-lookup"><span data-stu-id="a80eb-121">This column is hidden by default to help the page load quickly.</span></span>

![Screenshot with resource health graph added](.\media\resource-group-insights\0003-overview.png)

<span data-ttu-id="a80eb-123">By default, the resources are grouped by app layer and resource type.</span><span class="sxs-lookup"><span data-stu-id="a80eb-123">By default, the resources are grouped by app layer and resource type.</span></span> <span data-ttu-id="a80eb-124">**App layer** is a simple categorization of resource types, that only exists within the context of the resource group insights overview page.</span><span class="sxs-lookup"><span data-stu-id="a80eb-124">**App layer** is a simple categorization of resource types, that only exists within the context of the resource group insights overview page.</span></span> <span data-ttu-id="a80eb-125">There are resource types related to application code, compute infrastructure, networking, storage + databases.</span><span class="sxs-lookup"><span data-stu-id="a80eb-125">There are resource types related to application code, compute infrastructure, networking, storage + databases.</span></span> <span data-ttu-id="a80eb-126">Management tools get their own app layers, and every other resource is categorized as belonging to the **Other** app layer.</span><span class="sxs-lookup"><span data-stu-id="a80eb-126">Management tools get their own app layers, and every other resource is categorized as belonging to the **Other** app layer.</span></span> <span data-ttu-id="a80eb-127">This grouping can help you see at-a-glance what subsystems of your application are healthy and unhealthy.</span><span class="sxs-lookup"><span data-stu-id="a80eb-127">This grouping can help you see at-a-glance what subsystems of your application are healthy and unhealthy.</span></span>

## <a name="diagnose-issues-in-your-resource-group"></a><span data-ttu-id="a80eb-128">Diagnose issues in your resource group</span><span class="sxs-lookup"><span data-stu-id="a80eb-128">Diagnose issues in your resource group</span></span>

<span data-ttu-id="a80eb-129">The resource group insights page provides several other tools scoped to help you diagnose issues</span><span class="sxs-lookup"><span data-stu-id="a80eb-129">The resource group insights page provides several other tools scoped to help you diagnose issues</span></span>

   |         |          |
   | ---------------- |:-----|
   | [<span data-ttu-id="a80eb-130">**Alerts**</span><span class="sxs-lookup"><span data-stu-id="a80eb-130">**Alerts**</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-unified-alerts)      |  <span data-ttu-id="a80eb-131">View, create, and manage your alerts.</span><span class="sxs-lookup"><span data-stu-id="a80eb-131">View, create, and manage your alerts.</span></span> |
   | [<span data-ttu-id="a80eb-132">**Metrics**</span><span class="sxs-lookup"><span data-stu-id="a80eb-132">**Metrics**</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) | <span data-ttu-id="a80eb-133">Visualize and explore your metric based data.</span><span class="sxs-lookup"><span data-stu-id="a80eb-133">Visualize and explore your metric based data.</span></span>    |
   | [<span data-ttu-id="a80eb-134">**Activity logs**</span><span class="sxs-lookup"><span data-stu-id="a80eb-134">**Activity logs**</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) | <span data-ttu-id="a80eb-135">Subscription level events that have occurred in Azure.</span><span class="sxs-lookup"><span data-stu-id="a80eb-135">Subscription level events that have occurred in Azure.</span></span>  |
   | [<span data-ttu-id="a80eb-136">**Application map**</span><span class="sxs-lookup"><span data-stu-id="a80eb-136">**Application map**</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-app-map) | <span data-ttu-id="a80eb-137">Navigate your distributed application's topology to identify performance bottlenecks or failure hotspots.</span><span class="sxs-lookup"><span data-stu-id="a80eb-137">Navigate your distributed application's topology to identify performance bottlenecks or failure hotspots.</span></span> |

## <a name="failures-and-performance"></a><span data-ttu-id="a80eb-138">Failures and performance</span><span class="sxs-lookup"><span data-stu-id="a80eb-138">Failures and performance</span></span>

<span data-ttu-id="a80eb-139">What if you've noticed your application is running slowly, or users have reported errors?</span><span class="sxs-lookup"><span data-stu-id="a80eb-139">What if you've noticed your application is running slowly, or users have reported errors?</span></span> <span data-ttu-id="a80eb-140">It's time consuming to search through all of your resources to isolate problems.</span><span class="sxs-lookup"><span data-stu-id="a80eb-140">It's time consuming to search through all of your resources to isolate problems.</span></span>

<span data-ttu-id="a80eb-141">The **Performance** and **Failures** tabs simplify this process by bringing together performance and failure diagnostic views for many common resource types.</span><span class="sxs-lookup"><span data-stu-id="a80eb-141">The **Performance** and **Failures** tabs simplify this process by bringing together performance and failure diagnostic views for many common resource types.</span></span>

<span data-ttu-id="a80eb-142">Most resource types will open a gallery of Azure Monitor Workbook templates.</span><span class="sxs-lookup"><span data-stu-id="a80eb-142">Most resource types will open a gallery of Azure Monitor Workbook templates.</span></span> <span data-ttu-id="a80eb-143">Each workbook you create can be customized, saved, shared with your team, and reused in the future to diagnose similar issues.</span><span class="sxs-lookup"><span data-stu-id="a80eb-143">Each workbook you create can be customized, saved, shared with your team, and reused in the future to diagnose similar issues.</span></span>

### <a name="investigate-failures"></a><span data-ttu-id="a80eb-144">Investigate failures</span><span class="sxs-lookup"><span data-stu-id="a80eb-144">Investigate failures</span></span>

<span data-ttu-id="a80eb-145">To test out the Failures tab select **Failures** under **Investigate** in the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="a80eb-145">To test out the Failures tab select **Failures** under **Investigate** in the left-hand menu.</span></span>

<span data-ttu-id="a80eb-146">The left-side menu bar changes after your selection is made, offering you new options.</span><span class="sxs-lookup"><span data-stu-id="a80eb-146">The left-side menu bar changes after your selection is made, offering you new options.</span></span>

![Screenshot of Failure overview pane](.\media\resource-group-insights\00004-failures.png)

<span data-ttu-id="a80eb-148">When App Service is chosen, you are presented with a gallery of Azure Monitor Workbook templates.</span><span class="sxs-lookup"><span data-stu-id="a80eb-148">When App Service is chosen, you are presented with a gallery of Azure Monitor Workbook templates.</span></span>

![Screenshot of application workbook gallery](.\media\resource-group-insights\0005-failure-insights-workbook.png)

<span data-ttu-id="a80eb-150">Choosing the template for Failure Insights will open the workbook.</span><span class="sxs-lookup"><span data-stu-id="a80eb-150">Choosing the template for Failure Insights will open the workbook.</span></span>

![Screenshot of failure report](.\media\resource-group-insights\0006-failure-visual.png)

<span data-ttu-id="a80eb-152">You can select any of the rows.</span><span class="sxs-lookup"><span data-stu-id="a80eb-152">You can select any of the rows.</span></span> <span data-ttu-id="a80eb-153">The selection is then displayed in a graphical details view.</span><span class="sxs-lookup"><span data-stu-id="a80eb-153">The selection is then displayed in a graphical details view.</span></span>

![Screenshot of failure details](.\media\resource-group-insights\0007-failure-details.png)

<span data-ttu-id="a80eb-155">Workbooks abstract away the difficult work of creating custom reports and visualizations into an easily consumable format.</span><span class="sxs-lookup"><span data-stu-id="a80eb-155">Workbooks abstract away the difficult work of creating custom reports and visualizations into an easily consumable format.</span></span> <span data-ttu-id="a80eb-156">While some users may only want to adjust the prebuilt parameters, workbooks are completely customizable.</span><span class="sxs-lookup"><span data-stu-id="a80eb-156">While some users may only want to adjust the prebuilt parameters, workbooks are completely customizable.</span></span>

<span data-ttu-id="a80eb-157">To get a sense of how this workbook functions internally, select **Edit** in the top bar.</span><span class="sxs-lookup"><span data-stu-id="a80eb-157">To get a sense of how this workbook functions internally, select **Edit** in the top bar.</span></span>

![Screenshot of additional edit option](.\media\resource-group-insights\0008-failure-edit.png)

<span data-ttu-id="a80eb-159">A number of **Edit** boxes appear near the various elements of the workbook.</span><span class="sxs-lookup"><span data-stu-id="a80eb-159">A number of **Edit** boxes appear near the various elements of the workbook.</span></span> <span data-ttu-id="a80eb-160">Select the **Edit** box below the table of operations.</span><span class="sxs-lookup"><span data-stu-id="a80eb-160">Select the **Edit** box below the table of operations.</span></span>

![Screenshot of edit boxes](.\media\resource-group-insights\0009-failure-edit-graph.png)

<span data-ttu-id="a80eb-162">This reveals the underlying Log Analytics query that is driving the table visualization.</span><span class="sxs-lookup"><span data-stu-id="a80eb-162">This reveals the underlying Log Analytics query that is driving the table visualization.</span></span>

 ![Screenshot of log analytics query window](.\media\resource-group-insights\0010-failure-edit-query.png)

<span data-ttu-id="a80eb-164">You can modify the query directly.</span><span class="sxs-lookup"><span data-stu-id="a80eb-164">You can modify the query directly.</span></span> <span data-ttu-id="a80eb-165">Or you can use it as a reference and borrow from it when designing your own custom parameterized workbook.</span><span class="sxs-lookup"><span data-stu-id="a80eb-165">Or you can use it as a reference and borrow from it when designing your own custom parameterized workbook.</span></span>

### <a name="investigate-performance"></a><span data-ttu-id="a80eb-166">Investigate performance</span><span class="sxs-lookup"><span data-stu-id="a80eb-166">Investigate performance</span></span>

<span data-ttu-id="a80eb-167">Performance offers its own gallery of workbooks.</span><span class="sxs-lookup"><span data-stu-id="a80eb-167">Performance offers its own gallery of workbooks.</span></span> <span data-ttu-id="a80eb-168">For App Service the prebuilt Application Performance workbook offers the following view:</span><span class="sxs-lookup"><span data-stu-id="a80eb-168">For App Service the prebuilt Application Performance workbook offers the following view:</span></span>

 ![Screenshot of performance view](.\media\resource-group-insights\0011-performance.png)

<span data-ttu-id="a80eb-170">In this case, if you select edit you will see that this set of visualizations is powered by Azure Monitor Metrics.</span><span class="sxs-lookup"><span data-stu-id="a80eb-170">In this case, if you select edit you will see that this set of visualizations is powered by Azure Monitor Metrics.</span></span>

 ![Screenshot of performance view with Azure Metrics](.\media\resource-group-insights\0012-performance-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="a80eb-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="a80eb-172">Next steps</span></span>

- [<span data-ttu-id="a80eb-173">Azure Monitor Workbooks</span><span class="sxs-lookup"><span data-stu-id="a80eb-173">Azure Monitor Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)
- [<span data-ttu-id="a80eb-174">Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="a80eb-174">Azure Resource Health</span></span>](https://docs.microsoft.com/azure/service-health/resource-health-overview)
- [<span data-ttu-id="a80eb-175">Azure Monitor Alerts</span><span class="sxs-lookup"><span data-stu-id="a80eb-175">Azure Monitor Alerts</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-unified-alerts)
