---
title: Control a device from Azure IoT Hub quickstart (Python) | Microsoft Docs
description: In this quickstart, you run two sample Python applications. One application is a back-end application that can remotely control devices connected to your hub. The other application simulates a device connected to your hub that can be controlled remotely.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: quickstart
ms.custom: mvc
ms.date: 04/30/2018
ms.author: dobett
ms.openlocfilehash: c48faa70154f59bae35045b623d6533c241115bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864406"
---
# <a name="quickstart-control-a-device-connected-to-an-iot-hub-python"></a><span data-ttu-id="c66a3-105">Quickstart: Control a device connected to an IoT hub (Python)</span><span class="sxs-lookup"><span data-stu-id="c66a3-105">Quickstart: Control a device connected to an IoT hub (Python)</span></span>

[!INCLUDE [iot-hub-quickstarts-2-selector](../../includes/iot-hub-quickstarts-2-selector.md)]

<span data-ttu-id="c66a3-106">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud and manage your devices from the cloud.</span><span class="sxs-lookup"><span data-stu-id="c66a3-106">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud and manage your devices from the cloud.</span></span> <span data-ttu-id="c66a3-107">In this quickstart, you use a *direct method* to control a simulated device connected to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c66a3-107">In this quickstart, you use a *direct method* to control a simulated device connected to your IoT hub.</span></span> <span data-ttu-id="c66a3-108">You can use direct methods to remotely change the behavior of a device connected to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c66a3-108">You can use direct methods to remotely change the behavior of a device connected to your IoT hub.</span></span>

<span data-ttu-id="c66a3-109">The quickstart uses two pre-written Python applications:</span><span class="sxs-lookup"><span data-stu-id="c66a3-109">The quickstart uses two pre-written Python applications:</span></span>

* <span data-ttu-id="c66a3-110">A simulated device application that responds to direct methods called from a back-end application.</span><span class="sxs-lookup"><span data-stu-id="c66a3-110">A simulated device application that responds to direct methods called from a back-end application.</span></span> <span data-ttu-id="c66a3-111">To receive the direct method calls, this application connects to a device-specific endpoint on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c66a3-111">To receive the direct method calls, this application connects to a device-specific endpoint on your IoT hub.</span></span>
* <span data-ttu-id="c66a3-112">A back-end application that calls the direct methods on the simulated device.</span><span class="sxs-lookup"><span data-stu-id="c66a3-112">A back-end application that calls the direct methods on the simulated device.</span></span> <span data-ttu-id="c66a3-113">To call a direct method on a device, this application connects to service-side endpoint on your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c66a3-113">To call a direct method on a device, this application connects to service-side endpoint on your IoT hub.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c66a3-114">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="c66a3-114">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c66a3-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c66a3-115">Prerequisites</span></span>

<span data-ttu-id="c66a3-116">The two sample applications you run in this quickstart are written using Python.</span><span class="sxs-lookup"><span data-stu-id="c66a3-116">The two sample applications you run in this quickstart are written using Python.</span></span> <span data-ttu-id="c66a3-117">You need either Python 2.7.x or 3.5.x on your development machine.</span><span class="sxs-lookup"><span data-stu-id="c66a3-117">You need either Python 2.7.x or 3.5.x on your development machine.</span></span>

<span data-ttu-id="c66a3-118">You can download Python for multiple platforms from [Python.org](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c66a3-118">You can download Python for multiple platforms from [Python.org](https://www.python.org/downloads/).</span></span>

<span data-ttu-id="c66a3-119">You can verify the current version of Python on your development machine using one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="c66a3-119">You can verify the current version of Python on your development machine using one of the following commands:</span></span>

```python
python --version
```

```python
python3 --version
```

<span data-ttu-id="c66a3-120">If you haven't already done so, download the sample Python project from https://github.com/Azure-Samples/azure-iot-samples-python/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="c66a3-120">If you haven't already done so, download the sample Python project from https://github.com/Azure-Samples/azure-iot-samples-python/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="c66a3-121">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="c66a3-121">Create an IoT hub</span></span>

<span data-ttu-id="c66a3-122">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-python.md), you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="c66a3-122">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-python.md), you can skip this step.</span></span>

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]

## <a name="register-a-device"></a><span data-ttu-id="c66a3-123">Register a device</span><span class="sxs-lookup"><span data-stu-id="c66a3-123">Register a device</span></span>

<span data-ttu-id="c66a3-124">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-python.md), you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="c66a3-124">If you completed the previous [Quickstart: Send telemetry from a device to an IoT hub](quickstart-send-telemetry-python.md), you can skip this step.</span></span>

<span data-ttu-id="c66a3-125">A device must be registered with your IoT hub before it can connect.</span><span class="sxs-lookup"><span data-stu-id="c66a3-125">A device must be registered with your IoT hub before it can connect.</span></span> <span data-ttu-id="c66a3-126">In this quickstart, you use the Azure CLI to register a simulated device.</span><span class="sxs-lookup"><span data-stu-id="c66a3-126">In this quickstart, you use the Azure CLI to register a simulated device.</span></span>

1. <span data-ttu-id="c66a3-127">Add the IoT Hub CLI extension and create the device identity.</span><span class="sxs-lookup"><span data-stu-id="c66a3-127">Add the IoT Hub CLI extension and create the device identity.</span></span> <span data-ttu-id="c66a3-128">Replace `{YourIoTHubName}` with the name of your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="c66a3-128">Replace `{YourIoTHubName}` with the name of your IoT hub:</span></span>

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name {YourIoTHubName} --device-id MyPythonDevice
    ```

    <span data-ttu-id="c66a3-129">If you choose a different name for your device, update the device name in the sample applications before you run them.</span><span class="sxs-lookup"><span data-stu-id="c66a3-129">If you choose a different name for your device, update the device name in the sample applications before you run them.</span></span>

1. <span data-ttu-id="c66a3-130">Run the following command to get the _device connection string_ for the device you just registered:</span><span class="sxs-lookup"><span data-stu-id="c66a3-130">Run the following command to get the _device connection string_ for the device you just registered:</span></span>

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id MyPythonDevice --output table
    ```

    <span data-ttu-id="c66a3-131">Make a note of the device connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="c66a3-131">Make a note of the device connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="c66a3-132">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="c66a3-132">You use this value later in the quickstart.</span></span>

1. <span data-ttu-id="c66a3-133">You also need a _service connection string_ to enable the back-end application to connect to your IoT hub and retrieve the messages.</span><span class="sxs-lookup"><span data-stu-id="c66a3-133">You also need a _service connection string_ to enable the back-end application to connect to your IoT hub and retrieve the messages.</span></span> <span data-ttu-id="c66a3-134">The following command retrieves the service connection string for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="c66a3-134">The following command retrieves the service connection string for your IoT hub:</span></span>

    ```azurecli-interactive
    az iot hub show-connection-string --hub-name {YourIoTHubName} --output table
    ```

    <span data-ttu-id="c66a3-135">Make a note of the service connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="c66a3-135">Make a note of the service connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="c66a3-136">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="c66a3-136">You use this value later in the quickstart.</span></span> <span data-ttu-id="c66a3-137">The service connection string is different from the device connection string.</span><span class="sxs-lookup"><span data-stu-id="c66a3-137">The service connection string is different from the device connection string.</span></span>

## <a name="listen-for-direct-method-calls"></a><span data-ttu-id="c66a3-138">Listen for direct method calls</span><span class="sxs-lookup"><span data-stu-id="c66a3-138">Listen for direct method calls</span></span>

<span data-ttu-id="c66a3-139">The simulated device application connects to a device-specific endpoint on your IoT hub, sends simulated telemetry, and listens for direct method calls from your hub.</span><span class="sxs-lookup"><span data-stu-id="c66a3-139">The simulated device application connects to a device-specific endpoint on your IoT hub, sends simulated telemetry, and listens for direct method calls from your hub.</span></span> <span data-ttu-id="c66a3-140">In this quickstart, the direct method call from the hub tells the device to change the interval at which it sends telemetry.</span><span class="sxs-lookup"><span data-stu-id="c66a3-140">In this quickstart, the direct method call from the hub tells the device to change the interval at which it sends telemetry.</span></span> <span data-ttu-id="c66a3-141">The simulated device sends an acknowledgement back to your hub after it executes the direct method.</span><span class="sxs-lookup"><span data-stu-id="c66a3-141">The simulated device sends an acknowledgement back to your hub after it executes the direct method.</span></span>

1. <span data-ttu-id="c66a3-142">In a terminal window, navigate to the root folder of the sample Python project.</span><span class="sxs-lookup"><span data-stu-id="c66a3-142">In a terminal window, navigate to the root folder of the sample Python project.</span></span> <span data-ttu-id="c66a3-143">Then navigate to the **iot-hub\Quickstarts\simulated-device-2** folder.</span><span class="sxs-lookup"><span data-stu-id="c66a3-143">Then navigate to the **iot-hub\Quickstarts\simulated-device-2** folder.</span></span>

1. <span data-ttu-id="c66a3-144">Open the **SimulatedDevice.py** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="c66a3-144">Open the **SimulatedDevice.py** file in a text editor of your choice.</span></span>

    <span data-ttu-id="c66a3-145">Replace the value of the `CONNECTION_STRING` variable with the device connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="c66a3-145">Replace the value of the `CONNECTION_STRING` variable with the device connection string you made a note of previously.</span></span> <span data-ttu-id="c66a3-146">Then save your changes to **SimulatedDevice.py** file.</span><span class="sxs-lookup"><span data-stu-id="c66a3-146">Then save your changes to **SimulatedDevice.py** file.</span></span>

1. <span data-ttu-id="c66a3-147">In the terminal window, run the following commands to install the required libraries for the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="c66a3-147">In the terminal window, run the following commands to install the required libraries for the simulated device application:</span></span>

    ```cmd/sh
    pip install azure-iothub-device-client
    ```

1. <span data-ttu-id="c66a3-148">In the terminal window, run the following commands to run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="c66a3-148">In the terminal window, run the following commands to run the simulated device application:</span></span>

    ```cmd/sh
    python SimulatedDevice.py
    ```

    <span data-ttu-id="c66a3-149">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="c66a3-149">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span></span>

    ![Run the simulated device](media/quickstart-control-device-python/SimulatedDevice-1.png)

## <a name="call-the-direct-method"></a><span data-ttu-id="c66a3-151">Call the direct method</span><span class="sxs-lookup"><span data-stu-id="c66a3-151">Call the direct method</span></span>

<span data-ttu-id="c66a3-152">The back-end application connects to a service-side endpoint on your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c66a3-152">The back-end application connects to a service-side endpoint on your IoT Hub.</span></span> <span data-ttu-id="c66a3-153">The application makes direct method calls to a device through your IoT hub and listens for acknowledgements.</span><span class="sxs-lookup"><span data-stu-id="c66a3-153">The application makes direct method calls to a device through your IoT hub and listens for acknowledgements.</span></span> <span data-ttu-id="c66a3-154">An IoT Hub back-end application typically runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="c66a3-154">An IoT Hub back-end application typically runs in the cloud.</span></span>

1. <span data-ttu-id="c66a3-155">In another terminal window, navigate to the root folder of the sample Python project.</span><span class="sxs-lookup"><span data-stu-id="c66a3-155">In another terminal window, navigate to the root folder of the sample Python project.</span></span> <span data-ttu-id="c66a3-156">Then navigate to the **iot-hub\Quickstarts\back-end-application** folder.</span><span class="sxs-lookup"><span data-stu-id="c66a3-156">Then navigate to the **iot-hub\Quickstarts\back-end-application** folder.</span></span>

1. <span data-ttu-id="c66a3-157">Open the **BackEndApplication.py** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="c66a3-157">Open the **BackEndApplication.py** file in a text editor of your choice.</span></span>

    <span data-ttu-id="c66a3-158">Replace the value of the `CONNECTION_STRING` variable with the service connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="c66a3-158">Replace the value of the `CONNECTION_STRING` variable with the service connection string you made a note of previously.</span></span> <span data-ttu-id="c66a3-159">Then save your changes to the **BackEndApplication.py** file.</span><span class="sxs-lookup"><span data-stu-id="c66a3-159">Then save your changes to the **BackEndApplication.py** file.</span></span>

1. <span data-ttu-id="c66a3-160">In the terminal window, run the following commands to install the required libraries for the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="c66a3-160">In the terminal window, run the following commands to install the required libraries for the simulated device application:</span></span>

    ```cmd/sh
    pip install azure-iothub-service-client future
    ```

1. <span data-ttu-id="c66a3-161">In the terminal window, run the following commands to run the back-end application:</span><span class="sxs-lookup"><span data-stu-id="c66a3-161">In the terminal window, run the following commands to run the back-end application:</span></span>

    ```cmd/sh
    python BackEndApplication.py
    ```

    <span data-ttu-id="c66a3-162">The following screenshot shows the output as the application makes a direct method call to the device and receives an acknowledgement:</span><span class="sxs-lookup"><span data-stu-id="c66a3-162">The following screenshot shows the output as the application makes a direct method call to the device and receives an acknowledgement:</span></span>

    ![Run the back-end application](media/quickstart-control-device-python/BackEndApplication.png)

    <span data-ttu-id="c66a3-164">After you run the back-end application, you see a message in the console window running the simulated device, and the rate at which it sends messages changes:</span><span class="sxs-lookup"><span data-stu-id="c66a3-164">After you run the back-end application, you see a message in the console window running the simulated device, and the rate at which it sends messages changes:</span></span>

    ![Change in simulated client](media/quickstart-control-device-python/SimulatedDevice-2.png)

## <a name="clean-up-resources"></a><span data-ttu-id="c66a3-166">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="c66a3-166">Clean up resources</span></span>

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="c66a3-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="c66a3-167">Next steps</span></span>

<span data-ttu-id="c66a3-168">In this quickstart, you've called a direct method on a device from a back-end application, and responded to the direct method call in a simulated device application.</span><span class="sxs-lookup"><span data-stu-id="c66a3-168">In this quickstart, you've called a direct method on a device from a back-end application, and responded to the direct method call in a simulated device application.</span></span>

<span data-ttu-id="c66a3-169">To learn how to route device-to-cloud messages to different destinations in the cloud, continue to the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="c66a3-169">To learn how to route device-to-cloud messages to different destinations in the cloud, continue to the next tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c66a3-170">Tutorial: Route telemetry to different endpoints for processing</span><span class="sxs-lookup"><span data-stu-id="c66a3-170">Tutorial: Route telemetry to different endpoints for processing</span></span>](tutorial-routing.md)