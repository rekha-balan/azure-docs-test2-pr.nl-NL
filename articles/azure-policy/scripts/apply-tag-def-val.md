---
title: Azure Policy json sample - Apply tag and its default value | Microsoft Docs
description: This json sample policy appends a specified tag name and value, if that tag is not provided.
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
ms.openlocfilehash: f8be0aab95297b87e1de23530c1e8d76e48af85d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857969"
---
# <a name="apply-tag-and-its-default-value"></a><span data-ttu-id="b2cbb-103">Apply tag and its default value</span><span class="sxs-lookup"><span data-stu-id="b2cbb-103">Apply tag and its default value</span></span>

<span data-ttu-id="b2cbb-104">This policy appends a specified tag name and value, if that tag is not provided.</span><span class="sxs-lookup"><span data-stu-id="b2cbb-104">This policy appends a specified tag name and value, if that tag is not provided.</span></span> <span data-ttu-id="b2cbb-105">You specify the tag name and value to apply.</span><span class="sxs-lookup"><span data-stu-id="b2cbb-105">You specify the tag name and value to apply.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="b2cbb-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="b2cbb-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/built-in-policy/apply-default-tag-value/azurepolicy.json "Apply tag and its default value")]

<span data-ttu-id="b2cbb-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b2cbb-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="b2cbb-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="b2cbb-108">Deploy with the portal</span></span>

<span data-ttu-id="b2cbb-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fapply-default-tag-value%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="b2cbb-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fapply-default-tag-value%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="b2cbb-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2cbb-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "apply-default-tag-value" -DisplayName "Apply tag and its default value" -description "Applies a required tag and its default value if it is not specified by the user." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/apply-default-tag-value/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/apply-default-tag-value/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -tagName <tagName> -tagValue <tagValue> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="b2cbb-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="b2cbb-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="b2cbb-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="b2cbb-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```


## <a name="deploy-with-azure-cli"></a><span data-ttu-id="b2cbb-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b2cbb-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'apply-default-tag-value' --display-name 'Apply tag and its default value' --description 'Applies a required tag and its default value if it is not specified by the user.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/apply-default-tag-value/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/apply-default-tag-value/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "apply-default-tag-value"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="b2cbb-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="b2cbb-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="b2cbb-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="b2cbb-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="b2cbb-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="b2cbb-116">Next steps</span></span>

- <span data-ttu-id="b2cbb-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b2cbb-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>