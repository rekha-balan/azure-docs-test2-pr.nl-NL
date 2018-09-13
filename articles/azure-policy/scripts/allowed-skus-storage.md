---
title: Azure Policy json sample - Allowed SKUs for storage accounts and virtual machines | Microsoft Docs
description: This json sample policy requires that storage accounts and virtual machines use approved SKUs.
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
ms.openlocfilehash: 56285431a6be7966d23dd71172623282167929cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866118"
---
# <a name="allowed-skus-for-storage-accounts-and-virtual-machines"></a><span data-ttu-id="7ee9a-103">Allowed SKUs for storage accounts and virtual machines</span><span class="sxs-lookup"><span data-stu-id="7ee9a-103">Allowed SKUs for storage accounts and virtual machines</span></span>

<span data-ttu-id="7ee9a-104">This policy requires that storage accounts and virtual machines use approved SKUs.</span><span class="sxs-lookup"><span data-stu-id="7ee9a-104">This policy requires that storage accounts and virtual machines use approved SKUs.</span></span> <span data-ttu-id="7ee9a-105">Uses built-in policies to ensure approved SKUs.</span><span class="sxs-lookup"><span data-stu-id="7ee9a-105">Uses built-in policies to ensure approved SKUs.</span></span> <span data-ttu-id="7ee9a-106">You specify an array of approved virtual machines SKUs, and an array of approved storage account SKUs.</span><span class="sxs-lookup"><span data-stu-id="7ee9a-106">You specify an array of approved virtual machines SKUs, and an array of approved storage account SKUs.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="7ee9a-107">Sample template</span><span class="sxs-lookup"><span data-stu-id="7ee9a-107">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/PolicyInitiatives/skus-for-multiple-types/azurepolicyset.json "Allowed SKUs for Storage Accounts and Virtual Machines")]

<span data-ttu-id="7ee9a-108">You can deploy this template using the [Azure portal](#deploy-with-the-portal) or with [PowerShell](#deploy-with-powershell).</span><span class="sxs-lookup"><span data-stu-id="7ee9a-108">You can deploy this template using the [Azure portal](#deploy-with-the-portal) or with [PowerShell](#deploy-with-powershell).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="7ee9a-109">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="7ee9a-109">Deploy with the portal</span></span>

<span data-ttu-id="7ee9a-110">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://aka.ms/getpolicy)</span><span class="sxs-lookup"><span data-stu-id="7ee9a-110">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://aka.ms/getpolicy)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="7ee9a-111">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ee9a-111">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$policydefinitions = "https://raw.githubusercontent.com/Azure/azure-policy/master/samples/PolicyInitiatives/skus-for-multiple-types/azurepolicyset.definitions.json"
$policysetparameters = "https://raw.githubusercontent.com/Azure/azure-policy/master/samples/PolicyInitiatives/skus-for-multiple-types/azurepolicyset.parameters.json"

$policyset= New-AzureRmPolicySetDefinition -Name "skus-for-multiple-types" -DisplayName "Allowed SKUs for Storage Accounts and Virtual Machines" -Description "This policy allows you to speficy what skus are allowed for storage accounts and virtual machines" -PolicyDefinition $policydefinitions -Parameter $policysetparameters 
 
New-AzureRmPolicyAssignment -PolicySetDefinition $policyset -Name <assignmentName> -Scope <scope>  -LISTOFALLOWEDSKUS_1 <VM SKUs> -LISTOFALLOWEDSKUS_2 <Storage Account SKUs>
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="7ee9a-112">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="7ee9a-112">Clean up PowerShell deployment</span></span>

<span data-ttu-id="7ee9a-113">Run the following command to remove the policy assignment and definition.</span><span class="sxs-lookup"><span data-stu-id="7ee9a-113">Run the following command to remove the policy assignment and definition.</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name <assignmentName>
Remove-AzureRmPolicySetDefinitions -Name "skus-for-multiple-types"
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="7ee9a-114">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7ee9a-114">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy set-definition create --name "skus-for-multiple-types" --display-name "Allowed SKUs for Storage Accounts and Virtual Machines" --description "This policy allows you to speficy what skus are allowed for storage accounts and virtual machines" --definitions "https://raw.githubusercontent.com/Azure/azure-policy/master/samples/PolicyInitiatives/skus-for-multiple-types/azurepolicyset.definitions.json" --params "https://raw.githubusercontent.com/Azure/azure-policy/master/samples/PolicyInitiatives/skus-for-multiple-types/azurepolicyset.parameters.json"

az policy assignment create --name <assignmentName> --scope <scope> --policy-set-definition "skus-for-multiple-types" --params "{ 'LISTOFALLOWEDSKUS_1': { 'value': <VM SKU Array> }, 'LISTOFALLOWEDSKUS_2': { 'value': <Storage Account SKU Array> } }"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="7ee9a-115">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="7ee9a-115">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="7ee9a-116">Run the following command to remove the policy assignment and definition.</span><span class="sxs-lookup"><span data-stu-id="7ee9a-116">Run the following command to remove the policy assignment and definition.</span></span>

```azurecli-interactive
az policy assignment delete --name <assignmentName>
az policy set-definition delete --name "skus-for-multiple-types"
```

## <a name="next-steps"></a><span data-ttu-id="7ee9a-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ee9a-117">Next steps</span></span>

- <span data-ttu-id="7ee9a-118">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7ee9a-118">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>