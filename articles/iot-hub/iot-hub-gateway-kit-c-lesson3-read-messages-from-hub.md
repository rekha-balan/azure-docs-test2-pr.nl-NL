---
title: 'SensorTag device & Azure IoT Gateway - Lesson 3: Read messages | Microsoft Docs'
description: Run a sample code on your host computer to read the messages from your IoT hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: data in the cloud, cloud data collection, iot cloud service, iot data
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f5114cce6e535f233b6e8a58966cc5eb2714c5ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550462"
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="a6a88-104">Read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a6a88-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a6a88-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="a6a88-105">What you will do</span></span>

- <span data-ttu-id="a6a88-106">Run sample code on your host computer to read messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6a88-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="a6a88-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a6a88-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a6a88-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="a6a88-108">What you will learn</span></span>

<span data-ttu-id="a6a88-109">How to use the gulp tool to read messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6a88-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a6a88-110">What you need</span><span class="sxs-lookup"><span data-stu-id="a6a88-110">What you need</span></span>

- <span data-ttu-id="a6a88-111">The BLE sample application that you ran successfully in Lesson 3.</span><span class="sxs-lookup"><span data-stu-id="a6a88-111">The BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="a6a88-112">Get your IoT hub and device connection strings</span><span class="sxs-lookup"><span data-stu-id="a6a88-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="a6a88-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6a88-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span></span> <span data-ttu-id="a6a88-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6a88-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="a6a88-115">List all your IoT hubs in your resource group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a6a88-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="a6a88-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="a6a88-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span></span>
- <span data-ttu-id="a6a88-117">Get the IoT hub connection string by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a6a88-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="a6a88-118">`{my hub name}` is the name that you specified in Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="a6a88-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="a6a88-119">Configure the device connection for the sample code</span><span class="sxs-lookup"><span data-stu-id="a6a88-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="a6a88-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span><span class="sxs-lookup"><span data-stu-id="a6a88-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="a6a88-121">To do this, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="a6a88-121">To do this, follow these steps:</span></span>

1. <span data-ttu-id="a6a88-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span><span class="sxs-lookup"><span data-stu-id="a6a88-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="a6a88-123">Make the following replacements in the `config-azure.json` file:</span><span class="sxs-lookup"><span data-stu-id="a6a88-123">Make the following replacements in the `config-azure.json` file:</span></span>

   ![screenshot of config azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="a6a88-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span><span class="sxs-lookup"><span data-stu-id="a6a88-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="a6a88-126">Read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a6a88-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="a6a88-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span><span class="sxs-lookup"><span data-stu-id="a6a88-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="a6a88-128">Run the gateway sample application and read IoT Hub messages by the following command:</span><span class="sxs-lookup"><span data-stu-id="a6a88-128">Run the gateway sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="a6a88-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span><span class="sxs-lookup"><span data-stu-id="a6a88-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="a6a88-130">It also spawns a child process to receive the message.</span><span class="sxs-lookup"><span data-stu-id="a6a88-130">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="a6a88-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span><span class="sxs-lookup"><span data-stu-id="a6a88-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="a6a88-132">The sample application instance will terminate automatically in 40 seconds.</span><span class="sxs-lookup"><span data-stu-id="a6a88-132">The sample application instance will terminate automatically in 40 seconds.</span></span>

![BLE Sample application with sent and received messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="a6a88-134">Summary</span><span class="sxs-lookup"><span data-stu-id="a6a88-134">Summary</span></span>

<span data-ttu-id="a6a88-135">You've run a sample code to read messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6a88-135">You've run a sample code to read messages from your IoT hub.</span></span> <span data-ttu-id="a6a88-136">You're ready to read the messages that are stored in your Azure table storage.</span><span class="sxs-lookup"><span data-stu-id="a6a88-136">You're ready to read the messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6a88-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6a88-137">Next steps</span></span>
[<span data-ttu-id="a6a88-138">Create an Azure function app and Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="a6a88-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)




