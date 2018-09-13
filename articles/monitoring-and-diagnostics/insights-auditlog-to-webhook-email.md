---
title: Call a webhook on Azure Activity Log alerts | Microsoft Docs
description: Route Activity log events to other services for custom actions. For example send SMS, log bugs, or notify a team via chat/messaging service.
author: kamathashwin
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: ashwink
ms.openlocfilehash: 4ee65a10616fff81044c181fce8708a596e9e6de
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549668"
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="0048d-104">Call a webhook on Azure Activity Log alerts</span><span class="sxs-lookup"><span data-stu-id="0048d-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="0048d-105">Webhooks allow you to route an Azure alert notification to other systems for post-processing or custom actions.</span><span class="sxs-lookup"><span data-stu-id="0048d-105">Webhooks allow you to route an Azure alert notification to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="0048d-106">You can use a webhook on an alert to route it to services that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span><span class="sxs-lookup"><span data-stu-id="0048d-106">You can use a webhook on an alert to route it to services that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="0048d-107">This article describes how to set a webhook to be called when an Azure Activity Log alert fires.</span><span class="sxs-lookup"><span data-stu-id="0048d-107">This article describes how to set a webhook to be called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="0048d-108">It also shows what the payload for the HTTP POST to a webhook looks like.</span><span class="sxs-lookup"><span data-stu-id="0048d-108">It also shows what the payload for the HTTP POST to a webhook looks like.</span></span> <span data-ttu-id="0048d-109">For information on the setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0048d-109">For information on the setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="0048d-110">You can also set up an Activity Log alert to send email when activated.</span><span class="sxs-lookup"><span data-stu-id="0048d-110">You can also set up an Activity Log alert to send email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="0048d-111">This feature is currently in preview and will be removed at some point in the future.</span><span class="sxs-lookup"><span data-stu-id="0048d-111">This feature is currently in preview and will be removed at some point in the future.</span></span>
>
>

<span data-ttu-id="0048d-112">You can set up an Activity Log alert using the [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-alert-rules), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="0048d-112">You can set up an Activity Log alert using the [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-alert-rules), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="0048d-113">Currently, you cannot set one up using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0048d-113">Currently, you cannot set one up using the Azure portal.</span></span>

## <a name="authenticating-the-webhook"></a><span data-ttu-id="0048d-114">Authenticating the webhook</span><span class="sxs-lookup"><span data-stu-id="0048d-114">Authenticating the webhook</span></span>
<span data-ttu-id="0048d-115">The webhook can authenticate using either of these methods:</span><span class="sxs-lookup"><span data-stu-id="0048d-115">The webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="0048d-116">**Token-based authorization** - The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="0048d-116">**Token-based authorization** - The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="0048d-117">**Basic authorization** - The webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="0048d-117">**Basic authorization** - The webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="0048d-118">Payload schema</span><span class="sxs-lookup"><span data-stu-id="0048d-118">Payload schema</span></span>
<span data-ttu-id="0048d-119">The POST operation contains the following JSON payload and schema for all Activity Log-based alerts.</span><span class="sxs-lookup"><span data-stu-id="0048d-119">The POST operation contains the following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="0048d-120">This schema is similar to the one used by metric-based alerts.</span><span class="sxs-lookup"><span data-stu-id="0048d-120">This schema is similar to the one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="0048d-121">Element Name</span><span class="sxs-lookup"><span data-stu-id="0048d-121">Element Name</span></span> | <span data-ttu-id="0048d-122">Description</span><span class="sxs-lookup"><span data-stu-id="0048d-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0048d-123">status</span><span class="sxs-lookup"><span data-stu-id="0048d-123">status</span></span> |<span data-ttu-id="0048d-124">Used for metric alerts.</span><span class="sxs-lookup"><span data-stu-id="0048d-124">Used for metric alerts.</span></span> <span data-ttu-id="0048d-125">Always set to "activated" for Activity Log alerts.</span><span class="sxs-lookup"><span data-stu-id="0048d-125">Always set to "activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="0048d-126">context</span><span class="sxs-lookup"><span data-stu-id="0048d-126">context</span></span> |<span data-ttu-id="0048d-127">Context of the event.</span><span class="sxs-lookup"><span data-stu-id="0048d-127">Context of the event.</span></span> |
| <span data-ttu-id="0048d-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="0048d-128">resourceProviderName</span></span> |<span data-ttu-id="0048d-129">The resource provider of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="0048d-129">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="0048d-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="0048d-130">conditionType</span></span> |<span data-ttu-id="0048d-131">Always "Event."</span><span class="sxs-lookup"><span data-stu-id="0048d-131">Always "Event."</span></span> |
| <span data-ttu-id="0048d-132">name</span><span class="sxs-lookup"><span data-stu-id="0048d-132">name</span></span> |<span data-ttu-id="0048d-133">Name of the alert rule.</span><span class="sxs-lookup"><span data-stu-id="0048d-133">Name of the alert rule.</span></span> |
| <span data-ttu-id="0048d-134">id</span><span class="sxs-lookup"><span data-stu-id="0048d-134">id</span></span> |<span data-ttu-id="0048d-135">Resource ID of the alert.</span><span class="sxs-lookup"><span data-stu-id="0048d-135">Resource ID of the alert.</span></span> |
| <span data-ttu-id="0048d-136">description</span><span class="sxs-lookup"><span data-stu-id="0048d-136">description</span></span> |<span data-ttu-id="0048d-137">Alert description as set during creation of the alert.</span><span class="sxs-lookup"><span data-stu-id="0048d-137">Alert description as set during creation of the alert.</span></span> |
| <span data-ttu-id="0048d-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0048d-138">subscriptionId</span></span> |<span data-ttu-id="0048d-139">Azure Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="0048d-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="0048d-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="0048d-140">timestamp</span></span> |<span data-ttu-id="0048d-141">Time at which the event was generated by the Azure service that processed the request.</span><span class="sxs-lookup"><span data-stu-id="0048d-141">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="0048d-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="0048d-142">resourceId</span></span> |<span data-ttu-id="0048d-143">Resource ID of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="0048d-143">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="0048d-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="0048d-144">resourceGroupName</span></span> |<span data-ttu-id="0048d-145">Name of the resource group for the impacted resource</span><span class="sxs-lookup"><span data-stu-id="0048d-145">Name of the resource group for the impacted resource</span></span> |
| <span data-ttu-id="0048d-146">properties</span><span class="sxs-lookup"><span data-stu-id="0048d-146">properties</span></span> |<span data-ttu-id="0048d-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about the event.</span><span class="sxs-lookup"><span data-stu-id="0048d-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="0048d-148">event</span><span class="sxs-lookup"><span data-stu-id="0048d-148">event</span></span> |<span data-ttu-id="0048d-149">Element containing metadata about the event.</span><span class="sxs-lookup"><span data-stu-id="0048d-149">Element containing metadata about the event.</span></span> |
| <span data-ttu-id="0048d-150">authorization</span><span class="sxs-lookup"><span data-stu-id="0048d-150">authorization</span></span> |<span data-ttu-id="0048d-151">The RBAC properties of the event.</span><span class="sxs-lookup"><span data-stu-id="0048d-151">The RBAC properties of the event.</span></span> <span data-ttu-id="0048d-152">These usually include the “action”, “role” and the “scope.”</span><span class="sxs-lookup"><span data-stu-id="0048d-152">These usually include the “action”, “role” and the “scope.”</span></span> |
| <span data-ttu-id="0048d-153">category</span><span class="sxs-lookup"><span data-stu-id="0048d-153">category</span></span> |<span data-ttu-id="0048d-154">Category of the event.</span><span class="sxs-lookup"><span data-stu-id="0048d-154">Category of the event.</span></span> <span data-ttu-id="0048d-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span><span class="sxs-lookup"><span data-stu-id="0048d-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="0048d-156">caller</span><span class="sxs-lookup"><span data-stu-id="0048d-156">caller</span></span> |<span data-ttu-id="0048d-157">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span><span class="sxs-lookup"><span data-stu-id="0048d-157">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="0048d-158">Can be null for certain system calls.</span><span class="sxs-lookup"><span data-stu-id="0048d-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="0048d-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="0048d-159">correlationId</span></span> |<span data-ttu-id="0048d-160">Usually a GUID in string format.</span><span class="sxs-lookup"><span data-stu-id="0048d-160">Usually a GUID in string format.</span></span> <span data-ttu-id="0048d-161">Events with correlationId belong to the same larger action and usually share a correlationId.</span><span class="sxs-lookup"><span data-stu-id="0048d-161">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="0048d-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="0048d-162">eventDescription</span></span> |<span data-ttu-id="0048d-163">Static text description of the event.</span><span class="sxs-lookup"><span data-stu-id="0048d-163">Static text description of the event.</span></span> |
| <span data-ttu-id="0048d-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="0048d-164">eventDataId</span></span> |<span data-ttu-id="0048d-165">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="0048d-165">Unique identifier for the event.</span></span> |
| <span data-ttu-id="0048d-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="0048d-166">eventSource</span></span> |<span data-ttu-id="0048d-167">Name of the Azure service or infrastructure that generated the event.</span><span class="sxs-lookup"><span data-stu-id="0048d-167">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="0048d-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="0048d-168">httpRequest</span></span> |<span data-ttu-id="0048d-169">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span><span class="sxs-lookup"><span data-stu-id="0048d-169">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="0048d-170">level</span><span class="sxs-lookup"><span data-stu-id="0048d-170">level</span></span> |<span data-ttu-id="0048d-171">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span><span class="sxs-lookup"><span data-stu-id="0048d-171">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="0048d-172">operationId</span><span class="sxs-lookup"><span data-stu-id="0048d-172">operationId</span></span> |<span data-ttu-id="0048d-173">Usually a GUID shared among the events corresponding to single operation.</span><span class="sxs-lookup"><span data-stu-id="0048d-173">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="0048d-174">operationName</span><span class="sxs-lookup"><span data-stu-id="0048d-174">operationName</span></span> |<span data-ttu-id="0048d-175">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="0048d-175">Name of the operation.</span></span> |
| <span data-ttu-id="0048d-176">properties</span><span class="sxs-lookup"><span data-stu-id="0048d-176">properties</span></span> |<span data-ttu-id="0048d-177">Properties of the event.</span><span class="sxs-lookup"><span data-stu-id="0048d-177">Properties of the event.</span></span> |
| <span data-ttu-id="0048d-178">status</span><span class="sxs-lookup"><span data-stu-id="0048d-178">status</span></span> |<span data-ttu-id="0048d-179">String.</span><span class="sxs-lookup"><span data-stu-id="0048d-179">String.</span></span> <span data-ttu-id="0048d-180">Status of the operation.</span><span class="sxs-lookup"><span data-stu-id="0048d-180">Status of the operation.</span></span> <span data-ttu-id="0048d-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span><span class="sxs-lookup"><span data-stu-id="0048d-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="0048d-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="0048d-182">subStatus</span></span> |<span data-ttu-id="0048d-183">Usually includes the HTTP status code of the corresponding REST call.</span><span class="sxs-lookup"><span data-stu-id="0048d-183">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="0048d-184">It might also include other strings describing a substatus.</span><span class="sxs-lookup"><span data-stu-id="0048d-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="0048d-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span><span class="sxs-lookup"><span data-stu-id="0048d-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0048d-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="0048d-186">Next steps</span></span>
* [<span data-ttu-id="0048d-187">Learn more about the Activity Log</span><span class="sxs-lookup"><span data-stu-id="0048d-187">Learn more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="0048d-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span><span class="sxs-lookup"><span data-stu-id="0048d-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="0048d-189">[Use Logic App to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="0048d-189">[Use Logic App to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="0048d-190">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span><span class="sxs-lookup"><span data-stu-id="0048d-190">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="0048d-191">[Use Logic App to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="0048d-191">[Use Logic App to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="0048d-192">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span><span class="sxs-lookup"><span data-stu-id="0048d-192">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="0048d-193">[Use Logic App to send a message to an Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="0048d-193">[Use Logic App to send a message to an Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="0048d-194">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span><span class="sxs-lookup"><span data-stu-id="0048d-194">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
