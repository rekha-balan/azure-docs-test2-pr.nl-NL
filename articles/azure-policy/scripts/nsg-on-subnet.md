---
title: Azure Policy json sample - NSG x on every subnet | Microsoft Docs
description: This json sample policy requires that a specific network security group is used with every virtual subnet.
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
ms.openlocfilehash: 82bff45e1d6577a064f8545935f8faf07b4d5b8c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865786"
---
# <a name="nsg-x-on-every-subnet"></a><span data-ttu-id="24dde-103">NSG x on every subnet</span><span class="sxs-lookup"><span data-stu-id="24dde-103">NSG x on every subnet</span></span>

<span data-ttu-id="24dde-104">This policy requires that a specific network security group is used with every virtual subnet.</span><span class="sxs-lookup"><span data-stu-id="24dde-104">This policy requires that a specific network security group is used with every virtual subnet.</span></span> <span data-ttu-id="24dde-105">You specify the ID of the network security group to use.</span><span class="sxs-lookup"><span data-stu-id="24dde-105">You specify the ID of the network security group to use.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="24dde-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="24dde-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/Network/enforce-nsg-on-subnet/azurepolicy.json "NSG X on every subnet")]

<span data-ttu-id="24dde-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="24dde-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="24dde-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="24dde-108">Deploy with the portal</span></span>

<span data-ttu-id="24dde-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fenforce-nsg-on-subnet%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="24dde-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fenforce-nsg-on-subnet%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="24dde-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="24dde-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "enforce-nsg-on-subnet" -DisplayName "NSG X on every subnet" -description "This policy enforces a specific NSG on every subnet" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/enforce-nsg-on-subnet/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/enforce-nsg-on-subnet/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -nsgId <NSG Id> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="24dde-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="24dde-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="24dde-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="24dde-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="24dde-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="24dde-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'enforce-nsg-on-subnet' --display-name 'NSG X on every subnet' --description 'This policy enforces a specific NSG on every subnet' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/enforce-nsg-on-subnet/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/enforce-nsg-on-subnet/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "enforce-nsg-on-subnet"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="24dde-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="24dde-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="24dde-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="24dde-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="24dde-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="24dde-116">Next steps</span></span>

- <span data-ttu-id="24dde-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="24dde-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>