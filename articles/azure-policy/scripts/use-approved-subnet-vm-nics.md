---
title: Azure Policy json sample - Use approved subnet for VM network interfaces | Microsoft Docs
description: This json sample policy requires that network interfaces use an approved subnet.
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
ms.openlocfilehash: 0af19930c8cdc1b9eaff5982495c8f07107fafd0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857782"
---
# <a name="use-approved-subnet-for-vm-network-interfaces"></a><span data-ttu-id="69e32-103">Use approved subnet for VM network interfaces</span><span class="sxs-lookup"><span data-stu-id="69e32-103">Use approved subnet for VM network interfaces</span></span>

<span data-ttu-id="69e32-104">This policy requires that network interfaces use an approved subnet.</span><span class="sxs-lookup"><span data-stu-id="69e32-104">This policy requires that network interfaces use an approved subnet.</span></span> <span data-ttu-id="69e32-105">You specify the ID of the approved subnet.</span><span class="sxs-lookup"><span data-stu-id="69e32-105">You specify the ID of the approved subnet.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="69e32-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="69e32-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/Network/vm-creation-in-approved-subnet/azurepolicy.json "Use approved subnet for VM network interfaces")]

<span data-ttu-id="69e32-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="69e32-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="69e32-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="69e32-108">Deploy with the portal</span></span>

<span data-ttu-id="69e32-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fvm-creation-in-approved-subnet%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="69e32-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fvm-creation-in-approved-subnet%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="69e32-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="69e32-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "vm-creation-in-approved-subnet" -DisplayName "Use approved subnet for VM network interfaces" -description "This policy enforces VM network interfaces to use subnet" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/vm-creation-in-approved-subnet/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/vm-creation-in-approved-subnet/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -subnetId <Subnet Id> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="69e32-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="69e32-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="69e32-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="69e32-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="69e32-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="69e32-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'vm-creation-in-approved-subnet' --display-name 'Use approved subnet for VM network interfaces' --description 'This policy enforces VM network interfaces to use subnet' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/vm-creation-in-approved-subnet/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/vm-creation-in-approved-subnet/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "vm-creation-in-approved-subnet"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="69e32-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="69e32-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="69e32-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="69e32-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="69e32-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="69e32-116">Next steps</span></span>

- <span data-ttu-id="69e32-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="69e32-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>