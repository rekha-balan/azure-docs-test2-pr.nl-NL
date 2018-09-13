---
title: Create resource group in Azure Resource Manager template | Microsoft Docs
description: Describes how to create a new resource group in an Azure Resource Manager template.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2018
ms.author: tomfitz
ms.openlocfilehash: 003f5d114a233738783d265a18ee7d2ccbfaba10
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871331"
---
# <a name="create-resource-groups-in-azure-resource-manager-templates"></a><span data-ttu-id="52ad6-103">Create resource groups in Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="52ad6-103">Create resource groups in Azure Resource Manager templates</span></span>

<span data-ttu-id="52ad6-104">To create a resource group in an Azure Resource Manager template, define a **Microsoft.Resources/resourceGroups** resource with a name and location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="52ad6-104">To create a resource group in an Azure Resource Manager template, define a **Microsoft.Resources/resourceGroups** resource with a name and location for the resource group.</span></span> <span data-ttu-id="52ad6-105">Deploy the template to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="52ad6-105">Deploy the template to your Azure subscription.</span></span> <span data-ttu-id="52ad6-106">For more information about subscription level deployments, see [Deploy resources to an Azure subscription](deploy-to-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="52ad6-106">For more information about subscription level deployments, see [Deploy resources to an Azure subscription](deploy-to-subscription.md).</span></span>

<span data-ttu-id="52ad6-107">You can also deploy resources to that resource group in the same template.</span><span class="sxs-lookup"><span data-stu-id="52ad6-107">You can also deploy resources to that resource group in the same template.</span></span>

<span data-ttu-id="52ad6-108">This article uses Azure CLI and PowerShell to deploy the templates.</span><span class="sxs-lookup"><span data-stu-id="52ad6-108">This article uses Azure CLI and PowerShell to deploy the templates.</span></span>

## <a name="create-empty-resource-group"></a><span data-ttu-id="52ad6-109">Create empty resource group</span><span class="sxs-lookup"><span data-stu-id="52ad6-109">Create empty resource group</span></span>

<span data-ttu-id="52ad6-110">The following example creates an empty resource group.</span><span class="sxs-lookup"><span data-stu-id="52ad6-110">The following example creates an empty resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.1",
    "parameters": {
        "rgName": {
            "type": "string"
        },
        "rgLocation": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Resources/resourceGroups",
            "apiVersion": "2018-05-01",
            "location": "[parameters('rgLocation')]",
            "name": "[parameters('rgName')]",
            "properties": {}
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="52ad6-111">To deploy this template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="52ad6-111">To deploy this template with Azure CLI, use:</span></span>

```azurecli-interactive
az deployment create \
  -n demoEmptyRG \
  -l southcentralus \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/emptyRG.json \
  --parameters rgName=demoRG rgLocation=northcentralus
```

<span data-ttu-id="52ad6-112">To deploy this template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="52ad6-112">To deploy this template with PowerShell, use:</span></span>

```azurepowershell-interactive
New-AzureRmDeployment `
  -Name demoEmptyRG `
  -Location southcentralus `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/emptyRG.json `
  -rgName demogroup `
  -rgLocation northcentralus
```

## <a name="create-several-resource-groups"></a><span data-ttu-id="52ad6-113">Create several resource groups</span><span class="sxs-lookup"><span data-stu-id="52ad6-113">Create several resource groups</span></span>

<span data-ttu-id="52ad6-114">Use the [copy element](resource-group-create-multiple.md) with resource groups to create more than one resource group.</span><span class="sxs-lookup"><span data-stu-id="52ad6-114">Use the [copy element](resource-group-create-multiple.md) with resource groups to create more than one resource group.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.1",
    "parameters": {
        "rgNamePrefix": {
            "type": "string"
        },
        "rgLocation": {
            "type": "string"
        },
        "instanceCount": {
            "type": "int"
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Resources/resourceGroups",
            "apiVersion": "2018-05-01",
            "location": "[parameters('rgLocation')]",
            "name": "[concat(parameters('rgNamePrefix'), copyIndex())]",
            "copy": {
                "name": "rgCopy",
                "count": "[parameters('instanceCount')]"
            },
            "properties": {}
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="52ad6-115">To deploy this template with Azure CLI and create three resource groups, use:</span><span class="sxs-lookup"><span data-stu-id="52ad6-115">To deploy this template with Azure CLI and create three resource groups, use:</span></span>

```azurecli-interactive
az deployment create \
  -n demoCopyRG \
  -l southcentralus \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/copyRG.json \
  --parameters rgNamePrefix=demoRG rgLocation=northcentralus instanceCount=3
```

<span data-ttu-id="52ad6-116">To deploy this template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="52ad6-116">To deploy this template with PowerShell, use:</span></span>

```azurepowershell-interactive
New-AzureRmDeployment `
  -Name demoCopyRG `
  -Location southcentralus `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/copyRG.json `
  -rgName demogroup `
  -rgLocation northcentralus `
  -instanceCount 3
```

## <a name="create-resource-group-and-deploy-resource"></a><span data-ttu-id="52ad6-117">Create resource group and deploy resource</span><span class="sxs-lookup"><span data-stu-id="52ad6-117">Create resource group and deploy resource</span></span>

<span data-ttu-id="52ad6-118">To create the resource group and deploy resources to it, use a nested template.</span><span class="sxs-lookup"><span data-stu-id="52ad6-118">To create the resource group and deploy resources to it, use a nested template.</span></span> <span data-ttu-id="52ad6-119">The nested template defines the resources to deploy to the resource group.</span><span class="sxs-lookup"><span data-stu-id="52ad6-119">The nested template defines the resources to deploy to the resource group.</span></span> <span data-ttu-id="52ad6-120">Set the nested template as dependent on the resource group to make sure the resource group exists before deploying the resources.</span><span class="sxs-lookup"><span data-stu-id="52ad6-120">Set the nested template as dependent on the resource group to make sure the resource group exists before deploying the resources.</span></span>

<span data-ttu-id="52ad6-121">The following example creates a resource group, and deploys a storage account to the resource group.</span><span class="sxs-lookup"><span data-stu-id="52ad6-121">The following example creates a resource group, and deploys a storage account to the resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.1",
    "parameters": {
        "rgName": {
            "type": "string"
        },
        "rgLocation": {
            "type": "string"
        },
        "storagePrefix": {
            "type": "string",
            "maxLength": 11
        }
    },
    "variables": {
        "storageName": "[concat(parameters('storagePrefix'), uniqueString(subscription().id, parameters('rgName')))]"
    },
    "resources": [
        {
            "type": "Microsoft.Resources/resourceGroups",
            "apiVersion": "2018-05-01",
            "location": "[parameters('rgLocation')]",
            "name": "[parameters('rgName')]",
            "properties": {}
        },
        {
            "type": "Microsoft.Resources/deployments",
            "apiVersion": "2017-05-10",
            "name": "storageDeployment",
            "resourceGroup": "[parameters('rgName')]",
            "dependsOn": [
                "[resourceId('Microsoft.Resources/resourceGroups/', parameters('rgName'))]"
            ],
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "apiVersion": "2017-10-01",
                            "name": "[variables('storageName')]",
                            "location": "[parameters('rgLocation')]",
                            "kind": "StorageV2",
                            "sku": {
                                "name": "Standard_LRS"
                            }
                        }
                    ],
                    "outputs": {}
                }
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="52ad6-122">To deploy this template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="52ad6-122">To deploy this template with Azure CLI, use:</span></span>

```azurecli-interactive
az deployment create \
  -n demoRGStorage \
  -l southcentralus \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/newRGWithStorage.json \
  --parameters rgName=rgStorage rgLocation=northcentralus storagePrefix=storage
```

<span data-ttu-id="52ad6-123">To deploy this template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="52ad6-123">To deploy this template with PowerShell, use:</span></span>

```azurepowershell-interactive
New-AzureRmDeployment `
  -Name demoRGStorage `
  -Location southcentralus `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/newRGWithStorage.json `
  -rgName rgStorage `
  -rgLocation northcentralus `
  -storagePrefix storage
```

## <a name="next-steps"></a><span data-ttu-id="52ad6-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="52ad6-124">Next steps</span></span>
* <span data-ttu-id="52ad6-125">To learn about subscription level deployments, see [Deploy resources to an Azure subscription](deploy-to-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="52ad6-125">To learn about subscription level deployments, see [Deploy resources to an Azure subscription](deploy-to-subscription.md).</span></span>
* <span data-ttu-id="52ad6-126">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="52ad6-126">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="52ad6-127">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="52ad6-127">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="52ad6-128">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="52ad6-128">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

