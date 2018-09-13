---
featureFlags:
- usabilla
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 4: Cloud-to-device | Microsoft Docs'
description: The sample application runs on Pi and monitors incoming messages from your IoT hub. A new gulp task sends messages to Pi from your IoT hub to blink the LED.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: cloud to device, message from cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 225276c15a3be7bc749af39a2fcbec76a969a264
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661126"
---
# <a name="run-the-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="e37b9-105">Run the sample application to receive cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="e37b9-105">Run the sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="e37b9-106">In this article, you deploy a sample application on Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="e37b9-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="e37b9-107">The sample application monitors incoming messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e37b9-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="e37b9-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e37b9-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="e37b9-109">When the sample application receives the messages, it blinks the LED.</span><span class="sxs-lookup"><span data-stu-id="e37b9-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="e37b9-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e37b9-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e37b9-111">What you will do</span><span class="sxs-lookup"><span data-stu-id="e37b9-111">What you will do</span></span>
* <span data-ttu-id="e37b9-112">Connect the sample application to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e37b9-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="e37b9-113">Deploy and run the sample application.</span><span class="sxs-lookup"><span data-stu-id="e37b9-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="e37b9-114">Send messages from your IoT hub to Pi to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="e37b9-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e37b9-115">What you will learn</span><span class="sxs-lookup"><span data-stu-id="e37b9-115">What you will learn</span></span>
<span data-ttu-id="e37b9-116">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="e37b9-116">In this article, you will learn:</span></span>
* <span data-ttu-id="e37b9-117">How to monitor incoming messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="e37b9-117">How to monitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="e37b9-118">How to send cloud-to-device messages from your IoT hub to Pi.</span><span class="sxs-lookup"><span data-stu-id="e37b9-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e37b9-119">What you need</span><span class="sxs-lookup"><span data-stu-id="e37b9-119">What you need</span></span>
* <span data-ttu-id="e37b9-120">Raspberry Pi 3, set up for use.</span><span class="sxs-lookup"><span data-stu-id="e37b9-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="e37b9-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="e37b9-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="e37b9-122">An IoT hub that is created in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e37b9-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="e37b9-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e37b9-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="e37b9-124">Connect the sample application to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="e37b9-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="e37b9-125">Make sure that you're in the repo folder `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="e37b9-125">Make sure that you're in the repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="e37b9-126">Open the sample application in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="e37b9-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="e37b9-127">Notice the `app.js` file in the `app` subfolder.</span><span class="sxs-lookup"><span data-stu-id="e37b9-127">Notice the `app.js` file in the `app` subfolder.</span></span> <span data-ttu-id="e37b9-128">The `app.js` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e37b9-128">The `app.js` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="e37b9-129">The `blinkLED` function blinks the LED.</span><span class="sxs-lookup"><span data-stu-id="e37b9-129">The `blinkLED` function blinks the LED.</span></span>
   
   ![Repo structure in the sample application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="e37b9-131">Initialize the configuration file by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="e37b9-131">Initialize the configuration file by using the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="e37b9-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to the task of deploying and running the sample application.</span><span class="sxs-lookup"><span data-stu-id="e37b9-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to the task of deploying and running the sample application.</span></span> <span data-ttu-id="e37b9-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span><span class="sxs-lookup"><span data-stu-id="e37b9-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="e37b9-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span><span class="sxs-lookup"><span data-stu-id="e37b9-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>
   
   ![Contents of the config-raspberrypi.json file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="e37b9-136">Replace **[device hostname or IP address]** with the IP address of Pi or the host name that you get by running the `devdisco list --eth` command.</span><span class="sxs-lookup"><span data-stu-id="e37b9-136">Replace **[device hostname or IP address]** with the IP address of Pi or the host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="e37b9-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span><span class="sxs-lookup"><span data-stu-id="e37b9-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="e37b9-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span><span class="sxs-lookup"><span data-stu-id="e37b9-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="e37b9-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span><span class="sxs-lookup"><span data-stu-id="e37b9-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="e37b9-140">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="e37b9-140">Deploy and run the sample application</span></span>
<span data-ttu-id="e37b9-141">Deploy and run the sample application on Pi by running the following command:</span><span class="sxs-lookup"><span data-stu-id="e37b9-141">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="e37b9-142">The command deploys the sample application to Pi.</span><span class="sxs-lookup"><span data-stu-id="e37b9-142">The command deploys the sample application to Pi.</span></span> <span data-ttu-id="e37b9-143">Then, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e37b9-143">Then, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="e37b9-144">After the sample application runs, it starts listening to messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e37b9-144">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="e37b9-145">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span><span class="sxs-lookup"><span data-stu-id="e37b9-145">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="e37b9-146">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="e37b9-146">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="e37b9-147">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span><span class="sxs-lookup"><span data-stu-id="e37b9-147">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="e37b9-148">The last one is a "stop" message that tells the application to stop running.</span><span class="sxs-lookup"><span data-stu-id="e37b9-148">The last one is a "stop" message that tells the application to stop running.</span></span>

![Sample application with gulp command and blink messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="e37b9-150">Summary</span><span class="sxs-lookup"><span data-stu-id="e37b9-150">Summary</span></span>
<span data-ttu-id="e37b9-151">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="e37b9-151">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="e37b9-152">The next task is optional: change the on and off behavior of the LED.</span><span class="sxs-lookup"><span data-stu-id="e37b9-152">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e37b9-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="e37b9-153">Next steps</span></span>
[<span data-ttu-id="e37b9-154">Change the on and off behavior of the LED</span><span class="sxs-lookup"><span data-stu-id="e37b9-154">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)




