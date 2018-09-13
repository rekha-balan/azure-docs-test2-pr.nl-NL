---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 3: Create function app | Microsoft Docs'
description: The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: storing data in the cloud, data stored in cloud, iot cloud service
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 37ee5962-95ce-40e8-8162-17e735eaec21
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: be4f9849cdd33691e6a1adbd54d1240e0a6d9191
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672219"
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="e03f3-104">Create an Azure function app and Azure storage account</span><span class="sxs-lookup"><span data-stu-id="e03f3-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="e03f3-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span><span class="sxs-lookup"><span data-stu-id="e03f3-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="e03f3-106">An Azure function app hosts the execution of your functions in Azure.</span><span class="sxs-lookup"><span data-stu-id="e03f3-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="e03f3-107">What will you do</span><span class="sxs-lookup"><span data-stu-id="e03f3-107">What will you do</span></span>
<span data-ttu-id="e03f3-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="e03f3-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="e03f3-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="e03f3-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="e03f3-110">The storage account is used for reading the persisted copies of messages from Azure table.</span><span class="sxs-lookup"><span data-stu-id="e03f3-110">The storage account is used for reading the persisted copies of messages from Azure table.</span></span> <span data-ttu-id="e03f3-111">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e03f3-111">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="e03f3-112">What will you learn</span><span class="sxs-lookup"><span data-stu-id="e03f3-112">What will you learn</span></span>
<span data-ttu-id="e03f3-113">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="e03f3-113">In this article, you will learn:</span></span>
* <span data-ttu-id="e03f3-114">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e03f3-114">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="e03f3-115">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="e03f3-115">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="e03f3-116">What do you need</span><span class="sxs-lookup"><span data-stu-id="e03f3-116">What do you need</span></span>
<span data-ttu-id="e03f3-117">You must have successfully completed:</span><span class="sxs-lookup"><span data-stu-id="e03f3-117">You must have successfully completed:</span></span>
- <span data-ttu-id="e03f3-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="e03f3-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="e03f3-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="e03f3-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="e03f3-120">Open the sample app</span><span class="sxs-lookup"><span data-stu-id="e03f3-120">Open the sample app</span></span>
<span data-ttu-id="e03f3-121">Open the sample project in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="e03f3-121">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Repo structure][repo-structure]

* <span data-ttu-id="e03f3-123">The file in the `app` subfolder is the key source file.</span><span class="sxs-lookup"><span data-stu-id="e03f3-123">The file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="e03f3-124">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span><span class="sxs-lookup"><span data-stu-id="e03f3-124">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="e03f3-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="e03f3-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="e03f3-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="e03f3-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="e03f3-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span><span class="sxs-lookup"><span data-stu-id="e03f3-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="e03f3-128">Configure Azure Resource Manager templates and create resources in Azure</span><span class="sxs-lookup"><span data-stu-id="e03f3-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="e03f3-129">Update the `arm-template-param.json` file in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e03f3-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager template parameters][arm-template-parameters]

* <span data-ttu-id="e03f3-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="e03f3-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="e03f3-132">Replace **[prefix string for new resources]** with any prefix you want.</span><span class="sxs-lookup"><span data-stu-id="e03f3-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="e03f3-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span><span class="sxs-lookup"><span data-stu-id="e03f3-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="e03f3-134">Do not use a dash or number initial in the prefix.</span><span class="sxs-lookup"><span data-stu-id="e03f3-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="e03f3-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span><span class="sxs-lookup"><span data-stu-id="e03f3-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="e03f3-136">It takes about five minutes to create these resources.</span><span class="sxs-lookup"><span data-stu-id="e03f3-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="e03f3-137">While the resource creation is in progress, you can move on to the next article.</span><span class="sxs-lookup"><span data-stu-id="e03f3-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="e03f3-138">Summary</span><span class="sxs-lookup"><span data-stu-id="e03f3-138">Summary</span></span>
<span data-ttu-id="e03f3-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span><span class="sxs-lookup"><span data-stu-id="e03f3-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="e03f3-140">You can now deploy and run the sample to send device-to-cloud messages on Edison.</span><span class="sxs-lookup"><span data-stu-id="e03f3-140">You can now deploy and run the sample to send device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e03f3-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="e03f3-141">Next steps</span></span>
<span data-ttu-id="e03f3-142">[Run a sample application to send device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="e03f3-142">[Run a sample application to send device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
