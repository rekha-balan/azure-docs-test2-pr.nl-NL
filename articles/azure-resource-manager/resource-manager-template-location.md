---
title: Azure resource location in template | Microsoft Docs
description: Shows how to set a location for a resource in an Azure Resource Manager template
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: b949318eb689eec9f0d08e91f2a9d0169d9d816f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563681"
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Set resource location in Azure Resource Manager templates
When deploying a template, you must provide a location for each resource. This topic shows how to determine the locations that are available to your subscription for each resource type.

## <a name="determine-supported-locations"></a>Determine supported locations

For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/). However, your subscription might not have access to all the locations in that list. To see a customized list of locations that are available to your subscription, use Azure PowerShell or Azure CLI. 

The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

The following example uses Azure CLI 2.0 to get the locations for the `Microsoft.Web\sites` resource type:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Set location in template

After determining the supported locations for your resources, you need to set that location in your template. The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`. You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters. 

The following example shows a storage account that is deployed to the same location as the resource group:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

If you need to hardcode the location in your template, provide the name of one of the supported regions. The following example shows a storage account that is always deployed to North Central US:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a>Next Steps
* For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).

