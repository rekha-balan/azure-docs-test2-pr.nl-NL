---
title: Azure Policy json sample - Allowed load balancer SKUs | Microsoft Docs
description: This json sample policy requires that load balancers use an approved SKU.
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
ms.openlocfilehash: 5a99665bab189b123046e38939826ae8bcf6cb45
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870911"
---
# <a name="allowed-load-balancer-skus"></a><span data-ttu-id="e43b0-103">Allowed load balancer SKUs</span><span class="sxs-lookup"><span data-stu-id="e43b0-103">Allowed load balancer SKUs</span></span>

<span data-ttu-id="e43b0-104">This policy requires that load balancers use an approved SKU.</span><span class="sxs-lookup"><span data-stu-id="e43b0-104">This policy requires that load balancers use an approved SKU.</span></span> <span data-ttu-id="e43b0-105">You specify an array of allowed SKUs.</span><span class="sxs-lookup"><span data-stu-id="e43b0-105">You specify an array of allowed SKUs.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="e43b0-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="e43b0-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/Network/load-balancer-skus/azurepolicy.json "Allowed Load Balancer SKUs")]

<span data-ttu-id="e43b0-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e43b0-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="e43b0-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="e43b0-108">Deploy with the portal</span></span>

<span data-ttu-id="e43b0-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fload-balancer-skus%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="e43b0-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fload-balancer-skus%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="e43b0-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="e43b0-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "load-balancer-skus" -DisplayName "Allowed Load Balancer SKUs" -description "This policy enables you to specify a set of load balancer SKUs that your organization can deploy." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/load-balancer-skus/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/load-balancer-skus/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -listOfAllowedSKUs <Allowed SKUs> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="e43b0-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="e43b0-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="e43b0-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e43b0-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="e43b0-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e43b0-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'load-balancer-skus' --display-name 'Allowed Load Balancer SKUs' --description 'This policy enables you to specify a set of load balancer SKUs that your organization can deploy.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/load-balancer-skus/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/load-balancer-skus/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "load-balancer-skus"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="e43b0-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="e43b0-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="e43b0-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e43b0-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="e43b0-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="e43b0-116">Next steps</span></span>

- <span data-ttu-id="e43b0-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e43b0-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>