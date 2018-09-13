---
title: Get started with Azure IoT Hub device twins (Java) | Microsoft Docs
description: How to use Azure IoT Hub device twins to add tags and then use an IoT Hub query. You use the Azure IoT device SDK for Java to implement the device app and the Azure IoT service SDK for Java to implement a service app that adds the tags and runs the IoT Hub query.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: java
ms.topic: conceptual
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: b8884cafbf250b9d7a88219b5647addafee9904a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868423"
---
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="61b8d-104">Get started with device twins (Java)</span><span class="sxs-lookup"><span data-stu-id="61b8d-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="61b8d-105">In this tutorial, you create two Java console apps:</span><span class="sxs-lookup"><span data-stu-id="61b8d-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="61b8d-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span><span class="sxs-lookup"><span data-stu-id="61b8d-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="61b8d-107">**simulated-device**, a Java device app that connects to your IoT hub and reports its connectivity condition using a reported property.</span><span class="sxs-lookup"><span data-stu-id="61b8d-107">**simulated-device**, a Java device app that connects to your IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="61b8d-108">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span><span class="sxs-lookup"><span data-stu-id="61b8d-108">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

<span data-ttu-id="61b8d-109">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="61b8d-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="61b8d-110">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="61b8d-110">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="61b8d-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="61b8d-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="61b8d-112">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="61b8d-112">An active Azure account.</span></span> <span data-ttu-id="61b8d-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="61b8d-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="61b8d-114">Create the service app</span><span class="sxs-lookup"><span data-stu-id="61b8d-114">Create the service app</span></span>

<span data-ttu-id="61b8d-115">In this section, you create a Java app that adds location metadata as a tag to the device twin in IoT Hub associated with **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="61b8d-115">In this section, you create a Java app that adds location metadata as a tag to the device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="61b8d-116">The app first queries IoT hub for devices located in the US, and then for devices that report a cellular network connection.</span><span class="sxs-lookup"><span data-stu-id="61b8d-116">The app first queries IoT hub for devices located in the US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="61b8d-117">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="61b8d-117">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="61b8d-118">In the `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="61b8d-118">In the `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using the following command at your command prompt.</span></span> <span data-ttu-id="61b8d-119">Note this is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="61b8d-119">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="61b8d-120">At your command prompt, navigate to the `add-tags-query` folder.</span><span class="sxs-lookup"><span data-stu-id="61b8d-120">At your command prompt, navigate to the `add-tags-query` folder.</span></span>

1. <span data-ttu-id="61b8d-121">Using a text editor, open the `pom.xml` file in the `add-tags-query` folder and add the following dependency to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="61b8d-121">Using a text editor, open the `pom.xml` file in the `add-tags-query` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="61b8d-122">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="61b8d-122">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="61b8d-123">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="61b8d-123">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="61b8d-124">Add the following **build** node after the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="61b8d-124">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="61b8d-125">This configuration instructs Maven to use Java 1.8 to build the app:</span><span class="sxs-lookup"><span data-stu-id="61b8d-125">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="61b8d-126">Save and close the `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="61b8d-126">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="61b8d-127">Using a text editor, open the `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="61b8d-127">Using a text editor, open the `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="61b8d-128">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="61b8d-128">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="61b8d-129">Add the following class-level variables to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="61b8d-129">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="61b8d-130">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span><span class="sxs-lookup"><span data-stu-id="61b8d-130">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="61b8d-131">Update the **main** method signature to include the following `throws` clause:</span><span class="sxs-lookup"><span data-stu-id="61b8d-131">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="61b8d-132">Add the following code to the **main** method to create the **DeviceTwin** and **DeviceTwinDevice** objects.</span><span class="sxs-lookup"><span data-stu-id="61b8d-132">Add the following code to the **main** method to create the **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="61b8d-133">The **DeviceTwin** object handles the communication with your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="61b8d-133">The **DeviceTwin** object handles the communication with your IoT hub.</span></span> <span data-ttu-id="61b8d-134">The **DeviceTwinDevice** object represents the device twin with its properties and tags:</span><span class="sxs-lookup"><span data-stu-id="61b8d-134">The **DeviceTwinDevice** object represents the device twin with its properties and tags:</span></span>

    ```java
    // Get the DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="61b8d-135">Add the following `try/catch` block to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="61b8d-135">Add the following `try/catch` block to the **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="61b8d-136">To update the **region** and **plant** device twin tags in your device twin, add the following code in the `try` block:</span><span class="sxs-lookup"><span data-stu-id="61b8d-136">To update the **region** and **plant** device twin tags in your device twin, add the following code in the `try` block:</span></span>

    ```java
    // Get the device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from the existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create the tags and attach them to the DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update the device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve the device twin with the tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. <span data-ttu-id="61b8d-137">To query the device twins in IoT hub, add the following code to the `try` block after the code you added in the previous step.</span><span class="sxs-lookup"><span data-stu-id="61b8d-137">To query the device twins in IoT hub, add the following code to the `try` block after the code you added in the previous step.</span></span> <span data-ttu-id="61b8d-138">The code runs two queries.</span><span class="sxs-lookup"><span data-stu-id="61b8d-138">The code runs two queries.</span></span> <span data-ttu-id="61b8d-139">Each query returns a maximum of 100 devices:</span><span class="sxs-lookup"><span data-stu-id="61b8d-139">Each query returns a maximum of 100 devices:</span></span>

    ```java
    // Query the device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct the query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run the query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct the query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run the query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. <span data-ttu-id="61b8d-140">Save and close the `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span><span class="sxs-lookup"><span data-stu-id="61b8d-140">Save and close the `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="61b8d-141">Build the **add-tags-query** app and correct any errors.</span><span class="sxs-lookup"><span data-stu-id="61b8d-141">Build the **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="61b8d-142">At your command prompt, navigate to the `add-tags-query` folder and run the following command:</span><span class="sxs-lookup"><span data-stu-id="61b8d-142">At your command prompt, navigate to the `add-tags-query` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="61b8d-143">Create a device app</span><span class="sxs-lookup"><span data-stu-id="61b8d-143">Create a device app</span></span>

<span data-ttu-id="61b8d-144">In this section, you create a Java console app that sets a reported property value that is sent to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61b8d-144">In this section, you create a Java console app that sets a reported property value that is sent to IoT Hub.</span></span>

1. <span data-ttu-id="61b8d-145">In the `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="61b8d-145">In the `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="61b8d-146">Note this is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="61b8d-146">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="61b8d-147">At your command prompt, navigate to the `simulated-device` folder.</span><span class="sxs-lookup"><span data-stu-id="61b8d-147">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="61b8d-148">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="61b8d-148">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="61b8d-149">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="61b8d-149">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="61b8d-150">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="61b8d-150">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="61b8d-151">Add the following **build** node after the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="61b8d-151">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="61b8d-152">This configuration instructs Maven to use Java 1.8 to build the app:</span><span class="sxs-lookup"><span data-stu-id="61b8d-152">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="61b8d-153">Save and close the `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="61b8d-153">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="61b8d-154">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="61b8d-154">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="61b8d-155">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="61b8d-155">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="61b8d-156">Add the following class-level variables to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="61b8d-156">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="61b8d-157">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span><span class="sxs-lookup"><span data-stu-id="61b8d-157">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="61b8d-158">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span><span class="sxs-lookup"><span data-stu-id="61b8d-158">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> 

1. <span data-ttu-id="61b8d-159">Add the following code to the **main** method to:</span><span class="sxs-lookup"><span data-stu-id="61b8d-159">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="61b8d-160">Create a device client to communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61b8d-160">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="61b8d-161">Create a **Device** object to store the device twin properties.</span><span class="sxs-lookup"><span data-stu-id="61b8d-161">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object to store the device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed to " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="61b8d-162">Add the following code to the **main** method to create a **connectivityType** reported property and send it to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="61b8d-162">Add the following code to the **main** method to create a **connectivityType** reported property and send it to IoT Hub:</span></span>

    ```java
    try {
      // Open the DeviceClient and start the device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it to your IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="61b8d-163">Add the following code to the end of the **main** method.</span><span class="sxs-lookup"><span data-stu-id="61b8d-163">Add the following code to the end of the **main** method.</span></span> <span data-ttu-id="61b8d-164">Waiting for the **Enter** key allows time for IoT Hub to report the status of the device twin operations:</span><span class="sxs-lookup"><span data-stu-id="61b8d-164">Waiting for the **Enter** key allows time for IoT Hub to report the status of the device twin operations:</span></span>

    ```java
    System.out.println("Press any key to exit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="61b8d-165">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="61b8d-165">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="61b8d-166">Build the **simulated-device** app and correct any errors.</span><span class="sxs-lookup"><span data-stu-id="61b8d-166">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="61b8d-167">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span><span class="sxs-lookup"><span data-stu-id="61b8d-167">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="61b8d-168">Run the apps</span><span class="sxs-lookup"><span data-stu-id="61b8d-168">Run the apps</span></span>

<span data-ttu-id="61b8d-169">You are now ready to run the console apps.</span><span class="sxs-lookup"><span data-stu-id="61b8d-169">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="61b8d-170">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app:</span><span class="sxs-lookup"><span data-stu-id="61b8d-170">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service app to update tag values and run device queries](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="61b8d-172">You can see the **plant** and **region** tags added to the device twin.</span><span class="sxs-lookup"><span data-stu-id="61b8d-172">You can see the **plant** and **region** tags added to the device twin.</span></span> <span data-ttu-id="61b8d-173">The first query returns your device, but the second does not.</span><span class="sxs-lookup"><span data-stu-id="61b8d-173">The first query returns your device, but the second does not.</span></span>

1. <span data-ttu-id="61b8d-174">At a command prompt in the `simulated-device` folder, run the following command to add the **connectivityType** reported property to the device twin:</span><span class="sxs-lookup"><span data-stu-id="61b8d-174">At a command prompt in the `simulated-device` folder, run the following command to add the **connectivityType** reported property to the device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![The device client adds the **connectivityType** reported property](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="61b8d-176">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app a second time:</span><span class="sxs-lookup"><span data-stu-id="61b8d-176">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service app to update tag values and run device queries](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="61b8d-178">Now your device has sent the **connectivityType** property to IoT Hub, the second query returns your device.</span><span class="sxs-lookup"><span data-stu-id="61b8d-178">Now your device has sent the **connectivityType** property to IoT Hub, the second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61b8d-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="61b8d-179">Next steps</span></span>

<span data-ttu-id="61b8d-180">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="61b8d-180">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="61b8d-181">You added device metadata as tags from a back-end app, and wrote a device app to report device connectivity information in the device twin.</span><span class="sxs-lookup"><span data-stu-id="61b8d-181">You added device metadata as tags from a back-end app, and wrote a device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="61b8d-182">You also learned how to query the device twin information using the SQL-like IoT Hub query language.</span><span class="sxs-lookup"><span data-stu-id="61b8d-182">You also learned how to query the device twin information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="61b8d-183">Use the following resources to learn how to:</span><span class="sxs-lookup"><span data-stu-id="61b8d-183">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="61b8d-184">Send telemetry from devices with the [Get started with IoT Hub](quickstart-send-telemetry-java.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="61b8d-184">Send telemetry from devices with the [Get started with IoT Hub](quickstart-send-telemetry-java.md) tutorial.</span></span>
* <span data-ttu-id="61b8d-185">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](quickstart-control-device-java.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="61b8d-185">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](quickstart-control-device-java.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
