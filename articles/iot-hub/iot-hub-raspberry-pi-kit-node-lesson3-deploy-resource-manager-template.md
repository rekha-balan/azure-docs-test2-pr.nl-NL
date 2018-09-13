---
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 3: Template deployment | Microsoft Docs'
description: The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: storing data in the cloud, data stored in cloud, iot cloud service
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f8d5d4d0fdf7d54501c7f89135ade0427f5f4b6e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554586"
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="5240d-104">Create an Azure function app and Azure storage account</span><span class="sxs-lookup"><span data-stu-id="5240d-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="5240d-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span><span class="sxs-lookup"><span data-stu-id="5240d-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="5240d-106">An Azure function app hosts the execution of your functions in Azure.</span><span class="sxs-lookup"><span data-stu-id="5240d-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5240d-107">What you will do</span><span class="sxs-lookup"><span data-stu-id="5240d-107">What you will do</span></span>
<span data-ttu-id="5240d-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="5240d-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="5240d-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="5240d-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="5240d-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5240d-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5240d-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="5240d-111">What you will learn</span></span>
<span data-ttu-id="5240d-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="5240d-112">In this article, you will learn:</span></span>

* <span data-ttu-id="5240d-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span><span class="sxs-lookup"><span data-stu-id="5240d-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="5240d-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="5240d-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5240d-115">What you need</span><span class="sxs-lookup"><span data-stu-id="5240d-115">What you need</span></span>
<span data-ttu-id="5240d-116">You must have successfully completed:</span><span class="sxs-lookup"><span data-stu-id="5240d-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="5240d-117">Get started with Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="5240d-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="5240d-118">Create your Azure IoT hub</span><span class="sxs-lookup"><span data-stu-id="5240d-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-the-sample-app"></a><span data-ttu-id="5240d-119">Open the sample app</span><span class="sxs-lookup"><span data-stu-id="5240d-119">Open the sample app</span></span>
<span data-ttu-id="5240d-120">Open the sample project in Visual Studio Code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="5240d-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Repo structure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="5240d-122">The `app.js` file in the `app` subfolder is the key source file.</span><span class="sxs-lookup"><span data-stu-id="5240d-122">The `app.js` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="5240d-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span><span class="sxs-lookup"><span data-stu-id="5240d-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="5240d-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="5240d-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="5240d-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="5240d-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="5240d-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span><span class="sxs-lookup"><span data-stu-id="5240d-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="5240d-127">Configure Azure Resource Manager templates and create resources in Azure</span><span class="sxs-lookup"><span data-stu-id="5240d-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="5240d-128">Update the `arm-template-param.json` file in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5240d-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager template parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="5240d-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5240d-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="5240d-131">Replace **[prefix string for new resources]** with any prefix you want.</span><span class="sxs-lookup"><span data-stu-id="5240d-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="5240d-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span><span class="sxs-lookup"><span data-stu-id="5240d-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="5240d-133">Do not use a dash or number initial in the prefix.</span><span class="sxs-lookup"><span data-stu-id="5240d-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="5240d-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span><span class="sxs-lookup"><span data-stu-id="5240d-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="5240d-135">It takes about five minutes to create these resources.</span><span class="sxs-lookup"><span data-stu-id="5240d-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="5240d-136">While the resource creation is in progress, you can move on to the next article.</span><span class="sxs-lookup"><span data-stu-id="5240d-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="5240d-137">Summary</span><span class="sxs-lookup"><span data-stu-id="5240d-137">Summary</span></span>
<span data-ttu-id="5240d-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span><span class="sxs-lookup"><span data-stu-id="5240d-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="5240d-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span><span class="sxs-lookup"><span data-stu-id="5240d-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5240d-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="5240d-140">Next steps</span></span>
[<span data-ttu-id="5240d-141">Run a sample application to send device-to-cloud messages on Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="5240d-141">Run a sample application to send device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)



