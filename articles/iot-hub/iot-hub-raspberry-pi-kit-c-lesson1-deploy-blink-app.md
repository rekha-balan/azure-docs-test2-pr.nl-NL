---
title: 'Connect Raspberry Pi (C) to Azure IoT - Lesson 1: Deploy app | Microsoft Docs'
description: Clone the sample C application from GitHub, and gulp to deploy this application to your Raspberry Pi 3 board. This sample application blinks the LED connected to the board every two seconds.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: raspberry pi led blink, blink led with raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 397821a14cab03e1e8c23c31693a899ea446c4cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552149"
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="b5d57-105">Create and deploy the blink application</span><span class="sxs-lookup"><span data-stu-id="b5d57-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b5d57-106">What you will do</span><span class="sxs-lookup"><span data-stu-id="b5d57-106">What you will do</span></span>
<span data-ttu-id="b5d57-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="b5d57-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Raspberry Pi 3.</span></span> <span data-ttu-id="b5d57-108">The sample application blinks the LED connected to the board every two seconds.</span><span class="sxs-lookup"><span data-stu-id="b5d57-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="b5d57-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b5d57-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b5d57-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="b5d57-110">What you will learn</span></span>
<span data-ttu-id="b5d57-111">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="b5d57-111">In this article, you will learn:</span></span>

* <span data-ttu-id="b5d57-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span><span class="sxs-lookup"><span data-stu-id="b5d57-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="b5d57-113">How to deploy and run the sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="b5d57-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="b5d57-114">How to deploy and debug applications running remotely on Pi.</span><span class="sxs-lookup"><span data-stu-id="b5d57-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b5d57-115">What you need</span><span class="sxs-lookup"><span data-stu-id="b5d57-115">What you need</span></span>
<span data-ttu-id="b5d57-116">You must have successfully completed the following operations:</span><span class="sxs-lookup"><span data-stu-id="b5d57-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="b5d57-117">Configure your device</span><span class="sxs-lookup"><span data-stu-id="b5d57-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="b5d57-118">Get the tools</span><span class="sxs-lookup"><span data-stu-id="b5d57-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="b5d57-119">Obtain the IP address and host name of Pi</span><span class="sxs-lookup"><span data-stu-id="b5d57-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="b5d57-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="b5d57-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="b5d57-121">You should see an output that is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="b5d57-121">You should see an output that is similar to the following:</span></span>

![Device discovery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="b5d57-123">Take note of the `IP address` and `hostname` of Pi.</span><span class="sxs-lookup"><span data-stu-id="b5d57-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="b5d57-124">You need this information later in this article.</span><span class="sxs-lookup"><span data-stu-id="b5d57-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="b5d57-125">Make sure that Pi is connected to the same network as your computer.</span><span class="sxs-lookup"><span data-stu-id="b5d57-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="b5d57-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span><span class="sxs-lookup"><span data-stu-id="b5d57-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="b5d57-127">Open the sample application</span><span class="sxs-lookup"><span data-stu-id="b5d57-127">Open the sample application</span></span>
<span data-ttu-id="b5d57-128">To open the sample application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="b5d57-128">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="b5d57-129">Clone the sample repository from GitHub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b5d57-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="b5d57-130">Open the sample application in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="b5d57-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Repo structure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="b5d57-132">The `main.c` file in the `app` subfolder is the key source file that contains the code to control the LED.</span><span class="sxs-lookup"><span data-stu-id="b5d57-132">The `main.c` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="b5d57-133">Install application dependencies</span><span class="sxs-lookup"><span data-stu-id="b5d57-133">Install application dependencies</span></span>
<span data-ttu-id="b5d57-134">Install the libraries and other modules you need for the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b5d57-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="b5d57-135">Configure the device connection</span><span class="sxs-lookup"><span data-stu-id="b5d57-135">Configure the device connection</span></span>
<span data-ttu-id="b5d57-136">To configure the device connection, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="b5d57-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="b5d57-137">Generate the device configuration file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b5d57-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="b5d57-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span><span class="sxs-lookup"><span data-stu-id="b5d57-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="b5d57-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="b5d57-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="b5d57-140">Open the device configuration file in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b5d57-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="b5d57-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span><span class="sxs-lookup"><span data-stu-id="b5d57-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="b5d57-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b5d57-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="b5d57-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span><span class="sxs-lookup"><span data-stu-id="b5d57-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="b5d57-145">On Windows these commands are available in **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="b5d57-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="b5d57-146">On MacOS you need to run **brew install ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="b5d57-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="b5d57-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="b5d57-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="b5d57-148">Updated lines should look as below:</span><span class="sxs-lookup"><span data-stu-id="b5d57-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="b5d57-149">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="b5d57-149">Congratulations!</span></span> <span data-ttu-id="b5d57-150">You've successfully created the first sample application for Pi.</span><span class="sxs-lookup"><span data-stu-id="b5d57-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="b5d57-151">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="b5d57-151">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="b5d57-152">Install the Azure IoT Hub SDK on Pi</span><span class="sxs-lookup"><span data-stu-id="b5d57-152">Install the Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="b5d57-153">Install the Azure IoT Hub SDK on Pi by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b5d57-153">Install the Azure IoT Hub SDK on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="b5d57-154">This task might take a few minutes to complete the first time you run it.</span><span class="sxs-lookup"><span data-stu-id="b5d57-154">This task might take a few minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="b5d57-155">Deploy and run the sample app</span><span class="sxs-lookup"><span data-stu-id="b5d57-155">Deploy and run the sample app</span></span>
<span data-ttu-id="b5d57-156">Deploy and run the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="b5d57-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="b5d57-157">Verify the app works</span><span class="sxs-lookup"><span data-stu-id="b5d57-157">Verify the app works</span></span>
<span data-ttu-id="b5d57-158">The sample application terminates automatically after the LED blinks for 20 times.</span><span class="sxs-lookup"><span data-stu-id="b5d57-158">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="b5d57-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="b5d57-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="b5d57-160">![LED blinking](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="b5d57-160">![LED blinking](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="b5d57-161">Summary</span><span class="sxs-lookup"><span data-stu-id="b5d57-161">Summary</span></span>
<span data-ttu-id="b5d57-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="b5d57-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="b5d57-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span><span class="sxs-lookup"><span data-stu-id="b5d57-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5d57-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5d57-164">Next steps</span></span>
[<span data-ttu-id="b5d57-165">Get Azure tools</span><span class="sxs-lookup"><span data-stu-id="b5d57-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)





