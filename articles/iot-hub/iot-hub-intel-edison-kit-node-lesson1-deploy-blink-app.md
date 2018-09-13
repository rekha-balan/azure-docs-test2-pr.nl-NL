---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 1: Deploy app | Microsoft Docs'
description: Clone the sample C application from GitHub, and run gulp to deploy this application to your Intel Edison board. This sample application blinks the LED connected to the board every two seconds.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino led projects, arduino led blink, arduino led blink code, arduino blink program, arduino blink example
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1930bd7e17280a5855f63c5c00b47ca668cd4ed6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661135"
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="ea98c-105">Create and deploy the blink application</span><span class="sxs-lookup"><span data-stu-id="ea98c-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="ea98c-106">What you will do</span><span class="sxs-lookup"><span data-stu-id="ea98c-106">What you will do</span></span>
<span data-ttu-id="ea98c-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="ea98c-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="ea98c-108">The sample application blinks the LED connected to the board every two seconds.</span><span class="sxs-lookup"><span data-stu-id="ea98c-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="ea98c-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="ea98c-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ea98c-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="ea98c-110">What you will learn</span></span>
* <span data-ttu-id="ea98c-111">How to deploy and run the sample application on Edison.</span><span class="sxs-lookup"><span data-stu-id="ea98c-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ea98c-112">What you need</span><span class="sxs-lookup"><span data-stu-id="ea98c-112">What you need</span></span>
<span data-ttu-id="ea98c-113">You must have successfully completed the following operations:</span><span class="sxs-lookup"><span data-stu-id="ea98c-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="ea98c-114">[Configure your device][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="ea98c-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="ea98c-115">[Get the tools][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="ea98c-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="ea98c-116">Open the sample application</span><span class="sxs-lookup"><span data-stu-id="ea98c-116">Open the sample application</span></span>
<span data-ttu-id="ea98c-117">To open the sample application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ea98c-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="ea98c-118">Clone the sample repository from GitHub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="ea98c-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="ea98c-119">Open the sample application in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="ea98c-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Repo structure][repo-structure]

<span data-ttu-id="ea98c-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span><span class="sxs-lookup"><span data-stu-id="ea98c-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="ea98c-122">Install application dependencies</span><span class="sxs-lookup"><span data-stu-id="ea98c-122">Install application dependencies</span></span>
<span data-ttu-id="ea98c-123">Install the libraries and other modules you need for the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="ea98c-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="ea98c-124">Configure the device connection</span><span class="sxs-lookup"><span data-stu-id="ea98c-124">Configure the device connection</span></span>
<span data-ttu-id="ea98c-125">To configure the device connection, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ea98c-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="ea98c-126">Generate the device configuration file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="ea98c-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="ea98c-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span><span class="sxs-lookup"><span data-stu-id="ea98c-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="ea98c-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="ea98c-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="ea98c-129">Open the device configuration file in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="ea98c-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="ea98c-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span><span class="sxs-lookup"><span data-stu-id="ea98c-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="ea98c-132">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="ea98c-132">Congratulations!</span></span> <span data-ttu-id="ea98c-133">You've successfully created the first sample application for Edison.</span><span class="sxs-lookup"><span data-stu-id="ea98c-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="ea98c-134">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="ea98c-134">Deploy and run the sample application</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="ea98c-135">Deploy and run the sample app</span><span class="sxs-lookup"><span data-stu-id="ea98c-135">Deploy and run the sample app</span></span>
<span data-ttu-id="ea98c-136">Deploy and run the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="ea98c-136">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="ea98c-137">Verify the app works</span><span class="sxs-lookup"><span data-stu-id="ea98c-137">Verify the app works</span></span>
<span data-ttu-id="ea98c-138">The sample application terminates automatically after the LED blinks for 20 times.</span><span class="sxs-lookup"><span data-stu-id="ea98c-138">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="ea98c-139">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="ea98c-139">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![LED blinking][led-blinking]

## <a name="summary"></a><span data-ttu-id="ea98c-141">Summary</span><span class="sxs-lookup"><span data-stu-id="ea98c-141">Summary</span></span>
<span data-ttu-id="ea98c-142">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="ea98c-142">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="ea98c-143">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span><span class="sxs-lookup"><span data-stu-id="ea98c-143">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea98c-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea98c-144">Next steps</span></span>
<span data-ttu-id="ea98c-145">[Get the Azure tools][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="ea98c-145">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md



