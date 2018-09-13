---
title: 'Connect Intel Edison (C) to Azure IoT - Lesson 1: Deploy application | Microsoft Docs'
description: Clone the sample C application from GitHub, and run gulp to deploy this application to your Intel Edison board. This sample application blinks the LED connected to the board every two seconds.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino led projects, arduino led blink, arduino led blink code, arduino blink program, arduino blink example
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 910600eb8a45688f8763e8238c348850ec49f043
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550760"
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="f2fce-105">Create and deploy the blink application</span><span class="sxs-lookup"><span data-stu-id="f2fce-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="f2fce-106">What you will do</span><span class="sxs-lookup"><span data-stu-id="f2fce-106">What you will do</span></span>
<span data-ttu-id="f2fce-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="f2fce-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="f2fce-108">The sample application blinks the LED connected to the board every two seconds.</span><span class="sxs-lookup"><span data-stu-id="f2fce-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="f2fce-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="f2fce-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f2fce-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="f2fce-110">What you will learn</span></span>
* <span data-ttu-id="f2fce-111">How to deploy and run the sample application on Edison.</span><span class="sxs-lookup"><span data-stu-id="f2fce-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f2fce-112">What you need</span><span class="sxs-lookup"><span data-stu-id="f2fce-112">What you need</span></span>
<span data-ttu-id="f2fce-113">You must have successfully completed the following operations:</span><span class="sxs-lookup"><span data-stu-id="f2fce-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="f2fce-114">[Configure your device][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="f2fce-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="f2fce-115">[Get the tools][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="f2fce-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="f2fce-116">Open the sample application</span><span class="sxs-lookup"><span data-stu-id="f2fce-116">Open the sample application</span></span>
<span data-ttu-id="f2fce-117">To open the sample application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f2fce-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="f2fce-118">Clone the sample repository from GitHub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="f2fce-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="f2fce-119">Open the sample application in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="f2fce-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Repo structure][repo-structure]

<span data-ttu-id="f2fce-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span><span class="sxs-lookup"><span data-stu-id="f2fce-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="f2fce-122">Install application dependencies</span><span class="sxs-lookup"><span data-stu-id="f2fce-122">Install application dependencies</span></span>
<span data-ttu-id="f2fce-123">Install the libraries and other modules you need for the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="f2fce-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="f2fce-124">Configure the device connection</span><span class="sxs-lookup"><span data-stu-id="f2fce-124">Configure the device connection</span></span>
<span data-ttu-id="f2fce-125">To configure the device connection, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f2fce-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="f2fce-126">Generate the device configuration file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="f2fce-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="f2fce-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span><span class="sxs-lookup"><span data-stu-id="f2fce-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="f2fce-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="f2fce-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="f2fce-129">Open the device configuration file in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="f2fce-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="f2fce-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span><span class="sxs-lookup"><span data-stu-id="f2fce-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="f2fce-132">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="f2fce-132">Congratulations!</span></span> <span data-ttu-id="f2fce-133">You've successfully created the first sample application for Edison.</span><span class="sxs-lookup"><span data-stu-id="f2fce-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="f2fce-134">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="f2fce-134">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="f2fce-135">Install the Azure IoT Hub SDK on Edison</span><span class="sxs-lookup"><span data-stu-id="f2fce-135">Install the Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="f2fce-136">Install the Azure IoT Hub SDK on Edison by running the following command:</span><span class="sxs-lookup"><span data-stu-id="f2fce-136">Install the Azure IoT Hub SDK on Edison by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="f2fce-137">This task might take a long time to complete, depending on your network connection.</span><span class="sxs-lookup"><span data-stu-id="f2fce-137">This task might take a long time to complete, depending on your network connection.</span></span> <span data-ttu-id="f2fce-138">It needs to be run only once for one Edison.</span><span class="sxs-lookup"><span data-stu-id="f2fce-138">It needs to be run only once for one Edison.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="f2fce-139">Deploy and run the sample app</span><span class="sxs-lookup"><span data-stu-id="f2fce-139">Deploy and run the sample app</span></span>
<span data-ttu-id="f2fce-140">Deploy and run the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="f2fce-140">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="f2fce-141">Verify the app works</span><span class="sxs-lookup"><span data-stu-id="f2fce-141">Verify the app works</span></span>
<span data-ttu-id="f2fce-142">The sample application terminates automatically after the LED blinks for 20 times.</span><span class="sxs-lookup"><span data-stu-id="f2fce-142">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="f2fce-143">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="f2fce-143">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![LED blinking][led-blinking]

## <a name="summary"></a><span data-ttu-id="f2fce-145">Summary</span><span class="sxs-lookup"><span data-stu-id="f2fce-145">Summary</span></span>
<span data-ttu-id="f2fce-146">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="f2fce-146">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="f2fce-147">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span><span class="sxs-lookup"><span data-stu-id="f2fce-147">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2fce-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2fce-148">Next steps</span></span>
<span data-ttu-id="f2fce-149">[Get the Azure tools][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="f2fce-149">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md



