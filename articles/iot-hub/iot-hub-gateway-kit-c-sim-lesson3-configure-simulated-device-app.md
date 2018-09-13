---
title: 'Simulated device & Azure IoT Gateway - Lesson 3: Run sample app | Microsoft Docs'
description: Run a simulated device sample app to send temperature data to your IoT hub
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: data to cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fbddbb71e41e83f561cec0deebc870d1cdaaad04
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552123"
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="5e725-104">Configure and run a simulated device sample app</span><span class="sxs-lookup"><span data-stu-id="5e725-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5e725-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="5e725-105">What you will do</span></span>

- <span data-ttu-id="5e725-106">Clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="5e725-106">Clone the sample repository.</span></span>
- <span data-ttu-id="5e725-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span><span class="sxs-lookup"><span data-stu-id="5e725-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="5e725-108">Configure and run the simulated device sample application.</span><span class="sxs-lookup"><span data-stu-id="5e725-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="5e725-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5e725-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e725-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="5e725-110">What you will learn</span></span>

<span data-ttu-id="5e725-111">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="5e725-111">In this article, you will learn:</span></span>

- <span data-ttu-id="5e725-112">How to configure and run the simulated device sample application.</span><span class="sxs-lookup"><span data-stu-id="5e725-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e725-113">What you need</span><span class="sxs-lookup"><span data-stu-id="5e725-113">What you need</span></span>

<span data-ttu-id="5e725-114">You must have successfully completed</span><span class="sxs-lookup"><span data-stu-id="5e725-114">You must have successfully completed</span></span>

- [<span data-ttu-id="5e725-115">Create an IoT hub and register your device</span><span class="sxs-lookup"><span data-stu-id="5e725-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="5e725-116">Clone the sample repository to the host computer</span><span class="sxs-lookup"><span data-stu-id="5e725-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="5e725-117">To clone the sample repository, follow these steps on the host computer:</span><span class="sxs-lookup"><span data-stu-id="5e725-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="5e725-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5e725-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="5e725-119">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="5e725-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="5e725-120">Configure the simulated device and your NUC</span><span class="sxs-lookup"><span data-stu-id="5e725-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="5e725-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="5e725-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="5e725-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="5e725-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Config you don't have a TI SensorTag device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="5e725-124">Initialize the configuration file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="5e725-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="5e725-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="5e725-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="5e725-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5e725-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="5e725-127">![screenshot of config gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="5e725-127">![screenshot of config gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="5e725-128">Get the connection string of your IoT hub logical device</span><span class="sxs-lookup"><span data-stu-id="5e725-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="5e725-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span><span class="sxs-lookup"><span data-stu-id="5e725-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="5e725-130">`{IoT hub name}` is the IoT hub name that you used.</span><span class="sxs-lookup"><span data-stu-id="5e725-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="5e725-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="5e725-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="5e725-132">Configure the simulated device cloud upload sample application</span><span class="sxs-lookup"><span data-stu-id="5e725-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="5e725-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span><span class="sxs-lookup"><span data-stu-id="5e725-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="5e725-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="5e725-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![screenshot of config sensortag](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="5e725-136">Make the following replacements in the code:</span><span class="sxs-lookup"><span data-stu-id="5e725-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="5e725-137">Replace `[IoT hub name]` with the IoT hub name.</span><span class="sxs-lookup"><span data-stu-id="5e725-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="5e725-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span><span class="sxs-lookup"><span data-stu-id="5e725-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="5e725-139">Run the application.</span><span class="sxs-lookup"><span data-stu-id="5e725-139">Run the application.</span></span>

   <span data-ttu-id="5e725-140">Deploy and run the application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="5e725-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="5e725-141">Verify the sample application works</span><span class="sxs-lookup"><span data-stu-id="5e725-141">Verify the sample application works</span></span>

<span data-ttu-id="5e725-142">You should now see output like the following:</span><span class="sxs-lookup"><span data-stu-id="5e725-142">You should now see output like the following:</span></span>

![simulated device sample application output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="5e725-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span><span class="sxs-lookup"><span data-stu-id="5e725-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="5e725-145">Summary</span><span class="sxs-lookup"><span data-stu-id="5e725-145">Summary</span></span>

<span data-ttu-id="5e725-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span><span class="sxs-lookup"><span data-stu-id="5e725-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e725-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e725-147">Next steps</span></span>
[<span data-ttu-id="5e725-148">Read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="5e725-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)



