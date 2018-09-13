---
title: Azure Policy json sample - Billing tags policy initiative | Microsoft Docs
description: This json sample policy set requires specified tag values for cost center and product name.
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
ms.openlocfilehash: e8ec9dd992f2d01145ecd53e65c346e53a093697
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968265"
---
# <a name="billing-tags-policy-initiative"></a><span data-ttu-id="94633-103">Billing tags policy initiative</span><span class="sxs-lookup"><span data-stu-id="94633-103">Billing tags policy initiative</span></span>

<span data-ttu-id="94633-104">This policy set requires specified tag values for cost center and product name.</span><span class="sxs-lookup"><span data-stu-id="94633-104">This policy set requires specified tag values for cost center and product name.</span></span> <span data-ttu-id="94633-105">Uses built-in policies to apply and enforce required tags.</span><span class="sxs-lookup"><span data-stu-id="94633-105">Uses built-in policies to apply and enforce required tags.</span></span> <span data-ttu-id="94633-106">You specify the required values for the tags.</span><span class="sxs-lookup"><span data-stu-id="94633-106">You specify the required values for the tags.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="94633-107">Sample template</span><span class="sxs-lookup"><span data-stu-id="94633-107">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/PolicyInitiatives/multiple-billing-tags/azurepolicyset.json "Billing Tags Policy Initiative")]

<span data-ttu-id="94633-108">You can deploy this template using the [Azure portal](#deploy-with-the-portal) or with  [PowerShell](#deploy-with-powershell).</span><span class="sxs-lookup"><span data-stu-id="94633-108">You can deploy this template using the [Azure portal](#deploy-with-the-portal) or with  [PowerShell](#deploy-with-powershell).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="94633-109">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="94633-109">Deploy with the portal</span></span>

<span data-ttu-id="94633-110">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://aka.ms/getpolicy)</span><span class="sxs-lookup"><span data-stu-id="94633-110">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://aka.ms/getpolicy)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="94633-111">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="94633-111">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$policydefinitions = "https://raw.githubusercontent.com/Azure/azure-policy/master/samples/PolicyInitiatives/multiple-billing-tags/azurepolicyset.definitions.json"
$policysetparameters = "https://raw.githubusercontent.com/Azure/azure-policy/master/samples/PolicyInitiatives/multiple-billing-tags/azurepolicyset.parameters.json"

$policyset= New-AzureRmPolicySetDefinition -Name "multiple-billing-tags" -DisplayName "Billing Tags Policy Initiative" -Description "Specify cost Center tag and product name tag" -PolicyDefinition $policydefinitions -Parameter $policysetparameters

New-AzureRmPolicyAssignment -PolicySetDefinition $policyset -Name <assignmentname> -Scope <scope>  -costCenterValue <required value for Cost Center tag> -productNameValue <required value for product Name tag>
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="94633-112">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="94633-112">Clean up PowerShell deployment</span></span>

<span data-ttu-id="94633-113">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="94633-113">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="apply-tags-to-existing-resources"></a><span data-ttu-id="94633-114">Apply tags to existing resources</span><span class="sxs-lookup"><span data-stu-id="94633-114">Apply tags to existing resources</span></span>

<span data-ttu-id="94633-115">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span><span class="sxs-lookup"><span data-stu-id="94633-115">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span></span> <span data-ttu-id="94633-116">The following script retains any other tags that existed on the resources:</span><span class="sxs-lookup"><span data-stu-id="94633-116">The following script retains any other tags that existed on the resources:</span></span>

```powershell
$resources = Get-AzureRmResource -ResourceGroupName 'ExampleGroup'

foreach ($r in $resources) {
    try {
        Set-AzureRmResource -Tags ($a = if ($r.Tags -eq $NULL) { @{} } else {$r.Tags}) -ResourceId $r.ResourceId -Force -UsePatchSemantics
    }
    catch {
        Write-Host $r.ResourceId + "can't be updated"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="94633-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="94633-117">Next steps</span></span>

- <span data-ttu-id="94633-118">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="94633-118">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>