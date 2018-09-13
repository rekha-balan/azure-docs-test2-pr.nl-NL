---
title: Export Resource Manager template with Azure PowerShell | Microsoft Docs
description: Use Azure Resource Manager and Azure PowerShell to export a template from a resource group.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/23/2018
ms.author: tomfitz
ms.openlocfilehash: c69bab9d2956568473dd6def86ecbd9bbb6577cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868099"
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="43192-103">Export Azure Resource Manager templates with PowerShell</span><span class="sxs-lookup"><span data-stu-id="43192-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="43192-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="43192-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="43192-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span><span class="sxs-lookup"><span data-stu-id="43192-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="43192-106">It's important to note that there are two different ways to export a template:</span><span class="sxs-lookup"><span data-stu-id="43192-106">It's important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="43192-107">You can export the **actual template used for a deployment**.</span><span class="sxs-lookup"><span data-stu-id="43192-107">You can export the **actual template used for a deployment**.</span></span> <span data-ttu-id="43192-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span><span class="sxs-lookup"><span data-stu-id="43192-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="43192-109">This approach is helpful when you need to retrieve a template.</span><span class="sxs-lookup"><span data-stu-id="43192-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="43192-110">You can export a **generated template that represents the current state of the resource group**.</span><span class="sxs-lookup"><span data-stu-id="43192-110">You can export a **generated template that represents the current state of the resource group**.</span></span> <span data-ttu-id="43192-111">The exported template is not based on any template that you used for deployment.</span><span class="sxs-lookup"><span data-stu-id="43192-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="43192-112">Instead, it creates a template that is a "snapshot" or "backup" of the resource group.</span><span class="sxs-lookup"><span data-stu-id="43192-112">Instead, it creates a template that is a "snapshot" or "backup" of the resource group.</span></span> <span data-ttu-id="43192-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span><span class="sxs-lookup"><span data-stu-id="43192-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="43192-114">Use this option to redeploy resources to the same resource group.</span><span class="sxs-lookup"><span data-stu-id="43192-114">Use this option to redeploy resources to the same resource group.</span></span> <span data-ttu-id="43192-115">To use this template for another resource group, you may have to significantly modify it.</span><span class="sxs-lookup"><span data-stu-id="43192-115">To use this template for another resource group, you may have to significantly modify it.</span></span>

<span data-ttu-id="43192-116">This article shows both approaches.</span><span class="sxs-lookup"><span data-stu-id="43192-116">This article shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="43192-117">Deploy a solution</span><span class="sxs-lookup"><span data-stu-id="43192-117">Deploy a solution</span></span>

<span data-ttu-id="43192-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span><span class="sxs-lookup"><span data-stu-id="43192-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="43192-119">If you already have a resource group in your subscription that you want to export, you don't have to deploy this solution.</span><span class="sxs-lookup"><span data-stu-id="43192-119">If you already have a resource group in your subscription that you want to export, you don't have to deploy this solution.</span></span> <span data-ttu-id="43192-120">However, the rest of this article refers to the template for this solution.</span><span class="sxs-lookup"><span data-stu-id="43192-120">However, the rest of this article refers to the template for this solution.</span></span> <span data-ttu-id="43192-121">The example script deploys a storage account.</span><span class="sxs-lookup"><span data-stu-id="43192-121">The example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="43192-122">Save template from deployment history</span><span class="sxs-lookup"><span data-stu-id="43192-122">Save template from deployment history</span></span>

<span data-ttu-id="43192-123">You can retrieve a template from your deployment history by using the [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span><span class="sxs-lookup"><span data-stu-id="43192-123">You can retrieve a template from your deployment history by using the [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="43192-124">The following example saves the template that you previously deploy:</span><span class="sxs-lookup"><span data-stu-id="43192-124">The following example saves the template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="43192-125">It returns the location of the template.</span><span class="sxs-lookup"><span data-stu-id="43192-125">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="43192-126">Open the file, and notice that it's the exact template you used for deployment.</span><span class="sxs-lookup"><span data-stu-id="43192-126">Open the file, and notice that it's the exact template you used for deployment.</span></span> <span data-ttu-id="43192-127">The parameters and variables match the template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="43192-127">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="43192-128">You can redeploy this template.</span><span class="sxs-lookup"><span data-stu-id="43192-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="43192-129">Export resource group as template</span><span class="sxs-lookup"><span data-stu-id="43192-129">Export resource group as template</span></span>

<span data-ttu-id="43192-130">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span><span class="sxs-lookup"><span data-stu-id="43192-130">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="43192-131">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span><span class="sxs-lookup"><span data-stu-id="43192-131">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span> <span data-ttu-id="43192-132">It is intended as a snapshot of the resource group, which you can use to redeploy to the same resource group.</span><span class="sxs-lookup"><span data-stu-id="43192-132">It is intended as a snapshot of the resource group, which you can use to redeploy to the same resource group.</span></span> <span data-ttu-id="43192-133">To use the exported template for other solutions, you must significantly modify it.</span><span class="sxs-lookup"><span data-stu-id="43192-133">To use the exported template for other solutions, you must significantly modify it.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="43192-134">It returns the location of the template.</span><span class="sxs-lookup"><span data-stu-id="43192-134">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="43192-135">Open the file, and notice that it's different than the template in GitHub.</span><span class="sxs-lookup"><span data-stu-id="43192-135">Open the file, and notice that it's different than the template in GitHub.</span></span> <span data-ttu-id="43192-136">It has different parameters and no variables.</span><span class="sxs-lookup"><span data-stu-id="43192-136">It has different parameters and no variables.</span></span> <span data-ttu-id="43192-137">The storage SKU and location are hard-coded to values.</span><span class="sxs-lookup"><span data-stu-id="43192-137">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="43192-138">The following example shows the exported template, but your template has a slightly different parameter name:</span><span class="sxs-lookup"><span data-stu-id="43192-138">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="43192-139">You can redeploy this template, but it requires guessing a unique name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="43192-139">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="43192-140">The name of your parameter is slightly different.</span><span class="sxs-lookup"><span data-stu-id="43192-140">The name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="43192-141">Customize exported template</span><span class="sxs-lookup"><span data-stu-id="43192-141">Customize exported template</span></span>

<span data-ttu-id="43192-142">You can modify this template to make it easier to use and more flexible.</span><span class="sxs-lookup"><span data-stu-id="43192-142">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="43192-143">To allow for more locations, change the location property to use the same location as the resource group:</span><span class="sxs-lookup"><span data-stu-id="43192-143">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="43192-144">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span><span class="sxs-lookup"><span data-stu-id="43192-144">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="43192-145">Add a parameter for a storage name suffix, and a storage SKU:</span><span class="sxs-lookup"><span data-stu-id="43192-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="43192-146">Add a variable that constructs the storage account name with the uniqueString function:</span><span class="sxs-lookup"><span data-stu-id="43192-146">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="43192-147">Set the name of the storage account to the variable:</span><span class="sxs-lookup"><span data-stu-id="43192-147">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="43192-148">Set the SKU to the parameter:</span><span class="sxs-lookup"><span data-stu-id="43192-148">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="43192-149">Your template now looks like:</span><span class="sxs-lookup"><span data-stu-id="43192-149">Your template now looks like:</span></span>

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

<span data-ttu-id="43192-150">Redeploy the modified template.</span><span class="sxs-lookup"><span data-stu-id="43192-150">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43192-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="43192-151">Next steps</span></span>
* <span data-ttu-id="43192-152">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="43192-152">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="43192-153">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="43192-153">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="43192-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="43192-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
