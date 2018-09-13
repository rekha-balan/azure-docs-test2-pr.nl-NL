---
title: Cloud-to-device messages with Azure IoT Hub (Java) | Microsoft Docs
description: How to send cloud-to-device messages to a device from an Azure IoT hub using the Azure IoT SDKs for Java. You modify a simulated device app to receive cloud-to-device messages and modify a back-end app to send the cloud-to-device messages.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/07/2017
ms.author: dobett
ms.openlocfilehash: 43ce2481a622e403804de07c2c049f4470ece66f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549292"
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="d38b7-104">Send cloud-to-device messages with IoT Hub (Java)</span><span class="sxs-lookup"><span data-stu-id="d38b7-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="d38b7-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="d38b7-105">Introduction</span></span>
<span data-ttu-id="d38b7-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="d38b7-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="d38b7-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="d38b7-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="d38b7-108">This tutorial builds on [Get started with IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="d38b7-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="d38b7-109">It shows you how to:</span><span class="sxs-lookup"><span data-stu-id="d38b7-109">It shows you how to:</span></span>

* <span data-ttu-id="d38b7-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d38b7-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="d38b7-111">Receive cloud-to-device messages on a device.</span><span class="sxs-lookup"><span data-stu-id="d38b7-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="d38b7-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d38b7-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="d38b7-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="d38b7-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="d38b7-114">At the end of this tutorial, you run two Java console apps:</span><span class="sxs-lookup"><span data-stu-id="d38b7-114">At the end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="d38b7-115">**simulated-device**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="d38b7-115">**simulated-device**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="d38b7-116">**send-c2d-messages**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span><span class="sxs-lookup"><span data-stu-id="d38b7-116">**send-c2d-messages**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="d38b7-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="d38b7-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="d38b7-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="d38b7-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="d38b7-119">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="d38b7-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d38b7-120">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="d38b7-120">Java SE 8.</span></span> <br/> <span data-ttu-id="d38b7-121">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="d38b7-121">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d38b7-122">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="d38b7-122">Maven 3.</span></span>  <br/> <span data-ttu-id="d38b7-123">[Prepare your development environment][lnk-dev-setup] describes how to install Maven for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="d38b7-123">[Prepare your development environment][lnk-dev-setup] describes how to install Maven for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d38b7-124">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="d38b7-124">An active Azure account.</span></span> <span data-ttu-id="d38b7-125">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="d38b7-125">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="d38b7-126">Receive messages in the simulated device app</span><span class="sxs-lookup"><span data-stu-id="d38b7-126">Receive messages in the simulated device app</span></span>
<span data-ttu-id="d38b7-127">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d38b7-127">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="d38b7-128">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span><span class="sxs-lookup"><span data-stu-id="d38b7-128">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>
2. <span data-ttu-id="d38b7-129">Add the following **MessageCallback** class as a nested class inside the **App** class.</span><span class="sxs-lookup"><span data-stu-id="d38b7-129">Add the following **MessageCallback** class as a nested class inside the **App** class.</span></span> <span data-ttu-id="d38b7-130">The **execute** method is invoked when the device receives a message from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d38b7-130">The **execute** method is invoked when the device receives a message from IoT Hub.</span></span> <span data-ttu-id="d38b7-131">In this example, the device always notifies the IoT hub that it has completed the message:</span><span class="sxs-lookup"><span data-stu-id="d38b7-131">In this example, the device always notifies the IoT hub that it has completed the message:</span></span>
   
    ```
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="d38b7-132">Modify the **main** method to create an **AppMessageCallback** instance and call the **setMessageCallback** method before it opens the client as follows:</span><span class="sxs-lookup"><span data-stu-id="d38b7-132">Modify the **main** method to create an **AppMessageCallback** instance and call the **setMessageCallback** method before it opens the client as follows:</span></span>
   
    ```
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d38b7-133">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span><span class="sxs-lookup"><span data-stu-id="d38b7-133">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="d38b7-134">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="d38b7-134">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="d38b7-135">Send a cloud-to-device message</span><span class="sxs-lookup"><span data-stu-id="d38b7-135">Send a cloud-to-device message</span></span>
<span data-ttu-id="d38b7-136">In this section, you create a Java console app that sends cloud-to-device messages to the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="d38b7-136">In this section, you create a Java console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="d38b7-137">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="d38b7-137">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="d38b7-138">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d38b7-138">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="d38b7-139">Create a Maven project called **send-c2d-messages** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="d38b7-139">Create a Maven project called **send-c2d-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="d38b7-140">Note this command is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="d38b7-140">Note this command is a single, long command:</span></span>
   
    ```
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```
2. <span data-ttu-id="d38b7-141">At your command prompt, navigate to the new send-c2d-messages folder.</span><span class="sxs-lookup"><span data-stu-id="d38b7-141">At your command prompt, navigate to the new send-c2d-messages folder.</span></span>
3. <span data-ttu-id="d38b7-142">Using a text editor, open the pom.xml file in the send-c2d-messages folder and add the following dependency to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="d38b7-142">Using a text editor, open the pom.xml file in the send-c2d-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="d38b7-143">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span><span class="sxs-lookup"><span data-stu-id="d38b7-143">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>
   
    ```
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.2.18</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d38b7-144">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="d38b7-144">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="d38b7-145">Save and close the pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="d38b7-145">Save and close the pom.xml file.</span></span>
5. <span data-ttu-id="d38b7-146">Using a text editor, open the send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span><span class="sxs-lookup"><span data-stu-id="d38b7-146">Using a text editor, open the send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>
6. <span data-ttu-id="d38b7-147">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="d38b7-147">Add the following **import** statements to the file:</span></span>
   
    ```
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```
7. <span data-ttu-id="d38b7-148">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with the values your noted earlier:</span><span class="sxs-lookup"><span data-stu-id="d38b7-148">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with the values your noted earlier:</span></span>
   
    ```
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```
8. <span data-ttu-id="d38b7-149">Replace the **main** method with the following code.</span><span class="sxs-lookup"><span data-stu-id="d38b7-149">Replace the **main** method with the following code.</span></span> <span data-ttu-id="d38b7-150">This code connects to your IoT hub, sends a message to your device, and then waits for an acknowledgment that the device received and processed the message:</span><span class="sxs-lookup"><span data-stu-id="d38b7-150">This code connects to your IoT hub, sends a message to your device, and then waits for an acknowledgment that the device received and processed the message:</span></span>
   
    ```
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver(deviceId);
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud to device message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent to device");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d38b7-151">For simplicity's sake, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="d38b7-151">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d38b7-152">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span><span class="sxs-lookup"><span data-stu-id="d38b7-152">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="run-the-applications"></a><span data-ttu-id="d38b7-153">Run the applications</span><span class="sxs-lookup"><span data-stu-id="d38b7-153">Run the applications</span></span>
<span data-ttu-id="d38b7-154">You are now ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="d38b7-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="d38b7-155">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry to your IoT hub and to listen for cloud-to-device messages sent from your hub:</span><span class="sxs-lookup"><span data-stu-id="d38b7-155">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry to your IoT hub and to listen for cloud-to-device messages sent from your hub:</span></span>
   
    ```
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```
   
    ![Run the simulated device app][img-simulated-device]
2. <span data-ttu-id="d38b7-157">At a command prompt in the send-c2d-messages folder, run the following command to send a cloud-to-device message and wait for a feedback acknowledgment:</span><span class="sxs-lookup"><span data-stu-id="d38b7-157">At a command prompt in the send-c2d-messages folder, run the following command to send a cloud-to-device message and wait for a feedback acknowledgment:</span></span>
   
    ```
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```
   
    ![Run the command to send the cloud-to-device message][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="d38b7-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="d38b7-159">Next steps</span></span>
<span data-ttu-id="d38b7-160">In this tutorial, you learned how to send and receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="d38b7-160">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="d38b7-161">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="d38b7-161">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="d38b7-162">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span><span class="sxs-lookup"><span data-stu-id="d38b7-162">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[Get started with IoT Hub]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IoT Hub developer guide]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure portal]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22

