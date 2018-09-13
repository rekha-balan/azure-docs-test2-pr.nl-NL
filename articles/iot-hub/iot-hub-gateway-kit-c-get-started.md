---
title: SensorTag device & Azure IoT Gateway - Get started | Microsoft Docs
description: Get started with IoT Gateway Starter Kit, create your Azure IoT hub, and connect SensorTag and Gateway to the IoT hub
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure iot hub, iot gateway, getting started with the internet of things, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7f186167509769fbdc1f4aa2ae06657ff0b1424c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661807"
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="0aa90-104">Get started with IoT Gateway Starter Kit with a SensorTag</span><span class="sxs-lookup"><span data-stu-id="0aa90-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Simulated Device](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="0aa90-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="0aa90-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="0aa90-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="0aa90-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="0aa90-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0aa90-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="0aa90-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="0aa90-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="0aa90-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="0aa90-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="0aa90-112">Lesson 1: Configure your NUC</span><span class="sxs-lookup"><span data-stu-id="0aa90-112">Lesson 1: Configure your NUC</span></span>
![Lesson1 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="0aa90-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Gateway SDK package on NUC, and run a sample app to verify the gateway functionality.</span><span class="sxs-lookup"><span data-stu-id="0aa90-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Gateway SDK package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="0aa90-115">*Estimated time to complete: 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="0aa90-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="0aa90-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="0aa90-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="0aa90-117">Lesson 2: Create your IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0aa90-117">Lesson 2: Create your IoT Hub</span></span>
![Lesson2 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="0aa90-119">In this lesson, you install the tools and software on your host computer.</span><span class="sxs-lookup"><span data-stu-id="0aa90-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="0aa90-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0aa90-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="0aa90-121">Complete Lesson 1 before you start this lesson.</span><span class="sxs-lookup"><span data-stu-id="0aa90-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="0aa90-122">Get the tools</span><span class="sxs-lookup"><span data-stu-id="0aa90-122">Get the tools</span></span>
<span data-ttu-id="0aa90-123">Install the tools and software on your host computer.</span><span class="sxs-lookup"><span data-stu-id="0aa90-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="0aa90-124">*Estimated time to complete: 20 minutes*</span><span class="sxs-lookup"><span data-stu-id="0aa90-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="0aa90-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="0aa90-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="0aa90-126">Create an IoT hub and register your device</span><span class="sxs-lookup"><span data-stu-id="0aa90-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="0aa90-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0aa90-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="0aa90-128">*Estimated time to complete: 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="0aa90-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="0aa90-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="0aa90-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="0aa90-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="0aa90-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="0aa90-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span><span class="sxs-lookup"><span data-stu-id="0aa90-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="0aa90-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span><span class="sxs-lookup"><span data-stu-id="0aa90-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="0aa90-133">Modules communicate with one another via a message broker.</span><span class="sxs-lookup"><span data-stu-id="0aa90-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="0aa90-134">The sample application has a BLE module and an IoT hub module.</span><span class="sxs-lookup"><span data-stu-id="0aa90-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="0aa90-135">The BLE module receives data from BLE SensorTag.</span><span class="sxs-lookup"><span data-stu-id="0aa90-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="0aa90-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in the Azure IoT Gateway SDK.</span><span class="sxs-lookup"><span data-stu-id="0aa90-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in the Azure IoT Gateway SDK.</span></span>

![Lesson 3 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="0aa90-138">Configure and run the BLE sample app</span><span class="sxs-lookup"><span data-stu-id="0aa90-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="0aa90-139">Set up the connectivity between SensorTag and your gateway.</span><span class="sxs-lookup"><span data-stu-id="0aa90-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="0aa90-140">Then finish the configuration and run the BLE sample application.</span><span class="sxs-lookup"><span data-stu-id="0aa90-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="0aa90-141">*Estimated time to complete: 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="0aa90-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="0aa90-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="0aa90-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="0aa90-143">Read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="0aa90-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="0aa90-144">Run sample code on your host computer to read messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0aa90-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="0aa90-145">*Estimated time to complete: 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="0aa90-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="0aa90-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="0aa90-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="0aa90-147">Lesson 4: Save messages to Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="0aa90-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="0aa90-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="0aa90-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Lesson 4 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="0aa90-150">Create an Azure function app and Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="0aa90-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="0aa90-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="0aa90-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="0aa90-152">*Estimated time to complete: 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="0aa90-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="0aa90-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="0aa90-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="0aa90-154">Read messages persisted in Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="0aa90-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="0aa90-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="0aa90-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="0aa90-156">*Estimated time to complete: 5 minutes*</span><span class="sxs-lookup"><span data-stu-id="0aa90-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="0aa90-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0aa90-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0aa90-158">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="0aa90-158">Troubleshooting</span></span>
<span data-ttu-id="0aa90-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span><span class="sxs-lookup"><span data-stu-id="0aa90-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="0aa90-160">Explore more</span><span class="sxs-lookup"><span data-stu-id="0aa90-160">Explore more</span></span>
<span data-ttu-id="0aa90-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span><span class="sxs-lookup"><span data-stu-id="0aa90-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>



