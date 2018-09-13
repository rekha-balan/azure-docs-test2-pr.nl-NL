---
title: Upload files from devices to Azure IoT Hub with Java | Microsoft Docs
description: How to upload files from a device to the cloud using Azure IoT device SDK for Java. Uploaded files are stored in an Azure storage blob container.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: java
ms.topic: conceptual
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 7eb18a623683fb8a3662297825e90234644ead39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867327"
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub"></a><span data-ttu-id="c272f-104">Upload files from your device to the cloud with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c272f-104">Upload files from your device to the cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="c272f-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial to show you how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.yml).</span><span class="sxs-lookup"><span data-stu-id="c272f-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial to show you how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.yml).</span></span> <span data-ttu-id="c272f-106">The tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="c272f-106">The tutorial shows you how to:</span></span>

- <span data-ttu-id="c272f-107">Securely provide a device with an Azure blob URI for uploading a file.</span><span class="sxs-lookup"><span data-stu-id="c272f-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="c272f-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span><span class="sxs-lookup"><span data-stu-id="c272f-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="c272f-109">The [Get started with IoT Hub](quickstart-send-telemetry-java.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c272f-109">The [Get started with IoT Hub](quickstart-send-telemetry-java.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="c272f-110">The [Process Device-to-Cloud messages](tutorial-routing.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="c272f-110">The [Process Device-to-Cloud messages](tutorial-routing.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="c272f-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span><span class="sxs-lookup"><span data-stu-id="c272f-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="c272f-112">For example:</span><span class="sxs-lookup"><span data-stu-id="c272f-112">For example:</span></span>

* <span data-ttu-id="c272f-113">Large files that contain images</span><span class="sxs-lookup"><span data-stu-id="c272f-113">Large files that contain images</span></span>
* <span data-ttu-id="c272f-114">Videos</span><span class="sxs-lookup"><span data-stu-id="c272f-114">Videos</span></span>
* <span data-ttu-id="c272f-115">Vibration data sampled at high frequency</span><span class="sxs-lookup"><span data-stu-id="c272f-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="c272f-116">Some form of preprocessed data.</span><span class="sxs-lookup"><span data-stu-id="c272f-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="c272f-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/introduction.md) or the [Hadoop](../hdinsight/index.yml) stack.</span><span class="sxs-lookup"><span data-stu-id="c272f-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/introduction.md) or the [Hadoop](../hdinsight/index.yml) stack.</span></span> <span data-ttu-id="c272f-118">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c272f-118">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="c272f-119">At the end of this tutorial you run two Java console apps:</span><span class="sxs-lookup"><span data-stu-id="c272f-119">At the end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="c272f-120">**simulated-device**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c272f-120">**simulated-device**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="c272f-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c272f-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="c272f-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c272f-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="c272f-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="c272f-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="c272f-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c272f-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="c272f-125">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="c272f-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="c272f-126">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="c272f-126">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="c272f-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="c272f-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="c272f-128">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="c272f-128">An active Azure account.</span></span> <span data-ttu-id="c272f-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="c272f-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="c272f-130">Upload a file from a device app</span><span class="sxs-lookup"><span data-stu-id="c272f-130">Upload a file from a device app</span></span>

<span data-ttu-id="c272f-131">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) to upload a file to IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c272f-131">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) to upload a file to IoT hub.</span></span>

1. <span data-ttu-id="c272f-132">Copy an image file to the `simulated-device` folder and rename it `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="c272f-132">Copy an image file to the `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="c272f-133">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="c272f-133">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="c272f-134">Add the variable declaration to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="c272f-134">Add the variable declaration to the **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="c272f-135">To process file upload status callback messages, add the following nested class to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="c272f-135">To process file upload status callback messages, add the following nested class to the **App** class:</span></span>

    ```java
    // Define a callback method to print status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to file upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="c272f-136">To upload images to IoT Hub, add the following method to the **App** class to upload images to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="c272f-136">To upload images to IoT Hub, add the following method to the **App** class to upload images to IoT Hub:</span></span>

    ```java
    // Use IoT Hub to upload a file asynchronously to Azure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="c272f-137">Modify the **main** method to call the **uploadFile** method as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="c272f-137">Modify the **main** method to call the **uploadFile** method as shown in the following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get the filename and start the upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. <span data-ttu-id="c272f-138">Use the following command to build the **simulated-device** app and check for errors:</span><span class="sxs-lookup"><span data-stu-id="c272f-138">Use the following command to build the **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="c272f-139">Receive a file upload notification</span><span class="sxs-lookup"><span data-stu-id="c272f-139">Receive a file upload notification</span></span>

<span data-ttu-id="c272f-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c272f-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="c272f-141">You need the **iothubowner** connection string for your IoT Hub to complete this section.</span><span class="sxs-lookup"><span data-stu-id="c272f-141">You need the **iothubowner** connection string for your IoT Hub to complete this section.</span></span> <span data-ttu-id="c272f-142">You can find the connection string in the [Azure portal](https://portal.azure.com/) on the **Shared access policy** blade.</span><span class="sxs-lookup"><span data-stu-id="c272f-142">You can find the connection string in the [Azure portal](https://portal.azure.com/) on the **Shared access policy** blade.</span></span>

1. <span data-ttu-id="c272f-143">Create a Maven project called **read-file-upload-notification** using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="c272f-143">Create a Maven project called **read-file-upload-notification** using the following command at your command prompt.</span></span> <span data-ttu-id="c272f-144">Note this command is a single, long command:</span><span class="sxs-lookup"><span data-stu-id="c272f-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="c272f-145">At your command prompt, navigate to the new `read-file-upload-notification` folder.</span><span class="sxs-lookup"><span data-stu-id="c272f-145">At your command prompt, navigate to the new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="c272f-146">Using a text editor, open the `pom.xml` file in the `read-file-upload-notification` folder and add the following dependency to the **dependencies** node.</span><span class="sxs-lookup"><span data-stu-id="c272f-146">Using a text editor, open the `pom.xml` file in the `read-file-upload-notification` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="c272f-147">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span><span class="sxs-lookup"><span data-stu-id="c272f-147">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c272f-148">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="c272f-148">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="c272f-149">Save and close the `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="c272f-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="c272f-150">Using a text editor, open the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="c272f-150">Using a text editor, open the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="c272f-151">Add the following **import** statements to the file:</span><span class="sxs-lookup"><span data-stu-id="c272f-151">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="c272f-152">Add the following class-level variables to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="c272f-152">Add the following class-level variables to the **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="c272f-153">To print information about the file upload to the console, add the following nested class to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="c272f-153">To print information about the file upload to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Create a thread to receive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="c272f-154">To start the thread that listens for file upload notifications, add the following code to the **main** method:</span><span class="sxs-lookup"><span data-stu-id="c272f-154">To start the thread that listens for file upload notifications, add the following code to the **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from the ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start the thread to receive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER to exit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="c272f-155">Save and close the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="c272f-155">Save and close the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="c272f-156">Use the following command to build the **read-file-upload-notification** app and check for errors:</span><span class="sxs-lookup"><span data-stu-id="c272f-156">Use the following command to build the **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="c272f-157">Run the applications</span><span class="sxs-lookup"><span data-stu-id="c272f-157">Run the applications</span></span>

<span data-ttu-id="c272f-158">Now you are ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="c272f-158">Now you are ready to run the applications.</span></span>

<span data-ttu-id="c272f-159">At a command prompt in the `read-file-upload-notification` folder, run the following command:</span><span class="sxs-lookup"><span data-stu-id="c272f-159">At a command prompt in the `read-file-upload-notification` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="c272f-160">At a command prompt in the `simulated-device` folder, run the following command:</span><span class="sxs-lookup"><span data-stu-id="c272f-160">At a command prompt in the `simulated-device` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="c272f-161">The following screenshot shows the output from the **simulated-device** app:</span><span class="sxs-lookup"><span data-stu-id="c272f-161">The following screenshot shows the output from the **simulated-device** app:</span></span>

![Output from simulated-device app](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="c272f-163">The following screenshot shows the output from the **read-file-upload-notification** app:</span><span class="sxs-lookup"><span data-stu-id="c272f-163">The following screenshot shows the output from the **read-file-upload-notification** app:</span></span>

![Output from read-file-upload-notification app](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="c272f-165">You can use the portal to view the uploaded file in the storage container you configured:</span><span class="sxs-lookup"><span data-stu-id="c272f-165">You can use the portal to view the uploaded file in the storage container you configured:</span></span>

![Uploaded file](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="c272f-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="c272f-167">Next steps</span></span>

<span data-ttu-id="c272f-168">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span><span class="sxs-lookup"><span data-stu-id="c272f-168">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="c272f-169">You can continue to explore IoT hub features and scenarios with the following articles:</span><span class="sxs-lookup"><span data-stu-id="c272f-169">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="c272f-170">[Create an IoT hub programmatically][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="c272f-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="c272f-171">[Introduction to C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="c272f-171">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="c272f-172">[Azure IoT SDKs][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="c272f-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="c272f-173">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="c272f-173">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c272f-174">[Simulating a device with IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="c272f-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Azure IoT Developer Center]: http://azure.microsoft.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-quickstart-create-account.md
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: ../iot-edge/tutorial-simulate-device-linux.md


