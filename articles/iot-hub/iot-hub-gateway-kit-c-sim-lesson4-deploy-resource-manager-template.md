---
title: 'Simulated device & Azure IoT Gateway - Lesson 4: Save messages | Microsoft Docs'
description: Save messages from Intel NUC to your IoT hub, write them to Azure Table storage and then read them from the cloud.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: storing data in the cloud, data stored in cloud, iot cloud service
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 586e6cb83a8193ff56c718edeb12bf7e286f9a84
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661282"
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="a6f2c-104">Create an Azure function app and storage account</span><span class="sxs-lookup"><span data-stu-id="a6f2c-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="a6f2c-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="a6f2c-106">An Azure function app hosts the execution of your functions in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="a6f2c-107">What you will do</span><span class="sxs-lookup"><span data-stu-id="a6f2c-107">What you will do</span></span>

- <span data-ttu-id="a6f2c-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="a6f2c-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="a6f2c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a6f2c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="a6f2c-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="a6f2c-111">What you will learn</span></span>

<span data-ttu-id="a6f2c-112">In this lesson, you will learn:</span><span class="sxs-lookup"><span data-stu-id="a6f2c-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="a6f2c-113">How to use Azure Resource Manager to deploy Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="a6f2c-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a6f2c-115">What you need</span><span class="sxs-lookup"><span data-stu-id="a6f2c-115">What you need</span></span>

<span data-ttu-id="a6f2c-116">You must have successfully completed the previous lessons:</span><span class="sxs-lookup"><span data-stu-id="a6f2c-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="a6f2c-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span><span class="sxs-lookup"><span data-stu-id="a6f2c-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [<span data-ttu-id="a6f2c-118">Lesson 2: Get your host computer and Azure IoT hub ready</span><span class="sxs-lookup"><span data-stu-id="a6f2c-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="a6f2c-119">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a6f2c-119">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="a6f2c-120">Open a sample app</span><span class="sxs-lookup"><span data-stu-id="a6f2c-120">Open a sample app</span></span>

<span data-ttu-id="a6f2c-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a6f2c-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![repo structure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="a6f2c-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="a6f2c-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="a6f2c-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="a6f2c-126">Configure Azure Resource Manager templates and create resources in Azure</span><span class="sxs-lookup"><span data-stu-id="a6f2c-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="a6f2c-127">Update the `arm-template-param.json` file in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![arm template json](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="a6f2c-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="a6f2c-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a6f2c-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="a6f2c-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="a6f2c-132">Summary</span><span class="sxs-lookup"><span data-stu-id="a6f2c-132">Summary</span></span>

<span data-ttu-id="a6f2c-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="a6f2c-134">You can now read messages that are sent by your gateway to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6f2c-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6f2c-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6f2c-135">Next steps</span></span>
<span data-ttu-id="a6f2c-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a6f2c-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>


