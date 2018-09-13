---
title: Control a device from Azure IoT Hub quickstart (Java) | Microsoft Docs
description: In this quickstart, you run two sample Java applications. One application is a back-end application that can remotely control devices connected to your hub. The other application simulates a device connected to your hub that can be controlled remotely.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: java
ms.topic: quickstart
ms.custom: mvc
ms.date: 06/22/2018
ms.author: dobett
ms.openlocfilehash: 5da4248f0b0a72c3614b4c3e5ea042c4341f4e03
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868817"
---
# <a name="quickstart-control-a-device-connected-to-an-iot-hub-java"></a><span data-ttu-id="abb1c-105">Quickstart: Control a device connected to an IoT hub (Java)</span><span class="sxs-lookup"><span data-stu-id="abb1c-105">Quickstart: Control a device connected to an IoT hub (Java)</span></span>

[!INCLUDE [iot-hub-quickstarts-2-selector](../../includes/iot-hub-quickstarts-2-selector.md)]

<span data-ttu-id="abb1c-106">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud and manage your devices from the cloud.</span><span class="sxs-lookup"><span data-stu-id="abb1c-106">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud and manage your devices from the cloud.</span></span> <span data-ttu-id="abb1c-107">In this quickstart, you use a *direct method* to control a simulated device connected to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="abb1c-107">In this quickstart, you use a *direct method* to control a simulated device connected to your IoT hub.</span></span> <span data-ttu-id="abb1c-108">You can use direct methods to remotely change the behavior of a device connected to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="abb1c-108">You can use direct methods to remotely change the behavior of a device connected to your IoT hub.</span></span>

<span data-ttu-id="abb1c-109">The quickstart uses two pre-written Java applications:</span><span class="sxs-lookup"><span data-stu-id="abb1c-109">The quickstart uses two pre-written Java applications:</span></span>

* <span data-ttu-id="abb1c-110">A simulated device application that responds to direct methods called from a back-end application.</span><span class="sxs-lookup"><span data-stu-id="abb1c-110">A simulated device application that responds to direct methods called from a back-end application.</span></span> <span data-ttu-id="abb1c-111">To receive the direct method calls, this application connects to a device-specific endpoint on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="abb1c-111">To receive the direct method calls, this application connects to a device-specific endpoint on your IoT hub.</span></span>
* <span data-ttu-id="abb1c-112">A back-end application that calls the direct methods on the simulated device.</span><span class="sxs-lookup"><span data-stu-id="abb1c-112">A back-end application that calls the direct methods on the simulated device.</span></span> <span data-ttu-id="abb1c-113">To call a direct method on a device, this application connects to service-side endpoint on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="abb1c-113">To call a direct method on a device, this application connects to service-side endpoint on your IoT hub.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="abb1c-114">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="abb1c-114">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abb1c-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="abb1c-115">Prerequisites</span></span>

<span data-ttu-id="abb1c-116">The two sample applications you run in this quickstart are written using Java.</span><span class="sxs-lookup"><span data-stu-id="abb1c-116">The two sample applications you run in this quickstart are written using Java.</span></span> <span data-ttu-id="abb1c-117">You need Java SE 8 or later on your development machine.</span><span class="sxs-lookup"><span data-stu-id="abb1c-117">You need Java SE 8 or later on your development machine.</span></span>

<span data-ttu-id="abb1c-118">You can download Java for multiple platforms from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="abb1c-118">You can download Java for multiple platforms from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

<span data-ttu-id="abb1c-119">You can verify the current version of Java on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="abb1c-119">You can verify the current version of Java on your development machine using the following command:</span></span>

```cmd/sh
java --version
```

<span data-ttu-id="abb1c-120">To build the samples, you need to install Maven 3.</span><span class="sxs-lookup"><span data-stu-id="abb1c-120">To build the samples, you need to install Maven 3.</span></span> <span data-ttu-id="abb1c-121">You can download Maven for multiple platforms from [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="abb1c-121">You can download Maven for multiple platforms from [Apache Maven](https://maven.apache.org/download.cgi).</span></span>

<span data-ttu-id="abb1c-122">You can verify the current version of Maven on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="abb1c-122">You can verify the current version of Maven on your development machine using the following command:</span></span>

```cmd/sh
mvn --version
```

<span data-ttu-id="abb1c-123">If you haven't already done so, download the sample Java project from https://github.com/Azure-Samples/azure-iot-samples-java/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="abb1c-123">If you haven't already done so, download the sample Java project from https://github.com/Azure-Samples/azure-iot-samples-java/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="abb1c-124">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="abb1c-124">Create an IoT hub</span></span>

<span data-ttu-id="abb1c-125">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-java.md), you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="abb1c-125">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-java.md), you can skip this step.</span></span>

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]

## <a name="register-a-device"></a><span data-ttu-id="abb1c-126">Register a device</span><span class="sxs-lookup"><span data-stu-id="abb1c-126">Register a device</span></span>

<span data-ttu-id="abb1c-127">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-java.md), you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="abb1c-127">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-java.md), you can skip this step.</span></span>

<span data-ttu-id="abb1c-128">A device must be registered with your IoT hub before it can connect.</span><span class="sxs-lookup"><span data-stu-id="abb1c-128">A device must be registered with your IoT hub before it can connect.</span></span> <span data-ttu-id="abb1c-129">In this quickstart, you use the Azure CLI to register a simulated device.</span><span class="sxs-lookup"><span data-stu-id="abb1c-129">In this quickstart, you use the Azure CLI to register a simulated device.</span></span>

1. <span data-ttu-id="abb1c-130">Add the IoT Hub CLI extension and create the device identity.</span><span class="sxs-lookup"><span data-stu-id="abb1c-130">Add the IoT Hub CLI extension and create the device identity.</span></span> <span data-ttu-id="abb1c-131">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="abb1c-131">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span></span>

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name {YourIoTHubName} --device-id MyJavaDevice
    ```

    <span data-ttu-id="abb1c-132">If you choose a different name for your device, update the device name in the sample applications before you run them.</span><span class="sxs-lookup"><span data-stu-id="abb1c-132">If you choose a different name for your device, update the device name in the sample applications before you run them.</span></span>

2. <span data-ttu-id="abb1c-133">Run the following command to get the _device connection string_ for the device you just registered:</span><span class="sxs-lookup"><span data-stu-id="abb1c-133">Run the following command to get the _device connection string_ for the device you just registered:</span></span>

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id MyJavaDevice --output table
    ```

    <span data-ttu-id="abb1c-134">Make a note of the device connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="abb1c-134">Make a note of the device connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="abb1c-135">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="abb1c-135">You use this value later in the quickstart.</span></span>

## <a name="retrieve-the-service-connection-string"></a><span data-ttu-id="abb1c-136">Retrieve the service connection string</span><span class="sxs-lookup"><span data-stu-id="abb1c-136">Retrieve the service connection string</span></span>

<span data-ttu-id="abb1c-137">You also need your IoT hub _service connection string_ to enable the back-end application to connect to the hub and retrieve the messages.</span><span class="sxs-lookup"><span data-stu-id="abb1c-137">You also need your IoT hub _service connection string_ to enable the back-end application to connect to the hub and retrieve the messages.</span></span> <span data-ttu-id="abb1c-138">The following command retrieves the service connection string for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="abb1c-138">The following command retrieves the service connection string for your IoT hub:</span></span>

```azurecli-interactive
az iot hub show-connection-string --hub-name {YourIoTHubName} --output table
```

<span data-ttu-id="abb1c-139">Make a note of the service connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="abb1c-139">Make a note of the service connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="abb1c-140">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="abb1c-140">You use this value later in the quickstart.</span></span>

## <a name="listen-for-direct-method-calls"></a><span data-ttu-id="abb1c-141">Listen for direct method calls</span><span class="sxs-lookup"><span data-stu-id="abb1c-141">Listen for direct method calls</span></span>

<span data-ttu-id="abb1c-142">The simulated device application connects to a device-specific endpoint on your IoT hub, sends simulated telemetry, and listens for direct method calls from your hub.</span><span class="sxs-lookup"><span data-stu-id="abb1c-142">The simulated device application connects to a device-specific endpoint on your IoT hub, sends simulated telemetry, and listens for direct method calls from your hub.</span></span> <span data-ttu-id="abb1c-143">In this quickstart, the direct method call from the hub tells the device to change the interval at which it sends telemetry.</span><span class="sxs-lookup"><span data-stu-id="abb1c-143">In this quickstart, the direct method call from the hub tells the device to change the interval at which it sends telemetry.</span></span> <span data-ttu-id="abb1c-144">The simulated device sends an acknowledgement back to your hub after it executes the direct method.</span><span class="sxs-lookup"><span data-stu-id="abb1c-144">The simulated device sends an acknowledgement back to your hub after it executes the direct method.</span></span>

1. <span data-ttu-id="abb1c-145">In a terminal window, navigate to the root folder of the sample Java project.</span><span class="sxs-lookup"><span data-stu-id="abb1c-145">In a terminal window, navigate to the root folder of the sample Java project.</span></span> <span data-ttu-id="abb1c-146">Then navigate to the **iot-hub\Quickstarts\simulated-device-2** folder.</span><span class="sxs-lookup"><span data-stu-id="abb1c-146">Then navigate to the **iot-hub\Quickstarts\simulated-device-2** folder.</span></span>

2. <span data-ttu-id="abb1c-147">Open the **src/main/java/com/microsoft/docs/iothub/samples/SimulatedDevice.java** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="abb1c-147">Open the **src/main/java/com/microsoft/docs/iothub/samples/SimulatedDevice.java** file in a text editor of your choice.</span></span>

    <span data-ttu-id="abb1c-148">Replace the value of the `connString` variable with the device connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="abb1c-148">Replace the value of the `connString` variable with the device connection string you made a note of previously.</span></span> <span data-ttu-id="abb1c-149">Then save your changes to **SimulatedDevice.java** file.</span><span class="sxs-lookup"><span data-stu-id="abb1c-149">Then save your changes to **SimulatedDevice.java** file.</span></span>

3. <span data-ttu-id="abb1c-150">In the terminal window, run the following commands to install the required libraries and build the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="abb1c-150">In the terminal window, run the following commands to install the required libraries and build the simulated device application:</span></span>

    ```cmd/sh
    mvn clean package
    ```

4. <span data-ttu-id="abb1c-151">In the terminal window, run the following commands to run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="abb1c-151">In the terminal window, run the following commands to run the simulated device application:</span></span>

    ```cmd/sh
    java -jar target/simulated-device-2-1.0.0-with-deps.jar
    ```

    <span data-ttu-id="abb1c-152">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="abb1c-152">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span></span>

    ![Run the simulated device](media/quickstart-control-device-java/SimulatedDevice-1.png)

## <a name="call-the-direct-method"></a><span data-ttu-id="abb1c-154">Call the direct method</span><span class="sxs-lookup"><span data-stu-id="abb1c-154">Call the direct method</span></span>

<span data-ttu-id="abb1c-155">The back-end application connects to a service-side endpoint on your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="abb1c-155">The back-end application connects to a service-side endpoint on your IoT Hub.</span></span> <span data-ttu-id="abb1c-156">The application makes direct method calls to a device through your IoT hub and listens for acknowledgements.</span><span class="sxs-lookup"><span data-stu-id="abb1c-156">The application makes direct method calls to a device through your IoT hub and listens for acknowledgements.</span></span> <span data-ttu-id="abb1c-157">An IoT Hub back-end application typically runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="abb1c-157">An IoT Hub back-end application typically runs in the cloud.</span></span>

1. <span data-ttu-id="abb1c-158">In another terminal window, navigate to the root folder of the sample Java project.</span><span class="sxs-lookup"><span data-stu-id="abb1c-158">In another terminal window, navigate to the root folder of the sample Java project.</span></span> <span data-ttu-id="abb1c-159">Then navigate to the **iot-hub\Quickstarts\back-end-application** folder.</span><span class="sxs-lookup"><span data-stu-id="abb1c-159">Then navigate to the **iot-hub\Quickstarts\back-end-application** folder.</span></span>

2. <span data-ttu-id="abb1c-160">Open the **src/main/java/com/microsoft/docs/iothub/samples/BackEndApplication.java** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="abb1c-160">Open the **src/main/java/com/microsoft/docs/iothub/samples/BackEndApplication.java** file in a text editor of your choice.</span></span>

    <span data-ttu-id="abb1c-161">Replace the value of the `iotHubConnectionString` variable with the service connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="abb1c-161">Replace the value of the `iotHubConnectionString` variable with the service connection string you made a note of previously.</span></span> <span data-ttu-id="abb1c-162">Then save your changes to the **BackEndApplication.java** file.</span><span class="sxs-lookup"><span data-stu-id="abb1c-162">Then save your changes to the **BackEndApplication.java** file.</span></span>

3. <span data-ttu-id="abb1c-163">In the terminal window, run the following commands to install the required libraries and build the back-end application:</span><span class="sxs-lookup"><span data-stu-id="abb1c-163">In the terminal window, run the following commands to install the required libraries and build the back-end application:</span></span>

    ```cmd/sh
    mvn clean package
    ```

4. <span data-ttu-id="abb1c-164">In the terminal window, run the following commands to run the back-end application:</span><span class="sxs-lookup"><span data-stu-id="abb1c-164">In the terminal window, run the following commands to run the back-end application:</span></span>

    ```cmd/sh
    java -jar target/back-end-application-1.0.0-with-deps.jar
    ```

    <span data-ttu-id="abb1c-165">The following screenshot shows the output as the application makes a direct method call to the device and receives an acknowledgement:</span><span class="sxs-lookup"><span data-stu-id="abb1c-165">The following screenshot shows the output as the application makes a direct method call to the device and receives an acknowledgement:</span></span>

    ![Run the back-end application](media/quickstart-control-device-java/BackEndApplication.png)

    <span data-ttu-id="abb1c-167">After you run the back-end application, you see a message in the console window running the simulated device, and the rate at which it sends messages changes:</span><span class="sxs-lookup"><span data-stu-id="abb1c-167">After you run the back-end application, you see a message in the console window running the simulated device, and the rate at which it sends messages changes:</span></span>

    ![Change in simulated client](media/quickstart-control-device-java/SimulatedDevice-2.png)

## <a name="clean-up-resources"></a><span data-ttu-id="abb1c-169">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="abb1c-169">Clean up resources</span></span>

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="abb1c-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="abb1c-170">Next steps</span></span>

<span data-ttu-id="abb1c-171">In this quickstart, you've called a direct method on a device from a back-end application, and responded to the direct method call in a simulated device application.</span><span class="sxs-lookup"><span data-stu-id="abb1c-171">In this quickstart, you've called a direct method on a device from a back-end application, and responded to the direct method call in a simulated device application.</span></span>

<span data-ttu-id="abb1c-172">To learn how to route device-to-cloud messages to different destinations in the cloud, continue to the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="abb1c-172">To learn how to route device-to-cloud messages to different destinations in the cloud, continue to the next tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abb1c-173">Tutorial: Route telemetry to different endpoints for processing</span><span class="sxs-lookup"><span data-stu-id="abb1c-173">Tutorial: Route telemetry to different endpoints for processing</span></span>](tutorial-routing.md)