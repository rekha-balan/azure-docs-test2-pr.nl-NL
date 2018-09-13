---
title: Azure Policy json sample - Allowed peering location for Express Route | Microsoft Docs
description: This policy requires that Express Routes use specified peering locations.
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
ms.openlocfilehash: ee11b43b261afb7aae3be90d2ccc5220edaaa955
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869109"
---
# <a name="allowed-peering-location-for-express-route"></a><span data-ttu-id="49ea3-103">Allowed peering location for Express Route</span><span class="sxs-lookup"><span data-stu-id="49ea3-103">Allowed peering location for Express Route</span></span>

<span data-ttu-id="49ea3-104">This policy requires that Express Routes use specified peering locations.</span><span class="sxs-lookup"><span data-stu-id="49ea3-104">This policy requires that Express Routes use specified peering locations.</span></span> <span data-ttu-id="49ea3-105">You specify an array of allowed peering locations.</span><span class="sxs-lookup"><span data-stu-id="49ea3-105">You specify an array of allowed peering locations.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="49ea3-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="49ea3-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/Network/express-route-peeringLocation/azurepolicy.json "Allowed Peering Location for Express Route")]

<span data-ttu-id="49ea3-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="49ea3-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="49ea3-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="49ea3-108">Deploy with the portal</span></span>

<span data-ttu-id="49ea3-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fexpress-route-peeringLocation%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="49ea3-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fexpress-route-peeringLocation%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="49ea3-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="49ea3-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "express-route-peeringLocation" -DisplayName "Allowed Peering Location for Express Route" -description "This policy enables you to specify a set of allowed peering location for express route" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-peeringLocation/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-peeringLocation/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -listOfLocations <Allowed Peering Locations> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="49ea3-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="49ea3-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="49ea3-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="49ea3-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="49ea3-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="49ea3-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'express-route-peeringLocation' --display-name 'Allowed Peering Location for Express Route' --description 'This policy enables you to specify a set of allowed peering location for express route' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-peeringLocation/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-peeringLocation/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "express-route-peeringLocation"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="49ea3-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="49ea3-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="49ea3-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="49ea3-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="49ea3-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="49ea3-116">Next steps</span></span>

- <span data-ttu-id="49ea3-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="49ea3-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>