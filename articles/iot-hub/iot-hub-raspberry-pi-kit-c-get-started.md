---
title: Raspberry Pi to cloud (C) - Connect Raspberry Pi to Azure IoT Hub | Microsoft Docs
description: Connect Raspberry Pi to Azure IoT Hub for Raspberry Pi to send data to the Azure cloud.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure iot raspberry pi, raspberry pi iot hub, raspberry pi send data to cloud, raspberry pi to cloud
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/13/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 97870e18364953ac05f373e22b4f6c1bb7222ba6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563878"
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-c"></a><span data-ttu-id="235f9-104">Connect Raspberry Pi to Azure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="235f9-104">Connect Raspberry Pi to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="235f9-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span><span class="sxs-lookup"><span data-stu-id="235f9-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="235f9-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="235f9-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="235f9-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="235f9-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="235f9-108">What you do</span><span class="sxs-lookup"><span data-stu-id="235f9-108">What you do</span></span>

* <span data-ttu-id="235f9-109">Setup Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="235f9-109">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="235f9-110">Create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="235f9-110">Create an IoT hub.</span></span>
* <span data-ttu-id="235f9-111">Register a device for Pi in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="235f9-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="235f9-112">Run a sample application on Pi to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="235f9-112">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="235f9-113">Connect Raspberry Pi to an IoT hub that you create.</span><span class="sxs-lookup"><span data-stu-id="235f9-113">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="235f9-114">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span><span class="sxs-lookup"><span data-stu-id="235f9-114">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="235f9-115">Finally, you send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="235f9-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="235f9-116">What you learn</span><span class="sxs-lookup"><span data-stu-id="235f9-116">What you learn</span></span>

* <span data-ttu-id="235f9-117">How to create an Azure IoT hub and get your new device connection string.</span><span class="sxs-lookup"><span data-stu-id="235f9-117">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="235f9-118">How to connect Pi with a BME280 sensor.</span><span class="sxs-lookup"><span data-stu-id="235f9-118">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="235f9-119">How to collect sensor data by running a sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="235f9-119">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="235f9-120">How to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="235f9-120">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="235f9-121">What you need</span><span class="sxs-lookup"><span data-stu-id="235f9-121">What you need</span></span>

![What you need](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="235f9-123">The Raspberry Pi 2 or Raspberry Pi 3 board.</span><span class="sxs-lookup"><span data-stu-id="235f9-123">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="235f9-124">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="235f9-124">An active Azure subscription.</span></span> <span data-ttu-id="235f9-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="235f9-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="235f9-126">A monitor, a USB keyboard, and mouse that connect to Pi.</span><span class="sxs-lookup"><span data-stu-id="235f9-126">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="235f9-127">A Mac or a PC that is running Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="235f9-127">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="235f9-128">An Internet connection.</span><span class="sxs-lookup"><span data-stu-id="235f9-128">An Internet connection.</span></span>
* <span data-ttu-id="235f9-129">A 16 GB or above microSD card.</span><span class="sxs-lookup"><span data-stu-id="235f9-129">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="235f9-130">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span><span class="sxs-lookup"><span data-stu-id="235f9-130">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="235f9-131">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span><span class="sxs-lookup"><span data-stu-id="235f9-131">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="235f9-132">The following items are optional:</span><span class="sxs-lookup"><span data-stu-id="235f9-132">The following items are optional:</span></span>

* <span data-ttu-id="235f9-133">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span><span class="sxs-lookup"><span data-stu-id="235f9-133">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="235f9-134">A breadboard.</span><span class="sxs-lookup"><span data-stu-id="235f9-134">A breadboard.</span></span>
* <span data-ttu-id="235f9-135">6 F/M jumper wires.</span><span class="sxs-lookup"><span data-stu-id="235f9-135">6 F/M jumper wires.</span></span>
* <span data-ttu-id="235f9-136">A diffused 10-mm LED.</span><span class="sxs-lookup"><span data-stu-id="235f9-136">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="235f9-137">These items are optional because the code sample support simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="235f9-137">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="235f9-138">Setup Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="235f9-138">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="235f9-139">Install the Raspbian operating system for Pi</span><span class="sxs-lookup"><span data-stu-id="235f9-139">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="235f9-140">Prepare the microSD card for installation of the Raspbian image.</span><span class="sxs-lookup"><span data-stu-id="235f9-140">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="235f9-141">Download Raspbian.</span><span class="sxs-lookup"><span data-stu-id="235f9-141">Download Raspbian.</span></span>
   1. <span data-ttu-id="235f9-142">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span><span class="sxs-lookup"><span data-stu-id="235f9-142">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="235f9-143">Extract the Raspbian image to a folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="235f9-143">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="235f9-144">Install Raspbian to the microSD card.</span><span class="sxs-lookup"><span data-stu-id="235f9-144">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="235f9-145">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="235f9-145">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="235f9-146">Run Etcher and select the Raspbian image that you extracted in step 1.</span><span class="sxs-lookup"><span data-stu-id="235f9-146">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="235f9-147">Select the microSD card drive.</span><span class="sxs-lookup"><span data-stu-id="235f9-147">Select the microSD card drive.</span></span> <span data-ttu-id="235f9-148">Note that Etcher may have already selected the correct drive.</span><span class="sxs-lookup"><span data-stu-id="235f9-148">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="235f9-149">Click Flash to install Raspbian to the microSD card.</span><span class="sxs-lookup"><span data-stu-id="235f9-149">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="235f9-150">Remove the microSD card from your computer when installation is complete.</span><span class="sxs-lookup"><span data-stu-id="235f9-150">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="235f9-151">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span><span class="sxs-lookup"><span data-stu-id="235f9-151">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="235f9-152">Insert the microSD card into Pi.</span><span class="sxs-lookup"><span data-stu-id="235f9-152">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="235f9-153">Enable SSH and SPI</span><span class="sxs-lookup"><span data-stu-id="235f9-153">Enable SSH and SPI</span></span>

1. <span data-ttu-id="235f9-154">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span><span class="sxs-lookup"><span data-stu-id="235f9-154">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="235f9-155">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span><span class="sxs-lookup"><span data-stu-id="235f9-155">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![The Raspbian Preferences menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="235f9-157">On the **Interfaces** tab, set **SPI** and **SSH** to **Enable**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="235f9-157">On the **Interfaces** tab, set **SPI** and **SSH** to **Enable**, and then click **OK**.</span></span>

   ![Enable SPI and SSH on Raspberry Pi](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="235f9-159">To enable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="235f9-159">To enable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="235f9-160">Connect the sensor to Pi</span><span class="sxs-lookup"><span data-stu-id="235f9-160">Connect the sensor to Pi</span></span>

<span data-ttu-id="235f9-161">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span><span class="sxs-lookup"><span data-stu-id="235f9-161">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="235f9-162">If you don’t have the sensor, skip this section.</span><span class="sxs-lookup"><span data-stu-id="235f9-162">If you don’t have the sensor, skip this section.</span></span>

![The Raspberry Pi and sensor connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="235f9-164">For sensor pins, use the following wiring:</span><span class="sxs-lookup"><span data-stu-id="235f9-164">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="235f9-165">Start (Sensor & LED)</span><span class="sxs-lookup"><span data-stu-id="235f9-165">Start (Sensor & LED)</span></span>     | <span data-ttu-id="235f9-166">End (Board)</span><span class="sxs-lookup"><span data-stu-id="235f9-166">End (Board)</span></span>            | <span data-ttu-id="235f9-167">Cable Color</span><span class="sxs-lookup"><span data-stu-id="235f9-167">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="235f9-168">LED VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="235f9-168">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="235f9-169">GPIO 4 (Pin 7)</span><span class="sxs-lookup"><span data-stu-id="235f9-169">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="235f9-170">White cable</span><span class="sxs-lookup"><span data-stu-id="235f9-170">White cable</span></span>   |
| <span data-ttu-id="235f9-171">LED GND (Pin 6G)</span><span class="sxs-lookup"><span data-stu-id="235f9-171">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="235f9-172">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="235f9-172">GND (Pin 6)</span></span>            | <span data-ttu-id="235f9-173">Black cable</span><span class="sxs-lookup"><span data-stu-id="235f9-173">Black cable</span></span>   |
| <span data-ttu-id="235f9-174">VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="235f9-174">VDD (Pin 18F)</span></span>            | <span data-ttu-id="235f9-175">3.3V PWR (Pin 17)</span><span class="sxs-lookup"><span data-stu-id="235f9-175">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="235f9-176">White cable</span><span class="sxs-lookup"><span data-stu-id="235f9-176">White cable</span></span>   |
| <span data-ttu-id="235f9-177">GND (Pin 20F)</span><span class="sxs-lookup"><span data-stu-id="235f9-177">GND (Pin 20F)</span></span>            | <span data-ttu-id="235f9-178">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="235f9-178">GND (Pin 20)</span></span>           | <span data-ttu-id="235f9-179">Black cable</span><span class="sxs-lookup"><span data-stu-id="235f9-179">Black cable</span></span>   |
| <span data-ttu-id="235f9-180">SCK (Pin 21F)</span><span class="sxs-lookup"><span data-stu-id="235f9-180">SCK (Pin 21F)</span></span>            | <span data-ttu-id="235f9-181">SPI0 SCLK (Pin 23)</span><span class="sxs-lookup"><span data-stu-id="235f9-181">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="235f9-182">Orange cable</span><span class="sxs-lookup"><span data-stu-id="235f9-182">Orange cable</span></span>  |
| <span data-ttu-id="235f9-183">SDO (Pin 22F)</span><span class="sxs-lookup"><span data-stu-id="235f9-183">SDO (Pin 22F)</span></span>            | <span data-ttu-id="235f9-184">SPI0 MISO (Pin 21)</span><span class="sxs-lookup"><span data-stu-id="235f9-184">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="235f9-185">Yellow cable</span><span class="sxs-lookup"><span data-stu-id="235f9-185">Yellow cable</span></span>  |
| <span data-ttu-id="235f9-186">SDI (Pin 23F)</span><span class="sxs-lookup"><span data-stu-id="235f9-186">SDI (Pin 23F)</span></span>            | <span data-ttu-id="235f9-187">SPI0 MOSI (Pin 19)</span><span class="sxs-lookup"><span data-stu-id="235f9-187">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="235f9-188">Green cable</span><span class="sxs-lookup"><span data-stu-id="235f9-188">Green cable</span></span>   |
| <span data-ttu-id="235f9-189">CS (Pin 24F)</span><span class="sxs-lookup"><span data-stu-id="235f9-189">CS (Pin 24F)</span></span>             | <span data-ttu-id="235f9-190">SPI0 CS (Pin 24)</span><span class="sxs-lookup"><span data-stu-id="235f9-190">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="235f9-191">Blue cable</span><span class="sxs-lookup"><span data-stu-id="235f9-191">Blue cable</span></span>    |

<span data-ttu-id="235f9-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span><span class="sxs-lookup"><span data-stu-id="235f9-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="235f9-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span><span class="sxs-lookup"><span data-stu-id="235f9-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Connected Pi and BME280](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

<span data-ttu-id="235f9-195">Turn on Pi by using the micro USB cable and the power supply.</span><span class="sxs-lookup"><span data-stu-id="235f9-195">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="235f9-196">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span><span class="sxs-lookup"><span data-stu-id="235f9-196">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span>

![Connected to wired network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="235f9-198">Run a sample application on Pi</span><span class="sxs-lookup"><span data-stu-id="235f9-198">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="235f9-199">Install the prerequisite packages</span><span class="sxs-lookup"><span data-stu-id="235f9-199">Install the prerequisite packages</span></span>

1. <span data-ttu-id="235f9-200">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="235f9-200">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
    - <span data-ttu-id="235f9-201">[PuTTY](http://www.putty.org/) for Windows.</span><span class="sxs-lookup"><span data-stu-id="235f9-201">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="235f9-202">The built-in SSH client on Ubuntu or macOS.</span><span class="sxs-lookup"><span data-stu-id="235f9-202">The built-in SSH client on Ubuntu or macOS.</span></span>

1. <span data-ttu-id="235f9-203">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C and Cmake by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="235f9-203">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C and Cmake by running the following commands:</span></span>

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake
   ```


### <a name="configure-the-sample-application"></a><span data-ttu-id="235f9-204">Configure the sample application</span><span class="sxs-lookup"><span data-stu-id="235f9-204">Configure the sample application</span></span>

1. <span data-ttu-id="235f9-205">Clone the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="235f9-205">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https//github.com/Azure-samples/iot-hub-c-raspberry-pi-clientapp
   ```
1. <span data-ttu-id="235f9-206">Open the config file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="235f9-206">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberry-pi-clientapp
   nano config.json
   ```

   ![Config file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="235f9-208">There are two macros in this file you can configurate.</span><span class="sxs-lookup"><span data-stu-id="235f9-208">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="235f9-209">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span><span class="sxs-lookup"><span data-stu-id="235f9-209">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="235f9-210">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span><span class="sxs-lookup"><span data-stu-id="235f9-210">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="235f9-211">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="235f9-211">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="235f9-212">Save and exit by pressing Control-O > Enter > Control-X.</span><span class="sxs-lookup"><span data-stu-id="235f9-212">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="235f9-213">Build and run the sample application</span><span class="sxs-lookup"><span data-stu-id="235f9-213">Build and run the sample application</span></span>

1. <span data-ttu-id="235f9-214">Build the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="235f9-214">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Build output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="235f9-216">Run the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="235f9-216">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="235f9-217">Make sure you copy-paste the device connection string into the single quotes.</span><span class="sxs-lookup"><span data-stu-id="235f9-217">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="235f9-218">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="235f9-218">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Output - sensor data sent from Raspberry Pi to your IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="235f9-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="235f9-220">Next steps</span></span>

<span data-ttu-id="235f9-221">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="235f9-221">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]








