---
title: Azure Policy json sample - Require encryption for Data Lake Store | Microsoft Docs
description: This json sample policy requires encryption for Data Lake Store.
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
ms.openlocfilehash: 470adb5f27c8a5318197c100a8f973319d9c5001
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865015"
---
# <a name="require-data-lake-store-encryption"></a>Require Data Lake Store encryption

This built-in policy denies any Data Lake Store accounts that don't have encryption enabled.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a>Sample template

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.DataLakeStore/accounts"
      },
      {
        "field": "Microsoft.DataLakeStore/accounts/encryptionState",
        "equals": "Disabled"
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli). To get the built-in policy, use the ID `a7ff3161-0087-490a-9ad9-ad6217f4f43a`.

## <a name="deploy-with-the-portal"></a>Deploy with the portal

When assigning a policy, select **Enforce encryption on DataLakeStore accounts** from the available built-in definitions.

## <a name="deploy-with-powershell"></a>Deploy with PowerShell

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/a7ff3161-0087-490a-9ad9-ad6217f4f43a

New-AzureRmPolicyAssignment -name "Data Lake Store encryption" -PolicyDefinition $definition -Scope <scope>
```

### <a name="clean-up-powershell-deployment"></a>Clean up PowerShell deployment

Run the following command to remove the policy assignment.

```powershell
Remove-AzureRmPolicyAssignment -Name "Data Lake Store encryption" -Scope <scope>
```

## <a name="deploy-with-azure-cli"></a>Deploy with Azure CLI

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy assignment create --scope <scope> --name "Data Lake Store encryption" --policy a7ff3161-0087-490a-9ad9-ad6217f4f43a
```

### <a name="clean-up-azure-cli-deployment"></a>Clean up Azure CLI deployment

Run the following command to remove the policy assignment.

```azurecli-interactive
az policy assignment delete --name "Data Lake Store encryption" --resource-group myResourceGroup
```

## <a name="next-steps"></a>Next steps

- Review more examples at [Azure Policy samples](../json-samples.md).