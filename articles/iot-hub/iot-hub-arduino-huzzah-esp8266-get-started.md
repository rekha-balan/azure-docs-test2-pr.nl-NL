---
title: ESP8266 to cloud - Connect Feather HUZZAH ESP8266 to Azure IoT Hub | Microsoft Docs
description: Explains how to connect an Arduino device, called Adafruit Feather HUZZAH ESP8266, to Azure IoT Hub, which is a Microsoft cloud service that helps manage your IoT assets.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: ''
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: xshi
ms.openlocfilehash: dacfc9acd4ff9933834614e85d7c7079c509bd96
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551322"
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="4d94d-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span><span class="sxs-lookup"><span data-stu-id="4d94d-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connection between DHT22, Feather HUZZAH ESP8266, and IoT Hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="4d94d-105">What you do</span><span class="sxs-lookup"><span data-stu-id="4d94d-105">What you do</span></span>


<span data-ttu-id="4d94d-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span><span class="sxs-lookup"><span data-stu-id="4d94d-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="4d94d-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span><span class="sxs-lookup"><span data-stu-id="4d94d-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="4d94d-108">Finally, you send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="4d94d-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="4d94d-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="4d94d-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="4d94d-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span><span class="sxs-lookup"><span data-stu-id="4d94d-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="4d94d-112">Don't have a kit yet?</span><span class="sxs-lookup"><span data-stu-id="4d94d-112">Don't have a kit yet?</span></span> <span data-ttu-id="4d94d-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="4d94d-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="4d94d-114">What you learn</span><span class="sxs-lookup"><span data-stu-id="4d94d-114">What you learn</span></span>

* <span data-ttu-id="4d94d-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="4d94d-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="4d94d-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span><span class="sxs-lookup"><span data-stu-id="4d94d-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="4d94d-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="4d94d-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="4d94d-118">How to send the sensor data to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="4d94d-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4d94d-119">What you need</span><span class="sxs-lookup"><span data-stu-id="4d94d-119">What you need</span></span>

![Parts needed for the tutorial](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="4d94d-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="4d94d-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="4d94d-122">The Feather HUZZAH ESP8266 board</span><span class="sxs-lookup"><span data-stu-id="4d94d-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="4d94d-123">A Micro USB to Type A USB cable</span><span class="sxs-lookup"><span data-stu-id="4d94d-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="4d94d-124">You also need the following things for your development environment:</span><span class="sxs-lookup"><span data-stu-id="4d94d-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="4d94d-125">Mac or PC that is running Windows or Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="4d94d-125">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="4d94d-126">Wireless network for Feather HUZZAH ESP8266 to connect to.</span><span class="sxs-lookup"><span data-stu-id="4d94d-126">Wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="4d94d-127">Internet connection to download the configuration tool.</span><span class="sxs-lookup"><span data-stu-id="4d94d-127">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="4d94d-128">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span><span class="sxs-lookup"><span data-stu-id="4d94d-128">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="4d94d-129">Earlier versions don't work with the AzureIoT library.</span><span class="sxs-lookup"><span data-stu-id="4d94d-129">Earlier versions don't work with the AzureIoT library.</span></span>





<span data-ttu-id="4d94d-130">The following items are optional in case you don’t have a sensor.</span><span class="sxs-lookup"><span data-stu-id="4d94d-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="4d94d-131">You also have the option of using simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="4d94d-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="4d94d-132">An Adafruit DHT22 temperature and humidity sensor</span><span class="sxs-lookup"><span data-stu-id="4d94d-132">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="4d94d-133">A breadboard</span><span class="sxs-lookup"><span data-stu-id="4d94d-133">A breadboard</span></span>
* <span data-ttu-id="4d94d-134">M/M jumper wires</span><span class="sxs-lookup"><span data-stu-id="4d94d-134">M/M jumper wires</span></span>

## <a name="create-an-iot-hub-and-register-a-device-for-feather-huzzah-esp8266"></a><span data-ttu-id="4d94d-135">Create an IoT hub and register a device for Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="4d94d-135">Create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>

### <a name="to-create-your-iot-hub-in-the-azure-portal-follow-these-steps"></a><span data-ttu-id="4d94d-136">To create your IoT hub in the Azure portal, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="4d94d-136">To create your IoT hub in the Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="4d94d-137">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4d94d-137">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
1. <span data-ttu-id="4d94d-138">Click **New** > **Internet of Things** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-138">Click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Create IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/3_iot-hub-creation.png)

1. <span data-ttu-id="4d94d-140">In the **IoT hub** pane, enter the necessary information for your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="4d94d-140">In the **IoT hub** pane, enter the necessary information for your IoT hub:</span></span>

   ![Basic information for IoT hub creation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/4_iot-hub-provide-basic-info.png)

   * <span data-ttu-id="4d94d-142">**Name**: The name for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-142">**Name**: The name for your IoT hub.</span></span> <span data-ttu-id="4d94d-143">If the name you enter is valid, a green check mark appears.</span><span class="sxs-lookup"><span data-stu-id="4d94d-143">If the name you enter is valid, a green check mark appears.</span></span>
   * <span data-ttu-id="4d94d-144">**Pricing and scale tier**: Select the free F1 tier for this demo.</span><span class="sxs-lookup"><span data-stu-id="4d94d-144">**Pricing and scale tier**: Select the free F1 tier for this demo.</span></span> <span data-ttu-id="4d94d-145">See [pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="4d94d-145">See [pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>
   * <span data-ttu-id="4d94d-146">**Resource group**: Create a resource group to host the IoT hub, or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="4d94d-146">**Resource group**: Create a resource group to host the IoT hub, or use an existing one.</span></span> <span data-ttu-id="4d94d-147">See [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d94d-147">See [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>
   * <span data-ttu-id="4d94d-148">**Location**: Select the closest location to you where the IoT hub is created.</span><span class="sxs-lookup"><span data-stu-id="4d94d-148">**Location**: Select the closest location to you where the IoT hub is created.</span></span>
   * <span data-ttu-id="4d94d-149">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="4d94d-149">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

1. <span data-ttu-id="4d94d-150">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-150">Click **Create**.</span></span> <span data-ttu-id="4d94d-151">It could take a few minutes for your IoT hub to be created.</span><span class="sxs-lookup"><span data-stu-id="4d94d-151">It could take a few minutes for your IoT hub to be created.</span></span> <span data-ttu-id="4d94d-152">You can see progress in the **Notifications** pane.</span><span class="sxs-lookup"><span data-stu-id="4d94d-152">You can see progress in the **Notifications** pane.</span></span>

   ![Monitor the IoT hub creation progress in the notification pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/5_iot-hub-monitor-creation-progress-notification-pane.png)

1. <span data-ttu-id="4d94d-154">After your IoT hub is created, click it from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="4d94d-154">After your IoT hub is created, click it from the dashboard.</span></span> <span data-ttu-id="4d94d-155">Make a note of the **Hostname** value that is used later in this article, and then click **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-155">Make a note of the **Hostname** value that is used later in this article, and then click **Shared access policies**.</span></span>

   ![Get the Hostname of your IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/6_iot-hub-get-hostname.png)

1. <span data-ttu-id="4d94d-157">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and save the **Connection string** value for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-157">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and save the **Connection string** value for your IoT hub.</span></span> <span data-ttu-id="4d94d-158">You use this value later in this article.</span><span class="sxs-lookup"><span data-stu-id="4d94d-158">You use this value later in this article.</span></span> <span data-ttu-id="4d94d-159">For more information, see [Control access to IoT Hub](iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="4d94d-159">For more information, see [Control access to IoT Hub](iot-hub-devguide-security.md).</span></span>

   ![Get IoT hub connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/7_iot-hub-get-connection-string.png)

<span data-ttu-id="4d94d-161">You've now created your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-161">You've now created your IoT hub.</span></span> <span data-ttu-id="4d94d-162">Ensure that you save the **Hostname** and **Connection string** values.</span><span class="sxs-lookup"><span data-stu-id="4d94d-162">Ensure that you save the **Hostname** and **Connection string** values.</span></span> <span data-ttu-id="4d94d-163">They're used later in this article.</span><span class="sxs-lookup"><span data-stu-id="4d94d-163">They're used later in this article.</span></span>


### <a name="register-a-device-for-feather-huzzah-esp8266-in-your-iot-hub"></a><span data-ttu-id="4d94d-164">Register a device for Feather HUZZAH ESP8266 in your IoT hub</span><span class="sxs-lookup"><span data-stu-id="4d94d-164">Register a device for Feather HUZZAH ESP8266 in your IoT hub</span></span>

<span data-ttu-id="4d94d-165">Every IoT hub has an identity registry that stores information about the devices that are permitted to connect to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-165">Every IoT hub has an identity registry that stores information about the devices that are permitted to connect to the IoT hub.</span></span> <span data-ttu-id="4d94d-166">Before a device can connect to an IoT hub, there must be an entry for that device in the identity registry for that IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-166">Before a device can connect to an IoT hub, there must be an entry for that device in the identity registry for that IoT hub.</span></span>


<span data-ttu-id="4d94d-167">In this section, you use a CLI tool called *iothub explorer*.</span><span class="sxs-lookup"><span data-stu-id="4d94d-167">In this section, you use a CLI tool called *iothub explorer*.</span></span> <span data-ttu-id="4d94d-168">Use this tool to register a device for Feather HUZZAH ESP8266 in the identity registry of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-168">Use this tool to register a device for Feather HUZZAH ESP8266 in the identity registry of your IoT hub.</span></span>



> [!NOTE]
> <span data-ttu-id="4d94d-169">iothub explorer requires Node.js 4.x or later to work properly.</span><span class="sxs-lookup"><span data-stu-id="4d94d-169">iothub explorer requires Node.js 4.x or later to work properly.</span></span>

<span data-ttu-id="4d94d-170">To register a device for Feather HUZZAH ESP8266, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="4d94d-170">To register a device for Feather HUZZAH ESP8266, follow these steps:</span></span>

1. <span data-ttu-id="4d94d-171">[Download](https://nodejs.org/en/download/) and install the latest LTS version of Node.js, NPM included.</span><span class="sxs-lookup"><span data-stu-id="4d94d-171">[Download](https://nodejs.org/en/download/) and install the latest LTS version of Node.js, NPM included.</span></span>
1. <span data-ttu-id="4d94d-172">Install iothub explorer by using NPM.</span><span class="sxs-lookup"><span data-stu-id="4d94d-172">Install iothub explorer by using NPM.</span></span>

   * <span data-ttu-id="4d94d-173">Windows 7 or later:</span><span class="sxs-lookup"><span data-stu-id="4d94d-173">Windows 7 or later:</span></span>

     <span data-ttu-id="4d94d-174">Start a command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4d94d-174">Start a command prompt as an administrator.</span></span> <span data-ttu-id="4d94d-175">Install iothub explorer by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4d94d-175">Install iothub explorer by running the following command:</span></span>

     ```bash
     npm install -g iothub-explorer
     ```

   * <span data-ttu-id="4d94d-176">Ubuntu 16.04 or later:</span><span class="sxs-lookup"><span data-stu-id="4d94d-176">Ubuntu 16.04 or later:</span></span>

     <span data-ttu-id="4d94d-177">Open a terminal by using the keyboard shortcut Ctrl+Alt+T, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="4d94d-177">Open a terminal by using the keyboard shortcut Ctrl+Alt+T, and then run the following command:</span></span>

     ```bash
     sudo npm install -g iothub-explorer
     ```

   * <span data-ttu-id="4d94d-178">MacOS 10.1 or later:</span><span class="sxs-lookup"><span data-stu-id="4d94d-178">MacOS 10.1 or later:</span></span>

     <span data-ttu-id="4d94d-179">Open a terminal, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="4d94d-179">Open a terminal, and then run the following command:</span></span>

     ```bash
     npm install -g iothub-explorer
     ```

3. <span data-ttu-id="4d94d-180">Log in to your IoT hub by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4d94d-180">Log in to your IoT hub by running the following command:</span></span>

   ```bash
   iothub-explorer login [your IoT hub connection string]
   ```

4. <span data-ttu-id="4d94d-181">Register a new device.</span><span class="sxs-lookup"><span data-stu-id="4d94d-181">Register a new device.</span></span> <span data-ttu-id="4d94d-182">In the next example, `deviceID` is `new-device`.</span><span class="sxs-lookup"><span data-stu-id="4d94d-182">In the next example, `deviceID` is `new-device`.</span></span> <span data-ttu-id="4d94d-183">Get its connection string by running the following command.</span><span class="sxs-lookup"><span data-stu-id="4d94d-183">Get its connection string by running the following command.</span></span>

   ```bash
   iothub-explorer create new-device --connection-string
   ```

<span data-ttu-id="4d94d-184">Make a note of the connection string of the registered device.</span><span class="sxs-lookup"><span data-stu-id="4d94d-184">Make a note of the connection string of the registered device.</span></span> <span data-ttu-id="4d94d-185">It's used later.</span><span class="sxs-lookup"><span data-stu-id="4d94d-185">It's used later.</span></span>


> [!NOTE]
> <span data-ttu-id="4d94d-186">To view the connection string of registered devices, run the `iothub-explorer list` command.</span><span class="sxs-lookup"><span data-stu-id="4d94d-186">To view the connection string of registered devices, run the `iothub-explorer list` command.</span></span>


## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="4d94d-187">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span><span class="sxs-lookup"><span data-stu-id="4d94d-187">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
<span data-ttu-id="4d94d-188">In this section, you connect the sensors to your board.</span><span class="sxs-lookup"><span data-stu-id="4d94d-188">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="4d94d-189">Then you plug in your device to your computer for further use.</span><span class="sxs-lookup"><span data-stu-id="4d94d-189">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="4d94d-190">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="4d94d-190">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="4d94d-191">Use the breadboard and jumper wires to make the connection as follows.</span><span class="sxs-lookup"><span data-stu-id="4d94d-191">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="4d94d-192">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span><span class="sxs-lookup"><span data-stu-id="4d94d-192">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Connections reference](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="4d94d-194">For sensor pins, use the following wiring:</span><span class="sxs-lookup"><span data-stu-id="4d94d-194">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="4d94d-195">Start (Sensor)</span><span class="sxs-lookup"><span data-stu-id="4d94d-195">Start (Sensor)</span></span>           | <span data-ttu-id="4d94d-196">End (Board)</span><span class="sxs-lookup"><span data-stu-id="4d94d-196">End (Board)</span></span>           | <span data-ttu-id="4d94d-197">Cable Color</span><span class="sxs-lookup"><span data-stu-id="4d94d-197">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="4d94d-198">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="4d94d-198">VDD (Pin 31F)</span></span>            | <span data-ttu-id="4d94d-199">3V (Pin 58H)</span><span class="sxs-lookup"><span data-stu-id="4d94d-199">3V (Pin 58H)</span></span>           | <span data-ttu-id="4d94d-200">Red cable</span><span class="sxs-lookup"><span data-stu-id="4d94d-200">Red cable</span></span>     |
| <span data-ttu-id="4d94d-201">DATA (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="4d94d-201">DATA (Pin 32F)</span></span>           | <span data-ttu-id="4d94d-202">GPIO 2 (Pin 46A)</span><span class="sxs-lookup"><span data-stu-id="4d94d-202">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="4d94d-203">Blue cable</span><span class="sxs-lookup"><span data-stu-id="4d94d-203">Blue cable</span></span>    |
| <span data-ttu-id="4d94d-204">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="4d94d-204">GND (Pin 34F)</span></span>            | <span data-ttu-id="4d94d-205">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="4d94d-205">GND (PIn 56I)</span></span>          | <span data-ttu-id="4d94d-206">Black cable</span><span class="sxs-lookup"><span data-stu-id="4d94d-206">Black cable</span></span>   |

<span data-ttu-id="4d94d-207">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="4d94d-207">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>





<span data-ttu-id="4d94d-208">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span><span class="sxs-lookup"><span data-stu-id="4d94d-208">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Connect DHT22 with Feather Huzzah](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="4d94d-210">Connect Feather HUZZAH ESP8266 to your computer</span><span class="sxs-lookup"><span data-stu-id="4d94d-210">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="4d94d-211">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span><span class="sxs-lookup"><span data-stu-id="4d94d-211">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Connect Feather Huzzah to your computer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="4d94d-213">Add serial port permissions (Ubuntu only)</span><span class="sxs-lookup"><span data-stu-id="4d94d-213">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="4d94d-214">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="4d94d-214">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="4d94d-215">To add serial port permissions, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="4d94d-215">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="4d94d-216">Run the following commands at a terminal:</span><span class="sxs-lookup"><span data-stu-id="4d94d-216">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="4d94d-217">You get one of the following outputs:</span><span class="sxs-lookup"><span data-stu-id="4d94d-217">You get one of the following outputs:</span></span>

   * <span data-ttu-id="4d94d-218">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="4d94d-218">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="4d94d-219">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="4d94d-219">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="4d94d-220">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span><span class="sxs-lookup"><span data-stu-id="4d94d-220">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="4d94d-221">Add the user to the group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4d94d-221">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="4d94d-222">`<group-owner-name>` is the group owner name you obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="4d94d-222">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="4d94d-223">`<username>` is your Ubuntu user name.</span><span class="sxs-lookup"><span data-stu-id="4d94d-223">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="4d94d-224">Sign out of Ubuntu, and then sign in again for the change to appear.</span><span class="sxs-lookup"><span data-stu-id="4d94d-224">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="4d94d-225">Collect sensor data and send it to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="4d94d-225">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="4d94d-226">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="4d94d-226">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="4d94d-227">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-227">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="4d94d-228">Get the sample application from GitHub</span><span class="sxs-lookup"><span data-stu-id="4d94d-228">Get the sample application from GitHub</span></span>

<span data-ttu-id="4d94d-229">The sample application is hosted on GitHub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-229">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="4d94d-230">Clone the sample repository that contains the sample application from GitHub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-230">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="4d94d-231">To clone the sample repository, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="4d94d-231">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="4d94d-232">Open a command prompt or a terminal window.</span><span class="sxs-lookup"><span data-stu-id="4d94d-232">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="4d94d-233">Go to a folder where you want the sample application to be stored.</span><span class="sxs-lookup"><span data-stu-id="4d94d-233">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="4d94d-234">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="4d94d-234">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="4d94d-235">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="4d94d-235">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span></span>

1. <span data-ttu-id="4d94d-236">Open the folder where the sample application is stored.</span><span class="sxs-lookup"><span data-stu-id="4d94d-236">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="4d94d-237">Open the app.ino file in the app folder in the Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="4d94d-237">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Open the sample application in Arduino IDE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="4d94d-239">In the Arduino IDE, click **File** > **Preferences**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-239">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="4d94d-240">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span><span class="sxs-lookup"><span data-stu-id="4d94d-240">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="4d94d-241">In the pop-up window, enter the following URL, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-241">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Point to a package url in Arduino IDE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="4d94d-243">In the **Preference** dialog box, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-243">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="4d94d-244">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span><span class="sxs-lookup"><span data-stu-id="4d94d-244">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="4d94d-245">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span><span class="sxs-lookup"><span data-stu-id="4d94d-245">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![The esp8266 package is installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="4d94d-247">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-247">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="4d94d-248">Install necessary libraries</span><span class="sxs-lookup"><span data-stu-id="4d94d-248">Install necessary libraries</span></span>

1. <span data-ttu-id="4d94d-249">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-249">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="4d94d-250">Search for the following library names one by one.</span><span class="sxs-lookup"><span data-stu-id="4d94d-250">Search for the following library names one by one.</span></span> <span data-ttu-id="4d94d-251">For each  library that you find, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-251">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="4d94d-252">Don’t have a real DHT22 sensor?</span><span class="sxs-lookup"><span data-stu-id="4d94d-252">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="4d94d-253">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span><span class="sxs-lookup"><span data-stu-id="4d94d-253">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="4d94d-254">To set up the sample application to use simulated data, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="4d94d-254">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="4d94d-255">Open the `config.h` file in the `app` folder.</span><span class="sxs-lookup"><span data-stu-id="4d94d-255">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="4d94d-256">Locate the following line of code and change the value from `false` to `true`:</span><span class="sxs-lookup"><span data-stu-id="4d94d-256">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configure the sample application to use simulated data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="4d94d-258">Save the file with `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="4d94d-258">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="4d94d-259">Deploy the sample application to Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="4d94d-259">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="4d94d-260">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="4d94d-260">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="4d94d-261">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="4d94d-261">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="4d94d-262">Enter your credentials</span><span class="sxs-lookup"><span data-stu-id="4d94d-262">Enter your credentials</span></span>

<span data-ttu-id="4d94d-263">After the upload completes successfully, follow these steps to enter your credentials:</span><span class="sxs-lookup"><span data-stu-id="4d94d-263">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="4d94d-264">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-264">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="4d94d-265">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span><span class="sxs-lookup"><span data-stu-id="4d94d-265">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="4d94d-266">Select **No line ending** for the left drop-down list.</span><span class="sxs-lookup"><span data-stu-id="4d94d-266">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="4d94d-267">Select **115200 baud** for the right drop-down list.</span><span class="sxs-lookup"><span data-stu-id="4d94d-267">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="4d94d-268">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span><span class="sxs-lookup"><span data-stu-id="4d94d-268">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="4d94d-269">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="4d94d-269">Wi-Fi SSID</span></span>
   * <span data-ttu-id="4d94d-270">Wi-Fi password</span><span class="sxs-lookup"><span data-stu-id="4d94d-270">Wi-Fi password</span></span>
   * <span data-ttu-id="4d94d-271">Device connection string</span><span class="sxs-lookup"><span data-stu-id="4d94d-271">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="4d94d-272">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="4d94d-272">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="4d94d-273">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span><span class="sxs-lookup"><span data-stu-id="4d94d-273">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="4d94d-274">Enter `Y` to have the information erased.</span><span class="sxs-lookup"><span data-stu-id="4d94d-274">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="4d94d-275">You are asked to provide the information a second time.</span><span class="sxs-lookup"><span data-stu-id="4d94d-275">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="4d94d-276">Verify the sample application is running successfully</span><span class="sxs-lookup"><span data-stu-id="4d94d-276">Verify the sample application is running successfully</span></span>

<span data-ttu-id="4d94d-277">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span><span class="sxs-lookup"><span data-stu-id="4d94d-277">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Final output in Arduino IDE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="4d94d-279">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d94d-279">Next steps</span></span>

<span data-ttu-id="4d94d-280">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d94d-280">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
















