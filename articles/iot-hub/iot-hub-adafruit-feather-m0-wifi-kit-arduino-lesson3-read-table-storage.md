---
title: 'Connect Arduino (C) to Azure IoT - Lesson 3: Table storage | Microsoft Docs'
description: Monitor the device-to-cloud messages as they are written to your Azure Table storage.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: data in the cloud, cloud data collection, iot cloud service, iot data
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: da6389f8c8cb1a686c6f8672ed910676ec6838b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551300"
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="0b234-104">Read messages persisted in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0b234-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0b234-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="0b234-105">What you will do</span></span>
<span data-ttu-id="0b234-106">Monitor the device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board to your IoT hub as the messages are written to your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="0b234-106">Monitor the device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board to your IoT hub as the messages are written to your Azure Table storage.</span></span>

<span data-ttu-id="0b234-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="0b234-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0b234-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="0b234-108">What you will learn</span></span>
<span data-ttu-id="0b234-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="0b234-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0b234-110">What you need</span><span class="sxs-lookup"><span data-stu-id="0b234-110">What you need</span></span>
<span data-ttu-id="0b234-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on your Arduino board][run-blink-application].</span><span class="sxs-lookup"><span data-stu-id="0b234-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="0b234-112">Read new messages from your storage account</span><span class="sxs-lookup"><span data-stu-id="0b234-112">Read new messages from your storage account</span></span>
<span data-ttu-id="0b234-113">In the previous article, you ran a sample application on your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="0b234-113">In the previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="0b234-114">The sample application sent messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0b234-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="0b234-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span><span class="sxs-lookup"><span data-stu-id="0b234-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="0b234-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="0b234-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="0b234-117">To read messages stored in your Azure Table storage, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="0b234-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="0b234-118">Get the connection string by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="0b234-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="0b234-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span><span class="sxs-lookup"><span data-stu-id="0b234-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="0b234-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="0b234-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="0b234-121">Open the configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="0b234-121">Open the configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="0b234-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span><span class="sxs-lookup"><span data-stu-id="0b234-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="0b234-123">Save the `config-arduino.json` file.</span><span class="sxs-lookup"><span data-stu-id="0b234-123">Save the `config-arduino.json` file.</span></span>
5. <span data-ttu-id="0b234-124">Send messages again and read them from your Azure Table storage by running the following command:</span><span class="sxs-lookup"><span data-stu-id="0b234-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor the serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="0b234-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span><span class="sxs-lookup"><span data-stu-id="0b234-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp-run]

## <a name="summary"></a><span data-ttu-id="0b234-127">Summary</span><span class="sxs-lookup"><span data-stu-id="0b234-127">Summary</span></span>
<span data-ttu-id="0b234-128">You've successfully connected your Arduino board to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="0b234-128">You've successfully connected your Arduino board to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="0b234-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="0b234-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="0b234-130">You can now send cloud-to-device messages from your IoT hub to your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="0b234-130">You can now send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b234-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="0b234-131">Next steps</span></span>
<span data-ttu-id="0b234-132">[Send cloud-to-device messages][send-cloud-to-device-messages]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="0b234-132">[Send cloud-to-device messages][send-cloud-to-device-messages]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
