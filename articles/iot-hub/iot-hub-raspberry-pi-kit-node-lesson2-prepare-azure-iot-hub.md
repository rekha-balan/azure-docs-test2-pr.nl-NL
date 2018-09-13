---
featureFlags:
- usabilla
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 2: Register device | Microsoft Docs'
description: Create a resource group, create an Azure IoT hub, and register Pi in the IoT Hub identity registry by using Azure CLI.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: raspberry pi cloud, pi cloud connect
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564516"
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="3f4b7-104">Create your IoT hub and register Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="3f4b7-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="3f4b7-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="3f4b7-105">What you will do</span></span>
* <span data-ttu-id="3f4b7-106">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-106">Create a resource group.</span></span>
* <span data-ttu-id="3f4b7-107">Create your Azure IoT hub in the resource group.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="3f4b7-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="3f4b7-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="3f4b7-109">When you use Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-109">When you use Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="3f4b7-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3f4b7-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3f4b7-111">What you will learn</span><span class="sxs-lookup"><span data-stu-id="3f4b7-111">What you will learn</span></span>
<span data-ttu-id="3f4b7-112">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="3f4b7-112">In this article, you will learn:</span></span>
* <span data-ttu-id="3f4b7-113">How to use Azure CLI to create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="3f4b7-113">How to use Azure CLI to create an IoT hub</span></span>
* <span data-ttu-id="3f4b7-114">How to create a device identity for Pi in your IoT hub</span><span class="sxs-lookup"><span data-stu-id="3f4b7-114">How to create a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3f4b7-115">What you need</span><span class="sxs-lookup"><span data-stu-id="3f4b7-115">What you need</span></span>
* <span data-ttu-id="3f4b7-116">An Azure account</span><span class="sxs-lookup"><span data-stu-id="3f4b7-116">An Azure account</span></span>
* <span data-ttu-id="3f4b7-117">A Mac or a Windows computer with the Azure CLI installed</span><span class="sxs-lookup"><span data-stu-id="3f4b7-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="3f4b7-118">Create your IoT hub</span><span class="sxs-lookup"><span data-stu-id="3f4b7-118">Create your IoT hub</span></span>
<span data-ttu-id="3f4b7-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="3f4b7-120">To create your IoT hub, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="3f4b7-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="3f4b7-121">Sign in to your Azure account by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3f4b7-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="3f4b7-122">All your available subscriptions are listed after a successful sign-in.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="3f4b7-123">Set the default subscription that you want to use by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3f4b7-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="3f4b7-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="3f4b7-125">Register the provider by running the following command.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-125">Register the provider by running the following command.</span></span> <span data-ttu-id="3f4b7-126">Resource providers are services that provide resources for your application.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="3f4b7-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="3f4b7-128">Create a resource group named iot-sample in the West US region by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3f4b7-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="3f4b7-129">`westus` is the location you create your resource group.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="3f4b7-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="3f4b7-131">Create an IoT hub in the iot-sample resource group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3f4b7-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="3f4b7-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="3f4b7-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="3f4b7-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="3f4b7-134">The name of your IoT hub must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="3f4b7-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="3f4b7-136">Register Pi in your IoT hub</span><span class="sxs-lookup"><span data-stu-id="3f4b7-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="3f4b7-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="3f4b7-138">You will use Azure CLI to register your Pi and create a self-signed X.509 certificate for device authentication.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-138">You will use Azure CLI to register your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="3f4b7-139">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="3f4b7-139">Run the following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="3f4b7-140">Summary</span><span class="sxs-lookup"><span data-stu-id="3f4b7-140">Summary</span></span>
<span data-ttu-id="3f4b7-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="3f4b7-142">You're ready to learn how to send messages from Pi to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3f4b7-142">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f4b7-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f4b7-143">Next steps</span></span>
[<span data-ttu-id="3f4b7-144">Create an Azure function app and an Azure storage account to process and store IoT hub messages</span><span class="sxs-lookup"><span data-stu-id="3f4b7-144">Create an Azure function app and an Azure storage account to process and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

