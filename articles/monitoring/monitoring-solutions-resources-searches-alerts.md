---
title: Saved searches and alerts in management solutions | Microsoft Docs
description: Management solutions typically include saved searches in Log Analytics to analyze data collected by the solution.  They may also define alerts to notify the user or automatically take action in response to a critical issue.  This article describes how to define Log Analytics saved searches and alerts in a Resource Manager template so they can be included in management solutions.
services: monitoring
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/18/2018
ms.author: bwren, vinagara
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c29d6cb0da2e394912a2584b0d3c3cedf13f054c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869539"
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-management-solution-preview"></a><span data-ttu-id="a0bc8-105">Adding Log Analytics saved searches and alerts to management solution (Preview)</span><span class="sxs-lookup"><span data-stu-id="a0bc8-105">Adding Log Analytics saved searches and alerts to management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="a0bc8-106">This is preliminary documentation for creating management solutions which are currently in preview.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-106">This is preliminary documentation for creating management solutions which are currently in preview.</span></span> <span data-ttu-id="a0bc8-107">Any schema described below is subject to change.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="a0bc8-108">[Management solutions](monitoring-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-108">[Management solutions](monitoring-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="a0bc8-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="a0bc8-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](monitoring-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](monitoring-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a0bc8-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Design and build a management solution in Azure](monitoring-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="a0bc8-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Design and build a management solution in Azure](monitoring-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="a0bc8-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a0bc8-112">Prerequisites</span></span>
<span data-ttu-id="a0bc8-113">This article assumes that you're already familiar with how to [create a management solution](monitoring-solutions-creating.md) and the structure of a [Resource Manager template](../resource-group-authoring-templates.md) and solution file.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-113">This article assumes that you're already familiar with how to [create a management solution](monitoring-solutions-creating.md) and the structure of a [Resource Manager template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="a0bc8-114">Log Analytics Workspace</span><span class="sxs-lookup"><span data-stu-id="a0bc8-114">Log Analytics Workspace</span></span>
<span data-ttu-id="a0bc8-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="a0bc8-116">As described in [Log Analytics workspace and Automation account](monitoring-solutions.md#log-analytics-workspace-and-automation-account), the workspace isn't included in the management solution but must exist before the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-116">As described in [Log Analytics workspace and Automation account](monitoring-solutions.md#log-analytics-workspace-and-automation-account), the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="a0bc8-117">If it isn't available, then the solution install fails.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-117">If it isn't available, then the solution install fails.</span></span>

<span data-ttu-id="a0bc8-118">The name of the workspace is in the name of each Log Analytics resource.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="a0bc8-119">This is done in the solution with the **workspace** parameter as in the following example of a SavedSearch resource.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-119">This is done in the solution with the **workspace** parameter as in the following example of a SavedSearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"

## <a name="log-analytics-api-version"></a><span data-ttu-id="a0bc8-120">Log Analytics API version</span><span class="sxs-lookup"><span data-stu-id="a0bc8-120">Log Analytics API version</span></span>
<span data-ttu-id="a0bc8-121">All Log Analytics resources defined in a Resource Manager template have a property **apiVersion** that defines the version of the API the resource should use.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-121">All Log Analytics resources defined in a Resource Manager template have a property **apiVersion** that defines the version of the API the resource should use.</span></span>   

<span data-ttu-id="a0bc8-122">The following table lists the API version for the resource used in this example.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-122">The following table lists the API version for the resource used in this example.</span></span>

| <span data-ttu-id="a0bc8-123">Resource type</span><span class="sxs-lookup"><span data-stu-id="a0bc8-123">Resource type</span></span> | <span data-ttu-id="a0bc8-124">API version</span><span class="sxs-lookup"><span data-stu-id="a0bc8-124">API version</span></span> | <span data-ttu-id="a0bc8-125">Query</span><span class="sxs-lookup"><span data-stu-id="a0bc8-125">Query</span></span> |
|:---|:---|:---|
| <span data-ttu-id="a0bc8-126">savedSearches</span><span class="sxs-lookup"><span data-stu-id="a0bc8-126">savedSearches</span></span> | <span data-ttu-id="a0bc8-127">2017-03-15-preview</span><span class="sxs-lookup"><span data-stu-id="a0bc8-127">2017-03-15-preview</span></span> | <span data-ttu-id="a0bc8-128">Event &#124; where EventLevelName == "Error"</span><span class="sxs-lookup"><span data-stu-id="a0bc8-128">Event &#124; where EventLevelName == "Error"</span></span>  |


## <a name="saved-searches"></a><span data-ttu-id="a0bc8-129">Saved Searches</span><span class="sxs-lookup"><span data-stu-id="a0bc8-129">Saved Searches</span></span>
<span data-ttu-id="a0bc8-130">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-130">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="a0bc8-131">Saved searches appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-131">Saved searches appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal.</span></span>  <span data-ttu-id="a0bc8-132">A saved search is also required for each alert.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-132">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="a0bc8-133">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-133">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span>  <span data-ttu-id="a0bc8-134">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-134">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="a0bc8-135">Each property of a saved search is described in the following table.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-135">Each property of a saved search is described in the following table.</span></span> 

| <span data-ttu-id="a0bc8-136">Property</span><span class="sxs-lookup"><span data-stu-id="a0bc8-136">Property</span></span> | <span data-ttu-id="a0bc8-137">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-137">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a0bc8-138">category</span><span class="sxs-lookup"><span data-stu-id="a0bc8-138">category</span></span> | <span data-ttu-id="a0bc8-139">The category for the saved search.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-139">The category for the saved search.</span></span>  <span data-ttu-id="a0bc8-140">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-140">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="a0bc8-141">displayname</span><span class="sxs-lookup"><span data-stu-id="a0bc8-141">displayname</span></span> | <span data-ttu-id="a0bc8-142">Name to display for the saved search in the portal.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-142">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="a0bc8-143">query</span><span class="sxs-lookup"><span data-stu-id="a0bc8-143">query</span></span> | <span data-ttu-id="a0bc8-144">Query to run.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-144">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="a0bc8-145">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-145">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="a0bc8-146">For example, if your query was **Type: AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type: AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-146">For example, if your query was **Type: AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type: AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="a0bc8-147">Alerts</span><span class="sxs-lookup"><span data-stu-id="a0bc8-147">Alerts</span></span>
<span data-ttu-id="a0bc8-148">[Azure Log alerts](../monitoring-and-diagnostics/monitor-alerts-unified-log.md) are created by Azure Alert rules that run specified log queries at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-148">[Azure Log alerts](../monitoring-and-diagnostics/monitor-alerts-unified-log.md) are created by Azure Alert rules that run specified log queries at regular intervals.</span></span>  <span data-ttu-id="a0bc8-149">If the results of the query match specified criteria, an alert record is created and one or more actions are run using [Action Groups](../monitoring-and-diagnostics/monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-149">If the results of the query match specified criteria, an alert record is created and one or more actions are run using [Action Groups](../monitoring-and-diagnostics/monitoring-action-groups.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="a0bc8-150">Beginning May 14, 2018, all alerts in a workspace will automatically begin to extend into Azure.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-150">Beginning May 14, 2018, all alerts in a workspace will automatically begin to extend into Azure.</span></span> <span data-ttu-id="a0bc8-151">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-151">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="a0bc8-152">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-152">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span></span> <span data-ttu-id="a0bc8-153">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-153">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span></span> <span data-ttu-id="a0bc8-154">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group - Azure Resource Manager Template](../monitoring-and-diagnostics/monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-154">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group - Azure Resource Manager Template](../monitoring-and-diagnostics/monitoring-create-action-group-with-resource-manager-template.md).</span></span>

<span data-ttu-id="a0bc8-155">Alert rules in a management solution are made up of the following three different resources.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-155">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="a0bc8-156">**Saved search.**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-156">**Saved search.**</span></span>  <span data-ttu-id="a0bc8-157">Defines the log search that is run.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-157">Defines the log search that is run.</span></span>  <span data-ttu-id="a0bc8-158">Multiple alert rules can share a single saved search.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-158">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="a0bc8-159">**Schedule.**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-159">**Schedule.**</span></span>  <span data-ttu-id="a0bc8-160">Defines how often the log search is run.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-160">Defines how often the log search is run.</span></span>  <span data-ttu-id="a0bc8-161">Each alert rule has one and only one schedule.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-161">Each alert rule has one and only one schedule.</span></span>
- <span data-ttu-id="a0bc8-162">**Alert action.**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-162">**Alert action.**</span></span>  <span data-ttu-id="a0bc8-163">Each alert rule has one action group resource or action resource (legacy) with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record is created and the alert's severity.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-163">Each alert rule has one action group resource or action resource (legacy) with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record is created and the alert's severity.</span></span> <span data-ttu-id="a0bc8-164">[Action group](../monitoring-and-diagnostics/monitoring-action-groups.md) resource can have a list of configured actions to take when alert is fired - such as voice call, SMS, email, webhook, ITSM tool, automation runbook, logic app, etc.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-164">[Action group](../monitoring-and-diagnostics/monitoring-action-groups.md) resource can have a list of configured actions to take when alert is fired - such as voice call, SMS, email, webhook, ITSM tool, automation runbook, logic app, etc.</span></span>
 
<span data-ttu-id="a0bc8-165">The action resource (legacy) will optionally define a mail and runbook response.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-165">The action resource (legacy) will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="a0bc8-166">**Webhook action (legacy).**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-166">**Webhook action (legacy).**</span></span>  <span data-ttu-id="a0bc8-167">If the alert rule calls a webhook, then it requires an additional action resource with a type of **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-167">If the alert rule calls a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="a0bc8-168">Saved search resources are described above.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-168">Saved search resources are described above.</span></span>  <span data-ttu-id="a0bc8-169">The other resources are described below.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-169">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="a0bc8-170">Schedule resource</span><span class="sxs-lookup"><span data-stu-id="a0bc8-170">Schedule resource</span></span>

<span data-ttu-id="a0bc8-171">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-171">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="a0bc8-172">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-172">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="a0bc8-173">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-173">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> <span data-ttu-id="a0bc8-174">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-174">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="a0bc8-175">The properties for schedule resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-175">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="a0bc8-176">Element name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-176">Element name</span></span> | <span data-ttu-id="a0bc8-177">Required</span><span class="sxs-lookup"><span data-stu-id="a0bc8-177">Required</span></span> | <span data-ttu-id="a0bc8-178">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-178">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a0bc8-179">enabled</span><span class="sxs-lookup"><span data-stu-id="a0bc8-179">enabled</span></span>       | <span data-ttu-id="a0bc8-180">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-180">Yes</span></span> | <span data-ttu-id="a0bc8-181">Specifies whether the alert is enabled when it's created.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-181">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="a0bc8-182">interval</span><span class="sxs-lookup"><span data-stu-id="a0bc8-182">interval</span></span>      | <span data-ttu-id="a0bc8-183">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-183">Yes</span></span> | <span data-ttu-id="a0bc8-184">How often the query runs in minutes.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-184">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="a0bc8-185">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="a0bc8-185">queryTimeSpan</span></span> | <span data-ttu-id="a0bc8-186">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-186">Yes</span></span> | <span data-ttu-id="a0bc8-187">Length of time in minutes over which to evaluate results.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-187">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="a0bc8-188">The schedule resource should depend on the saved search so that it's created before the schedule.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-188">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>

> [!NOTE]
> <span data-ttu-id="a0bc8-189">Schedule Name must be unique in a given workspace; two schedules cannot have the same ID even if they are associated with different saved searches.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-189">Schedule Name must be unique in a given workspace; two schedules cannot have the same ID even if they are associated with different saved searches.</span></span> <span data-ttu-id="a0bc8-190">Also name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-190">Also name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>


### <a name="actions"></a><span data-ttu-id="a0bc8-191">Actions</span><span class="sxs-lookup"><span data-stu-id="a0bc8-191">Actions</span></span>
<span data-ttu-id="a0bc8-192">A schedule can have multiple actions.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-192">A schedule can have multiple actions.</span></span> <span data-ttu-id="a0bc8-193">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-193">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="a0bc8-194">Some actions will define both so that the processes are performed when the threshold is met.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-194">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="a0bc8-195">Actions can be defined using [action group] resource or action resource.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-195">Actions can be defined using [action group] resource or action resource.</span></span>

> [!NOTE]
> <span data-ttu-id="a0bc8-196">Beginning May 14, 2018, all alerts in a workspace will automatically begin to extend into Azure.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-196">Beginning May 14, 2018, all alerts in a workspace will automatically begin to extend into Azure.</span></span> <span data-ttu-id="a0bc8-197">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-197">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="a0bc8-198">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-198">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span></span> <span data-ttu-id="a0bc8-199">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-199">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span></span> <span data-ttu-id="a0bc8-200">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group - Azure Resource Manager Template](../monitoring-and-diagnostics/monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-200">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group - Azure Resource Manager Template](../monitoring-and-diagnostics/monitoring-create-action-group-with-resource-manager-template.md).</span></span>


<span data-ttu-id="a0bc8-201">There are two types of action resource specified by the **Type** property.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-201">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="a0bc8-202">A schedule requires one **Alert** action, which defines the details of the alert rule and what actions are taken when an alert is created.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-202">A schedule requires one **Alert** action, which defines the details of the alert rule and what actions are taken when an alert is created.</span></span> <span data-ttu-id="a0bc8-203">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-203">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

<span data-ttu-id="a0bc8-204">Alert actions have the following structure.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-204">Alert actions have the following structure.</span></span>  <span data-ttu-id="a0bc8-205">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-205">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


```
    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                  },
              },
      "AzNsNotification": {
        "GroupIds": "[variables('MyAlert').AzNsNotification.GroupIds]",
        "CustomEmailSubject": "[variables('MyAlert').AzNsNotification.CustomEmailSubject]",
        "CustomWebhookPayload": "[variables('MyAlert').AzNsNotification.CustomWebhookPayload]"
        }
        }
    }
```

<span data-ttu-id="a0bc8-206">The properties for Alert action resources are described in the following tables.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-206">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="a0bc8-207">Element name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-207">Element name</span></span> | <span data-ttu-id="a0bc8-208">Required</span><span class="sxs-lookup"><span data-stu-id="a0bc8-208">Required</span></span> | <span data-ttu-id="a0bc8-209">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-209">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a0bc8-210">Type</span><span class="sxs-lookup"><span data-stu-id="a0bc8-210">Type</span></span> | <span data-ttu-id="a0bc8-211">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-211">Yes</span></span> | <span data-ttu-id="a0bc8-212">Type of the action.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-212">Type of the action.</span></span>  <span data-ttu-id="a0bc8-213">This is **Alert** for alert actions.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-213">This is **Alert** for alert actions.</span></span> |
| <span data-ttu-id="a0bc8-214">Name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-214">Name</span></span> | <span data-ttu-id="a0bc8-215">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-215">Yes</span></span> | <span data-ttu-id="a0bc8-216">Display name for the alert.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-216">Display name for the alert.</span></span>  <span data-ttu-id="a0bc8-217">This is the name that's displayed in the console for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-217">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="a0bc8-218">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-218">Description</span></span> | <span data-ttu-id="a0bc8-219">No</span><span class="sxs-lookup"><span data-stu-id="a0bc8-219">No</span></span> | <span data-ttu-id="a0bc8-220">Optional description of the alert.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-220">Optional description of the alert.</span></span> |
| <span data-ttu-id="a0bc8-221">Severity</span><span class="sxs-lookup"><span data-stu-id="a0bc8-221">Severity</span></span> | <span data-ttu-id="a0bc8-222">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-222">Yes</span></span> | <span data-ttu-id="a0bc8-223">Severity of the alert record from the following values:</span><span class="sxs-lookup"><span data-stu-id="a0bc8-223">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="a0bc8-224">**critical**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-224">**critical**</span></span><br><span data-ttu-id="a0bc8-225">**warning**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-225">**warning**</span></span><br><span data-ttu-id="a0bc8-226">**informational**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-226">**informational**</span></span>


#### <a name="threshold"></a><span data-ttu-id="a0bc8-227">Threshold</span><span class="sxs-lookup"><span data-stu-id="a0bc8-227">Threshold</span></span>
<span data-ttu-id="a0bc8-228">This section is required.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-228">This section is required.</span></span>  <span data-ttu-id="a0bc8-229">It defines the properties for the alert threshold.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-229">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="a0bc8-230">Element name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-230">Element name</span></span> | <span data-ttu-id="a0bc8-231">Required</span><span class="sxs-lookup"><span data-stu-id="a0bc8-231">Required</span></span> | <span data-ttu-id="a0bc8-232">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-232">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a0bc8-233">Operator</span><span class="sxs-lookup"><span data-stu-id="a0bc8-233">Operator</span></span> | <span data-ttu-id="a0bc8-234">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-234">Yes</span></span> | <span data-ttu-id="a0bc8-235">Operator for the comparison from the following values:</span><span class="sxs-lookup"><span data-stu-id="a0bc8-235">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="a0bc8-236">**gt = greater than<br>lt = less than**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-236">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="a0bc8-237">Value</span><span class="sxs-lookup"><span data-stu-id="a0bc8-237">Value</span></span> | <span data-ttu-id="a0bc8-238">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-238">Yes</span></span> | <span data-ttu-id="a0bc8-239">The value to compare the results.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-239">The value to compare the results.</span></span> |

##### <a name="metricstrigger"></a><span data-ttu-id="a0bc8-240">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="a0bc8-240">MetricsTrigger</span></span>
<span data-ttu-id="a0bc8-241">This section is optional.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-241">This section is optional.</span></span>  <span data-ttu-id="a0bc8-242">Include it for a metric measurement alert.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-242">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="a0bc8-243">Metric measurement alerts are currently in public preview.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-243">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="a0bc8-244">Element name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-244">Element name</span></span> | <span data-ttu-id="a0bc8-245">Required</span><span class="sxs-lookup"><span data-stu-id="a0bc8-245">Required</span></span> | <span data-ttu-id="a0bc8-246">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-246">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a0bc8-247">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="a0bc8-247">TriggerCondition</span></span> | <span data-ttu-id="a0bc8-248">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-248">Yes</span></span> | <span data-ttu-id="a0bc8-249">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span><span class="sxs-lookup"><span data-stu-id="a0bc8-249">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="a0bc8-250">**Total<br>Consecutive**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-250">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="a0bc8-251">Operator</span><span class="sxs-lookup"><span data-stu-id="a0bc8-251">Operator</span></span> | <span data-ttu-id="a0bc8-252">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-252">Yes</span></span> | <span data-ttu-id="a0bc8-253">Operator for the comparison from the following values:</span><span class="sxs-lookup"><span data-stu-id="a0bc8-253">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="a0bc8-254">**gt = greater than<br>lt = less than**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-254">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="a0bc8-255">Value</span><span class="sxs-lookup"><span data-stu-id="a0bc8-255">Value</span></span> | <span data-ttu-id="a0bc8-256">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-256">Yes</span></span> | <span data-ttu-id="a0bc8-257">Number of the times the criteria must be met to trigger the alert.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-257">Number of the times the criteria must be met to trigger the alert.</span></span> |


#### <a name="throttling"></a><span data-ttu-id="a0bc8-258">Throttling</span><span class="sxs-lookup"><span data-stu-id="a0bc8-258">Throttling</span></span>
<span data-ttu-id="a0bc8-259">This section is optional.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-259">This section is optional.</span></span>  <span data-ttu-id="a0bc8-260">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-260">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="a0bc8-261">Element name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-261">Element name</span></span> | <span data-ttu-id="a0bc8-262">Required</span><span class="sxs-lookup"><span data-stu-id="a0bc8-262">Required</span></span> | <span data-ttu-id="a0bc8-263">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-263">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a0bc8-264">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-264">DurationInMinutes</span></span> | <span data-ttu-id="a0bc8-265">Yes if Throttling element included</span><span class="sxs-lookup"><span data-stu-id="a0bc8-265">Yes if Throttling element included</span></span> | <span data-ttu-id="a0bc8-266">Number of minutes to suppress alerts after one from the same alert rule is created.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-266">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |


#### <a name="azure-action-group"></a><span data-ttu-id="a0bc8-267">Azure action group</span><span class="sxs-lookup"><span data-stu-id="a0bc8-267">Azure action group</span></span>
<span data-ttu-id="a0bc8-268">All alerts in Azure, use Action Group as the default mechanism for handling actions.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-268">All alerts in Azure, use Action Group as the default mechanism for handling actions.</span></span> <span data-ttu-id="a0bc8-269">With Action Group, you can specify your actions once and then associate the action group to multiple alerts - across Azure.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-269">With Action Group, you can specify your actions once and then associate the action group to multiple alerts - across Azure.</span></span> <span data-ttu-id="a0bc8-270">Without the need, to repeatedly declare the same actions over and over again.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-270">Without the need, to repeatedly declare the same actions over and over again.</span></span> <span data-ttu-id="a0bc8-271">Action Groups support multiple actions - including email, SMS, Voice Call, ITSM Connection, Automation Runbook, Webhook URI and more.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-271">Action Groups support multiple actions - including email, SMS, Voice Call, ITSM Connection, Automation Runbook, Webhook URI and more.</span></span> 

<span data-ttu-id="a0bc8-272">For user's who have extended their alerts into Azure - a schedule should now have Action Group details passed along with threshold, to be able to create an alert.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-272">For user's who have extended their alerts into Azure - a schedule should now have Action Group details passed along with threshold, to be able to create an alert.</span></span> <span data-ttu-id="a0bc8-273">E-mail details, Webhook URLs, Runbook Automation details, and other Actions, need to be defined in side an Action Group first before creating an alert; one can create [Action Group from Azure Monitor](../monitoring-and-diagnostics/monitoring-action-groups.md) in Portal or use [Action Group - Resource Template](../monitoring-and-diagnostics/monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-273">E-mail details, Webhook URLs, Runbook Automation details, and other Actions, need to be defined in side an Action Group first before creating an alert; one can create [Action Group from Azure Monitor](../monitoring-and-diagnostics/monitoring-action-groups.md) in Portal or use [Action Group - Resource Template](../monitoring-and-diagnostics/monitoring-create-action-group-with-resource-manager-template.md).</span></span>

| <span data-ttu-id="a0bc8-274">Element name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-274">Element name</span></span> | <span data-ttu-id="a0bc8-275">Required</span><span class="sxs-lookup"><span data-stu-id="a0bc8-275">Required</span></span> | <span data-ttu-id="a0bc8-276">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-276">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a0bc8-277">AzNsNotification</span><span class="sxs-lookup"><span data-stu-id="a0bc8-277">AzNsNotification</span></span> | <span data-ttu-id="a0bc8-278">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-278">Yes</span></span> | <span data-ttu-id="a0bc8-279">The resource ID of the Azure action group to be associated with alert for taking necessary actions when alert criteria is met.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-279">The resource ID of the Azure action group to be associated with alert for taking necessary actions when alert criteria is met.</span></span> |
| <span data-ttu-id="a0bc8-280">CustomEmailSubject</span><span class="sxs-lookup"><span data-stu-id="a0bc8-280">CustomEmailSubject</span></span> | <span data-ttu-id="a0bc8-281">No</span><span class="sxs-lookup"><span data-stu-id="a0bc8-281">No</span></span> | <span data-ttu-id="a0bc8-282">Custom subject line of the mail sent to all addresses specified in associated action group.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-282">Custom subject line of the mail sent to all addresses specified in associated action group.</span></span> |
| <span data-ttu-id="a0bc8-283">CustomWebhookPayload</span><span class="sxs-lookup"><span data-stu-id="a0bc8-283">CustomWebhookPayload</span></span> | <span data-ttu-id="a0bc8-284">No</span><span class="sxs-lookup"><span data-stu-id="a0bc8-284">No</span></span> | <span data-ttu-id="a0bc8-285">Customized payload to be sent to all webhook endpoints defined in associated action group.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-285">Customized payload to be sent to all webhook endpoints defined in associated action group.</span></span> <span data-ttu-id="a0bc8-286">The format depends on what the webhook is expecting and should be a valid serialized JSON.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-286">The format depends on what the webhook is expecting and should be a valid serialized JSON.</span></span> |


#### <a name="actions-for-oms-legacy"></a><span data-ttu-id="a0bc8-287">Actions for OMS (legacy)</span><span class="sxs-lookup"><span data-stu-id="a0bc8-287">Actions for OMS (legacy)</span></span>

<span data-ttu-id="a0bc8-288">Every schedule has one **Alert** action.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-288">Every schedule has one **Alert** action.</span></span>  <span data-ttu-id="a0bc8-289">This defines the details of the alert and optionally notification and remediation actions.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-289">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="a0bc8-290">A notification sends an email to one or more addresses.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-290">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="a0bc8-291">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-291">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

> [!NOTE]
> <span data-ttu-id="a0bc8-292">Beginning May 14, 2018, all alerts in a workspace will automatically begin to extend into Azure.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-292">Beginning May 14, 2018, all alerts in a workspace will automatically begin to extend into Azure.</span></span> <span data-ttu-id="a0bc8-293">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-293">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="a0bc8-294">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-294">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span></span> <span data-ttu-id="a0bc8-295">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-295">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span></span> <span data-ttu-id="a0bc8-296">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group - Azure Resource Manager Template](../monitoring-and-diagnostics/monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="a0bc8-296">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group - Azure Resource Manager Template](../monitoring-and-diagnostics/monitoring-create-action-group-with-resource-manager-template.md).</span></span>

##### <a name="emailnotification"></a><span data-ttu-id="a0bc8-297">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="a0bc8-297">EmailNotification</span></span>
 <span data-ttu-id="a0bc8-298">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-298">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="a0bc8-299">Element name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-299">Element name</span></span> | <span data-ttu-id="a0bc8-300">Required</span><span class="sxs-lookup"><span data-stu-id="a0bc8-300">Required</span></span> | <span data-ttu-id="a0bc8-301">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-301">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a0bc8-302">Recipients</span><span class="sxs-lookup"><span data-stu-id="a0bc8-302">Recipients</span></span> | <span data-ttu-id="a0bc8-303">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-303">Yes</span></span> | <span data-ttu-id="a0bc8-304">Comma-delimited list of email addresses to send notification when an alert is created such as in the following example.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-304">Comma-delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="a0bc8-305">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="a0bc8-305">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="a0bc8-306">Subject</span><span class="sxs-lookup"><span data-stu-id="a0bc8-306">Subject</span></span> | <span data-ttu-id="a0bc8-307">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-307">Yes</span></span> | <span data-ttu-id="a0bc8-308">Subject line of the mail.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-308">Subject line of the mail.</span></span> |
| <span data-ttu-id="a0bc8-309">Attachment</span><span class="sxs-lookup"><span data-stu-id="a0bc8-309">Attachment</span></span> | <span data-ttu-id="a0bc8-310">No</span><span class="sxs-lookup"><span data-stu-id="a0bc8-310">No</span></span> | <span data-ttu-id="a0bc8-311">Attachments are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-311">Attachments are not currently supported.</span></span>  <span data-ttu-id="a0bc8-312">If this element is included, it should be **None**.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-312">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="a0bc8-313">Remediation</span><span class="sxs-lookup"><span data-stu-id="a0bc8-313">Remediation</span></span>
<span data-ttu-id="a0bc8-314">This section is optional  Include it if you want a runbook to start in response to the alert.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-314">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="a0bc8-315">Element name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-315">Element name</span></span> | <span data-ttu-id="a0bc8-316">Required</span><span class="sxs-lookup"><span data-stu-id="a0bc8-316">Required</span></span> | <span data-ttu-id="a0bc8-317">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-317">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a0bc8-318">RunbookName</span><span class="sxs-lookup"><span data-stu-id="a0bc8-318">RunbookName</span></span> | <span data-ttu-id="a0bc8-319">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-319">Yes</span></span> | <span data-ttu-id="a0bc8-320">Name of the runbook to start.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-320">Name of the runbook to start.</span></span> |
| <span data-ttu-id="a0bc8-321">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="a0bc8-321">WebhookUri</span></span> | <span data-ttu-id="a0bc8-322">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-322">Yes</span></span> | <span data-ttu-id="a0bc8-323">Uri of the webhook for the runbook.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-323">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="a0bc8-324">Expiry</span><span class="sxs-lookup"><span data-stu-id="a0bc8-324">Expiry</span></span> | <span data-ttu-id="a0bc8-325">No</span><span class="sxs-lookup"><span data-stu-id="a0bc8-325">No</span></span> | <span data-ttu-id="a0bc8-326">Date and time that the remediation expires.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-326">Date and time that the remediation expires.</span></span> |

##### <a name="webhook-actions"></a><span data-ttu-id="a0bc8-327">Webhook actions</span><span class="sxs-lookup"><span data-stu-id="a0bc8-327">Webhook actions</span></span>

<span data-ttu-id="a0bc8-328">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-328">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="a0bc8-329">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-329">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="a0bc8-330">They also provide the additional option of providing a payload to be delivered to the remote process.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-330">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="a0bc8-331">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-331">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="a0bc8-332">The properties for Webhook action resources are described in the following tables.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-332">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="a0bc8-333">Element name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-333">Element name</span></span> | <span data-ttu-id="a0bc8-334">Required</span><span class="sxs-lookup"><span data-stu-id="a0bc8-334">Required</span></span> | <span data-ttu-id="a0bc8-335">Description</span><span class="sxs-lookup"><span data-stu-id="a0bc8-335">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a0bc8-336">type</span><span class="sxs-lookup"><span data-stu-id="a0bc8-336">type</span></span> | <span data-ttu-id="a0bc8-337">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-337">Yes</span></span> | <span data-ttu-id="a0bc8-338">Type of the action.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-338">Type of the action.</span></span>  <span data-ttu-id="a0bc8-339">This is **Webhook** for webhook actions.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-339">This is **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="a0bc8-340">name</span><span class="sxs-lookup"><span data-stu-id="a0bc8-340">name</span></span> | <span data-ttu-id="a0bc8-341">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-341">Yes</span></span> | <span data-ttu-id="a0bc8-342">Display name for the action.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-342">Display name for the action.</span></span>  <span data-ttu-id="a0bc8-343">This is not displayed in the console.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-343">This is not displayed in the console.</span></span> |
| <span data-ttu-id="a0bc8-344">wehookUri</span><span class="sxs-lookup"><span data-stu-id="a0bc8-344">wehookUri</span></span> | <span data-ttu-id="a0bc8-345">Yes</span><span class="sxs-lookup"><span data-stu-id="a0bc8-345">Yes</span></span> | <span data-ttu-id="a0bc8-346">Uri for the webhook.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-346">Uri for the webhook.</span></span> |
| <span data-ttu-id="a0bc8-347">customPayload</span><span class="sxs-lookup"><span data-stu-id="a0bc8-347">customPayload</span></span> | <span data-ttu-id="a0bc8-348">No</span><span class="sxs-lookup"><span data-stu-id="a0bc8-348">No</span></span> | <span data-ttu-id="a0bc8-349">Custom payload to be sent to the webhook.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-349">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="a0bc8-350">The format depends on what the webhook is expecting.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-350">The format depends on what the webhook is expecting.</span></span> |


## <a name="sample"></a><span data-ttu-id="a0bc8-351">Sample</span><span class="sxs-lookup"><span data-stu-id="a0bc8-351">Sample</span></span>

<span data-ttu-id="a0bc8-352">Following is a sample of a solution that includes that includes the following resources:</span><span class="sxs-lookup"><span data-stu-id="a0bc8-352">Following is a sample of a solution that includes that includes the following resources:</span></span>

- <span data-ttu-id="a0bc8-353">Saved search</span><span class="sxs-lookup"><span data-stu-id="a0bc8-353">Saved search</span></span>
- <span data-ttu-id="a0bc8-354">Schedule</span><span class="sxs-lookup"><span data-stu-id="a0bc8-354">Schedule</span></span>
- <span data-ttu-id="a0bc8-355">Action group</span><span class="sxs-lookup"><span data-stu-id="a0bc8-355">Action group</span></span>

<span data-ttu-id="a0bc8-356">The sample uses [standard solution parameters]( monitoring-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-356">The sample uses [standard solution parameters]( monitoring-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

```
    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "actiongroup": {
            "type": "string",
            "metadata": {
              "Description": "List of action groups for alert actions separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion-Search": "2017-03-15-preview",
              "LogAnalyticsApiVersion-Solution": "2015-11-01-preview",

          "MySearch": {
            "displayName": "Error records by hour",
            "query": "MyRecord_CL | summarize AggregatedValue = avg(Rating_d) by Instance_s, bin(TimeGenerated, 60m)",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "AzNsNotification": {
              "GroupIds": [
                "[parameters('actiongroup')]"
              ],
              "CustomEmailSubject": "Sample alert"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion-Solution')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion-Search')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion-Search')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion-Search')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
            "AzNsNotification": {
              "GroupIds": "[variables('MyAlert').AzNsNotification.GroupIds]",
              "CustomEmailSubject": "[variables('MyAlert').AzNsNotification.CustomEmailSubject]"
            }             
            }
          }
        ]
    }
```

<span data-ttu-id="a0bc8-357">The following parameter file provides samples values for this solution.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-357">The following parameter file provides samples values for this solution.</span></span>
```
    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "actiongroup": {
                "value": "/subscriptions/3b540246-808d-4331-99aa-917b808a9166/resourcegroups/myTestGroup/providers/microsoft.insights/actiongroups/sample"
            }
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="a0bc8-358">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0bc8-358">Next steps</span></span>
* <span data-ttu-id="a0bc8-359">[Add views](monitoring-solutions-resources-views.md) to your management solution.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-359">[Add views](monitoring-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="a0bc8-360">[Add Automation runbooks and other resources](monitoring-solutions-resources-automation.md) to your management solution.</span><span class="sxs-lookup"><span data-stu-id="a0bc8-360">[Add Automation runbooks and other resources](monitoring-solutions-resources-automation.md) to your management solution.</span></span>

