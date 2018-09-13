---
title: Map custom field to Azure Event Grid schema
description: Describes how to convert your custom schema to the Azure Event Grid schema.
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: tomfitz
ms.openlocfilehash: 32f93f383ec4044afb0696fcef1705c9ed65d673
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868028"
---
# <a name="map-custom-fields-to-event-grid-schema"></a><span data-ttu-id="93f5a-103">Map custom fields to Event Grid schema</span><span class="sxs-lookup"><span data-stu-id="93f5a-103">Map custom fields to Event Grid schema</span></span>

<span data-ttu-id="93f5a-104">If your event data does not match the expected [Event Grid schema](event-schema.md), you can still use Event Grid to route event to subscribers.</span><span class="sxs-lookup"><span data-stu-id="93f5a-104">If your event data does not match the expected [Event Grid schema](event-schema.md), you can still use Event Grid to route event to subscribers.</span></span> <span data-ttu-id="93f5a-105">This article describes how to map your schema to the Event Grid schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-105">This article describes how to map your schema to the Event Grid schema.</span></span>

[!INCLUDE [event-grid-preview-feature-note.md](../../includes/event-grid-preview-feature-note.md)]

## <a name="original-event-schema"></a><span data-ttu-id="93f5a-106">Original event schema</span><span class="sxs-lookup"><span data-stu-id="93f5a-106">Original event schema</span></span>

<span data-ttu-id="93f5a-107">Let's suppose you have an application that sends events in the following format:</span><span class="sxs-lookup"><span data-stu-id="93f5a-107">Let's suppose you have an application that sends events in the following format:</span></span>

```json
[
  {
    "myEventTypeField":"Created",
    "resource":"Users/example/Messages/1000",
    "resourceData":{"someDataField1":"SomeDataFieldValue"}
  }
]
```

<span data-ttu-id="93f5a-108">Although that format doesn't match the required schema, Event Grid enables you to map your fields to the schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-108">Although that format doesn't match the required schema, Event Grid enables you to map your fields to the schema.</span></span> <span data-ttu-id="93f5a-109">Or, you can receive the values in the original schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-109">Or, you can receive the values in the original schema.</span></span>

## <a name="create-custom-topic-with-mapped-fields"></a><span data-ttu-id="93f5a-110">Create custom topic with mapped fields</span><span class="sxs-lookup"><span data-stu-id="93f5a-110">Create custom topic with mapped fields</span></span>

<span data-ttu-id="93f5a-111">When creating a custom topic, specify how to map fields from your original event to the event grid schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-111">When creating a custom topic, specify how to map fields from your original event to the event grid schema.</span></span> <span data-ttu-id="93f5a-112">There are three properties you use to customize the mapping:</span><span class="sxs-lookup"><span data-stu-id="93f5a-112">There are three properties you use to customize the mapping:</span></span>

* <span data-ttu-id="93f5a-113">The `--input-schema` parameter specifies the type of schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-113">The `--input-schema` parameter specifies the type of schema.</span></span> <span data-ttu-id="93f5a-114">The available options are *cloudeventv01schema*, *customeventschema*, and *eventgridschema*.</span><span class="sxs-lookup"><span data-stu-id="93f5a-114">The available options are *cloudeventv01schema*, *customeventschema*, and *eventgridschema*.</span></span> <span data-ttu-id="93f5a-115">The default value is eventgridschema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-115">The default value is eventgridschema.</span></span> <span data-ttu-id="93f5a-116">When creating custom mapping between your schema and the event grid schema, use customeventschema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-116">When creating custom mapping between your schema and the event grid schema, use customeventschema.</span></span> <span data-ttu-id="93f5a-117">When events are in the CloudEvents schema, use cloudeventv01schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-117">When events are in the CloudEvents schema, use cloudeventv01schema.</span></span>

* <span data-ttu-id="93f5a-118">The `--input-mapping-default-values` parameter specifies default values for fields in the Event Grid schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-118">The `--input-mapping-default-values` parameter specifies default values for fields in the Event Grid schema.</span></span> <span data-ttu-id="93f5a-119">You can set default values for *subject*, *eventtype*, and *dataversion*.</span><span class="sxs-lookup"><span data-stu-id="93f5a-119">You can set default values for *subject*, *eventtype*, and *dataversion*.</span></span> <span data-ttu-id="93f5a-120">Typically, you use this parameter when your custom schema does not include a field that corresponds to one of those three fields.</span><span class="sxs-lookup"><span data-stu-id="93f5a-120">Typically, you use this parameter when your custom schema does not include a field that corresponds to one of those three fields.</span></span> <span data-ttu-id="93f5a-121">For example, you can specify that dataversion is always set to **1.0**.</span><span class="sxs-lookup"><span data-stu-id="93f5a-121">For example, you can specify that dataversion is always set to **1.0**.</span></span>

* <span data-ttu-id="93f5a-122">The `--input-mapping-fields` parameter maps fields from your schema to the event grid schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-122">The `--input-mapping-fields` parameter maps fields from your schema to the event grid schema.</span></span> <span data-ttu-id="93f5a-123">You specify values in space-separated key/value pairs.</span><span class="sxs-lookup"><span data-stu-id="93f5a-123">You specify values in space-separated key/value pairs.</span></span> <span data-ttu-id="93f5a-124">For the key name, use the name of the event grid field.</span><span class="sxs-lookup"><span data-stu-id="93f5a-124">For the key name, use the name of the event grid field.</span></span> <span data-ttu-id="93f5a-125">For the value, use the name of your field.</span><span class="sxs-lookup"><span data-stu-id="93f5a-125">For the value, use the name of your field.</span></span> <span data-ttu-id="93f5a-126">You can use key names for *id*, *topic*, *eventtime*, *subject*, *eventtype*, and *dataversion*.</span><span class="sxs-lookup"><span data-stu-id="93f5a-126">You can use key names for *id*, *topic*, *eventtime*, *subject*, *eventtype*, and *dataversion*.</span></span>

<span data-ttu-id="93f5a-127">The following example creates a custom topic with some mapped and default fields:</span><span class="sxs-lookup"><span data-stu-id="93f5a-127">The following example creates a custom topic with some mapped and default fields:</span></span>

```azurecli-interactive
# if you have not already installed the extension, do it now.
# This extension is required for preview features.
az extension add --name eventgrid

az eventgrid topic create \
  -n demotopic \
  -l eastus2 \
  -g myResourceGroup \
  --input-schema customeventschema
  --input-mapping-fields eventType=myEventTypeField \
  --input-mapping-default-values subject=DefaultSubject dataVersion=1.0
```

## <a name="subscribe-to-event-grid-topic"></a><span data-ttu-id="93f5a-128">Subscribe to event grid topic</span><span class="sxs-lookup"><span data-stu-id="93f5a-128">Subscribe to event grid topic</span></span>

<span data-ttu-id="93f5a-129">When subscribing to the custom topic, you specify the schema you would like to use for receiving the events.</span><span class="sxs-lookup"><span data-stu-id="93f5a-129">When subscribing to the custom topic, you specify the schema you would like to use for receiving the events.</span></span> <span data-ttu-id="93f5a-130">You use the `--event-delivery-schema` parameter and set it to *cloudeventv01schema*, *eventgridschema*, or *inputeventschema*.</span><span class="sxs-lookup"><span data-stu-id="93f5a-130">You use the `--event-delivery-schema` parameter and set it to *cloudeventv01schema*, *eventgridschema*, or *inputeventschema*.</span></span> <span data-ttu-id="93f5a-131">The default value is eventgridschema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-131">The default value is eventgridschema.</span></span>

<span data-ttu-id="93f5a-132">The examples in this section use a Queue storage for the event handler.</span><span class="sxs-lookup"><span data-stu-id="93f5a-132">The examples in this section use a Queue storage for the event handler.</span></span> <span data-ttu-id="93f5a-133">For more information, see [Route custom events to Azure Queue storage](custom-event-to-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="93f5a-133">For more information, see [Route custom events to Azure Queue storage](custom-event-to-queue-storage.md).</span></span>

<span data-ttu-id="93f5a-134">The following example subscribes to an event grid topic and uses the default event grid schema:</span><span class="sxs-lookup"><span data-stu-id="93f5a-134">The following example subscribes to an event grid topic and uses the default event grid schema:</span></span>

```azurecli-interactive
az eventgrid event-subscription create \
  --topic-name demotopic \
  -g myResourceGroup \
  --name eventsub1 \
  --endpoint-type storagequeue \
  --endpoint <storage-queue-url>
```

<span data-ttu-id="93f5a-135">The next example uses the input schema of the event:</span><span class="sxs-lookup"><span data-stu-id="93f5a-135">The next example uses the input schema of the event:</span></span>

```azurecli-interactive
az eventgrid event-subscription create \
  --topic-name demotopic \
  -g myResourceGroup \
  --name eventsub2 \
  --event-delivery-schema inputeventschema \
  --endpoint-type storagequeue \
  --endpoint <storage-queue-url>
```

## <a name="publish-event-to-topic"></a><span data-ttu-id="93f5a-136">Publish event to topic</span><span class="sxs-lookup"><span data-stu-id="93f5a-136">Publish event to topic</span></span>

<span data-ttu-id="93f5a-137">You are now ready to send an event to the custom topic, and see the result of the mapping.</span><span class="sxs-lookup"><span data-stu-id="93f5a-137">You are now ready to send an event to the custom topic, and see the result of the mapping.</span></span> <span data-ttu-id="93f5a-138">The following script to post an event in the [example schema](#original-event-schema):</span><span class="sxs-lookup"><span data-stu-id="93f5a-138">The following script to post an event in the [example schema](#original-event-schema):</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name demotopic -g myResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name demotopic -g myResourceGroup --query "key1" --output tsv)

body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/mapeventfields.json)'")

curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="93f5a-139">Now, look at your Queue storage.</span><span class="sxs-lookup"><span data-stu-id="93f5a-139">Now, look at your Queue storage.</span></span> <span data-ttu-id="93f5a-140">The two subscriptions delivered events in different schemas.</span><span class="sxs-lookup"><span data-stu-id="93f5a-140">The two subscriptions delivered events in different schemas.</span></span>

<span data-ttu-id="93f5a-141">The first subscription used event grid schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-141">The first subscription used event grid schema.</span></span> <span data-ttu-id="93f5a-142">The format of the delivered event is:</span><span class="sxs-lookup"><span data-stu-id="93f5a-142">The format of the delivered event is:</span></span>

```json
{
  "Id": "016b3d68-881f-4ea3-8a9c-ed9246582abe",
  "EventTime": "2018-05-01T20:00:25.2606434Z",
  "EventType": "Created",
  "DataVersion": "1.0",
  "MetadataVersion": "1",
  "Topic": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.EventGrid/topics/demotopic",
  "Subject": "DefaultSubject",
  "Data": {
    "myEventTypeField": "Created",
    "resource": "Users/example/Messages/1000",
    "resourceData": { "someDataField1": "SomeDataFieldValue" } 
  }
}
```

<span data-ttu-id="93f5a-143">These fields contain the mappings from the custom topic.</span><span class="sxs-lookup"><span data-stu-id="93f5a-143">These fields contain the mappings from the custom topic.</span></span> <span data-ttu-id="93f5a-144">**myEventTypeField** is mapped to **EventType**.</span><span class="sxs-lookup"><span data-stu-id="93f5a-144">**myEventTypeField** is mapped to **EventType**.</span></span> <span data-ttu-id="93f5a-145">The default values for **DataVersion** and **Subject** are used.</span><span class="sxs-lookup"><span data-stu-id="93f5a-145">The default values for **DataVersion** and **Subject** are used.</span></span> <span data-ttu-id="93f5a-146">The **Data** object contains the original event schema fields.</span><span class="sxs-lookup"><span data-stu-id="93f5a-146">The **Data** object contains the original event schema fields.</span></span>

<span data-ttu-id="93f5a-147">The second subscription used the input event schema.</span><span class="sxs-lookup"><span data-stu-id="93f5a-147">The second subscription used the input event schema.</span></span> <span data-ttu-id="93f5a-148">The format of the delivered event is:</span><span class="sxs-lookup"><span data-stu-id="93f5a-148">The format of the delivered event is:</span></span>

```json
{
  "myEventTypeField": "Created",
  "resource": "Users/example/Messages/1000",
  "resourceData": { "someDataField1": "SomeDataFieldValue" }
}
```

<span data-ttu-id="93f5a-149">Notice that the original fields were delivered.</span><span class="sxs-lookup"><span data-stu-id="93f5a-149">Notice that the original fields were delivered.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93f5a-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="93f5a-150">Next steps</span></span>

* <span data-ttu-id="93f5a-151">For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).</span><span class="sxs-lookup"><span data-stu-id="93f5a-151">For information about event delivery and retries, [Event Grid message delivery and retry](delivery-and-retry.md).</span></span>
* <span data-ttu-id="93f5a-152">For an introduction to Event Grid, see [About Event Grid](overview.md).</span><span class="sxs-lookup"><span data-stu-id="93f5a-152">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="93f5a-153">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="93f5a-153">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
