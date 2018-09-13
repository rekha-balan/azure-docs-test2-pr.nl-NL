---
title: Monitor the health of your Azure IoT Hub | Microsoft Docs
description: Use Azure Monitor and Azure Resource Health to monitor your IoT Hub and diagnose problems quickly
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 08/09/2018
ms.author: kgremban
ms.openlocfilehash: 4f7eefc7d6b067c360fdc3ce12b9a7ae36080bd8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865558"
---
# <a name="monitor-the-health-of-azure-iot-hub-and-diagnose-problems-quickly"></a><span data-ttu-id="56402-103">Monitor the health of Azure IoT Hub and diagnose problems quickly</span><span class="sxs-lookup"><span data-stu-id="56402-103">Monitor the health of Azure IoT Hub and diagnose problems quickly</span></span>

<span data-ttu-id="56402-104">Businesses that implement Azure IoT Hub expect reliable performance from their resources.</span><span class="sxs-lookup"><span data-stu-id="56402-104">Businesses that implement Azure IoT Hub expect reliable performance from their resources.</span></span> <span data-ttu-id="56402-105">To help you maintain a close watch on your operations, IoT Hub is fully integrated with [Azure Monitor][lnk-AM] and [Azure Resource Health][lnk-ARH].</span><span class="sxs-lookup"><span data-stu-id="56402-105">To help you maintain a close watch on your operations, IoT Hub is fully integrated with [Azure Monitor][lnk-AM] and [Azure Resource Health][lnk-ARH].</span></span> <span data-ttu-id="56402-106">These two services work in tandem to provide you with the data you need to keep your IoT solutions up and running in a healthy state.</span><span class="sxs-lookup"><span data-stu-id="56402-106">These two services work in tandem to provide you with the data you need to keep your IoT solutions up and running in a healthy state.</span></span> 

<span data-ttu-id="56402-107">Azure Monitor is a single source of monitoring and logging for all your Azure services.</span><span class="sxs-lookup"><span data-stu-id="56402-107">Azure Monitor is a single source of monitoring and logging for all your Azure services.</span></span> <span data-ttu-id="56402-108">You can send the diagnostic logs that Azure Monitor generates to Log Analytics, Event Hubs, or Azure Storage for custom processing.</span><span class="sxs-lookup"><span data-stu-id="56402-108">You can send the diagnostic logs that Azure Monitor generates to Log Analytics, Event Hubs, or Azure Storage for custom processing.</span></span> <span data-ttu-id="56402-109">Azure Monitor's metrics and diagnostics settings give you visibility into the performance of your resources.</span><span class="sxs-lookup"><span data-stu-id="56402-109">Azure Monitor's metrics and diagnostics settings give you visibility into the performance of your resources.</span></span> <span data-ttu-id="56402-110">Continue reading this article to learn how to [Use Azure Monitor](#use-azure-monitor) with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="56402-110">Continue reading this article to learn how to [Use Azure Monitor](#use-azure-monitor) with your IoT hub.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="56402-111">The events emitted by the IoT Hub service using Azure Monitor diagnostic logs are not guaranteed to be reliable or ordered.</span><span class="sxs-lookup"><span data-stu-id="56402-111">The events emitted by the IoT Hub service using Azure Monitor diagnostic logs are not guaranteed to be reliable or ordered.</span></span> <span data-ttu-id="56402-112">Some events might be lost or delivered out of order.</span><span class="sxs-lookup"><span data-stu-id="56402-112">Some events might be lost or delivered out of order.</span></span> <span data-ttu-id="56402-113">Diagnostic logs also aren't meant to be real-time, and it may take several minutes for events to be logged to your choice of destination.</span><span class="sxs-lookup"><span data-stu-id="56402-113">Diagnostic logs also aren't meant to be real-time, and it may take several minutes for events to be logged to your choice of destination.</span></span>

<span data-ttu-id="56402-114">Azure Resource Health helps you diagnose and get support when an Azure issues impacts your resources.</span><span class="sxs-lookup"><span data-stu-id="56402-114">Azure Resource Health helps you diagnose and get support when an Azure issues impacts your resources.</span></span> <span data-ttu-id="56402-115">A personalized dashboard provides current and past health status for your IoT Hubs.</span><span class="sxs-lookup"><span data-stu-id="56402-115">A personalized dashboard provides current and past health status for your IoT Hubs.</span></span> <span data-ttu-id="56402-116">Continue reading this article to learn how to [Use Azure Resource Health](#use-azure-resource-health) with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="56402-116">Continue reading this article to learn how to [Use Azure Resource Health](#use-azure-resource-health) with your IoT hub.</span></span> 

<span data-ttu-id="56402-117">In addition to integrating with these two services, IoT Hub also provides its own metrics that you can use to understand the state of your IoT resources.</span><span class="sxs-lookup"><span data-stu-id="56402-117">In addition to integrating with these two services, IoT Hub also provides its own metrics that you can use to understand the state of your IoT resources.</span></span> <span data-ttu-id="56402-118">To learn more, see [Understand IoT Hub metrics][lnk-metrics].</span><span class="sxs-lookup"><span data-stu-id="56402-118">To learn more, see [Understand IoT Hub metrics][lnk-metrics].</span></span>

## <a name="use-azure-monitor"></a><span data-ttu-id="56402-119">Use Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="56402-119">Use Azure Monitor</span></span>

<span data-ttu-id="56402-120">Azure Monitor provides resource-level diagnostics information, which means that you can monitor operations that take place within your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="56402-120">Azure Monitor provides resource-level diagnostics information, which means that you can monitor operations that take place within your IoT hub.</span></span> 

<span data-ttu-id="56402-121">Azure Monitor's diagnostics settings replaces the IoT Hub operations monitor.</span><span class="sxs-lookup"><span data-stu-id="56402-121">Azure Monitor's diagnostics settings replaces the IoT Hub operations monitor.</span></span> <span data-ttu-id="56402-122">If you currently use operations monitoring, you should migrate your workflows.</span><span class="sxs-lookup"><span data-stu-id="56402-122">If you currently use operations monitoring, you should migrate your workflows.</span></span> <span data-ttu-id="56402-123">For more information, see [Migrate from operations monitoring to diagnostics settings][lnk-migrate].</span><span class="sxs-lookup"><span data-stu-id="56402-123">For more information, see [Migrate from operations monitoring to diagnostics settings][lnk-migrate].</span></span>

<span data-ttu-id="56402-124">To learn more about the specific metrics and events that Azure Monitor watches, see [Supported metrics with Azure Monitor][lnk-AM-metrics] and [Supported services, schemas, and categories for Azure Diagnostic Logs][lnk-AM-schemas].</span><span class="sxs-lookup"><span data-stu-id="56402-124">To learn more about the specific metrics and events that Azure Monitor watches, see [Supported metrics with Azure Monitor][lnk-AM-metrics] and [Supported services, schemas, and categories for Azure Diagnostic Logs][lnk-AM-schemas].</span></span>

[!INCLUDE [iot-hub-diagnostics-settings](../../includes/iot-hub-diagnostics-settings.md)]

### <a name="understand-the-logs"></a><span data-ttu-id="56402-125">Understand the logs</span><span class="sxs-lookup"><span data-stu-id="56402-125">Understand the logs</span></span>

<span data-ttu-id="56402-126">Azure Monitor tracks different operations that occur in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="56402-126">Azure Monitor tracks different operations that occur in IoT Hub.</span></span> <span data-ttu-id="56402-127">Each category has a schema that defines how events in that category are reported.</span><span class="sxs-lookup"><span data-stu-id="56402-127">Each category has a schema that defines how events in that category are reported.</span></span> 

#### <a name="connections"></a><span data-ttu-id="56402-128">Connections</span><span class="sxs-lookup"><span data-stu-id="56402-128">Connections</span></span>

<span data-ttu-id="56402-129">The connections category tracks device connect and disconnect events from an IoT hub as well as errors.</span><span class="sxs-lookup"><span data-stu-id="56402-129">The connections category tracks device connect and disconnect events from an IoT hub as well as errors.</span></span> <span data-ttu-id="56402-130">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span><span class="sxs-lookup"><span data-stu-id="56402-130">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

> [!NOTE]
> <span data-ttu-id="56402-131">For reliable connection status of devices check [Device heartbeat][lnk-devguide-heartbeat].</span><span class="sxs-lookup"><span data-stu-id="56402-131">For reliable connection status of devices check [Device heartbeat][lnk-devguide-heartbeat].</span></span>

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Information",
    "properties": "{\"deviceId\":\"<deviceId>\",\"protocol\":\"<protocol>\",\"authType\":\"{\\\"scope\\\":\\\"device\\\",\\\"type\\\":\\\"sas\\\",\\\"issuer\\\":\\\"iothub\\\",\\\"acceptingIpFilterRule\\\":null}\",\"maskedIpAddress\":\"<maskedIpAddress>\"}", 
    "location": "Resource location"
}
```

#### <a name="cloud-to-device-commands"></a><span data-ttu-id="56402-132">Cloud-to-device commands</span><span class="sxs-lookup"><span data-stu-id="56402-132">Cloud-to-device commands</span></span>

<span data-ttu-id="56402-133">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span><span class="sxs-lookup"><span data-stu-id="56402-133">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="56402-134">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span><span class="sxs-lookup"><span data-stu-id="56402-134">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="56402-135">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span><span class="sxs-lookup"><span data-stu-id="56402-135">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

```json
{
    "time": " UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "messageExpired",
    "category": "C2DCommands",
    "level": "Error",
    "resultType": "Event status",
    "resultDescription": "MessageDescription",
    "properties": "{\"deviceId\":\"<deviceId>\",\"messageId\":\"<messageId>\",\"messageSizeInBytes\":\"<messageSize>\",\"protocol\":\"Amqp\",\"deliveryAcknowledgement\":\"<None, NegativeOnly, PositiveOnly, Full>\",\"deliveryCount\":\"0\",\"expiryTime\":\"<timestamp>\",\"timeInSystem\":\"<timeInSystem>\",\"ttl\":<ttl>, \"EventProcessedUtcTime\":\"<UTC timestamp>\",\"EventEnqueuedUtcTime\":\"<UTC timestamp>\", \"maskedIpAddresss\": \"<maskedIpAddress>\", \"statusCode\": \"4XX\"}",
    "location": "Resource location"
}
```

#### <a name="device-identity-operations"></a><span data-ttu-id="56402-136">Device identity operations</span><span class="sxs-lookup"><span data-stu-id="56402-136">Device identity operations</span></span>

<span data-ttu-id="56402-137">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="56402-137">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="56402-138">Tracking this category is useful for provisioning scenarios.</span><span class="sxs-lookup"><span data-stu-id="56402-138">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "get",
    "category": "DeviceIdentityOperations",
    "level": "Error",    
    "resultType": "Event status",
    "resultDescription": "MessageDescription",
    "properties": "{\"maskedIpAddress\":\"<maskedIpAddress>\",\"deviceId\":\"<deviceId>\", \"statusCode\":\"4XX\"}",
    "location": "Resource location"
}
```

#### <a name="routes"></a><span data-ttu-id="56402-139">Routes</span><span class="sxs-lookup"><span data-stu-id="56402-139">Routes</span></span>

<span data-ttu-id="56402-140">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="56402-140">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="56402-141">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span><span class="sxs-lookup"><span data-stu-id="56402-141">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="56402-142">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span><span class="sxs-lookup"><span data-stu-id="56402-142">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "endpointUnhealthy",
    "category": "Routes",
    "level": "Error",
    "properties": "{\"deviceId\": \"<deviceId>\",\"endpointName\":\"<endpointName>\",\"messageId\":<messageId>,\"details\":\"<errorDetails>\",\"routeName\": \"<routeName>\"}",
    "location": "Resource location"
}
```

#### <a name="device-telemetry"></a><span data-ttu-id="56402-143">Device telemetry</span><span class="sxs-lookup"><span data-stu-id="56402-143">Device telemetry</span></span>

<span data-ttu-id="56402-144">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span><span class="sxs-lookup"><span data-stu-id="56402-144">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="56402-145">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span><span class="sxs-lookup"><span data-stu-id="56402-145">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="56402-146">This category cannot catch errors caused by code running on the device itself.</span><span class="sxs-lookup"><span data-stu-id="56402-146">This category cannot catch errors caused by code running on the device itself.</span></span>

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "ingress",
    "category": "DeviceTelemetry",
    "level": "Error",
    "resultType": "Event status",
    "resultDescription": "MessageDescription",
    "properties": "{\"deviceId\":\"<deviceId>\",\"batching\":\"0\",\"messageSizeInBytes\":\"<messageSizeInBytes>\",\"EventProcessedUtcTime\":\"<UTC timestamp>\",\"EventEnqueuedUtcTime\":\"<UTC timestamp>\",\"partitionId\":\"1\"}", 
    "location": "Resource location"
}
```

#### <a name="file-upload-operations"></a><span data-ttu-id="56402-147">File upload operations</span><span class="sxs-lookup"><span data-stu-id="56402-147">File upload operations</span></span>

<span data-ttu-id="56402-148">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span><span class="sxs-lookup"><span data-stu-id="56402-148">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="56402-149">This category includes:</span><span class="sxs-lookup"><span data-stu-id="56402-149">This category includes:</span></span>

* <span data-ttu-id="56402-150">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span><span class="sxs-lookup"><span data-stu-id="56402-150">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="56402-151">Failed uploads reported by the device.</span><span class="sxs-lookup"><span data-stu-id="56402-151">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="56402-152">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span><span class="sxs-lookup"><span data-stu-id="56402-152">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="56402-153">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span><span class="sxs-lookup"><span data-stu-id="56402-153">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "ingress",
    "category": "FileUploadOperations",
    "level": "Error",
    "resultType": "Event status",
    "resultDescription": "MessageDescription",
    "durationMs": "1",
    "properties": "{\"deviceId\":\"<deviceId>\",\"protocol\":\"<protocol>\",\"authType\":\"{\\\"scope\\\":\\\"device\\\",\\\"type\\\":\\\"sas\\\",\\\"issuer\\\":\\\"iothub\\\",\\\"acceptingIpFilterRule\\\":null}\",\"blobUri\":\"http//bloburi.com\"}",
    "location": "Resource location"
}
```

#### <a name="cloud-to-device-twin-operations"></a><span data-ttu-id="56402-154">Cloud-to-device twin operations</span><span class="sxs-lookup"><span data-stu-id="56402-154">Cloud-to-device twin operations</span></span>

<span data-ttu-id="56402-155">The cloud-to-device twin operations category tracks service-initiated events on device twins.</span><span class="sxs-lookup"><span data-stu-id="56402-155">The cloud-to-device twin operations category tracks service-initiated events on device twins.</span></span> <span data-ttu-id="56402-156">These operations can include get twin, update or replace tags, and update or replace desired properties.</span><span class="sxs-lookup"><span data-stu-id="56402-156">These operations can include get twin, update or replace tags, and update or replace desired properties.</span></span> 

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "read",
    "category": "C2DTwinOperations",
    "level": "Information",
    "durationMs": "1",
    "properties": "{\"deviceId\":\"<deviceId>\",\"sdkVersion\":\"<sdkVersion>\",\"messageSize\":\"<messageSize>\"}", 
    "location": "Resource location"
}
```

#### <a name="device-to-cloud-twin-operations"></a><span data-ttu-id="56402-157">Device-to-cloud twin operations</span><span class="sxs-lookup"><span data-stu-id="56402-157">Device-to-cloud twin operations</span></span>

<span data-ttu-id="56402-158">The device-to-cloud twin operations category tracks device-initiated events on device twins.</span><span class="sxs-lookup"><span data-stu-id="56402-158">The device-to-cloud twin operations category tracks device-initiated events on device twins.</span></span> <span data-ttu-id="56402-159">These operations can include get twin, update reported properties, and subscribe to desired properties.</span><span class="sxs-lookup"><span data-stu-id="56402-159">These operations can include get twin, update reported properties, and subscribe to desired properties.</span></span>

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "update",
    "category": "D2CTwinOperations",
    "level": "Information",
    "durationMs": "1",
    "properties": "{\"deviceId\":\"<deviceId>\",\"protocol\":\"<protocol>\",\"authenticationType\":\"{\\\"scope\\\":\\\"device\\\",\\\"type\\\":\\\"sas\\\",\\\"issuer\\\":\\\"iothub\\\",\\\"acceptingIpFilterRule\\\":null}\"}", 
    "location": "Resource location"
}
```

#### <a name="twin-queries"></a><span data-ttu-id="56402-160">Twin queries</span><span class="sxs-lookup"><span data-stu-id="56402-160">Twin queries</span></span>

<span data-ttu-id="56402-161">The twin queries category reports on query requests for device twins that are initiated in the cloud.</span><span class="sxs-lookup"><span data-stu-id="56402-161">The twin queries category reports on query requests for device twins that are initiated in the cloud.</span></span> 

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "query",
    "category": "TwinQueries",
    "level": "Information",
    "durationMs": "1",
    "properties": "{\"query\":\"<twin query>\",\"sdkVersion\":\"<sdkVersion>\",\"messageSize\":\"<messageSize>\",\"pageSize\":\"<pageSize>\", \"continuation\":\"<true, false>\", \"resultSize\":\"<resultSize>\"}", 
    "location": "Resource location"
}
```

#### <a name="jobs-operations"></a><span data-ttu-id="56402-162">Jobs operations</span><span class="sxs-lookup"><span data-stu-id="56402-162">Jobs operations</span></span>

<span data-ttu-id="56402-163">The jobs operations category reports on job requests to update device twins or invoke direct methods on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="56402-163">The jobs operations category reports on job requests to update device twins or invoke direct methods on multiple devices.</span></span> <span data-ttu-id="56402-164">These requests are initiated in the cloud.</span><span class="sxs-lookup"><span data-stu-id="56402-164">These requests are initiated in the cloud.</span></span> 

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "jobCompleted",
    "category": "JobsOperations",
    "level": "Information",
    "durationMs": "1",
    "properties": "{\"jobId\":\"<jobId>\", \"sdkVersion\": \"<sdkVersion>\",\"messageSize\": <messageSize>,\"filter\":\"DeviceId IN ['1414ded9-b445-414d-89b9-e48e8c6285d5']\",\"startTimeUtc\":\"Wednesday, September 13, 2017\",\"duration\":\"0\"}", 
    "location": "Resource location"
}
```

#### <a name="direct-methods"></a><span data-ttu-id="56402-165">Direct Methods</span><span class="sxs-lookup"><span data-stu-id="56402-165">Direct Methods</span></span>

<span data-ttu-id="56402-166">The direct methods category tracks request-response interactions sent to individual devices.</span><span class="sxs-lookup"><span data-stu-id="56402-166">The direct methods category tracks request-response interactions sent to individual devices.</span></span> <span data-ttu-id="56402-167">These requests are initiated in the cloud.</span><span class="sxs-lookup"><span data-stu-id="56402-167">These requests are initiated in the cloud.</span></span> 

```json
{
    "time": "UTC timestamp",
    "resourceId": "Resource Id",
    "operationName": "send",
    "category": "DirectMethods",
    "level": "Information",
    "durationMs": "1",
    "properties": "{\"deviceId\":\"<deviceId>\", \"RequestSize\": 1, \"ResponseSize\": 1, \"sdkVersion\": \"2017-07-11\"}", 
    "location": "Resource location"
}
```

### <a name="read-logs-from-azure-event-hubs"></a><span data-ttu-id="56402-168">Read logs from Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="56402-168">Read logs from Azure Event Hubs</span></span>

<span data-ttu-id="56402-169">After you set up event logging through diagnostics settings, you can create applications that read out the logs so that you can take action based on the information in them.</span><span class="sxs-lookup"><span data-stu-id="56402-169">After you set up event logging through diagnostics settings, you can create applications that read out the logs so that you can take action based on the information in them.</span></span> <span data-ttu-id="56402-170">This sample code retrieves logs from an event hub:</span><span class="sxs-lookup"><span data-stu-id="56402-170">This sample code retrieves logs from an event hub:</span></span>

```csharp
class Program 
{ 
    static string connectionString = "{your AMS eventhub endpoint connection string}"; 
    static string monitoringEndpointName = "{your AMS event hub endpoint name}"; 
    static EventHubClient eventHubClient; 
//This is the Diagnostic Settings schema 
    class AzureMonitorDiagnosticLog 
    { 
        string time { get; set; } 
        string resourceId { get; set; } 
        string operationName { get; set; } 
        string category { get; set; } 
        string level { get; set; } 
        string resultType { get; set; } 
        string resultDescription { get; set; } 
        string durationMs { get; set; } 
        string callerIpAddress { get; set; } 
        string correlationId { get; set; } 
        string identity { get; set; } 
        string location { get; set; } 
        Dictionary<string, string> properties { get; set; } 
    }; 
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
                var deserializer = new JavaScriptSerializer(); 
                //deserialize json data to azure monitor object 
                AzureMonitorDiagnosticLog message = new JavaScriptSerializer().Deserialize<AzureMonitorDiagnosticLog>(result); 
 
            } 
        } 
    } 
} 
```

## <a name="use-azure-resource-health"></a><span data-ttu-id="56402-171">Use Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="56402-171">Use Azure Resource Health</span></span>

<span data-ttu-id="56402-172">Use Azure Resource Health to monitor whether your IoT hub is up and running.</span><span class="sxs-lookup"><span data-stu-id="56402-172">Use Azure Resource Health to monitor whether your IoT hub is up and running.</span></span> <span data-ttu-id="56402-173">You can also learn whether a regional outage is impacting the health of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="56402-173">You can also learn whether a regional outage is impacting the health of your IoT hub.</span></span> <span data-ttu-id="56402-174">To understand specific details about the health state of your Azure IoT Hub, we recommend that you [Use Azure Monitor](#use-azure-monitor).</span><span class="sxs-lookup"><span data-stu-id="56402-174">To understand specific details about the health state of your Azure IoT Hub, we recommend that you [Use Azure Monitor](#use-azure-monitor).</span></span> 

<span data-ttu-id="56402-175">Azure IoT Hub indicates health at a regional level.</span><span class="sxs-lookup"><span data-stu-id="56402-175">Azure IoT Hub indicates health at a regional level.</span></span> <span data-ttu-id="56402-176">If there a regional outage impacting your IoT hub, the health status shows as **Unknown**.</span><span class="sxs-lookup"><span data-stu-id="56402-176">If there a regional outage impacting your IoT hub, the health status shows as **Unknown**.</span></span> <span data-ttu-id="56402-177">To learn more about the specific health checks that Azure Resource Health performs, see [Resource types and health checks in Azure resource health][lnk-ARH-checks].</span><span class="sxs-lookup"><span data-stu-id="56402-177">To learn more about the specific health checks that Azure Resource Health performs, see [Resource types and health checks in Azure resource health][lnk-ARH-checks].</span></span>

<span data-ttu-id="56402-178">To check the health of your IoT hubs, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="56402-178">To check the health of your IoT hubs, follow these steps:</span></span>

1. <span data-ttu-id="56402-179">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="56402-179">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="56402-180">Navigate to **Service Health** > **Resource health**.</span><span class="sxs-lookup"><span data-stu-id="56402-180">Navigate to **Service Health** > **Resource health**.</span></span>
1. <span data-ttu-id="56402-181">From the drop-down boxes, select your subscription and **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="56402-181">From the drop-down boxes, select your subscription and **IoT Hub**.</span></span>

<span data-ttu-id="56402-182">To learn more about how to interpret health data, see [Azure resource health overview][lnk-ARH]</span><span class="sxs-lookup"><span data-stu-id="56402-182">To learn more about how to interpret health data, see [Azure resource health overview][lnk-ARH]</span></span>

## <a name="next-steps"></a><span data-ttu-id="56402-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="56402-183">Next steps</span></span>

- <span data-ttu-id="56402-184">[Understand IoT Hub metrics][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="56402-184">[Understand IoT Hub metrics][lnk-metrics]</span></span>
- <span data-ttu-id="56402-185">[IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox][lnk-monitoring-notifications]</span><span class="sxs-lookup"><span data-stu-id="56402-185">[IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox][lnk-monitoring-notifications]</span></span>


[lnk-AM]: ../monitoring-and-diagnostics/index.yml
[lnk-ARH]: ../service-health/resource-health-overview.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-migrate]: iot-hub-migrate-to-diagnostics-settings.md
[lnk-AM-metrics]: ../monitoring-and-diagnostics/monitoring-supported-metrics.md
[lnk-AM-schemas]: ../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md
[lnk-ARH-checks]: ../service-health/resource-health-checks-resource-types.md
[lnk-monitoring-notifications]: iot-hub-monitoring-notifications-with-azure-logic-apps.md
[lnk-devguide-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
