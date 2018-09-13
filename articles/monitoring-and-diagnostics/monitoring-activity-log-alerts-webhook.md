# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="bfda3-101">Webhooks for Azure Activity Log alerts</span><span class="sxs-lookup"><span data-stu-id="bfda3-101">Webhooks for Azure Activity Log alerts</span></span>
<span data-ttu-id="bfda3-102">As part of the definition of an Action Group you are able to configure Webhook endpoints to receive Activity Log Alerts notifications.</span><span class="sxs-lookup"><span data-stu-id="bfda3-102">As part of the definition of an Action Group you are able to configure Webhook endpoints to receive Activity Log Alerts notifications.</span></span> <span data-ttu-id="bfda3-103">Webhooks allow you to route these notifications to other systems for post-processing or custom actions.</span><span class="sxs-lookup"><span data-stu-id="bfda3-103">Webhooks allow you to route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="bfda3-104">This article shows what the payload for the HTTP POST to a webhook looks like.</span><span class="sxs-lookup"><span data-stu-id="bfda3-104">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="bfda3-105">For information on the setup and schema for Azure Activity Log alerts, [see this page instead](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="bfda3-105">For information on the setup and schema for Azure Activity Log alerts, [see this page instead](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="bfda3-106">For information on the setup and schema for Action Groups, [see this page instead](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="bfda3-106">For information on the setup and schema for Action Groups, [see this page instead](monitoring-action-groups.md)</span></span>

## <a name="authenticating-the-webhook"></a><span data-ttu-id="bfda3-107">Authenticating the webhook</span><span class="sxs-lookup"><span data-stu-id="bfda3-107">Authenticating the webhook</span></span>
<span data-ttu-id="bfda3-108">The webhook can authenticate using token-based authorization - The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="bfda3-108">The webhook can authenticate using token-based authorization - The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="bfda3-109">Payload schema</span><span class="sxs-lookup"><span data-stu-id="bfda3-109">Payload schema</span></span>
<span data-ttu-id="bfda3-110">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span><span class="sxs-lookup"><span data-stu-id="bfda3-110">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="bfda3-111">Common</span><span class="sxs-lookup"><span data-stu-id="bfda3-111">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="bfda3-112">Administrative</span><span class="sxs-lookup"><span data-stu-id="bfda3-112">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="bfda3-113">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="bfda3-113">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                },
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="bfda3-114">For specific schema details on Service Health Notification activity log alerts [click here](monitoring-service-notifications.md) For specific schema details on all other Activity Log alerts [click here](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="bfda3-114">For specific schema details on Service Health Notification activity log alerts [click here](monitoring-service-notifications.md) For specific schema details on all other Activity Log alerts [click here](monitoring-overview-activity-logs.md)</span></span>

| <span data-ttu-id="bfda3-115">Element Name</span><span class="sxs-lookup"><span data-stu-id="bfda3-115">Element Name</span></span> | <span data-ttu-id="bfda3-116">Description</span><span class="sxs-lookup"><span data-stu-id="bfda3-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bfda3-117">status</span><span class="sxs-lookup"><span data-stu-id="bfda3-117">status</span></span> |<span data-ttu-id="bfda3-118">Used for metric alerts.</span><span class="sxs-lookup"><span data-stu-id="bfda3-118">Used for metric alerts.</span></span> <span data-ttu-id="bfda3-119">Always set to "activated" for Activity Log alerts.</span><span class="sxs-lookup"><span data-stu-id="bfda3-119">Always set to "activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="bfda3-120">context</span><span class="sxs-lookup"><span data-stu-id="bfda3-120">context</span></span> |<span data-ttu-id="bfda3-121">Context of the event.</span><span class="sxs-lookup"><span data-stu-id="bfda3-121">Context of the event.</span></span> |
| <span data-ttu-id="bfda3-122">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="bfda3-122">resourceProviderName</span></span> |<span data-ttu-id="bfda3-123">The resource provider of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="bfda3-123">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="bfda3-124">conditionType</span><span class="sxs-lookup"><span data-stu-id="bfda3-124">conditionType</span></span> |<span data-ttu-id="bfda3-125">Always "Event."</span><span class="sxs-lookup"><span data-stu-id="bfda3-125">Always "Event."</span></span> |
| <span data-ttu-id="bfda3-126">name</span><span class="sxs-lookup"><span data-stu-id="bfda3-126">name</span></span> |<span data-ttu-id="bfda3-127">Name of the alert rule.</span><span class="sxs-lookup"><span data-stu-id="bfda3-127">Name of the alert rule.</span></span> |
| <span data-ttu-id="bfda3-128">id</span><span class="sxs-lookup"><span data-stu-id="bfda3-128">id</span></span> |<span data-ttu-id="bfda3-129">Resource ID of the alert.</span><span class="sxs-lookup"><span data-stu-id="bfda3-129">Resource ID of the alert.</span></span> |
| <span data-ttu-id="bfda3-130">description</span><span class="sxs-lookup"><span data-stu-id="bfda3-130">description</span></span> |<span data-ttu-id="bfda3-131">Alert description as set during creation of the alert.</span><span class="sxs-lookup"><span data-stu-id="bfda3-131">Alert description as set during creation of the alert.</span></span> |
| <span data-ttu-id="bfda3-132">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="bfda3-132">subscriptionId</span></span> |<span data-ttu-id="bfda3-133">Azure Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="bfda3-133">Azure Subscription ID.</span></span> |
| <span data-ttu-id="bfda3-134">timestamp</span><span class="sxs-lookup"><span data-stu-id="bfda3-134">timestamp</span></span> |<span data-ttu-id="bfda3-135">Time at which the event was generated by the Azure service that processed the request.</span><span class="sxs-lookup"><span data-stu-id="bfda3-135">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="bfda3-136">resourceId</span><span class="sxs-lookup"><span data-stu-id="bfda3-136">resourceId</span></span> |<span data-ttu-id="bfda3-137">Resource ID of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="bfda3-137">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="bfda3-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="bfda3-138">resourceGroupName</span></span> |<span data-ttu-id="bfda3-139">Name of the resource group for the impacted resource</span><span class="sxs-lookup"><span data-stu-id="bfda3-139">Name of the resource group for the impacted resource</span></span> |
| <span data-ttu-id="bfda3-140">properties</span><span class="sxs-lookup"><span data-stu-id="bfda3-140">properties</span></span> |<span data-ttu-id="bfda3-141">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span><span class="sxs-lookup"><span data-stu-id="bfda3-141">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="bfda3-142">event</span><span class="sxs-lookup"><span data-stu-id="bfda3-142">event</span></span> |<span data-ttu-id="bfda3-143">Element containing metadata about the event.</span><span class="sxs-lookup"><span data-stu-id="bfda3-143">Element containing metadata about the event.</span></span> |
| <span data-ttu-id="bfda3-144">authorization</span><span class="sxs-lookup"><span data-stu-id="bfda3-144">authorization</span></span> |<span data-ttu-id="bfda3-145">The RBAC properties of the event.</span><span class="sxs-lookup"><span data-stu-id="bfda3-145">The RBAC properties of the event.</span></span> <span data-ttu-id="bfda3-146">These properties usually include the “action”, “role” and the “scope.”</span><span class="sxs-lookup"><span data-stu-id="bfda3-146">These properties usually include the “action”, “role” and the “scope.”</span></span> |
| <span data-ttu-id="bfda3-147">category</span><span class="sxs-lookup"><span data-stu-id="bfda3-147">category</span></span> |<span data-ttu-id="bfda3-148">Category of the event.</span><span class="sxs-lookup"><span data-stu-id="bfda3-148">Category of the event.</span></span> <span data-ttu-id="bfda3-149">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span><span class="sxs-lookup"><span data-stu-id="bfda3-149">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="bfda3-150">caller</span><span class="sxs-lookup"><span data-stu-id="bfda3-150">caller</span></span> |<span data-ttu-id="bfda3-151">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span><span class="sxs-lookup"><span data-stu-id="bfda3-151">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="bfda3-152">Can be null for certain system calls.</span><span class="sxs-lookup"><span data-stu-id="bfda3-152">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="bfda3-153">correlationId</span><span class="sxs-lookup"><span data-stu-id="bfda3-153">correlationId</span></span> |<span data-ttu-id="bfda3-154">Usually a GUID in string format.</span><span class="sxs-lookup"><span data-stu-id="bfda3-154">Usually a GUID in string format.</span></span> <span data-ttu-id="bfda3-155">Events with correlationId belong to the same larger action and usually share a correlationId.</span><span class="sxs-lookup"><span data-stu-id="bfda3-155">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="bfda3-156">eventDescription</span><span class="sxs-lookup"><span data-stu-id="bfda3-156">eventDescription</span></span> |<span data-ttu-id="bfda3-157">Static text description of the event.</span><span class="sxs-lookup"><span data-stu-id="bfda3-157">Static text description of the event.</span></span> |
| <span data-ttu-id="bfda3-158">eventDataId</span><span class="sxs-lookup"><span data-stu-id="bfda3-158">eventDataId</span></span> |<span data-ttu-id="bfda3-159">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="bfda3-159">Unique identifier for the event.</span></span> |
| <span data-ttu-id="bfda3-160">eventSource</span><span class="sxs-lookup"><span data-stu-id="bfda3-160">eventSource</span></span> |<span data-ttu-id="bfda3-161">Name of the Azure service or infrastructure that generated the event.</span><span class="sxs-lookup"><span data-stu-id="bfda3-161">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="bfda3-162">httpRequest</span><span class="sxs-lookup"><span data-stu-id="bfda3-162">httpRequest</span></span> |<span data-ttu-id="bfda3-163">The request usually includes the “clientRequestId”, “clientIpAddress” and HTTP “method” (for example, PUT).</span><span class="sxs-lookup"><span data-stu-id="bfda3-163">The request usually includes the “clientRequestId”, “clientIpAddress” and HTTP “method” (for example, PUT).</span></span> |
| <span data-ttu-id="bfda3-164">level</span><span class="sxs-lookup"><span data-stu-id="bfda3-164">level</span></span> |<span data-ttu-id="bfda3-165">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span><span class="sxs-lookup"><span data-stu-id="bfda3-165">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="bfda3-166">operationId</span><span class="sxs-lookup"><span data-stu-id="bfda3-166">operationId</span></span> |<span data-ttu-id="bfda3-167">Usually a GUID shared among the events corresponding to single operation.</span><span class="sxs-lookup"><span data-stu-id="bfda3-167">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="bfda3-168">operationName</span><span class="sxs-lookup"><span data-stu-id="bfda3-168">operationName</span></span> |<span data-ttu-id="bfda3-169">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="bfda3-169">Name of the operation.</span></span> |
| <span data-ttu-id="bfda3-170">properties</span><span class="sxs-lookup"><span data-stu-id="bfda3-170">properties</span></span> |<span data-ttu-id="bfda3-171">Properties of the event.</span><span class="sxs-lookup"><span data-stu-id="bfda3-171">Properties of the event.</span></span> |
| <span data-ttu-id="bfda3-172">status</span><span class="sxs-lookup"><span data-stu-id="bfda3-172">status</span></span> |<span data-ttu-id="bfda3-173">String.</span><span class="sxs-lookup"><span data-stu-id="bfda3-173">String.</span></span> <span data-ttu-id="bfda3-174">Status of the operation.</span><span class="sxs-lookup"><span data-stu-id="bfda3-174">Status of the operation.</span></span> <span data-ttu-id="bfda3-175">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span><span class="sxs-lookup"><span data-stu-id="bfda3-175">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="bfda3-176">subStatus</span><span class="sxs-lookup"><span data-stu-id="bfda3-176">subStatus</span></span> |<span data-ttu-id="bfda3-177">Usually includes the HTTP status code of the corresponding REST call.</span><span class="sxs-lookup"><span data-stu-id="bfda3-177">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="bfda3-178">It might also include other strings describing a substatus.</span><span class="sxs-lookup"><span data-stu-id="bfda3-178">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="bfda3-179">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span><span class="sxs-lookup"><span data-stu-id="bfda3-179">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bfda3-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfda3-180">Next steps</span></span>
* [<span data-ttu-id="bfda3-181">Learn more about the Activity Log</span><span class="sxs-lookup"><span data-stu-id="bfda3-181">Learn more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="bfda3-182">Execute Azure Automation scripts (Runbooks) on Azure alerts</span><span class="sxs-lookup"><span data-stu-id="bfda3-182">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="bfda3-183">[Use Logic App to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="bfda3-183">[Use Logic App to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="bfda3-184">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span><span class="sxs-lookup"><span data-stu-id="bfda3-184">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="bfda3-185">[Use Logic App to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="bfda3-185">[Use Logic App to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="bfda3-186">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span><span class="sxs-lookup"><span data-stu-id="bfda3-186">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="bfda3-187">[Use Logic App to send a message to an Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="bfda3-187">[Use Logic App to send a message to an Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="bfda3-188">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span><span class="sxs-lookup"><span data-stu-id="bfda3-188">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
