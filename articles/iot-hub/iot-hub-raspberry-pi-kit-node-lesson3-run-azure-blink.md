---
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 3: Run sample | Microsoft Docs'
description: Deploy and run a sample application to Raspberry Pi 3 that sends messages to your IoT hub and blinks the LED.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: blink led cloud pi, led blink from cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f0ab325e1183d7e381712fe3088a45fd1fe054c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551519"
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="38dc4-104">Run a sample application to send device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="38dc4-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="38dc4-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="38dc4-105">What you will do</span></span>
<span data-ttu-id="38dc4-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="38dc4-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="38dc4-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="38dc4-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="38dc4-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="38dc4-108">What you will learn</span></span>
<span data-ttu-id="38dc4-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span><span class="sxs-lookup"><span data-stu-id="38dc4-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="38dc4-110">What you need</span><span class="sxs-lookup"><span data-stu-id="38dc4-110">What you need</span></span>
* <span data-ttu-id="38dc4-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="38dc4-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="38dc4-112">Get your IoT hub and device connection strings</span><span class="sxs-lookup"><span data-stu-id="38dc4-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="38dc4-113">The device connection string is used by your Pi to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="38dc4-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="38dc4-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="38dc4-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="38dc4-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="38dc4-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="38dc4-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="38dc4-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="38dc4-117">Get the IoT hub connection string by running the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="38dc4-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="38dc4-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span><span class="sxs-lookup"><span data-stu-id="38dc4-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="38dc4-119">Get the device connection string by running the following command:</span><span class="sxs-lookup"><span data-stu-id="38dc4-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="38dc4-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="38dc4-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="38dc4-121">Configure the device connection</span><span class="sxs-lookup"><span data-stu-id="38dc4-121">Configure the device connection</span></span>
1. <span data-ttu-id="38dc4-122">Initialize the configuration file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="38dc4-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="38dc4-123">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="38dc4-123">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="38dc4-125">Make the following replacements in the `config-raspberrypi.json` file:</span><span class="sxs-lookup"><span data-stu-id="38dc4-125">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="38dc4-126">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span><span class="sxs-lookup"><span data-stu-id="38dc4-126">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="38dc4-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span><span class="sxs-lookup"><span data-stu-id="38dc4-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="38dc4-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span><span class="sxs-lookup"><span data-stu-id="38dc4-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="38dc4-129">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span><span class="sxs-lookup"><span data-stu-id="38dc4-129">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="38dc4-130">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="38dc4-130">Deploy and run the sample application</span></span>
<span data-ttu-id="38dc4-131">Deploy and run the sample application on Pi by running the following command:</span><span class="sxs-lookup"><span data-stu-id="38dc4-131">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="38dc4-132">Verify that the sample application works</span><span class="sxs-lookup"><span data-stu-id="38dc4-132">Verify that the sample application works</span></span>
<span data-ttu-id="38dc4-133">You should see the LED that is connected to Pi blinking every two seconds.</span><span class="sxs-lookup"><span data-stu-id="38dc4-133">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="38dc4-134">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="38dc4-134">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="38dc4-135">In addition, each message received by the IoT hub is printed in the console window.</span><span class="sxs-lookup"><span data-stu-id="38dc4-135">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="38dc4-136">The sample application terminates automatically after sending 20 messages.</span><span class="sxs-lookup"><span data-stu-id="38dc4-136">The sample application terminates automatically after sending 20 messages.</span></span>

![Sample application with sent and received messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="38dc4-138">Summary</span><span class="sxs-lookup"><span data-stu-id="38dc4-138">Summary</span></span>
<span data-ttu-id="38dc4-139">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="38dc4-139">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="38dc4-140">You can now monitor your messages as they are written to the storage account.</span><span class="sxs-lookup"><span data-stu-id="38dc4-140">You can now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38dc4-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="38dc4-141">Next steps</span></span>
[<span data-ttu-id="38dc4-142">Read messages persisted in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="38dc4-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)



