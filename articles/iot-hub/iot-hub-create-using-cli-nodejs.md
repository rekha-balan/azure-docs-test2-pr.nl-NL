---
title: Create an IoT hub using Azure CLI (azure.js) | Microsoft Docs
description: How to create an Azure IoT hub using the cross-platform Azure CLI (azure.js).
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: ''
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: boltean
ms.openlocfilehash: 8ac82da36b2edb71fcd0599dac12a3ed18e33b6f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553563"
---
# <a name="create-an-iot-hub-using-the-azure-cli"></a><span data-ttu-id="bd624-103">Create an IoT hub using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bd624-103">Create an IoT hub using the Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="bd624-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="bd624-104">Introduction</span></span>

<span data-ttu-id="bd624-105">You can use Azure CLI (azure.js) to create and manage Azure IoT hubs programmatically.</span><span class="sxs-lookup"><span data-stu-id="bd624-105">You can use Azure CLI (azure.js) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="bd624-106">This article shows you how to use the Azure CLI (azure.js) to create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bd624-106">This article shows you how to use the Azure CLI (azure.js) to create an IoT hub.</span></span>

<span data-ttu-id="bd624-107">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="bd624-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="bd624-108">Azure CLI (azure.js) – the CLI for the classic and resource management deployment models as described in this article.</span><span class="sxs-lookup"><span data-stu-id="bd624-108">Azure CLI (azure.js) – the CLI for the classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="bd624-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - the next generation CLI for the resource management deployment model.</span><span class="sxs-lookup"><span data-stu-id="bd624-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - the next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="bd624-110">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="bd624-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="bd624-111">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="bd624-111">An active Azure account.</span></span> <span data-ttu-id="bd624-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="bd624-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="bd624-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span><span class="sxs-lookup"><span data-stu-id="bd624-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="bd624-114">If you already have the Azure CLI installed, you can validate the current version at the command prompt with the following command:</span><span class="sxs-lookup"><span data-stu-id="bd624-114">If you already have the Azure CLI installed, you can validate the current version at the command prompt with the following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="bd624-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd624-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bd624-116">The Azure CLI must be in Azure Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="bd624-116">The Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="bd624-117">Set your Azure account and subscription</span><span class="sxs-lookup"><span data-stu-id="bd624-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="bd624-118">At the command prompt, login by typing the following command:</span><span class="sxs-lookup"><span data-stu-id="bd624-118">At the command prompt, login by typing the following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="bd624-119">Use the suggested web browser and code to authenticate.</span><span class="sxs-lookup"><span data-stu-id="bd624-119">Use the suggested web browser and code to authenticate.</span></span>
1. <span data-ttu-id="bd624-120">If you have multiple Azure subscriptions, connecting to Azure grants you access to all the Azure subscriptions associated with your credentials.</span><span class="sxs-lookup"><span data-stu-id="bd624-120">If you have multiple Azure subscriptions, connecting to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="bd624-121">You can view the Azure subscriptions, and identify which one is the default, using the command:</span><span class="sxs-lookup"><span data-stu-id="bd624-121">You can view the Azure subscriptions, and identify which one is the default, using the command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="bd624-122">To set the subscription context under which you want to run the rest of the commands use:</span><span class="sxs-lookup"><span data-stu-id="bd624-122">To set the subscription context under which you want to run the rest of the commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="bd624-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="bd624-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="bd624-124">The article [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] provides more information about how to use the Azure CLI to manage Azure resources.</span><span class="sxs-lookup"><span data-stu-id="bd624-124">The article [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] provides more information about how to use the Azure CLI to manage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="bd624-125">Create an IoT Hub</span><span class="sxs-lookup"><span data-stu-id="bd624-125">Create an IoT Hub</span></span>

<span data-ttu-id="bd624-126">Required parameters:</span><span class="sxs-lookup"><span data-stu-id="bd624-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="bd624-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="bd624-127">**resource-group**.</span></span> <span data-ttu-id="bd624-128">The resource group name.</span><span class="sxs-lookup"><span data-stu-id="bd624-128">The resource group name.</span></span> <span data-ttu-id="bd624-129">The format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span><span class="sxs-lookup"><span data-stu-id="bd624-129">The format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="bd624-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="bd624-130">**name**.</span></span> <span data-ttu-id="bd624-131">The name of the IoT hub to be created.</span><span class="sxs-lookup"><span data-stu-id="bd624-131">The name of the IoT hub to be created.</span></span> <span data-ttu-id="bd624-132">The format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span><span class="sxs-lookup"><span data-stu-id="bd624-132">The format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="bd624-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="bd624-133">**location**.</span></span> <span data-ttu-id="bd624-134">The location (azure region/datacenter) to provision the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="bd624-134">The location (azure region/datacenter) to provision the IoT hub.</span></span>
* <span data-ttu-id="bd624-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="bd624-135">**sku-name**.</span></span> <span data-ttu-id="bd624-136">The name of the sku, one of: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="bd624-136">The name of the sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="bd624-137">For the latest full list, refer to the pricing page for IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="bd624-137">For the latest full list, refer to the pricing page for IoT Hub.</span></span>
* <span data-ttu-id="bd624-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="bd624-138">**units**.</span></span> <span data-ttu-id="bd624-139">The number of provisioned units.</span><span class="sxs-lookup"><span data-stu-id="bd624-139">The number of provisioned units.</span></span> <span data-ttu-id="bd624-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span><span class="sxs-lookup"><span data-stu-id="bd624-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="bd624-141">IoT Hub units are based on your total message count and the number of devices you want to connect.</span><span class="sxs-lookup"><span data-stu-id="bd624-141">IoT Hub units are based on your total message count and the number of devices you want to connect.</span></span>

<span data-ttu-id="bd624-142">To see all the parameters available for creation, you can use the help command in command prompt:</span><span class="sxs-lookup"><span data-stu-id="bd624-142">To see all the parameters available for creation, you can use the help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="bd624-143">Quick example: To create an IoT Hub called **exampleIoTHubName** in the resource group **exampleResourceGroup**, run the following command:</span><span class="sxs-lookup"><span data-stu-id="bd624-143">Quick example: To create an IoT Hub called **exampleIoTHubName** in the resource group **exampleResourceGroup**, run the following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="bd624-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span><span class="sxs-lookup"><span data-stu-id="bd624-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="bd624-145">You can delete the IoT hub **exampleIoTHubName** using following command:</span><span class="sxs-lookup"><span data-stu-id="bd624-145">You can delete the IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="bd624-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="bd624-146">Next steps</span></span>

<span data-ttu-id="bd624-147">To learn more about developing for IoT Hub, see the following article:</span><span class="sxs-lookup"><span data-stu-id="bd624-147">To learn more about developing for IoT Hub, see the following article:</span></span>

* <span data-ttu-id="bd624-148">[IoT SDKs][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="bd624-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="bd624-149">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="bd624-149">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="bd624-150">[Using the Azure portal to manage IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="bd624-150">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://msdn.microsoft.com/library/mt589014.aspx
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
