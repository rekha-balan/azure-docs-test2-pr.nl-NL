---
title: Azure Policy json sample - Deny hybrid use benefit | Microsoft Docs
description: This json sample policy prohibits use of Azure Hybrid Use Benefit (AHUB).
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
ms.openlocfilehash: ad90253cfc23eda4c54d76092238920f1947964a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868635"
---
# <a name="deny-hybrid-use-benefit"></a><span data-ttu-id="33a39-103">Deny hybrid use benefit</span><span class="sxs-lookup"><span data-stu-id="33a39-103">Deny hybrid use benefit</span></span>

<span data-ttu-id="33a39-104">Prohibits use of Azure Hybrid Use Benefit (AHUB).</span><span class="sxs-lookup"><span data-stu-id="33a39-104">Prohibits use of Azure Hybrid Use Benefit (AHUB).</span></span> <span data-ttu-id="33a39-105">Use when you do not want to permit use of on-premises licenses.</span><span class="sxs-lookup"><span data-stu-id="33a39-105">Use when you do not want to permit use of on-premises licenses.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="33a39-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="33a39-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/compute/deny-hybrid-use-benefit/azurepolicy.json "Deny hybrid use benefit")]

<span data-ttu-id="33a39-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="33a39-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="33a39-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="33a39-108">Deploy with the portal</span></span>

<span data-ttu-id="33a39-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fdeny-hybrid-use-benefit%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="33a39-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fdeny-hybrid-use-benefit%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="33a39-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="33a39-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "deny-hybrid-use-benefit" -DisplayName "Deny hybrid use benefit" -description "This policy will deny usage of hybrid use benefit." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/deny-hybrid-use-benefit/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/deny-hybrid-use-benefit/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="33a39-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="33a39-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="33a39-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="33a39-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="33a39-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="33a39-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'deny-hybrid-use-benefit' --display-name 'Deny hybrid use benefit' --description 'This policy will deny usage of hybrid use benefit.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/deny-hybrid-use-benefit/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/deny-hybrid-use-benefit/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "deny-hybrid-use-benefit"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="33a39-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="33a39-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="33a39-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="33a39-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="33a39-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="33a39-116">Next steps</span></span>

- <span data-ttu-id="33a39-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="33a39-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>