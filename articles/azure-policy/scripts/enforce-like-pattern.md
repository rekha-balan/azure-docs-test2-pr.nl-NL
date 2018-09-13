---
title: Azure Policy json sample - enforce like pattern  | Microsoft Docs
description: This json sample policy requires that resources meet the like pattern for naming conventions.
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
ms.date: 11/13/2017
ms.author: dacoulte
ms.custom: mvc
ms.openlocfilehash: 33f67cc96395d1e481618e75fccb535c92d2fe75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857051"
---
# <a name="enforce-like-pattern-for-naming-conventions"></a><span data-ttu-id="d585a-103">Enforce like pattern for naming conventions</span><span class="sxs-lookup"><span data-stu-id="d585a-103">Enforce like pattern for naming conventions</span></span>

<span data-ttu-id="d585a-104">Require resource names meet a like pattern for naming conventions.</span><span class="sxs-lookup"><span data-stu-id="d585a-104">Require resource names meet a like pattern for naming conventions.</span></span> <span data-ttu-id="d585a-105">Specify the allowed like pattern as a parameter.</span><span class="sxs-lookup"><span data-stu-id="d585a-105">Specify the allowed like pattern as a parameter.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="d585a-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="d585a-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/TextPatterns/enforce-like-pattern/azurepolicy.json "enforce like pattern")]

<span data-ttu-id="d585a-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d585a-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="d585a-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="d585a-108">Deploy with the portal</span></span>

<span data-ttu-id="d585a-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FTextPatterns%2Fenforce-like-pattern%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="d585a-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FTextPatterns%2Fenforce-like-pattern%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="d585a-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="d585a-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "enforce-like-pattern" -DisplayName "Ensure resource names meet the like condition for a pattern." -description "Ensure resource names meet the like condition for a pattern." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/TextPatterns/enforce-like-pattern/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/TextPatterns/enforce-like-pattern/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="d585a-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="d585a-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="d585a-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="d585a-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="d585a-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d585a-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli
az policy definition create --name 'enforce-like-pattern' --display-name 'Ensure resource names meet the like condition for a pattern.' --description 'Ensure resource names meet the like condition for a pattern.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/TextPatterns/enforce-like-pattern/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/TextPatterns/enforce-like-pattern/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "enforce-like-pattern" 
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="d585a-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="d585a-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="d585a-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="d585a-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="d585a-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="d585a-116">Next steps</span></span>

- <span data-ttu-id="d585a-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d585a-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>