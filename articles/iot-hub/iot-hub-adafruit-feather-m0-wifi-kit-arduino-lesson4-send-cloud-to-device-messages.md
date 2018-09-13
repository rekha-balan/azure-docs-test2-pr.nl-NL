---
title: 'Connect Arduino (C) to Azure IoT - Lesson 4: Cloud-to-device | Microsoft Docs'
description: A sample application runs on Adafruit Feather M0 WiFi and monitors incoming messages from your IoT hub. A new gulp task sends messages to Adafruit Feather M0 WiFi from your IoT hub to blink the LED.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino control led from web, arduino control led via web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 803ec6ae163689ee4ece9b6f235c16d18a0ca501
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551037"
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="9b756-105">Run a sample application to receive cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="9b756-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="9b756-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span><span class="sxs-lookup"><span data-stu-id="9b756-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="9b756-107">The sample application monitors incoming messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9b756-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="9b756-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9b756-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="9b756-109">When the sample application receives the messages, it blinks the LED.</span><span class="sxs-lookup"><span data-stu-id="9b756-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="9b756-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9b756-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9b756-111">What you will do</span><span class="sxs-lookup"><span data-stu-id="9b756-111">What you will do</span></span>
* <span data-ttu-id="9b756-112">Connect the sample application to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9b756-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="9b756-113">Deploy and run the sample application.</span><span class="sxs-lookup"><span data-stu-id="9b756-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="9b756-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="9b756-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9b756-115">What you will learn</span><span class="sxs-lookup"><span data-stu-id="9b756-115">What you will learn</span></span>
<span data-ttu-id="9b756-116">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="9b756-116">In this article, you will learn:</span></span>
* <span data-ttu-id="9b756-117">How to monitor incoming messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9b756-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="9b756-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="9b756-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9b756-119">What you need</span><span class="sxs-lookup"><span data-stu-id="9b756-119">What you need</span></span>
* <span data-ttu-id="9b756-120">Your Arduino board, set up for use.</span><span class="sxs-lookup"><span data-stu-id="9b756-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="9b756-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="9b756-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="9b756-122">An IoT hub that is created in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9b756-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="9b756-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="9b756-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="9b756-124">Connect the sample application to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="9b756-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="9b756-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="9b756-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="9b756-126">Open the sample application in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="9b756-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="9b756-127">Notice the `app.ino` file in the `app` subfolder.</span><span class="sxs-lookup"><span data-stu-id="9b756-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="9b756-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9b756-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="9b756-129">The `blinkLED` function blinks the LED.</span><span class="sxs-lookup"><span data-stu-id="9b756-129">The `blinkLED` function blinks the LED.</span></span>

   ![Repo structure in the sample application][repo-structure]

2. <span data-ttu-id="9b756-131">Obtain the serial port of the device with the device discovery cli:</span><span class="sxs-lookup"><span data-stu-id="9b756-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="9b756-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span><span class="sxs-lookup"><span data-stu-id="9b756-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Device discovery][device-discovery]

3. <span data-ttu-id="9b756-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span><span class="sxs-lookup"><span data-stu-id="9b756-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="9b756-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="9b756-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="9b756-137">On macOS or Ubuntu, it will start with `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="9b756-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="9b756-138">Initialize the configuration file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="9b756-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="9b756-139">Make the following replacements in the `config-arduino.json` file:</span><span class="sxs-lookup"><span data-stu-id="9b756-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="9b756-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span><span class="sxs-lookup"><span data-stu-id="9b756-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="9b756-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span><span class="sxs-lookup"><span data-stu-id="9b756-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="9b756-142">The `config-arduino.json` file is in the subfolder of your home folder.</span><span class="sxs-lookup"><span data-stu-id="9b756-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![Contents of the config-arduino.json file][config-arduino-json]

   * <span data-ttu-id="9b756-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="9b756-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="9b756-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span><span class="sxs-lookup"><span data-stu-id="9b756-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="9b756-146">Remove the string if your Wi-Fi doesn't require password.</span><span class="sxs-lookup"><span data-stu-id="9b756-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="9b756-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span><span class="sxs-lookup"><span data-stu-id="9b756-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="9b756-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span><span class="sxs-lookup"><span data-stu-id="9b756-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="9b756-149">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="9b756-149">Deploy and run the sample application</span></span>
<span data-ttu-id="9b756-150">Deploy and run the sample application on your Arduino board by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="9b756-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="9b756-151">The gulp command deploys the sample application to your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="9b756-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="9b756-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9b756-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="9b756-153">After the sample application runs, it starts listening to messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9b756-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="9b756-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="9b756-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="9b756-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="9b756-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="9b756-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="9b756-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="9b756-157">The last one is a "stop" message that stops the application from running.</span><span class="sxs-lookup"><span data-stu-id="9b756-157">The last one is a "stop" message that stops the application from running.</span></span>

![Sample application with gulp command and blink messages][sample-application]

## <a name="summary"></a><span data-ttu-id="9b756-159">Summary</span><span class="sxs-lookup"><span data-stu-id="9b756-159">Summary</span></span>
<span data-ttu-id="9b756-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="9b756-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="9b756-161">The next task is optional: change the on and off behavior of the LED.</span><span class="sxs-lookup"><span data-stu-id="9b756-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b756-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b756-162">Next steps</span></span>
<span data-ttu-id="9b756-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="9b756-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md




