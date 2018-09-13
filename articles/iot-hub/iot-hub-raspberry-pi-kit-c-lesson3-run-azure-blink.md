---
title: 'Connect Raspberry Pi (C) to Azure IoT - Lesson 3: Run sample | Microsoft Docs'
description: Deploy and run a sample application to Raspberry Pi 3 that sends messages to your IoT hub and blinks the LED.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: blink led cloud pi, led blink from cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d00a4bcd2a717155121c29e9c65d11a2893abdb7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552383"
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="0be2b-104">Run a sample application to send device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="0be2b-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0be2b-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="0be2b-105">What you will do</span></span>
<span data-ttu-id="0be2b-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0be2b-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="0be2b-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0be2b-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0be2b-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="0be2b-108">What you will learn</span></span>
<span data-ttu-id="0be2b-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span><span class="sxs-lookup"><span data-stu-id="0be2b-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0be2b-110">What you need</span><span class="sxs-lookup"><span data-stu-id="0be2b-110">What you need</span></span>
* <span data-ttu-id="0be2b-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="0be2b-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="0be2b-112">Get your IoT hub and device connection strings</span><span class="sxs-lookup"><span data-stu-id="0be2b-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="0be2b-113">The device connection string is used by your Pi to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0be2b-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="0be2b-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0be2b-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="0be2b-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="0be2b-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="0be2b-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="0be2b-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="0be2b-117">Get the IoT hub connection string by running the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="0be2b-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="0be2b-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span><span class="sxs-lookup"><span data-stu-id="0be2b-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="0be2b-119">Get the device connection string by running the following command:</span><span class="sxs-lookup"><span data-stu-id="0be2b-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="0be2b-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="0be2b-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="0be2b-121">Configure the device connection</span><span class="sxs-lookup"><span data-stu-id="0be2b-121">Configure the device connection</span></span>
1. <span data-ttu-id="0be2b-122">Initialize the configuration file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="0be2b-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="0be2b-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span><span class="sxs-lookup"><span data-stu-id="0be2b-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="0be2b-124">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="0be2b-124">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="0be2b-126">Make the following replacements in the `config-raspberrypi.json` file:</span><span class="sxs-lookup"><span data-stu-id="0be2b-126">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="0be2b-127">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span><span class="sxs-lookup"><span data-stu-id="0be2b-127">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="0be2b-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span><span class="sxs-lookup"><span data-stu-id="0be2b-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="0be2b-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span><span class="sxs-lookup"><span data-stu-id="0be2b-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="0be2b-130">You don't need `azure_storage_connection_string` in this article.</span><span class="sxs-lookup"><span data-stu-id="0be2b-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="0be2b-131">Keep it as is.</span><span class="sxs-lookup"><span data-stu-id="0be2b-131">Keep it as is.</span></span>

<span data-ttu-id="0be2b-132">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span><span class="sxs-lookup"><span data-stu-id="0be2b-132">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="0be2b-133">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="0be2b-133">Deploy and run the sample application</span></span>
<span data-ttu-id="0be2b-134">Deploy and run the sample application on Pi by running the following command:</span><span class="sxs-lookup"><span data-stu-id="0be2b-134">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="0be2b-135">Verify that the sample application works</span><span class="sxs-lookup"><span data-stu-id="0be2b-135">Verify that the sample application works</span></span>
<span data-ttu-id="0be2b-136">You should see the LED that is connected to Pi blinking every two seconds.</span><span class="sxs-lookup"><span data-stu-id="0be2b-136">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="0be2b-137">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0be2b-137">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="0be2b-138">In addition, each message received by the IoT hub is printed in the console window.</span><span class="sxs-lookup"><span data-stu-id="0be2b-138">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="0be2b-139">The sample application terminates automatically after sending 20 messages.</span><span class="sxs-lookup"><span data-stu-id="0be2b-139">The sample application terminates automatically after sending 20 messages.</span></span>

![Sample application with sent and received messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="0be2b-141">Summary</span><span class="sxs-lookup"><span data-stu-id="0be2b-141">Summary</span></span>
<span data-ttu-id="0be2b-142">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0be2b-142">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="0be2b-143">You now monitor your messages as they are written to the storage account.</span><span class="sxs-lookup"><span data-stu-id="0be2b-143">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0be2b-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="0be2b-144">Next steps</span></span>
[<span data-ttu-id="0be2b-145">Read messages persisted in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0be2b-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)



