---
title: 'SensorTag device & Azure IoT Gateway - Lesson 4: Table storage | Microsoft Docs'
description: Save messages from Intel NUC to your IoT hub, write them to Azure Table storage and then read them from the cloud.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: retrieve data from cloud, iot cloud service
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 62bb1a86b9596b50925b957311c63dab8d53010e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564509"
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="ee7cd-104">Read messages persisted in Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="ee7cd-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ee7cd-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="ee7cd-105">What you will do</span></span>

- <span data-ttu-id="ee7cd-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="ee7cd-107">Then run a sample code on your host computer to read the messages in your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-107">Then run a sample code on your host computer to read the messages in your Azure Table storage.</span></span> 

<span data-ttu-id="ee7cd-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ee7cd-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ee7cd-109">What you will learn</span><span class="sxs-lookup"><span data-stu-id="ee7cd-109">What you will learn</span></span>

<span data-ttu-id="ee7cd-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ee7cd-111">What you need</span><span class="sxs-lookup"><span data-stu-id="ee7cd-111">What you need</span></span>

<span data-ttu-id="ee7cd-112">You have have successfully done the following tasks:</span><span class="sxs-lookup"><span data-stu-id="ee7cd-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="ee7cd-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="ee7cd-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="ee7cd-114">[Run the gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span><span class="sxs-lookup"><span data-stu-id="ee7cd-114">[Run the gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="ee7cd-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="ee7cd-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="ee7cd-116">Get your Azure storage connection strings</span><span class="sxs-lookup"><span data-stu-id="ee7cd-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="ee7cd-117">Early in this lesson, you successfully created an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="ee7cd-118">To get the connection string of the Azure storage account, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="ee7cd-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="ee7cd-119">List all your storage accounts.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="ee7cd-120">Get azure storage connection string.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="ee7cd-121">Use iot-gateway as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-121">Use iot-gateway as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="ee7cd-122">Configure the device connection</span><span class="sxs-lookup"><span data-stu-id="ee7cd-122">Configure the device connection</span></span>

<span data-ttu-id="ee7cd-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="ee7cd-124">To configure the device connection, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ee7cd-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="ee7cd-125">Open the device configuration file `config-azure.json` by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="ee7cd-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="ee7cd-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="ee7cd-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="ee7cd-129">Read messages in your Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="ee7cd-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="ee7cd-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span><span class="sxs-lookup"><span data-stu-id="ee7cd-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="ee7cd-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="ee7cd-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="ee7cd-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="ee7cd-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="ee7cd-135">The sample application instance will terminate automatically in 40 seconds.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![gulp read](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="ee7cd-137">Summary</span><span class="sxs-lookup"><span data-stu-id="ee7cd-137">Summary</span></span>

<span data-ttu-id="ee7cd-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span><span class="sxs-lookup"><span data-stu-id="ee7cd-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>

