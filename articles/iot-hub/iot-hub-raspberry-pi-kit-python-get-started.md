---
title: Raspberry Pi to cloud (Python) - Connect Raspberry Pi to Azure IoT Hub | Microsoft Docs
description: Learn how to setup and connect Raspberry Pi to Azure IoT Hub for Raspberry Pi to send data to the Azure cloud platform in this tutorial.
author: rangv
manager: ''
keywords: azure iot raspberry pi, raspberry pi iot hub, raspberry pi send data to cloud, raspberry pi to cloud
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: conceptual
ms.date: 04/11/2018
ms.author: rangv
ms.openlocfilehash: 6e668394bcb647df901dfac72c552475e56f20bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864440"
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-python"></a><span data-ttu-id="c4ff2-104">Connect Raspberry Pi to Azure IoT Hub (Python)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-104">Connect Raspberry Pi to Azure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="c4ff2-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="c4ff2-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](about-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](about-iot-hub.md).</span></span> <span data-ttu-id="c4ff2-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="c4ff2-108">Don't have a kit yet?</span><span class="sxs-lookup"><span data-stu-id="c4ff2-108">Don't have a kit yet?</span></span> <span data-ttu-id="c4ff2-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="c4ff2-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="c4ff2-111">What you do</span><span class="sxs-lookup"><span data-stu-id="c4ff2-111">What you do</span></span>

* <span data-ttu-id="c4ff2-112">Create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-112">Create an IoT hub.</span></span>
* <span data-ttu-id="c4ff2-113">Register a device for Pi in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="c4ff2-114">Setup Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="c4ff2-115">Run a sample application on Pi to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="c4ff2-116">Connect Raspberry Pi to an IoT hub that you create.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="c4ff2-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="c4ff2-118">Finally, you send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="c4ff2-119">What you learn</span><span class="sxs-lookup"><span data-stu-id="c4ff2-119">What you learn</span></span>

* <span data-ttu-id="c4ff2-120">How to create an Azure IoT hub and get your new device connection string.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="c4ff2-121">How to connect Pi with a BME280 sensor.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="c4ff2-122">How to collect sensor data by running a sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="c4ff2-123">How to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c4ff2-124">What you need</span><span class="sxs-lookup"><span data-stu-id="c4ff2-124">What you need</span></span>

![What you need](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="c4ff2-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="c4ff2-127">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-127">An active Azure subscription.</span></span> <span data-ttu-id="c4ff2-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="c4ff2-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="c4ff2-130">A Mac or a PC that is running Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="c4ff2-131">An Internet connection.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-131">An Internet connection.</span></span>
* <span data-ttu-id="c4ff2-132">A 16 GB or above microSD card.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="c4ff2-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="c4ff2-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="c4ff2-135">The following items are optional:</span><span class="sxs-lookup"><span data-stu-id="c4ff2-135">The following items are optional:</span></span>

* <span data-ttu-id="c4ff2-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="c4ff2-137">A breadboard.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-137">A breadboard.</span></span>
* <span data-ttu-id="c4ff2-138">6 F/M jumper wires.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="c4ff2-139">A diffused 10-mm LED.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="c4ff2-140">These items are optional because the code sample support simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="c4ff2-141">Set up Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="c4ff2-141">Set up Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="c4ff2-142">Install the Raspbian operating system for Pi</span><span class="sxs-lookup"><span data-stu-id="c4ff2-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="c4ff2-143">Prepare the microSD card for installation of the Raspbian image.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="c4ff2-144">Download Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="c4ff2-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="c4ff2-146">Extract the Raspbian image to a folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="c4ff2-147">Install Raspbian to the microSD card.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="c4ff2-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="c4ff2-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="c4ff2-150">Select the microSD card drive.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-150">Select the microSD card drive.</span></span> <span data-ttu-id="c4ff2-151">Note that Etcher may have already selected the correct drive.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="c4ff2-152">Click Flash to install Raspbian to the microSD card.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="c4ff2-153">Remove the microSD card from your computer when installation is complete.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="c4ff2-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="c4ff2-155">Insert the microSD card into Pi.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="c4ff2-156">Enable SSH and I2C</span><span class="sxs-lookup"><span data-stu-id="c4ff2-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="c4ff2-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="c4ff2-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![The Raspbian Preferences menu](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="c4ff2-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="c4ff2-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Enable I2C and SSH on Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="c4ff2-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="c4ff2-164">Connect the sensor to Pi</span><span class="sxs-lookup"><span data-stu-id="c4ff2-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="c4ff2-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="c4ff2-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![The Raspberry Pi and sensor connection](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="c4ff2-168">The BME280 sensor can collect temperature and humidity data.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="c4ff2-169">And the LED will blink if there is a communication between device and the cloud.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="c4ff2-170">For sensor pins, use the following wiring:</span><span class="sxs-lookup"><span data-stu-id="c4ff2-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="c4ff2-171">Start (Sensor & LED)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="c4ff2-172">End (Board)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-172">End (Board)</span></span>            | <span data-ttu-id="c4ff2-173">Cable Color</span><span class="sxs-lookup"><span data-stu-id="c4ff2-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="c4ff2-174">VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="c4ff2-175">3.3V PWR (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="c4ff2-176">White cable</span><span class="sxs-lookup"><span data-stu-id="c4ff2-176">White cable</span></span>   |
| <span data-ttu-id="c4ff2-177">GND (Pin 7G)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="c4ff2-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-178">GND (Pin 6)</span></span>            | <span data-ttu-id="c4ff2-179">Brown cable</span><span class="sxs-lookup"><span data-stu-id="c4ff2-179">Brown cable</span></span>   |
| <span data-ttu-id="c4ff2-180">SDI (Pin 10G)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="c4ff2-181">I2C1 SDA (Pin 3)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="c4ff2-182">Red cable</span><span class="sxs-lookup"><span data-stu-id="c4ff2-182">Red cable</span></span>     |
| <span data-ttu-id="c4ff2-183">SCK (Pin 8G)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="c4ff2-184">I2C1 SCL (Pin 5)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="c4ff2-185">Orange cable</span><span class="sxs-lookup"><span data-stu-id="c4ff2-185">Orange cable</span></span>  |
| <span data-ttu-id="c4ff2-186">LED VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="c4ff2-187">GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="c4ff2-188">White cable</span><span class="sxs-lookup"><span data-stu-id="c4ff2-188">White cable</span></span>   |
| <span data-ttu-id="c4ff2-189">LED GND (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="c4ff2-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="c4ff2-190">GND (Pin 20)</span></span>           | <span data-ttu-id="c4ff2-191">Black cable</span><span class="sxs-lookup"><span data-stu-id="c4ff2-191">Black cable</span></span>   |

<span data-ttu-id="c4ff2-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="c4ff2-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Connected Pi and BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="c4ff2-195">Connect Pi to the network</span><span class="sxs-lookup"><span data-stu-id="c4ff2-195">Connect Pi to the network</span></span>

<span data-ttu-id="c4ff2-196">Turn on Pi by using the micro USB cable and the power supply.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="c4ff2-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="c4ff2-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Connected to wired network](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="c4ff2-200">Make sure that Pi is connected to the same network as your computer.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="c4ff2-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="c4ff2-202">Run a sample application on Pi</span><span class="sxs-lookup"><span data-stu-id="c4ff2-202">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="c4ff2-203">Install the prerequisite packages</span><span class="sxs-lookup"><span data-stu-id="c4ff2-203">Install the prerequisite packages</span></span>

<span data-ttu-id="c4ff2-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="c4ff2-205">**Windows Users**</span><span class="sxs-lookup"><span data-stu-id="c4ff2-205">**Windows Users**</span></span>
   1. <span data-ttu-id="c4ff2-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="c4ff2-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   
   <span data-ttu-id="c4ff2-208">**Mac and Ubuntu Users**</span><span class="sxs-lookup"><span data-stu-id="c4ff2-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="c4ff2-209">Use the built-in SSH client on Ubuntu or macOS.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-209">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="c4ff2-210">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-210">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="c4ff2-211">The default username is `pi` , and the password is `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-211">The default username is `pi` , and the password is `raspberry`.</span></span>


### <a name="configure-the-sample-application"></a><span data-ttu-id="c4ff2-212">Configure the sample application</span><span class="sxs-lookup"><span data-stu-id="c4ff2-212">Configure the sample application</span></span>

1. <span data-ttu-id="c4ff2-213">Clone the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="c4ff2-213">Clone the sample application by running the following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="c4ff2-214">Open the config file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="c4ff2-214">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="c4ff2-215">There are 5 macros in this file you can configurate.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="c4ff2-216">The first one is `MESSAGE_TIMESPAN`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-216">The first one is `MESSAGE_TIMESPAN`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="c4ff2-217">The second one `SIMULATED_DATA`, which is a Boolean value for whether to use simulated sensor data or not.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-217">The second one `SIMULATED_DATA`, which is a Boolean value for whether to use simulated sensor data or not.</span></span> <span data-ttu-id="c4ff2-218">`I2C_ADDRESS` is the I2C address which your BME280 sensor is connected.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-218">`I2C_ADDRESS` is the I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="c4ff2-219">`GPIO_PIN_ADDRESS` is the GPIO address for your LED.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-219">`GPIO_PIN_ADDRESS` is the GPIO address for your LED.</span></span> <span data-ttu-id="c4ff2-220">The last one is `BLINK_TIMESPAN`, which defined the timespan when your LED is turned on in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-220">The last one is `BLINK_TIMESPAN`, which defined the timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="c4ff2-221">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `True` to make the sample application create and use simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-221">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `True` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="c4ff2-222">Save and exit by pressing Control-O > Enter > Control-X.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="c4ff2-223">Build and run the sample application</span><span class="sxs-lookup"><span data-stu-id="c4ff2-223">Build and run the sample application</span></span>

1. <span data-ttu-id="c4ff2-224">Build the sample application by running the following command.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-224">Build the sample application by running the following command.</span></span> <span data-ttu-id="c4ff2-225">Because the Azure IoT SDKs for Python are wrappers on top of the Azure IoT Device C SDK, you will need to compile the C libraries if you want or need to generate the Python libraries from source code.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-225">Because the Azure IoT SDKs for Python are wrappers on top of the Azure IoT Device C SDK, you will need to compile the C libraries if you want or need to generate the Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="c4ff2-226">You can also specify the version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-226">You can also specify the version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="c4ff2-227">If you run script without parameter, the script will automatically detect the version of python installed (Search sequence 2.7->3.4->3.5).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-227">If you run script without parameter, the script will automatically detect the version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="c4ff2-228">Make sure your Python version keeps consistent during building and running.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="c4ff2-229">On building the Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-229">On building the Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="c4ff2-230">If you run into this issue, check the memory consumption of the device using `free -m command` in another terminal window during that time.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-230">If you run into this issue, check the memory consumption of the device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="c4ff2-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have to temporarily increase the swap space to get more available memory to successfully build the Python client-side device SDK library.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have to temporarily increase the swap space to get more available memory to successfully build the Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="c4ff2-232">Run the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="c4ff2-232">Run the sample application by running the following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="c4ff2-233">Make sure you copy-paste the device connection string into the single quotes.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-233">Make sure you copy-paste the device connection string into the single quotes.</span></span> <span data-ttu-id="c4ff2-234">And if you use the python 3, then you can use the command `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-234">And if you use the python 3, then you can use the command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="c4ff2-235">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-235">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

   ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="c4ff2-237">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4ff2-237">Next steps</span></span>

<span data-ttu-id="c4ff2-238">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c4ff2-238">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="c4ff2-239">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi, see the [Use Azure IoT Toolkit extension for Visual Studio Code to send and receive messages between your device and IoT Hub](iot-hub-vscode-iot-toolkit-cloud-device-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="c4ff2-239">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi, see the [Use Azure IoT Toolkit extension for Visual Studio Code to send and receive messages between your device and IoT Hub](iot-hub-vscode-iot-toolkit-cloud-device-messaging.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
