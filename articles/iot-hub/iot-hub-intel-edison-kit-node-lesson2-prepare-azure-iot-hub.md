---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 2: Register device | Microsoft Docs'
description: Create a resource group, create an Azure IoT hub, and register Edison in the Azure IoT hub by using the Azure CLI.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: ''
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: c1465cc2-d0d9-4326-967c-64d95b61dd54
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 81584c1b7314c4331ac059b8e3ed782970588ae2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563021"
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="a09a7-103">Create your IoT hub and register Intel Edison</span><span class="sxs-lookup"><span data-stu-id="a09a7-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a09a7-104">What you will do</span><span class="sxs-lookup"><span data-stu-id="a09a7-104">What you will do</span></span>
* <span data-ttu-id="a09a7-105">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="a09a7-105">Create a resource group.</span></span>
* <span data-ttu-id="a09a7-106">Create your Azure IoT hub in the resource group.</span><span class="sxs-lookup"><span data-stu-id="a09a7-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="a09a7-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="a09a7-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="a09a7-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span><span class="sxs-lookup"><span data-stu-id="a09a7-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="a09a7-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a09a7-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a09a7-110">What you will learn</span><span class="sxs-lookup"><span data-stu-id="a09a7-110">What you will learn</span></span>
<span data-ttu-id="a09a7-111">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="a09a7-111">In this article, you will learn:</span></span>
* <span data-ttu-id="a09a7-112">How to use the Azure CLI to create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a09a7-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="a09a7-113">How to create a device identity for Edison in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a09a7-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a09a7-114">What you need</span><span class="sxs-lookup"><span data-stu-id="a09a7-114">What you need</span></span>
* <span data-ttu-id="a09a7-115">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="a09a7-115">An Azure account.</span></span> <span data-ttu-id="a09a7-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="a09a7-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="a09a7-117">You should have the Azure CLI installed.</span><span class="sxs-lookup"><span data-stu-id="a09a7-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="a09a7-118">Create your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a09a7-118">Create your IoT hub</span></span>
<span data-ttu-id="a09a7-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span><span class="sxs-lookup"><span data-stu-id="a09a7-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="a09a7-120">To create your IoT hub, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="a09a7-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="a09a7-121">Sign in to your Azure account by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a09a7-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="a09a7-122">All your available subscriptions are listed after a successful sign-in.</span><span class="sxs-lookup"><span data-stu-id="a09a7-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="a09a7-123">Set the default subscription that you want to use by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a09a7-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="a09a7-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span><span class="sxs-lookup"><span data-stu-id="a09a7-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="a09a7-125">Register the provider by running the following command.</span><span class="sxs-lookup"><span data-stu-id="a09a7-125">Register the provider by running the following command.</span></span> <span data-ttu-id="a09a7-126">Resource providers are services that provide resources for your application.</span><span class="sxs-lookup"><span data-stu-id="a09a7-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="a09a7-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span><span class="sxs-lookup"><span data-stu-id="a09a7-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="a09a7-128">Create a resource group named iot-sample in the West US region by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a09a7-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="a09a7-129">`westus` is the location you create your resource group.</span><span class="sxs-lookup"><span data-stu-id="a09a7-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="a09a7-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span><span class="sxs-lookup"><span data-stu-id="a09a7-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="a09a7-131">Create an IoT hub in the iot-sample resource group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a09a7-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="a09a7-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span><span class="sxs-lookup"><span data-stu-id="a09a7-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="a09a7-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="a09a7-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="a09a7-134">The name of your IoT hub must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="a09a7-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="a09a7-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a09a7-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="a09a7-136">Register Edison in your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a09a7-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="a09a7-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span><span class="sxs-lookup"><span data-stu-id="a09a7-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="a09a7-138">Register Edison in your IoT hub by running following command:</span><span class="sxs-lookup"><span data-stu-id="a09a7-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="a09a7-139">Summary</span><span class="sxs-lookup"><span data-stu-id="a09a7-139">Summary</span></span>
<span data-ttu-id="a09a7-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a09a7-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="a09a7-141">You're ready to learn how to send messages from Edison to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a09a7-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a09a7-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="a09a7-142">Next steps</span></span>
<span data-ttu-id="a09a7-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="a09a7-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md