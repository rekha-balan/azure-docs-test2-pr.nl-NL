---
title: Using OMS Log Analytics Alert REST API
description: The Log Analytics Alert REST API allows you to create and manage alerts in Log Analytics which is part of Operations Management Suite (OMS).  This article provides details of the API and several examples for performing different operations.
services: log-analytics
documentationcenter: ''
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6c747a2b54eb42abb76ef10ed045302a9a8546f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671755"
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="a7c14-104">Create and manage alert rules in Log Analytics with REST API</span><span class="sxs-lookup"><span data-stu-id="a7c14-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="a7c14-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="a7c14-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="a7c14-106">This article provides details of the API and several examples for performing different operations.</span><span class="sxs-lookup"><span data-stu-id="a7c14-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="a7c14-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span><span class="sxs-lookup"><span data-stu-id="a7c14-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="a7c14-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="a7c14-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="a7c14-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span><span class="sxs-lookup"><span data-stu-id="a7c14-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="a7c14-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span><span class="sxs-lookup"><span data-stu-id="a7c14-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="a7c14-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span><span class="sxs-lookup"><span data-stu-id="a7c14-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7c14-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7c14-112">Prerequisites</span></span>
<span data-ttu-id="a7c14-113">Currently, alerts can only be created with a saved search in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a7c14-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="a7c14-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="a7c14-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="a7c14-115">Schedules</span><span class="sxs-lookup"><span data-stu-id="a7c14-115">Schedules</span></span>
<span data-ttu-id="a7c14-116">A saved search can have one or more schedules.</span><span class="sxs-lookup"><span data-stu-id="a7c14-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="a7c14-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span><span class="sxs-lookup"><span data-stu-id="a7c14-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="a7c14-118">Schedules have the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="a7c14-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="a7c14-119">Property</span><span class="sxs-lookup"><span data-stu-id="a7c14-119">Property</span></span> | <span data-ttu-id="a7c14-120">Description</span><span class="sxs-lookup"><span data-stu-id="a7c14-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a7c14-121">Interval</span><span class="sxs-lookup"><span data-stu-id="a7c14-121">Interval</span></span> |<span data-ttu-id="a7c14-122">How often the search is run.</span><span class="sxs-lookup"><span data-stu-id="a7c14-122">How often the search is run.</span></span> <span data-ttu-id="a7c14-123">Measured in minutes.</span><span class="sxs-lookup"><span data-stu-id="a7c14-123">Measured in minutes.</span></span> |
| <span data-ttu-id="a7c14-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="a7c14-124">QueryTimeSpan</span></span> |<span data-ttu-id="a7c14-125">The time interval over which the criteria is evaluated.</span><span class="sxs-lookup"><span data-stu-id="a7c14-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="a7c14-126">Must be equal to or greater than Interval.</span><span class="sxs-lookup"><span data-stu-id="a7c14-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="a7c14-127">Measured in minutes.</span><span class="sxs-lookup"><span data-stu-id="a7c14-127">Measured in minutes.</span></span> |
| <span data-ttu-id="a7c14-128">Version</span><span class="sxs-lookup"><span data-stu-id="a7c14-128">Version</span></span> |<span data-ttu-id="a7c14-129">The API version being used.</span><span class="sxs-lookup"><span data-stu-id="a7c14-129">The API version being used.</span></span>  <span data-ttu-id="a7c14-130">Currently, this should always be set to 1.</span><span class="sxs-lookup"><span data-stu-id="a7c14-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="a7c14-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="a7c14-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="a7c14-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span><span class="sxs-lookup"><span data-stu-id="a7c14-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="a7c14-133">Retrieving schedules</span><span class="sxs-lookup"><span data-stu-id="a7c14-133">Retrieving schedules</span></span>
<span data-ttu-id="a7c14-134">Use the Get method to retrieve all schedules for a saved search.</span><span class="sxs-lookup"><span data-stu-id="a7c14-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="a7c14-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span><span class="sxs-lookup"><span data-stu-id="a7c14-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="a7c14-136">Following is a sample response for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="a7c14-137">Creating a schedule</span><span class="sxs-lookup"><span data-stu-id="a7c14-137">Creating a schedule</span></span>
<span data-ttu-id="a7c14-138">Use the Put method with a unique schedule ID to create a new schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="a7c14-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span><span class="sxs-lookup"><span data-stu-id="a7c14-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="a7c14-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span><span class="sxs-lookup"><span data-stu-id="a7c14-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="a7c14-141">Editing a schedule</span><span class="sxs-lookup"><span data-stu-id="a7c14-141">Editing a schedule</span></span>
<span data-ttu-id="a7c14-142">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-142">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="a7c14-143">The body of the request must include the etag of the schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-143">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="a7c14-144">Deleting schedules</span><span class="sxs-lookup"><span data-stu-id="a7c14-144">Deleting schedules</span></span>
<span data-ttu-id="a7c14-145">Use the Delete method with a schedule ID to delete a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-145">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="a7c14-146">Actions</span><span class="sxs-lookup"><span data-stu-id="a7c14-146">Actions</span></span>
<span data-ttu-id="a7c14-147">A schedule can have multiple actions.</span><span class="sxs-lookup"><span data-stu-id="a7c14-147">A schedule can have multiple actions.</span></span> <span data-ttu-id="a7c14-148">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span><span class="sxs-lookup"><span data-stu-id="a7c14-148">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="a7c14-149">Some actions will define both so that the processes are performed when the threshold is met.</span><span class="sxs-lookup"><span data-stu-id="a7c14-149">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="a7c14-150">All actions have the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="a7c14-150">All actions have the properties in the following table.</span></span>  <span data-ttu-id="a7c14-151">Different types of alerts have different additional properties which are described below.</span><span class="sxs-lookup"><span data-stu-id="a7c14-151">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="a7c14-152">Property</span><span class="sxs-lookup"><span data-stu-id="a7c14-152">Property</span></span> | <span data-ttu-id="a7c14-153">Description</span><span class="sxs-lookup"><span data-stu-id="a7c14-153">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a7c14-154">Type</span><span class="sxs-lookup"><span data-stu-id="a7c14-154">Type</span></span> |<span data-ttu-id="a7c14-155">Type of the action.</span><span class="sxs-lookup"><span data-stu-id="a7c14-155">Type of the action.</span></span>  <span data-ttu-id="a7c14-156">Currently the possible values are Alert and Webhook.</span><span class="sxs-lookup"><span data-stu-id="a7c14-156">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="a7c14-157">Name</span><span class="sxs-lookup"><span data-stu-id="a7c14-157">Name</span></span> |<span data-ttu-id="a7c14-158">Display name for the alert.</span><span class="sxs-lookup"><span data-stu-id="a7c14-158">Display name for the alert.</span></span> |
| <span data-ttu-id="a7c14-159">Version</span><span class="sxs-lookup"><span data-stu-id="a7c14-159">Version</span></span> |<span data-ttu-id="a7c14-160">The API version being used.</span><span class="sxs-lookup"><span data-stu-id="a7c14-160">The API version being used.</span></span>  <span data-ttu-id="a7c14-161">Currently, this should always be set to 1.</span><span class="sxs-lookup"><span data-stu-id="a7c14-161">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="a7c14-162">Retrieving actions</span><span class="sxs-lookup"><span data-stu-id="a7c14-162">Retrieving actions</span></span>
<span data-ttu-id="a7c14-163">Use the Get method to retrieve all actions for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-163">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="a7c14-164">Use the Get method with the action ID to retrieve a particular action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-164">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="a7c14-165">Creating or editing actions</span><span class="sxs-lookup"><span data-stu-id="a7c14-165">Creating or editing actions</span></span>
<span data-ttu-id="a7c14-166">Use the Put method with an action ID that is unique to the schedule to create a new action.</span><span class="sxs-lookup"><span data-stu-id="a7c14-166">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="a7c14-167">When you create an action in the OMS console, a GUID is for the action ID.</span><span class="sxs-lookup"><span data-stu-id="a7c14-167">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

<span data-ttu-id="a7c14-168">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-168">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="a7c14-169">The body of the request must include the etag of the schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-169">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="a7c14-170">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span><span class="sxs-lookup"><span data-stu-id="a7c14-170">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="a7c14-171">Deleting actions</span><span class="sxs-lookup"><span data-stu-id="a7c14-171">Deleting actions</span></span>
<span data-ttu-id="a7c14-172">Use the Delete method with the action ID to delete an action.</span><span class="sxs-lookup"><span data-stu-id="a7c14-172">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="a7c14-173">Alert Actions</span><span class="sxs-lookup"><span data-stu-id="a7c14-173">Alert Actions</span></span>
<span data-ttu-id="a7c14-174">A Schedule should have one and only one Alert action.</span><span class="sxs-lookup"><span data-stu-id="a7c14-174">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="a7c14-175">Alert actions have one or more of the sections in the following table.</span><span class="sxs-lookup"><span data-stu-id="a7c14-175">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="a7c14-176">Each is described in further detail below.</span><span class="sxs-lookup"><span data-stu-id="a7c14-176">Each is described in further detail below.</span></span>

| <span data-ttu-id="a7c14-177">Section</span><span class="sxs-lookup"><span data-stu-id="a7c14-177">Section</span></span> | <span data-ttu-id="a7c14-178">Description</span><span class="sxs-lookup"><span data-stu-id="a7c14-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a7c14-179">Threshold</span><span class="sxs-lookup"><span data-stu-id="a7c14-179">Threshold</span></span> |<span data-ttu-id="a7c14-180">Criteria for when the action is run.</span><span class="sxs-lookup"><span data-stu-id="a7c14-180">Criteria for when the action is run.</span></span> |
| <span data-ttu-id="a7c14-181">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="a7c14-181">EmailNotification</span></span> |<span data-ttu-id="a7c14-182">Send mail to multiple recipients.</span><span class="sxs-lookup"><span data-stu-id="a7c14-182">Send mail to multiple recipients.</span></span> |
| <span data-ttu-id="a7c14-183">Remediation</span><span class="sxs-lookup"><span data-stu-id="a7c14-183">Remediation</span></span> |<span data-ttu-id="a7c14-184">Start a runbook in Azure Automation to attempt to correct identified issue.</span><span class="sxs-lookup"><span data-stu-id="a7c14-184">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="a7c14-185">Thresholds</span><span class="sxs-lookup"><span data-stu-id="a7c14-185">Thresholds</span></span>
<span data-ttu-id="a7c14-186">An Alert action should have one and only one threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-186">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="a7c14-187">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span><span class="sxs-lookup"><span data-stu-id="a7c14-187">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="a7c14-188">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span><span class="sxs-lookup"><span data-stu-id="a7c14-188">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="a7c14-189">Thresholds have the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="a7c14-189">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="a7c14-190">Property</span><span class="sxs-lookup"><span data-stu-id="a7c14-190">Property</span></span> | <span data-ttu-id="a7c14-191">Description</span><span class="sxs-lookup"><span data-stu-id="a7c14-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a7c14-192">Operator</span><span class="sxs-lookup"><span data-stu-id="a7c14-192">Operator</span></span> |<span data-ttu-id="a7c14-193">Operator for the threshold comparison.</span><span class="sxs-lookup"><span data-stu-id="a7c14-193">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="a7c14-194">gt = Greater Than</span><span class="sxs-lookup"><span data-stu-id="a7c14-194">gt = Greater Than</span></span> <br> <span data-ttu-id="a7c14-195">lt = Less Than</span><span class="sxs-lookup"><span data-stu-id="a7c14-195">lt = Less Than</span></span> |
| <span data-ttu-id="a7c14-196">Value</span><span class="sxs-lookup"><span data-stu-id="a7c14-196">Value</span></span> |<span data-ttu-id="a7c14-197">Value for the threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-197">Value for the threshold.</span></span> |

<span data-ttu-id="a7c14-198">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span><span class="sxs-lookup"><span data-stu-id="a7c14-198">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="a7c14-199">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span><span class="sxs-lookup"><span data-stu-id="a7c14-199">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="a7c14-200">Following is a sample response for an action with only a threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-200">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="a7c14-201">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-201">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="a7c14-202">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-202">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="a7c14-203">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="a7c14-203">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="a7c14-204">Email Notification</span><span class="sxs-lookup"><span data-stu-id="a7c14-204">Email Notification</span></span>
<span data-ttu-id="a7c14-205">Email Notifications send mail to one or more recipients.</span><span class="sxs-lookup"><span data-stu-id="a7c14-205">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="a7c14-206">They include the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="a7c14-206">They include the properties in the following table.</span></span>

| <span data-ttu-id="a7c14-207">Property</span><span class="sxs-lookup"><span data-stu-id="a7c14-207">Property</span></span> | <span data-ttu-id="a7c14-208">Description</span><span class="sxs-lookup"><span data-stu-id="a7c14-208">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a7c14-209">Recipients</span><span class="sxs-lookup"><span data-stu-id="a7c14-209">Recipients</span></span> |<span data-ttu-id="a7c14-210">List of mail addresses.</span><span class="sxs-lookup"><span data-stu-id="a7c14-210">List of mail addresses.</span></span> |
| <span data-ttu-id="a7c14-211">Subject</span><span class="sxs-lookup"><span data-stu-id="a7c14-211">Subject</span></span> |<span data-ttu-id="a7c14-212">The subject of the mail.</span><span class="sxs-lookup"><span data-stu-id="a7c14-212">The subject of the mail.</span></span> |
| <span data-ttu-id="a7c14-213">Attachment</span><span class="sxs-lookup"><span data-stu-id="a7c14-213">Attachment</span></span> |<span data-ttu-id="a7c14-214">Attachments are not currently supported, so this will always have a value of “None”.</span><span class="sxs-lookup"><span data-stu-id="a7c14-214">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="a7c14-215">Following is a sample response for an email notification action with a threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-215">Following is a sample response for an email notification action with a threshold.</span></span>  

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

<span data-ttu-id="a7c14-216">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-216">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="a7c14-217">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-217">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="a7c14-218">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-218">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="a7c14-219">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="a7c14-219">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="a7c14-220">Remediation actions</span><span class="sxs-lookup"><span data-stu-id="a7c14-220">Remediation actions</span></span>
<span data-ttu-id="a7c14-221">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span><span class="sxs-lookup"><span data-stu-id="a7c14-221">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="a7c14-222">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span><span class="sxs-lookup"><span data-stu-id="a7c14-222">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="a7c14-223">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span><span class="sxs-lookup"><span data-stu-id="a7c14-223">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

<span data-ttu-id="a7c14-224">Remediations include the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="a7c14-224">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="a7c14-225">Property</span><span class="sxs-lookup"><span data-stu-id="a7c14-225">Property</span></span> | <span data-ttu-id="a7c14-226">Description</span><span class="sxs-lookup"><span data-stu-id="a7c14-226">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a7c14-227">RunbookName</span><span class="sxs-lookup"><span data-stu-id="a7c14-227">RunbookName</span></span> |<span data-ttu-id="a7c14-228">Name of the runbook.</span><span class="sxs-lookup"><span data-stu-id="a7c14-228">Name of the runbook.</span></span> <span data-ttu-id="a7c14-229">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="a7c14-229">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="a7c14-230">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="a7c14-230">WebhookUri</span></span> |<span data-ttu-id="a7c14-231">URI of the webhook.</span><span class="sxs-lookup"><span data-stu-id="a7c14-231">URI of the webhook.</span></span> |
| <span data-ttu-id="a7c14-232">Expiry</span><span class="sxs-lookup"><span data-stu-id="a7c14-232">Expiry</span></span> |<span data-ttu-id="a7c14-233">The expiration date and time of the webhook.</span><span class="sxs-lookup"><span data-stu-id="a7c14-233">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="a7c14-234">If the webhook doesn’t have an expiration, then this can be any valid future date.</span><span class="sxs-lookup"><span data-stu-id="a7c14-234">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="a7c14-235">Following is a sample response for a remediation action with a threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-235">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="a7c14-236">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-236">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="a7c14-237">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-237">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="a7c14-238">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-238">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="a7c14-239">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="a7c14-239">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="a7c14-240">Example</span><span class="sxs-lookup"><span data-stu-id="a7c14-240">Example</span></span>
<span data-ttu-id="a7c14-241">Following is a complete example to create a new email alert.</span><span class="sxs-lookup"><span data-stu-id="a7c14-241">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="a7c14-242">This creates a new schedule along with an action containing a threshold and email.</span><span class="sxs-lookup"><span data-stu-id="a7c14-242">This creates a new schedule along with an action containing a threshold and email.</span></span>

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

### <a name="webhook-actions"></a><span data-ttu-id="a7c14-243">Webhook actions</span><span class="sxs-lookup"><span data-stu-id="a7c14-243">Webhook actions</span></span>
<span data-ttu-id="a7c14-244">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span><span class="sxs-lookup"><span data-stu-id="a7c14-244">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="a7c14-245">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span><span class="sxs-lookup"><span data-stu-id="a7c14-245">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="a7c14-246">They also provide the additional option of providing a payload to be delivered to the remote process.</span><span class="sxs-lookup"><span data-stu-id="a7c14-246">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="a7c14-247">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-247">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="a7c14-248">You can add multiple Webhook actions that will all be run when the threshold is met.</span><span class="sxs-lookup"><span data-stu-id="a7c14-248">You can add multiple Webhook actions that will all be run when the threshold is met.</span></span>

<span data-ttu-id="a7c14-249">Webhook actions include the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="a7c14-249">Webhook actions include the properties in the following table.</span></span>

| <span data-ttu-id="a7c14-250">Property</span><span class="sxs-lookup"><span data-stu-id="a7c14-250">Property</span></span> | <span data-ttu-id="a7c14-251">Description</span><span class="sxs-lookup"><span data-stu-id="a7c14-251">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a7c14-252">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="a7c14-252">WebhookUri</span></span> |<span data-ttu-id="a7c14-253">The subject of the mail.</span><span class="sxs-lookup"><span data-stu-id="a7c14-253">The subject of the mail.</span></span> |
| <span data-ttu-id="a7c14-254">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="a7c14-254">CustomPayload</span></span> |<span data-ttu-id="a7c14-255">Custom payload to be sent to the webhook.</span><span class="sxs-lookup"><span data-stu-id="a7c14-255">Custom payload to be sent to the webhook.</span></span>  <span data-ttu-id="a7c14-256">The format will depend on what the webhook is expecting.</span><span class="sxs-lookup"><span data-stu-id="a7c14-256">The format will depend on what the webhook is expecting.</span></span> |

<span data-ttu-id="a7c14-257">Following is a sample response for webhook action and an associated alert action with a threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-257">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="a7c14-258">Create or edit a webhook action</span><span class="sxs-lookup"><span data-stu-id="a7c14-258">Create or edit a webhook action</span></span>
<span data-ttu-id="a7c14-259">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-259">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="a7c14-260">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span><span class="sxs-lookup"><span data-stu-id="a7c14-260">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="a7c14-261">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span><span class="sxs-lookup"><span data-stu-id="a7c14-261">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="a7c14-262">The body of the request must include the etag of the action.</span><span class="sxs-lookup"><span data-stu-id="a7c14-262">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="a7c14-263">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7c14-263">Next steps</span></span>
* <span data-ttu-id="a7c14-264">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a7c14-264">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

