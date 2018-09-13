---
title: ESP8266 to cloud - Connect Feather HUZZAH ESP8266 to Azure IoT Hub | Microsoft Docs
description: Learn how to setup and connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub for it to send data to the Azure cloud platform in this tutorial.
author: rangv
manager: nasing
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 04/11/2018
ms.author: rangv
ms.openlocfilehash: ea7754c9bf755a5fc00823629df17317be0f8901
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44786960"
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="bfa0a-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span><span class="sxs-lookup"><span data-stu-id="bfa0a-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connection between DHT22, Feather HUZZAH ESP8266, and IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="bfa0a-105">What you do</span><span class="sxs-lookup"><span data-stu-id="bfa0a-105">What you do</span></span>

<span data-ttu-id="bfa0a-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="bfa0a-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="bfa0a-108">Finally, you send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="bfa0a-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="bfa0a-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="bfa0a-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="bfa0a-112">Don't have a kit yet?</span><span class="sxs-lookup"><span data-stu-id="bfa0a-112">Don't have a kit yet?</span></span> <span data-ttu-id="bfa0a-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="bfa0a-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="bfa0a-114">What you learn</span><span class="sxs-lookup"><span data-stu-id="bfa0a-114">What you learn</span></span>

* <span data-ttu-id="bfa0a-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="bfa0a-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="bfa0a-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span><span class="sxs-lookup"><span data-stu-id="bfa0a-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="bfa0a-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="bfa0a-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="bfa0a-118">How to send the sensor data to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="bfa0a-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bfa0a-119">What you need</span><span class="sxs-lookup"><span data-stu-id="bfa0a-119">What you need</span></span>

![Parts needed for the tutorial](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="bfa0a-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="bfa0a-122">The Feather HUZZAH ESP8266 board</span><span class="sxs-lookup"><span data-stu-id="bfa0a-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="bfa0a-123">A Micro USB to Type A USB cable</span><span class="sxs-lookup"><span data-stu-id="bfa0a-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="bfa0a-124">You also need the following things for your development environment:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="bfa0a-125">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-125">An active Azure subscription.</span></span> <span data-ttu-id="bfa0a-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="bfa0a-127">A Mac or PC that is running Windows or Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-127">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="bfa0a-128">A wireless network for Feather HUZZAH ESP8266 to connect to.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-128">A wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="bfa0a-129">An Internet connection to download the configuration tool.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-129">An Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="bfa0a-130">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino).</span><span class="sxs-lookup"><span data-stu-id="bfa0a-130">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino).</span></span>

> [!Note]
> <span data-ttu-id="bfa0a-131">The Arduino IDE version used by Visual Studio Code extension for Arduino has to be version 1.6.8 or later.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-131">The Arduino IDE version used by Visual Studio Code extension for Arduino has to be version 1.6.8 or later.</span></span> <span data-ttu-id="bfa0a-132">Earlier versions don't work with the AzureIoT library.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-132">Earlier versions don't work with the AzureIoT library.</span></span>

<span data-ttu-id="bfa0a-133">The following items are optional in case you don’t have a sensor.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-133">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="bfa0a-134">You also have the option of using simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-134">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="bfa0a-135">An Adafruit DHT22 temperature and humidity sensor</span><span class="sxs-lookup"><span data-stu-id="bfa0a-135">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="bfa0a-136">A breadboard</span><span class="sxs-lookup"><span data-stu-id="bfa0a-136">A breadboard</span></span>
* <span data-ttu-id="bfa0a-137">M/M jumper wires</span><span class="sxs-lookup"><span data-stu-id="bfa0a-137">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="bfa0a-138">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span><span class="sxs-lookup"><span data-stu-id="bfa0a-138">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>

<span data-ttu-id="bfa0a-139">In this section, you connect the sensors to your board.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-139">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="bfa0a-140">Then you plug in your device to your computer for further use.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-140">Then you plug in your device to your computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="bfa0a-141">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="bfa0a-141">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="bfa0a-142">Use the breadboard and jumper wires to make the connection as follows.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-142">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="bfa0a-143">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-143">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Connections reference](media/iot-hub-arduino-huzzah-esp8266-get-started/17_connections_on_breadboard.png)

<span data-ttu-id="bfa0a-145">For sensor pins, use the following wiring:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-145">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="bfa0a-146">Start (Sensor)</span><span class="sxs-lookup"><span data-stu-id="bfa0a-146">Start (Sensor)</span></span>           | <span data-ttu-id="bfa0a-147">End (Board)</span><span class="sxs-lookup"><span data-stu-id="bfa0a-147">End (Board)</span></span>            | <span data-ttu-id="bfa0a-148">Cable Color</span><span class="sxs-lookup"><span data-stu-id="bfa0a-148">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------  |
| <span data-ttu-id="bfa0a-149">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="bfa0a-149">VDD (Pin 31F)</span></span>            | <span data-ttu-id="bfa0a-150">3V (Pin 58H)</span><span class="sxs-lookup"><span data-stu-id="bfa0a-150">3V (Pin 58H)</span></span>           | <span data-ttu-id="bfa0a-151">Red cable</span><span class="sxs-lookup"><span data-stu-id="bfa0a-151">Red cable</span></span>     |
| <span data-ttu-id="bfa0a-152">DATA (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="bfa0a-152">DATA (Pin 32F)</span></span>           | <span data-ttu-id="bfa0a-153">GPIO 2 (Pin 46A)</span><span class="sxs-lookup"><span data-stu-id="bfa0a-153">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="bfa0a-154">Blue cable</span><span class="sxs-lookup"><span data-stu-id="bfa0a-154">Blue cable</span></span>    |
| <span data-ttu-id="bfa0a-155">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="bfa0a-155">GND (Pin 34F)</span></span>            | <span data-ttu-id="bfa0a-156">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="bfa0a-156">GND (PIn 56I)</span></span>          | <span data-ttu-id="bfa0a-157">Black cable</span><span class="sxs-lookup"><span data-stu-id="bfa0a-157">Black cable</span></span>   |

<span data-ttu-id="bfa0a-158">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="bfa0a-158">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>

<span data-ttu-id="bfa0a-159">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-159">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Connect DHT22 with Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="bfa0a-161">Connect Feather HUZZAH ESP8266 to your computer</span><span class="sxs-lookup"><span data-stu-id="bfa0a-161">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="bfa0a-162">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-162">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Connect Feather Huzzah to your computer](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="bfa0a-164">Add serial port permissions (Ubuntu only)</span><span class="sxs-lookup"><span data-stu-id="bfa0a-164">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="bfa0a-165">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-165">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="bfa0a-166">To add serial port permissions, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-166">To add serial port permissions, follow these steps:</span></span>

1. <span data-ttu-id="bfa0a-167">Run the following commands at a terminal:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-167">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="bfa0a-168">You get one of the following outputs:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-168">You get one of the following outputs:</span></span>

   * <span data-ttu-id="bfa0a-169">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="bfa0a-169">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="bfa0a-170">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="bfa0a-170">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="bfa0a-171">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-171">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

2. <span data-ttu-id="bfa0a-172">Add the user to the group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-172">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="bfa0a-173">`<group-owner-name>` is the group owner name you obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-173">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="bfa0a-174">`<username>` is your Ubuntu user name.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-174">`<username>` is your Ubuntu user name.</span></span>

3. <span data-ttu-id="bfa0a-175">Sign out of Ubuntu, and then sign in again for the change to appear.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-175">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="bfa0a-176">Collect sensor data and send it to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="bfa0a-176">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="bfa0a-177">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-177">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="bfa0a-178">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-178">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="bfa0a-179">Get the sample application from GitHub</span><span class="sxs-lookup"><span data-stu-id="bfa0a-179">Get the sample application from GitHub</span></span>

<span data-ttu-id="bfa0a-180">The sample application is hosted on GitHub.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-180">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="bfa0a-181">Clone the sample repository that contains the sample application from GitHub.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-181">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="bfa0a-182">To clone the sample repository, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-182">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="bfa0a-183">Open a command prompt or a terminal window.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-183">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="bfa0a-184">Go to a folder where you want the sample application to be stored.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-184">Go to a folder where you want the sample application to be stored.</span></span>

3. <span data-ttu-id="bfa0a-185">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-185">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

   <span data-ttu-id="bfa0a-186">Next, install the package for Feather HUZZAH ESP8266 in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-186">Next, install the package for Feather HUZZAH ESP8266 in Visual Studio Code.</span></span>

4. <span data-ttu-id="bfa0a-187">Open the folder where the sample application is stored.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-187">Open the folder where the sample application is stored.</span></span>

5. <span data-ttu-id="bfa0a-188">Open the app.ino file in the app folder in the Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-188">Open the app.ino file in the app folder in the Visual Studio Code.</span></span>

   ![Open the sample application in Visual Studio Code](media/iot-hub-arduino-huzzah-esp8266-get-started/10_vscode-open-sample-app.png)

6. <span data-ttu-id="bfa0a-190">In the Visual Studio Code, enter `F1`.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-190">In the Visual Studio Code, enter `F1`.</span></span>

7. <span data-ttu-id="bfa0a-191">Type **Arduino** and select **Arduino: Board Manager**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-191">Type **Arduino** and select **Arduino: Board Manager**.</span></span>

8. <span data-ttu-id="bfa0a-192">In the **Arduino Board Manager** tab, click **Additional URLs**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-192">In the **Arduino Board Manager** tab, click **Additional URLs**.</span></span>

   ![VS Code Arduino Board Manager](media/iot-hub-arduino-huzzah-esp8266-get-started/11_vscode-arduino-board-manager.png)

9. <span data-ttu-id="bfa0a-194">In the **User Settings** window, copy and paste the following at the end of the file</span><span class="sxs-lookup"><span data-stu-id="bfa0a-194">In the **User Settings** window, copy and paste the following at the end of the file</span></span>

   ```
   "arduino.additionalUrls": "http://arduino.esp8266.com/stable/package_esp8266com_index.json"
   ```
   
   ![Configure Arduino package URL in VS Code](media/iot-hub-arduino-huzzah-esp8266-get-started/12_vscode-package-url.png)

10. <span data-ttu-id="bfa0a-196">Save the file and close the **User Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-196">Save the file and close the **User Settings** tab.</span></span>

11. <span data-ttu-id="bfa0a-197">Click **Refresh Package Indexes**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-197">Click **Refresh Package Indexes**.</span></span> <span data-ttu-id="bfa0a-198">After the refresh finishes, search for **esp8266**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-198">After the refresh finishes, search for **esp8266**.</span></span>

12. <span data-ttu-id="bfa0a-199">Click **Install** button for esp8266.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-199">Click **Install** button for esp8266.</span></span>

   <span data-ttu-id="bfa0a-200">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-200">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![The esp8266 package is installed](media/iot-hub-arduino-huzzah-esp8266-get-started/13_vscode-esp8266-installed.png)

13. <span data-ttu-id="bfa0a-202">Enter `F1`, then type **Arduino** and select **Arduino: Board Config**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-202">Enter `F1`, then type **Arduino** and select **Arduino: Board Config**.</span></span>

14. <span data-ttu-id="bfa0a-203">Click box for **Selected Board:** and type **esp8266**, then select **Adafruit HUZZAH ESP8266 (esp8266)**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-203">Click box for **Selected Board:** and type **esp8266**, then select **Adafruit HUZZAH ESP8266 (esp8266)**.</span></span>

   ![Select esp8266 board](media/iot-hub-arduino-huzzah-esp8266-get-started/14_vscode-select-esp8266.png)

### <a name="install-necessary-libraries"></a><span data-ttu-id="bfa0a-205">Install necessary libraries</span><span class="sxs-lookup"><span data-stu-id="bfa0a-205">Install necessary libraries</span></span>

1. <span data-ttu-id="bfa0a-206">In the Visual Studio Code, enter `F1`, then type **Arduino** and select **Arduino: Library Manager**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-206">In the Visual Studio Code, enter `F1`, then type **Arduino** and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="bfa0a-207">Search for the following library names one by one.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-207">Search for the following library names one by one.</span></span> <span data-ttu-id="bfa0a-208">For each library that you find, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-208">For each library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="bfa0a-209">Don’t have a real DHT22 sensor?</span><span class="sxs-lookup"><span data-stu-id="bfa0a-209">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="bfa0a-210">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-210">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="bfa0a-211">To set up the sample application to use simulated data, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-211">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="bfa0a-212">Open the `config.h` file in the `app` folder.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-212">Open the `config.h` file in the `app` folder.</span></span>

2. <span data-ttu-id="bfa0a-213">Locate the following line of code and change the value from `false` to `true`:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-213">Locate the following line of code and change the value from `false` to `true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   
   ![Configure the sample application to use simulated data](media/iot-hub-arduino-huzzah-esp8266-get-started/15_vscode-configure-app-use-simulated-data.png)

3. <span data-ttu-id="bfa0a-215">Save the file.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-215">Save the file.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="bfa0a-216">Deploy the sample application to Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="bfa0a-216">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="bfa0a-217">In the Visual Studio Code, click **<Select Serial Port>** on the status bar, and then click the serial port for Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-217">In the Visual Studio Code, click **<Select Serial Port>** on the status bar, and then click the serial port for Feather HUZZAH ESP8266.</span></span>

2. <span data-ttu-id="bfa0a-218">Enter `F1`, then type **Arduino** and select **Arduino: Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-218">Enter `F1`, then type **Arduino** and select **Arduino: Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="bfa0a-219">Enter your credentials</span><span class="sxs-lookup"><span data-stu-id="bfa0a-219">Enter your credentials</span></span>

<span data-ttu-id="bfa0a-220">After the upload completes successfully, follow these steps to enter your credentials:</span><span class="sxs-lookup"><span data-stu-id="bfa0a-220">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="bfa0a-221">Open Arduino IDE, click **Tools** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-221">Open Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="bfa0a-222">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-222">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>

3. <span data-ttu-id="bfa0a-223">Select **No line ending** for the left drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-223">Select **No line ending** for the left drop-down list.</span></span>

4. <span data-ttu-id="bfa0a-224">Select **115200 baud** for the right drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-224">Select **115200 baud** for the right drop-down list.</span></span>

5. <span data-ttu-id="bfa0a-225">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-225">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>

   * <span data-ttu-id="bfa0a-226">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="bfa0a-226">Wi-Fi SSID</span></span>
   * <span data-ttu-id="bfa0a-227">Wi-Fi password</span><span class="sxs-lookup"><span data-stu-id="bfa0a-227">Wi-Fi password</span></span>
   * <span data-ttu-id="bfa0a-228">Device connection string</span><span class="sxs-lookup"><span data-stu-id="bfa0a-228">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="bfa0a-229">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-229">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="bfa0a-230">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-230">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="bfa0a-231">Enter `Y` to have the information erased.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-231">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="bfa0a-232">You are asked to provide the information a second time.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-232">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="bfa0a-233">Verify the sample application is running successfully</span><span class="sxs-lookup"><span data-stu-id="bfa0a-233">Verify the sample application is running successfully</span></span>

<span data-ttu-id="bfa0a-234">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-234">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Final output in Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/16_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="bfa0a-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfa0a-236">Next steps</span></span>

<span data-ttu-id="bfa0a-237">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bfa0a-237">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]