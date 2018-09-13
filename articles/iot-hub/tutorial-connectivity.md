---
title: Check device connectivity to Azure IoT Hub
description: Use IoT Hub tools to troubleshoot, during development, device connectivity issues to your IoT hub.
services: iot-hub
author: dominicbetts
manager: timlt
ms.author: dobett
ms.custom: mvc
ms.date: 05/29/2018
ms.topic: tutorial
ms.service: iot-hub
ms.openlocfilehash: dc857760cf0d3fa2e146f22196b7bc36d119df5f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866799"
---
# <a name="tutorial-use-a-simulated-device-to-test-connectivity-with-your-iot-hub"></a><span data-ttu-id="e1bd8-103">Tutorial: Use a simulated device to test connectivity with your IoT hub</span><span class="sxs-lookup"><span data-stu-id="e1bd8-103">Tutorial: Use a simulated device to test connectivity with your IoT hub</span></span>

<span data-ttu-id="e1bd8-104">In this tutorial, you use Azure IoT Hub portal tools and Azure CLI commands to test device connectivity.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-104">In this tutorial, you use Azure IoT Hub portal tools and Azure CLI commands to test device connectivity.</span></span> <span data-ttu-id="e1bd8-105">This tutorial also uses a simple device simulator that you run on your desktop machine.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-105">This tutorial also uses a simple device simulator that you run on your desktop machine.</span></span>

<span data-ttu-id="e1bd8-106">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-106">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

<span data-ttu-id="e1bd8-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-107">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e1bd8-108">Check your device authentication</span><span class="sxs-lookup"><span data-stu-id="e1bd8-108">Check your device authentication</span></span>
> * <span data-ttu-id="e1bd8-109">Check device-to-cloud connectivity</span><span class="sxs-lookup"><span data-stu-id="e1bd8-109">Check device-to-cloud connectivity</span></span>
> * <span data-ttu-id="e1bd8-110">Check cloud-to-device connectivity</span><span class="sxs-lookup"><span data-stu-id="e1bd8-110">Check cloud-to-device connectivity</span></span>
> * <span data-ttu-id="e1bd8-111">Check device twin synchronization</span><span class="sxs-lookup"><span data-stu-id="e1bd8-111">Check device twin synchronization</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="prerequisites"></a><span data-ttu-id="e1bd8-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e1bd8-112">Prerequisites</span></span>

<span data-ttu-id="e1bd8-113">The CLI scripts you run in this tutorial use the [Microsoft Azure IoT Extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e1bd8-113">The CLI scripts you run in this tutorial use the [Microsoft Azure IoT Extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension/blob/master/README.md).</span></span> <span data-ttu-id="e1bd8-114">To install this extension, run the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-114">To install this extension, run the following CLI command:</span></span>

```azurecli-interactive
az extension add --name azure-cli-iot-ext
```

<span data-ttu-id="e1bd8-115">The device simulator application you run in this tutorial is written using Node.js.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-115">The device simulator application you run in this tutorial is written using Node.js.</span></span> <span data-ttu-id="e1bd8-116">You need Node.js v4.x.x or later on your development machine.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-116">You need Node.js v4.x.x or later on your development machine.</span></span>

<span data-ttu-id="e1bd8-117">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="e1bd8-117">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span></span>

<span data-ttu-id="e1bd8-118">You can verify the current version of Node.js on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-118">You can verify the current version of Node.js on your development machine using the following command:</span></span>

```cmd/sh
node --version
```

<span data-ttu-id="e1bd8-119">Download the sample device simulator Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-119">Download the sample device simulator Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="e1bd8-120">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="e1bd8-120">Create an IoT hub</span></span>

<span data-ttu-id="e1bd8-121">If you created a free or standard tier IoT hub in a previous quickstart or tutorial, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-121">If you created a free or standard tier IoT hub in a previous quickstart or tutorial, you can skip this step.</span></span>

[!INCLUDE [iot-hub-tutorials-create-free-hub](../../includes/iot-hub-tutorials-create-free-hub.md)]

## <a name="check-device-authentication"></a><span data-ttu-id="e1bd8-122">Check device authentication</span><span class="sxs-lookup"><span data-stu-id="e1bd8-122">Check device authentication</span></span>

<span data-ttu-id="e1bd8-123">A device must authenticate with your hub before it can exchange any data with the hub.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-123">A device must authenticate with your hub before it can exchange any data with the hub.</span></span> <span data-ttu-id="e1bd8-124">You can use the **IoT Devices** tool in the **Device Management** section of the portal to manage your devices and check the authentication keys they're using.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-124">You can use the **IoT Devices** tool in the **Device Management** section of the portal to manage your devices and check the authentication keys they're using.</span></span> <span data-ttu-id="e1bd8-125">In this section of the tutorial, you add a new test device, retrieve its key, and check that the test device can connect to the hub.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-125">In this section of the tutorial, you add a new test device, retrieve its key, and check that the test device can connect to the hub.</span></span> <span data-ttu-id="e1bd8-126">Later you reset the authentication key to observe what happens when a device tries to use an outdated key.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-126">Later you reset the authentication key to observe what happens when a device tries to use an outdated key.</span></span> <span data-ttu-id="e1bd8-127">This section of the tutorial uses the Azure portal to create, manage, and monitor a device, and the sample Node.js device simulator.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-127">This section of the tutorial uses the Azure portal to create, manage, and monitor a device, and the sample Node.js device simulator.</span></span>

<span data-ttu-id="e1bd8-128">Sign in to the portal and navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-128">Sign in to the portal and navigate to your IoT hub.</span></span> <span data-ttu-id="e1bd8-129">Then navigate to the **IoT Devices** tool:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-129">Then navigate to the **IoT Devices** tool:</span></span>

![IoT Devices tool](media/tutorial-connectivity/iot-devices-tool.png)

<span data-ttu-id="e1bd8-131">To register a new device, click **+ Add**, set **Device ID** to **MyTestDevice**, and click **Save**:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-131">To register a new device, click **+ Add**, set **Device ID** to **MyTestDevice**, and click **Save**:</span></span>

![Add new device](media/tutorial-connectivity/add-device.png)

<span data-ttu-id="e1bd8-133">To retrieve the connection string for **MyTestDevice**, click on it in the list of devices and then copy the **Connection string-primary key** value.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-133">To retrieve the connection string for **MyTestDevice**, click on it in the list of devices and then copy the **Connection string-primary key** value.</span></span> <span data-ttu-id="e1bd8-134">The connection string includes the *shared access key* for the device.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-134">The connection string includes the *shared access key* for the device.</span></span>

![Retrieve device connection string](media/tutorial-connectivity/copy-connection-string.png)

<span data-ttu-id="e1bd8-136">To simulate **MyTestDevice** sending telemetry to your IoT hub, run the Node.js simulated device application you downloaded previously.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-136">To simulate **MyTestDevice** sending telemetry to your IoT hub, run the Node.js simulated device application you downloaded previously.</span></span>

<span data-ttu-id="e1bd8-137">In a terminal window on your development machine, navigate to the root folder of the sample Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-137">In a terminal window on your development machine, navigate to the root folder of the sample Node.js project you downloaded.</span></span> <span data-ttu-id="e1bd8-138">Then navigate to the **iot-hub\Tutorials\ConnectivityTests\simulated-device** folder.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-138">Then navigate to the **iot-hub\Tutorials\ConnectivityTests\simulated-device** folder.</span></span>

<span data-ttu-id="e1bd8-139">In the terminal window, run the following commands to install the required libraries and run the simulated device application.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-139">In the terminal window, run the following commands to install the required libraries and run the simulated device application.</span></span> <span data-ttu-id="e1bd8-140">Use the device connectin string you made a note of when you added the device in the portal.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-140">Use the device connectin string you made a note of when you added the device in the portal.</span></span>

```cmd/sh
npm install
node SimulatedDevice-1.js "{your device connection string}"
```

<span data-ttu-id="e1bd8-141">The terminal window displays information as it tries to connect to your hub:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-141">The terminal window displays information as it tries to connect to your hub:</span></span>

![Simulated device connecting](media/tutorial-connectivity/sim-1-connected.png)

<span data-ttu-id="e1bd8-143">You've now successfully authenticated from a device using a device key generated by your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-143">You've now successfully authenticated from a device using a device key generated by your IoT hub.</span></span>

### <a name="reset-keys"></a><span data-ttu-id="e1bd8-144">Reset keys</span><span class="sxs-lookup"><span data-stu-id="e1bd8-144">Reset keys</span></span>

<span data-ttu-id="e1bd8-145">In this section, you reset the device key and observe the error when the simulated device tries to connect.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-145">In this section, you reset the device key and observe the error when the simulated device tries to connect.</span></span>

<span data-ttu-id="e1bd8-146">To reset the primary device key for **MyTestDevice**, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-146">To reset the primary device key for **MyTestDevice**, run the following commands:</span></span>

```azurecli-interactive
# Generate a new Base64 encoded key using the current date
read key < <(date +%s | sha256sum | base64 | head -c 32)

# Requires the IoT Extension for Azure CLI 2.0
# az extension add --name azure-cli-iot-ext

# Reset the primary device key for MyTestDevice
az iot hub device-identity update --device-id MyTestDevice --set authentication.symmetricKey.primaryKey=$key --hub-name {YourIoTHubName}
```

<span data-ttu-id="e1bd8-147">In the terminal window on your development machine, run the simulated device application again:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-147">In the terminal window on your development machine, run the simulated device application again:</span></span>

```cmd/sh
npm install
node SimulatedDevice-1.js "{your device connection string}"
```

<span data-ttu-id="e1bd8-148">This time you see an authentication error when the application tries to connect:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-148">This time you see an authentication error when the application tries to connect:</span></span>

![Connection error](media/tutorial-connectivity/sim-1-fail.png)

### <a name="generate-shared-access-signature-sas-token"></a><span data-ttu-id="e1bd8-150">Generate shared access signature (SAS) token</span><span class="sxs-lookup"><span data-stu-id="e1bd8-150">Generate shared access signature (SAS) token</span></span>

<span data-ttu-id="e1bd8-151">If your device uses one of the IoT Hub device SDKs, the SDK library code generates the SAS token used to authenticate with the hub.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-151">If your device uses one of the IoT Hub device SDKs, the SDK library code generates the SAS token used to authenticate with the hub.</span></span> <span data-ttu-id="e1bd8-152">A SAS token is generated from the name of your hub, the name of your device, and the device key.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-152">A SAS token is generated from the name of your hub, the name of your device, and the device key.</span></span>

<span data-ttu-id="e1bd8-153">In some scenarios, such as in a cloud protocol gateway or as part of a custom authentication scheme, you may need to generate the SAS token yourself.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-153">In some scenarios, such as in a cloud protocol gateway or as part of a custom authentication scheme, you may need to generate the SAS token yourself.</span></span> <span data-ttu-id="e1bd8-154">To troubleshoot issues with your SAS generation code, it's useful to be able to generate a known-good SAS token to use during testing.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-154">To troubleshoot issues with your SAS generation code, it's useful to be able to generate a known-good SAS token to use during testing.</span></span>

> [!NOTE]
> <span data-ttu-id="e1bd8-155">The SimulatedDevice-2.js sample includes examples of generating a SAS token both with and without the SDK.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-155">The SimulatedDevice-2.js sample includes examples of generating a SAS token both with and without the SDK.</span></span>

<span data-ttu-id="e1bd8-156">To generate a known-good SAS token using the CLI, run the following command:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-156">To generate a known-good SAS token using the CLI, run the following command:</span></span>

```azurecli-interactive
az iot hub generate-sas-token --device-id MyTestDevice --hub-name {YourIoTHubName}
```

<span data-ttu-id="e1bd8-157">Make a note of the full text of the generated SAS token.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-157">Make a note of the full text of the generated SAS token.</span></span> <span data-ttu-id="e1bd8-158">A SAS token looks like the following: `'SharedAccessSignature sr=tutorials-iot-hub.azure-devices.net%2Fdevices%2FMyTestDevice&sig=....&se=1524155307'`</span><span class="sxs-lookup"><span data-stu-id="e1bd8-158">A SAS token looks like the following: `'SharedAccessSignature sr=tutorials-iot-hub.azure-devices.net%2Fdevices%2FMyTestDevice&sig=....&se=1524155307'`</span></span>

<span data-ttu-id="e1bd8-159">In a terminal window on your development machine, navigate to the root folder of the sample Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-159">In a terminal window on your development machine, navigate to the root folder of the sample Node.js project you downloaded.</span></span> <span data-ttu-id="e1bd8-160">Then navigate to the **iot-hub\Tutorials\ConnectivityTests\simulated-device** folder.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-160">Then navigate to the **iot-hub\Tutorials\ConnectivityTests\simulated-device** folder.</span></span>

<span data-ttu-id="e1bd8-161">In the terminal window, run the following commands to install the required libraries and run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-161">In the terminal window, run the following commands to install the required libraries and run the simulated device application:</span></span>

```cmd/sh
npm install
node SimulatedDevice-2.js "{Your SAS token}"
```

<span data-ttu-id="e1bd8-162">The terminal window displays information as it tries to connect to your hub using the SAS token:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-162">The terminal window displays information as it tries to connect to your hub using the SAS token:</span></span>

![Simulated device connecting with token](media/tutorial-connectivity/sim-2-connected.png)

<span data-ttu-id="e1bd8-164">You've now successfully authenticated from a device using a test SAS token generated by a CLI command.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-164">You've now successfully authenticated from a device using a test SAS token generated by a CLI command.</span></span> <span data-ttu-id="e1bd8-165">The **SimulatedDevice-2.js** file includes sample code that shows you how to generate a SAS token in code.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-165">The **SimulatedDevice-2.js** file includes sample code that shows you how to generate a SAS token in code.</span></span>

### <a name="protocols"></a><span data-ttu-id="e1bd8-166">Protocols</span><span class="sxs-lookup"><span data-stu-id="e1bd8-166">Protocols</span></span>

<span data-ttu-id="e1bd8-167">A device can use any of the following protocols to connect to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-167">A device can use any of the following protocols to connect to your IoT hub:</span></span>

| <span data-ttu-id="e1bd8-168">Protocol</span><span class="sxs-lookup"><span data-stu-id="e1bd8-168">Protocol</span></span> | <span data-ttu-id="e1bd8-169">Outbound port</span><span class="sxs-lookup"><span data-stu-id="e1bd8-169">Outbound port</span></span> |
| --- | --- |
| <span data-ttu-id="e1bd8-170">MQTT</span><span class="sxs-lookup"><span data-stu-id="e1bd8-170">MQTT</span></span> |<span data-ttu-id="e1bd8-171">8883</span><span class="sxs-lookup"><span data-stu-id="e1bd8-171">8883</span></span> |
| <span data-ttu-id="e1bd8-172">MQTT over WebSockets</span><span class="sxs-lookup"><span data-stu-id="e1bd8-172">MQTT over WebSockets</span></span> |<span data-ttu-id="e1bd8-173">443</span><span class="sxs-lookup"><span data-stu-id="e1bd8-173">443</span></span> |
| <span data-ttu-id="e1bd8-174">AMQP</span><span class="sxs-lookup"><span data-stu-id="e1bd8-174">AMQP</span></span> |<span data-ttu-id="e1bd8-175">5671</span><span class="sxs-lookup"><span data-stu-id="e1bd8-175">5671</span></span> |
| <span data-ttu-id="e1bd8-176">AMQP over WebSockets</span><span class="sxs-lookup"><span data-stu-id="e1bd8-176">AMQP over WebSockets</span></span> |<span data-ttu-id="e1bd8-177">443</span><span class="sxs-lookup"><span data-stu-id="e1bd8-177">443</span></span> |
| <span data-ttu-id="e1bd8-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e1bd8-178">HTTPS</span></span> |<span data-ttu-id="e1bd8-179">443</span><span class="sxs-lookup"><span data-stu-id="e1bd8-179">443</span></span> |

<span data-ttu-id="e1bd8-180">If the outbound port is blocked by a firewall, the device can't connect:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-180">If the outbound port is blocked by a firewall, the device can't connect:</span></span>

![Port blocked](media/tutorial-connectivity/port-blocked.png)

## <a name="check-device-to-cloud-connectivity"></a><span data-ttu-id="e1bd8-182">Check device-to-cloud connectivity</span><span class="sxs-lookup"><span data-stu-id="e1bd8-182">Check device-to-cloud connectivity</span></span>

<span data-ttu-id="e1bd8-183">After a device connects, it typically tries to send telemetry to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-183">After a device connects, it typically tries to send telemetry to your IoT hub.</span></span> <span data-ttu-id="e1bd8-184">This section shows you how you can verify that the telemetry sent by the device reaches your hub.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-184">This section shows you how you can verify that the telemetry sent by the device reaches your hub.</span></span>

<span data-ttu-id="e1bd8-185">First, retrieve the current connection string for your simulated device using the following command:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-185">First, retrieve the current connection string for your simulated device using the following command:</span></span>

```azurecli-interactive
az iot hub device-identity show-connection-string --device-id MyTestDevice --output table --hub-name {YourIoTHubName}
```

<span data-ttu-id="e1bd8-186">To run a simulated device that sends messages, navigate to the **iot-hub\Tutorials\ConnectivityTests\simulated-device** folder in the code you downloaded.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-186">To run a simulated device that sends messages, navigate to the **iot-hub\Tutorials\ConnectivityTests\simulated-device** folder in the code you downloaded.</span></span>

<span data-ttu-id="e1bd8-187">In the terminal window, run the following commands to install the required libraries and run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-187">In the terminal window, run the following commands to install the required libraries and run the simulated device application:</span></span>

```cmd/sh
npm install
node SimulatedDevice-3.js "{your device connection string}"
```

<span data-ttu-id="e1bd8-188">The terminal window displays information as it sends telemetry to your hub:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-188">The terminal window displays information as it sends telemetry to your hub:</span></span>

![Simulated device sending messages](media/tutorial-connectivity/sim-3-sending.png)

<span data-ttu-id="e1bd8-190">You can use **Metrics** in the portal to verify that the telemetry messages are reaching your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-190">You can use **Metrics** in the portal to verify that the telemetry messages are reaching your IoT hub:</span></span>

![Navigate to IoT Hub metrics](media/tutorial-connectivity/metrics-portal.png)

<span data-ttu-id="e1bd8-192">Select your IoT hub in the **Resource** drop-down, select **Telemetry messages sent** as the metric, and set the time range to **Past hour**.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-192">Select your IoT hub in the **Resource** drop-down, select **Telemetry messages sent** as the metric, and set the time range to **Past hour**.</span></span> <span data-ttu-id="e1bd8-193">The chart shows the aggregate count of messages sent by the simulated device:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-193">The chart shows the aggregate count of messages sent by the simulated device:</span></span>

![Show IoT Hub metrics](media/tutorial-connectivity/metrics-active.png)

<span data-ttu-id="e1bd8-195">It takes a few minutes for the metrics to become available after you start the simulated device.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-195">It takes a few minutes for the metrics to become available after you start the simulated device.</span></span>

## <a name="check-cloud-to-device-connectivity"></a><span data-ttu-id="e1bd8-196">Check cloud-to-device connectivity</span><span class="sxs-lookup"><span data-stu-id="e1bd8-196">Check cloud-to-device connectivity</span></span>

<span data-ttu-id="e1bd8-197">This section shows how you can make a test direct method call to a device to check cloud-to-device connectivity.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-197">This section shows how you can make a test direct method call to a device to check cloud-to-device connectivity.</span></span> <span data-ttu-id="e1bd8-198">You run a simulated device on your development machine to listen for direct method calls from your hub.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-198">You run a simulated device on your development machine to listen for direct method calls from your hub.</span></span>

<span data-ttu-id="e1bd8-199">In a terminal window, use the following command to run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-199">In a terminal window, use the following command to run the simulated device application:</span></span>

```cmd/sh
node SimulatedDevice-3.js "{your device connection string}"
```

<span data-ttu-id="e1bd8-200">Use a CLI command to call a direct method on the device:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-200">Use a CLI command to call a direct method on the device:</span></span>

```azurecli-interactive
az iot hub invoke-device-method --device-id MyTestDevice --method-name TestMethod --timeout 10 --method-payload '{"key":"value"}' --hub-name {YourIoTHubName}
```

<span data-ttu-id="e1bd8-201">The simulated device prints a message to the console when it receives a direct method call:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-201">The simulated device prints a message to the console when it receives a direct method call:</span></span>

![Simulated device receives direct method call](media/tutorial-connectivity/receive-method-call.png)

<span data-ttu-id="e1bd8-203">When the simulated device successfully receives the direct method call, it sends an acknowledgement back to the hub:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-203">When the simulated device successfully receives the direct method call, it sends an acknowledgement back to the hub:</span></span>

![Receive direct method acknowledgement](media/tutorial-connectivity/method-acknowledgement.png)

## <a name="check-twin-synchronization"></a><span data-ttu-id="e1bd8-205">Check twin synchronization</span><span class="sxs-lookup"><span data-stu-id="e1bd8-205">Check twin synchronization</span></span>

<span data-ttu-id="e1bd8-206">Devices use twins to synchronize state between the device and the hub.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-206">Devices use twins to synchronize state between the device and the hub.</span></span> <span data-ttu-id="e1bd8-207">In this section, you use CLI commands to send _desired properties_ to a device and read the _reported properties_ sent by the device.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-207">In this section, you use CLI commands to send _desired properties_ to a device and read the _reported properties_ sent by the device.</span></span>

<span data-ttu-id="e1bd8-208">The simulated device you use in this section sends reported properties to the hub whenever it starts up, and prints desired properties to the console whenever it receives them.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-208">The simulated device you use in this section sends reported properties to the hub whenever it starts up, and prints desired properties to the console whenever it receives them.</span></span>

<span data-ttu-id="e1bd8-209">In a terminal window, use the following command to run the simulated device application:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-209">In a terminal window, use the following command to run the simulated device application:</span></span>

```cmd/sh
node SimulatedDevice-3.js "{your device connection string}"
```

<span data-ttu-id="e1bd8-210">To verify that the hub received the reported properties from the device, use the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-210">To verify that the hub received the reported properties from the device, use the following CLI command:</span></span>

```azurecli-interactive
az iot hub device-twin show --device-id MyTestDevice --hub-name {YourIoTHubName}
```

<span data-ttu-id="e1bd8-211">In the output from the command, you can see the **devicelaststarted** property in the reported properties section.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-211">In the output from the command, you can see the **devicelaststarted** property in the reported properties section.</span></span> <span data-ttu-id="e1bd8-212">This property shows the date and time you last started the simulated device.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-212">This property shows the date and time you last started the simulated device.</span></span>

![View reported properties](media/tutorial-connectivity/reported-properties.png)

<span data-ttu-id="e1bd8-214">To verify that the hub can send desired property values to the device, use the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-214">To verify that the hub can send desired property values to the device, use the following CLI command:</span></span>

```azurecli-interactive
az iot hub device-twin update --set properties.desired='{"mydesiredproperty":"propertyvalue"}' --device-id MyTestDevice --hub-name {YourIoTHubName}
```

<span data-ttu-id="e1bd8-215">The simulated device prints a message when it receives a desired property update from the hub:</span><span class="sxs-lookup"><span data-stu-id="e1bd8-215">The simulated device prints a message when it receives a desired property update from the hub:</span></span>

![Receive desired properties](media/tutorial-connectivity/desired-properties.png)

<span data-ttu-id="e1bd8-217">In addition to receiving desired property changes as they're made, the simulated device automatically checks for desired properties when it starts up.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-217">In addition to receiving desired property changes as they're made, the simulated device automatically checks for desired properties when it starts up.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="e1bd8-218">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e1bd8-218">Clean up resources</span></span>

<span data-ttu-id="e1bd8-219">If you don't need the IoT hub any longer, delete it and the resource group in the portal.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-219">If you don't need the IoT hub any longer, delete it and the resource group in the portal.</span></span> <span data-ttu-id="e1bd8-220">To do so, select the **tutorials-iot-hub-rg** resource group that contains your IoT hub and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-220">To do so, select the **tutorials-iot-hub-rg** resource group that contains your IoT hub and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1bd8-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1bd8-221">Next steps</span></span>

<span data-ttu-id="e1bd8-222">In this tutorial, you've seen how to check your device keys, check device-to-cloud connectivity, check cloud-to-device connectivity, and check device twin synchronization.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-222">In this tutorial, you've seen how to check your device keys, check device-to-cloud connectivity, check cloud-to-device connectivity, and check device twin synchronization.</span></span> <span data-ttu-id="e1bd8-223">To learn more about how to monitor your IoT hub, visit the how-to article for IoT Hub monitoring.</span><span class="sxs-lookup"><span data-stu-id="e1bd8-223">To learn more about how to monitor your IoT hub, visit the how-to article for IoT Hub monitoring.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1bd8-224">Monitor with diagnostics</span><span class="sxs-lookup"><span data-stu-id="e1bd8-224">Monitor with diagnostics</span></span>](iot-hub-monitor-resource-health.md)
