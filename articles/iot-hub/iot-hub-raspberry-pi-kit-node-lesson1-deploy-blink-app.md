---
featureFlags:
- usabilla
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 1: Deploy app | Microsoft Docs'
description: Clone the sample Node.js application from GitHub, and gulp to deploy this application to your Raspberry Pi 3 board. This sample application blinks the LED connected to the board every two seconds.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: raspberry pi led blink, blink led with raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ac822ac44ca26c2f9c8b32088b279cd2237b84de
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564019"
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="3d394-105">Create and deploy the blink application</span><span class="sxs-lookup"><span data-stu-id="3d394-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="3d394-106">What you will do</span><span class="sxs-lookup"><span data-stu-id="3d394-106">What you will do</span></span>
<span data-ttu-id="3d394-107">Clone the sample Node.js application from GitHub and use the gulp tool to deploy the sample application to your Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="3d394-107">Clone the sample Node.js application from GitHub and use the gulp tool to deploy the sample application to your Raspberry Pi 3.</span></span> <span data-ttu-id="3d394-108">The sample application blinks the LED connected to the board every two seconds.</span><span class="sxs-lookup"><span data-stu-id="3d394-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="3d394-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3d394-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3d394-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="3d394-110">What you will learn</span></span>
<span data-ttu-id="3d394-111">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="3d394-111">In this article, you will learn:</span></span>

* <span data-ttu-id="3d394-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span><span class="sxs-lookup"><span data-stu-id="3d394-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="3d394-113">How to deploy and run the sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="3d394-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="3d394-114">How to deploy and debug applications running remotely on Pi.</span><span class="sxs-lookup"><span data-stu-id="3d394-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3d394-115">What you need</span><span class="sxs-lookup"><span data-stu-id="3d394-115">What you need</span></span>
<span data-ttu-id="3d394-116">You must have successfully completed the following operations:</span><span class="sxs-lookup"><span data-stu-id="3d394-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="3d394-117">Configure your device</span><span class="sxs-lookup"><span data-stu-id="3d394-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="3d394-118">Get the tools</span><span class="sxs-lookup"><span data-stu-id="3d394-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="3d394-119">Obtain the IP address and host name of Pi</span><span class="sxs-lookup"><span data-stu-id="3d394-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="3d394-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="3d394-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="3d394-121">You should see an output that is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="3d394-121">You should see an output that is similar to the following:</span></span>

![Device discovery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="3d394-123">Take note of the `IP address` and `hostname` of Pi.</span><span class="sxs-lookup"><span data-stu-id="3d394-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="3d394-124">You need this information later in this article.</span><span class="sxs-lookup"><span data-stu-id="3d394-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="3d394-125">Make sure that Pi is connected to the same network as your computer.</span><span class="sxs-lookup"><span data-stu-id="3d394-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="3d394-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span><span class="sxs-lookup"><span data-stu-id="3d394-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="3d394-127">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="3d394-127">Clone the sample application</span></span>
<span data-ttu-id="3d394-128">To open the sample code, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="3d394-128">To open the sample code, follow these steps:</span></span>

1. <span data-ttu-id="3d394-129">Clone the sample repository from GitHub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3d394-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="3d394-130">Open the sample application in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="3d394-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Repo structure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="3d394-132">The `app.js` file in the `app` subfolder is the key source file that contains the code to control the LED.</span><span class="sxs-lookup"><span data-stu-id="3d394-132">The `app.js` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="3d394-133">Install application dependencies</span><span class="sxs-lookup"><span data-stu-id="3d394-133">Install application dependencies</span></span>
<span data-ttu-id="3d394-134">Install the libraries and other modules you need for the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3d394-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="3d394-135">Configure the device connection</span><span class="sxs-lookup"><span data-stu-id="3d394-135">Configure the device connection</span></span>
<span data-ttu-id="3d394-136">To configure the device connection, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="3d394-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="3d394-137">Generate the device configuration file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3d394-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="3d394-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span><span class="sxs-lookup"><span data-stu-id="3d394-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="3d394-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="3d394-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="3d394-140">Open the device configuration file in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3d394-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="3d394-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span><span class="sxs-lookup"><span data-stu-id="3d394-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="3d394-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="3d394-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="3d394-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span><span class="sxs-lookup"><span data-stu-id="3d394-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="3d394-145">On Windows these commands are available in **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="3d394-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="3d394-146">On MacOS you need to run **brew install ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="3d394-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="3d394-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="3d394-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="3d394-148">Updated lines should look as below:</span><span class="sxs-lookup"><span data-stu-id="3d394-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="3d394-149">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="3d394-149">Congratulations!</span></span> <span data-ttu-id="3d394-150">You've successfully created the first sample application for Pi.</span><span class="sxs-lookup"><span data-stu-id="3d394-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="3d394-151">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="3d394-151">Deploy and run the sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="3d394-152">Install Node.js and NPM on Pi</span><span class="sxs-lookup"><span data-stu-id="3d394-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="3d394-153">Install Node.js and NPM on Pi by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3d394-153">Install Node.js and NPM on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="3d394-154">This task might take 10 minutes to complete the first time you run it.</span><span class="sxs-lookup"><span data-stu-id="3d394-154">This task might take 10 minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="3d394-155">Deploy and run the sample app</span><span class="sxs-lookup"><span data-stu-id="3d394-155">Deploy and run the sample app</span></span>
<span data-ttu-id="3d394-156">Deploy and run the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3d394-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="3d394-157">Verify the app works</span><span class="sxs-lookup"><span data-stu-id="3d394-157">Verify the app works</span></span>
<span data-ttu-id="3d394-158">You should now see the LED on Pi blinking every two seconds.</span><span class="sxs-lookup"><span data-stu-id="3d394-158">You should now see the LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="3d394-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span><span class="sxs-lookup"><span data-stu-id="3d394-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="3d394-160">![LED blinking](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="3d394-160">![LED blinking](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="3d394-161">Summary</span><span class="sxs-lookup"><span data-stu-id="3d394-161">Summary</span></span>
<span data-ttu-id="3d394-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span><span class="sxs-lookup"><span data-stu-id="3d394-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="3d394-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span><span class="sxs-lookup"><span data-stu-id="3d394-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d394-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="3d394-164">Next steps</span></span>
[<span data-ttu-id="3d394-165">Get the Azure tools</span><span class="sxs-lookup"><span data-stu-id="3d394-165">Get the Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)





