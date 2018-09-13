---
title: Azure Policy json sample - Require SQL Server version 12.0 | Microsoft Docs
description: This json sample policy requires SQL servers to use version 12.0.
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
ms.openlocfilehash: cb0558c5eae79d46cca5cdc4c1b2e5d1996921bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871055"
---
# <a name="require-sql-server-version-120"></a><span data-ttu-id="094e2-103">Require SQL Server version 12.0</span><span class="sxs-lookup"><span data-stu-id="094e2-103">Require SQL Server version 12.0</span></span>

<span data-ttu-id="094e2-104">This policy requires SQL servers to use version 12.0.</span><span class="sxs-lookup"><span data-stu-id="094e2-104">This policy requires SQL servers to use version 12.0.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="094e2-105">Sample template</span><span class="sxs-lookup"><span data-stu-id="094e2-105">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/built-in-policy/require-sqlserver-version12/azurepolicy.json "Require SQL Server version 12.0")]

<span data-ttu-id="094e2-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="094e2-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="094e2-107">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="094e2-107">Deploy with the portal</span></span>

<span data-ttu-id="094e2-108">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Frequire-sqlserver-version12%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="094e2-108">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Frequire-sqlserver-version12%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="094e2-109">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="094e2-109">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "require-sqlserver-version12" -DisplayName "Require SQL Server version 12.0" -description "This policy ensures all SQL servers use version 12.0." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/require-sqlserver-version12/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/require-sqlserver-version12/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="094e2-110">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="094e2-110">Clean up PowerShell deployment</span></span>

<span data-ttu-id="094e2-111">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="094e2-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="094e2-112">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="094e2-112">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'require-sqlserver-version12' --display-name 'Require SQL Server version 12.0' --description 'This policy ensures all SQL servers use version 12.0.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/require-sqlserver-version12/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/require-sqlserver-version12/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "require-sqlserver-version12"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="094e2-113">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="094e2-113">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="094e2-114">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="094e2-114">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="094e2-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="094e2-115">Next steps</span></span>

- <span data-ttu-id="094e2-116">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="094e2-116">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>