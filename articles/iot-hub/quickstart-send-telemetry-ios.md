---
title: Send telemetry to Azure IoT Hub quickstart | Microsoft Docs
description: In this quickstart, you run a sample iOS application to send simulated telemetry to an IoT hub and to read telemetry from the IoT hub for processing in the cloud.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: quickstart
ms.custom: mvc
ms.date: 04/20/2018
ms.author: kgremban
ms.openlocfilehash: aecb9a1819060e0da6338e8e16bf681fad42dd22
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968008"
---
# <a name="quickstart-send-telemetry-from-a-device-to-an-iot-hub-ios"></a><span data-ttu-id="02097-103">Quickstart: Send telemetry from a device to an IoT hub (iOS)</span><span class="sxs-lookup"><span data-stu-id="02097-103">Quickstart: Send telemetry from a device to an IoT hub (iOS)</span></span>

[!INCLUDE [iot-hub-quickstarts-1-selector](../../includes/iot-hub-quickstarts-1-selector.md)]

<span data-ttu-id="02097-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span><span class="sxs-lookup"><span data-stu-id="02097-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span></span> <span data-ttu-id="02097-105">In this article, you send telemetry from a simulated device application to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="02097-105">In this article, you send telemetry from a simulated device application to IoT Hub.</span></span> <span data-ttu-id="02097-106">Then you can view the data from a back-end application.</span><span class="sxs-lookup"><span data-stu-id="02097-106">Then you can view the data from a back-end application.</span></span> 

<span data-ttu-id="02097-107">This article uses a pre-written Swift application to send the telemetry and a CLI utility to read the telemetry from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="02097-107">This article uses a pre-written Swift application to send the telemetry and a CLI utility to read the telemetry from IoT Hub.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="02097-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="02097-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02097-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="02097-109">Prerequisites</span></span>

- <span data-ttu-id="02097-110">Download the code sample from [Azure samples](https://github.com/Azure-Samples/azure-iot-samples-ios/archive/master.zip)</span><span class="sxs-lookup"><span data-stu-id="02097-110">Download the code sample from [Azure samples](https://github.com/Azure-Samples/azure-iot-samples-ios/archive/master.zip)</span></span> 
- <span data-ttu-id="02097-111">The latest version of [XCode](https://developer.apple.com/xcode/), running the latest version of the iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="02097-111">The latest version of [XCode](https://developer.apple.com/xcode/), running the latest version of the iOS SDK.</span></span> <span data-ttu-id="02097-112">This quickstart was tested with XCode 9.3 and iOS 11.3.</span><span class="sxs-lookup"><span data-stu-id="02097-112">This quickstart was tested with XCode 9.3 and iOS 11.3.</span></span>
- <span data-ttu-id="02097-113">The latest version of [CocoaPods](https://guides.cocoapods.org/using/getting-started.html).</span><span class="sxs-lookup"><span data-stu-id="02097-113">The latest version of [CocoaPods](https://guides.cocoapods.org/using/getting-started.html).</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="02097-114">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="02097-114">Create an IoT hub</span></span>

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]

## <a name="register-a-device"></a><span data-ttu-id="02097-115">Register a device</span><span class="sxs-lookup"><span data-stu-id="02097-115">Register a device</span></span>

<span data-ttu-id="02097-116">A device must be registered with your IoT hub before it can connect.</span><span class="sxs-lookup"><span data-stu-id="02097-116">A device must be registered with your IoT hub before it can connect.</span></span> <span data-ttu-id="02097-117">In this quickstart, you use the Azure CLI to register a simulated device.</span><span class="sxs-lookup"><span data-stu-id="02097-117">In this quickstart, you use the Azure CLI to register a simulated device.</span></span>

1. <span data-ttu-id="02097-118">Add the IoT Hub CLI extension and create the device identity.</span><span class="sxs-lookup"><span data-stu-id="02097-118">Add the IoT Hub CLI extension and create the device identity.</span></span> <span data-ttu-id="02097-119">Replace `{YourIoTHubName}` with a name for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="02097-119">Replace `{YourIoTHubName}` with a name for your IoT hub:</span></span>

   ```azurecli-interactive
   az extension add --name azure-cli-iot-ext
   az iot hub device-identity create --hub-name {YourIoTHubName} --device-id myiOSdevice
   ```

    <span data-ttu-id="02097-120">If you choose a different name for your device, update the device name in the sample applications before you run them.</span><span class="sxs-lookup"><span data-stu-id="02097-120">If you choose a different name for your device, update the device name in the sample applications before you run them.</span></span>

1. <span data-ttu-id="02097-121">Run the following command to get the _device connection string_ for the device you just registered:</span><span class="sxs-lookup"><span data-stu-id="02097-121">Run the following command to get the _device connection string_ for the device you just registered:</span></span>

   ```azurecli-interactive
   az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id myiOSdevice --output table
   ```

   <span data-ttu-id="02097-122">Make a note of the device connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="02097-122">Make a note of the device connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="02097-123">You use this value later in the article.</span><span class="sxs-lookup"><span data-stu-id="02097-123">You use this value later in the article.</span></span>

## <a name="send-simulated-telemetry"></a><span data-ttu-id="02097-124">Send simulated telemetry</span><span class="sxs-lookup"><span data-stu-id="02097-124">Send simulated telemetry</span></span>

<span data-ttu-id="02097-125">The sample application runs on an iOS device, which connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span><span class="sxs-lookup"><span data-stu-id="02097-125">The sample application runs on an iOS device, which connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span></span> 

### <a name="install-cocoapods"></a><span data-ttu-id="02097-126">Install CocoaPods</span><span class="sxs-lookup"><span data-stu-id="02097-126">Install CocoaPods</span></span>

<span data-ttu-id="02097-127">CocoaPods manage dependencies for iOS projects that use third-party libraries.</span><span class="sxs-lookup"><span data-stu-id="02097-127">CocoaPods manage dependencies for iOS projects that use third-party libraries.</span></span>

<span data-ttu-id="02097-128">In a terminal window, navigate to the Azure-IoT-Samples-iOS folder that you downloaded in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="02097-128">In a terminal window, navigate to the Azure-IoT-Samples-iOS folder that you downloaded in the prerequisites.</span></span> <span data-ttu-id="02097-129">Then, navigate to the sample project:</span><span class="sxs-lookup"><span data-stu-id="02097-129">Then, navigate to the sample project:</span></span>

```sh
cd quickstart/sample-device
```

<span data-ttu-id="02097-130">Make sure that XCode is closed, then run the following command to install the CocoaPods that are declared in the **podfile** file:</span><span class="sxs-lookup"><span data-stu-id="02097-130">Make sure that XCode is closed, then run the following command to install the CocoaPods that are declared in the **podfile** file:</span></span>

```sh
pod install
```

<span data-ttu-id="02097-131">Along with installing the pods required for your project, the installation command also created an XCode workspace file that is already configured to use the pods for dependencies.</span><span class="sxs-lookup"><span data-stu-id="02097-131">Along with installing the pods required for your project, the installation command also created an XCode workspace file that is already configured to use the pods for dependencies.</span></span> 

### <a name="run-the-sample-application"></a><span data-ttu-id="02097-132">Run the sample application</span><span class="sxs-lookup"><span data-stu-id="02097-132">Run the sample application</span></span> 

1. <span data-ttu-id="02097-133">Open the sample workspace in XCode.</span><span class="sxs-lookup"><span data-stu-id="02097-133">Open the sample workspace in XCode.</span></span>

   ```sh
   open "MQTT Client Sample.xcworkspace"
   ```

2. <span data-ttu-id="02097-134">Expand the **MQTT Client Sample** project and then expand the folder of the same name.</span><span class="sxs-lookup"><span data-stu-id="02097-134">Expand the **MQTT Client Sample** project and then expand the folder of the same name.</span></span>  
3. <span data-ttu-id="02097-135">Open **ViewController.swift** for editing in XCode.</span><span class="sxs-lookup"><span data-stu-id="02097-135">Open **ViewController.swift** for editing in XCode.</span></span> 
4. <span data-ttu-id="02097-136">Search for the **connectionString** variable and update the value with the device connection string that you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="02097-136">Search for the **connectionString** variable and update the value with the device connection string that you made a note of previously.</span></span>
5. <span data-ttu-id="02097-137">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="02097-137">Save your changes.</span></span> 
6. <span data-ttu-id="02097-138">Run the project in the device emulator with the **Build and run** button or the key combo **command + r**.</span><span class="sxs-lookup"><span data-stu-id="02097-138">Run the project in the device emulator with the **Build and run** button or the key combo **command + r**.</span></span> 

   ![Run the project](media/quickstart-send-telemetry-ios/run-sample.png)

7. <span data-ttu-id="02097-140">When the emulator opens, select **Start** in the sample app.</span><span class="sxs-lookup"><span data-stu-id="02097-140">When the emulator opens, select **Start** in the sample app.</span></span>

<span data-ttu-id="02097-141">The following screenshot shows some example output as the application sends simulated telemetry to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="02097-141">The following screenshot shows some example output as the application sends simulated telemetry to your IoT hub:</span></span>

   ![Run the simulated device](media/quickstart-send-telemetry-ios/view-d2c.png)

## <a name="read-the-telemetry-from-your-hub"></a><span data-ttu-id="02097-143">Read the telemetry from your hub</span><span class="sxs-lookup"><span data-stu-id="02097-143">Read the telemetry from your hub</span></span>

<span data-ttu-id="02097-144">The sample app that you ran on the XCode emulator shows data about messages sent from the device.</span><span class="sxs-lookup"><span data-stu-id="02097-144">The sample app that you ran on the XCode emulator shows data about messages sent from the device.</span></span> <span data-ttu-id="02097-145">You can also view the data through your IoT hub as it is received.</span><span class="sxs-lookup"><span data-stu-id="02097-145">You can also view the data through your IoT hub as it is received.</span></span> <span data-ttu-id="02097-146">The IoT Hub CLI extension can connect to the service-side **Events** endpoint on your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="02097-146">The IoT Hub CLI extension can connect to the service-side **Events** endpoint on your IoT Hub.</span></span> <span data-ttu-id="02097-147">The extension receives the device-to-cloud messages sent from your simulated device.</span><span class="sxs-lookup"><span data-stu-id="02097-147">The extension receives the device-to-cloud messages sent from your simulated device.</span></span> <span data-ttu-id="02097-148">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="02097-148">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span></span>

<span data-ttu-id="02097-149">Run the following Azure CLI commands, replacing `{YourIoTHubName}` with the name of your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="02097-149">Run the following Azure CLI commands, replacing `{YourIoTHubName}` with the name of your IoT hub:</span></span>

```azurecli-interactive
az iot hub monitor-events --device-id myiOSdevice --hub-name {YourIoTHubName}
```

<span data-ttu-id="02097-150">The following screenshot shows the output as the extension receives telemetry sent by the simulated device to the hub:</span><span class="sxs-lookup"><span data-stu-id="02097-150">The following screenshot shows the output as the extension receives telemetry sent by the simulated device to the hub:</span></span>

<span data-ttu-id="02097-151">The following screenshot shows the type of telemetry that you see in your terminal window:</span><span class="sxs-lookup"><span data-stu-id="02097-151">The following screenshot shows the type of telemetry that you see in your terminal window:</span></span>

![View telemetry](media/quickstart-send-telemetry-ios/view-telemetry.png)

## <a name="clean-up-resources"></a><span data-ttu-id="02097-153">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="02097-153">Clean up resources</span></span>

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="02097-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="02097-154">Next steps</span></span>

<span data-ttu-id="02097-155">In this article, you set up an IoT hub, registered a device, sent simulated telemetry to the hub from an iOS device, and read the telemetry from the hub.</span><span class="sxs-lookup"><span data-stu-id="02097-155">In this article, you set up an IoT hub, registered a device, sent simulated telemetry to the hub from an iOS device, and read the telemetry from the hub.</span></span> 

<span data-ttu-id="02097-156">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span><span class="sxs-lookup"><span data-stu-id="02097-156">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="02097-157">Quickstart: Control a device connected to an IoT hub</span><span class="sxs-lookup"><span data-stu-id="02097-157">Quickstart: Control a device connected to an IoT hub</span></span>](quickstart-control-device-node.md)

<!-- Links -->
[lnk-process-d2c-tutorial]: tutorial-routing.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: ../iot-edge/tutorial-simulate-device-linux.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
