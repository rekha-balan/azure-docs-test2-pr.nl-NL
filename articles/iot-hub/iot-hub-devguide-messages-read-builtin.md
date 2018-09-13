---
title: Understand the Azure IoT Hub built-in endpoint | Microsoft Docs
description: Developer guide - describes how to use the built-in, Event Hub-compatible endpoint toread device-to-cloud messages.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 07/18/2018
ms.author: dobett
ms.openlocfilehash: 767c91e4926e553b63b8331ac99edcd7823d2c13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968009"
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="e1ead-103">Read device-to-cloud messages from the built-in endpoint</span><span class="sxs-lookup"><span data-stu-id="e1ead-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="e1ead-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**) that is compatible with [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="e1ead-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**) that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="e1ead-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span><span class="sxs-lookup"><span data-stu-id="e1ead-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="e1ead-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span><span class="sxs-lookup"><span data-stu-id="e1ead-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="e1ead-107">Property</span><span class="sxs-lookup"><span data-stu-id="e1ead-107">Property</span></span>            | <span data-ttu-id="e1ead-108">Description</span><span class="sxs-lookup"><span data-stu-id="e1ead-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="e1ead-109">**Partition count**</span><span class="sxs-lookup"><span data-stu-id="e1ead-109">**Partition count**</span></span> | <span data-ttu-id="e1ead-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span><span class="sxs-lookup"><span data-stu-id="e1ead-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="e1ead-111">**Retention time**</span><span class="sxs-lookup"><span data-stu-id="e1ead-111">**Retention time**</span></span>  | <span data-ttu-id="e1ead-112">This property specifies how long in days messages are retained by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e1ead-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="e1ead-113">The default is one day, but it can be increased to seven days.</span><span class="sxs-lookup"><span data-stu-id="e1ead-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="e1ead-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ead-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="e1ead-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ead-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="e1ead-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span><span class="sxs-lookup"><span data-stu-id="e1ead-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="e1ead-117">You can modify the retention time, either programmatically using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or with the [Azure portal][lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="e1ead-117">You can modify the retention time, either programmatically using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or with the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="e1ead-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span><span class="sxs-lookup"><span data-stu-id="e1ead-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="e1ead-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span><span class="sxs-lookup"><span data-stu-id="e1ead-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="e1ead-120">Read from the built-in endpoint</span><span class="sxs-lookup"><span data-stu-id="e1ead-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="e1ead-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span><span class="sxs-lookup"><span data-stu-id="e1ead-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="e1ead-122">Then use **messages/events** as the Event Hub name.</span><span class="sxs-lookup"><span data-stu-id="e1ead-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="e1ead-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name:</span><span class="sxs-lookup"><span data-stu-id="e1ead-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name:</span></span>

1. <span data-ttu-id="e1ead-124">Sign in to the [Azure portal][lnk-management-portal] and navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e1ead-124">Sign in to the [Azure portal][lnk-management-portal] and navigate to your IoT hub.</span></span>
1. <span data-ttu-id="e1ead-125">Click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="e1ead-125">Click **Endpoints**.</span></span>
1. <span data-ttu-id="e1ead-126">In the **Built-in endpoints** section, click **Events**.</span><span class="sxs-lookup"><span data-stu-id="e1ead-126">In the **Built-in endpoints** section, click **Events**.</span></span> 
1. <span data-ttu-id="e1ead-127">A properties page opens, which contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span><span class="sxs-lookup"><span data-stu-id="e1ead-127">A properties page opens, which contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Device-to-cloud settings][img-eventhubcompatible]

<span data-ttu-id="e1ead-129">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown under **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="e1ead-129">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown under **Endpoints**.</span></span>

<span data-ttu-id="e1ead-130">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span><span class="sxs-lookup"><span data-stu-id="e1ead-130">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="e1ead-131">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="e1ead-131">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**.</span></span> <span data-ttu-id="e1ead-132">The **Namespace** would be **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="e1ead-132">The **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="e1ead-133">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e1ead-133">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="e1ead-134">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span><span class="sxs-lookup"><span data-stu-id="e1ead-134">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="e1ead-135">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span><span class="sxs-lookup"><span data-stu-id="e1ead-135">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="e1ead-136">[Java Event Hubs client](https://github.com/Azure/azure-event-hubs-java).</span><span class="sxs-lookup"><span data-stu-id="e1ead-136">[Java Event Hubs client](https://github.com/Azure/azure-event-hubs-java).</span></span>
* <span data-ttu-id="e1ead-137">[Apache Storm spout](../hdinsight/storm/apache-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e1ead-137">[Apache Storm spout](../hdinsight/storm/apache-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="e1ead-138">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="e1ead-138">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="e1ead-139">[Apache Spark integration](../hdinsight/spark/apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="e1ead-139">[Apache Spark integration](../hdinsight/spark/apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1ead-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1ead-140">Next steps</span></span>

<span data-ttu-id="e1ead-141">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="e1ead-141">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="e1ead-142">The [Quickstarts][lnk-get-started] show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span><span class="sxs-lookup"><span data-stu-id="e1ead-142">The [Quickstarts][lnk-get-started] show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="e1ead-143">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1ead-143">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="e1ead-144">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="e1ead-144">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: quickstart-send-telemetry-node.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: tutorial-routing.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: https://docs.microsoft.com/azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph
[lnk-amqp]: https://www.amqp.org/
