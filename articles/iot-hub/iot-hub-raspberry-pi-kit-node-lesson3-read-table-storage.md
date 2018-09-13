---
featureFlags:
- usabilla
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 3: Table storage | Microsoft Docs'
description: Monitor the device-to-cloud messages as they are written to your Azure Table storage.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: retrieve data from cloud, iot cloud service
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 14bb8456506e6afb3845d1aa59c9c66c3cf0dc4a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551661"
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="cf461-104">Read messages persisted in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="cf461-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cf461-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="cf461-105">What you will do</span></span>
<span data-ttu-id="cf461-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="cf461-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="cf461-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cf461-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cf461-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="cf461-108">What you will learn</span></span>
<span data-ttu-id="cf461-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="cf461-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cf461-110">What you need</span><span class="sxs-lookup"><span data-stu-id="cf461-110">What you need</span></span>
<span data-ttu-id="cf461-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="cf461-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="cf461-112">Read new messages from your storage account</span><span class="sxs-lookup"><span data-stu-id="cf461-112">Read new messages from your storage account</span></span>
<span data-ttu-id="cf461-113">In the previous article, you ran a sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="cf461-113">In the previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="cf461-114">The sample application sent messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="cf461-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="cf461-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span><span class="sxs-lookup"><span data-stu-id="cf461-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="cf461-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="cf461-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="cf461-117">To read messages stored in your Azure Table storage, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="cf461-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="cf461-118">Get the connection string by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="cf461-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="cf461-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span><span class="sxs-lookup"><span data-stu-id="cf461-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="cf461-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="cf461-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="cf461-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="cf461-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="cf461-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span><span class="sxs-lookup"><span data-stu-id="cf461-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="cf461-123">Save the `config-raspberrypi.json` file.</span><span class="sxs-lookup"><span data-stu-id="cf461-123">Save the `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="cf461-124">Send messages again and read them from your Azure Table storage by running the following command:</span><span class="sxs-lookup"><span data-stu-id="cf461-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="cf461-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span><span class="sxs-lookup"><span data-stu-id="cf461-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>
   
    ![gulp run --read-storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a><span data-ttu-id="cf461-127">Summary</span><span class="sxs-lookup"><span data-stu-id="cf461-127">Summary</span></span>
<span data-ttu-id="cf461-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="cf461-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="cf461-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="cf461-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="cf461-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span><span class="sxs-lookup"><span data-stu-id="cf461-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf461-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf461-131">Next steps</span></span>
[<span data-ttu-id="cf461-132">Run the sample application to receive cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="cf461-132">Run the sample application to receive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)


