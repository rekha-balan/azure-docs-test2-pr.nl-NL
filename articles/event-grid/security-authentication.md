---
title: Azure Event Grid security and authentication
description: Describes Azure Event Grid and its concepts.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: conceptual
ms.date: 08/13/2018
ms.author: babanisa
ms.openlocfilehash: ce0e766a07fd19f523f1f35b9a3cbc865cfb8c71
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866138"
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="8b70d-103">Event Grid security and authentication</span><span class="sxs-lookup"><span data-stu-id="8b70d-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="8b70d-104">Azure Event Grid has three types of authentication:</span><span class="sxs-lookup"><span data-stu-id="8b70d-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="8b70d-105">Event subscriptions</span><span class="sxs-lookup"><span data-stu-id="8b70d-105">Event subscriptions</span></span>
* <span data-ttu-id="8b70d-106">Event publishing</span><span class="sxs-lookup"><span data-stu-id="8b70d-106">Event publishing</span></span>
* <span data-ttu-id="8b70d-107">WebHook event delivery</span><span class="sxs-lookup"><span data-stu-id="8b70d-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="8b70d-108">WebHook Event delivery</span><span class="sxs-lookup"><span data-stu-id="8b70d-108">WebHook Event delivery</span></span>

<span data-ttu-id="8b70d-109">Webhooks are one of the many ways to receive events from Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="8b70d-109">Webhooks are one of the many ways to receive events from Azure Event Grid.</span></span> <span data-ttu-id="8b70d-110">When a new event is ready, EventGrid service POSTs an HTTP request to the configured endpoint with the event in the request body.</span><span class="sxs-lookup"><span data-stu-id="8b70d-110">When a new event is ready, EventGrid service POSTs an HTTP request to the configured endpoint with the event in the request body.</span></span>

<span data-ttu-id="8b70d-111">Like many other services that support webhooks, EventGrid requires you to prove "ownership" of your Webhook endpoint before it starts delivering events to that endpoint.</span><span class="sxs-lookup"><span data-stu-id="8b70d-111">Like many other services that support webhooks, EventGrid requires you to prove "ownership" of your Webhook endpoint before it starts delivering events to that endpoint.</span></span> <span data-ttu-id="8b70d-112">This requirement is to prevent an unsuspecting endpoint from becoming the target endpoint for event delivery from EventGrid.</span><span class="sxs-lookup"><span data-stu-id="8b70d-112">This requirement is to prevent an unsuspecting endpoint from becoming the target endpoint for event delivery from EventGrid.</span></span> <span data-ttu-id="8b70d-113">However, when you use any of the three Azure services listed below, the Azure infrastructure automatically handles this validation:</span><span class="sxs-lookup"><span data-stu-id="8b70d-113">However, when you use any of the three Azure services listed below, the Azure infrastructure automatically handles this validation:</span></span>

* <span data-ttu-id="8b70d-114">Azure Logic Apps,</span><span class="sxs-lookup"><span data-stu-id="8b70d-114">Azure Logic Apps,</span></span>
* <span data-ttu-id="8b70d-115">Azure Automation,</span><span class="sxs-lookup"><span data-stu-id="8b70d-115">Azure Automation,</span></span>
* <span data-ttu-id="8b70d-116">Azure Functions for EventGrid Trigger.</span><span class="sxs-lookup"><span data-stu-id="8b70d-116">Azure Functions for EventGrid Trigger.</span></span>

<span data-ttu-id="8b70d-117">If you're using any other type of endpoint, such as an HTTP trigger based Azure function, your endpoint code needs to participate in a validation handshake with EventGrid.</span><span class="sxs-lookup"><span data-stu-id="8b70d-117">If you're using any other type of endpoint, such as an HTTP trigger based Azure function, your endpoint code needs to participate in a validation handshake with EventGrid.</span></span> <span data-ttu-id="8b70d-118">EventGrid supports two different validation handshake models:</span><span class="sxs-lookup"><span data-stu-id="8b70d-118">EventGrid supports two different validation handshake models:</span></span>

1. <span data-ttu-id="8b70d-119">**ValidationCode handshake**: At the time of event subscription creation, EventGrid POSTs a "subscription validation event" to your endpoint.</span><span class="sxs-lookup"><span data-stu-id="8b70d-119">**ValidationCode handshake**: At the time of event subscription creation, EventGrid POSTs a "subscription validation event" to your endpoint.</span></span> <span data-ttu-id="8b70d-120">The schema of this event is similar to any other EventGridEvent, and the data portion of this event includes a `validationCode` property.</span><span class="sxs-lookup"><span data-stu-id="8b70d-120">The schema of this event is similar to any other EventGridEvent, and the data portion of this event includes a `validationCode` property.</span></span> <span data-ttu-id="8b70d-121">Once your application has verified that the validation request is for an expected event subscription, your application code needs to respond by echoing back the validation code to EventGrid.</span><span class="sxs-lookup"><span data-stu-id="8b70d-121">Once your application has verified that the validation request is for an expected event subscription, your application code needs to respond by echoing back the validation code to EventGrid.</span></span> <span data-ttu-id="8b70d-122">This handshake mechanism is supported in all EventGrid versions.</span><span class="sxs-lookup"><span data-stu-id="8b70d-122">This handshake mechanism is supported in all EventGrid versions.</span></span>

2. <span data-ttu-id="8b70d-123">**ValidationURL handshake (Manual handshake)**: In certain cases, you may not have control of the source code of the endpoint to be able to implement the ValidationCode based handshake.</span><span class="sxs-lookup"><span data-stu-id="8b70d-123">**ValidationURL handshake (Manual handshake)**: In certain cases, you may not have control of the source code of the endpoint to be able to implement the ValidationCode based handshake.</span></span> <span data-ttu-id="8b70d-124">For example, if you use a third-party service (like [Zapier](https://zapier.com) or [IFTTT](https://ifttt.com/)), you might not be able to programmatically respond back with the validation code.</span><span class="sxs-lookup"><span data-stu-id="8b70d-124">For example, if you use a third-party service (like [Zapier](https://zapier.com) or [IFTTT](https://ifttt.com/)), you might not be able to programmatically respond back with the validation code.</span></span> <span data-ttu-id="8b70d-125">Hence, starting with version 2018-05-01-preview, EventGrid now supports a manual validation handshake.</span><span class="sxs-lookup"><span data-stu-id="8b70d-125">Hence, starting with version 2018-05-01-preview, EventGrid now supports a manual validation handshake.</span></span> <span data-ttu-id="8b70d-126">If you are creating an event subscription using SDK/tools that use this new API version (2018-05-01-preview), EventGrid sends a `validationUrl` property (in addition to the `validationCode` property) as part of the data portion of the subscription validation event.</span><span class="sxs-lookup"><span data-stu-id="8b70d-126">If you are creating an event subscription using SDK/tools that use this new API version (2018-05-01-preview), EventGrid sends a `validationUrl` property (in addition to the `validationCode` property) as part of the data portion of the subscription validation event.</span></span> <span data-ttu-id="8b70d-127">To complete the handshake, just do a GET request on that URL, either through a REST client or using your web browser.</span><span class="sxs-lookup"><span data-stu-id="8b70d-127">To complete the handshake, just do a GET request on that URL, either through a REST client or using your web browser.</span></span> <span data-ttu-id="8b70d-128">The provided validation URL is valid only for about 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="8b70d-128">The provided validation URL is valid only for about 10 minutes.</span></span> <span data-ttu-id="8b70d-129">During that time, the provisioning state of the event subscription is `AwaitingManualAction`.</span><span class="sxs-lookup"><span data-stu-id="8b70d-129">During that time, the provisioning state of the event subscription is `AwaitingManualAction`.</span></span> <span data-ttu-id="8b70d-130">If you don't complete the manual validation within 10 minutes, the provisioning state is set to `Failed`.</span><span class="sxs-lookup"><span data-stu-id="8b70d-130">If you don't complete the manual validation within 10 minutes, the provisioning state is set to `Failed`.</span></span> <span data-ttu-id="8b70d-131">You will have to reattempt the creation of the event subscription before you attempt to do the manual validation again.</span><span class="sxs-lookup"><span data-stu-id="8b70d-131">You will have to reattempt the creation of the event subscription before you attempt to do the manual validation again.</span></span>

<span data-ttu-id="8b70d-132">This mechanism of manual validation is in preview.</span><span class="sxs-lookup"><span data-stu-id="8b70d-132">This mechanism of manual validation is in preview.</span></span> <span data-ttu-id="8b70d-133">To use it, you must install the [Event Grid extension](/cli/azure/azure-cli-extensions-list) for [AZ CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8b70d-133">To use it, you must install the [Event Grid extension](/cli/azure/azure-cli-extensions-list) for [AZ CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="8b70d-134">You can install it with `az extension add --name eventgrid`.</span><span class="sxs-lookup"><span data-stu-id="8b70d-134">You can install it with `az extension add --name eventgrid`.</span></span> <span data-ttu-id="8b70d-135">If you are using the REST API, ensure you are using `api-version=2018-05-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="8b70d-135">If you are using the REST API, ensure you are using `api-version=2018-05-01-preview`.</span></span>

### <a name="validation-details"></a><span data-ttu-id="8b70d-136">Validation details</span><span class="sxs-lookup"><span data-stu-id="8b70d-136">Validation details</span></span>

* <span data-ttu-id="8b70d-137">At the time of event subscription creation/update, Event Grid posts a Subscription Validation Event to the target endpoint.</span><span class="sxs-lookup"><span data-stu-id="8b70d-137">At the time of event subscription creation/update, Event Grid posts a Subscription Validation Event to the target endpoint.</span></span> 
* <span data-ttu-id="8b70d-138">The event contains a header value "aeg-event-type: SubscriptionValidation".</span><span class="sxs-lookup"><span data-stu-id="8b70d-138">The event contains a header value "aeg-event-type: SubscriptionValidation".</span></span>
* <span data-ttu-id="8b70d-139">The event body has the same schema as other Event Grid events.</span><span class="sxs-lookup"><span data-stu-id="8b70d-139">The event body has the same schema as other Event Grid events.</span></span>
* <span data-ttu-id="8b70d-140">The eventType property of the event is "Microsoft.EventGrid.SubscriptionValidationEvent".</span><span class="sxs-lookup"><span data-stu-id="8b70d-140">The eventType property of the event is "Microsoft.EventGrid.SubscriptionValidationEvent".</span></span>
* <span data-ttu-id="8b70d-141">The data property of the event includes a "validationCode" property with a randomly generated string.</span><span class="sxs-lookup"><span data-stu-id="8b70d-141">The data property of the event includes a "validationCode" property with a randomly generated string.</span></span> <span data-ttu-id="8b70d-142">For example, "validationCode: acb13…".</span><span class="sxs-lookup"><span data-stu-id="8b70d-142">For example, "validationCode: acb13…".</span></span>
* <span data-ttu-id="8b70d-143">If you are using API version 2018-05-01-preview, the event data also includes a `validationUrl` property with a URL for manually validating the subscription.</span><span class="sxs-lookup"><span data-stu-id="8b70d-143">If you are using API version 2018-05-01-preview, the event data also includes a `validationUrl` property with a URL for manually validating the subscription.</span></span>
* <span data-ttu-id="8b70d-144">The array contains only the validation event.</span><span class="sxs-lookup"><span data-stu-id="8b70d-144">The array contains only the validation event.</span></span> <span data-ttu-id="8b70d-145">Other events are sent in a separate request after you echo back the validation code.</span><span class="sxs-lookup"><span data-stu-id="8b70d-145">Other events are sent in a separate request after you echo back the validation code.</span></span>
* <span data-ttu-id="8b70d-146">The EventGrid DataPlane SDKs have classes corresponding to the subscription validation event data and subscription validation response.</span><span class="sxs-lookup"><span data-stu-id="8b70d-146">The EventGrid DataPlane SDKs have classes corresponding to the subscription validation event data and subscription validation response.</span></span>

<span data-ttu-id="8b70d-147">An example SubscriptionValidationEvent is shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8b70d-147">An example SubscriptionValidationEvent is shown in the following example:</span></span>

```json
[{
  "id": "2d1781af-3a4c-4d7c-bd0c-e34b19da4e66",
  "topic": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "subject": "",
  "data": {
    "validationCode": "512d38b6-c7b8-40c8-89fe-f46f9e9622b6",
    "validationUrl": "https://rp-eastus2.eventgrid.azure.net:553/eventsubscriptions/estest/validate?id=B2E34264-7D71-453A-B5FB-B62D0FDC85EE&t=2018-04-26T20:30:54.4538837Z&apiVersion=2018-05-01-preview&token=1BNqCxBBSSE9OnNSfZM4%2b5H9zDegKMY6uJ%2fO2DFRkwQ%3d"
  },
  "eventType": "Microsoft.EventGrid.SubscriptionValidationEvent",
  "eventTime": "2018-01-25T22:12:19.4556811Z",
  "metadataVersion": "1",
  "dataVersion": "1"
}]
```

<span data-ttu-id="8b70d-148">To prove endpoint ownership, echo back the validation code in the validationResponse property, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="8b70d-148">To prove endpoint ownership, echo back the validation code in the validationResponse property, as shown in the following example:</span></span>

```json
{
  "validationResponse": "512d38b6-c7b8-40c8-89fe-f46f9e9622b6"
}
```

<span data-ttu-id="8b70d-149">Alternatively, you can manually validate the subscription by sending a GET request to the validation URL.</span><span class="sxs-lookup"><span data-stu-id="8b70d-149">Alternatively, you can manually validate the subscription by sending a GET request to the validation URL.</span></span> <span data-ttu-id="8b70d-150">The event subscription stays in a pending state until validated.</span><span class="sxs-lookup"><span data-stu-id="8b70d-150">The event subscription stays in a pending state until validated.</span></span>

<span data-ttu-id="8b70d-151">You can find C# Sample that shows how to handle the subscription validation handshake at https://github.com/Azure-Samples/event-grid-dotnet-publish-consume-events/blob/master/EventGridConsumer/EventGridConsumer/Function1.cs.</span><span class="sxs-lookup"><span data-stu-id="8b70d-151">You can find C# Sample that shows how to handle the subscription validation handshake at https://github.com/Azure-Samples/event-grid-dotnet-publish-consume-events/blob/master/EventGridConsumer/EventGridConsumer/Function1.cs.</span></span>

### <a name="checklist"></a><span data-ttu-id="8b70d-152">Checklist</span><span class="sxs-lookup"><span data-stu-id="8b70d-152">Checklist</span></span>

<span data-ttu-id="8b70d-153">During event subscription creation, if you are seeing an error message such as "The attempt to validate the provided endpoint https://your-endpoint-here failed.</span><span class="sxs-lookup"><span data-stu-id="8b70d-153">During event subscription creation, if you are seeing an error message such as "The attempt to validate the provided endpoint https://your-endpoint-here failed.</span></span> <span data-ttu-id="8b70d-154">For more details, visit https://aka.ms/esvalidation", it indicates that there's a failure in the validation handshake.</span><span class="sxs-lookup"><span data-stu-id="8b70d-154">For more details, visit https://aka.ms/esvalidation", it indicates that there's a failure in the validation handshake.</span></span> <span data-ttu-id="8b70d-155">To resolve this error, verify the following aspects:</span><span class="sxs-lookup"><span data-stu-id="8b70d-155">To resolve this error, verify the following aspects:</span></span>

* <span data-ttu-id="8b70d-156">Do you have control of the application code in the target endpoint?</span><span class="sxs-lookup"><span data-stu-id="8b70d-156">Do you have control of the application code in the target endpoint?</span></span> <span data-ttu-id="8b70d-157">For example, if you are writing an HTTP trigger based Azure Function, do you have access to the application code to make changes to it?</span><span class="sxs-lookup"><span data-stu-id="8b70d-157">For example, if you are writing an HTTP trigger based Azure Function, do you have access to the application code to make changes to it?</span></span>
* <span data-ttu-id="8b70d-158">If you have access to the application code, please implement the ValidationCode based handshake mechanism as shown in the sample above.</span><span class="sxs-lookup"><span data-stu-id="8b70d-158">If you have access to the application code, please implement the ValidationCode based handshake mechanism as shown in the sample above.</span></span>

* <span data-ttu-id="8b70d-159">If you don't have access to the application code (e.g. if you are using a third party service that supports webhooks), you can use the manual handshake mechanism.</span><span class="sxs-lookup"><span data-stu-id="8b70d-159">If you don't have access to the application code (e.g. if you are using a third party service that supports webhooks), you can use the manual handshake mechanism.</span></span> <span data-ttu-id="8b70d-160">In order to do this, ensure you are using the 2018-05-01-preview API version (e.g. using the EventGrid CLI extension described above) in order to receive the validationUrl in the validation event.</span><span class="sxs-lookup"><span data-stu-id="8b70d-160">In order to do this, ensure you are using the 2018-05-01-preview API version (e.g. using the EventGrid CLI extension described above) in order to receive the validationUrl in the validation event.</span></span> <span data-ttu-id="8b70d-161">To complete the manual validation handshake, get the value of the "validationUrl" property and visit that URL in your web browser.</span><span class="sxs-lookup"><span data-stu-id="8b70d-161">To complete the manual validation handshake, get the value of the "validationUrl" property and visit that URL in your web browser.</span></span> <span data-ttu-id="8b70d-162">If validation is successful, you should see a message in your web browser that validation is successful, and you will see that event subscription's provisioningState is "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="8b70d-162">If validation is successful, you should see a message in your web browser that validation is successful, and you will see that event subscription's provisioningState is "Succeeded".</span></span> 

### <a name="event-delivery-security"></a><span data-ttu-id="8b70d-163">Event delivery security</span><span class="sxs-lookup"><span data-stu-id="8b70d-163">Event delivery security</span></span>

<span data-ttu-id="8b70d-164">You can secure your webhook endpoint by adding query parameters to the webhook URL when creating an Event Subscription.</span><span class="sxs-lookup"><span data-stu-id="8b70d-164">You can secure your webhook endpoint by adding query parameters to the webhook URL when creating an Event Subscription.</span></span> <span data-ttu-id="8b70d-165">Set one of these query parameters to be a secret such as an [access token](https://en.wikipedia.org/wiki/Access_token) which the webhook can use to recognize the event is coming from Event Grid with valid permissions.</span><span class="sxs-lookup"><span data-stu-id="8b70d-165">Set one of these query parameters to be a secret such as an [access token](https://en.wikipedia.org/wiki/Access_token) which the webhook can use to recognize the event is coming from Event Grid with valid permissions.</span></span> <span data-ttu-id="8b70d-166">Event Grid will include these query parameters in every event delivery to the webhook.</span><span class="sxs-lookup"><span data-stu-id="8b70d-166">Event Grid will include these query parameters in every event delivery to the webhook.</span></span>

<span data-ttu-id="8b70d-167">When editing the Event Subscription, the query parameters will not be displayed or returned unless the [--include-full-endpoint-url](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription?view=azure-cli-latest#az-eventgrid-event-subscription-show) parameter is used in Azure [CLI](https://docs.microsoft.com/cli/azure?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="8b70d-167">When editing the Event Subscription, the query parameters will not be displayed or returned unless the [--include-full-endpoint-url](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription?view=azure-cli-latest#az-eventgrid-event-subscription-show) parameter is used in Azure [CLI](https://docs.microsoft.com/cli/azure?view=azure-cli-latest).</span></span>

<span data-ttu-id="8b70d-168">Finally, it's important to note that Azure Event Grid only supports HTTPS webhook endpoints.</span><span class="sxs-lookup"><span data-stu-id="8b70d-168">Finally, it's important to note that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>

## <a name="event-subscription"></a><span data-ttu-id="8b70d-169">Event subscription</span><span class="sxs-lookup"><span data-stu-id="8b70d-169">Event subscription</span></span>

<span data-ttu-id="8b70d-170">To subscribe to an event, you must have the **Microsoft.EventGrid/EventSubscriptions/Write** permission on the required resource.</span><span class="sxs-lookup"><span data-stu-id="8b70d-170">To subscribe to an event, you must have the **Microsoft.EventGrid/EventSubscriptions/Write** permission on the required resource.</span></span> <span data-ttu-id="8b70d-171">You need this permission because you're writing a new subscription at the scope of the resource.</span><span class="sxs-lookup"><span data-stu-id="8b70d-171">You need this permission because you're writing a new subscription at the scope of the resource.</span></span> <span data-ttu-id="8b70d-172">The required resource differs based on whether you're subscribing to a system topic or custom topic.</span><span class="sxs-lookup"><span data-stu-id="8b70d-172">The required resource differs based on whether you're subscribing to a system topic or custom topic.</span></span> <span data-ttu-id="8b70d-173">Both types are described in this section.</span><span class="sxs-lookup"><span data-stu-id="8b70d-173">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="8b70d-174">System topics (Azure service publishers)</span><span class="sxs-lookup"><span data-stu-id="8b70d-174">System topics (Azure service publishers)</span></span>

<span data-ttu-id="8b70d-175">For system topics, you need permission to write a new event subscription at the scope of the resource publishing the event.</span><span class="sxs-lookup"><span data-stu-id="8b70d-175">For system topics, you need permission to write a new event subscription at the scope of the resource publishing the event.</span></span> <span data-ttu-id="8b70d-176">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="8b70d-176">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="8b70d-177">For example, to subscribe to an event on a storage account named **myacct**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="8b70d-177">For example, to subscribe to an event on a storage account named **myacct**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="8b70d-178">Custom topics</span><span class="sxs-lookup"><span data-stu-id="8b70d-178">Custom topics</span></span>

<span data-ttu-id="8b70d-179">For custom topics, you need permission to write a new event subscription at the scope of the event grid topic.</span><span class="sxs-lookup"><span data-stu-id="8b70d-179">For custom topics, you need permission to write a new event subscription at the scope of the event grid topic.</span></span> <span data-ttu-id="8b70d-180">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="8b70d-180">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="8b70d-181">For example, to subscribe to a custom topic named **mytopic**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="8b70d-181">For example, to subscribe to a custom topic named **mytopic**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="8b70d-182">Topic publishing</span><span class="sxs-lookup"><span data-stu-id="8b70d-182">Topic publishing</span></span>

<span data-ttu-id="8b70d-183">Topics use either Shared Access Signature (SAS) or key authentication.</span><span class="sxs-lookup"><span data-stu-id="8b70d-183">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="8b70d-184">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span><span class="sxs-lookup"><span data-stu-id="8b70d-184">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="8b70d-185">You include the authentication value in the HTTP header.</span><span class="sxs-lookup"><span data-stu-id="8b70d-185">You include the authentication value in the HTTP header.</span></span> <span data-ttu-id="8b70d-186">For SAS, use **aeg-sas-token** for the header value.</span><span class="sxs-lookup"><span data-stu-id="8b70d-186">For SAS, use **aeg-sas-token** for the header value.</span></span> <span data-ttu-id="8b70d-187">For key authentication, use **aeg-sas-key** for the header value.</span><span class="sxs-lookup"><span data-stu-id="8b70d-187">For key authentication, use **aeg-sas-key** for the header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="8b70d-188">Key authentication</span><span class="sxs-lookup"><span data-stu-id="8b70d-188">Key authentication</span></span>

<span data-ttu-id="8b70d-189">Key authentication is the simplest form of authentication.</span><span class="sxs-lookup"><span data-stu-id="8b70d-189">Key authentication is the simplest form of authentication.</span></span> <span data-ttu-id="8b70d-190">Use the format: `aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="8b70d-190">Use the format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="8b70d-191">For example, you pass a key with:</span><span class="sxs-lookup"><span data-stu-id="8b70d-191">For example, you pass a key with:</span></span>

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="8b70d-192">SAS tokens</span><span class="sxs-lookup"><span data-stu-id="8b70d-192">SAS tokens</span></span>

<span data-ttu-id="8b70d-193">SAS tokens for Event Grid include the resource, an expiration time, and a signature.</span><span class="sxs-lookup"><span data-stu-id="8b70d-193">SAS tokens for Event Grid include the resource, an expiration time, and a signature.</span></span> <span data-ttu-id="8b70d-194">The format of the SAS token is: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="8b70d-194">The format of the SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="8b70d-195">The resource is the path for the event grid topic to which you're sending events.</span><span class="sxs-lookup"><span data-stu-id="8b70d-195">The resource is the path for the event grid topic to which you're sending events.</span></span> <span data-ttu-id="8b70d-196">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="8b70d-196">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="8b70d-197">You generate the signature from a key.</span><span class="sxs-lookup"><span data-stu-id="8b70d-197">You generate the signature from a key.</span></span>

<span data-ttu-id="8b70d-198">For example, a valid **aeg-sas-token** value is:</span><span class="sxs-lookup"><span data-stu-id="8b70d-198">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
```

<span data-ttu-id="8b70d-199">The following example creates a SAS token for use with Event Grid:</span><span class="sxs-lookup"><span data-stu-id="8b70d-199">The following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    var culture = CultureInfo.CreateSpecificCulture("en-US");
    var encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString(culture));

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="8b70d-200">Management Access Control</span><span class="sxs-lookup"><span data-stu-id="8b70d-200">Management Access Control</span></span>

<span data-ttu-id="8b70d-201">Azure Event Grid allows you to control the level of access given to different users to do various management operations such as list event subscriptions, create new ones, and generate keys.</span><span class="sxs-lookup"><span data-stu-id="8b70d-201">Azure Event Grid allows you to control the level of access given to different users to do various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="8b70d-202">Event Grid uses Azure's Role Based Access Check (RBAC).</span><span class="sxs-lookup"><span data-stu-id="8b70d-202">Event Grid uses Azure's Role Based Access Check (RBAC).</span></span>

### <a name="operation-types"></a><span data-ttu-id="8b70d-203">Operation types</span><span class="sxs-lookup"><span data-stu-id="8b70d-203">Operation types</span></span>

<span data-ttu-id="8b70d-204">Azure event grid supports the following actions:</span><span class="sxs-lookup"><span data-stu-id="8b70d-204">Azure event grid supports the following actions:</span></span>

* <span data-ttu-id="8b70d-205">Microsoft.EventGrid/\*/read</span><span class="sxs-lookup"><span data-stu-id="8b70d-205">Microsoft.EventGrid/\*/read</span></span>
* <span data-ttu-id="8b70d-206">Microsoft.EventGrid/\*/write</span><span class="sxs-lookup"><span data-stu-id="8b70d-206">Microsoft.EventGrid/\*/write</span></span>
* <span data-ttu-id="8b70d-207">Microsoft.EventGrid/\*/delete</span><span class="sxs-lookup"><span data-stu-id="8b70d-207">Microsoft.EventGrid/\*/delete</span></span>
* <span data-ttu-id="8b70d-208">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="8b70d-208">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span>
* <span data-ttu-id="8b70d-209">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="8b70d-209">Microsoft.EventGrid/topics/listKeys/action</span></span>
* <span data-ttu-id="8b70d-210">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="8b70d-210">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="8b70d-211">The last three operations return potentially secret information, which gets filtered out of normal read operations.</span><span class="sxs-lookup"><span data-stu-id="8b70d-211">The last three operations return potentially secret information, which gets filtered out of normal read operations.</span></span> <span data-ttu-id="8b70d-212">It is best practice for you to restrict access to these operations.</span><span class="sxs-lookup"><span data-stu-id="8b70d-212">It is best practice for you to restrict access to these operations.</span></span> <span data-ttu-id="8b70d-213">Custom roles can be created using [Azure PowerShell](../role-based-access-control/role-assignments-powershell.md), [Azure Command-Line Interface (CLI)](../role-based-access-control/role-assignments-cli.md), and the [REST API](../role-based-access-control/role-assignments-rest.md).</span><span class="sxs-lookup"><span data-stu-id="8b70d-213">Custom roles can be created using [Azure PowerShell](../role-based-access-control/role-assignments-powershell.md), [Azure Command-Line Interface (CLI)](../role-based-access-control/role-assignments-cli.md), and the [REST API](../role-based-access-control/role-assignments-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="8b70d-214">Enforcing Role Based Access Check (RBAC)</span><span class="sxs-lookup"><span data-stu-id="8b70d-214">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="8b70d-215">Use the following steps to enforce RBAC for different users:</span><span class="sxs-lookup"><span data-stu-id="8b70d-215">Use the following steps to enforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="8b70d-216">Create a custom role definition file (.json)</span><span class="sxs-lookup"><span data-stu-id="8b70d-216">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="8b70d-217">The following are sample Event Grid role definitions that allow users to perform different sets of actions.</span><span class="sxs-lookup"><span data-stu-id="8b70d-217">The following are sample Event Grid role definitions that allow users to perform different sets of actions.</span></span>

<span data-ttu-id="8b70d-218">**EventGridReadOnlyRole.json**: Only allow read-only operations.</span><span class="sxs-lookup"><span data-stu-id="8b70d-218">**EventGridReadOnlyRole.json**: Only allow read-only operations.</span></span>

```json
{
  "Name": "Event grid read only role",
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856",
  "IsCustom": true,
  "Description": "Event grid read only role",
  "Actions": [
    "Microsoft.EventGrid/*/read"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/<Subscription Id>"
  ]
}
```

<span data-ttu-id="8b70d-219">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span><span class="sxs-lookup"><span data-stu-id="8b70d-219">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>

```json
{
  "Name": "Event grid No Delete Listkeys role",
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174",
  "IsCustom": true,
  "Description": "Event grid No Delete Listkeys role",
  "Actions": [
    "Microsoft.EventGrid/*/write",
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action"
    "Microsoft.EventGrid/topics/listkeys/action",
    "Microsoft.EventGrid/topics/regenerateKey/action"
  ],
  "NotActions": [
    "Microsoft.EventGrid/*/delete"
  ],
  "AssignableScopes": [
    "/subscriptions/<Subscription id>"
  ]
}
```

<span data-ttu-id="8b70d-220">**EventGridContributorRole.json**: Allows all event grid actions.</span><span class="sxs-lookup"><span data-stu-id="8b70d-220">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>

```json
{
  "Name": "Event grid contributor role",
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514",
  "IsCustom": true,
  "Description": "Event grid contributor role",
  "Actions": [
    "Microsoft.EventGrid/*/write",
    "Microsoft.EventGrid/*/delete",
    "Microsoft.EventGrid/topics/listkeys/action",
    "Microsoft.EventGrid/topics/regenerateKey/action",
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action"
  ],
  "NotActions": [],
  "AssignableScopes": [
    "/subscriptions/<Subscription id>"
  ]
}
```

#### <a name="create-and-assign-custom-role-with-azure-cli"></a><span data-ttu-id="8b70d-221">Create and assign custom role with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8b70d-221">Create and assign custom role with Azure CLI</span></span>

<span data-ttu-id="8b70d-222">To create a custom role, use:</span><span class="sxs-lookup"><span data-stu-id="8b70d-222">To create a custom role, use:</span></span>

```azurecli
az role definition create --role-definition @<file path>
```

<span data-ttu-id="8b70d-223">To assign the role to a user, use:</span><span class="sxs-lookup"><span data-stu-id="8b70d-223">To assign the role to a user, use:</span></span>

```azurecli
az role assignment create --assignee <user name> --role "<name of role>"
```

## <a name="next-steps"></a><span data-ttu-id="8b70d-224">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b70d-224">Next steps</span></span>

* <span data-ttu-id="8b70d-225">For an introduction to Event Grid, see [About Event Grid](overview.md)</span><span class="sxs-lookup"><span data-stu-id="8b70d-225">For an introduction to Event Grid, see [About Event Grid](overview.md)</span></span>
