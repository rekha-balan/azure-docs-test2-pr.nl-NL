---
title: Azure Policy json sample - Require storage account encryption | Microsoft Docs
description: This json sample policy requires the storage account to use blob encryption.
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
ms.openlocfilehash: 7693eb73cca33488b4e9bce3b6908428574d7435
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868841"
---
# <a name="require-storage-account-encryption"></a><span data-ttu-id="f674c-103">Require storage account encryption</span><span class="sxs-lookup"><span data-stu-id="f674c-103">Require storage account encryption</span></span>

<span data-ttu-id="f674c-104">This policy requires the storage account to use blob encryption.</span><span class="sxs-lookup"><span data-stu-id="f674c-104">This policy requires the storage account to use blob encryption.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="f674c-105">Sample template</span><span class="sxs-lookup"><span data-stu-id="f674c-105">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/built-in-policy/require-storageaccount-encryption/azurepolicy.json "Require storage account encryption")]

<span data-ttu-id="f674c-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f674c-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="f674c-107">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="f674c-107">Deploy with the portal</span></span>

<span data-ttu-id="f674c-108">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Frequire-storageaccount-encryption%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="f674c-108">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Frequire-storageaccount-encryption%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="f674c-109">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f674c-109">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "require-storageaccount-encryption" -DisplayName "Require storage account encryption" -description "This policy ensures encryption for storage accounts is turned on." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/require-storageaccount-encryption/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/require-storageaccount-encryption/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="f674c-110">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="f674c-110">Clean up PowerShell deployment</span></span>

<span data-ttu-id="f674c-111">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f674c-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="f674c-112">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f674c-112">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'require-storageaccount-encryption' --display-name 'Require storage account encryption' --description 'This policy ensures encryption for storage accounts is turned on.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/require-storageaccount-encryption/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/require-storageaccount-encryption/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "require-storageaccount-encryption"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="f674c-113">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="f674c-113">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="f674c-114">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f674c-114">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="f674c-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="f674c-115">Next steps</span></span>

- <span data-ttu-id="f674c-116">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f674c-116">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>