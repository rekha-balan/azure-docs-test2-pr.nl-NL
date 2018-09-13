---
title: 'Connect Intel Edison (C) to Azure IoT - Lesson 3: Monitor messages | Microsoft Docs'
description: Monitor the device-to-cloud messages as they are written to your Azure Table storage.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: data in the cloud, cloud data collection, iot cloud service, iot data
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6179268cd5dc0da60cdee41e7480c5c517a9a908
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555877"
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="5e3bf-104">Read messages persisted in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5e3bf-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5e3bf-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="5e3bf-105">What you will do</span></span>
<span data-ttu-id="5e3bf-106">Monitor the device-to-cloud messages that are sent from Intel Edison to your IoT hub as the messages are written to your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-106">Monitor the device-to-cloud messages that are sent from Intel Edison to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="5e3bf-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5e3bf-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e3bf-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="5e3bf-108">What you will learn</span></span>
<span data-ttu-id="5e3bf-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e3bf-110">What you need</span><span class="sxs-lookup"><span data-stu-id="5e3bf-110">What you need</span></span>
<span data-ttu-id="5e3bf-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="5e3bf-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="5e3bf-112">Read new messages from your storage account</span><span class="sxs-lookup"><span data-stu-id="5e3bf-112">Read new messages from your storage account</span></span>
<span data-ttu-id="5e3bf-113">In the previous article, you ran a sample application on Edison.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-113">In the previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="5e3bf-114">The sample application sent messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="5e3bf-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="5e3bf-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="5e3bf-117">To read messages stored in your Azure Table storage, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="5e3bf-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="5e3bf-118">Get the connection string by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="5e3bf-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="5e3bf-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="5e3bf-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="5e3bf-121">Open the configuration file `config-edison.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="5e3bf-121">Open the configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="5e3bf-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="5e3bf-123">Save the `config-edison.json` file.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-123">Save the `config-edison.json` file.</span></span>
5. <span data-ttu-id="5e3bf-124">Send messages again and read them from your Azure Table storage by running the following command:</span><span class="sxs-lookup"><span data-stu-id="5e3bf-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="5e3bf-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a><span data-ttu-id="5e3bf-127">Summary</span><span class="sxs-lookup"><span data-stu-id="5e3bf-127">Summary</span></span>
<span data-ttu-id="5e3bf-128">You've successfully connected Edison to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-128">You've successfully connected Edison to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="5e3bf-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="5e3bf-130">You can now send cloud-to-device messages from your IoT hub to Edison.</span><span class="sxs-lookup"><span data-stu-id="5e3bf-130">You can now send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e3bf-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e3bf-131">Next steps</span></span>
<span data-ttu-id="5e3bf-132">[Run a sample application to receive cloud-to-device messages][receive-cloud-to-device-messages]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="5e3bf-132">[Run a sample application to receive cloud-to-device messages][receive-cloud-to-device-messages]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
