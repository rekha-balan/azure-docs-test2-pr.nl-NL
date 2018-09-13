---
title: Azure IoT Hub operations monitoring | Microsoft Docs
description: How to use Azure IoT Hub operations monitoring to monitor the status of operations on your IoT hub in real time.
services: iot-hub
documentationcenter: ''
author: nberdy
manager: timlt
editor: ''
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: nberdy
ms.openlocfilehash: 80d580407a377f32eab6173a9842b448747d2331
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540660"
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="3915f-103">IoT Hub operations monitoring</span><span class="sxs-lookup"><span data-stu-id="3915f-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="3915f-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span><span class="sxs-lookup"><span data-stu-id="3915f-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="3915f-105">IoT Hub tracks events across several categories of operations.</span><span class="sxs-lookup"><span data-stu-id="3915f-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="3915f-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span><span class="sxs-lookup"><span data-stu-id="3915f-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="3915f-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span><span class="sxs-lookup"><span data-stu-id="3915f-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="3915f-108">IoT Hub monitors six categories of events:</span><span class="sxs-lookup"><span data-stu-id="3915f-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="3915f-109">Device identity operations</span><span class="sxs-lookup"><span data-stu-id="3915f-109">Device identity operations</span></span>
* <span data-ttu-id="3915f-110">Device telemetry</span><span class="sxs-lookup"><span data-stu-id="3915f-110">Device telemetry</span></span>
* <span data-ttu-id="3915f-111">Cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="3915f-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="3915f-112">Connections</span><span class="sxs-lookup"><span data-stu-id="3915f-112">Connections</span></span>
* <span data-ttu-id="3915f-113">File uploads</span><span class="sxs-lookup"><span data-stu-id="3915f-113">File uploads</span></span>
* <span data-ttu-id="3915f-114">Message routing</span><span class="sxs-lookup"><span data-stu-id="3915f-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="3915f-115">How to enable operations monitoring</span><span class="sxs-lookup"><span data-stu-id="3915f-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="3915f-116">Create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3915f-116">Create an IoT hub.</span></span> <span data-ttu-id="3915f-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span><span class="sxs-lookup"><span data-stu-id="3915f-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="3915f-118">Open the blade of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3915f-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="3915f-119">From there, click **Operations monitoring**.</span><span class="sxs-lookup"><span data-stu-id="3915f-119">From there, click **Operations monitoring**.</span></span>

    ![Access operations monitoring configuration in the portal][1]

1. <span data-ttu-id="3915f-121">Select the monitoring categories you wish you monitor, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3915f-121">Select the monitoring categories you wish you monitor, and then click **Save**.</span></span> <span data-ttu-id="3915f-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span><span class="sxs-lookup"><span data-stu-id="3915f-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="3915f-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="3915f-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Configure operations monitoring on your IoT hub][2]

> [!NOTE]
> <span data-ttu-id="3915f-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span><span class="sxs-lookup"><span data-stu-id="3915f-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="3915f-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span><span class="sxs-lookup"><span data-stu-id="3915f-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="3915f-127">Event categories and how to use them</span><span class="sxs-lookup"><span data-stu-id="3915f-127">Event categories and how to use them</span></span>

<span data-ttu-id="3915f-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span><span class="sxs-lookup"><span data-stu-id="3915f-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="3915f-129">Device identity operations</span><span class="sxs-lookup"><span data-stu-id="3915f-129">Device identity operations</span></span>

<span data-ttu-id="3915f-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="3915f-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="3915f-131">Tracking this category is useful for provisioning scenarios.</span><span class="sxs-lookup"><span data-stu-id="3915f-131">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a><span data-ttu-id="3915f-132">Device telemetry</span><span class="sxs-lookup"><span data-stu-id="3915f-132">Device telemetry</span></span>

<span data-ttu-id="3915f-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span><span class="sxs-lookup"><span data-stu-id="3915f-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="3915f-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span><span class="sxs-lookup"><span data-stu-id="3915f-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="3915f-135">This category cannot catch errors caused by code running on the device itself.</span><span class="sxs-lookup"><span data-stu-id="3915f-135">This category cannot catch errors caused by code running on the device itself.</span></span>

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a><span data-ttu-id="3915f-136">Cloud-to-device commands</span><span class="sxs-lookup"><span data-stu-id="3915f-136">Cloud-to-device commands</span></span>

<span data-ttu-id="3915f-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span><span class="sxs-lookup"><span data-stu-id="3915f-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="3915f-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span><span class="sxs-lookup"><span data-stu-id="3915f-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="3915f-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span><span class="sxs-lookup"><span data-stu-id="3915f-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a><span data-ttu-id="3915f-140">Connections</span><span class="sxs-lookup"><span data-stu-id="3915f-140">Connections</span></span>

<span data-ttu-id="3915f-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3915f-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="3915f-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span><span class="sxs-lookup"><span data-stu-id="3915f-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a><span data-ttu-id="3915f-143">File uploads</span><span class="sxs-lookup"><span data-stu-id="3915f-143">File uploads</span></span>

<span data-ttu-id="3915f-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span><span class="sxs-lookup"><span data-stu-id="3915f-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="3915f-145">This category includes:</span><span class="sxs-lookup"><span data-stu-id="3915f-145">This category includes:</span></span>

* <span data-ttu-id="3915f-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span><span class="sxs-lookup"><span data-stu-id="3915f-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="3915f-147">Failed uploads reported by the device.</span><span class="sxs-lookup"><span data-stu-id="3915f-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="3915f-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span><span class="sxs-lookup"><span data-stu-id="3915f-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="3915f-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span><span class="sxs-lookup"><span data-stu-id="3915f-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a><span data-ttu-id="3915f-150">Message routing</span><span class="sxs-lookup"><span data-stu-id="3915f-150">Message routing</span></span>

<span data-ttu-id="3915f-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3915f-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="3915f-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span><span class="sxs-lookup"><span data-stu-id="3915f-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="3915f-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span><span class="sxs-lookup"><span data-stu-id="3915f-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a><span data-ttu-id="3915f-154">View events</span><span class="sxs-lookup"><span data-stu-id="3915f-154">View events</span></span>

<span data-ttu-id="3915f-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span><span class="sxs-lookup"><span data-stu-id="3915f-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="3915f-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="3915f-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="3915f-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span><span class="sxs-lookup"><span data-stu-id="3915f-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="3915f-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span><span class="sxs-lookup"><span data-stu-id="3915f-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="3915f-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span><span class="sxs-lookup"><span data-stu-id="3915f-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="3915f-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3915f-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="3915f-161">Connect to the monitoring endpoint</span><span class="sxs-lookup"><span data-stu-id="3915f-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="3915f-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span><span class="sxs-lookup"><span data-stu-id="3915f-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="3915f-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span><span class="sxs-lookup"><span data-stu-id="3915f-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="3915f-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span><span class="sxs-lookup"><span data-stu-id="3915f-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="3915f-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3915f-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="3915f-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span><span class="sxs-lookup"><span data-stu-id="3915f-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="3915f-167">The following steps show you how to find the necessary values in the portal:</span><span class="sxs-lookup"><span data-stu-id="3915f-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="3915f-168">In the portal, navigate to your IoT Hub resource blade.</span><span class="sxs-lookup"><span data-stu-id="3915f-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="3915f-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span><span class="sxs-lookup"><span data-stu-id="3915f-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Event Hub-compatible endpoint values][img-endpoints]

1. <span data-ttu-id="3915f-171">Choose **Shared access policies**, then choose **service**.</span><span class="sxs-lookup"><span data-stu-id="3915f-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="3915f-172">Make a note of the **Primary key** value:</span><span class="sxs-lookup"><span data-stu-id="3915f-172">Make a note of the **Primary key** value:</span></span>

    ![Service shared access policy primary key][img-service-key]

<span data-ttu-id="3915f-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span><span class="sxs-lookup"><span data-stu-id="3915f-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="3915f-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span><span class="sxs-lookup"><span data-stu-id="3915f-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="3915f-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="3915f-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="3915f-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span><span class="sxs-lookup"><span data-stu-id="3915f-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="3915f-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="3915f-178">Next steps</span></span>
<span data-ttu-id="3915f-179">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="3915f-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3915f-180">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3915f-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="3915f-181">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="3915f-181">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

<!-- Links and images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md



