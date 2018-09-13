---
title: Saved searches and alerts in OMS solutions | Microsoft Docs
description: Solutions in OMS will typically include saved searches in Log Analytics to analyze data collected by the solution.  They may also define alerts to notify the user or automatically take action in response to a critical issue.  This article describes how to define Log Analytics saved searches and alerts in an ARM template so they can be included in management solutions.
services: operations-management-suite
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 35264f1ec5df5a3e171f7631e0d3b46bf9c0b8e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562777"
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a><span data-ttu-id="81575-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span><span class="sxs-lookup"><span data-stu-id="81575-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="81575-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span><span class="sxs-lookup"><span data-stu-id="81575-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="81575-107">Any schema described below is subject to change.</span><span class="sxs-lookup"><span data-stu-id="81575-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="81575-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span><span class="sxs-lookup"><span data-stu-id="81575-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="81575-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span><span class="sxs-lookup"><span data-stu-id="81575-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="81575-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="81575-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="81575-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="81575-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="81575-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="81575-112">Prerequisites</span></span>
<span data-ttu-id="81575-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span><span class="sxs-lookup"><span data-stu-id="81575-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="81575-114">Log Analytics Workspace</span><span class="sxs-lookup"><span data-stu-id="81575-114">Log Analytics Workspace</span></span>
<span data-ttu-id="81575-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="81575-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="81575-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span><span class="sxs-lookup"><span data-stu-id="81575-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="81575-117">If it isn't available, then the solution install will fail.</span><span class="sxs-lookup"><span data-stu-id="81575-117">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="81575-118">The name of the workspace is in the name of each Log Analytics resource.</span><span class="sxs-lookup"><span data-stu-id="81575-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="81575-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span><span class="sxs-lookup"><span data-stu-id="81575-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="81575-120">Saved Searches</span><span class="sxs-lookup"><span data-stu-id="81575-120">Saved Searches</span></span>
<span data-ttu-id="81575-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span><span class="sxs-lookup"><span data-stu-id="81575-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="81575-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span><span class="sxs-lookup"><span data-stu-id="81575-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span></span>  <span data-ttu-id="81575-123">A saved search is also required for each alert.</span><span class="sxs-lookup"><span data-stu-id="81575-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="81575-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="81575-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span> 

    {
        "name": "<name-of-savedsearch>"
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "<api-version-of-resource>",
        "dependsOn": []
        "tags": {},
        "properties": {
            "etag": "*",
            "query": "<query-to-run>",
            "displayName": "<saved-search-display-name>",
            "category": ""<saved-search-category>"
        }
    }

<span data-ttu-id="81575-125">Each of the properties of a saved search are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="81575-125">Each of the properties of a saved search are described in the following table.</span></span> 

| <span data-ttu-id="81575-126">Property</span><span class="sxs-lookup"><span data-stu-id="81575-126">Property</span></span> | <span data-ttu-id="81575-127">Description</span><span class="sxs-lookup"><span data-stu-id="81575-127">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="81575-128">category</span><span class="sxs-lookup"><span data-stu-id="81575-128">category</span></span> | <span data-ttu-id="81575-129">The category for the saved search.</span><span class="sxs-lookup"><span data-stu-id="81575-129">The category for the saved search.</span></span>  <span data-ttu-id="81575-130">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span><span class="sxs-lookup"><span data-stu-id="81575-130">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="81575-131">displayname</span><span class="sxs-lookup"><span data-stu-id="81575-131">displayname</span></span> | <span data-ttu-id="81575-132">Name to display for the saved search in the portal.</span><span class="sxs-lookup"><span data-stu-id="81575-132">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="81575-133">query</span><span class="sxs-lookup"><span data-stu-id="81575-133">query</span></span> | <span data-ttu-id="81575-134">Query to run.</span><span class="sxs-lookup"><span data-stu-id="81575-134">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="81575-135">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span><span class="sxs-lookup"><span data-stu-id="81575-135">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="81575-136">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="81575-136">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="81575-137">Alerts</span><span class="sxs-lookup"><span data-stu-id="81575-137">Alerts</span></span>
<span data-ttu-id="81575-138">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span><span class="sxs-lookup"><span data-stu-id="81575-138">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="81575-139">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span><span class="sxs-lookup"><span data-stu-id="81575-139">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="81575-140">Alert rules in a management solution are made up of the following three different resources.</span><span class="sxs-lookup"><span data-stu-id="81575-140">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="81575-141">**Saved search.**</span><span class="sxs-lookup"><span data-stu-id="81575-141">**Saved search.**</span></span>  <span data-ttu-id="81575-142">Defines the log search that will be run.</span><span class="sxs-lookup"><span data-stu-id="81575-142">Defines the log search that will be run.</span></span>  <span data-ttu-id="81575-143">Multiple alert rules can share a single saved search.</span><span class="sxs-lookup"><span data-stu-id="81575-143">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="81575-144">**Schedule.**</span><span class="sxs-lookup"><span data-stu-id="81575-144">**Schedule.**</span></span>  <span data-ttu-id="81575-145">Defines how often the log search will be run.</span><span class="sxs-lookup"><span data-stu-id="81575-145">Defines how often the log search will be run.</span></span>  <span data-ttu-id="81575-146">Each alert rule will have one and only one schedule.</span><span class="sxs-lookup"><span data-stu-id="81575-146">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="81575-147">**Alert action.**</span><span class="sxs-lookup"><span data-stu-id="81575-147">**Alert action.**</span></span>  <span data-ttu-id="81575-148">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span><span class="sxs-lookup"><span data-stu-id="81575-148">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span></span>  <span data-ttu-id="81575-149">The action resource will optionally define a mail and runbook response.</span><span class="sxs-lookup"><span data-stu-id="81575-149">The action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="81575-150">**Webhook action (optional).**</span><span class="sxs-lookup"><span data-stu-id="81575-150">**Webhook action (optional).**</span></span>  <span data-ttu-id="81575-151">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="81575-151">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="81575-152">Saved search resources are described above.</span><span class="sxs-lookup"><span data-stu-id="81575-152">Saved search resources are described above.</span></span>  <span data-ttu-id="81575-153">The other resources are described below.</span><span class="sxs-lookup"><span data-stu-id="81575-153">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="81575-154">Schedule resource</span><span class="sxs-lookup"><span data-stu-id="81575-154">Schedule resource</span></span>

<span data-ttu-id="81575-155">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span><span class="sxs-lookup"><span data-stu-id="81575-155">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="81575-156">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span><span class="sxs-lookup"><span data-stu-id="81575-156">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="81575-157">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span><span class="sxs-lookup"><span data-stu-id="81575-157">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> 

    {
      "name": "<name-of-schedule-resource>",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
      "apiVersion": "<api-version-of-resource>",
      "dependsOn": [
        "<name-of-saved-search>"
      ],
      "properties": {  
        "etag": "*",               
        "interval": <schedule-interval-in-minutes>,
        "queryTimeSpan": <query-timespan-in-minutes>,
        "enabled": <schedule-enabled>       
      }
    }

<span data-ttu-id="81575-158">The properties for schedule resources are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="81575-158">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="81575-159">Element name</span><span class="sxs-lookup"><span data-stu-id="81575-159">Element name</span></span> | <span data-ttu-id="81575-160">Required</span><span class="sxs-lookup"><span data-stu-id="81575-160">Required</span></span> | <span data-ttu-id="81575-161">Description</span><span class="sxs-lookup"><span data-stu-id="81575-161">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="81575-162">enabled</span><span class="sxs-lookup"><span data-stu-id="81575-162">enabled</span></span>       | <span data-ttu-id="81575-163">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-163">Yes</span></span> | <span data-ttu-id="81575-164">Specifies whether the alert is enabled when it's created.</span><span class="sxs-lookup"><span data-stu-id="81575-164">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="81575-165">interval</span><span class="sxs-lookup"><span data-stu-id="81575-165">interval</span></span>      | <span data-ttu-id="81575-166">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-166">Yes</span></span> | <span data-ttu-id="81575-167">How often the query runs in minutes.</span><span class="sxs-lookup"><span data-stu-id="81575-167">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="81575-168">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="81575-168">queryTimeSpan</span></span> | <span data-ttu-id="81575-169">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-169">Yes</span></span> | <span data-ttu-id="81575-170">Length of time in minutes over which to evaluate results.</span><span class="sxs-lookup"><span data-stu-id="81575-170">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="81575-171">The schedule resource should depend on the saved search so that it's created before the schedule.</span><span class="sxs-lookup"><span data-stu-id="81575-171">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="81575-172">Actions</span><span class="sxs-lookup"><span data-stu-id="81575-172">Actions</span></span>
<span data-ttu-id="81575-173">There are two types of action resource specified by the **Type** property.</span><span class="sxs-lookup"><span data-stu-id="81575-173">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="81575-174">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span><span class="sxs-lookup"><span data-stu-id="81575-174">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="81575-175">It may also include a **Webhook** action if a webhook should be called from the alert.</span><span class="sxs-lookup"><span data-stu-id="81575-175">It may also include a **Webhook** action if a webhook should be called from the alert.</span></span>  

<span data-ttu-id="81575-176">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="81575-176">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="81575-177">Alert actions</span><span class="sxs-lookup"><span data-stu-id="81575-177">Alert actions</span></span>

<span data-ttu-id="81575-178">Every schedule will have one **Alert** action.</span><span class="sxs-lookup"><span data-stu-id="81575-178">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="81575-179">This defines the details of the alert and optionally notification and remediation actions.</span><span class="sxs-lookup"><span data-stu-id="81575-179">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="81575-180">A notification sends an email to one or more addresses.</span><span class="sxs-lookup"><span data-stu-id="81575-180">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="81575-181">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span><span class="sxs-lookup"><span data-stu-id="81575-181">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

<span data-ttu-id="81575-182">Alert actions have the following structure.</span><span class="sxs-lookup"><span data-stu-id="81575-182">Alert actions have the following structure.</span></span>

    {
        "name": "<name-of-the-action>",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "<api-version-of-resource>",
        "dependsOn": [
            <name-of-schedule>
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "<display-name-of-alert>",
            "description": "<description-of-alert>",
            "severity": "<severity-of-alert>",
            "threshold": {
                "operator": "<threshold-operator>",
                "value": "<threshold-value>"
                "metricsTrigger": {
                    "triggerCondition": "<trigger-condition>",
                    "operator": "<trigger-operator>",
                    "value": "<trigger-value>"
                },
            },
            "throttling": {
                "durationInMinutes": "<throttling-duration-in-minutes>"
            },
            "emailNotification": {
                "recipients": [
                    <mail-recipients>
                ],
                "subject": "<mail-subject>",
                "attachment": "None"
            },
            "remediation": {
                "runbookName": "<name-of-runbook>",
                "webhookUri": "<runbook-uri>"
            }
        }
    }

<span data-ttu-id="81575-183">The properties for Alert action resources are described in the following tables.</span><span class="sxs-lookup"><span data-stu-id="81575-183">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="81575-184">Element name</span><span class="sxs-lookup"><span data-stu-id="81575-184">Element name</span></span> | <span data-ttu-id="81575-185">Required</span><span class="sxs-lookup"><span data-stu-id="81575-185">Required</span></span> | <span data-ttu-id="81575-186">Description</span><span class="sxs-lookup"><span data-stu-id="81575-186">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="81575-187">Type</span><span class="sxs-lookup"><span data-stu-id="81575-187">Type</span></span> | <span data-ttu-id="81575-188">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-188">Yes</span></span> | <span data-ttu-id="81575-189">Type of the action.</span><span class="sxs-lookup"><span data-stu-id="81575-189">Type of the action.</span></span>  <span data-ttu-id="81575-190">This will be **Alert** for alert actions.</span><span class="sxs-lookup"><span data-stu-id="81575-190">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="81575-191">Name</span><span class="sxs-lookup"><span data-stu-id="81575-191">Name</span></span> | <span data-ttu-id="81575-192">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-192">Yes</span></span> | <span data-ttu-id="81575-193">Display name for the alert.</span><span class="sxs-lookup"><span data-stu-id="81575-193">Display name for the alert.</span></span>  <span data-ttu-id="81575-194">This is the name that's displayed in the console for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="81575-194">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="81575-195">Description</span><span class="sxs-lookup"><span data-stu-id="81575-195">Description</span></span> | <span data-ttu-id="81575-196">No</span><span class="sxs-lookup"><span data-stu-id="81575-196">No</span></span> | <span data-ttu-id="81575-197">Optional description of the alert.</span><span class="sxs-lookup"><span data-stu-id="81575-197">Optional description of the alert.</span></span> |
| <span data-ttu-id="81575-198">Severity</span><span class="sxs-lookup"><span data-stu-id="81575-198">Severity</span></span> | <span data-ttu-id="81575-199">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-199">Yes</span></span> | <span data-ttu-id="81575-200">Severity of the alert record from the following values:</span><span class="sxs-lookup"><span data-stu-id="81575-200">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="81575-201">**Critical**</span><span class="sxs-lookup"><span data-stu-id="81575-201">**Critical**</span></span><br><span data-ttu-id="81575-202">**Warning**</span><span class="sxs-lookup"><span data-stu-id="81575-202">**Warning**</span></span><br><span data-ttu-id="81575-203">**Informational**</span><span class="sxs-lookup"><span data-stu-id="81575-203">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="81575-204">Threshold</span><span class="sxs-lookup"><span data-stu-id="81575-204">Threshold</span></span>
<span data-ttu-id="81575-205">This section is required.</span><span class="sxs-lookup"><span data-stu-id="81575-205">This section is required.</span></span>  <span data-ttu-id="81575-206">It defines the properties for the alert threshold.</span><span class="sxs-lookup"><span data-stu-id="81575-206">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="81575-207">Element name</span><span class="sxs-lookup"><span data-stu-id="81575-207">Element name</span></span> | <span data-ttu-id="81575-208">Required</span><span class="sxs-lookup"><span data-stu-id="81575-208">Required</span></span> | <span data-ttu-id="81575-209">Description</span><span class="sxs-lookup"><span data-stu-id="81575-209">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="81575-210">Operator</span><span class="sxs-lookup"><span data-stu-id="81575-210">Operator</span></span> | <span data-ttu-id="81575-211">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-211">Yes</span></span> | <span data-ttu-id="81575-212">Operator for the comparison from the following values:</span><span class="sxs-lookup"><span data-stu-id="81575-212">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="81575-213">**gt = greater than<br>lt = less than**</span><span class="sxs-lookup"><span data-stu-id="81575-213">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="81575-214">Value</span><span class="sxs-lookup"><span data-stu-id="81575-214">Value</span></span> | <span data-ttu-id="81575-215">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-215">Yes</span></span> | <span data-ttu-id="81575-216">The value to compare the results.</span><span class="sxs-lookup"><span data-stu-id="81575-216">The value to compare the results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="81575-217">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="81575-217">MetricsTrigger</span></span>
<span data-ttu-id="81575-218">This section is optional.</span><span class="sxs-lookup"><span data-stu-id="81575-218">This section is optional.</span></span>  <span data-ttu-id="81575-219">Include it for a metric measurement alert.</span><span class="sxs-lookup"><span data-stu-id="81575-219">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="81575-220">Metric measurement alerts are currently in public preview.</span><span class="sxs-lookup"><span data-stu-id="81575-220">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="81575-221">Element name</span><span class="sxs-lookup"><span data-stu-id="81575-221">Element name</span></span> | <span data-ttu-id="81575-222">Required</span><span class="sxs-lookup"><span data-stu-id="81575-222">Required</span></span> | <span data-ttu-id="81575-223">Description</span><span class="sxs-lookup"><span data-stu-id="81575-223">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="81575-224">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="81575-224">TriggerCondition</span></span> | <span data-ttu-id="81575-225">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-225">Yes</span></span> | <span data-ttu-id="81575-226">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span><span class="sxs-lookup"><span data-stu-id="81575-226">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="81575-227">**Total<br>Consecutive**</span><span class="sxs-lookup"><span data-stu-id="81575-227">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="81575-228">Operator</span><span class="sxs-lookup"><span data-stu-id="81575-228">Operator</span></span> | <span data-ttu-id="81575-229">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-229">Yes</span></span> | <span data-ttu-id="81575-230">Operator for the comparison from the following values:</span><span class="sxs-lookup"><span data-stu-id="81575-230">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="81575-231">**gt = greater than<br>lt = less than**</span><span class="sxs-lookup"><span data-stu-id="81575-231">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="81575-232">Value</span><span class="sxs-lookup"><span data-stu-id="81575-232">Value</span></span> | <span data-ttu-id="81575-233">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-233">Yes</span></span> | <span data-ttu-id="81575-234">Number of the times the criteria must be met to trigger the alert.</span><span class="sxs-lookup"><span data-stu-id="81575-234">Number of the times the criteria must be met to trigger the alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="81575-235">Throttling</span><span class="sxs-lookup"><span data-stu-id="81575-235">Throttling</span></span>
<span data-ttu-id="81575-236">This section is optional.</span><span class="sxs-lookup"><span data-stu-id="81575-236">This section is optional.</span></span>  <span data-ttu-id="81575-237">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span><span class="sxs-lookup"><span data-stu-id="81575-237">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="81575-238">Element name</span><span class="sxs-lookup"><span data-stu-id="81575-238">Element name</span></span> | <span data-ttu-id="81575-239">Required</span><span class="sxs-lookup"><span data-stu-id="81575-239">Required</span></span> | <span data-ttu-id="81575-240">Description</span><span class="sxs-lookup"><span data-stu-id="81575-240">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="81575-241">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="81575-241">DurationInMinutes</span></span> | <span data-ttu-id="81575-242">Yes if Throttling element included</span><span class="sxs-lookup"><span data-stu-id="81575-242">Yes if Throttling element included</span></span> | <span data-ttu-id="81575-243">Number of minutes to suppress alerts after one from the same alert rule is created.</span><span class="sxs-lookup"><span data-stu-id="81575-243">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="81575-244">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="81575-244">EmailNotification</span></span>
 <span data-ttu-id="81575-245">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span><span class="sxs-lookup"><span data-stu-id="81575-245">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="81575-246">Element name</span><span class="sxs-lookup"><span data-stu-id="81575-246">Element name</span></span> | <span data-ttu-id="81575-247">Required</span><span class="sxs-lookup"><span data-stu-id="81575-247">Required</span></span> | <span data-ttu-id="81575-248">Description</span><span class="sxs-lookup"><span data-stu-id="81575-248">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="81575-249">Recipients</span><span class="sxs-lookup"><span data-stu-id="81575-249">Recipients</span></span> | <span data-ttu-id="81575-250">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-250">Yes</span></span> | <span data-ttu-id="81575-251">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span><span class="sxs-lookup"><span data-stu-id="81575-251">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="81575-252">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="81575-252">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="81575-253">Subject</span><span class="sxs-lookup"><span data-stu-id="81575-253">Subject</span></span> | <span data-ttu-id="81575-254">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-254">Yes</span></span> | <span data-ttu-id="81575-255">Subject line of the mail.</span><span class="sxs-lookup"><span data-stu-id="81575-255">Subject line of the mail.</span></span> |
| <span data-ttu-id="81575-256">Attachment</span><span class="sxs-lookup"><span data-stu-id="81575-256">Attachment</span></span> | <span data-ttu-id="81575-257">No</span><span class="sxs-lookup"><span data-stu-id="81575-257">No</span></span> | <span data-ttu-id="81575-258">Attachments are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="81575-258">Attachments are not currently supported.</span></span>  <span data-ttu-id="81575-259">If this element is included, it should be **None**.</span><span class="sxs-lookup"><span data-stu-id="81575-259">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="81575-260">Remediation</span><span class="sxs-lookup"><span data-stu-id="81575-260">Remediation</span></span>
<span data-ttu-id="81575-261">This section is optional  Include it if you want a runbook to start in response to the alert.</span><span class="sxs-lookup"><span data-stu-id="81575-261">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="81575-262">Element name</span><span class="sxs-lookup"><span data-stu-id="81575-262">Element name</span></span> | <span data-ttu-id="81575-263">Required</span><span class="sxs-lookup"><span data-stu-id="81575-263">Required</span></span> | <span data-ttu-id="81575-264">Description</span><span class="sxs-lookup"><span data-stu-id="81575-264">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="81575-265">RunbookName</span><span class="sxs-lookup"><span data-stu-id="81575-265">RunbookName</span></span> | <span data-ttu-id="81575-266">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-266">Yes</span></span> | <span data-ttu-id="81575-267">Name of the runbook to start.</span><span class="sxs-lookup"><span data-stu-id="81575-267">Name of the runbook to start.</span></span> |
| <span data-ttu-id="81575-268">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="81575-268">WebhookUri</span></span> | <span data-ttu-id="81575-269">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-269">Yes</span></span> | <span data-ttu-id="81575-270">Uri of the webhook for the runbook.</span><span class="sxs-lookup"><span data-stu-id="81575-270">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="81575-271">Expiry</span><span class="sxs-lookup"><span data-stu-id="81575-271">Expiry</span></span> | <span data-ttu-id="81575-272">No</span><span class="sxs-lookup"><span data-stu-id="81575-272">No</span></span> | <span data-ttu-id="81575-273">Date and time that the remediation expires.</span><span class="sxs-lookup"><span data-stu-id="81575-273">Date and time that the remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="81575-274">Webhook actions</span><span class="sxs-lookup"><span data-stu-id="81575-274">Webhook actions</span></span>

<span data-ttu-id="81575-275">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span><span class="sxs-lookup"><span data-stu-id="81575-275">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="81575-276">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span><span class="sxs-lookup"><span data-stu-id="81575-276">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="81575-277">They also provide the additional option of providing a payload to be delivered to the remote process.</span><span class="sxs-lookup"><span data-stu-id="81575-277">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="81575-278">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span><span class="sxs-lookup"><span data-stu-id="81575-278">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

    {
        "name": "<name-of-the-action>",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "<api-version-of-resource>",
        "dependsOn": [
            <name-of-schedule>
            <name-of-alert-action>
        ],
        "properties": {
            "etag": "*",
            "type": "Webhook",
            "name": "<display-name-of-action>",
            "severity": "<severity-of-alert>",
            "customPayload": "<payload-to-send>"
        }
    }

<span data-ttu-id="81575-279">The properties for Webhook action resources are described in the following tables.</span><span class="sxs-lookup"><span data-stu-id="81575-279">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="81575-280">Element name</span><span class="sxs-lookup"><span data-stu-id="81575-280">Element name</span></span> | <span data-ttu-id="81575-281">Required</span><span class="sxs-lookup"><span data-stu-id="81575-281">Required</span></span> | <span data-ttu-id="81575-282">Description</span><span class="sxs-lookup"><span data-stu-id="81575-282">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="81575-283">type</span><span class="sxs-lookup"><span data-stu-id="81575-283">type</span></span> | <span data-ttu-id="81575-284">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-284">Yes</span></span> | <span data-ttu-id="81575-285">Type of the action.</span><span class="sxs-lookup"><span data-stu-id="81575-285">Type of the action.</span></span>  <span data-ttu-id="81575-286">This will be **Webhook** for webhook actions.</span><span class="sxs-lookup"><span data-stu-id="81575-286">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="81575-287">name</span><span class="sxs-lookup"><span data-stu-id="81575-287">name</span></span> | <span data-ttu-id="81575-288">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-288">Yes</span></span> | <span data-ttu-id="81575-289">Display name for the action.</span><span class="sxs-lookup"><span data-stu-id="81575-289">Display name for the action.</span></span>  <span data-ttu-id="81575-290">This is not displayed in the console.</span><span class="sxs-lookup"><span data-stu-id="81575-290">This is not displayed in the console.</span></span> |
| <span data-ttu-id="81575-291">wehookUri</span><span class="sxs-lookup"><span data-stu-id="81575-291">wehookUri</span></span> | <span data-ttu-id="81575-292">Yes</span><span class="sxs-lookup"><span data-stu-id="81575-292">Yes</span></span> | <span data-ttu-id="81575-293">Uri for the webhook.</span><span class="sxs-lookup"><span data-stu-id="81575-293">Uri for the webhook.</span></span> |
| <span data-ttu-id="81575-294">customPayload</span><span class="sxs-lookup"><span data-stu-id="81575-294">customPayload</span></span> | <span data-ttu-id="81575-295">No</span><span class="sxs-lookup"><span data-stu-id="81575-295">No</span></span> | <span data-ttu-id="81575-296">Custom payload to be sent to the webhook.</span><span class="sxs-lookup"><span data-stu-id="81575-296">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="81575-297">The format will depend on what the webhook is expecting.</span><span class="sxs-lookup"><span data-stu-id="81575-297">The format will depend on what the webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="81575-298">Sample</span><span class="sxs-lookup"><span data-stu-id="81575-298">Sample</span></span>

<span data-ttu-id="81575-299">Following is a sample of a solution that include that includes the following resources:</span><span class="sxs-lookup"><span data-stu-id="81575-299">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="81575-300">Saved search</span><span class="sxs-lookup"><span data-stu-id="81575-300">Saved search</span></span>
- <span data-ttu-id="81575-301">Schedule</span><span class="sxs-lookup"><span data-stu-id="81575-301">Schedule</span></span>
- <span data-ttu-id="81575-302">Alert action</span><span class="sxs-lookup"><span data-stu-id="81575-302">Alert action</span></span>
- <span data-ttu-id="81575-303">Webhook action</span><span class="sxs-lookup"><span data-stu-id="81575-303">Webhook action</span></span>

<span data-ttu-id="81575-304">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span><span class="sxs-lookup"><span data-stu-id="81575-304">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

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
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for the email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
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
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
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
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
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
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
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
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
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
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
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
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="81575-305">The following parameter file provides samples values for this solution.</span><span class="sxs-lookup"><span data-stu-id="81575-305">The following parameter file provides samples values for this solution.</span></span>

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
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="81575-306">Next steps</span><span class="sxs-lookup"><span data-stu-id="81575-306">Next steps</span></span>
* <span data-ttu-id="81575-307">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span><span class="sxs-lookup"><span data-stu-id="81575-307">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="81575-308">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span><span class="sxs-lookup"><span data-stu-id="81575-308">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>

