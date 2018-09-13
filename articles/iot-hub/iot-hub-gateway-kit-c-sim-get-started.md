---
title: Simulated device & Azure IoT Gateway - Get started | Microsoft Docs
description: Get started with IoT Gateway Starter Kit, create your Azure IoT hub, and connect Gateway to the IoT hub
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure iot hub, iot gateway, getting started with the internet of things, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 937ae01584dd6d2e7b986c1e2410a7192cf173e6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563011"
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="35b1c-104">Get started with IoT Gateway Starter Kit with a simulated device</span><span class="sxs-lookup"><span data-stu-id="35b1c-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [Simulated Device](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="35b1c-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="35b1c-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="35b1c-108">You will be working with Intel NUC that's running Wind River Linux.</span><span class="sxs-lookup"><span data-stu-id="35b1c-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="35b1c-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="35b1c-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="35b1c-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="35b1c-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="35b1c-111">Lesson 1: Configure your NUC</span><span class="sxs-lookup"><span data-stu-id="35b1c-111">Lesson 1: Configure your NUC</span></span>
![Lesson1 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="35b1c-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Gateway SDK package on NUC, and run a sample app to verify the gateway functionality.</span><span class="sxs-lookup"><span data-stu-id="35b1c-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Gateway SDK package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="35b1c-114">*Estimated time to complete: 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="35b1c-114">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="35b1c-115">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="35b1c-115">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="35b1c-116">Lesson 2: Create your IoT Hub</span><span class="sxs-lookup"><span data-stu-id="35b1c-116">Lesson 2: Create your IoT Hub</span></span>
![Lesson2 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="35b1c-118">In this lesson, you install the tools and software on your host computer.</span><span class="sxs-lookup"><span data-stu-id="35b1c-118">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="35b1c-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="35b1c-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="35b1c-120">Complete Lesson 1 before you start this lesson.</span><span class="sxs-lookup"><span data-stu-id="35b1c-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="35b1c-121">Get the tools</span><span class="sxs-lookup"><span data-stu-id="35b1c-121">Get the tools</span></span>
<span data-ttu-id="35b1c-122">Install the tools and software on your host computer.</span><span class="sxs-lookup"><span data-stu-id="35b1c-122">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="35b1c-123">*Estimated time to complete: 20 minutes*</span><span class="sxs-lookup"><span data-stu-id="35b1c-123">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="35b1c-124">Go to [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="35b1c-124">Go to [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="35b1c-125">Create an IoT hub and register your device</span><span class="sxs-lookup"><span data-stu-id="35b1c-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="35b1c-126">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="35b1c-126">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="35b1c-127">*Estimated time to complete: 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="35b1c-127">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="35b1c-128">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="35b1c-128">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="35b1c-129">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="35b1c-129">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="35b1c-130">In this lesson, you will use scripts to automate the configuration and execution of a simulated device app in your gateway.</span><span class="sxs-lookup"><span data-stu-id="35b1c-130">In this lesson, you will use scripts to automate the configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="35b1c-131">The simulated device app generates sample temperature data and sends it to an IoT hub module.</span><span class="sxs-lookup"><span data-stu-id="35b1c-131">The simulated device app generates sample temperature data and sends it to an IoT hub module.</span></span> <span data-ttu-id="35b1c-132">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in the Azure IoT Gateway SDK.</span><span class="sxs-lookup"><span data-stu-id="35b1c-132">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in the Azure IoT Gateway SDK.</span></span>

![Lesson 3 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="35b1c-134">Configure and run a simulated device</span><span class="sxs-lookup"><span data-stu-id="35b1c-134">Configure and run a simulated device</span></span>
<span data-ttu-id="35b1c-135">Prepare the sample codes.</span><span class="sxs-lookup"><span data-stu-id="35b1c-135">Prepare the sample codes.</span></span> <span data-ttu-id="35b1c-136">Then configure and run the simulated device sample application.</span><span class="sxs-lookup"><span data-stu-id="35b1c-136">Then configure and run the simulated device sample application.</span></span>

<span data-ttu-id="35b1c-137">*Estimated time to complete: 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="35b1c-137">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="35b1c-138">Go to [Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="35b1c-138">Go to [Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="35b1c-139">Read messages from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="35b1c-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="35b1c-140">Run a sample code on your host computer to read the messages from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="35b1c-140">Run a sample code on your host computer to read the messages from your IoT hub.</span></span>

<span data-ttu-id="35b1c-141">*Estimated time to complete: 15 minutes*</span><span class="sxs-lookup"><span data-stu-id="35b1c-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="35b1c-142">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="35b1c-142">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="35b1c-143">Lesson 4: Save messages to Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="35b1c-143">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="35b1c-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="35b1c-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Lesson 4 end-to-end diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="35b1c-146">Create an Azure function app and Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="35b1c-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="35b1c-147">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="35b1c-147">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="35b1c-148">*Estimated time to complete: 10 minutes*</span><span class="sxs-lookup"><span data-stu-id="35b1c-148">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="35b1c-149">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="35b1c-149">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="35b1c-150">Read messages persisted in Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="35b1c-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="35b1c-151">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="35b1c-151">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="35b1c-152">*Estimated time to complete: 5 minutes*</span><span class="sxs-lookup"><span data-stu-id="35b1c-152">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="35b1c-153">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="35b1c-153">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="35b1c-154">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="35b1c-154">Troubleshooting</span></span>
<span data-ttu-id="35b1c-155">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span><span class="sxs-lookup"><span data-stu-id="35b1c-155">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="35b1c-156">Explore more</span><span class="sxs-lookup"><span data-stu-id="35b1c-156">Explore more</span></span>
<span data-ttu-id="35b1c-157">Visit the [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) to learn more.</span><span class="sxs-lookup"><span data-stu-id="35b1c-157">Visit the [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) to learn more.</span></span>



