---
title: 'Connect Intel Edison (C) to Azure IoT - Lesson 3: Send messages | Microsoft Docs'
description: Deploy and run a sample application to Intel Edison that sends messages to your IoT hub and blinks the LED.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot cloud service, arduino send data to cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6dcd702c316bfac5df9fbd566e7601fbe63adce3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550550"
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="3ae3a-104">Run a sample application to send device-to-cloud messages</span><span class="sxs-lookup"><span data-stu-id="3ae3a-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="3ae3a-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="3ae3a-105">What you will do</span></span>
<span data-ttu-id="3ae3a-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="3ae3a-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="3ae3a-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3ae3a-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="3ae3a-108">What you will learn</span></span>
<span data-ttu-id="3ae3a-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3ae3a-110">What you need</span><span class="sxs-lookup"><span data-stu-id="3ae3a-110">What you need</span></span>
* <span data-ttu-id="3ae3a-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="3ae3a-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="3ae3a-112">Get your IoT hub and device connection strings</span><span class="sxs-lookup"><span data-stu-id="3ae3a-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="3ae3a-113">The device connection string is used to connect Edison to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="3ae3a-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="3ae3a-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="3ae3a-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="3ae3a-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="3ae3a-117">Get the IoT hub connection string by running the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="3ae3a-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="3ae3a-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="3ae3a-119">Get the device connection string by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3ae3a-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="3ae3a-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="3ae3a-121">Configure the device connection</span><span class="sxs-lookup"><span data-stu-id="3ae3a-121">Configure the device connection</span></span>
1. <span data-ttu-id="3ae3a-122">Initialize the configuration file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="3ae3a-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > <span data-ttu-id="3ae3a-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="3ae3a-124">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3ae3a-124">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. <span data-ttu-id="3ae3a-126">Make the following replacements in the `config-edison.json` file:</span><span class="sxs-lookup"><span data-stu-id="3ae3a-126">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="3ae3a-127">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-127">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="3ae3a-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="3ae3a-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3ae3a-130">You don't need `azure_storage_connection_string` in this article.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="3ae3a-131">Keep it as is.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-131">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="3ae3a-132">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="3ae3a-132">Deploy and run the sample application</span></span>
<span data-ttu-id="3ae3a-133">Deploy and run the sample application on Edison by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3ae3a-133">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="3ae3a-134">Verify that the sample application works</span><span class="sxs-lookup"><span data-stu-id="3ae3a-134">Verify that the sample application works</span></span>
<span data-ttu-id="3ae3a-135">You should see the LED that is connected to Edison blinking every two seconds.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-135">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="3ae3a-136">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-136">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="3ae3a-137">In addition, each message received by the IoT hub is printed in the console window.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-137">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="3ae3a-138">The sample application terminates automatically after sending 20 messages.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-138">The sample application terminates automatically after sending 20 messages.</span></span>

![Sample application with sent and received messages][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="3ae3a-140">Summary</span><span class="sxs-lookup"><span data-stu-id="3ae3a-140">Summary</span></span>
<span data-ttu-id="3ae3a-141">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-141">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="3ae3a-142">You now monitor your messages as they are written to the storage account.</span><span class="sxs-lookup"><span data-stu-id="3ae3a-142">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ae3a-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ae3a-143">Next steps</span></span>
<span data-ttu-id="3ae3a-144">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="3ae3a-144">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md

