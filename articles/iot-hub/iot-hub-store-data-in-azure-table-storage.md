---
title: Save IoT Hub messages to Azure data storage | Microsoft Docs
description: Use Azure Function App to save IoT Hub messages to Azure table storage. The IoT Hub messages contain information like sensor data that is sent from your IoT device.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot data storage, iot sensor data storage
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: xshi
ms.openlocfilehash: c800329b29f9ea0d5dba99d49e7d1d2470fcb135
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555724"
---
# <a name="save-iot-hub-messages-that-contain-information-like-sensor-data-to-azure-table-storage"></a><span data-ttu-id="47d78-105">Save IoT Hub messages that contain information like sensor data to Azure table storage</span><span class="sxs-lookup"><span data-stu-id="47d78-105">Save IoT Hub messages that contain information like sensor data to Azure table storage</span></span>

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-will-learn"></a><span data-ttu-id="47d78-106">What you will learn</span><span class="sxs-lookup"><span data-stu-id="47d78-106">What you will learn</span></span>

<span data-ttu-id="47d78-107">You learn how to create an Azure storage account and an Azure Function App to store IoT Hub messages in Azure table storage.</span><span class="sxs-lookup"><span data-stu-id="47d78-107">You learn how to create an Azure storage account and an Azure Function App to store IoT Hub messages in Azure table storage.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="47d78-108">What you will do</span><span class="sxs-lookup"><span data-stu-id="47d78-108">What you will do</span></span>

- <span data-ttu-id="47d78-109">Create an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="47d78-109">Create an Azure storage account.</span></span>
- <span data-ttu-id="47d78-110">Prepare for IoT Hub connection to read messages.</span><span class="sxs-lookup"><span data-stu-id="47d78-110">Prepare for IoT Hub connection to read messages.</span></span>
- <span data-ttu-id="47d78-111">Create and deploy an Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="47d78-111">Create and deploy an Azure Function App.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="47d78-112">What you will need</span><span class="sxs-lookup"><span data-stu-id="47d78-112">What you will need</span></span>

- <span data-ttu-id="47d78-113">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="47d78-113">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="47d78-114">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="47d78-114">An active Azure subscription.</span></span>
  - <span data-ttu-id="47d78-115">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="47d78-115">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="47d78-116">A running application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47d78-116">A running application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="47d78-117">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="47d78-117">Create an Azure storage account</span></span>

1. <span data-ttu-id="47d78-118">In the Azure portal, click **New** > **Storage** > **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="47d78-118">In the Azure portal, click **New** > **Storage** > **Storage account**.</span></span>
1. <span data-ttu-id="47d78-119">Enter the necessary information for the storage acount:</span><span class="sxs-lookup"><span data-stu-id="47d78-119">Enter the necessary information for the storage acount:</span></span>

   ![Create an storage account in the Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-store-data-in-azure-table-storage/1_azure-portal-create-storage-account.png)

   <span data-ttu-id="47d78-121">**Name**: The name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="47d78-121">**Name**: The name of the storage account.</span></span> <span data-ttu-id="47d78-122">The name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="47d78-122">The name must be globally unique.</span></span>

   <span data-ttu-id="47d78-123">**Resource group**: Use the same resource group that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="47d78-123">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="47d78-124">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="47d78-124">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>
1. <span data-ttu-id="47d78-125">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="47d78-125">Click **Create**.</span></span>

## <a name="prepare-for-iot-hub-connection-to-read-messages"></a><span data-ttu-id="47d78-126">Prepare for IoT Hub connection to read messages</span><span class="sxs-lookup"><span data-stu-id="47d78-126">Prepare for IoT Hub connection to read messages</span></span>

<span data-ttu-id="47d78-127">IoT Hub exposes a built-in Event Hub-compatible endpoint to enable applications to read IoT Hub messages.</span><span class="sxs-lookup"><span data-stu-id="47d78-127">IoT Hub exposes a built-in Event Hub-compatible endpoint to enable applications to read IoT Hub messages.</span></span> <span data-ttu-id="47d78-128">Meanwhile, applications use consumer groups to read data from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="47d78-128">Meanwhile, applications use consumer groups to read data from IoT Hub.</span></span> <span data-ttu-id="47d78-129">Before creating an Azure Function App to read data from your IoT hub, you need to:</span><span class="sxs-lookup"><span data-stu-id="47d78-129">Before creating an Azure Function App to read data from your IoT hub, you need to:</span></span>

- <span data-ttu-id="47d78-130">Get the connection string of your IoT hub endpoint.</span><span class="sxs-lookup"><span data-stu-id="47d78-130">Get the connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="47d78-131">Create a consumer group for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47d78-131">Create a consumer group for your IoT hub.</span></span>

### <a name="get-the-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="47d78-132">Get the connection string of your IoT hub endpoint</span><span class="sxs-lookup"><span data-stu-id="47d78-132">Get the connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="47d78-133">Open your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47d78-133">Open your IoT hub.</span></span>
1. <span data-ttu-id="47d78-134">On the **IoT Hub** pane, click **Endpoints** under **MESSAGING**.</span><span class="sxs-lookup"><span data-stu-id="47d78-134">On the **IoT Hub** pane, click **Endpoints** under **MESSAGING**.</span></span>
1. <span data-ttu-id="47d78-135">On the right pane, click **Events** under **Built-in endpoints**.</span><span class="sxs-lookup"><span data-stu-id="47d78-135">On the right pane, click **Events** under **Built-in endpoints**.</span></span>
1. <span data-ttu-id="47d78-136">In the **Properties** pane, make a note of the following values:</span><span class="sxs-lookup"><span data-stu-id="47d78-136">In the **Properties** pane, make a note of the following values:</span></span>
   - <span data-ttu-id="47d78-137">Event Hub-compatible endpoint</span><span class="sxs-lookup"><span data-stu-id="47d78-137">Event Hub-compatible endpoint</span></span>
   - <span data-ttu-id="47d78-138">Event Hub-compatible name</span><span class="sxs-lookup"><span data-stu-id="47d78-138">Event Hub-compatible name</span></span>

   ![Get the connection string of your IoT hub endpoint in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-store-data-in-azure-table-storage/2_azure-portal-iot-hub-endpoint-connection-string.png)

1. <span data-ttu-id="47d78-140">On the **IoT Hub** pane, click **Shared access policies** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="47d78-140">On the **IoT Hub** pane, click **Shared access policies** under **SETTINGS**.</span></span>
1. <span data-ttu-id="47d78-141">Click **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="47d78-141">Click **iothubowner**.</span></span>
1. <span data-ttu-id="47d78-142">Make a note of the **Primary key** value.</span><span class="sxs-lookup"><span data-stu-id="47d78-142">Make a note of the **Primary key** value.</span></span>
1. <span data-ttu-id="47d78-143">Make up the connection string of your IoT hub endpoint as follows:</span><span class="sxs-lookup"><span data-stu-id="47d78-143">Make up the connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!Note]
   > <span data-ttu-id="47d78-144">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with the values you noted down.</span><span class="sxs-lookup"><span data-stu-id="47d78-144">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with the values you noted down.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="47d78-145">Create a consumer group for your IoT hub</span><span class="sxs-lookup"><span data-stu-id="47d78-145">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="47d78-146">Open your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47d78-146">Open your IoT hub.</span></span>
1. <span data-ttu-id="47d78-147">On the **IoT Hub** pane, click **Endpoints** under **MESSAGING**.</span><span class="sxs-lookup"><span data-stu-id="47d78-147">On the **IoT Hub** pane, click **Endpoints** under **MESSAGING**.</span></span>
1. <span data-ttu-id="47d78-148">On the right pane, click **Events** under **Built-in endpoints**.</span><span class="sxs-lookup"><span data-stu-id="47d78-148">On the right pane, click **Events** under **Built-in endpoints**.</span></span>
1. <span data-ttu-id="47d78-149">In the **Properties** pane, enter a name under **Consumer groups** and make a note of the name.</span><span class="sxs-lookup"><span data-stu-id="47d78-149">In the **Properties** pane, enter a name under **Consumer groups** and make a note of the name.</span></span>
1. <span data-ttu-id="47d78-150">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="47d78-150">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="47d78-151">Create and deploy an Azure Function App</span><span class="sxs-lookup"><span data-stu-id="47d78-151">Create and deploy an Azure Function App</span></span>

1. <span data-ttu-id="47d78-152">In the [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App**.</span><span class="sxs-lookup"><span data-stu-id="47d78-152">In the [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App**.</span></span>
1. <span data-ttu-id="47d78-153">Enter the necessary information for the Function App.</span><span class="sxs-lookup"><span data-stu-id="47d78-153">Enter the necessary information for the Function App.</span></span>

   ![Create an Fuction App in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-store-data-in-azure-table-storage/3_azure-portal-create-function-app.png)

   <span data-ttu-id="47d78-155">**App name**: The name of the Function App.</span><span class="sxs-lookup"><span data-stu-id="47d78-155">**App name**: The name of the Function App.</span></span> <span data-ttu-id="47d78-156">The name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="47d78-156">The name must be globally unique.</span></span>

   <span data-ttu-id="47d78-157">**Resource group**: Use the same resource group that your IoT Hub uses.</span><span class="sxs-lookup"><span data-stu-id="47d78-157">**Resource group**: Use the same resource group that your IoT Hub uses.</span></span>

   <span data-ttu-id="47d78-158">**Storage Account**: The storage account that you created.</span><span class="sxs-lookup"><span data-stu-id="47d78-158">**Storage Account**: The storage account that you created.</span></span>

   <span data-ttu-id="47d78-159">**Pin to dashboard**: Check this option for easy access to the Function App from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="47d78-159">**Pin to dashboard**: Check this option for easy access to the Function App from the dashboard.</span></span>
1. <span data-ttu-id="47d78-160">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="47d78-160">Click **Create**.</span></span>
1. <span data-ttu-id="47d78-161">Open the Function App once it is created.</span><span class="sxs-lookup"><span data-stu-id="47d78-161">Open the Function App once it is created.</span></span>
1. <span data-ttu-id="47d78-162">Create a new function in the Function App.</span><span class="sxs-lookup"><span data-stu-id="47d78-162">Create a new function in the Function App.</span></span>
   1. <span data-ttu-id="47d78-163">Click **New Function**.</span><span class="sxs-lookup"><span data-stu-id="47d78-163">Click **New Function**.</span></span>
   1. <span data-ttu-id="47d78-164">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span><span class="sxs-lookup"><span data-stu-id="47d78-164">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>
   1. <span data-ttu-id="47d78-165">Click the **EventHubTrigger-JavaScript** template.</span><span class="sxs-lookup"><span data-stu-id="47d78-165">Click the **EventHubTrigger-JavaScript** template.</span></span>
   1. <span data-ttu-id="47d78-166">Enter the necessary information for the template.</span><span class="sxs-lookup"><span data-stu-id="47d78-166">Enter the necessary information for the template.</span></span>

      <span data-ttu-id="47d78-167">**Name your function**: The name of the functio.</span><span class="sxs-lookup"><span data-stu-id="47d78-167">**Name your function**: The name of the functio.</span></span>

      <span data-ttu-id="47d78-168">**Event Hub name**: The Event Hub-compatible name you noted down.</span><span class="sxs-lookup"><span data-stu-id="47d78-168">**Event Hub name**: The Event Hub-compatible name you noted down.</span></span>

      <span data-ttu-id="47d78-169">**Event Hub connection**: Click new to add the connection string of your IoT hub endpoint that you made up.</span><span class="sxs-lookup"><span data-stu-id="47d78-169">**Event Hub connection**: Click new to add the connection string of your IoT hub endpoint that you made up.</span></span>
   1. <span data-ttu-id="47d78-170">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="47d78-170">Click **Create**.</span></span>
1. <span data-ttu-id="47d78-171">Configure an output of the function.</span><span class="sxs-lookup"><span data-stu-id="47d78-171">Configure an output of the function.</span></span>
   1. <span data-ttu-id="47d78-172">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span><span class="sxs-lookup"><span data-stu-id="47d78-172">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Add a table storage to your Fuction App in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-store-data-in-azure-table-storage/4_azure-portal-function-app-add-output-table-storage.png)
   1. <span data-ttu-id="47d78-174">Enter the necessary information.</span><span class="sxs-lookup"><span data-stu-id="47d78-174">Enter the necessary information.</span></span>

      <span data-ttu-id="47d78-175">**Table name**: Use `deviceData` for the name.</span><span class="sxs-lookup"><span data-stu-id="47d78-175">**Table name**: Use `deviceData` for the name.</span></span>

      <span data-ttu-id="47d78-176">**Storage account connection**: Click **new** and select your storage account.</span><span class="sxs-lookup"><span data-stu-id="47d78-176">**Storage account connection**: Click **new** and select your storage account.</span></span>
   1. <span data-ttu-id="47d78-177">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="47d78-177">Click **Save**.</span></span>
1. <span data-ttu-id="47d78-178">Under **Triggers**, click **Azure Event Hub (myEventHubTrigger)**.</span><span class="sxs-lookup"><span data-stu-id="47d78-178">Under **Triggers**, click **Azure Event Hub (myEventHubTrigger)**.</span></span>
1. <span data-ttu-id="47d78-179">Under **Event Hub consumer group**, enter the name of the consumer group that you created, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="47d78-179">Under **Event Hub consumer group**, enter the name of the consumer group that you created, and then click **Save**.</span></span>
1. <span data-ttu-id="47d78-180">Click **Develop**, and then click **View files**.</span><span class="sxs-lookup"><span data-stu-id="47d78-180">Click **Develop**, and then click **View files**.</span></span>
1. <span data-ttu-id="47d78-181">Click **Add** to add a new file named `package.json`, paste in the following information, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="47d78-181">Click **Add** to add a new file named `package.json`, paste in the following information, and then click **Save**.</span></span>

   ```json
   {
      "name": "iothub_save_message_to_table",
      "version": "0.0.1",
      "private": true,
      "main": "index.js",
      "author": "Microsoft Corp.",
      "dependencies": {
         "azure-iothub": "1.0.9",
         "azure-iot-common": "1.0.7",
         "moment": "2.14.1"
      }
   }
   ```
1. <span data-ttu-id="47d78-182">Replace the code in `index.js` with the following, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="47d78-182">Replace the code in `index.js` with the following, and then click **Save**.</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is revieved in the IoTHub.
   // The message payload is persisted in an Azure Storage Table
   var moment = require('moment');

   module.exports = function (context, iotHubMessage) {
      context.log('Message received: ' + JSON.stringify(iotHubMessage));
      context.bindings.outputTable = {
      "partitionKey": moment.utc().format('YYYYMMDD'),
         "rowKey": moment.utc().format('hhmmss') + process.hrtime()[1] + '',
         "message": JSON.stringify(iotHubMessage)
      };
      context.done();
   };
   ```
1. <span data-ttu-id="47d78-183">Click **Function app settings** > **Open dev console**.</span><span class="sxs-lookup"><span data-stu-id="47d78-183">Click **Function app settings** > **Open dev console**.</span></span>

   <span data-ttu-id="47d78-184">You should be at the `wwwroot` folder of the Function App.</span><span class="sxs-lookup"><span data-stu-id="47d78-184">You should be at the `wwwroot` folder of the Function App.</span></span>
1. <span data-ttu-id="47d78-185">Go to the function folder by running the following command:</span><span class="sxs-lookup"><span data-stu-id="47d78-185">Go to the function folder by running the following command:</span></span>

   ```bash
   cd <your function name>
   ```
1. <span data-ttu-id="47d78-186">Install the npm package by running the following command:</span><span class="sxs-lookup"><span data-stu-id="47d78-186">Install the npm package by running the following command:</span></span>

   ```bash
   npm install
   ```

   > [!Note]
   > <span data-ttu-id="47d78-187">The installation may take some time to complete.</span><span class="sxs-lookup"><span data-stu-id="47d78-187">The installation may take some time to complete.</span></span>

<span data-ttu-id="47d78-188">By now, you have created the Function App.</span><span class="sxs-lookup"><span data-stu-id="47d78-188">By now, you have created the Function App.</span></span> <span data-ttu-id="47d78-189">It stores messages that your IoT hub receives in your Azure table storage.</span><span class="sxs-lookup"><span data-stu-id="47d78-189">It stores messages that your IoT hub receives in your Azure table storage.</span></span>

> [!Note]
> <span data-ttu-id="47d78-190">You can use the **Run** button to test the Function App.</span><span class="sxs-lookup"><span data-stu-id="47d78-190">You can use the **Run** button to test the Function App.</span></span> <span data-ttu-id="47d78-191">When you click **Run**, the test message is sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47d78-191">When you click **Run**, the test message is sent to your IoT hub.</span></span> <span data-ttu-id="47d78-192">The arrival of the message should trigger the Function App to start and then save the message to your Azure table storage.</span><span class="sxs-lookup"><span data-stu-id="47d78-192">The arrival of the message should trigger the Function App to start and then save the message to your Azure table storage.</span></span> <span data-ttu-id="47d78-193">The **Logs** pane records the details of the process.</span><span class="sxs-lookup"><span data-stu-id="47d78-193">The **Logs** pane records the details of the process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="47d78-194">Verify your message in your table storage</span><span class="sxs-lookup"><span data-stu-id="47d78-194">Verify your message in your table storage</span></span>

1. <span data-ttu-id="47d78-195">Run the sample application on your device to send messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47d78-195">Run the sample application on your device to send messages to your IoT hub.</span></span>
1. <span data-ttu-id="47d78-196">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="47d78-196">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="47d78-197">Open Microsoft Azure Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="47d78-197">Open Microsoft Azure Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span></span>
1. <span data-ttu-id="47d78-198">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="47d78-198">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="47d78-199">You should see messages sent from your device to your IoT hub logged in the `deviceData` table.</span><span class="sxs-lookup"><span data-stu-id="47d78-199">You should see messages sent from your device to your IoT hub logged in the `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47d78-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="47d78-200">Next steps</span></span>

<span data-ttu-id="47d78-201">You’ve successfully created your Azure storage account and Azure Function App to store messages that your IoT hub receives in your Azure table storage.</span><span class="sxs-lookup"><span data-stu-id="47d78-201">You’ve successfully created your Azure storage account and Azure Function App to store messages that your IoT hub receives in your Azure table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]



