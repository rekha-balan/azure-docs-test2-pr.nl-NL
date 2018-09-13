---
title: Azure IoT device management with IoT extension for Azure CLI 2.0 | Microsoft Docs
description: Use the IoT extension for Azure CLI 2.0 tool for Azure IoT Hub device management, featuring the Direct methods and the Twin’s desired properties management options.
author: chrissie926
manager: ''
keywords: azure iot device management, azure iot hub device management, device management iot, iot hub device management
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 01/16/2018
ms.author: menchi
ms.openlocfilehash: dc96e70a031d6080217e71b829ec5de3c64e4cf7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856319"
---
# <a name="use-the-iot-extension-for-azure-cli-20-for-azure-iot-hub-device-management"></a><span data-ttu-id="932e5-104">Use the IoT extension for Azure CLI 2.0 for Azure IoT Hub device management</span><span class="sxs-lookup"><span data-stu-id="932e5-104">Use the IoT extension for Azure CLI 2.0 for Azure IoT Hub device management</span></span>

![End-to-end diagram](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="932e5-106">[The IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension) is a new open source IoT extension that adds to the capabilities of [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="932e5-106">[The IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension) is a new open source IoT extension that adds to the capabilities of [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview?view=azure-cli-latest).</span></span> <span data-ttu-id="932e5-107">Azure CLI 2.0 includes commands for interacting with Azure resource manager and management endpoints.</span><span class="sxs-lookup"><span data-stu-id="932e5-107">Azure CLI 2.0 includes commands for interacting with Azure resource manager and management endpoints.</span></span> <span data-ttu-id="932e5-108">For example, you can use Azure CLI 2.0 to create an Azure VM or an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="932e5-108">For example, you can use Azure CLI 2.0 to create an Azure VM or an IoT hub.</span></span> <span data-ttu-id="932e5-109">A CLI extension enables an Azure service to augment the Azure CLI giving you access to additional service-specific capabilities.</span><span class="sxs-lookup"><span data-stu-id="932e5-109">A CLI extension enables an Azure service to augment the Azure CLI giving you access to additional service-specific capabilities.</span></span> <span data-ttu-id="932e5-110">The IoT extension gives IoT developers command line access to all IoT Hub, IoT Edge, and IoT Hub Device Provisioning Service capabilities.</span><span class="sxs-lookup"><span data-stu-id="932e5-110">The IoT extension gives IoT developers command line access to all IoT Hub, IoT Edge, and IoT Hub Device Provisioning Service capabilities.</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-whole.md)]

| <span data-ttu-id="932e5-111">Management option</span><span class="sxs-lookup"><span data-stu-id="932e5-111">Management option</span></span>          | <span data-ttu-id="932e5-112">Task</span><span class="sxs-lookup"><span data-stu-id="932e5-112">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="932e5-113">Direct methods</span><span class="sxs-lookup"><span data-stu-id="932e5-113">Direct methods</span></span>             | <span data-ttu-id="932e5-114">Make a device act such as starting or stopping sending messages or rebooting the device.</span><span class="sxs-lookup"><span data-stu-id="932e5-114">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="932e5-115">Twin desired properties</span><span class="sxs-lookup"><span data-stu-id="932e5-115">Twin desired properties</span></span>    | <span data-ttu-id="932e5-116">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="932e5-116">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="932e5-117">Twin reported properties</span><span class="sxs-lookup"><span data-stu-id="932e5-117">Twin reported properties</span></span>   | <span data-ttu-id="932e5-118">Get the reported state of a device.</span><span class="sxs-lookup"><span data-stu-id="932e5-118">Get the reported state of a device.</span></span> <span data-ttu-id="932e5-119">For example, the device reports the LED is blinking now.</span><span class="sxs-lookup"><span data-stu-id="932e5-119">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="932e5-120">Twin tags</span><span class="sxs-lookup"><span data-stu-id="932e5-120">Twin tags</span></span>                  | <span data-ttu-id="932e5-121">Store device-specific metadata in the cloud.</span><span class="sxs-lookup"><span data-stu-id="932e5-121">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="932e5-122">For example, the deployment location of a vending machine.</span><span class="sxs-lookup"><span data-stu-id="932e5-122">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="932e5-123">Device twin queries</span><span class="sxs-lookup"><span data-stu-id="932e5-123">Device twin queries</span></span>        | <span data-ttu-id="932e5-124">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span><span class="sxs-lookup"><span data-stu-id="932e5-124">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="932e5-125">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="932e5-125">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

<span data-ttu-id="932e5-126">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span><span class="sxs-lookup"><span data-stu-id="932e5-126">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="932e5-127">IoT Hub persists a device twin for each device that connects to it.</span><span class="sxs-lookup"><span data-stu-id="932e5-127">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="932e5-128">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="932e5-128">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="932e5-129">What you learn</span><span class="sxs-lookup"><span data-stu-id="932e5-129">What you learn</span></span>

<span data-ttu-id="932e5-130">You learn using the IoT extension for Azure CLI 2.0 with various management options on your development machine.</span><span class="sxs-lookup"><span data-stu-id="932e5-130">You learn using the IoT extension for Azure CLI 2.0 with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="932e5-131">What you do</span><span class="sxs-lookup"><span data-stu-id="932e5-131">What you do</span></span>

<span data-ttu-id="932e5-132">Run Azure CLI 2.0 and the IoT extension for Azure CLI 2.0 with various management options.</span><span class="sxs-lookup"><span data-stu-id="932e5-132">Run Azure CLI 2.0 and the IoT extension for Azure CLI 2.0 with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="932e5-133">What you need</span><span class="sxs-lookup"><span data-stu-id="932e5-133">What you need</span></span>

- <span data-ttu-id="932e5-134">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="932e5-134">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="932e5-135">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="932e5-135">An active Azure subscription.</span></span>
  - <span data-ttu-id="932e5-136">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="932e5-136">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="932e5-137">A client application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="932e5-137">A client application that sends messages to your Azure IoT hub.</span></span>

- <span data-ttu-id="932e5-138">Make sure your device is running with the client application during this tutorial.</span><span class="sxs-lookup"><span data-stu-id="932e5-138">Make sure your device is running with the client application during this tutorial.</span></span>

- [<span data-ttu-id="932e5-139">Python 2.7x or Python 3.x</span><span class="sxs-lookup"><span data-stu-id="932e5-139">Python 2.7x or Python 3.x</span></span>](https://www.python.org/downloads/)

- <span data-ttu-id="932e5-140">Install Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="932e5-140">Install Azure CLI 2.0.</span></span> <span data-ttu-id="932e5-141">One simple way to install on Windows is to download and install the [MSI](https://aka.ms/InstallAzureCliWindows).</span><span class="sxs-lookup"><span data-stu-id="932e5-141">One simple way to install on Windows is to download and install the [MSI](https://aka.ms/InstallAzureCliWindows).</span></span> <span data-ttu-id="932e5-142">You can also follow the installation instructions on [Microsoft Docs](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) to setup Azure CLI 2.0 in your environment.</span><span class="sxs-lookup"><span data-stu-id="932e5-142">You can also follow the installation instructions on [Microsoft Docs](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) to setup Azure CLI 2.0 in your environment.</span></span> <span data-ttu-id="932e5-143">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span><span class="sxs-lookup"><span data-stu-id="932e5-143">At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above.</span></span> <span data-ttu-id="932e5-144">Use `az –version` to validate.</span><span class="sxs-lookup"><span data-stu-id="932e5-144">Use `az –version` to validate.</span></span> 

- <span data-ttu-id="932e5-145">Install the IoT extension.</span><span class="sxs-lookup"><span data-stu-id="932e5-145">Install the IoT extension.</span></span> <span data-ttu-id="932e5-146">The simplest way is to run `az extension add --name azure-cli-iot-ext`.</span><span class="sxs-lookup"><span data-stu-id="932e5-146">The simplest way is to run `az extension add --name azure-cli-iot-ext`.</span></span> <span data-ttu-id="932e5-147">[The IoT extension readme](https://github.com/Azure/azure-iot-cli-extension/blob/master/README.md) describes several ways to install the extension.</span><span class="sxs-lookup"><span data-stu-id="932e5-147">[The IoT extension readme](https://github.com/Azure/azure-iot-cli-extension/blob/master/README.md) describes several ways to install the extension.</span></span>


## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="932e5-148">Log in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="932e5-148">Log in to your Azure account</span></span>

<span data-ttu-id="932e5-149">Log in to your Azure account by running the following command:</span><span class="sxs-lookup"><span data-stu-id="932e5-149">Log in to your Azure account by running the following command:</span></span>

```bash
az login
```

## <a name="direct-methods"></a><span data-ttu-id="932e5-150">Direct methods</span><span class="sxs-lookup"><span data-stu-id="932e5-150">Direct methods</span></span>

```bash
az iot hub invoke-device-method --device-id <your device id> --hub-name <your hub name> --method-name <the method name> --method-payload <the method payload>
```

## <a name="device-twin-desired-properties"></a><span data-ttu-id="932e5-151">Device twin desired properties</span><span class="sxs-lookup"><span data-stu-id="932e5-151">Device twin desired properties</span></span>

<span data-ttu-id="932e5-152">Set a desired property interval = 3000 by running the following command:</span><span class="sxs-lookup"><span data-stu-id="932e5-152">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
az iot hub device-twin update -n <your hub name> -d <your device id> --set properties.desired.interval = 3000
```

<span data-ttu-id="932e5-153">This property can be read from your device.</span><span class="sxs-lookup"><span data-stu-id="932e5-153">This property can be read from your device.</span></span>

## <a name="device-twin-reported-properties"></a><span data-ttu-id="932e5-154">Device twin reported properties</span><span class="sxs-lookup"><span data-stu-id="932e5-154">Device twin reported properties</span></span>

<span data-ttu-id="932e5-155">Get the reported properties of the device by running the following command:</span><span class="sxs-lookup"><span data-stu-id="932e5-155">Get the reported properties of the device by running the following command:</span></span>

```bash
az iot hub device-twin show -n <your hub name> -d <your device id>
```

<span data-ttu-id="932e5-156">One of the twin reported properties is $metadata.$lastUpdated which shows the last time the device app updated its reported property set.</span><span class="sxs-lookup"><span data-stu-id="932e5-156">One of the twin reported properties is $metadata.$lastUpdated which shows the last time the device app updated its reported property set.</span></span>

## <a name="device-twin-tags"></a><span data-ttu-id="932e5-157">Device twin tags</span><span class="sxs-lookup"><span data-stu-id="932e5-157">Device twin tags</span></span>

<span data-ttu-id="932e5-158">Display the tags and properties of the device by running the following command:</span><span class="sxs-lookup"><span data-stu-id="932e5-158">Display the tags and properties of the device by running the following command:</span></span>

```bash
az iot hub device-twin show --hub-name <your hub name> --device-id <your device id>
```

<span data-ttu-id="932e5-159">Add a field role = temperature&humidity to the device by running the following command:</span><span class="sxs-lookup"><span data-stu-id="932e5-159">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
az iot hub device-twin update --hub-name <your hub name> --device-id <your device id> --set tags = '{"role":"temperature&humidity"}}'
```

## <a name="device-twin-queries"></a><span data-ttu-id="932e5-160">Device twin queries</span><span class="sxs-lookup"><span data-stu-id="932e5-160">Device twin queries</span></span>

<span data-ttu-id="932e5-161">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span><span class="sxs-lookup"><span data-stu-id="932e5-161">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
az iot hub query --hub-name <your hub name> --query-command "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="932e5-162">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span><span class="sxs-lookup"><span data-stu-id="932e5-162">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
az iot hub query --hub-name <your hub name> --query-command "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="932e5-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="932e5-163">Next steps</span></span>

<span data-ttu-id="932e5-164">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="932e5-164">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
