---
title: Send telemetry to Azure IoT Hub quickstart (Java) | Microsoft Docs
description: In this quickstart, you run two sample Java applications to send simulated telemetry to an IoT hub and to read telemetry from the IoT hub for processing in the cloud.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: java
ms.topic: quickstart
ms.custom: mvc
ms.date: 06/22/2018
ms.author: dobett
ms.openlocfilehash: 903c5ce4b914575dbd0a807efeec30c8b32fa9dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864688"
---
# <a name="quickstart-send-telemetry-from-a-device-to-an-iot-hub-and-read-the-telemetry-from-the-hub-with-a-back-end-application-java"></a><span data-ttu-id="8b69a-103">Quickstart: Send telemetry from a device to an IoT hub and read the telemetry from the hub with a back-end application (Java)</span><span class="sxs-lookup"><span data-stu-id="8b69a-103">Quickstart: Send telemetry from a device to an IoT hub and read the telemetry from the hub with a back-end application (Java)</span></span>

[!INCLUDE [iot-hub-quickstarts-1-selector](../../includes/iot-hub-quickstarts-1-selector.md)]

<span data-ttu-id="8b69a-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span><span class="sxs-lookup"><span data-stu-id="8b69a-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span></span> <span data-ttu-id="8b69a-105">In this quickstart, you send telemetry from a simulated device application, through IoT Hub, to a back-end application for processing.</span><span class="sxs-lookup"><span data-stu-id="8b69a-105">In this quickstart, you send telemetry from a simulated device application, through IoT Hub, to a back-end application for processing.</span></span>

<span data-ttu-id="8b69a-106">The quickstart uses two pre-written Java applications, one to send the telemetry and one to read the telemetry from the hub.</span><span class="sxs-lookup"><span data-stu-id="8b69a-106">The quickstart uses two pre-written Java applications, one to send the telemetry and one to read the telemetry from the hub.</span></span> <span data-ttu-id="8b69a-107">Before you run these two applications, you create an IoT hub and register a device with the hub.</span><span class="sxs-lookup"><span data-stu-id="8b69a-107">Before you run these two applications, you create an IoT hub and register a device with the hub.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8b69a-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="8b69a-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b69a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8b69a-109">Prerequisites</span></span>

<span data-ttu-id="8b69a-110">The two sample applications you run in this quickstart are written using Java.</span><span class="sxs-lookup"><span data-stu-id="8b69a-110">The two sample applications you run in this quickstart are written using Java.</span></span> <span data-ttu-id="8b69a-111">You need Java SE 8 or later on your development machine.</span><span class="sxs-lookup"><span data-stu-id="8b69a-111">You need Java SE 8 or later on your development machine.</span></span>

<span data-ttu-id="8b69a-112">You can download Java for multiple platforms from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="8b69a-112">You can download Java for multiple platforms from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

<span data-ttu-id="8b69a-113">You can verify the current version of Java on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="8b69a-113">You can verify the current version of Java on your development machine using the following command:</span></span>

```cmd/sh
java --version
```

<span data-ttu-id="8b69a-114">To build the samples, you need to install Maven 3.</span><span class="sxs-lookup"><span data-stu-id="8b69a-114">To build the samples, you need to install Maven 3.</span></span> <span data-ttu-id="8b69a-115">You can download Maven for multiple platforms from [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="8b69a-115">You can download Maven for multiple platforms from [Apache Maven](https://maven.apache.org/download.cgi).</span></span>

<span data-ttu-id="8b69a-116">You can verify the current version of Maven on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="8b69a-116">You can verify the current version of Maven on your development machine using the following command:</span></span>

```cmd/sh
mvn --version
```

<span data-ttu-id="8b69a-117">Download the sample Java project from https://github.com/Azure-Samples/azure-iot-samples-java/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="8b69a-117">Download the sample Java project from https://github.com/Azure-Samples/azure-iot-samples-java/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="8b69a-118">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="8b69a-118">Create an IoT hub</span></span>

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]

## <a name="register-a-device"></a><span data-ttu-id="8b69a-119">Register a device</span><span class="sxs-lookup"><span data-stu-id="8b69a-119">Register a device</span></span>

<span data-ttu-id="8b69a-120">A device must be registered with your IoT hub before it can connect.</span><span class="sxs-lookup"><span data-stu-id="8b69a-120">A device must be registered with your IoT hub before it can connect.</span></span> <span data-ttu-id="8b69a-121">In this quickstart, you use the Azure CLI to register a simulated device.</span><span class="sxs-lookup"><span data-stu-id="8b69a-121">In this quickstart, you use the Azure CLI to register a simulated device.</span></span>

1. <span data-ttu-id="8b69a-122">Add the IoT Hub CLI extension and create the device identity.</span><span class="sxs-lookup"><span data-stu-id="8b69a-122">Add the IoT Hub CLI extension and create the device identity.</span></span> <span data-ttu-id="8b69a-123">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="8b69a-123">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span></span>

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name {YourIoTHubName} --device-id MyJavaDevice
    ```

    <span data-ttu-id="8b69a-124">If you choose a different name for your device, update the device name in the sample applications before you run them.</span><span class="sxs-lookup"><span data-stu-id="8b69a-124">If you choose a different name for your device, update the device name in the sample applications before you run them.</span></span>

2. <span data-ttu-id="8b69a-125">Run the following command to get the _device connection string_ for the device you just registered:</span><span class="sxs-lookup"><span data-stu-id="8b69a-125">Run the following command to get the _device connection string_ for the device you just registered:</span></span>

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id MyJavaDevice --output table
    ```

    <span data-ttu-id="8b69a-126">Make a note of the device connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="8b69a-126">Make a note of the device connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="8b69a-127">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="8b69a-127">You use this value later in the quickstart.</span></span>

3. <span data-ttu-id="8b69a-128">You also need the _Event Hubs-compatible endpoint_, _Event Hubs-compatible path_, and _iothubowner primary key_ from your IoT hub to enable the back-end application to connect to your IoT hub and retrieve the messages.</span><span class="sxs-lookup"><span data-stu-id="8b69a-128">You also need the _Event Hubs-compatible endpoint_, _Event Hubs-compatible path_, and _iothubowner primary key_ from your IoT hub to enable the back-end application to connect to your IoT hub and retrieve the messages.</span></span> <span data-ttu-id="8b69a-129">The following commands retrieve these values for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="8b69a-129">The following commands retrieve these values for your IoT hub:</span></span>

    ```azurecli-interactive
    az iot hub show --query properties.eventHubEndpoints.events.endpoint --name {YourIoTHubName}

    az iot hub show --query properties.eventHubEndpoints.events.path --name {YourIoTHubName}

    az iot hub policy show --name iothubowner --query primaryKey --hub-name {your IoT Hub name}
    ```

    <span data-ttu-id="8b69a-130">Make a note of these three values, which you use later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="8b69a-130">Make a note of these three values, which you use later in the quickstart.</span></span>

## <a name="send-simulated-telemetry"></a><span data-ttu-id="8b69a-131">Send simulated telemetry</span><span class="sxs-lookup"><span data-stu-id="8b69a-131">Send simulated telemetry</span></span>

<span data-ttu-id="8b69a-132">The simulated device application connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span><span class="sxs-lookup"><span data-stu-id="8b69a-132">The simulated device application connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span></span>

1. <span data-ttu-id="8b69a-133">In a terminal window, navigate to the root folder of the sample Java project.</span><span class="sxs-lookup"><span data-stu-id="8b69a-133">In a terminal window, navigate to the root folder of the sample Java project.</span></span> <span data-ttu-id="8b69a-134">Then navigate to the **iot-hub\Quickstarts\simulated-device** folder.</span><span class="sxs-lookup"><span data-stu-id="8b69a-134">Then navigate to the **iot-hub\Quickstarts\simulated-device** folder.</span></span>

2. <span data-ttu-id="8b69a-135">Open the **src/main/java/com/microsoft/docs/iothub/samples/SimulatedDevice.java** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="8b69a-135">Open the **src/main/java/com/microsoft/docs/iothub/samples/SimulatedDevice.java** file in a text editor of your choice.</span></span>

    <span data-ttu-id="8b69a-136">Replace the value of the `connString` variable with the device connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="8b69a-136">Replace the value of the `connString` variable with the device connection string you made a note of previously.</span></span> <span data-ttu-id="8b69a-137">Then save your changes to **SimulatedDevice.java** file.</span><span class="sxs-lookup"><span data-stu-id="8b69a-137">Then save your changes to **SimulatedDevice.java** file.</span></span>

3. <span data-ttu-id="8b69a-138">In the terminal window, run the following commands to install the required libraries and build the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="8b69a-138">In the terminal window, run the following commands to install the required libraries and build the simulated device application:</span></span>

    ```cmd/sh
    mvn clean package
    ```

4. <span data-ttu-id="8b69a-139">In the terminal window, run the following commands to run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="8b69a-139">In the terminal window, run the following commands to run the simulated device application:</span></span>

    ```cmd/sh
    java -jar target/simulated-device-1.0.0-with-deps.jar
    ```

    <span data-ttu-id="8b69a-140">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="8b69a-140">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span></span>

    ![Run the simulated device](media/quickstart-send-telemetry-java/SimulatedDevice.png)

## <a name="read-the-telemetry-from-your-hub"></a><span data-ttu-id="8b69a-142">Read the telemetry from your hub</span><span class="sxs-lookup"><span data-stu-id="8b69a-142">Read the telemetry from your hub</span></span>

<span data-ttu-id="8b69a-143">The back-end application connects to the service-side **Events** endpoint on your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b69a-143">The back-end application connects to the service-side **Events** endpoint on your IoT Hub.</span></span> <span data-ttu-id="8b69a-144">The application receives the device-to-cloud messages sent from your simulated device.</span><span class="sxs-lookup"><span data-stu-id="8b69a-144">The application receives the device-to-cloud messages sent from your simulated device.</span></span> <span data-ttu-id="8b69a-145">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="8b69a-145">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span></span>

1. <span data-ttu-id="8b69a-146">In another terminal window, navigate to the root folder of the sample Java project.</span><span class="sxs-lookup"><span data-stu-id="8b69a-146">In another terminal window, navigate to the root folder of the sample Java project.</span></span> <span data-ttu-id="8b69a-147">Then navigate to the **iot-hub\Quickstarts\read-d2c-messages** folder.</span><span class="sxs-lookup"><span data-stu-id="8b69a-147">Then navigate to the **iot-hub\Quickstarts\read-d2c-messages** folder.</span></span>

2. <span data-ttu-id="8b69a-148">Open the **src/main/java/com/microsoft/docs/iothub/samples/ReadDeviceToCloudMessages.java** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="8b69a-148">Open the **src/main/java/com/microsoft/docs/iothub/samples/ReadDeviceToCloudMessages.java** file in a text editor of your choice.</span></span> <span data-ttu-id="8b69a-149">Update the following variables and save your changes to the file.</span><span class="sxs-lookup"><span data-stu-id="8b69a-149">Update the following variables and save your changes to the file.</span></span>

    | <span data-ttu-id="8b69a-150">Variable</span><span class="sxs-lookup"><span data-stu-id="8b69a-150">Variable</span></span> | <span data-ttu-id="8b69a-151">Value</span><span class="sxs-lookup"><span data-stu-id="8b69a-151">Value</span></span> |
    | -------- | ----------- |
    | `eventHubsCompatibleEndpoint` | <span data-ttu-id="8b69a-152">Replace the value of the variable with the Event Hubs-compatible endpoint you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="8b69a-152">Replace the value of the variable with the Event Hubs-compatible endpoint you made a note of previously.</span></span> |
    | `eventHubsCompatiblePath`     | <span data-ttu-id="8b69a-153">Replace the value of the variable with the Event Hubs-compatible path you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="8b69a-153">Replace the value of the variable with the Event Hubs-compatible path you made a note of previously.</span></span> |
    | `iotHubSasKey`                | <span data-ttu-id="8b69a-154">Replace the value of the variable with the iothubowner primary key you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="8b69a-154">Replace the value of the variable with the iothubowner primary key you made a note of previously.</span></span> |


3. <span data-ttu-id="8b69a-155">In the terminal window, run the following commands to install the required libraries and build the back-end application:</span><span class="sxs-lookup"><span data-stu-id="8b69a-155">In the terminal window, run the following commands to install the required libraries and build the back-end application:</span></span>

    ```cmd/sh
    mvn clean package
    ```

4. <span data-ttu-id="8b69a-156">In the terminal window, run the following commands to run the back-end application:</span><span class="sxs-lookup"><span data-stu-id="8b69a-156">In the terminal window, run the following commands to run the back-end application:</span></span>

    ```cmd/sh
    java -jar target/read-d2c-messages-1.0.0-with-deps.jar
    ```

    <span data-ttu-id="8b69a-157">The following screenshot shows the output as the back-end application receives telemetry sent by the simulated device to the hub:</span><span class="sxs-lookup"><span data-stu-id="8b69a-157">The following screenshot shows the output as the back-end application receives telemetry sent by the simulated device to the hub:</span></span>

    ![Run the back-end application](media/quickstart-send-telemetry-java/ReadDeviceToCloud.png)

## <a name="clean-up-resources"></a><span data-ttu-id="8b69a-159">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="8b69a-159">Clean up resources</span></span>

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="8b69a-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b69a-160">Next steps</span></span>

<span data-ttu-id="8b69a-161">In this quickstart, you've setup an IoT hub, registered a device, sent simulated telemetry to the hub using a Java application, and read the telemetry from the hub using a simple back-end application.</span><span class="sxs-lookup"><span data-stu-id="8b69a-161">In this quickstart, you've setup an IoT hub, registered a device, sent simulated telemetry to the hub using a Java application, and read the telemetry from the hub using a simple back-end application.</span></span>

<span data-ttu-id="8b69a-162">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span><span class="sxs-lookup"><span data-stu-id="8b69a-162">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8b69a-163">Quickstart: Control a device connected to an IoT hub</span><span class="sxs-lookup"><span data-stu-id="8b69a-163">Quickstart: Control a device connected to an IoT hub</span></span>](quickstart-control-device-java.md)