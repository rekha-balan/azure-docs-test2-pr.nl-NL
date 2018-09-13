---
title: ESP8266 to cloud - Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub | Microsoft Docs
description: Learn how to setup and connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub for it to send data to the Azure cloud platform in this tutorial.
author: rangv
manager: ''
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 04/11/2018
ms.author: rangv
ms.openlocfilehash: 75ff53d5be29af08bb8e9c1b41f61040e5710cf7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776457"
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="d3634-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span><span class="sxs-lookup"><span data-stu-id="d3634-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![connection between DHT22, Thing Dev, and IoT Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="d3634-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="d3634-105">What you will do</span></span>

<span data-ttu-id="d3634-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span><span class="sxs-lookup"><span data-stu-id="d3634-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="d3634-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span><span class="sxs-lookup"><span data-stu-id="d3634-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="d3634-108">Finally, send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3634-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="d3634-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3634-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="d3634-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="d3634-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="d3634-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span><span class="sxs-lookup"><span data-stu-id="d3634-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="d3634-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="d3634-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d3634-113">What you will learn</span><span class="sxs-lookup"><span data-stu-id="d3634-113">What you will learn</span></span>

* <span data-ttu-id="d3634-114">How to create an IoT hub and register a device for Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="d3634-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="d3634-115">How to connect Thing Dev with the sensor and your computer.</span><span class="sxs-lookup"><span data-stu-id="d3634-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="d3634-116">How to collect sensor data by running a sample application on Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="d3634-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="d3634-117">How to send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3634-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="d3634-118">What you will need</span><span class="sxs-lookup"><span data-stu-id="d3634-118">What you will need</span></span>

![parts needed for the tutorial](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="d3634-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="d3634-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="d3634-121">The Sparkfun ESP8266 Thing Dev board.</span><span class="sxs-lookup"><span data-stu-id="d3634-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="d3634-122">A Micro USB to Type A USB cable.</span><span class="sxs-lookup"><span data-stu-id="d3634-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="d3634-123">You also need the following for your development environment:</span><span class="sxs-lookup"><span data-stu-id="d3634-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="d3634-124">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d3634-124">An active Azure subscription.</span></span> <span data-ttu-id="d3634-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="d3634-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="d3634-126">Mac or PC that is running Windows or Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d3634-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="d3634-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span><span class="sxs-lookup"><span data-stu-id="d3634-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="d3634-128">Internet connection to download the configuration tool.</span><span class="sxs-lookup"><span data-stu-id="d3634-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="d3634-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span><span class="sxs-lookup"><span data-stu-id="d3634-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="d3634-130">The following items are optional in case you don’t have a sensor.</span><span class="sxs-lookup"><span data-stu-id="d3634-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="d3634-131">You also have the option of using simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="d3634-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="d3634-132">An Adafruit DHT22 temperature and humidity sensor.</span><span class="sxs-lookup"><span data-stu-id="d3634-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="d3634-133">A breadboard.</span><span class="sxs-lookup"><span data-stu-id="d3634-133">A breadboard.</span></span>
* <span data-ttu-id="d3634-134">M/M jumper wires.</span><span class="sxs-lookup"><span data-stu-id="d3634-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="d3634-135">Connect ESP8266 Thing Dev with the sensor and your computer</span><span class="sxs-lookup"><span data-stu-id="d3634-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="d3634-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="d3634-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="d3634-137">Use the breadboard and jumper wires to make the connection as follows.</span><span class="sxs-lookup"><span data-stu-id="d3634-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="d3634-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span><span class="sxs-lookup"><span data-stu-id="d3634-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![connections reference](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="d3634-140">For sensor pins, we will use the following wiring:</span><span class="sxs-lookup"><span data-stu-id="d3634-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="d3634-141">Start (Sensor)</span><span class="sxs-lookup"><span data-stu-id="d3634-141">Start (Sensor)</span></span>           | <span data-ttu-id="d3634-142">End (Board)</span><span class="sxs-lookup"><span data-stu-id="d3634-142">End (Board)</span></span>           | <span data-ttu-id="d3634-143">Cable Color</span><span class="sxs-lookup"><span data-stu-id="d3634-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="d3634-144">VDD (Pin 27F)</span><span class="sxs-lookup"><span data-stu-id="d3634-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="d3634-145">3V (Pin 8A)</span><span class="sxs-lookup"><span data-stu-id="d3634-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="d3634-146">Red cable</span><span class="sxs-lookup"><span data-stu-id="d3634-146">Red cable</span></span>     |
| <span data-ttu-id="d3634-147">DATA (Pin 28F)</span><span class="sxs-lookup"><span data-stu-id="d3634-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="d3634-148">GPIO 2 (Pin 9A)</span><span class="sxs-lookup"><span data-stu-id="d3634-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="d3634-149">White cable</span><span class="sxs-lookup"><span data-stu-id="d3634-149">White cable</span></span>    |
| <span data-ttu-id="d3634-150">GND (Pin 30F)</span><span class="sxs-lookup"><span data-stu-id="d3634-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="d3634-151">GND (Pin 7J)</span><span class="sxs-lookup"><span data-stu-id="d3634-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="d3634-152">Black cable</span><span class="sxs-lookup"><span data-stu-id="d3634-152">Black cable</span></span>   |


- <span data-ttu-id="d3634-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="d3634-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="d3634-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span><span class="sxs-lookup"><span data-stu-id="d3634-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![connect dht22 with ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="d3634-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span><span class="sxs-lookup"><span data-stu-id="d3634-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="d3634-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span><span class="sxs-lookup"><span data-stu-id="d3634-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![connect feather huzzah to your computer](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="d3634-159">Add serial port permissions – Ubuntu only</span><span class="sxs-lookup"><span data-stu-id="d3634-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="d3634-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="d3634-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="d3634-161">To add serial port permissions for a normal user, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d3634-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="d3634-162">Run the following commands at a terminal:</span><span class="sxs-lookup"><span data-stu-id="d3634-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="d3634-163">You get one of the following outputs:</span><span class="sxs-lookup"><span data-stu-id="d3634-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="d3634-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="d3634-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="d3634-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="d3634-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="d3634-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span><span class="sxs-lookup"><span data-stu-id="d3634-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="d3634-167">Add the user to the group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="d3634-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="d3634-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="d3634-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="d3634-169">`<username>` is your Ubuntu user name.</span><span class="sxs-lookup"><span data-stu-id="d3634-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="d3634-170">Log out Ubuntu and log in it again for the change to take effect.</span><span class="sxs-lookup"><span data-stu-id="d3634-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="d3634-171">Collect sensor data and send it to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="d3634-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="d3634-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="d3634-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="d3634-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3634-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="d3634-174">Get the sample application from GitHub</span><span class="sxs-lookup"><span data-stu-id="d3634-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="d3634-175">The sample application is hosted on GitHub.</span><span class="sxs-lookup"><span data-stu-id="d3634-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="d3634-176">Clone the sample repository that contains the sample application from GitHub.</span><span class="sxs-lookup"><span data-stu-id="d3634-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="d3634-177">To clone the sample repository, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d3634-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="d3634-178">Open a command prompt or a terminal window.</span><span class="sxs-lookup"><span data-stu-id="d3634-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="d3634-179">Go to a folder where you want the sample application to be stored.</span><span class="sxs-lookup"><span data-stu-id="d3634-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="d3634-180">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="d3634-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="d3634-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="d3634-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="d3634-182">Open the folder where the sample application is stored.</span><span class="sxs-lookup"><span data-stu-id="d3634-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="d3634-183">Open the app.ino file in the app folder in Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="d3634-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![open the sample application in arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="d3634-185">In the Arduino IDE, click **File** > **Preferences**.</span><span class="sxs-lookup"><span data-stu-id="d3634-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="d3634-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span><span class="sxs-lookup"><span data-stu-id="d3634-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="d3634-187">In the pop-up window, enter the following URL, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3634-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![point to a package url in arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="d3634-189">In the **Preference** dialog box, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3634-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="d3634-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span><span class="sxs-lookup"><span data-stu-id="d3634-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="d3634-191">ESP8266 with a version of 2.2.0 or later should be installed.</span><span class="sxs-lookup"><span data-stu-id="d3634-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![the esp8266 package is installed](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="d3634-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="d3634-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="d3634-194">Install necessary libraries</span><span class="sxs-lookup"><span data-stu-id="d3634-194">Install necessary libraries</span></span>

1. <span data-ttu-id="d3634-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span><span class="sxs-lookup"><span data-stu-id="d3634-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="d3634-196">Search for the following library names one by one.</span><span class="sxs-lookup"><span data-stu-id="d3634-196">Search for the following library names one by one.</span></span> <span data-ttu-id="d3634-197">For each of the library you find, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="d3634-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="d3634-198">Don’t have a real DHT22 sensor?</span><span class="sxs-lookup"><span data-stu-id="d3634-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="d3634-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span><span class="sxs-lookup"><span data-stu-id="d3634-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="d3634-200">To enable the sample application to use simulated data, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d3634-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="d3634-201">Open the `config.h` file in the `app` folder.</span><span class="sxs-lookup"><span data-stu-id="d3634-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="d3634-202">Locate the following line of code and change the value from `false` to `true`:</span><span class="sxs-lookup"><span data-stu-id="d3634-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![configure the sample application to use simulated data](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="d3634-204">Save with `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="d3634-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="d3634-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="d3634-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="d3634-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="d3634-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="d3634-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="d3634-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="d3634-208">If you are using macOS you could probably see the following messages during uploading.</span><span class="sxs-lookup"><span data-stu-id="d3634-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="d3634-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="d3634-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="d3634-210">Please open your ternimal window and finish below actions to solve this issue.</span><span class="sxs-lookup"><span data-stu-id="d3634-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="d3634-211">Enter your credentials</span><span class="sxs-lookup"><span data-stu-id="d3634-211">Enter your credentials</span></span>

<span data-ttu-id="d3634-212">After the upload completes successfully, follow the steps to enter your credentials:</span><span class="sxs-lookup"><span data-stu-id="d3634-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="d3634-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="d3634-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="d3634-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span><span class="sxs-lookup"><span data-stu-id="d3634-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="d3634-215">Select **No line ending** for the left drop-down list.</span><span class="sxs-lookup"><span data-stu-id="d3634-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="d3634-216">Select **115200 baud** for the right drop-down list.</span><span class="sxs-lookup"><span data-stu-id="d3634-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="d3634-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span><span class="sxs-lookup"><span data-stu-id="d3634-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="d3634-218">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="d3634-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="d3634-219">Wi-Fi password</span><span class="sxs-lookup"><span data-stu-id="d3634-219">Wi-Fi password</span></span>
   * <span data-ttu-id="d3634-220">Device connection string</span><span class="sxs-lookup"><span data-stu-id="d3634-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="d3634-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="d3634-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="d3634-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span><span class="sxs-lookup"><span data-stu-id="d3634-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="d3634-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span><span class="sxs-lookup"><span data-stu-id="d3634-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="d3634-224">Verify the sample application is running successfully</span><span class="sxs-lookup"><span data-stu-id="d3634-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="d3634-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span><span class="sxs-lookup"><span data-stu-id="d3634-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![final output in arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="d3634-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3634-227">Next steps</span></span>

<span data-ttu-id="d3634-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3634-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
