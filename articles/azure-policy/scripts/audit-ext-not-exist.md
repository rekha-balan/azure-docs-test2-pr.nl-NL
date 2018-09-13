---
title: Azure Policy json sample - Audit if extension does not exist  | Microsoft Docs
description: This json sample policy audits if an extension is not deployed with a virtual machine.
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
ms.openlocfilehash: cad271a5a218cb13ff4434f3570e6ad5699a7f6c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868962"
---
# <a name="audit-if-extension-does-not-exist"></a><span data-ttu-id="6b75d-103">Audit if extension does not exist</span><span class="sxs-lookup"><span data-stu-id="6b75d-103">Audit if extension does not exist</span></span>

<span data-ttu-id="6b75d-104">This policy audits if an extension is not deployed with a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6b75d-104">This policy audits if an extension is not deployed with a virtual machine.</span></span> <span data-ttu-id="6b75d-105">You specify the extension publisher and type to check whether it was deployed.</span><span class="sxs-lookup"><span data-stu-id="6b75d-105">You specify the extension publisher and type to check whether it was deployed.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="6b75d-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="6b75d-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/compute/audit-vm-extension/azurepolicy.json "Audit if extension does not exist")]

<span data-ttu-id="6b75d-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b75d-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="6b75d-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="6b75d-108">Deploy with the portal</span></span>

<span data-ttu-id="6b75d-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Faudit-vm-extension%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="6b75d-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Faudit-vm-extension%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="6b75d-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b75d-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "audit-vm-extension" -DisplayName "Audit if extension does not exist" -description "This policy audits if a required extension doesn't exist." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/audit-vm-extension/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/audit-vm-extension/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -publisher <Extension Publisher> -type <Extension Type> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="6b75d-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="6b75d-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="6b75d-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="6b75d-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="6b75d-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6b75d-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'audit-vm-extension' --display-name 'Audit if extension does not exist' --description 'This policy audits if a required extension doesn't exist.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/audit-vm-extension/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/audit-vm-extension/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "audit-vm-extension"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="6b75d-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="6b75d-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="6b75d-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="6b75d-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="6b75d-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b75d-116">Next steps</span></span>

- <span data-ttu-id="6b75d-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6b75d-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>