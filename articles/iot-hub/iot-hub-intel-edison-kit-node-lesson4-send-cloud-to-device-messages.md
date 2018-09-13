---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 4: Receive messages | Microsoft Docs'
description: A sample application runs on Edison and monitors incoming messages from your IoT hub. A new gulp task sends messages to Edison from your IoT hub to blink the LED.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino control led from web, arduino control led via web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: da2bbcc8990ee343b09f030c9776700b45516dda
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552399"
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="4fbfa-105">Run a sample application to receive cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="4fbfa-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="4fbfa-106">In this article, you deploy a sample application on Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="4fbfa-107">The sample application monitors incoming messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="4fbfa-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="4fbfa-109">When the sample application receives the messages, it blinks the LED.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="4fbfa-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="4fbfa-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4fbfa-111">What you will do</span><span class="sxs-lookup"><span data-stu-id="4fbfa-111">What you will do</span></span>
* <span data-ttu-id="4fbfa-112">Connect the sample application to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="4fbfa-113">Deploy and run the sample application.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="4fbfa-114">Send messages from your IoT hub to Edison to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4fbfa-115">What you will learn</span><span class="sxs-lookup"><span data-stu-id="4fbfa-115">What you will learn</span></span>
<span data-ttu-id="4fbfa-116">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="4fbfa-116">In this article, you will learn:</span></span>
* <span data-ttu-id="4fbfa-117">How to monitor incoming messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="4fbfa-118">How to send cloud-to-device messages from your IoT hub to Edison.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4fbfa-119">What you need</span><span class="sxs-lookup"><span data-stu-id="4fbfa-119">What you need</span></span>
* <span data-ttu-id="4fbfa-120">Intel Edison, set up for use.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="4fbfa-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="4fbfa-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="4fbfa-122">An IoT hub that is created in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="4fbfa-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="4fbfa-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="4fbfa-124">Connect the sample application to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="4fbfa-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="4fbfa-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="4fbfa-126">Open the sample application in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="4fbfa-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="4fbfa-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="4fbfa-128">The `blinkLED` function blinks the LED.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-128">The `blinkLED` function blinks the LED.</span></span>

   ![Repo structure in the sample application][repo-structure]
2. <span data-ttu-id="4fbfa-130">Initialize the configuration file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="4fbfa-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="4fbfa-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="4fbfa-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="4fbfa-133">The `config-edison.json` file is in the subfolder of your home folder.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![Contents of the config-edison.json file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="4fbfa-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="4fbfa-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="4fbfa-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="4fbfa-138">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="4fbfa-138">Deploy and run the sample application</span></span>
<span data-ttu-id="4fbfa-139">Deploy and run the sample application on Edison by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="4fbfa-139">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="4fbfa-140">The gulp command deploys the sample application to Edison.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-140">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="4fbfa-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="4fbfa-142">After the sample application runs, it starts listening to messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-142">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="4fbfa-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="4fbfa-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="4fbfa-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="4fbfa-146">The last one is a "stop" message that stops the application from running.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-146">The last one is a "stop" message that stops the application from running.</span></span>

![Sample application with gulp command and blink messages][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="4fbfa-148">Summary</span><span class="sxs-lookup"><span data-stu-id="4fbfa-148">Summary</span></span>
<span data-ttu-id="4fbfa-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="4fbfa-150">The next task is optional: change the on and off behavior of the LED.</span><span class="sxs-lookup"><span data-stu-id="4fbfa-150">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fbfa-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="4fbfa-151">Next steps</span></span>
<span data-ttu-id="4fbfa-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="4fbfa-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md


