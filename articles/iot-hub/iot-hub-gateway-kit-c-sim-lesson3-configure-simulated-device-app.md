---
title: 'Simulated device & Azure IoT Gateway - Lesson 3: Run sample app | Microsoft Docs'
description: Run a simulated device sample app to send temperature data to your IoT hub
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: data to cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fbddbb71e41e83f561cec0deebc870d1cdaaad04
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552123"
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Configure and run a simulated device sample app

## <a name="what-you-will-do"></a>What you will do

- Clone the sample repository.
- Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application. Configure and run the simulated device sample application.

If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>What you will learn

In this article, you will learn:

- How to configure and run the simulated device sample application.

## <a name="what-you-need"></a>What you need

You must have successfully completed

- [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a>Clone the sample repository to the host computer

To clone the sample repository, follow these steps on the host computer:

1. Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.
2. Run the following commands:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a>Configure the simulated device and your NUC

1. Open the configuration file `config.json` in Visual Studio Code by running the following command:

   ```bash
   code config.json
   ```

2. Replace `"has_sensortag": true` with `"has_sensortag": false`

   ![Config you don't have a TI SensorTag device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Initialize the configuration file by running the following commands:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Open `config-gateway.json` in Visual Studio Code by running the following command:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.
   ![screenshot of config gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a>Get the connection string of your IoT hub logical device

To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}` is the IoT hub name that you used. Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a>Configure the simulated device cloud upload sample application

To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:

1. Open `config-sensortag.json` in Visual Studio Code by running the following command:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![screenshot of config sensortag](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Make the following replacements in the code:
   - Replace `[IoT hub name]` with the IoT hub name.
   - Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.

3. Run the application.

   Deploy and run the application by running the following command:

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a>Verify the sample application works

You should now see output like the following:

![simulated device sample application output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

The application sends temperature data to your IoT hub, which lasts for 40 seconds.

## <a name="summary"></a>Summary

You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.

## <a name="next-steps"></a>Next steps
[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)



