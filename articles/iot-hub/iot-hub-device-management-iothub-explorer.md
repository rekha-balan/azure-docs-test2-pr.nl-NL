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
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>Use iothub-explorer for Azure IoT Hub device management

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry. It comes with management options that you can use to perform various tasks.

| Management option          | Task                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Direct methods             | Make a device act such as starting or stopping sending messages or rebooting the device.                                        |
| Twin desired properties    | Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.         |
| Twin reported properties   | Get the reported state of a device. For example, the device reports the LED is blinking now.                                    |
| Twin tags                  | Store device-specific metadata in the cloud. For example, the deployment location of a vending machine.                         |
| Cloud-to-device messages   | Send notifications to a device. For example, "It is very likely to rain today. Don't forget to bring an umbrella."              |
| Device twin queries        | Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use. |

For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> Device twins are JSON documents that store device state information (metadata, configurations, and conditions). IoT Hub persists a device twin for each device that connects to it. For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>What you learn

You learn using iothub-explorer with various management options.

## <a name="what-you-do"></a>What you do

Run iothub-explorer with various management options.

## <a name="what-you-need"></a>What you need

- Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:
  - An active Azure subscription.
  - An Azure IoT hub under your subscription.
  - A client application that sends messages to your Azure IoT hub.
- iothub-explorer. ([Install iothub-explorer](https://github.com/azure/iothub-explorer))

## <a name="connect-to-your-iot-hub"></a>Connect to your IoT hub

Connect to your IoT hub by running the following command:

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>Use iothub-explorer with direct methods

Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:

```bash
iothub-explorer device-method <your device Id> start
```

Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>Use iothub-explorer with twin’s desired properties

Set a desired property interval = 3000 by running the following command:

```bash
iothub-explorer update-twin mydevice {\"properties\":{\"desired\":{\"interval\":3000}}}
```

This property can be read by your device.

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>Use iothub-explorer with twin’s reported properties

Get the reported properties of the device by running the following command:

```bash
iothub-explorer get-twin <your device id>
```

One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.

## <a name="use-iothub-explorer-with-twins-tags"></a>Use iothub-explorer with twin’s tags

Display the tags and properties of the device by running the following command:

```bash
iothub-explorer get-twin <your device id>
```

Add a field role = temperature&humidity to the device by running the following command:

```bash
iothub-explorer update-twin <your device id> {\"tags\":{\"role\":\"temperature&humidity\"}}
```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>Use iothub-explorer with Cloud-to-device messages

Send a "Hello World" message to the device by running the following command:

```bash
iothub-explorer send <device-id> "Hello World"
```

See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.

## <a name="use-iothub-explorer-with-device-twins-queries"></a>Use iothub-explorer with device twins queries

Query devices with a tag of role = 'temperature&humidity' by running the following command:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Next steps

You've learned how to use iothub-explorer with various management options.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]