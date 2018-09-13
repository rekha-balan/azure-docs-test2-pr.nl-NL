---
title: 'SensorTag device & Azure IoT Gateway - Lesson 3: Run sample app | Microsoft Docs'
description: Run a BLE sample application to receive data from BLE SensorTag and from your IoT hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: ble app, sensor monitor app, sensor data collection, data from sensors, sensor data to cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 41bcaed4ddf6a5c7a650161c338088dcbe6f06c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540796"
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="2901d-104">Configure and run a BLE sample application</span><span class="sxs-lookup"><span data-stu-id="2901d-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2901d-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="2901d-105">What you will do</span></span>

- <span data-ttu-id="2901d-106">Clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="2901d-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="2901d-107">Set up the connectivity between SensorTag and Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2901d-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="2901d-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span><span class="sxs-lookup"><span data-stu-id="2901d-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="2901d-109">And configure and run the BLE sample application.</span><span class="sxs-lookup"><span data-stu-id="2901d-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="2901d-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2901d-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2901d-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="2901d-111">What you will learn</span></span>

<span data-ttu-id="2901d-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="2901d-112">In this article, you will learn:</span></span>

- <span data-ttu-id="2901d-113">How to configure and run the BLE sample application.</span><span class="sxs-lookup"><span data-stu-id="2901d-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2901d-114">What you need</span><span class="sxs-lookup"><span data-stu-id="2901d-114">What you need</span></span>

<span data-ttu-id="2901d-115">You must have successfully completed</span><span class="sxs-lookup"><span data-stu-id="2901d-115">You must have successfully completed</span></span>

- [<span data-ttu-id="2901d-116">Create an IoT hub and register SensorTag</span><span class="sxs-lookup"><span data-stu-id="2901d-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="2901d-117">Clone the sample repository to the host computer</span><span class="sxs-lookup"><span data-stu-id="2901d-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="2901d-118">To clone the sample repository, follow these steps on the host computer:</span><span class="sxs-lookup"><span data-stu-id="2901d-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="2901d-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2901d-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="2901d-120">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="2901d-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="2901d-121">Set up the connectivity between SensorTag and Intel NUC</span><span class="sxs-lookup"><span data-stu-id="2901d-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="2901d-122">To set up the connectivity, follow these steps on the host computer:</span><span class="sxs-lookup"><span data-stu-id="2901d-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="2901d-123">Initialize the configuration file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="2901d-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="2901d-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="2901d-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="2901d-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2901d-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="2901d-126">![screenshot of config gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="2901d-126">![screenshot of config gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="2901d-127">Install helper tools on Intel NUC by running the following command:</span><span class="sxs-lookup"><span data-stu-id="2901d-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="2901d-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span><span class="sxs-lookup"><span data-stu-id="2901d-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![turn on Sensor Tag](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="2901d-130">Scan SensorTag devices by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="2901d-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="2901d-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span><span class="sxs-lookup"><span data-stu-id="2901d-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="2901d-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="2901d-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="2901d-133">Get the connection string of SensorTag</span><span class="sxs-lookup"><span data-stu-id="2901d-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="2901d-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span><span class="sxs-lookup"><span data-stu-id="2901d-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="2901d-135">`{IoT hub name}` is the IoT hub name that you used.</span><span class="sxs-lookup"><span data-stu-id="2901d-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="2901d-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="2901d-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="2901d-137">Configure the BLE sample application</span><span class="sxs-lookup"><span data-stu-id="2901d-137">Configure the BLE sample application</span></span>

<span data-ttu-id="2901d-138">To configure and run the BLE sample application, follow these steps on the host computer:</span><span class="sxs-lookup"><span data-stu-id="2901d-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="2901d-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="2901d-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![screenshot of config sensortag](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="2901d-141">Make the following replacements in the code:</span><span class="sxs-lookup"><span data-stu-id="2901d-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="2901d-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span><span class="sxs-lookup"><span data-stu-id="2901d-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="2901d-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span><span class="sxs-lookup"><span data-stu-id="2901d-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="2901d-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span><span class="sxs-lookup"><span data-stu-id="2901d-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="2901d-145">Run the BLE sample application.</span><span class="sxs-lookup"><span data-stu-id="2901d-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="2901d-146">To run the BLE sample application, follow these steps on the host computer:</span><span class="sxs-lookup"><span data-stu-id="2901d-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="2901d-147">Turn on SensorTag.</span><span class="sxs-lookup"><span data-stu-id="2901d-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="2901d-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span><span class="sxs-lookup"><span data-stu-id="2901d-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="2901d-149">Verify that the BLE sample application works</span><span class="sxs-lookup"><span data-stu-id="2901d-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="2901d-150">You should now see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="2901d-150">You should now see an output like the following:</span></span>

![BLE sample application output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="2901d-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2901d-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="2901d-153">The sample application terminates automatically after sending 40 seconds.</span><span class="sxs-lookup"><span data-stu-id="2901d-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="2901d-154">Summary</span><span class="sxs-lookup"><span data-stu-id="2901d-154">Summary</span></span>

<span data-ttu-id="2901d-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2901d-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="2901d-156">You're ready to learn how to verify that your IoT hub has received the data.</span><span class="sxs-lookup"><span data-stu-id="2901d-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2901d-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="2901d-157">Next steps</span></span>
[<span data-ttu-id="2901d-158">Read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="2901d-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)



