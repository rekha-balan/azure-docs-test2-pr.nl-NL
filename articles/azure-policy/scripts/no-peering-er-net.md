---
title: Azure Policy json sample - No network peering to ER network | Microsoft Docs
description: This json sample policy prohibits a network peering from being associated to a network in a specified resource group.
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
ms.openlocfilehash: a9b428fcfdd20a9b55497496cd46afd3c70e29d2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855718"
---
# <a name="no-network-peering-to-er-network"></a><span data-ttu-id="ffec0-103">No network peering to ER network</span><span class="sxs-lookup"><span data-stu-id="ffec0-103">No network peering to ER network</span></span>

<span data-ttu-id="ffec0-104">This policy prohibits a network peering from being associated to a network in a specified resource group.</span><span class="sxs-lookup"><span data-stu-id="ffec0-104">This policy prohibits a network peering from being associated to a network in a specified resource group.</span></span> <span data-ttu-id="ffec0-105">Use to prevent connection with central managed network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="ffec0-105">Use to prevent connection with central managed network infrastructure.</span></span> <span data-ttu-id="ffec0-106">You specify the name of the resource group to prevent association.</span><span class="sxs-lookup"><span data-stu-id="ffec0-106">You specify the name of the resource group to prevent association.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="ffec0-107">Sample template</span><span class="sxs-lookup"><span data-stu-id="ffec0-107">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/Network/no-network-peerings-to-er-network/azurepolicy.json "No network peering to ER network")]

<span data-ttu-id="ffec0-108">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ffec0-108">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="ffec0-109">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="ffec0-109">Deploy with the portal</span></span>

<span data-ttu-id="ffec0-110">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fno-network-peerings-to-er-network%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="ffec0-110">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fno-network-peerings-to-er-network%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="ffec0-111">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffec0-111">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "no-network-peerings-to-er-network" -DisplayName "No network peering to ER network" -description "No network peering can be associated to networks in network in a resource group containing central managed network infrastructure." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/no-network-peerings-to-er-network/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/no-network-peerings-to-er-network/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -resourceGroupName <ER Network Resource Group Name> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="ffec0-112">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="ffec0-112">Clean up PowerShell deployment</span></span>

<span data-ttu-id="ffec0-113">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ffec0-113">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="ffec0-114">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ffec0-114">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'no-network-peerings-to-er-network' --display-name 'No network peering to ER network' --description 'No network peering can be associated to networks in network in a resource group containing central managed network infrastructure.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/no-network-peerings-to-er-network/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/no-network-peerings-to-er-network/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "no-network-peerings-to-er-network"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="ffec0-115">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="ffec0-115">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="ffec0-116">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ffec0-116">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="ffec0-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="ffec0-117">Next steps</span></span>

- <span data-ttu-id="ffec0-118">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ffec0-118">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>