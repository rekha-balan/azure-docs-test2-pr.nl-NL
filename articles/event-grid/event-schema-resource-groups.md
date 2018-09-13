---
title: Azure Event Grid resource group event schema
description: Describes the properties that are provided for resource group events with Azure Event Grid
services: event-grid
author: tfitzmac
ms.service: event-grid
ms.topic: reference
ms.date: 08/17/2018
ms.author: tomfitz
ms.openlocfilehash: 22629ba553cc58435f99ed0fed97be252b24b409
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966645"
---
# <a name="azure-event-grid-event-schema-for-resource-groups"></a><span data-ttu-id="754ae-103">Azure Event Grid event schema for resource groups</span><span class="sxs-lookup"><span data-stu-id="754ae-103">Azure Event Grid event schema for resource groups</span></span>

<span data-ttu-id="754ae-104">This article provides the properties and schema for resource group events.</span><span class="sxs-lookup"><span data-stu-id="754ae-104">This article provides the properties and schema for resource group events.</span></span> <span data-ttu-id="754ae-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span><span class="sxs-lookup"><span data-stu-id="754ae-105">For an introduction to event schemas, see [Azure Event Grid event schema](event-schema.md).</span></span>

<span data-ttu-id="754ae-106">Azure subscriptions and resource groups emit the same event types.</span><span class="sxs-lookup"><span data-stu-id="754ae-106">Azure subscriptions and resource groups emit the same event types.</span></span> <span data-ttu-id="754ae-107">The event types are related to changes in resources.</span><span class="sxs-lookup"><span data-stu-id="754ae-107">The event types are related to changes in resources.</span></span> <span data-ttu-id="754ae-108">The primary difference is that resource groups emit events for resources within the resource group, and Azure subscriptions emit events for resources across the subscription.</span><span class="sxs-lookup"><span data-stu-id="754ae-108">The primary difference is that resource groups emit events for resources within the resource group, and Azure subscriptions emit events for resources across the subscription.</span></span>

<span data-ttu-id="754ae-109">Resource events are created for PUT, PATCH, and DELETE operations that are sent to `management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="754ae-109">Resource events are created for PUT, PATCH, and DELETE operations that are sent to `management.azure.com`.</span></span> <span data-ttu-id="754ae-110">POST and GET operations do not create events.</span><span class="sxs-lookup"><span data-stu-id="754ae-110">POST and GET operations do not create events.</span></span> <span data-ttu-id="754ae-111">Operations sent to the data plane (like `myaccount.blob.core.windows.net`) do not create events.</span><span class="sxs-lookup"><span data-stu-id="754ae-111">Operations sent to the data plane (like `myaccount.blob.core.windows.net`) do not create events.</span></span>

<span data-ttu-id="754ae-112">When you subscribe to events for a resource group, your endpoint receives all events for that resource group.</span><span class="sxs-lookup"><span data-stu-id="754ae-112">When you subscribe to events for a resource group, your endpoint receives all events for that resource group.</span></span> <span data-ttu-id="754ae-113">The events can include event you want to see, such as updating a virtual machine, but also events that maybe aren't important to you, such as writing a new entry in the deployment history.</span><span class="sxs-lookup"><span data-stu-id="754ae-113">The events can include event you want to see, such as updating a virtual machine, but also events that maybe aren't important to you, such as writing a new entry in the deployment history.</span></span> <span data-ttu-id="754ae-114">You can either receive all events at your endpoint and write code that processes the events you want to handle, or you can set a filter when creating the event subscription.</span><span class="sxs-lookup"><span data-stu-id="754ae-114">You can either receive all events at your endpoint and write code that processes the events you want to handle, or you can set a filter when creating the event subscription.</span></span>

<span data-ttu-id="754ae-115">To programmatically handle events, you can sort events by looking at the `operationName` value.</span><span class="sxs-lookup"><span data-stu-id="754ae-115">To programmatically handle events, you can sort events by looking at the `operationName` value.</span></span> <span data-ttu-id="754ae-116">For example, your event endpoint might only process events for operations that are equal to `Microsoft.Compute/virtualMachines/write` or `Microsoft.Storage/storageAccounts/write`.</span><span class="sxs-lookup"><span data-stu-id="754ae-116">For example, your event endpoint might only process events for operations that are equal to `Microsoft.Compute/virtualMachines/write` or `Microsoft.Storage/storageAccounts/write`.</span></span>

<span data-ttu-id="754ae-117">The event subject is the resource ID of the resource that is the target of the operation.</span><span class="sxs-lookup"><span data-stu-id="754ae-117">The event subject is the resource ID of the resource that is the target of the operation.</span></span> <span data-ttu-id="754ae-118">To filter events for a resource, provide that resource ID when creating the event subscription.</span><span class="sxs-lookup"><span data-stu-id="754ae-118">To filter events for a resource, provide that resource ID when creating the event subscription.</span></span>  <span data-ttu-id="754ae-119">To filter by a resource type, use a value in following format: `/subscriptions/<subscription-id>/resourcegroups/<resource-group>/providers/Microsoft.Compute/virtualMachines`</span><span class="sxs-lookup"><span data-stu-id="754ae-119">To filter by a resource type, use a value in following format: `/subscriptions/<subscription-id>/resourcegroups/<resource-group>/providers/Microsoft.Compute/virtualMachines`</span></span>

<span data-ttu-id="754ae-120">For a list of sample scripts and tutorials, see [Resource group event source](event-sources.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="754ae-120">For a list of sample scripts and tutorials, see [Resource group event source](event-sources.md#resource-groups).</span></span>

## <a name="available-event-types"></a><span data-ttu-id="754ae-121">Available event types</span><span class="sxs-lookup"><span data-stu-id="754ae-121">Available event types</span></span>

<span data-ttu-id="754ae-122">Resource groups emit management events from Azure Resource Manager, such as when a VM is created or a storage account is deleted.</span><span class="sxs-lookup"><span data-stu-id="754ae-122">Resource groups emit management events from Azure Resource Manager, such as when a VM is created or a storage account is deleted.</span></span>

| <span data-ttu-id="754ae-123">Event type</span><span class="sxs-lookup"><span data-stu-id="754ae-123">Event type</span></span> | <span data-ttu-id="754ae-124">Description</span><span class="sxs-lookup"><span data-stu-id="754ae-124">Description</span></span> |
| ---------- | ----------- |
| <span data-ttu-id="754ae-125">Microsoft.Resources.ResourceWriteSuccess</span><span class="sxs-lookup"><span data-stu-id="754ae-125">Microsoft.Resources.ResourceWriteSuccess</span></span> | <span data-ttu-id="754ae-126">Raised when a resource create or update operation succeeds.</span><span class="sxs-lookup"><span data-stu-id="754ae-126">Raised when a resource create or update operation succeeds.</span></span> |
| <span data-ttu-id="754ae-127">Microsoft.Resources.ResourceWriteFailure</span><span class="sxs-lookup"><span data-stu-id="754ae-127">Microsoft.Resources.ResourceWriteFailure</span></span> | <span data-ttu-id="754ae-128">Raised when a resource create or update operation fails.</span><span class="sxs-lookup"><span data-stu-id="754ae-128">Raised when a resource create or update operation fails.</span></span> |
| <span data-ttu-id="754ae-129">Microsoft.Resources.ResourceWriteCancel</span><span class="sxs-lookup"><span data-stu-id="754ae-129">Microsoft.Resources.ResourceWriteCancel</span></span> | <span data-ttu-id="754ae-130">Raised when a resource create or update operation is canceled.</span><span class="sxs-lookup"><span data-stu-id="754ae-130">Raised when a resource create or update operation is canceled.</span></span> |
| <span data-ttu-id="754ae-131">Microsoft.Resources.ResourceDeleteSuccess</span><span class="sxs-lookup"><span data-stu-id="754ae-131">Microsoft.Resources.ResourceDeleteSuccess</span></span> | <span data-ttu-id="754ae-132">Raised when a resource delete operation succeeds.</span><span class="sxs-lookup"><span data-stu-id="754ae-132">Raised when a resource delete operation succeeds.</span></span> |
| <span data-ttu-id="754ae-133">Microsoft.Resources.ResourceDeleteFailure</span><span class="sxs-lookup"><span data-stu-id="754ae-133">Microsoft.Resources.ResourceDeleteFailure</span></span> | <span data-ttu-id="754ae-134">Raised when a resource delete operation fails.</span><span class="sxs-lookup"><span data-stu-id="754ae-134">Raised when a resource delete operation fails.</span></span> |
| <span data-ttu-id="754ae-135">Microsoft.Resources.ResourceDeleteCancel</span><span class="sxs-lookup"><span data-stu-id="754ae-135">Microsoft.Resources.ResourceDeleteCancel</span></span> | <span data-ttu-id="754ae-136">Raised when a resource delete operation is canceled.</span><span class="sxs-lookup"><span data-stu-id="754ae-136">Raised when a resource delete operation is canceled.</span></span> <span data-ttu-id="754ae-137">This event happens when a template deployment is canceled.</span><span class="sxs-lookup"><span data-stu-id="754ae-137">This event happens when a template deployment is canceled.</span></span> |

## <a name="example-event"></a><span data-ttu-id="754ae-138">Example event</span><span class="sxs-lookup"><span data-stu-id="754ae-138">Example event</span></span>

<span data-ttu-id="754ae-139">The following example shows the schema for a **ResourceWriteSuccess** event.</span><span class="sxs-lookup"><span data-stu-id="754ae-139">The following example shows the schema for a **ResourceWriteSuccess** event.</span></span> <span data-ttu-id="754ae-140">The same schema is used for **ResourceWriteFailure** and **ResourceWriteCancel** events with different values for `eventType`.</span><span class="sxs-lookup"><span data-stu-id="754ae-140">The same schema is used for **ResourceWriteFailure** and **ResourceWriteCancel** events with different values for `eventType`.</span></span>

```json
[{
  "subject": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
  "eventType": "Microsoft.Resources.ResourceWriteSuccess",
  "eventTime": "2018-07-19T18:38:04.6117357Z",
  "id": "4db48cba-50a2-455a-93b4-de41a3b5b7f6",
  "data": {
    "authorization": {
      "scope": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
      "action": "Microsoft.Storage/storageAccounts/write",
      "evidence": {
        "role": "Subscription Admin"
      }
    },
    "claims": {
      "aud": "{audience-claim}",
      "iss": "{issuer-claim}",
      "iat": "{issued-at-claim}",
      "nbf": "{not-before-claim}",
      "exp": "{expiration-claim}",
      "_claim_names": "{\"groups\":\"src1\"}",
      "_claim_sources": "{\"src1\":{\"endpoint\":\"{URI}\"}}",
      "http://schemas.microsoft.com/claims/authnclassreference": "1",
      "aio": "{token}",
      "http://schemas.microsoft.com/claims/authnmethodsreferences": "rsa,mfa",
      "appid": "{ID}",
      "appidacr": "2",
      "http://schemas.microsoft.com/2012/01/devicecontext/claims/identifier": "{ID}",
      "e_exp": "{expiration}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "{last-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "{first-name}",
      "ipaddr": "{IP-address}",
      "name": "{full-name}",
      "http://schemas.microsoft.com/identity/claims/objectidentifier": "{ID}",
      "onprem_sid": "{ID}",
      "puid": "{ID}",
      "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "{ID}",
      "http://schemas.microsoft.com/identity/claims/tenantid": "{ID}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": "{user-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "{user-name}",
      "uti": "{ID}",
      "ver": "1.0"
    },
    "correlationId": "{ID}",
    "resourceProvider": "Microsoft.Storage",
    "resourceUri": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
    "operationName": "Microsoft.Storage/storageAccounts/write",
    "status": "Succeeded",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}"
  },
  "dataVersion": "2",
  "metadataVersion": "1",
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}"
}]
```

<span data-ttu-id="754ae-141">The following example shows the schema for a **ResourceDeleteSuccess** event.</span><span class="sxs-lookup"><span data-stu-id="754ae-141">The following example shows the schema for a **ResourceDeleteSuccess** event.</span></span> <span data-ttu-id="754ae-142">The same schema is used for **ResourceDeleteFailure** and **ResourceDeleteCancel** events with different values for `eventType`.</span><span class="sxs-lookup"><span data-stu-id="754ae-142">The same schema is used for **ResourceDeleteFailure** and **ResourceDeleteCancel** events with different values for `eventType`.</span></span>

```json
[{
  "subject": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
  "eventType": "Microsoft.Resources.ResourceDeleteSuccess",
  "eventTime": "2018-07-19T19:24:12.763881Z",
  "id": "19a69642-1aad-4a96-a5ab-8d05494513ce",
  "data": {
    "authorization": {
      "scope": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
      "action": "Microsoft.Storage/storageAccounts/delete",
      "evidence": {
        "role": "Subscription Admin"
      }
    },
    "claims": {
      "aud": "{audience-claim}",
      "iss": "{issuer-claim}",
      "iat": "{issued-at-claim}",
      "nbf": "{not-before-claim}",
      "exp": "{expiration-claim}",
      "_claim_names": "{\"groups\":\"src1\"}",
      "_claim_sources": "{\"src1\":{\"endpoint\":\"{URI}\"}}",
      "http://schemas.microsoft.com/claims/authnclassreference": "1",
      "aio": "{token}",
      "http://schemas.microsoft.com/claims/authnmethodsreferences": "rsa,mfa",
      "appid": "{ID}",
      "appidacr": "2",
      "http://schemas.microsoft.com/2012/01/devicecontext/claims/identifier": "{ID}",
      "e_exp": "262800",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "{last-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "{first-name}",
      "ipaddr": "{IP-address}",
      "name": "{full-name}",
      "http://schemas.microsoft.com/identity/claims/objectidentifier": "{ID}",
      "onprem_sid": "{ID}",
      "puid": "{ID}",
      "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "{ID}",
      "http://schemas.microsoft.com/identity/claims/tenantid": "{ID}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": "{user-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "{user-name}",
      "uti": "{ID}",
      "ver": "1.0"
    },
    "correlationId": "{ID}",
    "httpRequest": {
      "clientRequestId": "{ID}",
      "clientIpAddress": "{IP-address}",
      "method": "DELETE",
      "url": "https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2018-02-01"
    },
    "resourceProvider": "Microsoft.Storage",
    "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
    "operationName": "Microsoft.Storage/storageAccounts/delete",
    "status": "Succeeded",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}"
  },
  "dataVersion": "2",
  "metadataVersion": "1",
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}"
}]
```

## <a name="event-properties"></a><span data-ttu-id="754ae-143">Event properties</span><span class="sxs-lookup"><span data-stu-id="754ae-143">Event properties</span></span>

<span data-ttu-id="754ae-144">An event has the following top-level data:</span><span class="sxs-lookup"><span data-stu-id="754ae-144">An event has the following top-level data:</span></span>

| <span data-ttu-id="754ae-145">Property</span><span class="sxs-lookup"><span data-stu-id="754ae-145">Property</span></span> | <span data-ttu-id="754ae-146">Type</span><span class="sxs-lookup"><span data-stu-id="754ae-146">Type</span></span> | <span data-ttu-id="754ae-147">Description</span><span class="sxs-lookup"><span data-stu-id="754ae-147">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="754ae-148">topic</span><span class="sxs-lookup"><span data-stu-id="754ae-148">topic</span></span> | <span data-ttu-id="754ae-149">string</span><span class="sxs-lookup"><span data-stu-id="754ae-149">string</span></span> | <span data-ttu-id="754ae-150">Full resource path to the event source.</span><span class="sxs-lookup"><span data-stu-id="754ae-150">Full resource path to the event source.</span></span> <span data-ttu-id="754ae-151">This field is not writeable.</span><span class="sxs-lookup"><span data-stu-id="754ae-151">This field is not writeable.</span></span> <span data-ttu-id="754ae-152">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="754ae-152">Event Grid provides this value.</span></span> |
| <span data-ttu-id="754ae-153">subject</span><span class="sxs-lookup"><span data-stu-id="754ae-153">subject</span></span> | <span data-ttu-id="754ae-154">string</span><span class="sxs-lookup"><span data-stu-id="754ae-154">string</span></span> | <span data-ttu-id="754ae-155">Publisher-defined path to the event subject.</span><span class="sxs-lookup"><span data-stu-id="754ae-155">Publisher-defined path to the event subject.</span></span> |
| <span data-ttu-id="754ae-156">eventType</span><span class="sxs-lookup"><span data-stu-id="754ae-156">eventType</span></span> | <span data-ttu-id="754ae-157">string</span><span class="sxs-lookup"><span data-stu-id="754ae-157">string</span></span> | <span data-ttu-id="754ae-158">One of the registered event types for this event source.</span><span class="sxs-lookup"><span data-stu-id="754ae-158">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="754ae-159">eventTime</span><span class="sxs-lookup"><span data-stu-id="754ae-159">eventTime</span></span> | <span data-ttu-id="754ae-160">string</span><span class="sxs-lookup"><span data-stu-id="754ae-160">string</span></span> | <span data-ttu-id="754ae-161">The time the event is generated based on the provider's UTC time.</span><span class="sxs-lookup"><span data-stu-id="754ae-161">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="754ae-162">id</span><span class="sxs-lookup"><span data-stu-id="754ae-162">id</span></span> | <span data-ttu-id="754ae-163">string</span><span class="sxs-lookup"><span data-stu-id="754ae-163">string</span></span> | <span data-ttu-id="754ae-164">Unique identifier for the event.</span><span class="sxs-lookup"><span data-stu-id="754ae-164">Unique identifier for the event.</span></span> |
| <span data-ttu-id="754ae-165">data</span><span class="sxs-lookup"><span data-stu-id="754ae-165">data</span></span> | <span data-ttu-id="754ae-166">object</span><span class="sxs-lookup"><span data-stu-id="754ae-166">object</span></span> | <span data-ttu-id="754ae-167">Resource group event data.</span><span class="sxs-lookup"><span data-stu-id="754ae-167">Resource group event data.</span></span> |
| <span data-ttu-id="754ae-168">dataVersion</span><span class="sxs-lookup"><span data-stu-id="754ae-168">dataVersion</span></span> | <span data-ttu-id="754ae-169">string</span><span class="sxs-lookup"><span data-stu-id="754ae-169">string</span></span> | <span data-ttu-id="754ae-170">The schema version of the data object.</span><span class="sxs-lookup"><span data-stu-id="754ae-170">The schema version of the data object.</span></span> <span data-ttu-id="754ae-171">The publisher defines the schema version.</span><span class="sxs-lookup"><span data-stu-id="754ae-171">The publisher defines the schema version.</span></span> |
| <span data-ttu-id="754ae-172">metadataVersion</span><span class="sxs-lookup"><span data-stu-id="754ae-172">metadataVersion</span></span> | <span data-ttu-id="754ae-173">string</span><span class="sxs-lookup"><span data-stu-id="754ae-173">string</span></span> | <span data-ttu-id="754ae-174">The schema version of the event metadata.</span><span class="sxs-lookup"><span data-stu-id="754ae-174">The schema version of the event metadata.</span></span> <span data-ttu-id="754ae-175">Event Grid defines the schema of the top-level properties.</span><span class="sxs-lookup"><span data-stu-id="754ae-175">Event Grid defines the schema of the top-level properties.</span></span> <span data-ttu-id="754ae-176">Event Grid provides this value.</span><span class="sxs-lookup"><span data-stu-id="754ae-176">Event Grid provides this value.</span></span> |

<span data-ttu-id="754ae-177">The data object has the following properties:</span><span class="sxs-lookup"><span data-stu-id="754ae-177">The data object has the following properties:</span></span>

| <span data-ttu-id="754ae-178">Property</span><span class="sxs-lookup"><span data-stu-id="754ae-178">Property</span></span> | <span data-ttu-id="754ae-179">Type</span><span class="sxs-lookup"><span data-stu-id="754ae-179">Type</span></span> | <span data-ttu-id="754ae-180">Description</span><span class="sxs-lookup"><span data-stu-id="754ae-180">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="754ae-181">authorization</span><span class="sxs-lookup"><span data-stu-id="754ae-181">authorization</span></span> | <span data-ttu-id="754ae-182">object</span><span class="sxs-lookup"><span data-stu-id="754ae-182">object</span></span> | <span data-ttu-id="754ae-183">The requested authorization for the operation.</span><span class="sxs-lookup"><span data-stu-id="754ae-183">The requested authorization for the operation.</span></span> |
| <span data-ttu-id="754ae-184">claims</span><span class="sxs-lookup"><span data-stu-id="754ae-184">claims</span></span> | <span data-ttu-id="754ae-185">object</span><span class="sxs-lookup"><span data-stu-id="754ae-185">object</span></span> | <span data-ttu-id="754ae-186">The properties of the claims.</span><span class="sxs-lookup"><span data-stu-id="754ae-186">The properties of the claims.</span></span> <span data-ttu-id="754ae-187">For more information, see [JWT specification](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).</span><span class="sxs-lookup"><span data-stu-id="754ae-187">For more information, see [JWT specification](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).</span></span> |
| <span data-ttu-id="754ae-188">correlationId</span><span class="sxs-lookup"><span data-stu-id="754ae-188">correlationId</span></span> | <span data-ttu-id="754ae-189">string</span><span class="sxs-lookup"><span data-stu-id="754ae-189">string</span></span> | <span data-ttu-id="754ae-190">An operation ID for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="754ae-190">An operation ID for troubleshooting.</span></span> |
| <span data-ttu-id="754ae-191">httpRequest</span><span class="sxs-lookup"><span data-stu-id="754ae-191">httpRequest</span></span> | <span data-ttu-id="754ae-192">object</span><span class="sxs-lookup"><span data-stu-id="754ae-192">object</span></span> | <span data-ttu-id="754ae-193">The details of the operation.</span><span class="sxs-lookup"><span data-stu-id="754ae-193">The details of the operation.</span></span> <span data-ttu-id="754ae-194">This object is only included when updating an existing resource or deleting a resource.</span><span class="sxs-lookup"><span data-stu-id="754ae-194">This object is only included when updating an existing resource or deleting a resource.</span></span> |
| <span data-ttu-id="754ae-195">resourceProvider</span><span class="sxs-lookup"><span data-stu-id="754ae-195">resourceProvider</span></span> | <span data-ttu-id="754ae-196">string</span><span class="sxs-lookup"><span data-stu-id="754ae-196">string</span></span> | <span data-ttu-id="754ae-197">The resource provider performing the operation.</span><span class="sxs-lookup"><span data-stu-id="754ae-197">The resource provider performing the operation.</span></span> |
| <span data-ttu-id="754ae-198">resourceUri</span><span class="sxs-lookup"><span data-stu-id="754ae-198">resourceUri</span></span> | <span data-ttu-id="754ae-199">string</span><span class="sxs-lookup"><span data-stu-id="754ae-199">string</span></span> | <span data-ttu-id="754ae-200">The URI of the resource in the operation.</span><span class="sxs-lookup"><span data-stu-id="754ae-200">The URI of the resource in the operation.</span></span> |
| <span data-ttu-id="754ae-201">operationName</span><span class="sxs-lookup"><span data-stu-id="754ae-201">operationName</span></span> | <span data-ttu-id="754ae-202">string</span><span class="sxs-lookup"><span data-stu-id="754ae-202">string</span></span> | <span data-ttu-id="754ae-203">The operation that was performed.</span><span class="sxs-lookup"><span data-stu-id="754ae-203">The operation that was performed.</span></span> |
| <span data-ttu-id="754ae-204">status</span><span class="sxs-lookup"><span data-stu-id="754ae-204">status</span></span> | <span data-ttu-id="754ae-205">string</span><span class="sxs-lookup"><span data-stu-id="754ae-205">string</span></span> | <span data-ttu-id="754ae-206">The status of the operation.</span><span class="sxs-lookup"><span data-stu-id="754ae-206">The status of the operation.</span></span> |
| <span data-ttu-id="754ae-207">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="754ae-207">subscriptionId</span></span> | <span data-ttu-id="754ae-208">string</span><span class="sxs-lookup"><span data-stu-id="754ae-208">string</span></span> | <span data-ttu-id="754ae-209">The subscription ID of the resource.</span><span class="sxs-lookup"><span data-stu-id="754ae-209">The subscription ID of the resource.</span></span> |
| <span data-ttu-id="754ae-210">tenantId</span><span class="sxs-lookup"><span data-stu-id="754ae-210">tenantId</span></span> | <span data-ttu-id="754ae-211">string</span><span class="sxs-lookup"><span data-stu-id="754ae-211">string</span></span> | <span data-ttu-id="754ae-212">The tenant ID of the resource.</span><span class="sxs-lookup"><span data-stu-id="754ae-212">The tenant ID of the resource.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="754ae-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="754ae-213">Next steps</span></span>

* <span data-ttu-id="754ae-214">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="754ae-214">For an introduction to Azure Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="754ae-215">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="754ae-215">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
