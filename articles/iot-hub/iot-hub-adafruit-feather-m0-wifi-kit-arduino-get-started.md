---
title: M0 to cloud - Connect Feather M0 WiFi to Azure IoT Hub | Microsoft Docs
description: Explains how to connect an Arduino device, called Adafruit Feather M0 WiFi, to Azure IoT Hub, which is a Microsoft cloud service that helps manage your IoT assets.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: ''
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b7c196dbb45b32ca038005f610fb4104ae9e84ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551722"
---
# <a name="connect-adafruit-feather-m0-wifi-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="1df61-103">Connect Adafruit Feather M0 WiFi to Azure IoT Hub in the cloud</span><span class="sxs-lookup"><span data-stu-id="1df61-103">Connect Adafruit Feather M0 WiFi to Azure IoT Hub in the cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connection between BME280, Feather M0 WiFi, and IoT Hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="1df61-105">In this tutorial, you begin by learning the basics of working with your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="1df61-105">In this tutorial, you begin by learning the basics of working with your Arduino board.</span></span> <span data-ttu-id="1df61-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="1df61-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="1df61-107">What you do</span><span class="sxs-lookup"><span data-stu-id="1df61-107">What you do</span></span>

<span data-ttu-id="1df61-108">Connect Adafruit Feather M0 WiFi to an IoT hub that you create.</span><span class="sxs-lookup"><span data-stu-id="1df61-108">Connect Adafruit Feather M0 WiFi to an IoT hub that you create.</span></span> <span data-ttu-id="1df61-109">Then you run a sample application on M0 WiFi to collect the temperature and humidity data from a BME280.</span><span class="sxs-lookup"><span data-stu-id="1df61-109">Then you run a sample application on M0 WiFi to collect the temperature and humidity data from a BME280.</span></span> <span data-ttu-id="1df61-110">Finally, you send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1df61-110">Finally, you send the sensor data to your IoT hub.</span></span>



## <a name="what-you-learn"></a><span data-ttu-id="1df61-111">What you learn</span><span class="sxs-lookup"><span data-stu-id="1df61-111">What you learn</span></span>

* <span data-ttu-id="1df61-112">How to create an IoT hub and register a device for Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="1df61-112">How to create an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="1df61-113">How to connect Feather M0 WiFi with the sensor and your computer</span><span class="sxs-lookup"><span data-stu-id="1df61-113">How to connect Feather M0 WiFi with the sensor and your computer</span></span>
* <span data-ttu-id="1df61-114">How to collect sensor data by running a sample application on Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="1df61-114">How to collect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="1df61-115">How to send the sensor data to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="1df61-115">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1df61-116">What you need</span><span class="sxs-lookup"><span data-stu-id="1df61-116">What you need</span></span>

![Parts needed for the tutorial](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="1df61-118">To complete this operation, you need the following parts from your Feather M0 WiFi Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="1df61-118">To complete this operation, you need the following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="1df61-119">The Feather M0 WiFi board</span><span class="sxs-lookup"><span data-stu-id="1df61-119">The Feather M0 WiFi board</span></span>
* <span data-ttu-id="1df61-120">A Micro USB to Type A USB cable</span><span class="sxs-lookup"><span data-stu-id="1df61-120">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="1df61-121">You also need the following things for your development environment:</span><span class="sxs-lookup"><span data-stu-id="1df61-121">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="1df61-122">Mac or PC that is running Windows or Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="1df61-122">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="1df61-123">Wireless network for Feather M0 WiFi to connect to.</span><span class="sxs-lookup"><span data-stu-id="1df61-123">Wireless network for Feather M0 WiFi to connect to.</span></span>
* <span data-ttu-id="1df61-124">Internet connection to download the configuration tool.</span><span class="sxs-lookup"><span data-stu-id="1df61-124">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="1df61-125">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span><span class="sxs-lookup"><span data-stu-id="1df61-125">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="1df61-126">Earlier versions don't work with the AzureIoT library.</span><span class="sxs-lookup"><span data-stu-id="1df61-126">Earlier versions don't work with the AzureIoT library.</span></span>


<span data-ttu-id="1df61-127">The following items are optional in case you don’t have a sensor.</span><span class="sxs-lookup"><span data-stu-id="1df61-127">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="1df61-128">You also have the option of using simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="1df61-128">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="1df61-129">An BME280 temperature and humidity sensor</span><span class="sxs-lookup"><span data-stu-id="1df61-129">An BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="1df61-130">A breadboard</span><span class="sxs-lookup"><span data-stu-id="1df61-130">A breadboard</span></span>
* <span data-ttu-id="1df61-131">M/M jumper wires</span><span class="sxs-lookup"><span data-stu-id="1df61-131">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-the-sensor-and-your-computer"></a><span data-ttu-id="1df61-132">Connect Feather M0 WiFi with the sensor and your computer</span><span class="sxs-lookup"><span data-stu-id="1df61-132">Connect Feather M0 WiFi with the sensor and your computer</span></span>
<span data-ttu-id="1df61-133">In this section, you connect the sensors to your board.</span><span class="sxs-lookup"><span data-stu-id="1df61-133">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="1df61-134">Then you plug in your device to your computer for further use.</span><span class="sxs-lookup"><span data-stu-id="1df61-134">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-m0-wifi"></a><span data-ttu-id="1df61-135">Connect a DHT22 temperature and humidity sensor to Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="1df61-135">Connect a DHT22 temperature and humidity sensor to Feather M0 WiFi</span></span>

<span data-ttu-id="1df61-136">Use the breadboard and jumper wires to make the connection as follows.</span><span class="sxs-lookup"><span data-stu-id="1df61-136">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="1df61-137">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span><span class="sxs-lookup"><span data-stu-id="1df61-137">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Connections reference](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="1df61-139">For sensor pins, use the following wiring:</span><span class="sxs-lookup"><span data-stu-id="1df61-139">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="1df61-140">Start (Sensor)</span><span class="sxs-lookup"><span data-stu-id="1df61-140">Start (Sensor)</span></span>           | <span data-ttu-id="1df61-141">End (Board)</span><span class="sxs-lookup"><span data-stu-id="1df61-141">End (Board)</span></span>            | <span data-ttu-id="1df61-142">Cable Color</span><span class="sxs-lookup"><span data-stu-id="1df61-142">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="1df61-143">VDD (Pin 27A)</span><span class="sxs-lookup"><span data-stu-id="1df61-143">VDD (Pin 27A)</span></span>            | <span data-ttu-id="1df61-144">3V (Pin 3A)</span><span class="sxs-lookup"><span data-stu-id="1df61-144">3V (Pin 3A)</span></span>            | <span data-ttu-id="1df61-145">Red cable</span><span class="sxs-lookup"><span data-stu-id="1df61-145">Red cable</span></span>     |
| <span data-ttu-id="1df61-146">GND (Pin 29A)</span><span class="sxs-lookup"><span data-stu-id="1df61-146">GND (Pin 29A)</span></span>            | <span data-ttu-id="1df61-147">GND (Pin 6A)</span><span class="sxs-lookup"><span data-stu-id="1df61-147">GND (Pin 6A)</span></span>           | <span data-ttu-id="1df61-148">Black cable</span><span class="sxs-lookup"><span data-stu-id="1df61-148">Black cable</span></span>   |
| <span data-ttu-id="1df61-149">SCK (Pin 30A)</span><span class="sxs-lookup"><span data-stu-id="1df61-149">SCK (Pin 30A)</span></span>            | <span data-ttu-id="1df61-150">SCK (Pin 12A)</span><span class="sxs-lookup"><span data-stu-id="1df61-150">SCK (Pin 12A)</span></span>          | <span data-ttu-id="1df61-151">Yellow cable</span><span class="sxs-lookup"><span data-stu-id="1df61-151">Yellow cable</span></span>  |
| <span data-ttu-id="1df61-152">SDO (Pin 31A)</span><span class="sxs-lookup"><span data-stu-id="1df61-152">SDO (Pin 31A)</span></span>            | <span data-ttu-id="1df61-153">MI (Pin 14A)</span><span class="sxs-lookup"><span data-stu-id="1df61-153">MI (Pin 14A)</span></span>           | <span data-ttu-id="1df61-154">White cable</span><span class="sxs-lookup"><span data-stu-id="1df61-154">White cable</span></span>   |
| <span data-ttu-id="1df61-155">SDI (Pin 32A)</span><span class="sxs-lookup"><span data-stu-id="1df61-155">SDI (Pin 32A)</span></span>            | <span data-ttu-id="1df61-156">M0 (Pin 13A)</span><span class="sxs-lookup"><span data-stu-id="1df61-156">M0 (Pin 13A)</span></span>           | <span data-ttu-id="1df61-157">Blue cable</span><span class="sxs-lookup"><span data-stu-id="1df61-157">Blue cable</span></span>    |
| <span data-ttu-id="1df61-158">CS (Pin 33A)</span><span class="sxs-lookup"><span data-stu-id="1df61-158">CS (Pin 33A)</span></span>             | <span data-ttu-id="1df61-159">GPIO 5 (Pin 15J)</span><span class="sxs-lookup"><span data-stu-id="1df61-159">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="1df61-160">Orange cable</span><span class="sxs-lookup"><span data-stu-id="1df61-160">Orange cable</span></span>  |

<span data-ttu-id="1df61-161">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi Pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="1df61-161">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi Pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="1df61-162">Now your Feather M0 WiFi should be connected with a working sensor.</span><span class="sxs-lookup"><span data-stu-id="1df61-162">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Connect DHT22 with Feather Huzzah](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-to-your-computer"></a><span data-ttu-id="1df61-164">Connect Feather M0 WiFi to your computer</span><span class="sxs-lookup"><span data-stu-id="1df61-164">Connect Feather M0 WiFi to your computer</span></span>

<span data-ttu-id="1df61-165">As shown next, use the Micro USB to Type A USB cable to connect Feather M0 WiFi to your computer.</span><span class="sxs-lookup"><span data-stu-id="1df61-165">As shown next, use the Micro USB to Type A USB cable to connect Feather M0 WiFi to your computer.</span></span>

![Connect Feather Huzzah to your computer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="1df61-167">Add serial port permissions (Ubuntu only)</span><span class="sxs-lookup"><span data-stu-id="1df61-167">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="1df61-168">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="1df61-168">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="1df61-169">To add serial port permissions, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="1df61-169">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="1df61-170">Run the following commands at a terminal:</span><span class="sxs-lookup"><span data-stu-id="1df61-170">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="1df61-171">You get one of the following outputs:</span><span class="sxs-lookup"><span data-stu-id="1df61-171">You get one of the following outputs:</span></span>

   * <span data-ttu-id="1df61-172">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="1df61-172">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="1df61-173">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="1df61-173">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="1df61-174">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span><span class="sxs-lookup"><span data-stu-id="1df61-174">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="1df61-175">Add the user to the group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1df61-175">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="1df61-176">`<group-owner-name>` is the group owner name you obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="1df61-176">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="1df61-177">`<username>` is your Ubuntu user name.</span><span class="sxs-lookup"><span data-stu-id="1df61-177">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="1df61-178">Sign out of Ubuntu, and then sign in again for the change to appear.</span><span class="sxs-lookup"><span data-stu-id="1df61-178">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="1df61-179">Collect sensor data and send it to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="1df61-179">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="1df61-180">In this section, you deploy and run a sample application on Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="1df61-180">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="1df61-181">The sample application blinks the LED on Feather M0 WiFi, and sends the temperature and humidity data collected from the BME280 sensor to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1df61-181">The sample application blinks the LED on Feather M0 WiFi, and sends the temperature and humidity data collected from the BME280 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github-and-prepare-arduino-ide"></a><span data-ttu-id="1df61-182">Get the sample application from GitHub and prepare Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="1df61-182">Get the sample application from GitHub and prepare Arduino IDE</span></span>

<span data-ttu-id="1df61-183">The sample application is hosted on GitHub.</span><span class="sxs-lookup"><span data-stu-id="1df61-183">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="1df61-184">Clone the sample repository that contains the sample application from GitHub.</span><span class="sxs-lookup"><span data-stu-id="1df61-184">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="1df61-185">To clone the sample repository, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="1df61-185">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="1df61-186">Open a command prompt or a terminal window.</span><span class="sxs-lookup"><span data-stu-id="1df61-186">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="1df61-187">Go to a folder where you want the sample application to be stored.</span><span class="sxs-lookup"><span data-stu-id="1df61-187">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="1df61-188">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="1df61-188">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

<span data-ttu-id="1df61-189">Install the package for Feather M0 WiFi in the Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="1df61-189">Install the package for Feather M0 WiFi in the Arduino IDE:</span></span>

1. <span data-ttu-id="1df61-190">Open the folder where the sample application is stored.</span><span class="sxs-lookup"><span data-stu-id="1df61-190">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="1df61-191">Open the app.ino file in the app folder in the Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="1df61-191">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Open the sample application in Arduino IDE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="1df61-193">Click **Tools** > **Board** > **Boards Manager**, and then install the `Arduino SAMD Boards` version `1.6.2` or later</span><span class="sxs-lookup"><span data-stu-id="1df61-193">Click **Tools** > **Board** > **Boards Manager**, and then install the `Arduino SAMD Boards` version `1.6.2` or later</span></span> 

   <span data-ttu-id="1df61-194">Boards Manager indicates that `Arduino SAMD Boards` with a version of `1.6.2` or later is installed.</span><span class="sxs-lookup"><span data-stu-id="1df61-194">Boards Manager indicates that `Arduino SAMD Boards` with a version of `1.6.2` or later is installed.</span></span>

   ![The esp8266 package is installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

1. <span data-ttu-id="1df61-196">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="1df61-196">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

1. <span data-ttu-id="1df61-197">Install Drivers (Windows Only) When you plug in the Feather, you'll need to possibly install a driver Click [here](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) to download the Driver Installer.</span><span class="sxs-lookup"><span data-stu-id="1df61-197">Install Drivers (Windows Only) When you plug in the Feather, you'll need to possibly install a driver Click [here](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) to download the Driver Installer.</span></span>
   <span data-ttu-id="1df61-198">Follow the steps to install the drivers you want to install.</span><span class="sxs-lookup"><span data-stu-id="1df61-198">Follow the steps to install the drivers you want to install.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="1df61-199">Install necessary libraries</span><span class="sxs-lookup"><span data-stu-id="1df61-199">Install necessary libraries</span></span>

1. <span data-ttu-id="1df61-200">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span><span class="sxs-lookup"><span data-stu-id="1df61-200">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="1df61-201">Search for the following library names one by one.</span><span class="sxs-lookup"><span data-stu-id="1df61-201">Search for the following library names one by one.</span></span> <span data-ttu-id="1df61-202">For each  library that you find, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="1df61-202">For each  library that you find, click **Install**.</span></span>
   * `Adafruit_WINC1500`
   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-bme280-sensor"></a><span data-ttu-id="1df61-203">Don’t have a real BME280 sensor?</span><span class="sxs-lookup"><span data-stu-id="1df61-203">Don’t have a real BME280 sensor?</span></span>

<span data-ttu-id="1df61-204">The sample application can simulate temperature and humidity data in case you don’t have a real BME280 sensor.</span><span class="sxs-lookup"><span data-stu-id="1df61-204">The sample application can simulate temperature and humidity data in case you don’t have a real BME280 sensor.</span></span> <span data-ttu-id="1df61-205">To set up the sample application to use simulated data, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="1df61-205">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="1df61-206">Open the `config.h` file in the `app` folder.</span><span class="sxs-lookup"><span data-stu-id="1df61-206">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="1df61-207">Locate the following line of code and change the value from `false` to `true`:</span><span class="sxs-lookup"><span data-stu-id="1df61-207">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configure the sample application to use simulated data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="1df61-209">Save the file with `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="1df61-209">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-m0-wifi"></a><span data-ttu-id="1df61-210">Deploy the sample application to Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="1df61-210">Deploy the sample application to Feather M0 WiFi</span></span>

1. <span data-ttu-id="1df61-211">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="1df61-211">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather M0 WiFi.</span></span>
1. <span data-ttu-id="1df61-212">Click **Sketch** > **Upload** to build and deploy the sample application to Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="1df61-212">Click **Sketch** > **Upload** to build and deploy the sample application to Feather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="1df61-213">Enter your credentials</span><span class="sxs-lookup"><span data-stu-id="1df61-213">Enter your credentials</span></span>

<span data-ttu-id="1df61-214">After the upload completes successfully, follow these steps to enter your credentials:</span><span class="sxs-lookup"><span data-stu-id="1df61-214">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="1df61-215">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="1df61-215">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="1df61-216">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span><span class="sxs-lookup"><span data-stu-id="1df61-216">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="1df61-217">Select **No line ending** for the left drop-down list.</span><span class="sxs-lookup"><span data-stu-id="1df61-217">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="1df61-218">Select **115200 baud** for the right drop-down list.</span><span class="sxs-lookup"><span data-stu-id="1df61-218">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="1df61-219">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span><span class="sxs-lookup"><span data-stu-id="1df61-219">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="1df61-220">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="1df61-220">Wi-Fi SSID</span></span>
   * <span data-ttu-id="1df61-221">Wi-Fi password</span><span class="sxs-lookup"><span data-stu-id="1df61-221">Wi-Fi password</span></span>
   * <span data-ttu-id="1df61-222">Device connection string</span><span class="sxs-lookup"><span data-stu-id="1df61-222">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="1df61-223">The credential information is stored in the EEPROM of Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="1df61-223">The credential information is stored in the EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="1df61-224">If you click the reset button on the Feather M0 WiFi board, the sample application asks if you want to erase the information.</span><span class="sxs-lookup"><span data-stu-id="1df61-224">If you click the reset button on the Feather M0 WiFi board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="1df61-225">Enter `Y` to have the information erased.</span><span class="sxs-lookup"><span data-stu-id="1df61-225">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="1df61-226">You are asked to provide the information a second time.</span><span class="sxs-lookup"><span data-stu-id="1df61-226">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="1df61-227">Verify the sample application is running successfully</span><span class="sxs-lookup"><span data-stu-id="1df61-227">Verify the sample application is running successfully</span></span>

<span data-ttu-id="1df61-228">If you see the following output from the serial monitor window and the blinking LED on Feather M0 WiFi, the sample application is running successfully.</span><span class="sxs-lookup"><span data-stu-id="1df61-228">If you see the following output from the serial monitor window and the blinking LED on Feather M0 WiFi, the sample application is running successfully.</span></span>

![Final output in Arduino IDE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="1df61-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="1df61-230">Next steps</span></span>

<span data-ttu-id="1df61-231">You have successfully connected a Feather M0 WiFi to your IoT hub, and sent the captured sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1df61-231">You have successfully connected a Feather M0 WiFi to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]










