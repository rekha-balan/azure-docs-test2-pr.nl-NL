---
title: Azure Activity Log event schema
description: Understand the event schema for data emitted into the Activity Log
author: johnkemnetz
services: azure-monitor
ms.service: azure-monitor
ms.topic: reference
ms.date: 4/12/2018
ms.author: dukek
ms.component: activitylog
ms.openlocfilehash: 9c1f4699f067ece3108813d28ff834c68f44316d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870898"
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="b68d7-103">Azure Activity Log event schema</span><span class="sxs-lookup"><span data-stu-id="b68d7-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="b68d7-104">The **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span><span class="sxs-lookup"><span data-stu-id="b68d7-104">The **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="b68d7-105">This article describes the event schema per category of data.</span><span class="sxs-lookup"><span data-stu-id="b68d7-105">This article describes the event schema per category of data.</span></span> <span data-ttu-id="b68d7-106">The schema of the data differs depending on if you are reading the data in the portal, PowerShell, CLI, or directly via the REST API versus [streaming the data to storage or Event Hubs using a Log Profile](./monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="b68d7-106">The schema of the data differs depending on if you are reading the data in the portal, PowerShell, CLI, or directly via the REST API versus [streaming the data to storage or Event Hubs using a Log Profile](./monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> <span data-ttu-id="b68d7-107">The examples below show the schema as made available via the portal, PowerShell, CLI, and REST API.</span><span class="sxs-lookup"><span data-stu-id="b68d7-107">The examples below show the schema as made available via the portal, PowerShell, CLI, and REST API.</span></span> <span data-ttu-id="b68d7-108">A mapping of those properties to the [Azure diagnostic logs schema](./monitoring-diagnostic-logs-schema.md) is provided at the end of the article.</span><span class="sxs-lookup"><span data-stu-id="b68d7-108">A mapping of those properties to the [Azure diagnostic logs schema](./monitoring-diagnostic-logs-schema.md) is provided at the end of the article.</span></span>

## <a name="administrative"></a><span data-ttu-id="b68d7-109">Administrative</span><span class="sxs-lookup"><span data-stu-id="b68d7-109">Administrative</span></span>
<span data-ttu-id="b68d7-110">This category contains the record of all create, update, delete, and action operations performed through Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b68d7-110">This category contains the record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="b68d7-111">Examples of the types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span><span class="sxs-lookup"><span data-stu-id="b68d7-111">Examples of the types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="b68d7-112">If the operation type is Write, Delete, or Action, the records of both the start and success or fail of that operation are recorded in the Administrative category.</span><span class="sxs-lookup"><span data-stu-id="b68d7-112">If the operation type is Write, Delete, or Action, the records of both the start and success or fail of that operation are recorded in the Administrative category.</span></span> <span data-ttu-id="b68d7-113">The Administrative category also includes any changes to role-based access control in a subscription.</span><span class="sxs-lookup"><span data-stu-id="b68d7-113">The Administrative category also includes any changes to role-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="b68d7-114">Sample event</span><span class="sxs-lookup"><span data-stu-id="b68d7-114">Sample event</span></span>
```json
{
    "authorization": {
        "action": "Microsoft.Network/networkSecurityGroups/write",
        "scope": "/subscriptions/<subscription ID>/resourcegroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNSG"
    },
    "caller": "rob@contoso.com",
    "channels": "Operation",
    "claims": {
        "aud": "https://management.core.windows.net/",
        "iss": "https://sts.windows.net/1114444b-7467-4144-a616-e3a5d63e147b/",
        "iat": "1234567890",
        "nbf": "1234567890",
        "exp": "1234567890",
        "_claim_names": "{\"groups\":\"src1\"}",
        "_claim_sources": "{\"src1\":{\"endpoint\":\"https://graph.windows.net/1114444b-7467-4144-a616-e3a5d63e147b/users/f409edeb-4d29-44b5-9763-ee9348ad91bb/getMemberObjects\"}}",
        "http://schemas.microsoft.com/claims/authnclassreference": "1",
        "aio": "A3GgTJdwK4vy7Fa7l6DgJC2mI0GX44tML385OpU1Q+z+jaPnFMwB",
        "http://schemas.microsoft.com/claims/authnmethodsreferences": "rsa,mfa",
        "appid": "355249ed-15d9-460d-8481-84026b065942",
        "appidacr": "2",
        "http://schemas.microsoft.com/2012/01/devicecontext/claims/identifier": "10845a4d-ffa4-4b61-a3b4-e57b9b31cdb5",
        "e_exp": "262800",
        "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Robertson",
        "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "Rob",
        "ipaddr": "111.111.1.111",
        "name": "Rob Robertson",
        "http://schemas.microsoft.com/identity/claims/objectidentifier": "f409edeb-4d29-44b5-9763-ee9348ad91bb",
        "onprem_sid": "S-1-5-21-4837261184-168309720-1886587427-18514304",
        "puid": "18247BBD84827C6D",
        "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
        "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "b-24Jf94A3FH2sHWVIFqO3-RSJEiv24Jnif3gj7s",
        "http://schemas.microsoft.com/identity/claims/tenantid": "1114444b-7467-4144-a616-e3a5d63e147b",
        "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": "rob@contoso.com",
        "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "rob@contoso.com",
        "uti": "IdP3SUJGtkGlt7dDQVRPAA",
        "ver": "1.0"
    },
    "correlationId": "b5768deb-836b-41cc-803e-3f4de2f9e40b",
    "eventDataId": "d0d36f97-b29c-4cd9-9d3d-ea2b92af3e9d",
    "eventName": {
        "value": "EndRequest",
        "localizedValue": "End request"
    },
    "category": {
        "value": "Administrative",
        "localizedValue": "Administrative"
    },
    "eventTimestamp": "2018-01-29T20:42:31.3810679Z",
    "id": "/subscriptions/<subscription ID>/resourcegroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNSG/events/d0d36f97-b29c-4cd9-9d3d-ea2b92af3e9d/ticks/636528553513810679",
    "level": "Informational",
    "operationId": "04e575f8-48d0-4c43-a8b3-78c4eb01d287",
    "operationName": {
        "value": "Microsoft.Network/networkSecurityGroups/write",
        "localizedValue": "Microsoft.Network/networkSecurityGroups/write"
    },
    "resourceGroupName": "myResourceGroup",
    "resourceProviderName": {
        "value": "Microsoft.Network",
        "localizedValue": "Microsoft.Network"
    },
    "resourceType": {
        "value": "Microsoft.Network/networkSecurityGroups",
        "localizedValue": "Microsoft.Network/networkSecurityGroups"
    },
    "resourceId": "/subscriptions/<subscription ID>/resourcegroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNSG",
    "status": {
        "value": "Succeeded",
        "localizedValue": "Succeeded"
    },
    "subStatus": {
        "value": "",
        "localizedValue": ""
    },
    "submissionTimestamp": "2018-01-29T20:42:50.0724829Z",
    "subscriptionId": "<subscription ID>",
    "properties": {
        "statusCode": "Created",
        "serviceRequestId": "a4c11dbd-697e-47c5-9663-12362307157d",
        "responseBody": "",
        "requestbody": ""
    },
    "relatedEvents": []
}

```

### <a name="property-descriptions"></a><span data-ttu-id="b68d7-115">Property descriptions</span><span class="sxs-lookup"><span data-stu-id="b68d7-115">Property descriptions</span></span>
| <span data-ttu-id="b68d7-116">Element Name</span><span class="sxs-lookup"><span data-stu-id="b68d7-116">Element Name</span></span> | <span data-ttu-id="b68d7-117">Description</span><span class="sxs-lookup"><span data-stu-id="b68d7-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b68d7-118">authorization</span><span class="sxs-lookup"><span data-stu-id="b68d7-118">authorization</span></span> |<span data-ttu-id="b68d7-119">Blob of RBAC properties of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-119">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="b68d7-120">Usually includes the “action”, “role” and “scope” properties.</span><span class="sxs-lookup"><span data-stu-id="b68d7-120">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="b68d7-121">caller</span><span class="sxs-lookup"><span data-stu-id="b68d7-121">caller</span></span> |<span data-ttu-id="b68d7-122">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span><span class="sxs-lookup"><span data-stu-id="b68d7-122">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="b68d7-123">channels</span><span class="sxs-lookup"><span data-stu-id="b68d7-123">channels</span></span> |<span data-ttu-id="b68d7-124">One of the following values: “Admin”, “Operation”</span><span class="sxs-lookup"><span data-stu-id="b68d7-124">One of the following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="b68d7-125">claims</span><span class="sxs-lookup"><span data-stu-id="b68d7-125">claims</span></span> |<span data-ttu-id="b68d7-126">The JWT token used by Active Directory to authenticate the user or application to perform this operation in Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b68d7-126">The JWT token used by Active Directory to authenticate the user or application to perform this operation in Resource Manager.</span></span> |
| <span data-ttu-id="b68d7-127">correlationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-127">correlationId</span></span> |<span data-ttu-id="b68d7-128">Usually a GUID in the string format.</span><span class="sxs-lookup"><span data-stu-id="b68d7-128">Usually a GUID in the string format.</span></span> <span data-ttu-id="b68d7-129">Events that share a correlationId belong to the same uber action.</span><span class="sxs-lookup"><span data-stu-id="b68d7-129">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="b68d7-130">description</span><span class="sxs-lookup"><span data-stu-id="b68d7-130">description</span></span> |<span data-ttu-id="b68d7-131">Static text description of an event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-131">Static text description of an event.</span></span> |
| <span data-ttu-id="b68d7-132">eventDataId</span><span class="sxs-lookup"><span data-stu-id="b68d7-132">eventDataId</span></span> |<span data-ttu-id="b68d7-133">Unique identifier of an event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-133">Unique identifier of an event.</span></span> |
| <span data-ttu-id="b68d7-134">httpRequest</span><span class="sxs-lookup"><span data-stu-id="b68d7-134">httpRequest</span></span> |<span data-ttu-id="b68d7-135">Blob describing the Http Request.</span><span class="sxs-lookup"><span data-stu-id="b68d7-135">Blob describing the Http Request.</span></span> <span data-ttu-id="b68d7-136">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span><span class="sxs-lookup"><span data-stu-id="b68d7-136">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="b68d7-137">For example, PUT).</span><span class="sxs-lookup"><span data-stu-id="b68d7-137">For example, PUT).</span></span> |
| <span data-ttu-id="b68d7-138">level</span><span class="sxs-lookup"><span data-stu-id="b68d7-138">level</span></span> |<span data-ttu-id="b68d7-139">Level of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-139">Level of the event.</span></span> <span data-ttu-id="b68d7-140">One of the following values: “Critical”, “Error”, “Warning”, and “Informational”</span><span class="sxs-lookup"><span data-stu-id="b68d7-140">One of the following values: “Critical”, “Error”, “Warning”, and “Informational”</span></span> |
| <span data-ttu-id="b68d7-141">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b68d7-141">resourceGroupName</span></span> |<span data-ttu-id="b68d7-142">Name of the resource group for the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="b68d7-142">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="b68d7-143">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="b68d7-143">resourceProviderName</span></span> |<span data-ttu-id="b68d7-144">Name of the resource provider for the impacted resource</span><span class="sxs-lookup"><span data-stu-id="b68d7-144">Name of the resource provider for the impacted resource</span></span> |
| <span data-ttu-id="b68d7-145">resourceId</span><span class="sxs-lookup"><span data-stu-id="b68d7-145">resourceId</span></span> |<span data-ttu-id="b68d7-146">Resource ID of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="b68d7-146">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="b68d7-147">operationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-147">operationId</span></span> |<span data-ttu-id="b68d7-148">A GUID shared among the events that correspond to a single operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-148">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="b68d7-149">operationName</span><span class="sxs-lookup"><span data-stu-id="b68d7-149">operationName</span></span> |<span data-ttu-id="b68d7-150">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-150">Name of the operation.</span></span> |
| <span data-ttu-id="b68d7-151">properties</span><span class="sxs-lookup"><span data-stu-id="b68d7-151">properties</span></span> |<span data-ttu-id="b68d7-152">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-152">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="b68d7-153">status</span><span class="sxs-lookup"><span data-stu-id="b68d7-153">status</span></span> |<span data-ttu-id="b68d7-154">String describing the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-154">String describing the status of the operation.</span></span> <span data-ttu-id="b68d7-155">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="b68d7-155">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="b68d7-156">subStatus</span><span class="sxs-lookup"><span data-stu-id="b68d7-156">subStatus</span></span> |<span data-ttu-id="b68d7-157">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span><span class="sxs-lookup"><span data-stu-id="b68d7-157">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="b68d7-158">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-158">eventTimestamp</span></span> |<span data-ttu-id="b68d7-159">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-159">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="b68d7-160">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-160">submissionTimestamp</span></span> |<span data-ttu-id="b68d7-161">Timestamp when the event became available for querying.</span><span class="sxs-lookup"><span data-stu-id="b68d7-161">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="b68d7-162">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="b68d7-162">subscriptionId</span></span> |<span data-ttu-id="b68d7-163">Azure Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="b68d7-163">Azure Subscription ID.</span></span> |

## <a name="service-health"></a><span data-ttu-id="b68d7-164">Service health</span><span class="sxs-lookup"><span data-stu-id="b68d7-164">Service health</span></span>
<span data-ttu-id="b68d7-165">This category contains the record of any service health incidents that have occurred in Azure.</span><span class="sxs-lookup"><span data-stu-id="b68d7-165">This category contains the record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="b68d7-166">An example of the type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span><span class="sxs-lookup"><span data-stu-id="b68d7-166">An example of the type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="b68d7-167">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in the subscription that would be impacted by the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-167">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in the subscription that would be impacted by the event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="b68d7-168">Sample event</span><span class="sxs-lookup"><span data-stu-id="b68d7-168">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/<subscription ID>/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/<subscription ID>",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "<subscription ID>",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```
<span data-ttu-id="b68d7-169">Refer to the [service health notifications](./monitoring-service-notifications.md) article for documentation about the values in the properties.</span><span class="sxs-lookup"><span data-stu-id="b68d7-169">Refer to the [service health notifications](./monitoring-service-notifications.md) article for documentation about the values in the properties.</span></span>

## <a name="alert"></a><span data-ttu-id="b68d7-170">Alert</span><span class="sxs-lookup"><span data-stu-id="b68d7-170">Alert</span></span>
<span data-ttu-id="b68d7-171">This category contains the record of all activations of Azure alerts.</span><span class="sxs-lookup"><span data-stu-id="b68d7-171">This category contains the record of all activations of Azure alerts.</span></span> <span data-ttu-id="b68d7-172">An example of the type of event you would see in this category is "CPU % on myVM has been over 80 for the past 5 minutes."</span><span class="sxs-lookup"><span data-stu-id="b68d7-172">An example of the type of event you would see in this category is "CPU % on myVM has been over 80 for the past 5 minutes."</span></span> <span data-ttu-id="b68d7-173">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span><span class="sxs-lookup"><span data-stu-id="b68d7-173">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="b68d7-174">Each time a supported Azure alert type 'activates,' or the conditions are met to generate a notification, a record of the activation is also pushed to this category of the Activity Log.</span><span class="sxs-lookup"><span data-stu-id="b68d7-174">Each time a supported Azure alert type 'activates,' or the conditions are met to generate a notification, a record of the activation is also pushed to this category of the Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="b68d7-175">Sample event</span><span class="sxs-lookup"><span data-stu-id="b68d7-175">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in the last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "<subscription ID>"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="b68d7-176">Property descriptions</span><span class="sxs-lookup"><span data-stu-id="b68d7-176">Property descriptions</span></span>
| <span data-ttu-id="b68d7-177">Element Name</span><span class="sxs-lookup"><span data-stu-id="b68d7-177">Element Name</span></span> | <span data-ttu-id="b68d7-178">Description</span><span class="sxs-lookup"><span data-stu-id="b68d7-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b68d7-179">caller</span><span class="sxs-lookup"><span data-stu-id="b68d7-179">caller</span></span> | <span data-ttu-id="b68d7-180">Always Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="b68d7-180">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="b68d7-181">channels</span><span class="sxs-lookup"><span data-stu-id="b68d7-181">channels</span></span> | <span data-ttu-id="b68d7-182">Always “Admin, Operation”</span><span class="sxs-lookup"><span data-stu-id="b68d7-182">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="b68d7-183">claims</span><span class="sxs-lookup"><span data-stu-id="b68d7-183">claims</span></span> | <span data-ttu-id="b68d7-184">JSON blob with the SPN (service principal name), or resource type, of the alert engine.</span><span class="sxs-lookup"><span data-stu-id="b68d7-184">JSON blob with the SPN (service principal name), or resource type, of the alert engine.</span></span> |
| <span data-ttu-id="b68d7-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-185">correlationId</span></span> | <span data-ttu-id="b68d7-186">A GUID in the string format.</span><span class="sxs-lookup"><span data-stu-id="b68d7-186">A GUID in the string format.</span></span> |
| <span data-ttu-id="b68d7-187">description</span><span class="sxs-lookup"><span data-stu-id="b68d7-187">description</span></span> |<span data-ttu-id="b68d7-188">Static text description of the alert event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-188">Static text description of the alert event.</span></span> |
| <span data-ttu-id="b68d7-189">eventDataId</span><span class="sxs-lookup"><span data-stu-id="b68d7-189">eventDataId</span></span> |<span data-ttu-id="b68d7-190">Unique identifier of the alert event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-190">Unique identifier of the alert event.</span></span> |
| <span data-ttu-id="b68d7-191">level</span><span class="sxs-lookup"><span data-stu-id="b68d7-191">level</span></span> |<span data-ttu-id="b68d7-192">Level of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-192">Level of the event.</span></span> <span data-ttu-id="b68d7-193">One of the following values: “Critical”, “Error”, “Warning”, and “Informational”</span><span class="sxs-lookup"><span data-stu-id="b68d7-193">One of the following values: “Critical”, “Error”, “Warning”, and “Informational”</span></span> |
| <span data-ttu-id="b68d7-194">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b68d7-194">resourceGroupName</span></span> |<span data-ttu-id="b68d7-195">Name of the resource group for the impacted resource if it is a metric alert.</span><span class="sxs-lookup"><span data-stu-id="b68d7-195">Name of the resource group for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="b68d7-196">For other alert types, this is the name of the resource group that contains the alert itself.</span><span class="sxs-lookup"><span data-stu-id="b68d7-196">For other alert types, this is the name of the resource group that contains the alert itself.</span></span> |
| <span data-ttu-id="b68d7-197">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="b68d7-197">resourceProviderName</span></span> |<span data-ttu-id="b68d7-198">Name of the resource provider for the impacted resource if it is a metric alert.</span><span class="sxs-lookup"><span data-stu-id="b68d7-198">Name of the resource provider for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="b68d7-199">For other alert types, this is the name of the resource provider for the alert itself.</span><span class="sxs-lookup"><span data-stu-id="b68d7-199">For other alert types, this is the name of the resource provider for the alert itself.</span></span> |
| <span data-ttu-id="b68d7-200">resourceId</span><span class="sxs-lookup"><span data-stu-id="b68d7-200">resourceId</span></span> | <span data-ttu-id="b68d7-201">Name of the resource ID for the impacted resource if it is a metric alert.</span><span class="sxs-lookup"><span data-stu-id="b68d7-201">Name of the resource ID for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="b68d7-202">For other alert types, this is the resource ID of the alert resource itself.</span><span class="sxs-lookup"><span data-stu-id="b68d7-202">For other alert types, this is the resource ID of the alert resource itself.</span></span> |
| <span data-ttu-id="b68d7-203">operationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-203">operationId</span></span> |<span data-ttu-id="b68d7-204">A GUID shared among the events that correspond to a single operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-204">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="b68d7-205">operationName</span><span class="sxs-lookup"><span data-stu-id="b68d7-205">operationName</span></span> |<span data-ttu-id="b68d7-206">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-206">Name of the operation.</span></span> |
| <span data-ttu-id="b68d7-207">properties</span><span class="sxs-lookup"><span data-stu-id="b68d7-207">properties</span></span> |<span data-ttu-id="b68d7-208">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-208">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="b68d7-209">status</span><span class="sxs-lookup"><span data-stu-id="b68d7-209">status</span></span> |<span data-ttu-id="b68d7-210">String describing the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-210">String describing the status of the operation.</span></span> <span data-ttu-id="b68d7-211">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="b68d7-211">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="b68d7-212">subStatus</span><span class="sxs-lookup"><span data-stu-id="b68d7-212">subStatus</span></span> | <span data-ttu-id="b68d7-213">Usually null for alerts.</span><span class="sxs-lookup"><span data-stu-id="b68d7-213">Usually null for alerts.</span></span> |
| <span data-ttu-id="b68d7-214">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-214">eventTimestamp</span></span> |<span data-ttu-id="b68d7-215">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-215">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="b68d7-216">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-216">submissionTimestamp</span></span> |<span data-ttu-id="b68d7-217">Timestamp when the event became available for querying.</span><span class="sxs-lookup"><span data-stu-id="b68d7-217">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="b68d7-218">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="b68d7-218">subscriptionId</span></span> |<span data-ttu-id="b68d7-219">Azure Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="b68d7-219">Azure Subscription ID.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="b68d7-220">Properties field per alert type</span><span class="sxs-lookup"><span data-stu-id="b68d7-220">Properties field per alert type</span></span>
<span data-ttu-id="b68d7-221">The properties field will contain different values depending on the source of the alert event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-221">The properties field will contain different values depending on the source of the alert event.</span></span> <span data-ttu-id="b68d7-222">Two common alert event providers are Activity Log alerts and metric alerts.</span><span class="sxs-lookup"><span data-stu-id="b68d7-222">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="b68d7-223">Properties for Activity Log alerts</span><span class="sxs-lookup"><span data-stu-id="b68d7-223">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="b68d7-224">Element Name</span><span class="sxs-lookup"><span data-stu-id="b68d7-224">Element Name</span></span> | <span data-ttu-id="b68d7-225">Description</span><span class="sxs-lookup"><span data-stu-id="b68d7-225">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b68d7-226">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="b68d7-226">properties.subscriptionId</span></span> | <span data-ttu-id="b68d7-227">The subscription ID from the activity log event which caused this activity log alert rule to be activated.</span><span class="sxs-lookup"><span data-stu-id="b68d7-227">The subscription ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="b68d7-228">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="b68d7-228">properties.eventDataId</span></span> | <span data-ttu-id="b68d7-229">The event data ID from the activity log event which caused this activity log alert rule to be activated.</span><span class="sxs-lookup"><span data-stu-id="b68d7-229">The event data ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="b68d7-230">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="b68d7-230">properties.resourceGroup</span></span> | <span data-ttu-id="b68d7-231">The resource group from the activity log event which caused this activity log alert rule to be activated.</span><span class="sxs-lookup"><span data-stu-id="b68d7-231">The resource group from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="b68d7-232">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="b68d7-232">properties.resourceId</span></span> | <span data-ttu-id="b68d7-233">The resource ID from the activity log event which caused this activity log alert rule to be activated.</span><span class="sxs-lookup"><span data-stu-id="b68d7-233">The resource ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="b68d7-234">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-234">properties.eventTimestamp</span></span> | <span data-ttu-id="b68d7-235">The event timestamp of the activity log event which caused this activity log alert rule to be activated.</span><span class="sxs-lookup"><span data-stu-id="b68d7-235">The event timestamp of the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="b68d7-236">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="b68d7-236">properties.operationName</span></span> | <span data-ttu-id="b68d7-237">The operation name from the activity log event which caused this activity log alert rule to be activated.</span><span class="sxs-lookup"><span data-stu-id="b68d7-237">The operation name from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="b68d7-238">properties.status</span><span class="sxs-lookup"><span data-stu-id="b68d7-238">properties.status</span></span> | <span data-ttu-id="b68d7-239">The status from the activity log event which caused this activity log alert rule to be activated.</span><span class="sxs-lookup"><span data-stu-id="b68d7-239">The status from the activity log event which caused this activity log alert rule to be activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="b68d7-240">Properties for metric alerts</span><span class="sxs-lookup"><span data-stu-id="b68d7-240">Properties for metric alerts</span></span>
| <span data-ttu-id="b68d7-241">Element Name</span><span class="sxs-lookup"><span data-stu-id="b68d7-241">Element Name</span></span> | <span data-ttu-id="b68d7-242">Description</span><span class="sxs-lookup"><span data-stu-id="b68d7-242">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b68d7-243">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="b68d7-243">properties.RuleUri</span></span> | <span data-ttu-id="b68d7-244">Resource ID of the metric alert rule itself.</span><span class="sxs-lookup"><span data-stu-id="b68d7-244">Resource ID of the metric alert rule itself.</span></span> |
| <span data-ttu-id="b68d7-245">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="b68d7-245">properties.RuleName</span></span> | <span data-ttu-id="b68d7-246">The name of the metric alert rule.</span><span class="sxs-lookup"><span data-stu-id="b68d7-246">The name of the metric alert rule.</span></span> |
| <span data-ttu-id="b68d7-247">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="b68d7-247">properties.RuleDescription</span></span> | <span data-ttu-id="b68d7-248">The description of the metric alert rule (as defined in the alert rule).</span><span class="sxs-lookup"><span data-stu-id="b68d7-248">The description of the metric alert rule (as defined in the alert rule).</span></span> |
| <span data-ttu-id="b68d7-249">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="b68d7-249">properties.Threshold</span></span> | <span data-ttu-id="b68d7-250">The threshold value used in the evaluation of the metric alert rule.</span><span class="sxs-lookup"><span data-stu-id="b68d7-250">The threshold value used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="b68d7-251">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="b68d7-251">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="b68d7-252">The window size used in the evaluation of the metric alert rule.</span><span class="sxs-lookup"><span data-stu-id="b68d7-252">The window size used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="b68d7-253">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="b68d7-253">properties.Aggregation</span></span> | <span data-ttu-id="b68d7-254">The aggregation type defined in the metric alert rule.</span><span class="sxs-lookup"><span data-stu-id="b68d7-254">The aggregation type defined in the metric alert rule.</span></span> |
| <span data-ttu-id="b68d7-255">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="b68d7-255">properties.Operator</span></span> | <span data-ttu-id="b68d7-256">The conditional operator used in the evaluation of the metric alert rule.</span><span class="sxs-lookup"><span data-stu-id="b68d7-256">The conditional operator used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="b68d7-257">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="b68d7-257">properties.MetricName</span></span> | <span data-ttu-id="b68d7-258">The metric name of the metric used in the evaluation of the metric alert rule.</span><span class="sxs-lookup"><span data-stu-id="b68d7-258">The metric name of the metric used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="b68d7-259">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="b68d7-259">properties.MetricUnit</span></span> | <span data-ttu-id="b68d7-260">The metric unit for the metric used in the evaluation of the metric alert rule.</span><span class="sxs-lookup"><span data-stu-id="b68d7-260">The metric unit for the metric used in the evaluation of the metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="b68d7-261">Autoscale</span><span class="sxs-lookup"><span data-stu-id="b68d7-261">Autoscale</span></span>
<span data-ttu-id="b68d7-262">This category contains the record of any events related to the operation of the autoscale engine based on any autoscale settings you have defined in your subscription.</span><span class="sxs-lookup"><span data-stu-id="b68d7-262">This category contains the record of any events related to the operation of the autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="b68d7-263">An example of the type of event you would see in this category is "Autoscale scale up action failed."</span><span class="sxs-lookup"><span data-stu-id="b68d7-263">An example of the type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="b68d7-264">Using autoscale, you can automatically scale out or scale in the number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="b68d7-264">Using autoscale, you can automatically scale out or scale in the number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="b68d7-265">When the conditions are met to scale up or down, the start and succeeded or failed events will be recorded in this category.</span><span class="sxs-lookup"><span data-stu-id="b68d7-265">When the conditions are met to scale up or down, the start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="b68d7-266">Sample event</span><span class="sxs-lookup"><span data-stu-id="b68d7-266">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "The autoscale engine attempting to scale resource '/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "The autoscale engine attempting to scale resource '/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
    "ResourceName": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "<subscription ID>"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="b68d7-267">Property descriptions</span><span class="sxs-lookup"><span data-stu-id="b68d7-267">Property descriptions</span></span>
| <span data-ttu-id="b68d7-268">Element Name</span><span class="sxs-lookup"><span data-stu-id="b68d7-268">Element Name</span></span> | <span data-ttu-id="b68d7-269">Description</span><span class="sxs-lookup"><span data-stu-id="b68d7-269">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b68d7-270">caller</span><span class="sxs-lookup"><span data-stu-id="b68d7-270">caller</span></span> | <span data-ttu-id="b68d7-271">Always Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="b68d7-271">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="b68d7-272">channels</span><span class="sxs-lookup"><span data-stu-id="b68d7-272">channels</span></span> | <span data-ttu-id="b68d7-273">Always “Admin, Operation”</span><span class="sxs-lookup"><span data-stu-id="b68d7-273">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="b68d7-274">claims</span><span class="sxs-lookup"><span data-stu-id="b68d7-274">claims</span></span> | <span data-ttu-id="b68d7-275">JSON blob with the SPN (service principal name), or resource type, of the autoscale engine.</span><span class="sxs-lookup"><span data-stu-id="b68d7-275">JSON blob with the SPN (service principal name), or resource type, of the autoscale engine.</span></span> |
| <span data-ttu-id="b68d7-276">correlationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-276">correlationId</span></span> | <span data-ttu-id="b68d7-277">A GUID in the string format.</span><span class="sxs-lookup"><span data-stu-id="b68d7-277">A GUID in the string format.</span></span> |
| <span data-ttu-id="b68d7-278">description</span><span class="sxs-lookup"><span data-stu-id="b68d7-278">description</span></span> |<span data-ttu-id="b68d7-279">Static text description of the autoscale event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-279">Static text description of the autoscale event.</span></span> |
| <span data-ttu-id="b68d7-280">eventDataId</span><span class="sxs-lookup"><span data-stu-id="b68d7-280">eventDataId</span></span> |<span data-ttu-id="b68d7-281">Unique identifier of the autoscale event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-281">Unique identifier of the autoscale event.</span></span> |
| <span data-ttu-id="b68d7-282">level</span><span class="sxs-lookup"><span data-stu-id="b68d7-282">level</span></span> |<span data-ttu-id="b68d7-283">Level of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-283">Level of the event.</span></span> <span data-ttu-id="b68d7-284">One of the following values: “Critical”, “Error”, “Warning”, and “Informational”</span><span class="sxs-lookup"><span data-stu-id="b68d7-284">One of the following values: “Critical”, “Error”, “Warning”, and “Informational”</span></span> |
| <span data-ttu-id="b68d7-285">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b68d7-285">resourceGroupName</span></span> |<span data-ttu-id="b68d7-286">Name of the resource group for the autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="b68d7-286">Name of the resource group for the autoscale setting.</span></span> |
| <span data-ttu-id="b68d7-287">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="b68d7-287">resourceProviderName</span></span> |<span data-ttu-id="b68d7-288">Name of the resource provider for the autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="b68d7-288">Name of the resource provider for the autoscale setting.</span></span> |
| <span data-ttu-id="b68d7-289">resourceId</span><span class="sxs-lookup"><span data-stu-id="b68d7-289">resourceId</span></span> |<span data-ttu-id="b68d7-290">Resource ID of the autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="b68d7-290">Resource ID of the autoscale setting.</span></span> |
| <span data-ttu-id="b68d7-291">operationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-291">operationId</span></span> |<span data-ttu-id="b68d7-292">A GUID shared among the events that correspond to a single operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-292">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="b68d7-293">operationName</span><span class="sxs-lookup"><span data-stu-id="b68d7-293">operationName</span></span> |<span data-ttu-id="b68d7-294">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-294">Name of the operation.</span></span> |
| <span data-ttu-id="b68d7-295">properties</span><span class="sxs-lookup"><span data-stu-id="b68d7-295">properties</span></span> |<span data-ttu-id="b68d7-296">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-296">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="b68d7-297">properties.Description</span><span class="sxs-lookup"><span data-stu-id="b68d7-297">properties.Description</span></span> | <span data-ttu-id="b68d7-298">Detailed description of what the autoscale engine was doing.</span><span class="sxs-lookup"><span data-stu-id="b68d7-298">Detailed description of what the autoscale engine was doing.</span></span> |
| <span data-ttu-id="b68d7-299">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="b68d7-299">properties.ResourceName</span></span> | <span data-ttu-id="b68d7-300">Resource ID of the impacted resource (the resource on which the scale action was being performed)</span><span class="sxs-lookup"><span data-stu-id="b68d7-300">Resource ID of the impacted resource (the resource on which the scale action was being performed)</span></span> |
| <span data-ttu-id="b68d7-301">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="b68d7-301">properties.OldInstancesCount</span></span> | <span data-ttu-id="b68d7-302">The number of instances before the autoscale action took effect.</span><span class="sxs-lookup"><span data-stu-id="b68d7-302">The number of instances before the autoscale action took effect.</span></span> |
| <span data-ttu-id="b68d7-303">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="b68d7-303">properties.NewInstancesCount</span></span> | <span data-ttu-id="b68d7-304">The number of instances after the autoscale action took effect.</span><span class="sxs-lookup"><span data-stu-id="b68d7-304">The number of instances after the autoscale action took effect.</span></span> |
| <span data-ttu-id="b68d7-305">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="b68d7-305">properties.LastScaleActionTime</span></span> | <span data-ttu-id="b68d7-306">The timestamp of when the autoscale action occurred.</span><span class="sxs-lookup"><span data-stu-id="b68d7-306">The timestamp of when the autoscale action occurred.</span></span> |
| <span data-ttu-id="b68d7-307">status</span><span class="sxs-lookup"><span data-stu-id="b68d7-307">status</span></span> |<span data-ttu-id="b68d7-308">String describing the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-308">String describing the status of the operation.</span></span> <span data-ttu-id="b68d7-309">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="b68d7-309">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="b68d7-310">subStatus</span><span class="sxs-lookup"><span data-stu-id="b68d7-310">subStatus</span></span> | <span data-ttu-id="b68d7-311">Usually null for autoscale.</span><span class="sxs-lookup"><span data-stu-id="b68d7-311">Usually null for autoscale.</span></span> |
| <span data-ttu-id="b68d7-312">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-312">eventTimestamp</span></span> |<span data-ttu-id="b68d7-313">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-313">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="b68d7-314">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-314">submissionTimestamp</span></span> |<span data-ttu-id="b68d7-315">Timestamp when the event became available for querying.</span><span class="sxs-lookup"><span data-stu-id="b68d7-315">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="b68d7-316">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="b68d7-316">subscriptionId</span></span> |<span data-ttu-id="b68d7-317">Azure Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="b68d7-317">Azure Subscription ID.</span></span> |

## <a name="security"></a><span data-ttu-id="b68d7-318">Security</span><span class="sxs-lookup"><span data-stu-id="b68d7-318">Security</span></span>
<span data-ttu-id="b68d7-319">This category contains the record any alerts generated by Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="b68d7-319">This category contains the record any alerts generated by Azure Security Center.</span></span> <span data-ttu-id="b68d7-320">An example of the type of event you would see in this category is "Suspicious double extension file executed."</span><span class="sxs-lookup"><span data-stu-id="b68d7-320">An example of the type of event you would see in this category is "Suspicious double extension file executed."</span></span>

### <a name="sample-event"></a><span data-ttu-id="b68d7-321">Sample event</span><span class="sxs-lookup"><span data-stu-id="b68d7-321">Sample event</span></span>
```json
{
    "channels": "Operation",
    "correlationId": "965d6c6a-a790-4a7e-8e9a-41771b3fbc38",
    "description": "Suspicious double extension file executed. Machine logs indicate an execution of a process with a suspicious double extension.\r\nThis extension may trick users into thinking files are safe to be opened and might indicate the presence of malware on the system.",
    "eventDataId": "965d6c6a-a790-4a7e-8e9a-41771b3fbc38",
    "eventName": {
        "value": "Suspicious double extension file executed",
        "localizedValue": "Suspicious double extension file executed"
    },
    "category": {
        "value": "Security",
        "localizedValue": "Security"
    },
    "eventTimestamp": "2017-10-18T06:02:18.6179339Z",
    "id": "/subscriptions/<subscription ID>/providers/Microsoft.Security/locations/centralus/alerts/965d6c6a-a790-4a7e-8e9a-41771b3fbc38/events/965d6c6a-a790-4a7e-8e9a-41771b3fbc38/ticks/636439033386179339",
    "level": "Informational",
    "operationId": "965d6c6a-a790-4a7e-8e9a-41771b3fbc38",
    "operationName": {
        "value": "Microsoft.Security/locations/alerts/activate/action",
        "localizedValue": "Microsoft.Security/locations/alerts/activate/action"
    },
    "resourceGroupName": "myResourceGroup",
    "resourceProviderName": {
        "value": "Microsoft.Security",
        "localizedValue": "Microsoft.Security"
    },
    "resourceType": {
        "value": "Microsoft.Security/locations/alerts",
        "localizedValue": "Microsoft.Security/locations/alerts"
    },
    "resourceId": "/subscriptions/<subscription ID>/providers/Microsoft.Security/locations/centralus/alerts/2518939942613820660_a48f8653-3fc6-4166-9f19-914f030a13d3",
    "status": {
        "value": "Active",
        "localizedValue": "Active"
    },
    "subStatus": {
        "value": null
    },
    "submissionTimestamp": "2017-10-18T06:02:52.2176969Z",
    "subscriptionId": "<subscription ID>",
    "properties": {
        "accountLogonId": "0x2r4",
        "commandLine": "c:\\mydirectory\\doubleetension.pdf.exe",
        "domainName": "hpc",
        "parentProcess": "unknown",
        "parentProcess id": "0",
        "processId": "6988",
        "processName": "c:\\mydirectory\\doubleetension.pdf.exe",
        "userName": "myUser",
        "UserSID": "S-3-2-12",
        "ActionTaken": "Detected",
        "Severity": "High"
    },
    "relatedEvents": []
}

```

### <a name="property-descriptions"></a><span data-ttu-id="b68d7-322">Property descriptions</span><span class="sxs-lookup"><span data-stu-id="b68d7-322">Property descriptions</span></span>
| <span data-ttu-id="b68d7-323">Element Name</span><span class="sxs-lookup"><span data-stu-id="b68d7-323">Element Name</span></span> | <span data-ttu-id="b68d7-324">Description</span><span class="sxs-lookup"><span data-stu-id="b68d7-324">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b68d7-325">channels</span><span class="sxs-lookup"><span data-stu-id="b68d7-325">channels</span></span> | <span data-ttu-id="b68d7-326">Always “Operation”</span><span class="sxs-lookup"><span data-stu-id="b68d7-326">Always “Operation”</span></span> |
| <span data-ttu-id="b68d7-327">correlationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-327">correlationId</span></span> | <span data-ttu-id="b68d7-328">A GUID in the string format.</span><span class="sxs-lookup"><span data-stu-id="b68d7-328">A GUID in the string format.</span></span> |
| <span data-ttu-id="b68d7-329">description</span><span class="sxs-lookup"><span data-stu-id="b68d7-329">description</span></span> |<span data-ttu-id="b68d7-330">Static text description of the security event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-330">Static text description of the security event.</span></span> |
| <span data-ttu-id="b68d7-331">eventDataId</span><span class="sxs-lookup"><span data-stu-id="b68d7-331">eventDataId</span></span> |<span data-ttu-id="b68d7-332">Unique identifier of the security event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-332">Unique identifier of the security event.</span></span> |
| <span data-ttu-id="b68d7-333">eventName</span><span class="sxs-lookup"><span data-stu-id="b68d7-333">eventName</span></span> |<span data-ttu-id="b68d7-334">Friendly name of the security event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-334">Friendly name of the security event.</span></span> |
| <span data-ttu-id="b68d7-335">id</span><span class="sxs-lookup"><span data-stu-id="b68d7-335">id</span></span> |<span data-ttu-id="b68d7-336">Unique resource identifier of the security event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-336">Unique resource identifier of the security event.</span></span> |
| <span data-ttu-id="b68d7-337">level</span><span class="sxs-lookup"><span data-stu-id="b68d7-337">level</span></span> |<span data-ttu-id="b68d7-338">Level of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-338">Level of the event.</span></span> <span data-ttu-id="b68d7-339">One of the following values: “Critical”, “Error”, “Warning”, or “Informational”</span><span class="sxs-lookup"><span data-stu-id="b68d7-339">One of the following values: “Critical”, “Error”, “Warning”, or “Informational”</span></span> |
| <span data-ttu-id="b68d7-340">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b68d7-340">resourceGroupName</span></span> |<span data-ttu-id="b68d7-341">Name of the resource group for the resource.</span><span class="sxs-lookup"><span data-stu-id="b68d7-341">Name of the resource group for the resource.</span></span> |
| <span data-ttu-id="b68d7-342">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="b68d7-342">resourceProviderName</span></span> |<span data-ttu-id="b68d7-343">Name of the resource provider for Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="b68d7-343">Name of the resource provider for Azure Security Center.</span></span> <span data-ttu-id="b68d7-344">Always "Microsoft.Security".</span><span class="sxs-lookup"><span data-stu-id="b68d7-344">Always "Microsoft.Security".</span></span> |
| <span data-ttu-id="b68d7-345">resourceType</span><span class="sxs-lookup"><span data-stu-id="b68d7-345">resourceType</span></span> |<span data-ttu-id="b68d7-346">The type of resource that generated the security event, such as "Microsoft.Security/locations/alerts"</span><span class="sxs-lookup"><span data-stu-id="b68d7-346">The type of resource that generated the security event, such as "Microsoft.Security/locations/alerts"</span></span> |
| <span data-ttu-id="b68d7-347">resourceId</span><span class="sxs-lookup"><span data-stu-id="b68d7-347">resourceId</span></span> |<span data-ttu-id="b68d7-348">Resource ID of the security alert.</span><span class="sxs-lookup"><span data-stu-id="b68d7-348">Resource ID of the security alert.</span></span> |
| <span data-ttu-id="b68d7-349">operationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-349">operationId</span></span> |<span data-ttu-id="b68d7-350">A GUID shared among the events that correspond to a single operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-350">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="b68d7-351">operationName</span><span class="sxs-lookup"><span data-stu-id="b68d7-351">operationName</span></span> |<span data-ttu-id="b68d7-352">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-352">Name of the operation.</span></span> |
| <span data-ttu-id="b68d7-353">properties</span><span class="sxs-lookup"><span data-stu-id="b68d7-353">properties</span></span> |<span data-ttu-id="b68d7-354">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-354">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> <span data-ttu-id="b68d7-355">These properties will vary depending on the type of security alert.</span><span class="sxs-lookup"><span data-stu-id="b68d7-355">These properties will vary depending on the type of security alert.</span></span> <span data-ttu-id="b68d7-356">See [this page](../security-center/security-center-alerts-type.md) for a description of the types of alerts that come from Security Center.</span><span class="sxs-lookup"><span data-stu-id="b68d7-356">See [this page](../security-center/security-center-alerts-type.md) for a description of the types of alerts that come from Security Center.</span></span> |
| <span data-ttu-id="b68d7-357">properties.Severity</span><span class="sxs-lookup"><span data-stu-id="b68d7-357">properties.Severity</span></span> |<span data-ttu-id="b68d7-358">The severity level.</span><span class="sxs-lookup"><span data-stu-id="b68d7-358">The severity level.</span></span> <span data-ttu-id="b68d7-359">Possible values are "High," "Medium," or "Low."</span><span class="sxs-lookup"><span data-stu-id="b68d7-359">Possible values are "High," "Medium," or "Low."</span></span> |
| <span data-ttu-id="b68d7-360">status</span><span class="sxs-lookup"><span data-stu-id="b68d7-360">status</span></span> |<span data-ttu-id="b68d7-361">String describing the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-361">String describing the status of the operation.</span></span> <span data-ttu-id="b68d7-362">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="b68d7-362">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="b68d7-363">subStatus</span><span class="sxs-lookup"><span data-stu-id="b68d7-363">subStatus</span></span> | <span data-ttu-id="b68d7-364">Usually null for security events.</span><span class="sxs-lookup"><span data-stu-id="b68d7-364">Usually null for security events.</span></span> |
| <span data-ttu-id="b68d7-365">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-365">eventTimestamp</span></span> |<span data-ttu-id="b68d7-366">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-366">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="b68d7-367">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-367">submissionTimestamp</span></span> |<span data-ttu-id="b68d7-368">Timestamp when the event became available for querying.</span><span class="sxs-lookup"><span data-stu-id="b68d7-368">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="b68d7-369">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="b68d7-369">subscriptionId</span></span> |<span data-ttu-id="b68d7-370">Azure Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="b68d7-370">Azure Subscription ID.</span></span> |

## <a name="recommendation"></a><span data-ttu-id="b68d7-371">Recommendation</span><span class="sxs-lookup"><span data-stu-id="b68d7-371">Recommendation</span></span>
<span data-ttu-id="b68d7-372">This category contains the record of any new recommendations that are generated for your services.</span><span class="sxs-lookup"><span data-stu-id="b68d7-372">This category contains the record of any new recommendations that are generated for your services.</span></span> <span data-ttu-id="b68d7-373">An example of a recommendation would be "Use availability sets for improved fault tolerance."</span><span class="sxs-lookup"><span data-stu-id="b68d7-373">An example of a recommendation would be "Use availability sets for improved fault tolerance."</span></span> <span data-ttu-id="b68d7-374">There are 4 types of Recommendation events that can be generated: High Availability, Performance, Security, and Cost Optimization.</span><span class="sxs-lookup"><span data-stu-id="b68d7-374">There are 4 types of Recommendation events that can be generated: High Availability, Performance, Security, and Cost Optimization.</span></span> 

### <a name="sample-event"></a><span data-ttu-id="b68d7-375">Sample event</span><span class="sxs-lookup"><span data-stu-id="b68d7-375">Sample event</span></span>
```json
{
    "channels": "Operation",
    "correlationId": "92481dfd-c5bf-4752-b0d6-0ecddaa64776",
    "description": "The action was successful.",
    "eventDataId": "06cb0e44-111b-47c7-a4f2-aa3ee320c9c5",
    "eventName": {
        "value": "",
        "localizedValue": ""
    },
    "category": {
        "value": "Recommendation",
        "localizedValue": "Recommendation"
    },
    "eventTimestamp": "2018-06-07T21:30:42.976919Z",
    "id": "/SUBSCRIPTIONS/<Subscription ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.COMPUTE/VIRTUALMACHINES/MYVM/events/06cb0e44-111b-47c7-a4f2-aa3ee320c9c5/ticks/636640038429769190",
    "level": "Informational",
    "operationId": "",
    "operationName": {
        "value": "Microsoft.Advisor/generateRecommendations/action",
        "localizedValue": "Microsoft.Advisor/generateRecommendations/action"
    },
    "resourceGroupName": "MYRESOURCEGROUP",
    "resourceProviderName": {
        "value": "MICROSOFT.COMPUTE",
        "localizedValue": "MICROSOFT.COMPUTE"
    },
    "resourceType": {
        "value": "MICROSOFT.COMPUTE/virtualmachines",
        "localizedValue": "MICROSOFT.COMPUTE/virtualmachines"
    },
    "resourceId": "/SUBSCRIPTIONS/<Subscription ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.COMPUTE/VIRTUALMACHINES/MYVM",
    "status": {
        "value": "Active",
        "localizedValue": "Active"
    },
    "subStatus": {
        "value": "",
        "localizedValue": ""
    },
    "submissionTimestamp": "2018-06-07T21:30:42.976919Z",
    "subscriptionId": "<Subscription ID>",
    "properties": {
        "recommendationSchemaVersion": "1.0",
        "recommendationCategory": "Security",
        "recommendationImpact": "High",
        "recommendationRisk": "None"
    },
    "relatedEvents": []
}

```
### <a name="property-descriptions"></a><span data-ttu-id="b68d7-376">Property descriptions</span><span class="sxs-lookup"><span data-stu-id="b68d7-376">Property descriptions</span></span>
| <span data-ttu-id="b68d7-377">Element Name</span><span class="sxs-lookup"><span data-stu-id="b68d7-377">Element Name</span></span> | <span data-ttu-id="b68d7-378">Description</span><span class="sxs-lookup"><span data-stu-id="b68d7-378">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b68d7-379">channels</span><span class="sxs-lookup"><span data-stu-id="b68d7-379">channels</span></span> | <span data-ttu-id="b68d7-380">Always “Operation”</span><span class="sxs-lookup"><span data-stu-id="b68d7-380">Always “Operation”</span></span> |
| <span data-ttu-id="b68d7-381">correlationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-381">correlationId</span></span> | <span data-ttu-id="b68d7-382">A GUID in the string format.</span><span class="sxs-lookup"><span data-stu-id="b68d7-382">A GUID in the string format.</span></span> |
| <span data-ttu-id="b68d7-383">description</span><span class="sxs-lookup"><span data-stu-id="b68d7-383">description</span></span> |<span data-ttu-id="b68d7-384">Static text description of the recommendation event</span><span class="sxs-lookup"><span data-stu-id="b68d7-384">Static text description of the recommendation event</span></span> |
| <span data-ttu-id="b68d7-385">eventDataId</span><span class="sxs-lookup"><span data-stu-id="b68d7-385">eventDataId</span></span> | <span data-ttu-id="b68d7-386">Unique identifier of the recommendation event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-386">Unique identifier of the recommendation event.</span></span> |
| <span data-ttu-id="b68d7-387">category</span><span class="sxs-lookup"><span data-stu-id="b68d7-387">category</span></span> | <span data-ttu-id="b68d7-388">Always "Recommendation"</span><span class="sxs-lookup"><span data-stu-id="b68d7-388">Always "Recommendation"</span></span> |
| <span data-ttu-id="b68d7-389">id</span><span class="sxs-lookup"><span data-stu-id="b68d7-389">id</span></span> |<span data-ttu-id="b68d7-390">Unique resource identifier of the recommendation event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-390">Unique resource identifier of the recommendation event.</span></span> |
| <span data-ttu-id="b68d7-391">level</span><span class="sxs-lookup"><span data-stu-id="b68d7-391">level</span></span> |<span data-ttu-id="b68d7-392">Level of the event.</span><span class="sxs-lookup"><span data-stu-id="b68d7-392">Level of the event.</span></span> <span data-ttu-id="b68d7-393">One of the following values: “Critical”, “Error”, “Warning”, or “Informational”</span><span class="sxs-lookup"><span data-stu-id="b68d7-393">One of the following values: “Critical”, “Error”, “Warning”, or “Informational”</span></span> |
| <span data-ttu-id="b68d7-394">operationName</span><span class="sxs-lookup"><span data-stu-id="b68d7-394">operationName</span></span> |<span data-ttu-id="b68d7-395">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-395">Name of the operation.</span></span>  <span data-ttu-id="b68d7-396">Always "Microsoft.Advisor/generateRecommendations/action"</span><span class="sxs-lookup"><span data-stu-id="b68d7-396">Always "Microsoft.Advisor/generateRecommendations/action"</span></span>|
| <span data-ttu-id="b68d7-397">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b68d7-397">resourceGroupName</span></span> |<span data-ttu-id="b68d7-398">Name of the resource group for the resource.</span><span class="sxs-lookup"><span data-stu-id="b68d7-398">Name of the resource group for the resource.</span></span> |
| <span data-ttu-id="b68d7-399">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="b68d7-399">resourceProviderName</span></span> |<span data-ttu-id="b68d7-400">Name of the resource provider for the resource that this recommendation applies to, such as "MICROSOFT.COMPUTE"</span><span class="sxs-lookup"><span data-stu-id="b68d7-400">Name of the resource provider for the resource that this recommendation applies to, such as "MICROSOFT.COMPUTE"</span></span> |
| <span data-ttu-id="b68d7-401">resourceType</span><span class="sxs-lookup"><span data-stu-id="b68d7-401">resourceType</span></span> |<span data-ttu-id="b68d7-402">Name of the resource type for the resource that this recommendation applies to, such as "MICROSOFT.COMPUTE/virtualmachines"</span><span class="sxs-lookup"><span data-stu-id="b68d7-402">Name of the resource type for the resource that this recommendation applies to, such as "MICROSOFT.COMPUTE/virtualmachines"</span></span> |
| <span data-ttu-id="b68d7-403">resourceId</span><span class="sxs-lookup"><span data-stu-id="b68d7-403">resourceId</span></span> |<span data-ttu-id="b68d7-404">Resource ID of the resource that the recommendation applies to</span><span class="sxs-lookup"><span data-stu-id="b68d7-404">Resource ID of the resource that the recommendation applies to</span></span> |
| <span data-ttu-id="b68d7-405">status</span><span class="sxs-lookup"><span data-stu-id="b68d7-405">status</span></span> | <span data-ttu-id="b68d7-406">Always "Active"</span><span class="sxs-lookup"><span data-stu-id="b68d7-406">Always "Active"</span></span> |
| <span data-ttu-id="b68d7-407">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-407">submissionTimestamp</span></span> |<span data-ttu-id="b68d7-408">Timestamp when the event became available for querying.</span><span class="sxs-lookup"><span data-stu-id="b68d7-408">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="b68d7-409">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="b68d7-409">subscriptionId</span></span> |<span data-ttu-id="b68d7-410">Azure Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="b68d7-410">Azure Subscription ID.</span></span> |
| <span data-ttu-id="b68d7-411">properties</span><span class="sxs-lookup"><span data-stu-id="b68d7-411">properties</span></span> |<span data-ttu-id="b68d7-412">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the recommendation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-412">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the recommendation.</span></span>|
| <span data-ttu-id="b68d7-413">properties.recommendationSchemaVersion</span><span class="sxs-lookup"><span data-stu-id="b68d7-413">properties.recommendationSchemaVersion</span></span>| <span data-ttu-id="b68d7-414">Schema version of the recommendation properties published in the Activity Log entry</span><span class="sxs-lookup"><span data-stu-id="b68d7-414">Schema version of the recommendation properties published in the Activity Log entry</span></span> |
| <span data-ttu-id="b68d7-415">properties.recommendationCategory</span><span class="sxs-lookup"><span data-stu-id="b68d7-415">properties.recommendationCategory</span></span> | <span data-ttu-id="b68d7-416">Category of the recommendation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-416">Category of the recommendation.</span></span> <span data-ttu-id="b68d7-417">Possible values are "High Availability", "Performance", "Security", and "Cost"</span><span class="sxs-lookup"><span data-stu-id="b68d7-417">Possible values are "High Availability", "Performance", "Security", and "Cost"</span></span> |
| <span data-ttu-id="b68d7-418">properties.recommendationImpact</span><span class="sxs-lookup"><span data-stu-id="b68d7-418">properties.recommendationImpact</span></span>| <span data-ttu-id="b68d7-419">Impact of the recommendation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-419">Impact of the recommendation.</span></span> <span data-ttu-id="b68d7-420">Possible values are "High", "Medium", "Low"</span><span class="sxs-lookup"><span data-stu-id="b68d7-420">Possible values are "High", "Medium", "Low"</span></span> |
| <span data-ttu-id="b68d7-421">properties.recommendationRisk</span><span class="sxs-lookup"><span data-stu-id="b68d7-421">properties.recommendationRisk</span></span>| <span data-ttu-id="b68d7-422">Risk of the recommendation.</span><span class="sxs-lookup"><span data-stu-id="b68d7-422">Risk of the recommendation.</span></span> <span data-ttu-id="b68d7-423">Possible values are "Error", "Warning", "None"</span><span class="sxs-lookup"><span data-stu-id="b68d7-423">Possible values are "Error", "Warning", "None"</span></span> |

## <a name="mapping-to-diagnostic-logs-schema"></a><span data-ttu-id="b68d7-424">Mapping to diagnostic logs schema</span><span class="sxs-lookup"><span data-stu-id="b68d7-424">Mapping to diagnostic logs schema</span></span>

<span data-ttu-id="b68d7-425">When streaming the Azure Activity Log to a storage account or Event Hubs namespace, the data follows the [Azure diagnostic logs schema](./monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b68d7-425">When streaming the Azure Activity Log to a storage account or Event Hubs namespace, the data follows the [Azure diagnostic logs schema](./monitoring-diagnostic-logs-schema.md).</span></span> <span data-ttu-id="b68d7-426">Here is the mapping of properties from the schema above to the diagnostic logs schema:</span><span class="sxs-lookup"><span data-stu-id="b68d7-426">Here is the mapping of properties from the schema above to the diagnostic logs schema:</span></span>

| <span data-ttu-id="b68d7-427">Diagnostic logs schema property</span><span class="sxs-lookup"><span data-stu-id="b68d7-427">Diagnostic logs schema property</span></span> | <span data-ttu-id="b68d7-428">Activity Log REST API schema property</span><span class="sxs-lookup"><span data-stu-id="b68d7-428">Activity Log REST API schema property</span></span> | <span data-ttu-id="b68d7-429">Notes</span><span class="sxs-lookup"><span data-stu-id="b68d7-429">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b68d7-430">time</span><span class="sxs-lookup"><span data-stu-id="b68d7-430">time</span></span> | <span data-ttu-id="b68d7-431">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="b68d7-431">eventTimestamp</span></span> |  |
| <span data-ttu-id="b68d7-432">resourceId</span><span class="sxs-lookup"><span data-stu-id="b68d7-432">resourceId</span></span> | <span data-ttu-id="b68d7-433">resourceId</span><span class="sxs-lookup"><span data-stu-id="b68d7-433">resourceId</span></span> | <span data-ttu-id="b68d7-434">subscriptionId, resourceType, resourceGroupName are all inferred from the resourceId.</span><span class="sxs-lookup"><span data-stu-id="b68d7-434">subscriptionId, resourceType, resourceGroupName are all inferred from the resourceId.</span></span> |
| <span data-ttu-id="b68d7-435">operationName</span><span class="sxs-lookup"><span data-stu-id="b68d7-435">operationName</span></span> | <span data-ttu-id="b68d7-436">operationName.value</span><span class="sxs-lookup"><span data-stu-id="b68d7-436">operationName.value</span></span> |  |
| <span data-ttu-id="b68d7-437">category</span><span class="sxs-lookup"><span data-stu-id="b68d7-437">category</span></span> | <span data-ttu-id="b68d7-438">Part of operation name</span><span class="sxs-lookup"><span data-stu-id="b68d7-438">Part of operation name</span></span> | <span data-ttu-id="b68d7-439">Breakout of the operation type - "Write"/"Delete"/"Action"</span><span class="sxs-lookup"><span data-stu-id="b68d7-439">Breakout of the operation type - "Write"/"Delete"/"Action"</span></span> |
| <span data-ttu-id="b68d7-440">resultType</span><span class="sxs-lookup"><span data-stu-id="b68d7-440">resultType</span></span> | <span data-ttu-id="b68d7-441">status.value</span><span class="sxs-lookup"><span data-stu-id="b68d7-441">status.value</span></span> | |
| <span data-ttu-id="b68d7-442">resultSignature</span><span class="sxs-lookup"><span data-stu-id="b68d7-442">resultSignature</span></span> | <span data-ttu-id="b68d7-443">substatus.value</span><span class="sxs-lookup"><span data-stu-id="b68d7-443">substatus.value</span></span> | |
| <span data-ttu-id="b68d7-444">resultDescription</span><span class="sxs-lookup"><span data-stu-id="b68d7-444">resultDescription</span></span> | <span data-ttu-id="b68d7-445">description</span><span class="sxs-lookup"><span data-stu-id="b68d7-445">description</span></span> |  |
| <span data-ttu-id="b68d7-446">durationMs</span><span class="sxs-lookup"><span data-stu-id="b68d7-446">durationMs</span></span> | <span data-ttu-id="b68d7-447">N/A</span><span class="sxs-lookup"><span data-stu-id="b68d7-447">N/A</span></span> | <span data-ttu-id="b68d7-448">Always 0</span><span class="sxs-lookup"><span data-stu-id="b68d7-448">Always 0</span></span> |
| <span data-ttu-id="b68d7-449">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="b68d7-449">callerIpAddress</span></span> | <span data-ttu-id="b68d7-450">httpRequest.clientIpAddress</span><span class="sxs-lookup"><span data-stu-id="b68d7-450">httpRequest.clientIpAddress</span></span> |  |
| <span data-ttu-id="b68d7-451">correlationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-451">correlationId</span></span> | <span data-ttu-id="b68d7-452">correlationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-452">correlationId</span></span> |  |
| <span data-ttu-id="b68d7-453">identity</span><span class="sxs-lookup"><span data-stu-id="b68d7-453">identity</span></span> | <span data-ttu-id="b68d7-454">claims and authorization properties</span><span class="sxs-lookup"><span data-stu-id="b68d7-454">claims and authorization properties</span></span> |  |
| <span data-ttu-id="b68d7-455">Level</span><span class="sxs-lookup"><span data-stu-id="b68d7-455">Level</span></span> | <span data-ttu-id="b68d7-456">Level</span><span class="sxs-lookup"><span data-stu-id="b68d7-456">Level</span></span> |  |
| <span data-ttu-id="b68d7-457">location</span><span class="sxs-lookup"><span data-stu-id="b68d7-457">location</span></span> | <span data-ttu-id="b68d7-458">N/A</span><span class="sxs-lookup"><span data-stu-id="b68d7-458">N/A</span></span> | <span data-ttu-id="b68d7-459">Location of where the event was processed.</span><span class="sxs-lookup"><span data-stu-id="b68d7-459">Location of where the event was processed.</span></span> <span data-ttu-id="b68d7-460">*This is not the location of the resource, but rather where the event was processed. This property will be removed in a future update.*</span><span class="sxs-lookup"><span data-stu-id="b68d7-460">*This is not the location of the resource, but rather where the event was processed. This property will be removed in a future update.*</span></span> |
| <span data-ttu-id="b68d7-461">Properties</span><span class="sxs-lookup"><span data-stu-id="b68d7-461">Properties</span></span> | <span data-ttu-id="b68d7-462">properties.eventProperties</span><span class="sxs-lookup"><span data-stu-id="b68d7-462">properties.eventProperties</span></span> |  |
| <span data-ttu-id="b68d7-463">properties.eventCategory</span><span class="sxs-lookup"><span data-stu-id="b68d7-463">properties.eventCategory</span></span> | <span data-ttu-id="b68d7-464">category</span><span class="sxs-lookup"><span data-stu-id="b68d7-464">category</span></span> | <span data-ttu-id="b68d7-465">If properties.eventCategory is not present, category is "Administrative"</span><span class="sxs-lookup"><span data-stu-id="b68d7-465">If properties.eventCategory is not present, category is "Administrative"</span></span> |
| <span data-ttu-id="b68d7-466">properties.eventName</span><span class="sxs-lookup"><span data-stu-id="b68d7-466">properties.eventName</span></span> | <span data-ttu-id="b68d7-467">eventName</span><span class="sxs-lookup"><span data-stu-id="b68d7-467">eventName</span></span> |  |
| <span data-ttu-id="b68d7-468">properties.operationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-468">properties.operationId</span></span> | <span data-ttu-id="b68d7-469">operationId</span><span class="sxs-lookup"><span data-stu-id="b68d7-469">operationId</span></span> |  |
| <span data-ttu-id="b68d7-470">properties.eventProperties</span><span class="sxs-lookup"><span data-stu-id="b68d7-470">properties.eventProperties</span></span> | <span data-ttu-id="b68d7-471">properties</span><span class="sxs-lookup"><span data-stu-id="b68d7-471">properties</span></span> |  |


## <a name="next-steps"></a><span data-ttu-id="b68d7-472">Next steps</span><span class="sxs-lookup"><span data-stu-id="b68d7-472">Next steps</span></span>
* [<span data-ttu-id="b68d7-473">Learn more about the Activity Log (formerly Audit Logs)</span><span class="sxs-lookup"><span data-stu-id="b68d7-473">Learn more about the Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="b68d7-474">Stream the Azure Activity Log to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b68d7-474">Stream the Azure Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
