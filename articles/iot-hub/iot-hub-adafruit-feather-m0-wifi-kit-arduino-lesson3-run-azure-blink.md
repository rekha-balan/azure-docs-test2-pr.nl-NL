---
title: 'Connect Arduino (C) to Azure IoT - Lesson 3: Run sample | Microsoft Docs'
description: Deploy and run a sample application to Adafruit Feather M0 WiFi that sends messages to your IoT hub and blinks the LED.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot cloud service, arduino send data to cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e0296e003903f08adbecab4ccb05f4e8e05eba02
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564138"
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="4c7d6-104">Run a sample application to send device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="4c7d6-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="4c7d6-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="4c7d6-105">What you will do</span></span>
<span data-ttu-id="4c7d6-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="4c7d6-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="4c7d6-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4c7d6-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="4c7d6-108">What you will learn</span></span>
<span data-ttu-id="4c7d6-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4c7d6-110">What you need</span><span class="sxs-lookup"><span data-stu-id="4c7d6-110">What you need</span></span>
* <span data-ttu-id="4c7d6-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="4c7d6-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="4c7d6-112">Get your IoT hub and device connection strings</span><span class="sxs-lookup"><span data-stu-id="4c7d6-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="4c7d6-113">The device connection string is used to connect your Arduino board to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="4c7d6-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="4c7d6-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="4c7d6-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="4c7d6-117">Get the IoT hub connection string by running the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="4c7d6-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="4c7d6-119">Get the device connection string by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="4c7d6-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="4c7d6-121">Configure the device connection</span><span class="sxs-lookup"><span data-stu-id="4c7d6-121">Configure the device connection</span></span>
<span data-ttu-id="4c7d6-122">To configure the device connection, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="4c7d6-123">Obtain the serial port of the device with the device discovery cli:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="4c7d6-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Device discovery][device-discovery]

2. <span data-ttu-id="4c7d6-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="4c7d6-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="4c7d6-129">On macOS or Ubuntu, it starts with `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="4c7d6-130">Initialize the configuration file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="4c7d6-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="4c7d6-133">Make the following replacements in the `config-arduino.json` file:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="4c7d6-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="4c7d6-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="4c7d6-136">Remove the string if your Wi-Fi doesn't require password.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="4c7d6-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="4c7d6-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4c7d6-139">You don't need `azure_storage_connection_string` in this article.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="4c7d6-140">Keep it as is.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="4c7d6-141">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="4c7d6-141">Deploy and run the sample application</span></span>
<span data-ttu-id="4c7d6-142">Deploy and run the sample application on your Arduino board by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4c7d6-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="4c7d6-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="4c7d6-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="4c7d6-145">Verify that the sample application works</span><span class="sxs-lookup"><span data-stu-id="4c7d6-145">Verify that the sample application works</span></span>
<span data-ttu-id="4c7d6-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="4c7d6-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="4c7d6-148">In addition, each message received by the IoT hub is printed in the console window.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="4c7d6-149">The sample application terminates automatically after sending 20 messages.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-149">The sample application terminates automatically after sending 20 messages.</span></span>

![Sample application with sent and received messages][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="4c7d6-151">Summary</span><span class="sxs-lookup"><span data-stu-id="4c7d6-151">Summary</span></span>
<span data-ttu-id="4c7d6-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="4c7d6-153">You now monitor your messages as they are written to the storage account.</span><span class="sxs-lookup"><span data-stu-id="4c7d6-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c7d6-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c7d6-154">Next steps</span></span>
<span data-ttu-id="4c7d6-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="4c7d6-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md



