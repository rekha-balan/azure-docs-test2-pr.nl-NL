---
title: Azure Policy json sample - Audit transparent data encryption status | Microsoft Docs
description: This json sample policy audits SQL database transparent data encryption if it is not enabled.
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
ms.openlocfilehash: 0cbdec2f81c1ad81b0f7f9441b88571454558578
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856947"
---
# <a name="audit-transparent-data-encryption-status"></a><span data-ttu-id="34b03-103">Audit transparent data encryption status</span><span class="sxs-lookup"><span data-stu-id="34b03-103">Audit transparent data encryption status</span></span>

<span data-ttu-id="34b03-104">This policy audits SQL database transparent data encryption if it is not enabled.</span><span class="sxs-lookup"><span data-stu-id="34b03-104">This policy audits SQL database transparent data encryption if it is not enabled.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="34b03-105">Sample template</span><span class="sxs-lookup"><span data-stu-id="34b03-105">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/SQL/audit-sql-db-tde-status/azurepolicy.json "Audit transparent data encryption status")]

<span data-ttu-id="34b03-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="34b03-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="34b03-107">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="34b03-107">Deploy with the portal</span></span>

<span data-ttu-id="34b03-108">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FSQL%2Faudit-sql-db-tde-status%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="34b03-108">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FSQL%2Faudit-sql-db-tde-status%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="34b03-109">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="34b03-109">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "audit-sql-db-tde-status" -DisplayName "Audit transparent data encryption status" -description "Audit transparent data encryption status for SQL databases" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/SQL/audit-sql-db-tde-status/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/SQL/audit-sql-db-tde-status/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="34b03-110">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="34b03-110">Clean up PowerShell deployment</span></span>

<span data-ttu-id="34b03-111">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="34b03-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="34b03-112">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="34b03-112">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'audit-sql-db-tde-status' --display-name 'Audit transparent data encryption status' --description 'Audit transparent data encryption status for SQL databases' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/SQL/audit-sql-db-tde-status/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/SQL/audit-sql-db-tde-status/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "audit-sql-db-tde-status"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="34b03-113">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="34b03-113">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="34b03-114">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="34b03-114">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="34b03-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="34b03-115">Next steps</span></span>

- <span data-ttu-id="34b03-116">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="34b03-116">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>