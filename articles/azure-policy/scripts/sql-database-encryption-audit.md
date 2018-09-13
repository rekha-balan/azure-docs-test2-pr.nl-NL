---
title: Azure Policy json sample - Audit transparent data encryption for SQL Database | Microsoft Docs
description: This json sample policy audits if SQL database does not have transparent data encryption enabled.
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
ms.openlocfilehash: 91759155a828c9da4de7f2190b1d27fd1d312bd6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857641"
---
# <a name="audit-sql-database-encryption"></a><span data-ttu-id="1b54e-103">Audit SQL database encryption</span><span class="sxs-lookup"><span data-stu-id="1b54e-103">Audit SQL database encryption</span></span>

<span data-ttu-id="1b54e-104">This built-in policy audits if SQL database does not have transparent data encryption enabled.</span><span class="sxs-lookup"><span data-stu-id="1b54e-104">This built-in policy audits if SQL database does not have transparent data encryption enabled.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="1b54e-105">Sample template</span><span class="sxs-lookup"><span data-stu-id="1b54e-105">Sample template</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Sql/servers/databases"
      },
      {
        "field": "name",
        "notEquals": "master"
      }
    ]
  },
  "then": {
    "effect": "AuditIfNotExists",
    "details": {
      "type": "Microsoft.Sql/servers/databases/transparentDataEncryption",
      "name": "current",
      "existenceCondition": {
        "allOf": [
          {
            "field": "Microsoft.Sql/transparentDataEncryption.status",
            "equals": "enabled"
          }
        ]
      }
    }
  }
}
```

<span data-ttu-id="1b54e-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1b54e-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span> <span data-ttu-id="1b54e-107">To get the built-in policy, use the ID `17k78e20-9358-41c9-923c-fb736d382a12`.</span><span class="sxs-lookup"><span data-stu-id="1b54e-107">To get the built-in policy, use the ID `17k78e20-9358-41c9-923c-fb736d382a12`.</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="1b54e-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="1b54e-108">Deploy with the portal</span></span>

<span data-ttu-id="1b54e-109">When assigning a policy, select **Audit transparent data encryption status** from the available built-in definitions.</span><span class="sxs-lookup"><span data-stu-id="1b54e-109">When assigning a policy, select **Audit transparent data encryption status** from the available built-in definitions.</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="1b54e-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b54e-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/17k78e20-9358-41c9-923c-fb736d382a12

New-AzureRmPolicyAssignment -name "SQL TDE Audit" -PolicyDefinition $definition -Scope <scope>
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="1b54e-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="1b54e-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="1b54e-112">Run the following command to remove the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="1b54e-112">Run the following command to remove the policy assignment.</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name "SQL TDE Audit" -Scope <scope>
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="1b54e-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1b54e-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy assignment create --scope <scope> --name "SQL TDE Audit" --policy 17k78e20-9358-41c9-923c-fb736d382a12
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="1b54e-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="1b54e-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="1b54e-115">Run the following command to remove the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="1b54e-115">Run the following command to remove the policy assignment.</span></span>

```azurecli-interactive
az policy assignment delete --name "SQL TDE Audit" --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1b54e-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b54e-116">Next steps</span></span>

- <span data-ttu-id="1b54e-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1b54e-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>