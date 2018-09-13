---
title: Azure Policy json sample - Allowed locations | Microsoft Docs
description: This json sample policy requires that all resources are deployed to the approved locations.
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
ms.openlocfilehash: 0a0bcb48161a1bfa15cc39742fbc86527fc12e0c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857308"
---
# <a name="allowed-locations"></a><span data-ttu-id="e82cb-103">Allowed locations</span><span class="sxs-lookup"><span data-stu-id="e82cb-103">Allowed locations</span></span>

<span data-ttu-id="e82cb-104">This policy requires that all resources are deployed to the approved locations.</span><span class="sxs-lookup"><span data-stu-id="e82cb-104">This policy requires that all resources are deployed to the approved locations.</span></span> <span data-ttu-id="e82cb-105">You specify an array of approved locations.</span><span class="sxs-lookup"><span data-stu-id="e82cb-105">You specify an array of approved locations.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="e82cb-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="e82cb-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/built-in-policy/allowed-locations/azurepolicy.json "Allowed locations")]

<span data-ttu-id="e82cb-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e82cb-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="e82cb-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="e82cb-108">Deploy with the portal</span></span>

<span data-ttu-id="e82cb-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fallowed-locations%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="e82cb-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2Fbuilt-in-policy%2Fallowed-locations%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="e82cb-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="e82cb-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "allowed-locations" -DisplayName "Allowed locations" -description "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-locations/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-locations/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -listOfAllowedLocations <Allowed locations> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="e82cb-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="e82cb-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="e82cb-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e82cb-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="e82cb-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e82cb-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'allowed-locations' --display-name 'Allowed locations' --description 'This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-locations/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/built-in-policy/allowed-locations/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "allowed-locations"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="e82cb-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="e82cb-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="e82cb-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e82cb-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="e82cb-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="e82cb-116">Next steps</span></span>

- <span data-ttu-id="e82cb-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e82cb-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>