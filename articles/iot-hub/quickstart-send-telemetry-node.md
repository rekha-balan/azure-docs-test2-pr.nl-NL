---
title: Send telemetry to Azure IoT Hub quickstart (Node.js) | Microsoft Docs
description: In this quickstart, you run two sample Node.js applications to send simulated telemetry to an IoT hub and to read telemetry from the IoT hub for processing in the cloud.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: node
ms.topic: quickstart
ms.custom: mvc
ms.date: 06/19/2018
ms.author: dobett
ms.openlocfilehash: dc255a36e2347aac204f7bd32fe3e9cf25d54b19
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857109"
---
# <a name="quickstart-send-telemetry-from-a-device-to-an-iot-hub-and-read-the-telemetry-from-the-hub-with-a-back-end-application-nodejs"></a><span data-ttu-id="766cb-103">Quickstart: Send telemetry from a device to an IoT hub and read the telemetry from the hub with a back-end application (Node.js)</span><span class="sxs-lookup"><span data-stu-id="766cb-103">Quickstart: Send telemetry from a device to an IoT hub and read the telemetry from the hub with a back-end application (Node.js)</span></span>

[!INCLUDE [iot-hub-quickstarts-1-selector](../../includes/iot-hub-quickstarts-1-selector.md)]

<span data-ttu-id="766cb-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span><span class="sxs-lookup"><span data-stu-id="766cb-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span></span> <span data-ttu-id="766cb-105">In this quickstart, you send telemetry from a simulated device application, through IoT Hub, to a back-end application for processing.</span><span class="sxs-lookup"><span data-stu-id="766cb-105">In this quickstart, you send telemetry from a simulated device application, through IoT Hub, to a back-end application for processing.</span></span>

<span data-ttu-id="766cb-106">The quickstart uses two pre-written Node.js applications, one to send the telemetry and one to read the telemetry from the hub.</span><span class="sxs-lookup"><span data-stu-id="766cb-106">The quickstart uses two pre-written Node.js applications, one to send the telemetry and one to read the telemetry from the hub.</span></span> <span data-ttu-id="766cb-107">Before you run these two applications, you create an IoT hub and register a device with the hub.</span><span class="sxs-lookup"><span data-stu-id="766cb-107">Before you run these two applications, you create an IoT hub and register a device with the hub.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="766cb-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="766cb-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="766cb-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="766cb-109">Prerequisites</span></span>

<span data-ttu-id="766cb-110">The two sample applications you run in this quickstart are written using Node.js.</span><span class="sxs-lookup"><span data-stu-id="766cb-110">The two sample applications you run in this quickstart are written using Node.js.</span></span> <span data-ttu-id="766cb-111">You need Node.js v4.x.x or later on your development machine.</span><span class="sxs-lookup"><span data-stu-id="766cb-111">You need Node.js v4.x.x or later on your development machine.</span></span>

<span data-ttu-id="766cb-112">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="766cb-112">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span></span>

<span data-ttu-id="766cb-113">You can verify the current version of Node.js on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="766cb-113">You can verify the current version of Node.js on your development machine using the following command:</span></span>

```cmd/sh
node --version
```

<span data-ttu-id="766cb-114">Download the sample Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="766cb-114">Download the sample Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="766cb-115">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="766cb-115">Create an IoT hub</span></span>

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]

## <a name="register-a-device"></a><span data-ttu-id="766cb-116">Register a device</span><span class="sxs-lookup"><span data-stu-id="766cb-116">Register a device</span></span>

<span data-ttu-id="766cb-117">A device must be registered with your IoT hub before it can connect.</span><span class="sxs-lookup"><span data-stu-id="766cb-117">A device must be registered with your IoT hub before it can connect.</span></span> <span data-ttu-id="766cb-118">In this quickstart, you use the Azure CLI to register a simulated device.</span><span class="sxs-lookup"><span data-stu-id="766cb-118">In this quickstart, you use the Azure CLI to register a simulated device.</span></span>

1. <span data-ttu-id="766cb-119">Add the IoT Hub CLI extension and create the device identity.</span><span class="sxs-lookup"><span data-stu-id="766cb-119">Add the IoT Hub CLI extension and create the device identity.</span></span> <span data-ttu-id="766cb-120">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="766cb-120">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span></span>

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name {YourIoTHubName} --device-id MyNodeDevice
    ```

    <span data-ttu-id="766cb-121">If you choose a different name for your device, update the device name in the sample applications before you run them.</span><span class="sxs-lookup"><span data-stu-id="766cb-121">If you choose a different name for your device, update the device name in the sample applications before you run them.</span></span>

1. <span data-ttu-id="766cb-122">Run the following command to get the _device connection string_ for the device you just registered:</span><span class="sxs-lookup"><span data-stu-id="766cb-122">Run the following command to get the _device connection string_ for the device you just registered:</span></span>

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id MyNodeDevice --output table
    ```

    <span data-ttu-id="766cb-123">Make a note of the device connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="766cb-123">Make a note of the device connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="766cb-124">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="766cb-124">You use this value later in the quickstart.</span></span>

1. <span data-ttu-id="766cb-125">You also need a _service connection string_ to enable the back-end application to connect to your IoT hub and retrieve the messages.</span><span class="sxs-lookup"><span data-stu-id="766cb-125">You also need a _service connection string_ to enable the back-end application to connect to your IoT hub and retrieve the messages.</span></span> <span data-ttu-id="766cb-126">The following command retrieves the service connection string for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="766cb-126">The following command retrieves the service connection string for your IoT hub:</span></span>

    ```azurecli-interactive
    az iot hub show-connection-string --name {YourIoTHubName} --output table
    ```

    <span data-ttu-id="766cb-127">Make a note of the service connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="766cb-127">Make a note of the service connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="766cb-128">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="766cb-128">You use this value later in the quickstart.</span></span> <span data-ttu-id="766cb-129">The service connection string is different from the device connection string.</span><span class="sxs-lookup"><span data-stu-id="766cb-129">The service connection string is different from the device connection string.</span></span>

## <a name="send-simulated-telemetry"></a><span data-ttu-id="766cb-130">Send simulated telemetry</span><span class="sxs-lookup"><span data-stu-id="766cb-130">Send simulated telemetry</span></span>

<span data-ttu-id="766cb-131">The simulated device application connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span><span class="sxs-lookup"><span data-stu-id="766cb-131">The simulated device application connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span></span>

1. <span data-ttu-id="766cb-132">In a terminal window, navigate to the root folder of the sample Node.js project.</span><span class="sxs-lookup"><span data-stu-id="766cb-132">In a terminal window, navigate to the root folder of the sample Node.js project.</span></span> <span data-ttu-id="766cb-133">Then navigate to the **iot-hub\Quickstarts\simulated-device** folder.</span><span class="sxs-lookup"><span data-stu-id="766cb-133">Then navigate to the **iot-hub\Quickstarts\simulated-device** folder.</span></span>

1. <span data-ttu-id="766cb-134">Open the **SimulatedDevice.js** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="766cb-134">Open the **SimulatedDevice.js** file in a text editor of your choice.</span></span>

    <span data-ttu-id="766cb-135">Replace the value of the `connectionString` variable with the device connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="766cb-135">Replace the value of the `connectionString` variable with the device connection string you made a note of previously.</span></span> <span data-ttu-id="766cb-136">Then save your changes to **SimulatedDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="766cb-136">Then save your changes to **SimulatedDevice.js** file.</span></span>

1. <span data-ttu-id="766cb-137">In the terminal window, run the following commands to install the required libraries and run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="766cb-137">In the terminal window, run the following commands to install the required libraries and run the simulated device application:</span></span>

    ```cmd/sh
    npm install
    node SimulatedDevice.js
    ```

    <span data-ttu-id="766cb-138">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="766cb-138">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span></span>

    ![Run the simulated device](media/quickstart-send-telemetry-node/SimulatedDevice.png)

## <a name="read-the-telemetry-from-your-hub"></a><span data-ttu-id="766cb-140">Read the telemetry from your hub</span><span class="sxs-lookup"><span data-stu-id="766cb-140">Read the telemetry from your hub</span></span>

<span data-ttu-id="766cb-141">The back-end application connects to the service-side **Events** endpoint on your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="766cb-141">The back-end application connects to the service-side **Events** endpoint on your IoT Hub.</span></span> <span data-ttu-id="766cb-142">The application receives the device-to-cloud messages sent from your simulated device.</span><span class="sxs-lookup"><span data-stu-id="766cb-142">The application receives the device-to-cloud messages sent from your simulated device.</span></span> <span data-ttu-id="766cb-143">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="766cb-143">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span></span>

1. <span data-ttu-id="766cb-144">In another terminal window, navigate to the root folder of the sample Node.js project.</span><span class="sxs-lookup"><span data-stu-id="766cb-144">In another terminal window, navigate to the root folder of the sample Node.js project.</span></span> <span data-ttu-id="766cb-145">Then navigate to the **read-d2c-messages** folder.</span><span class="sxs-lookup"><span data-stu-id="766cb-145">Then navigate to the **read-d2c-messages** folder.</span></span>

1. <span data-ttu-id="766cb-146">Open the **iot-hub\Quickstarts\ReadDeviceToCloudMessages.js** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="766cb-146">Open the **iot-hub\Quickstarts\ReadDeviceToCloudMessages.js** file in a text editor of your choice.</span></span>

    <span data-ttu-id="766cb-147">Replace the value of the `connectionString` variable with the service connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="766cb-147">Replace the value of the `connectionString` variable with the service connection string you made a note of previously.</span></span> <span data-ttu-id="766cb-148">Then save your changes to the **ReadDeviceToCloudMessages.js** file.</span><span class="sxs-lookup"><span data-stu-id="766cb-148">Then save your changes to the **ReadDeviceToCloudMessages.js** file.</span></span>

1. <span data-ttu-id="766cb-149">In the terminal window, run the following commands to install the required libraries and run the back-end application:</span><span class="sxs-lookup"><span data-stu-id="766cb-149">In the terminal window, run the following commands to install the required libraries and run the back-end application:</span></span>

    ```cmd/sh
    npm install
    node ReadDeviceToCloudMessages.js
    ```

    <span data-ttu-id="766cb-150">The following screenshot shows the output as the back-end application receives telemetry sent by the simulated device to the hub:</span><span class="sxs-lookup"><span data-stu-id="766cb-150">The following screenshot shows the output as the back-end application receives telemetry sent by the simulated device to the hub:</span></span>

    ![Run the back-end application](media/quickstart-send-telemetry-node/ReadDeviceToCloud.png)

## <a name="clean-up-resources"></a><span data-ttu-id="766cb-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="766cb-152">Clean up resources</span></span>

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="766cb-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="766cb-153">Next steps</span></span>

<span data-ttu-id="766cb-154">In this quickstart, you've setup an IoT hub, registered a device, sent simulated telemetry to the hub using a Node.js application, and read the telemetry from the hub using a simple back-end application.</span><span class="sxs-lookup"><span data-stu-id="766cb-154">In this quickstart, you've setup an IoT hub, registered a device, sent simulated telemetry to the hub using a Node.js application, and read the telemetry from the hub using a simple back-end application.</span></span>

<span data-ttu-id="766cb-155">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span><span class="sxs-lookup"><span data-stu-id="766cb-155">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="766cb-156">Quickstart: Control a device connected to an IoT hub</span><span class="sxs-lookup"><span data-stu-id="766cb-156">Quickstart: Control a device connected to an IoT hub</span></span>](quickstart-control-device-node.md)
