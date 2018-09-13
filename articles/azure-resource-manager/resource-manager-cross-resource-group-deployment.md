---
title: Deploy Azure resources to multiple subscription and resource groups | Microsoft Docs
description: Shows how to target more than one Azure subscription and resource group during deployment.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2018
ms.author: tomfitz
ms.openlocfilehash: fec075a744b5f47a4be7f1b960cceedfea7b9a2c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865914"
---
# <a name="deploy-azure-resources-to-more-than-one-subscription-or-resource-group"></a><span data-ttu-id="06c30-103">Deploy Azure resources to more than one subscription or resource group</span><span class="sxs-lookup"><span data-stu-id="06c30-103">Deploy Azure resources to more than one subscription or resource group</span></span>

<span data-ttu-id="06c30-104">Typically, you deploy all the resources in your template to a single [resource group](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="06c30-104">Typically, you deploy all the resources in your template to a single [resource group](resource-group-overview.md).</span></span> <span data-ttu-id="06c30-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups or subscriptions.</span><span class="sxs-lookup"><span data-stu-id="06c30-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups or subscriptions.</span></span> <span data-ttu-id="06c30-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span><span class="sxs-lookup"><span data-stu-id="06c30-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="06c30-107">Resource Manager enables you to use nested templates to target different subscriptions and resource groups than the subscription and resource group used for the parent template.</span><span class="sxs-lookup"><span data-stu-id="06c30-107">Resource Manager enables you to use nested templates to target different subscriptions and resource groups than the subscription and resource group used for the parent template.</span></span>

> [!NOTE]
> <span data-ttu-id="06c30-108">You can deploy to only five resource groups in a single deployment.</span><span class="sxs-lookup"><span data-stu-id="06c30-108">You can deploy to only five resource groups in a single deployment.</span></span> <span data-ttu-id="06c30-109">Typically, this limitation means you can deploy to one resource group specified for the parent template, and up to four resource groups in nested or linked deployments.</span><span class="sxs-lookup"><span data-stu-id="06c30-109">Typically, this limitation means you can deploy to one resource group specified for the parent template, and up to four resource groups in nested or linked deployments.</span></span> <span data-ttu-id="06c30-110">However, if your parent template contains only nested or linked templates and does not itself deploy any resources, then you can include up to five resource groups in nested or linked deployments.</span><span class="sxs-lookup"><span data-stu-id="06c30-110">However, if your parent template contains only nested or linked templates and does not itself deploy any resources, then you can include up to five resource groups in nested or linked deployments.</span></span>

## <a name="specify-a-subscription-and-resource-group"></a><span data-ttu-id="06c30-111">Specify a subscription and resource group</span><span class="sxs-lookup"><span data-stu-id="06c30-111">Specify a subscription and resource group</span></span>

<span data-ttu-id="06c30-112">To target a different resource, use a nested or linked template.</span><span class="sxs-lookup"><span data-stu-id="06c30-112">To target a different resource, use a nested or linked template.</span></span> <span data-ttu-id="06c30-113">The `Microsoft.Resources/deployments` resource type provides parameters for `subscriptionId` and `resourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="06c30-113">The `Microsoft.Resources/deployments` resource type provides parameters for `subscriptionId` and `resourceGroup`.</span></span> <span data-ttu-id="06c30-114">These properties enable you to specify a different subscription and resource group for the nested deployment.</span><span class="sxs-lookup"><span data-stu-id="06c30-114">These properties enable you to specify a different subscription and resource group for the nested deployment.</span></span> <span data-ttu-id="06c30-115">All the resource groups must exist before running the deployment.</span><span class="sxs-lookup"><span data-stu-id="06c30-115">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="06c30-116">If you do not specify either the subscription ID or resource group, the subscription and resource group from the parent template is used.</span><span class="sxs-lookup"><span data-stu-id="06c30-116">If you do not specify either the subscription ID or resource group, the subscription and resource group from the parent template is used.</span></span>

<span data-ttu-id="06c30-117">The account you use to deploy the template must have permissions to deploy to the specified subscription ID.</span><span class="sxs-lookup"><span data-stu-id="06c30-117">The account you use to deploy the template must have permissions to deploy to the specified subscription ID.</span></span> <span data-ttu-id="06c30-118">If the specified subscription exists in a different Azure Active Directory tenant, you must [add guest users from another directory](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md).</span><span class="sxs-lookup"><span data-stu-id="06c30-118">If the specified subscription exists in a different Azure Active Directory tenant, you must [add guest users from another directory](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md).</span></span>

<span data-ttu-id="06c30-119">To specify a different resource group and subscription, use:</span><span class="sxs-lookup"><span data-stu-id="06c30-119">To specify a different resource group and subscription, use:</span></span>

```json
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "resourceGroup": "[parameters('secondResourceGroup')]",
        "subscriptionId": "[parameters('secondSubscriptionID')]",
        ...
    }
]
```

<span data-ttu-id="06c30-120">If your resource groups are in the same subscription, you can remove the **subscriptionId** value.</span><span class="sxs-lookup"><span data-stu-id="06c30-120">If your resource groups are in the same subscription, you can remove the **subscriptionId** value.</span></span>

<span data-ttu-id="06c30-121">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group specified in the `secondResourceGroup` parameter:</span><span class="sxs-lookup"><span data-stu-id="06c30-121">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group specified in the `secondResourceGroup` parameter:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storagePrefix": {
            "type": "string",
            "maxLength": 11
        },
        "secondResourceGroup": {
            "type": "string"
        },
        "secondSubscriptionID": {
            "type": "string",
            "defaultValue": ""
        },
        "secondStorageLocation": {
            "type": "string",
            "defaultValue": "[resourceGroup().location]"
        }
    },
    "variables": {
        "firstStorageName": "[concat(parameters('storagePrefix'), uniqueString(resourceGroup().id))]",
        "secondStorageName": "[concat(parameters('storagePrefix'), uniqueString(parameters('secondSubscriptionID'), parameters('secondResourceGroup')))]"
    },
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "[parameters('secondResourceGroup')]",
            "subscriptionId": "[parameters('secondSubscriptionID')]",
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
                            "name": "[variables('secondStorageName')]",
                            "apiVersion": "2017-06-01",
                            "location": "[parameters('secondStorageLocation')]",
                            "sku":{
                                "name": "Standard_LRS"
                            },
                            "kind": "Storage",
                            "properties": {
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[variables('firstStorageName')]",
            "apiVersion": "2017-06-01",
            "location": "[resourceGroup().location]",
            "sku":{
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {
            }
        }
    ]
}
```

<span data-ttu-id="06c30-122">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span><span class="sxs-lookup"><span data-stu-id="06c30-122">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span>

## <a name="use-the-resourcegroup-and-subscription-functions"></a><span data-ttu-id="06c30-123">Use the resourceGroup() and subscription() functions</span><span class="sxs-lookup"><span data-stu-id="06c30-123">Use the resourceGroup() and subscription() functions</span></span>

<span data-ttu-id="06c30-124">For cross resource group deployments, the [resourceGroup()](resource-group-template-functions-resource.md#resourcegroup) and [subscription()](resource-group-template-functions-resource.md#subscription) functions resolve differently based on how you specify the nested template.</span><span class="sxs-lookup"><span data-stu-id="06c30-124">For cross resource group deployments, the [resourceGroup()](resource-group-template-functions-resource.md#resourcegroup) and [subscription()](resource-group-template-functions-resource.md#subscription) functions resolve differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="06c30-125">If you embed one template within another template, the functions in the nested template resolve to the parent resource group and subscription.</span><span class="sxs-lookup"><span data-stu-id="06c30-125">If you embed one template within another template, the functions in the nested template resolve to the parent resource group and subscription.</span></span> <span data-ttu-id="06c30-126">An embedded template uses the following format:</span><span class="sxs-lookup"><span data-stu-id="06c30-126">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() and subscription() refer to parent resource group/subscription
    }
}
```

<span data-ttu-id="06c30-127">If you link to a separate template, the functions in the linked template resolve to the nested resource group and subscription.</span><span class="sxs-lookup"><span data-stu-id="06c30-127">If you link to a separate template, the functions in the linked template resolve to the nested resource group and subscription.</span></span> <span data-ttu-id="06c30-128">A linked template uses the following format:</span><span class="sxs-lookup"><span data-stu-id="06c30-128">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() and subscription() in linked template refer to linked resource group/subscription
    }
}
```

## <a name="example-templates"></a><span data-ttu-id="06c30-129">Example templates</span><span class="sxs-lookup"><span data-stu-id="06c30-129">Example templates</span></span>

<span data-ttu-id="06c30-130">The following templates demonstrate multiple resource group deployments.</span><span class="sxs-lookup"><span data-stu-id="06c30-130">The following templates demonstrate multiple resource group deployments.</span></span> <span data-ttu-id="06c30-131">Scripts to deploy the templates are shown after the table.</span><span class="sxs-lookup"><span data-stu-id="06c30-131">Scripts to deploy the templates are shown after the table.</span></span>

|<span data-ttu-id="06c30-132">Template</span><span class="sxs-lookup"><span data-stu-id="06c30-132">Template</span></span>  |<span data-ttu-id="06c30-133">Description</span><span class="sxs-lookup"><span data-stu-id="06c30-133">Description</span></span>  |
|---------|---------|
|[<span data-ttu-id="06c30-134">Cross subscription template</span><span class="sxs-lookup"><span data-stu-id="06c30-134">Cross subscription template</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/crosssubscription.json) |<span data-ttu-id="06c30-135">Deploys one storage account to one resource group and one storage account to a second resource group.</span><span class="sxs-lookup"><span data-stu-id="06c30-135">Deploys one storage account to one resource group and one storage account to a second resource group.</span></span> <span data-ttu-id="06c30-136">Include a value for the subscription ID when the second resource group is in a different subscription.</span><span class="sxs-lookup"><span data-stu-id="06c30-136">Include a value for the subscription ID when the second resource group is in a different subscription.</span></span> |
|[<span data-ttu-id="06c30-137">Cross resource group properties template</span><span class="sxs-lookup"><span data-stu-id="06c30-137">Cross resource group properties template</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/crossresourcegroupproperties.json) |<span data-ttu-id="06c30-138">Demonstrates how the `resourceGroup()` function resolves.</span><span class="sxs-lookup"><span data-stu-id="06c30-138">Demonstrates how the `resourceGroup()` function resolves.</span></span> <span data-ttu-id="06c30-139">It does not deploy any resources.</span><span class="sxs-lookup"><span data-stu-id="06c30-139">It does not deploy any resources.</span></span> |

### <a name="powershell"></a><span data-ttu-id="06c30-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06c30-140">PowerShell</span></span>

<span data-ttu-id="06c30-141">For PowerShell, to deploy two storage accounts to two resource groups in the **same subscription**, use:</span><span class="sxs-lookup"><span data-stu-id="06c30-141">For PowerShell, to deploy two storage accounts to two resource groups in the **same subscription**, use:</span></span>

```azurepowershell-interactive
$firstRG = "primarygroup"
$secondRG = "secondarygroup"

New-AzureRmResourceGroup -Name $firstRG -Location southcentralus
New-AzureRmResourceGroup -Name $secondRG -Location eastus

New-AzureRmResourceGroupDeployment `
  -ResourceGroupName $firstRG `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crosssubscription.json `
  -storagePrefix storage `
  -secondResourceGroup $secondRG `
  -secondStorageLocation eastus
```

<span data-ttu-id="06c30-142">For PowerShell, to deploy two storage accounts to **two subscriptions**, use:</span><span class="sxs-lookup"><span data-stu-id="06c30-142">For PowerShell, to deploy two storage accounts to **two subscriptions**, use:</span></span>

```azurepowershell-interactive
$firstRG = "primarygroup"
$secondRG = "secondarygroup"

$firstSub = "<first-subscription-id>"
$secondSub = "<second-subscription-id>"

Select-AzureRmSubscription -Subscription $secondSub
New-AzureRmResourceGroup -Name $secondRG -Location eastus

Select-AzureRmSubscription -Subscription $firstSub
New-AzureRmResourceGroup -Name $firstRG -Location southcentralus

New-AzureRmResourceGroupDeployment `
  -ResourceGroupName $firstRG `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crosssubscription.json `
  -storagePrefix storage `
  -secondResourceGroup $secondRG `
  -secondStorageLocation eastus `
  -secondSubscriptionID $secondSub
```

<span data-ttu-id="06c30-143">For PowerShell, to test how the **resource group object** resolves for the parent template, inline template, and linked template, use:</span><span class="sxs-lookup"><span data-stu-id="06c30-143">For PowerShell, to test how the **resource group object** resolves for the parent template, inline template, and linked template, use:</span></span>

```azurepowershell-interactive
New-AzureRmResourceGroup -Name parentGroup -Location southcentralus
New-AzureRmResourceGroup -Name inlineGroup -Location southcentralus
New-AzureRmResourceGroup -Name linkedGroup -Location southcentralus

New-AzureRmResourceGroupDeployment `
  -ResourceGroupName parentGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crossresourcegroupproperties.json
```

<span data-ttu-id="06c30-144">In the preceding example, both **parentRG** and **inlineRG** resolve to **parentGroup**.</span><span class="sxs-lookup"><span data-stu-id="06c30-144">In the preceding example, both **parentRG** and **inlineRG** resolve to **parentGroup**.</span></span> <span data-ttu-id="06c30-145">**linkedRG** resolves to **linkedGroup**.</span><span class="sxs-lookup"><span data-stu-id="06c30-145">**linkedRG** resolves to **linkedGroup**.</span></span> <span data-ttu-id="06c30-146">The output from the preceding example is:</span><span class="sxs-lookup"><span data-stu-id="06c30-146">The output from the preceding example is:</span></span>

```powershell
 Name             Type                       Value
 ===============  =========================  ==========
 parentRG         Object                     {
                                               "id": "/subscriptions/<subscription-id>/resourceGroups/parentGroup",
                                               "name": "parentGroup",
                                               "location": "southcentralus",
                                               "properties": {
                                                 "provisioningState": "Succeeded"
                                               }
                                             }
 inlineRG         Object                     {
                                               "id": "/subscriptions/<subscription-id>/resourceGroups/parentGroup",
                                               "name": "parentGroup",
                                               "location": "southcentralus",
                                               "properties": {
                                                 "provisioningState": "Succeeded"
                                               }
                                             }
 linkedRG         Object                     {
                                               "id": "/subscriptions/<subscription-id>/resourceGroups/linkedGroup",
                                               "name": "linkedGroup",
                                               "location": "southcentralus",
                                               "properties": {
                                                 "provisioningState": "Succeeded"
                                               }
                                             }
```

### <a name="azure-cli"></a><span data-ttu-id="06c30-147">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="06c30-147">Azure CLI</span></span>

<span data-ttu-id="06c30-148">For Azure CLI, to deploy two storage accounts to two resource groups in the **same subscription**, use:</span><span class="sxs-lookup"><span data-stu-id="06c30-148">For Azure CLI, to deploy two storage accounts to two resource groups in the **same subscription**, use:</span></span>

```azurecli-interactive
firstRG="primarygroup"
secondRG="secondarygroup"

az group create --name $firstRG --location southcentralus
az group create --name $secondRG --location eastus
az group deployment create \
  --name ExampleDeployment \
  --resource-group $firstRG \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crosssubscription.json \
  --parameters storagePrefix=tfstorage secondResourceGroup=$secondRG secondStorageLocation=eastus
```

<span data-ttu-id="06c30-149">For Azure CLI, to deploy two storage accounts to **two subscriptions**, use:</span><span class="sxs-lookup"><span data-stu-id="06c30-149">For Azure CLI, to deploy two storage accounts to **two subscriptions**, use:</span></span>

```azurecli-interactive
firstRG="primarygroup"
secondRG="secondarygroup"

firstSub="<first-subscription-id>"
secondSub="<second-subscription-id>"

az account set --subscription $secondSub
az group create --name $secondRG --location eastus

az account set --subscription $firstSub
az group create --name $firstRG --location southcentralus

az group deployment create \
  --name ExampleDeployment \
  --resource-group $firstRG \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crosssubscription.json \
  --parameters storagePrefix=storage secondResourceGroup=$secondRG secondStorageLocation=eastus secondSubscriptionID=$secondSub
```

<span data-ttu-id="06c30-150">For Azure CLI, to test how the **resource group object** resolves for the parent template, inline template, and linked template, use:</span><span class="sxs-lookup"><span data-stu-id="06c30-150">For Azure CLI, to test how the **resource group object** resolves for the parent template, inline template, and linked template, use:</span></span>

```azurecli-interactive
az group create --name parentGroup --location southcentralus
az group create --name inlineGroup --location southcentralus
az group create --name linkedGroup --location southcentralus

az group deployment create \
  --name ExampleDeployment \
  --resource-group parentGroup \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/crossresourcegroupproperties.json 
```

<span data-ttu-id="06c30-151">In the preceding example, both **parentRG** and **inlineRG** resolve to **parentGroup**.</span><span class="sxs-lookup"><span data-stu-id="06c30-151">In the preceding example, both **parentRG** and **inlineRG** resolve to **parentGroup**.</span></span> <span data-ttu-id="06c30-152">**linkedRG** resolves to **linkedGroup**.</span><span class="sxs-lookup"><span data-stu-id="06c30-152">**linkedRG** resolves to **linkedGroup**.</span></span> <span data-ttu-id="06c30-153">The output from the preceding example is:</span><span class="sxs-lookup"><span data-stu-id="06c30-153">The output from the preceding example is:</span></span>

```azurecli
...
"outputs": {
  "inlineRG": {
    "type": "Object",
    "value": {
      "id": "/subscriptions/<subscription-id>/resourceGroups/parentGroup",
      "location": "southcentralus",
      "name": "parentGroup",
      "properties": {
        "provisioningState": "Succeeded"
      }
    }
  },
  "linkedRG": {
    "type": "Object",
    "value": {
      "id": "/subscriptions/<subscription-id>/resourceGroups/linkedGroup",
      "location": "southcentralus",
      "name": "linkedGroup",
      "properties": {
        "provisioningState": "Succeeded"
      }
    }
  },
  "parentRG": {
    "type": "Object",
    "value": {
      "id": "/subscriptions/<subscription-id>/resourceGroups/parentGroup",
      "location": "southcentralus",
      "name": "parentGroup",
      "properties": {
        "provisioningState": "Succeeded"
      }
    }
  }
},
...
```

## <a name="next-steps"></a><span data-ttu-id="06c30-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="06c30-154">Next steps</span></span>

* <span data-ttu-id="06c30-155">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="06c30-155">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="06c30-156">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="06c30-156">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="06c30-157">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="06c30-157">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
