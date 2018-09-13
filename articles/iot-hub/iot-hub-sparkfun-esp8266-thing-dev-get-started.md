---
title: ESP8266 to cloud - Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub | Microsoft Docs
description: A guide to connecting an Arduino device, Sparkfun ESP8266 Thing Dev, to Azure IoT Hub which is a Microsoft cloud service that helps manage your IoT assets.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: ''
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: xshi
ms.openlocfilehash: 6b15e9a910c1fb1125a0a218a9d6adafdd229564
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550062"
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="88bb5-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span><span class="sxs-lookup"><span data-stu-id="88bb5-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![connection between DHT22, Thing Dev, and IoT Hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="88bb5-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="88bb5-105">What you will do</span></span>

<span data-ttu-id="88bb5-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span><span class="sxs-lookup"><span data-stu-id="88bb5-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="88bb5-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span><span class="sxs-lookup"><span data-stu-id="88bb5-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="88bb5-108">Finally, send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="88bb5-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="88bb5-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="88bb5-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="88bb5-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span><span class="sxs-lookup"><span data-stu-id="88bb5-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="88bb5-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="88bb5-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="88bb5-113">What you will learn</span><span class="sxs-lookup"><span data-stu-id="88bb5-113">What you will learn</span></span>

* <span data-ttu-id="88bb5-114">How to create an IoT hub and register a device for Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="88bb5-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="88bb5-115">How to connect Thing Dev with the sensor and your computer.</span><span class="sxs-lookup"><span data-stu-id="88bb5-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="88bb5-116">How to collect sensor data by running a sample application on Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="88bb5-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="88bb5-117">How to send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="88bb5-118">What you will need</span><span class="sxs-lookup"><span data-stu-id="88bb5-118">What you will need</span></span>

![parts needed for the tutorial](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="88bb5-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="88bb5-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="88bb5-121">The Sparkfun ESP8266 Thing Dev board.</span><span class="sxs-lookup"><span data-stu-id="88bb5-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="88bb5-122">A Micro USB to Type A USB cable.</span><span class="sxs-lookup"><span data-stu-id="88bb5-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="88bb5-123">You also need the following for your development environment:</span><span class="sxs-lookup"><span data-stu-id="88bb5-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="88bb5-124">Mac or PC that is running Windows or Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="88bb5-124">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="88bb5-125">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span><span class="sxs-lookup"><span data-stu-id="88bb5-125">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="88bb5-126">Internet connection to download the configuration tool.</span><span class="sxs-lookup"><span data-stu-id="88bb5-126">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="88bb5-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span><span class="sxs-lookup"><span data-stu-id="88bb5-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="88bb5-128">The following items are optional in case you don’t have a sensor.</span><span class="sxs-lookup"><span data-stu-id="88bb5-128">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="88bb5-129">You also have the option of using simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="88bb5-129">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="88bb5-130">An Adafruit DHT22 temperature and humidity sensor.</span><span class="sxs-lookup"><span data-stu-id="88bb5-130">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="88bb5-131">A breadboard.</span><span class="sxs-lookup"><span data-stu-id="88bb5-131">A breadboard.</span></span>
* <span data-ttu-id="88bb5-132">M/M jumper wires.</span><span class="sxs-lookup"><span data-stu-id="88bb5-132">M/M jumper wires.</span></span>

## <a name="create-an-iot-hub-and-register-a-device-for-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="88bb5-133">Create an IoT hub and register a device for Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="88bb5-133">Create an IoT hub and register a device for Sparkfun ESP8266 Thing Dev</span></span>

### <a name="create-your-azure-iot-hub-in-the-azure-portal"></a><span data-ttu-id="88bb5-134">Create your Azure IoT hub in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="88bb5-134">Create your Azure IoT hub in the Azure portal</span></span>

1. <span data-ttu-id="88bb5-135">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="88bb5-135">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
1. <span data-ttu-id="88bb5-136">Click **New** > **Internet of Things** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-136">Click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![create iot hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/3_iot-hub-creation.png)

1. <span data-ttu-id="88bb5-138">In the **IoT hub** pane, enter the necessary information for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="88bb5-138">In the **IoT hub** pane, enter the necessary information for your IoT hub:</span></span>

   ![basic information for iot hub creation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/4_iot-hub-provide-basic-info.png)

   * <span data-ttu-id="88bb5-140">**Name**: The name for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-140">**Name**: The name for your IoT hub.</span></span> <span data-ttu-id="88bb5-141">If the name you enter is valid, a green check mark appears.</span><span class="sxs-lookup"><span data-stu-id="88bb5-141">If the name you enter is valid, a green check mark appears.</span></span>
   * <span data-ttu-id="88bb5-142">**Pricing and scale tier**: Select the free F1 tier, will suffice for this demo.</span><span class="sxs-lookup"><span data-stu-id="88bb5-142">**Pricing and scale tier**: Select the free F1 tier, will suffice for this demo.</span></span> <span data-ttu-id="88bb5-143">See [pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="88bb5-143">See [pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>
   * <span data-ttu-id="88bb5-144">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="88bb5-144">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span></span> <span data-ttu-id="88bb5-145">See [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="88bb5-145">See [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>
   * <span data-ttu-id="88bb5-146">**Location**: Select the closest location to you where the IoT hub is created.</span><span class="sxs-lookup"><span data-stu-id="88bb5-146">**Location**: Select the closest location to you where the IoT hub is created.</span></span>
   * <span data-ttu-id="88bb5-147">**Pin the dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="88bb5-147">**Pin the dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>
1. <span data-ttu-id="88bb5-148">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-148">Click **Create**.</span></span> <span data-ttu-id="88bb5-149">It could take a few minutes for your IoT hub to be created.</span><span class="sxs-lookup"><span data-stu-id="88bb5-149">It could take a few minutes for your IoT hub to be created.</span></span> <span data-ttu-id="88bb5-150">You can see progress in the **Notifications** pane.</span><span class="sxs-lookup"><span data-stu-id="88bb5-150">You can see progress in the **Notifications** pane.</span></span>

   ![monitor the iot hub creation progress in the notification pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/5_iot-hub-monitor-creation-progress-notification-pane.png)

1. <span data-ttu-id="88bb5-152">Once your IoT hub is created, click it from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="88bb5-152">Once your IoT hub is created, click it from the dashboard.</span></span> <span data-ttu-id="88bb5-153">Make a note of the **Hostname** that is used later, and then click **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-153">Make a note of the **Hostname** that is used later, and then click **Shared access policies**.</span></span>

   ![get hostname of your IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/6_iot-hub-get-hostname.png)

1. <span data-ttu-id="88bb5-155">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and make a note of the **Connection string** of your IoT hub that is used later.</span><span class="sxs-lookup"><span data-stu-id="88bb5-155">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and make a note of the **Connection string** of your IoT hub that is used later.</span></span> <span data-ttu-id="88bb5-156">For more information, see [Control access to IoT Hub](iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="88bb5-156">For more information, see [Control access to IoT Hub](iot-hub-devguide-security.md).</span></span>

   ![get iot hub connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/7_iot-hub-get-connection-string.png)

<span data-ttu-id="88bb5-158">You have now created your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-158">You have now created your IoT hub.</span></span> <span data-ttu-id="88bb5-159">The host name and connection string that you noted down will be used later.</span><span class="sxs-lookup"><span data-stu-id="88bb5-159">The host name and connection string that you noted down will be used later.</span></span>

### <a name="register-a-device-for-sparkfun-esp8266-thing-dev-in-your-iot-hub"></a><span data-ttu-id="88bb5-160">Register a device for Sparkfun ESP8266 Thing Dev in your IoT hub</span><span class="sxs-lookup"><span data-stu-id="88bb5-160">Register a device for Sparkfun ESP8266 Thing Dev in your IoT hub</span></span>

<span data-ttu-id="88bb5-161">Every IoT hub has an identity registry that stores information about the devices that are permitted to connect to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-161">Every IoT hub has an identity registry that stores information about the devices that are permitted to connect to the IoT hub.</span></span> <span data-ttu-id="88bb5-162">Before a device can connect to an IoT hub, there must be an entry for that device in the IoT hub's identity registry.</span><span class="sxs-lookup"><span data-stu-id="88bb5-162">Before a device can connect to an IoT hub, there must be an entry for that device in the IoT hub's identity registry.</span></span>

<span data-ttu-id="88bb5-163">In this section, you will use a CLI tool iothub explorer to register a device for ESP8266 Thing Dev in the identity registry of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-163">In this section, you will use a CLI tool iothub explorer to register a device for ESP8266 Thing Dev in the identity registry of your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="88bb5-164">iothub explorer requires Node.js 4.x or higher to work properly.</span><span class="sxs-lookup"><span data-stu-id="88bb5-164">iothub explorer requires Node.js 4.x or higher to work properly.</span></span>

<span data-ttu-id="88bb5-165">To register a device for ESP8266 Thing Dev, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="88bb5-165">To register a device for ESP8266 Thing Dev, follow these steps:</span></span>

1. <span data-ttu-id="88bb5-166">[Download](https://nodejs.org/en/download/) and install the latest LTS version of Node.js, NPM included.</span><span class="sxs-lookup"><span data-stu-id="88bb5-166">[Download](https://nodejs.org/en/download/) and install the latest LTS version of Node.js, NPM included.</span></span>
1. <span data-ttu-id="88bb5-167">Install iothub explorer by using NPM.</span><span class="sxs-lookup"><span data-stu-id="88bb5-167">Install iothub explorer by using NPM.</span></span>

   * <span data-ttu-id="88bb5-168">Windows 7 or later Start a command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="88bb5-168">Windows 7 or later Start a command prompt as an administrator.</span></span> <span data-ttu-id="88bb5-169">Install iothub explorer by running the following command:</span><span class="sxs-lookup"><span data-stu-id="88bb5-169">Install iothub explorer by running the following command:</span></span>

     ```bash
     npm install -g iothub-explorer
     ```
   * <span data-ttu-id="88bb5-170">Ubuntu 16.04 or later Open a terminal by using the keyboard shortcut Ctrl + Alt + T, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="88bb5-170">Ubuntu 16.04 or later Open a terminal by using the keyboard shortcut Ctrl + Alt + T, and then run the following command:</span></span>

     ```bash
     sudo npm install -g iothub-explorer
     ```
   * <span data-ttu-id="88bb5-171">macOS 10.1 or later Open a terminal, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="88bb5-171">macOS 10.1 or later Open a terminal, and then run the following command:</span></span>

     ```bash
     npm install -g iothub-explorer
     ```
1. <span data-ttu-id="88bb5-172">Log in to your IoT hub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="88bb5-172">Log in to your IoT hub by running the following command:</span></span>

   ```bash
   iothub-explorer login [your iot hub connection string]
   ```
1. <span data-ttu-id="88bb5-173">Register a new device, which `deviceID` is `new-device`, and get its connection string by running the following command.</span><span class="sxs-lookup"><span data-stu-id="88bb5-173">Register a new device, which `deviceID` is `new-device`, and get its connection string by running the following command.</span></span>

   ```bash
   iothub-explorer create new-device --connection-string
   ```

<span data-ttu-id="88bb5-174">Make a note of the connection string of the registered device, it will be used later.</span><span class="sxs-lookup"><span data-stu-id="88bb5-174">Make a note of the connection string of the registered device, it will be used later.</span></span>

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="88bb5-175">Connect ESP8266 Thing Dev with the sensor and your computer</span><span class="sxs-lookup"><span data-stu-id="88bb5-175">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="88bb5-176">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="88bb5-176">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="88bb5-177">Use the breadboard and jumper wires to make the connection as follows.</span><span class="sxs-lookup"><span data-stu-id="88bb5-177">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="88bb5-178">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span><span class="sxs-lookup"><span data-stu-id="88bb5-178">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![connections reference](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="88bb5-180">For sensor pins, we will use the following wiring:</span><span class="sxs-lookup"><span data-stu-id="88bb5-180">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="88bb5-181">Start (Sensor)</span><span class="sxs-lookup"><span data-stu-id="88bb5-181">Start (Sensor)</span></span>           | <span data-ttu-id="88bb5-182">End (Board)</span><span class="sxs-lookup"><span data-stu-id="88bb5-182">End (Board)</span></span>           | <span data-ttu-id="88bb5-183">Cable Color</span><span class="sxs-lookup"><span data-stu-id="88bb5-183">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="88bb5-184">VDD (Pin 27F)</span><span class="sxs-lookup"><span data-stu-id="88bb5-184">VDD (Pin 27F)</span></span>            | <span data-ttu-id="88bb5-185">3V (Pin 8A)</span><span class="sxs-lookup"><span data-stu-id="88bb5-185">3V (Pin 8A)</span></span>           | <span data-ttu-id="88bb5-186">Red cable</span><span class="sxs-lookup"><span data-stu-id="88bb5-186">Red cable</span></span>     |
| <span data-ttu-id="88bb5-187">DATA (Pin 28F)</span><span class="sxs-lookup"><span data-stu-id="88bb5-187">DATA (Pin 28F)</span></span>           | <span data-ttu-id="88bb5-188">GPIO 2 (Pin 9A)</span><span class="sxs-lookup"><span data-stu-id="88bb5-188">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="88bb5-189">White cable</span><span class="sxs-lookup"><span data-stu-id="88bb5-189">White cable</span></span>    |
| <span data-ttu-id="88bb5-190">GND (Pin 30F)</span><span class="sxs-lookup"><span data-stu-id="88bb5-190">GND (Pin 30F)</span></span>            | <span data-ttu-id="88bb5-191">GND (Pin 7J)</span><span class="sxs-lookup"><span data-stu-id="88bb5-191">GND (Pin 7J)</span></span>          | <span data-ttu-id="88bb5-192">Black cable</span><span class="sxs-lookup"><span data-stu-id="88bb5-192">Black cable</span></span>   |


- <span data-ttu-id="88bb5-193">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="88bb5-193">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="88bb5-194">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span><span class="sxs-lookup"><span data-stu-id="88bb5-194">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![connect dht22 with ESP8266 Thing Dev](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="88bb5-196">Connect Sparkfun ESP8266 Thing Dev to your computer</span><span class="sxs-lookup"><span data-stu-id="88bb5-196">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="88bb5-197">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span><span class="sxs-lookup"><span data-stu-id="88bb5-197">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![connect feather huzzah to your computer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="88bb5-199">Add serial port permissions – Ubuntu only</span><span class="sxs-lookup"><span data-stu-id="88bb5-199">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="88bb5-200">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="88bb5-200">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="88bb5-201">To add serial port permissions for a normal user, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="88bb5-201">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="88bb5-202">Run the following commands at a terminal:</span><span class="sxs-lookup"><span data-stu-id="88bb5-202">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="88bb5-203">You get one of the following outputs:</span><span class="sxs-lookup"><span data-stu-id="88bb5-203">You get one of the following outputs:</span></span>

   * <span data-ttu-id="88bb5-204">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="88bb5-204">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="88bb5-205">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="88bb5-205">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="88bb5-206">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span><span class="sxs-lookup"><span data-stu-id="88bb5-206">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="88bb5-207">Add the user to the group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="88bb5-207">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="88bb5-208">`<group-owner-name>` is the group owner name you obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="88bb5-208">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="88bb5-209">`<username>` is your Ubuntu user name.</span><span class="sxs-lookup"><span data-stu-id="88bb5-209">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="88bb5-210">Log out Ubuntu and log in it again for the change to take effect.</span><span class="sxs-lookup"><span data-stu-id="88bb5-210">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="88bb5-211">Collect sensor data and send it to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="88bb5-211">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="88bb5-212">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="88bb5-212">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="88bb5-213">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-213">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="88bb5-214">Get the sample application from GitHub</span><span class="sxs-lookup"><span data-stu-id="88bb5-214">Get the sample application from GitHub</span></span>

<span data-ttu-id="88bb5-215">The sample application is hosted on GitHub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-215">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="88bb5-216">Clone the sample repository that contains the sample application from GitHub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-216">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="88bb5-217">To clone the sample repository, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="88bb5-217">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="88bb5-218">Open a command prompt or a terminal window.</span><span class="sxs-lookup"><span data-stu-id="88bb5-218">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="88bb5-219">Go to a folder where you want the sample application to be stored.</span><span class="sxs-lookup"><span data-stu-id="88bb5-219">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="88bb5-220">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="88bb5-220">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="88bb5-221">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="88bb5-221">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="88bb5-222">Open the folder where the sample application is stored.</span><span class="sxs-lookup"><span data-stu-id="88bb5-222">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="88bb5-223">Open the app.ino file in the app folder in Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="88bb5-223">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![open the sample application in arduino ide](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="88bb5-225">In the Arduino IDE, click **File** > **Preferences**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-225">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="88bb5-226">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span><span class="sxs-lookup"><span data-stu-id="88bb5-226">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="88bb5-227">In the pop-up window, enter the following URL, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-227">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![point to a package url in arduino ide](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="88bb5-229">In the **Preference** dialog box, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-229">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="88bb5-230">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span><span class="sxs-lookup"><span data-stu-id="88bb5-230">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="88bb5-231">ESP8266 with a version of 2.2.0 or later should be installed.</span><span class="sxs-lookup"><span data-stu-id="88bb5-231">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![the esp8266 package is installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="88bb5-233">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-233">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="88bb5-234">Install necessary libraries</span><span class="sxs-lookup"><span data-stu-id="88bb5-234">Install necessary libraries</span></span>

1. <span data-ttu-id="88bb5-235">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-235">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="88bb5-236">Search for the following library names one by one.</span><span class="sxs-lookup"><span data-stu-id="88bb5-236">Search for the following library names one by one.</span></span> <span data-ttu-id="88bb5-237">For each of the library you find, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-237">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="88bb5-238">Don’t have a real DHT22 sensor?</span><span class="sxs-lookup"><span data-stu-id="88bb5-238">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="88bb5-239">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span><span class="sxs-lookup"><span data-stu-id="88bb5-239">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="88bb5-240">To enable the sample application to use simulated data, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="88bb5-240">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="88bb5-241">Open the `config.h` file in the `app` folder.</span><span class="sxs-lookup"><span data-stu-id="88bb5-241">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="88bb5-242">Locate the following line of code and change the value from `false` to `true`:</span><span class="sxs-lookup"><span data-stu-id="88bb5-242">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![configure the sample application to use simulated data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="88bb5-244">Save with `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="88bb5-244">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="88bb5-245">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="88bb5-245">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="88bb5-246">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="88bb5-246">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="88bb5-247">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="88bb5-247">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="88bb5-248">Enter your credentials</span><span class="sxs-lookup"><span data-stu-id="88bb5-248">Enter your credentials</span></span>

<span data-ttu-id="88bb5-249">After the upload completes successfully, follow the steps to enter your credentials:</span><span class="sxs-lookup"><span data-stu-id="88bb5-249">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="88bb5-250">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-250">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="88bb5-251">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span><span class="sxs-lookup"><span data-stu-id="88bb5-251">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="88bb5-252">Select **No line ending** for the left drop-down list.</span><span class="sxs-lookup"><span data-stu-id="88bb5-252">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="88bb5-253">Select **115200 baud** for the right drop-down list.</span><span class="sxs-lookup"><span data-stu-id="88bb5-253">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="88bb5-254">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-254">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="88bb5-255">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="88bb5-255">Wi-Fi SSID</span></span>
   * <span data-ttu-id="88bb5-256">Wi-Fi password</span><span class="sxs-lookup"><span data-stu-id="88bb5-256">Wi-Fi password</span></span>
   * <span data-ttu-id="88bb5-257">Device connection string</span><span class="sxs-lookup"><span data-stu-id="88bb5-257">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="88bb5-258">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="88bb5-258">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="88bb5-259">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span><span class="sxs-lookup"><span data-stu-id="88bb5-259">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="88bb5-260">Enter `Y` to have the information erased and you are asked to provide the information again.</span><span class="sxs-lookup"><span data-stu-id="88bb5-260">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="88bb5-261">Verify the sample application is running successfully</span><span class="sxs-lookup"><span data-stu-id="88bb5-261">Verify the sample application is running successfully</span></span>

<span data-ttu-id="88bb5-262">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span><span class="sxs-lookup"><span data-stu-id="88bb5-262">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![final output in arduino ide](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="88bb5-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="88bb5-264">Next steps</span></span>

<span data-ttu-id="88bb5-265">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="88bb5-265">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]















