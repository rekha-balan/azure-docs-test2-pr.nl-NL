---
title: Azure Policy json sample - Audit SQL DB level audit Setting | Microsoft Docs
description: This json sample policy audits SQL database audit settings if those settings do not match a specified setting.
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
ms.openlocfilehash: 84c166267fa5acf9e340f36654130c60844c71bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967619"
---
# <a name="audit-sql-db-level-audit-setting"></a><span data-ttu-id="7be0d-103">Audit SQL DB level audit setting</span><span class="sxs-lookup"><span data-stu-id="7be0d-103">Audit SQL DB level audit setting</span></span>

<span data-ttu-id="7be0d-104">This policy audits SQL database audit settings if those settings do not match a specified setting.</span><span class="sxs-lookup"><span data-stu-id="7be0d-104">This policy audits SQL database audit settings if those settings do not match a specified setting.</span></span> <span data-ttu-id="7be0d-105">You specify a value that indicates whether audit settings should be enabled or disabled.</span><span class="sxs-lookup"><span data-stu-id="7be0d-105">You specify a value that indicates whether audit settings should be enabled or disabled.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="7be0d-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="7be0d-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/SQL/audit-sql-db-auditing/azurepolicy.json "Audit SQL DB Level Audit Setting")]

<span data-ttu-id="7be0d-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7be0d-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="7be0d-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="7be0d-108">Deploy with the portal</span></span>

<span data-ttu-id="7be0d-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FSQL%2Faudit-sql-db-auditing%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="7be0d-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FSQL%2Faudit-sql-db-auditing%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="7be0d-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="7be0d-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "audit-sql-db-auditing" -DisplayName "Audit SQL DB Level Audit Setting" -description "Audit DB level audit setting for SQL databases" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/SQL/audit-sql-db-auditing/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/SQL/audit-sql-db-auditing/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -setting <Audit Setting> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="7be0d-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="7be0d-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="7be0d-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="7be0d-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="7be0d-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7be0d-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'audit-sql-db-auditing' --display-name 'Audit SQL DB Level Audit Setting' --description 'Audit DB level audit setting for SQL databases' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/SQL/audit-sql-db-auditing/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/SQL/audit-sql-db-auditing/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "audit-sql-db-auditing"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="7be0d-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="7be0d-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="7be0d-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="7be0d-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="7be0d-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="7be0d-116">Next steps</span></span>

- <span data-ttu-id="7be0d-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7be0d-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>