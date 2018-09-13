---
title: Raspberry Pi to cloud (Node.js) - Connect Raspberry Pi to Azure IoT Hub | Microsoft Docs
description: Connect Raspberry Pi to Azure IoT Hub for Raspberry Pi to send data to the Azure cloud.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure iot raspberry pi, raspberry pi iot hub, raspberry pi send data to cloud, raspberry pi to cloud
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/14/2017
ms.author: xshi
ms.openlocfilehash: f1372898c78c09b69370dd76549c3a3ff47f66bb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551319"
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="afa9c-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="afa9c-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="afa9c-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span><span class="sxs-lookup"><span data-stu-id="afa9c-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="afa9c-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="afa9c-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="afa9c-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="afa9c-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="afa9c-108">Don't have a kit yet?</span><span class="sxs-lookup"><span data-stu-id="afa9c-108">Don't have a kit yet?</span></span> <span data-ttu-id="afa9c-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="afa9c-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="afa9c-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="afa9c-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="afa9c-111">What you do</span><span class="sxs-lookup"><span data-stu-id="afa9c-111">What you do</span></span>

* <span data-ttu-id="afa9c-112">Setup Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="afa9c-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="afa9c-113">Create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="afa9c-113">Create an IoT hub.</span></span>
* <span data-ttu-id="afa9c-114">Register a device for Pi in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="afa9c-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="afa9c-115">Run a sample application on Pi to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="afa9c-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="afa9c-116">Connect Raspberry Pi to an IoT hub that you create.</span><span class="sxs-lookup"><span data-stu-id="afa9c-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="afa9c-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span><span class="sxs-lookup"><span data-stu-id="afa9c-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="afa9c-118">Finally, you send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="afa9c-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="afa9c-119">What you learn</span><span class="sxs-lookup"><span data-stu-id="afa9c-119">What you learn</span></span>

* <span data-ttu-id="afa9c-120">How to create an Azure IoT hub and get your new device connection string.</span><span class="sxs-lookup"><span data-stu-id="afa9c-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="afa9c-121">How to connect Pi with a BME280 sensor.</span><span class="sxs-lookup"><span data-stu-id="afa9c-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="afa9c-122">How to collect sensor data by running a sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="afa9c-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="afa9c-123">How to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="afa9c-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="afa9c-124">What you need</span><span class="sxs-lookup"><span data-stu-id="afa9c-124">What you need</span></span>

![What you need](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="afa9c-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span><span class="sxs-lookup"><span data-stu-id="afa9c-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="afa9c-127">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="afa9c-127">An active Azure subscription.</span></span> <span data-ttu-id="afa9c-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="afa9c-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="afa9c-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span><span class="sxs-lookup"><span data-stu-id="afa9c-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="afa9c-130">A Mac or a PC that is running Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="afa9c-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="afa9c-131">An Internet connection.</span><span class="sxs-lookup"><span data-stu-id="afa9c-131">An Internet connection.</span></span>
* <span data-ttu-id="afa9c-132">A 16 GB or above microSD card.</span><span class="sxs-lookup"><span data-stu-id="afa9c-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="afa9c-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span><span class="sxs-lookup"><span data-stu-id="afa9c-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="afa9c-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span><span class="sxs-lookup"><span data-stu-id="afa9c-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="afa9c-135">The following items are optional:</span><span class="sxs-lookup"><span data-stu-id="afa9c-135">The following items are optional:</span></span>

* <span data-ttu-id="afa9c-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span><span class="sxs-lookup"><span data-stu-id="afa9c-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="afa9c-137">A breadboard.</span><span class="sxs-lookup"><span data-stu-id="afa9c-137">A breadboard.</span></span>
* <span data-ttu-id="afa9c-138">6 F/M jumper wires.</span><span class="sxs-lookup"><span data-stu-id="afa9c-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="afa9c-139">A diffused 10-mm LED.</span><span class="sxs-lookup"><span data-stu-id="afa9c-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="afa9c-140">These items are optional because the code sample support simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="afa9c-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="afa9c-141">Setup Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="afa9c-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="afa9c-142">Install the Raspbian operating system for Pi</span><span class="sxs-lookup"><span data-stu-id="afa9c-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="afa9c-143">Prepare the microSD card for installation of the Raspbian image.</span><span class="sxs-lookup"><span data-stu-id="afa9c-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="afa9c-144">Download Raspbian.</span><span class="sxs-lookup"><span data-stu-id="afa9c-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="afa9c-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span><span class="sxs-lookup"><span data-stu-id="afa9c-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="afa9c-146">Extract the Raspbian image to a folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="afa9c-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="afa9c-147">Install Raspbian to the microSD card.</span><span class="sxs-lookup"><span data-stu-id="afa9c-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="afa9c-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="afa9c-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="afa9c-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span><span class="sxs-lookup"><span data-stu-id="afa9c-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="afa9c-150">Select the microSD card drive.</span><span class="sxs-lookup"><span data-stu-id="afa9c-150">Select the microSD card drive.</span></span> <span data-ttu-id="afa9c-151">Note that Etcher may have already selected the correct drive.</span><span class="sxs-lookup"><span data-stu-id="afa9c-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="afa9c-152">Click Flash to install Raspbian to the microSD card.</span><span class="sxs-lookup"><span data-stu-id="afa9c-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="afa9c-153">Remove the microSD card from your computer when installation is complete.</span><span class="sxs-lookup"><span data-stu-id="afa9c-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="afa9c-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span><span class="sxs-lookup"><span data-stu-id="afa9c-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="afa9c-155">Insert the microSD card into Pi.</span><span class="sxs-lookup"><span data-stu-id="afa9c-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="afa9c-156">Enable SSH and I2C</span><span class="sxs-lookup"><span data-stu-id="afa9c-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="afa9c-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span><span class="sxs-lookup"><span data-stu-id="afa9c-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="afa9c-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span><span class="sxs-lookup"><span data-stu-id="afa9c-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![The Raspbian Preferences menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="afa9c-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="afa9c-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span>

   ![Enable I2C and SSH on Raspberry Pi](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="afa9c-162">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2).</span><span class="sxs-lookup"><span data-stu-id="afa9c-162">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="afa9c-163">Connect the sensor to Pi</span><span class="sxs-lookup"><span data-stu-id="afa9c-163">Connect the sensor to Pi</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="afa9c-164">Connect the sensor to Pi</span><span class="sxs-lookup"><span data-stu-id="afa9c-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="afa9c-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span><span class="sxs-lookup"><span data-stu-id="afa9c-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="afa9c-166">If you don’t have the sensor, skip this section.</span><span class="sxs-lookup"><span data-stu-id="afa9c-166">If you don’t have the sensor, skip this section.</span></span>

![The Raspberry Pi and sensor connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)


<span data-ttu-id="afa9c-168">For sensor pins, use the following wiring:</span><span class="sxs-lookup"><span data-stu-id="afa9c-168">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="afa9c-169">Start (Sensor & LED)</span><span class="sxs-lookup"><span data-stu-id="afa9c-169">Start (Sensor & LED)</span></span>     | <span data-ttu-id="afa9c-170">End (Board)</span><span class="sxs-lookup"><span data-stu-id="afa9c-170">End (Board)</span></span>            | <span data-ttu-id="afa9c-171">Cable Color</span><span class="sxs-lookup"><span data-stu-id="afa9c-171">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="afa9c-172">VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="afa9c-172">VDD (Pin 5G)</span></span>             | <span data-ttu-id="afa9c-173">3.3V PWR (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="afa9c-173">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="afa9c-174">White cable</span><span class="sxs-lookup"><span data-stu-id="afa9c-174">White cable</span></span>   |
| <span data-ttu-id="afa9c-175">GND (Pin 7G)</span><span class="sxs-lookup"><span data-stu-id="afa9c-175">GND (Pin 7G)</span></span>             | <span data-ttu-id="afa9c-176">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="afa9c-176">GND (Pin 6)</span></span>            | <span data-ttu-id="afa9c-177">Brown cable</span><span class="sxs-lookup"><span data-stu-id="afa9c-177">Brown cable</span></span>   |
| <span data-ttu-id="afa9c-178">SCK (Pin 8G)</span><span class="sxs-lookup"><span data-stu-id="afa9c-178">SCK (Pin 8G)</span></span>             | <span data-ttu-id="afa9c-179">I2C1 SDA (Pin 3)</span><span class="sxs-lookup"><span data-stu-id="afa9c-179">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="afa9c-180">Orange cable</span><span class="sxs-lookup"><span data-stu-id="afa9c-180">Orange cable</span></span>  |
| <span data-ttu-id="afa9c-181">SDI (Pin 10G)</span><span class="sxs-lookup"><span data-stu-id="afa9c-181">SDI (Pin 10G)</span></span>            | <span data-ttu-id="afa9c-182">I2C1 SCL (Pin 5)</span><span class="sxs-lookup"><span data-stu-id="afa9c-182">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="afa9c-183">Red cable</span><span class="sxs-lookup"><span data-stu-id="afa9c-183">Red cable</span></span>     |
| <span data-ttu-id="afa9c-184">LED VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="afa9c-184">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="afa9c-185">GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="afa9c-185">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="afa9c-186">White cable</span><span class="sxs-lookup"><span data-stu-id="afa9c-186">White cable</span></span>   |
| <span data-ttu-id="afa9c-187">LED GND (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="afa9c-187">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="afa9c-188">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="afa9c-188">GND (Pin 20)</span></span>           | <span data-ttu-id="afa9c-189">Black cable</span><span class="sxs-lookup"><span data-stu-id="afa9c-189">Black cable</span></span>   |

<span data-ttu-id="afa9c-190">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span><span class="sxs-lookup"><span data-stu-id="afa9c-190">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="afa9c-191">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span><span class="sxs-lookup"><span data-stu-id="afa9c-191">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Connected Pi and BME280](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

<span data-ttu-id="afa9c-193">Turn on Pi by using the micro USB cable and the power supply.</span><span class="sxs-lookup"><span data-stu-id="afa9c-193">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="afa9c-194">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span><span class="sxs-lookup"><span data-stu-id="afa9c-194">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span>

![Connected to wired network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="afa9c-196">Run a sample application on Pi</span><span class="sxs-lookup"><span data-stu-id="afa9c-196">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="afa9c-197">Clone sample application and install the prerequisite packages</span><span class="sxs-lookup"><span data-stu-id="afa9c-197">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="afa9c-198">Use one of the following SSH clients from your host computer to connect to Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="afa9c-198">Use one of the following SSH clients from your host computer to connect to Intel NUC.</span></span>
    - <span data-ttu-id="afa9c-199">[PuTTY](http://www.putty.org/) for Windows.</span><span class="sxs-lookup"><span data-stu-id="afa9c-199">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="afa9c-200">The built-in SSH client on Ubuntu or macOS.</span><span class="sxs-lookup"><span data-stu-id="afa9c-200">The built-in SSH client on Ubuntu or macOS.</span></span>

1. <span data-ttu-id="afa9c-201">Clone the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="afa9c-201">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https//github.com/Azure-samples/iot-hub-node-raspberry-pi-clientapp
   ```

1. <span data-ttu-id="afa9c-202">Install all packages by the following command.</span><span class="sxs-lookup"><span data-stu-id="afa9c-202">Install all packages by the following command.</span></span> <span data-ttu-id="afa9c-203">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span><span class="sxs-lookup"><span data-stu-id="afa9c-203">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberry-pi-clientapp
   npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="afa9c-204">It might take several minutes to finish this installation process denpening on your network connection.</span><span class="sxs-lookup"><span data-stu-id="afa9c-204">It might take several minutes to finish this installation process denpening on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="afa9c-205">Configure the sample application</span><span class="sxs-lookup"><span data-stu-id="afa9c-205">Configure the sample application</span></span>

1. <span data-ttu-id="afa9c-206">Open the config file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="afa9c-206">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Config file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="afa9c-208">There are two items in this file you can configurate.</span><span class="sxs-lookup"><span data-stu-id="afa9c-208">There are two items in this file you can configurate.</span></span> <span data-ttu-id="afa9c-209">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span><span class="sxs-lookup"><span data-stu-id="afa9c-209">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="afa9c-210">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span><span class="sxs-lookup"><span data-stu-id="afa9c-210">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="afa9c-211">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="afa9c-211">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="afa9c-212">Save and exit by pressing Control-O > Enter > Control-X.</span><span class="sxs-lookup"><span data-stu-id="afa9c-212">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="afa9c-213">Run the sample application</span><span class="sxs-lookup"><span data-stu-id="afa9c-213">Run the sample application</span></span>

1. <span data-ttu-id="afa9c-214">Run the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="afa9c-214">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="afa9c-215">Make sure you copy-paste the device connection string into the single quotes.</span><span class="sxs-lookup"><span data-stu-id="afa9c-215">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="afa9c-216">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="afa9c-216">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Output - sensor data sent from Raspberry Pi to your IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="afa9c-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="afa9c-218">Next steps</span></span>

<span data-ttu-id="afa9c-219">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="afa9c-219">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]







