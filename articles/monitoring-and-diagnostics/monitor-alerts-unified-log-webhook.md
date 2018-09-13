---
title: Webhook actions for log alerts in Azure Alerts
description: This article describes how to an log alert rule using log analytics or application insights, will push data as HTTP webhook and details of the different customizations possible.
author: msvijayn
services: monitoring
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 05/01/2018
ms.author: vinagara
ms.component: alerts
ms.openlocfilehash: f20e102ee1d100ea02da53fe460b56f8f8390418
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867375"
---
# <a name="webhook-actions-for-log-alert-rules"></a><span data-ttu-id="47ae2-103">Webhook actions for log alert rules</span><span class="sxs-lookup"><span data-stu-id="47ae2-103">Webhook actions for log alert rules</span></span>
<span data-ttu-id="47ae2-104">When an [alert is created in Azure ](monitor-alerts-unified-usage.md), you have the option of [configuring using action groups](monitoring-action-groups.md) to perform one or more actions.</span><span class="sxs-lookup"><span data-stu-id="47ae2-104">When an [alert is created in Azure ](monitor-alerts-unified-usage.md), you have the option of [configuring using action groups](monitoring-action-groups.md) to perform one or more actions.</span></span>  <span data-ttu-id="47ae2-105">This article describes the different webhook actions that are available and details on configuring the custom JSON-based webhook.</span><span class="sxs-lookup"><span data-stu-id="47ae2-105">This article describes the different webhook actions that are available and details on configuring the custom JSON-based webhook.</span></span>


## <a name="webhook-actions"></a><span data-ttu-id="47ae2-106">Webhook actions</span><span class="sxs-lookup"><span data-stu-id="47ae2-106">Webhook actions</span></span>

<span data-ttu-id="47ae2-107">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="47ae2-107">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="47ae2-108">The service being called should support webhooks and determine how it uses any payload it receives.</span><span class="sxs-lookup"><span data-stu-id="47ae2-108">The service being called should support webhooks and determine how it uses any payload it receives.</span></span>   <span data-ttu-id="47ae2-109">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="47ae2-109">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  

<span data-ttu-id="47ae2-110">Webhook actions require the properties in the following table:</span><span class="sxs-lookup"><span data-stu-id="47ae2-110">Webhook actions require the properties in the following table:</span></span>

| <span data-ttu-id="47ae2-111">Property</span><span class="sxs-lookup"><span data-stu-id="47ae2-111">Property</span></span> | <span data-ttu-id="47ae2-112">Description</span><span class="sxs-lookup"><span data-stu-id="47ae2-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="47ae2-113">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="47ae2-113">Webhook URL</span></span> |<span data-ttu-id="47ae2-114">The URL of the webhook.</span><span class="sxs-lookup"><span data-stu-id="47ae2-114">The URL of the webhook.</span></span> |
| <span data-ttu-id="47ae2-115">Custom JSON payload</span><span class="sxs-lookup"><span data-stu-id="47ae2-115">Custom JSON payload</span></span> |<span data-ttu-id="47ae2-116">Custom payload to send with the webhook, when this option is chosen during alert creation.</span><span class="sxs-lookup"><span data-stu-id="47ae2-116">Custom payload to send with the webhook, when this option is chosen during alert creation.</span></span> <span data-ttu-id="47ae2-117">Details available at [Manage alerts using Azure Alerts ](monitor-alerts-unified-usage.md)</span><span class="sxs-lookup"><span data-stu-id="47ae2-117">Details available at [Manage alerts using Azure Alerts ](monitor-alerts-unified-usage.md)</span></span> |

> [!NOTE]
> <span data-ttu-id="47ae2-118">Test Webhook button alongside *Include custom JSON payload for webhook* option for Log Alert, will trigger dummy call to test the webhook URL.</span><span class="sxs-lookup"><span data-stu-id="47ae2-118">Test Webhook button alongside *Include custom JSON payload for webhook* option for Log Alert, will trigger dummy call to test the webhook URL.</span></span> <span data-ttu-id="47ae2-119">It does not contain actual data and representative of JSON schema used for Log Alerts.</span><span class="sxs-lookup"><span data-stu-id="47ae2-119">It does not contain actual data and representative of JSON schema used for Log Alerts.</span></span> 

<span data-ttu-id="47ae2-120">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span><span class="sxs-lookup"><span data-stu-id="47ae2-120">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span></span>  <span data-ttu-id="47ae2-121">By default, the payload includes the values in the following table:  You can choose to replace this payload with a custom one of your own.</span><span class="sxs-lookup"><span data-stu-id="47ae2-121">By default, the payload includes the values in the following table:  You can choose to replace this payload with a custom one of your own.</span></span>  <span data-ttu-id="47ae2-122">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span><span class="sxs-lookup"><span data-stu-id="47ae2-122">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span></span>


| <span data-ttu-id="47ae2-123">Parameter</span><span class="sxs-lookup"><span data-stu-id="47ae2-123">Parameter</span></span> | <span data-ttu-id="47ae2-124">Variable</span><span class="sxs-lookup"><span data-stu-id="47ae2-124">Variable</span></span> | <span data-ttu-id="47ae2-125">Description</span><span class="sxs-lookup"><span data-stu-id="47ae2-125">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="47ae2-126">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="47ae2-126">AlertRuleName</span></span> |<span data-ttu-id="47ae2-127">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="47ae2-127">#alertrulename</span></span> |<span data-ttu-id="47ae2-128">Name of the alert rule.</span><span class="sxs-lookup"><span data-stu-id="47ae2-128">Name of the alert rule.</span></span> |
| <span data-ttu-id="47ae2-129">Severity</span><span class="sxs-lookup"><span data-stu-id="47ae2-129">Severity</span></span> |<span data-ttu-id="47ae2-130">#severity</span><span class="sxs-lookup"><span data-stu-id="47ae2-130">#severity</span></span> |<span data-ttu-id="47ae2-131">Severity set for the fired log alert.</span><span class="sxs-lookup"><span data-stu-id="47ae2-131">Severity set for the fired log alert.</span></span> |
| <span data-ttu-id="47ae2-132">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="47ae2-132">AlertThresholdOperator</span></span> |<span data-ttu-id="47ae2-133">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="47ae2-133">#thresholdoperator</span></span> |<span data-ttu-id="47ae2-134">Threshold operator for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="47ae2-134">Threshold operator for the alert rule.</span></span>  <span data-ttu-id="47ae2-135">*Greater than* or *Less than*.</span><span class="sxs-lookup"><span data-stu-id="47ae2-135">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="47ae2-136">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="47ae2-136">AlertThresholdValue</span></span> |<span data-ttu-id="47ae2-137">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="47ae2-137">#thresholdvalue</span></span> |<span data-ttu-id="47ae2-138">Threshold value for the alert rule.</span><span class="sxs-lookup"><span data-stu-id="47ae2-138">Threshold value for the alert rule.</span></span> |
| <span data-ttu-id="47ae2-139">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="47ae2-139">LinkToSearchResults</span></span> |<span data-ttu-id="47ae2-140">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="47ae2-140">#linktosearchresults</span></span> |<span data-ttu-id="47ae2-141">Link to Analytics portal that returns the records from the query that created the alert.</span><span class="sxs-lookup"><span data-stu-id="47ae2-141">Link to Analytics portal that returns the records from the query that created the alert.</span></span> |
| <span data-ttu-id="47ae2-142">ResultCount</span><span class="sxs-lookup"><span data-stu-id="47ae2-142">ResultCount</span></span> |<span data-ttu-id="47ae2-143">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="47ae2-143">#searchresultcount</span></span> |<span data-ttu-id="47ae2-144">Number of records in the search results.</span><span class="sxs-lookup"><span data-stu-id="47ae2-144">Number of records in the search results.</span></span> |
| <span data-ttu-id="47ae2-145">Search Interval End time</span><span class="sxs-lookup"><span data-stu-id="47ae2-145">Search Interval End time</span></span> |<span data-ttu-id="47ae2-146">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="47ae2-146">#searchintervalendtimeutc</span></span> |<span data-ttu-id="47ae2-147">End time for the query in UTC, format - mm/dd/yyyy HH:mm:ss AM/PM.</span><span class="sxs-lookup"><span data-stu-id="47ae2-147">End time for the query in UTC, format - mm/dd/yyyy HH:mm:ss AM/PM.</span></span> |
| <span data-ttu-id="47ae2-148">Search Interval</span><span class="sxs-lookup"><span data-stu-id="47ae2-148">Search Interval</span></span> |<span data-ttu-id="47ae2-149">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="47ae2-149">#searchinterval</span></span> |<span data-ttu-id="47ae2-150">Time window for the alert rule, format - HH:mm:ss.</span><span class="sxs-lookup"><span data-stu-id="47ae2-150">Time window for the alert rule, format - HH:mm:ss.</span></span> |
| <span data-ttu-id="47ae2-151">Search Interval StartTime</span><span class="sxs-lookup"><span data-stu-id="47ae2-151">Search Interval StartTime</span></span> |<span data-ttu-id="47ae2-152">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="47ae2-152">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="47ae2-153">Start time for the query in UTC, format - mm/dd/yyyy HH:mm:ss AM/PM..</span><span class="sxs-lookup"><span data-stu-id="47ae2-153">Start time for the query in UTC, format - mm/dd/yyyy HH:mm:ss AM/PM..</span></span> 
| <span data-ttu-id="47ae2-154">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="47ae2-154">SearchQuery</span></span> |<span data-ttu-id="47ae2-155">#searchquery</span><span class="sxs-lookup"><span data-stu-id="47ae2-155">#searchquery</span></span> |<span data-ttu-id="47ae2-156">Log search query used by the alert rule.</span><span class="sxs-lookup"><span data-stu-id="47ae2-156">Log search query used by the alert rule.</span></span> |
| <span data-ttu-id="47ae2-157">SearchResults</span><span class="sxs-lookup"><span data-stu-id="47ae2-157">SearchResults</span></span> |<span data-ttu-id="47ae2-158">"IncludeSearchResults": true</span><span class="sxs-lookup"><span data-stu-id="47ae2-158">"IncludeSearchResults": true</span></span>|<span data-ttu-id="47ae2-159">Records returned by the query as a JSON Table, limited to the first 1,000 records; if "IncludeSearchResults": true is added in custom JSON webhook definition as a top-level property.</span><span class="sxs-lookup"><span data-stu-id="47ae2-159">Records returned by the query as a JSON Table, limited to the first 1,000 records; if "IncludeSearchResults": true is added in custom JSON webhook definition as a top-level property.</span></span> |
| <span data-ttu-id="47ae2-160">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="47ae2-160">WorkspaceID</span></span> |<span data-ttu-id="47ae2-161">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="47ae2-161">#workspaceid</span></span> |<span data-ttu-id="47ae2-162">ID of your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="47ae2-162">ID of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="47ae2-163">Application ID</span><span class="sxs-lookup"><span data-stu-id="47ae2-163">Application ID</span></span> |<span data-ttu-id="47ae2-164">#applicationid</span><span class="sxs-lookup"><span data-stu-id="47ae2-164">#applicationid</span></span> |<span data-ttu-id="47ae2-165">ID of your Application Insight app.</span><span class="sxs-lookup"><span data-stu-id="47ae2-165">ID of your Application Insight app.</span></span> |
| <span data-ttu-id="47ae2-166">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="47ae2-166">Subscription ID</span></span> |<span data-ttu-id="47ae2-167">#subscriptionid</span><span class="sxs-lookup"><span data-stu-id="47ae2-167">#subscriptionid</span></span> |<span data-ttu-id="47ae2-168">ID of your Azure Subscription used with Application Insights.</span><span class="sxs-lookup"><span data-stu-id="47ae2-168">ID of your Azure Subscription used with Application Insights.</span></span> 

> [!NOTE]
> <span data-ttu-id="47ae2-169">LinkToSearchResults passes parameters like SearchQuery, Search Interval StartTime & Search Interval End time in the URL to Azure portal for viewing in Analytics section.</span><span class="sxs-lookup"><span data-stu-id="47ae2-169">LinkToSearchResults passes parameters like SearchQuery, Search Interval StartTime & Search Interval End time in the URL to Azure portal for viewing in Analytics section.</span></span> <span data-ttu-id="47ae2-170">Azure portal has URI size limit of approx 2000 characters and will open if parameters values exceed the said limit.</span><span class="sxs-lookup"><span data-stu-id="47ae2-170">Azure portal has URI size limit of approx 2000 characters and will open if parameters values exceed the said limit.</span></span> <span data-ttu-id="47ae2-171">Users can manually input details to view results in Analytics portal or use the [Application Insights Analytics REST API](https://dev.applicationinsights.io/documentation/Using-the-API) or [Log Analytics REST API](https://dev.loganalytics.io/reference) to retrieve results programmatically</span><span class="sxs-lookup"><span data-stu-id="47ae2-171">Users can manually input details to view results in Analytics portal or use the [Application Insights Analytics REST API](https://dev.applicationinsights.io/documentation/Using-the-API) or [Log Analytics REST API](https://dev.loganalytics.io/reference) to retrieve results programmatically</span></span> 

<span data-ttu-id="47ae2-172">For example, you might specify the following custom payload that includes a single parameter called *text*.</span><span class="sxs-lookup"><span data-stu-id="47ae2-172">For example, you might specify the following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="47ae2-173">The service that this webhook calls would be expecting this parameter.</span><span class="sxs-lookup"><span data-stu-id="47ae2-173">The service that this webhook calls would be expecting this parameter.</span></span>

```json

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }
```
<span data-ttu-id="47ae2-174">This example payload would resolve to something like the following when sent to the webhook.</span><span class="sxs-lookup"><span data-stu-id="47ae2-174">This example payload would resolve to something like the following when sent to the webhook.</span></span>

```json
    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }
```
<span data-ttu-id="47ae2-175">As all variables in a custom webhook have to specified within JSON enclosure like "#searchinterval", the resultant webhook will also have variable data inside enclosure like "00:05:00".</span><span class="sxs-lookup"><span data-stu-id="47ae2-175">As all variables in a custom webhook have to specified within JSON enclosure like "#searchinterval", the resultant webhook will also have variable data inside enclosure like "00:05:00".</span></span>

<span data-ttu-id="47ae2-176">To include search results in a custom payload, ensure that **IncudeSearchResults** is set as a top-level property in the json payload.</span><span class="sxs-lookup"><span data-stu-id="47ae2-176">To include search results in a custom payload, ensure that **IncudeSearchResults** is set as a top-level property in the json payload.</span></span> 

## <a name="sample-payloads"></a><span data-ttu-id="47ae2-177">Sample payloads</span><span class="sxs-lookup"><span data-stu-id="47ae2-177">Sample payloads</span></span>
<span data-ttu-id="47ae2-178">This section shows sample payload for webhook for Log Alerts, including when payload is standard and when its custom.</span><span class="sxs-lookup"><span data-stu-id="47ae2-178">This section shows sample payload for webhook for Log Alerts, including when payload is standard and when its custom.</span></span>

> [!NOTE]
> <span data-ttu-id="47ae2-179">To ensure backward compatibility, standard webhook payload for alerts using Azure Log Analytics is same as [Log Analytics alert management](../log-analytics/log-analytics-alerts-creating.md).</span><span class="sxs-lookup"><span data-stu-id="47ae2-179">To ensure backward compatibility, standard webhook payload for alerts using Azure Log Analytics is same as [Log Analytics alert management](../log-analytics/log-analytics-alerts-creating.md).</span></span> <span data-ttu-id="47ae2-180">But for log alerts using [Application Insights](../application-insights/app-insights-analytics.md), the standard webhook payload is based on Action Group schema.</span><span class="sxs-lookup"><span data-stu-id="47ae2-180">But for log alerts using [Application Insights](../application-insights/app-insights-analytics.md), the standard webhook payload is based on Action Group schema.</span></span>

### <a name="standard-webhook-for-log-alerts"></a><span data-ttu-id="47ae2-181">Standard Webhook for Log Alerts</span><span class="sxs-lookup"><span data-stu-id="47ae2-181">Standard Webhook for Log Alerts</span></span> 
<span data-ttu-id="47ae2-182">Both of these examples have stated a dummy payload with only two columns and two rows.</span><span class="sxs-lookup"><span data-stu-id="47ae2-182">Both of these examples have stated a dummy payload with only two columns and two rows.</span></span>

#### <a name="log-alert-for-azure-log-analytics"></a><span data-ttu-id="47ae2-183">Log Alert for Azure Log-Analytics</span><span class="sxs-lookup"><span data-stu-id="47ae2-183">Log Alert for Azure Log-Analytics</span></span>
<span data-ttu-id="47ae2-184">Following is a sample payload for a standard webhook action *without custom Json option* being used for  log analytics-based alerts.</span><span class="sxs-lookup"><span data-stu-id="47ae2-184">Following is a sample payload for a standard webhook action *without custom Json option* being used for  log analytics-based alerts.</span></span>

```json
{
    "WorkspaceId":"12345a-1234b-123c-123d-12345678e",
    "AlertRuleName":"AcmeRule","SearchQuery":"search *",
    "SearchResult":
        {
        "tables":[
                    {"name":"PrimaryResult","columns":
                        [
                        {"name":"$table","type":"string"},
                        {"name":"Id","type":"string"},
                        {"name":"TimeGenerated","type":"datetime"}
                        ],
                    "rows":
                        [
                            ["Fabrikam","33446677a","2018-02-02T15:03:12.18Z"],
                            ["Contoso","33445566b","2018-02-02T15:16:53.932Z"]
                        ]
                    }
                ]
        },
    "SearchIntervalStartTimeUtc": "2018-03-26T08:10:40Z",
    "SearchIntervalEndtimeUtc": "2018-03-26T09:10:40Z",
    "AlertThresholdOperator": "Greater Than",
    "AlertThresholdValue": 0,
    "ResultCount": 2,
    "SearchIntervalInSeconds": 3600,
    "LinkToSearchResults": "https://workspaceID.portal.mms.microsoft.com/#Workspace/search/index?_timeInterval.intervalEnd=2018-03-26T09%3a10%3a40.0000000Z&_timeInterval.intervalDuration=3600&q=Usage",
    "Description": null,
    "Severity": "Warning"
 }
 ```   

#### <a name="log-alert-for-azure-application-insights"></a><span data-ttu-id="47ae2-185">Log Alert for Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="47ae2-185">Log Alert for Azure Application Insights</span></span>
<span data-ttu-id="47ae2-186">Following is a sample payload for a standard webhook *without custom Json option* when used for application insights-based log-alerts.</span><span class="sxs-lookup"><span data-stu-id="47ae2-186">Following is a sample payload for a standard webhook *without custom Json option* when used for application insights-based log-alerts.</span></span>
    
```json
{
    "schemaId":"Microsoft.Insights/LogAlert","data":
    { 
    "SubscriptionId":"12345a-1234b-123c-123d-12345678e",
    "AlertRuleName":"AcmeRule","SearchQuery":"search *",
    "SearchResult":
        {
        "tables":[
                    {"name":"PrimaryResult","columns":
                        [
                        {"name":"$table","type":"string"},
                        {"name":"Id","type":"string"},
                        {"name":"TimeGenerated","type":"datetime"}
                        ],
                    "rows":
                        [
                            ["Fabrikam","33446677a","2018-02-02T15:03:12.18Z"],
                            ["Contoso","33445566b","2018-02-02T15:16:53.932Z"]
                        ]
                    }
                ]
        },
    "SearchIntervalStartTimeUtc": "2018-03-26T08:10:40Z",
    "SearchIntervalEndtimeUtc": "2018-03-26T09:10:40Z",
    "AlertThresholdOperator": "Greater Than",
    "AlertThresholdValue": 0,
    "ResultCount": 2,
    "SearchIntervalInSeconds": 3600,
    "LinkToSearchResults": "https://analytics.applicationinsights.io/subscriptions/12345a-1234b-123c-123d-12345678e/?query=search+*+&timeInterval.intervalEnd=2018-03-26T09%3a10%3a40.0000000Z&_timeInterval.intervalDuration=3600&q=Usage",
    "Description": null,
    "Severity": "Error",
    "ApplicationId": "123123f0-01d3-12ab-123f-abc1ab01c0a1"
    }
}
```

#### <a name="log-alert-with-custom-json-payload"></a><span data-ttu-id="47ae2-187">Log Alert with custom JSON Payload</span><span class="sxs-lookup"><span data-stu-id="47ae2-187">Log Alert with custom JSON Payload</span></span>
<span data-ttu-id="47ae2-188">For example, to create a custom payload that includes just the alert name and the search results, you could use the following:</span><span class="sxs-lookup"><span data-stu-id="47ae2-188">For example, to create a custom payload that includes just the alert name and the search results, you could use the following:</span></span> 

```json
    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }
```

<span data-ttu-id="47ae2-189">Following is a sample payload for a custom webhook action for any log alert.</span><span class="sxs-lookup"><span data-stu-id="47ae2-189">Following is a sample payload for a custom webhook action for any log alert.</span></span>
    
```json
    {
    "alertname":"AcmeRule","IncludeSearchResults":true,
    "SearchResult":
        {
        "tables":[
                    {"name":"PrimaryResult","columns":
                        [
                        {"name":"$table","type":"string"},
                        {"name":"Id","type":"string"},
                        {"name":"TimeGenerated","type":"datetime"}
                        ],
                    "rows":
                        [
                            ["Fabrikam","33446677a","2018-02-02T15:03:12.18Z"],
                            ["Contoso","33445566b","2018-02-02T15:16:53.932Z"]
                        ]
                    }
                ]
        }
    }
```


## <a name="next-steps"></a><span data-ttu-id="47ae2-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="47ae2-190">Next steps</span></span>
- <span data-ttu-id="47ae2-191">Learn about [Log Alerts in Azure Alerts ](monitor-alerts-unified-log.md)</span><span class="sxs-lookup"><span data-stu-id="47ae2-191">Learn about [Log Alerts in Azure Alerts ](monitor-alerts-unified-log.md)</span></span>
- <span data-ttu-id="47ae2-192">Create and manage [action groups in Azure](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="47ae2-192">Create and manage [action groups in Azure](monitoring-action-groups.md)</span></span>
- <span data-ttu-id="47ae2-193">Learn more about [Application Insights](../application-insights/app-insights-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="47ae2-193">Learn more about [Application Insights](../application-insights/app-insights-analytics.md)</span></span>
- <span data-ttu-id="47ae2-194">Learn more about [Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47ae2-194">Learn more about [Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> 