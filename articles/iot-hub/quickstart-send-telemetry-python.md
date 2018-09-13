---
title: Send telemetry to Azure IoT Hub quickstart (Python) | Microsoft Docs
description: In this quickstart, you run a sample Python application to send simulated telemetry to an IoT hub and use a utility to read telemetry from the IoT hub.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: quickstart
ms.custom: mvc
ms.date: 09/07/2018
ms.author: dobett
ms.openlocfilehash: ca2f054016be0620d979f55e1bb26d118ab853f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867343"
---
# <a name="quickstart-send-telemetry-from-a-device-to-an-iot-hub-and-read-the-telemetry-from-the-hub-with-a-back-end-application-python"></a><span data-ttu-id="09b2b-103">Quickstart: Send telemetry from a device to an IoT hub and read the telemetry from the hub with a back-end application (Python)</span><span class="sxs-lookup"><span data-stu-id="09b2b-103">Quickstart: Send telemetry from a device to an IoT hub and read the telemetry from the hub with a back-end application (Python)</span></span>

[!INCLUDE [iot-hub-quickstarts-1-selector](../../includes/iot-hub-quickstarts-1-selector.md)]

<span data-ttu-id="09b2b-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span><span class="sxs-lookup"><span data-stu-id="09b2b-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span></span> <span data-ttu-id="09b2b-105">In this quickstart, you send telemetry from a simulated device application, through IoT Hub, to a back-end application for processing.</span><span class="sxs-lookup"><span data-stu-id="09b2b-105">In this quickstart, you send telemetry from a simulated device application, through IoT Hub, to a back-end application for processing.</span></span>

<span data-ttu-id="09b2b-106">The quickstart uses a pre-written Python application to send the telemetry and a CLI utility to read the telemetry from the hub.</span><span class="sxs-lookup"><span data-stu-id="09b2b-106">The quickstart uses a pre-written Python application to send the telemetry and a CLI utility to read the telemetry from the hub.</span></span> <span data-ttu-id="09b2b-107">Before you run these two applications, you create an IoT hub and register a device with the hub.</span><span class="sxs-lookup"><span data-stu-id="09b2b-107">Before you run these two applications, you create an IoT hub and register a device with the hub.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="09b2b-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="09b2b-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09b2b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="09b2b-109">Prerequisites</span></span>

<span data-ttu-id="09b2b-110">The two sample applications you run in this quickstart are written using Python.</span><span class="sxs-lookup"><span data-stu-id="09b2b-110">The two sample applications you run in this quickstart are written using Python.</span></span> <span data-ttu-id="09b2b-111">You need either Python 2.7.x or 3.5.x on your development machine.</span><span class="sxs-lookup"><span data-stu-id="09b2b-111">You need either Python 2.7.x or 3.5.x on your development machine.</span></span>

<span data-ttu-id="09b2b-112">You can download Python for multiple platforms from [Python.org](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="09b2b-112">You can download Python for multiple platforms from [Python.org](https://www.python.org/downloads/).</span></span>

<span data-ttu-id="09b2b-113">You can verify the current version of Python on your development machine using one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="09b2b-113">You can verify the current version of Python on your development machine using one of the following commands:</span></span>

```python
python --version
```

```python
python3 --version
```

<span data-ttu-id="09b2b-114">Download the sample Python project from https://github.com/Azure-Samples/azure-iot-samples-python/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="09b2b-114">Download the sample Python project from https://github.com/Azure-Samples/azure-iot-samples-python/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="09b2b-115">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="09b2b-115">Create an IoT hub</span></span>

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]

## <a name="register-a-device"></a><span data-ttu-id="09b2b-116">Register a device</span><span class="sxs-lookup"><span data-stu-id="09b2b-116">Register a device</span></span>

<span data-ttu-id="09b2b-117">A device must be registered with your IoT hub before it can connect.</span><span class="sxs-lookup"><span data-stu-id="09b2b-117">A device must be registered with your IoT hub before it can connect.</span></span> <span data-ttu-id="09b2b-118">In this quickstart, you use the Azure CLI to register a simulated device.</span><span class="sxs-lookup"><span data-stu-id="09b2b-118">In this quickstart, you use the Azure CLI to register a simulated device.</span></span>

1. <span data-ttu-id="09b2b-119">Add the IoT Hub CLI extension and create the device identity.</span><span class="sxs-lookup"><span data-stu-id="09b2b-119">Add the IoT Hub CLI extension and create the device identity.</span></span> <span data-ttu-id="09b2b-120">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="09b2b-120">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span></span>

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name {YourIoTHubName} --device-id MyPythonDevice
    ```

    <span data-ttu-id="09b2b-121">If you choose a different name for your device, update the device name in the sample application before you run it.</span><span class="sxs-lookup"><span data-stu-id="09b2b-121">If you choose a different name for your device, update the device name in the sample application before you run it.</span></span>

1. <span data-ttu-id="09b2b-122">Run the following command to get the _device connection string_ for the device you just registered:</span><span class="sxs-lookup"><span data-stu-id="09b2b-122">Run the following command to get the _device connection string_ for the device you just registered:</span></span>

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id MyPythonDevice --output table
    ```

    <span data-ttu-id="09b2b-123">Make a note of the device connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="09b2b-123">Make a note of the device connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="09b2b-124">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="09b2b-124">You use this value later in the quickstart.</span></span>

## <a name="send-simulated-telemetry"></a><span data-ttu-id="09b2b-125">Send simulated telemetry</span><span class="sxs-lookup"><span data-stu-id="09b2b-125">Send simulated telemetry</span></span>

<span data-ttu-id="09b2b-126">The simulated device application connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span><span class="sxs-lookup"><span data-stu-id="09b2b-126">The simulated device application connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span></span>

1. <span data-ttu-id="09b2b-127">In a terminal window, navigate to the root folder of the sample Python project.</span><span class="sxs-lookup"><span data-stu-id="09b2b-127">In a terminal window, navigate to the root folder of the sample Python project.</span></span> <span data-ttu-id="09b2b-128">Then navigate to the **iot-hub\Quickstarts\simulated-device** folder.</span><span class="sxs-lookup"><span data-stu-id="09b2b-128">Then navigate to the **iot-hub\Quickstarts\simulated-device** folder.</span></span>

1. <span data-ttu-id="09b2b-129">Open the **SimulatedDevice.py** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="09b2b-129">Open the **SimulatedDevice.py** file in a text editor of your choice.</span></span>

    <span data-ttu-id="09b2b-130">Replace the value of the `CONNECTION_STRING` variable with the device connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="09b2b-130">Replace the value of the `CONNECTION_STRING` variable with the device connection string you made a note of previously.</span></span> <span data-ttu-id="09b2b-131">Then save your changes to **SimulatedDevice.py** file.</span><span class="sxs-lookup"><span data-stu-id="09b2b-131">Then save your changes to **SimulatedDevice.py** file.</span></span>

1. <span data-ttu-id="09b2b-132">In the terminal window, run the following commands to install the required libraries for the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="09b2b-132">In the terminal window, run the following commands to install the required libraries for the simulated device application:</span></span>

    ```cmd/sh
    pip install azure-iothub-device-client
    ```

1. <span data-ttu-id="09b2b-133">In the terminal window, run the following commands to run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="09b2b-133">In the terminal window, run the following commands to run the simulated device application:</span></span>

    ```cmd/sh
    python SimulatedDevice.py
    ```

    <span data-ttu-id="09b2b-134">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="09b2b-134">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span></span>

    ![Run the simulated device](media/quickstart-send-telemetry-python/SimulatedDevice.png)

## <a name="read-the-telemetry-from-your-hub"></a><span data-ttu-id="09b2b-136">Read the telemetry from your hub</span><span class="sxs-lookup"><span data-stu-id="09b2b-136">Read the telemetry from your hub</span></span>

<span data-ttu-id="09b2b-137">The IoT Hub CLI extension can connect to the service-side **Events** endpoint on your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09b2b-137">The IoT Hub CLI extension can connect to the service-side **Events** endpoint on your IoT Hub.</span></span> <span data-ttu-id="09b2b-138">The extension receives the device-to-cloud messages sent from your simulated device.</span><span class="sxs-lookup"><span data-stu-id="09b2b-138">The extension receives the device-to-cloud messages sent from your simulated device.</span></span> <span data-ttu-id="09b2b-139">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="09b2b-139">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span></span>

<span data-ttu-id="09b2b-140">Run the following Azure CLI commands, replacing `{YourIoTHubName}` with the name of your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="09b2b-140">Run the following Azure CLI commands, replacing `{YourIoTHubName}` with the name of your IoT hub:</span></span>

```azurecli-interactive
az iot hub monitor-events --device-id MyPythonDevice --hub-name {YourIoTHubName}
```

<span data-ttu-id="09b2b-141">The following screenshot shows the output as the extension receives telemetry sent by the simulated device to the hub:</span><span class="sxs-lookup"><span data-stu-id="09b2b-141">The following screenshot shows the output as the extension receives telemetry sent by the simulated device to the hub:</span></span>

![Run the back-end application](media/quickstart-send-telemetry-python/ReadDeviceToCloud.png)

## <a name="clean-up-resources"></a><span data-ttu-id="09b2b-143">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="09b2b-143">Clean up resources</span></span>

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="09b2b-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="09b2b-144">Next steps</span></span>

<span data-ttu-id="09b2b-145">In this quickstart, you've setup an IoT hub, registered a device, sent simulated telemetry to the hub using a Python application, and read the telemetry from the hub using a simple back-end application.</span><span class="sxs-lookup"><span data-stu-id="09b2b-145">In this quickstart, you've setup an IoT hub, registered a device, sent simulated telemetry to the hub using a Python application, and read the telemetry from the hub using a simple back-end application.</span></span>

<span data-ttu-id="09b2b-146">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span><span class="sxs-lookup"><span data-stu-id="09b2b-146">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09b2b-147">Quickstart: Control a device connected to an IoT hub</span><span class="sxs-lookup"><span data-stu-id="09b2b-147">Quickstart: Control a device connected to an IoT hub</span></span>](quickstart-control-device-python.md)