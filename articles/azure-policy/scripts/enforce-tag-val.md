---
title: Azure Policy json sample - Enforce tag and its value | Microsoft Docs
description: This json sample policy requires a specified tag name and value.
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
ms.openlocfilehash: e22b7cd15e8ab611f1682b33c3a57405b33619c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856511"
---
# <a name="enforce-tag-and-its-value"></a><span data-ttu-id="01b46-103">Enforce tag and its value</span><span class="sxs-lookup"><span data-stu-id="01b46-103">Enforce tag and its value</span></span>

<span data-ttu-id="01b46-104">This policy requires a specified tag name and value.</span><span class="sxs-lookup"><span data-stu-id="01b46-104">This policy requires a specified tag name and value.</span></span> <span data-ttu-id="01b46-105">You specify the tag name and value to enforce.</span><span class="sxs-lookup"><span data-stu-id="01b46-105">You specify the tag name and value to enforce.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="01b46-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="01b46-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/built-in-policy/enforce-tag-value/azurepolicy.json "Enforce tag and its value")]

<span data-ttu-id="01b46-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="01b46-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="01b46-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="01b46-108">Deploy with the portal</span></span>

<span data-ttu-id="01b46-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fenforce-tag-value%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="01b46-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fenforce-tag-value%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="01b46-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="01b46-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "enforce-tag-value" -DisplayName "Enforce tag and its value" -description "Enforces a required tag and its value." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/enforce-tag-value/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/enforce-tag-value/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -tagName <tagName> -tagValue <tagValue> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="01b46-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="01b46-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="01b46-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="01b46-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="01b46-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="01b46-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'enforce-tag-value' --display-name 'Enforce tag and its value' --description 'Enforces a required tag and its value.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/enforce-tag-value/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/enforce-tag-value/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "enforce-tag-value"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="01b46-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="01b46-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="01b46-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="01b46-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="01b46-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="01b46-116">Next steps</span></span>

- <span data-ttu-id="01b46-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="01b46-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>