---
title: Receive events from Azure Event Grid to an HTTP endpoint
description: Describes how to validate an HTTP endpoint, then receive and deserialize Events from Azure Event Grid
services: event-grid
author: banisadr
manager: darosa
ms.service: event-grid
ms.topic: conceptual
ms.date: 04/26/2018
ms.author: babanisa
ms.openlocfilehash: 1ff0cf9d2733d7ebb6e739ce44da6442ffc26c1c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865035"
---
# <a name="receive-events-to-an-http-endpoint"></a><span data-ttu-id="b4499-103">Receive events to an HTTP endpoint</span><span class="sxs-lookup"><span data-stu-id="b4499-103">Receive events to an HTTP endpoint</span></span>

<span data-ttu-id="b4499-104">This article describes how to [validate an HTTP endpoint](security-authentication.md#webhook-event-delivery) to receive events from an Event Subscription and then receive and deserialize events.</span><span class="sxs-lookup"><span data-stu-id="b4499-104">This article describes how to [validate an HTTP endpoint](security-authentication.md#webhook-event-delivery) to receive events from an Event Subscription and then receive and deserialize events.</span></span> <span data-ttu-id="b4499-105">This article uses an Azure Function for demonstration purposes, however the same concepts apply regardless of where the application is hosted.</span><span class="sxs-lookup"><span data-stu-id="b4499-105">This article uses an Azure Function for demonstration purposes, however the same concepts apply regardless of where the application is hosted.</span></span>

> [!NOTE]
> <span data-ttu-id="b4499-106">It is **strongly** recommended that you use an [Event Grid Trigger](../azure-functions/functions-bindings-event-grid.md) when triggering an Azure Function with Event Grid.</span><span class="sxs-lookup"><span data-stu-id="b4499-106">It is **strongly** recommended that you use an [Event Grid Trigger](../azure-functions/functions-bindings-event-grid.md) when triggering an Azure Function with Event Grid.</span></span> <span data-ttu-id="b4499-107">The use of a generic WebHook trigger here is demonstrative.</span><span class="sxs-lookup"><span data-stu-id="b4499-107">The use of a generic WebHook trigger here is demonstrative.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4499-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4499-108">Prerequisites</span></span>

* <span data-ttu-id="b4499-109">You will need a function app with an [HTTP triggered function](../azure-functions/functions-create-generic-webhook-triggered-function.md)</span><span class="sxs-lookup"><span data-stu-id="b4499-109">You will need a function app with an [HTTP triggered function](../azure-functions/functions-create-generic-webhook-triggered-function.md)</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="b4499-110">Add dependencies</span><span class="sxs-lookup"><span data-stu-id="b4499-110">Add dependencies</span></span>

<span data-ttu-id="b4499-111">If you are developing in .NET, [add a dependency](../azure-functions/functions-reference-csharp.md#referencing-custom-assemblies) to your function for the `Microsoft.Azure.EventGrid` [Nuget package](https://www.nuget.org/packages/Microsoft.Azure.EventGrid).</span><span class="sxs-lookup"><span data-stu-id="b4499-111">If you are developing in .NET, [add a dependency](../azure-functions/functions-reference-csharp.md#referencing-custom-assemblies) to your function for the `Microsoft.Azure.EventGrid` [Nuget package](https://www.nuget.org/packages/Microsoft.Azure.EventGrid).</span></span> <span data-ttu-id="b4499-112">SDKs for other languages are available via the [Publish SDKs](./sdk-overview.md#data-plane-sdks) reference.</span><span class="sxs-lookup"><span data-stu-id="b4499-112">SDKs for other languages are available via the [Publish SDKs](./sdk-overview.md#data-plane-sdks) reference.</span></span> <span data-ttu-id="b4499-113">These packages contain the models for native event types such as `EventGridEvent`, `StorageBlobCreatedEventData`, and `EventHubCaptureFileCreatedEventData`.</span><span class="sxs-lookup"><span data-stu-id="b4499-113">These packages contain the models for native event types such as `EventGridEvent`, `StorageBlobCreatedEventData`, and `EventHubCaptureFileCreatedEventData`.</span></span>

<span data-ttu-id="b4499-114">Click on the "View Files" link in your Azure Function (right most pane in the Azure functions portal), and create a file called project.json.</span><span class="sxs-lookup"><span data-stu-id="b4499-114">Click on the "View Files" link in your Azure Function (right most pane in the Azure functions portal), and create a file called project.json.</span></span> <span data-ttu-id="b4499-115">Add the following contents to the `project.json` file and save it:</span><span class="sxs-lookup"><span data-stu-id="b4499-115">Add the following contents to the `project.json` file and save it:</span></span>

 ```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.Azure.EventGrid": "1.3.0"
      }
    }
   }
}
```

![Added NuGet package](./media/receive-events/add-dependencies.png)

## <a name="endpoint-validation"></a><span data-ttu-id="b4499-117">Endpoint validation</span><span class="sxs-lookup"><span data-stu-id="b4499-117">Endpoint validation</span></span>

<span data-ttu-id="b4499-118">The first thing you want to do is handle `Microsoft.EventGrid.SubscriptionValidationEvent` events.</span><span class="sxs-lookup"><span data-stu-id="b4499-118">The first thing you want to do is handle `Microsoft.EventGrid.SubscriptionValidationEvent` events.</span></span> <span data-ttu-id="b4499-119">Every time someone subscribes to an event, Event Grid sends a validation event to the endpoint with a `validationCode` in the data payload.</span><span class="sxs-lookup"><span data-stu-id="b4499-119">Every time someone subscribes to an event, Event Grid sends a validation event to the endpoint with a `validationCode` in the data payload.</span></span> <span data-ttu-id="b4499-120">The endpoint is required to echo this back in the response body to [prove the endpoint is valid and owned by you](security-authentication.md#webhook-event-delivery).</span><span class="sxs-lookup"><span data-stu-id="b4499-120">The endpoint is required to echo this back in the response body to [prove the endpoint is valid and owned by you](security-authentication.md#webhook-event-delivery).</span></span> <span data-ttu-id="b4499-121">If you are using an [Event Grid Trigger](../azure-functions/functions-bindings-event-grid.md) rather than a WebHook triggered Function, endpoint validation is handled for you.</span><span class="sxs-lookup"><span data-stu-id="b4499-121">If you are using an [Event Grid Trigger](../azure-functions/functions-bindings-event-grid.md) rather than a WebHook triggered Function, endpoint validation is handled for you.</span></span> <span data-ttu-id="b4499-122">If you use a third-party API service (like [Zapier](https://zapier.com) or [IFTTT](https://ifttt.com/)), you might not be able to programmatically echo the validation code.</span><span class="sxs-lookup"><span data-stu-id="b4499-122">If you use a third-party API service (like [Zapier](https://zapier.com) or [IFTTT](https://ifttt.com/)), you might not be able to programmatically echo the validation code.</span></span> <span data-ttu-id="b4499-123">For those services, you can manually validate the subscription by using a validation URL that is sent in the subscription validation event.</span><span class="sxs-lookup"><span data-stu-id="b4499-123">For those services, you can manually validate the subscription by using a validation URL that is sent in the subscription validation event.</span></span> <span data-ttu-id="b4499-124">Copy that URL in the `validationUrl` property and send a GET request either through a REST client or your web browser.</span><span class="sxs-lookup"><span data-stu-id="b4499-124">Copy that URL in the `validationUrl` property and send a GET request either through a REST client or your web browser.</span></span>

<span data-ttu-id="b4499-125">Manual validation is in preview.</span><span class="sxs-lookup"><span data-stu-id="b4499-125">Manual validation is in preview.</span></span> <span data-ttu-id="b4499-126">To use it, you must install the [Event Grid extension](/cli/azure/azure-cli-extensions-list) for [Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b4499-126">To use it, you must install the [Event Grid extension](/cli/azure/azure-cli-extensions-list) for [Azure CLI](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="b4499-127">You can install it with `az extension add --name eventgrid`.</span><span class="sxs-lookup"><span data-stu-id="b4499-127">You can install it with `az extension add --name eventgrid`.</span></span> <span data-ttu-id="b4499-128">If you are using the REST API, ensure you are using `api-version=2018-05-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="b4499-128">If you are using the REST API, ensure you are using `api-version=2018-05-01-preview`.</span></span>

<span data-ttu-id="b4499-129">To programmatically echo the validation code, use the following code (you can also find related samples at https://github.com/Azure-Samples/event-grid-dotnet-publish-consume-events/tree/master/EventGridConsumer):</span><span class="sxs-lookup"><span data-stu-id="b4499-129">To programmatically echo the validation code, use the following code (you can also find related samples at https://github.com/Azure-Samples/event-grid-dotnet-publish-consume-events/tree/master/EventGridConsumer):</span></span>

```csharp
using System.Net;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using Newtonsoft.Json.Serialization;
using Microsoft.Azure.EventGrid.Models;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{

    log.Info($"C# HTTP trigger function begun");
    string response = string.Empty;
    const string SubscriptionValidationEvent = "Microsoft.EventGrid.SubscriptionValidationEvent";

    string requestContent = await req.Content.ReadAsStringAsync();
    EventGridEvent[] eventGridEvents = JsonConvert.DeserializeObject<EventGridEvent[]>(requestContent);

    foreach (EventGridEvent eventGridEvent in eventGridEvents)
    {
        JObject dataObject = eventGridEvent.Data as JObject;

        // Deserialize the event data into the appropriate type based on event type
        if (string.Equals(eventGridEvent.EventType, SubscriptionValidationEvent, StringComparison.OrdinalIgnoreCase))
        {
            var eventData = dataObject.ToObject<SubscriptionValidationEventData>();
            log.Info($"Got SubscriptionValidation event data, validation code: {eventData.ValidationCode}, topic: {eventGridEvent.Topic}");
            // Do any additional validation (as required) and then return back the below response
            var responseData = new SubscriptionValidationResponse();
            responseData.ValidationResponse = eventData.ValidationCode;
            return req.CreateResponse(HttpStatusCode.OK, responseData);
        }
    }

    return req.CreateResponse(HttpStatusCode.OK, response);
}

```

```javascript
var http = require('http');

module.exports = function (context, req) {
    context.log('JavaScript HTTP trigger function begun');
    var validationEventType = "Microsoft.EventGrid.SubscriptionValidationEvent";

    for (var events in req.body) {
        var body = req.body[events];
        // Deserialize the event data into the appropriate type based on event type
        if (body.data && body.eventType == validationEventType) {
            context.log("Got SubscriptionValidation event data, validation code: " + body.data.validationCode + " topic: " + body.topic);

            // Do any additional validation (as required) and then return back the below response
            var code = body.data.validationCode;
            context.res = { status: 200, body: { "ValidationResponse": code } };
        }
    }
    context.done();
};
```

### <a name="test-validation-response"></a><span data-ttu-id="b4499-130">Test validation response</span><span class="sxs-lookup"><span data-stu-id="b4499-130">Test validation response</span></span>

<span data-ttu-id="b4499-131">Test the validation response function by pasting the sample event into the test field for the function:</span><span class="sxs-lookup"><span data-stu-id="b4499-131">Test the validation response function by pasting the sample event into the test field for the function:</span></span>

```json
[{
  "id": "2d1781af-3a4c-4d7c-bd0c-e34b19da4e66",
  "topic": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "subject": "",
  "data": {
    "validationCode": "512d38b6-c7b8-40c8-89fe-f46f9e9622b6"
  },
  "eventType": "Microsoft.EventGrid.SubscriptionValidationEvent",
  "eventTime": "2018-01-25T22:12:19.4556811Z",
  "metadataVersion": "1",
  "dataVersion": "1"
}]
```

<span data-ttu-id="b4499-132">When you click Run, the Output should be 200 OK and `{"ValidationResponse":"512d38b6-c7b8-40c8-89fe-f46f9e9622b6"}` in the body:</span><span class="sxs-lookup"><span data-stu-id="b4499-132">When you click Run, the Output should be 200 OK and `{"ValidationResponse":"512d38b6-c7b8-40c8-89fe-f46f9e9622b6"}` in the body:</span></span>

![validation response](./media/receive-events/validation-response.png)

## <a name="handle-blob-storage-events"></a><span data-ttu-id="b4499-134">Handle Blob storage events</span><span class="sxs-lookup"><span data-stu-id="b4499-134">Handle Blob storage events</span></span>

<span data-ttu-id="b4499-135">Now, let's extend the function to handle `Microsoft.Storage.BlobCreated`:</span><span class="sxs-lookup"><span data-stu-id="b4499-135">Now, let's extend the function to handle `Microsoft.Storage.BlobCreated`:</span></span>

```cs
using System.Net;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using Newtonsoft.Json.Serialization;
using Microsoft.Azure.EventGrid.Models;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function begun");
    string response = string.Empty;
    const string SubscriptionValidationEvent = "Microsoft.EventGrid.SubscriptionValidationEvent";
    const string StorageBlobCreatedEvent = "Microsoft.Storage.BlobCreated";

    string requestContent = await req.Content.ReadAsStringAsync();
    EventGridEvent[] eventGridEvents = JsonConvert.DeserializeObject<EventGridEvent[]>(requestContent);

    foreach (EventGridEvent eventGridEvent in eventGridEvents)
    {
        JObject dataObject = eventGridEvent.Data as JObject;

        // Deserialize the event data into the appropriate type based on event type 
        if (string.Equals(eventGridEvent.EventType, SubscriptionValidationEvent, StringComparison.OrdinalIgnoreCase))
        {
            var eventData = dataObject.ToObject<SubscriptionValidationEventData>();
            log.Info($"Got SubscriptionValidation event data, validation code: {eventData.ValidationCode}, topic: {eventGridEvent.Topic}");

            // Do any additional validation (as required) and then return back the below response
            var responseData = new SubscriptionValidationResponse();
            responseData.ValidationResponse = eventData.ValidationCode;
            return req.CreateResponse(HttpStatusCode.OK, responseData);
        }

        else if (string.Equals(eventGridEvent.EventType, StorageBlobCreatedEvent, StringComparison.OrdinalIgnoreCase))
        {
            var eventData = dataObject.ToObject<StorageBlobCreatedEventData>();
            log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
        }
    }

    return req.CreateResponse(HttpStatusCode.OK, response);
}

```

```javascript
var http = require('http');

module.exports = function (context, req) {
    context.log('JavaScript HTTP trigger function begun');
    var validationEventType = "Microsoft.EventGrid.SubscriptionValidationEvent";
    var storageBlobCreatedEvent = "Microsoft.Storage.BlobCreated";

    for (var events in req.body) {
        var body = req.body[events];
        // Deserialize the event data into the appropriate type based on event type  
        if (body.data && body.eventType == validationEventType) {
            context.log("Got SubscriptionValidation event data, validation code: " + body.data.validationCode + " topic: " + body.topic);

            // Do any additional validation (as required) and then return back the below response
            var code = body.data.validationCode;
            context.res = { status: 200, body: { "ValidationResponse": code } };
        }

        else if (body.data && body.eventType == storageBlobCreatedEvent) {
            var blobCreatedEventData = body.data;
            context.log("Relaying received blob created event payload:" + JSON.stringify(blobCreatedEventData));
        }
    }
    context.done();
};

```

### <a name="test-blob-created-event-handling"></a><span data-ttu-id="b4499-136">Test Blob Created event handling</span><span class="sxs-lookup"><span data-stu-id="b4499-136">Test Blob Created event handling</span></span>

<span data-ttu-id="b4499-137">Test the new functionality of the function by putting a [Blob storage event](./event-schema-blob-storage.md#example-event) into the test field and running:</span><span class="sxs-lookup"><span data-stu-id="b4499-137">Test the new functionality of the function by putting a [Blob storage event](./event-schema-blob-storage.md#example-event) into the test field and running:</span></span>

```json
[{
  "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
  "subject": "/blobServices/default/containers/testcontainer/blobs/testfile.txt",
  "eventType": "Microsoft.Storage.BlobCreated",
  "eventTime": "2017-06-26T18:41:00.9584103Z",
  "id": "831e1650-001e-001b-66ab-eeb76e069631",
  "data": {
    "api": "PutBlockList",
    "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
    "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
    "eTag": "0x8D4BCC2E4835CD0",
    "contentType": "text/plain",
    "contentLength": 524288,
    "blobType": "BlockBlob",
    "url": "https://example.blob.core.windows.net/testcontainer/testfile.txt",
    "sequencer": "00000000000004420000000000028963",
    "storageDiagnostics": {
      "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
    }
  },
  "dataVersion": "",
  "metadataVersion": "1"
}]
```

<span data-ttu-id="b4499-138">You should see the blob URL output in the function log:</span><span class="sxs-lookup"><span data-stu-id="b4499-138">You should see the blob URL output in the function log:</span></span>

![Output log](./media/receive-events/blob-event-response.png)

<span data-ttu-id="b4499-140">You can also test by creating a Blob storage account or General Purpose V2 (GPv2) Storage account, [adding and event subscription](../storage/blobs/storage-blob-event-quickstart.md), and setting the endpoint to the function URL:</span><span class="sxs-lookup"><span data-stu-id="b4499-140">You can also test by creating a Blob storage account or General Purpose V2 (GPv2) Storage account, [adding and event subscription](../storage/blobs/storage-blob-event-quickstart.md), and setting the endpoint to the function URL:</span></span>

![Function URL](./media/receive-events/function-url.png)

## <a name="handle-custom-events"></a><span data-ttu-id="b4499-142">Handle Custom events</span><span class="sxs-lookup"><span data-stu-id="b4499-142">Handle Custom events</span></span>

<span data-ttu-id="b4499-143">Finally, lets extend the function once more so that it can also handle custom events.</span><span class="sxs-lookup"><span data-stu-id="b4499-143">Finally, lets extend the function once more so that it can also handle custom events.</span></span> <span data-ttu-id="b4499-144">Add a check for your event `Contoso.Items.ItemReceived`.</span><span class="sxs-lookup"><span data-stu-id="b4499-144">Add a check for your event `Contoso.Items.ItemReceived`.</span></span> <span data-ttu-id="b4499-145">Your final code should look like:</span><span class="sxs-lookup"><span data-stu-id="b4499-145">Your final code should look like:</span></span>

```cs
using System.Net;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using Newtonsoft.Json.Serialization;
using Microsoft.Azure.EventGrid.Models;

class ContosoItemReceivedEventData
{
    public string id { get; set; }
    public string message { get; set; }
    public string time { get; set; }
}

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function begun");
    string response = string.Empty;
    const string SubscriptionValidationEvent = "Microsoft.EventGrid.SubscriptionValidationEvent";
    const string StorageBlobCreatedEvent = "Microsoft.Storage.BlobCreated";
    const string CustomTopicEvent = "Contoso.Items.ItemReceived";

    string requestContent = await req.Content.ReadAsStringAsync();
    EventGridEvent[] eventGridEvents = JsonConvert.DeserializeObject<EventGridEvent[]>(requestContent);

    foreach (EventGridEvent eventGridEvent in eventGridEvents)
    {
        JObject dataObject = eventGridEvent.Data as JObject;

        // Deserialize the event data into the appropriate type based on event type
        if (string.Equals(eventGridEvent.EventType, SubscriptionValidationEvent, StringComparison.OrdinalIgnoreCase))
        {
            var eventData = dataObject.ToObject<SubscriptionValidationEventData>();
            log.Info($"Got SubscriptionValidation event data, validation code: {eventData.ValidationCode}, topic: {eventGridEvent.Topic}");
            // Do any additional validation (as required) and then return back the below response
            var responseData = new SubscriptionValidationResponse();
            responseData.ValidationResponse = eventData.ValidationCode;
            return req.CreateResponse(HttpStatusCode.OK, responseData);
        }

        else if (string.Equals(eventGridEvent.EventType, StorageBlobCreatedEvent, StringComparison.OrdinalIgnoreCase))
        {
            var eventData = dataObject.ToObject<StorageBlobCreatedEventData>();
            log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
        }

        else if (string.Equals(eventGridEvent.EventType, CustomTopicEvent, StringComparison.OrdinalIgnoreCase))
        {
            var eventData = dataObject.ToObject<ContosoItemReceivedEventData>();
            log.Info($"Got ContosoItemReceived event data, item URI {eventData.id}");
        }
    }

    return req.CreateResponse(HttpStatusCode.OK, response);
}

```

```javascript
var http = require('http');
var t = require('tcomb');

module.exports = function (context, req) {
    context.log('JavaScript HTTP trigger function begun');
    var validationEventType = "Microsoft.EventGrid.SubscriptionValidationEvent";
    var storageBlobCreatedEvent = "Microsoft.Storage.BlobCreated";
    var customEventType = "Contoso.Items.ItemReceived";
    var ContosoItemReceivedEventData = t.struct({
        id: t.Str,
        message: t.Str,
        time: t.Str,
    })

    for (var events in req.body) {
        var body = req.body[events];
        // Deserialize the event data into the appropriate type based on event type
        if (body.data && body.eventType == validationEventType) {
            context.log("Got SubscriptionValidation event data, validation code: " + body.data.validationCode + " topic: " + body.topic);

            // Do any additional validation (as required) and then return back the below response
            var code = body.data.validationCode;
            context.res = { status: 200, body: { "ValidationResponse": code } };
        }

        else if (body.data && body.eventType == storageBlobCreatedEvent) {
            var blobCreatedEventData = body.data;
            context.log("Relaying received blob created event payload:" + JSON.stringify(blobCreatedEventData));
        }

        else if (body.data && body.eventType == customEventType) {
            var payload = new ContosoItemReceivedEventData(body.data);
            context.log("Relaying received custom payload:" + JSON.stringify(payload));
            context.log(payload instanceof ContosoItemReceivedEventData);
        }
    }
    context.done();
};

```

### <a name="test-custom-event-handling"></a><span data-ttu-id="b4499-146">Test custom event handling</span><span class="sxs-lookup"><span data-stu-id="b4499-146">Test custom event handling</span></span>

<span data-ttu-id="b4499-147">Finally, test that your extented function can now handle your custom event type:</span><span class="sxs-lookup"><span data-stu-id="b4499-147">Finally, test that your extented function can now handle your custom event type:</span></span>

```json
[{
    "subject": "Contoso/foo/bar/items",
    "eventType": "Microsoft.EventGrid.CustomEventType",
    "eventTime": "2017-08-16T01:57:26.005121Z",
    "id": "602a88ef-0001-00e6-1233-1646070610ea",
    "data": { 
            "id": "831e1650-001e-001b-66ab-eeb76e069631",
            "message": "Contoso item Foo",
            "time": "2017-06-26T18:41:00.9584103Z"
            },
    "dataVersion": "",
    "metadataVersion": "1"
}]
```

<span data-ttu-id="b4499-148">You can also test this functionality live by [sending a custom event with CURL from the Portal](./custom-event-quickstart-portal.md) or by [posting to a custom topic](./post-to-custom-topic.md)  using any service or application that can POST to an endpoint such as [Postman](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="b4499-148">You can also test this functionality live by [sending a custom event with CURL from the Portal](./custom-event-quickstart-portal.md) or by [posting to a custom topic](./post-to-custom-topic.md)  using any service or application that can POST to an endpoint such as [Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="b4499-149">Create a custom topic and an event subscription with the endpoint set as the Function URL.</span><span class="sxs-lookup"><span data-stu-id="b4499-149">Create a custom topic and an event subscription with the endpoint set as the Function URL.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4499-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4499-150">Next steps</span></span>

* <span data-ttu-id="b4499-151">Explore the [Azure Event Grid Mangement and Publish SDKs](./sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b4499-151">Explore the [Azure Event Grid Mangement and Publish SDKs](./sdk-overview.md)</span></span>
* <span data-ttu-id="b4499-152">Learn how to [post to a custom topic](./post-to-custom-topic.md)</span><span class="sxs-lookup"><span data-stu-id="b4499-152">Learn how to [post to a custom topic](./post-to-custom-topic.md)</span></span>
* <span data-ttu-id="b4499-153">Try one of the in-depth Event Grid and Functions tutorials such as [resizing images uploaded to Blob storage](resize-images-on-storage-blob-upload-event.md)</span><span class="sxs-lookup"><span data-stu-id="b4499-153">Try one of the in-depth Event Grid and Functions tutorials such as [resizing images uploaded to Blob storage](resize-images-on-storage-blob-upload-event.md)</span></span>
