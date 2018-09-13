---
title: Understand the webhook schema used in activity log alerts
description: Learn about the schema of the JSON that is posted to a webhook URL when an activity log alert activates.
author: johnkemnetz
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 03/31/2017
ms.author: johnkem
ms.component: alerts
ms.openlocfilehash: 3935da72cb747a642ee1f360dc5318fc2d34e763
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783177"
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="5e460-103">Webhooks for Azure activity log alerts</span><span class="sxs-lookup"><span data-stu-id="5e460-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="5e460-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span><span class="sxs-lookup"><span data-stu-id="5e460-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="5e460-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span><span class="sxs-lookup"><span data-stu-id="5e460-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="5e460-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span><span class="sxs-lookup"><span data-stu-id="5e460-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="5e460-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="5e460-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="5e460-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="5e460-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="5e460-109">Authenticate the webhook</span><span class="sxs-lookup"><span data-stu-id="5e460-109">Authenticate the webhook</span></span>
<span data-ttu-id="5e460-110">The webhook can optionally use token-based authorization for authentication.</span><span class="sxs-lookup"><span data-stu-id="5e460-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="5e460-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="5e460-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="5e460-112">Payload schema</span><span class="sxs-lookup"><span data-stu-id="5e460-112">Payload schema</span></span>
<span data-ttu-id="5e460-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span><span class="sxs-lookup"><span data-stu-id="5e460-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

### <a name="common"></a><span data-ttu-id="5e460-114">Common</span><span class="sxs-lookup"><span data-stu-id="5e460-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
### <a name="administrative"></a><span data-ttu-id="5e460-115">Administrative</span><span class="sxs-lookup"><span data-stu-id="5e460-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
### <a name="servicehealth"></a><span data-ttu-id="5e460-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="5e460-116">ServiceHealth</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
    "status": "Activated",
    "context": {
        "activityLog": {
        "channels": "Admin",
        "correlationId": "bbac944f-ddc0-4b4c-aa85-cc7dc5d5c1a6",
        "description": "Active: Virtual Machines - Australia East",
        "eventSource": "ServiceHealth",
        "eventTimestamp": "2017-10-18T23:49:25.3736084+00:00",
        "eventDataId": "6fa98c0f-334a-b066-1934-1a4b3d929856",
        "level": "Informational",
        "operationName": "Microsoft.ServiceHealth/incident/action",
        "operationId": "bbac944f-ddc0-4b4c-aa85-cc7dc5d5c1a6",
        "properties": {
            "title": "Virtual Machines - Australia East",
            "service": "Virtual Machines",
            "region": "Australia East",
            "communication": "Starting at 02:48 UTC on 18 Oct 2017 you have been identified as a customer using Virtual Machines in Australia East who may receive errors starting Dv2 Promo and DSv2 Promo Virtual Machines which are in a stopped &quot;deallocated&quot; or suspended state. Customers can still provision Dv1 and Dv2 series Virtual Machines or try deploying Virtual Machines in other regions, as a possible workaround. Engineers have identified a possible fix for the underlying cause, and are exploring implementation options. The next update will be provided as events warrant.",
            "incidentType": "Incident",
            "trackingId": "0NIH-U2O",
            "impactStartTime": "2017-10-18T02:48:00.0000000Z",
            "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"Australia East\"}],\"ServiceName\":\"Virtual Machines\"}]",
            "defaultLanguageTitle": "Virtual Machines - Australia East",
            "defaultLanguageContent": "Starting at 02:48 UTC on 18 Oct 2017 you have been identified as a customer using Virtual Machines in Australia East who may receive errors starting Dv2 Promo and DSv2 Promo Virtual Machines which are in a stopped &quot;deallocated&quot; or suspended state. Customers can still provision Dv1 and Dv2 series Virtual Machines or try deploying Virtual Machines in other regions, as a possible workaround. Engineers have identified a possible fix for the underlying cause, and are exploring implementation options. The next update will be provided as events warrant.",
            "stage": "Active",
            "communicationId": "636439673646212912",
            "version": "0.1.1"
        },
        "status": "Active",
        "subscriptionId": "45529734-0ed9-4895-a0df-44b59a5a07f9",
        "submissionTimestamp": "2017-10-18T23:49:28.7864349+00:00"
        }
    },
    "properties": {}
    }
}
```

<span data-ttu-id="5e460-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="5e460-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span> <span data-ttu-id="5e460-118">Additionally, learn how to [configure service health webhook notifications with your existing problem management solutions](../service-health/service-health-alert-webhook-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5e460-118">Additionally, learn how to [configure service health webhook notifications with your existing problem management solutions](../service-health/service-health-alert-webhook-guide.md).</span></span>

<span data-ttu-id="5e460-119">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="5e460-119">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="5e460-120">Element name</span><span class="sxs-lookup"><span data-stu-id="5e460-120">Element name</span></span> | <span data-ttu-id="5e460-121">Description</span><span class="sxs-lookup"><span data-stu-id="5e460-121">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5e460-122">status</span><span class="sxs-lookup"><span data-stu-id="5e460-122">status</span></span> |<span data-ttu-id="5e460-123">Used for metric alerts.</span><span class="sxs-lookup"><span data-stu-id="5e460-123">Used for metric alerts.</span></span> <span data-ttu-id="5e460-124">Always set to "activated" for activity log alerts.</span><span class="sxs-lookup"><span data-stu-id="5e460-124">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="5e460-125">context</span><span class="sxs-lookup"><span data-stu-id="5e460-125">context</span></span> |<span data-ttu-id="5e460-126">Context of the event.</span><span class="sxs-lookup"><span data-stu-id="5e460-126">Context of the event.</span></span> |
| <span data-ttu-id="5e460-127">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="5e460-127">resourceProviderName</span></span> |<span data-ttu-id="5e460-128">The resource provider of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="5e460-128">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="5e460-129">conditionType</span><span class="sxs-lookup"><span data-stu-id="5e460-129">conditionType</span></span> |<span data-ttu-id="5e460-130">Always "Event."</span><span class="sxs-lookup"><span data-stu-id="5e460-130">Always "Event."</span></span> |
| <span data-ttu-id="5e460-131">name</span><span class="sxs-lookup"><span data-stu-id="5e460-131">name</span></span> |<span data-ttu-id="5e460-132">Name of the alert rule.</span><span class="sxs-lookup"><span data-stu-id="5e460-132">Name of the alert rule.</span></span> |
| <span data-ttu-id="5e460-133">id</span><span class="sxs-lookup"><span data-stu-id="5e460-133">id</span></span> |<span data-ttu-id="5e460-134">Resource ID of the alert.</span><span class="sxs-lookup"><span data-stu-id="5e460-134">Resource ID of the alert.</span></span> |
| <span data-ttu-id="5e460-135">description</span><span class="sxs-lookup"><span data-stu-id="5e460-135">description</span></span> |<span data-ttu-id="5e460-136">Alert description set when the alert is created.</span><span class="sxs-lookup"><span data-stu-id="5e460-136">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="5e460-137">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="5e460-137">subscriptionId</span></span> |<span data-ttu-id="5e460-138">Azure subscription ID.</span><span class="sxs-lookup"><span data-stu-id="5e460-138">Azure subscription ID.</span></span> |
| <span data-ttu-id="5e460-139">timestamp</span><span class="sxs-lookup"><span data-stu-id="5e460-139">timestamp</span></span> |<span data-ttu-id="5e460-140">Time at which the event was generated by the Azure service that processed the request.</span><span class="sxs-lookup"><span data-stu-id="5e460-140">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="5e460-141">resourceId</span><span class="sxs-lookup"><span data-stu-id="5e460-141">resourceId</span></span> |<span data-ttu-id="5e460-142">Resource ID of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="5e460-142">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="5e460-143">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5e460-143">resourceGroupName</span></span> |<span data-ttu-id="5e460-144">Name of the resource group for the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="5e460-144">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="5e460-145">properties</span><span class="sxs-lookup"><span data-stu-id="5e460-145">properties</span></span> |<span data-ttu-id="5e460-146">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span><span class="sxs-lookup"><span data-stu-id="5e460-146">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="5e460-147">event</span><span class="sxs-lookup"><span data-stu-id="5e460-147">event</span></span> |<span data-ttu-id="5e460-148">Element that contains metadata about the event.</span><span class="sxs-lookup"><span data-stu-id="5e460-148">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="5e460-149">authorization</span><span class="sxs-lookup"><span data-stu-id="5e460-149">authorization</span></span> |<span data-ttu-id="5e460-150">The Role-Based Access Control properties of the event.</span><span class="sxs-lookup"><span data-stu-id="5e460-150">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="5e460-151">These properties usually include the action, the role, and the scope.</span><span class="sxs-lookup"><span data-stu-id="5e460-151">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="5e460-152">category</span><span class="sxs-lookup"><span data-stu-id="5e460-152">category</span></span> |<span data-ttu-id="5e460-153">Category of the event.</span><span class="sxs-lookup"><span data-stu-id="5e460-153">Category of the event.</span></span> <span data-ttu-id="5e460-154">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span><span class="sxs-lookup"><span data-stu-id="5e460-154">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="5e460-155">caller</span><span class="sxs-lookup"><span data-stu-id="5e460-155">caller</span></span> |<span data-ttu-id="5e460-156">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span><span class="sxs-lookup"><span data-stu-id="5e460-156">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="5e460-157">Can be null for certain system calls.</span><span class="sxs-lookup"><span data-stu-id="5e460-157">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="5e460-158">correlationId</span><span class="sxs-lookup"><span data-stu-id="5e460-158">correlationId</span></span> |<span data-ttu-id="5e460-159">Usually a GUID in string format.</span><span class="sxs-lookup"><span data-stu-id="5e460-159">Usually a GUID in string format.</span></span> <span data-ttu-id="5e460-160">Events with correlationId belong to the same larger action and usually share a correlationId.</span><span class="sxs-lookup"><span data-stu-id="5e460-160">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="5e460-161">eventDescription</span><span class="sxs-lookup"><span data-stu-id="5e460-161">eventDescription</span></span> |<span data-ttu-id="5e460-162">Static text description of the event.</span><span class="sxs-lookup"><span data-stu-id="5e460-162">Static text description of the event.</span></span> |
| <span data-ttu-id="5e460-163">eventDataId</span><span class="sxs-lookup"><span data-stu-id="5e460-163">eventDataId</span></span> |<span data-ttu-id="5e460-164">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="5e460-164">Unique identifier for the event.</span></span> |
| <span data-ttu-id="5e460-165">eventSource</span><span class="sxs-lookup"><span data-stu-id="5e460-165">eventSource</span></span> |<span data-ttu-id="5e460-166">Name of the Azure service or infrastructure that generated the event.</span><span class="sxs-lookup"><span data-stu-id="5e460-166">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="5e460-167">httpRequest</span><span class="sxs-lookup"><span data-stu-id="5e460-167">httpRequest</span></span> |<span data-ttu-id="5e460-168">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span><span class="sxs-lookup"><span data-stu-id="5e460-168">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="5e460-169">level</span><span class="sxs-lookup"><span data-stu-id="5e460-169">level</span></span> |<span data-ttu-id="5e460-170">One of the following values: Critical, Error, Warning and Informational.</span><span class="sxs-lookup"><span data-stu-id="5e460-170">One of the following values: Critical, Error, Warning and Informational.</span></span> |
| <span data-ttu-id="5e460-171">operationId</span><span class="sxs-lookup"><span data-stu-id="5e460-171">operationId</span></span> |<span data-ttu-id="5e460-172">Usually a GUID shared among the events corresponding to single operation.</span><span class="sxs-lookup"><span data-stu-id="5e460-172">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="5e460-173">operationName</span><span class="sxs-lookup"><span data-stu-id="5e460-173">operationName</span></span> |<span data-ttu-id="5e460-174">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="5e460-174">Name of the operation.</span></span> |
| <span data-ttu-id="5e460-175">properties</span><span class="sxs-lookup"><span data-stu-id="5e460-175">properties</span></span> |<span data-ttu-id="5e460-176">Properties of the event.</span><span class="sxs-lookup"><span data-stu-id="5e460-176">Properties of the event.</span></span> |
| <span data-ttu-id="5e460-177">status</span><span class="sxs-lookup"><span data-stu-id="5e460-177">status</span></span> |<span data-ttu-id="5e460-178">String.</span><span class="sxs-lookup"><span data-stu-id="5e460-178">String.</span></span> <span data-ttu-id="5e460-179">Status of the operation.</span><span class="sxs-lookup"><span data-stu-id="5e460-179">Status of the operation.</span></span> <span data-ttu-id="5e460-180">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span><span class="sxs-lookup"><span data-stu-id="5e460-180">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="5e460-181">subStatus</span><span class="sxs-lookup"><span data-stu-id="5e460-181">subStatus</span></span> |<span data-ttu-id="5e460-182">Usually includes the HTTP status code of the corresponding REST call.</span><span class="sxs-lookup"><span data-stu-id="5e460-182">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="5e460-183">It might also include other strings that describe a substatus.</span><span class="sxs-lookup"><span data-stu-id="5e460-183">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="5e460-184">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span><span class="sxs-lookup"><span data-stu-id="5e460-184">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e460-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e460-185">Next steps</span></span>
* <span data-ttu-id="5e460-186">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="5e460-186">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="5e460-187">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="5e460-187">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="5e460-188">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5e460-188">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="5e460-189">This example is for metric alerts, but it can be modified to work with an activity log alert.</span><span class="sxs-lookup"><span data-stu-id="5e460-189">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="5e460-190">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5e460-190">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="5e460-191">This example is for metric alerts, but it can be modified to work with an activity log alert.</span><span class="sxs-lookup"><span data-stu-id="5e460-191">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="5e460-192">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5e460-192">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="5e460-193">This example is for metric alerts, but it can be modified to work with an activity log alert.</span><span class="sxs-lookup"><span data-stu-id="5e460-193">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
