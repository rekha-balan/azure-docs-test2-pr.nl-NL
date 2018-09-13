---
title: Develop templates for Azure Stack | Microsoft Docs
description: Learn Azure Stack template best practices
services: azure-stack
documentationcenter: ''
author: HeathL17
manager: byronr
editor: ''
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/4/2016
ms.author: helaw
ms.openlocfilehash: 5530d2d10695f1760ff56e9f171af836f926bead
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556169"
---
# <a name="azure-resource-manager-template-considerations"></a><span data-ttu-id="7f58a-103">Azure Resource Manager template considerations</span><span class="sxs-lookup"><span data-stu-id="7f58a-103">Azure Resource Manager template considerations</span></span>
<span data-ttu-id="7f58a-104">As you develop your application, it is important to ensure template portability between Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7f58a-104">As you develop your application, it is important to ensure template portability between Azure and Azure Stack.</span></span>  <span data-ttu-id="7f58a-105">This topic provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access to an Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="7f58a-105">This topic provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access to an Azure Stack environment.</span></span>

## <a name="public-namespaces"></a><span data-ttu-id="7f58a-106">Public namespaces</span><span class="sxs-lookup"><span data-stu-id="7f58a-106">Public namespaces</span></span>
<span data-ttu-id="7f58a-107">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than the Azure public cloud.</span><span class="sxs-lookup"><span data-stu-id="7f58a-107">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than the Azure public cloud.</span></span> <span data-ttu-id="7f58a-108">As a result, hardcoded public endpoints in Resource Manager templates will fail when you try to deploy them to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7f58a-108">As a result, hardcoded public endpoints in Resource Manager templates will fail when you try to deploy them to Azure Stack.</span></span> <span data-ttu-id="7f58a-109">Instead, you can use the *reference* and *concatenate* function to dynamically build the service endpoint based on values retrieved from the resource provider during deployment.</span><span class="sxs-lookup"><span data-stu-id="7f58a-109">Instead, you can use the *reference* and *concatenate* function to dynamically build the service endpoint based on values retrieved from the resource provider during deployment.</span></span> <span data-ttu-id="7f58a-110">For example, rather than specifying *blob.core.windows.net* in your template, retrieve the [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) to dynamically set the *osDisk.URI* endpoint:</span><span class="sxs-lookup"><span data-stu-id="7f58a-110">For example, rather than specifying *blob.core.windows.net* in your template, retrieve the [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) to dynamically set the *osDisk.URI* endpoint:</span></span>

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a><span data-ttu-id="7f58a-111">API versioning</span><span class="sxs-lookup"><span data-stu-id="7f58a-111">API versioning</span></span>
<span data-ttu-id="7f58a-112">Azure service versions may differ between Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7f58a-112">Azure service versions may differ between Azure and Azure Stack.</span></span> <span data-ttu-id="7f58a-113">Each resource requires the apiVersion attribute, which defines the capabilities offered.</span><span class="sxs-lookup"><span data-stu-id="7f58a-113">Each resource requires the apiVersion attribute, which defines the capabilities offered.</span></span> <span data-ttu-id="7f58a-114">To ensure API version compatibility in Azure Stack TP3, the following are valid API versions for each Resource Provider:</span><span class="sxs-lookup"><span data-stu-id="7f58a-114">To ensure API version compatibility in Azure Stack TP3, the following are valid API versions for each Resource Provider:</span></span>

| <span data-ttu-id="7f58a-115">Resource Provider</span><span class="sxs-lookup"><span data-stu-id="7f58a-115">Resource Provider</span></span> | <span data-ttu-id="7f58a-116">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7f58a-116">apiVersion</span></span> |
| --- | --- |
| <span data-ttu-id="7f58a-117">Compute</span><span class="sxs-lookup"><span data-stu-id="7f58a-117">Compute</span></span> |<span data-ttu-id="7f58a-118">'2015-06-15'</span><span class="sxs-lookup"><span data-stu-id="7f58a-118">'2015-06-15'</span></span> |
| <span data-ttu-id="7f58a-119">Network</span><span class="sxs-lookup"><span data-stu-id="7f58a-119">Network</span></span> |<span data-ttu-id="7f58a-120">'2015-06-15', '2015-05-01-preview'</span><span class="sxs-lookup"><span data-stu-id="7f58a-120">'2015-06-15', '2015-05-01-preview'</span></span> |
| <span data-ttu-id="7f58a-121">Storage</span><span class="sxs-lookup"><span data-stu-id="7f58a-121">Storage</span></span> |<span data-ttu-id="7f58a-122">'2016-01-01', '2015-06-15', '2015-05-01-preview'</span><span class="sxs-lookup"><span data-stu-id="7f58a-122">'2016-01-01', '2015-06-15', '2015-05-01-preview'</span></span> |
| <span data-ttu-id="7f58a-123">KeyVault</span><span class="sxs-lookup"><span data-stu-id="7f58a-123">KeyVault</span></span> | <span data-ttu-id="7f58a-124">'2015-06-01'</span><span class="sxs-lookup"><span data-stu-id="7f58a-124">'2015-06-01'</span></span> |
| <span data-ttu-id="7f58a-125">App Service</span><span class="sxs-lookup"><span data-stu-id="7f58a-125">App Service</span></span> |<span data-ttu-id="7f58a-126">'2015-08-01'</span><span class="sxs-lookup"><span data-stu-id="7f58a-126">'2015-08-01'</span></span> |
| <span data-ttu-id="7f58a-127">MySQL</span><span class="sxs-lookup"><span data-stu-id="7f58a-127">MySQL</span></span> |<span data-ttu-id="7f58a-128">'2015-09-01'</span><span class="sxs-lookup"><span data-stu-id="7f58a-128">'2015-09-01'</span></span> |
| <span data-ttu-id="7f58a-129">SQL</span><span class="sxs-lookup"><span data-stu-id="7f58a-129">SQL</span></span> |<span data-ttu-id="7f58a-130">'2014-04-01-preview'</span><span class="sxs-lookup"><span data-stu-id="7f58a-130">'2014-04-01-preview'</span></span> |

## <a name="template-functions"></a><span data-ttu-id="7f58a-131">Template functions</span><span class="sxs-lookup"><span data-stu-id="7f58a-131">Template functions</span></span>
<span data-ttu-id="7f58a-132">Resource Manager [functions](../azure-resource-manager/resource-group-template-functions.md) provide capabilities required to build dynamic templates.</span><span class="sxs-lookup"><span data-stu-id="7f58a-132">Resource Manager [functions](../azure-resource-manager/resource-group-template-functions.md) provide capabilities required to build dynamic templates.</span></span> <span data-ttu-id="7f58a-133">As an example, you can use functions for tasks like:</span><span class="sxs-lookup"><span data-stu-id="7f58a-133">As an example, you can use functions for tasks like:</span></span>

* <span data-ttu-id="7f58a-134">Concatenating or trimming strings</span><span class="sxs-lookup"><span data-stu-id="7f58a-134">Concatenating or trimming strings</span></span> 
* <span data-ttu-id="7f58a-135">Reference values from other resources</span><span class="sxs-lookup"><span data-stu-id="7f58a-135">Reference values from other resources</span></span>
* <span data-ttu-id="7f58a-136">Iterating on resources to deploy multiple instances</span><span class="sxs-lookup"><span data-stu-id="7f58a-136">Iterating on resources to deploy multiple instances</span></span> 

<span data-ttu-id="7f58a-137">As you build your templates, some functions are not available in Azure Stack TP3, and should not be used.</span><span class="sxs-lookup"><span data-stu-id="7f58a-137">As you build your templates, some functions are not available in Azure Stack TP3, and should not be used.</span></span> <span data-ttu-id="7f58a-138">These functions are:</span><span class="sxs-lookup"><span data-stu-id="7f58a-138">These functions are:</span></span>

* <span data-ttu-id="7f58a-139">Skip</span><span class="sxs-lookup"><span data-stu-id="7f58a-139">Skip</span></span>
* <span data-ttu-id="7f58a-140">Take</span><span class="sxs-lookup"><span data-stu-id="7f58a-140">Take</span></span>

## <a name="resource-location"></a><span data-ttu-id="7f58a-141">Resource location</span><span class="sxs-lookup"><span data-stu-id="7f58a-141">Resource location</span></span>
<span data-ttu-id="7f58a-142">Resource Manager templates use a location attribute to place resources during deployment.</span><span class="sxs-lookup"><span data-stu-id="7f58a-142">Resource Manager templates use a location attribute to place resources during deployment.</span></span> <span data-ttu-id="7f58a-143">In Azure, locations refer to a region like West US or South America.</span><span class="sxs-lookup"><span data-stu-id="7f58a-143">In Azure, locations refer to a region like West US or South America.</span></span> <span data-ttu-id="7f58a-144">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span><span class="sxs-lookup"><span data-stu-id="7f58a-144">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span></span>  <span data-ttu-id="7f58a-145">To ensure templates are transferrable between Azure and Azure Stack, you should reference the resource group location as you deploy individual resources.</span><span class="sxs-lookup"><span data-stu-id="7f58a-145">To ensure templates are transferrable between Azure and Azure Stack, you should reference the resource group location as you deploy individual resources.</span></span> <span data-ttu-id="7f58a-146">You can do this using [resourceGroup().Location](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L54) to ensure resources inherit the resource group location.</span><span class="sxs-lookup"><span data-stu-id="7f58a-146">You can do this using [resourceGroup().Location](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L54) to ensure resources inherit the resource group location.</span></span>  <span data-ttu-id="7f58a-147">The following Resource Manager template excerpt is an example of using this function while deploying a storage account:</span><span class="sxs-lookup"><span data-stu-id="7f58a-147">The following Resource Manager template excerpt is an example of using this function while deploying a storage account:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="7f58a-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f58a-148">Next steps</span></span>
* [<span data-ttu-id="7f58a-149">Deploy templates with PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f58a-149">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
* [<span data-ttu-id="7f58a-150">Deploy templates with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7f58a-150">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="7f58a-151">Deploy templates with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f58a-151">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

