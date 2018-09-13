---
title: Using OMS Log Analytics Alert REST API
description: The Log Analytics Alert REST API allows you to create and manage alerts in Log Analytics which is part of Operations Management Suite (OMS).  This article provides details of the API and several examples for performing different operations.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 9097ca13bf4f65db4b0924044a9c0f075e3703af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826917"
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="1f114-104">Create and manage alert rules in Log Analytics with REST API</span><span class="sxs-lookup"><span data-stu-id="1f114-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="1f114-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="1f114-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="1f114-106">This article provides details of the API and several examples for performing different operations.</span><span class="sxs-lookup"><span data-stu-id="1f114-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="1f114-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span><span class="sxs-lookup"><span data-stu-id="1f114-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="1f114-108">In this document, you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open-source command-line tool that simplifies invoking the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="1f114-108">In this document, you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open-source command-line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="1f114-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span><span class="sxs-lookup"><span data-stu-id="1f114-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="1f114-110">With these tools, you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span><span class="sxs-lookup"><span data-stu-id="1f114-110">With these tools, you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="1f114-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span><span class="sxs-lookup"><span data-stu-id="1f114-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f114-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1f114-112">Prerequisites</span></span>
<span data-ttu-id="1f114-113">Currently, alerts can only be created with a saved search in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1f114-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="1f114-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="1f114-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="1f114-115">Schedules</span><span class="sxs-lookup"><span data-stu-id="1f114-115">Schedules</span></span>
<span data-ttu-id="1f114-116">A saved search can have one or more schedules.</span><span class="sxs-lookup"><span data-stu-id="1f114-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="1f114-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span><span class="sxs-lookup"><span data-stu-id="1f114-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="1f114-118">Schedules have the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="1f114-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="1f114-119">Property</span><span class="sxs-lookup"><span data-stu-id="1f114-119">Property</span></span> | <span data-ttu-id="1f114-120">Description</span><span class="sxs-lookup"><span data-stu-id="1f114-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1f114-121">Interval</span><span class="sxs-lookup"><span data-stu-id="1f114-121">Interval</span></span> |<span data-ttu-id="1f114-122">How often the search is run.</span><span class="sxs-lookup"><span data-stu-id="1f114-122">How often the search is run.</span></span> <span data-ttu-id="1f114-123">Measured in minutes.</span><span class="sxs-lookup"><span data-stu-id="1f114-123">Measured in minutes.</span></span> |
| <span data-ttu-id="1f114-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="1f114-124">QueryTimeSpan</span></span> |<span data-ttu-id="1f114-125">The time interval over which the criteria is evaluated.</span><span class="sxs-lookup"><span data-stu-id="1f114-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="1f114-126">Must be equal to or greater than Interval.</span><span class="sxs-lookup"><span data-stu-id="1f114-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="1f114-127">Measured in minutes.</span><span class="sxs-lookup"><span data-stu-id="1f114-127">Measured in minutes.</span></span> |
| <span data-ttu-id="1f114-128">Version</span><span class="sxs-lookup"><span data-stu-id="1f114-128">Version</span></span> |<span data-ttu-id="1f114-129">The API version being used.</span><span class="sxs-lookup"><span data-stu-id="1f114-129">The API version being used.</span></span>  <span data-ttu-id="1f114-130">Currently, this should always be set to 1.</span><span class="sxs-lookup"><span data-stu-id="1f114-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="1f114-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="1f114-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="1f114-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30-minute span.</span><span class="sxs-lookup"><span data-stu-id="1f114-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30-minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="1f114-133">Retrieving schedules</span><span class="sxs-lookup"><span data-stu-id="1f114-133">Retrieving schedules</span></span>
<span data-ttu-id="1f114-134">Use the Get method to retrieve all schedules for a saved search.</span><span class="sxs-lookup"><span data-stu-id="1f114-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="1f114-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span><span class="sxs-lookup"><span data-stu-id="1f114-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="1f114-136">Following is a sample response for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="1f114-137">Creating a schedule</span><span class="sxs-lookup"><span data-stu-id="1f114-137">Creating a schedule</span></span>
<span data-ttu-id="1f114-138">Use the Put method with a unique schedule ID to create a new schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="1f114-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span><span class="sxs-lookup"><span data-stu-id="1f114-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="1f114-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span><span class="sxs-lookup"><span data-stu-id="1f114-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="1f114-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span><span class="sxs-lookup"><span data-stu-id="1f114-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="1f114-142">Editing a schedule</span><span class="sxs-lookup"><span data-stu-id="1f114-142">Editing a schedule</span></span>
<span data-ttu-id="1f114-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="1f114-144">The body of the request must include the etag of the schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-144">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="1f114-145">Deleting schedules</span><span class="sxs-lookup"><span data-stu-id="1f114-145">Deleting schedules</span></span>
<span data-ttu-id="1f114-146">Use the Delete method with a schedule ID to delete a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-146">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="1f114-147">Actions</span><span class="sxs-lookup"><span data-stu-id="1f114-147">Actions</span></span>
<span data-ttu-id="1f114-148">A schedule can have multiple actions.</span><span class="sxs-lookup"><span data-stu-id="1f114-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="1f114-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span><span class="sxs-lookup"><span data-stu-id="1f114-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="1f114-150">Some actions will define both so that the processes are performed when the threshold is met.</span><span class="sxs-lookup"><span data-stu-id="1f114-150">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="1f114-151">All actions have the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="1f114-151">All actions have the properties in the following table.</span></span>  <span data-ttu-id="1f114-152">Different types of alerts have different additional properties, which are described below.</span><span class="sxs-lookup"><span data-stu-id="1f114-152">Different types of alerts have different additional properties, which are described below.</span></span>

| <span data-ttu-id="1f114-153">Property</span><span class="sxs-lookup"><span data-stu-id="1f114-153">Property</span></span> | <span data-ttu-id="1f114-154">Description</span><span class="sxs-lookup"><span data-stu-id="1f114-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1f114-155">Type</span><span class="sxs-lookup"><span data-stu-id="1f114-155">Type</span></span> |<span data-ttu-id="1f114-156">Type of the action.</span><span class="sxs-lookup"><span data-stu-id="1f114-156">Type of the action.</span></span>  <span data-ttu-id="1f114-157">Currently the possible values are Alert and Webhook.</span><span class="sxs-lookup"><span data-stu-id="1f114-157">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="1f114-158">Name</span><span class="sxs-lookup"><span data-stu-id="1f114-158">Name</span></span> |<span data-ttu-id="1f114-159">Display name for the alert.</span><span class="sxs-lookup"><span data-stu-id="1f114-159">Display name for the alert.</span></span> |
| <span data-ttu-id="1f114-160">Version</span><span class="sxs-lookup"><span data-stu-id="1f114-160">Version</span></span> |<span data-ttu-id="1f114-161">The API version being used.</span><span class="sxs-lookup"><span data-stu-id="1f114-161">The API version being used.</span></span>  <span data-ttu-id="1f114-162">Currently, this should always be set to 1.</span><span class="sxs-lookup"><span data-stu-id="1f114-162">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="1f114-163">Retrieving actions</span><span class="sxs-lookup"><span data-stu-id="1f114-163">Retrieving actions</span></span>

> [!NOTE]
> <span data-ttu-id="1f114-164">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-164">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span></span> <span data-ttu-id="1f114-165">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="1f114-165">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="1f114-166">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="1f114-166">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span></span> <span data-ttu-id="1f114-167">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span><span class="sxs-lookup"><span data-stu-id="1f114-167">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span></span> <span data-ttu-id="1f114-168">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span><span class="sxs-lookup"><span data-stu-id="1f114-168">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span></span>

<span data-ttu-id="1f114-169">Use the Get method to retrieve all actions for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-169">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="1f114-170">Use the Get method with the action ID to retrieve a particular action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-170">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="1f114-171">Creating or editing actions</span><span class="sxs-lookup"><span data-stu-id="1f114-171">Creating or editing actions</span></span>
<span data-ttu-id="1f114-172">Use the Put method with an action ID that is unique to the schedule to create a new action.</span><span class="sxs-lookup"><span data-stu-id="1f114-172">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="1f114-173">When you create an action in the OMS console, a GUID is for the action ID.</span><span class="sxs-lookup"><span data-stu-id="1f114-173">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="1f114-174">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span><span class="sxs-lookup"><span data-stu-id="1f114-174">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="1f114-175">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-175">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="1f114-176">The body of the request must include the etag of the schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-176">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="1f114-177">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span><span class="sxs-lookup"><span data-stu-id="1f114-177">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="1f114-178">Deleting actions</span><span class="sxs-lookup"><span data-stu-id="1f114-178">Deleting actions</span></span>

> [!NOTE]
> <span data-ttu-id="1f114-179">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-179">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span></span> <span data-ttu-id="1f114-180">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="1f114-180">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="1f114-181">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="1f114-181">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span></span> <span data-ttu-id="1f114-182">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span><span class="sxs-lookup"><span data-stu-id="1f114-182">For users that extend alerts to Azure, actions are now controlled in Azure action groups.</span></span> <span data-ttu-id="1f114-183">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span><span class="sxs-lookup"><span data-stu-id="1f114-183">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span></span>

<span data-ttu-id="1f114-184">Use the Delete method with the action ID to delete an action.</span><span class="sxs-lookup"><span data-stu-id="1f114-184">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="1f114-185">Alert Actions</span><span class="sxs-lookup"><span data-stu-id="1f114-185">Alert Actions</span></span>
<span data-ttu-id="1f114-186">A Schedule should have one and only one Alert action.</span><span class="sxs-lookup"><span data-stu-id="1f114-186">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="1f114-187">Alert actions have one or more of the sections in the following table.</span><span class="sxs-lookup"><span data-stu-id="1f114-187">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="1f114-188">Each is described in further detail below.</span><span class="sxs-lookup"><span data-stu-id="1f114-188">Each is described in further detail below.</span></span>

| <span data-ttu-id="1f114-189">Section</span><span class="sxs-lookup"><span data-stu-id="1f114-189">Section</span></span> | <span data-ttu-id="1f114-190">Description</span><span class="sxs-lookup"><span data-stu-id="1f114-190">Description</span></span> | <span data-ttu-id="1f114-191">Usage</span><span class="sxs-lookup"><span data-stu-id="1f114-191">Usage</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1f114-192">Threshold</span><span class="sxs-lookup"><span data-stu-id="1f114-192">Threshold</span></span> |<span data-ttu-id="1f114-193">Criteria for when the action is run.</span><span class="sxs-lookup"><span data-stu-id="1f114-193">Criteria for when the action is run.</span></span>| <span data-ttu-id="1f114-194">Required for every alert, before or after they are extended to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-194">Required for every alert, before or after they are extended to Azure.</span></span> |
| <span data-ttu-id="1f114-195">Severity</span><span class="sxs-lookup"><span data-stu-id="1f114-195">Severity</span></span> |<span data-ttu-id="1f114-196">Label used to classify alert when triggered.</span><span class="sxs-lookup"><span data-stu-id="1f114-196">Label used to classify alert when triggered.</span></span>| <span data-ttu-id="1f114-197">Required for every alert, before or after they are extended to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-197">Required for every alert, before or after they are extended to Azure.</span></span> |
| <span data-ttu-id="1f114-198">Action Groups</span><span class="sxs-lookup"><span data-stu-id="1f114-198">Action Groups</span></span> |<span data-ttu-id="1f114-199">IDs of Azure ActionGroup where actions required are specified, like - E-Mails, SMSs, Voice Calls, Webhooks, Automation Runbooks, ITSM Connectors, etc.</span><span class="sxs-lookup"><span data-stu-id="1f114-199">IDs of Azure ActionGroup where actions required are specified, like - E-Mails, SMSs, Voice Calls, Webhooks, Automation Runbooks, ITSM Connectors, etc.</span></span>| <span data-ttu-id="1f114-200">Required once alerts are extended to Azure</span><span class="sxs-lookup"><span data-stu-id="1f114-200">Required once alerts are extended to Azure</span></span>|
| <span data-ttu-id="1f114-201">Customize Actions</span><span class="sxs-lookup"><span data-stu-id="1f114-201">Customize Actions</span></span>|<span data-ttu-id="1f114-202">Modify the standard output for select actions from ActionGroup</span><span class="sxs-lookup"><span data-stu-id="1f114-202">Modify the standard output for select actions from ActionGroup</span></span>| <span data-ttu-id="1f114-203">Optional for every alert, can be used after alerts are extended to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-203">Optional for every alert, can be used after alerts are extended to Azure.</span></span> |
| <span data-ttu-id="1f114-204">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="1f114-204">EmailNotification</span></span> |<span data-ttu-id="1f114-205">Send mail to multiple recipients.</span><span class="sxs-lookup"><span data-stu-id="1f114-205">Send mail to multiple recipients.</span></span> | <span data-ttu-id="1f114-206">Not required, if alerts are extended to Azure</span><span class="sxs-lookup"><span data-stu-id="1f114-206">Not required, if alerts are extended to Azure</span></span>|
| <span data-ttu-id="1f114-207">Remediation</span><span class="sxs-lookup"><span data-stu-id="1f114-207">Remediation</span></span> |<span data-ttu-id="1f114-208">Start a runbook in Azure Automation to attempt to correct identified issue.</span><span class="sxs-lookup"><span data-stu-id="1f114-208">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |<span data-ttu-id="1f114-209">Not required, if alerts are extended to Azure</span><span class="sxs-lookup"><span data-stu-id="1f114-209">Not required, if alerts are extended to Azure</span></span>|
| <span data-ttu-id="1f114-210">Webhook Actions</span><span class="sxs-lookup"><span data-stu-id="1f114-210">Webhook Actions</span></span> | <span data-ttu-id="1f114-211">Push data from Alerts, to desired service as JSON</span><span class="sxs-lookup"><span data-stu-id="1f114-211">Push data from Alerts, to desired service as JSON</span></span> |<span data-ttu-id="1f114-212">Not required, if alerts are extended to Azure</span><span class="sxs-lookup"><span data-stu-id="1f114-212">Not required, if alerts are extended to Azure</span></span>|

> [!NOTE]
> <span data-ttu-id="1f114-213">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-213">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span></span> <span data-ttu-id="1f114-214">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="1f114-214">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="1f114-215">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="1f114-215">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span></span>

#### <a name="thresholds"></a><span data-ttu-id="1f114-216">Thresholds</span><span class="sxs-lookup"><span data-stu-id="1f114-216">Thresholds</span></span>
<span data-ttu-id="1f114-217">An Alert action should have one and only one threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-217">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="1f114-218">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span><span class="sxs-lookup"><span data-stu-id="1f114-218">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="1f114-219">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span><span class="sxs-lookup"><span data-stu-id="1f114-219">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="1f114-220">Thresholds have the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="1f114-220">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="1f114-221">Property</span><span class="sxs-lookup"><span data-stu-id="1f114-221">Property</span></span> | <span data-ttu-id="1f114-222">Description</span><span class="sxs-lookup"><span data-stu-id="1f114-222">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1f114-223">Operator</span><span class="sxs-lookup"><span data-stu-id="1f114-223">Operator</span></span> |<span data-ttu-id="1f114-224">Operator for the threshold comparison.</span><span class="sxs-lookup"><span data-stu-id="1f114-224">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="1f114-225">gt = Greater Than</span><span class="sxs-lookup"><span data-stu-id="1f114-225">gt = Greater Than</span></span> <br> <span data-ttu-id="1f114-226">lt = Less Than</span><span class="sxs-lookup"><span data-stu-id="1f114-226">lt = Less Than</span></span> |
| <span data-ttu-id="1f114-227">Value</span><span class="sxs-lookup"><span data-stu-id="1f114-227">Value</span></span> |<span data-ttu-id="1f114-228">Value for the threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-228">Value for the threshold.</span></span> |

<span data-ttu-id="1f114-229">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span><span class="sxs-lookup"><span data-stu-id="1f114-229">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="1f114-230">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30-minute span.</span><span class="sxs-lookup"><span data-stu-id="1f114-230">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30-minute span.</span></span>

<span data-ttu-id="1f114-231">Following is a sample response for an action with only a threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-231">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="1f114-232">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-232">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="1f114-233">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-233">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="1f114-234">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="1f114-234">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="severity"></a><span data-ttu-id="1f114-235">Severity</span><span class="sxs-lookup"><span data-stu-id="1f114-235">Severity</span></span>
<span data-ttu-id="1f114-236">Log Analytics allows you to classify your alerts into categories, to allow easier management and triage.</span><span class="sxs-lookup"><span data-stu-id="1f114-236">Log Analytics allows you to classify your alerts into categories, to allow easier management and triage.</span></span> <span data-ttu-id="1f114-237">The Alert severity defined is: informational, warning, and critical.</span><span class="sxs-lookup"><span data-stu-id="1f114-237">The Alert severity defined is: informational, warning, and critical.</span></span> <span data-ttu-id="1f114-238">These are mapped to the normalized severity scale of Azure Alerts as:</span><span class="sxs-lookup"><span data-stu-id="1f114-238">These are mapped to the normalized severity scale of Azure Alerts as:</span></span>

|<span data-ttu-id="1f114-239">Log Analytics Severity Level</span><span class="sxs-lookup"><span data-stu-id="1f114-239">Log Analytics Severity Level</span></span>  |<span data-ttu-id="1f114-240">Azure Alerts Severity Level</span><span class="sxs-lookup"><span data-stu-id="1f114-240">Azure Alerts Severity Level</span></span>  |
|---------|---------|
|<span data-ttu-id="1f114-241">critical</span><span class="sxs-lookup"><span data-stu-id="1f114-241">critical</span></span> |<span data-ttu-id="1f114-242">Sev 0</span><span class="sxs-lookup"><span data-stu-id="1f114-242">Sev 0</span></span>|
|<span data-ttu-id="1f114-243">warning</span><span class="sxs-lookup"><span data-stu-id="1f114-243">warning</span></span> |<span data-ttu-id="1f114-244">Sev 1</span><span class="sxs-lookup"><span data-stu-id="1f114-244">Sev 1</span></span>|
|<span data-ttu-id="1f114-245">informational</span><span class="sxs-lookup"><span data-stu-id="1f114-245">informational</span></span> | <span data-ttu-id="1f114-246">Sev 2</span><span class="sxs-lookup"><span data-stu-id="1f114-246">Sev 2</span></span>|

<span data-ttu-id="1f114-247">Following is a sample response for an action with only a threshold and severity.</span><span class="sxs-lookup"><span data-stu-id="1f114-247">Following is a sample response for an action with only a threshold and severity.</span></span> 

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Severity": "critical",
        "Version": 1    }

<span data-ttu-id="1f114-248">Use the Put method with a unique action ID to create a new action for a schedule with severity.</span><span class="sxs-lookup"><span data-stu-id="1f114-248">Use the Put method with a unique action ID to create a new action for a schedule with severity.</span></span>  

    $thresholdWithSevJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1','Severity': 'critical', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdWithSevJson

<span data-ttu-id="1f114-249">Use the Put method with an existing action ID to modify a severity action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-249">Use the Put method with an existing action ID to modify a severity action for a schedule.</span></span>  <span data-ttu-id="1f114-250">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="1f114-250">The body of the request must include the etag of the action.</span></span>

    $thresholdWithSevJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1','Severity': 'critical', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdWithSevJson

#### <a name="action-groups"></a><span data-ttu-id="1f114-251">Action Groups</span><span class="sxs-lookup"><span data-stu-id="1f114-251">Action Groups</span></span>
<span data-ttu-id="1f114-252">All alerts in Azure, use Action Group as the default mechanism for handling actions.</span><span class="sxs-lookup"><span data-stu-id="1f114-252">All alerts in Azure, use Action Group as the default mechanism for handling actions.</span></span> <span data-ttu-id="1f114-253">With Action Group, you can specify your actions once and then associate the action group to multiple alerts - across Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-253">With Action Group, you can specify your actions once and then associate the action group to multiple alerts - across Azure.</span></span> <span data-ttu-id="1f114-254">Without the need, to repeatedly declare the same actions over and over again.</span><span class="sxs-lookup"><span data-stu-id="1f114-254">Without the need, to repeatedly declare the same actions over and over again.</span></span> <span data-ttu-id="1f114-255">Action Groups support multiple actions - including email, SMS, Voice Call, ITSM Connection, Automation Runbook, Webhook URI and more.</span><span class="sxs-lookup"><span data-stu-id="1f114-255">Action Groups support multiple actions - including email, SMS, Voice Call, ITSM Connection, Automation Runbook, Webhook URI and more.</span></span> 

<span data-ttu-id="1f114-256">For user's who have extended their alerts into Azure - a schedule should now have Action Group details passed along with threshold, to be able to create an alert.</span><span class="sxs-lookup"><span data-stu-id="1f114-256">For user's who have extended their alerts into Azure - a schedule should now have Action Group details passed along with threshold, to be able to create an alert.</span></span> <span data-ttu-id="1f114-257">E-mail details, Webhook URLs, Runbook Automation details, and other Actions, need to be defined in side an Action Group first before creating an alert; one can create [Action Group from Azure Monitor](../monitoring-and-diagnostics/monitoring-action-groups.md) in Portal or use [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span><span class="sxs-lookup"><span data-stu-id="1f114-257">E-mail details, Webhook URLs, Runbook Automation details, and other Actions, need to be defined in side an Action Group first before creating an alert; one can create [Action Group from Azure Monitor](../monitoring-and-diagnostics/monitoring-action-groups.md) in Portal or use [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span></span>

<span data-ttu-id="1f114-258">To add association of action group to an alert, specify the unique Azure Resource Manager ID of the action group in the alert definition.</span><span class="sxs-lookup"><span data-stu-id="1f114-258">To add association of action group to an alert, specify the unique Azure Resource Manager ID of the action group in the alert definition.</span></span> <span data-ttu-id="1f114-259">A sample illustration is provided below:</span><span class="sxs-lookup"><span data-stu-id="1f114-259">A sample illustration is provided below:</span></span>

     "etag": "W/\"datetime'2017-12-13T10%3A52%3A21.1697364Z'\"",
      "properties": {
        "Type": "Alert",
        "Name": "test-alert",
        "Description": "I need to put a descriptio here",
        "Threshold": {
          "Operator": "gt",
          "Value": 12
        },
        "AzNsNotification": {
          "GroupIds": [
            "/subscriptions/1234a45-123d-4321-12aa-123b12a5678/resourcegroups/my-resource-group/providers/microsoft.insights/actiongroups/test-actiongroup"
          ]
        },
        "Severity": "critical",
        "Version": 1
      },

<span data-ttu-id="1f114-260">Use the Put method with a unique action ID to associate already existing Action Group for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-260">Use the Put method with a unique action ID to associate already existing Action Group for a schedule.</span></span>  <span data-ttu-id="1f114-261">The following is a sample illustration of usage.</span><span class="sxs-lookup"><span data-stu-id="1f114-261">The following is a sample illustration of usage.</span></span>

    $AzNsJson = "{'properties': { 'Name': 'test-alert', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 12 },'Severity': 'critical', 'AzNsNotification': {'GroupIds': ['subscriptions/1234a45-123d-4321-12aa-123b12a5678/resourcegroups/my-resource-group/providers/microsoft.insights/actiongroups/test-actiongroup']} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myAzNsaction?api-version=2015-03-20 $AzNsJson

<span data-ttu-id="1f114-262">Use the Put method with an existing action ID to modify an Action Group associated for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-262">Use the Put method with an existing action ID to modify an Action Group associated for a schedule.</span></span>  <span data-ttu-id="1f114-263">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="1f114-263">The body of the request must include the etag of the action.</span></span>

    $AzNsJson = "{'etag': 'datetime'2017-12-13T10%3A52%3A21.1697364Z'\"', properties': { 'Name': 'test-alert', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 12 },'Severity': 'critical', 'AzNsNotification': {'GroupIds': ['subscriptions/1234a45-123d-4321-12aa-123b12a5678/resourcegroups/my-resource-group/providers/microsoft.insights/actiongroups/test-actiongroup']} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myAzNsaction?api-version=2015-03-20 $AzNsJson

#### <a name="customize-actions"></a><span data-ttu-id="1f114-264">Customize Actions</span><span class="sxs-lookup"><span data-stu-id="1f114-264">Customize Actions</span></span>
<span data-ttu-id="1f114-265">By default actions, follow standard template and format for notifications.</span><span class="sxs-lookup"><span data-stu-id="1f114-265">By default actions, follow standard template and format for notifications.</span></span> <span data-ttu-id="1f114-266">But user can customize some actions, even if they are controlled by Action Groups.</span><span class="sxs-lookup"><span data-stu-id="1f114-266">But user can customize some actions, even if they are controlled by Action Groups.</span></span> <span data-ttu-id="1f114-267">Currently, customization is possible for Email Subject and Webhook Payload.</span><span class="sxs-lookup"><span data-stu-id="1f114-267">Currently, customization is possible for Email Subject and Webhook Payload.</span></span>

##### <a name="customize-e-mail-subject-for-action-group"></a><span data-ttu-id="1f114-268">Customize E-Mail Subject for Action Group</span><span class="sxs-lookup"><span data-stu-id="1f114-268">Customize E-Mail Subject for Action Group</span></span>
<span data-ttu-id="1f114-269">By default, the email subject for alerts is: Alert Notification <AlertName> for <WorkspaceName>.</span><span class="sxs-lookup"><span data-stu-id="1f114-269">By default, the email subject for alerts is: Alert Notification <AlertName> for <WorkspaceName>.</span></span> <span data-ttu-id="1f114-270">But this can be customized, so that you can specific words or tags - to allow you to easily employ filter rules in your Inbox.</span><span class="sxs-lookup"><span data-stu-id="1f114-270">But this can be customized, so that you can specific words or tags - to allow you to easily employ filter rules in your Inbox.</span></span> <span data-ttu-id="1f114-271">The customize email header details need to send along with ActionGroup details, as in sample below.</span><span class="sxs-lookup"><span data-stu-id="1f114-271">The customize email header details need to send along with ActionGroup details, as in sample below.</span></span>

     "etag": "W/\"datetime'2017-12-13T10%3A52%3A21.1697364Z'\"",
      "properties": {
        "Type": "Alert",
        "Name": "test-alert",
        "Description": "I need to put a descriptio here",
        "Threshold": {
          "Operator": "gt",
          "Value": 12
        },
        "AzNsNotification": {
          "GroupIds": [
            "/subscriptions/1234a45-123d-4321-12aa-123b12a5678/resourcegroups/my-resource-group/providers/microsoft.insights/actiongroups/test-actiongroup"
          ]
          "CustomEmailSubject": "Azure Alert fired"
        },
        "Severity": "critical",
        "Version": 1
      },

<span data-ttu-id="1f114-272">Use the Put method with a unique action ID to associate already existing Action Group with customization for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-272">Use the Put method with a unique action ID to associate already existing Action Group with customization for a schedule.</span></span>  <span data-ttu-id="1f114-273">The following is a sample illustration of usage.</span><span class="sxs-lookup"><span data-stu-id="1f114-273">The following is a sample illustration of usage.</span></span>

    $AzNsJson = "{'properties': { 'Name': 'test-alert', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 12 },'Severity': 'critical', 'AzNsNotification': {'GroupIds': ['subscriptions/1234a45-123d-4321-12aa-123b12a5678/resourcegroups/my-resource-group/providers/microsoft.insights/actiongroups/test-actiongroup'], 'CustomEmailSubject': 'Azure Alert fired'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myAzNsaction?api-version=2015-03-20 $AzNsJson

<span data-ttu-id="1f114-274">Use the Put method with an existing action ID to modify an Action Group associated for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-274">Use the Put method with an existing action ID to modify an Action Group associated for a schedule.</span></span>  <span data-ttu-id="1f114-275">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="1f114-275">The body of the request must include the etag of the action.</span></span>

    $AzNsJson = "{'etag': 'datetime'2017-12-13T10%3A52%3A21.1697364Z'\"', properties': { 'Name': 'test-alert', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 12 },'Severity': 'critical', 'AzNsNotification': {'GroupIds': ['subscriptions/1234a45-123d-4321-12aa-123b12a5678/resourcegroups/my-resource-group/providers/microsoft.insights/actiongroups/test-actiongroup']}, 'CustomEmailSubject': 'Azure Alert fired' }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myAzNsaction?api-version=2015-03-20 $AzNsJson

##### <a name="customize-webhook-payload-for-action-group"></a><span data-ttu-id="1f114-276">Customize Webhook Payload for Action Group</span><span class="sxs-lookup"><span data-stu-id="1f114-276">Customize Webhook Payload for Action Group</span></span>
<span data-ttu-id="1f114-277">By default, the webhook sent via Action Group for log analytics has a fixed structure.</span><span class="sxs-lookup"><span data-stu-id="1f114-277">By default, the webhook sent via Action Group for log analytics has a fixed structure.</span></span> <span data-ttu-id="1f114-278">But one can customize the JSON payload by using specific variables supported, to meet requirements of the webhook endpoint.</span><span class="sxs-lookup"><span data-stu-id="1f114-278">But one can customize the JSON payload by using specific variables supported, to meet requirements of the webhook endpoint.</span></span> <span data-ttu-id="1f114-279">For more information, see [Webhook action for log alert rules](../monitoring-and-diagnostics/monitor-alerts-unified-log-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="1f114-279">For more information, see [Webhook action for log alert rules](../monitoring-and-diagnostics/monitor-alerts-unified-log-webhook.md).</span></span> 

<span data-ttu-id="1f114-280">The customize webhook details need to send along with ActionGroup details and will be applied to all Webhook URI specified inside the action group; as in sample below.</span><span class="sxs-lookup"><span data-stu-id="1f114-280">The customize webhook details need to send along with ActionGroup details and will be applied to all Webhook URI specified inside the action group; as in sample below.</span></span>

     "etag": "W/\"datetime'2017-12-13T10%3A52%3A21.1697364Z'\"",
      "properties": {
        "Type": "Alert",
        "Name": "test-alert",
        "Description": "I need to put a descriptio here",
        "Threshold": {
          "Operator": "gt",
          "Value": 12
        },
        "AzNsNotification": {
          "GroupIds": [
            "/subscriptions/1234a45-123d-4321-12aa-123b12a5678/resourcegroups/my-resource-group/providers/microsoft.insights/actiongroups/test-actiongroup"
          ]
          "CustomWebhookPayload": "{\"field1\":\"value1\",\"field2\":\"value2\"}",
          "CustomEmailSubject": "Azure Alert fired"
        },
        "Severity": "critical",
        "Version": 1
      },

<span data-ttu-id="1f114-281">Use the Put method with a unique action ID to associate already existing Action Group with customization for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-281">Use the Put method with a unique action ID to associate already existing Action Group with customization for a schedule.</span></span>  <span data-ttu-id="1f114-282">The following is a sample illustration of usage.</span><span class="sxs-lookup"><span data-stu-id="1f114-282">The following is a sample illustration of usage.</span></span>

    $AzNsJson = "{'properties': { 'Name': 'test-alert', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 12 },'Severity': 'critical', 'AzNsNotification': {'GroupIds': ['subscriptions/1234a45-123d-4321-12aa-123b12a5678/resourcegroups/my-resource-group/providers/microsoft.insights/actiongroups/test-actiongroup'], 'CustomEmailSubject': 'Azure Alert fired','CustomWebhookPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myAzNsaction?api-version=2015-03-20 $AzNsJson

<span data-ttu-id="1f114-283">Use the Put method with an existing action ID to modify an Action Group associated for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-283">Use the Put method with an existing action ID to modify an Action Group associated for a schedule.</span></span>  <span data-ttu-id="1f114-284">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="1f114-284">The body of the request must include the etag of the action.</span></span>

    $AzNsJson = "{'etag': 'datetime'2017-12-13T10%3A52%3A21.1697364Z'\"', properties': { 'Name': 'test-alert', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 12 },'Severity': 'critical', 'AzNsNotification': {'GroupIds': ['subscriptions/1234a45-123d-4321-12aa-123b12a5678/resourcegroups/my-resource-group/providers/microsoft.insights/actiongroups/test-actiongroup']}, 'CustomEmailSubject': 'Azure Alert fired','CustomWebhookPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}' }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myAzNsaction?api-version=2015-03-20 $AzNsJson

#### <a name="email-notification"></a><span data-ttu-id="1f114-285">Email Notification</span><span class="sxs-lookup"><span data-stu-id="1f114-285">Email Notification</span></span>
<span data-ttu-id="1f114-286">Email Notifications send mail to one or more recipients.</span><span class="sxs-lookup"><span data-stu-id="1f114-286">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="1f114-287">They include the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="1f114-287">They include the properties in the following table.</span></span>

> [!NOTE]
> <span data-ttu-id="1f114-288">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-288">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span></span> <span data-ttu-id="1f114-289">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="1f114-289">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="1f114-290">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="1f114-290">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span></span> <span data-ttu-id="1f114-291">For users that extend alerts to Azure, actions like E-Mail Notification are now controlled in Azure action groups.</span><span class="sxs-lookup"><span data-stu-id="1f114-291">For users that extend alerts to Azure, actions like E-Mail Notification are now controlled in Azure action groups.</span></span> <span data-ttu-id="1f114-292">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span><span class="sxs-lookup"><span data-stu-id="1f114-292">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span></span>
   

| <span data-ttu-id="1f114-293">Property</span><span class="sxs-lookup"><span data-stu-id="1f114-293">Property</span></span> | <span data-ttu-id="1f114-294">Description</span><span class="sxs-lookup"><span data-stu-id="1f114-294">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1f114-295">Recipients</span><span class="sxs-lookup"><span data-stu-id="1f114-295">Recipients</span></span> |<span data-ttu-id="1f114-296">List of mail addresses.</span><span class="sxs-lookup"><span data-stu-id="1f114-296">List of mail addresses.</span></span> |
| <span data-ttu-id="1f114-297">Subject</span><span class="sxs-lookup"><span data-stu-id="1f114-297">Subject</span></span> |<span data-ttu-id="1f114-298">The subject of the mail.</span><span class="sxs-lookup"><span data-stu-id="1f114-298">The subject of the mail.</span></span> |
| <span data-ttu-id="1f114-299">Attachment</span><span class="sxs-lookup"><span data-stu-id="1f114-299">Attachment</span></span> |<span data-ttu-id="1f114-300">Attachments are not currently supported, so this will always have a value of “None.”</span><span class="sxs-lookup"><span data-stu-id="1f114-300">Attachments are not currently supported, so this will always have a value of “None.”</span></span> |

<span data-ttu-id="1f114-301">Following is a sample response for an email notification action with a threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-301">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="1f114-302">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-302">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="1f114-303">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-303">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="1f114-304">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-304">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="1f114-305">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="1f114-305">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="1f114-306">Remediation actions</span><span class="sxs-lookup"><span data-stu-id="1f114-306">Remediation actions</span></span>
<span data-ttu-id="1f114-307">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span><span class="sxs-lookup"><span data-stu-id="1f114-307">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="1f114-308">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span><span class="sxs-lookup"><span data-stu-id="1f114-308">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="1f114-309">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span><span class="sxs-lookup"><span data-stu-id="1f114-309">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

> [!NOTE]
> <span data-ttu-id="1f114-310">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-310">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span></span> <span data-ttu-id="1f114-311">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="1f114-311">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="1f114-312">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="1f114-312">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span></span> <span data-ttu-id="1f114-313">For users that extend alerts to Azure, actions like Remediation using runbook are now controlled in Azure action groups.</span><span class="sxs-lookup"><span data-stu-id="1f114-313">For users that extend alerts to Azure, actions like Remediation using runbook are now controlled in Azure action groups.</span></span> <span data-ttu-id="1f114-314">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span><span class="sxs-lookup"><span data-stu-id="1f114-314">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span></span>

<span data-ttu-id="1f114-315">Remediations include the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="1f114-315">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="1f114-316">Property</span><span class="sxs-lookup"><span data-stu-id="1f114-316">Property</span></span> | <span data-ttu-id="1f114-317">Description</span><span class="sxs-lookup"><span data-stu-id="1f114-317">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1f114-318">RunbookName</span><span class="sxs-lookup"><span data-stu-id="1f114-318">RunbookName</span></span> |<span data-ttu-id="1f114-319">Name of the runbook.</span><span class="sxs-lookup"><span data-stu-id="1f114-319">Name of the runbook.</span></span> <span data-ttu-id="1f114-320">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="1f114-320">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="1f114-321">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="1f114-321">WebhookUri</span></span> |<span data-ttu-id="1f114-322">URI of the webhook.</span><span class="sxs-lookup"><span data-stu-id="1f114-322">URI of the webhook.</span></span> |
| <span data-ttu-id="1f114-323">Expiry</span><span class="sxs-lookup"><span data-stu-id="1f114-323">Expiry</span></span> |<span data-ttu-id="1f114-324">The expiration date and time of the webhook.</span><span class="sxs-lookup"><span data-stu-id="1f114-324">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="1f114-325">If the webhook doesn’t have an expiration, then this can be any valid future date.</span><span class="sxs-lookup"><span data-stu-id="1f114-325">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="1f114-326">Following is a sample response for a remediation action with a threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-326">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="1f114-327">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-327">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="1f114-328">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-328">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="1f114-329">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-329">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="1f114-330">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="1f114-330">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="1f114-331">Example</span><span class="sxs-lookup"><span data-stu-id="1f114-331">Example</span></span>
<span data-ttu-id="1f114-332">Following is a complete example to create a new email alert.</span><span class="sxs-lookup"><span data-stu-id="1f114-332">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="1f114-333">This creates a new schedule along with an action containing a threshold and email.</span><span class="sxs-lookup"><span data-stu-id="1f114-333">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

#### <a name="webhook-actions"></a><span data-ttu-id="1f114-334">Webhook actions</span><span class="sxs-lookup"><span data-stu-id="1f114-334">Webhook actions</span></span>
<span data-ttu-id="1f114-335">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span><span class="sxs-lookup"><span data-stu-id="1f114-335">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="1f114-336">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span><span class="sxs-lookup"><span data-stu-id="1f114-336">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="1f114-337">They also provide the additional option of providing a payload to be delivered to the remote process.</span><span class="sxs-lookup"><span data-stu-id="1f114-337">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

> [!NOTE]
> <span data-ttu-id="1f114-338">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f114-338">Beginning May 14, 2018, all alerts in a workspace will be automatically extended to Azure.</span></span> <span data-ttu-id="1f114-339">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="1f114-339">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="1f114-340">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="1f114-340">For more information, see [Extend Alerts into Azure from OMS](../monitoring-and-diagnostics/monitoring-alerts-extend.md).</span></span> <span data-ttu-id="1f114-341">For users that extend alerts to Azure, actions like Webhook are now controlled in Azure action groups.</span><span class="sxs-lookup"><span data-stu-id="1f114-341">For users that extend alerts to Azure, actions like Webhook are now controlled in Azure action groups.</span></span> <span data-ttu-id="1f114-342">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span><span class="sxs-lookup"><span data-stu-id="1f114-342">When a workspace and its alerts are extended to Azure, you can retrieve or add actions by using the [Action Group API](https://docs.microsoft.com/rest/api/monitor/actiongroups).</span></span>


<span data-ttu-id="1f114-343">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-343">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  

<span data-ttu-id="1f114-344">Following is a sample response for webhook action and an associated alert action with a threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-344">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

##### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="1f114-345">Create or edit a webhook action</span><span class="sxs-lookup"><span data-stu-id="1f114-345">Create or edit a webhook action</span></span>
<span data-ttu-id="1f114-346">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-346">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="1f114-347">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span><span class="sxs-lookup"><span data-stu-id="1f114-347">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="1f114-348">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="1f114-348">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="1f114-349">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="1f114-349">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction


## <a name="next-steps"></a><span data-ttu-id="1f114-350">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f114-350">Next steps</span></span>
* <span data-ttu-id="1f114-351">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1f114-351">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>
* <span data-ttu-id="1f114-352">Learn about [log alerts in azure alerts](../monitoring-and-diagnostics/monitor-alerts-unified-log.md)</span><span class="sxs-lookup"><span data-stu-id="1f114-352">Learn about [log alerts in azure alerts](../monitoring-and-diagnostics/monitor-alerts-unified-log.md)</span></span>

