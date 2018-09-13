---
title: Deploy resources to Azure | Microsoft Docs
description: Use Azure PowerShell or Azure CLI to deploy resources to Azure. The resources are defined in a Resource Manager template.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: a77354d0719240e5916b5ec945dad75e534802d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563885"
---
# <a name="deploy-resources-to-azure"></a><span data-ttu-id="e7e08-104">Deploy resources to Azure</span><span class="sxs-lookup"><span data-stu-id="e7e08-104">Deploy resources to Azure</span></span>

<span data-ttu-id="e7e08-105">This topic shows how to deploy resources to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e7e08-105">This topic shows how to deploy resources to your Azure subscription.</span></span> <span data-ttu-id="e7e08-106">You can use either Azure PowerShell or Azure CLI to deploy a Resource Manager template that defines the infrastructure for your solution.</span><span class="sxs-lookup"><span data-stu-id="e7e08-106">You can use either Azure PowerShell or Azure CLI to deploy a Resource Manager template that defines the infrastructure for your solution.</span></span>

<span data-ttu-id="e7e08-107">For an introduction to concepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7e08-107">For an introduction to concepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="e7e08-108">Steps for deployment</span><span class="sxs-lookup"><span data-stu-id="e7e08-108">Steps for deployment</span></span>

<span data-ttu-id="e7e08-109">This topic assumes you are deploying the [example storage template](#example-storage-template) in this topic.</span><span class="sxs-lookup"><span data-stu-id="e7e08-109">This topic assumes you are deploying the [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="e7e08-110">You can use a different template, but the parameters you pass are different than what is shown in this topic.</span><span class="sxs-lookup"><span data-stu-id="e7e08-110">You can use a different template, but the parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="e7e08-111">After creating a template, the general steps for deploying your template are:</span><span class="sxs-lookup"><span data-stu-id="e7e08-111">After creating a template, the general steps for deploying your template are:</span></span>

1. <span data-ttu-id="e7e08-112">Log in to your account</span><span class="sxs-lookup"><span data-stu-id="e7e08-112">Log in to your account</span></span>
2. <span data-ttu-id="e7e08-113">Select the subscription to use (only necessary if you have multiple subscriptions, and you want to use one that is not the default subscription)</span><span class="sxs-lookup"><span data-stu-id="e7e08-113">Select the subscription to use (only necessary if you have multiple subscriptions, and you want to use one that is not the default subscription)</span></span>
3. <span data-ttu-id="e7e08-114">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="e7e08-114">Create a resource group</span></span>
4. <span data-ttu-id="e7e08-115">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="e7e08-115">Deploy the template</span></span>
5. <span data-ttu-id="e7e08-116">Check your deployment status</span><span class="sxs-lookup"><span data-stu-id="e7e08-116">Check your deployment status</span></span>

<span data-ttu-id="e7e08-117">The following sections show how to perform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e7e08-117">The following sections show how to perform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="e7e08-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7e08-118">PowerShell</span></span>

1. <span data-ttu-id="e7e08-119">To install Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="e7e08-119">To install Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs).</span></span>

2. <span data-ttu-id="e7e08-120">To quickly get started with deployment, use the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="e7e08-120">To quickly get started with deployment, use the following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="e7e08-121">The `Set-AzureRmContext` cmdlet is only needed if you want to use a subscription other than your default subscription.</span><span class="sxs-lookup"><span data-stu-id="e7e08-121">The `Set-AzureRmContext` cmdlet is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="e7e08-122">To see all your subscriptions and their IDs, use:</span><span class="sxs-lookup"><span data-stu-id="e7e08-122">To see all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="e7e08-123">The deployment can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="e7e08-123">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="e7e08-124">When it finishes, you see a message similar to:</span><span class="sxs-lookup"><span data-stu-id="e7e08-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="e7e08-125">To see that your resource group and storage account were deployed to your subscription, use:</span><span class="sxs-lookup"><span data-stu-id="e7e08-125">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="e7e08-126">You can specify template parameters as PowerShell parameters when deploying a template.</span><span class="sxs-lookup"><span data-stu-id="e7e08-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="e7e08-127">The earlier example did not include any template parameters, so the default values in the template were used.</span><span class="sxs-lookup"><span data-stu-id="e7e08-127">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="e7e08-128">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span><span class="sxs-lookup"><span data-stu-id="e7e08-128">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="e7e08-129">You now have two storage accounts in your resource group.</span><span class="sxs-lookup"><span data-stu-id="e7e08-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="e7e08-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e7e08-130">Azure CLI</span></span>

1. <span data-ttu-id="e7e08-131">To install Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e7e08-131">To install Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="e7e08-132">To quickly get started with deployment, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="e7e08-132">To quickly get started with deployment, use the following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="e7e08-133">The `az account set` command is only needed if you want to use a subscription other than your default subscription.</span><span class="sxs-lookup"><span data-stu-id="e7e08-133">The `az account set` command is only needed if you want to use a subscription other than your default subscription.</span></span> <span data-ttu-id="e7e08-134">To see all your subscriptions and their IDs, use:</span><span class="sxs-lookup"><span data-stu-id="e7e08-134">To see all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="e7e08-135">The deployment can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="e7e08-135">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="e7e08-136">When it finishes, you see a message similar to:</span><span class="sxs-lookup"><span data-stu-id="e7e08-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="e7e08-137">To see that your resource group and storage account were deployed to your subscription, use:</span><span class="sxs-lookup"><span data-stu-id="e7e08-137">To see that your resource group and storage account were deployed to your subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="e7e08-138">You can specify template parameters as PowerShell parameters when deploying a template.</span><span class="sxs-lookup"><span data-stu-id="e7e08-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="e7e08-139">The earlier example did not include any template parameters, so the default values in the template were used.</span><span class="sxs-lookup"><span data-stu-id="e7e08-139">The earlier example did not include any template parameters, so the default values in the template were used.</span></span> <span data-ttu-id="e7e08-140">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span><span class="sxs-lookup"><span data-stu-id="e7e08-140">To deploy another storage account, and provide parameter values for the storage name prefix and the storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="e7e08-141">You now have two storage accounts in your resource group.</span><span class="sxs-lookup"><span data-stu-id="e7e08-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="e7e08-142">Example storage template</span><span class="sxs-lookup"><span data-stu-id="e7e08-142">Example storage template</span></span>

<span data-ttu-id="e7e08-143">Use the following example template to deploy a storage account to your subscription:</span><span class="sxs-lookup"><span data-stu-id="e7e08-143">Use the following example template to deploy a storage account to your subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "The type of replication to use for the storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="e7e08-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="e7e08-144">Next steps</span></span>

* <span data-ttu-id="e7e08-145">For detailed information about using PowerShell to deploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="e7e08-145">For detailed information about using PowerShell to deploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="e7e08-146">For detailed information about using Azure CLI to deploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="e7e08-146">For detailed information about using Azure CLI to deploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



