---
title: Azure Policy json sample - No user defined route table | Microsoft Docs
description: This json sample policy prohibits virtual networks from being deployed with a user-defined route table.
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
ms.openlocfilehash: 614522bc8bdb2da8bc549972ec1d7699a2f1acd0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870379"
---
# <a name="no-user-defined-route-table"></a><span data-ttu-id="7bf04-103">No user defined route table</span><span class="sxs-lookup"><span data-stu-id="7bf04-103">No user defined route table</span></span>

<span data-ttu-id="7bf04-104">This policy prohibits virtual networks from being deployed with a user-defined route table.</span><span class="sxs-lookup"><span data-stu-id="7bf04-104">This policy prohibits virtual networks from being deployed with a user-defined route table.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="7bf04-105">Sample template</span><span class="sxs-lookup"><span data-stu-id="7bf04-105">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/Network/no-route-table-in-ER-Network/azurepolicy.json "No User Defined Route Table")]

<span data-ttu-id="7bf04-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7bf04-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="7bf04-107">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="7bf04-107">Deploy with the portal</span></span>

<span data-ttu-id="7bf04-108">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fno-route-table-in-ER-Network%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="7bf04-108">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fno-route-table-in-ER-Network%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="7bf04-109">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bf04-109">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "no-route-table-in-ER-Network" -DisplayName "No User Defined Route Table" -description "Forbid virtual networks to use user defined route table" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/no-route-table-in-ER-Network/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/no-route-table-in-ER-Network/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="7bf04-110">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="7bf04-110">Clean up PowerShell deployment</span></span>

<span data-ttu-id="7bf04-111">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="7bf04-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="7bf04-112">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7bf04-112">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'no-route-table-in-ER-Network' --display-name 'No User Defined Route Table' --description 'Forbid virtual networks to use user defined route table' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/no-route-table-in-ER-Network/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/no-route-table-in-ER-Network/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "no-route-table-in-ER-Network"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="7bf04-113">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="7bf04-113">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="7bf04-114">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="7bf04-114">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="7bf04-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="7bf04-115">Next steps</span></span>

- <span data-ttu-id="7bf04-116">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7bf04-116">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>