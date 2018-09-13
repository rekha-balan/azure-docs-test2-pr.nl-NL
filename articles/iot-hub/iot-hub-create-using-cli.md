---
title: Create an IoT Hub using Azure CLI (az.py) | Microsoft Docs
description: How to create an Azure IoT hub using the cross-platform Azure CLI 2.0 (az.py).
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: ''
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: dobett
ms.openlocfilehash: 5f5b9c18b37c9df6b091bde3e7e478a1cd1a0b1e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556710"
---
# <a name="create-an-iot-hub-using-the-azure-cli-20"></a><span data-ttu-id="d3119-103">Create an IoT hub using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3119-103">Create an IoT hub using the Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="d3119-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="d3119-104">Introduction</span></span>

<span data-ttu-id="d3119-105">You can use Azure CLI 2.0 (az.py) to create and manage Azure IoT hubs programmatically.</span><span class="sxs-lookup"><span data-stu-id="d3119-105">You can use Azure CLI 2.0 (az.py) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="d3119-106">This article shows you how to use the Azure CLI 2.0 (az.py) to create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3119-106">This article shows you how to use the Azure CLI 2.0 (az.py) to create an IoT hub.</span></span>

<span data-ttu-id="d3119-107">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="d3119-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="d3119-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – the CLI for the classic and resource management deployment models.</span><span class="sxs-lookup"><span data-stu-id="d3119-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – the CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="d3119-109">Azure CLI 2.0 (az.py) - the next generation CLI for the resource management deployment model as described in this article.</span><span class="sxs-lookup"><span data-stu-id="d3119-109">Azure CLI 2.0 (az.py) - the next generation CLI for the resource management deployment model as described in this article.</span></span>

<span data-ttu-id="d3119-110">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="d3119-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d3119-111">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="d3119-111">An active Azure account.</span></span> <span data-ttu-id="d3119-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="d3119-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="d3119-113">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="d3119-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="d3119-114">Sign in and set your Azure account</span><span class="sxs-lookup"><span data-stu-id="d3119-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="d3119-115">Sign in to your Azure account and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="d3119-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="d3119-116">At the command prompt, run the [login command][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="d3119-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="d3119-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span><span class="sxs-lookup"><span data-stu-id="d3119-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

2. <span data-ttu-id="d3119-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span><span class="sxs-lookup"><span data-stu-id="d3119-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="d3119-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span><span class="sxs-lookup"><span data-stu-id="d3119-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="d3119-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3119-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="d3119-121">You can use either the subscription name or ID from the output of the previous command:</span><span class="sxs-lookup"><span data-stu-id="d3119-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="d3119-122">Create an IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d3119-122">Create an IoT Hub</span></span>

<span data-ttu-id="d3119-123">Use the Azure CLI to create a resource group and then add an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3119-123">Use the Azure CLI to create a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="d3119-124">When you create an IoT hub, you must create it in a resource group.</span><span class="sxs-lookup"><span data-stu-id="d3119-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="d3119-125">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="d3119-125">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="d3119-126">The previous example creates the resource group in the West US location.</span><span class="sxs-lookup"><span data-stu-id="d3119-126">The previous example creates the resource group in the West US location.</span></span> <span data-ttu-id="d3119-127">You can view a list of available locations by running the command `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="d3119-127">You can view a list of available locations by running the command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="d3119-128">Run the following [command to create an IoT hub][lnk-az-iot-command] in your resource group:</span><span class="sxs-lookup"><span data-stu-id="d3119-128">Run the following [command to create an IoT hub][lnk-az-iot-command] in your resource group:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

> [!NOTE]
> <span data-ttu-id="d3119-129">The name of your IoT hub must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="d3119-129">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="d3119-130">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span><span class="sxs-lookup"><span data-stu-id="d3119-130">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="d3119-131">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="d3119-131">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="d3119-132">Remove an IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d3119-132">Remove an IoT Hub</span></span>

<span data-ttu-id="d3119-133">You can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="d3119-133">You can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="d3119-134">To delete an IoT hub, run the following command:</span><span class="sxs-lookup"><span data-stu-id="d3119-134">To delete an IoT hub, run the following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="d3119-135">To delete a resource group and all its resources, run the following command:</span><span class="sxs-lookup"><span data-stu-id="d3119-135">To delete a resource group and all its resources, run the following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="d3119-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3119-136">Next steps</span></span>
<span data-ttu-id="d3119-137">To learn more about developing for IoT Hub, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="d3119-137">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="d3119-138">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d3119-138">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="d3119-139">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="d3119-139">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d3119-140">[Using the Azure portal to manage IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="d3119-140">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
