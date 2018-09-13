---
title: 'SensorTag device & Azure IoT Gateway - Lesson 3: Read messages | Microsoft Docs'
description: Run a sample code on your host computer to read the messages from your IoT hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: data in the cloud, cloud data collection, iot cloud service, iot data
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f5114cce6e535f233b6e8a58966cc5eb2714c5ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550462"
---
# <a name="read-messages-from-your-iot-hub"></a>Read messages from your IoT hub

## <a name="what-you-will-do"></a>What you will do

- Run sample code on your host computer to read messages from your IoT hub.

If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>What you will learn

How to use the gulp tool to read messages from your IoT hub.

## <a name="what-you-need"></a>What you need

- The BLE sample application that you ran successfully in Lesson 3.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Get your IoT hub and device connection strings

The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub. The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.

- List all your IoT hubs in your resource group by running the following command:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.
- Get the IoT hub connection string by running the following command:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}` is the name that you specified in Lesson 2.

## <a name="configure-the-device-connection-for-the-sample-code"></a>Configure the device connection for the sample code

Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer. To do this, follow these steps:

1. Open `config-azure.json` in Visual Studio Code by running the following command in a console window:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Make the following replacements in the `config-azure.json` file:

   ![screenshot of config azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.

## <a name="read-messages-from-your-iot-hub"></a>Read messages from your IoT hub

If you have a TI SensorTag, make sure you have already powered on your SensorTag. Run the gateway sample application and read IoT Hub messages by the following command:

```bash
gulp run --iot-hub
```

The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds. It also spawns a child process to receive the message.

The messages that are being sent and received are all displayed instantly on the same console window in the host machine. The sample application instance will terminate automatically in 40 seconds.

![BLE Sample application with sent and received messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a>Summary

You've run a sample code to read messages from your IoT hub. You're ready to read the messages that are stored in your Azure table storage.

## <a name="next-steps"></a>Next steps
[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)




