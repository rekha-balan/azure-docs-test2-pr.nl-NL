---
title: Provision a Redis Cache using Azure Resource Manager | Microsoft Docs
description: Use Azure Resource Manager template to deploy an Azure Redis Cache.
services: app-service
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 8d0586bdb88ccd458cf9d0675f42fb2494dde802
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549113"
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="11206-103">Create a Redis Cache using a template</span><span class="sxs-lookup"><span data-stu-id="11206-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="11206-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="11206-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="11206-105">The cache can be used with an existing storage account to keep diagnostic data.</span><span class="sxs-lookup"><span data-stu-id="11206-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="11206-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span><span class="sxs-lookup"><span data-stu-id="11206-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="11206-107">You can use this template for your own deployments, or customize it to meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="11206-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="11206-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span><span class="sxs-lookup"><span data-stu-id="11206-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="11206-109">Updating one cache in the region affects all other caches in the region.</span><span class="sxs-lookup"><span data-stu-id="11206-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="11206-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="11206-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="11206-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="11206-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="11206-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span><span class="sxs-lookup"><span data-stu-id="11206-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="11206-113">Create a Premium Redis Cache with clustering</span><span class="sxs-lookup"><span data-stu-id="11206-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="11206-114">Create Premium Redis Cache with data persistence</span><span class="sxs-lookup"><span data-stu-id="11206-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="11206-115">Create Premium Redis Cache with VNet and optional clustering</span><span class="sxs-lookup"><span data-stu-id="11206-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="11206-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="11206-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="11206-117">What you will deploy</span><span class="sxs-lookup"><span data-stu-id="11206-117">What you will deploy</span></span>
<span data-ttu-id="11206-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span><span class="sxs-lookup"><span data-stu-id="11206-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="11206-119">To run the deployment automatically, click the following button:</span><span class="sxs-lookup"><span data-stu-id="11206-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="11206-120">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="11206-120">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="11206-121">Parameters</span><span class="sxs-lookup"><span data-stu-id="11206-121">Parameters</span></span>
<span data-ttu-id="11206-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="11206-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="11206-123">The template includes a section called Parameters that contains all of the parameter values.</span><span class="sxs-lookup"><span data-stu-id="11206-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="11206-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="11206-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="11206-125">Do not define parameters for values that always stay the same.</span><span class="sxs-lookup"><span data-stu-id="11206-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="11206-126">Each parameter value is used in the template to define the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="11206-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="11206-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="11206-127">redisCacheLocation</span></span>
<span data-ttu-id="11206-128">The location of the Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="11206-128">The location of the Redis Cache.</span></span> <span data-ttu-id="11206-129">For best performance, use the same location as the app to be used with the cache.</span><span class="sxs-lookup"><span data-stu-id="11206-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="11206-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="11206-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="11206-131">The name of the existing storage account to use for diagnostics.</span><span class="sxs-lookup"><span data-stu-id="11206-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="11206-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="11206-132">enableNonSslPort</span></span>
<span data-ttu-id="11206-133">A boolean value that indicates whether to allow access via non-SSL ports.</span><span class="sxs-lookup"><span data-stu-id="11206-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="11206-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="11206-134">diagnosticsStatus</span></span>
<span data-ttu-id="11206-135">A value that indicates whether diagnostics is enabled.</span><span class="sxs-lookup"><span data-stu-id="11206-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="11206-136">Use ON or OFF.</span><span class="sxs-lookup"><span data-stu-id="11206-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="11206-137">Resources to deploy</span><span class="sxs-lookup"><span data-stu-id="11206-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="11206-138">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="11206-138">Redis Cache</span></span>
<span data-ttu-id="11206-139">Creates the Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="11206-139">Creates the Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-to-run-deployment"></a><span data-ttu-id="11206-140">Commands to run deployment</span><span class="sxs-lookup"><span data-stu-id="11206-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="11206-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11206-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="11206-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="11206-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup



