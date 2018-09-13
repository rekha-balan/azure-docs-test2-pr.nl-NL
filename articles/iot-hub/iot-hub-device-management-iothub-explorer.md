---
title: Azure IoT device management with iothub-explorer | Microsoft Docs
description: Use the iothub-explorer CLI tool for Azure IoT Hub device management, featuring the Direct methods and the Twin’s desired properties management options.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure iot device management, azure iot hub device management, device management iot, iot hub device management
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: xshi
ms.openlocfilehash: a950ff024295e11114e8517783fc3b766752eef2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552799"
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="b605b-104">Use iothub-explorer for Azure IoT Hub device management</span><span class="sxs-lookup"><span data-stu-id="b605b-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="b605b-105">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span><span class="sxs-lookup"><span data-stu-id="b605b-105">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="b605b-106">It comes with management options that you can use to perform various tasks.</span><span class="sxs-lookup"><span data-stu-id="b605b-106">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="b605b-107">Management option</span><span class="sxs-lookup"><span data-stu-id="b605b-107">Management option</span></span>          | <span data-ttu-id="b605b-108">Task</span><span class="sxs-lookup"><span data-stu-id="b605b-108">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b605b-109">Direct methods</span><span class="sxs-lookup"><span data-stu-id="b605b-109">Direct methods</span></span>             | <span data-ttu-id="b605b-110">Make a device act such as starting or stopping sending messages or rebooting the device.</span><span class="sxs-lookup"><span data-stu-id="b605b-110">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="b605b-111">Twin desired properties</span><span class="sxs-lookup"><span data-stu-id="b605b-111">Twin desired properties</span></span>    | <span data-ttu-id="b605b-112">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="b605b-112">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="b605b-113">Twin reported properties</span><span class="sxs-lookup"><span data-stu-id="b605b-113">Twin reported properties</span></span>   | <span data-ttu-id="b605b-114">Get the reported state of a device.</span><span class="sxs-lookup"><span data-stu-id="b605b-114">Get the reported state of a device.</span></span> <span data-ttu-id="b605b-115">For example, the device reports the LED is blinking now.</span><span class="sxs-lookup"><span data-stu-id="b605b-115">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="b605b-116">Twin tags</span><span class="sxs-lookup"><span data-stu-id="b605b-116">Twin tags</span></span>                  | <span data-ttu-id="b605b-117">Store device-specific metadata in the cloud.</span><span class="sxs-lookup"><span data-stu-id="b605b-117">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="b605b-118">For example, the deployment location of a vending machine.</span><span class="sxs-lookup"><span data-stu-id="b605b-118">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="b605b-119">Cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="b605b-119">Cloud-to-device messages</span></span>   | <span data-ttu-id="b605b-120">Send notifications to a device.</span><span class="sxs-lookup"><span data-stu-id="b605b-120">Send notifications to a device.</span></span> <span data-ttu-id="b605b-121">For example, "It is very likely to rain today.</span><span class="sxs-lookup"><span data-stu-id="b605b-121">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="b605b-122">Don't forget to bring an umbrella."</span><span class="sxs-lookup"><span data-stu-id="b605b-122">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="b605b-123">Device twin queries</span><span class="sxs-lookup"><span data-stu-id="b605b-123">Device twin queries</span></span>        | <span data-ttu-id="b605b-124">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span><span class="sxs-lookup"><span data-stu-id="b605b-124">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="b605b-125">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="b605b-125">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b605b-126">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span><span class="sxs-lookup"><span data-stu-id="b605b-126">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="b605b-127">IoT Hub persists a device twin for each device that connects to it.</span><span class="sxs-lookup"><span data-stu-id="b605b-127">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="b605b-128">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="b605b-128">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b605b-129">What you learn</span><span class="sxs-lookup"><span data-stu-id="b605b-129">What you learn</span></span>

<span data-ttu-id="b605b-130">You learn using iothub-explorer with various management options.</span><span class="sxs-lookup"><span data-stu-id="b605b-130">You learn using iothub-explorer with various management options.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b605b-131">What you do</span><span class="sxs-lookup"><span data-stu-id="b605b-131">What you do</span></span>

<span data-ttu-id="b605b-132">Run iothub-explorer with various management options.</span><span class="sxs-lookup"><span data-stu-id="b605b-132">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b605b-133">What you need</span><span class="sxs-lookup"><span data-stu-id="b605b-133">What you need</span></span>

- <span data-ttu-id="b605b-134">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="b605b-134">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="b605b-135">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b605b-135">An active Azure subscription.</span></span>
  - <span data-ttu-id="b605b-136">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="b605b-136">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="b605b-137">A client application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b605b-137">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="b605b-138">iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="b605b-138">iothub-explorer.</span></span> <span data-ttu-id="b605b-139">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="b605b-139">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="b605b-140">Connect to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="b605b-140">Connect to your IoT hub</span></span>

<span data-ttu-id="b605b-141">Connect to your IoT hub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-141">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="b605b-142">Use iothub-explorer with direct methods</span><span class="sxs-lookup"><span data-stu-id="b605b-142">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="b605b-143">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-143">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="b605b-144">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-144">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="b605b-145">Use iothub-explorer with twin’s desired properties</span><span class="sxs-lookup"><span data-stu-id="b605b-145">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="b605b-146">Set a desired property interval = 3000 by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-146">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin mydevice {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="b605b-147">This property can be read by your device.</span><span class="sxs-lookup"><span data-stu-id="b605b-147">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="b605b-148">Use iothub-explorer with twin’s reported properties</span><span class="sxs-lookup"><span data-stu-id="b605b-148">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="b605b-149">Get the reported properties of the device by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-149">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="b605b-150">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span><span class="sxs-lookup"><span data-stu-id="b605b-150">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="b605b-151">Use iothub-explorer with twin’s tags</span><span class="sxs-lookup"><span data-stu-id="b605b-151">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="b605b-152">Display the tags and properties of the device by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-152">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="b605b-153">Add a field role = temperature&humidity to the device by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-153">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"tags\":{\"role\":\"temperature&humidity\"}}
```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="b605b-154">Use iothub-explorer with Cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="b605b-154">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="b605b-155">Send a "Hello World" message to the device by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-155">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="b605b-156">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span><span class="sxs-lookup"><span data-stu-id="b605b-156">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="b605b-157">Use iothub-explorer with device twins queries</span><span class="sxs-lookup"><span data-stu-id="b605b-157">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="b605b-158">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-158">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="b605b-159">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b605b-159">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="b605b-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="b605b-160">Next steps</span></span>

<span data-ttu-id="b605b-161">You've learned how to use iothub-explorer with various management options.</span><span class="sxs-lookup"><span data-stu-id="b605b-161">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]