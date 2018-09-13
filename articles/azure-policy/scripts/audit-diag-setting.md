---
title: Azure Policy json sample - Audit diagnostic setting | Microsoft Docs
description: This json sample policy audits if diagnostic settings not enabled for specified resource types.
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
ms.openlocfilehash: b0e2cc82dbb8270dad48f2fc68070299427f81ba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855710"
---
# <a name="audit-diagnostic-setting"></a><span data-ttu-id="deabc-103">Audit diagnostic setting</span><span class="sxs-lookup"><span data-stu-id="deabc-103">Audit diagnostic setting</span></span>

<span data-ttu-id="deabc-104">This built-in policy audits if diagnostic settings are not enabled for specified resource types.</span><span class="sxs-lookup"><span data-stu-id="deabc-104">This built-in policy audits if diagnostic settings are not enabled for specified resource types.</span></span> <span data-ttu-id="deabc-105">You specify an array of resource types to check whether diagnostic settings are enabled.</span><span class="sxs-lookup"><span data-stu-id="deabc-105">You specify an array of resource types to check whether diagnostic settings are enabled.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="deabc-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="deabc-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/Monitoring/audit-diagnostic-setting/azurepolicy.json "Audit diagnostic setting")]

<span data-ttu-id="deabc-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="deabc-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span> <span data-ttu-id="deabc-108">To get the built-in policy, use the ID `7f89b1eb-583c-429a-8828-af049802c1d9`.</span><span class="sxs-lookup"><span data-stu-id="deabc-108">To get the built-in policy, use the ID `7f89b1eb-583c-429a-8828-af049802c1d9`.</span></span>

## <a name="parameters"></a><span data-ttu-id="deabc-109">Parameters</span><span class="sxs-lookup"><span data-stu-id="deabc-109">Parameters</span></span>

<span data-ttu-id="deabc-110">To pass in the parameter value, use the following format:</span><span class="sxs-lookup"><span data-stu-id="deabc-110">To pass in the parameter value, use the following format:</span></span>

```json
{"listOfResourceTypes":{"value":["Microsoft.Cache/Redis","Microsoft.Compute/virtualmachines"]}}
```

## <a name="deploy-with-the-portal"></a><span data-ttu-id="deabc-111">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="deabc-111">Deploy with the portal</span></span>

<span data-ttu-id="deabc-112">When assigning a policy, select **Audit diagnostic setting** from the available built-in definitions.</span><span class="sxs-lookup"><span data-stu-id="deabc-112">When assigning a policy, select **Audit diagnostic setting** from the available built-in definitions.</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="deabc-113">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="deabc-113">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/7f89b1eb-583c-429a-8828-af049802c1d9

New-AzureRmPolicyAssignment -name "Audit diagnostics" -PolicyDefinition $definition -PolicyParameter '{"listOfResourceTypes":{"value":["Microsoft.Cache/Redis","Microsoft.Compute/virtualmachines"]}}' -Scope <scope>
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="deabc-114">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="deabc-114">Clean up PowerShell deployment</span></span>

<span data-ttu-id="deabc-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="deabc-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name "Audit diagnostics" -Scope <scope>
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="deabc-116">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="deabc-116">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy assignment create --scope <scope> --name "Audit diagnostics" --policy 7f89b1eb-583c-429a-8828-af049802c1d9 --params '{"listOfResourceTypes":{"value":["Microsoft.Cache/Redis","Microsoft.Compute/virtualmachines"]}}'
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="deabc-117">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="deabc-117">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="deabc-118">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="deabc-118">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az policy assignment delete --name "Audit diagnostics" --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="deabc-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="deabc-119">Next steps</span></span>

- <span data-ttu-id="deabc-120">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="deabc-120">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>