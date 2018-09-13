---
title: Azure Policy json sample - Allowed resource types | Microsoft Docs
description: This json sample policy ensures only approved resource types are deployed.
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
ms.openlocfilehash: 2c13ba322a468ef96f5be4573947c73fb50dfe8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865057"
---
# <a name="allowed-resource-types"></a><span data-ttu-id="fdba5-103">Allowed resource types</span><span class="sxs-lookup"><span data-stu-id="fdba5-103">Allowed resource types</span></span>

<span data-ttu-id="fdba5-104">This policy ensures only approved resource types are deployed.</span><span class="sxs-lookup"><span data-stu-id="fdba5-104">This policy ensures only approved resource types are deployed.</span></span> <span data-ttu-id="fdba5-105">You specify an array of resource types that are permitted.</span><span class="sxs-lookup"><span data-stu-id="fdba5-105">You specify an array of resource types that are permitted.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="fdba5-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="fdba5-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/built-in-policy/allowed-resourcetypes/azurepolicy.json "Allowed resource types")]

<span data-ttu-id="fdba5-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fdba5-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="fdba5-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="fdba5-108">Deploy with the portal</span></span>

<span data-ttu-id="fdba5-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fallowed-resourcetypes%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="fdba5-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fallowed-resourcetypes%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="fdba5-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdba5-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "allowed-resourcetypes" -DisplayName "Allowed resource types" -description "This policy enables you to specify the resource types that your organization can deploy." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-resourcetypes/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-resourcetypes/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -listOfResourceTypesAllowed <Allowed resource types> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="fdba5-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="fdba5-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="fdba5-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="fdba5-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="fdba5-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fdba5-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'allowed-resourcetypes' --display-name 'Allowed resource types' --description 'This policy enables you to specify the resource types that your organization can deploy.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-resourcetypes/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-resourcetypes/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "allowed-resourcetypes"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="fdba5-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="fdba5-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="fdba5-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="fdba5-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="fdba5-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="fdba5-116">Next steps</span></span>

- <span data-ttu-id="fdba5-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fdba5-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>