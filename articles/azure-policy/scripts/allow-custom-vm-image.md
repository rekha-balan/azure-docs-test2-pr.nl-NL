---
title: Azure Policy json sample - Allow custom VM image from a resource group  | Microsoft Docs
description: This json sample policy requires that custom images come from an approved resource group.
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
ms.openlocfilehash: 7e98a9706ea7432060fede1677216fa35e47269f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865263"
---
# <a name="allow-custom-vm-image-from-a-resource-group"></a><span data-ttu-id="b64e3-103">Allow custom VM image from a resource group</span><span class="sxs-lookup"><span data-stu-id="b64e3-103">Allow custom VM image from a resource group</span></span>

<span data-ttu-id="b64e3-104">This json sample policy requires that custom images come from an approved resource group.</span><span class="sxs-lookup"><span data-stu-id="b64e3-104">This json sample policy requires that custom images come from an approved resource group.</span></span> <span data-ttu-id="b64e3-105">You specify the name of the approved resource group.</span><span class="sxs-lookup"><span data-stu-id="b64e3-105">You specify the name of the approved resource group.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="b64e3-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="b64e3-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/compute/custom-image-from-rg/azurepolicy.json "Allow custom VM image from a Resource Group")]


<span data-ttu-id="b64e3-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b64e3-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="b64e3-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="b64e3-108">Deploy with the portal</span></span>

<span data-ttu-id="b64e3-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fcustom-image-from-rg%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="b64e3-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fcustom-image-from-rg%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="b64e3-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="b64e3-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "custom-image-from-rg" -DisplayName "Allow custom VM image from a Resource Group" -description "This policy allows only usage of images from a resource group" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/custom-image-from-rg/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/custom-image-from-rg/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -resourceGroupName <Resource Group Name> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="b64e3-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="b64e3-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="b64e3-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="b64e3-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="b64e3-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b64e3-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'custom-image-from-rg' --display-name 'Allow custom VM image from a Resource Group' --description 'This policy allows only usage of images from a resource group' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/custom-image-from-rg/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/custom-image-from-rg/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "custom-image-from-rg"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="b64e3-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="b64e3-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="b64e3-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="b64e3-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="b64e3-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="b64e3-116">Next steps</span></span>

- <span data-ttu-id="b64e3-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b64e3-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>