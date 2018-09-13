---
title: Create an Azure IoT Hub using a PowerShell cmdlet | Microsoft Docs
description: How to use a PowerShell cmdlet to create an IoT hub.
services: iot-hub
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: dobett
ms.openlocfilehash: 7a2f3761a1d9af7b364eae4e752477c4349814a4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555302"
---
# <a name="create-an-iot-hub-using-the-new-azurermiothub-cmdlet"></a><span data-ttu-id="4d681-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span><span class="sxs-lookup"><span data-stu-id="4d681-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="4d681-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="4d681-104">Introduction</span></span>

<span data-ttu-id="4d681-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="4d681-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span></span> <span data-ttu-id="4d681-106">This tutorial shows you how to create an IoT hub with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d681-106">This tutorial shows you how to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="4d681-107">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4d681-107">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="4d681-108">This article covers using the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="4d681-108">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="4d681-109">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="4d681-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="4d681-110">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="4d681-110">An active Azure account.</span></span> <br/><span data-ttu-id="4d681-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="4d681-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="4d681-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span><span class="sxs-lookup"><span data-stu-id="4d681-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>
* <span data-ttu-id="4d681-113">[Azure Resource Manager cmdlets][lnk-rm-install].</span><span class="sxs-lookup"><span data-stu-id="4d681-113">[Azure Resource Manager cmdlets][lnk-rm-install].</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="4d681-114">Connect to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="4d681-114">Connect to your Azure subscription</span></span>
<span data-ttu-id="4d681-115">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="4d681-115">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="4d681-116">Create resource group</span><span class="sxs-lookup"><span data-stu-id="4d681-116">Create resource group</span></span>

<span data-ttu-id="4d681-117">You need a resource group to deploy an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4d681-117">You need a resource group to deploy an IoT hub.</span></span> <span data-ttu-id="4d681-118">You can use an existing resource group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="4d681-118">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="4d681-119">You can use the following command to discover the locations where you can deploy an IoT hub:</span><span class="sxs-lookup"><span data-stu-id="4d681-119">You can use the following command to discover the locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="4d681-120">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span><span class="sxs-lookup"><span data-stu-id="4d681-120">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span></span> <span data-ttu-id="4d681-121">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span><span class="sxs-lookup"><span data-stu-id="4d681-121">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="4d681-122">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="4d681-122">Create an IoT hub</span></span>

<span data-ttu-id="4d681-123">To create an IoT hub in the resource group you created in the previous step, use the following command.</span><span class="sxs-lookup"><span data-stu-id="4d681-123">To create an IoT hub in the resource group you created in the previous step, use the following command.</span></span> <span data-ttu-id="4d681-124">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span><span class="sxs-lookup"><span data-stu-id="4d681-124">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

> [!NOTE]
> <span data-ttu-id="4d681-125">The name of the IoT hub must be unique.</span><span class="sxs-lookup"><span data-stu-id="4d681-125">The name of the IoT hub must be unique.</span></span>

<span data-ttu-id="4d681-126">You can list all the IoT hubs in your subscription using the following command:</span><span class="sxs-lookup"><span data-stu-id="4d681-126">You can list all the IoT hubs in your subscription using the following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="4d681-127">The previous example adds an S1 Standard IoT Hub for which you are billed.</span><span class="sxs-lookup"><span data-stu-id="4d681-127">The previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="4d681-128">You can delete the IoT hub using the following command:</span><span class="sxs-lookup"><span data-stu-id="4d681-128">You can delete the IoT hub using the following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="4d681-129">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span><span class="sxs-lookup"><span data-stu-id="4d681-129">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="4d681-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d681-130">Next steps</span></span>

<span data-ttu-id="4d681-131">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span><span class="sxs-lookup"><span data-stu-id="4d681-131">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span></span>

* <span data-ttu-id="4d681-132">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="4d681-132">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="4d681-133">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="4d681-133">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="4d681-134">To learn more about developing for IoT Hub, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="4d681-134">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="4d681-135">[Introduction to C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="4d681-135">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="4d681-136">[Azure IoT SDKs][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="4d681-136">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="4d681-137">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="4d681-137">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4d681-138">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="4d681-138">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: /powershell/azureps-cmdlets-docs
[lnk-iothub-cmdlets]: /powershell/resourcemanager/azurerm.iothub/v1.3.0/azurerm.iothub
[lnk-rm-install]: /powershell/resourcemanager/
[lnk-rest-api]: https://msdn.microsoft.com/library/mt589014.aspx

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
