---
title: Send telemetry to Azure IoT Hub quickstart (C#) | Microsoft Docs
description: In this quickstart, you run two sample C# applications to send simulated telemetry to an IoT hub and to read telemetry from the IoT hub for processing in the cloud.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: csharp
ms.topic: quickstart
ms.custom: mvc
ms.date: 06/20/2018
ms.author: dobett
ms.openlocfilehash: 34f933474337d3cddce752b79dc0d3fdb4c39c0c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867198"
---
# <a name="quickstart-send-telemetry-from-a-device-to-an-iot-hub-and-read-the-telemetry-from-the-hub-with-a-back-end-application-c"></a><span data-ttu-id="a01cd-103">Quickstart: Send telemetry from a device to an IoT hub and read the telemetry from the hub with a back-end application (C#)</span><span class="sxs-lookup"><span data-stu-id="a01cd-103">Quickstart: Send telemetry from a device to an IoT hub and read the telemetry from the hub with a back-end application (C#)</span></span>

[!INCLUDE [iot-hub-quickstarts-1-selector](../../includes/iot-hub-quickstarts-1-selector.md)]

<span data-ttu-id="a01cd-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span><span class="sxs-lookup"><span data-stu-id="a01cd-104">IoT Hub is an Azure service that enables you to ingest high volumes of telemetry from your IoT devices into the cloud for storage or processing.</span></span> <span data-ttu-id="a01cd-105">In this quickstart, you send telemetry from a simulated device application, through IoT Hub, to a back-end application for processing.</span><span class="sxs-lookup"><span data-stu-id="a01cd-105">In this quickstart, you send telemetry from a simulated device application, through IoT Hub, to a back-end application for processing.</span></span>

<span data-ttu-id="a01cd-106">The quickstart uses two pre-written C# applications, one to send the telemetry and one to read the telemetry from the hub.</span><span class="sxs-lookup"><span data-stu-id="a01cd-106">The quickstart uses two pre-written C# applications, one to send the telemetry and one to read the telemetry from the hub.</span></span> <span data-ttu-id="a01cd-107">Before you run these two applications, you create an IoT hub and register a device with the hub.</span><span class="sxs-lookup"><span data-stu-id="a01cd-107">Before you run these two applications, you create an IoT hub and register a device with the hub.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a01cd-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="a01cd-108">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a01cd-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a01cd-109">Prerequisites</span></span>

<span data-ttu-id="a01cd-110">The two sample applications you run in this quickstart are written using C#.</span><span class="sxs-lookup"><span data-stu-id="a01cd-110">The two sample applications you run in this quickstart are written using C#.</span></span> <span data-ttu-id="a01cd-111">You need the .NET Core SDK 2.1.0 or greater on your development machine.</span><span class="sxs-lookup"><span data-stu-id="a01cd-111">You need the .NET Core SDK 2.1.0 or greater on your development machine.</span></span>

<span data-ttu-id="a01cd-112">You can download the .NET Core SDK for multiple platforms from [.NET](https://www.microsoft.com/net/download/all).</span><span class="sxs-lookup"><span data-stu-id="a01cd-112">You can download the .NET Core SDK for multiple platforms from [.NET](https://www.microsoft.com/net/download/all).</span></span>

<span data-ttu-id="a01cd-113">You can verify the current version of C# on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="a01cd-113">You can verify the current version of C# on your development machine using the following command:</span></span>

```cmd/sh
dotnet --version
```

<span data-ttu-id="a01cd-114">Download the sample C# project from https://github.com/Azure-Samples/azure-iot-samples-csharp/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="a01cd-114">Download the sample C# project from https://github.com/Azure-Samples/azure-iot-samples-csharp/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="a01cd-115">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="a01cd-115">Create an IoT hub</span></span>

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]

## <a name="register-a-device"></a><span data-ttu-id="a01cd-116">Register a device</span><span class="sxs-lookup"><span data-stu-id="a01cd-116">Register a device</span></span>

<span data-ttu-id="a01cd-117">A device must be registered with your IoT hub before it can connect.</span><span class="sxs-lookup"><span data-stu-id="a01cd-117">A device must be registered with your IoT hub before it can connect.</span></span> <span data-ttu-id="a01cd-118">In this quickstart, you use the Azure CLI to register a simulated device.</span><span class="sxs-lookup"><span data-stu-id="a01cd-118">In this quickstart, you use the Azure CLI to register a simulated device.</span></span>

1. <span data-ttu-id="a01cd-119">Add the IoT Hub CLI extension and create the device identity.</span><span class="sxs-lookup"><span data-stu-id="a01cd-119">Add the IoT Hub CLI extension and create the device identity.</span></span> <span data-ttu-id="a01cd-120">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a01cd-120">Replace `{YourIoTHubName}` with the name you chose for your IoT hub:</span></span>

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name {YourIoTHubName} --device-id MyDotnetDevice
    ```

    <span data-ttu-id="a01cd-121">If you choose a different name for your device, update the device name in the sample applications before you run them.</span><span class="sxs-lookup"><span data-stu-id="a01cd-121">If you choose a different name for your device, update the device name in the sample applications before you run them.</span></span>

2. <span data-ttu-id="a01cd-122">Run the following command to get the _device connection string_ for the device you just registered:</span><span class="sxs-lookup"><span data-stu-id="a01cd-122">Run the following command to get the _device connection string_ for the device you just registered:</span></span>

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id MyDotnetDevice --output table
    ```

    <span data-ttu-id="a01cd-123">Make a note of the device connection string, which looks like `Hostname=...=`.</span><span class="sxs-lookup"><span data-stu-id="a01cd-123">Make a note of the device connection string, which looks like `Hostname=...=`.</span></span> <span data-ttu-id="a01cd-124">You use this value later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="a01cd-124">You use this value later in the quickstart.</span></span>

3. <span data-ttu-id="a01cd-125">You also need the _Event Hubs-compatible endpoint_, _Event Hubs-compatible path_, and _iothubowner primary key_ from your IoT hub to enable the back-end application to connect to your IoT hub and retrieve the messages.</span><span class="sxs-lookup"><span data-stu-id="a01cd-125">You also need the _Event Hubs-compatible endpoint_, _Event Hubs-compatible path_, and _iothubowner primary key_ from your IoT hub to enable the back-end application to connect to your IoT hub and retrieve the messages.</span></span> <span data-ttu-id="a01cd-126">The following commands retrieve these values for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a01cd-126">The following commands retrieve these values for your IoT hub:</span></span>

    ```azurecli-interactive
    az iot hub show --query properties.eventHubEndpoints.events.endpoint --name {YourIoTHubName}

    az iot hub show --query properties.eventHubEndpoints.events.path --name {YourIoTHubName}

    az iot hub policy show --name iothubowner --query primaryKey --hub-name {your IoT Hub name}
    ```

    <span data-ttu-id="a01cd-127">Make a note of these three values, which you use later in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="a01cd-127">Make a note of these three values, which you use later in the quickstart.</span></span>

## <a name="send-simulated-telemetry"></a><span data-ttu-id="a01cd-128">Send simulated telemetry</span><span class="sxs-lookup"><span data-stu-id="a01cd-128">Send simulated telemetry</span></span>

<span data-ttu-id="a01cd-129">The simulated device application connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span><span class="sxs-lookup"><span data-stu-id="a01cd-129">The simulated device application connects to a device-specific endpoint on your IoT hub and sends simulated temperature and humidity telemetry.</span></span>

1. <span data-ttu-id="a01cd-130">In a terminal window, navigate to the root folder of the sample C# project.</span><span class="sxs-lookup"><span data-stu-id="a01cd-130">In a terminal window, navigate to the root folder of the sample C# project.</span></span> <span data-ttu-id="a01cd-131">Then navigate to the **iot-hub\Quickstarts\simulated-device** folder.</span><span class="sxs-lookup"><span data-stu-id="a01cd-131">Then navigate to the **iot-hub\Quickstarts\simulated-device** folder.</span></span>

2. <span data-ttu-id="a01cd-132">Open the **SimulatedDevice.cs** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="a01cd-132">Open the **SimulatedDevice.cs** file in a text editor of your choice.</span></span>

    <span data-ttu-id="a01cd-133">Replace the value of the `s_connectionString` variable with the device connection string you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="a01cd-133">Replace the value of the `s_connectionString` variable with the device connection string you made a note of previously.</span></span> <span data-ttu-id="a01cd-134">Then save your changes to **SimulatedDevice.cs** file.</span><span class="sxs-lookup"><span data-stu-id="a01cd-134">Then save your changes to **SimulatedDevice.cs** file.</span></span>

3. <span data-ttu-id="a01cd-135">In the terminal window, run the following commands to install the required packages for simulated device application:</span><span class="sxs-lookup"><span data-stu-id="a01cd-135">In the terminal window, run the following commands to install the required packages for simulated device application:</span></span>

    ```cmd/sh
    dotnet restore
    ```

4. <span data-ttu-id="a01cd-136">In the terminal window, run the following command to build and run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="a01cd-136">In the terminal window, run the following command to build and run the simulated device application:</span></span>

    ```cmd/sh
    dotnet run
    ```

    <span data-ttu-id="a01cd-137">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="a01cd-137">The following screenshot shows the output as the simulated device application sends telemetry to your IoT hub:</span></span>

    ![Run the simulated device](media/quickstart-send-telemetry-dotnet/SimulatedDevice.png)

## <a name="read-the-telemetry-from-your-hub"></a><span data-ttu-id="a01cd-139">Read the telemetry from your hub</span><span class="sxs-lookup"><span data-stu-id="a01cd-139">Read the telemetry from your hub</span></span>

<span data-ttu-id="a01cd-140">The back-end application connects to the service-side **Events** endpoint on your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a01cd-140">The back-end application connects to the service-side **Events** endpoint on your IoT Hub.</span></span> <span data-ttu-id="a01cd-141">The application receives the device-to-cloud messages sent from your simulated device.</span><span class="sxs-lookup"><span data-stu-id="a01cd-141">The application receives the device-to-cloud messages sent from your simulated device.</span></span> <span data-ttu-id="a01cd-142">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="a01cd-142">An IoT Hub back-end application typically runs in the cloud to receive and process device-to-cloud messages.</span></span>

1. <span data-ttu-id="a01cd-143">In another terminal window, navigate to the root folder of the sample C# project.</span><span class="sxs-lookup"><span data-stu-id="a01cd-143">In another terminal window, navigate to the root folder of the sample C# project.</span></span> <span data-ttu-id="a01cd-144">Then navigate to the **iot-hub\Quickstarts\read-d2c-messages** folder.</span><span class="sxs-lookup"><span data-stu-id="a01cd-144">Then navigate to the **iot-hub\Quickstarts\read-d2c-messages** folder.</span></span>

2. <span data-ttu-id="a01cd-145">Open the **ReadDeviceToCloudMessages.cs** file in a text editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="a01cd-145">Open the **ReadDeviceToCloudMessages.cs** file in a text editor of your choice.</span></span> <span data-ttu-id="a01cd-146">Update the following variables and save your changes to the file.</span><span class="sxs-lookup"><span data-stu-id="a01cd-146">Update the following variables and save your changes to the file.</span></span>

    | <span data-ttu-id="a01cd-147">Variable</span><span class="sxs-lookup"><span data-stu-id="a01cd-147">Variable</span></span> | <span data-ttu-id="a01cd-148">Value</span><span class="sxs-lookup"><span data-stu-id="a01cd-148">Value</span></span> |
    | -------- | ----------- |
    | `s_eventHubsCompatibleEndpoint` | <span data-ttu-id="a01cd-149">Replace the value of the variable with the Event Hubs-compatible endpoint you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="a01cd-149">Replace the value of the variable with the Event Hubs-compatible endpoint you made a note of previously.</span></span> |
    | `s_eventHubsCompatiblePath`     | <span data-ttu-id="a01cd-150">Replace the value of the variable with the Event Hubs-compatible path you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="a01cd-150">Replace the value of the variable with the Event Hubs-compatible path you made a note of previously.</span></span> |
    | `s_iotHubSasKey`                | <span data-ttu-id="a01cd-151">Replace the value of the variable with the iothubowner primary key you made a note of previously.</span><span class="sxs-lookup"><span data-stu-id="a01cd-151">Replace the value of the variable with the iothubowner primary key you made a note of previously.</span></span> |

3. <span data-ttu-id="a01cd-152">In the terminal window, run the following commands to install the required libraries for the back-end application:</span><span class="sxs-lookup"><span data-stu-id="a01cd-152">In the terminal window, run the following commands to install the required libraries for the back-end application:</span></span>

    ```cmd/sh
    dotnet restore
    ```

4. <span data-ttu-id="a01cd-153">In the terminal window, run the following commands to build and run the back-end application:</span><span class="sxs-lookup"><span data-stu-id="a01cd-153">In the terminal window, run the following commands to build and run the back-end application:</span></span>

    ```cmd/sh
    dotnet run
    ```

    <span data-ttu-id="a01cd-154">The following screenshot shows the output as the back-end application receives telemetry sent by the simulated device to the hub:</span><span class="sxs-lookup"><span data-stu-id="a01cd-154">The following screenshot shows the output as the back-end application receives telemetry sent by the simulated device to the hub:</span></span>

    ![Run the back-end application](media/quickstart-send-telemetry-dotnet/ReadDeviceToCloud.png)

## <a name="clean-up-resources"></a><span data-ttu-id="a01cd-156">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a01cd-156">Clean up resources</span></span>

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="a01cd-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="a01cd-157">Next steps</span></span>

<span data-ttu-id="a01cd-158">In this quickstart, you've setup an IoT hub, registered a device, sent simulated telemetry to the hub using a C# application, and read the telemetry from the hub using a simple back-end application.</span><span class="sxs-lookup"><span data-stu-id="a01cd-158">In this quickstart, you've setup an IoT hub, registered a device, sent simulated telemetry to the hub using a C# application, and read the telemetry from the hub using a simple back-end application.</span></span>

<span data-ttu-id="a01cd-159">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span><span class="sxs-lookup"><span data-stu-id="a01cd-159">To learn how to control your simulated device from a back-end application, continue to the next quickstart.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a01cd-160">Quickstart: Control a device connected to an IoT hub</span><span class="sxs-lookup"><span data-stu-id="a01cd-160">Quickstart: Control a device connected to an IoT hub</span></span>](quickstart-control-device-dotnet.md)