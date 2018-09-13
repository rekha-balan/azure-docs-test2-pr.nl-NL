---
title: Azure Policy json sample - NSG x on every NIC | Microsoft Docs
description: This json sample policy requires that a specific network security group is used with every virtual network interface.
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
ms.openlocfilehash: 528c809db4d6efc436089d25366db82acd1f6e6e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866186"
---
# <a name="nsg-x-on-every-nic"></a><span data-ttu-id="a37bf-103">NSG x on every NIC</span><span class="sxs-lookup"><span data-stu-id="a37bf-103">NSG x on every NIC</span></span>

<span data-ttu-id="a37bf-104">This policy requires that a specific network security group is used with every virtual network interface.</span><span class="sxs-lookup"><span data-stu-id="a37bf-104">This policy requires that a specific network security group is used with every virtual network interface.</span></span> <span data-ttu-id="a37bf-105">You specify the ID of the network security group to use.</span><span class="sxs-lookup"><span data-stu-id="a37bf-105">You specify the ID of the network security group to use.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="a37bf-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="a37bf-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/Network/enforce-nsg-on-nic/azurepolicy.json "NSG X on every nic")]

<span data-ttu-id="a37bf-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a37bf-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="a37bf-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="a37bf-108">Deploy with the portal</span></span>

<span data-ttu-id="a37bf-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fenforce-nsg-on-nic%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="a37bf-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fenforce-nsg-on-nic%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="a37bf-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="a37bf-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "enforce-nsg-on-nic" -DisplayName "NSG X on every nic" -description "This policy enforces a specific NSG on every virtual network interface" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/enforce-nsg-on-nic/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/enforce-nsg-on-nic/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -nsgId <Network Security Group Id> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="a37bf-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="a37bf-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="a37bf-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a37bf-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="a37bf-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a37bf-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'enforce-nsg-on-nic' --display-name 'NSG X on every nic' --description 'This policy enforces a specific NSG on every virtual network interface' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/enforce-nsg-on-nic/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/enforce-nsg-on-nic/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "enforce-nsg-on-nic"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="a37bf-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="a37bf-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="a37bf-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a37bf-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="a37bf-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="a37bf-116">Next steps</span></span>

- <span data-ttu-id="a37bf-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a37bf-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>