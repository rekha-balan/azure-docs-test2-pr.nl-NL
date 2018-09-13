---
title: 'Simulated device & Azure IoT Gateway - Lesson 3: Read messages | Microsoft Docs'
description: Run a sample code on your host computer to read the messages from your IoT hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: data in the cloud, cloud data collection, iot cloud service, iot data
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c504a587ca94255267fc3eabaf42ebf6413c0577
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554371"
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="9ba53-104">Read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="9ba53-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9ba53-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="9ba53-105">What you will do</span></span>

- <span data-ttu-id="9ba53-106">Run sample code on your host computer to read messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9ba53-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="9ba53-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9ba53-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9ba53-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="9ba53-108">What you will learn</span></span>

<span data-ttu-id="9ba53-109">How to use the gulp tool to read messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9ba53-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9ba53-110">What you need</span><span class="sxs-lookup"><span data-stu-id="9ba53-110">What you need</span></span>

- <span data-ttu-id="9ba53-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="9ba53-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="9ba53-112">Get your IoT hub and device connection strings</span><span class="sxs-lookup"><span data-stu-id="9ba53-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="9ba53-113">The device connection string is used by your simulated device to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9ba53-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="9ba53-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9ba53-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="9ba53-115">List all your IoT hubs in your resource group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="9ba53-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="9ba53-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span><span class="sxs-lookup"><span data-stu-id="9ba53-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="9ba53-117">Get the IoT hub connection string by running the following command:</span><span class="sxs-lookup"><span data-stu-id="9ba53-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="9ba53-118">`{my hub name}` is the name that you specified in Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="9ba53-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="9ba53-119">Configure the device connection for the sample code</span><span class="sxs-lookup"><span data-stu-id="9ba53-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="9ba53-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ba53-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="9ba53-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span><span class="sxs-lookup"><span data-stu-id="9ba53-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="9ba53-122">Make the following replacements in the `config-azure.json` file:</span><span class="sxs-lookup"><span data-stu-id="9ba53-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![screenshot of config azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="9ba53-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span><span class="sxs-lookup"><span data-stu-id="9ba53-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="9ba53-125">Read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="9ba53-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="9ba53-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span><span class="sxs-lookup"><span data-stu-id="9ba53-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="9ba53-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span><span class="sxs-lookup"><span data-stu-id="9ba53-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="9ba53-128">It also spawns a child process to receive the message.</span><span class="sxs-lookup"><span data-stu-id="9ba53-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="9ba53-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span><span class="sxs-lookup"><span data-stu-id="9ba53-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="9ba53-130">The application will exit in 40 seconds.</span><span class="sxs-lookup"><span data-stu-id="9ba53-130">The application will exit in 40 seconds.</span></span>

![Simulated Sample application with sent and received messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="9ba53-132">Summary</span><span class="sxs-lookup"><span data-stu-id="9ba53-132">Summary</span></span>

<span data-ttu-id="9ba53-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span><span class="sxs-lookup"><span data-stu-id="9ba53-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="9ba53-134">You've also read the messages that have been sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9ba53-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ba53-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="9ba53-135">Next steps</span></span>
[<span data-ttu-id="9ba53-136">Create an Azure function app and Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="9ba53-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)




