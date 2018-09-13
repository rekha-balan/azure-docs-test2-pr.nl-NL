---
title: Manage Azure IoT Hub cloud device messaging with iothub-explorer | Microsoft Docs
description: Learn how to use the iothub-explorer CLI tool to monitor device to cloud (D2C) messages and send cloud to device (C2D) messages in Azure IoT Hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iothub explorer, cloud device messaging, iot hub cloud to device, cloud to device messaging
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: xshi
ms.openlocfilehash: 94e71fd5cb3a59aac1f2b634c5d70432a65456f9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661058"
---
# <a name="use-iothub-explorer-to-send-and-receive-messages-between-your-device-and-iot-hub"></a>Use iothub-explorer to send and receive messages between your device and IoT Hub

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier. This tutorial focuses on how to use iothub-explorer to send and receive messages between your device and your IoT hub.

## <a name="what-you-will-learn"></a>What you will learn

You learn how to use iothub-explorer to monitor device-to-cloud messages and to send cloud-to-device messages. Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub. Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.

## <a name="what-you-will-do"></a>What you will do

- Use iothub-explorer to monitor device-to-cloud messages.
- Use iothub-explorer to send cloud-to-device messages.

## <a name="what-you-need"></a>What you need

- Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:
  - An active Azure subscription.
  - An Azure IoT hub under your subscription.
  - A client application that sends messages to your Azure IoT hub.
- iothub-explorer. ([Install iothub-explorer](https://github.com/azure/iothub-explorer))

## <a name="monitor-device-to-cloud-messages"></a>Monitor device-to-cloud messages

To monitor messages that are sent from your device to your IoT hub, follow these steps:

1. Open a console window.
1. Run the following command:

   ```bash
   iothub-explorer monitor-events <device-id> --login <IoTHubConnectionString>
   ```

   > [!Note]
   > Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub. Make sure you've finished the previous tutorial.

## <a name="send-cloud-to-device-messages"></a>Send cloud-to-device messages

To send a message from your IoT hub to your device, follow these steps:

1. Open a console window.
1. Start a session on your IoT hub by running the following command:

   ```bash
   iothub-explorer login <IoTHubConnectionString>
   ```

1. Send a message to your device by running the following command:

   ```bash
   iothub-explorer send <device-id> <message>
   ```

The command blinks the LED that is connected to your device and sends the message to your device.

> [!Note]
> There is no need for the device to send a separate ack command back to your IoT hub upon receiving the message.

## <a name="next-steps"></a>Next steps

You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]