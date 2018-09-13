---
title: 'Connect Raspberry Pi (C) to Azure IoT - Lesson 4: Cloud-to-device | Microsoft Docs'
description: A sample application runs on Pi and monitors incoming messages from your IoT hub. A new gulp task sends messages to Pi from your IoT hub to blink the LED.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: cloud to device, message from cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3440d570d86a8661520592c2c88b6a1c45f36200
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563916"
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="bc4bb-105">Run a sample application to receive cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="bc4bb-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="bc4bb-106">In this article, you deploy a sample application on Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="bc4bb-107">The sample application monitors incoming messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="bc4bb-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="bc4bb-109">When the sample application receives the messages, it blinks the LED.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="bc4bb-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bc4bb-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="bc4bb-111">What you will do</span><span class="sxs-lookup"><span data-stu-id="bc4bb-111">What you will do</span></span>
* <span data-ttu-id="bc4bb-112">Connect the sample application to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="bc4bb-113">Deploy and run the sample application.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="bc4bb-114">Send messages from your IoT hub to Pi to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bc4bb-115">What you will learn</span><span class="sxs-lookup"><span data-stu-id="bc4bb-115">What you will learn</span></span>
<span data-ttu-id="bc4bb-116">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="bc4bb-116">In this article, you will learn:</span></span>
* <span data-ttu-id="bc4bb-117">How to monitor incoming messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="bc4bb-118">How to send cloud-to-device messages from your IoT hub to Pi.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bc4bb-119">What you need</span><span class="sxs-lookup"><span data-stu-id="bc4bb-119">What you need</span></span>
* <span data-ttu-id="bc4bb-120">Raspberry Pi 3, set up for use.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="bc4bb-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="bc4bb-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="bc4bb-122">An IoT hub that is created in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="bc4bb-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="bc4bb-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="bc4bb-124">Connect the sample application to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="bc4bb-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="bc4bb-125">Make sure that you're in the repo folder `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-125">Make sure that you're in the repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="bc4bb-126">Open the sample application in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="bc4bb-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="bc4bb-127">Notice the `app.c` file in the `app` subfolder.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-127">Notice the `app.c` file in the `app` subfolder.</span></span> <span data-ttu-id="bc4bb-128">The `app.c` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-128">The `app.c` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="bc4bb-129">The `blinkLED` function blinks the LED.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-129">The `blinkLED` function blinks the LED.</span></span>

   ![Repo structure in the sample application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="bc4bb-131">Initialize the configuration file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="bc4bb-131">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="bc4bb-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to step to the task of deploying and running the sample application.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="bc4bb-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="bc4bb-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>

   ![Contents of the config-raspberrypi.json file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="bc4bb-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running the `devdisco list --eth` command.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="bc4bb-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="bc4bb-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="bc4bb-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="bc4bb-140">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="bc4bb-140">Deploy and run the sample application</span></span>
<span data-ttu-id="bc4bb-141">Deploy and run the sample application on Pi by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="bc4bb-141">Deploy and run the sample application on Pi by running the following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="bc4bb-142">The gulp command runs the install-tools task first.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-142">The gulp command runs the install-tools task first.</span></span> <span data-ttu-id="bc4bb-143">Then it deploys the sample application to Pi.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-143">Then it deploys the sample application to Pi.</span></span> <span data-ttu-id="bc4bb-144">Finally, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-144">Finally, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="bc4bb-145">After the sample application runs, it starts listening to messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-145">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="bc4bb-146">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-146">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="bc4bb-147">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-147">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="bc4bb-148">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-148">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="bc4bb-149">The last one is a "stop" message that stops the application from running.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-149">The last one is a "stop" message that stops the application from running.</span></span>

![Sample application with gulp command and blink messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="bc4bb-151">Summary</span><span class="sxs-lookup"><span data-stu-id="bc4bb-151">Summary</span></span>
<span data-ttu-id="bc4bb-152">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-152">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="bc4bb-153">The next task is optional: change the on and off behavior of the LED.</span><span class="sxs-lookup"><span data-stu-id="bc4bb-153">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc4bb-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc4bb-154">Next steps</span></span>
[<span data-ttu-id="bc4bb-155">Change the on and off behavior of the LED</span><span class="sxs-lookup"><span data-stu-id="bc4bb-155">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)



