---
title: Get started with Azure IoT Hub device management (Java) | Microsoft Docs
description: How to use Azure IoT Hub device management to initiate a remote device reboot. You use the Azure IoT device SDK for Java to implement a simulated device app that includes a direct method and the Azure IoT service SDK for Java to implement a service app that invokes the direct method.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: java
ms.topic: conceptual
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6a4ba8c2b88520dff028610cf64aa9b3a6e3fefd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857159"
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="a810b-104">Get started with device management (Java)</span><span class="sxs-lookup"><span data-stu-id="a810b-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="a810b-105">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="a810b-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a810b-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a810b-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="a810b-107">Create a simulated device app that implements a direct method to reboot the device.</span><span class="sxs-lookup"><span data-stu-id="a810b-107">Create a simulated device app that implements a direct method to reboot the device.</span></span> <span data-ttu-id="a810b-108">Direct methods are invoked from the cloud.</span><span class="sxs-lookup"><span data-stu-id="a810b-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="a810b-109">Create an app that invokes the reboot direct method in the simulated device app through your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a810b-109">Create an app that invokes the reboot direct method in the simulated device app through your IoT hub.</span></span> <span data-ttu-id="a810b-110">This app then monitors the reported properties from the device to see when the reboot operation is complete.</span><span class="sxs-lookup"><span data-stu-id="a810b-110">This app then monitors the reported properties from the device to see when the reboot operation is complete.</span></span>

<span data-ttu-id="a810b-111">At the end of this tutorial, you have two Java console apps:</span><span class="sxs-lookup"><span data-stu-id="a810b-111">At the end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="a810b-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="a810b-112">**simulated-device**.</span></span> <span data-ttu-id="a810b-113">This app:</span><span class="sxs-lookup"><span data-stu-id="a810b-113">This app:</span></span>

* <span data-ttu-id="a810b-114">Connects to your IoT hub with the device identity created earlier.</span><span class="sxs-lookup"><span data-stu-id="a810b-114">Connects to your IoT hub with the device identity created earlier.</span></span>
* <span data-ttu-id="a810b-115">Receives a reboot direct method call.</span><span class="sxs-lookup"><span data-stu-id="a810b-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="a810b-116">Simulates a physical reboot.</span><span class="sxs-lookup"><span data-stu-id="a810b-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="a810b-117">Reports the time of the last reboot through a reported property.</span><span class="sxs-lookup"><span data-stu-id="a810b-117">Reports the time of the last reboot through a reported property.</span></span>

<span data-ttu-id="a810b-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="a810b-118">**trigger-reboot**.</span></span> <span data-ttu-id="a810b-119">This app:</span><span class="sxs-lookup"><span data-stu-id="a810b-119">This app:</span></span>

* <span data-ttu-id="a810b-120">Calls a direct method in the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="a810b-120">Calls a direct method in the simulated device app.</span></span>
* <span data-ttu-id="a810b-121">Displays the response to the direct method call sent by the simulated device</span><span class="sxs-lookup"><span data-stu-id="a810b-121">Displays the response to the direct method call sent by the simulated device</span></span>
* <span data-ttu-id="a810b-122">Displays the updated reported properties.</span><span class="sxs-lookup"><span data-stu-id="a810b-122">Displays the updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="a810b-123">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="a810b-123">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="a810b-124">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="a810b-124">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="a810b-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="a810b-125">Java SE 8.</span></span> <br/> <span data-ttu-id="a810b-126">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="a810b-126">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a810b-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="a810b-127">Maven 3.</span></span>  <br/> <span data-ttu-id="a810b-128">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="a810b-128">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a810b-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a810b-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="a810b-130">Trigger a remote reboot on the device using a direct method</span><span class="sxs-lookup"><span data-stu-id="a810b-130">Trigger a remote reboot on the device using a direct method</span></span>

<span data-ttu-id="a810b-131">In this section, you create a Java console app that:</span><span class="sxs-lookup"><span data-stu-id="a810b-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="a810b-132">Invokes the reboot direct method in the simulated device app.</span><span class="sxs-lookup"><span data-stu-id="a810b-132">Invokes the reboot direct method in the simulated device app.</span></span>
1. <span data-ttu-id="a810b-133">Displays the response.</span><span class="sxs-lookup"><span data-stu-id="a810b-133">Displays the response.</span></span>
1. <span data-ttu-id="a810b-134">Polls the reported properties sent from the device to determine when the reboot is complete.</span><span class="sxs-lookup"><span data-stu-id="a810b-134">Polls the reported properties sent from the device to determine when the reboot is complete.</span></span>

<span data-ttu-id="a810b-135">This console app connects to your IoT Hub to invoke the direct method and read the reported properties.</span><span class="sxs-lookup"><span data-stu-id="a810b-135">This console app connects to your IoT Hub to invoke the direct method and read the reported properties.</span></span>

1. <span data-ttu-id="a810b-136">Create an empty folder called dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="a810b-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="a810b-137">In the dm-get-started folder, create a Maven project called **trigger-reboot** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="a810b-137">In the dm-get-started folder, create a Maven project called **trigger-reboot** using the following command at your command prompt.</span></span> <span data-ttu-id="a810b-138">The following shows a single, long command:</span><span class="sxs-lookup"><span data-stu-id="a810b-138">The following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a810b-139">At your command prompt, navigate to the trigger-reboot folder.</span><span class="sxs-lookup"><span data-stu-id="a810b-139">At your command prompt, navigate to the trigger-reboot folder.</span></span>

1. <span data-ttu-id="a810b-140">Using a text editor, open the pom.xml file in the trigger-reboot folder and add the following dependency to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="a810b-140">Using a text editor, open the pom.xml file in the trigger-reboot folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="a810b-141">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a810b-141">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a810b-142">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="a810b-142">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="a810b-143">Add the following **build** node after the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="a810b-143">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="a810b-144">This configuration instructs Maven to use Java 1.8 to build the app:</span><span class="sxs-lookup"><span data-stu-id="a810b-144">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="a810b-145">Save and close the pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="a810b-145">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="a810b-146">Using a text editor, open the trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span><span class="sxs-lookup"><span data-stu-id="a810b-146">Using a text editor, open the trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="a810b-147">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="a810b-147">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. <span data-ttu-id="a810b-148">Add the following class-level variables to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="a810b-148">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="a810b-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span><span class="sxs-lookup"><span data-stu-id="a810b-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="a810b-150">To implement a thread that reads the reported properties from the device twin every 10 seconds, add the following nested class to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="a810b-150">To implement a thread that reads the reported properties from the device twin every 10 seconds, add the following nested class to the **App** class:</span></span>

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="a810b-151">Modify the signature of the **main** method to throw the following exception:</span><span class="sxs-lookup"><span data-stu-id="a810b-151">Modify the signature of the **main** method to throw the following exception:</span></span>

    ```java
    public static void main(String[] args) throws IOException
    ```

1. <span data-ttu-id="a810b-152">To invoke the reboot direct method on the simulated device, add the following code to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="a810b-152">To invoke the reboot direct method on the simulated device, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="a810b-153">To start the thread to poll the reported properties from the simulated device, add the following code to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="a810b-153">To start the thread to poll the reported properties from the simulated device, add the following code to the **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="a810b-154">To enable you to stop the app, add the following code to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="a810b-154">To enable you to stop the app, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press ENTER to exit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="a810b-155">Save and close the trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span><span class="sxs-lookup"><span data-stu-id="a810b-155">Save and close the trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="a810b-156">Build the **trigger-reboot** back-end app and correct any errors.</span><span class="sxs-lookup"><span data-stu-id="a810b-156">Build the **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="a810b-157">At your command prompt, navigate to the trigger-reboot folder and run the following command:</span><span class="sxs-lookup"><span data-stu-id="a810b-157">At your command prompt, navigate to the trigger-reboot folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a810b-158">Create a simulated device app</span><span class="sxs-lookup"><span data-stu-id="a810b-158">Create a simulated device app</span></span>

<span data-ttu-id="a810b-159">In this section, you create a Java console app that simulates a device.</span><span class="sxs-lookup"><span data-stu-id="a810b-159">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="a810b-160">The app listens for the reboot direct method call from your IoT hub and immediately responds to that call.</span><span class="sxs-lookup"><span data-stu-id="a810b-160">The app listens for the reboot direct method call from your IoT hub and immediately responds to that call.</span></span> <span data-ttu-id="a810b-161">The app then sleeps for a while to simulate the reboot process before it uses a reported property to notify the **trigger-reboot** back-end app that the reboot is complete.</span><span class="sxs-lookup"><span data-stu-id="a810b-161">The app then sleeps for a while to simulate the reboot process before it uses a reported property to notify the **trigger-reboot** back-end app that the reboot is complete.</span></span>

1. <span data-ttu-id="a810b-162">In the dm-get-started folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="a810b-162">In the dm-get-started folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="a810b-163">The following is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="a810b-163">The following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a810b-164">At your command prompt, navigate to the simulated-device folder.</span><span class="sxs-lookup"><span data-stu-id="a810b-164">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="a810b-165">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependency to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="a810b-165">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="a810b-166">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a810b-166">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a810b-167">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="a810b-167">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="a810b-168">Add the following **build** node after the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="a810b-168">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="a810b-169">This configuration instructs Maven to use Java 1.8 to build the app:</span><span class="sxs-lookup"><span data-stu-id="a810b-169">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="a810b-170">Save and close the pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="a810b-170">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="a810b-171">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java source file.</span><span class="sxs-lookup"><span data-stu-id="a810b-171">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="a810b-172">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="a810b-172">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. <span data-ttu-id="a810b-173">Add the following class-level variables to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="a810b-173">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="a810b-174">Replace `{yourdeviceconnectionstring}` with the device connection string you noted in the *Create a device identity* section:</span><span class="sxs-lookup"><span data-stu-id="a810b-174">Replace `{yourdeviceconnectionstring}` with the device connection string you noted in the *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="a810b-175">To implement a callback handler for direct method status events, add the following nested class to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="a810b-175">To implement a callback handler for direct method status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="a810b-176">To implement a callback handler for device twin status events, add the following nested class to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="a810b-176">To implement a callback handler for device twin status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded to device twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="a810b-177">To implement a callback handler for property events, add the following nested class to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="a810b-177">To implement a callback handler for property events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. <span data-ttu-id="a810b-178">To implement a thread to simulate the device reboot, add the following nested class to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="a810b-178">To implement a thread to simulate the device reboot, add the following nested class to the **App** class.</span></span> <span data-ttu-id="a810b-179">The thread sleeps for five seconds and then sets the **lastReboot** reported property:</span><span class="sxs-lookup"><span data-stu-id="a810b-179">The thread sleeps for five seconds and then sets the **lastReboot** reported property:</span></span>

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="a810b-180">To implement the direct method on the device, add the following nested class to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="a810b-180">To implement the direct method on the device, add the following nested class to the **App** class.</span></span> <span data-ttu-id="a810b-181">When the simulated app receives a call to the **reboot** direct method, it returns an acknowledgement to the caller and then starts a thread to process the reboot:</span><span class="sxs-lookup"><span data-stu-id="a810b-181">When the simulated app receives a call to the **reboot** direct method, it returns an acknowledgement to the caller and then starts a thread to process the reboot:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="a810b-182">Modify the signature of the **main** method to throw the following exceptions:</span><span class="sxs-lookup"><span data-stu-id="a810b-182">Modify the signature of the **main** method to throw the following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="a810b-183">To instantiate a **DeviceClient**, add the following code to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="a810b-183">To instantiate a **DeviceClient**, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="a810b-184">To start listening for direct method calls, add the following code to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="a810b-184">To start listening for direct method calls, add the following code to the **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed to direct methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="a810b-185">To shut down the device simulator, add the following code to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="a810b-185">To shut down the device simulator, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="a810b-186">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span><span class="sxs-lookup"><span data-stu-id="a810b-186">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="a810b-187">Build the **simulated-device** back-end app and correct any errors.</span><span class="sxs-lookup"><span data-stu-id="a810b-187">Build the **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="a810b-188">At your command prompt, navigate to the simulated-device folder and run the following command:</span><span class="sxs-lookup"><span data-stu-id="a810b-188">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="a810b-189">Run the apps</span><span class="sxs-lookup"><span data-stu-id="a810b-189">Run the apps</span></span>

<span data-ttu-id="a810b-190">You are now ready to run the apps.</span><span class="sxs-lookup"><span data-stu-id="a810b-190">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="a810b-191">At a command prompt in the simulated-device folder, run the following command to begin listening for reboot method calls from your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a810b-191">At a command prompt in the simulated-device folder, run the following command to begin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub simulated device app to listen for reboot direct method calls][1]

1. <span data-ttu-id="a810b-193">At a command prompt in the trigger-reboot folder, run the following command to call the reboot method on your simulated device from your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a810b-193">At a command prompt in the trigger-reboot folder, run the following command to call the reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service app to call the reboot direct method][2]

1. <span data-ttu-id="a810b-195">The simulated device responds to the reboot direct method call:</span><span class="sxs-lookup"><span data-stu-id="a810b-195">The simulated device responds to the reboot direct method call:</span></span>

    ![Java IoT Hub simulated device app responds to the direct method call][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22