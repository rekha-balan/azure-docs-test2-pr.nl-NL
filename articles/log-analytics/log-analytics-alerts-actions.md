---
title: Responses to alerts in OMS Log Analytics | Microsoft Docs
description: Alerts in Log Analytics identify important information in your OMS repository and can proactively notify you of issues or invoke actions to attempt to correct them.  This article describes how to create an alert rule and details the different actions they can take.
services: log-analytics
documentationcenter: ''
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551664"
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a><span data-ttu-id="03506-104">Add actions to alert rules in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="03506-104">Add actions to alert rules in Log Analytics</span></span>
<span data-ttu-id="03506-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have the option of [configuring the alert rule](log-analytics-alerts.md) to perform one or more actions.</span><span class="sxs-lookup"><span data-stu-id="03506-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have the option of [configuring the alert rule](log-analytics-alerts.md) to perform one or more actions.</span></span>  <span data-ttu-id="03506-106">This article describes the different actions that are available and details on configuring each kind.</span><span class="sxs-lookup"><span data-stu-id="03506-106">This article describes the different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="03506-107">Action</span><span class="sxs-lookup"><span data-stu-id="03506-107">Action</span></span> | <span data-ttu-id="03506-108">Description</span><span class="sxs-lookup"><span data-stu-id="03506-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="03506-109">Email</span><span class="sxs-lookup"><span data-stu-id="03506-109">Email</span></span>](#email-actions) | <span data-ttu-id="03506-110">Send an e-mail with the details of the alert to one or more recipients.</span><span class="sxs-lookup"><span data-stu-id="03506-110">Send an e-mail with the details of the alert to one or more recipients.</span></span> |
| [<span data-ttu-id="03506-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="03506-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="03506-112">Invoke an external process through a single HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="03506-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="03506-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="03506-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="03506-114">Start a runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="03506-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="03506-115">Email actions</span><span class="sxs-lookup"><span data-stu-id="03506-115">Email actions</span></span>
<span data-ttu-id="03506-116">Email actions send an e-mail with the details of the alert to one or more recipients.</span><span class="sxs-lookup"><span data-stu-id="03506-116">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>  <span data-ttu-id="03506-117">You can specify the subject of the mail, but it's content is a standard format constructed by Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="03506-117">You can specify the subject of the mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="03506-118">It includes summary information such as the name of the alert in addition to details of up to ten records returned by the log search.</span><span class="sxs-lookup"><span data-stu-id="03506-118">It includes summary information such as the name of the alert in addition to details of up to ten records returned by the log search.</span></span>  <span data-ttu-id="03506-119">It also includes a link to a log search in Log Analytics that will return the entire set of records from that query.</span><span class="sxs-lookup"><span data-stu-id="03506-119">It also includes a link to a log search in Log Analytics that will return the entire set of records from that query.</span></span>   <span data-ttu-id="03506-120">The sender of the mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span><span class="sxs-lookup"><span data-stu-id="03506-120">The sender of the mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="03506-121">Email actions require the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="03506-121">Email actions require the properties in the following table.</span></span>

| <span data-ttu-id="03506-122">Property</span><span class="sxs-lookup"><span data-stu-id="03506-122">Property</span></span> | <span data-ttu-id="03506-123">Description</span><span class="sxs-lookup"><span data-stu-id="03506-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03506-124">Subject</span><span class="sxs-lookup"><span data-stu-id="03506-124">Subject</span></span> |<span data-ttu-id="03506-125">Subject in the email.</span><span class="sxs-lookup"><span data-stu-id="03506-125">Subject in the email.</span></span>  <span data-ttu-id="03506-126">You cannot modify the body of the mail.</span><span class="sxs-lookup"><span data-stu-id="03506-126">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="03506-127">Recipients</span><span class="sxs-lookup"><span data-stu-id="03506-127">Recipients</span></span> |<span data-ttu-id="03506-128">Addresses of all e-mail recipients.</span><span class="sxs-lookup"><span data-stu-id="03506-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="03506-129">If you specify more than one address, then separate the addresses with a semicolon (;).</span><span class="sxs-lookup"><span data-stu-id="03506-129">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="03506-130">Webhook actions</span><span class="sxs-lookup"><span data-stu-id="03506-130">Webhook actions</span></span>

<span data-ttu-id="03506-131">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="03506-131">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="03506-132">The service being called should support webhooks and determine how it will use any payload it receives.</span><span class="sxs-lookup"><span data-stu-id="03506-132">The service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="03506-133">You could also call a REST API that doesn't specifically support webhooks as long as the request is in a format that the API understands.</span><span class="sxs-lookup"><span data-stu-id="03506-133">You could also call a REST API that doesn't specifically support webhooks as long as the request is in a format that the API understands.</span></span>  <span data-ttu-id="03506-134">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="03506-134">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="03506-135">A complete walkthrough of creating an alert rule with a webhook to call Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="03506-135">A complete walkthrough of creating an alert rule with a webhook to call Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="03506-136">Webhook actions require the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="03506-136">Webhook actions require the properties in the following table.</span></span>

| <span data-ttu-id="03506-137">Property</span><span class="sxs-lookup"><span data-stu-id="03506-137">Property</span></span> | <span data-ttu-id="03506-138">Description</span><span class="sxs-lookup"><span data-stu-id="03506-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03506-139">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="03506-139">Webhook URL</span></span> |<span data-ttu-id="03506-140">The URL of the webhook.</span><span class="sxs-lookup"><span data-stu-id="03506-140">The URL of the webhook.</span></span> |
| <span data-ttu-id="03506-141">Custom JSON payload</span><span class="sxs-lookup"><span data-stu-id="03506-141">Custom JSON payload</span></span> |<span data-ttu-id="03506-142">Custom payload to send with the webhook.</span><span class="sxs-lookup"><span data-stu-id="03506-142">Custom payload to send with the webhook.</span></span>  <span data-ttu-id="03506-143">See below for details.</span><span class="sxs-lookup"><span data-stu-id="03506-143">See below for details.</span></span> |


<span data-ttu-id="03506-144">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span><span class="sxs-lookup"><span data-stu-id="03506-144">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span></span>  <span data-ttu-id="03506-145">By default, the payload will include the values in the following table.</span><span class="sxs-lookup"><span data-stu-id="03506-145">By default, the payload will include the values in the following table.</span></span>  <span data-ttu-id="03506-146">You can choose to replace this payload with a custom one of your own.</span><span class="sxs-lookup"><span data-stu-id="03506-146">You can choose to replace this payload with a custom one of your own.</span></span>  <span data-ttu-id="03506-147">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span><span class="sxs-lookup"><span data-stu-id="03506-147">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span></span>

| <span data-ttu-id="03506-148">Parameter</span><span class="sxs-lookup"><span data-stu-id="03506-148">Parameter</span></span> | <span data-ttu-id="03506-149">Variable</span><span class="sxs-lookup"><span data-stu-id="03506-149">Variable</span></span> | <span data-ttu-id="03506-150">Description</span><span class="sxs-lookup"><span data-stu-id="03506-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="03506-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="03506-151">AlertRuleName</span></span> |<span data-ttu-id="03506-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="03506-152">#alertrulename</span></span> |<span data-ttu-id="03506-153">Name of the alert rule.</span><span class="sxs-lookup"><span data-stu-id="03506-153">Name of the alert rule.</span></span> |
| <span data-ttu-id="03506-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="03506-154">AlertThresholdOperator</span></span> |<span data-ttu-id="03506-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="03506-155">#thresholdoperator</span></span> |<span data-ttu-id="03506-156">Threshold operator for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="03506-156">Threshold operator for the alert rule.</span></span>  <span data-ttu-id="03506-157">*Greater than* or *Less than*.</span><span class="sxs-lookup"><span data-stu-id="03506-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="03506-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="03506-158">AlertThresholdValue</span></span> |<span data-ttu-id="03506-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="03506-159">#thresholdvalue</span></span> |<span data-ttu-id="03506-160">Threshold value for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="03506-160">Threshold value for the alert rule.</span></span> |
| <span data-ttu-id="03506-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="03506-161">LinkToSearchResults</span></span> |<span data-ttu-id="03506-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="03506-162">#linktosearchresults</span></span> |<span data-ttu-id="03506-163">Link to Log Analytics log search that returns the records from the query that created the alert.</span><span class="sxs-lookup"><span data-stu-id="03506-163">Link to Log Analytics log search that returns the records from the query that created the alert.</span></span> |
| <span data-ttu-id="03506-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="03506-164">ResultCount</span></span> |<span data-ttu-id="03506-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="03506-165">#searchresultcount</span></span> |<span data-ttu-id="03506-166">Number of records in the search results.</span><span class="sxs-lookup"><span data-stu-id="03506-166">Number of records in the search results.</span></span> |
| <span data-ttu-id="03506-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="03506-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="03506-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="03506-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="03506-169">End time for the query in UTC format.</span><span class="sxs-lookup"><span data-stu-id="03506-169">End time for the query in UTC format.</span></span> |
| <span data-ttu-id="03506-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="03506-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="03506-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="03506-171">#searchinterval</span></span> |<span data-ttu-id="03506-172">Time window for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="03506-172">Time window for the alert rule.</span></span> |
| <span data-ttu-id="03506-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="03506-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="03506-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="03506-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="03506-175">Start time for the query in UTC format.</span><span class="sxs-lookup"><span data-stu-id="03506-175">Start time for the query in UTC format.</span></span> |
| <span data-ttu-id="03506-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="03506-176">SearchQuery</span></span> |<span data-ttu-id="03506-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="03506-177">#searchquery</span></span> |<span data-ttu-id="03506-178">Log search query used by the alert rule.</span><span class="sxs-lookup"><span data-stu-id="03506-178">Log search query used by the alert rule.</span></span> |
| <span data-ttu-id="03506-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="03506-179">SearchResults</span></span> |<span data-ttu-id="03506-180">See below</span><span class="sxs-lookup"><span data-stu-id="03506-180">See below</span></span> |<span data-ttu-id="03506-181">Records returned by the query in JSON format.</span><span class="sxs-lookup"><span data-stu-id="03506-181">Records returned by the query in JSON format.</span></span>  <span data-ttu-id="03506-182">Limited to the first 5,000 records.</span><span class="sxs-lookup"><span data-stu-id="03506-182">Limited to the first 5,000 records.</span></span> |
| <span data-ttu-id="03506-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="03506-183">WorkspaceID</span></span> |<span data-ttu-id="03506-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="03506-184">#workspaceid</span></span> |<span data-ttu-id="03506-185">ID of your OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="03506-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="03506-186">For example, you might specify the following custom payload that includes a single parameter called *text*.</span><span class="sxs-lookup"><span data-stu-id="03506-186">For example, you might specify the following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="03506-187">The service that this webhook calls would be expecting this parameter.</span><span class="sxs-lookup"><span data-stu-id="03506-187">The service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="03506-188">This example payload would resolve to something like the following when sent to the webhook.</span><span class="sxs-lookup"><span data-stu-id="03506-188">This example payload would resolve to something like the following when sent to the webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="03506-189">To include search results in a custom payload, add the following line as a top level property in the json payload.</span><span class="sxs-lookup"><span data-stu-id="03506-189">To include search results in a custom payload, add the following line as a top level property in the json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="03506-190">For example, to create a custom payload that includes just the alert name and the search results, you could use the following.</span><span class="sxs-lookup"><span data-stu-id="03506-190">For example, to create a custom payload that includes just the alert name and the search results, you could use the following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="03506-191">You can walk through a complete example of creating an alert rule with a webhook to start an external service at [Create an alert webhook action in OMS Log Analytics to send message to Slack](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="03506-191">You can walk through a complete example of creating an alert rule with a webhook to start an external service at [Create an alert webhook action in OMS Log Analytics to send message to Slack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="03506-192">Runbook actions</span><span class="sxs-lookup"><span data-stu-id="03506-192">Runbook actions</span></span>
<span data-ttu-id="03506-193">Runbook actions start a runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="03506-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="03506-194">In order to use this type of action, you must have the [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="03506-194">In order to use this type of action, you must have the [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="03506-195">You can select from the runbooks in the automation account that you configured in the Automation solution.</span><span class="sxs-lookup"><span data-stu-id="03506-195">You can select from the runbooks in the automation account that you configured in the Automation solution.</span></span>

<span data-ttu-id="03506-196">Runbook actions require the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="03506-196">Runbook actions require the properties in the following table.</span></span>

| <span data-ttu-id="03506-197">Property</span><span class="sxs-lookup"><span data-stu-id="03506-197">Property</span></span> | <span data-ttu-id="03506-198">Description</span><span class="sxs-lookup"><span data-stu-id="03506-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="03506-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="03506-199">Runbook</span></span> | <span data-ttu-id="03506-200">Runbook that you want to start when an alert is created.</span><span class="sxs-lookup"><span data-stu-id="03506-200">Runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="03506-201">Run on</span><span class="sxs-lookup"><span data-stu-id="03506-201">Run on</span></span> | <span data-ttu-id="03506-202">Specify **Azure** to run the runbook in the cloud.</span><span class="sxs-lookup"><span data-stu-id="03506-202">Specify **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="03506-203">Specify **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span><span class="sxs-lookup"><span data-stu-id="03506-203">Specify **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="03506-204">Runbook actions start the runbook using a [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="03506-204">Runbook actions start the runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="03506-205">When you create the alert rule, it will automatically create a new webhook for the runbook with the name **OMS Alert Remediation** followed by a GUID.</span><span class="sxs-lookup"><span data-stu-id="03506-205">When you create the alert rule, it will automatically create a new webhook for the runbook with the name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="03506-206">You cannot directly populate any parameters of the runbook, but the [$WebhookData parameter](../automation/automation-webhooks.md) will include the details of the alert, including the results of the log search that created it.</span><span class="sxs-lookup"><span data-stu-id="03506-206">You cannot directly populate any parameters of the runbook, but the [$WebhookData parameter](../automation/automation-webhooks.md) will include the details of the alert, including the results of the log search that created it.</span></span>  <span data-ttu-id="03506-207">The runbook will need to define **$WebhookData** as a parameter for it to access the properties of the alert.</span><span class="sxs-lookup"><span data-stu-id="03506-207">The runbook will need to define **$WebhookData** as a parameter for it to access the properties of the alert.</span></span>  <span data-ttu-id="03506-208">The alert data is available in json format in a single property called **SearchResults** in the **RequestBody** property of **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="03506-208">The alert data is available in json format in a single property called **SearchResults** in the **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="03506-209">This will have with the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="03506-209">This will have with the properties in the following table.</span></span>

| <span data-ttu-id="03506-210">Node</span><span class="sxs-lookup"><span data-stu-id="03506-210">Node</span></span> | <span data-ttu-id="03506-211">Description</span><span class="sxs-lookup"><span data-stu-id="03506-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="03506-212">id</span><span class="sxs-lookup"><span data-stu-id="03506-212">id</span></span> |<span data-ttu-id="03506-213">Path and GUID of the search.</span><span class="sxs-lookup"><span data-stu-id="03506-213">Path and GUID of the search.</span></span> |
| <span data-ttu-id="03506-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="03506-214">__metadata</span></span> |<span data-ttu-id="03506-215">Information about the alert including the number of records and status of the search results.</span><span class="sxs-lookup"><span data-stu-id="03506-215">Information about the alert including the number of records and status of the search results.</span></span> |
| <span data-ttu-id="03506-216">value</span><span class="sxs-lookup"><span data-stu-id="03506-216">value</span></span> |<span data-ttu-id="03506-217">Separate entry for each record in the search results.</span><span class="sxs-lookup"><span data-stu-id="03506-217">Separate entry for each record in the search results.</span></span>  <span data-ttu-id="03506-218">The details of the entry will match the properties and values of the record.</span><span class="sxs-lookup"><span data-stu-id="03506-218">The details of the entry will match the properties and values of the record.</span></span> |

<span data-ttu-id="03506-219">For example, the following runbook would extract the records returned by the log search  and assign different properties based on the type of each record.</span><span class="sxs-lookup"><span data-stu-id="03506-219">For example, the following runbook would extract the records returned by the log search  and assign different properties based on the type of each record.</span></span>  <span data-ttu-id="03506-220">Note that the runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="03506-220">Note that the runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a><span data-ttu-id="03506-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="03506-221">Next steps</span></span>
- <span data-ttu-id="03506-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span><span class="sxs-lookup"><span data-stu-id="03506-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="03506-223">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span><span class="sxs-lookup"><span data-stu-id="03506-223">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>