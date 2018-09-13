---
title: Develop templates for Azure Stack | Microsoft Docs
description: Learn Azure Stack template best practices
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: jeffgo
ms.openlocfilehash: d09dec2f327d8b5911a4e55832ba106838c7ebc3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855881"
---
# <a name="azure-resource-manager-template-considerations"></a><span data-ttu-id="e5346-103">Azure Resource Manager template considerations</span><span class="sxs-lookup"><span data-stu-id="e5346-103">Azure Resource Manager template considerations</span></span>

<span data-ttu-id="e5346-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="e5346-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="e5346-105">As you develop your application, it is important to ensure template portability between Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5346-105">As you develop your application, it is important to ensure template portability between Azure and Azure Stack.</span></span> <span data-ttu-id="e5346-106">This article provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access to an Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="e5346-106">This article provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access to an Azure Stack environment.</span></span>

## <a name="resource-provider-availability"></a><span data-ttu-id="e5346-107">Resource provider availability</span><span class="sxs-lookup"><span data-stu-id="e5346-107">Resource provider availability</span></span>

<span data-ttu-id="e5346-108">The template that you're planning to deploy must only use Microsoft Azure services that are already available or in preview in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5346-108">The template that you're planning to deploy must only use Microsoft Azure services that are already available or in preview in Azure Stack.</span></span>

## <a name="public-namespaces"></a><span data-ttu-id="e5346-109">Public namespaces</span><span class="sxs-lookup"><span data-stu-id="e5346-109">Public namespaces</span></span>

<span data-ttu-id="e5346-110">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than the Azure public cloud.</span><span class="sxs-lookup"><span data-stu-id="e5346-110">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than the Azure public cloud.</span></span> <span data-ttu-id="e5346-111">As a result, hardcoded public endpoints in Azure Resource Manager templates fail when you try to deploy them to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5346-111">As a result, hardcoded public endpoints in Azure Resource Manager templates fail when you try to deploy them to Azure Stack.</span></span> <span data-ttu-id="e5346-112">You can dynamically build service endpoints using the *reference* and *concatenate* functions to retrieve values from the resource provider during deployment.</span><span class="sxs-lookup"><span data-stu-id="e5346-112">You can dynamically build service endpoints using the *reference* and *concatenate* functions to retrieve values from the resource provider during deployment.</span></span> <span data-ttu-id="e5346-113">For example, instead of hardcoding *blob.core.windows.net* in your template, retrieve the [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) to dynamically set the *osDisk.URI* endpoint:</span><span class="sxs-lookup"><span data-stu-id="e5346-113">For example, instead of hardcoding *blob.core.windows.net* in your template, retrieve the [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) to dynamically set the *osDisk.URI* endpoint:</span></span>

     "osDisk": {"name": "osdisk","vhd": {"uri":
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a><span data-ttu-id="e5346-114">API versioning</span><span class="sxs-lookup"><span data-stu-id="e5346-114">API versioning</span></span>

<span data-ttu-id="e5346-115">Azure service versions may differ between Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5346-115">Azure service versions may differ between Azure and Azure Stack.</span></span> <span data-ttu-id="e5346-116">Each resource requires the **apiVersion** attribute, which defines the capabilities offered.</span><span class="sxs-lookup"><span data-stu-id="e5346-116">Each resource requires the **apiVersion** attribute, which defines the capabilities offered.</span></span> <span data-ttu-id="e5346-117">To ensure API version compatibility in Azure Stack, the following API versions are valid for each Resource Provider:</span><span class="sxs-lookup"><span data-stu-id="e5346-117">To ensure API version compatibility in Azure Stack, the following API versions are valid for each Resource Provider:</span></span>

| <span data-ttu-id="e5346-118">Resource Provider</span><span class="sxs-lookup"><span data-stu-id="e5346-118">Resource Provider</span></span> | <span data-ttu-id="e5346-119">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e5346-119">apiVersion</span></span> |
| --- | --- |
| <span data-ttu-id="e5346-120">Compute</span><span class="sxs-lookup"><span data-stu-id="e5346-120">Compute</span></span> |`'2015-06-15'` |
| <span data-ttu-id="e5346-121">Network</span><span class="sxs-lookup"><span data-stu-id="e5346-121">Network</span></span> |<span data-ttu-id="e5346-122">`'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="e5346-122">`'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="e5346-123">Storage</span><span class="sxs-lookup"><span data-stu-id="e5346-123">Storage</span></span> |<span data-ttu-id="e5346-124">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="e5346-124">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="e5346-125">KeyVault</span><span class="sxs-lookup"><span data-stu-id="e5346-125">KeyVault</span></span> | `'2015-06-01'` |
| <span data-ttu-id="e5346-126">App Service</span><span class="sxs-lookup"><span data-stu-id="e5346-126">App Service</span></span> |`'2015-08-01'` |

## <a name="template-functions"></a><span data-ttu-id="e5346-127">Template functions</span><span class="sxs-lookup"><span data-stu-id="e5346-127">Template functions</span></span>

<span data-ttu-id="e5346-128">Azure Resource Manager [functions](../../azure-resource-manager/resource-group-template-functions.md) provide capabilities required to build dynamic templates.</span><span class="sxs-lookup"><span data-stu-id="e5346-128">Azure Resource Manager [functions](../../azure-resource-manager/resource-group-template-functions.md) provide capabilities required to build dynamic templates.</span></span> <span data-ttu-id="e5346-129">As an example, you can use functions for tasks like:</span><span class="sxs-lookup"><span data-stu-id="e5346-129">As an example, you can use functions for tasks like:</span></span>

* <span data-ttu-id="e5346-130">Concatenating or trimming strings.</span><span class="sxs-lookup"><span data-stu-id="e5346-130">Concatenating or trimming strings.</span></span>
* <span data-ttu-id="e5346-131">Referencing values from other resources.</span><span class="sxs-lookup"><span data-stu-id="e5346-131">Referencing values from other resources.</span></span>
* <span data-ttu-id="e5346-132">Iterating on resources to deploy multiple instances.</span><span class="sxs-lookup"><span data-stu-id="e5346-132">Iterating on resources to deploy multiple instances.</span></span>

<span data-ttu-id="e5346-133">These functions are not available in Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="e5346-133">These functions are not available in Azure Stack:</span></span>

* <span data-ttu-id="e5346-134">Skip</span><span class="sxs-lookup"><span data-stu-id="e5346-134">Skip</span></span>
* <span data-ttu-id="e5346-135">Take</span><span class="sxs-lookup"><span data-stu-id="e5346-135">Take</span></span>

## <a name="resource-location"></a><span data-ttu-id="e5346-136">Resource location</span><span class="sxs-lookup"><span data-stu-id="e5346-136">Resource location</span></span>

<span data-ttu-id="e5346-137">Azure Resource Manager templates use a location attribute to place resources during deployment.</span><span class="sxs-lookup"><span data-stu-id="e5346-137">Azure Resource Manager templates use a location attribute to place resources during deployment.</span></span> <span data-ttu-id="e5346-138">In Azure, locations refer to a region like West US or South America.</span><span class="sxs-lookup"><span data-stu-id="e5346-138">In Azure, locations refer to a region like West US or South America.</span></span> <span data-ttu-id="e5346-139">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span><span class="sxs-lookup"><span data-stu-id="e5346-139">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span></span> <span data-ttu-id="e5346-140">To ensure templates are transferrable between Azure and Azure Stack, you should reference the resource group location as you deploy individual resources.</span><span class="sxs-lookup"><span data-stu-id="e5346-140">To ensure templates are transferrable between Azure and Azure Stack, you should reference the resource group location as you deploy individual resources.</span></span> <span data-ttu-id="e5346-141">You can do this using `[resourceGroup().Location]` to ensure all resources inherit the resource group location.</span><span class="sxs-lookup"><span data-stu-id="e5346-141">You can do this using `[resourceGroup().Location]` to ensure all resources inherit the resource group location.</span></span> <span data-ttu-id="e5346-142">The following excerpt is an example of using this function while deploying a storage account:</span><span class="sxs-lookup"><span data-stu-id="e5346-142">The following excerpt is an example of using this function while deploying a storage account:</span></span>

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used to store the VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]

## <a name="next-steps"></a><span data-ttu-id="e5346-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5346-143">Next steps</span></span>

* [<span data-ttu-id="e5346-144">Deploy templates with PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5346-144">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
* [<span data-ttu-id="e5346-145">Deploy templates with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e5346-145">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="e5346-146">Deploy templates with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e5346-146">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)
