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
# <a name="require-data-lake-store-encryption"></a><span data-ttu-id="7b8b7-103">Require Data Lake Store encryption</span><span class="sxs-lookup"><span data-stu-id="7b8b7-103">Require Data Lake Store encryption</span></span>

<span data-ttu-id="7b8b7-104">This built-in policy denies any Data Lake Store accounts that don't have encryption enabled.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-104">This built-in policy denies any Data Lake Store accounts that don't have encryption enabled.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="7b8b7-105">Sample template</span><span class="sxs-lookup"><span data-stu-id="7b8b7-105">Sample template</span></span>

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

<span data-ttu-id="7b8b7-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7b8b7-106">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span> <span data-ttu-id="7b8b7-107">To get the built-in policy, use the ID `a7ff3161-0087-490a-9ad9-ad6217f4f43a`.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-107">To get the built-in policy, use the ID `a7ff3161-0087-490a-9ad9-ad6217f4f43a`.</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="7b8b7-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="7b8b7-108">Deploy with the portal</span></span>

<span data-ttu-id="7b8b7-109">When assigning a policy, select **Enforce encryption on DataLakeStore accounts** from the available built-in definitions.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-109">When assigning a policy, select **Enforce encryption on DataLakeStore accounts** from the available built-in definitions.</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="7b8b7-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b8b7-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/a7ff3161-0087-490a-9ad9-ad6217f4f43a

New-AzureRmPolicyAssignment -name "Data Lake Store encryption" -PolicyDefinition $definition -Scope <scope>
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="7b8b7-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="7b8b7-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="7b8b7-112">Run the following command to remove the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-112">Run the following command to remove the policy assignment.</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name "Data Lake Store encryption" -Scope <scope>
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="7b8b7-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b8b7-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy assignment create --scope <scope> --name "Data Lake Store encryption" --policy a7ff3161-0087-490a-9ad9-ad6217f4f43a
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="7b8b7-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="7b8b7-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="7b8b7-115">Run the following command to remove the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="7b8b7-115">Run the following command to remove the policy assignment.</span></span>

```azurecli-interactive
az policy assignment delete --name "Data Lake Store encryption" --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7b8b7-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b8b7-116">Next steps</span></span>

- <span data-ttu-id="7b8b7-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7b8b7-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>