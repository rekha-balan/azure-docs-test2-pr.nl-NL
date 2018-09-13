---
title: Cloud-to-device messages with Azure IoT Hub (iOS) | Microsoft Docs
description: How to send cloud-to-device messages to a device from an Azure IoT hub using the Azure IoT SDKs for iOS.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 04/19/2018
ms.author: kgremban
ms.openlocfilehash: 0bdedeb7338d30f448d4c6a6a991365cbb54c1ed
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865761"
---
# <a name="send-cloud-to-device-messages-with-iot-hub-ios"></a><span data-ttu-id="a6599-103">Send cloud-to-device messages with IoT Hub (iOS)</span><span class="sxs-lookup"><span data-stu-id="a6599-103">Send cloud-to-device messages with IoT Hub (iOS)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]


<span data-ttu-id="a6599-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="a6599-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="a6599-105">The [Send telemetry from a device to an IoT hub] article shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="a6599-105">The [Send telemetry from a device to an IoT hub] article shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="a6599-106">This article shows you how to:</span><span class="sxs-lookup"><span data-stu-id="a6599-106">This article shows you how to:</span></span>

* <span data-ttu-id="a6599-107">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a6599-107">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="a6599-108">Receive cloud-to-device messages on a device.</span><span class="sxs-lookup"><span data-stu-id="a6599-108">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="a6599-109">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a6599-109">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="a6599-110">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="a6599-110">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="a6599-111">At the end of this article, you run two Swift iOS projects:</span><span class="sxs-lookup"><span data-stu-id="a6599-111">At the end of this article, you run two Swift iOS projects:</span></span>

* <span data-ttu-id="a6599-112">**sample-device**, the same app created in [Send telemetry from a device to an IoT hub], which connects to your IoT hub and receives cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="a6599-112">**sample-device**, the same app created in [Send telemetry from a device to an IoT hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="a6599-113">**sample-service**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span><span class="sxs-lookup"><span data-stu-id="a6599-113">**sample-service**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="a6599-114">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="a6599-114">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="a6599-115">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="a6599-115">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="a6599-116">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="a6599-116">To complete this tutorial, you need the following:</span></span>

- <span data-ttu-id="a6599-117">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="a6599-117">An active Azure account.</span></span> <span data-ttu-id="a6599-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span><span class="sxs-lookup"><span data-stu-id="a6599-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>
- <span data-ttu-id="a6599-119">An active IoT hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6599-119">An active IoT hub in Azure.</span></span> 
- <span data-ttu-id="a6599-120">The code sample from [Azure samples](https://github.com/Azure-Samples/azure-iot-samples-ios/archive/master.zip) .</span><span class="sxs-lookup"><span data-stu-id="a6599-120">The code sample from [Azure samples](https://github.com/Azure-Samples/azure-iot-samples-ios/archive/master.zip) .</span></span>
- <span data-ttu-id="a6599-121">The latest version of [XCode](https://developer.apple.com/xcode/), running the latest version of the iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="a6599-121">The latest version of [XCode](https://developer.apple.com/xcode/), running the latest version of the iOS SDK.</span></span> <span data-ttu-id="a6599-122">This quickstart was tested with XCode 9.3 and iOS 11.3.</span><span class="sxs-lookup"><span data-stu-id="a6599-122">This quickstart was tested with XCode 9.3 and iOS 11.3.</span></span>
- <span data-ttu-id="a6599-123">The latest version of [CocoaPods](https://guides.cocoapods.org/using/getting-started.html).</span><span class="sxs-lookup"><span data-stu-id="a6599-123">The latest version of [CocoaPods](https://guides.cocoapods.org/using/getting-started.html).</span></span>


## <a name="simulate-an-iot-device"></a><span data-ttu-id="a6599-124">Simulate an IoT device</span><span class="sxs-lookup"><span data-stu-id="a6599-124">Simulate an IoT device</span></span>
<span data-ttu-id="a6599-125">In this section, you simulate an iOS device running a Swift application to receive cloud-to-device messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6599-125">In this section, you simulate an iOS device running a Swift application to receive cloud-to-device messages from the IoT hub.</span></span> 

<span data-ttu-id="a6599-126">This is the sample device that you create in the article [Send telemetry from a device to an IoT hub].</span><span class="sxs-lookup"><span data-stu-id="a6599-126">This is the sample device that you create in the article [Send telemetry from a device to an IoT hub].</span></span> <span data-ttu-id="a6599-127">If you already have that running, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="a6599-127">If you already have that running, you can skip this section.</span></span>

### <a name="install-cocoapods"></a><span data-ttu-id="a6599-128">Install CocoaPods</span><span class="sxs-lookup"><span data-stu-id="a6599-128">Install CocoaPods</span></span>

<span data-ttu-id="a6599-129">CocoaPods manage dependencies for iOS projects that use third-party libraries.</span><span class="sxs-lookup"><span data-stu-id="a6599-129">CocoaPods manage dependencies for iOS projects that use third-party libraries.</span></span>

<span data-ttu-id="a6599-130">In a terminal window, navigate to the Azure-IoT-Samples-iOS folder that you downloaded in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="a6599-130">In a terminal window, navigate to the Azure-IoT-Samples-iOS folder that you downloaded in the prerequisites.</span></span> <span data-ttu-id="a6599-131">Then, navigate to the sample project:</span><span class="sxs-lookup"><span data-stu-id="a6599-131">Then, navigate to the sample project:</span></span>

```sh
cd quickstart/sample-device
```

<span data-ttu-id="a6599-132">Make sure that XCode is closed, then run the following command to install the CocoaPods that are declared in the **podfile** file:</span><span class="sxs-lookup"><span data-stu-id="a6599-132">Make sure that XCode is closed, then run the following command to install the CocoaPods that are declared in the **podfile** file:</span></span>

```sh
pod install
```

<span data-ttu-id="a6599-133">Along with installing the pods required for your project, the installation command also created an XCode workspace file that is already configured to use the pods for dependencies.</span><span class="sxs-lookup"><span data-stu-id="a6599-133">Along with installing the pods required for your project, the installation command also created an XCode workspace file that is already configured to use the pods for dependencies.</span></span> 

### <a name="run-the-sample-device-application"></a><span data-ttu-id="a6599-134">Run the sample device application</span><span class="sxs-lookup"><span data-stu-id="a6599-134">Run the sample device application</span></span> 

1. <span data-ttu-id="a6599-135">Retrieve the connection string for your device.</span><span class="sxs-lookup"><span data-stu-id="a6599-135">Retrieve the connection string for your device.</span></span> <span data-ttu-id="a6599-136">You can copy this string from the Azure portal in the device details blade, or retrieve it with the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="a6599-136">You can copy this string from the Azure portal in the device details blade, or retrieve it with the following CLI command:</span></span> 

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id {YourDeviceID} --output table
    ```

1. <span data-ttu-id="a6599-137">Open the sample workspace in XCode.</span><span class="sxs-lookup"><span data-stu-id="a6599-137">Open the sample workspace in XCode.</span></span>

   ```sh
   open "MQTT Client Sample.xcworkspace"
   ```

2. <span data-ttu-id="a6599-138">Expand the **MQTT Client Sample** project and then folder of the same name.</span><span class="sxs-lookup"><span data-stu-id="a6599-138">Expand the **MQTT Client Sample** project and then folder of the same name.</span></span>  
3. <span data-ttu-id="a6599-139">Open **ViewController.swift** for editing in XCode.</span><span class="sxs-lookup"><span data-stu-id="a6599-139">Open **ViewController.swift** for editing in XCode.</span></span> 
4. <span data-ttu-id="a6599-140">Search for the **connectionString** variable and update the value with the device connection string that you copied in the first step.</span><span class="sxs-lookup"><span data-stu-id="a6599-140">Search for the **connectionString** variable and update the value with the device connection string that you copied in the first step.</span></span>
5. <span data-ttu-id="a6599-141">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="a6599-141">Save your changes.</span></span> 
6. <span data-ttu-id="a6599-142">Run the project in the device emulator with the **Build and run** button or the key combo **command + r**.</span><span class="sxs-lookup"><span data-stu-id="a6599-142">Run the project in the device emulator with the **Build and run** button or the key combo **command + r**.</span></span> 

   ![Run the project](media/quickstart-send-telemetry-ios/run-sample.png)


## <a name="simulate-a-service-device"></a><span data-ttu-id="a6599-144">Simulate a service device</span><span class="sxs-lookup"><span data-stu-id="a6599-144">Simulate a service device</span></span>

<span data-ttu-id="a6599-145">In this section, you simulate a second iOS device with a Swift app that sends cloud-to-device messages through the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6599-145">In this section, you simulate a second iOS device with a Swift app that sends cloud-to-device messages through the IoT hub.</span></span> <span data-ttu-id="a6599-146">This configuration is useful for IoT scenarios where there is one iPhone or iPad functioning as a controller for other iOS devices connected to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6599-146">This configuration is useful for IoT scenarios where there is one iPhone or iPad functioning as a controller for other iOS devices connected to an IoT hub.</span></span> 

### <a name="install-cocoapods"></a><span data-ttu-id="a6599-147">Install CocoaPods</span><span class="sxs-lookup"><span data-stu-id="a6599-147">Install CocoaPods</span></span>

<span data-ttu-id="a6599-148">CocoaPods manage dependencies for iOS projects that use third-party libraries.</span><span class="sxs-lookup"><span data-stu-id="a6599-148">CocoaPods manage dependencies for iOS projects that use third-party libraries.</span></span>

<span data-ttu-id="a6599-149">Navigate to the Azure IoT iOS Samples folder that you downloaded in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="a6599-149">Navigate to the Azure IoT iOS Samples folder that you downloaded in the prerequisites.</span></span> <span data-ttu-id="a6599-150">Then, navigate to the sample service project:</span><span class="sxs-lookup"><span data-stu-id="a6599-150">Then, navigate to the sample service project:</span></span>

```sh
cd quickstart/sample-service
```

<span data-ttu-id="a6599-151">Make sure that XCode is closed, then run the following command to install the CocoaPods that are declared in the **podfile** file:</span><span class="sxs-lookup"><span data-stu-id="a6599-151">Make sure that XCode is closed, then run the following command to install the CocoaPods that are declared in the **podfile** file:</span></span>

```sh
pod install
```

<span data-ttu-id="a6599-152">Along with installing the pods required for your project, the installation command also created an XCode workspace file that is already configured to use the pods for dependencies.</span><span class="sxs-lookup"><span data-stu-id="a6599-152">Along with installing the pods required for your project, the installation command also created an XCode workspace file that is already configured to use the pods for dependencies.</span></span>

### <a name="run-the-sample-service-application"></a><span data-ttu-id="a6599-153">Run the sample service application</span><span class="sxs-lookup"><span data-stu-id="a6599-153">Run the sample service application</span></span>

1. <span data-ttu-id="a6599-154">Retrieve the service connection string for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6599-154">Retrieve the service connection string for your IoT hub.</span></span> <span data-ttu-id="a6599-155">You can copy this string from the Azure portal from the **iothubowner** policy in the **Shared access policies** blade, or retrieve it with the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="a6599-155">You can copy this string from the Azure portal from the **iothubowner** policy in the **Shared access policies** blade, or retrieve it with the following CLI command:</span></span>  

    ```azurecli-interactive
    az iot hub show-connection-string --hub-name {YourIoTHubName} --output table
    ```

2. <span data-ttu-id="a6599-156">Open the sample workspace in XCode.</span><span class="sxs-lookup"><span data-stu-id="a6599-156">Open the sample workspace in XCode.</span></span>

   ```sh
   open AzureIoTServiceSample.xcworkspace
   ```

3. <span data-ttu-id="a6599-157">Expand the **AzureIoTServiceSample** project and then expand the folder of the same name.</span><span class="sxs-lookup"><span data-stu-id="a6599-157">Expand the **AzureIoTServiceSample** project and then expand the folder of the same name.</span></span>  
4. <span data-ttu-id="a6599-158">Open **ViewController.swift** for editing in XCode.</span><span class="sxs-lookup"><span data-stu-id="a6599-158">Open **ViewController.swift** for editing in XCode.</span></span> 
5. <span data-ttu-id="a6599-159">Search for the **connectionString** variable and update the value with the service connection string that you copied previously.</span><span class="sxs-lookup"><span data-stu-id="a6599-159">Search for the **connectionString** variable and update the value with the service connection string that you copied previously.</span></span>
6. <span data-ttu-id="a6599-160">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="a6599-160">Save your changes.</span></span> 
7. <span data-ttu-id="a6599-161">In Xcode, change the emulator settings to a different iOS device than you used to run the IoT device.</span><span class="sxs-lookup"><span data-stu-id="a6599-161">In Xcode, change the emulator settings to a different iOS device than you used to run the IoT device.</span></span> <span data-ttu-id="a6599-162">XCode cannot run multiple emulators of the same type.</span><span class="sxs-lookup"><span data-stu-id="a6599-162">XCode cannot run multiple emulators of the same type.</span></span> 

   ![Change the emulator device](media/iot-hub-ios-swift-c2d/change-device.png)

8. <span data-ttu-id="a6599-164">Run the project in the device emulator with the **Build and run** button or the key combo **Command + r**.</span><span class="sxs-lookup"><span data-stu-id="a6599-164">Run the project in the device emulator with the **Build and run** button or the key combo **Command + r**.</span></span> 

   ![Run the project](media/iot-hub-ios-swift-c2d/run-app.png)


## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="a6599-166">Send a cloud-to-device message</span><span class="sxs-lookup"><span data-stu-id="a6599-166">Send a cloud-to-device message</span></span>
<span data-ttu-id="a6599-167">You are now ready to use the two applications to send and receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="a6599-167">You are now ready to use the two applications to send and receive cloud-to-device messages.</span></span>

1. <span data-ttu-id="a6599-168">In the **iOS App Sample** app running on the simulated IoT device, click **Start**.</span><span class="sxs-lookup"><span data-stu-id="a6599-168">In the **iOS App Sample** app running on the simulated IoT device, click **Start**.</span></span> <span data-ttu-id="a6599-169">The application starts sending device-to-cloud messages, but also starts listening for cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="a6599-169">The application starts sending device-to-cloud messages, but also starts listening for cloud-to-device messages.</span></span> 

   ![View sample IoT device app](media/iot-hub-ios-swift-c2d/view-d2c.png)

2. <span data-ttu-id="a6599-171">In the **IoTHub Service Client Sample** app running on the simulated service device, enter the ID for the IoT device that you want a to send a message to.</span><span class="sxs-lookup"><span data-stu-id="a6599-171">In the **IoTHub Service Client Sample** app running on the simulated service device, enter the ID for the IoT device that you want a to send a message to.</span></span> 
3. <span data-ttu-id="a6599-172">Write a plaintext message, then click **Send**.</span><span class="sxs-lookup"><span data-stu-id="a6599-172">Write a plaintext message, then click **Send**.</span></span> 

<span data-ttu-id="a6599-173">Several actions happen as soon as you click send.</span><span class="sxs-lookup"><span data-stu-id="a6599-173">Several actions happen as soon as you click send.</span></span> <span data-ttu-id="a6599-174">The service sample sends the message to your IoT hub, which the app has access to because of the service connection string that you provided.</span><span class="sxs-lookup"><span data-stu-id="a6599-174">The service sample sends the message to your IoT hub, which the app has access to because of the service connection string that you provided.</span></span> <span data-ttu-id="a6599-175">Your IoT hub checks the device ID, sends the message to the destination device, and sends a confirmation receipt to the source device.</span><span class="sxs-lookup"><span data-stu-id="a6599-175">Your IoT hub checks the device ID, sends the message to the destination device, and sends a confirmation receipt to the source device.</span></span> <span data-ttu-id="a6599-176">The app running on your simulated IoT device checks for messages from IoT Hub and prints the text from the most recent one on the screen.</span><span class="sxs-lookup"><span data-stu-id="a6599-176">The app running on your simulated IoT device checks for messages from IoT Hub and prints the text from the most recent one on the screen.</span></span>

<span data-ttu-id="a6599-177">Your output should look like the following example:</span><span class="sxs-lookup"><span data-stu-id="a6599-177">Your output should look like the following example:</span></span>

   ![View cloud-to-device messages](media/iot-hub-ios-swift-c2d/view-c2d.png)


## <a name="next-steps"></a><span data-ttu-id="a6599-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6599-179">Next steps</span></span>
<span data-ttu-id="a6599-180">In this tutorial, you learned how to send and receive cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="a6599-180">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="a6599-181">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Remote Monitoring solution accelerator].</span><span class="sxs-lookup"><span data-stu-id="a6599-181">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Remote Monitoring solution accelerator].</span></span>

<span data-ttu-id="a6599-182">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span><span class="sxs-lookup"><span data-stu-id="a6599-182">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-python-python-c2d/simulated-device.png
[img-send-command]:  media/iot-hub-python-python-c2d/send-command.png
[img-message-recieved]: media/iot-hub-python-python-c2d/message-recieved.png

<!-- Links -->
[Send telemetry from a device to an IoT hub]: quickstart-send-telemetry-ios.md

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IoT Hub developer guide]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure portal]: https://portal.azure.com
[Azure IoT Remote Monitoring solution accelerator]: https://azure.microsoft.com/documentation/suites/iot-suite/
