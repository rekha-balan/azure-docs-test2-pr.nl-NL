---
title: 'SensorTag device & Azure IoT Gateway - Lesson 2: Register device | Microsoft Docs'
description: ''
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure iot hub, internet of things cloud, azure iot hub create device, ti sensortag, ti ble
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 685a479583f5f11f57bef22dc5881285bb1f70d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552117"
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="4ecd8-103">Create your Azure IoT hub and register your device</span><span class="sxs-lookup"><span data-stu-id="4ecd8-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4ecd8-104">What you will do</span><span class="sxs-lookup"><span data-stu-id="4ecd8-104">What you will do</span></span>

- <span data-ttu-id="4ecd8-105">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="4ecd8-105">Create a resource group</span></span>
- <span data-ttu-id="4ecd8-106">Create your first IoT hub</span><span class="sxs-lookup"><span data-stu-id="4ecd8-106">Create your first IoT hub</span></span>
- <span data-ttu-id="4ecd8-107">Register your device in your IoT hub by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-107">Register your device in your IoT hub by using the Azure CLI.</span></span> 

<span data-ttu-id="4ecd8-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span></span> 

<span data-ttu-id="4ecd8-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4ecd8-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4ecd8-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="4ecd8-110">What you will learn</span></span>

<span data-ttu-id="4ecd8-111">In this lesson, you will learn:</span><span class="sxs-lookup"><span data-stu-id="4ecd8-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="4ecd8-112">How to use the Azure CLI to create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-112">How to use the Azure CLI to create an IoT hub.</span></span>
- <span data-ttu-id="4ecd8-113">How to register a device in an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-113">How to register a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4ecd8-114">What you need</span><span class="sxs-lookup"><span data-stu-id="4ecd8-114">What you need</span></span>

- <span data-ttu-id="4ecd8-115">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-115">An active Azure subscription.</span></span> <span data-ttu-id="4ecd8-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="4ecd8-117">You should have the Azure CLI installed.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-117">You should have the Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="4ecd8-118">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="4ecd8-118">Create an IoT hub</span></span>

<span data-ttu-id="4ecd8-119">To create an IoT hub, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="4ecd8-119">To create an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="4ecd8-120">Sign in to your Azure account by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4ecd8-120">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="4ecd8-121">All your available subscriptions will be listed after a successful sign-in.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="4ecd8-122">Set the default Azure subscription that you want to use by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4ecd8-122">Set the default Azure subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="4ecd8-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="4ecd8-124">Register the provider by running the following command.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-124">Register the provider by running the following command.</span></span> <span data-ttu-id="4ecd8-125">Resource providers are services that provide resources for your application.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="4ecd8-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="4ecd8-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4ecd8-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="4ecd8-128">`westus` is the location you create your resource group.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-128">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="4ecd8-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="4ecd8-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4ecd8-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="4ecd8-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="4ecd8-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="4ecd8-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="4ecd8-133">The name of your IoT hub must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-133">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="4ecd8-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="4ecd8-135">Register your device in your IoT hub</span><span class="sxs-lookup"><span data-stu-id="4ecd8-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="4ecd8-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="4ecd8-137">Register your device in your IoT hub by running following command:</span><span class="sxs-lookup"><span data-stu-id="4ecd8-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="4ecd8-138">Summary</span><span class="sxs-lookup"><span data-stu-id="4ecd8-138">Summary</span></span>

<span data-ttu-id="4ecd8-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="4ecd8-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4ecd8-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ecd8-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ecd8-141">Next steps</span></span>
[<span data-ttu-id="4ecd8-142">Configure and run a BLE sample app</span><span class="sxs-lookup"><span data-stu-id="4ecd8-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)