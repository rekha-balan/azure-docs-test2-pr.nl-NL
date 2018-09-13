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
# <a name="audit-sql-database-encryption"></a>Audit SQL database encryption

This built-in policy audits if SQL database does not have transparent data encryption enabled.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a>Sample template

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

You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli). To get the built-in policy, use the ID `17k78e20-9358-41c9-923c-fb736d382a12`.

## <a name="deploy-with-the-portal"></a>Deploy with the portal

When assigning a policy, select **Audit transparent data encryption status** from the available built-in definitions.

## <a name="deploy-with-powershell"></a>Deploy with PowerShell

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/17k78e20-9358-41c9-923c-fb736d382a12

New-AzureRmPolicyAssignment -name "SQL TDE Audit" -PolicyDefinition $definition -Scope <scope>
```

### <a name="clean-up-powershell-deployment"></a>Clean up PowerShell deployment

Run the following command to remove the policy assignment.

```powershell
Remove-AzureRmPolicyAssignment -Name "SQL TDE Audit" -Scope <scope>
```

## <a name="deploy-with-azure-cli"></a>Deploy with Azure CLI

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy assignment create --scope <scope> --name "SQL TDE Audit" --policy 17k78e20-9358-41c9-923c-fb736d382a12
```

### <a name="clean-up-azure-cli-deployment"></a>Clean up Azure CLI deployment

Run the following command to remove the policy assignment.

```azurecli-interactive
az policy assignment delete --name "SQL TDE Audit" --resource-group myResourceGroup
```

## <a name="next-steps"></a>Next steps

- Review more examples at [Azure Policy samples](../json-samples.md).