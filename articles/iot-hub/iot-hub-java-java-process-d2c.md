---
title: Process Azure IoT Hub device-to-cloud messages (Java) | Microsoft Docs
description: How to process IoT Hub device-to-cloud messages by using routing rules and custom endpoints to dispatch messages to other back-end services.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/07/2017
ms.author: dobett
ms.openlocfilehash: d3868184aae09164ab839fe2271e912fb1718c0a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552401"
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="2379a-103">Process IoT Hub device-to-cloud messages (Java)</span><span class="sxs-lookup"><span data-stu-id="2379a-103">Process IoT Hub device-to-cloud messages (Java)</span></span>
[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

## <a name="introduction"></a><span data-ttu-id="2379a-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="2379a-104">Introduction</span></span>
<span data-ttu-id="2379a-105">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="2379a-105">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="2379a-106">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2379a-106">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="2379a-107">This tutorial builds on the code shown in the [Get started with IoT Hub] tutorial, and shows you how to use message routing to process device-to-cloud messages in a scalable way.</span><span class="sxs-lookup"><span data-stu-id="2379a-107">This tutorial builds on the code shown in the [Get started with IoT Hub] tutorial, and shows you how to use message routing to process device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="2379a-108">The tutorial illustrates how to process messages that require immediate action from the solution back end.</span><span class="sxs-lookup"><span data-stu-id="2379a-108">The tutorial illustrates how to process messages that require immediate action from the solution back end.</span></span> <span data-ttu-id="2379a-109">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span><span class="sxs-lookup"><span data-stu-id="2379a-109">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="2379a-110">By contrast, data-point messages simply feed into an analytics engine.</span><span class="sxs-lookup"><span data-stu-id="2379a-110">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="2379a-111">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span><span class="sxs-lookup"><span data-stu-id="2379a-111">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="2379a-112">At the end of this tutorial, you run three Java console apps:</span><span class="sxs-lookup"><span data-stu-id="2379a-112">At the end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="2379a-113">**simulated-device**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="2379a-113">**simulated-device**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="2379a-114">This app uses the AMQP protocol to communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2379a-114">This app uses the AMQP protocol to communicate with IoT Hub.</span></span>
* <span data-ttu-id="2379a-115">**read-d2c-messages** displays the telemetry sent by your simulated device app.</span><span class="sxs-lookup"><span data-stu-id="2379a-115">**read-d2c-messages** displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="2379a-116">**read-critical-queue** de-queues the critical messages from the Service Bus queue attached to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2379a-116">**read-critical-queue** de-queues the critical messages from the Service Bus queue attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2379a-117">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2379a-117">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="2379a-118">For instructions on how to replace the simulated device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="2379a-118">For instructions on how to replace the simulated device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="2379a-119">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="2379a-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="2379a-120">A complete working version of the [Get started with IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="2379a-120">A complete working version of the [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="2379a-121">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="2379a-121">Java SE 8.</span></span> <br/> <span data-ttu-id="2379a-122">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="2379a-122">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2379a-123">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="2379a-123">Maven 3.</span></span>  <br/> <span data-ttu-id="2379a-124">[Prepare your development environment][lnk-dev-setup] describes how to install Maven for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="2379a-124">[Prepare your development environment][lnk-dev-setup] describes how to install Maven for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2379a-125">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="2379a-125">An active Azure account.</span></span> <br/><span data-ttu-id="2379a-126">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="2379a-126">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="2379a-127">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="2379a-127">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-simulated-device-app"></a><span data-ttu-id="2379a-128">Send interactive messages from a simulated device app</span><span class="sxs-lookup"><span data-stu-id="2379a-128">Send interactive messages from a simulated device app</span></span>
<span data-ttu-id="2379a-129">In this section, you modify the simulated device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span><span class="sxs-lookup"><span data-stu-id="2379a-129">In this section, you modify the simulated device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="2379a-130">Use a text editor to open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span><span class="sxs-lookup"><span data-stu-id="2379a-130">Use a text editor to open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="2379a-131">This file contains the code for the **simulated-device** app you created in the [Get started with IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="2379a-131">This file contains the code for the **simulated-device** app you created in the [Get started with IoT Hub] tutorial.</span></span>
2. <span data-ttu-id="2379a-132">Replace the **MessageSender** class with the following code:</span><span class="sxs-lookup"><span data-stu-id="2379a-132">Replace the **MessageSender** class with the following code:</span></span>
   
    ```
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    <span data-ttu-id="2379a-133">This method randomly adds the property `"level": "critical"` to messages sent by the simulated device, which simulates a message that requires immediate action by the application back-end.</span><span class="sxs-lookup"><span data-stu-id="2379a-133">This method randomly adds the property `"level": "critical"` to messages sent by the simulated device, which simulates a message that requires immediate action by the application back-end.</span></span> <span data-ttu-id="2379a-134">The application passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span><span class="sxs-lookup"><span data-stu-id="2379a-134">The application passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2379a-135">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot path example shown here.</span><span class="sxs-lookup"><span data-stu-id="2379a-135">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot path example shown here.</span></span>
   > 
   > 

2. <span data-ttu-id="2379a-136">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span><span class="sxs-lookup"><span data-stu-id="2379a-136">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2379a-137">For the sake of simplicity, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="2379a-137">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2379a-138">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span><span class="sxs-lookup"><span data-stu-id="2379a-138">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

3. <span data-ttu-id="2379a-139">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span><span class="sxs-lookup"><span data-stu-id="2379a-139">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>
   
    ```
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-to-your-iot-hub-and-route-messages-to-it"></a><span data-ttu-id="2379a-140">Add a queue to your IoT hub and route messages to it</span><span class="sxs-lookup"><span data-stu-id="2379a-140">Add a queue to your IoT hub and route messages to it</span></span>
<span data-ttu-id="2379a-141">In this section, you create a Service Bus queue, connect it to your IoT hub, and configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span><span class="sxs-lookup"><span data-stu-id="2379a-141">In this section, you create a Service Bus queue, connect it to your IoT hub, and configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span> <span data-ttu-id="2379a-142">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="2379a-142">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="2379a-143">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="2379a-143">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="2379a-144">Make a note of the namespace and queue name.</span><span class="sxs-lookup"><span data-stu-id="2379a-144">Make a note of the namespace and queue name.</span></span>

2. <span data-ttu-id="2379a-145">In the Azure portal, open your IoT hub and click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="2379a-145">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Endpoints in IoT hub][30]

3. <span data-ttu-id="2379a-147">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2379a-147">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="2379a-148">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span><span class="sxs-lookup"><span data-stu-id="2379a-148">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="2379a-149">When you are done, click **Save** at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2379a-149">When you are done, click **Save** at the bottom.</span></span>
    
    ![Adding an endpoint][31]
    
4. <span data-ttu-id="2379a-151">Now click **Routes** in your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2379a-151">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="2379a-152">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span><span class="sxs-lookup"><span data-stu-id="2379a-152">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="2379a-153">Select **DeviceTelemetry** as the source of data.</span><span class="sxs-lookup"><span data-stu-id="2379a-153">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="2379a-154">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span><span class="sxs-lookup"><span data-stu-id="2379a-154">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="2379a-155">When you are done, click **Save** at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2379a-155">When you are done, click **Save** at the bottom.</span></span>
    
    ![Adding a route][32]
    
    <span data-ttu-id="2379a-157">Make sure the fallback route is set to **ON**.</span><span class="sxs-lookup"><span data-stu-id="2379a-157">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="2379a-158">This setting is the default configuration of an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2379a-158">This setting is the default configuration of an IoT hub.</span></span>
    
    ![Fallback route][33]


## <a name="optional-read-from-the-queue-endpoint"></a><span data-ttu-id="2379a-160">(Optional) Read from the queue endpoint</span><span class="sxs-lookup"><span data-stu-id="2379a-160">(Optional) Read from the queue endpoint</span></span>
<span data-ttu-id="2379a-161">You can optionally read the messages from the queue endpoint by following the instructions in [Get started with queues][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="2379a-161">You can optionally read the messages from the queue endpoint by following the instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="2379a-162">Name the app **read-critical-queue**.</span><span class="sxs-lookup"><span data-stu-id="2379a-162">Name the app **read-critical-queue**.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="2379a-163">Run the applications</span><span class="sxs-lookup"><span data-stu-id="2379a-163">Run the applications</span></span>
<span data-ttu-id="2379a-164">Now you are ready to run the three applications.</span><span class="sxs-lookup"><span data-stu-id="2379a-164">Now you are ready to run the three applications.</span></span>

1. <span data-ttu-id="2379a-165">To run the **read-d2c-messages** application, in a command prompt or shell navigate to the read-d2c folder and execute the following command:</span><span class="sxs-lookup"><span data-stu-id="2379a-165">To run the **read-d2c-messages** application, in a command prompt or shell navigate to the read-d2c folder and execute the following command:</span></span>
   
   ```
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Run read-d2c-messages][readd2c]
2. <span data-ttu-id="2379a-167">To run the **read-critical-queue** application, in a command prompt or shell navigate to the read-critical-queue folder and execute the following command:</span><span class="sxs-lookup"><span data-stu-id="2379a-167">To run the **read-critical-queue** application, in a command prompt or shell navigate to the read-critical-queue folder and execute the following command:</span></span>
   
   ```
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Run read-critical-messages][readqueue]

3. <span data-ttu-id="2379a-169">To run the **simulated-device** app, in a command prompt or shell navigate to the simulated-device folder and execute the following command:</span><span class="sxs-lookup"><span data-stu-id="2379a-169">To run the **simulated-device** app, in a command prompt or shell navigate to the simulated-device folder and execute the following command:</span></span>
   
   ```
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Run simulated-device][simulateddevice]


## <a name="next-steps"></a><span data-ttu-id="2379a-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="2379a-171">Next steps</span></span>
<span data-ttu-id="2379a-172">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2379a-172">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>


<span data-ttu-id="2379a-173">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span><span class="sxs-lookup"><span data-stu-id="2379a-173">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="2379a-174">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="2379a-174">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="2379a-175">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span><span class="sxs-lookup"><span data-stu-id="2379a-175">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="2379a-176">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="2379a-176">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-process-d2c/route-creation.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[Azure blob storage]: ../storage/storage-dotnet-how-to-use-blobs.md
[Azure Data Factory]: https://azure.microsoft.com/documentation/services/data-factory/
[HDInsight (Hadoop)]: https://azure.microsoft.com/documentation/services/hdinsight/
[Service Bus queue]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md
[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[IoT Hub developer guide - Device to cloud]: iot-hub-devguide-messaging.md

[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[IoT Hub developer guide]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Get started with IoT Hub]: iot-hub-java-java-getstarted.md
[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot
[lnk-service-fabric]: https://azure.microsoft.com/documentation/services/service-fabric/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-hubs]: https://azure.microsoft.com/documentation/services/event-hubs/
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[About Azure Storage]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Get Started with Event Hubs]: ../event-hubs/event-hubs-java-ephjava-getstarted.md
[Azure Storage scalability Guidelines]: ../storage/storage-scalability-targets.md
[Azure Block Blobs]: https://msdn.microsoft.com/library/azure/ee691964.aspx
[Event Hubs]: ../event-hubs/event-hubs-overview.md
[EventProcessorHost]: https://github.com/Azure/azure-event-hubs/tree/master/java/azure-eventhubs-eph
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-c2d]: iot-hub-java-java-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[lnk-create-an-iot-hub]: iot-hub-java-java-getstarted.md#create-an-iot-hub







