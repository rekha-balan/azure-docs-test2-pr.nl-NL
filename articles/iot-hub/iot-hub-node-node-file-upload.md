---
title: Upload files from devices to Azure IoT Hub with Node | Microsoft Docs
description: How to upload files from a device to the cloud using Azure IoT device SDK for Node.js. Uploaded files are stored in an Azure storage blob container.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: nodejs
ms.topic: conceptual
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 936063e1419d5e2261033ea74d75687eade928e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868820"
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub"></a><span data-ttu-id="7d0a9-104">Upload files from your device to the cloud with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7d0a9-104">Upload files from your device to the cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="7d0a9-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-node-node-c2d.md) tutorial to show you how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.yml).</span><span class="sxs-lookup"><span data-stu-id="7d0a9-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-node-node-c2d.md) tutorial to show you how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.yml).</span></span> <span data-ttu-id="7d0a9-106">The tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-106">The tutorial shows you how to:</span></span>

- <span data-ttu-id="7d0a9-107">Securely provide a device with an Azure blob URI for uploading a file.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="7d0a9-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="7d0a9-109">The [Get started with IoT Hub](quickstart-send-telemetry-node.md) tutorial demonstrates the basic device-to-cloud messaging functionality of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-109">The [Get started with IoT Hub](quickstart-send-telemetry-node.md) tutorial demonstrates the basic device-to-cloud messaging functionality of IoT Hub.</span></span> <span data-ttu-id="7d0a9-110">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-110">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="7d0a9-111">For example:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-111">For example:</span></span>

* <span data-ttu-id="7d0a9-112">Large files that contain images</span><span class="sxs-lookup"><span data-stu-id="7d0a9-112">Large files that contain images</span></span>
* <span data-ttu-id="7d0a9-113">Videos</span><span class="sxs-lookup"><span data-stu-id="7d0a9-113">Videos</span></span>
* <span data-ttu-id="7d0a9-114">Vibration data sampled at high frequency</span><span class="sxs-lookup"><span data-stu-id="7d0a9-114">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="7d0a9-115">Some form of preprocessed data.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-115">Some form of preprocessed data.</span></span>

<span data-ttu-id="7d0a9-116">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/introduction.md) or the [Hadoop](../hdinsight/index.yml) stack.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-116">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/introduction.md) or the [Hadoop](../hdinsight/index.yml) stack.</span></span> <span data-ttu-id="7d0a9-117">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-117">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="7d0a9-118">At the end of this tutorial you run two Node.js console apps:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-118">At the end of this tutorial you run two Node.js console apps:</span></span>

* <span data-ttu-id="7d0a9-119">**SimulatedDevice.js**, which uploads a file to storage using a SAS URI provided by your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-119">**SimulatedDevice.js**, which uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="7d0a9-120">**ReadFileUploadNotification.js**, which receives file upload notifications from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-120">**ReadFileUploadNotification.js**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="7d0a9-121">IoT Hub supports many device platforms and languages (including C, .NET, Javascript, Python, and Java) through Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-121">IoT Hub supports many device platforms and languages (including C, .NET, Javascript, Python, and Java) through Azure IoT device SDKs.</span></span> <span data-ttu-id="7d0a9-122">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-122">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="7d0a9-123">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-123">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="7d0a9-124">Node.js version 4.0.x or later.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-124">Node.js version 4.0.x or later.</span></span>
* <span data-ttu-id="7d0a9-125">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-125">An active Azure account.</span></span> <span data-ttu-id="7d0a9-126">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="7d0a9-126">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="7d0a9-127">Upload a file from a device app</span><span class="sxs-lookup"><span data-stu-id="7d0a9-127">Upload a file from a device app</span></span>

<span data-ttu-id="7d0a9-128">In this section, you create the device app to upload a file to IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-128">In this section, you create the device app to upload a file to IoT hub.</span></span>

1. <span data-ttu-id="7d0a9-129">Create an empty folder called ```simulateddevice```.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-129">Create an empty folder called ```simulateddevice```.</span></span>  <span data-ttu-id="7d0a9-130">In the ```simulateddevice``` folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-130">In the ```simulateddevice``` folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="7d0a9-131">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-131">Accept all the defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="7d0a9-132">At your command prompt in the ```simulateddevice``` folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-132">At your command prompt in the ```simulateddevice``` folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="7d0a9-133">Using a text editor, create a **SimulatedDevice.js** file in the ```simulateddevice``` folder.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-133">Using a text editor, create a **SimulatedDevice.js** file in the ```simulateddevice``` folder.</span></span>

1. <span data-ttu-id="7d0a9-134">Add the following ```require``` statements at the start of the **SimulatedDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-134">Add the following ```require``` statements at the start of the **SimulatedDevice.js** file:</span></span>

    ```nodejs
    'use strict';
    
    var fs = require('fs');
    var mqtt = require('azure-iot-device-mqtt').Mqtt;
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    ```

1. <span data-ttu-id="7d0a9-135">Add a ```deviceconnectionstring``` variable and use it to create a **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-135">Add a ```deviceconnectionstring``` variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="7d0a9-136">Replace ```{deviceconnectionstring}``` with the name of the device you created in the _Create an IoT Hub_ section:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-136">Replace ```{deviceconnectionstring}``` with the name of the device you created in the _Create an IoT Hub_ section:</span></span>

    ```nodejs
    var connectionString = '{deviceconnectionstring}';
    var filename = 'myimage.png';
    ```

    > [!NOTE]
    > <span data-ttu-id="7d0a9-137">For the sake of simplicity the connection string is included in the code: this is not a recommended practice and depending on your use-case and architecture you may want to consider more secure ways of storing this secret.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-137">For the sake of simplicity the connection string is included in the code: this is not a recommended practice and depending on your use-case and architecture you may want to consider more secure ways of storing this secret.</span></span>

1. <span data-ttu-id="7d0a9-138">Add the following code to connect the client:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-138">Add the following code to connect the client:</span></span>

    ```nodejs
    var client = clientFromConnectionString(connectionString);
    console.log('Client connected');
    ```

1. <span data-ttu-id="7d0a9-139">Create a callback and use the **uploadToBlob** function to upload the file.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-139">Create a callback and use the **uploadToBlob** function to upload the file.</span></span>

    ```nodejs
    fs.stat(filename, function (err, stats) {
        const rr = fs.createReadStream(filename);
    
        client.uploadToBlob(filename, rr, stats.size, function (err) {
            if (err) {
                console.error('Error uploading file: ' + err.toString());
            } else {
                console.log('File uploaded');
            }
        });
    });
    ```

1. <span data-ttu-id="7d0a9-140">Save and close the **SimulatedDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-140">Save and close the **SimulatedDevice.js** file.</span></span>

1. <span data-ttu-id="7d0a9-141">Copy an image file to the `simulateddevice` folder and rename it `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-141">Copy an image file to the `simulateddevice` folder and rename it `myimage.png`.</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="7d0a9-142">Receive a file upload notification</span><span class="sxs-lookup"><span data-stu-id="7d0a9-142">Receive a file upload notification</span></span>

<span data-ttu-id="7d0a9-143">In this section, you create a Node.js console app that receives file upload notification messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-143">In this section, you create a Node.js console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="7d0a9-144">You can use the **iothubowner** connection string from your IoT Hub to complete this section.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-144">You can use the **iothubowner** connection string from your IoT Hub to complete this section.</span></span> <span data-ttu-id="7d0a9-145">You will find the connection string in the [Azure portal](https://portal.azure.com/) on the **Shared access policy** blade.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-145">You will find the connection string in the [Azure portal](https://portal.azure.com/) on the **Shared access policy** blade.</span></span>

1. <span data-ttu-id="7d0a9-146">Create an empty folder called ```fileuploadnotification```.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-146">Create an empty folder called ```fileuploadnotification```.</span></span>  <span data-ttu-id="7d0a9-147">In the ```fileuploadnotification``` folder, create a package.json file using the following command at your command prompt.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-147">In the ```fileuploadnotification``` folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="7d0a9-148">Accept all the defaults:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-148">Accept all the defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="7d0a9-149">At your command prompt in the ```fileuploadnotification``` folder, run the following command to install the **azure-iothub** SDK package:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-149">At your command prompt in the ```fileuploadnotification``` folder, run the following command to install the **azure-iothub** SDK package:</span></span>

    ```cmd/sh
    npm install azure-iothub --save
    ```

1. <span data-ttu-id="7d0a9-150">Using a text editor, create a **FileUploadNotification.js** file in the ```fileuploadnotification``` folder.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-150">Using a text editor, create a **FileUploadNotification.js** file in the ```fileuploadnotification``` folder.</span></span>

1. <span data-ttu-id="7d0a9-151">Add the following ```require``` statements at the start of the **FileUploadNotification.js** file:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-151">Add the following ```require``` statements at the start of the **FileUploadNotification.js** file:</span></span>

    ```nodejs
    'use strict';
    
    var Client = require('azure-iothub').Client;
    ```

1. <span data-ttu-id="7d0a9-152">Add a ```iothubconnectionstring``` variable and use it to create a **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-152">Add a ```iothubconnectionstring``` variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="7d0a9-153">Replace ```{iothubconnectionstring}``` with the connection string to the IoT hub you created in the _Create an IoT Hub_ section:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-153">Replace ```{iothubconnectionstring}``` with the connection string to the IoT hub you created in the _Create an IoT Hub_ section:</span></span>

    ```nodejs
    var connectionString = '{iothubconnectionstring}';
    ```

    > [!NOTE]
    > <span data-ttu-id="7d0a9-154">For the sake of simplicity the connection string is included in the code: this is not a recommended practice and depending on your use-case and architecture you may want to consider more secure ways of storing this secret.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-154">For the sake of simplicity the connection string is included in the code: this is not a recommended practice and depending on your use-case and architecture you may want to consider more secure ways of storing this secret.</span></span>

1. <span data-ttu-id="7d0a9-155">Add the following code to connect the client:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-155">Add the following code to connect the client:</span></span>

    ```nodejs
    var serviceClient = Client.fromConnectionString(connectionString);
    ```

1. <span data-ttu-id="7d0a9-156">Open the client and use the **getFileNotificationReceiver** function to receive status updates.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-156">Open the client and use the **getFileNotificationReceiver** function to receive status updates.</span></span>

    ```nodejs
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFileNotificationReceiver(function receiveFileUploadNotification(err, receiver){
          if (err) {
            console.error('error getting the file notification receiver: ' + err.toString());
          } else {
            receiver.on('message', function (msg) {
              console.log('File upload from device:')
              console.log(msg.getData().toString('utf-8'));
            });
          }
        });
      }
    });
    ```

1. <span data-ttu-id="7d0a9-157">Save and close the **FileUploadNotification.js** file.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-157">Save and close the **FileUploadNotification.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="7d0a9-158">Run the applications</span><span class="sxs-lookup"><span data-stu-id="7d0a9-158">Run the applications</span></span>

<span data-ttu-id="7d0a9-159">Now you are ready to run the applications.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-159">Now you are ready to run the applications.</span></span>

<span data-ttu-id="7d0a9-160">At a command prompt in the `fileuploadnotification` folder, run the following command:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-160">At a command prompt in the `fileuploadnotification` folder, run the following command:</span></span>

```cmd/sh
node FileUploadNotification.js
```

<span data-ttu-id="7d0a9-161">At a command prompt in the `simulateddevice` folder, run the following command:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-161">At a command prompt in the `simulateddevice` folder, run the following command:</span></span>

```cmd/sh
node SimulatedDevice.js
```

<span data-ttu-id="7d0a9-162">The following screenshot shows the output from the **SimulatedDevice** app:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-162">The following screenshot shows the output from the **SimulatedDevice** app:</span></span>

![Output from simulated-device app](./media/iot-hub-node-node-file-upload/simulated-device.png)

<span data-ttu-id="7d0a9-164">The following screenshot shows the output from the **FileUploadNotification** app:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-164">The following screenshot shows the output from the **FileUploadNotification** app:</span></span>

![Output from read-file-upload-notification app](./media/iot-hub-node-node-file-upload/read-file-upload-notification.png)

<span data-ttu-id="7d0a9-166">You can use the portal to view the uploaded file in the storage container you configured:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-166">You can use the portal to view the uploaded file in the storage container you configured:</span></span>

![Uploaded file](./media/iot-hub-node-node-file-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="7d0a9-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="7d0a9-168">Next steps</span></span>

<span data-ttu-id="7d0a9-169">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span><span class="sxs-lookup"><span data-stu-id="7d0a9-169">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="7d0a9-170">You can continue to explore IoT hub features and scenarios with the following articles:</span><span class="sxs-lookup"><span data-stu-id="7d0a9-170">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="7d0a9-171">[Create an IoT hub programmatically][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="7d0a9-171">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="7d0a9-172">[Introduction to C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="7d0a9-172">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="7d0a9-173">[Azure IoT SDKs][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="7d0a9-173">[Azure IoT SDKs][lnk-sdks]</span></span>

<!-- Links -->
[Azure IoT Developer Center]: http://azure.microsoft.com/develop/iot

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md
