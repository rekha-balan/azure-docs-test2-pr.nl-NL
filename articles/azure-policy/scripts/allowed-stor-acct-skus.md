---
title: Azure Policy json sample - Allowed storage account SKUs | Microsoft Docs
description: This json sample policy requires that storage accounts use an approved SKU.
services: azure-policy
documentationcenter: ''
author: DCtheGeek
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: azure-policy
ms.devlang: ''
ms.topic: sample
ms.tgt_pltfrm: ''
ms.workload: ''
ms.date: 10/30/2017
ms.author: dacoulte
ms.custom: mvc
ms.openlocfilehash: a99e32d3524d4262297c192b37e80941ee2c5f9d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968183"
---
# <a name="allowed-storage-account-skus"></a><span data-ttu-id="5ef9d-103">Allowed storage account SKUs</span><span class="sxs-lookup"><span data-stu-id="5ef9d-103">Allowed storage account SKUs</span></span>

<span data-ttu-id="5ef9d-104">This policy requires that storage accounts use an approved SKU.</span><span class="sxs-lookup"><span data-stu-id="5ef9d-104">This policy requires that storage accounts use an approved SKU.</span></span> <span data-ttu-id="5ef9d-105">You specify an array of approved SKUs.</span><span class="sxs-lookup"><span data-stu-id="5ef9d-105">You specify an array of approved SKUs.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="5ef9d-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="5ef9d-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/built-in-policy/allowed-storageaccount-sku/azurepolicy.json "Allowed storage account SKUs")]

<span data-ttu-id="5ef9d-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5ef9d-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="5ef9d-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="5ef9d-108">Deploy with the portal</span></span>

<span data-ttu-id="5ef9d-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fallowed-storageaccount-sku%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="5ef9d-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fallowed-storageaccount-sku%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="5ef9d-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ef9d-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "allowed-storageaccount-sku" -DisplayName "Allowed storage account SKUs" -description "This policy enables you to specify a set of storage account SKUs that your organization can deploy." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-storageaccount-sku/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-storageaccount-sku/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -listOfAllowedSKUs <Allowed SKUs> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="5ef9d-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="5ef9d-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="5ef9d-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="5ef9d-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="5ef9d-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5ef9d-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'allowed-storageaccount-sku' --display-name 'Allowed storage account SKUs' --description 'This policy enables you to specify a set of storage account SKUs that your organization can deploy.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-storageaccount-sku/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-storageaccount-sku/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "allowed-storageaccount-sku"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="5ef9d-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="5ef9d-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="5ef9d-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="5ef9d-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="5ef9d-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ef9d-116">Next steps</span></span>

- <span data-ttu-id="5ef9d-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5ef9d-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>