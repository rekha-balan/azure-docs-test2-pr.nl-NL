---
title: Azure IoT Hub and Event Grid | Microsoft Docs
description: Use Azure Event Grid to trigger processes based on actions that happen in IoT Hub.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 02/14/2018
ms.author: kgremban
ms.openlocfilehash: 3c12e98137f44ac094adaae282b5d56d30061e60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857587"
---
# <a name="react-to-iot-hub-events-by-using-event-grid-to-trigger-actions"></a><span data-ttu-id="a6efc-103">React to IoT Hub events by using Event Grid to trigger actions</span><span class="sxs-lookup"><span data-stu-id="a6efc-103">React to IoT Hub events by using Event Grid to trigger actions</span></span>

<span data-ttu-id="a6efc-104">Azure IoT Hub integrates with Azure Event Grid so that you can send event notifications to other services and trigger downstream processes.</span><span class="sxs-lookup"><span data-stu-id="a6efc-104">Azure IoT Hub integrates with Azure Event Grid so that you can send event notifications to other services and trigger downstream processes.</span></span> <span data-ttu-id="a6efc-105">Configure your business applications to listen for IoT Hub events so that you can react to critical events in a reliable, scalable, and secure manner.</span><span class="sxs-lookup"><span data-stu-id="a6efc-105">Configure your business applications to listen for IoT Hub events so that you can react to critical events in a reliable, scalable, and secure manner.</span></span> <span data-ttu-id="a6efc-106">For example, build an application to perform multiple actions like updating a database, creating a ticket, and delivering an email notification every time a new IoT device is registered to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6efc-106">For example, build an application to perform multiple actions like updating a database, creating a ticket, and delivering an email notification every time a new IoT device is registered to your IoT hub.</span></span> 

<span data-ttu-id="a6efc-107">[Azure Event Grid][lnk-eg-overview] is a fully managed event routing service that uses a publish-subscribe model.</span><span class="sxs-lookup"><span data-stu-id="a6efc-107">[Azure Event Grid][lnk-eg-overview] is a fully managed event routing service that uses a publish-subscribe model.</span></span> <span data-ttu-id="a6efc-108">Event Grid has built-in support for Azure services like [Azure Functions](../azure-functions/functions-overview.md) and [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md), and can deliver event alerts to non-Azure services using webhooks.</span><span class="sxs-lookup"><span data-stu-id="a6efc-108">Event Grid has built-in support for Azure services like [Azure Functions](../azure-functions/functions-overview.md) and [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md), and can deliver event alerts to non-Azure services using webhooks.</span></span> <span data-ttu-id="a6efc-109">For a complete list of the event handlers that Event Grid supports, see [An introduction to Azure Event Grid][lnk-eg-overview].</span><span class="sxs-lookup"><span data-stu-id="a6efc-109">For a complete list of the event handlers that Event Grid supports, see [An introduction to Azure Event Grid][lnk-eg-overview].</span></span> 

![Azure Event Grid architecture](./media/iot-hub-event-grid/event-grid-functional-model.png)

## <a name="regional-availability"></a><span data-ttu-id="a6efc-111">Regional availability</span><span class="sxs-lookup"><span data-stu-id="a6efc-111">Regional availability</span></span>

<span data-ttu-id="a6efc-112">The Event Grid integration is available for IoT hubs located in the regions where Event Grid is supported.</span><span class="sxs-lookup"><span data-stu-id="a6efc-112">The Event Grid integration is available for IoT hubs located in the regions where Event Grid is supported.</span></span> <span data-ttu-id="a6efc-113">For the latest list of regions, see [An introduction to Azure Event Grid][lnk-eg-overview].</span><span class="sxs-lookup"><span data-stu-id="a6efc-113">For the latest list of regions, see [An introduction to Azure Event Grid][lnk-eg-overview].</span></span> 

## <a name="event-types"></a><span data-ttu-id="a6efc-114">Event types</span><span class="sxs-lookup"><span data-stu-id="a6efc-114">Event types</span></span>

<span data-ttu-id="a6efc-115">IoT Hub publishes the following event types:</span><span class="sxs-lookup"><span data-stu-id="a6efc-115">IoT Hub publishes the following event types:</span></span> 

| <span data-ttu-id="a6efc-116">Event type</span><span class="sxs-lookup"><span data-stu-id="a6efc-116">Event type</span></span> | <span data-ttu-id="a6efc-117">Description</span><span class="sxs-lookup"><span data-stu-id="a6efc-117">Description</span></span> |
| ---------- | ----------- |
| <span data-ttu-id="a6efc-118">Microsoft.Devices.DeviceCreated</span><span class="sxs-lookup"><span data-stu-id="a6efc-118">Microsoft.Devices.DeviceCreated</span></span> | <span data-ttu-id="a6efc-119">Published when a device is registered to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6efc-119">Published when a device is registered to an IoT hub.</span></span> |
| <span data-ttu-id="a6efc-120">Microsoft.Devices.DeviceDeleted</span><span class="sxs-lookup"><span data-stu-id="a6efc-120">Microsoft.Devices.DeviceDeleted</span></span> | <span data-ttu-id="a6efc-121">Published when a device is deleted from an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6efc-121">Published when a device is deleted from an IoT hub.</span></span> |
| <span data-ttu-id="a6efc-122">Microsoft.Devices.DeviceConnected</span><span class="sxs-lookup"><span data-stu-id="a6efc-122">Microsoft.Devices.DeviceConnected</span></span> | <span data-ttu-id="a6efc-123">Published when a device is connected to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6efc-123">Published when a device is connected to an IoT hub.</span></span> |
| <span data-ttu-id="a6efc-124">Microsoft.Devices.DeviceDisconnected</span><span class="sxs-lookup"><span data-stu-id="a6efc-124">Microsoft.Devices.DeviceDisconnected</span></span> | <span data-ttu-id="a6efc-125">Published when a device is disconnected from an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6efc-125">Published when a device is disconnected from an IoT hub.</span></span> |

<span data-ttu-id="a6efc-126">Use either the Azure portal or Azure CLI to configure which events to publish from each IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6efc-126">Use either the Azure portal or Azure CLI to configure which events to publish from each IoT hub.</span></span> <span data-ttu-id="a6efc-127">For an example, try the tutorial [Send email notifications about Azure IoT Hub events using Logic Apps](../event-grid/publish-iot-hub-events-to-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a6efc-127">For an example, try the tutorial [Send email notifications about Azure IoT Hub events using Logic Apps](../event-grid/publish-iot-hub-events-to-logic-apps.md).</span></span>

## <a name="event-schema"></a><span data-ttu-id="a6efc-128">Event schema</span><span class="sxs-lookup"><span data-stu-id="a6efc-128">Event schema</span></span>

<span data-ttu-id="a6efc-129">IoT Hub events contain all the information you need to respond to changes in your device lifecycle.</span><span class="sxs-lookup"><span data-stu-id="a6efc-129">IoT Hub events contain all the information you need to respond to changes in your device lifecycle.</span></span> <span data-ttu-id="a6efc-130">You can identify an IoT Hub event by checking that the eventType property starts with **Microsoft.Devices**.</span><span class="sxs-lookup"><span data-stu-id="a6efc-130">You can identify an IoT Hub event by checking that the eventType property starts with **Microsoft.Devices**.</span></span> <span data-ttu-id="a6efc-131">For more information about how to use Event Grid event properties, see the [Event Grid event schema](../event-grid/event-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a6efc-131">For more information about how to use Event Grid event properties, see the [Event Grid event schema](../event-grid/event-schema.md).</span></span>

### <a name="device-connected-schema"></a><span data-ttu-id="a6efc-132">Device connected schema</span><span class="sxs-lookup"><span data-stu-id="a6efc-132">Device connected schema</span></span>

<span data-ttu-id="a6efc-133">The following example shows the schema of a device connected event:</span><span class="sxs-lookup"><span data-stu-id="a6efc-133">The following example shows the schema of a device connected event:</span></span> 

```json
[{  
  "id": "f6bbf8f4-d365-520d-a878-17bf7238abd8", 
  "topic": "/SUBSCRIPTIONS/<subscription ID>/RESOURCEGROUPS/<resource group name>/PROVIDERS/MICROSOFT.DEVICES/IOTHUBS/<hub name>", 
  "subject": "devices/LogicAppTestDevice", 
  "eventType": "Microsoft.Devices.DeviceConnected", 
  "eventTime": "2018-06-02T19:17:44.4383997Z", 
  "data": {
      "deviceConnectionStateEventInfo": {
        "sequenceNumber":
          "000000000000000001D4132452F67CE200000002000000000000000000000001"
      },
    "hubName": "egtesthub1",
    "deviceId": "LogicAppTestDevice",
    "moduleId" : "DeviceModuleID",
  }, 
  "dataVersion": "1", 
  "metadataVersion": "1" 
}]
```

### <a name="device-created-schema"></a><span data-ttu-id="a6efc-134">Device created schema</span><span class="sxs-lookup"><span data-stu-id="a6efc-134">Device created schema</span></span>

<span data-ttu-id="a6efc-135">The following example shows the schema of a device created event:</span><span class="sxs-lookup"><span data-stu-id="a6efc-135">The following example shows the schema of a device created event:</span></span> 

```json
[{
  "id": "56afc886-767b-d359-d59e-0da7877166b2",
  "topic": "/SUBSCRIPTIONS/<subscription ID>/RESOURCEGROUPS/<resource group name>/PROVIDERS/MICROSOFT.DEVICES/IOTHUBS/<hub name>",
  "subject": "devices/LogicAppTestDevice",
  "eventType": "Microsoft.Devices.DeviceCreated",
  "eventTime": "2018-01-02T19:17:44.4383997Z",
  "data": {
    "twin": {
      "deviceId": "LogicAppTestDevice",
      "etag": "AAAAAAAAAAE=",
      "deviceEtag":"null",
      "status": "enabled",
      "statusUpdateTime": "0001-01-01T00:00:00",
      "connectionState": "Disconnected",
      "lastActivityTime": "0001-01-01T00:00:00",
      "cloudToDeviceMessageCount": 0,
      "authenticationType": "sas",
      "x509Thumbprint": {
        "primaryThumbprint": null,
        "secondaryThumbprint": null
      },
      "version": 2,
      "properties": {
        "desired": {
          "$metadata": {
            "$lastUpdated": "2018-01-02T19:17:44.4383997Z"
          },
          "$version": 1
        },
        "reported": {
          "$metadata": {
            "$lastUpdated": "2018-01-02T19:17:44.4383997Z"
          },
          "$version": 1
        }
      }
    },
    "hubName": "egtesthub1",
    "deviceId": "LogicAppTestDevice"
  },
  "dataVersion": "1",
  "metadataVersion": "1"
}]
```

<span data-ttu-id="a6efc-136">For a detailed description of each property, see [Azure Event Grid event schema for IoT Hub](../event-grid/event-schema-iot-hub.md)</span><span class="sxs-lookup"><span data-stu-id="a6efc-136">For a detailed description of each property, see [Azure Event Grid event schema for IoT Hub](../event-grid/event-schema-iot-hub.md)</span></span>

## <a name="filter-events"></a><span data-ttu-id="a6efc-137">Filter events</span><span class="sxs-lookup"><span data-stu-id="a6efc-137">Filter events</span></span>

<span data-ttu-id="a6efc-138">IoT Hub event subscriptions can filter events based on event type and device name.</span><span class="sxs-lookup"><span data-stu-id="a6efc-138">IoT Hub event subscriptions can filter events based on event type and device name.</span></span> <span data-ttu-id="a6efc-139">Subject filters in Event Grid work based on **Begins With** (prefix) and **Ends With** (suffix) matches.</span><span class="sxs-lookup"><span data-stu-id="a6efc-139">Subject filters in Event Grid work based on **Begins With** (prefix) and **Ends With** (suffix) matches.</span></span> <span data-ttu-id="a6efc-140">The filter uses an `AND` operator, so events with a subject that match both the prefix and suffix are delivered to the subscriber.</span><span class="sxs-lookup"><span data-stu-id="a6efc-140">The filter uses an `AND` operator, so events with a subject that match both the prefix and suffix are delivered to the subscriber.</span></span> 

<span data-ttu-id="a6efc-141">The subject of IoT Events uses the format:</span><span class="sxs-lookup"><span data-stu-id="a6efc-141">The subject of IoT Events uses the format:</span></span>

```json
devices/{deviceId}
```
## <a name="limitations-for-device-connected-and-device-disconnected-events"></a><span data-ttu-id="a6efc-142">Limitations for device connected and device disconnected events</span><span class="sxs-lookup"><span data-stu-id="a6efc-142">Limitations for device connected and device disconnected events</span></span>

<span data-ttu-id="a6efc-143">To receive device connected and device disconnected events, you must open the D2C link or C2D link for your device.</span><span class="sxs-lookup"><span data-stu-id="a6efc-143">To receive device connected and device disconnected events, you must open the D2C link or C2D link for your device.</span></span> <span data-ttu-id="a6efc-144">If your device is using MQTT protocol, IoT Hub will keep the C2D link open.</span><span class="sxs-lookup"><span data-stu-id="a6efc-144">If your device is using MQTT protocol, IoT Hub will keep the C2D link open.</span></span> <span data-ttu-id="a6efc-145">For AMQP you can open the C2D link by calling the [Receive Async API](https://docs.microsoft.com/dotnet/api/microsoft.azure.devices.client.deviceclient.receiveasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="a6efc-145">For AMQP you can open the C2D link by calling the [Receive Async API](https://docs.microsoft.com/dotnet/api/microsoft.azure.devices.client.deviceclient.receiveasync?view=azure-dotnet).</span></span> <span data-ttu-id="a6efc-146">The D2C link is open if you are sending telemetry.</span><span class="sxs-lookup"><span data-stu-id="a6efc-146">The D2C link is open if you are sending telemetry.</span></span> <span data-ttu-id="a6efc-147">If the device connection is flickering, i.e. the device connects and disconnects frequently, we will not send every single connection state, but will publish the connection state that is snapshotted every minute.</span><span class="sxs-lookup"><span data-stu-id="a6efc-147">If the device connection is flickering, i.e. the device connects and disconnects frequently, we will not send every single connection state, but will publish the connection state that is snapshotted every minute.</span></span> <span data-ttu-id="a6efc-148">In case of an IoT Hub outage, we will publish the device connection state as soon as the outage is over.</span><span class="sxs-lookup"><span data-stu-id="a6efc-148">In case of an IoT Hub outage, we will publish the device connection state as soon as the outage is over.</span></span> <span data-ttu-id="a6efc-149">If the device disconnects during that outage, the device disconnected event will be published within 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="a6efc-149">If the device disconnects during that outage, the device disconnected event will be published within 10 minutes.</span></span>

## <a name="tips-for-consuming-events"></a><span data-ttu-id="a6efc-150">Tips for consuming events</span><span class="sxs-lookup"><span data-stu-id="a6efc-150">Tips for consuming events</span></span>

<span data-ttu-id="a6efc-151">Applications that handle IoT Hub events should follow these suggested practices:</span><span class="sxs-lookup"><span data-stu-id="a6efc-151">Applications that handle IoT Hub events should follow these suggested practices:</span></span>

* <span data-ttu-id="a6efc-152">Multiple subscriptions can be configured to route events to the same event handler, so it's important not to assume that events are from a particular source.</span><span class="sxs-lookup"><span data-stu-id="a6efc-152">Multiple subscriptions can be configured to route events to the same event handler, so it's important not to assume that events are from a particular source.</span></span> <span data-ttu-id="a6efc-153">Always check the message topic to ensure that it comes from the IoT hub that you expect.</span><span class="sxs-lookup"><span data-stu-id="a6efc-153">Always check the message topic to ensure that it comes from the IoT hub that you expect.</span></span> 
* <span data-ttu-id="a6efc-154">Don't assume that all events you receive are the types that you expect.</span><span class="sxs-lookup"><span data-stu-id="a6efc-154">Don't assume that all events you receive are the types that you expect.</span></span> <span data-ttu-id="a6efc-155">Always check the eventType before processing the message.</span><span class="sxs-lookup"><span data-stu-id="a6efc-155">Always check the eventType before processing the message.</span></span>
* <span data-ttu-id="a6efc-156">Messages can arrive out of order or after a delay.</span><span class="sxs-lookup"><span data-stu-id="a6efc-156">Messages can arrive out of order or after a delay.</span></span> <span data-ttu-id="a6efc-157">Use the etag field to understand if your information about objects is up-to-date.</span><span class="sxs-lookup"><span data-stu-id="a6efc-157">Use the etag field to understand if your information about objects is up-to-date.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6efc-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6efc-158">Next steps</span></span>

* [<span data-ttu-id="a6efc-159">Try the IoT Hub events tutorial</span><span class="sxs-lookup"><span data-stu-id="a6efc-159">Try the IoT Hub events tutorial</span></span>](../event-grid/publish-iot-hub-events-to-logic-apps.md)
* [<span data-ttu-id="a6efc-160">Learn how to order device connected and disconnected events</span><span class="sxs-lookup"><span data-stu-id="a6efc-160">Learn how to order device connected and disconnected events</span></span>](../iot-hub/iot-hub-how-to-order-connection-state-events.md)
* <span data-ttu-id="a6efc-161">[Learn more about Event Grid][lnk-eg-overview]</span><span class="sxs-lookup"><span data-stu-id="a6efc-161">[Learn more about Event Grid][lnk-eg-overview]</span></span>
* <span data-ttu-id="a6efc-162">[Compare the differences between routing IoT Hub events and messages][lnk-eg-compare]</span><span class="sxs-lookup"><span data-stu-id="a6efc-162">[Compare the differences between routing IoT Hub events and messages][lnk-eg-compare]</span></span>

<!-- Links -->
[lnk-eg-overview]: ../event-grid/overview.md
[lnk-eg-compare]: iot-hub-event-grid-routing-comparison.md