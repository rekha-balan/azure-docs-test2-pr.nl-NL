---
title: Control a device from Azure IoT Hub quickstart (Node.js) | Microsoft Docs
description: In this quickstart, you run two sample Node.js applications. One application is a back-end application that can remotely control devices connected to your hub. The other application simulates a device connected to your hub that can be controlled remotely.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: nodejs
ms.topic: quickstart
ms.custom: mvc
ms.date: 06/19/2018
ms.author: dobett
ms.openlocfilehash: 8d771fb17019e39da93995d0244c8089ea4a08b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867781"
---
# <a name="quickstart-control-a-device-connected-to-an-iot-hub-nodejs"></a><span data-ttu-id="fc31c-105">Quickstart: Control a device connected to an IoT hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="fc31c-105">Quickstart: Control a device connected to an IoT hub (Node.js)</span></span>

[!INCLUDE [iot-hub-quickstarts-2-selector](../../includes/iot-hub-quickstarts-2-selector.md)]

<span data-ttu-id="fc31c-106">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud and manage your devices from the cloud.</span><span class="sxs-lookup"><span data-stu-id="fc31c-106">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud and manage your devices from the cloud.</span></span> <span data-ttu-id="fc31c-107">In this quickstart, you use a *direct method* to control a simulated device connected to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fc31c-107">In this quickstart, you use a *direct method* to control a simulated device connected to your IoT hub.</span></span> <span data-ttu-id="fc31c-108">You can use direct methods to remotely change the behavior of a device connected to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fc31c-108">You can use direct methods to remotely change the behavior of a device connected to your IoT hub.</span></span>

<span data-ttu-id="fc31c-109">The quickstart uses two pre-written Node.js applications:</span><span class="sxs-lookup"><span data-stu-id="fc31c-109">The quickstart uses two pre-written Node.js applications:</span></span>

* <span data-ttu-id="fc31c-110">A simulated device application that responds to direct methods called from a back-end application.</span><span class="sxs-lookup"><span data-stu-id="fc31c-110">A simulated device application that responds to direct methods called from a back-end application.</span></span> <span data-ttu-id="fc31c-111">To receive the direct method calls, this application connects to a device-specific endpoint on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fc31c-111">To receive the direct method calls, this application connects to a device-specific endpoint on your IoT hub.</span></span>
* <span data-ttu-id="fc31c-112">A back-end application that calls the direct methods on the simulated device.</span><span class="sxs-lookup"><span data-stu-id="fc31c-112">A back-end application that calls the direct methods on the simulated device.</span></span> <span data-ttu-id="fc31c-113">To call a direct method on a device, this application connects to service-side endpoint on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fc31c-113">To call a direct method on a device, this application connects to service-side endpoint on your IoT hub.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fc31c-114">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="fc31c-114">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc31c-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fc31c-115">Prerequisites</span></span>

<span data-ttu-id="fc31c-116">The two sample applications you run in this quickstart are written using Node.js.</span><span class="sxs-lookup"><span data-stu-id="fc31c-116">The two sample applications you run in this quickstart are written using Node.js.</span></span> <span data-ttu-id="fc31c-117">You need Node.js v4.x.x or later on your development machine.</span><span class="sxs-lookup"><span data-stu-id="fc31c-117">You need Node.js v4.x.x or later on your development machine.</span></span>

<span data-ttu-id="fc31c-118">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="fc31c-118">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span></span>

<span data-ttu-id="fc31c-119">You can verify the current version of Node.js on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="fc31c-119">You can verify the current version of Node.js on your development machine using the following command:</span></span>

```cmd/sh
node --version
```

<span data-ttu-id="fc31c-120">If you haven't already done so, download the sample Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="fc31c-120">If you haven't already done so, download the sample Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="fc31c-121">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="fc31c-121">Create an IoT hub</span></span>

<span data-ttu-id="fc31c-122">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-node.md), you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="fc31c-122">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-node.md), you can skip this step.</span></span>

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]

## <a name="register-a-device"></a><span data-ttu-id="fc31c-123">Register a device</span><span class="sxs-lookup"><span data-stu-id="fc31c-123">Register a device</span></span>

<span data-ttu-id="fc31c-124">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-node.md), you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="fc31c-124">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-node.md), you can skip this step.</span></span>

<span data-ttu-id="fc31c-125">A device must be registered with your IoT hub before it can connect.</span><span class="sxs-lookup"><span data-stu-id="fc31c-125">A device must be registered with your IoT hub before it can connect.</span></span> <span data-ttu-id="fc31c-126">In this quickstart, you use the Azure CLI to register a simulated device.</span><span class="sxs-lookup"><span data-stu-id="fc31c-126">In this quickstart, you use the Azure CLI to register a simulated device.</span></span>

1. <span data-ttu-id="fc31c-127">Add the IoT Hub CLI extension and create the device identity.</span><span class="sxs-lookup"><span data-stu-id="fc31c-127">Add the IoT Hub CLI extension and create the device identity.</span></span> <span data-ttu-id="fc31c-128">Replace `{YourIoTHubName}` with the name of your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="fc31c-128">Replace `{YourIoTHubName}` with the name of your IoT hub:</span></span>

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name {YourIoTHubName} --device-id MyNodeDevice
    ```

    <span data-ttu-id="fc31c-129">If you choose a different name for your device, update the device name in the sample applications before you run them.</span><span class="sxs-lookup"><span data-stu-id="fc31c-129">If you choose a different name for your device, update the device name in the sample applications before you run them.</span></span>

1. <span data-ttu-id="fc31c-130">Run the following command to get the _device connection string_ for the device you just registered:</span><span class="sxs-lookup"><span data-stu-id="fc31c-130">Run the following command to get the _device connection string_ for the device you just registered:</span></span>

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id MyNodeDevice --output table
    ```

    <span data-ttu-id="fc31c-131">Make a note of the device connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="fc31c-131">Make a note of the device connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="fc31c-132">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="fc31c-132">You use this value later in the quickstart.</span></span>

1. <span data-ttu-id="fc31c-133">You also need a _service connection string_ to enable the back-end application to connect to your IoT hub and retrieve the messages.</span><span class="sxs-lookup"><span data-stu-id="fc31c-133">You also need a _service connection string_ to enable the back-end application to connect to your IoT hub and retrieve the messages.</span></span> <span data-ttu-id="fc31c-134">The following command retrieves the service connection string for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="fc31c-134">The following command retrieves the service connection string for your IoT hub:</span></span>

    ```azurecli-interactive
    az iot hub show-connection-string --hub-name {YourIoTHubName} --output table
    ```

    <span data-ttu-id="fc31c-135">Make a note of the service connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="fc31c-135">Make a note of the service connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="fc31c-136">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="fc31c-136">You use this value later in the quickstart.</span></span> <span data-ttu-id="fc31c-137">The service connection string is different from the device connection string.</span><span class="sxs-lookup"><span data-stu-id="fc31c-137">The service connection string is different from the device connection string.</span></span>

## <a name="listen-for-direct-method-calls"></a><span data-ttu-id="fc31c-138">Listen for direct method calls</span><span class="sxs-lookup"><span data-stu-id="fc31c-138">Listen for direct method calls</span></span>

<span data-ttu-id="fc31c-139">The simulated device application connects to a device-specific endpoint on your IoT hub, sends simulated telemetry, and listens for direct method calls from your hub.</span><span class="sxs-lookup"><span data-stu-id="fc31c-139">The simulated device application connects to a device-specific endpoint on your IoT hub, sends simulated telemetry, and listens for direct method calls from your hub.</span></span> <span data-ttu-id="fc31c-140">In this quickstart, the direct method call from the hub tells the device to change the interval at which it sends telemetry.</span><span class="sxs-lookup"><span data-stu-id="fc31c-140">In this quickstart, the direct method call from the hub tells the device to change the interval at which it sends telemetry.</span></span> <span data-ttu-id="fc31c-141">The simulated device sends an acknowledgement back to your hub after it executes the direct method.</span><span class="sxs-lookup"><span data-stu-id="fc31c-141">The simulated device sends an acknowledgement back to your hub after it executes the direct method.</span></span>

1. <span data-ttu-id="fc31c-142">In a terminal window, navigate to the root folder of the sample Node.js project.</span><span class="sxs-lookup"><span data-stu-id="fc31c-142">In a terminal window, navigate to the root folder of the sample Node.js project.</span></span> <span data-ttu-id="fc31c-143">Then navigate to the **iot-hub\Quickstarts\simulated-device-2** folder.</span><span class="sxs-lookup"><span data-stu-id="fc31c-143">Then navigate to the **iot-hub\Quickstarts\simulated-device-2** folder.</span></span>

1. <span data-ttu-id="fc31c-144">Open the **SimulatedDevice.js** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="fc31c-144">Open the **SimulatedDevice.js** file in a text editor of your choice.</span></span>

    <span data-ttu-id="fc31c-145">Replace the value of the `connectionString` variable with the device connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="fc31c-145">Replace the value of the `connectionString` variable with the device connection string you made a note of previously.</span></span> <span data-ttu-id="fc31c-146">Then save your changes to **SimulatedDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="fc31c-146">Then save your changes to **SimulatedDevice.js** file.</span></span>

1. <span data-ttu-id="fc31c-147">In the terminal window, run the following commands to install the required libraries and run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="fc31c-147">In the terminal window, run the following commands to install the required libraries and run the simulated device application:</span></span>

    ```cmd/sh
    npm install
    node SimulatedDevice.js
    ```

    <span data-ttu-id="fc31c-148">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="fc31c-148">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span></span>

    ![Run the simulated device](media/quickstart-control-device-node/SimulatedDevice-1.png)

## <a name="call-the-direct-method"></a><span data-ttu-id="fc31c-150">Call the direct method</span><span class="sxs-lookup"><span data-stu-id="fc31c-150">Call the direct method</span></span>

<span data-ttu-id="fc31c-151">The back-end application connects to a service-side endpoint on your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fc31c-151">The back-end application connects to a service-side endpoint on your IoT Hub.</span></span> <span data-ttu-id="fc31c-152">The application makes direct method calls to a device through your IoT hub and listens for acknowledgements.</span><span class="sxs-lookup"><span data-stu-id="fc31c-152">The application makes direct method calls to a device through your IoT hub and listens for acknowledgements.</span></span> <span data-ttu-id="fc31c-153">An IoT Hub back-end application typically runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="fc31c-153">An IoT Hub back-end application typically runs in the cloud.</span></span>

1. <span data-ttu-id="fc31c-154">In another terminal window, navigate to the root folder of the sample Node.js project.</span><span class="sxs-lookup"><span data-stu-id="fc31c-154">In another terminal window, navigate to the root folder of the sample Node.js project.</span></span> <span data-ttu-id="fc31c-155">Then navigate to the **iot-hub\Quickstarts\back-end-application** folder.</span><span class="sxs-lookup"><span data-stu-id="fc31c-155">Then navigate to the **iot-hub\Quickstarts\back-end-application** folder.</span></span>

1. <span data-ttu-id="fc31c-156">Open the **BackEndApplication.js** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="fc31c-156">Open the **BackEndApplication.js** file in a text editor of your choice.</span></span>

    <span data-ttu-id="fc31c-157">Replace the value of the `connectionString` variable with the service connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="fc31c-157">Replace the value of the `connectionString` variable with the service connection string you made a note of previously.</span></span> <span data-ttu-id="fc31c-158">Then save your changes to the **BackEndApplication.js** file.</span><span class="sxs-lookup"><span data-stu-id="fc31c-158">Then save your changes to the **BackEndApplication.js** file.</span></span>

1. <span data-ttu-id="fc31c-159">In the terminal window, run the following commands to install the required libraries and run the back-end application:</span><span class="sxs-lookup"><span data-stu-id="fc31c-159">In the terminal window, run the following commands to install the required libraries and run the back-end application:</span></span>

    ```cmd/sh
    npm install
    node BackEndApplication.js
    ```

    <span data-ttu-id="fc31c-160">The following screenshot shows the output as the application makes a direct method call to the device and receives an acknowledgement:</span><span class="sxs-lookup"><span data-stu-id="fc31c-160">The following screenshot shows the output as the application makes a direct method call to the device and receives an acknowledgement:</span></span>

    ![Run the back-end application](media/quickstart-control-device-node/BackEndApplication.png)

    <span data-ttu-id="fc31c-162">After you run the back-end application, you see a message in the console window running the simulated device, and the rate at which it sends messages changes:</span><span class="sxs-lookup"><span data-stu-id="fc31c-162">After you run the back-end application, you see a message in the console window running the simulated device, and the rate at which it sends messages changes:</span></span>

    ![Change in simulated client](media/quickstart-control-device-node/SimulatedDevice-2.png)

## <a name="clean-up-resources"></a><span data-ttu-id="fc31c-164">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="fc31c-164">Clean up resources</span></span>

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]


## <a name="next-steps"></a><span data-ttu-id="fc31c-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc31c-165">Next steps</span></span>

<span data-ttu-id="fc31c-166">In this quickstart, you've called a direct method on a device from a back-end application, and responded to the direct method call in a simulated device application.</span><span class="sxs-lookup"><span data-stu-id="fc31c-166">In this quickstart, you've called a direct method on a device from a back-end application, and responded to the direct method call in a simulated device application.</span></span>

<span data-ttu-id="fc31c-167">To learn how to route device-to-cloud messages to different destinations in the cloud, continue to the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="fc31c-167">To learn how to route device-to-cloud messages to different destinations in the cloud, continue to the next tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc31c-168">Tutorial: Route telemetry to different endpoints for processing</span><span class="sxs-lookup"><span data-stu-id="fc31c-168">Tutorial: Route telemetry to different endpoints for processing</span></span>](tutorial-routing.md)