---
title: Azure Policy json sample - Audit SQL Server audit settings | Microsoft Docs
description: This json sample policy audits SQL server audit settings.
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
ms.date: 04/27/2018
ms.author: dacoulte
ms.custom: mvc
ms.openlocfilehash: c56db0f6972b6a4a829f98e671c44ed891ae0a6e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866167"
---
# <a name="audit-sql-server-audit-settings"></a><span data-ttu-id="7cee5-103">Audit SQL server audit settings</span><span class="sxs-lookup"><span data-stu-id="7cee5-103">Audit SQL server audit settings</span></span>

<span data-ttu-id="7cee5-104">This built-in policy audits SQL server based on whether the audit settings are enabled.</span><span class="sxs-lookup"><span data-stu-id="7cee5-104">This built-in policy audits SQL server based on whether the audit settings are enabled.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="7cee5-105">Sample template</span><span class="sxs-lookup"><span data-stu-id="7cee5-105">Sample template</span></span>

```json
{
  "if": {
    "field": "type",
    "equals": "Microsoft.SQL/servers"
  },
  "then": {
    "effect": "auditIfNotExists",
    "details": {
      "type": "Microsoft.SQL/servers/auditingSettings",
      "name": "default",
      "existenceCondition": {
        "allOf": [
          {
            "field": "Microsoft.Sql/auditingSettings.state",
            "equals": "[parameters('setting')]"
          }
        ]
      }
    }
  }
}
```

<span data-ttu-id="7cee5-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7cee5-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span> <span data-ttu-id="7cee5-107">To get the built-in policy, use the ID `a6fb4358-5bf4-4ad7-ba82-2cd2f41ce5e9`.</span><span class="sxs-lookup"><span data-stu-id="7cee5-107">To get the built-in policy, use the ID `a6fb4358-5bf4-4ad7-ba82-2cd2f41ce5e9`.</span></span>

## <a name="parameters"></a><span data-ttu-id="7cee5-108">Parameters</span><span class="sxs-lookup"><span data-stu-id="7cee5-108">Parameters</span></span>

<span data-ttu-id="7cee5-109">To pass in the parameter value, use the following format:</span><span class="sxs-lookup"><span data-stu-id="7cee5-109">To pass in the parameter value, use the following format:</span></span>

```json
{"setting": {"value":"enabled"}}
```

## <a name="deploy-with-the-portal"></a><span data-ttu-id="7cee5-110">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="7cee5-110">Deploy with the portal</span></span>

<span data-ttu-id="7cee5-111">When assigning a policy, select **Audit SQL Server Level Audit Setting** from the available built-in definitions.</span><span class="sxs-lookup"><span data-stu-id="7cee5-111">When assigning a policy, select **Audit SQL Server Level Audit Setting** from the available built-in definitions.</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="7cee5-112">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cee5-112">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/a6fb4358-5bf4-4ad7-ba82-2cd2f41ce5e9

New-AzureRmPolicyAssignment -name "SQL Audit audit" -PolicyDefinition $definition -PolicyParameter '{"setting": {"value":"enabled"}}' -Scope <scope>
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="7cee5-113">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="7cee5-113">Clean up PowerShell deployment</span></span>

<span data-ttu-id="7cee5-114">Run the following command to remove the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="7cee5-114">Run the following command to remove the policy assignment.</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name "SQL Audit audit" -Scope <scope>
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="7cee5-115">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7cee5-115">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy assignment create --scope <scope> --name "SQL Audit audit" --policy a6fb4358-5bf4-4ad7-ba82-2cd2f41ce5e9 --params '{"setting": {"value":"enabled"}}'
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="7cee5-116">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="7cee5-116">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="7cee5-117">Run the following command to remove the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="7cee5-117">Run the following command to remove the policy assignment.</span></span>

```azurecli-interactive
az policy assignment delete --name "SQL Audit audit" --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7cee5-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="7cee5-118">Next steps</span></span>

- <span data-ttu-id="7cee5-119">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7cee5-119">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>