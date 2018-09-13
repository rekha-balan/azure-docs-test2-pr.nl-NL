---
title: Create an Azure IoT Hub using a template (PowerShell) | Microsoft Docs
description: How to use an Azure Resource Manager template to create an IoT Hub with PowerShell.
services: iot-hub
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: dobett
ms.openlocfilehash: f8ea428b7cab4b106ecc9bbf461c852dfe11dffe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550487"
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="c6145-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c6145-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>
[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="c6145-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="c6145-104">Introduction</span></span>
<span data-ttu-id="c6145-105">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span><span class="sxs-lookup"><span data-stu-id="c6145-105">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="c6145-106">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6145-106">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="c6145-107">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c6145-107">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c6145-108">This article covers using the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="c6145-108">This article covers using the Azure Resource Manager deployment model.</span></span>
> 
> 

<span data-ttu-id="c6145-109">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="c6145-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="c6145-110">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="c6145-110">An active Azure account.</span></span> <br/><span data-ttu-id="c6145-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="c6145-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="c6145-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span><span class="sxs-lookup"><span data-stu-id="c6145-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="c6145-113">The article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how to use PowerShell scripts and Azure Resource Manager templates to create Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c6145-113">The article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how to use PowerShell scripts and Azure Resource Manager templates to create Azure resources.</span></span> 
> 
> 

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="c6145-114">Connect to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="c6145-114">Connect to your Azure subscription</span></span>
<span data-ttu-id="c6145-115">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="c6145-115">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="c6145-116">You can use the following commands to discover where you can deploy an IoT hub and the currently supported API versions:</span><span class="sxs-lookup"><span data-stu-id="c6145-116">You can use the following commands to discover where you can deploy an IoT hub and the currently supported API versions:</span></span>

```
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="c6145-117">Create a resource group to contain your IoT hub using the following command in one of the supported locations for IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c6145-117">Create a resource group to contain your IoT hub using the following command in one of the supported locations for IoT Hub.</span></span> <span data-ttu-id="c6145-118">This example creates a resource group called **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="c6145-118">This example creates a resource group called **MyIoTRG1**:</span></span>

```
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-an-azure-resource-manager-template-to-create-an-iot-hub"></a><span data-ttu-id="c6145-119">Submit an Azure Resource Manager template to create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="c6145-119">Submit an Azure Resource Manager template to create an IoT hub</span></span>
<span data-ttu-id="c6145-120">Use a JSON template to create an IoT hub in your resource group.</span><span class="sxs-lookup"><span data-stu-id="c6145-120">Use a JSON template to create an IoT hub in your resource group.</span></span> <span data-ttu-id="c6145-121">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c6145-121">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="c6145-122">Use a text editor to create an Azure Resource Manager template called **template.json** with the following resource definition to create a new standard IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c6145-122">Use a text editor to create an Azure Resource Manager template called **template.json** with the following resource definition to create a new standard IoT hub.</span></span> <span data-ttu-id="c6145-123">This example adds the IoT Hub in the **East US** region, creates two consumer groups (**cg1** and **cg2**) on the Event Hub-compatible endpoint, and uses the **2016-02-03** API version.</span><span class="sxs-lookup"><span data-stu-id="c6145-123">This example adds the IoT Hub in the **East US** region, creates two consumer groups (**cg1** and **cg2**) on the Event Hub-compatible endpoint, and uses the **2016-02-03** API version.</span></span> <span data-ttu-id="c6145-124">This template also expects you to pass in the IoT hub name as a parameter called **hubName**.</span><span class="sxs-lookup"><span data-stu-id="c6145-124">This template also expects you to pass in the IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="c6145-125">For the current list of locations that support IoT Hub see [Azure Status][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="c6145-125">For the current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>
   
    ```
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```
2. <span data-ttu-id="c6145-126">Save the Azure Resource Manager template file on your local machine.</span><span class="sxs-lookup"><span data-stu-id="c6145-126">Save the Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="c6145-127">This example assumes you save it in a folder called **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="c6145-127">This example assumes you save it in a folder called **c:\templates**.</span></span>
3. <span data-ttu-id="c6145-128">Run the following command to deploy your new IoT hub, passing the name of your IoT hub as a parameter.</span><span class="sxs-lookup"><span data-stu-id="c6145-128">Run the following command to deploy your new IoT hub, passing the name of your IoT hub as a parameter.</span></span> <span data-ttu-id="c6145-129">In this example, the name of the IoT hub is **abcmyiothub** (note that this name must be globally unique so it should include your name or initials):</span><span class="sxs-lookup"><span data-stu-id="c6145-129">In this example, the name of the IoT hub is **abcmyiothub** (note that this name must be globally unique so it should include your name or initials):</span></span>
   
    ```
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
4. <span data-ttu-id="c6145-130">The output displays the keys for the IoT hub you created.</span><span class="sxs-lookup"><span data-stu-id="c6145-130">The output displays the keys for the IoT hub you created.</span></span>
5. <span data-ttu-id="c6145-131">You can verify that your application added the new IoT hub by visiting the [Azure portal][lnk-azure-portal] and viewing your list of resources, or by using the **Get-AzureRmResource** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c6145-131">You can verify that your application added the new IoT hub by visiting the [Azure portal][lnk-azure-portal] and viewing your list of resources, or by using the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="c6145-132">This example application adds an S1 Standard IoT Hub for which you are billed.</span><span class="sxs-lookup"><span data-stu-id="c6145-132">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="c6145-133">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span><span class="sxs-lookup"><span data-stu-id="c6145-133">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c6145-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="c6145-134">Next steps</span></span>
<span data-ttu-id="c6145-135">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want to explore further:</span><span class="sxs-lookup"><span data-stu-id="c6145-135">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want to explore further:</span></span>

* <span data-ttu-id="c6145-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="c6145-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="c6145-137">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6145-137">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="c6145-138">To learn more about developing for IoT Hub, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="c6145-138">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="c6145-139">[Introduction to C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="c6145-139">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="c6145-140">[Azure IoT SDKs][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="c6145-140">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="c6145-141">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="c6145-141">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c6145-142">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="c6145-142">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azureps-cmdlets-docs
[lnk-rest-api]: https://msdn.microsoft.com/library/mt589014.aspx
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
