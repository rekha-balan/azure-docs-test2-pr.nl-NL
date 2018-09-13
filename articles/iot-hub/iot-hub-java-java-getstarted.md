---
title: Get started with Azure IoT Hub (Java) | Microsoft Docs
description: How to send device-to-cloud messages from a device to an Azure IoT hub using the Azure IoT SDKs for Java. You create a simulated device app to send messages, a service app to register your device in the identity registry, and a service app to read the device-to-cloud messages from the IoT hub.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/07/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06c78d4b949a47804d67c5815ffd217f0e851f4e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661099"
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-java"></a><span data-ttu-id="d3278-104">Connect your simulated device to your IoT hub using Java</span><span class="sxs-lookup"><span data-stu-id="d3278-104">Connect your simulated device to your IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="d3278-105">At the end of this tutorial, you have three Java console apps:</span><span class="sxs-lookup"><span data-stu-id="d3278-105">At the end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="d3278-106">**create-device-identity**, which creates a device identity and associated security key to connect your simulated device app.</span><span class="sxs-lookup"><span data-stu-id="d3278-106">**create-device-identity**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="d3278-107">**read-d2c-messages**, which displays the telemetry sent by your simulated device app.</span><span class="sxs-lookup"><span data-stu-id="d3278-107">**read-d2c-messages**, which displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="d3278-108">**simulated-device**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="d3278-108">**simulated-device**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="d3278-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both apps to run on devices and your solution back end.</span><span class="sxs-lookup"><span data-stu-id="d3278-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both apps to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="d3278-110">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="d3278-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d3278-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="d3278-111">Java SE 8.</span></span> <br/> <span data-ttu-id="d3278-112">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="d3278-112">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d3278-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="d3278-113">Maven 3.</span></span>  <br/> <span data-ttu-id="d3278-114">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="d3278-114">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d3278-115">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="d3278-115">An active Azure account.</span></span> <span data-ttu-id="d3278-116">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="d3278-116">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="d3278-117">As a final step, make a note of the **Primary key** value.</span><span class="sxs-lookup"><span data-stu-id="d3278-117">As a final step, make a note of the **Primary key** value.</span></span> <span data-ttu-id="d3278-118">Then click **Endpoints** and the **Events** built-in endpoint.</span><span class="sxs-lookup"><span data-stu-id="d3278-118">Then click **Endpoints** and the **Events** built-in endpoint.</span></span> <span data-ttu-id="d3278-119">On the **Properties** blade, make a note of the **Event Hub-compatible name** and the **Event Hub-compatible endpoint** address.</span><span class="sxs-lookup"><span data-stu-id="d3278-119">On the **Properties** blade, make a note of the **Event Hub-compatible name** and the **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="d3278-120">You need these three values when you create your **read-d2c-messages** app.</span><span class="sxs-lookup"><span data-stu-id="d3278-120">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Azure portal IoT Hub Messaging blade][6]

<span data-ttu-id="d3278-122">You have now created your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3278-122">You have now created your IoT hub.</span></span> <span data-ttu-id="d3278-123">You have the IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d3278-123">You have the IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need to complete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="d3278-124">Create a device identity</span><span class="sxs-lookup"><span data-stu-id="d3278-124">Create a device identity</span></span>
<span data-ttu-id="d3278-125">In this section, you create a Java console app that creates a device identity in the identity registry in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3278-125">In this section, you create a Java console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="d3278-126">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span><span class="sxs-lookup"><span data-stu-id="d3278-126">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="d3278-127">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d3278-127">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="d3278-128">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d3278-128">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="d3278-129">Create an empty folder called iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="d3278-129">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="d3278-130">In the iot-java-get-started folder, create a Maven project called **create-device-identity** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="d3278-130">In the iot-java-get-started folder, create a Maven project called **create-device-identity** using the following command at your command prompt.</span></span> <span data-ttu-id="d3278-131">Note this is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="d3278-131">Note this is a single, long command:</span></span>
   
    ```
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```
2. <span data-ttu-id="d3278-132">At your command prompt, navigate to the create-device-identity folder.</span><span class="sxs-lookup"><span data-stu-id="d3278-132">At your command prompt, navigate to the create-device-identity folder.</span></span>
3. <span data-ttu-id="d3278-133">Using a text editor, open the pom.xml file in the create-device-identity folder and add the following dependency to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="d3278-133">Using a text editor, open the pom.xml file in the create-device-identity folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="d3278-134">This dependency enables you to use the iot-service-client package in your app:</span><span class="sxs-lookup"><span data-stu-id="d3278-134">This dependency enables you to use the iot-service-client package in your app:</span></span>
   
    ```
    </dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.2.18</version>
    </dependency>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="d3278-135">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="d3278-135">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="d3278-136">Save and close the pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="d3278-136">Save and close the pom.xml file.</span></span>
5. <span data-ttu-id="d3278-137">Using a text editor, open the create-device-identity\src\main\java\com\mycompany\app\App.java file.</span><span class="sxs-lookup"><span data-stu-id="d3278-137">Using a text editor, open the create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>
6. <span data-ttu-id="d3278-138">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="d3278-138">Add the following **import** statements to the file:</span></span>
   
    ```
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```
7. <span data-ttu-id="d3278-139">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** with the value your noted earlier:</span><span class="sxs-lookup"><span data-stu-id="d3278-139">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** with the value your noted earlier:</span></span>
   
    ```
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
   
    ```
8. <span data-ttu-id="d3278-140">Modify the signature of the **main** method to include the exceptions as follows:</span><span class="sxs-lookup"><span data-stu-id="d3278-140">Modify the signature of the **main** method to include the exceptions as follows:</span></span>
   
    ```
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```
9. <span data-ttu-id="d3278-141">Add the following code as the body of the **main** method.</span><span class="sxs-lookup"><span data-stu-id="d3278-141">Add the following code as the body of the **main** method.</span></span> <span data-ttu-id="d3278-142">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span><span class="sxs-lookup"><span data-stu-id="d3278-142">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="d3278-143">It then displays the device ID and key that you need later:</span><span class="sxs-lookup"><span data-stu-id="d3278-143">It then displays the device ID and key that you need later:</span></span>
   
    ```
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
   
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }
    System.out.println("Device ID: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```
10. <span data-ttu-id="d3278-144">Save and close the App.java file.</span><span class="sxs-lookup"><span data-stu-id="d3278-144">Save and close the App.java file.</span></span>
11. <span data-ttu-id="d3278-145">To build the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span><span class="sxs-lookup"><span data-stu-id="d3278-145">To build the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>
    
    ```
    mvn clean package -DskipTests
    ```
12. <span data-ttu-id="d3278-146">To run the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span><span class="sxs-lookup"><span data-stu-id="d3278-146">To run the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>
    
    ```
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```
13. <span data-ttu-id="d3278-147">Make a note of the **Device ID** and **Device key**.</span><span class="sxs-lookup"><span data-stu-id="d3278-147">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="d3278-148">You need these values later when you create an app that connects to IoT Hub as a device.</span><span class="sxs-lookup"><span data-stu-id="d3278-148">You need these values later when you create an app that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="d3278-149">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3278-149">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="d3278-150">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span><span class="sxs-lookup"><span data-stu-id="d3278-150">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="d3278-151">If your app needs to store other device-specific metadata, it should use an app-specific store.</span><span class="sxs-lookup"><span data-stu-id="d3278-151">If your app needs to store other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="d3278-152">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d3278-152">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="d3278-153">Receive device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="d3278-153">Receive device-to-cloud messages</span></span>
<span data-ttu-id="d3278-154">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d3278-154">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="d3278-155">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="d3278-155">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="d3278-156">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span><span class="sxs-lookup"><span data-stu-id="d3278-156">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="d3278-157">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span><span class="sxs-lookup"><span data-stu-id="d3278-157">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="d3278-158">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span><span class="sxs-lookup"><span data-stu-id="d3278-158">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="d3278-159">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span><span class="sxs-lookup"><span data-stu-id="d3278-159">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="d3278-160">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **read-d2c-messages** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="d3278-160">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **read-d2c-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="d3278-161">Note this is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="d3278-161">Note this is a single, long command:</span></span>
   
    ```
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```
2. <span data-ttu-id="d3278-162">At your command prompt, navigate to the read-d2c-messages folder.</span><span class="sxs-lookup"><span data-stu-id="d3278-162">At your command prompt, navigate to the read-d2c-messages folder.</span></span>
3. <span data-ttu-id="d3278-163">Using a text editor, open the pom.xml file in the read-d2c-messages folder and add the following dependency to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="d3278-163">Using a text editor, open the pom.xml file in the read-d2c-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="d3278-164">This dependency enables you to use the eventhubs-client package in your app to read from the Event Hub-compatible endpoint:</span><span class="sxs-lookup"><span data-stu-id="d3278-164">This dependency enables you to use the eventhubs-client package in your app to read from the Event Hub-compatible endpoint:</span></span>
   
    ```
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d3278-165">You can check for the latest version of **azure-eventhubs** using [Maven search][lnk-maven-eventhubs-search].</span><span class="sxs-lookup"><span data-stu-id="d3278-165">You can check for the latest version of **azure-eventhubs** using [Maven search][lnk-maven-eventhubs-search].</span></span>

4. <span data-ttu-id="d3278-166">Save and close the pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="d3278-166">Save and close the pom.xml file.</span></span>
5. <span data-ttu-id="d3278-167">Using a text editor, open the read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span><span class="sxs-lookup"><span data-stu-id="d3278-167">Using a text editor, open the read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>
6. <span data-ttu-id="d3278-168">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="d3278-168">Add the following **import** statements to the file:</span></span>
   
    ```
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```
7. <span data-ttu-id="d3278-169">Add the following class-level variable to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="d3278-169">Add the following class-level variable to the **App** class.</span></span> <span data-ttu-id="d3278-170">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with the values you noted previously:</span><span class="sxs-lookup"><span data-stu-id="d3278-170">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with the values you noted previously:</span></span>
   
    ```
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```
8. <span data-ttu-id="d3278-171">Add the following **receiveMessages** method to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="d3278-171">Add the following **receiveMessages** method to the **App** class.</span></span> <span data-ttu-id="d3278-172">This method creates an **EventHubClient** instance to connect to the Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance to read from an Event Hub partition.</span><span class="sxs-lookup"><span data-stu-id="d3278-172">This method creates an **EventHubClient** instance to connect to the Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance to read from an Event Hub partition.</span></span> <span data-ttu-id="d3278-173">It loops continuously and prints the message details until the app terminates.</span><span class="sxs-lookup"><span data-stu-id="d3278-173">It loops continuously and prints the message details until the app terminates.</span></span>
   
    ```
    private static EventHubClient receiveMessages(final String partitionId)
    {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      }
      catch(Exception e) {
        System.out.println("Failed to create client: " + e.getMessage());
        System.exit(1);
      }
      try {
        client.createReceiver( 
          EventHubClient.DEFAULT_CONSUMER_GROUP_NAME,  
          partitionId,  
          Instant.now()).thenAccept(new Consumer<PartitionReceiver>()
        {
          public void accept(PartitionReceiver receiver)
          {
            System.out.println("** Created receiver on partition " + partitionId);
            try {
              while (true) {
                Iterable<EventData> receivedEvents = receiver.receive(100).get();
                int batchSize = 0;
                if (receivedEvents != null)
                {
                  for(EventData receivedEvent: receivedEvents)
                  {
                    System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s", 
                      receivedEvent.getSystemProperties().getOffset(), 
                      receivedEvent.getSystemProperties().getSequenceNumber(), 
                      receivedEvent.getSystemProperties().getEnqueuedTime()));
                    System.out.println(String.format("| Device ID: %s", receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                    System.out.println(String.format("| Message Payload: %s", new String(receivedEvent.getBody(),
                      Charset.defaultCharset())));
                    batchSize++;
                  }
                }
                System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId,batchSize));
              }
            }
            catch (Exception e)
            {
              System.out.println("Failed to receive messages: " + e.getMessage());
            }
          }
        });
      }
      catch (Exception e)
      {
        System.out.println("Failed to create receiver: " + e.getMessage());
      }
      return client;
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d3278-174">This method uses a filter when it creates the receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span><span class="sxs-lookup"><span data-stu-id="d3278-174">This method uses a filter when it creates the receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="d3278-175">This technique is useful in a test environment so you can see the current set of messages.</span><span class="sxs-lookup"><span data-stu-id="d3278-175">This technique is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="d3278-176">In a production environment, your code should make sure that it processes all the messages - for more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="d3278-176">In a production environment, your code should make sure that it processes all the messages - for more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
   > 
   > 
9. <span data-ttu-id="d3278-177">Modify the signature of the **main** method to include the exception as follows:</span><span class="sxs-lookup"><span data-stu-id="d3278-177">Modify the signature of the **main** method to include the exception as follows:</span></span>
   
    ```
    public static void main( String[] args ) throws IOException
    ```
10. <span data-ttu-id="d3278-178">Add the following code to the **main** method in the **App** class.</span><span class="sxs-lookup"><span data-stu-id="d3278-178">Add the following code to the **main** method in the **App** class.</span></span> <span data-ttu-id="d3278-179">This code creates the two **EventHubClient** and **PartitionReceiver** instances and enables you to close the app when you have finished processing messages:</span><span class="sxs-lookup"><span data-stu-id="d3278-179">This code creates the two **EventHubClient** and **PartitionReceiver** instances and enables you to close the app when you have finished processing messages:</span></span>
    
    ```
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER to exit.");
    System.in.read();
    try
    {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    }
    catch (ServiceBusException sbe)
    {
      System.exit(1);
    }
    ```
    
    > [!NOTE]
    > <span data-ttu-id="d3278-180">This code assumes you created your IoT hub in the F1 (free) tier.</span><span class="sxs-lookup"><span data-stu-id="d3278-180">This code assumes you created your IoT hub in the F1 (free) tier.</span></span> <span data-ttu-id="d3278-181">A free IoT hub has two partitions named "0" and "1".</span><span class="sxs-lookup"><span data-stu-id="d3278-181">A free IoT hub has two partitions named "0" and "1".</span></span>
    > 
    > 
11. <span data-ttu-id="d3278-182">Save and close the App.java file.</span><span class="sxs-lookup"><span data-stu-id="d3278-182">Save and close the App.java file.</span></span>
12. <span data-ttu-id="d3278-183">To build the **read-d2c-messages** app using Maven, execute the following command at the command prompt in the read-d2c-messages folder:</span><span class="sxs-lookup"><span data-stu-id="d3278-183">To build the **read-d2c-messages** app using Maven, execute the following command at the command prompt in the read-d2c-messages folder:</span></span>
    
    ```
    mvn clean package -DskipTests
    ```

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d3278-184">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="d3278-184">Create a simulated device app</span></span>
<span data-ttu-id="d3278-185">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3278-185">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="d3278-186">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **simulated-device** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="d3278-186">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="d3278-187">Note this is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="d3278-187">Note this is a single, long command:</span></span>
   
    ```
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```
2. <span data-ttu-id="d3278-188">At your command prompt, navigate to the simulated-device folder.</span><span class="sxs-lookup"><span data-stu-id="d3278-188">At your command prompt, navigate to the simulated-device folder.</span></span>
3. <span data-ttu-id="d3278-189">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="d3278-189">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="d3278-190">This dependency enables you to use the iothub-java-client package in your app to communicate with your IoT hub and to serialize Java objects to JSON:</span><span class="sxs-lookup"><span data-stu-id="d3278-190">This dependency enables you to use the iothub-java-client package in your app to communicate with your IoT hub and to serialize Java objects to JSON:</span></span>
   
    ```
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.1.24</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d3278-191">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="d3278-191">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="d3278-192">Save and close the pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="d3278-192">Save and close the pom.xml file.</span></span>
5. <span data-ttu-id="d3278-193">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span><span class="sxs-lookup"><span data-stu-id="d3278-193">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>
6. <span data-ttu-id="d3278-194">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="d3278-194">Add the following **import** statements to the file:</span></span>
   
    ```
    import com.microsoft.azure.sdk.iot.device.DeviceClient;
    import com.microsoft.azure.sdk.iot.device.IotHubClientProtocol;
    import com.microsoft.azure.sdk.iot.device.Message;
    import com.microsoft.azure.sdk.iot.device.IotHubStatusCode;
    import com.microsoft.azure.sdk.iot.device.IotHubEventCallback;
    import com.microsoft.azure.sdk.iot.device.MessageCallback;
    import com.microsoft.azure.sdk.iot.device.IotHubMessageResult;
    import com.google.gson.Gson;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```
7. <span data-ttu-id="d3278-195">Add the following class-level variables to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="d3278-195">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="d3278-196">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span><span class="sxs-lookup"><span data-stu-id="d3278-196">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>
   
    ```
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="d3278-197">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span><span class="sxs-lookup"><span data-stu-id="d3278-197">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="d3278-198">You can use either the MQTT, AMQP, or HTTP protocol to communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d3278-198">You can use either the MQTT, AMQP, or HTTP protocol to communicate with IoT Hub.</span></span>
8. <span data-ttu-id="d3278-199">Add the following nested **TelemetryDataPoint** class inside the **App** class to specify the telemetry data your device sends to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="d3278-199">Add the following nested **TelemetryDataPoint** class inside the **App** class to specify the telemetry data your device sends to your IoT hub:</span></span>
   
    ```
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. <span data-ttu-id="d3278-200">Add the following nested **EventCallback** class inside the **App** class to display the acknowledgement status that the IoT hub returns when it processes a message from the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="d3278-200">Add the following nested **EventCallback** class inside the **App** class to display the acknowledgement status that the IoT hub returns when it processes a message from the simulated device app.</span></span> <span data-ttu-id="d3278-201">This method also notifies the main thread in the app when the message has been processed:</span><span class="sxs-lookup"><span data-stu-id="d3278-201">This method also notifies the main thread in the app when the message has been processed:</span></span>
   
    ```
    private static class EventCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to message with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```
10. <span data-ttu-id="d3278-202">Add the following nested **MessageSender** class inside the **App** class.</span><span class="sxs-lookup"><span data-stu-id="d3278-202">Add the following nested **MessageSender** class inside the **App** class.</span></span> <span data-ttu-id="d3278-203">The **run** method in this class generates sample telemetry data to send to your IoT hub and waits for an acknowledgement before sending the next message:</span><span class="sxs-lookup"><span data-stu-id="d3278-203">The **run** method in this class generates sample telemetry data to send to your IoT hub and waits for an acknowledgement before sending the next message:</span></span>
    
    ```
    private static class MessageSender implements Runnable {
    
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
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
    
    <span data-ttu-id="d3278-204">This method sends a new device-to-cloud message one second after the IoT hub acknowledges the previous message.</span><span class="sxs-lookup"><span data-stu-id="d3278-204">This method sends a new device-to-cloud message one second after the IoT hub acknowledges the previous message.</span></span> <span data-ttu-id="d3278-205">The message contains a JSON-serialized object with the deviceId and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span><span class="sxs-lookup"><span data-stu-id="d3278-205">The message contains a JSON-serialized object with the deviceId and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>
11. <span data-ttu-id="d3278-206">Replace the **main** method with the following code that creates a thread to send device-to-cloud messages to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="d3278-206">Replace the **main** method with the following code that creates a thread to send device-to-cloud messages to your IoT hub:</span></span>
    
    ```
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER to exit.");
      System.in.read();
      executor.shutdownNow();
      client.close();
    }
    ```
12. <span data-ttu-id="d3278-207">Save and close the App.java file.</span><span class="sxs-lookup"><span data-stu-id="d3278-207">Save and close the App.java file.</span></span>
13. <span data-ttu-id="d3278-208">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span><span class="sxs-lookup"><span data-stu-id="d3278-208">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>
    
    ```
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="d3278-209">To keep things simple, this tutorial does not implement any retry policy.</span><span class="sxs-lookup"><span data-stu-id="d3278-209">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d3278-210">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="d3278-210">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="d3278-211">Run the apps</span><span class="sxs-lookup"><span data-stu-id="d3278-211">Run the apps</span></span>
<span data-ttu-id="d3278-212">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="d3278-212">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="d3278-213">At a command prompt in the read-d2c folder, run the following command to begin monitoring the first partition in your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="d3278-213">At a command prompt in the read-d2c folder, run the following command to begin monitoring the first partition in your IoT hub:</span></span>
   
    ```
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```
   
    ![Java IoT Hub service app to monitor device-to-cloud messages][7]
2. <span data-ttu-id="d3278-215">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry data to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="d3278-215">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>
   
    ```
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```
   
    ![Java IoT Hub device app to send device-to-cloud messages][8]
3. <span data-ttu-id="d3278-217">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span><span class="sxs-lookup"><span data-stu-id="d3278-217">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>
   
    ![Azure portal Usage tile showing number of messages sent to IoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="d3278-219">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3278-219">Next steps</span></span>
<span data-ttu-id="d3278-220">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="d3278-220">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="d3278-221">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3278-221">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="d3278-222">You also created an app that displays the messages received by the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3278-222">You also created an app that displays the messages received by the IoT hub.</span></span> 

<span data-ttu-id="d3278-223">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span><span class="sxs-lookup"><span data-stu-id="d3278-223">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="d3278-224">[Connecting your device][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="d3278-224">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="d3278-225">[Getting started with device management][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="d3278-225">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="d3278-226">[Getting started with the IoT Gateway SDK][lnk-gateway-SDK]</span><span class="sxs-lookup"><span data-stu-id="d3278-226">[Getting started with the IoT Gateway SDK][lnk-gateway-SDK]</span></span>

<span data-ttu-id="d3278-227">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="d3278-227">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

<!-- Images. -->
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-getstarted/runapp1.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-getstarted/runapp2.png
[43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22




