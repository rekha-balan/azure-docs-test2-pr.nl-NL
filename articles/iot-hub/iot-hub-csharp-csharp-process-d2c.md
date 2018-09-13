---
title: Process Azure IoT Hub device-to-cloud messages using routes (.Net) | Microsoft Docs
description: How to process IoT Hub device-to-cloud messages by using routing rules and custom endpoints to dispatch messages to other back-end services.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/31/2017
ms.author: dobett
ms.openlocfilehash: 085772b275640f2509cecd535f6f493fce9011c1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551315"
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="b21e3-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span><span class="sxs-lookup"><span data-stu-id="b21e3-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

## <a name="introduction"></a><span data-ttu-id="b21e3-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="b21e3-104">Introduction</span></span>
<span data-ttu-id="b21e3-105">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="b21e3-105">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="b21e3-106">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b21e3-106">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="b21e3-107">This tutorial builds on the [Get started with IoT Hub] tutorial, and shows you how to use routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span><span class="sxs-lookup"><span data-stu-id="b21e3-107">This tutorial builds on the [Get started with IoT Hub] tutorial, and shows you how to use routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span> <span data-ttu-id="b21e3-108">The tutorial illustrates how to isolate messages that require immediate action from the solution back end for further processing.</span><span class="sxs-lookup"><span data-stu-id="b21e3-108">The tutorial illustrates how to isolate messages that require immediate action from the solution back end for further processing.</span></span> <span data-ttu-id="b21e3-109">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span><span class="sxs-lookup"><span data-stu-id="b21e3-109">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="b21e3-110">By contrast, data-point messages simply feed into an analytics engine.</span><span class="sxs-lookup"><span data-stu-id="b21e3-110">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="b21e3-111">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span><span class="sxs-lookup"><span data-stu-id="b21e3-111">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="b21e3-112">At the end of this tutorial, you run three .NET console apps:</span><span class="sxs-lookup"><span data-stu-id="b21e3-112">At the end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="b21e3-113">**SimulatedDevice**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="b21e3-113">**SimulatedDevice**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="b21e3-114">This app uses the AMQP protocol to communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b21e3-114">This app uses the AMQP protocol to communicate with IoT Hub.</span></span>
* <span data-ttu-id="b21e3-115">**ReadDeviceToCloudMessages** that displays the non-critical telemetry sent by your simulated device app.</span><span class="sxs-lookup"><span data-stu-id="b21e3-115">**ReadDeviceToCloudMessages** that displays the non-critical telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="b21e3-116">**ReadCriticalQueue** de-queues the critical messages sent by your simulated device app from the Service Bus queue attached to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b21e3-116">**ReadCriticalQueue** de-queues the critical messages sent by your simulated device app from the Service Bus queue attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b21e3-117">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b21e3-117">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="b21e3-118">To learn how to replace the simulated device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="b21e3-118">To learn how to replace the simulated device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="b21e3-119">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="b21e3-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b21e3-120">Visual Studio 2015 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b21e3-120">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b21e3-121">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="b21e3-121">An active Azure account.</span></span> <br/><span data-ttu-id="b21e3-122">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="b21e3-122">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="b21e3-123">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="b21e3-123">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-simulated-device-app"></a><span data-ttu-id="b21e3-124">Send interactive messages from a simulated device app</span><span class="sxs-lookup"><span data-stu-id="b21e3-124">Send interactive messages from a simulated device app</span></span>
<span data-ttu-id="b21e3-125">In this section, you modify the simulated device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span><span class="sxs-lookup"><span data-stu-id="b21e3-125">In this section, you modify the simulated device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span></span>

<span data-ttu-id="b21e3-126">In Visual Studio, in the **SimulatedDevice** project, replace the `SendDeviceToCloudMessagesAsync` method with the following code:</span><span class="sxs-lookup"><span data-stu-id="b21e3-126">In Visual Studio, in the **SimulatedDevice** project, replace the `SendDeviceToCloudMessagesAsync` method with the following code:</span></span>

```
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

<span data-ttu-id="b21e3-127">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the solution back-end.</span><span class="sxs-lookup"><span data-stu-id="b21e3-127">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the solution back-end.</span></span> <span data-ttu-id="b21e3-128">The device app passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span><span class="sxs-lookup"><span data-stu-id="b21e3-128">The device app passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="b21e3-129">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot-path example shown here.</span><span class="sxs-lookup"><span data-stu-id="b21e3-129">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="b21e3-130">For the sake of simplicity, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="b21e3-130">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b21e3-131">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span><span class="sxs-lookup"><span data-stu-id="b21e3-131">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="add-a-queue-to-your-iot-hub-and-route-messages-to-it"></a><span data-ttu-id="b21e3-132">Add a queue to your IoT hub and route messages to it</span><span class="sxs-lookup"><span data-stu-id="b21e3-132">Add a queue to your IoT hub and route messages to it</span></span>
<span data-ttu-id="b21e3-133">In this section, you:</span><span class="sxs-lookup"><span data-stu-id="b21e3-133">In this section, you:</span></span>

* <span data-ttu-id="b21e3-134">Create a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="b21e3-134">Create a Service Bus queue.</span></span>
* <span data-ttu-id="b21e3-135">Connect it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b21e3-135">Connect it to your IoT hub.</span></span>
* <span data-ttu-id="b21e3-136">Configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span><span class="sxs-lookup"><span data-stu-id="b21e3-136">Configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span>

<span data-ttu-id="b21e3-137">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="b21e3-137">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="b21e3-138">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="b21e3-138">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="b21e3-139">The queue must be in the same subscription and region as your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b21e3-139">The queue must be in the same subscription and region as your IoT hub.</span></span> <span data-ttu-id="b21e3-140">Make a note of the namespace and queue name.</span><span class="sxs-lookup"><span data-stu-id="b21e3-140">Make a note of the namespace and queue name.</span></span>

2. <span data-ttu-id="b21e3-141">In the Azure portal, open your IoT hub and click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="b21e3-141">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Endpoints in IoT hub][30]

3. <span data-ttu-id="b21e3-143">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b21e3-143">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="b21e3-144">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span><span class="sxs-lookup"><span data-stu-id="b21e3-144">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="b21e3-145">When you are done, click **Save** at the bottom.</span><span class="sxs-lookup"><span data-stu-id="b21e3-145">When you are done, click **Save** at the bottom.</span></span>
    
    ![Adding an endpoint][31]
    
4. <span data-ttu-id="b21e3-147">Now click **Routes** in your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b21e3-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="b21e3-148">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span><span class="sxs-lookup"><span data-stu-id="b21e3-148">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="b21e3-149">Select **DeviceTelemetry** as the source of data.</span><span class="sxs-lookup"><span data-stu-id="b21e3-149">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="b21e3-150">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span><span class="sxs-lookup"><span data-stu-id="b21e3-150">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="b21e3-151">When you are done, click **Save** at the bottom.</span><span class="sxs-lookup"><span data-stu-id="b21e3-151">When you are done, click **Save** at the bottom.</span></span>
    
    ![Adding a route][32]
    
    <span data-ttu-id="b21e3-153">Make sure the fallback route is set to **ON**.</span><span class="sxs-lookup"><span data-stu-id="b21e3-153">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="b21e3-154">This value is the default configuration for an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b21e3-154">This value is the default configuration for an IoT hub.</span></span>
    
    ![Fallback route][33]

## <a name="read-from-the-queue-endpoint"></a><span data-ttu-id="b21e3-156">Read from the queue endpoint</span><span class="sxs-lookup"><span data-stu-id="b21e3-156">Read from the queue endpoint</span></span>
<span data-ttu-id="b21e3-157">In this section, you read the messages from the queue endpoint.</span><span class="sxs-lookup"><span data-stu-id="b21e3-157">In this section, you read the messages from the queue endpoint.</span></span>

1. <span data-ttu-id="b21e3-158">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span><span class="sxs-lookup"><span data-stu-id="b21e3-158">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="b21e3-159">Name the project **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="b21e3-159">Name the project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="b21e3-160">In Solution Explorer, right-click the **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="b21e3-160">In Solution Explorer, right-click the **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="b21e3-161">This operation displays the **NuGet Package Manager** window.</span><span class="sxs-lookup"><span data-stu-id="b21e3-161">This operation displays the **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="b21e3-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept the terms of use.</span><span class="sxs-lookup"><span data-stu-id="b21e3-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept the terms of use.</span></span> <span data-ttu-id="b21e3-163">This operation downloads, installs, and adds a reference to the Azure Service Bus, with all its dependencies.</span><span class="sxs-lookup"><span data-stu-id="b21e3-163">This operation downloads, installs, and adds a reference to the Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="b21e3-164">Add the following **using** statements at the top of the **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="b21e3-164">Add the following **using** statements at the top of the **Program.cs** file:</span></span>
   
    ```
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="b21e3-165">Finally, add the following lines to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="b21e3-165">Finally, add the following lines to the **Main** method.</span></span> <span data-ttu-id="b21e3-166">Substitute the connection string with **Listen** permissions for the queue:</span><span class="sxs-lookup"><span data-stu-id="b21e3-166">Substitute the connection string with **Listen** permissions for the queue:</span></span>
   
    ```
    Console.WriteLine("Receive critical messages. Ctrl-C to exit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="b21e3-167">Run the applications</span><span class="sxs-lookup"><span data-stu-id="b21e3-167">Run the applications</span></span>
<span data-ttu-id="b21e3-168">Now you are ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="b21e3-168">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="b21e3-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span><span class="sxs-lookup"><span data-stu-id="b21e3-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="b21e3-170">Select **Multiple startup projects**, then select **Start** as the action for the **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span><span class="sxs-lookup"><span data-stu-id="b21e3-170">Select **Multiple startup projects**, then select **Start** as the action for the **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="b21e3-171">Press **F5** to start the three console apps.</span><span class="sxs-lookup"><span data-stu-id="b21e3-171">Press **F5** to start the three console apps.</span></span> <span data-ttu-id="b21e3-172">The **ReadDeviceToCloudMessages** app has only non-critical messages sent from the **SimulatedDevice** application, and the **ReadCriticalQueue** app has only critical messages.</span><span class="sxs-lookup"><span data-stu-id="b21e3-172">The **ReadDeviceToCloudMessages** app has only non-critical messages sent from the **SimulatedDevice** application, and the **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Three console apps][50]

## <a name="next-steps"></a><span data-ttu-id="b21e3-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="b21e3-174">Next steps</span></span>
<span data-ttu-id="b21e3-175">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b21e3-175">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="b21e3-176">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span><span class="sxs-lookup"><span data-stu-id="b21e3-176">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="b21e3-177">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="b21e3-177">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="b21e3-178">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span><span class="sxs-lookup"><span data-stu-id="b21e3-178">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="b21e3-179">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="b21e3-179">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-process-d2c/run1.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-process-d2c/create-identity-csharp1.png

[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->

[Azure blob storage]: ../storage/storage-dotnet-how-to-use-blobs.md
[Azure Data Factory]: https://azure.microsoft.com/documentation/services/data-factory/
[HDInsight (Hadoop)]: https://azure.microsoft.com/documentation/services/hdinsight/
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md

[IoT Hub developer guide - Device to cloud]: iot-hub-devguide-messaging.md

[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[IoT Hub developer guide]: iot-hub-devguide.md
[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot
[lnk-service-fabric]: https://azure.microsoft.com/documentation/services/service-fabric/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-hubs]: https://azure.microsoft.com/documentation/services/event-hubs/
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[About Azure Storage]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Get Started with Event Hubs]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[Azure Storage scalability Guidelines]: ../storage/storage-scalability-targets.md
[Azure Block Blobs]: https://msdn.microsoft.com/library/azure/ee691964.aspx
[Event Hubs]: ../event-hubs/event-hubs-overview.md
[EventProcessorHost]: http://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventprocessorhost(v=azure.95).aspx
[Event Hubs Programming Guide]: ../event-hubs/event-hubs-programming-guide.md
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Build multi-tier applications with Service Bus]: ../service-bus-messaging/service-bus-dotnet-multi-tier-app-using-service-bus-queues.md

[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/






