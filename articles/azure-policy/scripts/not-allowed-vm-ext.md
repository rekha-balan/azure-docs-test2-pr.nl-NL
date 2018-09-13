---
title: Azure Policy json sample - Not allowed VM extensions  | Microsoft Docs
description: This json sample policy prohibits the use of specified extensions.
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
ms.openlocfilehash: 06ffed16080f1e24ec0e163171c6913ecfc08496
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866474"
---
# <a name="not-allowed-vm-extensions"></a><span data-ttu-id="a4f1f-103">Not allowed VM extensions</span><span class="sxs-lookup"><span data-stu-id="a4f1f-103">Not allowed VM extensions</span></span>

<span data-ttu-id="a4f1f-104">Prohibits the use of specified extensions.</span><span class="sxs-lookup"><span data-stu-id="a4f1f-104">Prohibits the use of specified extensions.</span></span> <span data-ttu-id="a4f1f-105">You specify an array containing the prohibited extension types.</span><span class="sxs-lookup"><span data-stu-id="a4f1f-105">You specify an array containing the prohibited extension types.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="a4f1f-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="a4f1f-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/compute/not-allowed-vmextension/azurepolicy.json "Not allowed VM Extensions")]

<span data-ttu-id="a4f1f-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a4f1f-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="a4f1f-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="a4f1f-108">Deploy with the portal</span></span>

<span data-ttu-id="a4f1f-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fnot-allowed-vmextension%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="a4f1f-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fnot-allowed-vmextension%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="a4f1f-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4f1f-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "not-allowed-vmextension" -DisplayName "Not allowed VM Extensions" -description "This policy governs which VM extensions that are explicitly denied." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/not-allowed-vmextension/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/not-allowed-vmextension/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -notAllowedExtensions <Denied extension> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="a4f1f-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="a4f1f-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="a4f1f-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a4f1f-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="a4f1f-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a4f1f-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'not-allowed-vmextension' --display-name 'Not allowed VM Extensions' --description 'This policy governs which VM extensions that are explicitly denied.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/not-allowed-vmextension/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/not-allowed-vmextension/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "not-allowed-vmextension"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="a4f1f-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="a4f1f-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="a4f1f-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a4f1f-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="a4f1f-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4f1f-116">Next steps</span></span>

- <span data-ttu-id="a4f1f-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a4f1f-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>