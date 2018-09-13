---
title: Export Resource Manager template with Azure CLI | Microsoft Docs
description: Use Azure Resource Manager and Azure CLI to export a template from a resource group.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/23/2018
ms.author: tomfitz
ms.openlocfilehash: d4a1a687700badc550d37bf74f6a7e1680388897
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857474"
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="a9aea-103">Export Azure Resource Manager templates with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a9aea-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="a9aea-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="a9aea-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="a9aea-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span><span class="sxs-lookup"><span data-stu-id="a9aea-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="a9aea-106">It's important to note that there are two different ways to export a template:</span><span class="sxs-lookup"><span data-stu-id="a9aea-106">It's important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="a9aea-107">You can export the **actual template used for a deployment**.</span><span class="sxs-lookup"><span data-stu-id="a9aea-107">You can export the **actual template used for a deployment**.</span></span> <span data-ttu-id="a9aea-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span><span class="sxs-lookup"><span data-stu-id="a9aea-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="a9aea-109">This approach is helpful when you need to retrieve a template.</span><span class="sxs-lookup"><span data-stu-id="a9aea-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="a9aea-110">You can export a **generated template that represents the current state of the resource group**.</span><span class="sxs-lookup"><span data-stu-id="a9aea-110">You can export a **generated template that represents the current state of the resource group**.</span></span> <span data-ttu-id="a9aea-111">The exported template is not based on any template that you used for deployment.</span><span class="sxs-lookup"><span data-stu-id="a9aea-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="a9aea-112">Instead, it creates a template that is a "snapshot" or "backup" of the resource group.</span><span class="sxs-lookup"><span data-stu-id="a9aea-112">Instead, it creates a template that is a "snapshot" or "backup" of the resource group.</span></span> <span data-ttu-id="a9aea-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span><span class="sxs-lookup"><span data-stu-id="a9aea-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="a9aea-114">Use this option to redeploy resources to the same resource group.</span><span class="sxs-lookup"><span data-stu-id="a9aea-114">Use this option to redeploy resources to the same resource group.</span></span> <span data-ttu-id="a9aea-115">To use this template for another resource group, you may have to significantly modify it.</span><span class="sxs-lookup"><span data-stu-id="a9aea-115">To use this template for another resource group, you may have to significantly modify it.</span></span>

<span data-ttu-id="a9aea-116">This article shows both approaches.</span><span class="sxs-lookup"><span data-stu-id="a9aea-116">This article shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="a9aea-117">Deploy a solution</span><span class="sxs-lookup"><span data-stu-id="a9aea-117">Deploy a solution</span></span>

<span data-ttu-id="a9aea-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span><span class="sxs-lookup"><span data-stu-id="a9aea-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="a9aea-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span><span class="sxs-lookup"><span data-stu-id="a9aea-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="a9aea-120">However, the rest of this article refers to the template for this solution.</span><span class="sxs-lookup"><span data-stu-id="a9aea-120">However, the rest of this article refers to the template for this solution.</span></span> <span data-ttu-id="a9aea-121">The example script deploys a storage account.</span><span class="sxs-lookup"><span data-stu-id="a9aea-121">The example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="a9aea-122">Save template from deployment history</span><span class="sxs-lookup"><span data-stu-id="a9aea-122">Save template from deployment history</span></span>

<span data-ttu-id="a9aea-123">You can retrieve a template from your deployment history by using the [az group deployment export](/cli/azure/group/deployment#az-group-deployment-export) command.</span><span class="sxs-lookup"><span data-stu-id="a9aea-123">You can retrieve a template from your deployment history by using the [az group deployment export](/cli/azure/group/deployment#az-group-deployment-export) command.</span></span> <span data-ttu-id="a9aea-124">The following example saves the template that you previously deploy:</span><span class="sxs-lookup"><span data-stu-id="a9aea-124">The following example saves the template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="a9aea-125">It returns the template.</span><span class="sxs-lookup"><span data-stu-id="a9aea-125">It returns the template.</span></span> <span data-ttu-id="a9aea-126">Copy the JSON, and save as a file.</span><span class="sxs-lookup"><span data-stu-id="a9aea-126">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="a9aea-127">Notice that it's the exact template you used for deployment.</span><span class="sxs-lookup"><span data-stu-id="a9aea-127">Notice that it's the exact template you used for deployment.</span></span> <span data-ttu-id="a9aea-128">The parameters and variables match the template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="a9aea-128">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="a9aea-129">You can redeploy this template.</span><span class="sxs-lookup"><span data-stu-id="a9aea-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="a9aea-130">Export resource group as template</span><span class="sxs-lookup"><span data-stu-id="a9aea-130">Export resource group as template</span></span>

<span data-ttu-id="a9aea-131">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [az group export](/cli/azure/group#az-group-export) command.</span><span class="sxs-lookup"><span data-stu-id="a9aea-131">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [az group export](/cli/azure/group#az-group-export) command.</span></span> <span data-ttu-id="a9aea-132">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span><span class="sxs-lookup"><span data-stu-id="a9aea-132">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span> <span data-ttu-id="a9aea-133">It is intended as a snapshot of the resource group, which you can use to redeploy to the same resource group.</span><span class="sxs-lookup"><span data-stu-id="a9aea-133">It is intended as a snapshot of the resource group, which you can use to redeploy to the same resource group.</span></span> <span data-ttu-id="a9aea-134">To use the exported template for other solutions, you must significantly modify it.</span><span class="sxs-lookup"><span data-stu-id="a9aea-134">To use the exported template for other solutions, you must significantly modify it.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="a9aea-135">It returns the template.</span><span class="sxs-lookup"><span data-stu-id="a9aea-135">It returns the template.</span></span> <span data-ttu-id="a9aea-136">Copy the JSON, and save as a file.</span><span class="sxs-lookup"><span data-stu-id="a9aea-136">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="a9aea-137">Notice that it's different than the template in GitHub.</span><span class="sxs-lookup"><span data-stu-id="a9aea-137">Notice that it's different than the template in GitHub.</span></span> <span data-ttu-id="a9aea-138">The template has different parameters and no variables.</span><span class="sxs-lookup"><span data-stu-id="a9aea-138">The template has different parameters and no variables.</span></span> <span data-ttu-id="a9aea-139">The storage SKU and location are hard-coded to values.</span><span class="sxs-lookup"><span data-stu-id="a9aea-139">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="a9aea-140">The following example shows the exported template, but your template has a slightly different parameter name:</span><span class="sxs-lookup"><span data-stu-id="a9aea-140">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="a9aea-141">You can redeploy this template, but it requires guessing a unique name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="a9aea-141">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="a9aea-142">The name of your parameter is slightly different.</span><span class="sxs-lookup"><span data-stu-id="a9aea-142">The name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="a9aea-143">Customize exported template</span><span class="sxs-lookup"><span data-stu-id="a9aea-143">Customize exported template</span></span>

<span data-ttu-id="a9aea-144">You can modify this template to make it easier to use and more flexible.</span><span class="sxs-lookup"><span data-stu-id="a9aea-144">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="a9aea-145">To allow for more locations, change the location property to use the same location as the resource group:</span><span class="sxs-lookup"><span data-stu-id="a9aea-145">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="a9aea-146">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span><span class="sxs-lookup"><span data-stu-id="a9aea-146">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="a9aea-147">Add a parameter for a storage name suffix, and a storage SKU:</span><span class="sxs-lookup"><span data-stu-id="a9aea-147">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="a9aea-148">Add a variable that constructs the storage account name with the uniqueString function:</span><span class="sxs-lookup"><span data-stu-id="a9aea-148">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="a9aea-149">Set the name of the storage account to the variable:</span><span class="sxs-lookup"><span data-stu-id="a9aea-149">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="a9aea-150">Set the SKU to the parameter:</span><span class="sxs-lookup"><span data-stu-id="a9aea-150">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="a9aea-151">Your template now looks like:</span><span class="sxs-lookup"><span data-stu-id="a9aea-151">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="a9aea-152">Redeploy the modified template.</span><span class="sxs-lookup"><span data-stu-id="a9aea-152">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9aea-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9aea-153">Next steps</span></span>
* <span data-ttu-id="a9aea-154">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="a9aea-154">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="a9aea-155">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="a9aea-155">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="a9aea-156">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="a9aea-156">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>